---
title: 'Crear una red de grupos de disponibilidad de base de datos: Exchange 2013 Help'
TOCTitle: Creación de una red de grupos de disponibilidad de base de datos
ms:assetid: 6caec7be-788a-4058-87a7-f31c575b870c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298051(v=EXCHG.150)
ms:contentKeyID: 48268251
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creación de una red de grupos de disponibilidad de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-02_

Si es necesario, puede crear redes adicionales para su uso en un grupo de disponibilidad de base de datos (DAG). Puede usar el Centro de Administración de Exchange o el Shell para crear una red de DAG.

¿Está buscando otras tareas de administración relacionadas con los DAG? Consulte [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de disponibilidad de base de datos" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Las redes de DAG solo se pueden crear después de deshabilitar la configuración de red automática para un DAG. Para consultar los pasos detallados sobre cómo deshabilitar la configuración de red automática de un DAG, configure [Configurar las propiedades del grupo de disponibilidad de base de datos](configure-database-availability-group-properties-exchange-2013-help.md).

  - Al crear una red de DAG, debe asignar subconjuntos únicos que no esté usando ninguna red de DAG. Si usa subconjuntos asignados a una red de DAG existente, se eliminarán de esa red de DAG y se agregarán a la red de DAG recién creada.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para crear una red de grupos de disponibilidad de base de datos

1.  En el Centro de Administración de Exchange, vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**.

2.  Seleccione el DAG que desea configurar y, a continuación, haga clic en ![Agregar red de DAG](images/Dd298051.befcdc4e-7f7a-451d-a0a8-608c79f5d186(EXCHG.150).gif "Agregar red de DAG").

3.  En la página **nueva red de grupo de disponibilidad de base de datos**, especifique la siguiente información:
    
      - **Nombre de la red del grupo de disponibilidad de base de datos**   Use este campo para escribir un nombre que sea único en el DAG.
    
      - **Descripción**   Use este campo para proporcionar una descripción en texto de la red de DAG.
    
      - **Subredes**   Este campo permite asociar una o más subredes a la red de DAG. Haga clic en ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una subred, en ![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para editarla y en menos (-) para quitar la subred.

4.  Haga clic en **Guardar** para crear la red de DAG.

## Uso de Shell para crear una red del grupo de disponibilidad de base de datos

En este ejemplo, se crea la red ReplicationDagNetwork02 con una subred de 10.0.0.0 y una máscara de bits de 8 en DAG DAG1. La replicación está habilitada para la red y también se agrega una descripción opcional de la red.

    New-DatabaseAvailabilityGroupNetwork -DatabaseAvailabilityGroup DAG1 -Name ReplicationDagNetwork02 -Description "Replication network 2" -Subnets 10.0.0.0/8 -ReplicationEnabled:$True

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó una red de DAG correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**. Seleccione el DAG adecuado y la red de DAG recién creada aparecerá en el panel de detalles.

  - En el Shell, ejecute el siguiente comando para comprobar que la red de DAG se haya creado correctamente y para mostrar la información de configuración de la red de DAG.
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## Más información

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd298131\(v=exchg.150\))

