---
title: 'Importar y exportar saludos personalizados, anuncios, menús y avisos: Exchange 2013 Help'
TOCTitle: Importar y exportar saludos personalizados, anuncios, menús y avisos
ms:assetid: e82da5d5-625f-4d8b-8d31-ac45513aacfd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee681667(v=EXCHG.150)
ms:contentKeyID: 54652459
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Importar y exportar saludos personalizados, anuncios, menús y avisos

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-04-08_

Puede importar y exportar los archivos de audio que haya grabado para utilizarlos en planes de marcado y operadores automáticos de la mensajería unificada (UM). Por ejemplo, si actualiza desde una versión anterior de Exchange, puede que quiera exportar y guardar una copia de un archivo de audio. O puede que deba importar una copia de un mensaje de audio grabado antes de configurar el plan de marcado o el operador automático.

Los archivos de audio se utilizan para los siguientes fines:

  - En los planes de marcado de mensajería unificada, los archivos de audio se utilizan para saludos de bienvenida y anuncios informativos personalizados. Se reproducen cuando los usuarios de Outlook Voice Access llaman a un número de Outlook Voice Access.

  - En los operadores automáticos de mensajería unificada, los archivos de audio se utilizan para saludos utilizados para horarios comerciales y no comerciales, anuncios informativos, mensajes de menú y menús de navegación personalizados. Se reproducen cuando los usuarios llaman a un operador automático de mensajería unificada.

Los formatos de archivo de audio siguientes son compatibles para saludos, anuncios, menús y mensajes personalizados:

  - Archivos .wma codificados con Windows Media Audio 9.2 - 96 kbps/44 kHz/CBR de 1 paso estéreo (Grabadora de sonidos de Windows)

  - Archivos Windows Media Audio Voice 9 - 8 kbps/8 kHz/mono y archivos .wav codificados con el códec de audio PCM lineal (16 bits/muestra), 8 kilohercios (kHz)

Los archivos de audio que los planes de marcado y los operadores automáticos de mensajería unificada utilizan se importan en el buzón del sistema llamado {e0dc1c29-89c3-4034-b678-e6c29d823ed9} y se exportan desde este buzón del sistema. Los archivos de audio se pueden importar y exportar mediante los cmdlets **Import-UMPrompt** y **Export-UMPrompt**.

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entradas “Planes de marcado de mensajería unificada” y “Operadores automáticos de mensajería unificada” del tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para importar saludos, anuncios, menús y mensajes personalizados para los planes de marcado y los operadores automáticos de mensajería unificada

En este ejemplo se importa el archivo con el saludo de bienvenida llamado welcomegreeting.wav desde d:\\UMPrompts al plan de marcado de mensajería unificada `MyUMDialPlan`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

En este ejemplo se importa el archivo con el saludo de bienvenida llamado welcomegreeting.wav desde d:\\UMPrompts al operador automático de mensajería unificada `MyUMAutoAttendant`.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

## Usar el Shell para exportar saludos, anuncios, menús y mensajes personalizados para los planes de marcado y los operadores automáticos de mensajería unificada

En este ejemplo se exporta el saludo de bienvenida para el plan de marcado de mensajería unificada `MyUMDialPlan` y se guarda como un archivo llamado welcomegreeting.wav.

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav�? -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

En este ejemplo se exporta el saludo de bienvenida en horario comercial para el operador automático de mensajería unificada `MYUMAutoAttendant` y se guarda como un archivo llamado BusinessHoursWelcomeGreeting.wav.

    $prompt = Export-UMPrompt -BusinessHoursWelcomeGreeting -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "d:\UMPrompts\BusinessHoursWelcomeGreeting.wav" -Value $prompt.AudioData -Encoding Byte

