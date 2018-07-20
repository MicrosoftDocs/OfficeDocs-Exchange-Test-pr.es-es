---
title: 'Administrar el filtrado de destinatarios en servidores de transporte perimetral: Exchange 2013 Help'
TOCTitle: Administrar el filtrado de destinatarios en servidores de transporte perimetral
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 49896011
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar el filtrado de destinatarios en servidores de transporte perimetral

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

El agente de filtrado de destinatarios proporciona la capacidad de filtrado de destinatarios. Cuando el filtrado de destinatarios está habilitado en un servidor de Exchange, filtra los mensajes entrantes que provienen de Internet pero que no están autenticados. Estos mensajes se consideran mensajes externos.


> [!NOTE]
> Aunque el agente de filtrado de destinatarios está disponible en los servidores de buzones de correo, no debe configurarlo. Cuando el filtrado de destinatarios en un servidor de buzones de correo detecta un destinatario bloqueado o no válido en un mensaje que incluye otros destinatarios válidos, el mensaje se rechaza. Si instala agentes contra el correo no deseado en un servidor de buzones de correo, el agente de filtrado de destinatarios se habilita de manera predeterminada. Sin embargo, no está configurado para bloquear ningún destinatario. Para más información, vea <A href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo</A>.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones contra el correo no deseado" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - De manera predeterminada, las características contra correo no deseado no están habilitadas en el Servicio de transporte en un servidor de buzones. Por lo general, solo se habilitan las características contra correo no deseado si la organización de Exchange no realiza un filtrado previo contra correo no deseado antes de aceptar mensajes entrantes. Para obtener más información, consulte [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - El parámetro *AddressBookEnabled* del cmdlet **Set-AcceptedDomain** habilita o deshabilita el filtrado de destinatarios en un dominio aceptado. De manera predeterminada, el filtrado de destinatarios está habilitado para dominios autorizados y deshabilitado para dominios de retransmisión internos y dominios de retransmisión externos. Para ver el estado del parámetro *AddressBookEnabled* para los dominios aceptados en su organización, ejecute el siguiente comando:
    
        Get-AcceptedDomain | Format-List Name,AddressBookEnabled

  - Si deshabilita el filtrado de destinatarios mediante el procedimiento descrito en este tema, se deshabilitará la funcionalidad de filtrado de destinatarios, pero el agente de filtrado de destinatarios subyacente permanecerá habilitado.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para habilitar o deshabilitar el filtrado de destinatarios

Para deshabilitar el filtrado de destinatarios, ejecute el comando siguiente:

    Set-RecipientFilterConfig -Enabled $false

Para habilitar el filtrado de destinatarios, ejecute el comando siguiente:

    Set-RecipientFilterConfig -Enabled $true


> [!NOTE]
> Al deshabilitar el filtrado de destinatarios, el agente de filtrado de destinatarios subyacente aún está habilitado. Para deshabilitar el agente de filtrado de destinatarios, ejecute el siguiente comando: <CODE>Disable-TransportAgent "Recipient Filter Agent"</CODE>.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el filtrado de destinatarios se habilitó o deshabilitó correctamente, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-RecipientFilterConfig | Format-List Enabled

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Usar el Shell para habilitar o deshabilitar la lista de destinatarios bloqueados

Ejecute el siguiente comando:

    Set-RecipientFilterConfig -BlockListEnabled <$true | $false>

En este ejemplo, se habilita la lista de destinatarios bloqueados:

    Set-RecipientFilterConfig -BlockListEnabled $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la lista de destinatarios bloqueados se habilitó o deshabilitó correctamente, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-RecipientFilterConfig | Format-List BlockListEnabled

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Usar el Shell para configurar la lista de destinatarios bloqueados

Para reemplazar los valores existentes, ejecute el siguiente comando:

    Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>

En este ejemplo, se configura la lista de destinatarios bloqueados con los valores mark@contoso.com y kim@contoso.com:

    Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com

Para agregar o quitar entradas sin modificar valores existentes, ejecute el siguiente comando:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

En este ejemplo, se agrega chris@contoso.com a la lista de destinatarios y se quita michelle@contoso.com de la lista de destinatarios bloqueados:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la lista de destinatarios bloqueados se configuró correctamente, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-RecipientFilterConfig | Format-List BlockedRecipients

2.  Verifique que los valores mostrados son los valores que ha configurado.

## Usar el Shell para habilitar o deshabilitar la búsqueda de destinatarios

Ejecute el siguiente comando:

    Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>

Para bloquear mensajes dirigidos a destinatarios que no existen en la organización, ejecute el comando siguiente:

    Set-RecipientFilterConfig -RecipientValidationEnabled $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la búsqueda de destinatarios se habilitó o deshabilitó correctamente, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-RecipientFilterConfig | Format-List RecipientValidationEnabled

2.  Verifique que el valor mostrado es el valor que ha configurado.

