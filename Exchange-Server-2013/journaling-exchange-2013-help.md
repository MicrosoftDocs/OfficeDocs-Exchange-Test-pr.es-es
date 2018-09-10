---
title: 'Registro en diario: Exchange 2013 Help'
TOCTitle: Registro en diario
ms:assetid: 6a20f207-4485-44ef-b010-ec760eb5165b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998649(v=EXCHG.150)
ms:contentKeyID: 49895685
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registro en diario

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

El registro en diario puede ayudar a la organización a responder a los requisitos de cumplimiento legal, normativo y organizativo mediante el registro de las comunicaciones de correo electrónico entrantes y salientes. Al planear la retención y el cumplimento normativo de mensajes, es importante comprender el registro en diario, cómo se ajusta a las directivas de cumplimiento normativo de la organización y cómo Microsoft Exchange Server 2013 ayuda a asegurar los mensajes registrados en diario.

**Contenido**

Why journaling is important

Journaling agent

Journal rules

Journal rule replication

Journal reports

Interoperability with Exchange 2010 and Exchange 2007

Troubleshooting

## ¿Por qué es importante el registro en diario?

En primer lugar, es importante comprender la diferencia entre el registro en diario y una estrategia de archivado de datos:

  - *Registro en diario* es la capacidad para registrar todas las comunicaciones, incluidos los correos electrónicos, de una organización que se van a utilizar en la retención de correo electrónico de la organización o en la estrategia de archivo. Para cumplir con un mayor número de requisitos reglamentarios y de cumplimiento normativo, muchas organizaciones llevan registros de la comunicación que tiene lugar cuando los empleados llevan a cabo tareas comerciales cotidianas.

  - *Archivado de datos* se refiere a la realización de copias de seguridad de los datos, eliminarlos de sus entornos nativos y almacenarlos en otro lugar, con lo que se reduce la carga de su almacenamiento. Puede usar el registro en diario de Exchange como herramienta en la retención de correo electrónico o como estrategia de archivado.

Aunque ninguna normativa específica requiere el registro en diario, es posible que sea necesario realizarlo a los fines del cumplimiento normativo de ciertas reglamentaciones. Por ejemplo, las autoridades de empresas de algunos sectores financieros pueden ser consideradas responsables de las alegaciones que sus empleados realicen a sus clientes. Para comprobar que las reclamaciones son precisas, el funcionario corporativo puede configurar un sistema en el que los administradores revisen regularmente parte de las comunicaciones empleado-a-cliente. Cada trimestre los administradores comprueban el cumplimiento y aprueban la conducta de los empleados. Una vez que todos los administradores informan de la aprobación al funcionario corporativo, éste informa del cumplimiento, en nombre de la empresa, al organismo regulador. En este ejemplo, los mensajes de correo electrónico pueden ser un tipo de comunicación de empleado a cliente que los administradores deben revisar; por tanto, el registro en diario se puede usar para recopilar todos los mensajes de correo electrónico que envían los empleados que tratan con los clientes. Otros mecanismos de comunicación con los clientes pueden incluir faxes y conversaciones telefónicas, que también pueden estar sujetas a la normativa. La posibilidad de registrar en el diario todas las clases de datos de una empresa es una funcionalidad importante de la arquitectura de TI.

