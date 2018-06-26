---
title: 'Configuración de la dirección IP: Exchange 2013 Help'
TOCTitle: Configuración de la dirección IP
ms:assetid: 100541c1-2297-4c46-9602-b304736541a8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb266940(v=EXCHG.150)
ms:contentKeyID: 49895472
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuración de la dirección IP

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-11_

Antes de crear una puerta de enlace IP de mensajería unificada, debe definir un conjunto de direcciones IP o el nombre de dominio completo (FQDN) configurado en la puerta de enlace IP, IP PBX o el controlador de borde de sesión (SBC) que esté usando. Entonces, al crear la puerta de enlace IP de mensajería unificada, establezca la dirección IP de FQDN. Puede cambiar la dirección IP o el FQDN posteriormente.

Puede configurar la dirección IP o el FQDN con el EAC o el Shell. En el Centro de administración de Exchange, el cuadro **Dirección**, en la página **Puerta de enlace IP de MU** puede aceptar una dirección IP IPv4, una dirección IPv6 o un FQDN. También puede usar el parámetro *Address* en el cmdlet **Set-UMIPGateway** en el Shell para establecer una dirección IP IPv4, una dirección IPv6 o un FQDN. Si crea una puerta de enlace IP de mensajería unificada con un FQDN, debe crear los registros HOST A en su zona de búsqueda directa DNS. Si la configuración DNS de la puerta de enlace IP de MU se modifica, debe deshabilitar y habilitar la puerta de enlace IP de MU para garantizar que su información de configuración se actualice correctamente.

Para otras tareas de administración relacionadas con puertas de enlace IP de mensajería unificada, consulte [Procedimientos de puerta de enlace IP de mensajería unificada](um-ip-gateway-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Puertas de enlace IP de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una puerta de enlace IP de mensajería unificada. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para configurar la dirección IP en una puerta de enlace IP de mensajería unificada

1.  En la EAC, vaya a **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada**, seleccione la puerta de enlace IP de mensajería unificada que quiere modificar y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Puerta de enlace IP de MU**, en **Dirección**, escriba la dirección IP de la puerta de enlace VoIP, la IP PBX, o el controlador de borde de sesión (SBC).

3.  Haga clic en **Guardar** para guardar los cambios.


> [!IMPORTANT]
> Si usa un nombre de dominio completo en lugar de una dirección IP en la puerta de enlace IP de mensajería unificada, compruebe que se han creado los registros DNS correctos.



## Uso del Shell para configurar la dirección IP en una puerta de enlace IP de mensajería unificada

Este ejemplo configura una puerta de enlace IP de mensajería unificada denominada `MyUMIPGateway` con una dirección IP de 10.10.10.1.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

Este ejemplo configura una puerta de enlace IP de mensajería unificada denominada `MyUMIPGateway` con una dirección IP de 10.10.10.1 y escucha solicitudes SIP en el puerto TCP 5060.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.10 -Port 5061

En este ejemplo se impide que la puerta de enlace IP de mensajería unificada llamada `MyUMIPGateway` acepte llamadas entrantes y salientes, se establece una dirección IPv6 y se permite que la puerta de enlace IP de mensajería unificada utilice las direcciones IPv4 e IPv6.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

