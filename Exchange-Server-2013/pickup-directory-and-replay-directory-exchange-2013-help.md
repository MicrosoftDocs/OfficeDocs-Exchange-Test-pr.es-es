---
title: 'Directorio de recogida y directorio de reproducción: Exchange 2013 Help'
TOCTitle: Directorio de recogida y directorio de reproducción
ms:assetid: ae191700-953f-411c-906f-dc90feec3d5a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124230(v=EXCHG.150)
ms:contentKeyID: 49895834
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Directorio de recogida y directorio de reproducción

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

De manera predeterminada, los directorios de recogida y de reproducción existen en todos los servidores Buzón de correo de Microsoft Exchange Server 2013 o en el servidor de transporte perimetral. Los archivos de mensajes de correo electrónico con el formato correcto que copia al directorio de recogida o de reproducción se envían para su entrega. Los administradores usan el directorio de recogida para probar el flujo de correo y las aplicaciones lo usan para crear y enviar sus propios mensajes. El directorio de reproducción recibe mensajes de servidores de puerta de enlace externos y también se lo puede utilizar para reenviar los mensajes que los administradores exportan desde las colas de servidores de Exchange.

**Contenido**

Anatomía de un archivo de mensaje de correo electrónico

Cómo procesan los mensajes los directorios de recogida y de reproducción

Requisitos de archivos de mensaje de directorio de recogida

Modificaciones del encabezado del mensaje del directorio de recogida

Requisitos del archivo de mensaje del directorio de reproducción

Modificaciones del encabezado del mensaje del directorio de reproducción

Fallas en el procesamiento de los mensajes de los directorios de recogida y de reproducción

Consideraciones de seguridad para los directorios de recogida y de reproducción

Permisos para los directorios de recogida y de reproducción

## Anatomía de un archivo de mensaje de correo electrónico

Un mensaje de correo electrónico SMTP estándar está compuesto por el *sobre del mensaje* y el contenido del mensaje. El sobre del mensaje contiene información necesaria para la transmisión y la entrega del mensaje. El contenido del mensaje contiene el cuerpo del mensaje y campos de encabezado de mensaje, que se denominan de forma colectiva *encabezado del mensaje*. El sobre del mensaje se describe en RFC 2821 y el encabezado del mensaje se describe en RFC 2822.

Cuando un emisor redacta un mensaje de correo electrónico y lo envía para su entrega, el mensaje contiene la información básica necesaria para el cumplimiento de los estándares SMTP, como el remitente, un destinatario, la fecha y la hora de redacción del mensaje, una línea de asunto opcional y un cuerpo del mensaje también opcional. Esta información está contenida en el propio mensaje y, por definición, está contenida en el encabezado del mensaje.

El servidor de mensajería del remitente genera un sobre para el mensaje utilizando la información del remitente y el destinatario del encabezado del mensaje, y transmite el mensaje a Internet para entregarlo al servidor de mensajería del destinatario. Los destinatarios nunca ven el sobre del mensaje porque lo genera el proceso de transmisión del mensaje y no forma parte del mensaje.

Cada servidor implicado en la transmisión del mensaje puede insertar campos de encabezado del mensaje relacionados con la función del servidor al entregar el mensaje u otros campos de encabezado del mensaje específicos de la aplicación en el mensaje. Cuando el destinatario abre el mensaje con un cliente de correo electrónico, dicho cliente de correo electrónico muestra la información más relevante del encabezado del mensaje, como el remitente, los destinatarios y el tema, junto con el cuerpo del mensaje.

Volver al principio

## Cómo procesan los mensajes los directorios de recogida y de reproducción

En Exchange 2013, la ubicación predeterminada del directorio de recogida es `%ExchangeInstallPath%TransportRoles\Pickup`. La ubicación predeterminada del directorio de reproducción es `%ExchangeInstallPath%TransportRoles\Replay`. Un archivo de mensaje .eml con formato correcto que se copia en el directorio de recogida o de reproducción se procesa para su envío en los siguientes pasos:

