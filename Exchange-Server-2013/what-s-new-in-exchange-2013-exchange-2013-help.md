---
title: 'Novedades en Exchange 2013: Exchange 2013 Help'
TOCTitle: Novedades en Exchange 2013
ms:assetid: 97501135-2149-4590-8373-98e638ac8eb1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150540(v=EXCHG.150)
ms:contentKeyID: 48268456
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Novedades en Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Consulte las funcionalidades más recientes en Exchange 2013.

Microsoft Exchange Server 2013 ofrece un amplio y nuevo conjunto de tecnologías, funciones y servicios para la línea de productos de Exchange Server. Su objetivo es ayudar a las personas y organizaciones en la evolución de sus hábitos de trabajo de un enfoque basado en la comunicación a un enfoque colaborativo. Al mismo tiempo, Exchange Server 2013 ayuda a reducir el costo total de propiedad ya sea que implemente Exchange 2013 en forma local o realice el aprovisionamiento de los buzones en la nube. Las nuevas funciones y características de Exchange 2013 están pensadas para hacer lo siguiente:

  - **Compatibilidad con personal multigeneracional** la integración social y la simplificación de la búsqueda de personas son fundamentales para los usuarios. *Búsqueda Inteligente* aprende de los usuarios comportamientos de comunicación y colaboración para mejorar y dar prioridad a resultados de búsqueda de Exchange. Asimismo, con Exchange 2013 los usuarios pueden fusionar contactos de múltiples fuentes para proporcionar una vista única de una persona, enlazando información de contacto tomada de múltiples ubicaciones.

  - **Proporcionar una experiencia atractiva**   Microsoft Outlook 2013 y Microsoft Outlook Web App tienen un aspecto renovado. Outlook Web App pone énfasis en una interfaz de usuario eficaz que también admite el uso de capacidades táctiles, mejorando la experiencia en dispositivos móviles con Exchange.

  - **Integración con SharePoint y Lync**   Exchange 2013 ofrece mayor integración con Microsoft SharePoint 2013 y Microsoft Lync 2013 a través de buzones del sitio y exhibición de documentos electrónicos local. Juntos, estos productos ofrecen un conjunto de características que posibilitan situaciones como la exhibición de documentos electrónicos de empresas y la colaboración mediante buzones de sitio.

  - **Ayuda a adaptarse a los constantes cambios en las necesidades de cumplimiento normativo**    El cumplimiento y la exhibición de documentos electrónicos suponen un reto para muchas organizaciones. Exchange 2013 le ayuda a buscar y encontrar datos no solo en Exchange, sino en toda la organización. Con funciones mejoradas de búsqueda e indexado, puede realizar búsquedas en Exchange 2013, Lync 2013, SharePoint 2013, y servidores de archivos de Windows. Además, la prevención de pérdida de datos (DLP) también puede ayudar a proteger a la organización de usuarios que por error envíen información confidencial a personas no autorizadas. DLP le ayuda a identificar, supervisar y proteger datos sensibles gracias a un análisis de contenidos más pormenorizado.

  - **Proporcionar una solución resistente**   Exchange 2013 se basa en la arquitectura de Exchange Server 2010 y ha sido rediseñada para proporcionar mayor sencillez de escala, utilización de hardware y aislamiento de errores.

