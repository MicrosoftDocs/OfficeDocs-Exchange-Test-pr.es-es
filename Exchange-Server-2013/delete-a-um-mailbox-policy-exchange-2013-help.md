---
title: 'Eliminar una directiva de buzón de mensajería unificada: Exchange 2013 Help'
TOCTitle: Eliminar una directiva de buzón de mensajería unificada
ms:assetid: c8758464-3c52-4dd3-b2a6-142a99bb0628
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124536(v=EXCHG.150)
ms:contentKeyID: 50556883
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminar una directiva de buzón de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

Cuando elimine una directiva de buzones de mensajería unificada (UM), ésta no estará disponible para ser asociada a destinatarios que se hayan habilitado para mensajería unificada. No se puede eliminar una directiva de buzones de mensajería unificada si hace referencia a buzones habilitados para mensajería unificada, así como tampoco se puede eliminar un plan de marcado de mensajería unificada si hay una directiva de buzones de mensajería unificada asociada a él.

Para conocer tareas de administración adicionales relacionadas con las directivas de buzones de mensajería unificada, consulte [Procedimientos de políticas de buzón de mensajería unificada](um-mailbox-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para eliminar una directiva de buzones de mensajería unificada

1.  
    
    En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, en la barra de herramientas, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

## Uso del Shell para eliminar una directiva de buzón de mensajería unificada

En este ejemplo se elimina una directiva de buzón de mensajería unificada llamada `MyUMMailboxPolicy`.

    Remove-UMMailboxPolicy -Identity MyUMMailboxPolicy

