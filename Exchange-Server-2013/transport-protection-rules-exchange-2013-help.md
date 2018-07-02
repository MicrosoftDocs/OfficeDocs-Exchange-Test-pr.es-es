---
title: 'Reglas de protección de transporte: Exchange 2013 Help'
TOCTitle: Reglas de protección de transporte
ms:assetid: 9bd6d049-165e-4e51-a79f-3b8ff409da55
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298166(v=EXCHG.150)
ms:contentKeyID: 49895800
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Reglas de protección de transporte

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Los mensajes y los datos adjuntos de correo electrónico contienen cada vez más información crítica para la empresa como especificaciones de productos, documentos de estrategia empresarial y datos financieros, o información de identificación personal (PII) como detalles de contactos, números de seguridad social, números de tarjetas de crédito y registros de empleados. Existen varias reglamentaciones locales y específicas de la industria en muchas partes del mundo que rigen la recopilación, el almacenamiento y la divulgación de la información de identificación personal.

Para ayudar a proteger la información confidencial, las organizaciones crean directivas de mensajería que brindan pautas acerca de cómo administrar este tipo de información. En MicrosoftExchange Server 2013, puede usar reglas de protección de transporte para implementar estas directivas de mensajería mediante la inspección del contenido de mensajes, el cifrado de contenido de correo electrónico confidencial y el uso de la administración de derechos para controlar el acceso al contenido.

Para tareas de gestión relacionadas con la gestión de IRM, consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Reglas de protección de transporte y AD RMS

Las reglas de protección de transporte le permiten usar reglas de transporte para mensajes protegidos con IRM mediante la aplicación de una plantilla de directiva de derechos de [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823) (AD RMS).


> [!NOTE]
> AD&nbsp;RMS constituye una tecnología de protección de información que funciona con clientes y aplicaciones compatibles con Rights Management Service (RMS) a fin de proteger información confidencial en línea y sin conexión. Para utilizar la protección con IRM en una implementación local de Exchange, Exchange&nbsp;2013 necesita la implementación local de AD&nbsp;RMS que ejecute Windows Server 2008 o posterior.



AD RMS usa plantillas de directivas basadas en XML para permitir que las aplicaciones habilitadas con IRM compatibles apliquen directivas de protección uniformes. En Windows Server 2008 y posterior, el servidor de AD RMS presenta un servicio web que puede usarse para enumerar y adquirir plantillas. Exchange 2013 incluye la plantilla No reenviar.

Cuando se aplica la plantilla No reenviar a un mensaje, solo los destinatarios del mensaje pueden descifrarlo. Los destinatarios no pueden reenviar el mensaje a ninguna otra persona, copiar el contenido del mensaje ni imprimirlo.

Se pueden crear plantillas de RMS adicionales en la implementación local de AD RMS para cumplir con los requisitos de protección de derechos de la organización.


> [!IMPORTANT]
> Si una plantilla de directivas de derechos se elimina del servidor de AD&nbsp;RMS, debe modificar las reglas de protección de transporte que usa la plantilla eliminada. Si una regla de protección de transporte sigue usando una plantilla de directivas de derechos que se eliminó, el servidor de AD&nbsp;RMS no podrá autorizar el contenido a ninguno de los destinatarios y el remitente recibirá un informe de no entrega (NDR).<BR>En Windows Server 2008 y posterior, las plantillas de directivas de derechos se pueden archivar en lugar de eliminarlas. Las plantillas archivadas se pueden seguir usando para autorizar contenido, pero cuando cree o modifique una regla de protección de transporte, las plantillas archivadas no se incluirán en la lista de plantillas.



