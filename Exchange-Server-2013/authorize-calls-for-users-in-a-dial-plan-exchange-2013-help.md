---
title: 'Autorizar llamadas a los usuarios en un plan de marcado: Exchange 2013 Help'
TOCTitle: Autorizar llamadas a los usuarios en un plan de marcado
ms:assetid: 7c7fd0c4-4001-408e-b352-c49bac9f78cc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb691175(v=EXCHG.150)
ms:contentKeyID: 51406513
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizar llamadas a los usuarios en un plan de marcado

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-21_

Puede habilitar autorizaciones de marcado en un plan de marcado de mensajería unificada (UM). Las autorizaciones de marcado en un plan de marcado se utilizan para impedir que los usuarios no autenticados de Outlook Voice Access realicen llamadas nacionales/regionales o internacionales, o *llamadas externas*. Las llamadas externas se producen cuando la mensajería unificada realiza una llamada saliente para un usuario después de que hayan llamado a un número de teléfono de Outlook Voice Access que está configurado en un plan de marcado de MU. Cuando configura una opción en un plan de marcado de MU, dicha opción se aplica a todos los usuarios no autenticados que llaman a un número de Outlook Voice Access.

Para otras tareas de administración relacionadas con las llamadas externas, consulte [Permitir a los usuarios realizar llamadas a procedimientos](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-users-to-make-calls-procedures).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Antes de realizar este procedimiento, confirme que se han creado las reglas de marcado nacionales/regionales e internacionales en un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear reglas de marcado para usuarios](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/create-dialing-rules).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EMC para habilitar autorizaciones de marcado en un plan de marcado de MU para grupos de reglas de marcado nacionales o regionales

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

3.  En la página **Plan de marcado de MU** \> **Autorización de marcado**, haga clic en **Añadir**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") en **Grupos de reglas de marcado nacional o regional**.

4.  En la página **Seleccionar grupos de reglas de marcado para permitir**, seleccione el grupo de reglas de marcado, haga clic en **Aceptar** y, a continuación, haga clic en **Guardar**.

## Use el EAC para permitir autorizaciones de marcado en un plan de marcado de MU para grupos de reglas de marcado internacional

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

3.  En la página **Plan de marcado de MU** \> **Autorización de marcado**, haga clic en **Añadir**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") en **Grupos de reglas de marcado internacional autorizados**.

4.  En la página **Seleccionar grupos de reglas de marcado para permitir**, seleccione el grupo de reglas de marcado, haga clic en **Aceptar** y, a continuación, haga clic en **Guardar**.

## Usar el Shell para habilitar autorizaciones de marcado nacionales o regionales en un plan de marcado de MU

En este ejemplo, se habilitan las autorizaciones de marcado InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1 e InternationalGroup2 en un plan de marcado de MU denominado `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

