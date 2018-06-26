---
title: 'Probar la conectividad de Mensajería unificada con puertas de enlace VoIP y PBX: Exchange 2013 Help'
TOCTitle: Probar la conectividad de Mensajería unificada con puertas de enlace VoIP y PBX
ms:assetid: 2aca8631-a99a-4e29-aff0-e462385f03b2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996906(v=EXCHG.150)
ms:contentKeyID: 56271497
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Probar la conectividad de Mensajería unificada con puertas de enlace VoIP y PBX

 

_**Se aplica a:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2014-09-17_

Puede probar el funcionamiento de Mensajería unificada (UM) y los equipos de telefonía relacionados que estén conectados. Al realizar el siguiente procedimiento, el servidor de acceso de cliente y de buzones comprueba el funcionamiento de un extremo a otro del sistema de correo de voz. Esto incluye los componentes de telefonía conectados a los servidores de acceso de cliente y de buzones, incluidas las puertas de enlace VoIP, las centrales de conmutación (PBX), las PBX IP y el cableado.

Para obtener información sobre otras tareas de administración relacionadas con la solución de problemas de Mensajería unificada, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas \&quot;Servidor de buzones (servicio de Mensajería unificada)\&quot; y \&quot;Servidor de acceso de cliente (servicio enrutador de llamadas de Mensajería unificada)\&quot; del tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Para realizar los siguientes procedimientos, debe iniciar sesión en el servidor de buzones con una cuenta que sea miembro del grupo de administradores locales.

  - Compruebe que el servidor de buzones está instalado. No importa si está instalado en el mismo PC que el servidor de acceso de cliente o en otro distinto.

  - Compruebe que el servidor de acceso de cliente está instalado. No importa si está instalado en el mismo PC que el servidor de buzones o en otro distinto.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para comprobar el funcionamiento de la Mensajería unificada y los componentes de telefonía

En este ejemplo, se comprueba la capacidad de la puerta de enlace IP de MU para escuchar en el puerto TCP 5060 solicitudes SIP entrantes.

    Test-UMConnectivity -ListenPort 5060 -UMIPGateway MyIPGateway

En este ejemplo, se comprueba la capacidad del servidor de buzones local para usar una conexión de TCP no segura en lugar de una conexión de TLS mutua segura para realizar una llamada a través de una puerta de enlace IP de Mensajería unificada llamada `MyUMIPGateway` con el número de teléfono 56780.

    Test-UMConnectivity -UMIPGateway MyUMIPGateway -Phone 56780 -Secured $false

En este ejemplo, se comprueba el número de Outlook Voice Access en un plan de marcado con el URI de SIP. Este ejemplo se puede usar en un entorno que incluya Lync Server.

    Test-UMConnectivity -UMIPGateway OCSGateway1 -Phone "sip:SIPdialplan.contoso.com@contoso.com"


> [!NOTE]
> Puede establecer el parámetro <CODE>-Timeout</CODE> con un valor menor que 5 segundos. Sin embargo, es recomendable que siempre configure este parámetro con un valor de 5 segundos o más. Use el modo 2 cuando, en la sintaxis de línea de comandos se especifique el parámetro <CODE>&shy;UMIPGateway</CODE>.


