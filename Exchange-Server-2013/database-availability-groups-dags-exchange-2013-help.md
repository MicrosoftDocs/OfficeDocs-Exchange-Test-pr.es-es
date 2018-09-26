---
title: 'Grupos de disponibilidad de base de datos (DAG): Exchange 2013 Help'
TOCTitle: Grupos de disponibilidad de base de datos (DAG)
ms:assetid: ab9b88ce-2f44-4334-96ad-a666b95888a0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd979799(v=EXCHG.150)
ms:contentKeyID: 48268545
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Grupos de disponibilidad de base de datos (DAG)

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-06-04_

Obtenga más información sobre Exchange DAG en Exchange Server 2013. En este artículo se describe el ciclo de vida de los grupos de disponibilidad de base de datos (DAG), así como el uso de un DAG para obtener alta disponibilidad y resistencia de sitios.

Un grupo de disponibilidad de base de datos (DAG) es el componente básico del marco de alta disponibilidad y resistencia de sitios del servidor de buzones que ofrece Microsoft Exchange Server 2013. Se trata de un grupo de hasta 16 servidores de buzones de correo que aloja un conjunto de bases de datos y proporciona recuperación automática en el nivel de la base de datos de los errores que afectan a los servidores o bases de datos individuales.

Un DAG es un límite para la replicación de bases de datos de buzones, los cambios de bases de datos y de servidores, y las conmutaciones por error así como para un componente interno denominado *Active Manager*. Active Manager, que se ejecuta en todos los servidores de buzones, administra los cambios y las conmutaciones por error en el DAG. Para obtener más información acerca de Active Manager, consulte [Active Manager](active-manager-exchange-2013-help.md).

Cualquier servidor en un DAG puede hospedar una copia de una base de datos de buzones de correo de cualquier otro servidor en el DAG. Cuando se agrega un servidor a un DAG, funciona con los otros servidores del DAG para proporcionar recuperación automática de errores que afectan a las bases de datos de buzones, como un error de disco, de servidor o de red.

**Contenido**

Ciclo de vida de los grupos de disponibilidad de base de datos (DAG)

Usar un grupo de disponibilidad de base de datos (DAG) para obtener alta disponibilidad

Usar un grupo de disponibilidad de base de datos (DAG) para obtener resistencia de sitios

## Ciclo de vida de los grupos de disponibilidad de base de datos (DAG)

Los DAG aprovechan el concepto de la *implementación incremental*, que es la capacidad de implementar la disponibilidad de servicios y datos en todos los servidores y bases de datos de buzones una vez que se haya instalado Exchange. Tras la implementación de los servidores Buzón de correo de Exchange 2013, se puede crear un DAG, agregar servidores de buzones de correo y, a continuación, replicar las bases de datos de buzones entre los miembros del DAG.


> [!NOTE]
> Admite la creación de un DAG que contenga una combinación de servidores de buzones de correo físicos y servidores de buzones de correo virtualizados, siempre y cuando los servidores y la solución cumplan con <A href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos del sistema para Exchange&nbsp;2013</A> y los requisitos establecidos en <A href="exchange-2013-virtualization-exchange-2013-help.md">Virtualización de Exchange 2013</A>. Como en todas las configuraciones de alta disponibilidad de Exchange, se debe garantizar que el tamaño de todos los servidores de buzones de correo del DAG se haya determinado adecuadamente para poder controlar la carga de trabajo necesaria durante interrupciones programadas y no programadas.



Los DAG se crean con el cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd351107\(v=exchg.150\)). Inicialmente se crean como objetos vacíos en Active Directory. Este objeto de directorio se usa para almacenar información relevante acerca del DAG, como la información de suscripción del servidor y algunas configuraciones del DAG. Al agregar el primer servidor a un DAG, se crea automáticamente un clúster de conmutación por error para el DAG. El DAG usa de manera exclusiva este clúster de conmutación por error; dicho clúster debe dedicarse al DAG. El uso del clúster no se permite para ninguna otra finalidad.

