---
title: 'Crear un grupo de disponibilidad de base de datos: Exchange 2013 Help'
TOCTitle: Crear un grupo de disponibilidad de base de datos
ms:assetid: d6b98299-e203-488b-af73-50753fe152c8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351172(v=EXCHG.150)
ms:contentKeyID: 48268716
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear un grupo de disponibilidad de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Un grupo de disponibilidad de base de datos (DAG) es un conjunto de hasta 16 servidores de buzones Microsoft Exchange Server 2013 que ofrece recuperación automática de base de datos a partir de un error de base de datos, servidor o red. Cuando un servidor de buzones se agrega a un DAG, funciona con los demás servidores del DAG para ofrecer recuperación automática de base de datos a partir de los errores de base de datos, servidor y red.

¿Está buscando otras tareas de administración relacionadas con los DAG? Consulte [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Grupos de disponibilidad de base de datos" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Al crear un grupo de disponibilidad de base de datos (DAG) con servidores de buzones que ejecuten Windows Server 2012, debe preconfigurar el objeto de nombre en clúster (CNO) para poder agregar miembros al DAG. Si está creando un DAG sin un punto de acceso administrativo con servidores de buzones en los que se ejecuta Windows Server 2012 R2, no será necesario preconfigurar el CNO. Para conocer los pasos detallados, consulte [Preconfiguración del objeto de nombre de clúster para un grupo de disponibilidad de base de datos](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

  - Al crear un DAG, proporcione un nombre para el DAG de 15 caracteres como máximo. Además de proporcionar un nombre para el DAG, también debe asignar una o más direcciones IP (bien IPv4, bien tanto IPv4 como IPv6) al DAG, salvo que cree un DAG de Windows Server 2012 R2 sin un punto de acceso administrativo y no asigne ninguna dirección IP al DAG. De lo contrario, las direcciones IP que asigne deben estar en cada subred destinada a la red MAPI y se deben poder usar. Si especifica una o más direcciones IPv4 y el sistema está configurado para usar IPv6, la tarea también intenta asignar automáticamente una o más direcciones IPv6.

  - Cuando crea un DAG, tiene la opción de especificar un servidor testigo y un directorio testigo. Si especifica un servidor testigo, se recomienda usar un servidor de acceso de clientes que no tenga el rol de servidor Buzón de correo instalado. Esto le permite a un administrador de Exchange tener conocimiento de la disponibilidad del testigo y garantiza que todos los permisos de seguridad necesarios para usar el servidor testigo están en funcionamiento.
    
    Están disponibles las siguientes combinaciones de opciones y comportamientos:
    
      - Puede solamente especificar un nombre para el DAG y dejar en blanco los campos **Servidor testigo** y **Directorio testigo**. En este caso, la tarea buscará un servidor de acceso de clientes que no tenga instalado el rol de servidor Buzón de correo. De forma automática, creará el directorio testigo predeterminado para compartirlo con ese servidor de acceso de cliente y configurará el DAG para usar ese servidor como servidor testigo.
    
      - Puede especificar un nombre para el DAG, el servidor testigo que desea usar y el directorio que va a crear y compartir en el servidor testigo.
    
      - Puede especificar un nombre para el DAG y el servidor testigo que desea usar, y dejar en blanco el campo **Directorio testigo**. En este caso, la tarea creará el directorio testigo predeterminado en el servidor testigo especificado.
    
      - Puede especificar un nombre para el DAG, dejar en blanco el campo **Servidor testigo** y especificar el directorio que va a crear y compartir en el servidor testigo. En este caso, el asistente buscará un servidor de acceso de clientes que no tenga instalado el rol de servidor Buzón de correo, creará automáticamente el directorio testigo especificado en dicho servidor, lo compartirá y configurará el DAG para usar ese servidor de acceso de clientes como servidor testigo.
    

    > [!IMPORTANT]
    > Si el servidor testigo que especifique no es un servidor de&nbsp;Exchange&nbsp;2013 o Exchange 2010, deberá agregar el grupo de seguridad universal de subsistemas de confianza de Exchange al grupo de administradores locales del servidor testigo. Estos permisos de seguridad son necesarios para asegurar que Exchange&nbsp;pueda crear un directorio y compartirlo en el servidor testigo, según sea preciso. Si no se configuran los permisos correspondiente, aparece el mensaje de error siguiente:<BR><CODE>Error: An error occurred during discovery of the database availability group topology. Error: An error occurred while attempting a cluster operation. Error: Cluster API "AddClusterNode() (MaxPercentage=12) failed with 0x80070005. Error: Access is denied."</CODE>



  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para crear un grupo de disponibilidad de base de datos

1.  En la EAC, vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**.

2.  Haga clic en ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para crear un DAG.

3.  
    
    En la página **Nuevo grupo de disponibilidad de base de datos**, proporcione la información siguiente para el DAG:
    
      - **Nombre de grupo de disponibilidad de base de datos**   Use este campo para asignar un nombre exclusivo válido al DAG. Debe tener 15 caracteres como máximo. El nombre equivale a un nombre de equipo y el correspondiente CNO se creará con ese nombre en Active Directory. Este nombre será tanto el nombre del DAG como el nombre del clúster subyacente.
    
      - **Servidor testigo**   Use este campo para especificar un servidor testigo para el DAG. Si deja en blanco este campo, el sistema intentará seleccionar automáticamente un servidor de acceso de clientes en el sitio de Active Directory local que no esté instalado en un equipo con el servidor de buzones de correo que se usará como servidor testigo.
        

        > [!NOTE]
        > Si especifica un servidor testigo, debe usar un nombre de host o un nombre de dominio completo (FQDN). No se puede usar una dirección IP ni un nombre comodín. Además, el servidor testigo no puede ser miembro del DAG.

    
      - **Directorio testigo**   Use este campo para escribir la ruta a un directorio en el servidor testigo que se usará para almacenar datos testigos. Si el directorio no existe, el sistema lo crea en el servidor testigo. Si deja en blanco este campo, el directorio predeterminado (%SystemDrive%\\DAGFileShareWitnesses\\\<DAG FQDN\>) se creará en el servidor testigo.
    
      - **Direcciones IP de grupo de disponibilidad**   Use este campo para asignar una o más direcciones IPv4 estáticas al DAG. Escriba una dirección IPv4 y haga clic en ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregarla. Deje este campo en blanco si desea que el DAG use el Protocolo de configuración dinámica de host (DHCP) para obtener las direcciones IPv4 necesarias. De forma opcional, escriba 255.255.255.255 para crear un DAG sin una dirección IP o punto de acceso administrativo de clúster, algo que es válido únicamente en el caso de los DAG que contengan servidores de buzones con Windows Server 2012 R2.

4.  Haga clic en **Guardar** para crear el DAG.

## Uso del Shell para crear un grupo de disponibilidad de la base de datos

En este ejemplo se crea el DAG DAG1, que se configura para usar un servidor testigo FILESRV1 y el directorio local C:\\DAG1. DAG1 también está configurado para usar DHCP para las direcciones IP del DAG.

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer FILESRV1 -WitnessDirectory C:\DAG1

En este ejemplo se crea el DAG DAG2. El sistema selecciona automáticamente un servidor de acceso de cliente en el sitio de Active Directory local que no contiene el rol de servidor Buzón de correo como servidor testigo del DAG. DAG2 tiene asignada una única dirección IP estática porque, en este ejemplo, todos los miembros del DAG tienen la red MAPI en la misma subred.

    New-DatabaseAvailabilityGroup -Name DAG2 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

En este ejemplo se crea el DAG DAG3. DAG3 está configurado para usar el servidor testigo MBX2 y el directorio local de C:\\DAG3. DAG3 tiene asignadas varias direcciones IP estáticas, ya que los miembros del DAG se encuentran en subredes diferentes en la red MAPI.

    New-DatabaseAvailabilityGroup -Name DAG3 -WitnessServer MBX2 -WitnessDirectory C:\DAG3 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,192.168.0.8

En este ejemplo se crea el DAG DAG4 y se configura para utilizar DHCP. Además, el sistema seleccionará automáticamente el servidor testigo y se creará el directorio testigo predeterminado.

    New-DatabaseAvailabilityGroup -Name DAG4

En este ejemplo se crea el DAG DAG5, que no tendrá un punto de acceso administrativo (válido solo para DAG con Windows Server 2012 R2). Además, se usará MBX4 como el servidor testigo del DAG y se creará el directorio testigo predeterminado.

    New-DatabaseAvailabilityGroup -Name DAG5 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress]::None) -WitnessServer MBX4

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el DAG se creó correctamente, siga uno de estos pasos:

  - En el EAC, vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**. Se muestra el DAG recién creado.

  - En el Shell, ejecute el siguiente comando para comprobar que el DAG se creó y para mostrar la información de propiedades del DAG.
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## Más información

[Grupos de disponibilidad de base de datos (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[Configurar las propiedades del grupo de disponibilidad de base de datos](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\))

[New-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd351107\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd335225\(v=exchg.150\))

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/es-es/library/dd298049\(v=exchg.150\))

