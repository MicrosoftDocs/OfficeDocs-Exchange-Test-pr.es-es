---
title: 'Límites de tamaño de mensaje: Exchange 2013 Help'
TOCTitle: Límites de tamaño de mensaje
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 49895858
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Límites de tamaño de mensaje

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-08-20_

Se pueden aplicar límites a los mensajes que se mueven por la organización Exchange Server 2013 de Microsoft. Se puede restringir el tamaño total de un mensaje o el tamaño de los componentes de un mensaje, por ejemplo, el encabezado, los datos adjuntos y el número de destinatarios. Se pueden aplicar los límites globalmente para toda la organización de Exchange o para un conector u objeto de usuario concretos.

Al planear los límites de tamaño de los mensajes de la organización de Exchange, tenga en cuenta las siguientes preguntas:

  - ¿Qué límites debo imponer a todos los mensajes entrantes?

  - ¿Qué límites debo imponer a todos los mensajes salientes?

  - ¿Qué es la cuota de buzón de correo para mi organización de Exchange?

  - ¿Qué relación guarda el límite de tamaño elegido para los mensajes con el tamaño de la cuota de buzón?

  - ¿Hay usuarios en la organización de Exchange que deban enviar o recibir mensajes que superen el tamaño permitido indicado?

  - ¿Mi topología de red de Exchange incluye otros sistemas de mensajería o unidades de negocio claramente diferenciadas que posean diferentes límites de tamaño de los mensajes?

En este tema se proporcionan indicaciones que ayudan a resolver estas preguntas.

**Contenido**

Tipos de límites de tamaño de los mensajes

Ámbito de los límites

Orden de preferencia de los límites de tamaño de los mensajes

Mensajes exentos del límite de tamaño

## Tipos de límites de tamaño de los mensajes

A continuación se indican las categorías básicas de los límites de tamaño que pueden aplicarse a los mensajes individuales:

  - **Límites de tamaño de los encabezados de mensaje**   Estos límites se aplican al tamaño total de todos los campos de encabezado de un mensaje. No se tiene en cuenta el tamaño del cuerpo del mensaje ni de los datos adjuntos. Como los campos del encabezado son texto sin formato, el tamaño del encabezado lo determinan el número de caracteres de cada campo y el número total de campos del encabezado. Cada carácter de texto consume 1 byte.
    

    > [!NOTE]
    > Algunos firewalls o servidores de terceros proxy aplican sus propios límites de tamaño en los encabezados de mensaje. Es posible que estos firewalls o servidores proxy de terceros tengan dificultades para procesar mensajes con nombres de datos adjuntos de más de 50 caracteres, o bien con nombres de datos adjuntos que contengan caracteres que no sean US-ASCII.



  - **Límites de tamaño del mensaje**   Estos límites se aplican al tamaño total de un mensaje, que incluye el encabezado el cuerpo del mensaje y cualquier dato adjunto. Los límites de tamaño del mensaje pueden aplicarse a los mensajes entrantes o a los mensajes salientes. Para el flujo de mensajes interno, Exchange usa el encabezamiento de mensaje de `X-MS-Exchange-Organization-OriginalSize:` personalizado para registrar el tamaño original del mensaje al entrar en la organización de Exchange. Siempre que se comprueban los límites de tamaño de los mensajes indicado con respecto al mensaje, se usa el valor más bajo del tamaño del mensaje actual o el encabezado del tamaño del mensaje original. El tamaño del mensaje puede cambiar debido a la conversión del contenido, la codificación y el procesamiento de agentes.

  - **Límites de tamaño de los datos adjuntos**   Estos límites se aplican al tamaño máximo permitido para un solo archivo de datos adjuntos a un mensaje. El mensaje puede contener muchos datos adjuntos que aumenten considerablemente el tamaño total del mensaje. Sin embargo, un límite de tamaño de datos adjuntos solo se aplica al tamaño de los datos adjuntos individuales.

  - **Límites en los destinatarios**   Estos límites se aplican al número total de destinatarios del mensaje. Al redactar por primera vez un mensaje, los destinatarios constan en los campos del encabezamiento `To:`, `Cc:` y `Bcc:`. Cuando se envía el mensaje para entregarlo, los destinatarios pasan a ser entradas de `RCPT TO:` en el sobre del mensaje. Al enviar un mensaje, cada grupo de distribución cuenta como un único destinatario.

