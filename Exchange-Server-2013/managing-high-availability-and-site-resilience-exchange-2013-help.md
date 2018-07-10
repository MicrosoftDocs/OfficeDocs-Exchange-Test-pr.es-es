---
title: 'Administración de alta disponibilidad y resistencia de sitios: Exchange 2013 Help'
TOCTitle: Administración de alta disponibilidad y resistencia de sitios
ms:assetid: f9677392-88d2-457f-a488-245771a8c1f2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638215(v=EXCHG.150)
ms:contentKeyID: 48268895
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administración de alta disponibilidad y resistencia de sitios

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-05_

Tras construir, validar e implementar una solución de alta disponibilidad y resistencia de sitios de Microsoft Exchange Server 2013, la solución pasa de la fase de implementación a la fase operativa dentro del ciclo de vida general de la misma. La fase operativa consta de varias tareas, todas ellas relacionadas con una de las áreas siguientes: grupos de disponibilidad de base de datos (DAG), copias de bases de datos de buzones, supervisión proactiva de rendimiento y administración de conmutación y conmutación por error.

**Contenido**

Database availability group management

Mailbox database copy management

Proactive monitoring

Switchovers and failovers

## Administración del grupo de disponibilidad de base de datos

Las tareas de administración operativa asociadas a los grupos de disponibilidad de base de datos incluyen:

  - **Creación de uno o más grupos de disponibilidad de base de datos**   La creación de un grupo de disponibilidad de base de datos suele ser un procedimiento que se realiza una vez durante la fase de implementación del ciclo de vida de la solución. Sin embargo, durante la fase operativa puede haber muchos motivos para crear grupos de disponibilidad de base de datos (DAG), por ejemplo:
    
      - El DAG está configurado para el modo de replicación de otros fabricantes y desea volver a usar la replicación continua. No se puede cambiar un DAG para la replicación continua; es necesario crear un grupo nuevo.
    
      - Tiene servidores en varios dominios. Todos los miembros de un DAG deben ser también miembros del mismo dominio.

  - **Administración de la pertenencia a un grupo de disponibilidad de base de datos**   Administrar miembros de un grupo de disponibilidad de base de datos (DAG) es una tarea que se realiza en raras ocasiones durante la fase de implementación del ciclo de vida de la solución. Sin embargo, debido a la flexibilidad que aporta la implementación incremental, también se puede administrar la pertenencia a grupos de disponibilidad de base de datos a lo largo del ciclo de vida de la solución.

  - **Configuración de las propiedades de un grupo de disponibilidad de base de datos**   Cada grupo de disponibilidad de base de datos (DAG) dispone de varias propiedades que pueden configurarse según sea necesario. Entre estas propiedades se incluyen:
    
      - **Servidor testigo y directorio testigo**   El servidor testigo es un servidor externo al grupo de disponibilidad de base de datos (DAG) que actúa como votante de quórum cuando un DAG contiene un número par de miembros. El directorio testigo es un directorio creado y compartido en el servidor testigo que usa el sistema para mantener un quórum.
    
      - **Direcciones IP**   Cada grupo de disponibilidad de base de datos dispone de una o más direcciones IPv4 y, opcionalmente, de una o más direcciones IPv6. Las direcciones IP asignadas al DAG las usa el clúster subyacente del DAG. El número de direcciones IPv4 asignadas al DAG es igual al número de subredes que componen la red MAPI que usa el DAG. Puede configurar el DAG para que use direcciones IP estáticas, o bien obtener direcciones de forma automática mediante el Protocolo de configuración dinámica de host (DHCP).
    
      - **Modo de coordinación de activación de centros de datos**   El modo de coordinación de activación de centros de datos es una configuración de propiedad en un DAG que está diseñada para prevenir la falta de comunicación entre los nodos de un clúster en el nivel de la base de datos, en un escenario en el que se restaura un servicio a un centro de datos principal después de realizar un cambio de centro de datos. Para obtener más información acerca del modo de coordinación de activación de centros de datos, consulte [Modo de coordinación de activación de centro de datos](datacenter-activation-coordination-mode-exchange-2013-help.md).
    
      - **Servidor testigo alternativo y directorio testigo alternativo**   El servidor testigo alternativo y el directorio testigo alternativo son valores que se pueden preconfigurar como parte del proceso de planeación para un cambio de centros de datos. Se refieren al servidor testigo y al directorio testigo que se usarán cuando se realiza un cambio de centro de datos.
    
      - **Puerto de replicación**   De forma predeterminada, todos los grupos de disponibilidad de base de datos usan el puerto TCP 64327 para la replicación continua. Puede modificar el grupo de disponibilidad de base de datos para que use otro puerto TCP para la replicación mediante el parámetro *ReplicationPort* del cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)).
    
      - **Detección de redes**   Puede forzar a un grupo de disponibilidad para que detecte redes e interfaces de red. Esta operación se usa cuando se agregan o quitan redes, o cuando se introducen nuevas subredes. Se puede forzar que se vuelvan a detectar las redes de DAG mediante el parámetro *DiscoverNetworks* del cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)).
    
      - **Compresión de red**   De forma predeterminada, los grupos de disponibilidad de base de datos usan compresión solamente entre redes DAG de diferentes subredes. Puede habilitar la compresión de todas las redes DAG o solo para operaciones de propagación, o bien puede deshabilitar la compresión de todas las redes DAG.
    
      - **Cifrado de red**   De forma predeterminada, los grupos de disponibilidad de base de datos usan cifrado solamente entre redes DAG de diferentes subredes. Puede habilitar el cifrado de todas las redes DAG o solo para operaciones de propagación, o bien puede deshabilitar el cifrado de todas las redes DAG.

  - **Apagado de miembros de grupos de disponibilidad de base de datos**   La solución de alta disponibilidad de Exchange 2013 está integrada en el proceso de apagado de Windows. Si un administrador o una aplicación inician el apagado de un servidor Windows en un DAG con una base de datos montada que se replica en uno o más miembros del DAG, el sistema intentará activar otra copia de las bases de datos montada antes de permitir que se complete el proceso de apagado. Sin embargo, este nuevo comportamiento no garantiza que todas las bases de datos del servidor que se va a apagar experimenten una activación sin pérdida. Por lo tanto, es mejor realizar una conmutación de servidor antes de apagar un servidor miembro de un grupo de disponibilidad de base de datos.

