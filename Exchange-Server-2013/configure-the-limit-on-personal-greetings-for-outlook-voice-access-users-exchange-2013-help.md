---
title: 'Configurar límite saludos personales para usuarios Outlook Voice Access'
TOCTitle: Configurar el límite de saludos personales para los usuarios de Outlook Voice Access
ms:assetid: d400f250-0f55-45f5-9918-5f1d7819fbdf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201731(v=EXCHG.150)
ms:contentKeyID: 50556892
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el límite de saludos personales para los usuarios de Outlook Voice Access

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

La configuración de **Límite de saludos personales (minutos)** permite escribir el número máximo de minutos que pueden usar los usuarios asociados a la directiva de buzones de mensajería unificada (UM) para grabar su saludo de correo por voz. Esta configuración se aplica a sus saludos de correos de voz estándar y de correos de voz de Fuera de la oficina. De forma predeterminada, la duración máxima de saludo está establecida en 5 minutos. Sin embargo, puede establecer la duración máxima del saludo en cualquier valor entre 1 y 10 minutos.

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

## Uso de la EAC para cambiar la duración máxima del saludo

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de la lista, seleccione el plan de marcado de mensajería unificada que quiere modificar y luego, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página de **plan de marcado de mensajería unificada**, en **Directivas de buzón correo de mensajería unificada**, seleccione la directiva de buzones de mensajería unificada que desea administrar y, a continuación, en la barra de herramientas haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de mensajería unificada** \> **General**, en **Límite de saludos personales (minutos)**, escriba la duración, en minutos, permitida para los saludos personales de los usuarios de correo de voz.

4.  Haga clic en **Guardar**.

## Uso del Shell para cambiar el la duración máxima de saludo

En este ejemplo se configura la duración máxima de saludo de la directiva de buzón de UM `MyUMMailboxPolicy` en 3 minutos.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy MaxGreetingDuration 3

