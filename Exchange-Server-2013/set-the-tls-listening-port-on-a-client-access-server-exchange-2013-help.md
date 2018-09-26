---
title: 'Configurar puerto escucha TLS en servidor acceso cliente: Exchange 2013 Help'
TOCTitle: Configurar el puerto de escucha TLS en un servidor de acceso de cliente
ms:assetid: f4401923-61fa-4dc5-95f8-c0d2f515b2ea
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673576(v=EXCHG.150)
ms:contentKeyID: 50556910
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el puerto de escucha TLS en un servidor de acceso de cliente

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-17_

Puede configurar el puerto de Seguridad de la capa de transporte (TLS) que se usa para escuchar solicitudes SIP en un servidor de acceso de cliente que ejecute el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange. De manera predeterminada, al instalar un servidor de acceso de cliente, el número de puerto de escucha SIP TLS se establece en 5061.

Puede que tenga que configurar el puerto de escucha TLS en 5061 si desea:

  - Establecer la configuración de seguridad VoIP de un plan de marcado de mensajería unificada en SIP seguro.

  - Establecer la configuración de seguridad VoIP de un plan de marcado de mensajería unificada en Seguro.

  - Integrar en MicrosoftOffice Communications Server 2007 R2 o Microsoft Lync Server.

  - Usar la Seguridad de la capa de transporte mutua (TLS mutua) para cifrar los datos de red entre los servidores de acceso de cliente, los servidores de buzones de correo que ejecuten el servicio de mensajería unificada de Microsoft Exchange y las puertas de enlace VoIP, centrales de conmutación (PBX) habilitadas para el Protocolo de inicio de sesión (SIP), IP PBX o controladores de borde de sesión (SBC).

Si desea usar una TLS mutua entre una puerta de enlace IP de mensajería unificada y un plan de marcado que opere en modo seguro SIP o en modo seguro, cuando crea la puerta de enlace IP de mensajería unificada, debe configurarla con un nombre de dominio completo (FQDN) y, a continuación, configurarla para que escuche el puerto TLS 5061. Asimismo, debe comprobar que las puertas de enlace VoIP, PBX habilitadas para SIP, IP PBX y SBC también se hayan configurado para escuchar las solicitudes de TLS mutua en el puerto 5061.

Solo puede configurar los puertos TCP y TLS del servidor de acceso de cliente. No puede configurar los puertos de un servidor de buzones de correo de Exchange 2013. Sin embargo, puede usar el cmdlet **Set-UMService** para configurar los puertos de escucha TCP y TLS para los servidores de mensajería unificada de Exchange 2010.

Para consultar otras tareas relacionadas con la mensajería unificada y los servidores de acceso de clientes, vea [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servidor de acceso de cliente (servicio de enrutamiento de llamadas de mensajería unificada)" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que ha instalado correctamente los servidores de buzones y de acceso de clientes.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar el puerto de escucha TLS en un servidor de acceso de cliente

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor Exchange que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración del servicio de mensajería unificada**, en **Puerto de escucha TLS**, escriba el número del puerto TLS y, a continuación, haga clic en **Guardar**.

## Usar el Shell para configurar el puerto de escucha TLS en un servidor de acceso de cliente

En este ejemplo se establece el puerto de escucha TLS en un servidor de acceso de cliente denominado `MyClientAccessServer` en 5561.

```powershell
Set-UMCallRouterSettings -Server MyClientAccessServer -SipTlsListeningPort 5561
```