1.  Los directorios de recogida y de reproducción comprueban si hay nuevos archivos de mensaje cada cinco segundos. Este intervalo de sondeo no puede modificarse. Puede ajustar la velocidad de procesado de archivos de mensaje utilizando el parámetro *PickupDirectoryMaxMessagesPerMinute* con el cmdlet **Set-TransportService**. Este parámetro afecta al directorio de recogida y el directorio de reproducción. El valor predeterminado es 100 mensajes por minuto. Los archivos que no se pueden abrir se dejan en el directorio de recogida y se evalúan de nuevo en el siguiente sondeo.

2.  Se comprueban los límites establecidos en los archivos de mensajes en el directorio de recogida, como el tamaño máximo de los encabezados y el número máximo de destinatarios. El tamaño máximo predeterminado del encabezado es 64 KB y el número máximo de destinatarios es 100. Estos límites se pueden cambiar mediante el cmdlet **Set-TransportService**. Esta configuración afecta sólo al directorio de recogida.

3.  El nombre del archivo se modifica de *\<nombre\>*.eml a *\<nombre\>*.tmp. Si el archivo *\<filename\>*.tmp ya existe, el nombre de archivo se cambia a *\<filename\>\<datetime\>*.tmp. Si no se consigue cambiar el nombre del archivo, se genera un error de registro de eventos y el proceso de recogida continúa con el archivo siguiente.

4.  Una vez convertido correctamente el archivo .tmp en un mensaje de correo electrónico, se envía un comando de **delete on close** (eliminar al cerrar) al archivo .tmp. El archivo .tmp parece permanecer en el directorio de recogida, pero no se puede abrir.

5.  Después de poner en cola un mensaje correctamente, se emite un comando **close** y el archivo .tmp se elimina del directorio de recogida. Si se produce un error en la eliminación, se genera un error de registro de eventos. Si el servicio de transporte de Microsoft se reinicia mientras hay archivos .tmp en el directorio de recogida, todos los archivos .tmp se convierten a archivos .eml y se procesan de nuevo. Esto podría causar una duplicación de la transmisión de mensajes.

Volver al principio

## Requisitos de archivos de mensaje de directorio de recogida

Un archivo de mensaje que se copie en el directorio de recogida debe cumplir los requisitos siguientes para que se entregue correctamente:

  - El archivo de mensaje debe ser un archivo de texto que cumpla con el formato de mensaje SMTP básico. Se admiten contenidos y campos de encabezado de mensaje MIME.

  - El archivo de mensaje debe tener la extensión de nombre de archivo .eml.

  - Debe existir al menos una dirección de correo electrónico en los campos de encabezado del mensaje `Sender` o `From` en el encabezado del mensaje. Si existe una única dirección de correo electrónico en los campos `Sender` y `From`, la dirección de correo electrónico del campo `From` se utiliza como origen del mensaje en el sobre del mensaje.

  - Solo puede existir una dirección de correo electrónico en el campo `Sender`. No se permiten varias direcciones de correo electrónico. El campo `Sender` es opcional si solamente existe una dirección de correo electrónico en el campo `From`.

  - Se permiten varias direcciones de correo electrónico en el campo `From`, pero también debe existir una única dirección de correo electrónico en el campo `Sender`. La dirección del campo `Sender` se utiliza como origen del mensaje en el sobre del mensaje.

  - Debe existir al menos una dirección de correo electrónico en los campos `To`, `Cc` o `Bcc`.

  - Debe existir una línea en blanco entre el encabezado y el cuerpo del mensaje.

En este ejemplo, se muestra un mensaje de texto que utiliza un formato aceptable para el directorio de recogida.

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    
    This is the body of the message.

El contenido MIME también se admite en archivos de mensaje del directorio de recogida. MIME define una amplia gama de contenido de mensajes, que incluye lenguajes que no pueden representarse en texto ASCII de 7 bits, HTML y otros contenidos multimedia. La descripción de MIME y sus requisitos están fuera del alcance de este tema. En este ejemplo, se muestra un mensaje de MIME simple que usa un formato aceptable para el directorio de recogida.

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

Volver al principio

## Modificaciones del encabezado del mensaje del directorio de recogida

