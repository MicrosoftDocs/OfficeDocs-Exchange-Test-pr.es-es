---
title: 'Firewall de encabezado: Exchange 2013 Help'
TOCTitle: Firewall de encabezado
ms:assetid: 9b148f7b-47a9-4379-a55b-8d5310c1772f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232136(v=EXCHG.150)
ms:contentKeyID: 52062051
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- firewall de encabezado, encabezados X del bosque
- firewall de encabezado, permisos de firewall del encabezado
- firewall de encabezado, encabezados X de la organización
- firewall de encabezado, encabezados de enrutamiento
- firewall de encabezado, arquitectura de transporte
- firewall de encabezado, encabezados X
ms.translationtype: HT
---

# Firewall de encabezado

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

En Microsoft Exchange Server 2013, el *firewall de encabezado* es un mecanismo que quita campos de encabezado específicos de los mensajes entrantes y salientes. Hay dos tipos diferentes de campos de encabezado que resultan afectados por el firewall de encabezado:

  - **Encabezados X**   Un *encabezado X* es un campo de encabezado no oficial definido por el usuario. Los encabezados X no se mencionan específicamente en RFC 2822, pero el uso de un campo de encabezado no definido que empieza con **X-** se ha convertido en un modo aceptado de agregar campos de encabezados no oficiales a un mensaje. Las aplicaciones de mensajería, como las aplicaciones contra correo electrónico no deseado, antivirus y los servidores de mensajería pueden agregar sus propios encabezados X a un mensaje. En Exchange, los campos de encabezado X contienen detalles acerca de las acciones que el servicio de transporte efectúa en el mensaje, como el nivel de confianza contra correo no deseado (SCL), los resultados de filtrado de contenido y el estado del procesamiento de las reglas. Desvelar esta información a fuentes no autorizadas podría suponer un riesgo para la seguridad.

  - **Encabezados de enrutamiento**   Los encabezados de enrutamiento son campos con encabezado SMTP estándar que están definidos en RFC 2821 y RFC 2822. Los encabezados de enrutamiento marcan un mensaje con información acerca de los diversos servidores de mensajería utilizados para entregar el mensaje al destinatario. Los encabezados de enrutamiento que los usuarios malintencionados insertan en los mensajes se pueden usar para mostrar equivocadamente la ruta de enrutamiento que ha seguido el mensaje para llegar al destinatario.

El firewall de encabezado impide la suplantación de estos encabezados X relacionados con Exchange, ya que los quita de los mensajes que entran en la organización de Exchange y provienen de orígenes que no son de confianza. El firewall de encabezado impide la divulgación de estos encabezados X relacionados con Exchange, ya que los quita de los mensajes salientes de la organización de Exchange enviados a destinos que no son de confianza fuera de la organización de Exchange. El firewall de encabezado también evita la suplantación de encabezados de enrutamiento estándar que se usan para hacer un seguimiento del historial de ruta de un mensaje.

**Contenido**

Campos de encabezado de mensaje afectados por el firewall de encabezado en Exchange

Cómo se aplica el firewall de encabezado a los conectores de recepción y a los conectores de envío

Firewall de encabezado de los mensajes entrantes en los conectores de recepción

El firewall de encabezado de los mensajes salientes en los conectores de envío

Firewall de encabezado para otros orígenes del mensaje

Encabezados X de organización y los encabezados X de bosque en Exchange

## Campos de encabezado de mensaje afectados por el firewall de encabezado en Exchange