Además de crearse un clúster de conmutación por error, se inicia la infraestructura que supervisa los servidores en busca de errores en la red o el servidor. El mecanismo de latidos del clúster de conmutación por error y la base de datos del clúster se usan para administrar la información sobre el DAG que puede cambiar rápidamente (como el estado de montaje de la base de datos, el estado de replicación y la última ubicación de montaje) y para realizar un seguimiento de dicha información.

Mientras se crea, el DAG recibe un nombre único y una o varias direcciones IP estáticas, o bien se configura para que use el Protocolo de configuración dinámica de host (DHCP) o se crea sin un punto de acceso administrativo del clúster. Solo podrá crear los DAG sin ningún punto de acceso administrativo en servidores que ejecuten Exchange 2013 Service Pack 1 o una versión posterior en Windows Server 2012 R2, versión Standard o Datacenter Edition. Estas son las características de los DAG sin puntos de acceso administrativo del clúster:

  - No hay ninguna dirección IP asignada al clúster o al DAG y, por lo tanto, tampoco hay un recurso de dirección IP en el grupo de recursos principal del clúster.

  - No hay un nombre de red asignado al clúster y, por lo tanto, tampoco un recurso Nombre de red en el grupo de recursos principal del clúster

  - El nombre del clúster o del DAG no están registrados en DNS y no se puede resolver en la red.

  - No hay un objeto de nombre clúster (CNO) creado en Active Directory.

  - El clúster no se puede administrar mediante la herramienta Administración del clúster de conmutación por error. Se debe administrar mediante Windows PowerShell y los cmdlets de PowerShell se deben volver a ejecutar en cada miembro de clúster individual.

Este ejemplo muestra cómo usar el Shell para crear un DAG con un punto de acceso administrativo del clúster que tendrá tres servidores. Dos servidores (EX1 y EX2) están en la misma subred (10.0.0.0); el tercero (EX3) está en otra (192.168.0.0).

```powershell
New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer EX4 -DatabaseAvailabilityGroupIPAddresses 10.0.0.5,192.168.0.5
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX1
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX2
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX3
```

Los comandos para crear un DAG sin un punto de acceso administrativo del clúster son muy similares:

```powershell
New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer EX4 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress])::None
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX1
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX2
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX3
```

El clúster para DAG1 se crea al agregar EX1 al DAG. Durante la creación de clústeres, el cmdlet **Add-DatabaseAvailabilityGroupServer** recupera las direcciones IP configuradas para el DAG e ignora las que no coinciden con ninguna de las subredes halladas en EX1. En el primer ejemplo, el clúster para DAG1 se crea con la dirección IP 10.0.0.5, mientras que 192.168.0.5 no se tiene en cuenta. En el segundo ejemplo de arriba, el valor del parámetro *DatabaseAvailabilityGroupIPAddresses* indica a la tarea que cree un clúster de conmutación por error para el DAG que no tiene punto de acceso administrativo. Por tanto, el clúster se crea con un recurso de dirección IP o de nombre de red en el grupo de recursos principal del clúster.

A continuación, se agrega EX2 y el cmdlet **Add-DatabaseAvailabilityGroupServer** recupera de nuevo las direcciones IP configuradas para el DAG. Las direcciones IP del clúster no cambian porque EX2 está en la misma subred que EX1.

A continuación, se agrega EX3 y el cmdlet **Add-DatabaseAvailabilityGroupServer** recupera de nuevo las direcciones IP configuradas para el DAG. Puesto que en EX3 hay una subred que coincide con 192.168.0.5, la dirección 192.168.0.5 se agrega como recurso de dirección IP al grupo de clústeres. Además, se configura automáticamente una dependencia **OR** para el recurso Nombre de red de cada recurso de dirección IP. El clúster usará la dirección 192.168.0.5 cuando el grupo de recursos principal del clúster se mueva a EX3.

