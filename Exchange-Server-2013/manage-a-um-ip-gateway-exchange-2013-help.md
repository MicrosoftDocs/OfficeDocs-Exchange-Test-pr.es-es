---
title: 'Administrar una puerta de enlace IP de mensajería unificada: Exchange 2013 Help'
TOCTitle: Administrar una puerta de enlace IP de mensajería unificada
ms:assetid: 387e540f-8c59-42d2-a423-99fcf97e00aa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997283(v=EXCHG.150)
ms:contentKeyID: 49895571
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMIPGatewayGeneralPropertyPageControl
ms.translationtype: MT
---

# Administrar una puerta de enlace IP de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-21_

Después de crear una puerta de enlace IP de mensajería unificada (MU), puede ver o configurar diversas opciones. Por ejemplo, puede configurar la dirección IP o un nombre de dominio completo (FQDN), configurar las opciones de llamadas salientes y habilitar o deshabilitar el indicador de mensaje en espera.

Para otras tareas de administración relacionadas con puertas de enlace IP de mensajería unificada, consulte [Procedimientos de puerta de enlace IP de mensajería unificada](um-ip-gateway-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Puertas de enlace IP de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una puerta de enlace IP de mensajería unificada. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para ver o configurar las propiedades de la puerta de enlace IP de MU

1.  En el EAC, vaya a **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada**. En la vista de lista, seleccione la puerta de enlace IP de mensajería unificada que desee administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  
    
    Use la página **Puerta de enlace IP de la mensajería unificada** para ver y configurar las opciones de la puerta de enlace IP de mensajería unificada. Se pueden ver o configurar las siguientes opciones:
    
      - **Estado**   Este campo de sólo lectura muestra el estado de la puerta de enlace IP de MU.
    
      - **Nombre**   Use esta casilla para especificar un nombre exclusivo para la puerta de enlace IP de mensajería unificada. Se trata de un nombre para mostrar que aparecerá en la Consola de administración de Exchange. Si debe cambiar el nombre para mostrar de la puerta de enlace IP de mensajería unificada una vez creada, primero debe eliminar la puerta de enlace IP de mensajería unificada existente y, a continuación, crear otra puerta de enlace IP de mensajería unificada con el nombre adecuado. El nombre de puerta de enlace IP de mensajería unificada es necesario, pero solo se usa para su visualización. Como la organización puede usar varias puertas de enlace IP de mensajería unificada, es recomendable el uso de nombres significativos para designar las puertas de enlace IP de mensajería unificada. La longitud máxima que puede tener un nombre de puerta de enlace IP de mensajería unificada es de 64 caracteres y puede incluir espacios.
    
      - **Dirección**   Puede configurar una puerta de enlace IP de mensajería unificada con una dirección IP o un nombre de dominio completo (FQDN). Use este cuadro para indicar la dirección IP o FQDN configurada en la puerta de enlace VoIP, un PBX habilitado para SIP, un IP PBX o un SBC.
        
        Puede escribir caracteres alfabéticos y numéricos en este cuadro. Se admiten direcciones IPv4, IPv6 y FQDN. Si se usa un FQDN, también debe asegurarse de que se haya configurado correctamente un registro de host DNS para la puerta de enlace VoIP, de modo que el nombre del host se resuelva correctamente en una dirección IP. Asimismo, si utiliza un FQDN en lugar de una dirección IP, y se modifica la configuración de DNS para la puerta de enlace IP de mensajería unificada, deberá deshabilitar la puerta de enlace IP de mensajería unificada y habilitarla después para asegurarse de que la información de configuración de dicha puerta de enlace se actualiza correctamente.
        
        Si desea usar una Seguridad de la capa de transporte mutua (TLS mutua) entre una puerta de enlace IP de mensajería unificada y un plan de marcado funcionando en modo SIP protegido o modo protegido, debe configurar la puerta de enlace IP de mensajería unificada con un FQDN. También debe configurarla para que escuche en el puerto 5061 y verifique si también se configuraron puertas de enlace IP o IP PBX para escuchar las solicitudes TLS mutuas en el puerto 5061. Para configurar una puerta de enlace IP de mensajería unificada, ejecute el siguiente comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
    
      - **Permitir llamadas salientes a través de esta puerta de enlace IP de MU**   Seleccione esta casilla para permitir que la puerta de enlace IP de MU acepte y procese llamadas salientes. Esta opción no afecta las transferencias de llamadas ni las llamadas entrantes de una puerta de enlace VoIP.
        
        De forma predeterminada, cuando se crea una puerta de enlace IP de MU, esta opción está habilitada. Si se deshabilita esta opción, los usuarios asociados con el plan de marcado no podrán realizar llamadas salientes a través de la puerta de enlace VoIP, el IP PBX o el SBC definido en el campo **Dirección**.
    
      - **Permitir indicador de mensaje en espera**    Seleccione esta casilla a fin de permitir el envío de notificaciones por correo de voz a usuarios para las llamadas tomadas por la puerta de enlace IP de mensajería unificada. Esta opción permite a la puerta de enlace IP de MU recibir y enviar mensajes de notificación de SIP para los usuarios. Esta configuración está habilitada de forma predeterminada y permite el envío de notificaciones de mensajes en espera a los usuarios.
        
        El indicador de mensaje en espera puede hacer referencia a cualquier mecanismo que indica la existencia de un mensaje nuevo o no escuchado. La indicación de que se ha recibido un nuevo mensaje de voz puede encontrarse en la bandeja de entrada de clientes, como Outlook y Outlook Web App. Puede ser un servicio de mensajes cortos (SMS) o mensaje de texto enviado a un teléfono móvil registrado, una llamada saliente realizada desde un servidor de Exchange a un número preconfigurado o una lámpara encendida en un teléfono de escritorio de un usuario.

## Usar el Shell para configurar las propiedades de la puerta de enlace IP de MU

Este ejemplo modifica la dirección IP de una puerta de enlace IP de MU denominada `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

Este ejemplo impide que la puerta de enlace IP de mensajería unificada denominada `MyUMIPGateway` acepte llamadas entrantes, además de impedir llamadas salientes.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com -Status 2 -OutcallsAllowed $false

Este ejemplo permite que la puerta de enlace IP de mensajería unificada funcione como simulador de puerta de enlace VoIP y se pueda usar con el cmdlet **Test-UMConnectivity**.

    Set-UMIPGateway -Identity MyUMIPGateway -Simulator $true


> [!IMPORTANT]
> Hay un período de latencia antes de que todos los cambios realizados en la configuración de una puerta de enlace IP de UM se repliquen en todos los servidores de Exchange que se encuentran en el mismo plan de marcado de UM que la puerta de enlace IP de UM.



En este ejemplo se impide que la puerta de enlace IP de mensajería unificada llamada `MyUMIPGateway` acepte llamadas entrantes y evita las llamadas salientes, se establece una dirección IPv6 y se permite que la puerta de enlace IP de mensajería unificada utilice las direcciones IPv4 e IPv6.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## Usar el Shell para ver las propiedades de la puerta de enlace IP de MU

En este ejemplo, se muestra una lista con formato de todas las puertas de enlace IP de MU del bosque de Active Directory.

    Get-UMIPGateway |Format-List

En este ejemplo se muestran las propiedades de una puerta de enlace IP de mensajería unificada denominada `MyUMIPGateway`.

    Get-UMIPGateway -Identity MyUMIPGateway

En este ejemplo se muestran todas las puertas de enlace VoIP de mensajería unificada, incluidos los simuladores de puerta de enlace IP del bosque Active Directory.

    Get-UMIPGateway -IncludeSimulator $true

