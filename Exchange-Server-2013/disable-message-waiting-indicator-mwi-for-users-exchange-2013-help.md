---
title: 'Deshabilitar el indicador de espera de mensaje (MWI) para los usuarios: Exchange 2013 Help'
TOCTitle: Deshabilitar el indicador de espera de mensaje (MWI) para los usuarios
ms:assetid: 51cd6dc4-11d1-4eb9-a6c6-1965fcd24267
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673525(v=EXCHG.150)
ms:contentKeyID: 50556806
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar el indicador de espera de mensaje (MWI) para los usuarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-21_

Puede habilitar o deshabilitar el indicador de mensaje en espera para usuarios que estén asociados con una directiva de buzón de mensajería unificada. Indicador de mensaje en espera es una función incluida en la mayoría de los sistemas de correo de voz heredados. En su formato más básico, enciende una luz en el teléfono de un suscriptor del correo de voz para indicar la presencia de un nuevo mensaje de correo de voz. El indicador de mensaje en espera también puede ser un mensaje de texto al teléfono móvil del usuario habilitado para mensajería unificada. De forma predeterminada, esta función está habilitada.

Si el indicador de mensaje en espera está deshabilitado en la puerta de enlace IP de MU, la función no está disponible para los usuarios habilitados para MU asociados con la directiva de buzón de MU.

Para conocer tareas de administración adicionales relacionadas con directivas de buzones de correo de MU, consulte [Procedimientos de políticas de buzón de mensajería unificada](um-mailbox-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para deshabilitar el indicador de mensaje en espera

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En **Directivas de buzón de MU**, seleccione la directiva de buzón de MU que desea administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de MU**, desactive la casilla al lado de **Permitir indicador de mensaje en espera**.

4.  Haga clic en **Guardar**.

## Uso del Shell para deshabilitar el indicador de mensaje en espera

En este ejemplo, se deshabilita el indicador de mensaje en espera para usuarios asociados con la directiva de buzón de MU denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMessageWaitingIndicator $false

