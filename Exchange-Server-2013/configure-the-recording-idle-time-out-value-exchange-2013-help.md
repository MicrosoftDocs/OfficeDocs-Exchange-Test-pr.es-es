---
title: 'Configurar el valor de tiempo de espera de grabación: Exchange 2013 Help'
TOCTitle: Configurar el valor de tiempo de espera de grabación
ms:assetid: a7fb9a09-fde9-447d-ad2c-95598405e99b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423550(v=EXCHG.150)
ms:contentKeyID: 49895823
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el valor de tiempo de espera de grabación

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-11_

Puede especificar la cantidad de segundos de silencio permitidos por el sistema durante la grabación de un mensaje de voz antes de finalizar la llamada. Para la mayoría de las organizaciones, este valor se debería establecer en los 5 segundos predeterminados.

Este valor puede establecerse entre 2 y 10. Si especifica un valor demasiado bajo, es posible que el sistema desconecte a las personas que llaman antes de que dejen sus mensajes de voz. Si especifica un valor demasiado alto, es posible que los mensajes incluyan silencios prolongados.

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Utilice la EAC para configurar el valor de tiempo de espera de inactividad de grabación

1.  En la EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

4.  En **Configuraciones**, en **Tiempo de espera de inactividad de grabación (segundos)**, escriba el número en segundos.

5.  Haga clic en **Guardar**.

## Usar el Shell para configurar el valor del tiempo de espera de inactividad en la grabación

En este ejemplo, se establece en 10 el valor de tiempo de espera de inactividad en la grabación para un plan de marcado de MU denominado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -RecordingIdleTimeout 10

