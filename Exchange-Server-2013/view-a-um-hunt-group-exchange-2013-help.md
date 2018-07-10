---
title: 'Ver un grupo de captura de mensajería unificada: Exchange 2013 Help'
TOCTitle: Ver un grupo de captura de mensajería unificada
ms:assetid: f038f7b4-4de9-4373-bd58-09d49e37a3ed
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125167(v=EXCHG.150)
ms:contentKeyID: 50556906
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver un grupo de captura de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

Cuando visualice las propiedades de un grupo de búsqueda de mensajería unificada (UM), puede ver las propiedades asociadas a un único grupo de búsqueda o a todos los grupos de búsqueda de mensajería unificada asociados a una puerta de enlace IP de mensajería unificada. Si no se especifica ningún parámetro, se devolverán todos los grupos de búsqueda de mensajería unificada. No se puede utilizar la EAC para ver las propiedades de un grupo de búsqueda de mensajería unificada; debe utilizar el Shell.

Después de crear un grupo de búsqueda de mensajería unificada, los valores configurados no se pueden cambiar. Si desea cambiar una opción de configuración, como el identificador piloto de un grupo de búsqueda de mensajería unificada, deberá eliminar el grupo de extensiones existente y crear uno nuevo que tenga la configuración correcta.

Para consultar otras tareas relacionadas con los grupos de búsqueda de mensajería unificada, vea [Procedimientos de grupo de captura de mensajería unificada](um-hunt-group-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Grupos de extensiones de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una puerta de enlace de mensajería unificada. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un grupo de búsqueda de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un grupo de extensiones de mensajería unificada](create-a-um-hunt-group-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use el Shell para ver las propiedades de un grupo de búsqueda de mensajería unificada

En este ejemplo se muestra todos los grupos de extensiones de mensajería unificada del bosque de Active Directory.

    Get-UMHuntGroup

En este ejemplo se muestran los detalles de un grupo de búsqueda de mensajería unificada denominado `MyUMHuntGroup` en una lista con formato.

    Get-UMHuntGroup -identity MyUMIPGateway\MyUMHuntGroup | Format-List


> [!NOTE]
> Cuando use el cmdlet <STRONG>Get-UMHuntGroup</STRONG>, no puede especificar solo el nombre del grupo de búsqueda de mensajería unificada. También debe incluir el nombre de la puerta de enlace IP de mensajería unificada asociada al grupo de búsqueda correspondiente.


