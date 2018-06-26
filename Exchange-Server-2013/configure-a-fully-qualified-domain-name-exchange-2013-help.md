---
title: 'Configurar un nombre de dominio completo: Exchange 2013 Help'
TOCTitle: Configurar un nombre de dominio completo
ms:assetid: af093f87-59b7-44a8-a9a2-8f17f0cc7db8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423553(v=EXCHG.150)
ms:contentKeyID: 49895838
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar un nombre de dominio completo

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-09_

Puede configurar una puerta de enlace IP de mensajería unificada (MU) con una dirección IP o un nombre de dominio completo (FQDN). Al crear una puerta de enlace IP de mensajería unificada, debe definir la dirección IP o el FQDN configurado en la puerta de enlace VoIP, IP PBX o controlador de borde de sesión (SBC) que está utilizando. Puede cambiar la dirección IP o el FQDN después de haber creado la puerta de enlace IP de mensajería unificada.

Si crea una puerta de enlace IP de mensajería unificada mediante el uso de un FQDN, debe crear los registros HOST (A) adecuados en su zona de búsqueda directa de DNS. Si crea una puerta de enlace IP de mensajería unificada y usa un nombre de dominio completo (FQDN) y la configuración DNS para la puerta de enlace IP de mensajería unificada ha cambiado, deberá deshabilitar y, a continuación, habilitar la puerta de enlace IP de mensajería unificada para asegurarse de que la información de su configuración se actualiza correctamente.

Si desea usar una Seguridad de la capa de transporte mutua (TLS mutua) entre una puerta de enlace IP de mensajería unificada y un plan de marcado funcionando en modo SIP protegido o modo protegido, debe configurar la puerta de enlace IP de mensajería unificada con un FQDN. También debe configurarla para que escuche en el puerto 5061 y compruebe si también se configuraron las puertas de enlace VoIP, IP PBX o SBC para escuchar las solicitudes TLS mutuas en el puerto 5061. Para configurar una puerta de enlace IP de mensajería unificada, ejecute el siguiente comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.

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

## Usar el EAC para configurar un FQDN

1.  En la EAC, vaya a **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada**, seleccione la puerta de enlace IP de mensajería unificada que quiere modificar y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Puerta de enlace IP de mensajería unificada**, en **Direcciones**, ingrese el FQDN para la puerta de enlace VoIP, un PBX habilitado para SIP, IP PBX o SBC.

3.  Haga clic en **Guardar**.


> [!IMPORTANT]
> Si usa un FQDN en lugar de una dirección IP en la puerta de enlace IP de mensajería unificada, compruebe que se han creado los registros DNS correctos.



## Usar el Shell para configurar un FQDN

En este ejemplo, se configura una puerta de enlace IP de mensajería unificada denominada `MyUMIPGateway` con un FQDN denominado voipgateway.contoso.com.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com

En este ejemplo, se configura una puerta de enlace IP de mensajería unificada denominada `MySBC` con FQDN de sbc.contoso.com y escucha solicitudes SIP en el puerto TCP 5061.

    Set-UMIPGateway -Identity MySBC -Address sbc.contoso.com -Port 5061

