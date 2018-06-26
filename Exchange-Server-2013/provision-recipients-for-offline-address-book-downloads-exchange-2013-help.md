---
title: 'Establecer destinatarios para descargas de la libreta de direcciones sin conexión: Exchange 2013 Help'
TOCTitle: Establecer destinatarios para descargas de la libreta de direcciones sin conexión
ms:assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996345(v=EXCHG.150)
ms:contentKeyID: 49895485
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Establecer destinatarios para descargas de la libreta de direcciones sin conexión

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2013-02-15_

Si usa varias libretas de direcciones sin conexión (OAB) en la organización, existen varias maneras de especificar qué destinatarios descargan qué libreta de direcciones sin conexión:

  - **Por base de datos de buzón**   Puede usar el EAC o el Shell para establecer destinatarios para descargas OAB al vincular una base de datos de buzones de correo a un OAB predeterminado para clientes de Office Outlook 2007, Outlook 2010 y de Outlook 2013.

  - **Por destinatario**   Puede usar el cmdlet **Set-Mailbox** en el Shell para especificar qué OAB se descarga al vincular la OAB directamente al buzón del destinatario.

  - **Por varios destinatarios **  Puede usar un comando canalizado en el Shell para especificar la OAB que descargan varios destinatarios sobre la base de atributos comunes.

  - **Por directiva de libreta de direcciones**   Puede asignar una directiva de libreta de direcciones (ABP) a la cuenta de usuario de un buzón para especificar qué OAB se descarga en el buzón de un destinatario. Si asigna una ABP a una cuenta de usuario que ya tiene una OAB asignada, la OAB que se asigne explícitamente al buzón tendrá prioridad. Para obtener más información, consulte [Asignar una directiva de libreta de direcciones a usuarios de correo](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las OABs, consulte [Procedimientos de libretas de direcciones sin conexión](offline-address-book-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - No puede usar el Centro de administración de Exchange (EAC) para hacer estas tareas. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Use el Shell para establecer destinatarios para descargas de OAB al vincular sus bases de datos de buzones de correo a una base de datos de carpetas públicas o a una OAB predeterminada

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Bases de datos de buzones" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

En este ejemplo, se establece la distribución basada en Web de Mi OAB para la base de datos de buzones de correo predeterminada.

    Set-MailboxDatabase -Identity "Mailbox Database" -OfflineAddressBook "My OAB"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)).

## Usar el Shell para especificar qué OAB se descargará al vincular la OAB directamente al buzón del destinatario

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

Para especificar qué OAB se descarga al vincular la OAB directamente al buzón del destinatario, use la sintaxis siguiente.

    Set-Mailbox -Identity <MailboxIDParameter> -OfflineAddressBook <OfflineAddressBookIdParameter>


> [!NOTE]
> El parámetro <EM>Identity</EM> identifica el buzón y puede tener los valores siguientes: GUID, ADObjectID, nombre completo (DN), <EM>domain\account</EM>, nombre principal de usuario (UPN), LegacyExchangeDN, dirección Smtp y alias.



En este ejemplo, se especifica que el usuario José Ignacio descargará la OAB denominada Mi OAB.

    Set-Mailbox -Identity Kim -OfflineAddressBook "My OAB"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## Usar el Shell para especificar la OAB que descargarán varios destinatarios

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

En este ejemplo, se especifica que todos los buzones de usuario en Estados Unidos de Contoso descargan la OAB Contoso Estados Unidos.

    Get-User -ResultSize Unlimited -Filter { Company -eq "Contoso" -and RecipientType -eq "UserMailbox" } | Where { $_.CountryOrRegion -eq "United States"} | Set-Mailbox -OfflineAddressBook "Contoso United States"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-User](https://technet.microsoft.com/es-es/library/aa996896\(v=exchg.150\)) y [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

