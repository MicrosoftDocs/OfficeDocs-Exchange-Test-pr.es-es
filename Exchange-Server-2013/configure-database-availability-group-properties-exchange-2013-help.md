---
title: 'Configurar las propiedades del grupo de disponibilidad de base de datos: Exchange 2013 Help'
TOCTitle: Configurar las propiedades del grupo de disponibilidad de base de datos
ms:assetid: 50daeac5-a16f-4362-a325-19e0fe25d59d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd297985(v=EXCHG.150)
ms:contentKeyID: 48268116
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar las propiedades del grupo de disponibilidad de base de datos

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-06-24_

Puede usar el Centro de administración de Exchange o el Shell para configurar las propiedades de un grupo de disponibilidad de base de datos (DAG), incluidas la configuración de la dirección IP del DAG y el servidor testigo y el directorio testigo que usa el DAG. El Shell permite configurar las propiedades del DAG que no están disponibles en el EAC, como el servidor testigo de destino y la información de directorios testigo alternativos, el puerto TCP usado para la replicación y el modo de coordinación de activación de centros de datos (DAC).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de disponibilidad de base de datos" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Los valores de las propiedades del DAG se almacenan en Active Directory y la base de datos del clúster. Sin embargo, algunas propiedades se almacenan solo en la base de datos del clúster. Como resultado, el clúster subyacente para el DAG debe estar ejecutándose y tener quórum para establecer las propiedades para:
    
      - ReplicationPort
    
      - NetworkCompression
    
      - NetworkEncryption
    
      - DiscoverNetworks

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar la EAC para configurar las propiedades del grupo de disponibilidad de base de datos

1.  En el Centro de Administración de Exchange, vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**.

2.  Seleccione el DAG que desea configurar y haga clic en ![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  
    
    Use la página **General** para ver el estado operativo y la pertenencia del DAG y para configurar el servidor testigo del DAG, el directorio testigo y la configuración de red automática:
    
      - **Servidor testigo**   El nombre del host o el nombre de dominio completo (FQDN) del servidor testigo para el DAG. Aunque esta propiedad es necesaria para todos los DAG, el servidor testigo se usa cuando hay un número par de miembros de DAG y el modelo de quórum que usa el clúster sea Mayoría de recurso compartido de archivos y nodo.
    
      - **Directorio testigo**   La ruta de acceso completa del directorio usado para almacenar el archivo witness.log en el servidor testigo. Si bien esta es una propiedad requerida para todos los DAG, el directorio testigo se usa cuando el servidor testigo del DAG está en uso.
    
      - **Servidores de funcionamiento**   Un campo de solo lectura que muestra una lista de miembros DAG y su estado de funcionamiento actual.
    
      - **Configurar la red de grupos de base de datos manualmente**   Una casilla que se selecciona si se desea configurar todas las redes de DAG manualmente. Cuando se deja la casilla sin seleccionar, el sistema configura las redes de DAG automáticamente según la configuración de la interfaz de la red. Si la casilla está sin seleccionar, los cmdlets **Set-DatabaseAvailabilityGroupNetwork** y **New-DatabaseAvailabilityGroupNetwork** se deshabilitan para el uso administrativo en el DAG.

4.  
    
    Use la página **Direcciones IP** para ver y modificar las direcciones IP asignadas al DAG:
    
      - Seleccione una dirección IP existente y haga clic en ![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para modificarla.
    
      - Seleccione una dirección IP existente y haga clic en el ícono menos (eliminar) para quitarla.
    
      - Escriba una dirección IP y haga clic en el icono ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregarla al DAG.

5.  
    
    Haga clic en **Guardar** para guardar los cambios realizados.

## Usar el Shell para configurar las propiedades del grupo de disponibilidad de base de datos

En este ejemplo, se establece el directorio testigo como C:\\DAG1DIR para un DAG denominado DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessDirectory C:\DAG1DIR

En este ejemplo, se realiza la configuración previa de un servidor testigo alternativo de CAS3 y de un directorio testigo alternativo de C:\\DAGFileShareWitnesses\\DAG1.contoso.com para el DAG DAG1.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGFileShareWitnesses\DAG1.contoso.com -AlternateWitnessServer CAS3

En este ejemplo, se configura el DAG DAG1 para usar el protocolo de configuración dinámica de host (DHCP) para obtener una dirección IP.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 0.0.0.0

En este ejemplo, se configura el DAG DAG1 para que use la dirección IP estática 10.0.0.8.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

En este ejemplo, el DAG denominado DAG1 con varias subredes se configura con varias direcciones IP estáticas.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,10.0.1.8

En este ejemplo, se configura el DAG DAG1 para el modo DAC.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

En este ejemplo, se configura el puerto de replicación para un DAG DAG1 para que sea 63132.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -ReplicationPort 63132


> [!NOTE]
> Después de cambiar el puerto de replicación predeterminado para un DAG, debe modificar manualmente las excepciones del Firewall de Windows en cada miembro del DAG para permitir la comunicación con el puerto especificado.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si el DAG se configuró correctamente, siga estos pasos:

  - En el Shell, ejecute el siguiente comando para mostrar los valores de configuración del DAG y compruebe que el DAG se configuró correctamente.
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## Más información

[Crear un grupo de disponibilidad de base de datos](create-a-database-availability-group-exchange-2013-help.md)

[Eliminación de un grupo de disponibilidad de base de datos](remove-a-database-availability-group-exchange-2013-help.md)

[Creación de una red de grupos de disponibilidad de base de datos](create-a-database-availability-group-network-exchange-2013-help.md)

[Administración de la pertenencia a grupos de disponibilidad de base de datos](manage-database-availability-group-membership-exchange-2013-help.md)

[Get-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd351226\(v=exchg.150\))

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\))

