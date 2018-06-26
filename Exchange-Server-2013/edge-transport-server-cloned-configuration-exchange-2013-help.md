---
title: 'Configuración clonada del servidor de transporte perimetral: Exchange 2013 Help'
TOCTitle: Configuración clonada del servidor de transporte perimetral
ms:assetid: 683a6b8a-59bf-43ed-96c8-504945c2f665
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998622(v=EXCHG.150)
ms:contentKeyID: 61183327
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración clonada del servidor de transporte perimetral

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Los servidores de transporte perimetral almacenan su información de configuración en Active Directory Lightweight Directory Services (AD LDS). Puede instalar más de un servidor de transporte perimetral en la red perimetral y usar un round robin de DNS para ayudar a equilibrar el tráfico de red entre los servidores de transporte perimetral. Round robin es un sencillo mecanismo usado por los servidores DNS para compartir y distribuir cargas de los recursos de red.

Para asegurarse de que todos los servidores de transporte perimetral usan la misma información de configuración, use los scripts de configuración clonada proporcionados para duplicar la configuración de su servidor de origen en un servidor de destino.

La *configuración clonada* se usa para implementar servidores de transporte perimetral nuevos basados en un servidor de origen configurado. La información de configuración del servidor de origen se duplica y después, se exporta a un archivo XML. A continuación, el archivo XML se importa al servidor de destino.

En este tema, se proporciona información general sobre el proceso de configuración clonada. Para obtener instrucciones detalladas acerca de cómo configurar los servidores de transporte perimetral por medio de la configuración clonada, vea [Configurar el servidor de transporte perimetral mediante una configuración clonada](configure-edge-transport-server-using-cloned-configuration-exchange-2013-help.md).

**Contenido**

Configuración clonada y EdgeSync

Proceso de configuración clonada

Información de configuración de transporte

## Configuración clonada y EdgeSync

Después de importar la configuración clonada, ejecute el proceso EdgeSync. Para llevar a cabo la búsqueda de destinatarios y las tareas de seguridad de los mensajes, el servidor de transporte perimetral requiere los datos que residen en Active Directory. *EdgeSync* es una colección de procesos que se ejecutan en un servidor de buzones de correo de Exchange 2013 para establecer una replicación unidireccional de la información de configuración y destinatarios desde Active Directory a la instancia de AD LDS en un servidor de transporte perimetral. EdgeSync solo copia la información necesaria para que el servidor de transporte de bordes realice tareas contra correos electrónicos no deseados, así como la información acerca de la configuración del conector necesaria para permitir un flujo completo de correos. EdgeSync realiza actualizaciones programadas de manera que la información de AD LDS se mantiene actualizada.

Una configuración clonada no hace que se duplique la configuración de suscripción perimetral de un servidor. Los certificados utilizados por EdgeSync no se clonan. Debe ejecutar el proceso de EdgeSync en cada servidor de transporte perimetral por separado. EdgeSync sobrescribe la configuración que se incluye tanto en la información de la configuración clonada como en la información de replicación de EdgeSync. Estas configuraciones incluyen conectores de envío, conectores de recepción, dominios aceptados y dominios remotos.

## Proceso de configuración clonada

El proceso de configuración clonada consta de tres pasos:

1.  Exportación de la configuración del servidor de origen.
    
    Ejecute el script ExportEdgeConfig.ps1 (ubicado en %ExchangeInstallPath%Scripts) para exportar la información de configuración del servidor de origen a un archivo XML intermedio.

2.  Validación de la configuración en el servidor de destino.
    
    Ejecute el script ImportEdgeConfig.ps1 (ubicado en %ExchangeInstallPath%Scripts). Este script comprueba la información existente en el archivo XML intermedio a fin de verificar si la configuración exportada es válida para el servidor de destino y luego crea un archivo de respuesta. El archivo de respuesta contiene la información específica de servidor que se usó al importar la configuración al servidor de destino. El archivo de respuesta contiene entradas para todas las configuraciones del servidor de origen que no sean válidas para el servidor de destino. Puede modificar estas configuraciones de modo que sean válidas para el servidor de destino. Si todas las configuraciones son válidas, el archivo de respuesta no contendrá ninguna entrada.

