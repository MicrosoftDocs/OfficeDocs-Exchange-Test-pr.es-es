---
title: 'Implementación alta disponibilidad y resistencia de sitios: Exchange 2013 Help'
TOCTitle: Implementación de alta disponibilidad y resistencia de sitios
ms:assetid: 4c4e00a4-1f57-4fdb-b9b2-2779abf381a9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638129(v=EXCHG.150)
ms:contentKeyID: 48268096
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implementación de alta disponibilidad y resistencia de sitios

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Microsoft Exchange Server 2013 utiliza, tanto para la alta disponibilidad como para la resistencia de sitio, un concepto conocido como *implementación incremental*. Simplemente, instale dos o más servidores de buzones de correo de Exchange 2013 como servidores independientes y, luego, configúrelos de manera incremental junto con las bases de datos de buzones de correo para que haya una alta disponibilidad y resistencia de sitios según sea necesario.

## Introducción al proceso de implementación

Si bien los pasos concretos que cada organización utiliza pueden variar levemente, el proceso general de implementación de Exchange 2013 en una configuración de alta disponibilidad o de sitio resistente, es generalmente el mismo. Después de llevar a cabo la planeación y las tareas de diseño necesarias para desarrollar e implementar un grupo de disponibilidad de base de datos (DAG) y crear copias de bases de datos de buzones de correo, es necesario:

1.  Crear un DAG. Para obtener instrucciones detalladas, vea [Crear un grupo de disponibilidad de base de datos](create-a-database-availability-group-exchange-2013-help.md).

