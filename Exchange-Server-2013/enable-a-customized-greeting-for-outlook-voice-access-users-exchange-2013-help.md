---
title: 'Habilitar un saludo personalizado para los usuarios de Outlook Voice Access'
TOCTitle: Habilitar un saludo personalizado para los usuarios de Outlook Voice Access
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50556848
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar un saludo personalizado para los usuarios de Outlook Voice Access

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

De forma predeterminada, cada plan de marcado de mensajería unificada usa un archivo .wav estándar para el saludo de bienvenida que se reproduce a las personas que llaman, incluyendo los usuarios de Outlook Voice Access que marcan un número de Outlook Voice Access configurado. Sin embargo, puede crear un archivo .wav o .wma para el saludo de bienvenida y, a continuación, habilitarlo en el plan de marcado de mensajería unificada.

Por ejemplo, tal vez desee cambiar este saludo de bienvenida predeterminado y utilizar otro saludo de bienvenida específico de su empresa, como "Le damos la bienvenida a Outlook Voice Access para Woodgrove Bank." Para hacerlo, grabe el saludo de bienvenida personalizado y guárdelo como un archivo .wav o .wma. A continuación, configure el plan de marcado para usar el saludo de bienvenida personalizado.

Para obtener más información acerca de las opciones de menú disponibles para usuarios de Outlook Voice Access, consulte la Guía de referencia rápida de Outlook Voice Access, que está disponible en el [Centro de descargas de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=272767).

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar un saludo de bienvenida personalizado

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

4.  En **Outlook Voice Access**, en **Saludo de bienvenida**, haga clic en **Cambiar** y, a continuación, haga clic en **Examinar** para ubicar el archivo de saludo.
    

    > [!IMPORTANT]
    > El archivo que use para el saludo de bienvenida debe ser un archivo .wav o .wma.



5.  Después de ubicar el archivo, haga clic en **Abrir** y, a continuación, haga clic en **Guardar**.

## Usar el Shell para habilitar un saludo de bienvenida personalizado

En este ejemplo, se habilita un saludo de bienvenida que usa el archivo ubicado en C:\\UMPrompts\\welcome.wav para un plan de marcado de mensajería unificada denominado `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav

