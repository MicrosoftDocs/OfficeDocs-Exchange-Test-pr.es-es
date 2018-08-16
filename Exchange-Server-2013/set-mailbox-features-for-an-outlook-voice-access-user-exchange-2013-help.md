---
title: 'Conjunto características buzón usuario Outlook Voice Access Exchange 2013 Help'
TOCTitle: Conjunto de características de buzón para un usuario de Outlook Voice Access
ms:assetid: a56bfd75-7bc5-49b9-b098-06855a720dcd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124030(v=EXCHG.150)
ms:contentKeyID: 50556834
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conjunto de características de buzón para un usuario de Outlook Voice Access

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

La configuración de la interfaz de usuario de teléfono se utiliza cuando un usuario obtiene acceso al sistema de mensajería unificada mediante Outlook Voice Access. Cuando se modifica una configuración de la interfaz de usuario de teléfono de un usuario habilitado para mensajería unificada, se modifican las propiedades y sus valores en el buzón del usuario habilitado para mensajería unificada.

Puede cambiar los siguientes parámetros de TUI para un usuario habilitado para mensajería unificada:

  - Permitir el acceso de suscriptores

  - Permitir a la interfaz de usuario de teléfono acceso al calendario

  - Permitir el acceso TUI al correo electrónico

  - Permitir el reconocimiento automático de voz

Para otras tareas de administración relacionadas con los usuarios de mensajería unificada, consulte [Conjunto de características de buzón para un usuario de Outlook Voice Access](set-mailbox-features-for-an-outlook-voice-access-user-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que el destinatario Exchange existente tenga habilitada la mensajería unificada y correo de voz. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Shell para modificar las opciones de configuración de la interfaz de usuario de teléfono de un solo usuario habilitado para mensajería unificada

En este ejemplo, se habilita el acceso al correo electrónico y al calendario mediante la interfaz de usuario de teléfono de un usuario habilitado para mensajería unificada llamado Tony Smith.

    Set-UMMailbox -Identity tony@contoso.com TUIAccessToCal True -TUIAccessToEmail True -OperatorNumber 111111 -DisableMissedCallNotification False -AnonCallBlock True


> [!NOTE]
> La configuración de la interfaz de usuario de teléfono para usuarios también está disponible para directivas de buzones de correo de mensajería unificada. La modificación de la configuración de TUI en una directiva de buzones de mensajería unificada afecta a todos los usuarios asociados con la directiva de buzones de mensajería unificada. Para obtener más información acerca de cómo modificar la configuración de la interfaz de usuario de teléfono en una directiva de buzones de correo de mensajería unificada, consulte <A href="set-mailbox-features-for-outlook-voice-access-users-exchange-2013-help.md">Establecer características de buzón de correo para los usuarios de Outlook Voice Access</A>.


