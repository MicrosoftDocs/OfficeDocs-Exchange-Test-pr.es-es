---
title: 'Administración de la pertenencia a grupos de disponibilidad de base de datos: Exchange 2013 Help'
TOCTitle: Administración de la pertenencia a grupos de disponibilidad de base de datos
ms:assetid: fb2ea15e-96d5-4045-b75b-b0aa5fc60479
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351278(v=EXCHG.150)
ms:contentKeyID: 48268902
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administración de la pertenencia a grupos de disponibilidad de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-08-13_

Si se agrega un servidor a un grupo de disponibilidad de base de datos (DAG), funciona con los otros servidores del DAG para proporcionar recuperación automática de base de datos a partir de errores de base de datos, servidor y red. Si quita un servidor de un DAG, deja de quedar automáticamente protegido contra errores.

¿Está buscando otras tareas de administración relacionadas con los DAG? Consulte [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos por servidor

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Grupos de disponibilidad de base de datos" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Los DAG usan tecnología de agrupación en clústeres de conmutación por error (WFC) de Windows. Cada servidor de buzones de correo que pertenezca a un DAG también es un nodo en el clúster subyacente usado por el DAG. Por este motivo, un servidor de buzones solo puede ser miembro de un único DAG en un momento específico. Como los DAG usan tecnología WFC, todos los servidores agregados a un DAG deben ejecutar el mismo sistema operativo: Windows Server 2008 R2 Enterprise o Datacenter Edition, o la versión Standard o Datacenter Edition de Windows Server 2012 o Windows Server 2012 R2.

  - Si va a agregar servidores de buzones que ejecuten Windows Server 2012, debe preconfigurar el objeto de nombre en clúster (CNO) para el DAG. Si va a agregar servidores de buzones de correo que ejecutan Windows Server 2012 R2 y el DAG no tiene asignado un punto de acceso administrativo, no es necesario que preconfigure un CNO, ya que los DAG sin puntos de acceso administrativo no tienen CNO. Para conocer los pasos detallados, consulte [Preconfiguración del objeto de nombre de clúster para un grupo de disponibilidad de base de datos](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

  - Antes de agregar miembros a un DAG, debe crear un DAG. Para conocer los pasos detallados, consulte [Crear un grupo de disponibilidad de base de datos](create-a-database-availability-group-exchange-2013-help.md).

  - Es preciso quitar todas las copias de bases de datos replicadas del servidor antes de poderlo quitar de un DAG.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué quiere hacer?

## Usar el EAC para administrar la pertenencia a grupos de disponibilidad de base de datos

1.  En el EAC, vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**.

2.  Seleccione el DAG que quiere configurar y después haga clic en ![Administrar miembros de DAG](images/Dd351278.d567ae56-d6cd-4edb-ab67-ad8f7c58f337(EXCHG.150).gif "Administrar miembros de DAG").
    
      - Para agregar uno o varios servidores de buzones de correo al DAG, haga clic en ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"), seleccione los servidores de la lista, elija **Agregar** y después haga clic en **Aceptar**.
    
      - Para quitar uno o varios servidores de buzones del DAG, seleccione los servidores y haga clic en el icono de menos (-).

3.  Haga clic en **Guardar** para guardar los cambios.

4.  Cuando complete la tarea correctamente, haga clic en **Cerrar**.

## Uso del Shell para administrar la pertenencia a grupos de disponibilidad de la base de datos

En este ejemplo se agrega el servidor de buzones de correo MBX1 al DAG DAG1.

```powershell
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```

En este ejemplo se quita el servidor de buzones de correo MBX1 del DAG DAG1. Antes de ejecutar este comando, compruebe que en el servidor Buzón de correo no haya bases de datos replicadas.

```powershell
Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```

En este ejemplo se quita la configuración del servidor de buzones de correo MBX4 del DAG DAG2. Se espera que MBX4 pueda permanecer sin conexión durante un período prolongado. Por este motivo, su configuración se quita del DAG mientras está sin conexión para establecer el quórum con los miembros restantes del DAG que están en línea.

```powershell
Remove-DatabaseAvailabilityGroupServer -Identity DAG2 -MailboxServer MBX4 -ConfigurationOnly
```

## ¿Cómo saber si el proceso se completó correctamente?

Para comprobar que la pertenencia del DAG se administró correctamente, haga una de estas acciones:

  - En el EAC, vaya a **Servidores** \> **Grupos de disponibilidad de base de datos**. La pertenencia del DAG actual se muestra en la columna **Servidores miembro**.

  - En el Shell, ejecute este comando para mostrar la información de pertenencia del DAG.
    
    ```powershell
    Get-DatabaseAvailabilityGroup <DAGName> | Format-List Servers
    ```

## Más información

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/es-es/library/dd298049\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/es-es/library/dd297956\(v=exchg.150\))

