---
title: 'Copia seguridad restauración y recuperación ante desastres: Exchange 2013 Help'
TOCTitle: Copia de seguridad, restauración y recuperación ante desastres
ms:assetid: 394fc4ed-fa02-41fa-9159-cc2754ff8875
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876874(v=EXCHG.150)
ms:contentKeyID: 48267999
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Copia de seguridad, restauración y recuperación ante desastres

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Como parte de la planificación de protección de datos, es importante que comprenda las maneras en que los datos pueden protegerse y que determine qué métodos se adecuan mejor a las necesidades de su organización. La planificación de protección de datos es un proceso complejo que depende de muchas decisiones que usted toma durante la fase de planificación de su implementación.

Tradicionalmente, las copias de seguridad se han utilizado para los siguientes escenarios:

  - **Recuperación ante desastres**   En caso de un error de hardware o software, varias copias de base de datos en un DAG ofrecen alta disponibilidad con conmutación por error rápida con escasa o ninguna pérdida de datos. Esto elimina el tiempo de inactividad y la pérdida de productividad resultante con un coste significativo debida a la recuperación de una copia de seguridad hasta un momento dado a un disco o una cinta. Los DAG pueden extenderse a varios sitios y brindar resistencia contra errores del disco, el servidor, la red y el centro de datos.

  - **Recuperación de elementos eliminados accidentalmente**   Históricamente, en una situación en la que un usuario elimina elementos que, después, deben ser recuperados, el proceso involucra la búsqueda del medio de copia de seguridad en donde los datos que se deben recuperar estaban almacenados y, luego, obtener, de alguna manera, los elementos deseados y entregárselos al usuario. Con la nueva carpeta de elementos recuperables de Exchange 2013, es posible retener todos los datos eliminados y modificados durante un período de tiempo específico, de modo que la recuperación de estos elementos es más sencilla y rápida. Esto reduce la responsabilidad de los administradores de Exchange y del servicio de asistencia de IT al permitir que los usuarios mismos recuperen los elementos eliminados de manera accidental, y, consecuentemente, reduce la complejidad y los costos administrativos asociados con la recuperación de un único elemento. Para obtener más información, consulte [Directiva de mensajería y conformidad](messaging-policy-and-compliance-exchange-2013-help.md) y [Prevención de pérdida de datos](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention).

  - **Almacenamiento de datos a largo plazo**   Las copias de seguridad también se han usado como archivo y, generalmente, la cinta se usa para preservar las instantáneas de datos hasta un momento dado durante periodos de tiempo prolongados según los requisitos de cumplimiento. Las nuevas características de archivo, búsqueda en varios buzones de correo y retención de mensajes en Exchange 2013 proporcionan un mecanismo para preservar datos eficazmente en una forma accesible para el usuario final durante periodos de tiempo prolongados. De este modo se eliminan las restauraciones costosas desde la cinta y se incrementa la productividad. Para obtener más información, consulte [Archivado local en Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md), [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md) y [Conservación local y retención por juicio](https://docs.microsoft.com/es-es/exchange/security-and-compliance/in-place-and-litigation-holds).

  - **Instantánea de base de datos hasta un momento dado**   Si una copia pasada hasta un momento dado de datos del buzón de correo es un requisito para su organización, Exchange proporciona la capacidad de crear una copia de la base de datos atrasada en un entorno de DAG. Esto puede ser útil en eventos inusuales en los que la corrupción lógica del almacenamiento se replica a través de varias bases de datos en el DAG, lo que provoca la necesidad de retornar a un momento anterior. También, puede ser útil en caso de que un administrador elimine, de manera accidental, los buzones de correo o los datos de usuario. La recuperación de una copia atrasada puede ser más rápida que restaurar una copia de seguridad, ya que las copias atrasadas no requieren procesos de copia desde el servidor copia de seguridad hacia el servidor de Exchange que llevan mucho tiempo. Esto puede reducir significativamente el costo total de propiedad ya que disminuye el tiempo de inactividad.

Dado que existen características nativas de Exchange 2013 que responden a cada uno de estos escenarios de manera eficaz y rentable, podrá reducir o eliminar el uso de copias de seguridad tradicionales en su entorno.

Protección nativa de datos de Exchange

Tecnologías de copia de seguridad admitidas

Escritor de VSS de Exchange 2013

Recuperación de Exchange Server

Recuperación del almacén de contactos unificado

Base de datos de recuperación

Portabilidad de bases de datos

Portabilidad del tono de marcado

## Protección nativa de datos de Exchange

La [arquitectura preferida](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx) de Microsoft para Exchange Server 2013 usa un concepto conocido como Exchange Native Data Protection. Exchange Native Data Protection se basa en características integradas de Exchange para proteger los datos de su buzón de correo sin tener que usar copias de seguridad (aunque puede seguir utilizando dichas características para crear copias de seguridad). Exchange 2013 incluye varias características nuevas y cambios generales que, una vez implementados y configurados correctamente, ofrecen una protección de datos nativa que elimina la necesidad de realizar copias de datos tradicionales. Con las funciones de alta disponibilidad incorporadas en Exchange 2013 para minimizar el tiempo de inactividad y la pérdida de datos en caso de un desastre, también se puede reducir el costo total de propiedad del sistema de mensajería. Al combinar estas características con otras características integradas, como la retención legal, puede reducir o eliminar el uso de copias de seguridad tradicionales hasta un momento dado y reducir los costos asociados.

Además de determinar si Exchange 2013 le permite cambiar las copias de seguridad tradicionales hasta un momento dado, le recomendamos que evalúe el costo de la infraestructura actual de copias de seguridad. Considere el costo del tiempo de inactividad de los usuarios finales y la pérdida de datos al intentar recuperarse de un desastre con la infraestructura de copia de seguridad actual. Además, incluya costos de hardware, instalación y licencia, y los costos de administración asociados con la recuperación de datos y el mantenimiento de las copias de seguridad. Según los requisitos de la organización, es posible que un entorno de Exchange 2013 puro con al menos tres copias de bases de datos de buzones de correo ofrezca un menor costo total de propiedad que uno con copias de seguridad.

Antes de usar las características integradas de Exchange 2013 como un repuesto para copias de seguridad tradicionales, debe considerar varios problemas. También puede haber consideraciones exclusivas de su organización. Tenga en cuenta lo siguiente y recuerde que esta no es una lista exhaustiva:

  - Debe determinar cuántas copias de la base de datos deben implementarse. Se recomienda implementar un mínimo de tres copias de una base de datos de buzones de correo (no atrasadas) antes de eliminar formas tradicionales de protección para la base de datos, como la matriz redundante de discos independientes (RAID) o las copias de seguridad tradicionales basadas en VSS.

  - Las metas de objetivo de tiempo de recuperación y objetivo de punto de recuperación deben estar definidas de manera clara y se debe establecer que mediante el uso de un conjunto combinado de características integradas en lugar de copias de seguridad tradicionales le permita satisfacer estas metas.

  - Debe determinar la cantidad de copias que se necesitan de cada base datos para cubrir los diversos escenarios de error que el sistema está diseñado para proteger.

  - Debe determinar si la eliminación del uso del DAG o algunos de sus miembros captura costos suficientes para admitir una solución de copia de seguridad tradicional. En tal caso, debe determinar si esa solución mejora los acuerdos de nivel de servicios (SLA) de los objetivos de tiempo de recuperación o los objetivos de punto de recuperación.

  - Debe determinar si puede perder una copia hasta un momento dado si el miembro del DAG que hospeda la copia experimenta un error que afecta la copia o la integridad de la copia.

  - Exchange 2013 le permite implementar buzones de correo mucho más grandes, con un tamaño de base de datos de buzón de correo máximo de 2 terabytes (cuando se usan dos o más copias de bases de datos de buzones de correo altamente disponibles). Según los buzones de correo más grandes que la mayoría de las organizaciones probablemente implementen, debe determinar cuál será el objetivo de punto de recuperación si tiene que volver a reproducir una gran cantidad de archivos de registro al activar una copia de base de datos o una copia de base de datos retrasada.

  - Debe determinar cómo podrá detectar e impedir que la corrupción lógica en una copia de base de datos activa se replique a las copias pasivas de la base de datos. Esto incluye la determinación del plan de recuperación para esta situación y con qué frecuencia esto ha sucedido en el pasado. Si la corrupción lógica se produce frecuentemente en su organización, se recomienda que incluya ese escenario en su diseño mediante el uso de una o más copias retrasadas, con una ventana de retardo de reproducción para permitirle detectar y realizar acciones cuando ocurra una corrupción lógica, pero antes de que se replique esa corrupción a otras copias de base de datos.

Una de las funciones realizadas al final de una copia de seguridad completa o incremental, que se realizó exitosamente, es el truncamiento de los archivos de registro de transacciones que ya no se necesitan para la recuperación de bases de datos. Si no se van a realizar copias de seguridad, el truncamiento de registros no ocurrirá. Para impedir la creación de archivos de registro, debe permitir los registros circulares para sus bases de datos replicadas. Cuando se combina el registro circular con la replicación continua, se obtiene un nuevo tipo de registro circular denominado registro circular de replicación continua (CRCL), que es diferente del registro circular de Motor de almacenamiento extensible (ESE). Mientras que el registro circular de ESE lo realiza y administra el servicio Almacén de información de Microsoft Exchange, el CRCL lo realiza y administra el servicio de replicación de Microsoft Exchange. Si se habilita, el registro circular ESE no genera archivos de registro adicionales y, en su lugar, sobrescribe el archivo de registro actual en caso necesario. No obstante, en un entorno de replicación continua, los archivos de registro son necesarios para el envío y la reproducción. En consecuencia, cuando se habilita el CRCL, el archivo de registro actual no se sobrescribe y se generan archivos de registro cerrados para el proceso de envío y reproducción de registro.

Específicamente, el servicio de replicación de Microsoft Exchange administra el CRCL para mantener la continuidad del registro y para que no se eliminen los registros si aún son necesarios para la replicación. El servicio de replicación de Microsoft Exchange y el servicio Almacén de información de Microsoft Exchange se comunican mediante llamadas a procedimiento remoto (RPC) respecto de cuáles archivos de registro pueden eliminarse.

Para que se realice el truncamiento en copias de base de datos de buzones de correo altamente disponibles (no atrasadas), lo siguiente debe ser verdadero:

  - El archivo de registro cuenta con copia de seguridad o es compatible con CLCR.

  - El archivo de registro está por debajo del punto de control.

  - Las demás copias no atrasadas de la base de datos están de acuerdo con la eliminación.

  - Todas las copias atrasadas de la base de datos han inspeccionado el archivo de registro.

Para que se realice el truncamiento en copias de base de datos atrasadas, lo siguiente debe ser verdadero:

  - El archivo de registro está por debajo del punto de control.

  - El archivo de registro es anterior a ReplayLagTime + TruncationLagTime.

  - Se eliminó el archivo de registro de la copia activa de la base de datos.

Protección nativa de datos de Exchange

## Tecnologías de copia de seguridad admitidas

Exchange 2013 solo admite copias de seguridad basadas en VSS compatibles con Exchange. Exchange 2013 incluye un complemento para Copias de seguridad de Windows Server que permite realizar y restaurar copias de seguridad basadas en VSS de datos de Exchange. Para realizar copias de seguridad de Exchange 2013 y restaurarlo, debe usar una aplicación compatible con Exchange que admita VSS Writer para Exchange 2013, como Copias de seguridad de Windows Server (con el complemento de VSS), Microsoft System Center 2012 Data Protection Manager o una aplicación de terceros basada en VSS y compatible con Exchange.

Para obtener información detallada sobre cómo realizar copias de seguridad y de la restauración de datos de Exchange mediante la copia de seguridad de Windows Server, consulte [Uso de copias de seguridad de Windows Server para realizar copias de seguridad y restaurar datos de Exchange](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md).

Protección nativa de datos de Exchange

## Escritor de VSS de Exchange 2013

Exchange 2013 presenta un cambio significativo de la arquitectura del VSS writer usada en Exchange 2010 y en Exchange 2007. Las versiones anteriores de Exchange incluyen dos VSS writer: uno dentro del servicio Almacén de información de Microsoft Exchange (store.exe) y uno dentro del servicio Replicación de Microsoft Exchange (msexchangerepl.exe). En Exchange, la funcionalidad VSS writer que anteriormente se encontraba en el servicio Almacén de información de Microsoft Exchange se ha movido al servicio Replicación de Microsoft Exchange. El nuevo writer, que se denomina Microsoft Exchange Writer, ahora se usa en aplicaciones basadas en VSS con Exchange para realizar copias de seguridad de bases de datos activas y pasivas, y recuperar copias de seguridad de bases de datos. Aunque el nuevo writer se ejecuta en el servicio de replicación de Microsoft Exchange, requiere el servicio Almacén de información de Microsoft Exchange que se debe ejecutar para que el writer se anuncie. Como resultado, ambos servicios son necesarios para realizar copias de seguridad o restaurar bases de datos de Exchange.

Protección nativa de datos de Exchange

## Recuperación de Exchange Server

Prácticamente todas las configuraciones de los servidores de buzones de correo y de acceso de clientes se almacenan en Active Directory. Igual que las versiones anteriores de Exchange, Exchange 2013 incluye un parámetro de instalación para recuperar servidores perdidos. Este parámetro, */m:RecoverServer*, se usa para volver a construir y recrear un servidor perdido mediante el uso de información sobre configuraciones almacenada en Active Directory. Sin embargo, tenga en cuenta que hay varias opciones que no se restauran, tales como los cambios en los archivos web.config locales y otros archivos de configuración. Además, no se restauran las entradas del registro personalizado. Recomendamos que utilice un proceso de administración de cambios confiable para realizar un seguimiento y volver a crear estos cambios.

Para obtener información acerca de los pasos detallados para realizar la recuperación de servidor de un servidor perdido de Exchange 2013, consulte [Recuperar un servidor de Exchange](recover-an-exchange-server-exchange-2013-help.md). Para obtener información acerca de los pasos detallados para recuperar un servidor perdido que es miembro de un grupo de disponibilidad de base de datos (DAG), consulte [Recuperar un servidor miembro de un grupo de disponibilidad de base de datos](recover-a-database-availability-group-member-server-exchange-2013-help.md).

Protección nativa de datos de Exchange

## Recuperación del almacén de contactos unificado

Cuando Microsoft Lync Server 2013 se usa en un entorno de Exchange 2013, la información de contacto del usuario de Lync se almacena en una carpeta de contactos especial en el buzón de correo del usuario. Se denomina almacén de contactos unificado (UCS). Si restaura un buzón de correo migrado UCS, la lista de contactos de mensajería unificada del usuario de destino puede resultar afectada. Si el usuario se migra después de la última copia da seguridad, la restauración del buzón de correo resultará en una pérdida completa de la lista de contactos del usuario. En casos menos graves, las modificaciones a la lista de contactos realizadas por el usuario desde la última copia de seguridad se perderán. Paras mitigar esta pérdida potencial de datos, asegúrese de que el usuario vuelve a migrar al servidor de mensajería instantánea antes de restaurar el buzón de correo.

Protección nativa de datos de Exchange

## Base de datos de recuperación

Una base de datos de recuperación es un tipo de base de datos de buzones de correo especial que permite montar una base de datos de buzones de correo restaurada y extraer los datos de la base de datos restaurada como parte del proceso de recuperación. Puede usar el cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)) para extraer los datos de una base de datos de recuperación. Tras la extracción, los datos pueden exportarse a una carpeta o combinarse en un buzón de correo que ya exista. Las bases de datos de recuperación le permiten recuperar datos de una copia de seguridad o de una copia de una base de datos sin perjudicar el acceso del usuario a los datos actuales.

