---
title: 'Servicios de mensajería unificada: Exchange 2013 Help'
TOCTitle: Servicios de mensajería unificada
ms:assetid: f36835f2-1e5f-4e5a-88bc-0672af1e3498
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125191(v=EXCHG.150)
ms:contentKeyID: 50556911
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Servicios de mensajería unificada

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-18_

Los servidores de acceso de cliente que ejecutan el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange y los servidores de buzones que ejecutan el servicio de mensajería unificada de Microsoft Exchange permiten implementar la mensajería unificada (UM) y la funcionalidad de correo de voz para los usuarios de una organización.

¿Está buscando tareas de administración relacionadas con los servicios de mensajería unificada? Consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

**Contenido**

Client Access and Mailbox servers

Server configuration settings

Server operation

## Servidores Acceso de cliente y de Buzón de correo

En Exchange 2013, los roles del servidor de Exchange 2007 y Exchange 2010 se combinan para formar dos tipos de servidores, y todos los componentes o servicios de dichos roles del servidor se ejecutan en el mismo servidor físico o en dos servidores separados denominados buzones de acceso de cliente y buzones de correo.

En este nuevo modelo, el servidor de acceso de cliente es responsable de la Detección automática, la Capa de sockets seguros (SSL), la autenticación, la redirección y las conexiones proxy. El servidor de acceso de cliente representa el punto de entrada para las llamadas entrantes o solicitudes del Protocolo de inicio de sesión (SIP) para la mensajería unificada. La lógica de enrutamiento y SIP REDIRECT se implementan como un servicio que se incluye de forma automática en un servidor de acceso de cliente. Este servicio se conoce como Enrutador de llamadas de mensajería unificada de Microsoft Exchange. Se ejecuta en todos los servidores de acceso de cliente de la organización.

Cuando un servidor de acceso de clientes recibe un SIP INVITE para una llamada entrante, el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange redirige la llamada entrante al servidor de buzones. Después, se crea un canal de medios (RTP o SRTP) entre la puerta de enlace VoIP, PBX IP o el controlador de borde de sesión (SBC) y el servidor de buzones que hospeda el buzón del usuario. Aunque el servidor de acceso de clientes actúa como un redirector SIP, solo administra las solicitudes SIP de puertas de enlace VoIP, PBX IP o SBC. No recibe tráfico de medios. El tráfico de medios que usa RTP o SRTP solo se pasa entre el servidor de buzones y los interlocutores SIP, como puertas de enlace VoIP, PBX IP o SBC. Al implementar Exchange 2013 y la mensajería unificada, es necesario configurar las puertas de enlace VoIP, la PBX IP o los SBC para que apunten a los servidores de acceso de clientes que instaló a fin de que las llamadas entrantes se enruten correctamente para la mensajería unificada.

En Exchange 2013, el servidor de buzones controla los mismos procesos que el rol del servidor Mensajería unificada administraba en Exchange 2007 y en Exchange 2010. El servidor de buzones ejecuta el servicio de mensajería unificada de Microsoft Exchange y los procesos de trabajo de mensajería unificada.

Cuando se instalan servidores de acceso de cliente o de buzones y se implementa la mensajería unificada, no es necesario asociar ni agregar servidores de acceso de cliente ni de buzones a los planes de marcado de mensajería unificada. Los servidores de acceso de cliente y de buzones responden todas las llamadas entrantes y, a continuación, usan los planes de marcado de mensajería unificada para buscar usuarios.

No obstante, si va a integrar la mensajería unificada en Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server, los servidores Lync y el servidor de buzones controlan tanto el SIP como los canales de medios RTP y SRTP para las llamadas entrantes. En un entorno integrado con Lync no hay puertas de enlace VoIP, PBX IP ni SBC. Para Lync, el servidor de buzones que se ejecuta en el servicio de mensajería unificada de Microsoft Exchange actúa como un servidor de mensajería unificada de Exchange 2010. El servidor de buzones y el servidor de acceso de cliente se consideran homólogos de confianza porque ambos se deben agregar a un plan de marcado SIP. Lync enruta la llamada entrante mediante el componente de enrutamiento de entrada, que usa SIP para comunicarse con el servidor de acceso de clientes y, a continuación, enruta la llamada a un servidor de buzones.

Volver al principio

## Opciones de configuración del servidor

En Exchange 2013, todos los componentes de mensajería unificada y los valores de configuración que se aplican a un solo equipo que ejecuta el rol del servidor Mensajería unificada en Exchange 2010 aún estarán disponibles. No obstante, algunos de esos componentes y valores de configuración se encuentran en un servidor de acceso de cliente y otros, en un servidor de buzones. En algunos casos, la misma configuración está disponible en ambos. En la siguiente lista se muestran los parámetros y la configuración disponible en un servidor de acceso de clientes y en un servidor de buzones.

  - \[-DialPlans \<MultiValuedProperty\>\]

  - \[-MaxCallsAllowed \<Int32\>\]

  - \[-SipTcpListeningPort \<Int32\>\]

  - \[-SipTlsListeningPort \<Int32\>\]

  - \[-Status \<Enabled | Disabled | NoNewCalls\>\]

  - \[-UMStartupMode \<TCP | TLS | Dual\>\]