El directorio de recogida quita los siguientes campos de encabezado del mensaje:

  - `Received`

  - `Resent-*`

  - `Bcc`
    

    > [!NOTE]
    > Las direcciones de correo electrónico que se encuentran en los campos de encabezado de mensaje <CODE>Bcc</CODE> opcionales se procesan correctamente. Los destinatarios del campo <CODE>Bcc</CODE> se convierten en destinatarios de sobre de mensaje invisibles y se quitan del encabezado del mensaje para proteger su identidad. Si un mensaje sólo contiene destinatarios en el campo <CODE>Bcc</CODE>, el valor de <STRONG>Undisclosed Recipients</STRONG> (Destinatarios desconocidos) se agrega al campo <CODE>To</CODE> en el encabezado del mensaje.



El directorio de recogida agrega su propio campo de encabezado `Received` al mensaje como parte del proceso de envío. El campo de encabezado `Received` se aplica en el formato siguiente.

    Received: from localhost by Pickup with Microsoft SMTP Server id <ExchangeServerVersion><datetime>

El directorio de recogida modifica los siguientes campos de encabezado del mensaje si faltan o tienen un formato incorrecto:

  - **Id. de mensaje**   Si el campo `Message-Id` no existe o está vacío, el directorio de recogida agrega un campo Id. de mensaje con el formato *\<GUID\>*@*\<defaultdomain\>*.

  - **Fecha**   Si falta el campo `Date` o tiene un formato incorrecto, el directorio de recogida agrega la fecha y la hora del mensaje procesando el directorio de recogida.

Volver al principio

## Requisitos del archivo de mensaje del directorio de reproducción

El directorio de reproducción se emplea para volver a enviar mensajes exportados de Exchange y recibir mensajes de servidores de puerta de enlace externos. Esos mensajes ya están formateados para el directorio de reproducción. Casi no es necesario que un administrador o que otras aplicaciones redacten y envíen nuevos archivos de mensajes utilizando el directorio de reproducción. Debe utilizarse el directorio de recogida para crear y enviar nuevos archivos de mensaje.

Los mensajes del directorio de reproducción hacen un uso extensivo de *campos de encabezado X*. Los encabezados X son campos de encabezado de mensaje no oficiales definidos por el usuario que se encuentran en el encabezado del mensaje. Los encabezados X no se mencionan específicamente en RFC 2822, pero el uso de un campo de encabezado de mensaje no definido que empieza con "X-" se ha convertido en un método aceptado para agregar campos de encabezado de mensaje no oficiales a un mensaje. Los encabezados X específicos de Exchange que se utilizan en los archivos de mensaje del directorio de reproducción pueden establecer información de entrega que normalmente se encuentra en el sobre del mensaje. Esta función es necesaria para preservar información del mensaje original cuando utiliza el directorio de reproducción para procesar mensajes exportados de otro servidor de Exchange.

Un archivo de mensaje que se copie en el directorio de reproducción debe cumplir los requisitos siguientes para que se entregue correctamente:

  - El archivo de mensaje debe ser un archivo de texto que cumpla con el formato de mensaje SMTP básico. Se admiten contenidos y campos de encabezado de mensaje MIME.

  - El archivo de mensaje debe tener la extensión de nombre de archivo .eml.

  - Los encabezados X deben tener lugar antes de todos los campos de encabezado normales.

  - Debe haber una línea en blanco entre los campos de encabezado y el cuerpo del mensaje.

