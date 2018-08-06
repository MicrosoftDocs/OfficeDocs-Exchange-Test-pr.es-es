---
title: 'Asignar directiva libreta direcciones a usuarios de correo: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Asignar una directiva de libreta de direcciones a usuarios de correo
ms:assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh529942(v=EXCHG.150)
ms:contentKeyID: 49895880
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Asignar una directiva de libreta de direcciones a usuarios de correo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-10-11_

Después de crear una directiva de libreta de direcciones (ABP), debe asignarla a los usuarios de buzones. A los usuarios no se les asigna una ABP predeterminada cuando se crea su cuenta. Si no asigna ninguna ABP a un usuario, éste tendrá acceso a la lista global de direcciones (LGD) de toda la organización a través de Outlook y Outlook Web App. Para obtener más información, vea [Directivas de la libreta de direcciones](address-book-policies-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las directivas de libretas de direcciones (ABP), consulte [Procedimientos de directivas de la libreta de direcciones](address-book-policy-procedures-exchange-2013-help.md).

¿Interesado en escenarios que utilizan este procedimiento? Consulte [Caso: implementación de directivas de libretas de direcciones](scenario-deploying-address-book-policies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de libreta de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Use el EAC para asignar una ABP a los usuarios de buzones

1.  Vaya a **Destinatarios** \> **Buzones**.

2.  En la vista de la lista, seleccione el usuario al que quiere asignar la directiva y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  Haga clic en **Características de buzón de correo**.

4.  En la lista de **Directiva de libreta de direcciones**, seleccione la ABP que quiere aplicar a este usuario.

5.  Haga clic en **Guardar**.

## Use el EAC para asignar una ABP a varios usuarios de buzones

1.  Vaya a **Destinatarios** \> **Buzones**.

2.  En la vista de la lista, utilice la tecla Ctrl para seleccionar varios usuarios.

3.  En el panel de detalles, haga clic en **Más opciones**.

4.  En **Directiva de libreta de direcciones**, haga clic en **Actualizar**.

5.  En la lista de **Seleccionar directiva de libreta de direcciones**, seleccione la ABP que quiere aplicar a estos usuarios.

6.  Haga clic en **Guardar**.

## Usar el Shell para asignar una ABP a los usuarios de buzones

En este ejemplo se asigna la ABP denominada Todo Fabrikam al usuario de buzón existente joe@fabrikam.com.

    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"

En este ejemplo se asigna la ABP llamada ABP\_EngineeringDepartment a todos los usuarios de buzón cuyo valor `CustomAttribute11` contiene “Departamento de Ingeniería”.

    Get-Mailbox -Filter {(CustomAttribute11 -like "Engineering Department")} | Set-Mailbox -AddressBookPolicy ABP_EngineeringDepartment

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) y [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)).

