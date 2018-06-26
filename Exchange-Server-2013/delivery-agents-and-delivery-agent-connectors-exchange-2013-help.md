---
title: 'Agentes de entrega y conectores de agentes de entrega: Exchange 2013 Help'
TOCTitle: Agentes de entrega y conectores de agentes de entrega
ms:assetid: 38c942ee-b59d-47ec-87eb-bebad441ada5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638118(v=EXCHG.150)
ms:contentKeyID: 49895572
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agentes de entrega y conectores de agentes de entrega

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Un agente de entrega puede entregar mensajes desde el entorno de su servidor Exchange SMTP a un sistema que no use el protocolo SMTP. Cada agente de entrega está asociado a un conector de agente de entrega, que pone en cola a los mensajes enrutados al agente de entrega para el procesamiento y la entrega al dispositivo o sistema no SMTP.


> [!TIP]
> Cuando la arquitectura del conector externo permanece en Microsoft Exchange&nbsp;2013, recomendamos que, en lo posible, use agentes de entrega para enrutar mensajes a sistemas que no sean SMTP. Las razones principales de esto es que puede usar la administración de la cola para mensajes, sin necesidad de administrar la transferencia de archivos a un directorio de destino, y puede comprobar la entrega de los mensajes.



**Contenido**

Características y beneficios de los agentes de entrega

Agregar agentes de entrega a la organización

Conectores de agente de entrega

El conector de agente de entrega de mensajería de texto predeterminado

## Características y beneficios de los agentes de entrega

Un agente de entrega es un componente instalado en el servicio de transporte de un servidor de buzones de correo que puede realizar las siguientes tareas:

  - Establecer una conexión al sistema externo para la entrega de mensajes.

  - Recuperar mensajes de las colas de entrega de los servidores de buzones de correo.

  - Enviar mensajes al sistema externo.

  - Proporcionar confirmación para cada entrega de mensajes correcta.

Cuando la arquitectura del conector externo permanece en Microsoft Exchange Server 2013, recomendamos que, en lo posible, use agentes de entrega para enrutar mensajes a sistemas que no sean SMTP. Los agentes de entrega proporcionan las siguientes ventajas:

  - Permiten la administración de colas de mensajes enrutados a sistemas externos.

  - Debido a que ya no es necesario escribir o leer los mensajes desde el sistema de archivos, se mejora el rendimiento de entrega de mensajes.

  - Proporcionan acceso a propiedades del mensaje con eventos enriquecidos para desarrolladores de agentes.

  - El tiempo de rendimiento de un agente de entrega es más rápido que la implementación de un conector externo debido a que el agente de entrega puede usar las funciones de representación y administración de mensajes de Exchange.

  - Puede comprobar que los mensajes se entreguen al sistema externo, en vez de escribir simplemente al directorio de destino.

  - El uso de los conectores de agentes de entrega permite el análisis del contrato de nivel de servicio (SLA), ya que ahora es posible realizar el seguimiento de la entrega de mensajes al sistema externo.

## Agregar agentes de entrega a la organización

Para usar un agente de entrega en la organización, deberá cumplir con los siguientes requisitos:

1.  Adquirir el agente de entrega. Normalmente, los agentes de entrega son escritos por terceros. Exchange 2013 incluye solo un conector de agente de entrega de forma predeterminada: el conector de agente de entrega de mensajería de texto.

2.  Instalar el agente de entrega en los servidores de transporte de sus servidores de buzones de correo que funcionarán como servidores de origen para los conectores del agente de entrega.

3.  Crear un conector de agente de entrega para el protocolo específico.

Una vez finalizados estos procedimientos, los mensajes se enrutarán a los sistemas externos a través de conectores de agentes de entrega y el agente de entrega procesará los mensajes.

[Microsoft.Exchange.Datos.Transporte.Espacios de nombre de entrega](https://go.microsoft.com/fwlink/?linkid=262690) proporciona más información acerca del desarrollo de un agente de entrega.

## Conectores de agente de entrega

Un conector de agente de entrega en Exchange 2013 es similar al conector de agente de entrega presentado en Exchange 2010. Enrutan direcciones de mensajes a sistemas externos que no usan el protocolo SMTP. Cuando un mensaje se enruta a un conector de agente de entrega, el agente de entrega asociado realiza la conversión de contenido y la entrega del mensaje. Normalmente, un tercero crea y configura los agentes de entrega para que funcionen con un conector de agente de entrega en su organización.

Un conector de agente de entrega no se puede crear en el Centro de administración de Exchange. En su lugar, crea un conector de agente de entrega en el Shell de administración de Exchange con el cmdlet [New-DeliveryAgentConnector](https://technet.microsoft.com/es-es/library/dd351063\(v=exchg.150\)) y edita las propiedades del conector del agente de entrega con [Set-DeliveryAgentConnector](https://technet.microsoft.com/es-es/library/dd351159\(v=exchg.150\)). Puede especificar uno o más servidores de buzones de correo host para el conector, usando el parámetro *SourceTransportServers* opcional.

## El conector de agente de entrega de mensajería de texto predeterminado

Puede usar el conector de agente de entrega de mensajería de texto para enrutar mensajes a los dispositivos móviles. En su servidor Exchange, ejecute `Get-DeliveryAgentConnector | fl` para ver el conector y todos sus parámetros. Tenga en cuenta que *DeliveryProtocol* está establecido en `MOBILE`.