Para obtener instrucciones detalladas acerca de cómo crear un grupo de disponibilidad de base de datos, consulte [Crear un grupo de disponibilidad de base de datos](create-a-database-availability-group-exchange-2013-help.md). Para obtener instrucciones detalladas sobre cómo configurar DAG y las propiedades de un DAG, consulte [Configurar las propiedades del grupo de disponibilidad de base de datos](configure-database-availability-group-properties-exchange-2013-help.md). Para obtener más información acerca de cada una de las tareas anteriores, y sobre la administración de grupos de disponibilidad de base de datos en general, consulte [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md).

Volver al principio

## Administración de copias de base de datos de buzones de correo

Las tareas de administración operativa asociadas con las copias de base de datos de buzones incluyen:

  - **Agregar copias de bases de datos de buzones**   Cuando agrega una copia a la base de datos de buzones, se habilita automáticamente la replicación continua entre la base de datos existente y la copia de la base de datos.

  - **Configurar las propiedades de la copia de base de datos de buzones**   Puede configurar diferentes propiedades como, por ejemplo, la directiva de activación de base de datos, el periodo de retardo de reproducción y truncamiento (si lo hubiera) y la preferencia de activación para la copia de base de datos.

  - **Suspender o reanudar una copia de base de datos de buzones**   Puede suspender una copia de base de datos de buzones que se esté preparando para la propagación, o para otro tipo de tarea de mantenimiento. También puede suspender una copia de base de datos de buzones solo para activación. Esta configuración evita que el sistema active automáticamente la copia como resultado de un error, pero permite que el sistema mantenga actualizada la copia de la base de datos con respecto al envío y la reproducción de registros.

  - **Actualizar una copia de base de datos de buzones**   La actualización, también denominada *propagación*, es el proceso en el que se agrega una base de datos de buzones a otro servidor de buzones. Se convierte en la base de datos de línea de base para la copia. Tras la propagación inicial de la línea de base de la copia de base de datos, no será necesario volver a propagar la base de datos, salvo raras excepciones.

  - **Activar una copia de base de datos de buzones**   La activación de una copia de base de datos de buzones consiste en designar una determinada copia pasiva como la nueva copia activa de una base de datos de buzones. Se hace referencia a este proceso como *conmutación*. Para obtener más información, consulte "Conmutaciones y conmutaciones por error" más adelante en este tema.

  - **Quitar una copia de base de datos de buzones**   Puede quitar una copia de base de datos de buzones en cualquier momento. En ocasiones, puede ser necesario quitar una copia de una base de datos de buzones. Por ejemplo, no puede quitar un servidor de buzones de un grupo de disponibilidad de base de datos hasta que todas las copias de bases de datos de buzones se hayan eliminado del servidor. Además, debe quitar todas las copias de una base de datos de buzones antes de cambiar la ruta de una base de datos de buzones.