Volver al principio

## Ámbito de los límites

A continuación se indican las categorías básicas relativas al ámbito de los límites de tamaño que pueden aplicarse a los mensajes individuales:

  - **Límites organizativos**   Estos límites se aplican a todos los servidores Buzón de correo de Exchange 2013 y Exchange 2010 y los servidores de transporte de concentradores de Exchange 2007 existentes en la organización. Si posee un servidor de transporte perimetral instalado en la red perimetral, los límites especificados se aplican al servidor específico.

  - **Límites del conector**   Estos límites se aplican a cualquier mensaje que use los conectores de envío, recepción, agente de entrega o externo indicados para entregar los mensajes. Los conectores de envío se definen en el servicio de transporte en los servidores Buzón de correo y en los servidores de transporte perimetral. Los conectores de recepción se definen en el servicio de transporte en los servidores Buzón de correo, en el servicio de transporte frontend en los servidores Acceso de cliente y en los servidores de transporte perimetral.

  - **Vínculos al sitio de Active Directory**   El servicio de transporte en los servidores Buzón de correo usan los sitios de Active Directory y los costos que son asignados a los vínculos del sitio IP de Active Directory como uno de los factores que determinan la ruta de enrutamiento de menor costo entre los servidores Buzón de correo en la organización. Se puede asignar límites de tamaño de mensaje específicos a los vínculos del sitio de Active Directory de la organización.

  - **Límites del servidor**   Estos límites se aplican a un servidor Buzón de correo o servidor Transporte perimetral especificado. Se pueden configurar los límites de mensaje especificados por separado en cada servidor Buzón de correo o servidor de transporte perimetral.
    
    En Outlook Web App, la configuración del límite de tamaño máximo de solicitudes HTTP en los servidores Acceso de cliente controla también el tamaño de los mensajes que pueden enviar los usuarios de Outlook Web App.

  - **Límites del usuario**   Estos límites se aplican a un objeto usuario determinado, como un buzón de correo, un contacto, un grupo de distribución o una carpeta pública.

En la tabla siguiente figuran los límites de mensajes, además de información sobre cómo configurar los límites en el Shell de administración de Exchange o el Centro de Administración de Exchange (EAC).

### Límites de la organización

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Límite de tamaño</th>
<th>Valor predeterminado</th>
<th>Configuración del Shell</th>
<th>Configuración del EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamaño máximo para los mensajes recibidos</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parámetro: <em>MaxReceiveSize</em></p></td>
<td><p>Las fichas <strong>Flujo de correo</strong>&gt;<strong>Conectores de recepción</strong>&gt;<strong>Más opciones</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icono Más opciones" alt="Icono Más opciones" />&gt;<strong>Configuración de transporte de la organización</strong>&gt;<strong>Límites</strong>&gt;<strong>Tamaño máximo de mensaje de recepción</strong></p></td>
</tr>
<tr class="even">
<td><p>Tamaño máximo para los mensajes enviados</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parámetro: <em>MaxSendSize</em></p></td>
<td><p>Las fichas <strong>Flujo de correo</strong>&gt;<strong>Conectores de recepción</strong>&gt;<strong>Más opciones</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icono Más opciones" alt="Icono Más opciones" />&gt;<strong>Configuración de transporte de la organización</strong>&gt;<strong>Límites</strong>&gt;<strong>Tamaño máximo de mensaje de envío</strong></p></td>
</tr>
<tr class="odd">
<td><p>Número máximo de destinatarios por mensaje</p>

> [!NOTE]  

