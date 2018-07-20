---
title: 'Eliminar un grupo de extensiones de MU.: Exchange 2013 Help'
TOCTitle: Eliminar un grupo de extensiones de MU.
ms:assetid: 11ac102d-b58d-486c-85b6-e096428e556d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996318(v=EXCHG.150)
ms:contentKeyID: 50556742
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminar un grupo de extensiones de MU.

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

Cuando elimina un grupo de extensiones de mensajería unificada (MU), la puerta de enlace IP de MU asociada al grupo de extensiones de MU dejará de prestar servicio o responder a las llamadas entrantes. Si eliminar un grupo de extensiones de MU deja la puerta de enlace IP de MU sin ningún grupo de extensiones configurado, ésta no podrá manejar o procesar llamadas de MU.

Para consultar otras tareas relacionadas con grupos de extensiones de MU, consulte [Procedimientos de grupo de captura de mensajería unificada](um-hunt-group-procedures-exchange-2013-help.md).


> [!WARNING]
> Si desea cambiar la configuración del grupo de extensiones de MU, debe eliminar el grupo de extensiones y crear otro con la configuración deseada.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Grupos de extensiones de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una puerta de enlace IP de mensajería unificada. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un grupo de extensiones de MU. Para conocer los pasos detallados, consulte [Crear un grupo de extensiones de mensajería unificada](create-a-um-hunt-group-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para crear un grupo de extensiones de MU

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, haga clic en el plan de marcado de MU que desea cambiar y, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de MU**, en **Grupos de extensiones de MU**, seleccione el grupo de extensiones que desea eliminar y, en la barra de herramientas, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

3.  En la página **Advertencia**, haga clic en **Sí**.

## Uso del Shell para eliminar un grupo de extensiones de MU

En este ejemplo, se elimina un grupo de extensiones de MU llamado `MyUMHuntGroup`.

    Remove-UMHuntGroup -identity MyUMHuntGroup