El uso de una base de datos de recuperación para una base de datos de buzones de correo de cualquier versión anterior de Exchange no es compatible. Además, el buzón de correo de destino que se usa para combinaciones y extracciones de datos debe estar en el mismo bosque de Active Directory que la base de datos montada en la base de datos de recuperación.

Para obtener más información, consulte [Bases de datos de recuperación](recovery-databases-exchange-2013-help.md). Para obtener instrucciones detalladas acerca de cómo crear una base de datos de recuperación, consulte [Creación de una base de datos de recuperación](create-a-recovery-database-exchange-2013-help.md). Para obtener instrucciones detalladas acerca de cómo usar una base de datos de recuperación, consulte [Restauración de datos mediante una base de datos de recuperación](restore-data-using-a-recovery-database-exchange-2013-help.md).

Protección nativa de datos de Exchange

## Portabilidad de bases de datos

La portabilidad de bases de datos es una característica que permite que una base de datos de buzones de correo de Exchange 2013 se pueda mover o montar en cualquier otro servidor Buzones de Exchange 2013 de la misma organización. Al usar esta función, la fiabilidad se mejora mediante la eliminación de varios pasos manuales propensos a errores en el proceso de recuperación. Además, la portabilidad de bases de datos reduce los tiempos de recuperación completa en distintos escenarios de error.

