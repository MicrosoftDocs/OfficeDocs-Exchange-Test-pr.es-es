---
title: 'Seguimiento de conversión de contenido: Exchange 2013 Help'
TOCTitle: Seguimiento de conversión de contenido
ms:assetid: eb9c7df2-9093-49f9-aa4f-044909bd2225
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb397226(v=EXCHG.150)
ms:contentKeyID: 49895994
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Seguimiento de conversión de contenido

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-09-25_

El seguimiento de conversión de contenido captura errores de conversión de contenido MAPI realizada por el servicio de transporte de buzones de correo en mensajes entrantes y salientes en un servidor de buzones de correo de Microsoft Exchange Server 2013.

El servicio de transporte de buzones de correo en un servidor de buzones de correo es responsable de la conversión de contenido de los mensajes que se envían desde y hacia destinatarios de buzones de correo. En particular, el servicio de envío de transporte de buzones de correo convierte los mensajes salientes de los usuarios de buzones de correo de MAPI a MIME. El servicio de entrega de transporte de buzones de correo convierte los mensajes entrantes para los usuarios de buzones de correo de MIME a MAPI. El seguimiento de la conversión de contenido detecta los errores en las conversiones MAPI.

El categorizador del servicio de transporte en un servidor de buzones de correo es responsable de la conversión de contenido de todos los mensajes que se envían a destinatarios externos. La conversión de contenido no detecta errores de conversión de contenido que categorizador del servicio de transporte detecta cuando convierte los mensajes que se envían a destinatarios externos.

**Contenido**

Configure content conversion tracing

How content conversion tracing works

Considerations for content conversion tracing

## Configuración de seguimiento de conversión de contenido

El seguimiento de conversión de contenido se controla mediante los siguientes parámetros en los cmdlets **Set-TransportService** y **Set-MailboxTransportService**:

  - *ContentConversionTracingEnabled*   Este parámetro habilita o deshabilita el seguimiento de conversión de contenido en el servicio de transporte en el servidor de buzones de correo o en el servicio de transporte de buzones de correo en el servidor de buzones de correo. Los valores válidos de este parámetro son `$true` y `$false`. El valor predeterminado es `$false`. Si la organización de Exchange contiene varios servidores de buzones de correo, debe habilitar el seguimiento de conversión de contenido en cada uno de ellos.

  - *PipelineTracingPath*   A pesar de que este parámetro se asocia al seguimiento de canalización, también especifica la ubicación raíz de los archivos de seguimiento de la conversión de contenido. La ubicación predeterminada en el servicio de transporte es `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`. La ubicación predeterminada en el servicio de transporte de buzones de correo es `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`. La ruta de acceso debe ser local para el equipo Exchange.

La conversión de contenido crea una carpeta denominada `ContentConversionTracing` en la ruta de acceso especificada por el parámetro *PipelineTracingPath*. En la carpeta `ContentConversionTracing`, la conversión de contenido crea dos subcarpetas: `InboundFailures` y `OutboundFailures`. La carpeta `InboundFailures` contiene la información sobre los errores de conversión de contenido de los mensajes entrantes. La carpeta `OutboundFailures` contiene la información sobre los errores de conversión de contenido de los mensajes salientes.

El tamaño máximo para todos los archivos en la carpeta `InboundFailures` o la carpeta `OutboundFailures` es 128 megabytes (MB). El seguimiento de conversión de contenido no utiliza un registro circular para quitar los archivos antiguos sobre la base de la antigüedad o el tamaño de los archivos. Tan pronto como se haya alcanzado el tamaño máximo de una carpeta, el seguimiento de conversión de contenido deja de escribir información en la carpeta. Si desea asegurarse de que se no se sobrepasan los límites de tamaño máximos de la carpeta, puede crear una tarea programada que mueva periódicamente los archivos del seguimiento de conversión de contenido a otra ubicación.

Los permisos que se necesitan en las carpetas y subcarpetas que se utilizan en el seguimiento de la conversión de contenido son los siguientes:

  - Administradores: Control total

  - Servicio de red: Control total

  - Sistema: Control total


> [!WARNING]
> El seguimiento de conversión de contenido copia todo el contenido de los mensajes de correo electrónico. Para evitar la divulgación no deseada de información confidencial, debe establecer permisos de seguridad apropiados en la ubicación de los archivos de seguimiento de conversión de contenido.



Volver al principio

## Cómo funciona el seguimiento de conversión de contenido

Cuando se produce un error en la conversión de contenido de un mensaje entrante, se envía al remitente del mensaje una notificación del estado de entrega (DNS) con el código de estado 5.6.0. Si el seguimiento de conversión de contenido está habilitado, se registra la información sobre el error a la vez que se genera el mensaje de DNS 5.6.0. Cada error de conversión de contenido genera dos archivos independientes.

