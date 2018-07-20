---
title: 'Deshabilitar la vista previa del correo de voz para usuarios: Exchange 2013 Help'
TOCTitle: Deshabilitar la vista previa del correo de voz para usuarios
ms:assetid: 362fed13-3a9c-4111-bfa4-8c45ab6a3a01
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335199(v=EXCHG.150)
ms:contentKeyID: 51406489
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar la vista previa del correo de voz para usuarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-21_

Puede deshabilitar la función de Vista previa de correo de voz para los usuarios asociados a una directiva de buzones de mensajería unificada (UM). Si se deshabilita esta configuración, los usuarios no podrán recibir el texto de un mensaje de correo de voz en el cuerpo de un correo o mensaje de texto. La configuración predeterminada está habilitada.

Para conocer tareas de administración adicionales relacionadas con las directivas de buzones de mensajería unificada, consulte [Procedimientos de políticas de buzón de mensajería unificada](um-mailbox-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para deshabilitar la vista previa de correo de voz

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**, seleccione el plan de marcado de la mensajería unificada que quiere modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de mensajería unificada**, seleccione la directiva de buzón de UM que quiera administrar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de mensajería unificada** \> **General**, desactive la casilla de **Permitir vista previa de correo de voz**.

4.  Haga clic en **Guardar**.

## Usar el Shell para deshabilitar la vista previa de correo de voz

En este ejemplo, se evita que los usuarios que están asociados a una directiva de buzón de MU `MyUMMailboxPolicy` usen la función Vista previa de correo de voz.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy - AllowVoiceMailPreview $false

