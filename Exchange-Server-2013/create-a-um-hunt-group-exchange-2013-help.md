---
title: 'Crear un grupo de extensiones de mensajería unificada: Exchange 2013 Help'
TOCTitle: Crear un grupo de extensiones de mensajería unificada
ms:assetid: 43ecb1ec-5f82-4516-9010-de8f954d3758
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997679(v=EXCHG.150)
ms:contentKeyID: 50556776
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMHuntGroupWizardForm.CreateUMHuntGroupWizardPage1
ms.translationtype: MT
---

# Crear un grupo de extensiones de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-16_

Un grupo de extensiones de mensajería unificada es una representación lógica del grupo de extensiones IP PBX o de la central de conmutación (PBX). Los grupos de extensiones de mensajería unificada actúan como conexión o vínculo entre la puerta de enlace IP de mensajería unificada y un plan de marcado de mensajería unificada.


> [!NOTE]
> Si cuando crea una puerta de enlace de IP de mensajería unificada la asocia a un plan de marcado de mensajería unificada, también se creará un grupo de extensiones de mensajería unificada.




> [!NOTE]
> Si desea cambiar la configuración del grupo de extensiones de mensajería unificada, debe eliminar el grupo de extensiones y crear otro con la configuración deseada.



Para consultar otras tareas de administración relacionadas con los grupos de extensiones de mensajería unificada, vea [Procedimientos de grupo de captura de mensajería unificada](um-hunt-group-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Grupos de extensiones de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una puerta de enlace IP de mensajería unificada. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para crear un grupo de extensiones de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Grupos de extensiones de mensajería unificada**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Nuevo grupo de extensiones de mensajería unificada**, especifique la siguiente información:
    
      - **Nombre**   Use este cuadro para crear el nombre para mostrar del grupo de extensiones de mensajería unificada. Se requiere un nombre de grupo de extensiones de mensajería unificada exclusivo, que solo se usará para mostrar en el EAC y en el Shell. Si tiene que cambiar el nombre para mostrar del grupo de extensiones después de crearlo, antes debe eliminar el grupo de extensiones existente y, a continuación, crear otro grupo de extensiones con el nombre adecuado.
        
        Si la organización utiliza varios grupos de extensiones, es recomendable que use nombres significativos. La longitud máxima de un nombre de grupo de extensiones de MU es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Puerta de enlace IP de mensajería unificada**   Use este cuadro para especificar la puerta de enlace IP de mensajería unificada. Haga clic en **Examinar** para seleccionar la puerta de enlace IP de mensajería unificada y, a continuación, haga clic en **Aceptar**.
    
      - **Identificador piloto**   Use este cuadro para especificar una cadena que identifique exclusivamente al identificador piloto configurado en la PBX o IP-PBX.
        
        Puede usar un número de extensión o un Identificador uniforme de recursos (URI) del Protocolo de inicio de sesión (SIP) en este cuadro. Este cuadro admite caracteres alfanuméricos. Para PBX heredadas, se utiliza un valor numérico como identificador piloto. Sin embargo, algunas IP PBX pueden usar URI de SIP.

4.  
    
    Haga clic en **Guardar**.

## Usar el Shell para crear un grupo de extensiones de MU

Este ejemplo crea un grupo de extensiones MU denominado `MyUMHuntGroup` que tiene un identificador piloto de 12345.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 12345 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

Este ejemplo crea un grupo de extensiones de MU denominado `MyUMHuntGroup` que tiene varios identificadores piloto.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

