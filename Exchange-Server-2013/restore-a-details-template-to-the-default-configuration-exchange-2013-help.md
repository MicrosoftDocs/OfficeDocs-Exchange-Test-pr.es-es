---
title: 'Restaurar la configuración predeterminada de una plantilla de detalles: Exchange 2013 Help'
TOCTitle: Restaurar la configuración predeterminada de una plantilla de detalles
ms:assetid: 84c5f49b-614d-4f0e-8701-0979a2eb90bf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232102(v=EXCHG.150)
ms:contentKeyID: 49895749
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Restaurar la configuración predeterminada de una plantilla de detalles

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-12_

El Editor de plantillas de detalles no contiene un botón **Deshacer** ni le permite usar un método abreviado de teclado para deshacer una acción. Para deshacer una adición realizada a la plantilla, debe usar la tecla SUPR. Para deshacer una eliminación, debe volver a aplicar el ajuste. También es posible volver a la configuración original saliendo del Editor de plantillas de detalles sin guardar los cambios. Si desea deshacer los cambios una vez guardados, puede restaurar la plantilla. Al restaurar una plantilla, se pierden todas las personalizaciones y se restaura la configuración original de la plantilla.

En este tema se explica cómo usar el Cuadro de herramientas de Exchange 2013 o el Shell de administración de Exchange para restaurar una plantilla de detalles a la configuración predeterminada.

Para obtener más información acerca de las plantillas de detalles, consulte [Plantillas de detalles](details-templates-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Plantillas de detalles" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Cuadro de herramientas de Exchange para restaurar una plantilla de detalles a la configuración predeterminada

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange Server 2013** \> **Cuadro de herramientas de Exchange**.

2.  En **Cuadro de herramientas de Exchange**, haga clic en **Editor de plantillas de detalles** y, a continuación, en el panel de acción, haga clic en **Abrir herramienta**.

3.  En el **Editor de plantillas de detalles**, en el panel de detalles, seleccione la plantilla que desea restaurar y, a continuación, en el panel de acciones, haga clic en **Restaurar**.

4.  Haga clic en **Sí** para confirmar que desea restaurar la plantilla a su estado original. Se perderán todas las personalizaciones.

## Usar el Shell para restaurar una plantilla de detalles a la configuración predeterminada

En este ejemplo se restaura la plantilla de detalles de contactos en inglés de EE.UU..

    Restore-DetailsTemplate -Identity "en-US\Contact"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Restore-DetailsTemplate](https://technet.microsoft.com/es-es/library/bb125188\(v=exchg.150\)).

