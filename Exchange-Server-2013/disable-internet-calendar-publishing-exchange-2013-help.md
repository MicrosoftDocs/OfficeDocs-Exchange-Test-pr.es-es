---
title: 'Deshabilitar la publicación de calendarios de Internet: Exchange 2013 Help'
TOCTitle: Deshabilitar la publicación de calendarios de Internet
ms:assetid: f26dbf04-9dae-460f-a987-2ad3dfbc7b7e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ853047(v=EXCHG.150)
ms:contentKeyID: 50556909
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar la publicación de calendarios de Internet

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-15_

How you disable Internet calendar publishing depends on how you enabled it. If you created a sharing policy dedicated to Internet calendar publishing, you can either disable the policy or delete it altogether. If you configured Internet calendar publishing as a sharing rule in the default sharing policy, you can just remove the sharing rule for the **Anonymous** domain.

When you disable Internet calendar publishing, users who are provisioned to use the sharing policy won't be able to share calendar information with the **Anonymous** Internet domain specified in the policy. However, you can’t delete or disable a sharing policy that’s dedicated to Internet calendar publishing until all users who are provisioned to use that policy have the policy setting removed from their mailboxes. For details about changing the sharing policy setting for a user, see [Administrar los buzones de usuario](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/include-text-with-email-sent-when-voicemail-is-enabled).


> [!NOTE]
> If you disable or delete a sharing policy, users provisioned to use the policy will continue to share information until the Sharing Policy Assistant runs. To specify how often the Sharing Policy Assistant runs, use the <A href="https://technet.microsoft.com/es-es/library/aa998651(v=exchg.150)">Set-MailboxServer</A> cmdlet with the <EM>SharingPolicySchedule</EM> parameter.



To fully disable Internet calendar publishing, you should also disable the Outlook Web App virtual directory used for calendar publishing. Doing this prohibits access to the published calendar links previously shared by your Exchange organization users with external Internet users. This step is detailed later in this topic.

To learn more about Internet calendar publishing and sharing policies, see [Uso compartido](sharing-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete this task: 15 minutes.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Calendar and Sharing Permissions" entry in the [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md) topic.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## How do you do this?

## Step 1: Use the EAC or the Shell to disable or delete the sharing policy for Internet calendar publishing

## Use the EAC

1.  Navigate to **Organization** \> **Sharing**.

2.  In the list view, under **Individual Sharing**, perform one of the following steps:
    
      - If you created a sharing policy specifically for Internet calendar publishing, select that policy, and then either clear the check box in the **On** column to disable the sharing policy or click **Delete**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono") to delete it.
    
      - If you configured Internet calendar publishing as a sharing rule in the default sharing policy, perform the following steps:
        
        1.  Select the default sharing policy, and then click **Edit**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
        
        2.  In **sharing policy**, select the **Anonymous** sharing rule, and then click **Remove**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") to remove the sharing rule.
        
        3.  Click **Save**.

## Use the Shell

This example disables a dedicated Internet calendar publishing sharing policy named **Internet**.

```powershell
Set-SharingPolicy -Identity "Internet" -Enabled $false
```

This example deletes a dedicated Internet calendar publishing sharing policy named **Internet**.

```powershell
Remove-SharingPolicy -Identity "Internet"
```

For detailed syntax and parameter information, see [Set-SharingPolicy](https://technet.microsoft.com/es-es/library/dd297931\(v=exchg.150\)).

## How do you know this step worked?

To verify that you have successfully removed or updated the sharing policy, run the following Shell command and verify the sharing policy information.

```powershell
Get-SharingPolicy <policy name> | format-list
```

If you’ve removed the dedicated Internet calendar publishing sharing policy, you won’t see the policy in the cmdlet results.

If you’ve updated the default sharing policy, verify that the `Anonymous` domain has been removed from the *Domains* parameter.

For detailed syntax and parameter information, see [Get-SharingPolicy](https://technet.microsoft.com/es-es/library/dd335081\(v=exchg.150\)).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Step 2: Use the Shell to disable the Outlook Web App virtual directory Anonymous features


> [!NOTE]
> You can't use the EAC to disable Anonymous features for the Outlook Web App virtual directory.



This example disables Anonymous features for the Outlook Web App virtual directory on Client Access server CAS01.

```powershell
Set-OwaVirtualDirectory -Identity "CAS01" - AnonymousFeaturesEnabled -$false
```

For detailed syntax and parameter information, see [Set-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/bb123515\(v=exchg.150\)).

## How do you know this step worked?

To verify that you have successfully disabled the Anonymous features for the Outlook Web App virtual directory on the Client Access server, run the following Shell command and verify that the *AnonymousFeaturesEnabled* parameter is `$false`.

```powershell
Get-OwaVirtualDirectory | format-list
```

For detailed syntax and parameter information, see [Get-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/aa998588\(v=exchg.150\)).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


