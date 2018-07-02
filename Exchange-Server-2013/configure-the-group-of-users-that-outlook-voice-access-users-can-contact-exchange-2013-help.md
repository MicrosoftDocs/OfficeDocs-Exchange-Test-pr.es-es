---
title: 'Configurar el grupo de usuarios que pueden ponerse en contacto con los usuarios de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurar el grupo de usuarios que pueden ponerse en contacto con los usuarios de Outlook Voice Access
ms:assetid: a8dc0f9e-dc86-4128-af63-d4e550aed5bb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423551(v=EXCHG.150)
ms:contentKeyID: 49895826
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el grupo de usuarios que pueden ponerse en contacto con los usuarios de Outlook Voice Access

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-09_

Puede especificar qué usuarios pueden recibir las llamadas transferidas o los mensajes de correo de voz de los usuarios de Outlook Voice Access. La opción **En este plan de marcado únicamente** está seleccionada de manera predeterminada. Puede cambiar esta configuración para permitir que los usuarios de Outlook Voice Access transfieran llamadas o envíen mensajes de voz a los usuarios ubicados en toda la organización, a un operador automático de mensajería unificada existente o a un número de extensión específico.

Para obtener más información acerca de otras tareas relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Utilice la EAC para configurar el grupo de usuarios con los que pueden ponerse en contacto los usuarios de Outlook Voice Access

1.  En la EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

4.  En la **Búsqueda de & transferencia**, en **Permitir a los autores de llamadas buscar usuarios por nombre o alias**, seleccione una de las siguientes opciones:
    
      - **En este plan de marcado únicamente**   Use esta opción para permitir que los usuarios de Outlook Voice Access que llaman a un número de Outlook Voice Access localicen y se pongan en contacto con usuarios que están dentro del mismo plan de marcado.
    
      - **En toda la organización**   Use esta opción para permitir que los usuarios de Outlook Voice Access que llaman a un número de Outlook Voice Access localicen y se pongan en contacto con cualquier persona en toda la organización. Se incluyen todos los usuarios habilitados para buzón.
    
      - **Solo en este operador automático**   Use esta opción para permitir que los usuarios de Outlook Voice Access que llaman a un número de Outlook Voice Access se conecten con un operador automático específico. Debe crear el operador automático antes de especificarlo aquí. Esto permite que los usuarios de Outlook Voice Access se puedan transferir a otro operador automático. El operador automático que seleccione aquí puede ser un operador automático habilitado con voz o no habilitado con voz.
    
      - **Solo para esta extensión**   Use esta opción para permitir a los usuarios de Outlook Voice Access que se conecten con un número de extensión que usted haya indicado. Puede usar sólo dígitos numéricos para la extensión. La cantidad de dígitos que defina en este campo debe coincidir con la cantidad de dígitos de los números de extensión configurados en el plan de marcado de MU.

5.  Haga clic en **Guardar**.

## Utilice el Shell para configurar el grupo de usuarios con los que pueden ponerse en contacto los usuarios de Outlook Voice Access

En este ejemplo se establece un grupo de usuarios con los que los usuarios de Outlook Voice Access se pueden poner en contacto por un plan de marcado de mensajería unificada denominado `MyUMDialPlan` para toda la organización.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope 'GlobalAddressList' -UMAutoAttendant $null -AllowDialPlanSubscribers $false -AllowExtensions $false

En este ejemplo se establece un grupo de usuarios con los que los usuarios de Outlook Voice Access se pueden poner en contacto por un plan de marcado de mensajería unificada denominado `MyUMDialPlan` para toda la `DialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope DialPlan -AllowDialPlanSubscribers $false -AllowExtensions $false

