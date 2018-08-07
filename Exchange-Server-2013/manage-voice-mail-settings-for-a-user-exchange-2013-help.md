---
title: 'Administrar configuración de correo de voz para un usuario: Exchange 2013 Help'
TOCTitle: Administrar la configuración de correo de voz para un usuario
ms:assetid: 73957938-048a-4f9c-bd0f-a3c2c3dcd638
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998851(v=EXCHG.150)
ms:contentKeyID: 49895710
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar la configuración de correo de voz para un usuario

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede ver o establecer las características de mensajería unificada (MU) y de correo de voz, así como los valores de configuración de un usuario que tiene habilitada la MU y el correo de voz. Por ejemplo, puede hacer lo siguiente:

  - Restablecer su PIN de acceso de voz de Outlook.

  - Agregar un número de extensión de operador personal.

  - Añadir otros números de extensión.

  - Habilitar o deshabilitar el reconocimiento de voz automático (ASR).

  - Habilitar o deshabilitar reglas de respuesta a llamada.

  - Habilitar o deshabilitar el acceso a su correo electrónico o calendario.


> [!NOTE]
> Algunas de las configuraciones y características únicamente se pueden configurar mediante el Shell.



Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que el usuario existente actualmente tenga la mensajería unificada habilitada. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para ver o configurar las propiedades de un usuario habilitado para mensajería unificada

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En la vista de lista, seleccione el buzón de correo para el que desee cambiar la directiva de buzón de mensajería unificada.

3.  En el panel de detalles, bajo **Funciones de teléfono y voz** \> **Mensajería unificada**, haga clic en **Ver detalles**.

4.  En la página **Buzón de mensajería unificada**, haga clic en **Configuración de buzón de MU** para ver o cambiar las siguientes propiedades de MU de un usuario habilitado con mensajería unificada:
    
      - **Estado de PIN**   Este campo de solo visualización muestra el estado del buzón del usuario. De forma predeterminada, cuando un usuario tiene habilitada la MU, el estado de PIN aparece como **No bloqueado**. Sin embargo, si el usuario ha escrito varias veces un PIN de Outlook Voice Access incorrecto, el estado se muestra como **Bloqueado**.
    
      - **Directiva de buzón de MU**   Este cuadro muestra el nombre de la directiva de buzón de MU asociado al usuario con MU habilitada. Puede hacer clic en **Explorar** para localizar y especificar la directiva de MU que desea asociar a este buzón de MU.
    
      - **Extensión de operador personal**   Utilice este cuadro para especificar el número de extensión del operador para el usuario. De forma predeterminada, no está configurado un número de extensión. La longitud del número de extensión puede ser de 1 a 20 caracteres. Esto permite que las llamadas entrantes del usuario habilitado con MU se reenvíen al número de extensión que ha especificado en este cuadro.
        
        Puede configurar otros tipos de números de extensión del operador en planes de marcado y operadores automáticos. Sin embargo, estas extensiones están generalmente destinadas a recepcionistas u operadores de toda una compañía. La opción de extensión de operador personal se puede utilizar cuando un asistente administrativo o ayudante personal responde a las llamadas entrantes antes de que las responda un usuario en particular.

5.  En la página **Buzón de MU**, bajo **Otras extensiones**, puede agregar, cambiar y ver los números de extensión del usuario.
    
      - Para agregar un número de extensión, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la página **Agregar otra extensión**, utilice el botón **Explorar** para seleccionar el plan de marcado de MU y, a continuación, introduzca el número de extensión en el cuadro **Número de extensión**.
    
      - Para quitar un número de extensión, seleccione el que desea quitar y, a continuación, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

6.  Si realiza cualquier cambio, haga clic en **Guardar**.

## Usar el Shell para configurar las características de un usuario habilitado para mensajería unificada

En este ejemplo se deshabilita Reproducir en teléfono y las notificaciones de llamada, pero se habilita las notificaciones de mensajes de texto (SMS).


> [!NOTE]
> Para implementaciones locales e híbridas, al integrar la mensajería unificada en Lync Server, las notificaciones de llamadas perdidas no estarán disponibles para los usuarios que tengan un buzón en un servidor de buzones de Exchange 2007 o Exchange 2010. Las notificaciones de llamadas perdidas se generan cuando un usuario se desconecta antes de que la llamada se envíe a un servidor de buzones.



    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -MissedCallNotificationEnabled $false -PlayonPhoneEnabled $false -SMSMessageWaitingNotificationEnabled $true

En este ejemplo se evita que un usuario tenga acceso al calendario, pero se admite acceso al correo electrónico si usa Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -Extension 523456 -FAXEnabled $true -TUIAccessToCal $false -TUIAccessToEmail True

En este ejemplo se evita que un usuario tenga acceso al calendario y al correo electrónico si usa Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -TUIAccessToCalendarEnabled $false -TUIAccessToEmailEnabled $false

En este ejemplo se impido que un usuario cree reglas de respuesta a llamada, reciba fax entrante y use Outlook Voice Access, pero se habilita el reconocimiento de voz automático (ASR).

    Set-UMMailbox -Identity tony@contoso.com -AutomaticSpeechRecognitionEnabled $true -CallAnsweringRulesEnabled $false -FaxEnabled $false -SubscriberAccessEnabled $false 

## Uso del Shell para ver las propiedades de un usuario habilitado para UM

En este ejemplo se muestra una lista de todos los buzones habilitados para mensajería unificada en el bosque en una lista con formato.

    Get-UMMailbox | Format-List

En este ejemplo se muestran las propiedades del buzón de mensajería unificada de tonysmith@contoso.com.

    Get-UMMailbox -Identity tonysmith@contoso.com


> [!IMPORTANT]
> Si ejecuta Exchange 2007 y Exchange 2013, y el buzón del usuario está ubicado en un servidor de buzones de Exchange 2007, la ejecución del cmdlet <STRONG>Get-UMMailbox</STRONG> no funcionará correctamente. Para resolver este problema, ejecute el cmdlet <STRONG>Get-UMMailbox</STRONG> desde un servidor de Exchange 2007 o desde un equipo que ejecute las herramientas administrativas de Exchange 2007.