Los siguientes tipos de encabezados X y encabezados de enrutamiento resultan afectados por el firewall de encabezado:

  - **Encabezados X de organización**   Estos campos de encabezados X empiezan por **X-MS-Exchange-Organization-**.

  - **Encabezados X de bosque**   Estos campos de encabezados X empiezan por **X-MS-Exchange-Forest-**.
    
    Para obtener ejemplos de encabezados X de organización y de encabezados X de bosque, consulte la sección Encabezados X de organización y los encabezados X de bosque en Exchange al final de este tema.

  - **Recibido: encabezados de enrutamiento**   Cada servidor de mensajería que ha aceptado y reenviado el mensaje al destinatario agrega otra instancia de este campo de encabezado al encabezado del mensaje. El encabezado **Received:** normalmente incluye el nombre del servidor de mensajería y una marca de tiempo con la fecha.

  - **Reenvío-\*: encabezados de enrutamiento**   Los campos de encabezado de reenvío son de tipo informativo y se pueden usar para determinar si un usuario ha reenviado un mensaje. Están disponibles los siguientes campos de encabezado de reenvío: **Resent-Date:**, **Resent-From:**, **Resent-Sender:**, **Resent-To:**, **Resent-Cc:**, **Resent-Bcc:** y **Resent-Message-ID:**. Los campos de **Resent-** se usan para que el mensaje se muestre al destinatario como si el remitente original lo hubiese enviado directamente. El destinatario puede ver el encabezado del mensaje para saber quién ha reenviado el mensaje.

Exchange usa dos formas diferentes de aplicar los encabezados X, los encabezados X de bosque y los encabezados de enrutamiento que existen en los mensajes:

  - Los permisos se asignan a los conectores de envío o a los conectores de recepción que se pueden usar para conservar o eliminar tipos concretos de encabezados en mensajes cuando el mensaje viaja a través del conector.

  - El firewall de encabezado se implementa automáticamente para tipos concretos de encabezados en los mensajes durante otros tipos de envío de mensajes.

Volver al principio

## Cómo se aplica el firewall de encabezado a los conectores de recepción y a los conectores de envío

El firewall de encabezado se aplica a los mensajes que viajan a través de los conectores de envío y de los conectores de recepción basados en permisos específicos que se asignan a los conectores.

Si el premiso se asigna al conector de recepción o al conector de envío, el firewall de encabezado no se aplica a los mensajes que viajan a través del conector. Los campos de encabezado afectados se conservan en los mensajes.

Si el premiso no se asigna al conector de recepción o al conector de envío, el firewall de encabezado se aplica a los mensajes que viajan a través del conector. Los campos de encabezado afectados se eliminan de los mensajes.

La siguiente tabla describe los permisos de los conectores de envío y de los conectores de recepción que se usan para aplicar el firewall de encabezado y los campos de encabezado afectados.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de conector</th>
<th>Permiso</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Conector de recepción</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong></p></td>
<td><p>El permiso afecta a los campos de encabezados X de organización que empiezan por <strong>X-MS-Exchange-Organization-</strong> en los mensajes entrantes.</p></td>
</tr>
<tr class="even">
<td><p>Conector de recepción</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><p>El permiso afecta a los campos de encabezados X de bosque que empiezan por <strong>X-MS-Exchange-Forest-</strong> en los mensajes entrantes.</p></td>
</tr>
<tr class="odd">
<td><p>Conector de recepción</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Este permiso afecta a los campos de encabezado de enrutamiento <strong>Received:</strong> y <strong>Resent-*:</strong> en los mensajes entrantes.</p></td>
</tr>
<tr class="even">
<td><p>Conector de envío</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong></p></td>
<td><p>El permiso afecta a los campos de encabezados X de organización que empiezan por <strong>X-MS-Exchange-Organization-</strong> en los mensajes salientes.</p></td>
</tr>
<tr class="odd">
<td><p>Conector de envío</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><p>El permiso afecta a los campos de encabezados X de bosque que empiezan por <strong>X-MS-Exchange-Forest-</strong> en los mensajes salientes.</p></td>
</tr>
<tr class="even">
<td><p>Conector de envío</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Este permiso afecta a los campos de encabezado de enrutamiento <strong>Received:</strong> y <strong>Resent-*:</strong> en los mensajes salientes.</p></td>
</tr>
</tbody>
</table>


## Firewall de encabezado de los mensajes entrantes en los conectores de recepción

