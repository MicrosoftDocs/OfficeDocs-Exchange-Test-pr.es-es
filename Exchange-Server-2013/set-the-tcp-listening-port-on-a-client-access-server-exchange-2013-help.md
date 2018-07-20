---
title: 'Establecer el puerto de escucha TCP en un servidor de acceso de cliente: Exchange 2013 Help'
TOCTitle: Establecer el puerto de escucha TCP en un servidor de acceso de cliente
ms:assetid: 5f48f21a-d8d4-48b2-868f-9a3647693841
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673530(v=EXCHG.150)
ms:contentKeyID: 50556793
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer el puerto de escucha TCP en un servidor de acceso de cliente

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-09_

Puede configurar el puerto TCP que se usa para atender las solicitudes de SIP en un servidor de acceso de cliente que ejecute el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange. De manera predeterminada, cuando se instala un servidor de acceso de cliente, el número de puerto de escucha TCP de SIP se establece en 5060 y el servidor de acceso de cliente inicia en modo TCP. El puerto de escucha TCP de SIP no puede configurarse mediante el uso del EAC. Debe configurar el número del puerto de escucha TCP de SIP con el cmdlet **Set-UMCallRouterSettings**.

Es posible que deba configurar el puerto de escucha TCP en 5061 si sus puertas de enlace VoIP, IP-PBX o el controlador de borde de sesión (SBC) están configurados para usar un puerto TCP diferente del puerto SIP 5060 estándar.

Solo puede configurar el servidor de acceso de cliente TCP y puertos TLS. No puede configurar los puertos para un servidor de buzones de correo de Exchange 2013. Sin embargo, puede usar el cmdlet **Set-UMService** para configurar los puertos de escucha TCP y TLS para los servidores de mensajería unificada de Exchange 2010.

Para consultar otras tareas relacionadas con la mensajería unificada y los servidores de acceso de clientes, vea [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servidor de acceso de cliente (servicio de enrutamiento de llamadas de mensajería unificada)" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que haya instalado correctamente los servidores de buzones y de acceso de cliente.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar el puerto de escucha TCP en un servidor de acceso de clientes

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor Exchange que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración del enrutador de llamadas de mensajería unificada**, en **Puerto de escucha TCP**, escriba el número del puerto TCP y haga clic en **Guardar**.

## Usar el Shell para configurar el puerto de escucha TCP en un servidor de acceso de clientes

En este ejemplo, se establece el puerto de escucha TCP en un servidor de acceso de clientes llamado `MyClientAccessServer` en 5566.

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTCPListeningPort 5566