Para los DAG con puntos de acceso administrativo del clúster, la agrupación en clústeres de conmutación por error de Windows registra las direcciones IP del clúster en el Sistema de nombres de dominio (DNS) cuando el recurso Nombre de red se pone en línea. Además, cuando EX1 se agrega al clúster, se crea un objeto de nombre de clúster (CNO) en Active Directory. El nombre de red, las direcciones IP y el CNO para el clúster no se usan en las funciones del DAG. Los administradores y los usuarios finales no necesitan conectarse a la dirección IP ni al nombre del DAG o del clúster, ni usarlos como interfaz. Algunas aplicaciones de terceros se conectan al punto de acceso administrativo del clúster para realizar tareas de administración, como copia de seguridad o supervisión. Si no usa ninguna aplicación de terceros que requiera un punto de acceso administrativo del clúster, y el DAG ejecuta Exchange 2013 SP1 o una versión posterior en Windows Server 2012 R2, le recomendamos que cree un DAG sin un punto de acceso administrativo. Conseguirá que el proceso de configuración del DAG sea más sencillo, ya no necesitará una o varias direcciones IP y reducirá la superficie de ataque del DAG.

Los DAG también se configuran para usar un servidor testigo y un directorio testigo. El sistema configura automáticamente el servidor testigo y el directorio testigo, aunque también los puede configurar manualmente el administrador. En los ejemplos anteriores, EX4 (un servidor que no forma parte del DAG ni lo hará en el futuro) se está configurando manualmente como el servidor testigo del DAG.

De manera predeterminada, un DAG se diseña para que utilice la característica integrada de replicación continua y replique las bases de datos de buzones entre sus servidores. Si utiliza una replicación de datos de terceros que admite la API de replicación de terceros de Exchange 2013, deberá crear el DAG en el modo de replicación de terceros mediante el cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd351107\(v=exchg.150\)) con el parámetro *ThirdPartyReplication*. Una vez habilitado este modo, no se puede deshabilitar.

Una vez creado el DAG, se le pueden agregar servidores de buzones de correo. Cuando se agrega el primer servidor al DAG, se forma un clúster para que el DAG lo utilice. Los DAG hacen uso de la tecnología de clúster de conmutación por error de Windows, como el latido de clúster, las redes de clústeres y la base de datos de clústeres (para almacenar datos que cambian, por ejemplo el estado de base de datos que cambia de activa a pasiva y viceversa, o de montada a desmontada y viceversa). Al irse agregando al DAG cada uno de los siguientes servidores, se une al clúster subyacente, el Exchange ajusta automáticamente el modelo de quórum del clúster y el servidor se agrega al objeto DAG en Active Directory.

Una vez que se han agregado servidores de buzones de correo al DAG, se pueden configurar algunas de las propiedades de este último, por ejemplo si se debe usar el cifrado de red o la compresión de red para la replicación de bases de datos en el DAG. También se pueden configurar las redes de DAG y crear más.

Una vez que se han agregado miembros al DAG y éste se ha configurado, las bases de datos de buzones activas de cada servidor se pueden replicar en los demás miembros del DAG. Después de crear copias de las bases de datos de buzones, se puede supervisar su estado de mantenimiento con varias herramientas de supervisión integradas. Además, puede realizar cambios de base de datos y servidores.

Para obtener más información sobre la creación de DAG, la administración de los miembros de los DAG, la configuración de propiedades de los DAG, la creación y supervisión de copias de bases de datos de buzones, y la realización de cambios, consulte [Administración de alta disponibilidad y resistencia de sitios](managing-high-availability-and-site-resilience-exchange-2013-help.md).

## Modelos de cuórum de los grupos de disponibilidad de base de datos (DAG)

Debajo de cada DAG hay un clúster de conmutación por error de Windows. Los clústeres de conmutación por error utilizan el concepto de quórum, que emplea un consenso de votantes para garantizar que solamente un subconjunto de miembros del clúster (que podría ser todos los miembros o una mayoría de miembros) funcione a la vez. El quórum no es un concepto nuevo para Exchange 2013. Los servidores Buzón de correos de alta disponibilidad de versiones anteriores de Exchange usan también la agrupación en clústeres de conmutación por error y su concepto de quórum. El quórum representa una visión compartida de los miembros y los recursos, y el quórum de término también se utiliza para describir los datos físicos que representan la configuración dentro del clúster que se comparte entre todos los miembros del mismo. A consecuencia de ello, todos los DAG necesitan su clúster de conmutación por error subyacente para tener quórum. Si el clúster pierde quórum, todas las operaciones del DAG terminarán y todas las bases de datos albergadas en el mismo se desmontarán. En este caso, es necesario que intervenga el administrador para corregir el problema de quórum y restaurar las operaciones del DAG.

