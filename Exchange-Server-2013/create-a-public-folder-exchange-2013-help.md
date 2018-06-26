---
title: 'Crear una carpeta pública: Exchange 2013 Help'
TOCTitle: Crear una carpeta pública
ms:assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb691104(v=EXCHG.150)
ms:contentKeyID: 49116285
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
ms.translationtype: MT
---

# Crear una carpeta pública

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2014-02-24_

Public folders are designed for shared access and provide an easy and effective way to collect, organize, and share information with other people in your workgroup or organization.

By default, a public folder inherits the settings of its parent folder, including the permissions settings.


> [!NOTE]
> For more information about the storage quotas and limits for public folders, see the following topics: 
> <UL>
> <LI>
> <P>Para carpetas públicas de Office 365, vea <A href="https://go.microsoft.com/fwlink/?linkid=391188">Límites de Exchange Online</A>.</P>
> <LI>
> <P>For public folders in on-premises Exchange Server 2013, see <A href="limits-for-public-folders-exchange-2013-help.md">Límites de las carpetas públicas</A>.</P></LI></UL>



For additional management tasks related to managing public folders, see [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las carpetas públicas, consulte [Procedimientos de carpetas públicas en Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/jj966272\(v=exchg.150\)).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Public folders" entry in the [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md) topic.

  - You can’t create a public folder unless you’ve first created a public folder mailbox. For more information about how to create a public folder mailbox, see [Crear un buzón de carpetas públicas](create-a-public-folder-mailbox-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## What do you want to do?

## Use the EAC to create a public folder

When using the EAC to create a public folder, you’ll only be able to set the name and the path of the public folder. To configure additional settings, you’ll need to edit the public folder after it’s created.

1.  Navigate to **Public folders** \> **Public folders**.

2.  If you want to create this public folder as a child of an existing public folder, click the existing public folder in the list view. If you want to create a top-level public folder, skip this step.

3.  Click **Add**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  In **Public Folder**, type the name of the public folder.
    

    > [!IMPORTANT]
    > Don't use a backslash (\) in the name when creating a public folder.



5.  In the **Path** box, verify the path to the public folder. If this isn’t the desired path, click **Cancel** and follow Step 2 of this procedure.

6.  Click **Save**.

## Use the Shell to create a public folder

This example creates a public folder named Reports in the path Marketing\\2013.

    New-PublicFolder -Name Reports -Path \Marketing\2013


> [!IMPORTANT]
> Don't use a backslash (\) in the name when creating a public folder.



For detailed syntax and parameter information, see [New-PublicFolder](https://technet.microsoft.com/es-es/library/aa996405\(v=exchg.150\)).

## How do you know this worked?

To verify that you’ve successfully created a public folder, do the following:

  - In the EAC, click **Refresh** to refresh the list of public folders. Your new public folder should be displayed in the list.

  - In the Shell, run any of the following commands:
    
        Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
    
        Get-PublicFolder -Identity \Marketing\2013 -GetChildren
    
        Get-PublicFolder -Recurse


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


