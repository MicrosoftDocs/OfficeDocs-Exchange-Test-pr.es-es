---
title: 'Configurar el puerto de escucha: Exchange 2013 Help'
TOCTitle: Configurar el puerto de escucha
ms:assetid: 200ecbd8-18c3-4594-9cc8-924b3ab4eca1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633457(v=EXCHG.150)
ms:contentKeyID: 50556748
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el puerto de escucha

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede configurar el puerto TCP que se usa para escuchar las solicitudes del Protocolo de inicio de sesión (SIP) en una puerta de enlace IP de mensajería unificada (MU). De manera predeterminada, cuando crea una puerta de enlace IP de MU, el número de puerto de escucha TCP de SIP se establece en 5060. El puerto de escucha TCP de SIP no puede configurarse mediante el uso del EAC. Debe configurar el número del puerto de escucha TCP de SIP con el cmdlet **Set-UMIPGateway**.

Es posible que deba configurar el número de puerto de escucha TCP en 5061 si desea:

  - Establecer la configuración de seguridad VoIP en un plan de marcado de MU en SIP protegida.

  - Establecer la seguridad VoIP en un plan de marcado de mensajería unificada en Protegido.

  - Integrar con MicrosoftOffice Communications Server 2007 R2 o Microsoft Lync Server.

  - Use la Seguridad de la capa de transporte mutua (TLS mutua) para cifrar los datos de red entre los servidores de Exchange y una puerta de enlace VoIP, una central de conmutación (PBX) con SIP habilitado, una IP PBX o un controlador de borde de sesión (SBC).

Si desea usar una TLS mutua entre una puerta de enlace IP de MU y un plan de marcado que opere en modo SIP protegida o Protegida, cuando crea la puerta de enlace IP de MU, debe configurarla con un nombre de dominio completo (FQDN) y, luego, usar el Shell para configurar la puerta de enlace IP de MU para que escuche el puerto TCP 5061. Asimismo, debe comprobar que las puertas de enlace VoIP, PBX habilitados para SIP, IP PBX y SBC también hayan sido configurados para escuchar las solicitudes mutuas de TLS en el puerto 5061.


> [!IMPORTANT]
> Cuando crea una puerta de enlace IP de MU mediante el uso de un FQDN, debe crear los registros HOST (A) adecuados en su zona de búsqueda directa de DNS. Si crea una puerta de enlace IP de mensajería unificada y usa un nombre de dominio completo (FQDN) y la configuración DNS para la puerta de enlace IP de mensajería unificada ha cambiado, deberá deshabilitar y, a continuación, habilitar la puerta de enlace IP de mensajería unificada para asegurarse de que la información de configuración de la puerta de enlace IP de mensajería unificada se actualiza correctamente.



Para otras tareas de administración relacionadas con puertas de enlace IP de mensajería unificada, consulte [Procedimientos de puerta de enlace IP de mensajería unificada](um-ip-gateway-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Puertas de enlace IP de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo este procedimiento, confirme que se haya creado una puerta de enlace IP de MU. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Shell para configurar el puerto de escucha TCP

En este ejemplo, se configura una puerta de enlace IP de MU denominada `MyUMIPGateway` que tiene un FQDN de mTLS.MyUMIPGateway.contoso.com y escucha solicitudes de SIP en el puerto TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address mTLS.MYUMIPGateway.contoso.com -Port 5061

En este ejemplo, se configura una puerta de enlace IP de MU denominada `MyUMIPGateway` que tiene un FQDN de SIPSecured.MyUMIPGateway.contoso.com y escucha solicitudes de SIP en el puerto TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address SIPSecured.MyUMIPGateway.contoso.com -Port 5061

En este ejemplo, se configura una puerta de enlace IP de MU denominada `MyUMIPGateway` que tiene un FQDN de MyOCSUMIPGateway.contoso.com y escucha solicitudes de SIP en el puerto TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address MyOCSUMIPGateway.contoso.com -Port 5061