Los encabezados X descritos en la siguiente lista son necesarios para los mensajes del directorio de reproducción:

  - **Remitente X**   Este encabezado X sustituye al requisito de campo de encabezado `From` de un mensaje SMTP típico. Debe existir un campo `X-Sender` que contenga una dirección de correo electrónico. El directorio de reproducción ignora el campo de encabezado `From` si está presente, aunque el cliente de correo electrónico del destinatario muestra el valor del campo de encabezado de mensaje `From` como remitente del mensaje. Suelen existir otros parámetros en el campo `X-Sender`, como figura en el siguiente ejemplo.
    
        X-Sender: <bob@fabrikam.com> BODY=7bit RET=HDRS ENVID=12345ABCD auth=<someAuth>
    

    > [!NOTE]
    > Estos parámetros son valores del sobre del mensaje generados normalmente por el servidor emisor. Es posible que vea parámetros similares en archivos de mensaje exportados.<BR><CODE>RET</CODE> especifica si se devuelve todo el mensaje o solo los encabezados en caso de no poderse entregar el mensaje. <CODE>RET</CODE> puede tener un valor de <CODE>HDRS</CODE> o <CODE>FULL</CODE>.<CODE> ENVID</CODE> si es un identificador de sobre de mensaje. <CODE>BODY</CODE> especifica la codificación de texto del mensaje. <CODE>auth</CODE> especifica un mecanismo de autenticación al servidor de mensajes como se describe en RFC 2554.



  - **Destinatario X**   Este encabezado X sustituye al requisito de campo de encabezado `To` de un mensaje SMTP típico. Debe existir como mínimo un campo `X-Receiver` que contenga una dirección de correo electrónico. Se permiten múltiples campos `X-Receiver` para múltiples destinatarios. El directorio de reproducción ignora los campos de encabezado de mensaje `To` si están presentes, aunque el cliente de correo electrónico del destinatario muestra los valores de los campos de encabezado de mensaje `To` como destinatarios del mensaje. Pueden existir otros parámetros opcionales en los campos `X-Receiver`, como figura en el siguiente ejemplo.
    
        X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    

    > [!NOTE]
    > Estos parámetros son valores del sobre del mensaje generados normalmente por el servidor emisor. Es posible que vea parámetros similares en archivos de mensaje exportados. Estos parámetros se relacionan con los mensajes de notificación de estado de entrega (DSN) tal como se indica en RFC 1891.<BR><CODE>NOTIFY</CODE> puede tener un valor de <CODE>NEVER</CODE>, <CODE>DELAY</CODE> o <CODE>FAILURE</CODE>. <CODE>ORcpt</CODE> mantiene el destinatario original del mensaje.



Los encabezados X descritos en la siguiente lista son opcionales para los archivos de mensaje del directorio de reproducción:

  - **X-CreatedBy**   Se usa para las funciones de firewall de encabezado. Si existe este encabezado X, no debe estar en blanco. Si no existe el campo `X-CreatedBy`, se agrega con un valor de **Unspecified** (No especificado). Normalmente, el valor de este campo es **MSExchange15**, aunque también puede contener el tipo de espacio de direcciones que no son SMTP que se establece en un conector de envío, por ejemplo **Notes** (Notas).

  - **X-EndOfInjectedXHeaders**   Tamaño en bytes de todos los encabezados X presentes. Este encabezado X se puede utilizar como un marcador para indicar el último campo de encabezado X antes de que empiecen los campos de encabezado normales.

  - **X-ExtendedMessageProps**   Propiedades ampliadas del mensaje.

  - **X-HeloDomain**   La secuencia de dominio HELO/EHLO presentada durante la conversación de protocolo SMTP inicial.

  - **X-Source**   Lo usa el Visor de cola en la columna **MessageSourceName**. Si no se especifica el valor de este encabezado X, se usa el valor de **Replay** (Reproducción). Otros valores posibles para este encabezado X son **Smtp Receive Connector** (Conector de recepción Smtp) y **Smtp Send Connector** (Conector de envío Smtp).

  - **X-SourceIPAddress**   Dirección IP del servidor de envío. Este campo es `0.0.0.0` si no se indica una dirección IP.

En este ejemplo, se muestra un mensaje de texto que utiliza un formato aceptable para el directorio de reproducción.

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345AB auth=<someAuth>
    Subject: Optional message subject
    
    This is the body of the message.

El contenido MIME también es compatible en los archivos de mensajes del directorio de reproducción. MIME define una amplia gama de contenido de mensajes, que incluye lenguajes que no pueden representarse en texto ASCII de 7 bits, HTML y otros contenidos multimedia. La descripción de MIME y sus requisitos están fuera del alcance de este tema. En este ejemplo, se muestra un mensaje de MIME simple que usa un formato aceptable para el directorio de reproducción.

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345ABCD auth=<someAuth>
    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Optional message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

Volver al principio

## Modificaciones del encabezado del mensaje del directorio de reproducción

