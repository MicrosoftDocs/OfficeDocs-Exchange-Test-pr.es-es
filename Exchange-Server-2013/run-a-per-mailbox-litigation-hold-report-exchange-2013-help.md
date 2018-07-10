---
title: 'Ejecutar un informe de retención por litigio por buzón: Exchange 2013 Help'
TOCTitle: Ejecutar un informe de retención por litigio por buzón
ms:assetid: 98c46226-2f48-42c6-a741-34bb5944f519
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150542(v=EXCHG.150)
ms:contentKeyID: 48268478
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ejecutar un informe de retención por litigio por buzón

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-10-13_

Si su organización está implicada en una acción legal, tal vez deba adoptar medidas para conservar los datos pertinentes, como los mensajes de correo electrónico, que se puedan usar como pruebas. En las situaciones de este tipo, puede usar la retención por juicio para conservar todo el correo electrónico enviado o recibido por determinadas personas o retener todo el correo electrónico enviado y recibido en su organización durante un periodo de tiempo específico. Para obtener más información acerca de lo que sucede cuando un buzón de correo tiene una retención por juicio y cómo habilitarla y deshabilitarla, vea la sección "Características de buzón" en [Administrar los buzones de usuario](manage-user-mailboxes-exchange-2013-help.md).

Use el informe de retención por juicio para realizar el seguimiento de los siguientes tipos de cambio efectuados en un buzón de correo en un determinado periodo de tiempo:

  - Se ha habilitado la retención por juicio.

  - Se ha deshabilitado la retención por juicio.

Por cada uno de estos tipos de cambios, el informe incluye el usuario que realizó el cambio, así como la hora y la fecha en que se hizo.

## ¿Qué necesita saber antes de comenzar?

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría de administrador de solo vista" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilice el EAC para ejecutar un informe de retención de litigios

1.  En el EAC, navegue a **Administración de cumplimiento** \> **Auditoría**.

2.  Haga clic en **Ejecutar un informe de retención por juicio por buzón**.
    
    Microsoft Exchange ejecuta el informe de los cambios de retención por juicio efectuados en cualquier buzón de correo en las dos últimas semanas.

3.  Para ver los cambios de un buzón de correo específico, seleccione el buzón de correo en el panel de resultados de búsqueda. Consulte los resultados de la búsqueda en el panel de detalles.


> [!TIP]
> ¿Desear limitar los resultados de la búsqueda? Seleccione la fecha de inicio, la fecha de finalización o ambas, y seleccione los buzones de correo concretos en los que se buscará. Haga clic en <STRONG>Buscar</STRONG> para volver a ejecutar el informe.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha ejecutado correctamente un informe de retención por juicio, en el panel de resultados de búsqueda se mostrarán los buzones de correo que tenían cambios de retención por juicio dentro del intervalo de fechas. Si no hay resultados, significa que no se han producido retenciones por juicio dentro del intervalo de fechas, o que los últimos cambios todavía no se han aplicado.


> [!NOTE]
> Cuando un buzón de correo es puesto en retención por juicio, la retención puede llevar hasta 60 minutos en aplicarse.


