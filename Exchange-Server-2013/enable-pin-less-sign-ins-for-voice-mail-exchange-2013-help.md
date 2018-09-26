---
title: 'Habilitar inicios de sesión sin PIN para correo de voz: Exchange 2013 Help'
TOCTitle: Habilitar inicios de sesión sin PIN para correo de voz
ms:assetid: 54133753-317c-42ef-9b0d-ca9f2d2d6bd7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg602127(v=EXCHG.150)
ms:contentKeyID: 54652436
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar inicios de sesión sin PIN para correo de voz

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-04-08_

Puede configurar la mensajería unificada (UM) para que los usuarios puedan iniciar sesión en el correo de voz sin usar un PIN. De manera predeterminada, se les solicita a los usuarios de Outlook Voice Access que escriban un PIN para iniciar sesión y obtener acceso a sus buzones de correo, correos electrónicos, calendario y contactos personales, el directorio y opciones personales.


> [!WARNING]
> Habilitar inicios de sesión sin PIN para un solo usuario o un grupo de usuarios habilitados para correo de voz reduce el nivel de seguridad para correo de voz y representa un riesgo para la seguridad de la organización.



Para habilitar inicios de sesión sin PIN, debe configurar el parámetro *AllowPinlessVoiceMailAccess* en `$true` en la directiva de buzón de mensajería unificada (UM) y configurar el parámetro *PinlessAccessToVoiceMailEnabled* en `$true` en el buzón de mensajería unificada (UM). De forma predeterminada, ambos parámetros se configuran en `$false`, lo que requiere que un usuario de Outlook Voice Access escriba el PIN al obtener acceso al correo de voz.

La configuración de ambos parámetros en `$true` le permite habilitar inicios de sesión sin PIN para el correo de voz de un gran grupo de usuarios asociados con un buzón de mensajería unificada (UM) y también habilitar inicios de sesión sin PIN para un único buzón de mensajería unificada (UM) o para un subconjunto de buzones de mensajería unificada (UM). Aun si habilita inicios de sesión sin PIN para el correo de voz de un grupo de usuarios habilitados para mensajería unificada (UM) o de un único usuario habilitado para mensajería unificada (UM), cuando obtengan acceso al correo electrónico, el calendario, los contactos personales, el directorio u opciones personales, se les solicitará que escriban el PIN.

Para habilitar inicios de sesión sin PIN para el correo de voz de un usuario, se deben cumplir las siguientes condiciones:

  - Debe haber ejecutado el cmdlet siguiente sobre la directiva de buzón de mensajería unificada (UM): `Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true`

  - Debe tener el siguiente cmdlet en el buzón del usuario habilitado para mensajería unificada (UM): `Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true`

  - El usuario habilitado para mensajería unificada (UM) está asociado con la misma directiva de mensajería unificada (UM) para la que habilitó los inicios de sesión sin PIN.

  - El usuario habilitado para MU marca en Outlook Voice Access desde un número de teléfono que le ha sido asignado.

  - Solo puede usar el Shell para realizar este procedimiento. Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)). Para obtener información sobre cómo usar Windows PowerShell para conectarse a Exchange Online, vea [Conexión a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

Para consultar otras tareas relacionadas con las directivas de buzones de mensajería unificada, vea [Procedimientos de políticas de buzón de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policy-procedures).

Para tareas adicionales relacionadas con buzones de mensajería unificada (UM), consulte [Procedimientos de usuario habilitado para correo de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy).

  - Antes de realizar estos procedimientos, confirme que el usuario o los usuarios estén habilitados para mensajería unificada (UM) y correo de voz. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).

## ¿Qué desea hacer?

## Usar el Shell para habilitar el acceso sin PIN al correo de voz para usuarios habilitados para MU en una directiva de buzón de MU

Este ejemplo permite el acceso al correo de voz sin PIN en una directiva de buzón de mensajería unificada (UM) denominada `MyUMMailboxPolicy` para usuarios asociados con la directiva de buzón que marcan en Outlook Voice Access.

```powershell
Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true
```

## Usar el Shell para habilitar el acceso sin PIN al correo de voz en un buzón de usuario habilitado para MU

Este ejemplo habilita el acceso para correo de voz sin PIN para el usuario que marca en Outlook Voice Access para llegar al buzón denominado `tonys@contoso.com`.

```powershell
Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true
```

