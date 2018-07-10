---
title: 'Asignar permisos de exhibición de documentos electrónicos en Exchange: Exchange 2013 Help'
TOCTitle: Asignar permisos de exhibición de documentos electrónicos en Exchange
ms:assetid: 729e09d8-614b-431f-ae04-ae41fb4c628e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298059(v=EXCHG.150)
ms:contentKeyID: 48268269
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Asignar permisos de exhibición de documentos electrónicos en Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-10-02_

Si desea que los usuarios puedan usar la exhibición de documentos electrónicos local de Microsoft Exchange Server 2013, primero debe autorizarlos agregándolos al grupo de roles de administración del servicio de detección. Los miembros del grupo de roles de Discovery Management tienen permisos de acceso completo a buzones de detección creados por el programa de instalación de Exchange.


> [!WARNING]
> Los miembros del grupo de funciones de administración de la detección pueden acceder al contenido de mensajes confidenciales. Concretamente, estos miembros pueden usar <A href="in-place-ediscovery-exchange-2013-help.md">Exhibición de documentos electrónicos en contexto</A> para hacer búsquedas en todos los buzones de la organización de Exchange, previsualizar mensajes (y otros elementos de buzones), copiarlos en un buzón de detección y exportar los mensajes copiados a un archivo .pst. En la mayoría de las organizaciones, este permiso se otorga al personal de Recursos Humanos, cumplimiento y asesoría legal.<BR>



Para obtener más información acerca del grupo de roles de administración del servicio de detección, consulte [Administración de la detección](discovery-management-exchange-2013-help.md). Para obtener más información acerca del Control de acceso basado en roles (RBAC), consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Crear una búsqueda de exhibición de documentos electrónicos local](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [Crear o quitar una conservación local](create-or-remove-an-in-place-hold-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Grupos de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - De forma predeterminada, el grupo de roles de Discovery Management no contiene ningún miembro. Los administradores con la función Administración de la organización tampoco pueden crear ni administrar búsquedas de detección sin que se agreguen al grupo de funciones de Discovery Management.

  - En Exchange 2013, los miembros del grupo de roles Administración de la organización puede crear una [Conservación local y retención por juicio](in-place-hold-and-litigation-hold-exchange-2013-help.md) para suspender todo el contenido de los buzones. Sin embargo, para crear una retención local basada en consulta, el usuario debe ser miembro del grupo de roles de administración de detección o tener un rol de búsqueda de buzones asignado.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Uso del EAC para agregar un usuario al grupo de funciones de administración de la detección

1.  Vaya a **Permisos** \> **Roles de administrador**.

2.  En la vista de lista, seleccione **Administración de detección** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar")

3.  En **Grupo de roles**, bajo **Miembros**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En **Seleccionar miembros**, seleccione uno o más usuarios, haga clic en **Agregar** y, a continuación, haga clic en **Aceptar**.

5.  En **Grupo de roles**, haga clic en **Guardar**.

## Uso del Shell para agregar un usuario al grupo de funciones de administración de la detección

En este ejemplo se agrega el usuario BSuneja al grupo de roles de administración de detección.

    Add-RoleGroupMember -Identity "Discovery Management" -Member Bsuneja

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Add-RoleGroupMember](https://technet.microsoft.com/es-es/library/dd638207\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si agregó el usuario al grupo de funciones de administración de la detección, realice lo siguiente:

1.  En el EAC, vaya a **Permisos** \> **Roles de administrador**.

2.  En la vista de lista, seleccione **Administración de detección**.

3.  En el panel de detalles, compruebe si el usuario aparece en **Miembros**.

También puede ejecutar este comando para enumerar los miembros del grupo de roles de administración de detección.

    Get-RoleGroupMember -Identity "Discovery Management"


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