La siguiente tabla describe la aplicación predeterminada de los permisos del firewall de encabezado en los conectores de recepción.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Permiso</th>
<th>Las entidades de seguridad predeterminadas de Exchange que tienen asignado el permiso</th>
<th>Grupo de permisos que tiene como miembros las entidades de seguridad</th>
<th>El tipo de uso predeterminado que asigna los grupos de permisos al conector de recepción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong> y <strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Servidores de transporte de concentradores</p></li>
<li><p>Servidores de transporte perimetral</p></li>
<li><p>Servidores de Exchange</p>

> [!NOTE]
> únicamente en servidores de transporte de concentradores


</li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Cuenta de usuario anónima</p></td>
<td><p><strong>Anonymous</strong></p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Cuentas de usuario autenticadas</p></td>
<td><p><strong>ExchangeUsers</strong></p></td>
<td><p><code>Client</code> (no disponible en servidores de transporte perimetral)</p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Servidores de transporte de concentradores</p></li>
<li><p>Servidores de transporte perimetral</p></li>
<li><p>Servidores de Exchange</p>

> [!NOTE]
> Servidores de transporte de concentradores únicamente


</li>
<li><p>Servidores de seguridad externa</p></li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Cuenta de servidor asociado</p></td>
<td><p><strong>Partner</strong></p></td>
<td><p><code>Internet</code> y <code>Partner</code></p></td>
</tr>
</tbody>
</table>


Volver al principio

## Firewall de encabezado en los conectores de recepción personalizados

Si desea aplicar el firewall de encabezado a los mensajes en un escenario en el que haya un conector de recepción personalizado, use uno de los métodos siguientes:

  - Cree el conector de recepción con un tipo de uso que aplique automáticamente el firewall de encabezado a los mensajes. Tenga en cuenta que puede establecer el tipo de uso al crear el conector de recepción.
    
      - Para quitar los encabezados X de organización o los encabezados X de bosque de los mensajes, cree un conector de recepción y seleccione un tipo de uso distinto a `Internal`.
    
      - Para quitar los encabezados de enrutamiento de los mensajes, realice una de las siguientes acciones:
        
          - Cree un conector de recepción y seleccione el tipo de uso `Custom`. No asigne ningún grupo de permisos al conector de recepción.
        
          - Modifique un conector de recepción existente y establezca el parámetro *PermissionGroups* en el valor `None`.
        
        Tenga en cuenta que si tiene un conector de recepción sin grupos de permisos asignados, deberá agregar entidades de seguridad al conector de recepción como se describe en el último paso.

  - Use el cmdlet **Remove-ADPermission** para quitar el permiso **Ms-Exch-Accept-Headers-Organization**, el permiso **Ms-Exch-Accept-Headers-Forest** y el permiso **Ms-Exch-Accept-Headers-Routing** de una entidad de seguridad configurada en el conector de recepción. Este método no funciona si el permiso se ha asignado a la entidad de seguridad que usa un grupo de permisos en el conector de recepción, ya que no puede modificar las asignaciones de permisos ni la pertenencia al grupo de un grupo de permisos.

  - Use el cmdlet **Add-ADPermission** para agregar las entidades de seguridad adecuadas necesarias para el flujo de correo del conector de recepción. Asegúrese de que ninguna entidad de seguridad tenga el permiso **Ms-Exch-Accept-Headers-Organization**, el permiso **Ms-Exch-Accept-Headers-Forest** y el permiso **Ms-Exch-Accept-Headers-Routing** asignado a la misma. Si es necesario, use el cmdlet **Add-ADPermission** para denegar el permiso **Ms-Exch-Accept-Headers-Organization**, el permiso **Ms-Exch-Accept-Headers-Forest** y el permiso **Ms-Exch-Accept-Headers-Routing** a las entidades de seguridad configuradas en el conector de recepción.