</td>
<td><p>5000</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parámetro: <em>MaxRecipientEnvelopeLimit</em></p></td>
<td><p>Las fichas <strong>Flujo de correo</strong>&gt;<strong>Conectores de recepción</strong>&gt;<strong>Más opciones</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icono Más opciones" alt="Icono Más opciones" />&gt;<strong>Configuración de transporte de la organización</strong>&gt;<strong>Límites</strong>&gt;<strong>Número máximo de destinatarios</strong></p></td>
</tr>
<tr class="even">
<td><p>Tamaño máximo de datos adjuntos en reglas de transporte que se aplican en todos los servidores Buzón de correo de la organización</p></td>
<td><p>No configurado</p></td>
<td><p>Cmdlets: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Parámetro: <em>AttachmentSizeOver</em></p></td>
<td><p><strong>Flujo de correo</strong>&gt;<strong>Reglas</strong>&gt;<strong>Agregar</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Agregar icono" alt="Agregar icono" /> o <strong>Editar</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icono Editar" alt="Icono Editar" />.</p>
<p>Use el predicado <strong>Aplicar esta regla si</strong>&gt;<strong>cualquier dato adjunto</strong>&gt;<strong>es mayor que o igual que</strong></p>
<p>Use el predicado <strong>Aplicar esta regla si</strong>&gt;<strong>El tamaño del mensaje</strong>&gt;<strong>es mayor que o igual que</strong></p></td>
</tr>
<tr class="odd">
<td><p>Tamaño máximo del mensaje en reglas de transporte que se aplican en todos los servidores Buzón de correo de la organización</p></td>
<td><p></p></td>
<td><p>Cmdlets: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Parámetro: <em>MessageSizeOver</em></p></td>
<td><p><strong>Flujo de correo</strong>&gt;<strong>Reglas</strong>&gt;<strong>Agregar</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Agregar icono" alt="Agregar icono" /> o <strong>Editar</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icono Editar" alt="Icono Editar" />.</p>
<p>Use el predicado <strong>Aplicar esta regla si</strong>&gt;<strong>El tamaño del mensaje</strong>&gt;<strong>es mayor que o igual que</strong></p></td>
</tr>
</tbody>
</table>


Volver al principio

### Límites de conector

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Límite de tamaño</th>
<th>Valor predeterminado</th>
<th>Configuración del Shell</th>
<th>Configuración del EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamaño máximo de encabezado a través de un conector de recepción</p></td>
<td><p>128 KB</p></td>
<td><p>Cmdlets: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parámetro: <em>MaxHeaderSize</em></p></td>
<td><p>N/D</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Tamaño máximo de mensaje a través de un conector de recepción</p>

> [!NOTE]
> El tamaño real del mensaje puede ser menor debido a la codificación y conversión del contenido del mensaje.


</td>
<td><p><strong>Servicio de transporte en servidores Buzón de correo</strong></p>
<p>35 MB para los conectores predeterminados y de recepción de proxy de cliente</p>
<p><strong>Servicio de transporte front-end en servidores de Acceso de clientes</strong></p>
<p>36 MB para los conectores frontend predeterminados y de recepción front-end de proxy salientes.</p>
<p>35 MB para el conector de recepción front-end de cliente.</p></td>
<td><p>Cmdlets: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parámetro: <em>MaxMessageSize</em></p></td>
<td><p>Ficha <strong>Flujo de correo</strong>&gt;<strong>Conectores de recepción</strong>&gt;<strong>Editar</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icono Editar" alt="Icono Editar" />&gt;<strong>General</strong>&gt;<strong>Tamaño máximo de mensaje de recepción</strong></p></td>
</tr>
<tr class="odd">
<td><p>Número máximo de destinatarios por mensaje a través de un conector de recepción</p></td>
<td><p><strong>Servicio de transporte en servidores Buzón de correo</strong></p>
<p>5.000 para el conector de recepción predeterminado</p>
<p>200 para el conector de recepción proxy de cliente</p>
<p><strong>Servicio de transporte front-end en servidores de Acceso de clientes</strong></p>
<p>200 para los conectores front-end predeterminados, front-end de cliente y de recepción front-end proxy de cliente.</p>

> [!NOTE]
> Si, en el caso de un remitente anónimo, se supera el número de destinatarios, se acepta el mensaje para los 200&nbsp;primeros destinatarios. La mayoría de los servidores de mensajería SMTP detectan que tiene efecto algún límite de destinatarios. El servidor de mensajería SMTP seguirá enviando de nuevo el mensaje en grupos de 200&nbsp;destinatarios hasta que se haya entregado a todos los destinatarios.


