---
title: 'Habilitar a un usuario para el correo de voz: Exchange 2013 Help'
TOCTitle: Habilitar a un usuario para el correo de voz
ms:assetid: ad027767-5e14-4cb1-9f8a-0791d9188db5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124147(v=EXCHG.150)
ms:contentKeyID: 49895831
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.EnableUnifiedMessagingWizardForm.EnableUnifiedMessagingWizardPage
ms.translationtype: HT
---

# Habilitar a un usuario para el correo de voz

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Cuando se habilita a un usuario para mensajería unificada, se le aplican un conjunto de propiedades con las que el usuario podrá usar las características de correo de voz incluidas con la mensajería unificada. Después de habilitar un usuario para correo de voz, tiene la opción de agregar una dirección de Protocolo de inicio de sesión (SIP) al usuario si está asignado a una directiva de buzones de correo de mensajería unificada que esté vinculada al plan de marcado URI de SIP. O, puede agregar un número E.164 al usuario si está asignado a una directiva de buzones de correo de mensajería unificada vinculada al plan de marcado E.164. En ambos casos, el usuario debe tener un número de extensión configurado.

Se necesita un número de extensión para cada usuario que esté asociado con una extensión telefónica, un Identificador uniforme de recursos (URI) SIP o un plan de marcado E.164. El número de extensión debe tener el número correcto de dígitos, según se especifica en el plan de marcado de mensajería unificada para la directiva de buzón de mensajería unificada.


> [!NOTE]
> Debe agregar, quitar o modificar los números de extensión para todos los usuarios habilitados para mensajería unificada mediante el uso del EAC o el Shell, incluso si están vinculados a un plan de marcado URI de SIP o E.164. Para agregar, quitar o modificar una dirección SIP o los números E.164 para los usuarios necesitará usar el Shell, dado que estas opciones no están disponibles en el EAC.



Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para habilitar a un usuario para correo de voz

1.  En el EAC, haga clic en **Destinatarios**.

2.  En la vista de lista, seleccione el usuario cuyo buzón desee deshabilitar para la mensajería unificada.

3.  En el panel de detalles, en **Características de voz y teléfono**, haga clic en **Habilitar**.

4.  En la página **Habilitar el buzón de correo de mensajería unificada**, haga clic en el botón **Explorar** al lado de **Directivas de buzón de mensajería unificada**, ubique en la lista la directiva de buzones de correo de mensajería unificada que va a asignar al usuario y, a continuación, haga clic en **Aceptar**.

5.  En la página **Habilitar el buzón de correo de mensajería unificada**, complete los siguientes campos:
    
      - **Dirección SIP** o **Número E.164**   En el cuadro de texto **Dirección SIP** o **Número E.164**, escriba la dirección SIP o el número E.164 del usuario. Estas opciones están disponibles si el usuario que habilitó para mensajería unificada está asignado a la directiva de buzones de correo de mensajería unificada vinculada a un plan de marcado URI de SIP o E.164. No puede añadir una dirección SIP o un número E.164 para un usuario si el usuario está asociado con el plan de marcado de la extensión del teléfono.
        
        Cuando asigne un usuario a una directiva de buzones de correo de mensajería unificada vinculada a un plan de marcado de E.164 o URI de SIP, debe introducir un número de extensión para el usuario. El usuario usará este número de extensión cuando acceda a su buzón de correo a través de Outlook. El número de dígitos que se configura en esta casilla debe coincidir con el número de dígitos configurados en el plan de marcado URI de SIP o E.164.
    
      - **Número de extensión**   Use este cuadro de texto para ingresar manualmente el número de extensión para el usuario que está habilitando para mensajería unificada.
        
        Deberá proporcionar un número de extensión válido para el usuario y deberá coincidir con el número de dígitos especificado en el plan de marcado. Solo puede introducir dígitos del 1 al 20. El número de extensión típico es de 3 a 7 dígitos de largo. El número de dígitos en la extensión se configura en el plan de marcado que está vinculado a la directiva de buzones de correo de mensajería unificada asignada al usuario.
    
      - En **Configuración de PIN**, complete lo siguiente:
        
          - **Generar un PIN automáticamente**   Haga clic en este botón para generar de forma automática un PIN para que el usuario habilitado para mensajería unificada use el acceso al correo de voz por medio de Outlook Voice Access. Esta es la configuración predeterminada. El PIN se genera automáticamente de acuerdo con las directivas de PIN configuradas en la directiva de buzones de correo de mensajería asignada al usuario. El uso de esta configuración ayudará a proteger al PIN del usuario. El PIN se envía al usuario en el mensaje de bienvenida que este recibe después de su habilitación para MU. De manera predeterminada, tendrá que cambiar este PIN la primera vez que inicie sesión en el buzón de correo para obtener el correo de voz.
        
          - **Escriba un PIN**   Haga clic en este botón para escribir un PIN que el usuario usará para tener acceso al sistema de correo de voz. El PIN debe cumplir las opciones de la directiva de PIN configuradas en la directiva de buzón de mensajería unificada que esté asociada al usuario habilitado para mensajería unificada. Por ejemplo, si la directiva de buzón de correo de MU está configurada para aceptar solamente PIN que contengan siete o más dígitos, el PIN que introduzca en este cuadro debe tener al menos siete dígitos.
        
          - **Pedir que el usuario restablezca su PIN la primera vez que inicia sesión**   Seleccione esta casilla para obligar al usuario a que restablezca su PIN de correo de voz cuando acceda por primera vez al sistema de correo de voz desde un teléfono mediante el uso de Outlook Voice Access. Se le solicitará que introduzca un PIN con el que esté familiarizado. Hacer que los usuarios con habilitación para MU cambien el PIN la primera vez que inician sesión es un procedimiento recomendado de seguridad que los ayuda a protegerse contra el acceso no autorizado a sus datos y su bandeja de entrada. Esta casilla está activada de forma predeterminada.

6.  En la página **Habilitar el buzón de correo de mensajería unificada**, revise las configuraciones. Haga clic en **Finalizar** para habilitar al usuario para el correo de voz. Haga clic en **Atrás** para realizar cambios de configuración.

## Uso del Shell para habilitar a un usuario para correo de voz

En este ejemplo se habilita la mensajería unificada del buzón de correo de tonysmith@contoso.com, se configura el número de extensión como 51234, se configura el PIN para el usuario como 5643892 y se asigna al usuario una directiva de buzones de correo de mensajería unificada denominada `MyUMMailboxPolicy`.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

En este ejemplo se habilita la mensajería unificada en el buzón de correo de tonysmith@contoso.com, se asigna el usuario a una directiva de buzones de correo de mensajería unificada denominada `MyUMMailboxPolicy` y se establece el número de extensión, la dirección SIP y el PIN del usuario.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

