---
title: 'Eliminación de un grupo de disponibilidad de base de datos: Exchange 2013 Help'
TOCTitle: Eliminación de un grupo de disponibilidad de base de datos
ms:assetid: 071296e9-31b0-40f4-9a02-177d97486ebd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335069(v=EXCHG.150)
ms:contentKeyID: 48267766
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminación de un grupo de disponibilidad de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-16_

Quitar un grupo de disponibilidad de la base de datos (DAG) es una tarea rápida y fácil. Puede usar el Centro de Administración de Exchange o el Shell para eliminar un DAG.

¿Está buscando otras tareas de administración relacionadas con los DAG? Consulte [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de disponibilidad de base de datos" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Antes de poder quitar un DAG, el DAG debe estar vacío. Si el DAG que desea quitar contiene servidores Buzón de correos, es preciso quitar dichos servidores del DAG. Para obtener información detallada sobre cómo quitar un servidor Buzón de correos de un DAG, consulte [Administración de la pertenencia a grupos de disponibilidad de base de datos](manage-database-availability-group-membership-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de EAC para quitar un grupo de disponibilidad de la base de datos

1.  Vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**.

2.  Seleccione el DAG que desee quitar y haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

3.  Haga clic en **Sí** para confirmar la advertencia y quitar el DAG.

## Uso del Shell para quitar un grupo de disponibilidad de la base de datos

En este ejemplo, se elimina el DAG DAG1.

```powershell
Remove-DatabaseAvailabilityGroup -Identity DAG1
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el DAG se haya eliminado correctamente, siga uno de estos pasos:

  - En el Centro de Administración de Exchange, vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**, y vea si DAG todavía se muestra.

  - En el Shell, ejecute el comando siguiente para ver si el DAG todavía existe:
    
    ```powershell
Get-DatabaseAvailabilityGroup <DAGName>
```
    
    Si el DAG se eliminó correctamente, el comando anterior generará un mensaje de error que indica que no se encontró el objeto.