Para obtener más información, consulte [Portabilidad de bases de datos](database-portability-exchange-2013-help.md). Para obtener instrucciones detalladas sobre cómo usar la portabilidad de base de datos, consulte [Mover una base de datos de buzones mediante la portabilidad de bases de datos](move-a-mailbox-database-using-database-portability-exchange-2013-help.md).

Protección nativa de datos de Exchange

## Portabilidad del tono de marcado

La portabilidad del tono de marcado es una característica que proporciona una solución de continuidad empresarial limitada para los errores que afectan a una base de datos de buzones de correo, un servidor o un sitio completo. La portabilidad del tono de marcado permite a los usuarios tener un buzón de correo temporal para enviar y recibir mensajes de correo electrónico mientras su buzón de correo original se recupera o restaura. El buzón temporal puede estar en el mismo servidor de buzones de Exchange 2013 o en cualquier otro servidor de buzones de Exchange 2013 de su organización. Esto permite que un servidor alternativo hospede los buzones de correo de los usuarios que estaban previamente en un servidor que ya no estará disponible. Los clientes que son compatibles con la función de detección automática, como Microsoft Outlook, se redirigen automáticamente al nuevo servidor sin necesidad de actualizar manualmente el perfil de escritorio del usuario. Una vez restaurados los datos del buzón original del usuario, un administrador puede combinar un buzón recuperado del usuario con el buzón de tono de marcado del usuario y crear un solo buzón actualizado.

El proceso para usar la portabilidad del tono de marcado se denomina *recuperación del tono de marcado*. Una recuperación del tono de marcado implica la creación de una base de datos vacía en un servidor de buzones para sustituir la base de datos en la que se produjeron los errores. Esta base de datos vacía, conocida como una *base de datos de tonos de marcado*, permite a los usuarios enviar y recibir mensajes de correo electrónico mientras se recupera la base de datos con errores. Una vez recuperada la base de datos con errores, la base de datos de tono de marcado y la base de datos recuperada se intercambian y, luego, los datos de la base de datos de tono de marcado se combina con la base de datos recuperada.

Para obtener más información, consulte [Portabilidad del tono de marcado](dial-tone-portability-exchange-2013-help.md). Para ver los pasos detallados para realizar una recuperación del tono de marcado, consulte [Realizar una recuperación del tono de marcado](perform-a-dial-tone-recovery-exchange-2013-help.md).

Protección nativa de datos de Exchange