3.  Importación de la configuración en el servidor de destino.
    
    El script ImportEdgeConfig.ps1 usa el archivo XML intermedio y el archivo de respuesta para clonar una configuración existente o restaurar el servidor a una configuración específica.

## Paso 1: Exportación de la configuración del servidor de origen.

Después de instalar y configurar el rol de servidor Transporte perimetral, ejecute el script ExportEdgeConfig.ps1 (ubicado en %ExchangeInsallPath%Scripts). Este script recupera la información de configuración del servidor de origen y almacena dicha información en un archivo XML intermedio.

Se importa la siguiente información desde el servidor de origen y se almacena en el archivo XML intermedio:

  - Información relacionada con el servicio de transporte e información de la ruta de acceso del archivo de registro.
    
      - *ReceiveProtocolLogPath*
    
      - *SendProtocolLogPath*
    
      - *MessageTrackingLogPath*
    
      - *PickupDirectoryPath*
    
      - *RoutingTableLogPath*

  - Información relacionada con el agente de transporte, incluidas las configuraciones de estado y de prioridad de cada agente de transporte.

  - Información relacionada con todos los conectores de envío. Si se configuran conectores de envío para que usen credenciales, la contraseña se escribe en el archivo XML intermedio en forma de cadena cifrada. Puede usar el parámetro *-key* con los scripts ImportEdgeConfig.ps1 y ExportEdgeConfig.ps1 para especificar la cadena de 32 bytes que se usará para el cifrado y el descifrado de la contraseña. Si no usa el parámetro *-key*, se usa una clave de cifrado predeterminada.

  - Información relacionada con el conector de recepción. Para modificar las propiedades de enlace y puerto de la red local, debe modificar la información de configuración en el archivo de respuesta que se creó en el paso de validación de la configuración.

  - Configuración de dominio aceptado.

  - Configuración de dominio remoto.

  - Opciones de configuración de las funciones contra correo no deseado:
    
      - Información de la lista de direcciones IP permitidas. Solo se exportan las entradas de la lista de direcciones IP permitidas que el administrador configuró manualmente.
    
      - Información de la lista de direcciones IP bloqueadas.
    
      - Configuración del filtro de contenido.
    
      - Configuración del filtro de destinatarios.
    
      - Entradas de reescritura de direcciones.
    
      - Entradas de filtro de datos adjuntos.

Volver al principio

## Paso 2: Validación de la configuración en el servidor de destino

El servidor de destino es un servidor de Exchange 2013 con una instalación limpia del rol de servidor Transporte perimetral. En primer lugar, ejecute el script ImportEdgeConfig.ps1 (ubicado en %ExchangeInsallPath%Scripts) en el servidor de destino para validar la información existente en el archivo XML intermedio y crear el archivo de respuesta. El archivo de respuesta contiene la información específica de servidor que se usó al importar la configuración al servidor de destino. El archivo de respuesta contiene entradas para todas las configuraciones del servidor de origen que no sean válidas para el servidor de destino. Tendrá que modificar estas configuraciones de modo que sean válidas para el servidor de destino. Si todas las configuraciones son válidas, el archivo de respuesta no contendrá ninguna entrada. El archivo XML intermedio se puede usar en distintos servidores de destino. El archivo de respuesta es específico de un servidor de destino.

El script ImportEdgeConfig.ps1 (ubicado en %ExchangeInsallPath%Scripts) realiza las siguiente tareas:

  - Comprueba que se pueden crear rutas de datos y rutas de registros en el servidor de destino. Si las rutas de acceso no se pueden crear, se inserta una ruta de acceso en blanco en el archivo de respuesta.

  - Para cada conector de envío del archivo XML, el script agrega una entrada en blanco en el archivo de respuesta para la dirección IP de origen.

  - Para cada conector de recepción del archivo XML, el script agrega una entrada en blanco en el archivo de respuesta para los enlaces de la red local.

