---
title: 'Cree una puerta de enlace IP de mensajería unificada: Exchange 2013 Help'
TOCTitle: Cree una puerta de enlace IP de mensajería unificada
ms:assetid: 542d6b50-147b-4cec-b54d-61c7b8fc0fc7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998045(v=EXCHG.150)
ms:contentKeyID: 49895631
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMIPGatewayWizardForm.CreateUMIPGatewayWizardPage
ms.translationtype: MT
---

# Cree una puerta de enlace IP de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-16_

Cuando se crea una puerta de enlace IP de mensajería unificada, se habilitan los servidores de buzones Exchange para conectarse a una nueva puerta de enlace de voz sobre IP (VoIP), a una central de conmutación (PBX) habilitada para el Protocolo de inicio de sesión (SIP), a una IP PBX o a un controlador de borde de sesión (SBC). Inmediatamente después de crear una puerta de enlace IP de mensajería unificada, debe crear un nuevo grupo de extensiones de mensajería unificada y, a continuación, asociarlo a dicha puerta. Puede asociar la puerta de enlace IP de mensajería unificada a uno o varios planes de marcado de mensajería unificada mediante la creación de uno o varios grupos de extensiones de mensajería unificada.

Para otras tareas de administración relacionadas con puertas de enlace IP de mensajería unificada, consulte [Procedimientos de puerta de enlace IP de mensajería unificada](um-ip-gateway-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Puertas de enlace IP de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para crear una puerta de enlace IP de mensajería unificada

1.  
    
    En el EAC, vaya a **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada** y, a continuación, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nueva puerta de enlace IP de mensajería unificada**, especifique la siguiente información:
    
      - **Nombre**   Use este cuadro para especificar un nombre exclusivo para la puerta de enlace IP de mensajería unificada. Se trata de un nombre para mostrar que aparecerá en la Consola de administración de Exchange. Si tiene que cambiar el nombre para mostrar de la puerta de enlace IP de mensajería unificada una vez creada, primero deberá eliminar la puerta de enlace IP de mensajería unificada existente y, a continuación, crear otra puerta de enlace IP de mensajería unificada con el nombre que desee. El nombre de puerta de enlace IP de mensajería unificada es necesario, pero solo se usa para su visualización. Como la organización puede usar varias puertas de enlace IP de mensajería unificada, es recomendable el uso de nombres significativos para designar las puertas de enlace IP de mensajería unificada. La longitud máxima que puede tener un nombre de puerta de enlace IP de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Dirección**   Puede configurar una puerta de enlace IP de mensajería unificada con una dirección IP o un nombre de dominio completo (FQDN). Use este cuadro para indicar la dirección IP configurada en la puerta de enlace VoIP, un PBX habilitado para SIP, un IP PBX, un SBC o un FQDN. En este cuadro solo se admiten FQDN válidos y con el formato correcto.
        
        Puede escribir caracteres alfabéticos y numéricos en este cuadro. Se admiten direcciones IPv4, IPv6 y FQDN. Si desea usar una Seguridad de la capa de transporte mutua (TLS mutua) entre una puerta de enlace IP de mensajería unificada y un plan de marcado funcionando en modo SIP protegido o modo protegido, debe configurar la puerta de enlace IP de mensajería unificada con un FQDN. También debe configurarla para que escuche en el puerto 5061 y compruebe si también se configuraron puertas de enlace VoIP o IP PBX para escuchar las solicitudes TLS mutuas en el puerto 5061. Para configurar una puerta de enlace IP de mensajería unificada, ejecute el siguiente comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        Si se usa un FQDN, debe asegurarse de que se haya configurado correctamente un registro de host DNS para la puerta de enlace VoIP, de modo que el nombre del host se resuelva correctamente en una dirección IP. Asimismo, si utiliza un FQDN en lugar de una dirección IP, y se modifica la configuración de DNS para la puerta de enlace IP de mensajería unificada, deberá deshabilitar la puerta de enlace IP de mensajería unificada y habilitarla después para asegurarse de que la información de configuración de dicha puerta de enlace se actualiza correctamente.
    
      - **Plan de marcado de mensajería unificada**   Haga clic en **Examinar** para seleccionar el plan de marcado de mensajería unificada que desea asociar a la puerta de enlace IP de mensajería unificada. Cuando seleccione un plan de marcado de mensajería unificada con una puerta de enlace IP de mensajería unificada, también se creará un grupo de extensiones de mensajería unificada predeterminado y se asociará con el plan de marcado de mensajería unificada seleccionado. Si no selecciona un plan de marcado de mensajería unificada, deberá crear manualmente un grupo de extensiones de MU y, a continuación, asociar dicho grupo con la puerta de enlace IP de mensajería unificada que cree.

3.  
    
    Haga clic en **Guardar**.

## Usar el Shell para crear una puerta de enlace IP de MU

En este ejemplo se crea una puerta de enlace IP de mensajería unificada llamada `MyUMIPGateway` que habilita los servidores de buzones Exchange para que comiencen a aceptar llamadas de una puerta de enlace VoIP, una PBX habilitada para SIP, una IP PBX o un SBC con la dirección IP 10.10.10.1.

    New-UMIPGateway -Name MyUMIPGateway -Address 10.10.10.1

En este ejemplo se crea una puerta de enlace IP de mensajería unificada llamada `MyUMIPGateway` que habilita los servidores Exchange para que comiencen a aceptar llamadas de una puerta de enlace VoIP, una PBX habilitada para SIP, una IP PBX o un SBC cuyo nombre de dominio completo (FQDN) sea MyUMIPGateway.contoso.com y que escuche en el puerto 5061.

    New-UMIPGateway -Name MyUMIPGateway -Address "MyUMIPGateway.contoso.com" -Port 5061

Este ejemplo crea una puerta de enlace IP de mensajería unificada denominada `MyUMIPGateway` e impide que la puerta de enlace IP de mensajería unificada acepte llamadas entrantes o envíe llamadas salientes, establece una dirección IPv6 y permite que la puerta de enlace IP de mensajería unificada use direcciones IPv4 e IPV6.

    New-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