2.  Si es necesario, preconfigure el objeto de nombre de clúster (CNO). Se requiere la preconfiguración de CNO al implementar un DAG con servidores de buzones de correo que ejecutan Windows Server 2012. Si va a implementar un DAG sin un punto de acceso administrativo mediante servidores de buzones de correo que ejecutan Windows Server 2012 R2, no necesita preconfigurar un CNO. La preconfiguración también se requiere en entornos en los que la creación de cuentas de equipo esté restringida, o en los que las cuentas de equipo se crean en un contenedor que no sea el predeterminado para el equipo. Para conocer los pasos detallados, vea [Preconfiguración del objeto de nombre de clúster para un grupo de disponibilidad de base de datos](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

3.  Agregar dos o más servidores de buzones de correo al DAG. Para obtener instrucciones detalladas, vea [Administración de la pertenencia a grupos de disponibilidad de base de datos](manage-database-availability-group-membership-exchange-2013-help.md).

4.  Configurar las propiedades del DAG según sea necesario:
    
    1.  De manera opcional, configure el cifrado y la compresión del DAG, el puerto de replicación, las direcciones IP del DAG y otras propiedades. Para obtener instrucciones detalladas, vea [Configurar las propiedades del grupo de disponibilidad de base de datos](configure-database-availability-group-properties-exchange-2013-help.md).
    
    2.  Habilite el modo de coordinación de activación del centro de datos (CAD) del DAG. Esto protege al DAG de las condiciones de cerebro dividido en el nivel de la base de datos durante el cambio al centro de datos principal después de que se haya realizado una operación de cambio de centro de datos, y permite el uso de los cmdlets de recuperación del DAG integrados. Para obtener más información, vea [Modo de coordinación de activación de centro de datos](datacenter-activation-coordination-mode-exchange-2013-help.md).

5.  Agregar copias de la base de datos de buzones de correo en todos los servidores de buzones de correo del DAG. Para obtener instrucciones detalladas, vea [Adición de una copia de base de datos de buzones](add-a-mailbox-database-copy-exchange-2013-help.md).

## Ejemplo de implementación: DAG de cuatro miembros en dos centros de datos

En este ejemplo, se describe cómo la organización Contoso Ltd. configura e implementa un DAG de cuatro miembros que se extenderá a través de dos ubicaciones físicas: Redmond, Washington y Portland, Oregón.

## Infraestructura de base

Cada ubicación contiene los elementos de infraestructura necesarios para operar una infraestructura de mensajería basada en Exchange 2013, a saber:

  - Servicios de directorio (Active Directory o Servicios de dominio de Active Directory (AD DS))

  - Resolución de nombres del Sistema de nombres de dominio (DNS)

  - Varios servidores de acceso de clientes de Exchange 2013

  - Varios servidores de buzones de correo de Exchange 2013

En la siguiente figura, se ilustra la configuración de Contoso.

**Grupo de disponibilidad de base de datos extendido en dos sitios**

![Grupo de disponibilidad de base de datos extendido a dos sitios](images/Dd638129.1c326fd4-3c7b-4416-a63d-fbfdd0cc6b18(EXCHG.150).gif "Grupo de disponibilidad de base de datos extendido a dos sitios")

## Configuración de red

Tal como se ilustra en la figura anterior, la solución involucra el uso de varias subredes y redes. Cada servidor de buzones de correo del DAG tiene dos adaptadores de red en subredes diferentes. En cada servidor de buzones de correo, uno de los adaptadores de red se utilizará para la red MAPI (192.168.*x*.*x*) y el otro para la red de replicación (10.0.*x*.*x*). Sólo la red MAPI proporciona conectividad a Active Directory, a los servicios DNS y a otros servidores y clientes de Exchange. El adaptador utilizado para la red de replicación de cada miembro proporciona conectividad solamente a los adaptadores de red de replicación de los otros miembros del DAG.

En la siguiente tabla se detalla la configuración de todos los adaptadores de red de cada nodo.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre</th>
<th>Dirección IPv4</th>
<th>Máscara de subred</th>
<th>Puerta de enlace predeterminada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MBX1 (MAPI)</p></td>
<td><p>192.168.1.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (MAPI)</p></td>
<td><p>192.168.1.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (MAPI)</p></td>
<td><p>192.168.2.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (MAPI)</p></td>
<td><p>192.168.2.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX1 (replicación)</p></td>
<td><p>10.0.1.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Ninguno</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (replicación)</p></td>
<td><p>10.0.1.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Ninguno</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (replicación)</p></td>
<td><p>10.0.2.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Ninguno</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (replicación)</p></td>
<td><p>10.0.2.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Ninguno</p></td>
</tr>
</tbody>
</table>


Como se muestra en la tabla anterior, los adaptadores utilizados para las redes de replicación no utilizan puertas de enlace predeterminadas. Para brindar conectividad de red entre cada uno de los adaptadores de red de replicación, Contoso usa rutas estáticas persistentes, que se configuran mediante la herramienta Netsh.exe.

Para configurar el enrutamiento de los adaptadores de red de replicación en MBX1 y MBX2 se ejecutó el siguiente comando en cada servidor.

```powershell
netsh interface ipv4 add route 10.0.2.0/24 <NetworkName> 10.0.1.254
```

Para configurar el enrutamiento de los adaptadores de red de replicación en MBX3 y MBX4 se ejecutó el siguiente comando en cada servidor.

```powershell
netsh interface ipv4 add route 10.0.1.0/24 <NetworkName> 10.0.2.254
```

También se han configurado los siguientes parámetros de red adicionales:

  - La casilla de verificación **Registrar estas direcciones de conexiones en DNS** se selecciona para cada adaptador de red MAPI del miembro DAG y se la destilda para cada adaptador de red de replicación.

  - Al menos una dirección de servidor DNS está configurada para cada adaptador de red MAPI del miembro DAG y ninguna está configurada para los adaptadores de red de replicación. Para conseguir redundancia, Contoso utiliza múltiples direcciones de servidor DNS en los adaptadores de red MAPI.

  - Además, no utiliza Firewall de Windows, y está desactivado en los servidores.

Después de configurar los adaptadores de red, Contoso está listo para crear un DAG y agregarle los servidores de buzones de correo.

## Creación y configuración de grupos de disponibilidad de base de datos

El administrador ha decidido crear un script de interfaz de línea de comandos de Windows PowerShell que realiza varias tareas:

  - Utiliza el cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd351107\(v=exchg.150\)) para crear el DAG. Dado que REDMOND se considera el centro de datos principal, Contoso decidió usar un servidor testigo en el mismo centro de datos, CAS1.

  - Utiliza el cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)) para preconfigurar un servidor testigo alternativo y un directorio testigo alternativo en caso de que sea necesaria una conmutación de centro de datos.

  - Utiliza el cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/es-es/library/dd298049\(v=exchg.150\)) para agregar cada uno de los cuatro servidores de buzones de correo al DAG.

  - Utiliza el cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)) para configurar el DAG en el modo DAC. Para obtener más información acerca del modo DAC, vea [Modo de coordinación de activación de centro de datos](datacenter-activation-coordination-mode-exchange-2013-help.md).

Los comandos utilizados en el script son:

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer CAS1 -WitnessDirectory C:\DAGWitness\DAG1.contoso.com -DatabaseAvailabilityGroupIPAddresses 192.168.1.8,192.168.2.8

El comando anterior crea el DAG DAG1, configura el servidor CAS1 para que actúe como servidor testigo, configura un directorio testigo específico (C:\\DAGWitness\\DAG1.contoso.com) y configura dos direcciones IP para el DAG (una para cada subred de la red MAPI).

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGWitness\DAG1.contoso.com -AlternateWitnessServer CAS4

El comando anterior configura el grupo DAG1 para que use CAS4 como servidor testigo alternativo y un directorio testigo alternativo en CAS4 que usa la misma ruta de acceso que se configuró en CAS1.


