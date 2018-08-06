---
title: 'Cambiar programa generación libreta dirección sin conexión: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Cambiar el programa de generación de libretas de direcciones sin conexión
ms:assetid: d2b4d527-311e-442d-9f1f-54fac8371b80
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124719(v=EXCHG.150)
ms:contentKeyID: 49895934
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.OfflineAddressBookGeneralPage
ms.translationtype: MT
---

# Cambiar el programa de generación de libretas de direcciones sin conexión

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-12-05_

Una libreta de direcciones sin conexión (OAB) es una copia de una libreta de direcciones que se descarga para que un usuario de Outlook pueda tener acceso a la información que contiene cuando no tiene conexión con el servidor. Puede configurar la frecuencia con la que se genera una libreta de direcciones sin conexión mediante los parámetros *OABGeneratorWorkCycle* y *OABGeneratorWorkCycleCheckpoint* en el cmdlet Set-MailboxServer.

Para otras tareas de administración relacionadas con la libreta de direcciones sin conexión, consulte [Procedimientos de libretas de direcciones sin conexión](offline-address-book-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Libreta de direcciones sin conexión" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - No puede usar el centro de administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para configurar las propiedades de libretas de direcciones sin conexión

En este ejemplo, la libreta de direcciones sin conexión se genera cada seis horas todos los días en el servidor de buzones MBXServer01.

    Set-MailboxServer -Identity MBXServer01 -OABGeneratorWorkCycle 01.00:00:00 -OABGeneratorWorkCycleCheckpoint 06:00:00 

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OfflineAddressBook](https://technet.microsoft.com/es-es/library/aa996330\(v=exchg.150\)).