El directorio de reproducción elimina el campo de encabezado de mensaje `Bcc` del archivo del mensaje.

El directorio de reproducción agrega su propio campo de encabezado de mensaje `Received` a un mensaje como parte del proceso de envío de mensajes. El campo de encabezado de mensaje Recibido se aplica en el formato siguiente.

    Received: from <ReceivingServerName> by Replay with <ExchangeServerVersion><DateTime>

El directorio de reproducción modifica los siguientes campos de encabezado de mensaje en el encabezado del mensaje:

  - **Id. de mensaje**   Si este campo de encabezado de mensaje de este mensaje no existe o está vacío, el directorio de reproducción agrega un campo Id. de mensaje con el formato *\<GUID\>*@*\<defaultdomain\>*.

  - **Fecha**   Si este campo de encabezado de mensaje no existe o está defectuoso, el directorio de reproducción agrega el campo de encabezado de mensaje Fecha utilizando la fecha y la hora del procesamiento del mensaje por parte del directorio de reproducción.

Volver al principio

## Fallas en el procesamiento de los mensajes de los directorios de recogida y de reproducción

Es posible que un archivo de mensaje copiado en los directorios de recogida o reproducción no se sitúe correctamente en la cola para su entrega. Pueden producirse las siguientes categorías de error de envío de mensaje:

  - **Errores de entrega**   Un archivo de mensaje con el formato correcto y un remitente válido que no se puede enviar correctamente para su entrega genera un informe de no entrega (NDR). El contenido incorrecto o las violaciones de la restricción de los mensajes del directorio de recogida también podrían causar un NDR. Cuando se genera un NDR durante el procesamiento de mensajes, el archivo de mensaje original se adjunta al mensaje de NDR y el archivo de mensaje se elimina del directorio de recogida o del directorio de reproducción.
    

    > [!NOTE]
    > Un mensaje con un formato correcto enviado a la canalización de transporte puede experimentar más adelante un error de entrega y ser devuelto al remitente con un NDR. Este tipo de error puede deberse a un problema de transmisión que nada tiene que ver con los directorios de recogida o de reproducción, por ejemplo un error de servidor de mensajería o un error de enrutamiento en la ruta de entrega del mensaje.



  - **Correo con errores**   Un mensaje clasificado como *correo con errores* tiene graves problemas que impiden que los directorios de recogida o reproducción envíen el mensaje para su entrega. La otra condición que provoca correo erróneo es un mensaje con un formato correcto pero con destinatarios no válidos. En este caso, no se puede enviar un NDR al emisor porque éste no es válido.
    
    Los archivos de mensaje clasificados como correo con errores se dejan en los directorios de recogida o de reproducción y su nombre cambia de *\<filename\>*.eml a *\<filename\>*.bad. Si el archivo *\<nombrearchivo\>*.bad ya existe, se cambia el nombre a *\<nombrearchivo\>\<fechahora\>*.bad. Si existe correo erróneo en los directorios de recogida o de reproducción, se genera un error de registro de eventos, pero los mismos mensajes de correo con errores no generan errores de registro de eventos.
    

    > [!NOTE]
    > Siempre cree y guarde los archivos de mensaje en una ubicación distinta antes de copiarlos al directorio de recogida para su entrega. El directorio de recogida comprueba si existen mensajes nuevos cada 5&nbsp;segundos. Por lo tanto, si intenta crear y guardar los archivos de mensaje en el mismo directorio de recogida, es posible que éste intente procesar los archivos de mensaje antes de que los acabe.



Volver al principio

## Consideraciones de seguridad para los directorios de recogida y de reproducción

En la siguiente lista se describen problemas de seguridad comunes a los directorios de recogida y de reproducción:

  - Las comprobaciones de seguridad configuradas en un conector de recepción, como comprobaciones contra correo electrónico no deseado, antimalware, filtrado de remitentes o acciones de filtrado de destinatarios no se realizan en mensajes que se envían a través del directorio de recogida o de reproducción.

  - Un directorio de recogida o de reproducción comprometido puede actuar como una retransmisión abierta. Eso permite que los mensajes se reenvíen o *retransmitan* con un servidor distinto para ocultar el origen real del mensaje.