En la lista siguiente se muestran algunas de las normativas estadounidenses e internacionales más conocidas en las que el registro en diario puede formar parte de las estrategias de cumplimiento normativo:

  - Sarbanes-Oxley Act of 2002 (SOX) (Ley Sarbanes-Oxley de 2002, SOX)

  - Security Exchange Commission Rule 17a-4 (SEC Rule 17 A-4) (Norma 17a-4 de la Security Exchange Commission, Norma 17 A-4 de la SEC)

  - National Association of Securities Dealers 3010 & 3110 (NASD 3010 & 3110) (Normas 3010 y 3110 de la Asociación Nacional de Corredores de Bolsa, Normas 3010 y 3110 de la NASD)

  - Gramm-Leach-Bliley Act (Financial Modernization Act) (Ley Gramm-Leach-Bliley, Ley de Modernización Financiera)

  - Financial Institution Privacy Protection Act of 2001 (Ley de Protección de la Privacidad en las Instituciones Financieras de 2003)

  - Financial Institution Privacy Protection Act of 2003 (Ley de Protección de la Privacidad en las Instituciones Financieras de 2003)

  - Health Insurance Portability and Accountability Act of 1996 (HIPAA) (Ley de Responsabilidad y Transferibilidad del Seguro Médico de 1996, HIPAA)

  - Uniting and Strengthening America by Providing Appropriate Tools Required to Intercept and Obstruct Terrorism Act of 2001 (Patriot Act) (Ley de Unidad y Fortalecimiento de los Estados Unidos de Norteamérica mediante el Suministro de las Herramientas Apropiadas para Interceptar y Obstruir el Terrorismo de 2001, Ley Patriota)

  - European Union Data Protection Directive (EUDPD) (Directiva de Protección de Datos de la Unión Europea, EUDPD)

  - Japan’s Personal Information Protection Act (Ley de Protección de la Información Personal de Japón)

Volver al principio

## Agente de registro en diario

En una organización de Exchange 2013, los servidores de buzones enrutan el tráfico de correo electrónico. Todos los mensajes recorren al menos un servidor que ejecuta el servicio de transporte durante su vigencia. El *agente de registro en diario* es un agente de transporte centrado en el cumplimiento que procesa los mensajes de los servidores de buzones. Se desencadena en los eventos de transporte **OnSubmittedMessage** y **OnRoutedMessage**.


> [!NOTE]
> En Exchange&nbsp;2013, el agente de registro en diario es un agente integrado. Los agentes integrados no están incluidos en la lista de agentes que devuelve el cmdlet <STRONG>Get-TransportAgent</STRONG>. Para obtener más información, consulte <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



Exchange 2013 proporciona las siguientes opciones de registro en diario:

  - **Registro en diario estándar**   Esta opción se configura en una base de datos de buzones de correo. Permite al agente de registro en diario registrar todos los mensajes enviados o recibidos a través de los buzones ubicados en una base de datos de buzones de correo. Para registrar en diario todos los mensajes enviados y recibidos por todos los destinatarios y remitentes, debe configurar el registro en diario para todas las bases de datos de buzones de todos los servidores de buzones de la organización.

  - **Registro en diario premium**   Esta opción le permite, al agente de registro en diario, realizar registros más individualizados, mediante el uso de reglas de diario. En lugar de registrar en diario todos los buzones de una base de datos, es posible configurar reglas de diario que concuerden con las necesidades de la organización, registrando en diario destinatarios o miembros de grupos de distribución individuales. Para usar registro en diario premium debe tener una licencia de acceso de cliente (CAL) de servidor empresarial de Exchange.