Para obtener información acerca de los cambios realizados a Exchange Server 2013 desde la versión RTM, consulte [Actualizaciones para Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

Consulte las siguientes secciones para ampliar información sobre las novedades de Exchange 2013:

Centro de administración de Exchange

Arquitectura de Exchange 2013

Configuración

Directiva de mensajería y conformidad

Protección contra malware

Flujo de correo

Destinatarios

Uso compartido y colaboración

Integración con SharePoint y Lync

Clientes y móvil

Mensajería unificada

Buzón de lote se mueve

[Alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-exchange-2013-help.md)

Administración de carga de trabajo de Exchange


> [!NOTE]
> Si desea información sobre nuevas características de versiones anteriores de Exchange que han sido eliminadas, suspendidas o sustituidas en Exchange Server 2013, consulte <A href="what-s-discontinued-in-exchange-2013-exchange-2013-help.md">Qué se ha discontinuado en Exchange 2013</A>. También le puede interesar <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de la versión de Exchange&nbsp;2013</A>.



## Centro de administración de Exchange

Exchange 2013 ofrece una consola de administración unificada exclusiva que brinda facilidad de uso y está optimizada para gestionar implementaciones locales, en línea o híbridas. El *Centro de administración de Exchange* (EAC) en Exchange 2013 sustituye a la Consola de administración (EMC) de Exchange 2010 y al Panel de control de Exchange (ECP). (Sin embargo, “ECP” sigue siendo el nombre del directorio virtual que se utiliza en el EAC.) Algunas características del EAC incluyen:

  - **Vista de lista** La vista de lista de EAC se ha diseñado para eliminar las limitaciones que existían en ECP. ECP tenía la limitación de mostrar un máximo de 500 objetos y si deseaba ver los objetos que no estaban en la lista del panel de detalles, tenía que usar la búsqueda y el filtrado para encontrar esos objetos específicos. En Exchange 2013, el límite de visualización desde el interior de la vista de lista de EAC es de aproximadamente 20 000 objetos. Cuando el EAC devuelve los resultados, el cliente de EAC realiza la búsqueda y la ordenación, que incrementan considerablemente el rendimiento en comparación con el ECP en Exchange 2010. Además, se ha añadido la paginación para que pueda paginar los resultados. También puede configurar el tamaño de página y exportar a un archivo .csv.

  - **Añadir/quitar columnas en la vista de lista de destinatarios**   Puede elegir qué columnas desea ver, y con las cookies locales puede guardar sus vistas de lista personalizadas en función de la máquina que utilice para acceder al EAC.

  - **Proteger el directorio virtual ECP**   Puede dividir el acceso desde Internet e intranets en el directorio virtual ECP de IIS para permitir o no permitir las características de administración. Con esta característica, podrá conceder o denegar acceso a los usuarios que intentan acceder al EAC desde Internet, fuera del entorno de su organización y, a la vez, conceder acceso a las opciones de Outlook Web App de un usuario final.

  - **Administración de carpeta pública**   En Exchange 2010 y Exchange 2007, las carpetas públicas se administraban desde la consola de administración de carpetas públicas. Las carpetas públicas están ahora en el EAC y no necesitará usar una herramienta independiente para su administración.

  - **Notificaciones**   EnExchange 2013, el EAC tiene ahora un visor de Notificaciones para que pueda ver el estado de los procesos de ejecución prolongada y, si lo elije, recibirá la notificación mediante un mensaje de correo electrónico cuando finalice el proceso.

  - **Editor de usuarios de control de acceso basado en funciones (RBAC)**   En Exchange 2010, podía usar el Editor de usuarios RBAC del cuadro de herramientas Exchange para añadir usuarios a grupos de roles de administración. En Exchange 2013, la función del Editor de usuarios RBAC se ubica en el EAC, por lo que no necesita una herramienta distinta para gestionar RBAC.

  - **Herramientas de mensajería unificada**   En Exchange 2010, podía utilizar las herramientas de estadísticas de llamadas y los registros de llamadas de usuario para ayudar a proporcionar estadísticas e información de mensajería unificada acerca de llamadas concretas de un usuario habilitado para mensajería unificada. En Exchange 2013, las herramientas estadísticas de llamadas y registros de llamadas de usuario se ubican en el EAC, por lo que no necesita una herramienta distinta para gestionarlas.

  - **Mejoras de grupos:** el Centro de administración de Exchange (EAC) ahora puede mostrar hasta 10.000 destinatarios en la ventana **GruposSeleccionar miembros**. De manera predeterminada, se devuelven hasta 500 destinatarios cuando se abre la ventana **Seleccionar miembros**. Sin embargo, puede optar por que aparezcan hasta 10.000 destinatarios si hace clic en **Obtener todos los resultados** debajo de la lista de destinatarios. Ahora admitimos la búsqueda de más de 500 destinatarios mediante la barra de desplazamiento y también hemos agregado características de búsqueda mejorada para permitir el filtrado de los destinatarios que aparecen en la lista de destinatarios. Se puede filtrar por:
    
      - ciudad
    
      - empresa
    
      - país o región
    
      - departamento
    
      - oficina
    
      - cargo

Para obtener más información, consulte [Centro de administración de Exchange en Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

## Arquitectura de Exchange 2013

Las versiones anteriores de Exchange se optimizaron y diseñaron con ciertas restricciones tecnológicas existentes en ese momento. Por ejemplo, durante el desarrollo de Exchange 2007, una de las restricciones clave era el rendimiento del CPU. Para aliviar esta restricción, Exchange 2007 se dividió en diferentes funciones de servidor que permitían el escalamiento mediante la separación de servidores. Sin embargo, las funciones de servidor en Exchange 2007 y Exchange 2010 se combinaron muy bien. El acoplamiento compacto de las funciones tuvo varios inconvenientes, como dependencia de versión, afinidad geográfica (se requieren todas las funciones en un sitio específico), afinidad de sesión (se requiere un costoso equilibrio de carga de hardware de 7 capas) y complejidad de espacio de nombres.

Actualmente, la potencia del CPU es significativamente menos costosa y ya no representa un factor restrictivo. Sin dicha restricción, el principal objetivo de diseño de Exchange 2013 es la simplicidad de escala, la utilización de hardware y el aislamiento de errores. Con Exchange 2013, hemos reducido el número de roles de servidor a tres: los roles de servidor de acceso de cliente, buzón de correo y transporte perimetral.

El servidor de buzones incluye todos los componentes de servidor habituales incluidos en Exchange 2010: los protocolos de acceso de clientes, el servicio de transporte, las bases de datos de buzones y la mensajería unificada. El servidor de buzones administra la actividad de los buzones activos de ese servidor. El servidor Acceso de clientes proporciona servicios de autenticación, redireccionamiento limitado y proxy. El servidor de acceso de clientes como tal no realiza ninguna representación de datos. El servidor Acceso de clientes es un servidor fino y sin estado. Nunca se encuentra nada en cola o almacenado en el servidor Acceso de clientes. El servidor de acceso de clientes ofrece todos los protocolos de acceso de clientes habituales: HTTP, POP e IMAP y SMTP.

Con esta nueva arquitectura, el servidor acceso de clientes y el servidor buzón de correo se han "acoplado libremente". Todo el procesamiento y actividad de un buzón concreto se realiza en el servidor de buzón de correo que aloja la copia de la base de datos activa en la que reside dicho buzón. Toda la representación y transformación de datos se lleva a cabo a escala local en la copia de la base de datos activa, lo que elimina los problemas de compatibilidad de versiones entre el servidor de acceso de clientes y el servidor de buzón de correo.

Con Exchange 2013 Service Pack 1, hemos introducido de nuevo el rol de servidor de transporte perimetral. El rol de transporte perimetral se implementa normalmente en la red perimetral, fuera del bosque interno de Active Directory y está diseñado para minimizar la superficie de ataque de la implementación de Exchange. Controlando todo el flujo de correo orientado a Internet, también agrega capas adicionales de protección de mensajes y seguridad contra los virus y correo no deseado, y puede aplicar reglas de transporte para controlar el flujo de mensajes. Para obtener más información acerca del rol del servidor Transporte perimetral, consulte [Servidores de transporte perimetral](edge-transport-servers-exchange-2013-help.md).

La arquitectura de Exchange 2013 ofrece las siguientes ventajas:

  - **Flexibilidad de actualización de versión** No más rígidos requisitos de actualización. Un servidor Acceso de clientes puede actualizarse de forma independiente y en cualquier orden en relación con el servidor Buzón de correo.

  - **Indiferencia de sesión**   Con Exchange 2010, la afinidad de sesión con la función de servidor acceso de clientes era necesaria para varios protocolos. En Exchange 2013, los componentes de buzón de correo y acceso de clientes residirán en el mismo servidor Buzón de correo. Pero como el servidor de acceso de clientes simplemente pone en proxy todas las conexiones de un usuario en un servidor concreto de buzón de correo, no es necesario disponer de afinidad de sesiones en los servidores de acceso de clientes. Esto permite que las conexiones entrantes en los servidores de acceso de clientes se carguen usando tecnología de equilibrio de la carga como menos conexiones o round-robin.

  - **Simplicidad de implementación**   Con un diseño de resistencia de sitios de Exchange 2010, se precisaban hasta ocho espacios de nombres diferentes: dos espacios de nombres de Protocolo de Internet, dos para reserva de Outlook Web App, uno para Autodiscover, dos para acceso de clientes RPC y uno para SMTP. También era necesario contar con un espacio de nombre si actualizaba desde Exchange 2003 o Exchange 2007. Con Exchange 2013, el número mínimo de espacios de nombre disminuye a dos. Si coexiste con Exchange 2007, seguirá necesitando crear un nombre de host heredado, pero si coexiste con Exchange 2010 o instala una nueva organización de Exchange 2013, el número mínimo de espacios de nombre que necesita es de dos: uno para protocolos de cliente y otro para la detección automática. Puede que también necesite un espacio de nombres SMTP.

Como resultado de estos cambios arquitectónicos, ha habido ciertos cambios en la conectividad del cliente. En primer lugar, RPC ya no es un protocolo de acceso directo compatible. Esto significa que la conectividad de Outlook en su totalidad debe realizarse utilizando RPC mediante HTTP (también conocido como Outlook Anywhere). A primera vista, esto puede parecer una limitación pero en realidad tiene ciertos beneficios agregados. El beneficio más obvio es que no hay necesidad de tener el servicio de acceso de clientes de RPC en el servidor Acceso de clientes. Esto ocasiona la reducción de dos espacios de nombres que habitualmente se necesitarían para una solución de resistencia de sitios. Asimismo, ya no hay requerimientos para suministrar afinidad para el servicio de acceso de clientes de RPC.

En segundo lugar, los clientes de Outlook ya no se conectarán a un servidor FQDN como lo hacían en todas las versiones anteriores de Exchange. Outlook emplea Autodiscover para crear un nuevo punto de conexión compuesto por mailbox GUID, el símbolo @ y la parte de dominio de la dirección SMTP principal del usuario. Este sencillo cambio da como resultado la práctica eliminación del inoportuno mensaje "Su administrador ha realizado un cambio en su buzón de correo. Reinicie." Solamente Outlook 2007 y las versiones posteriores serán compatibles con Exchange 2013.

El modelo de alta disponibilidad del componente de buzón no ha cambiado significativamente desde Exchange 2010. La unidad de alta disponibilidad continúa siendo el grupo de disponibilidad de base de datos (DAG). El DAG aún utiliza clústeres de conmutación por error de Windows Server. La replicación continua todavía admite tanto replicación de modo de bloqueo y modo de archivo. Sin embargo, se han producido algunas mejoras. Los tiempos de conmutación por error se redujeron como resultado de las mejoras en el código de registro de transacciones y punto de comprobación más profundo en las bases de datos pasivas. El servicio de almacén de Exchange ha sido reescrito en código administrado (véase la sección "Almacén administrado" más adelante en este tema). Ahora cada base de datos se ejecuta bajo su propio proceso y permite el aislamiento de problemas de almacén en una única base de datos.

## Almacén administrado

En Exchange 2013, el *Almacén administrado* es el nombre de procesos de almacén de información recientemente reescritos Microsoft.Exchange.Store.Service.exe y Microsoft.Exchange.Store.Worker.exe. El nuevo Almacén administrado ha sido escrito en C\# y presenta una integración estrecha con el servicio de replicación de Microsoft Exchange (MSExchangeRepl.exe) para proporcionar una elevada disponibilidad gracias a una mayor resistencia. Asimismo, el almacén administrado se ha diseñado para permitir una administración más granular del consumo de recursos y un análisis de causa raíz más rápido mediante un diagnóstico mejorado.

El almacén administrado funciona con el servicio de replicación de Microsoft Exchange para administrar bases de datos de buzones de correo, que sigue usando el Motor de almacenamiento extensible (ESE) como motor de la base de datos. Exchange 2013 incluye cambios significativos en el esquema de la base de datos de buzones, que ofrecen muchas optimizaciones respecto de las versiones anteriores de Exchange. Además de estos cambios, el servicio de replicación de Microsoft Exchange es responsable de la disponibilidad de servicio completa en relación con servidores de buzón de correo. Los cambios de arquitectura permiten una conmutación por error de bases de datos más rápida y una mejor administración de errores de disco físico.

El almacén administrado también está integrado en el motor de búsqueda Search Foundation (el mismo motor de búsqueda usado por SharePoint 2013) para suministrar mayor solidez en la indización y búsqueda en comparación con Microsoft Search en las versiones anteriores de Exchange.

Para obtener más información, consulte [Alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-exchange-2013-help.md).

## Administración de certificados

La administración de certificados digitales es una de las tareas relacionadas con la seguridad más importantes de su organización de Exchange. Asegurar que los certificados estén correctamente configurados es fundamental para suministrar una infraestructura de mensajería segura para la empresa. En Exchange 2010, la consola de administración de Exchange era el método principal de administración de certificados. En Exchange 2013, la función de administración de certificados está suministrada por el Centro de administración de Exchange (EAC), la nueva interfaz de usuario del administrador de Exchange 2013.

El trabajo en los certificados relacionados con Exchange 2013 se centró en minimizar el número de certificados que un administrador debe administrar, minimizar la interacción que debe tener el administrador con los certificados y permitir la administración de certificados desde una ubicación central. Los beneficios obtenidos a partir de los cambios en la administración de certificados son:

  - La administración de certificados puede realizarse en un servidor de acceso de clientes o en el servidor de buzón de correo. El servidor de buzón tiene un certificado autofirmado instalado por defecto. El servidor de acceso de clientes automáticamente confía el certificado autofirmado en el servidor buzón de correo de Exchange 2013 de modo que los clientes no reciban advertencias acerca de un certificado autofirmado que no es de confianza siempre que el servidor acceso de clientes de Exchange 2013 tenga un certificado no autofirmado de una entidad de certificación (AC) de Windows o un tercero de confianza.

  - En versiones anteriores de Exchange, era difícil ver cuándo un certificado digital estaba a punto de expirar. En Exchange 2013, el centro de notificaciones mostrará advertencias cuando un certificado almacenado en cualquier servidor de Exchange 2013 esté a punto de expirar. Los administradores también pueden elegir recibir estas notificaciones por correo electrónico.

Para obtener más información, consulte [Certificados digitales y SSL](digital-certificates-and-ssl-exchange-2013-help.md).

## Programa de instalación

Se ha rescrito completamente el programa de instalación para que sea más sencillo que nunca instalar Exchange 2013 y asegurarse de que se dispone de los últimos paquetes acumulativos y actualizaciones de seguridad del producto. Aquí están algunas de las mejoras que hemos hecho:

  - **Programa de instalación siempre actualizado**   Cuando ejecuta el asistente del programa de instalación, se le dará la opción de descargar y usar los últimos paquetes acumulativos y actualizaciones de seguridad del producto, además de los paquetes de idiomas. Esta opción no solo actualiza los archivos que se utilizarán para ejecutar Exchange; El propio programa de instalación puede actualizarse por sí solo. Este diseño nos permite seguir mejorando el programa de instalación en un momento posterior a su lanzamiento e incluir comprobaciones de disponibilidad de las actualizaciones, a medida que se actualizan o modifican los requisitos.
    
    Si está utilizando el modo de instalación desatendida, no podemos descargar automáticamente actualizaciones. No obstante, puede seguir beneficiándose de ejecutar la última versión del programa de instalación descargando de antemano las últimas actualizaciones, y usar el parámetro `/UpdatesDir: <path>` para permitir que el programa de instalación se actualice antes de que dé comienzo el proceso de instalación.

  - **Comprobaciones mejoradas de disponibilidad**   Las comprobaciones de disponibilidad garantizan que su equipo y su organización están preparados para Exchange 2013. Una vez que le proporcionemos la información necesaria sobre instalación para ejecutar el programa de instalación, se ejecutan las comprobaciones de disponibilidad antes de que dé comienzo la instalación. El nuevo motor de comprobación de la disponibilidad ahora ejecuta todas las comprobaciones antes de informarle sobre las acciones que debe llevar a cabo antes de que el programa de instalación continúe, y lo hace más rápido que nunca. Como ocurre con versiones anteriores de Exchange, puede indicar al programa de instalación que instale las características de Windows requeridas por el programa de instalación, de manera que no tenga que instalarlas manualmente.

  - **Asistente simplificado y moderno**   Hemos eliminado todos los pasos del asistente del programa de instalación que no son absolutamente necesarias para que instale Exchange. Hemos dejado un asistente fácil de seguir que le guía durante todo el proceso de instalación, paso a paso.

Para obtener más información, consulte [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Directiva de mensajería y conformidad

Hay dos nuevas características de cumplimiento normativo y regulación de mensajes en Exchange 2013: prevención de pérdida de datos y el conector Microsoft Rights Management.

Las funcionalidades de *prevención de pérdida de datos* (DLP) ayudan a proteger los datos confidenciales y a informar a los usuarios de las políticas internas de cumplimiento normativo. DLP también puede proteger la organización frente a los usuarios que puedan enviar por error información confidencial a personas no autorizadas. DLP le ayuda a identificar, supervisar y proteger los datos confidenciales mediante un profundo análisis del contenido. Exchange 2013 ofrece directivas de DLP integradas que se basan en las normas de regulación, tales como las normas de información personal identificable (PII) y las normas de seguridad de datos del sector de tarjetas de pago (PCI), y se amplían para admitir otras directivas que sean de importancia para la empresa. Además, la nueva característica PolicyTips de Outlook 2013 informa a los usuarios en cuanto a violaciones de las directivas antes de que se envíen datos confidenciales.

El conector Microsoft Rights Management (conector RMS) es una aplicación opcional que mejora la protección de datos del servidor Exchange 2013 conectándose a servicios de Microsoft Rights Management basados en la nube. Una vez instalado, el conector RMS proporciona protección de datos continua mientras dure la información y, como estos servicios son personalizables, puede definir el nivel de protección que necesita. Por ejemplo, puede limitar el acceso a los mensajes de correo electrónico a determinados usuarios o establecer permisos de solo vista en ciertos mensajes.

Para más información sobre estas características, consulte:

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Conector Rights Management](https://go.microsoft.com/fwlink/p/?linkid=330432)

## Archivo, retención y exhibición de documentos electrónicos locales

Exchange 2013 incluye las siguientes mejoras en el archivo, retención y exhibición de documentos electrónicos locales para ayudar a su organización a satisfacer sus necesidades de cumplimiento:

  - **Retención local**   La retención local es un nuevo modelo de retención que le permite satisfacer requisitos legales en las siguientes situaciones:
    
      - Preservar los resultados de la consulta (retención basada en consulta), que permite la inmutabilidad de ámbito entre buzones de correo.
    
      - Colocar una retención basada en tiempo para satisfacer los requisitos de retención (por ejemplo, retener todos los elementos de un buzón durante siete años, una situación que exigía el uso de recuperación de un solo elemento/retención de elementos eliminados en Exchange 2010).
    
      - Colocar un buzón de correo en retención indefinida (similar a retención por juicio en Exchange 2010).
    
      - Colocar un usuario en varias retenciones para cumplir diversos requisitos de casos.

  - **Exhibición de documentos electrónicos local**   la exhibición de documentos electrónicos local autoriza a los usuarios a buscar datos de buzón de correo en todos los buzones de correo y archivos locales de una organización Exchange 2013 y copiar mensajes en un buzón de detección para su revisión. En Exchange 2013, la exhibición de documentos electrónicos local ha sido mejorada para permitir que los administradores de detección realicen búsquedas y retenciones con más eficacia. Entre estas mejoras se incluyen:
    
      - **Búsqueda federada** le permite buscar y conservar datos en múltiples repositorios de datos. Con Exchange 2013, puede realizar búsquedas de Exhibición de documentos electrónicos local en Exchange, SharePoint 2013, y Lync 2013. Puede utilizar el Centro de exhibición de documentos electrónicos en SharePoint 2013 para realizar búsquedas y retenciones de exhibición de documentos electrónicos local.
    
      - **La retención local basada en consultas** le permite mantener los resultados de la consulta, lo que permite la inmutabilidad de ámbito entre buzones de correo.
    
      - **Exportar resultados de búsqueda** Los administradores de detección pueden exportar contenidos del buzón de correo a un archivo .pst desde la Consola de detección de SharePoint 2013. Los cmdlets de solicitud de exportación de buzón de correo ya no son necesarios para exportar un buzón de correo a un archivo .pst.
    
      - **Estadísticas de palabras clave** Se ofrecen estadísticas de búsqueda según el término de búsqueda. Esto permite al administrador de detección tomar rápidamente decisiones inteligentes sobre cómo refinar aún más la consulta de búsqueda para ofrecer mejores resultados. Los resultados de búsqueda de eDiscovery se ordenan por relevancia.
    
      - **Sintaxis KQL** Los administradores de detección pueden utilizar la sintaxis del lenguaje de consulta de palabras clave (KQL) en las consultas de búsqueda. KQL es similar a la Sintaxis de consulta avanzada (AQS), que se utilizaba para realizar búsquedas de detección en Exchange 2010.
    
      - **Asistente de retención y exhibición de documentos electrónicos**   Los administradores de detección pueden utilizar el nuevo asistente de retención y exhibición de documentos electrónicos local para realizar operaciones de exhibición de documentos electrónicos y retención.
        

        > [!NOTE]
        > Si SharePoint 2013 no está disponible, hay un subconjunto de funciones de exhibición de documentos electrónicos disponibles en el Centro de administración de Exchange.



  - **Buscar en buzones principales y de archivo en Outlook Web App** Los usuarios pueden buscar en buzones principales y de archivo en Outlook Web App. Dos búsquedas independientes ya no son necesarias.

  - **Contenido de Archive Lync**   Exchange 2013 admite el archivo de contenido de Lync 2013 en el buzón de correo de un usuario. Puede poner contenido Lync en espera usando la Retención local y usar la Exhibición de documentos electrónicos local para buscar contenido de Lync archivado en Exchange.

  - **Directivas de retención** Las directivas de retención ayudan a su organización a reducir los riesgos asociados con el correo electrónico y otras comunicaciones y también a cumplir los requisitos de retención de correo electrónico. Las directivas de retención incluyen las siguientes opciones:
    
      - **Soporte de las etiquetas de retención Calendario y Tareas**   Puede crear etiquetas de directivas de retención para las carpetas predeterminadas Calendario y Tareas si desea caducar elementos de dichas carpetas. Los elementos de dichas carpetas también se mueven al archivo de usuario en función de la configuración de la directiva de archivo que se aplique al buzón de correo.
    
      - **Capacidad mejorada para conservar elementos durante un periodo específico**   Puede utilizar directivas de retención y una Retención local basada en tiempo para aplicar la retención de elementos en un periodo determinado.

Para obtener más información, consulte [Directiva de mensajería y conformidad](messaging-policy-and-compliance-exchange-2013-help.md).

## Reglas de transporte

Las reglas de transporte en Exchange Server 2013 suponen una continuación de las características disponibles en Exchange Server 2010. Sin embargo, se han realizado varias mejoras en las reglas de transporte en Exchange 2013. El cambio más importante es el apoyo de la prevención de pérdida de datos (DLP). También hay nuevos predicados y acciones, supervisión mejorada y algunos cambios de arquitectura.

Para obtener información, consulte [Novedades de las reglas de transporte](what-s-new-for-transport-rules-exchange-2013-help.md).

## Information Rights Management

Information Rights Management (IRM) es compatible con Cryptographic Mode 2, un modo de criptografía de Active Directory Rights Management Services (AD RMS) que admite un cifrado más potente al permitir usar claves de 2048 bits para RSA y claves de 256 bits para SHA-1. De manera adicional, el Mode 2 le permite usar el algoritmo de hash SHA-2. Para obtener más información acerca de los modos criptográficos en AD RMS, vea [AD RMS Cryptographic Modes (Modos de criptografía de AD RMS)](https://go.microsoft.com/fwlink/p/?linkid=263219).

## Auditoría

Exchange 2013 incluye las siguientes mejoras en la auditoría:

  - **Informes de auditoría**   El EAC incluye funciones de auditoría para que pueda ejecutar informes o exportar entradas desde el registro de auditoría de buzón de correo y el registro de auditoría del administrador. El registro de auditoría de buzón de correo se indica cada vez que otro usuario que no es el propietario obtiene acceso al buzón. Esto puede ayudar a determinar quién ha tenido acceso a un buzón y lo que ha hecho. El registro de auditoría del administrador guarda cualquier acción, según un cmdlet del Shell de administración de Exchange, que ha realizado un administrador. Esto puede ayudar a solucionar problemas de configuración o a identificar la causa de problemas relacionados con la seguridad o el cumplimiento normativo. Para obtener más información, vea [Informes de auditoría de Exchange](exchange-auditing-reports-exchange-2013-help.md).

  - **Consulta del registro de auditoría de administrador:** en lugar de exportar el registro de auditoría de administrador, para lo cual pueden transcurrir hasta 24 para recibirlo en un mensaje de correo electrónico, puede ver las entradas del registro de auditoría del administrador en el EAC. Para ello, vaya a **Administración de cumplimiento** \> **Auditoría** y haga clic en **Ver el registro de auditoría del administrador**. Se mostrarán hasta 1.000 entradas en varias páginas. Para restringir la búsqueda, puede especificar un intervalo de fechas. Para obtener más información, consulte [Ver el registro de auditoría del administrador](view-the-administrator-audit-log-exchange-2013-help.md).

## Protección contra malware

Las capacidades integradas de filtrado de malware de Exchange 2013 ayudan a proteger su red de software malicioso que se transfiere a través de los mensajes de correo electrónico. Todos los mensajes que se envían o reciben a través de su servidor Exchange son escaneados para detectar malware (virus y spyware). Si se detecta malware, se elimina el mensaje. También se pueden enviar notificaciones a los remitentes o administradores cuando se elimina y no se entrega un mensaje infectado. También puede elegir sustituir los elementos adjuntos infectados con mensajes predeterminados o personalizados que notifican a los remitentes sobre la detección del malware.

Para obtener más información acerca de la protección contra malware, consulte [Protección antimalware](anti-malware-protection-exchange-2013-help.md).

## Flujo de correo

El flujo de mensajes en una organización y lo que ocurre con ellos ha cambiado significativamente en Exchange 2013. Lo que sigue es un breve resumen de los cambios:

  - **La canalización de transporte** La canalización de transporte en Exchange 2013 ahora incluye varios servicios diferentes: el servicio de transporte de front-end en servidores de Acceso de clientes, el servicio de transporte en servidores Buzón de correo y el servicio de transporte de buzones en servidores Buzón de correo. Para obtener más información, vea [Flujo de correo](mail-flow-exchange-2013-help.md).

  - **Enrutamiento** El enrutamiento de correo en Exchange 2013 reconoce los límites del DAG así como los límites del sitio de Active Directory. Asimismo, se ha mejorado el enrutamiento de correo para colocar en cola los mensajes de forma más directa para destinatarios internos. Para obtener más información, consulte [Enrutamiento de correo](mail-routing-exchange-2013-help.md).

  - **Conectores**   El tamaño máximo de mensaje para un conector de envío o un conector de recepción, según se especifica en el parámetro *MaxMessageSize*, se ha incrementado de 10 MB a 25 MB. Si desea ampliar información sobre cómo configurar los parámetros de un conector, consulte [Set-SendConnector](https://technet.microsoft.com/es-es/library/aa998294\(v=exchg.150\)) y [Set-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125140\(v=exchg.150\)).
    
    Puede configurar un conector de envío en el servicio de transporte de un servidor de buzón de correo para que enrute el correo saliente a través de un servidor de transporte de front-end en el sitio local de Active Directory, mediante el parámetro *FrontEndProxyEnabled* del cmdlet **Set-SendConnector**, consolidando así la manera en que el correo electrónico se enruta desde el servicio de transporte.

  - **Transporte perimetral**   Opcionalmente puede instalar un servidor de transporte perimetral en la red perimetral para reducir la superficie expuesta a ataques y proporcionar seguridad y protección de mensajes. Para más información, vea [Servidores de transporte perimetral](edge-transport-servers-exchange-2013-help.md).

## Destinatarios

Esta sección describe las mejoras de administración de destinatarios en Exchange 2013:

  - **Directiva de nomenclatura de grupo**   Los administradores ahora pueden utilizar el EAC para crear una *directiva de nomenclatura de grupo*, que le permitirá normalizar y administrar los nombres de grupos de distribución que creen los usuarios de su organización. Puede requerir que se añada un prefijo o sufijo concreto al nombre de un grupo de distribución cuando se crea y puede bloquear el uso de determinadas palabras. Esta funcionalidad le ayuda a minimizar el uso de palabras inadecuadas en los nombres de grupo.
    
    Para obtener más información, consulte [Crear una directiva de nomenclatura de grupos de distribución](create-a-distribution-group-naming-policy-exchange-2013-help.md).

  - **Seguimiento de mensajes** Los administradores también pueden usar el Centro de administración de Exchange para realizar un seguimiento de la información de entrega de mensajes de correo electrónico enviado o recibido por cualquier usuario de su organización. Basta con seleccionar un buzón de correo y, a continuación, buscar los mensajes enviados o recibidos por un usuario concreto. Puede limitar la búsqueda si busca determinadas palabras en la línea de asunto. El informe de entrega resultante hace un seguimiento de un mensaje a través del proceso de entrega y especifica si el mensaje se entregó correctamente, tiene pendiente la entrega o no se entregó.
    
    Para obtener más información, vea [Seguimiento de mensajes con informes de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).

## Uso compartido y colaboración

Esta sección describe las mejoras de intercambio y colaboración en Exchange 2013.

  - **Carpetas públicas**  Las carpetas públicas se han modernizado para aprovechar las tecnologías de almacenamiento y alta disponibilidad existentes en el almacén de buzones. La arquitectura de carpeta pública usa buzones especialmente diseñados para almacenar la jerarquía y el contenido de carpeta pública. Este nuevo diseño también significa que ya no existe una base de datos de carpetas públicas. La replicación de carpetas públicas ahora utiliza el modelo de replicación continua. La alta disponibilidad para los buzones de contenido y jerarquía está suministrada por el grupo de disponibilidad de base de datos (DAG). Con este diseño, abandonamos el modelo de replicación de varios maestros para adoptar un modelo de replicación de un solo maestro.
    
    Los usuarios de Outlook Web App de la organización ahora tienen la posibilidad de agregar las carpetas públicas o quitarlas de sus Favoritos. Anteriormente, esto solo podía hacerse en Outlook.
    
    Para obtener más información, consulte [Carpetas públicas](public-folders-exchange-2013-help.md).

  - **Buzones del sitio** El correo electrónico y los documentos se mantienen tradicionalmente en dos repositorios de datos únicos e independientes. La mayoría de los equipos normalmente colaboraría utilizando ambos medios. El desafío reside en que se accede al correo electrónico y a los documentos usando clientes distintos, lo que suele resultar en una reducción en la productividad del usuario y una experiencia de usuario degradada.
    
    El *buzón del sitio* es un nuevo concepto en Exchange 2013 que aspira a resolver estos problemas. Los buzones del sitio mejoran la colaboración y la productividad del usuario al conceder acceso a documentos de SharePoint y correo electrónico de Outlook 2013 mediante el uso de la misma interfaz de cliente. Un buzón de sitio incluye funcionalmente pertenencia al sitio de SharePoint (propietarios y miembros), almacenamiento compartido mediante un buzón de correo de Exchange para los mensajes de correo electrónico y un sitio SharePoint para los documentos, además de una interfaz de administración que satisface las necesidades de ciclo de vida y aprovisionamiento.
    
    Para obtener más información, consulte [Buzones de correo del sitio](site-mailboxes-exchange-2013-help.md).

  - **Buzones de correo compartidos**   En versiones anteriores de Exchange, crear un buzón de correo compartido era un proceso de varios pasos en el que se tenía que utilizar el Shell de administración de Exchange para configurar los permisos delegados. En Exchange 2013, ahora puede crear un buzón de correo compartido en un solo paso a través del Centro de administración de Exchange. En el EAC, vaya a **Destinatarios** \> **Buzones de correo compartidos** para crear un buzón de correo compartido. El buzón de correo compartido es ahora un tipo de destinatario, de manera que puede buscar fácilmente los buzones compartidos en la interfaz del usuario o usando el Shell.
    
    Para obtener más información, consulte [Buzones compartidos](shared-mailboxes-exchange-2013-help.md).

## Integración con SharePoint y Lync

Exchange 2013 ofrece una mayor integración con SharePoint 2013 y Lync 2013. Los beneficios de esta integración mejorada incluyen:

  - Exchange 2013 se integra con SharePoint 2013 para permitir que los usuarios colaboren de manera más eficaz usando los buzones de correo locales.

  - Lync Server 2013 puede archivar contenido en Exchange 2013 y usar Exchange 2013 como almacén de contactos.

  - Los administradores de detección pueden realizar búsquedas de exhibición de documentos electrónicos y retención local a través de datos de SharePoint 2013, Exchange 2013 yLync 2013.

  - La autenticación de Oauth permite a las aplicaciones asociadas realizar la autenticación como un servicio o suplantar a los usuarios cuando es necesario.

Para obtener más información, consulte [Integración con SharePoint y Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

## Clientes y móvil

La interfaz del usuario de Outlook Web App es nueva y está optimizada para su uso en tabletas y smartphones, así como en equipos de sobremesa y portátiles. Las nuevas características incluyen aplicaciones para Outlook, que permite a usuarios y administradores ampliar las funciones de Outlook Web App; vinculación de contactos y la posibilidad de que los usuarios agreguen contactos desde sus cuentas de LinkedIn, así como actualizaciones en la apariencia y las características del calendario.

Para obtener más información, consulte [Novedades de Outlook Web App en Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md).

## Mensajería unificada

La mensajería unificada en Exchange 2013 incluye esencialmente las mismas características de correo de voz incluidas en Exchange 2010. Sin embargo, se han agregado algunas características y funciones nuevas y mejoradas a dichas funciones existentes. Más importante, los cambios arquitectónicos en la mensajería unificada de Exchange 2013 han logrado que los componentes, el servicio y las funciones que se incluían con la función de servidor de mensajería unificada en Exchange 2010 se dividan entre los servidores Buzón de correo y Acceso de clientes de Exchange 2013.

Para obtener más información, consulte [Novedades de mensajería unificada en Exchange 2013](what-s-new-for-unified-messaging-in-exchange-2013-exchange-2013-help.md).

## Buzón de lote se mueve

Exchange 2013 introduce el concepto de movimientos de lotes. La nueva arquitectura de movimiento se genera a partir de los movimientos del Servicio de replicación de buzones (MRS), con mayor capacidad de administración. La nueva arquitectura de movimiento de lote ofrece las siguientes mejoras:

  - Capacidad para mover varios buzones en lotes grandes.

  - Notificación por correo electrónico durante el movimiento con informes.

  - Reintento automático y priorización automática de movimientos.

  - Los buzones de correo de archivo principal y personal pueden moverse en forma conjunta o independiente.

  - Opción de finalización de solicitud de movimiento manual, que permite revisar el movimiento antes de finalizarlo.

  - Sincronizaciones incrementales periódicas para migrar los cambios.

Para obtener más información, consulte [Administración de movimientos locales](manage-on-premises-moves-exchange-2013-help.md).

## Alta disponibilidad y resistencia de sitios

Exchange 2013 usa DAG y copias de bases de datos de buzones, junto con otras funciones, tales como recuperación de un solo elemento, directivas de retención y copias de bases de datos retrasadas para suministrar protección de datos nativa de Exchange, alta disponibilidad y resistencia de sitios. La plataforma de alta disponibilidad, el almacén de información de Exchange y el motor de almacenamiento extensible (ESE) se han mejorado para suministrar una mayor disponibilidad, facilitar la administración y reducir los costos. Entre estas mejoras se incluyen:

  - **Disponibilidad administrada** Con la disponibilidad administrada, las funciones orientadas a la recuperación y supervisión interna se integran estrechamente para evitar errores, restaurar de manera proactiva los servicios, iniciar conmutaciones por error de servidores de forma automática o alertar a los administradores para que tomen medidas. El enfoque se centra en la supervisión y administración de la experiencia de usuario final y no solo en el tiempo activo de componente y servidor para ayudar a mantener el servicio disponible en forma continua.

  - **Almacén administrado**   Almacén administrado es el nombre de los procesos de Almacén de información, recientemente rescritos en Exchange 2013. El nuevo almacén administrado se escribe en C\# y se integra estrechamente con el servicio de replicación de Microsoft Exchange (MSExchangeRepl.exe) para suministrar mayor disponibilidad mediante una resistencia mejorada.

  - **Soporte para varias bases de datos por disco** Exchange 2013 incluye mejoras que le permiten brindar soporte a varias bases de datos (combinaciones de copias activas y pasivas) en el mismo disco y así aprovechar discos más grandes en términos de capacidad de la manera más eficiente posible.

  - **Restauración automática** permite restaurar rápidamente la redundancia de base de datos después de un error en el disco. Si se produce un error en el disco, la copia de bases de datos almacenada en ese disco se copia desde la copia de base de datos activa a un disco de reserva en el mismo servidor. Si se almacenaban varias copias de bases de datos en el disco con error, pueden volver a inicializarse todas automáticamente en un disco de reserva. Esto posibilita inicializaciones más rápidas dado que es probable que las bases de datos activas se encuentren en varios servidores y los datos se copien en paralelo.

  - **Recuperación automática de errores de almacenamiento**   Esta funcionalidad continúa la innovación introducida en Exchange 2010 para permitir que el sistema se recupere de errores que afectan la resistencia o la redundancia. Además de los Exchange 2010 comportamientos de comprobación de errores, Exchange 2013 incluye comportamientos de recuperación adicionales para tiempos de E/S largos, consumos excesivos de memoria por parte de MSExchangeRepl.exe y casos graves en los que el sistema se encuentra en un estado tan malo que las amenazas no pueden programarse.

  - **Mejoras en copias retrasadas**   Las copias retrasadas ahora pueden ocuparse en cierta medida de sí mismas con la reproducción automática de registros. Las copias retrasadas reproducen automáticamente los archivos de registro en una variedad de situaciones, como la restauración de una sola página y los casos de poco espacio en el disco. Si el sistema detecta que la aplicación de revisiones es necesaria para una copia retrasada, los registros se volverán a reproducir automáticamente en la copia retrasada al aplicar las revisiones de página. Las copias retrasadas también invocarán esta característica de reproducción automática cuando se alcance un umbral de espacio de disco bajo, y cuando la copia retrasada se haya detectado como la única copia disponible durante un período de tiempo específico. Además, las copias retrasadas pueden aprovechar la Red de seguridad, lo que hace que la recuperación o la activación sean más fáciles. *Red de seguridad* ha mejorado su funcionalidad en Exchange 2013 basándose en el contenedor de transporte de Exchange 2010.

  - **Mejoras en la alerta de copia única**   La alerta de copia única introducida en Exchange 2010 ya no es un script programado por separado. Ahora está integrada en los componentes de disponibilidad administrada en el sistema y es una función nativa de Exchange.

  - **Autoconfiguración de red DAG**   El sistema puede configurar automáticamente las redes DAG basándose en las opciones de configuración. Además de las opciones de configuración manual, las redes DAG también pueden distinguir entre MAPI y redes de replicación y configurar redes DAG automáticamente.

Para obtener más información acerca de estas características, consulte [Alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-exchange-2013-help.md) y [Cambios en la alta disponibilidad y resistencia de sitios respecto a versiones anteriores](changes-to-high-availability-and-site-resilience-over-previous-versions-exchange-2013-help.md).

## Administración de carga de trabajo de Exchange

La carga de trabajo de Exchange es una característica de un servidor, un protocolo o un servicio de Exchange que se definió de manera explícita para fines de administración de recursos del sistema de Exchange. Cada carga de trabajo de Exchange consume recursos del sistema como CPU, operaciones de base de datos de buzón de correo, o peticiones de Active Directory para ejecutar solicitudes del usuario o ejecutar trabajos en segundo plano. Ejemplos de cargas de trabajo de Exchange incluyen Outlook Web App, Exchange ActiveSync, migración del buzón de correo y asistentes del buzón de correo.

Hay dos formas de administrar cargas de trabajo de Exchange en Exchange 2013:

  - **Supervisar el estado de los recursos del sistema**   Administrar cargas de trabajo basándose en el estado de los recursos del sistema es una novedad en Exchange 2013.

  - **Controlar el consumo de recursos por parte de usuarios individuales**   En Exchange 2010 se podía controlar la forma en que los usuarios individuales consumían recursos (se denominaba limitación de usuarios), y esta funcionalidad se ha ampliado para Exchange 2013.

Para obtener más información acerca de estas características, consulte [Administración de carga de trabajo de Exchange](exchange-workload-management-exchange-2013-help.md).

