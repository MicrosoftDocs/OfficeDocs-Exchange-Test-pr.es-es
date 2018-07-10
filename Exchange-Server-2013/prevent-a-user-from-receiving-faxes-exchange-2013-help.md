---
title: 'Evitar que un usuario reciba faxes: Exchange 2013 Help'
TOCTitle: Evitar que un usuario reciba faxes
ms:assetid: b5d022b9-043a-4324-87fb-074d5e2c2ca3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201722(v=EXCHG.150)
ms:contentKeyID: 52061929
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Evitar que un usuario reciba faxes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Evitar que un usuario de mensajería unificada (UM) de recibir faxes. Obtener información sobre cómo cambiar la configuración de fax para usuarios de mensajería UNIFICADA nuevos y existentes.

De forma predeterminada, cuando se habilita un usuario para mensajería unificada, podrán recibir faxes si habilita el envío de faxes y configurar URI de un socio de fax en la directiva de buzón de mensajería UNIFICADA está vinculada al usuario. Se puede habilitar el envío de faxes o deshabilitado en mensajería UNIFICADA marca los planes, las directivas de buzón de mensajería UNIFICADA o buzón del usuario habilitado para mensajería UNIFICADA.

De manera predeterminada, el buzón de correo del usuario y el plan de marcado vinculado al usuario permiten los faxes entrantes. Sin embargo, para que un usuario reciba faxes, antes se deben habilitar los faxes de entrada en la directiva de buzón de correo de mensajería unificada asociada con el usuario habilitado para mensajería unificada y especificar el URI del socio de fax.


> [!NOTE]
> El CEF sirve para configurar el fax en una directiva de buzón de mensajería unificada. Sin embargo, debe utilizar el Shell para configurar las opciones de fax en los planes de marcado o para usuarios individuales.



Para obtener más información acerca de los partners de fax, consulte [Microsoft PinPoint para asociados de negocios de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para otras tareas de administración relacionadas con los faxes, consulte [Procedimientos de envío de faxes](faxing-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que el usuario tiene habilitada la mensajería unificada. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para impedir que un usuario habilitado para UM reciba faxes

En este ejemplo, se evita que un usuario habilitado para Mensajería unificada llamado Tony reciba mensajes de fax en su buzón.

    Set-UMMailbox -Identity tony@contoso.com -FaxEnabled $false

