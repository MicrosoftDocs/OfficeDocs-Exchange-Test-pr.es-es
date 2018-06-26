---
title: 'Crear una lista de direcciones mediante filtros de destinatario: Exchange 2013 Help'
TOCTitle: Crear una lista de direcciones mediante filtros de destinatario
ms:assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123718(v=EXCHG.150)
ms:contentKeyID: 49895770
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear una lista de direcciones mediante filtros de destinatario

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2014-12-16_

En este tema se explica cómo crear una lista de direcciones de correo mediante el uso de filtros de destinatarios. Para obtener más información acerca de las listas de direcciones, consulte [Listas de direcciones](address-lists-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las listas de direcciones, consulte [Procedimientos de la lista de direcciones](address-list-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Listas de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - Para usar el parámetro *RecipientFilter* a fin de crear un filtro personalizado, debe especificar una cadena para el filtro. El Shell usa OPATH para la sintaxis de filtrado. OPATH es un lenguaje de consultas diseñado para consultar orígenes de datos de objetos.

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para crear una lista de direcciones mediante el uso de filtros de destinatarios

En este ejemplo, se crea una lista de direcciones para todos los usuarios con buzones de correo de Exchange que residen en Washington u Oregon.

    New-AddressList -Name "Pacific Northwest Mailboxes" -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

En este ejemplo, se crea una lista de direcciones para todos los usuarios con buzones de Exchange que tienen `AgencyB` como valor para el parámetro *CustomAttribute15*.

    New-AddressList -Name "AgencyB" -RecipientFilter {(RecipientType -eq 'UserMailbox') -and (CustomAttribute15 -like *AgencyB*)}

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-AddressList](https://technet.microsoft.com/es-es/library/aa996912\(v=exchg.150\)).