La siguiente lista describe preocupaciones de seguridad adicionales que afectan al directorio de reproducción:

  - Los encabezados X utilizados por el directorio de reproducción permiten la creación manual del sobre del mensaje. La información de los campos `X-Sender` y `X-Receiver` puede ser totalmente distinta de los campos de encabezado de mensaje `To` o `From` que muestran los clientes de correo electrónico. Esta usurpación de la identidad del emisor y del dominio suele denominarse *suplantación de identidad*. Un *correo suplantado* es un mensaje de correo electrónico en el que la dirección del remitente se ha modificado para parecer que ha partido de un remitente que no es el que ha enviado originalmente el mensaje.

  - Si el campo `X-CreatedBy` tiene el valor **MSExchange15**, el destino se considera de confianza y no se aplica seguridad de encabezado. El *Firewall de encabezado* es una manera que tiene Exchange de preservar los encabezados X en mensajes que se transmiten entre servidores de Exchange de confianza, o de eliminar posibles encabezados X reveladores de los mensajes transmitidos a destinos que no son de confianza y que se encuentran fuera de la organización Exchange. Estos encabezados X pueden utilizarse para compartir información de Exchange como el nivel de confianza de correo no deseado (SCL), la firma de mensajes o el cifrado entre servidores de Exchange autorizados. Desvelar esta información a fuentes no autorizadas podría suponer un riesgo para la seguridad. Para obtener más información acerca de la seguridad de encabezado, consulte el artículo [Descripción del firewall de encabezado](https://go.microsoft.com/fwlink/?linkid=268394).

Debe aplicarse un mayor nivel de seguridad en el directorio de reproducción debido a los riesgos de seguridad adicionales asociados. Es posible otorgar acceso al directorio de recogida a los usuarios o aplicaciones que deban generar y enviar mensajes, pero no deben tener acceso al directorio de reproducción.

Tanto el directorio de recogida como el directorio de reproducción están habilitados de manera predeterminada en todos los servidores Buzón de correo y de transporte perimetral. Si el directorio de recogida o el de reproducción no son necesarios en un servidor de buzones de correo o de transporte perimetral en su organización, puede deshabilitar el directorio de recogida o el de reproducción en dicho servidor al configurar la ruta del directorio de recogida o el de reproducción con el valor `$null`. Para obtener más información, consulte [Configurar el directorio de recogida y el directorio de reproducción](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

Volver al principio

## Permisos para los directorios de recogida y de reproducción

Los siguientes permisos son necesarios para los directorios de recogida y de reproducción:

  - Administrador: Control total

  - Sistema: Control total

  - Servicio de red: Lectura, Escritura y Eliminar subcarpetas y archivos

De forma predeterminada, el servicio de transporte de Microsoft Exchange usa credenciales de seguridad de la cuenta de usuario del servicio de red para administrar la ubicación y los permisos de los directorios de recogida y de reproducción. La cuenta del servicio de red requiere estos permisos en el directorio de recogida para poder abrir archivos .eml, cambiar su nombre a .tmp, y eliminarlos o asignarles la extensión .bad si el mensaje se clasifica como correo erróneo.

La ubicación de estos directorios se puede cambiar mediante los parámetros *PickupDirectoryPath* y *ReplayDirectoryPath* en el cmdlet **Set-TransportService**. El cambio correcto de ubicación del directorio de recogida depende de los derechos que se otorguen a la cuenta del servicio de red en la nueva ubicación del directorio de recogida y de si los nuevos directorios ya existen. Si el directorio no existe, y si la cuenta del servicio de red tiene los derechos correspondientes para crear carpetas y aplicar permisos en la nueva ubicación, se crea el directorio y se le aplican los permisos correctos. Si ya existe el nuevo directorio, no se comprueban los permisos de la carpeta existente. Si cambia las ubicaciones de directorio con el parámetro *PickupDirectoryPath* o *ReplayDirectoryPath* mediante el cmdlet **Set-TransportService**, es conveniente comprobar que el directorio nuevo exista y que disponga de los correspondientes permisos.

Volver al principio

