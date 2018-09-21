---
title: 'Conectar puerta enlace VoIP IP PBX o controlador borde sesión UM'
TOCTitle: Conectar una puerta de enlace VoIP, IP PBX o un controlador de borde de sesión a mensajería unificada
ms:assetid: a7cecf59-b93a-413b-bb88-29f2669ef2cf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124084(v=EXCHG.150)
ms:contentKeyID: 50556843
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectar una puerta de enlace VoIP, IP PBX o un controlador de borde de sesión a mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Debe configurar las puertas de enlace de voz sobre IP (VoIP) y las centrales de conmutación IP (PBX) correctamente cuando implemente la mensajería unificada (UM) en su organización. Si está implementando UM en un entorno híbrido, también necesitará configurar correctamente sus controladores de borde de sesión (SBC). Para hacer esto, necesita configurar la interfaz o interfaces de las puertas de enlace VoIP, IP PBX y SBC para comunicarse con los servidores de acceso de clientes que se ejecutan en el Servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange y con los servidores de buzones que se ejecutan en el Servicio de mensajería unificada de Microsoft Exchange.


> [!IMPORTANT]
> Si efectúa tareas administrativas en la puerta de enlace VoIP, IP PBX o SBC con un explorador web, las solicitudes de HTTP que se envían a través de la red no estarán cifradas. Si quiere aumentar el nivel de seguridad de las puertas de enlace VoIP, IP PBX o SBC de su red, use el protocolo de seguridad de Internet (IPsec) o la capa de sockets seguros (SSL) para proteger las credenciales administrativas y los datos que se transmiten por la red. Además, se recomienda usar un mecanismo de autenticación seguro y contraseñas administrativas complejas para proteger las credenciales administrativas del dispositivo.



## Interfaces de dispositivos de telefonía IP

Existen varios tipos de puertos o interfaces que debe configurar para permitir la comunicación entre una puerta de enlace VoIP, IP PBX o SBC y los servidores de acceso de cliente y de buzones de correo en su red. Al configurar una puerta de enlace VoIP, IP PBX o SBC, debe tener en cuenta si el dispositivo es analógico, digital, o analógico y digital.

Si la interfaz de puerta de enlace VoIP que se conecta a la PBX es analógica, deberá establecer la configuración adecuada correctamente para habilitar la comunicación de la puerta de enlace VoIP con los servidores de acceso de cliente y de buzones de correo. Para las IP PBX y SBC, también debe configurar correctamente la interfaz IP para habilitar estos dispositivos para comunicarse con los servidores de acceso de cliente y de buzones de correo. Todos estos dispositivos tienen diferentes tipos de conexiones o puertos que están disponibles en función del modelo o proveedor del dispositivo.

Para habilitar la comunicación con los servidores de acceso de cliente y de buzones de correo en su red:

  - Para las puertas de enlace VoIP, debe configurar las interfaces de telefonía para comunicarse con sus PBX, y debe configurar la interfaz IP del dispositivo.

  - Para IP PBX, debe configurar las conexiones de red basadas en circuito y las conexiones basadas en IP.

  - Para SBC, debe configurar ambas interfaces IP, una para la red y la otra interfaz que se conecta por Internet o una conexión WAN dedicada.

A continuación tiene una lista de recursos que se encuentran en Exchange TechCenter que proporcionan información que le puede ayudar a configurar sus puertas de enlace VoIP, IP PBX y SBC:

  - **Documentación de puertas de enlace IP, IP PBX y PBX compatibles**   [Asesor de telefonía para Exchange 2013](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013) incluye archivos de configuración e información de configuración que puede usar para configurar puertas de enlace VoIP, IP PBX, PBX y SBC.

  - **Configuración y notas técnicas**   [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways) incluye archivos de configuración e información de configuración que puede usar para configurar puertas de enlace VoIP, IP PBX y PBX.

  - **Notas de configuración para la mensajería unificada de Exchange en línea**   [Notas de configuración de los controladores de borde de sesión admitidos](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-session-border-controllers) incluye archivos de configuración e información de configuración que puede usar para configurar puertas de enlace SBC.

Los especialistas en mensajería unificada están disponibles para ayudarle a configurar sus dispositivos de red basados en IP y telefonía. Un especialista en mensajería unificada de Exchange puede garantizarle una transición sin problemas a la mensajería unificada desde un sistema de correo de voz de un tercero o heredado, o le ayudará a planear e implementar un nuevo sistema de correo de voz con mensajería unificada de Exchange. La implementación de un sistema de correo de voz nuevo o la actualización de uno heredado requiere amplios conocimientos sobre puertas de enlace VoIP, IP PBX, PBX y de mensajería unificada. Para obtener más información sobre cómo contactar con un especialista en mensajería unificada, consulte [Especialistas de mensajería unificada de Microsoft Exchange Server 2013](http://go.microsoft.com/fwlink/p/?linkid=262708) o partners de mensajería unificada certificados en [Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951).

Después de configurar una interfaz de puerta de enlace VolP, IP PBX o SBC IP, debe crear y configurar una puerta de enlace IP de mensajería unificada para representar los dispositivos que ha implementado. Para obtener más información sobre cómo crear una puerta de enlace IP de mensajería unificada, consulte [Cree una puerta de enlace IP de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway).

Después de crear una puerta de enlace IP de mensajería unificada, los servidores de buzones y de acceso de clientes asociados con la puerta de enlace IP de mensajería unificada envían una solicitud SIP OPTIONS a la puerta de enlace VoIP, IP PBX o SBC para garantizar que responde. Si la puerta de enlace VoIP, IP PBX o SBC no responde, el servidor de buzones registrará un evento con ID 1088 indicando que se ha producido un error en la solicitud. Para resolver este problema, asegúrese de que la puerta de enlace VoIP, IP PBX o SBC está disponible y en línea, y que la configuración de la mensajería unificada es correcta.

Un servidor de buzones y de acceso de clientes solo se comunicará con las puertas de enlace VoIP, IP PBX o SBC que figuren como homólogos de Protocolo de inicio de sesión (SIP) de confianza. Un evento con ID 1175 se registrará cuando varios hosts DNS compartan la misma dirección IP. Este evento puede producirse si se han configurado zonas DNS con nombres de dominio completos (FQDN) para las puertas de enlace VoIP en la red. La mensajería unificada protege de las solicitudes no autorizadas recuperando la dirección URL interna del directorio virtual de servicios web de mensajería unificada que se encuentra en el servidor de buzones y, luego, usando dicha dirección URL para crear una lista de FQDN para los homólogos SIP de confianza. Cuando dos FQDN se resuelven con la misma dirección IP, este evento se registra.


> [!NOTE]
> Debe reiniciar el servicio de mensajería unificada de MicrosoftExchange si se ha configurado una puerta de enlace VoIP, IP PBX o SBC de mensajería unificada para que use un FQDN y el registro DNS de la puerta de enlace VoIP, IP PBX o SBC de mensajería unificada ha cambiado después de iniciarse el servicio. Si no reinicia el servicio, el servidor de buzones no encontrará la puerta de enlace VoIP, IP PBX o SBC. Esto se debe a que los servidores de buzones mantienen una memoria caché para todas las puertas de enlace VoIP, IP PBX o SBC que haya en memoria y la resolución de DNS solo se realiza cuando se reinicia el servicio o cuando cambia la configuración de una puerta de enlace VoIP, IP PBX o SBC.


