---
title: 'Prevención de pérdida de datos: Exchange 2013 Help'
TOCTitle: Prevención de pérdida de datos
ms:assetid: 7c8ed3c1-ca91-4d9b-b16b-0a2b8ac89730
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150527(v=EXCHG.150)
ms:contentKeyID: 48267681
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Prevención de pérdida de datos

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Obtenga más información sobre las directivas DLP en Exchange Server 2013 y Exchange Online, incluido el contenido y cómo se pueden probar. También obtendrá información sobre una característica nueva de DLP de Exchange.

La prevención de pérdida de datos (DLP) es un tema importante para los sistemas de mensaje empresariales debido al uso extensivo del correo electrónico para comunicaciones críticas del negocio que incluyen datos confidenciales. Para aplicar los requisitos de cumplimiento de estos datos y administrar su uso en el correo electrónico sin afectar la productividad de los trabajadores, las características de DLP facilitan la administración de datos confidenciales como nunca antes. Para obtener información conceptual de DLP, vea el siguiente vídeo.

> [!VIDEO https://www.microsoft.com/es-es/videoplayer/embed/31f2b48e-93ed-4be3-b46d-e7230c0fed8f]

Las directivas de DLP son paquetes sencillos que contienen conjuntos de condiciones, compuestos por reglas de transporte, acciones y excepciones que se crean en el Centro de administración de Exchange (EAC) y luego se activan para filtrar mensajes de correo electrónico y datos adjuntos. Puede crear una directiva de DLP, pero decidir no activarla. Esto le permite probar sus directivas sin afectar el flujo de correo. Las directivas de DLP pueden usar todas las capacidades de las reglas de transporte existentes. De hecho, se crearon nuevos tipos de reglas de transporte en Microsoft Exchange Server 2013 y Exchange Online para adquirir las nuevas funcionalidades de DLP. Una nueva característica importante de las reglas de transporte es el nuevo enfoque para clasificar información confidencial que se puede incorporar al procesamiento de flujo de correo. Esta característica nueva de DLP realiza un análisis profundo del contenido, mediante coincidencias de palabras clave, coincidencias de diccionario y otros exámenes de contenido con el objetivo de detectar el contenido que infringe las directivas de DLP de la organización. La versiones más recientes de Exchange Online y Exchange 2013 SP1 agregan [Creación de huella digital de documento](overview-of-document-fingerprinting-in-exchange.md), lo cual le ayuda a detectar información confidencial en formularios estándar. Para obtener más información acerca de las reglas de transporte, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) o [Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)) (Exchange Online) y [Integración de las reglas de información confidencial con las reglas de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md). También puede administrar las directivas de DLP mediante los cmdlets del Shell de administración de Exchange. Para obtener más información acerca de los cmdlets de directivas y conformidad, consulte [Cmdlets de directiva y conformidad](https://technet.microsoft.com/es-es/library/dd298082\(v=exchg.150\)).

Además de las directivas de DLP personalizables en sí, también puede informar a los remitentes de correo electrónico que pueden estar por infringir una de sus directivas, incluso antes de que envíen un mensaje ofensivo. Para ello, puede configurar las sugerencias de directivas. Las sugerencias de directiva son similares a las sugerencias de correo electrónico y se pueden configurar para introducir una breve nota en el cliente Outlook 2013 de Microsoft que proporcione información sobre posibles infracciones de la directiva a un usuario que esté creando un mensaje. En la versión más reciente de Exchange Online y en Exchange 2013 SP1, las sugerencias de directivas se muestran en Outlook Web App y OWA para dispositivos. Para obtener más información, consulte [Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).


> [!NOTE]
> Exchange Online: DLP es una característica premium que requiere una suscripción al plan 2 de Exchange Online. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Licencias de Exchange Online</A>.<BR>Exchange&nbsp;2013: La prevención de pérdida de datos (DLP) es una característica especial que requiere una licencia de acceso de cliente de empresa (CAL) de Exchange. Para obtener más información sobre las CAL y la emisión de licencias del servidor, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licencias de Exchange Server</A>.<BR><STRONG>Exchange Enterprise CAL con servicios:</STRONG> Debe tener en cuenta una diferencia en comportamiento si es cliente de Exchange Enterprise CAL con servicios con una implementación híbrida, donde tiene algunos buzones ubicados de forma local y algunos en Exchange Online. Las directivas de DLP se aplican en Exchange Online. Por lo tanto, los mensajes enviados desde un usuario local hasta otro usuario local no tienen aplicadas las directivas de DLP, porque el mensaje no abandona la infraestructura local.



¿Está buscando las tareas de administración relacionadas con la Prevención de pérdida de datos? Consulte [Procedimientos de DLP](dlp-procedures-exchange-2013-help.md) (Exchange 2013) o [Procedimientos de DLP](https://technet.microsoft.com/es-es/library/jj938003\(v=exchg.150\)) (Exchange Online).

**Contenido**

Establecer directivas para proteger los datos confidenciales

Tipos de información confidencial en las directivas de DLP

Detectar información confidencial junto con la clasificación tradicional de mensajes

Detección de datos de formulario confidenciales con la creación de huella digital de documento

Las Sugerencias de directivas notifican a los usuarios sobre las expectativas de contenido confidencial

Información acerca de los mensajes procesados por DLP

Requisitos previos para la instalación

Más información

## Establecer directivas para proteger los datos confidenciales

Las características de la prevención de pérdida de datos le pueden ayudar a identificar y supervisar muchas categorías de información confidencial que definió en las condiciones de sus directivas, como por ejemplo los números de identificación privada o los de la tarjeta de crédito. Tiene la opción de definir sus propias directivas y reglas de transporte personalizadas o de utilizar las plantillas de directivas de DLP predefinidas por Microsoft para comenzar rápidamente. Para obtener más información acerca de las plantillas de directivas incluidas, consulte [Plantillas de directivas de DLP suministradas en Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). Una *plantilla de directiva* incluye una gama de condiciones, reglas y acciones que puede seleccionar para crear y guardar una directiva de DLP real que le ayudará a inspeccionar los mensajes. Las plantillas de directivas son modelos a partir de los cuales puede seleccionar o crear sus propias reglas específicas para crear una directiva que se ajuste a sus necesidades para la prevención de pérdida de datos.

Existen tres métodos diferentes para empezar a utilizar DLP:

1.  **Aplicar una plantilla instantánea de Microsoft.**   La forma más rápida de empezar a usar directivas de DLP es crear e implementar una nueva directiva a partir de una plantilla. Esto le ahorra el trabajo de tener que generar un nuevo conjunto de reglas desde cero. Debe saber para cuál tipo de datos quiere realizar la comprobación o qué tipo de reglamentación de cumplimiento desea tratar. También debe conocer las expectativas de su organización con respecto al procesamiento de estos datos. Encontrará más información en [Plantillas de directivas de DLP suministradas en Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md) y [Crear una directiva DLP a partir de una plantilla](how-to-new-dlp-data-loss-prevention-policy-template.md).

2.  **Importar una directiva prefabricada de fuera de la organización.**   Puede importar directivas ya creadas fuera de su entorno de mensajería por proveedores de software independientes. De esto modo, podrá ampliar las soluciones de DLP para ajustarse a los requisitos de su empresa. Encontrará más información en [Plantillas de directiva de partners de Microsoft](policy-templates-from-microsoft-partners-exchange-2013-help.md), [Definir sus propios tipos de información y plantillas de DLP](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md) y [Importar una plantilla de directiva DLP personalizada desde un archivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

3.  **Crear una directiva personalizada sin ninguna condición preexistente.**   Su empresa puede disponer de sus propios requisitos para supervisar ciertos tipos de datos conocidos dentro de un sistema de mensajería. Puede crear una directiva personalizada por su cuenta a fin de comenzar a comprobar y actuar en función de sus propios datos de mensajes únicos. Para crear una directiva personalizada, debe conocer los requisitos y las limitaciones del entorno donde se aplicará la directiva de DLP. Encontrará más información en [Crear una nueva directiva de DLP personalizada](create-a-custom-dlp-policy-exchange-2013-help.md).

Una vez haya agregado una directiva, podrá revisar y modificar sus reglas, activarla o eliminarla completamente. Los procedimientos para estas acciones se encuentran en el tema [Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md).

## Tipos de información confidencial en las directivas de DLP

Cuando crea o modifica directivas de DLP, puede incluir reglas que incorporen comprobaciones de información confidencial. En el tema [Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) aparecen los tipos de información confidencial disponibles para utilizarse en sus directivas. Las condiciones establecidas en una directiva, como la cantidad de veces que algo debe suceder antes de tomar una medida o exactamente el tipo de medida, se pueden personalizar en las nuevas directivas para que así satisfagan sus requisitos específicos. Para obtener más información acerca de la creación de directivas de DLP, consulte [Crear una nueva directiva de DLP personalizada](create-a-custom-dlp-policy-exchange-2013-help.md). Para obtener más información acerca del paquete completo de reglas de transporte, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) o [Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)) (Exchange Online).

Para facilitar el uso de las reglas relacionadas con información confidencial, Microsoft le proporciona plantillas de directivas que ya incluyen algunos de los tipos de información confidencial. Sin embargo, no puede agregar condiciones para todos los tipos de información que figuran aquí en las plantillas de directivas, ya que las plantillas están diseñadas para ayudarlo a enfocarse en los tipos de datos relacionados con el cumplimiento más comunes dentro de su organización. Para obtener más información acerca de las plantillas pregeneradas, consulte [Plantillas de directivas de DLP suministradas en Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). Puede crear varias directivas de DLP para su organización y habilitarlas todas para que se examinen diferentes tipos de información. También puede crear una directiva de DLP que no esté basada en una plantilla existente. Para comenzar a crear una política de este tipo, consulte [Crear una nueva directiva de DLP personalizada](create-a-custom-dlp-policy-exchange-2013-help.md). Para obtener más información acerca de los tipos de información confidencial, consulte [Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

## Detección de datos de formulario confidenciales con la creación de huella digital de documento

Con Exchange 2013 SP1 y la versión más reciente de Exchange Online, puede usar [Creación de huella digital de documento](overview-of-document-fingerprinting-in-exchange.md) para crear fácilmente un tipo de información confidencial con base en un formulario estándar. Para aprender a proteger datos de formulario, consulte [Proteger los datos de formulario con huellas digitales de documentos](protect-form-data-with-document-fingerprinting-exchange-2013-help.md).

## Las Sugerencias de directivas notifican a los usuarios sobre las expectativas de contenido confidencial

Puede utilizar los mensajes de notificación de Sugerencias de directivas para informar a los destinatarios de correo electrónico sobre los posibles problemas de conformidad mientras generan un mensaje de correo electrónico. Al configurar una Sugerencia de directiva en una directiva de DLP, el mensaje de notificación únicamente aparecerá si hay algo en el mensaje del destinatario que cumpla las condiciones descritas en la directiva. Las Sugerencias de directivas son similares a las Sugerencias de correo que existen en Microsoft Exchange 2010. Para obtener más información, consulte [Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Detectar información confidencial junto con la clasificación tradicional de mensajes

Exchange 2013 y Exchange Online presentan un nuevo método de ayuda para administrar los datos de mensajes y datos adjuntos a la hora de compararlos con la clasificación tradicional de mensajes. Un factor clave de la fortaleza de una solución de DLP es la capacidad de identificar correctamente el contenido confidencial o delicado que puede ser exclusivo de una organización, las necesidades normativas, la geografía u otras necesidades empresariales. Exchange 2013 puede lograrlo a través de una nueva arquitectura para el análisis profundo de contenidos junto con los criterios de detección que establezca mediante reglas en las directivas de DLP. La prevención de pérdida de datos en Exchange 2013 se basa en la configuración del conjunto adecuado de reglas de información confidencial, de manera que puedan proporcionar un nivel alto de protección al mismo tiempo que minimizan las interrupciones inadecuadas del flujo de correo debido a falsos positivos y negativos. Este tipo de reglas, conocidas en el contexto de información de DLP como detección de información confidencial, funcionan en el marco que ofrecen las reglas de transporte para habilitar las funcionalidades de DLP.

Para obtener más información acerca de estas nuevas características, consulte [Integración de las reglas de información confidencial con las reglas de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md). Los campos tradicionales de clasificación de mensajes se puede seguir aplicando en los mensajes de Exchange y combinarse con la detección de nueva información confidencial en una única directiva de DLP o ejecutándolos concurrentemente para que sean analizados en Exchange de forma independiente. Para obtener más información sobre la clasificación de mensajes heredados de Exchange 2010, consulte la [descripción de las clasificaciones de mensajes](https://go.microsoft.com/fwlink/?linkid=266612) en la biblioteca de TechNet.

## Información acerca de los mensajes procesados por DLP

Para obtener información acerca de los mensajes y detecciones de directivas de DLP en su entorno de Exchange 2013, consulte [Ver informes de detección de directivas de DLP](view-dlp-policy-detection-reports-exchange-2013-help.md) y [Crear informes de incidentes para detecciones de directivas de DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md). Los datos relacionados con las detecciones de DLP están altamente integrados en la herramienta de seguimiento de mensajes de informes de entrega de Exchange 2013.

Para Exchange Online, vea [Ver informes de detección de directivas de DLP](https://technet.microsoft.com/es-es/library/dn904484\(v=exchg.150\)) y [Crear informes de incidentes para detecciones de directivas de DLP](https://technet.microsoft.com/es-es/library/dn904486\(v=exchg.150\)).

## Requisitos previos para la instalación

Para poder utilizar las características de DLP, debe tener Exchange 2013 o Exchange Online configurado con al menos un buzón de remitente. La prevención de pérdida de datos es una característica especial que requiere una Licencia de acceso de cliente (CAL) Enterprise. Para obtener más información acerca de cómo empezar a utilizar Exchange 2013, consulte [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md). Para obtener más información acerca de cómo empezar a utilizar Exchange Online, consulte [Exchange Online](https://technet.microsoft.com/es-es/library/jj200580\(v=exchg.150\)).

## Más información

Exchange 2013

  - [Directiva de mensajería y conformidad](messaging-policy-and-compliance-exchange-2013-help.md)

  - [Procedimientos de DLP](dlp-procedures-exchange-2013-help.md)

  - [Ver informes de detección de directivas de DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

  - [Creación de huella digital de documento](overview-of-document-fingerprinting-in-exchange.md)

  - [Cmdlets de directiva y conformidad](https://technet.microsoft.com/es-es/library/dd298082\(v=exchg.150\))

Exchange Online

  - [Seguridad y cumplimiento de Exchange Online](https://technet.microsoft.com/es-es/library/jj200706\(v=exchg.150\))

  - [Procedimientos de DLP](https://technet.microsoft.com/es-es/library/jj938003\(v=exchg.150\))

  - [Ver informes de detección de directivas de DLP](https://technet.microsoft.com/es-es/library/dn904484\(v=exchg.150\))

  - [Creación de huella digital de documento](overview-of-document-fingerprinting-in-exchange.md)

