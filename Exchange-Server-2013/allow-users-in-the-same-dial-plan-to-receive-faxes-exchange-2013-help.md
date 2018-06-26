---
title: 'Permitir a los usuarios en el mismo plan de marcado para recibir faxes: Exchange 2013 Help'
TOCTitle: Permitir a los usuarios en el mismo plan de marcado para recibir faxes
ms:assetid: cb245028-0b86-4171-879e-934dd35fa626
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124557(v=EXCHG.150)
ms:contentKeyID: 52061883
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir a los usuarios en el mismo plan de marcado para recibir faxes

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Puede permitir que todos los usuarios vinculados a un plan de marcado de mensajería unificada reciban mensajes de faxes en sus buzones de correo. Los usuarios habilitados para mensajería unificada que están vinculados a un plan de marcado de mensajería unificada pueden recibir mensajes de fax de manera predeterminada. Para permitir que los usuarios con mensajería unificada habilitada reciban mensajes de fax en sus buzones de correo, el plan de marcado se debe configurar para aceptar llamadas de fax entrantes. También debe habilitar los faxes en la directiva de buzones de correo de mensajería unificada y para el usuario. El envío de faxes está habilitado de forma predeterminada en los planes de marcado, en las directivas de buzones de correo de mensajería unificada y para los usuarios. No obstante, a veces puede que esta configuración predeterminada haya cambiado y que los usuarios habilitados para mensajería unificada no puedan recibirlos.

Si impide que se reciban mensajes de fax en un plan de marcado, todos los usuarios asociados con dicho plan no podrán recibir mensajes de fax, aunque configure las propiedades de uno o varios usuarios individuales para permitir que los reciban. La activación o desactivación de faxes en un plan de marcado de mensajería unificada tiene prioridad sobre la configuración de los faxes en una directiva de buzones de correo de mensajería unificada o un usuario individual habilitado para mensajería unificada.


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



## Usar el Shell para permitir que los usuarios vinculados a un plan de marcado reciban faxes

En este ejemplo se permite que los usuarios habilitados para mensajería unificada vinculados al plan de marcado de mensajería unificada denominado `MyUMDialPlan` puedan recibir faxes entrantes.

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $true

