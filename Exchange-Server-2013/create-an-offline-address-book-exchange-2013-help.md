---
title: 'Crear una libreta de direcciones sin conexión: Exchange 2013 Help'
TOCTitle: Crear una libreta de direcciones sin conexión
ms:assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124339(v=EXCHG.150)
ms:contentKeyID: 49895855
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
ms.translationtype: HT
---

# Crear una libreta de direcciones sin conexión

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-04-24_

Una libreta de direcciones sin conexión (OAB) en Exchange Server 2013 es una copia de la libreta de direcciones que se puede descargar que permite que el usuario de Outlook pueda acceder a la información mientras no está conectado al servidor. Los administradores de Exchange pueden decidir qué libretas de direcciones ponen a disposición de los usuarios para que puedan trabajar sin conexión; asimismo, pueden configurar el método de distribución de las libretas de direcciones (distribución basada en web o distribución de carpetas públicas).

Para otras tareas de administración relacionadas con las libretas de direcciones sin conexión, consulte [Procedimientos de libretas de direcciones sin conexión](offline-address-book-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Libreta de direcciones sin conexión" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para crear una libreta de direcciones sin conexión con distribución basada en web

En este ejemplo se crea una libreta de direcciones sin conexión denominada OAB\_Contoso que usa la distribución basada en web para Outlook 2007 o clientes de versiones posteriores mediante el uso del directorio virtual predeterminado.

    New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List" -VirtualDirectories $Null -GlobalWebDistributionEnabled $True

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-OfflineAddressBook](https://technet.microsoft.com/es-es/library/bb123692\(v=exchg.150\)) (página en inglés).