Tendrá que modificar manualmente el archivo de respuesta para proporcionar la siguiente información acerca de la configuración específica del servidor:

  - Rellene las rutas de datos y rutas de registros. Si estas rutas de acceso se dejan en blanco en el archivo de respuesta, en el siguiente paso se usarán las rutas de acceso configuradas en el archivo XML intermedio cuando se importe la configuración en el servidor de destino.

  - En cada una de las entradas del conector de envío, escriba la dirección IP de origen. Si este campo se deja en blanco, se producirá un error en el paso de importación de la configuración.

  - En cada una de las entradas del conector de recepción, escriba los enlaces de la red local. Si los enlaces de la red local se dejan en blanco, se producirá un error cuando intente importar la configuración en el servidor de destino.

Volver al principio

## Paso 3: Importación de la configuración en el servidor de destino

Puede realizar este paso en cualquier servidor de destino para clonar la configuración de un servidor de transporte perimetral existente o para restaurar el servidor a una configuración específica. Ejecute el script ImportEdgeConfig.ps1 (ubicado en %ExchangeInsallPath%Scripts) para validar e importar la configuración nueva. Después de ejecutar el script, la configuración del servidor de destino coincidirá con las configuraciones del archivo XML intermedio y del archivo de respuesta.


> [!IMPORTANT]
> Es recomendable realizar copias de seguridad de la configuración de servidor existente antes de ejecutar el proceso de importación de la configuración, de manera que si se produce un error en la operación de clonación, se puede restaurar el servidor al estado estable anterior.



En este paso se utiliza la información específica del servidor proporcionada en el archivo de respuesta. Si alguna configuración no está especificada en el archivo de respuesta, se usarán los datos del archivo XML intermedio. Antes de modificar la configuración, el script valida los datos del archivo XML intermedio y del archivo de respuesta.

La importación de la configuración modifica las siguientes opciones de configuración del servidor de destino:

  - Se modifica la configuración del agente de transporte.

  - Se quitan los conectores existentes en el servidor de destino y se agregan los conectores presentes en el archivo XML intermedio.

  - Se quitan los dominios aceptados existentes y se agregan las entradas de dominios aceptados del archivo XML intermedio.

  - Se quitan los dominios remotos existentes y se agregan las entradas de dominios remotos del archivo XML intermedio.

  - Se quitan las entradas de la lista de direcciones IP permitidas existentes y se agregan las entradas de la lista de direcciones IP permitidas del archivo intermedio de dominios remotos.

  - Se quitan las entradas de la lista de direcciones IP bloqueadas existentes y se agregan las entradas de la lista de direcciones IP bloqueadas del archivo intermedio de dominios remotos.

  - La siguiente configuración contra correo no deseado se clona en el servidor de destino:
    
      - Configuración del filtro de contenido
    
      - Configuración del filtro de destinatarios
    
      - Entradas de reescritura de direcciones
    
      - Entradas de filtro de datos adjuntos

Volver al principio

## Información de configuración de transporte

La configuración del objeto de configuración de transporte define configuraciones de transporte de correo electrónico para un servidor de transporte perimetral completo. Cuando importa el archivo XML intermedio en el servidor de destino, se importan todas las opciones del objeto de configuración del transporte, excepto las siguientes:

  - Nombres generales y fechas de creación del archivo XML exportado

  - Enviar información del conector

  - Recibir información del conector

  - Entradas de filtro de datos adjuntos

  - La entrada de atributo **MaxDumpsterSizePerStorageGroup**