</td>
<td><p>Cmdlets: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parámetro: <em>MaxRecipientsPerMessage</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Tamaño máximo de mensaje a través de un conector de envío</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlets: <strong>New-SendConnector</strong>, <strong>Set-SendConnector</strong></p>
<p>Parámetro: <em>MaxMessageSize</em></p></td>
<td><p>Ficha <strong>Flujo de correo</strong>&gt;<strong>Conectores de envío</strong>&gt;<strong>Editar</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icono Editar" alt="Icono Editar" />&gt;<strong>General</strong>&gt;<strong>Tamaño máximo de mensaje de envío</strong></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Tamaño máximo de mensaje a través de un vínculo del sitio de Active Directory</p></td>
<td><p>Ilimitado</p></td>
<td><p>Cmdlet: <strong>Set-AdSiteLink</strong></p>
<p>Parámetro: <em>MaxMessageSize</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Tamaño máximo de mensaje a través de un conector de agente de entrega</p></td>
<td><p>Ilimitado</p></td>
<td><p>Cmdlets: <strong>New-DeliveryAgentConnector</strong>, <strong>Set-DeliveryAgentConnector</strong></p>
<p>Parámetro: <em>MaxMessageSize</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Tamaño máximo de mensaje a través de un conector externo</p></td>
<td><p>Ilimitado</p></td>
<td><p><strong>Cmdlet: Set-ForeignConnector</strong> Parámetro: <em>MaxMessageSize</em></p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


Volver al principio

### Límites de servidor

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Límite de tamaño</th>
<th>Valor predeterminado</th>
<th>Configuración del Shell</th>
<th>Configuración del EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamaño máximo de encabezado para mensajes en el directorio de recogida</p></td>
<td><p>64 KB</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>Parámetro: <em>PickupDirectoryMaxHeaderSize</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Tamaño máximo de destinatarios por mensaje para mensajes en el directorio de recogida</p></td>
<td><p>100</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>Parámetro: <em>PickupDirectoryMaxRecipientsPerMessage</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Límites de tamaño de mensaje máximo específico por cliente para los clientes de Outlook Web App, Exchange ActiveSync y servicios Web Exchange</p></td>
<td><p>Outlook Web App35 MB</p>
<p>Exchange ActiveSync10 MB</p>
<p>Servicios Web Exchange   64 MB</p>

> [!NOTE]
> Estos valores son aproximadamente un 33% superiores al tamaño de mensaje máximo utilizable de la sobrecarga asociada con la codificación Base64.


</td>
<td><p>Estos valores se configuran en el archivo de configuración de la aplicación XML web.config pertinente en los servidores de acceso de cliente. Para obtener más información, vea <a href="configure-client-specific-message-size-limits-exchange-2013-help.md">Configurar límites de tamaño de mensaje específicos del cliente</a>.</p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


Volver al principio

### Límites de usuario

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Límite de tamaño</th>
<th>Valor predeterminado</th>
<th>Configuración del Shell</th>
<th>Configuración del EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamaño máximo de mensaje que puede enviar este destinatario</p></td>
<td><p>Ilimitado</p></td>
<td><p>Cmdlets:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-RemoteMailbox</strong></p>
<p>Parámetro: <em>MaxSendSize</em></p></td>
<td><p>Para buzones de correo:</p>
<p><strong>Destinatarios</strong>&gt;<strong>Buzones de correo</strong>&gt;<strong>Editar</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icono Editar" alt="Icono Editar" />&gt;<strong>Características de buzón</strong>&gt;<strong>Flujo de correo</strong>&gt;<strong>Restricciones en el tamaño del mensaje</strong>&gt;<strong>Ver detalles</strong>&gt;<strong>Mensajes enviados</strong></p>

> [!NOTE]
> Esta opción no puede configurarse mediante el EAC para otros tipos de destinatario.


