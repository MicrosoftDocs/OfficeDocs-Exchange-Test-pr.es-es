---
title: 'Configurar un número de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurar un número de Outlook Voice Access
ms:assetid: 443c838e-f266-4893-b6b2-e5fc96579b55
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997680(v=EXCHG.150)
ms:contentKeyID: 50556777
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar un número de Outlook Voice Access

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Un número de Outlook Voice Access permite que un usuario habilitado para la mensajería unificada y el correo de voz obtenga acceso a su buzón de correo mediante Outlook Voice Access. Cuando se configura un número de acceso de suscriptor o de Outlook Voice Access en un plan de marcado, los usuarios habilitados para la MU pueden llamar al número, iniciar una sesión en su buzón de correo y tener acceso a su correo electrónico, correo de voz, calendario e información de contacto personal.

De manera predeterminada, cuando se crea un plan de marcado de MU, no se configura ningún número de Outlook Voice Access. Para configurar un número de Outlook Voice Access, primero debe crear el plan de marcado y, luego, configurar el número de Outlook Voice Access en la opción **Outlook Voice Access** del plan de marcado. Si bien no es obligatorio tener un número de Outlook Voice Access, deberá configurar uno como mínimo para que un usuario habilitado para mensajería unificada pueda usar Outlook Voice Access para obtener acceso a sus buzones. Puede configurar varios números de Outlook Voice Access para un único plan de marcado.

Los números de Outlook Voice Access pueden incluir caracteres alfanuméricos y especiales, separadores y espacios. Por ejemplo:

  - \+14255551010

  - \+1-425-555-1010

  - 4255551010

  - \+1 425 555 1010

  - 1-800-555-CALL

Para obtener más información acerca de las opciones disponibles para los usuarios de Voice Access Outlook, consulte a la Guía de referencia rápida para Outlook Voice Access, que está disponible en el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=64645).

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para configurar un número de Outlook Voice Access

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de la lista, seleccione el plan de marcado de MU que quiere modificar y, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

4.  En **Outlook Voice Access**, en **Números de Outlook Voice Access**, use el cuadro para especificar el número que desea usar y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

5.  Haga clic en **Guardar**.

## Uso del Shell para configurar un número de Outlook Voice Access

En este ejemplo, se establece el número de Outlook Voice Access en 4255550100 para un plan de marcado de MU denominado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AccessTelephoneNumbers 4255550100

