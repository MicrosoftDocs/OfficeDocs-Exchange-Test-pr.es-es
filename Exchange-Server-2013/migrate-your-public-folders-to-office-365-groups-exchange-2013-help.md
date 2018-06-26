---
title: 'Migrar las carpetas públicas a grupos de Office 365: Exchange 2013 Help'
TOCTitle: Migrar las carpetas públicas a grupos de Office 365
ms:assetid: d89e727b-675a-4623-b572-260f8b44b966
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt843872(v=EXCHG.150)
ms:contentKeyID: 74468731
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Migrar las carpetas públicas a grupos de Office 365

 

_**Se aplica a:**Exchange Online, Exchange Server 2010, Exchange Server 2013_

_**Última modificación del tema:**2017-09-25_

**Resumen:** ¿por qué debe o no debe migrar las carpetas públicas de Exchange a los grupos de Office 365.

En este artículo se proporciona una comparación de las carpetas públicas y grupos de Office 365 y cómo uno u otro podría ser la mejor solución para su organización. Las carpetas públicas han estado presentes desde los albores de Exchange, mientras que los grupos se introdujeron más recientemente. Si desea migrar algunas o todas las carpetas públicas a grupos, este artículo describe cómo funciona el proceso y proporciona vínculos a los artículos que le guían paso a paso por el proceso.

## ¿Cuáles son las carpetas públicas?

[Carpetas públicas](public-folders-exchange-2013-help.md) contener distintos tipos de datos y están organizados en una estructura jerárquica.

Las carpetas públicas no se recomiendan para las siguientes situaciones:

  - **Archiving de datos**. Los usuarios con los límites de los buzones a veces utilizan carpetas públicas en lugar de buzones para archivar datos. Esta práctica no es recomendable porque afecta al almacenamiento en carpetas públicas y debilita el objetivo de los límites del buzón.

  - **Uso compartido de documentos y colaboración**. Las carpetas públicas no proporcionan características de administración de documentos, como control de versiones, controlan la funcionalidad de protección y desprotección y notificaciones automáticas de los cambios de contenido.

## Qué son los grupos de Office 365

Grupos en Office 365 le permiten elegir un conjunto de personas que desea colaborar con y, a continuación, configurar fácilmente una colección de recursos para aquellas personas compartir. No tiene que preocuparse de asignar manualmente los permisos a esos recursos, porque agregar miembros al grupo concede automáticamente a los miembros los permisos que necesitan para acceder a las herramientas y recursos proporciona el grupo. Los grupos son también la experiencia nueva y mejorada para las tareas que se han controlado anteriormente por las listas de distribución y comparten los buzones.

