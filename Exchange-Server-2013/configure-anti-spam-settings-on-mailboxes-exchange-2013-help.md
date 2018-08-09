---
title: 'Establecer configuración filtro spam en buzones correo: Exchange 2013 Help'
TOCTitle: Establecer las configuraciones de filtro de correo no deseado en los buzones de correo
ms:assetid: 868d7fd8-e817-46ba-9b67-edf2f50b9494
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123559(v=EXCHG.150)
ms:contentKeyID: 49895752
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer las configuraciones de filtro de correo no deseado en los buzones de correo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-11-17_

Puede configurar unos parámetros específicos de filtro de correo no deseado en buzones de correo individuales que sean diferentes a los filtros de correo no deseado que se han aplicado al resto de buzones de la organización de Exchange. Al configurar los parámetros de filtro de correo no deseado de un buzón, dicha configuración sobrescribe la correspondiente configuración del filtrado del contenido de toda la organización y de la configuración de filtros de correo no deseado de la misma.


> [!NOTE]
> El 1 de noviembre de 2016 Microsoft detuvo las actualizaciones de definiciones de correo no deseado para los filtros de SmartScreen en Exchange y Outlook. Las definiciones existentes de correo no deseado de SmartScreen permanecerán en su lugar, pero es probable que su eficacia se degrade con el tiempo. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange</A> (Fin del soporte de SmartScreen en Outlook y Exchange).



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Características de los filtros de correo no deseado" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) y entrada "Filtros de correo no deseado" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - De manera predeterminada, las características contra correo no deseado no están habilitadas en el Servicio de transporte en un servidor de buzones. Por lo general, solo se habilitan las características contra correo no deseado si la organización de Exchange no realiza un filtrado previo contra correo no deseado antes de aceptar mensajes entrantes. Para obtener más información, consulte [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - El valor de umbral de SCL de la carpeta de correo no deseado se comporta de forma distinta a los valores de eliminación, rechazo y cuarentena de SCL. Para obtener más información, consulte [Umbral de nivel de confianza de correo no deseado](spam-confidence-level-threshold-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para configurar las funciones contra el correo electrónico no deseado en un solo buzón

Para configurar la configuración de los filtros de correo no deseado en un único buzón, use la siguiente sintaxis.

    Set-Mailbox <MailboxIdentity> -AntispamBypassEnabled <$true | $false> -RequireSenderAuthenticationEnabled <$true | $false> -SCLDeleteEnabled <$true | $false | $null> -SCLDeleteThreshold <0-9 | $null> -SCLJunkEnabled <$true | $false | $null > -SCLJunkThreshold <0-9 | $null> -SCLQuarantineEnabled <$true | $false | $null > -SCLQuarantineThreshold <0-9 | $null> -SCLRejectEnabled <$true | $false | $null > -SCLRejectThreshold <0-9 | $null>

En este ejemplo se configura el buzón de un usuario llamado Jeff Phillips para que omita todos los filtros de correo no deseado y tener mensajes que cumplan o superen un umbral de SCL de la carpeta de correo no deseado de 5 entregados a esta carpeta en Microsoft Outlook.

    Set-Mailbox "Jeff Phillips" -AntispamBypassEnabled $true -SCLJunkEnabled $true -SCLJunkThreshold 4

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha configurado las características de los filtros de correo no deseado correctamente en un único buzón, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-Mailbox <MailboxIdentity> | Format-List SCL*,Bypass*,*SenderAuth*

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Usar el Shell para configurar las características de filtros de correo no deseado en varios buzones

Para configurar todas las funciones de filtros de correo no deseado en varios buzones, utilice la siguiente sintaxis.

    Get-Mailbox [<Filter>]| Set-Mailbox <Anti-Spam Settings>

En este ejemplo, se habilita el umbral de cuarentena SCL con un valor de 7 en todos los buzones del contenedor de usuarios del dominio Contoso.com.

    Get-Mailbox -OrganizationalUnit Contoso.com/Users | Set-Mailbox -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha configurado las características de los filtros de correo no deseado correctamente en varios buzones, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-Mailbox [<Filter>] | Format-List Name,SCL*,*SenderAuth*

2.  Verifique que los valores mostrados son los valores que ha configurado.

## Utilizar el Shell para configurar el umbral de correo no deseado de todos los buzones de la organización

Ejecute el siguiente comando:

    Set-OrganizationConfig -SCLJunkThreshold <Integer>

En este ejemplo se establece un umbral de 5 para el correo no deseado de la organización.

    Set-OrganizationConfig -SCLJunkThreshold 5

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha configurado el umbral de correo no deseado correctamente en todos los buzones de la organización, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-OrganizationConfig | Format-List SCLJunkThreshold

2.  Verifique que el valor mostrado es el valor que ha configurado.

