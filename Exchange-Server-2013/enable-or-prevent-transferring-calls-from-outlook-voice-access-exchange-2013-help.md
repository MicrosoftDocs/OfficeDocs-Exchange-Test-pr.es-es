---
title: 'Permitir o impedir la transferencia de llamadas desde Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Permitir o impedir la transferencia de llamadas desde Outlook Voice Access
ms:assetid: b80c57f1-394c-4608-8ad3-52a3e6d697db
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423554(v=EXCHG.150)
ms:contentKeyID: 52061874
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir o impedir la transferencia de llamadas desde Outlook Voice Access

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede permitir o impedir que los usuarios de Outlook Voice Access transfieran llamadas a un usuario asociado a un plan de marcado de mensajería unificada. Tanto esta opción como la opción **Dejar mensajes de voz sin que el teléfono de un usuario suene** están habilitadas de forma predeterminada, de modo que los usuarios de Outlook Voice Access pueden transferir llamadas a los usuarios en el mismo plan de marcado de mensajería unificada y dejarles mensajes de voz. Esta configuración solamente es válida con los usuarios de Outlook Voice Access que han especificado su PIN y están autenticados.

Para obtener más información acerca de otras tareas relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para permitir o impedir que los usuarios de Outlook Voice Access transfieran llamadas

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

3.  En **transferir & y buscar**, en **Permitir a quienes llaman**, active la casilla al lado de **se transfiera a los usuarios** para permitir que los autores de la llamada transfieran llamadas a otros usuarios dentro del plan de marcado. Si desea impedir que los usuarios de Outlook Voice Access transfieran llamadas a los usuarios, desactive esta casilla.

4.  Haga clic en **Guardar**.

## Usar el Shell para permitir o impedir que los usuarios de Outlook Voice Access transfieran llamadas

Este ejemplo permite que los usuarios de Outlook Voice Access transfieran llamadas a los usuarios en el mismo plan de marcado en un plan de marcado de mensajería unificada denominado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $true

En este ejemplo se impide que los usuarios de Outlook Voice Access transfieran llamadas a los usuarios en el mismo plan de marcado en un plan de marcado de mensajería unificada denominado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $false

