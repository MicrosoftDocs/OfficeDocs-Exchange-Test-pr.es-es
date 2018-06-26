---
title: 'Servidores de transporte perimetral: Exchange 2013 Help'
TOCTitle: Servidores de transporte perimetral
ms:assetid: cfff9f59-afac-447c-8297-afcebe49a52d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124701(v=EXCHG.150)
ms:contentKeyID: 61183334
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servidores de transporte perimetral

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-09-29_

Los servidores de transporte perimetral controlan todo el flujo de correo de Internet para minimizar la superficie de ataque. Esto proporciona servicios de retransmisión de Protocolo simple de transferencia de correo (SMTP) y de host inteligente para la organización de Exchange. Los agentes que se ejecutan en el servidor de transporte perimetral proporcionan niveles adicionales de protección de mensajes y seguridad. Estos agentes ofrecen protección frente a correo no deseado, y aplican reglas de transporte para controlar el flujo de correo.

Como el servidor de transporte perimetral está instalado en la red perimetral, nunca es miembro del bosque de Active Directory interno de la organización y no tiene acceso a la información de Active Directory. A pesar de ello, el servidor de transporte perimetral necesita datos que residen en Active Directory, como la información de conector para el flujo de correo y la información de destinatario para las tareas de búsqueda de destinatarios contra correo no deseado. Para sincronizar estos datos en el servidor de transporte perimetral, usamos el servicio Microsoft Exchange EdgeSync (EdgeSync). EdgeSync es una colección de procesos ejecutados en un servidor de buzones de correo de Exchange 2013para establecer una replicación unidireccional de la información de destinatario y de configuración desde Active Directory hacia la instancia de Active Directory Lightweight Directory Services (AD LDS) en el servidor de transporte perimetral. EdgeSync copia únicamente la información que el servidor de transporte perimetral necesita para realizar tareas de configuración contra correo no deseado y habilitar el flujo de correo de un extremo a otro. EdgeSync realiza actualizaciones programadas de manera que la información de AD LDS se mantiene actualizada.

Puede instalar más de un servidor de transporte perimetral en la red de perímetro. Implementar más de un servidor Transporte perimetral proporciona capacidades de redundancia y conmutación en el flujo de entrada de mensajes. Puede equilibrar la carga del tráfico SMTP a su organización entre los servidores de transporte perimetral. Para ello, tiene que definir varios registros MX con el mismo valor de prioridad para el dominio de correo. Puede lograr una coherencia en la configuración de varios servidores de transporte perimetral mediante el uso de scripts de configuración clonados.

El rol de servidor Transporte perimetral permite administrar los siguientes escenarios de procesamiento de mensajes.

## Flujo de correo de Internet

Los servidores de transporte perimetral aceptan mensajes que entran en la organización de Exchange procedentes de Internet. Después de que el servidor de transporte perimetral procesa los mensajes, el siguiente destino donde se enruten dependerá de la configuración de los servidores de Exchange internos:

  - Si el servidor de acceso de cliente y el servidor de buzones de correo están instalados en equipos distintos, el correo se enruta al servicio de transporte del servidor de buzones de correo. El servidor de acceso de cliente se omite para el flujo de correo SMTP entrante.

  - Si el servidor de acceso de cliente y el servidor de buzones de correo están instalados en el mismo equipo, el correo se enruta al servicio de transporte front-end en el servidor de acceso de cliente y, después, al servicio de transporte en el servidor de buzones de correo.

Todos los mensajes enviados a Internet desde la organización se enrutan a los servidores de transporte perimetral después de que el servicio de transporte procese los mensajes en el servidor de buzones de correo. Puede configurar el servidor de transporte perimetral para utilizar el DNS para resolver el registro de recursos MX para los dominios externos SMTP o puede configurar el servidor de transporte perimetral para reenviar mensajes a un host inteligente para la resolución DNS.

## Protección contra correo no deseado

En Exchange 2013, las funciones contra correo no deseado proporcionan servicios para bloquear correo electrónico comercial no solicitado (correo no deseado) en el perímetro de red.

Los emisores de correo electrónico no deseado utilizan diversas técnicas para enviar correo electrónico no deseado a una organización. Los servidores de transporte perimetral impiden que los usuarios reciban correo no deseado. Para ello, proporcionan una colección de agentes que, juntos, ofrecen varios niveles distintos de filtrado y protección contra correo no deseado: Establecer intervalos de retraso del tráfico de red (tarpitting) en los conectores hace que los intentos de recolección de correo electrónico sean ineficaces.

## Reglas de transporte perimetral

Las reglas de transporte perimetral se usan para controlar el flujo de mensajes que se envía a Internet o se recibe de Internet. Las reglas de transporte perimetral se configuran en cada servidor de transporte perimetral para ayudar a proteger los recursos de red y los datos corporativos, mediante la aplicación de una acción en los mensajes que cumplen las condiciones especificadas. Las condiciones de la regla de transporte perimetral se basan en datos (como palabras concretas o patrones de texto en el asunto, el cuerpo, el encabezado o el campo De del mensaje), el nivel de confianza de correo no deseado (SCL) o el tipo de datos adjuntos. Las acciones determinan la forma en que se procesará el mensaje cuando la condición especificada sea verdadera. Las acciones posibles incluyen poner en cuarentena un mensaje, anular o rechazar un mensaje, anexar destinatarios adicionales o registrar un evento. Las excepciones opcionales eximen la aplicación de acciones a mensajes en concreto.

## Reescritura de direcciones

La reescritura de direcciones ofrece un aspecto coherente de las direcciones de correo electrónico de cara a los destinatarios externos. Puede configurar la reescritura de direcciones en los servidores de transporte perimetral para modificar las direcciones SMTP en mensajes entrantes y salientes. La reescritura de direcciones es especialmente útil para organizaciones que acaban de fusionarse y quieren ofrecer coherencia en el aspecto de sus direcciones de correo electrónico.

Para más información sobre la reescritura de direcciones, vea [Reconfiguración de direcciones en los servidores de transporte perimetral](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