Para obtener más información al respecto, consulte los temas siguientes:

  - [Conectores de recepción](receive-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/es-es/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/es-es/library/aa996048\(v=exchg.150\))

Volver al principio

## El firewall de encabezado de los mensajes salientes en los conectores de envío

La siguiente tabla describe la aplicación predeterminada de los permisos del firewall de encabezado en los conectores de envío.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Permiso</th>
<th>Las entidades de seguridad predeterminadas de Exchange que tienen asignado el permiso</th>
<th>El tipo de uso predeterminado que asigna las entidades de seguridad al conector de envío</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong> y <strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Servidores de transporte de concentradores</p></li>
<li><p>Servidores de transporte perimetral</p></li>
<li><p>Servidores de Exchange</p>

> [!NOTE]
> únicamente en servidores de transporte de concentradores


</li>
<li><p>Servidores de seguridad externa</p></li>
<li><p>Grupo de seguridad universal <strong>ExchangeLegacyInterop</strong></p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Servidores de transporte de concentradores</p></li>
<li><p>Servidores de transporte perimetral</p></li>
<li><p>Servidores de Exchange</p>

> [!NOTE]
> únicamente en servidores de transporte de concentradores


</li>
<li><p>Servidores de seguridad externa</p></li>
<li><p>Grupo de seguridad universal <strong>ExchangeLegacyInterop</strong></p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Cuenta de usuario anónima</p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Servidores asociados</p></td>
<td><p><code>Partner</code></p></td>
</tr>
</tbody>
</table>


Volver al principio

## Firewall de encabezado en los conectores de envío personalizados

Si desea aplicar el firewall de encabezado a los mensajes en un escenario en el que haya un conector de envío personalizado, use uno de los métodos siguientes:

  - Cree el conector de envío con un tipo de uso que aplique automáticamente el firewall de encabezado a los mensajes. Tenga en cuenta que puede establecer el tipo de uso al crear el conector de envío.
    
      - Para quitar los encabezados X de organización o los encabezados X de bosque de los mensajes, cree un conector de envío y seleccione un tipo de uso distinto a `Internal` o `Partner`.
    
      - Para quitar los encabezados de enrutamiento de los mensajes, cree un conector de envío y seleccione el tipo de uso `Custom`. El permiso **Ms-Exch-Send-Headers-Routing** se asigna a todos los tipos de uso de los conectores de envío salvo a `Custom`.

  - Quite una entidad de seguridad que se asigne al permiso **Ms-Exch-Send-Headers-Organization**, al permiso **Ms-Exch-Send-Headers-Forest** y al permiso **Ms-Exch-Send-Headers-Routing** del conector.

  - Use el cmdlet **Remove-ADPermission** para quitar el permiso **Ms-Exch-Send-Headers-Organization**, el permiso **Ms-Exch-Send-Headers-Forest** y el permiso **Ms-Exch-Send-Headers-Routing** de una de las entidades de seguridad configurada en el conector de envío.

  - Use el cmdlet **Add-ADPermission** para denegar el permiso **Ms-Exch-Send-Headers-Organization**, el permiso **Ms-Exch-Send-Headers-Forest** y el permiso **Ms-Exch-Send-Headers-Routing** a una de las entidades de seguridad configuradas en el conector de envío.

Para obtener más información al respecto, consulte los temas siguientes:

  - [Conectores de envío](send-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/es-es/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/es-es/library/aa996048\(v=exchg.150\))

Volver al principio

## Firewall de encabezado para otros orígenes del mensaje