Un error en la conversión de contenido que se produzca cuando se convierte un mensaje entrante de MIME a MAPI genera los dos archivos siguientes en la carpeta InboundFailures:

  - **\<GUID\>.eml**   Este archivo contiene el mensaje del error en formato de texto.

  - **\<GUID\>.txt**   Este archivo contiene la descripción de la excepción, los resultados de la conversión, las opciones de conversión y los límites de tamaño de mensaje que el servicio de transporte de buzones de correo impone en todos los mensajes.

Un error en la conversión de contenido que se produzca cuando se convierte un mensaje saliente de MAPI a MIME genera los dos archivos siguientes en la carpeta OutboundFailures:

  - **\<GUID\>.msg**   Este archivo contiene el mensaje de error en formato de mensaje de Microsoft Outlook.

  - **\<GUID\>.txt**   Este archivo contiene la descripción de la excepción, los resultados de la conversión, las opciones de conversión y los límites de tamaño del mensaje que impone el controlador de almacenamiento en todos los mensajes.

El marcador de posición \<*GUID*\> es el mismo en ambos nombres de archivo. Cada error de conversión de contenido genera un GUID diferente que se usa en los nombres de archivo de los archivos de mensaje y de texto correspondientes. Un ejemplo de GUID que se usa en los nombres de archivo es `038b930e-61fd-4bfd-b9b4-0374c18b73f7`.

Volver al principio

## Consideraciones acerca del seguimiento de conversión de contenido

Puede dejar el seguimiento de la conversión de contenido habilitado para que se efectúe un control proactivo. O bien, puede habilitar el seguimiento de la conversión de contenido para solucionar un evento de error específico. Por lo general, puede reproducir errores en la conversión de contenido entrante si solicita al destinatario del mensaje de DNS 5.6.0 que vuelva a enviar el mensaje original.

Los errores en la conversión de contenido entrante son los más habituales. Entre algunos de los motivos de error en la conversión de contenido entrante se incluyen los siguientes:

  - **Infracción de los límites de tamaño de mensaje**   Estos límites de tamaño de mensaje son impuestos por el servicio de trasporte de buzones de correo para ayudar a evitar ataques por denegación de servicio (DoS). Estos límites en los mensajes figuran en el archivo \<*GUID*\>.txt. Dichos límites en los mensajes incluyen lo siguiente:
    
      - **MaxMimeTextHeaderLength**  Este límite especifica el número máximo de caracteres de texto que se pueden utilizar en un encabezado MIME. El valor es 2000.
    
      - **MaxMimeSubjectLength**  Este límite especifica el número máximo de caracteres de texto que se pueden utilizar en la línea del asunto. El valor es 255.
    
      - **MSize**   Este límite especifica el tamaño máximo del mensaje. El valor es 2147483647 bytes.
    
      - **MaxMimeRecipients**   Este límite especifica el número total de destinatarios que se pueden incluir en los campos Para, CC y CCO. El valor es 12288.
    
      - **MaxRecipientPropertyLength**  Este límite especifica el número máximo de caracteres de texto que se pueden utilizar en una descripción de destinatario. El valor es 1000.
    
      - **MaxBodyPartsTotal**  Este límite especifica el número máximo de partes de mensaje que se pueden utilizar en un mensaje de varias partes MIME. El valor es 250.
    
      - **MaxEmbeddedMessageDepth**   Este límite especifica el número máximo de mensajes reenviados que puede contener un mensaje. El valor es 30.
    
    Para obtener más información sobre los límites de tamaño de mensaje configurables que se utilizan en el servicio de transporte en servidores de buzones de correo o en servidores de transporte perimetral, consulte [Límites de tamaño de mensaje](message-size-limits-exchange-2013-help.md).

  - **Error en la conversión de un mensaje de iCalendar entrante para una convocatoria de reunión** En RFC 2445 se define iCalendar como un estándar para el intercambio de información de calendario. Entre los motivos específicos del error en la conversión se incluyen los siguientes:
    
      - Uso incorrecto de iCalendar por parte del agente remitente.
    
      - Construcciones de iCalendar que no son compatibles con el esquema de calendario de Outlook o Exchange.
    
    Los errores en la conversión de iCalendar no originan la recepción de un mensaje de DSN 5.6.0 por parte del remitente. En su lugar, el mensaje se entrega con archivo .ics como datos adjuntos que contiene el cuerpo del mensaje de iCalendar.

  - **Errores causados por un mensaje MIME con formato incorrecto**   Los mensajes de correo electrónico comerciales no solicitados o el correo no deseado pueden contener errores de formato en el encabezado del mensaje, por ejemplo, comillas distintas en las descripciones de destinatarios. Un número mucho más reducido de errores originados por mensajes MIME con formatos erróneos se consideran errores.

Los errores en la conversión de contenido saliente son mucho menos habituales que los errores en el contenido entrante. Cuando se producen errores salientes, generalmente, se deben a errores de código de Exchange o a que el contenido del mensaje está dañado.

Volver al principio

