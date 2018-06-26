---
title: 'Crear una lista global de direcciones: Exchange 2013 Help'
TOCTitle: Crear una lista global de direcciones
ms:assetid: 59e4955a-8999-4d17-be9f-23a41a23b929
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232063(v=EXCHG.150)
ms:contentKeyID: 49895647
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear una lista global de direcciones

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2014-12-16_

La lista global de direcciones (LGD) es un directorio que contiene entradas para todos los grupos, usuarios y contactos de la implementación de Microsoft Exchange de una organización. Si la organización utiliza directivas de la libreta de direcciones, es posible que desee crear GAL adicionales. Para obtener más información, vea [Directivas de la libreta de direcciones](address-book-policies-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las listas de direcciones, consulte [Procedimientos de la lista de direcciones](address-list-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Listas de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para crear una GAL mediante propiedades de filtro condicional

En este ejemplo, se crea una GAL denominada GAL\_Contoso que incluye destinatarios que son usuarios de buzones y que muestran su empresa con el nombre Contoso.

    New-GlobalAddressList -Name "GAL_Contoso" -IncludedRecipients MailboxUsers -ConditionalCompany Contoso


> [!NOTE]
> Si usa las propiedades de filtro condicional predefinido, el parámetro <EM>IncludedRecipients</EM> no puede estar en blanco.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-GlobalAddressList](https://technet.microsoft.com/es-es/library/bb123785\(v=exchg.150\)).

## Uso del Shell para crear una GAL mediante un filtro de destinatarios

En este ejemplo, se crea una GAL denominada GAL\_AgencyA que incluye destinatarios para los que el parámetro *CustomAttribute15* tiene un valor de `AgencyA`.

    New-GlobalAddressList -Name "GAL_AgencyA" -RecipientFilter {CustomAttribute15 -like "AgencyA"}

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-GlobalAddressList](https://technet.microsoft.com/es-es/library/bb123785\(v=exchg.150\)).