</td>
</tr>
<tr class="even">
<td><p>Tamaño máximo de mensaje que puede enviarse a este destinatario</p></td>
<td><p>Ilimitado</p>
<p>Para las directivas de aprovisionamiento de buzones de correo del sitios: 36 MB</p></td>
<td><p>Cmdlets:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>New-SiteMailboxProvisioningPolicy</strong></p>
<p><strong>Set-SiteMailboxProvisioningPolicy</strong></p>
<p>Parámetro: <em>MaxReceiveSize</em></p></td>
<td><p>Para buzones de correo:</p>
<p><strong>Destinatarios</strong>&gt;<strong>Buzones de correo</strong>&gt;<strong>Editar</strong><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icono Editar" alt="Icono Editar" />&gt;<strong>Características de buzón</strong>&gt;<strong>Flujo de correo</strong>&gt;<strong>Restricciones en el tamaño del mensaje</strong>&gt;<strong>Ver detalles</strong>&gt;<strong>Mensajes recibidos</strong></p>

> [!NOTE]
> Esta opción no puede configurarse mediante el EAC para otros tipos de destinatario.


</td>
</tr>
<tr class="odd">
<td><p>Número máximo de destinatarios por mensaje enviado por este destinatario</p></td>
<td><p>Ilimitado</p></td>
<td><p>Cmdlets:</p>
<p><strong>Set-Mailbox</strong>, <strong>Set-MailUser</strong></p>
<p>Parámetro: <em>RecipientLimits</em></p>
<p></p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Orden de preferencia de los límites de tamaño de los mensajes

Los límites de tamaño de los mensajes pueden establecerse en diferentes niveles en la organización de Exchange. Cuando un mensaje se enruta a través de la infraestructura de transporte, podría quedar sujeto a diferentes restricciones de tamaño de mensaje. Es conveniente planear las restricciones de tamaño de los mensajes de manera que contribuya a garantizar que los mensajes del circuito de transporte se rechacen lo antes posible si infringen los límites de tamaño de los mensajes. En líneas generales, resulta recomendable establecer límites más restrictivos en los puntos en que los mensajes entran en la infraestructura. Por ejemplo, cualquier restricción en el tamaño de los mensajes en los conectores de recepción que reciban mensajes por Internet debe tener una restricción en el tamaño de mensajes igual o inferior a la configurada para la organización interna de Exchange. Aceptar y procesar un mensaje procedente de Internet que terminará rechazado por los servidores de transporte en los servidores de Buzón de correo sería malgastar los recursos del sistema del servidor Exchange. Compruebe que los límites de los conectores, los servidores y la organización estén configurados de manera que se minimice el procesamiento innecesario de mensajes.

En este sentido, los límites de usuario son una excepción. Los límites relativos a los usuarios tienen prioridad sobre otras restricciones de tamaño de mensaje. Por lo tanto, puede configurar un usuario para que sobrepase los límites predeterminados de tamaño de mensaje de la organización. Por ejemplo, puede permitir que un determinado grupo de buzones de correo de usuario envíe mensajes de tamaño superior al del resto de la organización; para ello, debe configurar unos límites de envío y recepción personalizados para dichos buzones de correo.

Las excepciones en los límites de usuario solamente se aplican a los intercambios de mensajes efectuados entre usuarios autenticados. Si se envía un mensaje a un destinatario o un destinatario recibe un mensaje en Internet, se aplican los límites de la organización. Por ejemplo, supongamos que en su organización el tamaño de los mensajes está restringido a 10 MB, pero los usuarios del departamento de marketing tienen una configuración que les permite enviar y recibir mensajes de un tamaño máximo de 50 MB. Estos usuarios podrán intercambiar mensajes de gran volumen entre sí, aunque no podrán recibir mensajes de gran tamaño de usuarios de Internet, ya que dichos mensajes provienen de remitentes no autenticados.

Volver al principio

## Mensajes exentos del límite de tamaño

En la siguiente lista se muestran los tipos de mensajes generados por un servidor Buzón de correo o un servidor de transporte perimetral, exentos de todos los límites de tamaño de los mensajes:

  - Mensajes del sistema

  - Mensaje generado por un agente

  - Mensajes de notificación del estado de entrega (DSN)

  - Mensajes del informe del diario

  - Mensajes en cuarentena

Sin embargo, estos mensajes siguen teniendo en cuenta el valor de la organización sobre el máximo número de destinatarios que puede haber en un mensaje.

Volver al principio