Para ver la historia completa de grupos, consulte [Obtenga información acerca de Office 365 grupos](https://go.microsoft.com/fwlink/p/?linkid=858521).

## ¿Debe migrar las carpetas públicas a grupos de Office 365?

Grupos de Office 365 es la colaboración más reciente de Microsoft, lo que significa que existen muchas razones por qué serían una solución preferible a través de las carpetas públicas, una tecnología mucho más antiguos. En Outlook, por ejemplo, grupos pueden reemplazar carpetas públicas habilitadas para correo en conjunto. Compilar una lista de todos los escenarios en los que Office 365 grupos funciona mejor que las carpetas públicas es imposible, pero aquí son los puntos destacados:

  - **Colaboración a través de correo electrónico**. Grupos de Outlook tiene un espacio dedicado de **conversaciones** que almacena todos los correos electrónicos y permite a los usuarios colaborar a través de ellos. El grupo puede incluso configurarse para recibir mensajes de personas fuera del grupo o desde fuera de la organización. Si actualmente utiliza carpetas públicas habilitadas para correo para almacenar discusiones relacionadas con el proyecto, por ejemplo, o pedidos de compra que se necesitan para ser visto por un equipo de personas, utilizando grupos sería una mejora. Grupos también son mejores en situaciones cuando desea difundir información a un conjunto de usuarios.

  - **Colaboración en documentos**. En Outlook, grupos tiene una pestaña de **archivos** dedicada que muestra todos los archivos desde el sitio del grupo SharePoint team, así como de los datos adjuntos de correo. Obtener una vista de todos los archivos, por lo que no tiene que ir a buscar para ellos como lo haría en las carpetas públicas. Co-autoría también resulta más fácil. Si utiliza carpetas públicas para almacenar archivos destinados a ser consumidos por varias personas, considere migrar a grupos.

  - **Calendario compartido**. Tras la creación de cada grupo obtiene un calendario compartido. Cualquier miembro del grupo puede crear eventos en ese calendario. Cuando el favorito un grupo, el calendario de ese grupo puede mostrarse junto a su calendario personal. También puede suscribirse a los eventos de un grupo, en el que caso eventos creados en ese grupo aparecen en el calendario personal. Si utiliza carpetas públicas a los calendarios de host para el equipo, como una programación o un calendario, grupos sería una mejor experiencia.

  - **Permisos de simplificado**. Al asignar usuarios a un grupo, inmediatamente reciben los permisos que necesitan, mientras que con las carpetas públicas debe asignar manualmente los permisos adecuados. Los miembros pueden agregarse como "propietarios" o "miembros". Los propietarios tienen derechos completos en el grupo, incluida la capacidad para realizar tareas de administración de grupo. Los miembros también pueden crear contenido y editar archivos como propietarios, pero los miembros no pueden eliminar el contenido que no han creado. Si el modelo de permisos de las carpetas públicas es demasiado abrumadora para usted y desea algo sencillo y rápido, Office 365 grupos es la mejor opción.

  - **Presencia Web y móviles**. Las carpetas públicas no se puede acceder a través de dispositivos móviles y tengan un conjunto limitado de funcionalidad en la Web. Por otra parte, los grupos de Office 365, es accesibles a través de aplicaciones móviles de Outlook y tiene un conjunto más rico de características en el Web. Si el equipo está en constante movimiento y requiere acceso móvil, entonces debería utilizar grupos de Office 365.

  - **Acceso a las aplicaciones de una amplia gama de Office 365**. Cuando se crea un grupo, desbloquear acceso a una amplia gama de aplicaciones desde el paquete de Office 365. Obtenga un sitio de grupo de SharePoint para almacenar archivos y un plan en planes para realizar un seguimiento de las tareas. Grupos de Office 365 es el servicio de suscripción que combina los elementos de la serie completa de Office 365.

Aunque Office 365 grupos ofrece muchas ventajas, debe ser consciente de algunas diferencias importantes que verá después de salir de la experiencia de las carpetas públicas. Estos son principalmente:

  - **Jerarquía de carpetas**. Aunque las carpetas públicas se suelen utilizar para organizar el contenido de jerarquía con raíz profunda, Office 365 grupos tiene una estructura plana. Todos los correos electrónicos del grupo residen en el espacio de conversaciones y todos los documentos se entran en la ficha **archivos**. Además, no puede crear subcarpetas en grupos de Office 365.

  - **Roles de permisos granulares**. Aunque las carpetas públicas tienen una variedad de funciones de permiso, Office 365 grupos sólo proporciona dos: propietario y miembros.

Antes de mover a grupos, también es una buena idea tome nota de los diferentes límites que vienen con la creación y mantenimiento de grupos. Consulte *¿Cómo administro Mis grupos?* en [aprender acerca de los grupos de Office 365](https://go.microsoft.com/fwlink/p/?linkid=858521) para obtener más información.

## Migrar carpetas públicas a grupos de Office 365

Si decide cambiar a Office 365 grupos, puede utilizar un proceso conocido como *migración de lote* para mover el contenido de correo electrónico y calendario de las carpetas públicas existentes a grupos. Los pasos específicos para ejecutar una migración por lotes depende de qué versión de Exchange aloja actualmente la jerarquía de carpetas públicas. Al final de este artículo, encontrará vínculos a instrucciones que le guiarán a través del proceso de migración por lotes.


> [!NOTE]
> Cuando termine la migración de una carpeta pública habilitada para correo a un grupo concreto de Office 365, en ese momento se recibirán todos los mensajes dirigidos a la carpeta pública por el grupo.



Ventajas clave de las migraciones de lote son:

  - **Migración de SEÑORA de servicio replicación de buzón**. El proceso de migración utiliza cmdlets de migración por lotes. Migración a varios grupos puede activarse juntos en un lote único de migración. También hay secuencias de comandos disponibles para ayudar en el proceso de migración.

  - **Compatible con correo y calendario de carpetas públicas**. Los mensajes y correos electrónicos copiados aparecerá como se muestra en las conversaciones en grupo a los grupos y elementos copiados estarán visibles en los calendarios de grupo. Otros tipos de carpetas públicas, como tareas y contactos, no se admiten actualmente para esta migración.

  - **Las carpetas públicas locales se pueden migrar directamente a los grupos de Office 365**. Esta migración no requieren el primer movimiento de las carpetas públicas a Office 365 y, a continuación, mover a grupos. Los cmdlets de copia de datos Sra. leer los datos de carpetas públicas directamente desde su entorno local y, a continuación, copiar los datos en grupos de Office 365. Tenga en cuenta que las carpetas públicas de Exchange 2010 requerirá un extremo Outlook en cualquier lugar. Las carpetas públicas de Exchange 2013 y 2016 de Exchange requerirán un extremo basada en Proxy de SEÑORA.

  - **No una migración de "todo o nada"**. Elija carpetas públicas específicas para migrar a grupos, y sólo las carpetas públicas solicitadas se pueden migrar.

  - **Copia datos de un disparo**. Migraciones de lotes están diseñadas para ser simple única copia de datos de carpetas públicas de origen a los grupos de destino, sin las complejidades de sincronización incremental y finalización.

  - **Combina datos de carpetas públicas con los datos existentes en un grupo**. La copia de datos combinará el contenido de carpetas públicas con el contenido del grupo existente, si existe. Si es necesario para la copia de datos incremental, puede simplemente ejecutar la copia de datos tantas veces como sea necesario. Esto copiará los datos incrementales al grupo.

## Información general sobre migraciones de lote

Los pasos siguientes describen el proceso general de migrar el contenido de carpetas públicas a grupos de Office 365 en una migración por lotes. Los detalles específicos están contenidos en los artículos que se enumeran a continuación.

1.  **Seleccione fuente:** elija las carpetas públicas que desea migrar. Puede elegir cualquier correo de la carpeta que lo contiene o el contenido de calendario.

2.  **El objetivo de crear:** crear grupos correspondientes para las carpetas, con las configuraciones deseadas, como miembros, la configuración de privacidad y clasificación de datos.

3.  **Copiar datos:** usar los cmdlets de migración por lotes para copiar los datos de carpetas públicas a grupos.

4.  **Origen de bloqueo:** bloquear las carpetas públicas, una vez que haya verificado los datos en grupos.

5.  **Cutover:** copia cualquier dato nuevo que se ha creado entre los pasos 3 y 4.

Tenga en cuenta que las carpetas públicas y sus correspondientes grupos permanecerán en línea para los usuarios durante los pasos del 1 al 3 anteriores. Después del paso 3, puede evaluar si debe o no continuar con el resto de la migración, basado en la experiencia de grupos y el hecho de que se ajuste a los usuarios y su organización. Puede revertir la migración y volver a utilizar las carpetas públicas en ese momento. Si continúa con la migración, después de que finalice el paso 5, puede eliminar las carpetas públicas originales. Incluso después de la migración, es posible hacer roll back a carpetas públicas, proporcionado ha guardado los archivos de copia de seguridad desde el proceso de migración y no ha eliminado las carpetas públicas originales.

## Requisitos previos de migración por lotes e instrucciones paso a paso

Los siguientes requisitos previos son necesarios en su entorno de Exchange para poder ejecutar una migración por lotes. Los requisitos previos específicos dependen de la versión de Exchange que está ejecutando actualmente.

1.  Si las carpetas públicas son locales, los servidores necesitan estar ejecutando uno de las siguientes versiones:
    
      - Exchange 2010 SP3 RU8 o versiones posteriores
    
      - Intercambio de 2013 CU15 o posterior
    
      - Intercambio de 2016 CU4 o posterior

2.  Si las carpetas públicas son locales, debe tener configurado un entorno de Exchange híbrido. Consulte [Implementaciones híbridas de Exchange Server](https://technet.microsoft.com/es-es/library/jj200581\(v=exchg.150\)) para obtener más información.

**Instrucciones de migración**

Seleccione el vínculo apropiado a continuación para obtener instrucciones detalladas sobre cómo ejecutar una migración por lotes.

  - [Utilizar lotes de migración para migrar carpetas públicas de Exchange Online para Office 365 grupos](https://technet.microsoft.com/es-es/library/mt843871\(v=exchg.150\))

  - [Utilizar lotes de migración para migrar carpetas públicas de Exchange 2010 a Office 365 grupos](use-batch-migration-to-migrate-exchange-2010-public-folders-to-office-365-groups-exchange-2013-help.md)

  - [Utilizar lotes de migración para migrar carpetas públicas de Exchange de 2013 a Office 365 grupos](use-batch-migration-to-migrate-exchange-2013-public-folders-to-office-365-groups-exchange-2013-help.md)

  - [Migración de lote uso migrar carpetas públicas de Exchange 2016 a los grupos de Office 365](https://go.microsoft.com/fwlink/p/?linkid=859171)