El quórum es importante para asegurar la coherencia, como mecanismo para resolver empates y como garantía de la capacidad de respuesta de los clústeres:

  - **Garantizar la coherencia**   Un requisito fundamental para un clúster de conmutación por error de Windows es que cada uno de sus miembros tenga siempre una vista del clúster que sea coherente con los otros miembros. La sección del clúster actúa como repositorio definitivo de toda la información de configuración relativa al clúster. Si la sección del clúster no puede cargarse localmente en un miembro del DAG, el servicio del clúster no se inicia al no poder garantizar que el miembro cumpla el requisito de tener una vista del clúster que sea coherente con los otros miembros.

  - **Mecanismo para resolución de empates**   Se usa en los DAG un recurso de testigo de quórum con un número par de miembros para evitar el síndrome de cerebro dividido y asegurarse de que solamente se considere oficial una colección de los miembros del DAG. Cuando el servidor testigo se necesita para quórum, cualquier miembro del DAG que pueda comunicarse con el servidor testigo puede colocar un bloqueo de Bloque de mensajes del servidor en el archivo witness.log del servidor testigo. El miembro del DAG que bloquea el servidor testigo (denominado *nodo de bloqueo*) retiene un voto adicional por motivos de quórum. Los miembros del DAG que están en contacto con el nodo de bloqueo son mayoría y mantienen el quórum. Cualquier miembro del DAG que no pueda estar en contacto con el nodo de bloqueo forma parte de la minoría y por lo tanto pierde el quórum.

  - **Asegurar la capacidad de respuesta**   Para garantizar la capacidad de respuesta, el modelo de quórum se asegura de que, siempre que se ejecute el clúster, estén operativos y comunicativos suficientes miembros del sistema distribuido, y de que se garantice al menos una réplica del estado actual del clúster. No se necesita tiempo adicional para poner en conexión otros miembros ni para determinar si está garantizada un réplica en concreto.

Los DAG con un número par de miembros usan el modo de quórum Mayoría de recursos compartidos de archivos y nodo del clúster, que emplea un servidor testigo externo que ejerce de mecanismo para resolver empates. En este modo de quórum, cada miembro de DAG obtiene un voto. Asimismo, el servidor testigo se usa para proporcionar a un miembro de DAG un voto ponderado (por ejemplo, obtiene dos votos en vez de uno). Los datos del quórum de clúster se almacenan de forma predeterminada en el disco del sistema de cada miembro del DAG y se mantienen coherentes en esos discos. Sin embargo, no se guarda una copia de los datos del quórum en el servidor testigo. Se utiliza un archivo en el servidor testigo para mantener un seguimiento del miembro que tiene la copia de datos más actualizada, pero el servidor testigo no tiene una copia de los datos de quórum del clúster. En este modo, una mayoría de los votantes (los miembros del DAG más el servidor testigo) deben estar operativos y poderse comunicar entre sí para mantener el quórum. Si la mayoría de los votantes no pueden comunicarse entre sí, el clúster subyacente del DAG pierde el quórum y para que el DAG vuelva a estar operativo requerirá una intervención del administrador.

Los DAG con un número impar de miembros usan un modo de quórum de nodos mayoritarios. En este modo, cada miembro obtiene un voto y el disco del sistema local de cada miembro se usa para almacenar los datos de quórum del clúster. Si la configuración del clúster cambia, ese cambio se refleja en todos los discos. El cambio solamente se considera efectuado y permanente si se realiza en los discos de la mitad de los miembros (redondeado) más uno. Por ejemplo, en un DAG de cinco miembros, el cambio debe efectuarse en dos miembros más uno, o en un total de tres miembros.

