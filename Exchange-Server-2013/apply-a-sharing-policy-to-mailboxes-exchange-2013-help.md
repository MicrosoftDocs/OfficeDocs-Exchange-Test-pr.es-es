---
title: 'Aplicar una directiva de uso compartida a los buzones: Exchange 2013 Help'
TOCTitle: Aplicar una directiva de uso compartida a los buzones
ms:assetid: dd4cc765-8469-4176-bb6e-d5b0f5235927
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657501(v=EXCHG.150)
ms:contentKeyID: 49895960
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aplicar una directiva de uso compartida a los buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-15_

Sharing policies are a part of federated sharing and enable user-established, people-to-people sharing of calendar information with different types of external users. The sharing policy that an admin applies to the user’s mailbox determines what level of access a user can share and with whom. If you don’t change anything, then the default sharing policy applies to all users. If you create a new sharing policy, you have to apply that policy to mailboxes before it takes effect. A sharing policy can be applied to a single user mailbox or to multiple user mailboxes simultaneously. An admin can also disable a user’s sharing policy to prevent external access to calendars.

To learn more about federated sharing, see [Uso compartido](sharing-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el *Recipient Provisioning Permissions* entry in the [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md) topic.

  - A sharing policy must exist. For details, see [Crear una directiva de uso compartido](create-a-sharing-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## What do you want to do?

## Use the EAC to apply a sharing policy to a single mailbox

1.  Navigate to **recipients** \> **mailboxes**.

2.  In the list view, select the mailbox you want, and then click **Edit**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  In **User Mailbox**, click **mailbox features**.

4.  In the **Sharing policy** list, select the sharing policy you want to apply to this mailbox.

5.  Click **save** to apply the sharing policy.

## Use the EAC to apply a sharing policy to multiple mailboxes

1.  Navigate to **recipients** \> **mailboxes**.

2.  In the list view, hold the Ctrl key while you select multiple mailboxes..

3.  In the details pane, the mailbox properties will be configured for bulk editing. Click **More options**.

4.  Under **Sharing policy**, click **Update**.

5.  In **bulk assign sharing policy**, use the **Select the sharing policy** list to select a sharing policy to assign to the mailboxes.

6.  Click **save** to apply the sharing policy to the selected mailboxes.

## Use the Shell to apply a sharing policy to one or more mailboxes

This example applies the sharing policy Contoso to a single mailbox for the user Barbara.

```powershell
Set-Mailbox -Identity Barbara -SharingPolicy "Contoso"
```

This example specifies that all user mailboxes in the Marketing department use the sharing policy Contoso Marketing.

```powershell
Get-Mailbox -Filter {Department -eq "Marketing"} | Set-Mailbox -SharingPolicy "Contoso Marketing"
```

This example returns all mailboxes that have the sharing policy Contoso applied, and it sorts the users into a table that displays only their aliases and email addresses.

```powershell
Get-Mailbox -ResultSize unlimited | Where {$_.SharingPolicy -eq "Contoso" } | format-table Alias, EmailAddresses
```

For detailed syntax and parameter information, see [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) and [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)).

## How do you know this worked?

To verify that you have successfully applied the sharing policy to a user mailbox, do one of the following:

  - In the EAC, navigate to **Recipients** \> **Mailboxes**, and then select the mailbox to which you applied the sharing policy. Click **Edit**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"), click **mailbox features**, and then confirm that the correct sharing policy appears in the **Sharing policy** list.

  - Run the following Shell command to verify the sharing policy was assigned to a user mailbox. Verify that the correct sharing policy is listed in the *SharingPolicy* parameter.
    
    ```powershell
    Get-Mailbox <user name> | format-list
    ```


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