Luego de que se finaliza el proceso de importación, también puede configurar los ajustes con el cmdlet **Set-TransportConfig**. Para obtener más información, vea [Set-TransportConfig](https://technet.microsoft.com/es-es/library/bb124151\(v=exchg.150\)).

Los atributos de la tabla siguiente están asociados al objeto de configuración de transporte y los valores predeterminados. Este objeto se configura en servidores de buzones de correo y de transporte perimetral. Sin embargo, muchos atributos se aplican solo al servicio de transporte en los servidores de buzones de correo de Exchange 2013. Configurar estos atributos en un servidor de transporte perimetral no tendrá ningún efecto.

### Atributos de la configuración de transporte y valores predeterminados

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Descripción</th>
<th>Valor predeterminado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ClearCategories</strong></p></td>
<td><p>Este atributo especifica si deben desactivarse las categorías de Microsoft Outlook durante la conversión del contenido.</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><strong>GenerateCopyOfDSNFor</strong></p></td>
<td><p>Este atributo especifica los códigos de notificación de estado de entrega (DSN) que hacen que el mensaje de DSN se copie en la dirección del administrador de correo electrónico. Los códigos de DSN se especifican como <em>x.y.z</em> y se separan por comas.</p></td>
<td><p>5.4.8, 5.4.6, 5.4.4, 5.2.4, 5.2.0, 5.1.4</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalSMTPServers</strong></p></td>
<td><p>Este atributo especifica una lista de direcciones IP del servidor SMTP interno o una lista de intervalos de direcciones IP que el Id. del remitente y el filtro de conexión deben omitir.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>JournalingReportNdrTo</strong></p></td>
<td><p>Este atributo especifica la dirección de correo electrónico a la que se envían los informes de diario si el buzón de correo de registro en diario no está disponible. Este atributo no se aplica a la configuración de un servidor de transporte perimetral.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxDumpsterSizePerStorageGroup</strong></p></td>
<td><p>Este atributo especifica el tamaño máximo del contenedor de transporte de un servidor de buzones de correo. Este atributo no se aplica a la configuración de un servidor de transporte perimetral.</p></td>
<td><p>18 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxDumpsterTime</strong></p></td>
<td><p>Este atributo especifica cuánto tiempo deben permanecer los mensajes de correo electrónico en el contenedor de transporte de un servidor de buzones de correo. Este atributo no se aplica a la configuración de un servidor de transporte perimetral.</p></td>
<td><p>7.00:00:00</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxReceiveSize</strong></p></td>
<td><p>Este atributo especifica el tamaño máximo de los mensajes que pueden recibir los destinatarios de la organización. Este atributo no se aplica a la configuración de un servidor de transporte perimetral.</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxRecipientEnvelopeLimit</strong></p></td>
<td><p>Este atributo especifica el número máximo de destinatarios permitidos en un solo mensaje de correo electrónico. Este atributo no se aplica a la configuración de un servidor de transporte perimetral.</p></td>
<td><p>5.000</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxSendSize</strong></p></td>
<td><p>Este atributo especifica el tamaño máximo de los mensajes que pueden enviar los remitentes de la organización. Este atributo no se aplica a la configuración de un servidor de transporte perimetral.</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>TLSReceiveDomainSecureList</strong></p></td>
<td><p>Este atributo especifica los dominios remotos que usarán la autenticación mutua de Seguridad del nivel de transporte (TLS) mediante conectores de recepción configurados para admitir la seguridad de dominio. Si hay varios dominios, se los puede separar por comas. El carácter comodín (*) no se admite en los dominios enumerados en este atributo.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>TLSSendDomainSecureList</strong></p></td>
<td><p>Este atributo especifica los dominios remotos que usarán la autenticación mutua de TLS cuando se envía un correo electrónico mediante un conector de envío configurado para admitir la seguridad de dominio y el espacio de direcciones del dominio de destino. Si hay varios dominios, se los puede separar por comas. El carácter comodín (*) no se admite en los dominios enumerados en este atributo.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>VerifySecureSubmitEnabled</strong></p></td>
<td><p>Este atributo comprueba que los clientes de correo electrónico que envían mensajes desde buzones ubicados en servidores de buzones de correo envíen mensajes MAPI cifrados. Este atributo no se aplica a la configuración de un servidor de transporte perimetral. Los valores válidos de este atributo son <code>$true</code> o <code>$false</code>.</p></td>
<td><p>False</p></td>
</tr>
<tr class="odd">
<td><p><strong>VoicemailJournalingEnabled</strong></p></td>
<td><p>Este atributo especifica si el agente de registro en diario registra el correo de voz de mensajería unificada. Este atributo no se aplica a la configuración de un servidor de transporte perimetral.</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Si el servidor de transporte perimetral se suscribe a la organización de Exchange más adelante, el valor del atributo&nbsp;<STRONG>InternalSMTPServers</STRONG>&nbsp;se sobrescribirá durante el proceso de EdgeSync. Para obtener más información, vea <A href="edge-subscriptions-exchange-2013-help.md">Suscripciones perimetrales</A>.



Volver al principio