El quórum precisa una mayoría de votantes para que puedan comunicarse entre sí. Suponga un DAG con cuatro miembros. Como este DAG tiene un número par de miembros, un servidor testigo externo se emplea para proporcionar a uno de los miembros del clúster un quinto voto que resuelva el empate. Para mantener una mayoría de votantes, y por lo tanto quórum, debe haber al menos tres votantes a fin de poder comunicarse entre sí. Un máximo de dos votantes puede estar sin conexión en cualquier momento sin que se interrumpa el servicio y el acceso a los datos. Si tres votantes o más están sin conexión, el DAG pierde el quórum y el servicio y el acceso a los datos se interrumpirán hasta que se resuelva el problema.

Volver al principio

## Usar un grupo de disponibilidad de base de datos (DAG) para obtener alta disponibilidad

Consulte el ejemplo, en el que se usa un DAG con cinco miembros, para obtener información sobre cómo los DAG pueden proporcionar alta disponibilidad para las bases de datos de buzones. Este DAG se muestra en la siguiente figura.

**DAG con cinco miembros**

![Grupo de disponibilidad de base de datos (DAG)](images/Dd979799.21fcbf7b-cb10-49c0-8e32-bdf3c03f825d(EXCHG.150).gif "Grupo de disponibilidad de base de datos (DAG)")

En la figura anterior, las bases de datos verdes son copias de bases de datos de buzones activas y las azules son copias de bases de datos de buzones pasivas. En este ejemplo, las copias de bases de datos no se reflejan en cada uno de los servidores, si no que se distribuyen por varios servidores. De esta forma se garantiza que no haya dos servidores en un DAG con el mismo conjunto de copias de bases de datos. Así, se proporciona al DAG una mayor resistencia ante errores, incluidos los que tienen lugar mientras otros componentes están inactivos por razones de mantenimiento.

Observe la siguiente situación, en la que se usa el ejemplo de DAG anterior, y que muestra la resistencia ante varios errores de bases de datos y servidores.

Inicialmente, el estado de todas las bases de datos y servidores es correcto. Debe instalar algunas actualizaciones del sistema operativo en EX2, por lo tanto debe poner el servidor en modo de mantenimiento. Esto ocasiona un cambio de servidor, lo que activa la copia de DB4 en otro servidor Buzón de correo. Un cambio de servidor traslada todas las copias de bases de datos de buzones activas del servidor actual a uno o varios servidores Buzón de correo del DAG, como preparación ante el apagón programado del servidor actual. En este ejemplo, solo hay una base de datos de buzones activa en EX2 (DB4), por lo que únicamente se mueve una copia de base de datos de buzones activa.

**DAG con un servidor sin conexión por razones de mantenimiento**

![Grupo de disponibilidad de base de datos (DAG) con un servidor sin conexión](images/Dd979799.f48f0e77-80e1-4f14-8c36-112393895bdc(EXCHG.150).gif "Grupo de disponibilidad de base de datos (DAG) con un servidor sin conexión")

Mientras se realiza el mantenimiento en EX2, EX3 queda sin conexión como consecuencia de un error grave de hardware. Antes de quedar sin conexión, EX3 hospedaba la copia activa de DB2. Para recuperarse del error, el sistema activa automáticamente la copia de DB2 hospedada en EX1 en menos de 30 segundos. Se muestra en la siguiente figura.

**DAG con un servidor sin conexión por motivos de mantenimiento y un servidor con error**

![DAG con un servidor sin conexión y un servidor con error](images/Dd979799.9bbfd9e7-3881-4957-ae8d-32318cbc208b(EXCHG.150).gif "DAG con un servidor sin conexión y un servidor con error")

Después de que finalice el mantenimiento programado para EX2, coloque el servidor en línea y quite el modo de mantenimiento. En el momento en que EX2 está disponible, los demás miembros del DAG reciben una notificación al respecto, y las copias de DB1, DB4 y DB5 hospedadas en EX2 se sincronizan automáticamente con la copia activa de cada base de datos. Se muestra en la siguiente figura.

**DAG con un servidor restaurado que sincroniza sus copias de bases de datos**

![DAG con servidor restaurado que realiza la resincronización de bases de datos](images/Dd979799.58601531-e078-41d3-9287-e8e470ef7f41(EXCHG.150).gif "DAG con servidor restaurado que realiza la resincronización de bases de datos")