Los mensajes pueden entrar en la canalización de transporte en un servidor de buzones de correo o en un servidor de transporte perimetral sin usar los conectores de envío ni los de recepción. El firewall de encabezado se aplica a este otro tipo de origen del mensaje como se describe en la siguiente lista:

  - **Directorio de recogida y de reproducción**   Los administradores o las aplicaciones usan el directorio de reproducción para enviar archivos de mensaje. El directorio de reproducción se usa para volver a enviar los mensajes que no se han exportado desde las colas de mensajes de Exchange. Para obtener más información acerca del directorio de recogida y de reproducción consulte [Directorio de recogida y directorio de reproducción](pickup-directory-and-replay-directory-exchange-2013-help.md).
    
    Los encabezados X de organización, los encabezados X de bosque y los encabezados de enrutamiento se quitan de los archivos de mensajes en el directorio de recogida.
    
    Los encabezados de enrutamiento se conservan en los mensajes enviados por el directorio de reproducción.
    
    El hecho de que los encabezados X de organización y los encabezados X de bosque se conserven o se quitan de los mensajes en el directorio de reproducción, se controla desde el campo de encabezado **X-CreatedBy:** en el archivo del mensaje:
    
      - Si el valor de **X-CreatedBy:** es `MSExchange15`, los encabezados X de organización y los encabezados X de bosque se conservan en los mensajes.
    
      - Si el valor de **X-CreatedBy:** no es `MSExchange15`, los encabezados X de organización y los encabezados X de bosque se quitan de los mensajes.
    
      - Si el campo de encabezado **X-CreatedBy:** no existe en el archivo del mensaje, los encabezados X de organización y los encabezados X de bosque se quitan de los mensajes.

  - **Directorio de entrega**   Los conectores externos de los servidores de buzones de correo usan el directorio de entrega para enviar mensajes a servidores de mensajería que no usan SMTP para transferir mensajes. Para obtener más información acerca de los conectores externos, consulte [Conectores externos](foreign-connectors-exchange-2013-help.md).
    
    Los encabezados X de organización y los encabezados X de bosque se quitan de los archivos de mensajes antes de ponerlos en el directorio de entrega.
    
    Los encabezados de enrutamiento se conservan en los mensajes enviados por el directorio de entrega.

  - **Transporte de buzón de correo**   El servicio de transporte de buzón de correo existe en los servidores de buzones de correo para transmitir mensajes desde y a los buzones en los servidores de buzones de correo. Para obtener más información acerca del servicio de transporte de buzón de correo, consulte [Flujo de correo](mail-flow-exchange-2013-help.md).
    
    Los encabezados X de organización, los encabezados X de bosque y los encabezados de enrutamiento se quitan de los mensajes salientes que el servicio de envío de transporte de buzones de correo envía desde los buzones de correo.
    
    El servicio de entrega de transporte de buzones de correo conserva los encabezados de enrutamiento de los mensajes entrantes de los destinatarios de buzón. El servicio de entrega de transporte de buzones de correo conserva los siguientes encabezados X de organización de los mensajes entrantes de los destinatarios de buzón:
    
      - **X-MS-Exchange-Organization-SCL**
    
      - **X-MS-Exchange-Organization-AuthDomain**
    
      - **X-MS-Exchange-Organization-AuthMechanism**
    
      - **X-MS-Exchange-Organization-AuthSource**
    
      - **X-MS-Exchange-Organization-AuthAs**
    
      - **X-MS-Exchange-Organization-OriginalArrivalTime**
    
      - **X-MS-Exchange-Organization-OriginalSize**

  - **Mensajes DSN**   Los encabezados X de organización, los encabezados X de bosque y los encabezados de enrutamiento se quitan del mensaje original y del encabezado del mensaje original no adjunto al mensaje DSN. Para obtener más información acerca de los mensajes DSN, consulte [DSN y NDR en Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

  - **Envío del agente de transporte**   Los encabezados X de organización, los encabezados X de bosque y los encabezados de enrutamiento se conservan en los mensajes que envían los agentes de transporte.

Volver al principio

## Encabezados X de organización y los encabezados X de bosque en Exchange

El servicio de transporte o los servidores de transporte perimetral insertan campos de encabezado X personalizados en el encabezado del mensaje.

Los encabezados X de organización comienzan con **X-MS-Exchange-Organization-**. Los encabezados X de bosque comienzan con **X-MS-Exchange-Forest-**. En la tabla siguiente se describen algunos encabezados X de organización y encabezados X de bosque que se usan en los mensajes de una organización de Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>encabezado X</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Forest-RulesExecuted</strong></p></td>
<td><p>Reglas de transporte que actuaron en el mensaje.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-Antispam-Report</strong></p></td>
<td><p>Un resumen de los resultados del filtro contra correo electrónico no deseado que el agente de filtro de contenido ha aplicado al mensaje.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthAs</strong></p></td>
<td><p>Especifica el origen de autenticación. Este encabezado X siempre está presente cuando se ha evaluado la seguridad de un mensaje. Los valores posibles son <code>Anonymous</code>, <code>Internal</code>, <code>External</code> o <code>Partner</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthDomain</strong></p></td>
<td><p>Rellenado durante la autenticación de seguros de dominio. El valor es el FQDN del dominio remoto autenticado.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthMechanism</strong></p></td>
<td><p>Especifica el mecanismo de autenticación para enviar el mensaje. El valor es un número hexadecimal de 2 dígitos.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthSource</strong></p></td>
<td><p>Especifica el FQDN del equipo del servidor que ha evaluado la autenticación del mensaje en nombre de la organización.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Journal-Report</strong></p></td>
<td><p>Identifica informes de diario en el transporte. Tan pronto como el mensaje deja el servicio de transporte, el encabezado se convierte en <strong>X-MS-Journal-Report</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalArrivalTime</strong></p></td>
<td><p>Identifica el momento en que el mensaje entró por primera vez en la organización de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Sender</strong></p></td>
<td><p>Identifica el remitente original de un mensaje en cuarentena cuando entró por primera vez en la organización de Exchange.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalSize</strong></p></td>
<td><p>Identifica el tamaño original de un mensaje en cuarentena cuando entró por primera vez en la organización de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Scl</strong></p></td>
<td><p>Identifica el SCL original de un mensaje en cuarentena cuando entró por primera vez en la organización de Exchange.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-PCL</strong></p></td>
<td><p>Identifica el nivel de confianza de suplantación de identidad (phishing). Los posibles valores de nivel de confianza de protección contra suplantación de identidad (phishing) oscilan entre 1 y 8. Un valor superior indica que se trata de un mensaje sospechoso. Para obtener más información, consulte <a href="anti-spam-stamps-exchange-2013-help.md">Marcas de correo no deseado</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Quarantine</strong></p></td>
<td><p>Indica el mensaje que se ha puesto en cuarentena en el buzón de cuarentena de correo electrónico no deseado y que se ha enviado una notificación del estado de entrega (DSN). De manera alternativa, indica que el administrador ha puesto en cuarentena y ha liberado el mensaje. Este campo de encabezado X evita que el mensaje liberado se vuelva a enviar al buzón de cuarentena de correo electrónico no deseado. Para obtener más información, consulte <a href="release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md">Recuperar mensajes en cuarentena del buzón de cuarentena de correo no deseado</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-SCL</strong></p></td>
<td><p>Identifica el SCL del mensaje. Los posibles valores de SCL oscilan entre 0 y 9. Un valor superior indica que se trata de un mensaje sospechoso. El valor especial -1 exime al mensaje del procesamiento que efectúa el agente de filtro de contenido. Para obtener más información, consulte <a href="content-filtering-exchange-2013-help.md">Filtrado de contenido</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-SenderIdResult</strong></p></td>
<td><p>Contiene los resultados del agente del Id. de remitente El agente del Id. de remitente usa el marco de directivas de remitente (SPF) para comparar la dirección IP de origen del mensaje con el dominio que se usa en la dirección de correo electrónico del remitente. Los resultados del Id. del remitente se usan para calcular el SCL de un mensaje. Para obtener más información, consulte <a href="sender-id-exchange-2013-help.md">Id. del remitente</a>.</p></td>
</tr>
</tbody>
</table>


Volver al principio

