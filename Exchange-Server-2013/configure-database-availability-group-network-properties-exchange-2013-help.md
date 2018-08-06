---
title: 'Configurar propiedades red grupos disponibilidad base datos Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configuración de propiedades de red de grupos de disponibilidad de base de datos
ms:assetid: 41197639-988f-476c-9788-51d5191a7dce
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd297927(v=EXCHG.150)
ms:contentKeyID: 48268042
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuración de propiedades de red de grupos de disponibilidad de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-31_

Cada red de grupo de disponibilidad de base de datos (DAG) tiene diversas propiedades que puede configurar, la cual incluye el nombre de la red de DAG, el campo de descripción para la red de DAG, una lista de subredes que son usadas por la red de DAG y si la red de DAG está habilitada para replicación.

¿Está buscando otras tareas de administración relacionadas con los DAG? Consulte [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de disponibilidad de base de datos" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Puede configurar una red de DAG sólo cuando la configuración de red automática se haya deshabilitado para un DAG. Para consultar los pasos detallados sobre cómo deshabilitar la configuración de red automática de un DAG, configure [Configurar las propiedades del grupo de disponibilidad de base de datos](configure-database-availability-group-properties-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar las propiedades de un grupo de disponibilidad de base de datos

1.  En el Centro de Administración de Exchange, vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**.

2.  Seleccione el DAG que desee configurar y, en el panel Detalles, en la red de DAG que desee configurar, seleccione:
    
      - **Deshabilitar la replicación** o **Habilitar la replicación** Establece la configuración de replicación de la red de DAG.
    
      - **Eliminar**   Elimina una red de un DAG. Antes de poder quitar una red de DAG, primero debe quitar todos los subconjuntos asociados desde la red de DAG.
    
      - **Ver detalles**   Configura las propiedades de red de DAG, como el nombre, la descripción y las subredes asociadas para la red de DAG. También puede ver las interfaces de red asociadas con dichas subredes y habilitar o deshabilitar la replicación para la red de DAG.

## Usar el Shell para configurar las propiedades de la red del grupo de disponibilidad de base de datos

En este ejemplo, se agrega una subred de 10.0.0.0 y una máscara de subred de 255.0.0.0 a una red MapiDagNetwork de DAG en DAG DAG1.

    Set-DatabaseAvailabilityGroupNetwork -Subnets 10.0.0.0/8 -Identity DAG1\MapiDagNetwork

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya configurado correctamente las redes de DAG, siga estos pasos:

  - En el Shell, ejecute el siguiente comando para mostrar los ajustes de la configuración de una red de DAG y comprobar que la red de DAG se haya configurado correctamente.
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## Más información

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd298131\(v=exchg.150\))

