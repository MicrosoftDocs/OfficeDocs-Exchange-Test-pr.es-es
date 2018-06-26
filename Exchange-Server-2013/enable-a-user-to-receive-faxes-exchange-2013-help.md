---
title: 'Habilitar un usuario recibir faxes: Exchange 2013 Help'
TOCTitle: Habilitar un usuario recibir faxes
ms:assetid: a0505001-aac0-41ef-824f-76e5e56d7675
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201712(v=EXCHG.150)
ms:contentKeyID: 52061857
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar un usuario recibir faxes

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Puede habilitar un usuario de mensajería unificada para que reciba faxes. De manera predeterminada, cuando habilite un usuario para la mensajería unificada, podrá recibir faxes si habilita los faxes y configura un URI del socio de fax en la directiva de buzón de correo de mensajería unificada enlazada al usuario. El envío de faxes se puede habilitar o deshabilitar en los planes de marcado y las directivas de buzón de mensajería unificada, o en el buzón de correo del usuario habilitado para mensajería unificada.

De manera predeterminada, el buzón de correo del usuario y el plan de marcado vinculado al usuario permiten los faxes entrantes. Sin embargo, para que un usuario reciba faxes, antes se deben habilitar los faxes de entrada en la directiva de buzón de correo de mensajería unificada asociada con el usuario habilitado para mensajería unificada y especificar el URI del socio de fax.


> [!NOTE]
> Puede usar el EAC para configurar los parámetros de fax en una directiva de buzón de correo de mensajería unificada. Sin embargo, debe usar el Shell para configurar los parámetros de fax en los planes de marcado de los usuarios individuales.



Para obtener más información acerca de los partners de fax, consulte [Microsoft PinPoint para asociados de negocios de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para otras tareas de administración relacionadas con los faxes, consulte [Procedimientos de envío de faxes](faxing-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que la directiva de buzón de correo de mensajería unificada asignada al usuario tiene los faxes habilitados y que el URI del socio de fax esté bien configurado.

  - Antes de realizar estos procedimientos, confirme que el usuario tenga habilitada la mensajería unificada. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Shell para permitir que un usuario de mensajería unificada reciba faxes

En este ejemplo, se habilita a Tony Smith para que reciba faxes entrantes.

    Set-UMMailbox -Identity tonysmith@contoso.com -FaxEnabled $true