Para obtener más información sobre cómo agregar una copia de base de datos de buzones, consulte [Adición de una copia de base de datos de buzones](add-a-mailbox-database-copy-exchange-2013-help.md). Para obtener instrucciones detalladas acerca de cómo configurar copias de bases de datos de buzones, consulte [Configuración de las propiedades de una copia de base de datos de buzones](configure-mailbox-database-copy-properties-exchange-2013-help.md). Para obtener más información acerca de cada una de las tareas anteriores, y sobre la administración de copias de bases de datos de buzones en general, consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md). Para obtener más información sobre cómo quitar una copia de base de datos de buzones, consulte [Eliminación de una copia de base de datos de buzones](remove-a-mailbox-database-copy-exchange-2013-help.md).

Volver al principio

## Supervisión proactiva

Asegurarse de que los servidores funcionan de forma confiable y que las copias de base de datos están en buen estado son los objetivos clave para las operaciones diarias de mensajería. Exchange 2013 incluye una serie de características que se pueden usar para realizar diferentes tareas de supervisión de mantenimiento en grupos de disponibilidad de base de datos y copias de bases de datos de buzones, incluidas las siguientes:

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/es-es/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/es-es/library/bb691314\(v=exchg.150\))

  - Registro de eventos de canal Crimson

Además de supervisar el mantenimiento y el estado, también es importante supervisar las situaciones que pueden poner en peligro la disponibilidad. Por ejemplo, se recomienda que supervise la redundancia de las bases de datos replicadas. Esto es fundamental para evitar situaciones en las que solamente dispone de una copia de una base de datos. Este escenario debe tratarse con la máxima prioridad y resolverse lo antes posible.

Para obtener información detallada acerca de cómo supervisar el estado y el mantenimiento de grupos de disponibilidad de base de datos y copias de bases de datos de buzones, consulte [Supervisión de grupos de disponibilidad de base de datos](monitoring-database-availability-groups-exchange-2013-help.md).

Volver al principio

## Cambios y conmutaciones por error

Una *conmutación* es un proceso manual en el que un administrador activa una o más copias de una base de datos de buzones. Estas conmutaciones, que se pueden producir en la base de datos o en el servidor, suelen realizarse como parte de la preparación de actividades de mantenimiento. La administración de las conmutaciones implica realizar conmutaciones en bases de datos y servidores, según sea necesario. Por ejemplo, si necesita realizar el mantenimiento en un servidor de buzones de un grupo de disponibilidad de base de datos, primero haría una conmutación de servidor para que el servidor no hospede ninguna copia de base de datos activa. Para obtener instrucciones detalladas acerca de cómo realizar un cambio de base de datos, consulte [Activación de una copia de base de datos de buzones](activate-a-mailbox-database-copy-exchange-2013-help.md). Los cambios se pueden realizar en los centros de datos.

Una *conmutación por error* es la activación automática por parte del sistema de una o más copias de base de datos en respuesta a un error. Por ejemplo, la pérdida de una unidad de disco en un entorno sin RAID desencadenará un error de la base de datos. La pérdida de la red MAPI o una conmutación por error de energía desencadenarán una conmutación por error de servidor.

Volver al principio

