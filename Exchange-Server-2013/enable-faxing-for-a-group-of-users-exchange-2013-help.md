---
title: 'Habilitar el envío de faxes para un grupo de usuarios: Exchange 2013 Help'
TOCTitle: Habilitar el envío de faxes para un grupo de usuarios
ms:assetid: b8d9f54d-ff06-4942-83e1-fc6c4ad02178
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423556(v=EXCHG.150)
ms:contentKeyID: 52061873
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar el envío de faxes para un grupo de usuarios

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Puede habilitar los faxes entrantes para los usuarios vinculados a una directiva de buzones de correo de mensajería unificada. Cuando se habilitan usuarios para mensajería unificada, estos no pueden recibir mensajes de fax de forma predeterminada, hasta que especifique el URI del servidor de fax asociado, implemente un servidor de fax asociado a su organización y habilite los faxes en una directiva de buzones de correo de mensajería unificada. Si la opción para permitir faxes entrantes está deshabilitada en el plan de marcado de mensajería unificada, los usuarios vinculados a la directiva de buzones de correo de mensajería unificada seguirán sin poder recibir faxes. De igual modo, si la opción para permitir faxes entrantes está deshabilitada en un usuario individual, dicho usuario no podrá recibir faxes.

Para obtener más información acerca de los partners de fax, consulte [Microsoft PinPoint para asociados de negocios de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para otras tareas de administración relacionadas con los faxes, consulte [Procedimientos de envío de faxes](faxing-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar los faxes entrantes

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzones de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de mensajería unificada** \> **General**, active la casilla al lado de **Permitir faxes entrantes**.

4.  Haga clic en **Guardar** para guardar los cambios.

## Usar el Shell para habilitar los faxes entrantes

En este ejemplo se permite que los usuarios vinculados a la directiva de buzones de mensajería unificada de `MyUMMailboxPolicy` usen faxes entrantes.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $true