Cuando habilite el registro en diario estándar en una base de datos de buzones de correo, esta información se guarda en Active Directory y el agente de registro en diario se encarga de su lectura. De manera similar, las reglas de diario configuradas con el registro en diario premium también se guardan en Active Directory. El agente de registro en diario aplica dichas reglas. Para obtener más información sobre cómo configurar registros en diario Premium y estándar, consulte [Administrar registro en diario](https://docs.microsoft.com/es-es/exchange/security-and-compliance/journaling/manage-journaling).

Volver al principio

## Reglas de diario

Los siguientes son aspectos clave de las reglas del diario:

  - **Ámbito de regla de diario**   Define los mensajes que el agente de registro en diario va a registrar.

  - **Destinatario del diario**   Especifica la dirección SMTP del destinatario que desea registrar en diario.

  - **Buzón de registro en diario**   Especifica uno o más buzones que se usan para recopilar informes de diario.

## Ámbito de regla de diario

Puede usar una regla de diario para registrar en diario solo los mensajes internos, los mensajes externos, o ambos. En la lista siguiente se describen estos ámbitos:

  - **Solo mensajes internos**   Se trata de las reglas de diario que tienen el ámbito establecido en mensajes internos del diario enviados entre los destinatarios de la organización de Exchange.

  - **Solo mensajes externos**   Se trata de las reglas de diario que tienen el ámbito establecido en mensajes externos del diario enviados a destinatarios o recibidos de remitentes ubicados fuera de la organización de Exchange.

  - **Todos los mensajes**   Se trata de las reglas de diario que tienen el ámbito establecido en todos los mensajes del diario que pasan por la organización independientemente de su origen o destino. Incluyen mensajes que ya han procesado las reglas de diario en los ámbitos interno y externo.

## Destinatario del diario

Puede implementar reglas de diario orientadas especificando la dirección de SMTP del destinatario que desea registrar en diario. El destinatario puede ser un buzón de Exchange, un grupo de distribución, un usuario de correo o un contacto. Estos destinatarios pueden estar sujetos a requisitos de regulación o pueden estar implicados en procedimientos legales en los que los mensajes de correo electrónico u otras comunicaciones se recopilan como evidencia. La asignación de destinatarios específicos o grupos de destinatarios permite configurar fácilmente un entorno de registro de diario que coincida con los procesos de su organización y con los requisitos legales y normativos. Al seleccionar solo los destinatarios específicos que se deben registrar en diario, también se minimiza el almacenamiento y otros costes asociados a la retención de grandes cantidades de datos.

Se registrarán en diario todos los mensajes enviados o recibidos por los destinatarios que se hayan especificado en una regla de diario. Si especifica un grupo de distribución como destinatario del registro en diario, todos los mensajes enviados o recibidos por los miembros del grupo de distribución se registrarán en diario. Si no se especifica ningún destinatario, se registrarán en diario todos los mensajes enviados o recibidos por los destinatarios que estén dentro del alcance de la regla de diario.

**Destinatarios de diario con mensajería unificada habilitada**

Muchas organizaciones que implementan el registro en diario pueden usar también la mensajería unificada (MU) para consolidar su infraestructura de correo electrónico, correo de voz y fax. No obstante, es posible que no desee que el proceso de registro en diario genere informes de diario para los mensajes generados por la Mensajería unificada. En estos casos, también puede decidir si se van a registrar en diario los mensajes de correo de voz y de notificación de llamadas perdidas controlados por un servidor Exchange que ejecute el servicio de mensajería unificada, o bien si se van a omitir dichos mensajes. Si la organización no requiere el registro en diario de dichos mensajes, puede reducir la cantidad de espacio de disco duro requerido para almacenar los informes de diario omitiendo tales mensajes.


> [!NOTE]
> Los mensajes que contienen faxes generados por el servicio de mensajería unificada siempre se registran en diario, incluso si se deshabilita el registro en diario del correo de voz de mensajería unificada o los mensajes de notificación de llamadas perdidas.



Para obtener más información sobre cómo habilitar o deshabilitar los mensajes de correo de voz y de notificaciones de llamadas perdidas, consulte [Deshabilitar o habilitar el registro en diario de correo de voz y notificaciones de llamadas perdidas](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md).

## Buzones de registro en diario

El buzón de correo de registro en diario se usa para recopilar informes de diario. La manera en que configure este buzón de correo de registro en diario depende de las directivas de la organización y de los requisitos legales y normativos. Puede especificar un buzón de correo de registro en diario para reunir los mensajes de todas las reglas de diario configuradas en la organización, o puede usar buzones distintos para reglas de diario o grupos de reglas de diario distintos.


> [!IMPORTANT]
> Office&nbsp;365 no se puede designar como buzón de registro en diario. Se pueden entregar informes de registro en diario a un sistema de archivado local o a un servicio de archivado de terceros. Si va a ejecutar una implementación híbrida con buzones divididos entre los servidores locales y Office&nbsp;365, puede designar un buzón local como el buzón de registro en diario para los buzones locales y de Office 365.




> [!IMPORTANT]
> Los buzones de registro en diario contienen información muy confidencial. Debe proteger los buzones de registro en diario porque recopilan mensajes que se envían a y desde destinatarios de su organización. Estos mensajes pueden formar parte de procedimientos legales o estar sujetos a requisitos normativos. Hay varias leyes que requieren que los mensajes permanezcan sin manipulación antes de que se envíen a una autoridad de investigación. Le recomendamos que cree directivas que regulen quién puede obtener acceso a los buzones de registro en diario de su organización, limitando el acceso únicamente a aquellas personas que tengan necesidad directa de obtener acceso a ellos. Consulte con los representantes legales para asegurarse de que la solución de registro en diario cumple con todas las leyes y normativas que se aplican a la organización.




> [!IMPORTANT]
> Los buzones de correo de registro en diario deben aceptar mensajes hasta un tamaño igual o mayor que el tamaño máximo para mensajes que haya establecido en la organización. Si ha configurado excepciones en los parámetros MaxSendSize y MaxReceiveSize en el buzón de un usuario individual mayores que la configuración general de TransportConfig, debe establecer los parámetros MaxSendSize y MaxReceiveSize del buzón de correo de registro en diario en consecuencia para asegurarse de que los mensajes enviados al registro en diario se aceptan y no se ponen en cola o se rechazan. Los mensajes rechazados por el buzón de correo de registro en diario se intentan de nuevo periódicamente, lo que provoca el crecimiento innecesario de la base de datos y que se malgasten recursos. Además, se recomienda que configure un buzón de correo de registro en diario alternativo para evitar que se produzcan otras situaciones de no entrega.



## Buzón de registro en diario alternativo

Cuando el buzón de registro en diario no está disponible, quizá no desee que los informes de diario no entregados se acumulen en colas de correo en los servidores de buzones. Si es así, puede configurar un buzón alternativo para registro en diario donde recopilar estos informes de diario. El buzón alternativo para registro en diario recibe los informes diarios como archivos adjuntos en los informes de no entrega (NDR) generados cuando el buzón de registro en diario o el servidor que contiene dicho buzón deniega la entrega del informe de diario o deja de estar disponible.

Cuando un buzón de registro en diario vuelva a estar disponible, puede utilizar la característica **Enviar de nuevo** de OfficeOutlook para reenviar los informes de diario y entregarlos al buzón de registro en diario.

Si configura un buzón de registro en diario alternativo, todos los informes de diario rechazados o que no se pueden entregar de toda la organización de Exchange se entregarán al buzón de registro en diario alternativo. Por lo tanto, es importante asegurarse de que el buzón alternativo para registro en diario y el servidor de buzones en el que se encuentra puedan hacer frente a una gran cantidad de informes de diario.


> [!WARNING]
> Si configura un buzón de registro en diario alternativo, debe supervisarlo para asegurarse de que no deje de estar disponible al mismo tiempo que los buzones de diario. Si el buzón de registro en diario alternativo deja de estar disponible o rechaza los informes de diario, los informes de diario rechazados se pierden y no pueden recuperarse.



Dado que el buzón de registro en diario alternativo recopila todos los informes de diario rechazados de toda la organización de Exchange, debe asegurarse de que no se infrinja ninguna ley ni la reglamentación que se aplique a la organización. Si las leyes o la reglamentación prohíben a la organización almacenar los informes de diario enviados a distintos buzones de registro en diario en el mismo buzón alternativo para registro en diario, no podrá configurar un buzón alternativo para registro en diario. Consulte a sus representantes legales para saber si puede utilizar un buzón alternativo para registro en diario.

Cuando se configura el buzón para registro en diario alternativo, es conveniente aplicar los mismos criterios de configuración del buzón de registro en diario.


> [!IMPORTANT]
> El buzón de registro alternativo debe tratarse como un buzón dedicado especial. Los mensajes dirigidos directamente al buzón de correo diario alternativo no se registran en el diario.



Volver al principio

## Replicación de reglas de diario

Las reglas de diario se almacenan en Active Directory y todos los servidores de buzones se encargan de aplicarlas en la organización de Exchange 2013. Cuando se crea, modifica o elimina una regla de diario, el cambio se replica en todos los servidores de Active Directory de la organización. Luego, todos los servidores de buzones de la organización recuperan la configuración de reglas de diario actualizada de los servidores de Active Directory y aplican las reglas nuevas o modificadas.

Al replicar todas las reglas de diario en toda la organización, Exchange 2013 le permite proporcionar un conjunto coherente de reglas de diario en toda la organización. Todos los mensajes que pasan a través de la organización de Exchange 2013 están sujetos a las mismas reglas de diario.


> [!IMPORTANT]
> La replicación de las reglas de diario a través de una organización depende de replicación Active Directory. Tiempo de replicación entre controladores de dominio de Active Directory varía según el número de sitios en la organización y la velocidad de los vínculos y otros factores fuera del control del Microsoft Exchange. Tener en cuenta retrasos de replicación al implementar las reglas de diario en la organización. Para obtener más información acerca de la replicación de Active Directory, consulte <A href="https://go.microsoft.com/fwlink/?linkid=274904">Introducción a la replicación de Active Directory y utilizar Windows PowerShell de administración de topología</A>.




> [!IMPORTANT]
> Todos los servidores de buzones almacenan en caché la pertenencia a un grupo de distribución para evitar idas y vueltas repetidas a Active Directory. La memoria caché de grupos expandida reduce el número de solicitudes que cada servidor de buzones debe hacer a un controlador de dominio de Active Directory. De forma predeterminada, las entradas en la memoria caché de grupos expandida expiran en cuatro horas. Por lo tanto, si especifica un grupo de distribución como destinatario del diario, es posible que los cambios en la pertenencia al grupo de distribución no se apliquen a las reglas de diario, hasta que se actualice la memoria caché de grupos expandida. Para forzar una actualización inmediata de la memoria caché de destinatarios, debe detener e iniciar el servicio de transporte de Microsoft Exchange. Debe hacer esto para cada servidor de buzones donde quiera actualizar forzadamente el caché de destinatario.



Volver al principio

## Informes de diario

Un *informe de diario* es el mensaje que genera el agente de registro en diario cuando un mensaje coincide con una regla de diario y debe enviarse al buzón de correo de registro en diario. El mensaje original que coincide con la regla de diario se incluye sin alteraciones como un dato adjunto al informe de diario. El cuerpo de un informe de diario contiene información acerca del mensaje original, como la dirección de correo electrónico del remitente, el asunto, el id. del mensaje y las direcciones de correo electrónico de los destinatarios. Esto también se conoce como registro de sobres en diario, y es el único método de registro en diario compatible con Exchange 2013.

## Informes de diario y mensajes protegidos por IRM

Al implementar el registro en diario en un entorno de Exchange 2013, es necesario tener en cuenta los informes de diario y los mensajes protegidos por IRM. Estos mensajes afectan las capacidades de búsqueda y detección de aquellos sistemas de archivado de otros fabricantes que no tienen compatibilidad con RMS integrada. En Exchange 2013, es posible configurar el descifrado de informes de diarios para guardar una copia sin cifrar del texto del mensaje en un informe de diario.

Volver al principio

## Interoperabilidad con Exchange 2007

No existen grandes diferencias entre la función de registro en diario en Exchange 2013, Exchange 2010 y Exchange 2007. No obstante, el programa de instalación de Exchange 2010 y versiones posteriores crea un contenedor independiente en Active Directory para almacenar las reglas de diario. Al instalar el primer servidor Exchange 2010 o una versión posterior en una organización de Exchange 2007, el programa de instalación crea una copia de las reglas de diario existentes en Exchange 2007 y las almacena en el contenedor nuevo. Una vez que se completa el proceso de instalación, las reglas de diario de ambas versiones de Exchange mantienen coherencia.

Una vez completada la instalación, si cambia la configuración de las reglas de diario en Exchange 2010 (o una versión posterior), deberá realizar el mismo cambio en los servidores Exchange 2007 para garantizar que sean coherentes. Del mismo modo, los cambios realizados en las reglas de diario en Exchange 2007 también deben realizarse en Exchange 2010 o versiones posteriores. También puede exportar las reglas de diario de Exchange 2007 e importarlas en Exchange 2013.

Volver al principio

## Solución de problemas

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351). Si tiene problemas con el buzón **JournalingReportDNRTo**, vea [Las reglas de transporte y buzón de correo en Exchange Online no funcionan como se esperaba](https://go.microsoft.com/fwlink/p/?linkid=331674).

