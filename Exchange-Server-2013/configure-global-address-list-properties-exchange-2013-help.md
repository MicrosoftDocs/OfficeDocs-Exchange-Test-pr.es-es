---
title: 'Configurar propiedades de la lista global de direcciones: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configurar las propiedades de la lista global de direcciones
ms:assetid: 5fd2c96f-fe93-4b5a-8495-70c450511a37
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232068(v=EXCHG.150)
ms:contentKeyID: 49895661
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar las propiedades de la lista global de direcciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-12-16_

En este tema se explica cómo modificar la configuración de una lista global de direcciones (LGD).

Para otras tareas de administración relacionadas con las listas de direcciones, consulte [Procedimientos de la lista de direcciones](address-list-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Listas de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - No se puede editar la configuración de la LGD predeterminada.

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para configurar las propiedades de la LGD

En este ejemplo, se asigna un nombre nuevo, FourthCoffee, a la GAL cuyo GUID es 96d0c505-eba8-4103-ad4f-577a1bf4ad7b.

    Set-GlobalAddressList -Identity 96d0c505-eba8-4103-ad4f-577a1bf4ad7b -Name FourthCoffee


> [!NOTE]
> Si usa las propiedades de filtro condicional predefinido, el valor del parámetro <EM>IncludedRecipients</EM> no puede estar en blanco.



En este ejemplo, se modifican los destinatarios que se incluirán en la LGD Fourth Coffee global por aquellos cuya empresa está establecida en Fourth Coffee.

    Set-GlobalAddressList -Identity Fourth Coffee -RecipientFilter {Company -eq "Fourth Coffee"}

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-GlobalAddressList](https://technet.microsoft.com/es-es/library/bb123877\(v=exchg.150\)).

