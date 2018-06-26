---
title: 'Administrar mensajes de DSN: Exchange 2013 Help'
TOCTitle: Administrar mensajes de DSN
ms:assetid: 23c9d844-6fc7-44c9-a308-587338281611
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996803(v=EXCHG.150)
ms:contentKeyID: 49895521
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- cambiar mensaje del sistema
- cambiar mensaje de rechazo
- cambiar mensaje de cuota
- cambiar mensaje de NDR
ms.translationtype: HT
---

# Administrar mensajes de DSN

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2013-02-20_

Microsoft Exchange Server 2013 usa notificaciones del estado de entrega (DSN) para proporcionar informes de no entrega (NDRs) y otros mensajes de estado a los remitentes de mensajes. Puede usar los DSN integrados, o puede crear mensajes DSN personalizados para adaptarse a las necesidades de su organización.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "DSN" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - No se puede quitar un mensaje de DSN integrado incluido con Exchange. Para cambiar un mensaje de DSN integrado, debe crear un nuevo mensaje de DSN personalizado para el código de DSN que desee personalizar. Cuando quita un mensaje de DSN personalizado, el código de DSN que está asociado a ese mensaje vuelve al mensaje de DSN original incluido en Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para ver los mensajes DSN integrados y personalizados

Para ver una listas resumen de todos los mensajes DSN integrados con Exchange 2013, ejecute el siguiente comando:

    Get-SystemMessage -Original

Para ver una listas resumen de todos los mensajes DSN personalizados en su organización, ejecute el siguiente comando:

    Get-SystemMessage

Para ver información detallada para la personalización de mensajes de DSN para el código de DSN 5.1.2 que se envía a los remitentes internos en inglés, ejecute el siguiente comando:

    Get-SystemMessage En\Internal\5.1.2 | Format-List

## Usar el Shell para crear un mensaje personalizado de DSN

Ejecute el siguiente comando:

    New-SystemMessage -Internal <$true | $false> -Language <Locale> -DSNCode <x.y.z> -Text "<DSN text>"

Este ejemplo crea un mensaje DSN de texto sin formato DSN personalizado para el código de DNS 5.1.2 que se envía a los remitentes internos en inglés.

    New-SystemMessage -Internal $true -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

Este ejemplo crea un mensaje DSN de texto sin formato DSN personalizado para el código de DNS 5.1.2 que se envía a los remitentes externos en inglés.

    New-SystemMessage -Internal $false -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact your System Administrator for more information."

Este ejemplo crea un mensaje DSN HTML personalizado para el código de DNS 5.1.2 que se envía a los remitentes internos en inglés.

    New-SystemMessage -DSNCode 5.1.2 -Internal $true -Language En -Text 'You tried to send a message to a <B>disabled</B> mailbox. Please visit <A HREF="http://it.contoso.com">Internal Support</A> or contact &quot;InfoSec&quot; for more information.'

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar si ha creado correctamente un mensaje de DNS personalizado, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SystemMessge -DSNCode <x.y.z> | Format-List Name,Internal,Text,Language

2.  Compruebe que los valores que ve son los valores que ha configurado.

3.  Enviar un mensaje de prueba que generará el DSN personalizado que haya configurado.

## Uso del Shell para cambiar el texto de un mensaje de DSN personalizado

Para cambiar el texto de un mensaje de DSN personalizado use el siguiente comando:

    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> -Text "<DSN text>"

Este ejemplo cambia el texto asignado al mensaje de DSN personalizado para el código de DNS 5.1.2 que se envía a los remitentes internos en inglés.

    Set-SystemMessage En\Internal\5.1.2 -Text "The mailbox you tried to send an e-mail message to is disabled and is no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

## ¿Cómo saber si el proceso se ha completado correctamente?

Par comprobar si ha cambiado correctamente el texto de un mensaje de DNS personalizado, haga lo siguiente:

1.  Ejecute el siguiente comando: `Get-SystemMessage`.
    
        Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> | Format-List -Text

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Usar el Shell para quitar un mensaje personalizado de DSN

