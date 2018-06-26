---
title: 'Actualizar una lista global de direcciones: Exchange 2013 Help'
TOCTitle: Actualizar una lista global de direcciones
ms:assetid: 236e8530-62dd-4c43-8a5d-8465623252e6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb266966(v=EXCHG.150)
ms:contentKeyID: 49895518
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Actualizar una lista global de direcciones

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-12-16_

Puede utilizar el Shell para actualizar una lista global de direcciones (LGD). Una LGD es un directorio que contiene entradas para cada grupo, usuario y contacto dentro de la implementación de Microsoft Exchange de una organización.

Para otras tareas de administración relacionadas con las listas de direcciones, consulte [Procedimientos de la lista de direcciones](address-list-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Listas de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para actualizar una LGD

En este ejemplo, se actualiza una LGD para la empresa Fourth Coffee.


> [!NOTE]
> Al ejecutar este comando sólo se inicia el proceso de actualización. La actualización de LGD puede tardar varias horas.



    Update-GlobalAddressList -Identity "Fourth Coffee"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Update-GlobalAddressList](https://technet.microsoft.com/es-es/library/aa998806\(v=exchg.150\)).