En los servidores de buzones se usan los cmdlets **Set-UMService**, **Get-UMService**, **Enable-UMService** y **Disable-UMService** para ver o configurar las propiedades de mensajería unificada del servicio de mensajería unificada de Microsoft Exchange. Para ver o configurar las propiedades del servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange en un servidor de acceso de cliente, se usa un conjunto distinto de cmdlets: **Set-UMCallRouterSettings** y **Get-UMCallRouterSettings**. Esto garantiza que los cmdlets **Get-UMServer**, **Set-UMServer**, **Enable-UMServer** y **Disable-UMServer** existentes de Exchange 2007 y de Exchange 2010 funcionen en una implementación de coexistencia con los servidores de buzones de Exchange 2013. Esto también garantiza que los cmdlets funcionen cuando los servidores de buzones y de acceso de cliente se instalen en el mismo equipo o en equipos diferentes.

Volver al principio

## Operación del servidor

Cuando se instalan servidores de acceso de cliente y de buzones, se habilitan automáticamente para que puedan responder las llamadas de voz entrantes y salientes, y para que enruten los mensajes de correo de voz a los destinatarios adecuados en la organización de Exchange.

Puede permitir que el servicio de mensajería unificada de Microsoft Exchange en un servidor de buzones o el servicio de enrutamiento de llamadas de mensajería unificada de Microsoft Exchange en un servidor de acceso de cliente respondan las llamadas nuevas, o bien puede impedir que lo hagan. De manera predeterminada, un servidor de buzones o de acceso de cliente se encuentra en estado habilitado después de instalarse. Cuando se establece el servidor de buzones o de acceso de cliente para aceptar llamadas de voz, de fax, de operador automático o de Outlook Voice Access entrantes, se usa el cmdlet **Set-ServerComponentState**.

La configuración del modo de mantenimiento para un servidor de buzones o de acceso de cliente de Exchange 2013 permite dejar el servidor fuera de servicio. Para un servidor de buzones, "fuera de servicio" significa que el servidor no hospedará ninguna base de datos activa, todas las colas de transporte estarán vacías y el servidor no aceptará llamadas entrantes de servidores de acceso de cliente, puertas de enlace VoIP, IP PBX, PBX habilitadas para SIP o SBC. Para un servidor de acceso de cliente, "fuera de servicio" significa que el servidor no aceptará llamadas entrantes de puertas de enlace VoIP, IP PBX, PBX habilitadas para SIP o SBC.

En Exchange 2007 y en Exchange 2010, existe un parámetro de estado que permite controlar el estado operativo de un servidor de mensajería unificada. En cambio, en Exchange 2013, no hay ningún parámetro de estado disponible para ese fin en el cmdlet **Set-UMService** para un servidor de buzones o en el cmdlet **Set-UMCallRouterSettings** para un servidor de acceso de cliente.

Aunque los servidores de acceso de cliente y de buzones se habilitan cuando se instalan, ninguno de ellos puede procesar ni enrutar correctamente las llamadas entrantes a los usuarios habilitados para mensajería unificada hasta que se vincule un plan de marcado de mensajería unificada con, al menos, una puerta de enlace IP de mensajería unificada.

Después de vincular un plan de marcado a una puerta de enlace IP de mensajería unificada, los servidores de buzones y de acceso de cliente buscan todas las puertas de enlace IP de mensajería unificada asociadas al plan de marcado de mensajería unificada y las puertas de enlace VoIP, IP PBX y SBC. Para detectar e identificar cualquier cambio en la configuración en los planes de marcado de mensajería unificada o en las puertas de enlace IP de mensajería unificada, los servidores de acceso de cliente o de buzones comprueban la configuración cada 10 minutos.

Si la puerta de enlace IP de mensajería unificada detecta algún cambio en la configuración, el servidor de acceso de cliente o de buzones reacciona en consecuencia, y bien comienza a usar la puerta de enlace VoIP, IP PBX o SBC correspondiente, o deja de hacerlo. Una vez que los servidores de acceso de cliente y de buzones responden las llamadas entrantes para los usuarios vinculados a un plan de marcado de mensajería unificada y se comunican correctamente con las puertas de enlace VoIP, IP PBX o SBC, puede ejecutar un conjunto de operaciones de diagnóstico para comprobar que funcionan bien y que la conectividad entre los servidores Exchange y las puertas de enlace VoIP, IP PBX o SBC es correcta.

Volver al principio

