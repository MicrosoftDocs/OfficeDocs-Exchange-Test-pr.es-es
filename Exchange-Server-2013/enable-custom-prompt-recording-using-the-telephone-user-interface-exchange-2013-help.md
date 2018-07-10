---
title: 'Habilitar la grabación de mensajes personalizados con la interfaz de usuario de teléfono: Exchange 2013 Help'
TOCTitle: Habilitar la grabación de mensajes personalizados con la interfaz de usuario de teléfono
ms:assetid: f2e5c636-2be9-4d48-b5e7-37913ded62d1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb691404(v=EXCHG.150)
ms:contentKeyID: 54652461
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar la grabación de mensajes personalizados con la interfaz de usuario de teléfono

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2014-09-17_

El Shell es válido para habilitar la grabación de mensajes y saludos personalizados para planes de marcado de mensajería unificada (MU) y operadores automáticos mediante la interfaz de usuario de teléfono (TUI). Esto puede resultar útil cuando quiere cambiar un anuncio o saludo personalizado mediante el EAC o el Shell, o bien cuando se presenta una emergencia como el cierre de una organización debido a malas condiciones meteorológicas. Cuando va a cambiar un anuncio o saludo personalizado en un operador automático de mensajería unificada, debe habilitar la grabación de mensajes de TUI en el plan de marcado con el que está asociado el operador automático de mensajería unificada.

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entradas "Planes de marcado de mensajería unificada" y \&quot;Operadores automáticos de mensajería unificada\&quot; del tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué quiere hacer?

## Uso del Shell para habilitar la grabación de mensajes o saludos personalizados mediante la interfaz de usuario de teléfono

Para grabar saludos y mensajes personalizados con la interfaz de usuario de teléfono (TUI), siga estos pasos:

1.  Cree una cuenta de usuario de dominio que no pueda iniciar la sesión de forma interactiva.

2.  Delegue la función Administrador de la organización de Exchange a la cuenta de usuario de dominio.

3.  Cree un buzón para el usuario de dominio.

4.  Habilite el buzón del usuario de dominio para mensajería unificada.
    

    > [!IMPORTANT]
    > Permita que solo los administradores de saludos y mensajes puedan obtener acceso al número de extensión y el PIN de la cuenta de usuario. Use esta cuenta de usuario solo para administrar los mensajes por teléfono.



5.  Cree y guarde un archivo .wav o .wma para usar en un saludo personalizado para el operador automático o plan de marcado de MU.
    

    > [!NOTE]
    > Los archivos MP3 no se pueden usar en saludos personalizados.



6.  Use el EAC o el Shell para configurar el plan de marcado para usar el saludo de bienvenida personalizado o configurar el operador automático para usar el saludo en horario comercial o no comercial. Para obtener información más detallada sobre cómo configurar un plan de marcado, consulte [Habilitar un saludo personalizado para los usuarios de Outlook Voice Access](enable-a-customized-greeting-for-outlook-voice-access-users-exchange-2013-help.md). Para obtener información más detallada sobre cómo configurar un operador automático, consulte [Habilitar un saludo de horario comercial personalizada](enable-a-customized-business-hours-greeting-exchange-2013-help.md) o [Habilitar un personalizada no - saludo de horario comercial](enable-a-customized-non-business-hours-greeting-exchange-2013-help.md).

7.  Ejecute el siguiente cmdlet:
    
        Set-UMDialPlan -identity MyUMDialPlan -TUIPromptEditingEnabled $true


> [!NOTE]
> Antes de que pueda habilitar la grabación de un saludo o mensaje personalizado, debe iniciar sesión en el buzón configurado para grabar mensajes. Tras grabar el nuevo saludo o mensaje, debe cerrar sesión y volver a iniciar sesión antes de que pueda escuchar el nuevo saludo o mensaje cuando usa la TUI.



## Realizar la grabación de mensajes de Interfaz de usuario de teléfono (TUI) en un operador automático de mensajería unificada

1.  Compruebe que el operador automático esté vinculado con el plan de marcado habilitado para la grabación de mensajes de TUI.

2.  Llame a un número de teléfono que haya configurado en el operador automático de mensajería unificada.

3.  Mientras se reproduce el saludo en horario comercial o no comercial para el operador automático, pulse la tecla almohadilla (\#) y después pulse asterisco (\*).

4.  Se le pedirá que introduzca el número de extensión del usuario. Escriba el número de extensión del usuario habilitado para mensajería unificada que tenga permiso para realizar la grabación de mensajes de TUI.

5.  Se le solicitará un PIN. Especifique el PIN del usuario.

6.  Siga los mensajes del sistema para editar o actualizar el saludo o anuncio informativo para el operador automático.

## Realizar la grabación de mensajes de Interfaz de usuario de teléfono (TUI) en un plan de marcado de mensajería unificada

1.  Llame a un número de Acceso de voz de Outlook que use para iniciar sesión en Acceso de voz de Outlook.

2.  Mientras se reproduce el saludo de bienvenida para el plan de marcado, pulse la tecla almohadilla (\#) y después el asterisco (\*).

3.  Si realiza la llamada desde un teléfono que esté usando un usuario habilitado para mensajería unificada, se le solicitará un PIN. En lugar de escribir el PIN, pulse asterisco (\*). Se le pedirá un número de extensión. Escriba el número de extensión del usuario habilitado para mensajería unificada que tenga permiso para realizar la grabación de mensajes de TUI.

4.  Si realiza la llamada desde un teléfono que no esté usando un usuario habilitado para mensajería unificada, se le solicitará automáticamente un número de extensión. Escriba el número de extensión del usuario habilitado para mensajería unificada que tenga permiso para realizar la grabación de mensajes de TUI.

5.  Se le solicitará un PIN. Especifique el PIN del usuario.

6.  Siga los mensajes del sistema para editar o actualizar el saludo de bienvenida para el plan de marcado o el anuncio informativo.

