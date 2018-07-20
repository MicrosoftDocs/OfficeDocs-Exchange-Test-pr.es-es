---
title: 'Deshabilitar el envío de faxes para un grupo de usuarios: Exchange 2013 Help'
TOCTitle: Deshabilitar el envío de faxes para un grupo de usuarios
ms:assetid: 1c57c3ba-2b0e-43dd-9b28-43bada1592c5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ650864(v=EXCHG.150)
ms:contentKeyID: 52061800
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar el envío de faxes para un grupo de usuarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Puede deshabilitar los faxes entrantes para usuarios asociados a una directiva de buzón de mensajería unificada (UM). De forma predeterminada, cuando habilita a los usuarios para Mensajería unificada, estos no pueden recibir mensajes de fax hasta que no especifique la URI del servidor de socio de fax, se implemente un servidor de socio de fax para la organización y se habilite el envío de faxes en una directiva de buzón de mensajería unificada. Si la opción para permitir faxes entrantes está deshabilitada en el plan de marcado de mensajería unificada, los usuarios vinculados con la directiva de buzón de mensajería unificada seguirán sin poder recibir faxes. De forma similar, si la opción de permitir faxes entrantes está deshabilitada para un usuario concreto, dicho usuario tampoco podrá recibir faxes.

Para obtener más información acerca de los partners de fax, consulte [Microsoft PinPoint para asociados de negocios de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para otras tareas de administración relacionadas con el envío de faxes, vea [Procedimientos de envío de faxes](faxing-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para deshabilitar faxes entrantes

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzón que quiere modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de mensajería unificada** \> **General**, desactive la casilla de **Permitir faxes entrantes**.

4.  Haga clic en **Guardar** para guardar los cambios.

## Usar el Shell para deshabilitar faxes entrantes

En este ejemplo se impide que los usuarios vinculados a la directiva de buzón de mensajería unificada `MyUMMailboxPolicy` usen faxes entrantes.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $false

