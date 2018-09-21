---
title: 'Conectar puerta de enlace VoIP para comunicarse con PBX: Exchange 2013 Help'
TOCTitle: Conectar una puerta de enlace VoIP para comunicarse con una PBX
ms:assetid: 76bcdc54-3ec2-408a-bdbe-37826580dd62
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998872(v=EXCHG.150)
ms:contentKeyID: 50556820
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectar una puerta de enlace VoIP para comunicarse con una PBX

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-15_

Al configurar sus redes de datos y de telefonía para la mensajería unificada en Microsoft Exchange Server 2013, debe configurar las puertas de enlace VoIP para que se comuniquen con los servidores de acceso de cliente que se ejecutan en el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange y los servidores de buzones de correo que ejecutan el servicio de mensajería unificada de Microsoft Exchange. También debe configurar las puertas de enlace VolP para que se comuniquen con las centrales de conmutación (PBX) de la organización. Puede usar la información y los vínculos de este tema para configurar una puerta de enlace VolP para que se comunique con una PBX.

## Configurar una puerta de enlace VoIP

Al configurar una puerta de enlace VolP, debe tener en cuenta si el dispositivo de puerta de enlace VolP es analógico, digital, o analógico y digital. Si la interfaz de puerta de enlace VolP que se conecta a la PBX es analógica, deberá establecer correctamente la configuración para habilitar la comunicación de la puerta de enlace VolP con una central de conmutación. Si la interfaz de puerta de enlace VolP que se conecta a la PBX es digital, podría no necesitar ninguna configuración adicional para habilitar la comunicación de la interfaz digital con una central de conmutación.

Los siguientes sumergimientos de recursos en Exchange TechCenter proporcionan información que puede ayudarle a configurar correctamente sus puertas de enlace VoIP y PBXs:

  - **Documentación de puertas de enlace VoIP, IP PBX y PBX compatibles**   [Asesor de telefonía para Exchange 2013](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013) incluye archivos de configuración e información de configuración que puede usar para configurar puertas de enlace VoIP y PBXs.

  - **Configuración y notas técnicas**   [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways) incluye archivos de configuración e información de configuración que puede usar para configurar puertas de enlace VoIP y PBXs.

  - **Configuración de una puerta de enlace VolP basada en AudioCodes**  En la [página de recursos del servidor Microsoft Exchange](https://www.audiocodes.com/solutions/microsoft/exchange-server) encontrará la información de configuración y de soporte más reciente que le ayudará a configurar puertas de enlace VolP basadas en AudioCodes para usar con mensajería unificada.

  - **Configuración de una puerta de enlace VoIP basada en Dialogic** El [sitio web de Dialogic](https://www.dialogic.com/) proporciona la información de configuración y soporte más reciente para puertas de enlace VoIP basadas en Dialogic.

Recomendamos a todos los clientes que planean implementar la mensajería unificada que consigan la ayuda de un especialista en la materia. Un especialista en mensajería unificada de Exchange ayudará a garantizarle una actualización sin problemas a la mensajería unificada desde un sistema de correo de voz de un tercero o heredado y le ayudará a planificar e implementar un nuevo sistema de correo de voz con mensajería unificada de Exchange. La implementación de un sistema de correo de voz nuevo o la actualización de uno de heredado requiere amplios conocimientos sobre puertas de enlace VoIP, PBX y de mensajería unificada. Para obtener más información acerca de cómo contactar con un especialista en mensajería unificada, consulte [Especialistas de mensajería unificada de Microsoft Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=262708) o partners de mensajería unificada certificados en [Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951).

## Más información

[Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)

[Conectar la mensajería unificada a una puerta de enlace VoIP compatible](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)

