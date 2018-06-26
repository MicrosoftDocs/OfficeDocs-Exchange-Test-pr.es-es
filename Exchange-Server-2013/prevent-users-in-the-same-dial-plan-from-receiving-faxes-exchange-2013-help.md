---
title: 'Impedir que los usuarios en el mismo plan de marcado de recibir faxes: Exchange 2013 Help'
TOCTitle: Impedir que los usuarios en el mismo plan de marcado de recibir faxes
ms:assetid: 4fc66414-c950-4bca-ac20-4e489f288d06
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201688(v=EXCHG.150)
ms:contentKeyID: 52061827
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impedir que los usuarios en el mismo plan de marcado de recibir faxes

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Puede evitar que los usuarios habilitados para mensajería unificada vinculados a un plan de marcado de mensajería unificada reciban mensajes de fax. De manera predeterminada, los usuarios habilitados para mensajería unificada que están vinculados con un plan de marcado de mensajería unificada pueden recibir mensajes de fax. Sin embargo, puede que en alguna ocasión desee impedir que los usuarios asociados con un plan de marcado de mensajería unificada específico reciban mensajes de fax.

Puede impedir que los usuarios habilitados para mensajería unificada reciban faxes al configurar el plan de marcado de mensajería unificada, la directiva de buzón de mensajería unificada o el buzón del usuario habilitado para mensajería unificada. Si deshabilita la entrega de mensajes de fax entrantes en un plan de marcado de mensajería unificada, se impedirá a todos los usuarios asociados al plan de marcado recibir mensajes de fax. La habilitación o deshabilitación de los faxes en un plan de marcado de mensajería unificada tiene prioridad sobre la configuración de un usuario individual habilitado para MU.


> [!NOTE]
> Puede usar el EAC para configurar los parámetros de fax en una directiva de buzones de correo de mensajería unificada. Sin embargo, debe usar el Shell para configurar los parámetros de fax en los planes de marcado de los usuarios individuales.



Para obtener más información acerca de los partners de fax, consulte [Microsoft PinPoint para asociados de negocios de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para otras tareas de administración relacionadas con los faxes, consulte [Procedimientos de envío de faxes](faxing-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para impedir que los usuarios vinculados a un plan de marcado reciban faxes

En este ejemplo, se impide que los usuarios habilitados para MU asociados con el plan de marcado denominado `MyUMDialPlan` reciban faxes.

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $false