Una vez que se sustituye el componente de hardware dañado en EX3, éste se pone en línea. Una vez que EX3 está disponible, los demás miembros del DAG reciben una notificación al respecto, y las copias de DB2, DB3 y DB4 hospedadas en EX3 se sincronizan automáticamente con la copia activa de cada base de datos. Se muestra en la siguiente figura.

**DAG con un servidor reparado que sincroniza sus copias de bases de datos**

![DAG con miembro que realiza la resincronización de las copias de bases de datos](images/Dd979799.56259671-e840-4cf0-9ea2-3657dc36c035(EXCHG.150).gif "DAG con miembro que realiza la resincronización de las copias de bases de datos")

Volver al principio

## Usar un grupo de disponibilidad de base de datos (DAG) para obtener resistencia de sitios

Además de proporcionar alta disponibilidad en un centro de datos, un DAG se puede ampliar a otros centros de datos en una configuración que proporcione resistencia de sitio para uno o varios centros de datos. En las figuras del ejemplo anterior, el DAG está ubicado en un único centro de datos y un único sitio de Active Directory. La implementación incremental se puede utilizar para ampliar este DAG a otro centro de datos (y otro sitio de Active Directory) implementando un servidor Buzón de correo y los recursos de soporte necesarios (uno o varios servidores de Active Directory y servicios DNS). A continuación, se agrega el servidor de buzones de correo al DAG, tal como se indica en la figura siguiente.

**DAG ampliado en dos sitios de Active Directory**

![DAG ampliado en dos sitios de Active Directory](images/Dd979799.28e96e9d-d7d6-451a-b7b8-c06122c81dc9(EXCHG.150).gif "DAG ampliado en dos sitios de Active Directory")

En este ejemplo, una copia pasiva de cada base de datos activa del centro de datos de Redmond se configura en EX6 en el centro de datos de Dublín. No obstante hay muchos otros ejemplos de configuraciones de DAG que proporcionan resistencia de sitio. Por ejemplo:

  - En lugar de hospedar solamente copias de bases de datos pasivas, EX6 podría hospedar todas las copias activas, o bien una combinación de activas y pasivas.

  - Además de EX6, se podrían implementar varios miembros del DAG en el centro de datos de Dublín, lo que brindaría protección ante otros errores. Asimismo, esta configuración proporciona capacidad adicional, de modo que si se produce un error en el centro de datos de Redmond, el centro de datos de Dublín puede asumir una población mucho más grande de usuarios.

## Usar varios grupos de disponibilidad de base de datos (DAG) para obtener resistencia de sitios

En el ejemplo anterior, un solo DAG se amplía en varios centros de datos, lo que proporciona resistencia de sitio para uno o los dos centros de datos. Si se usa un solo DAG para brindar resistencia de sitio en un entorno en el que cada centro de datos en el que se amplía el DAG tiene una población de usuarios activos, hay un solo punto de error en la conexión WAN. Eso se debe a que el quórum precisa una mayoría de votantes activos y que puedan comunicarse entre sí.

En el ejemplo anterior, la mayoría de los votantes se encuentra en el centro de datos de Redmond. Si el centro de datos de Dublín hospeda bases de datos de buzones activas y tiene una población de usuarios locales, una desconexión de la WAN interrumpiría el servicio de mensajería para los usuarios de Dublín. Si la conexión de la WAN se interrumpe, los miembros del DAG del centro de datos de Redmond son los únicos que mantienen el quórum y siguen prestando el servicio de mensajería.

Para eliminar la WAN como único punto de error cuando necesite proporcionar resistencia de sitios a varios centros de datos con poblaciones de usuarios activos, debe implementar varios DAG y que cada uno de ellos disponga de mayoría de votantes en un centro de datos por separado. Si se interrumpe la conexión de la WAN, la replicación se bloquea hasta que se restablezca la conexión. Los usuarios dispondrán de servicio de mensajería porque cada DAG sigue atendiendo a su población de usuarios locales.

Volver al principio

