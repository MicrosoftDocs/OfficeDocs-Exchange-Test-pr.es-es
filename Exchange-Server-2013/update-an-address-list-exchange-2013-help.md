---
title: 'Actualizar una lista de direcciones: Exchange 2013 Help'
TOCTitle: Actualizar una lista de direcciones
ms:assetid: 163e7099-cf14-4bb0-a84c-1401e9db670e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996375(v=EXCHG.150)
ms:contentKeyID: 49895487
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.UpdateAddressListWizardForm.ScheduleWizardPage
ms.translationtype: HT
---

# Actualizar una lista de direcciones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-14_

Las listas de direcciones son un conjunto de objetos de destinatario y otros objetos de Active Directory. La lista de direcciones se aplica cuando se ha modificado la regla de filtro de lista de direcciones. Para actualizar la pertenencia de la lista de direcciones con el fin de incluir los destinatarios nuevos y quitar los destinatarios que ya no cumplen los criterios de filtrado, deberá aplicar la lista de direcciones.

Para otras tareas de administración relacionadas con las listas de direcciones, consulte [Procedimientos de la lista de direcciones](address-list-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Este proceso puede que tarde mucho tiempo en finalizar según el número de destinatarios en la lista de direcciones.

  - Algunas listas de direcciones contienen miles o decenas de miles de destinatarios, en función del tamaño de la organización y los filtros que haya añadido a las listas de direcciones. La actualización de las listas de direcciones puede precisar una gran cantidad de recursos informáticos. Por lo tanto, puede actualizar la lista de direcciones durante las horas de poca actividad.

  - Si la lista de direcciones contiene más de 3.000 destinatarios, le recomendamos que use el Shell de administración de Exchange para actualizarla.

Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para actualizar una lista de direcciones

1.  Vaya a **Organización** \> **Lista de direcciones**.

2.  En la vista de lista, seleccione la lista de direcciones que desee actualizar.

3.  En el panel de detalles, haga clic en **Actualizar**.

## Usar el Shell para actualizar una lista de direcciones

Este ejemplo actualiza la lista de direcciones Estado de Washington.

    Update-AddressList "Washington State"

Si tiene más de una lista de direcciones con el mismo nombre, debe especificar la ruta de acceso completa a la lista de direcciones que desea actualizar. Por ejemplo, si desea actualizar la lista de direcciones Ventas en Norteamérica, pero también existe una lista de direcciones Ventas en Europa, use el siguiente comando:

    Update-AddressList "North America\Sales"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Update-AddressList](https://technet.microsoft.com/es-es/library/aa997982\(v=exchg.150\)).