Para obtener más información acerca de la creación de plantillas de AD RMS, consulte [Guía paso a paso para la implementación de plantillas de directivas de derechos de AD RMS](https://go.microsoft.com/fwlink/p/?linkid=136593).

## Protección automática mediante reglas de protección de transporte

Los mensajes que contienen información crítica para la empresa o PII se pueden identificar mediante una combinación de condiciones de reglas de transporte, incluidas expresiones regulares que identifican patrones de texto tales como números de seguridad social. Las organizaciones requieren diferentes niveles de protección de la información confidencial. Algunos tipos de información pueden restringirse a empleados, contratistas o asociados; mientras que otros tipos pueden restringirse solamente a empleados a tiempo completo. El nivel deseado de protección se puede aplicar a los mensajes mediante la aplicación de una plantilla de directivas de derechos adecuada. Por ejemplo, los usuarios pueden marcar los mensajes o datos adjuntos de correo electrónico como información confidencial de la empresa. Como se ilustra en la figura siguiente, pude crear una regla de protección de transporte para inspeccionar el contenido de mensajes en busca de las palabras "Información confidencial de la empresa" y proteger el mensaje con IRM de manera automática.

Para obtener más información acerca de la creación de reglas de transporte para aplicar la protección de derechos, consulte [Crear una regla de protección de transporte](create-a-transport-protection-rule-exchange-2013-help.md).

## Protección persistente de adjuntos de correo electrónico

Los usuarios envían información crítica para la empresa y PII en datos adjuntos de correo electrónico con formatos de archivos comunes de Microsoft Office como Microsoft Office Word, Excel y PowerPoint. Todos estos formatos de archivos admiten la protección permanente a través de IRM y, de esta forma, puede asegurarse de que la información crítica para la empresa y PII contenida en estos documentos esté protegida adecuadamente. Las reglas de protección de transporte aplican la misma protección a los mensajes y los datos adjuntos de correo electrónico en formatos de archivos admitidos.

## Agente de reglas de transporte y agente de cifrado

Cuando usa reglas de protección de transporte para mensajes protegidos con IRM en función de condiciones de reglas, el agente de reglas de transporte en el servidor de transporte de concentradores inspecciona los mensajes. Si el mensaje cumple con todas las condiciones y ninguna de las excepciones, lo etiqueta para ser protegido con IRM. El agente de cifrado, un agente de transporte integrado que se activa con el evento **OnRoutedMessage**, aplica realmente la protección IRM al mensaje. El agente de cifrado actúa en mensajes solo si IRM está habilitado para mensajes internos. Para obtener más información acerca de cómo habilitar IRM, consulte [Habilitar o deshabilitar IRM para mensajes internos](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

Cuando se reinicia el servicio de transporte y procesa el primer mensaje que requiere el cifrado de IRM, el agente de cifrado debe ser capaz de conectarse con un servidor de AD RMS de la organización. Para los mensajes posteriores, el agente no necesita establecer contacto con el servidor de AD RMS. Si se produce un error en el cifrado de un mensaje debido a condiciones transitorias, Exchange vuelve a intentar cifrar el mensaje tres veces en intervalos de 10 minutos. Después de los tres intentos, si no se puede cifrar el mensaje, este no se entrega a los destinatarios. Se envía un NDR al remitente. Se recomienda planear la implementación de AD RMS para alta disponibilidad para asegurarse de que el flujo de mensajes no se vea afectado.

Cuando planee usar reglas de protección de transporte, debe considerar el tipo de información que desea proteger y planear la creación de reglas de manera consecuente. En Exchange 2013, las reglas de transporte tienen una gran cantidad de predicados que le permiten inspeccionar el contenido de los mensajes, incluidos los datos adjuntos admitidos, los encabezados de mensaje, las direcciones del remitente y del destinatario, los atributos de Active Directory tales como departamento, pertenencia a grupos de distribución y relaciones de administración del remitente con los destinatarios. Para obtener información detallada acerca de los predicados de reglas de transporte disponibles en Exchange 2013, consulte [Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Asimismo, debe tener en cuenta el tráfico de mensajería de la organización y la cantidad de mensajes que se protegerán mediante las reglas de protección de transporte. La aplicación de la protección de IRM a una gran cantidad de mensajes requiere más recursos en el servidor Buzón de correo. Además, la protección de una gran cantidad de mensajes o de todos los mensajes también afecta la experiencia del cliente, en especial, para los usuarios de Microsoft Outlook.