Ejecute el siguiente comando:

    Remove-SystemMessage <Local>\<Internal | External>\<DSNcode>

Este ejemplo quita el mensaje DSN personalizado para el código de DNS 5.1.2 que se envía a los remitentes internos en inglés.

    Remove-SystemMessage En\Internal\5.1.2

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha quitado correctamente un mensaje de DNS personalizado, haga lo siguiente:

1.  Ejecute el comando: `Get-SystemMessage`.

2.  Compruebe un DSN para la configuración regional, los destinatarios internos o externos y que el código de DSN eliminado no aparezca.

## Enviar copias de mensajes DSN al buzón de correo de destinatarios de Exchange

Puede especificar una lista de códigos de DSN que desee supervisar copiando los mensajes de DSN al buzón de correo del destinatario de Exchange. Sin embargo, de forma predeterminada, no se asigna ningún destinatario de Exchange, para que todos los mensajes que se envíen al destinatario de Exchange se descarten. Para enviar copias de mensajes de DSN al buzón de correo de destinatarios de Exchange, debe asignar un buzón de correo al destinatario de Exchange y, a continuación, especificar los códigos de DSN que desee supervisar. De manera predeterminada, los siguientes códigos DSN se controlan: `5.4.8`, `5.4.6`, `5.4.4`, `5.2.4`, `5.2.0` y `5.1.4`.

## Paso 1: Usar el Shell para asignar un buzón de correo a los destinatarios de Exchange

Para asignar un buzón de correo a los destinatarios de Exchange, realice los pasos siguientes:

1.  Debido al alto volumen potencial de correo electrónico, plantéese la creación de un buzón de correo y una cuenta de usuario de Active Directory para el destinatario de Exchange. Para obtener más información, consulte [Crear buzones de usuario](create-user-mailboxes-exchange-2013-help.md). De lo contrario, identifique el buzón de correo existente que desee asociar con el destinatario de Exchange.

2.  Ejecute el siguiente comando:
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient <MailboxIdentity>
    
    Por ejemplo, para asignar el buzón existente denominado "Buzón de correo del sistema Contoso" al destinatario de Exchange, hay que ejecutar el siguiente comando:
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient "Contoso System Mailbox"

## Paso 2: Especificar los códigos de DSN que desea supervisar

## Utilice el EAC para especificar los códigos de DSN

1.  En el EAC, vaya a **Flujo de correo** \> **Conectores de recepción** \> **Más opciones** ![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") \> **Configuración de transporte de la organización** \> **Entrega**.

2.  En la sección **Códigos de DNS**, escriba los códigos de DSN que desee supervisar con el formato *\<x.y.z\>* y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Seleccione una entrada existente y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para modificarla, o haga clic en**Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") para eliminarla. Cuando haya terminado, haga clic en **Guardar**.

## Usar el Shell para especificar los códigos de DSN

Para reemplazar los valores existentes, ejecute el siguiente comando:

    Set-TransportConfig -GenerateCopyOfDSNFor <x.y.z>,<x.y.z>...

En este ejemplo se configura la organización de Exchange para reenviar todos los mensajes de DSN que tengan los códigos de DSN 5.7.1, 5.7.2 y 5.7.3 al destinatario de Exchange.

    Set-TransportConfig -GenerateCopyOfDSNFor 5.7.1,5.7.2,5.7.3

Para agregar o quitar entradas sin modificar valores existentes, ejecute el siguiente comando:

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="<x.y.z>","<x.y.z>"...; Remove="<x.y.z>","<x.y.z>"...}

Este ejemplo agrega el código de DSN 5.7.5 y quita el código de DSN 5.7.1 de la lista existente de mensajes de DSN que se envían a cada destinatario de Exchange.

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="5.7.5"; Remove="5.7.1"}

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya configurado las copias de los mensajes de DNS correctamente que se deben enviar al buzón de correo del destinatario de Exchange, supervise el buzón de correo que esté asociado con el destinatario de Exchange, y compruebe que los mensajes de DSN contengan el código de DSN especificado.

