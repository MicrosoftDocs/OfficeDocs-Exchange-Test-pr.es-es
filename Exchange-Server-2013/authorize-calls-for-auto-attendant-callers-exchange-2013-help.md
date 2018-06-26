---
title: '¿Autorizar llamadas de llamadores de operador automático: Exchange 2013 Help'
TOCTitle: ¿Autorizar llamadas de llamadores de operador automático
ms:assetid: c6c94fad-64df-44aa-a198-980f017ef716
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb691238(v=EXCHG.150)
ms:contentKeyID: 51406554
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ¿Autorizar llamadas de llamadores de operador automático

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-21_

Puede habilitar las autorizaciones de marcado en un operador automático de mensajería unificada. Las autorizaciones de marcado en un operador automático se usan para prohibir que los usuarios que llaman al operador automático realicen llamadas telefónicas nacionales/regionales o internacionales o *llamadas externas*. Las llamadas externas se producen cuando la mensajería unificada realiza una llamada saliente para un usuario después de haber llamado a un número de teléfono configurado en un operador automático de mensajería unificada.

Para otras tareas de administración relacionadas con las llamadas externas, consulte [Permitir a los usuarios realizar llamadas a procedimientos](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que se han creado reglas de marcado nacional/regional e internacional en un plan de marcado de mensajería unificada. Para conocer los pasos detallados, consulte [Crear reglas de marcado para usuarios](create-dialing-rules-for-users-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar autorizaciones de marcado en un operador automático de mensajería unificada para grupos de reglas nacionales/regionales

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de MU**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada para el que quiera crear una autorización de marcado y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada** \> **Autorización de marcado**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") en **Grupos de reglas de marcado nacional/regional autorizados**.

4.  En la página **Seleccionar grupos de reglas de marcado para permitir**, seleccione el grupo de reglas de marcado, haga clic en **Aceptar** y, a continuación, haga clic en **Guardar**.

## Usar el EAC para habilitar autorizaciones de marcado en un operador automático de mensajería unificada para grupos de reglas internacionales

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de MU**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada para el que quiera crear una autorización de marcado y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada** \> **Autorización de marcado**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") en **Grupos de reglas de marcado internacional autorizados**.

4.  En la página **Seleccionar grupos de reglas de marcado para permitir**, seleccione el grupo de reglas de marcado, haga clic en **Aceptar** y, a continuación, haga clic en **Guardar**.

## Usar el Shell para habilitar autorizaciones de marcado nacional/regional en un operador automático de mensajería unificada

En este ejemplo se habilitan las autorizaciones de marcado InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1 e InternationalGroup2 en un operador automático de mensajería unificada denominado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

