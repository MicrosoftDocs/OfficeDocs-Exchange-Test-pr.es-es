---
title: 'Habilitar o deshabilitar la recuperación de elementos individuales de un buzón de correo: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar la recuperación de elementos individuales de un buzón de correo
ms:assetid: 2e7f1bcd-8395-45ad-86ce-22868bd46af0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633460(v=EXCHG.150)
ms:contentKeyID: 54652407
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar la recuperación de elementos individuales de un buzón de correo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-13_

Para habilitar o deshabilitar la recuperación de un elemento único en un buzón, puede usar el Shell. En Exchange Online, la recuperación de un elemento único está habilitada de forma predeterminada, cuando se crea un nuevo buzón. En Exchange 2013, la recuperación de un elemento único se deshabilita cuando se crea un buzón. Si la recuperación de un elemento único está habilitada, los mensajes que el usuario elimina (purga) permanentemente se conservan en la carpeta Elementos recuperables del buzón hasta que expira el período de retención de elementos eliminados. Esto permite al administrador recuperar los mensajes purgados por el usuario antes de que expire el período de retención de elementos eliminados. Además, si un usuario o un proceso modifican un mensaje, también se conservan copias del elemento original cuando se habilita la recuperación de un elemento único.

## ¿Qué necesito saber antes de empezar?

  - Tiempo estimado para finalizar: 2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Retenciones y retenciones legales" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - El Centro de administración de Exchange (EAC) no se puede usar para habilitar o deshabilitar la recuperación de un elemento único.

  - De manera predeterminada, este período es de 14 días en Exchange Online. El valor de esta configuración se puede ampliar a un máximo de 30 días. Para obtener información más detallada, consulte [Cambiar el tiempo que se conservan los elementos eliminados permanentemente para un buzón de correo de Exchange Online](https://technet.microsoft.com/es-es/library/dn163584\(v=exchg.150\))

  - De forma predeterminada, en Exchange 2013, el buzón usa la configuración de retención de elementos eliminados correspondiente a la base de datos de buzones. El período de retención de elementos eliminados de una base de datos de buzones de correo está establecido en 14 días, pero este valor se puede cambiar definiendo esta configuración por separado en cada buzón. Para información detallada, vea [Configurar la retención de elementos eliminados y las cuotas de elementos recuperables](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Usar el Shell para habilitar la recuperación de un elemento único

En este ejemplo se habilita la recuperación de un elemento único en el buzón de April Summers.

    Set-Mailbox -Identity "April Summers" -SingleItemRecoveryEnabled $true

En este otro ejemplo se habilita la recuperación de un elemento único en el buzón de Pilar Pinilla y se establece que los elementos eliminados se conserven durante 30 días.

    Set-Mailbox -Identity "Pilar Pinilla" -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

Por último, en este ejemplo se habilita la recuperación de un elemento único en todos los buzones de usuario de la organización.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true

En este otro ejemplo se habilita la recuperación de un elemento único en todos los buzones de la organización y se establece que los elementos eliminados se conserven durante 30 días.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

Para información detallada sobre la sintaxis y los parámetros, vea [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## Usar el Shell para deshabilitar la recuperación de elementos individuales

Quizás tenga que deshabilitar la recuperación de elementos individuales en un buzón de usuario. Por ejemplo, antes de poder usar **Search-Mailbox – DeleteContent** para eliminar permanentemente el contenido de un buzón, tiene que deshabilitar la recuperación de elementos individuales. Para obtener más información, consulte [Buscar y eliminar mensajes: Ayuda para administradores](search-for-and-delete-messages-admin-help-exchange-2013-help.md).

En este ejemplo se deshabilita la recuperación de elementos individuales en el buzón de Ayla Kol.

    Set-Mailbox -Identity "Ayla Kol" -SingleItemRecoveryEnabled $false

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si la recuperación de un elemento único se ha habilitado en un buzón y ver durante cuántos días se conservarán los elementos eliminados, ejecute el comando siguiente.

    Get-Mailbox <Name> | FL SingleItemRecoveryEnabled,RetainDeletedItemsFor

Puede utilizar este mismo comando para comprobar que la recuperación de elementos individuales de un buzón está deshabilitada.

## Más información

  - Para más información sobre la recuperación de un elemento único, vea [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md). Para recuperar mensajes purgados por el usuario antes de que expire el período de retención de elementos eliminados, consulte [Recuperar mensajes eliminados en el buzón de un usuario](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md).

  - Si un buzón se coloca en conservación local o retención por juicio, los mensajes en la carpeta Elementos recuperables se conservan hasta que expire la duración de retención. Si la duración de retención es ilimitada, los elementos se conservan hasta que la retención se quita o se cambia la duración de retención.