> [!NOTE]
> No es necesario utilizar la misma ruta de acceso; Contoso decidió hacerlo para estandarizar su configuración.



    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX3
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX4

Los comandos anteriores agregan cada uno de los servidores de buzones de correo, uno por vez, al DAG. Los comandos también instalan el componente de clúster de conmutación por error de Windows en cada servidor de buzones de correo (si no está ya instalado), crean una agrupación en clústeres de conmutación por error de Windows y vinculan cada servidor de buzones de correo al clúster recién creado.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly
```

El comando anterior habilita el modo DAC para el DAG.

## Bases de datos de buzones de correo y copias

Después de crear el DAG y agregar los servidores de buzones de correo al DAG, Contoso se prepara para crear bases de datos de buzones de correo y copias de éstas. Para cumplir con su criterio de resistencia a errores, Contoso está planeando configurar cada base de datos de buzones de correo con tres copias de bases de datos no atrasadas y una copia de base de datos atrasada. La copia atrasada tendrá configurado un retraso de la reproducción del registro de tres días.

Esta configuración proporciona un total de cuatro copias para cada base de datos (una activa, dos pasivas no atrasadas y una pasiva atrasada). Contoso planea tener cuatro bases de datos activas por servidor. Con cuatro bases de datos activas por servidor y tres copias pasivas de cada base de datos, la solución de Contoso contiene un total de 16 copias de bases de datos.

Como se muestra en la figura siguiente, Contoso tiene un diseño equilibrado de sus bases de datos.

**Diseño de la copia de base de datos de Contoso, Ltd**

![Diseño de la copia de base de datos de Contoso, Ltd](images/Dd638129.41d0c78e-ccaf-4b67-8bab-6fb344668ead(EXCHG.150).gif "Diseño de la copia de base de datos de Contoso, Ltd")

Cada servidor de buzones de correo hospeda una copia de base de datos de buzones de correo, dos copias pasivas no atrasadas y una copia pasiva atrasada. La copia atrasada de cada base de datos de buzones de correo activa se hospeda en un servidor de buzones de correo del otro sitio.

Para crear esta configuración, el administrador ejecuta varios comandos.

En MBX1, ejecute los siguientes comandos.

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -SuspendComment "Seed from MBX4" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB1\MBX3 -SourceServer MBX4
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -ActivationOnly

En MBX2, ejecute los siguientes comandos.

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -SuspendComment "Seed from MBX3" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB2\MBX4 -SourceServer MBX3
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -ActivationOnly

En MBX3, ejecute los siguientes comandos.

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -SuspendComment "Seed from MBX2" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB3\MBX1 -SourceServer MBX2
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -ActivationOnly

En MBX4, ejecute los comandos siguientes.

    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX2 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -SuspendComment "Seed from MBX1" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB4\MBX2 -SourceServer MBX1
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -ActivationOnly

En los ejemplos anteriores para el cmdlet **Add-MailboxDatabaseCopy**, no se ha especificado el parámetro *ActivationPreference*. La tarea incrementa el número de preferencia de activación automáticamente con cada copia que se agrega. La base de datos original siempre tiene un número de preferencia 1. A la primera copia agregada con el cmdlet **Add-MailboxDatabaseCopy** se le asigna automáticamente el número de preferencia 2. Siempre y cuando no se quiten copias, la siguiente copia agregada recibirá el número de preferencia 3, y así sucesivamente. Por lo tanto, en los ejemplos anteriores, la copia pasiva en el mismo centro de datos que la copia activa tiene un número de preferencia de activación 2, la copia pasiva no atrasada en el centro de datos remoto tiene un número de preferencia de activación 3 y la copia pasiva atrasada en el centro de datos remoto tiene un número de preferencia de activación 4.

Si bien hay dos copias de cada base de datos activa a través de la WAN de la otra ubicación, la propagación sobre la WAN sólo se llevó a cabo una vez. Esto se debe a que Contoso está aprovechando la capacidad de Exchange 2013 de utilizar una copia pasiva de base de datos como fuente para la propagación. El uso del cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298105\(v=exchg.150\)) con el parámetro *SeedingPostponed* evita que la tarea propague automáticamente la nueva copia de base de datos creada. Así, el administrador puede suspender la copia no propagada y, mediante el uso del cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)) con el parámetro *SourceServer*, puede especificar la copia local de la base de datos como fuente de la operación de propagación. Como resultado, la propagación de la segunda copia de la base de datos agregada a cada ubicación se realiza localmente y no sobre la WAN.


> [!NOTE]
> En el ejemplo anterior, la copia de la base de datos no atrasada se propaga sobre la WAN y, a continuación, se la utiliza para propagar la copia atrasada de la base de datos que se encuentra en el mismo centro de datos que la copia no atrasada.



Contoso ha configurado una de las copias pasivas de cada base de datos de buzones de correo como copia atrasada, para proporcionar una protección contra el inusual pero catastrófico caso de que se produzcan daños lógicos en la base de datos. Por lo tanto, el administrador configura las copias atrasadas con activación bloqueada mediante el uso del cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd351074\(v=exchg.150\)) con el parámetro *ActivationOnly*. Esto asegura que las copias de la base de datos atrasadas no se activen si se produce un error de base de datos o servidor.

## Validación de la solución

Después de implementar y configurar la solución, el administrador lleva a cabo varias acciones que validan la preparación del sistema, antes de mover los buzones de producción a las bases de datos del DAG. Se debe someter la solución a varios métodos de prueba e inspección, incluida la simulación de errores. Para validar la solución, el administrador realiza varias tareas.

Para comprobar el mantenimiento global del DAG, el administrador ejecuta el cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/es-es/library/bb691314\(v=exchg.150\)). Este cmdlet comprueba varios aspectos del estado de la replicación y la reproducción, para proporcionar información acerca de los servidores de buzones de correo y la copia de base de datos del DAG.

Para comprobar la actividad de replicación y reproducción, el administrador ejecuta el cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/es-es/library/dd298044\(v=exchg.150\)). Este cmdlet puede proporcionar información de estado en tiempo real acerca de una copia de base de datos de buzones de correo específica ubicada en un servidor específico. Para obtener más información acerca de cómo supervisar el mantenimiento y el estado de las bases de datos replicadas de un DAG, vea [Supervisión de grupos de disponibilidad de base de datos](monitoring-database-availability-groups-exchange-2013-help.md).

Para comprobar que los cambios funcionen como está previsto, el administrador usa el cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/es-es/library/dd298068\(v=exchg.150\)) para realizar una serie de cambios de base de datos y de servidor. Una vez que estas tareas se completan con éxito, el administrador utiliza el mismo cmdlet para devolver las copias de base de datos activas a sus ubicaciones originales.

Para comprobar el comportamiento esperado en varios escenarios de error, el administrador realiza varias tareas que simulan errores o los causan realmente. Por ejemplo, el administrador puede:

  - Desconectar el cable de alimentación en MBX1, lo que desencadena una conmutación por error de un servidor. Luego, el administrador comprueba que DB1 se active en otro servidor (preferentemente MBX2, de acuerdo con los valores de preferencia de activación).

  - Desconectar el cable de red del adaptador de red MAPI de MBX2, desencadenando una conmutación por error de servidor. Luego, el administrador comprueba que DB2 se active en otro servidor (preferentemente MBX1, de acuerdo con los valores de preferencia de activación).

  - Desconectar el disco utilizado por la copia activa de DB3, desencadenando una conmutación por error de base de datos. Luego, el administrador comprueba que DB3 se active en otro servidor (preferentemente MBX4, de acuerdo con los valores de preferencia de activación).

Es posible que la organización compruebe otros escenarios de conmutación por error, de acuerdo con las necesidades de la empresa. Después de simular un error individual (como desenchufar el cable de alimentación) y comprobar el comportamiento de recuperación de la solución, el administrador puede volverla a su configuración original. En algunos casos, se puede probar la solución para varios errores simultáneos. En última instancia, el plan de pruebas creado para la solución determinará si se la devuelve a su configuración original después de cada simulación de error realizada.

De manera adicional, un administrador puede decidir interrumpir la conexión de red entre los dos centros de datos, simulando así un error en el sitio. La realización de un cambio de centros de datos es un proceso mucho más complejo y coordinado; no obstante, si la solución implementada se diseñó para proporcionar resistencia de sitio a los servicios y datos de mensajería, se recomienda llevarlo a cabo.

## Transición a operaciones

Una vez implementada la solución, se la puede extender aún más mediante una implementación incremental. En este punto, la administración de la solución también realiza una transición a procesos de operación, en los que se llevan a cabo las siguientes tareas:

  - Supervisión del mantenimiento y el estado de los DAG y las copias de la base de datos de buzones de correo. Para obtener más información, vea [Supervisión de grupos de disponibilidad de base de datos](monitoring-database-availability-groups-exchange-2013-help.md).

  - Realice cambios de bases de datos según sea necesario. Para obtener instrucciones detalladas acerca de cómo realizar un cambio de base de datos, vea [Activación de una copia de base de datos de buzones](activate-a-mailbox-database-copy-exchange-2013-help.md).

Para obtener más información acerca de la administración de la solución, vea [Administración de alta disponibilidad y resistencia de sitios](managing-high-availability-and-site-resilience-exchange-2013-help.md).

