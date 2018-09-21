---
title: 'Cambiar la directiva de asignación en un buzón: Exchange 2013 Help'
TOCTitle: Cambiar la directiva de asignación en un buzón
ms:assetid: 011690a5-233a-4c03-8842-92276f899a89
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638076(v=EXCHG.150)
ms:contentKeyID: 49895431
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cambiar la directiva de asignación en un buzón

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-08_

Puede cambiar la directiva de asignación de funciones de administración asignada a un buzón. Cuando cambia una directiva de asignación del buzón, el cambio surte efecto apenas el usuario actualiza la conexión, por ejemplo, la próxima vez que inicie sesión en el buzón o que abra la página de opciones del buzón. Para obtener más información acerca de las directivas de asignación en Microsoft Exchange Server 2013, consulte [Descripción de las directivas de asignación de roles de administración](understanding-management-role-assignment-policies-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con permisos? Consulte [Permisos](permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Grupos de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use el EAC para cambiar la directiva de asignación en un buzón

1.  En el Centro de administración de Exchange (EAC), vaya a **Destinatarios** \> **Buzones**.

2.  Seleccione el usuario o el buzón de recursos al cual desee cambiar la directiva de asignación y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  Seleccione **Características de buzón**.

4.  En la lista **Directiva de asignación de roles**, seleccione la directiva de asignación que desee asignar al buzón y, a continuación, haga clic en **Guardar**.

## Usar el Shell para cambiar la directiva de asignación en un buzón

Para cambiar la directiva de asignación asignada a un buzón, utilice la sintaxis siguiente.

```powershell
Set-Mailbox <mailbox alias or name> -RoleAssignmentPolicy <assignment policy>
```

En este ejemplo, se establece la directiva de asignación a usuarios de mensajería unificada en el buzón Brian.

```powershell
Set-Mailbox Brian -RoleAssignmentPolicy "Unified Messaging Users"
```

## Usar el Shell para cambiar la directiva de asignación en un grupo de buzones a los que se asignó una directiva de asignación específica


> [!NOTE]
> No puede usar el EAC para cambiar de una vez la directiva de asignación en un grupo de buzones.



Este procedimiento usa la canalización, el cmdlet **Where** y el parámetro *WhatIf*. Para obtener más información acerca de estos conceptos, consulte los siguientes temas:

  - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))

  - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

  - [Modificadores WhatIf, Confirm y ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

Si desea cambiar la directiva de asignación de un grupo de buzones a los que se asignó una directiva específica, utilice la sintaxis siguiente.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<assignment policy to find>" } | Set-Mailbox -RoleAssignmentPolicy <assignment policy to set>

En este ejemplo, se encuentran todos los buzones a los que se asignó la directiva de asignación Usuarios de Redmond: sin correo de voz, y se cambia la directiva de asignación a Usuarios de Redmond: correo de voz habilitado.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled"

En este ejemplo, se incluye el parámetro *WhatIf* para que pueda ver todos los buzones que se cambiarían sin confirmar ningún cambio.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled" -WhatIf

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) o [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

