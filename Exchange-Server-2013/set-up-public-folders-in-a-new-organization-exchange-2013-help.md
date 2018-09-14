---
title: 'Configurar las carpetas públicas de una nueva organización: Exchange 2013 Help'
TOCTitle: Configurar las carpetas públicas de una nueva organización
ms:assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ651147(v=EXCHG.150)
ms:contentKeyID: 49895734
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar las carpetas públicas de una nueva organización

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-11-09_

**Resumen:**  Cómo configurar carpetas públicas, incluida la asignación de permisos en el Centro de admin. de Exchange.

This topic shows you how to get public folders configured and running in a new organization or in an organization that has never previously had public folders.


> [!NOTE]
> For more information about the storage quotas and limits for public folders, see the following topics: 
> <UL>
> <LI>
> <P>Para carpetas públicas de Office 365, vea <A href="https://go.microsoft.com/fwlink/?linkid=391188">Límites de Exchange Online</A>.</P>
> <LI>
> <P>For public folders in on-premises Exchange Server 2013, see <A href="limits-for-public-folders-exchange-2013-help.md">Límites de las carpetas públicas</A>.</P></LI></UL>



For additional management tasks related to public folders in Exchange Server 2013, see [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

For additional management tasks related to public folders in Exchange Online, see [Procedimientos de carpetas públicas en Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/jj966272\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete this task: 30 minutes.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Public folders" entry in the [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md) topic.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## How do you do this?

## Step 1: Create the primary public folder mailbox

The primary public folder mailbox contains a writeable copy of the public folder hierarchy plus content and is the first public folder mailbox that you create for your organization. Subsequent public folder mailboxes will be secondary public folder mailboxes, which will contain a read-only copy of the hierarchy plus content.

For detailed steps, see [Crear un buzón de carpetas públicas](https://docs.microsoft.com/es-es/exchange/collaboration-exo/public-folders/create-public-folder-mailbox).

## Step 2: Create your first public folder

For detailed steps, see [Crear una carpeta pública](https://docs.microsoft.com/es-es/exchange/collaboration-exo/public-folders/create-public-folder).

## Step 3: Assign permissions to the public folder

After you create the public folder, you’ll need to assign the **Owner** permissions level so that at least one user can access the public folder from the client and create subfolders. Any public folders created after this one will inherit the permissions of the parent public folder.

1.  In the Exchange admin center (EAC), navigate to **Public folders** \> **Public folders**.

2.  In the list view, select the public folder.

3.  In the details pane, under **Folder permissions**, click **Manage**.

4.  In **Public Folder Permissions**, click **Add**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

5.  Click **Browse** to select a user.

6.  In the **Permission level** list, select a level. At least one user should be an **Owner**.

7.  Click **Save**.

8.  You can add multiple users by clicking **Add**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") and assigning the appropriate permissions using the steps above. You can also customize the permission level by selecting or clearing the check boxes. When you edit a predefined permission level such as **Owner**, the permission level will change to **Custom**.

For information about how to use the Shell to assign permissions to a public folder, see [Add-PublicFolderClientPermission](https://technet.microsoft.com/es-es/library/bb124743\(v=exchg.150\)).

## Step 4 (Optional): Mail-enable the public folder

If you want users to send mail to the public folder, you can mail-enable it. This step is optional. If you don't mail-enable the public folder, users can post messages to the public folder by dragging items into it from within Outlook.

1.  In the EAC, navigate to **Public folders** \> **Public folders**.

2.  In the list view, select the public folder you want to mail-enable.

3.  In the details pane, under **Mail settings – Disabled**, click **Enable**.
    
    A warning displays asking if you are sure you want to enable mail for the public folder. Click **Yes**.

The public folder will be mail-enabled and the name of the public folder will become the alias of the public folder. If you have multiple recipients with that name, the public folder’s alias will be appended with a number. For example, if you have a distribution group named SalesTeam and you create a public folder named SalesTeam and then mail-enable it, the alias of that public folder will be SalesTeam1.

For information about how to use the Shell to mail-enable a public folder, see [Enable-MailPublicFolder](https://technet.microsoft.com/es-es/library/aa998824\(v=exchg.150\)).

