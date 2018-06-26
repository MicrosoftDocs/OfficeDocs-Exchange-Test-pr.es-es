---
title: 'Administrar miembros de grupos de roles: Exchange 2013 Help'
TOCTitle: Administrar miembros de grupos de roles
ms:assetid: c064729d-7cda-47fc-b105-acf4b300d430
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657492(v=EXCHG.150)
ms:contentKeyID: 49895886
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar miembros de grupos de roles

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2012-10-08_

Este tema muestra cómo agregar, quitar y ver los miembros de un grupo de funciones de administración en Microsoft Exchange Server 2013. Para obtener más información acerca de los grupos de roles en Exchange 2013, consulte [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md).

Para otras tareas de administración relacionadas con los grupos de funciones, consulte [Permisos](permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Grupos de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Agregar miembros a un grupo de funciones

Para dar a un usuario los permisos que un grupo de funciones le otorgan, es necesario agregar el usuario o un grupo de seguridad universal (USG) u otro grupo de funciones al cual el usuario pertenezca como miembro del grupo de funciones.

## Use el EAC para agregar miembros a un grupo de roles

1.  En el Centro de Administración de Exchange (EAC), navegue a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de funciones al cual desea agregar miembros y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la sección **Miembros**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  Seleccione los usuarios, los USG u otros grupos de funciones que desee agregar al grupo de funciones y, luego, haga clic en **Agregar** y en **Aceptar**.

5.  Haga clic en **Guardar** para guardar los cambios realizados en el grupo.

## Use el Shell para agregar miembros a un grupo de funciones

Ejemplos

Ejemplos

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se agregó correctamente un miembro o varios al grupo de funciones, realice lo siguiente:

1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de funciones al que agregó miembros.

3.  En el panel de detalles del grupo de funciones, compruebe que se hayan incluido los miembros que agregó.

## Quitar miembros de un grupo de funciones

Para quitar los permisos que un grupo de funciones concede a un usuario, debe quitar el usuario o el grupo de seguridad universal (USG) del que el usuario es miembro.

## Uso del EAC para quitar miembros de un grupo de funciones

1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de funciones del que desee quitar miembros y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la sección **Miembros**, seleccione los miembros que desea eliminar y, a continuación, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") y en **Guardar**.

## Uso del Shell para quitar miembros de un grupo de funciones

Ejemplos

Ejemplos

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se quitó correctamente un miembro o varios del grupo de funciones, realice lo siguiente:

1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de funciones del que eliminó miembros.

3.  En el panel de detalles del grupo de funciones, compruebe que los miembros que eliminó no estén en la lista.

## Ver los miembros de un grupo de funciones

Los permisos otorgados a miembros de un grupo de funciones los determinan las funciones de administración asignadas al grupo de funciones. Puede ver los miembros de un grupo de roles para ver los usuarios, los grupos de seguridad universal u otros grupos de roles a los que concede permisos el grupo de roles que especifica.

## Uso del EAC para ver los miembros de un grupo de funciones

1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de funciones del que desea ver los miembros.

3.  En el panel de detalles del grupo de funciones, vea los miembros en el panel de detalles del grupo de funciones.

## Uso del Shell para ver los miembros de un grupo de roles

Ejemplos

