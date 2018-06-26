---
title: 'Permitir o impedir que los usuarios de la misma directiva de buzón de mensajería unificada desde la creación de reglas de respuesta de llamada: Exchange 2013 Help'
TOCTitle: Permitir o impedir que los usuarios de la misma directiva de buzón de mensajería unificada desde la creación de reglas de respuesta de llamada
ms:assetid: e44acaa6-d5a8-41e8-94aa-100be0bd6391
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351209(v=EXCHG.150)
ms:contentKeyID: 50556900
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir o impedir que los usuarios de la misma directiva de buzón de mensajería unificada desde la creación de reglas de respuesta de llamada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Puede permitir que los usuarios asociados a una directiva de buzones de mensajería unificada (UM) configuren reglas de respuesta a llamadas o evitar que lo hagan. Si la opción para configurar reglas de respuesta a llamadas está deshabilitada en un plan de marcado de mensajería unificada, la función de reglas de respuesta a llamadas no estará disponible para los usuarios habilitados para mensajería unificada asociados a la directiva de buzones de mensajería unificada. De forma predeterminada, esta opción está habilitada.

Para conocer tareas de administración adicionales que permitan a los usuarios reenviar llamadas, vea [Reenvío de llamadas a procedimientos](forwarding-calls-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para habilitar o deshabilitar reglas de respuesta a llamadas para una directiva de buzones de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzones de mensajería unificada que desea administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de correo de mensajería unificada**, active o desactive la casilla de **Permitir a los usuarios configurar reglas de contestador automático**.

4.  Haga clic en **Guardar**.

## Usar el Shell habilitar o deshabilitar reglas de contestador automático en una directiva de buzón de MU

En este ejemplo se permite que los usuarios asociados a la directiva de buzones de mensajería unificada de `MyUMMailboxPolicy` creen reglas de respuesta a llamadas.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $true

En este ejemplo se impide que los usuarios asociados a la directiva de buzón de mensajería unificada `MyUMMailboxPolicy` creen reglas de contestador automático.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $false

