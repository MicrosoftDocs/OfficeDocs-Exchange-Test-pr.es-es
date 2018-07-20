---
title: 'Configurar el número de errores de inicio de sesión antes de que se desconecten los usuarios de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurar el número de errores de inicio de sesión antes de que se desconecten los usuarios de Outlook Voice Access
ms:assetid: 02f93888-168c-44bb-8cf6-17f5fcc3d733
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423537(v=EXCHG.150)
ms:contentKeyID: 49895440
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el número de errores de inicio de sesión antes de que se desconecten los usuarios de Outlook Voice Access

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-09_

Puede especificar el número de intentos de inicio de sesión incorrectos sucesivos que se permiten antes de que se desconecte la llamada. El valor de este parámetro puede estar entre 1 y 20. Si configura un valor demasiado bajo, puede frustrar a los usuarios. Para la mayoría de las organizaciones, este valor se debería establecer en los tres intentos predeterminados.

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Use el EAC para configurar el número de fallos de inicio de sesión antes de que se desconecte a los usuarios

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de MU que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de la mensajería unificada**, haga clic en **Configurar**.

4.  En **Configuración**, en **Número de errores de inicio de sesión antes de desconectar**, introduzca el número de fallos de inicio de sesión.

5.  Haga clic en **Guardar**.

## Usar el Shell para configurar el número de errores de inicio de sesión antes de desconectar a los usuarios

En este ejemplo, se establece en 5 el número de errores de inicio de sesión antes de desconectar a los usuarios de un plan de marcado de MU denominado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -LogonFailuresBeforeDisconnect 5

