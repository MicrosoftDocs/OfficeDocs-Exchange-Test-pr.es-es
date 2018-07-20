---
title: 'Protección contra correo no deseado: Exchange 2013 Help'
TOCTitle: Protección contra correo no deseado
ms:assetid: 6af88a08-687d-40b1-8b22-80704184403d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ218660(v=EXCHG.150)
ms:contentKeyID: 49116280
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Protección contra correo no deseado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-06_

Los *emisores de correo no deseado*, o remitentes malintencionados, usan diversas técnicas para enviar correo electrónico no deseado a una organización. Ninguna herramienta o proceso puede eliminar por sí solo todo el correo electrónico no deseado. No obstante, Microsoft Exchange Server 2013 ofrece un enfoque multidireccional, versátil y por niveles para reducir estos mensajes no deseados. Exchange usa agentes de transporte para ofrecer protección contra correo no deseado, aunque los agentes integrados que están disponibles en Exchange 2013 no han cambiado mucho desde Microsoft Exchange Server 2010.

Para obtener más características sobre el correo no deseado y una administración más sencilla, adquiera el servicio Microsoft Exchange Online Protection (EOP). Para ver una comparación entre las características de EOP y de Exchange 2013, vea [Ventajas de las características contra correo no deseado de Exchange Online Protection en Exchange Server 2013](benefits-of-anti-spam-features-in-exchange-online-protection-over-exchange-server-2013-exchange-2013-help.md). Para más información sobre la protección contra correo no deseado de Office 365, vea [Protección contra correo no deseado de Office 365](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us).

Para obtener más información acerca de las capacidades antimalware integradas en Exchange 2013, vea [Protección antimalware](anti-malware-protection-exchange-2013-help.md).

**Contenido**

Agentes contra correo no deseado en servidores de buzones de correo

Agentes contra correo electrónico no deseado en servidores de transporte perimetral

Marcas de correo no deseado

Estrategia para el enfoque contra correo electrónico no deseado

## Agentes contra correo no deseado en servidores de buzones de correo

En general, los agentes contra correo no deseado se habilitan en un servidor de buzones de correo cuando la organización no tiene ningún servidor de transporte perimetral o el correo electrónico no deseado no se filtra antes de aceptar mensajes entrantes. Para obtener más información, vea [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

Al igual que en todos los agentes de transporte, a los agentes contra correo electrónico no deseado se les asigna un valor de prioridad. Un valor bajo indica una prioridad alta, por lo que, en general, un agente contra correo no deseado con la prioridad 1 actuará sobre un mensaje antes que otro agente con la prioridad 9. No obstante, el evento SMTP en el que se registra el agente contra correo electrónico no deseado también es muy importante a la hora de determinar el orden en el que los agentes contra correo no deseado actúan sobre los mensajes. Un agente contra correo no deseado con prioridad baja que se registre en un evento SMTP con anterioridad en la canalización del transporte actuará antes sobre un mensaje que un agente con prioridad alta que se haya registrado posteriormente en el evento SMTP en la canalización de transporte.

En la siguiente lista se muestran los agentes y el orden predeterminado en el que se aplican a los mensajes en un servidor de buzones de correo en función del valor de prioridad predeterminado del agente contra correo no deseado del evento SMTP de la canalización de transporte en el que se registre el evento:

1.  **Agente de filtrado de remitentes**   El filtrado de remitentes compara el remitente del comando MAIL FROM: SMTP con una lista definida por el administrador de remitentes o dominios de remitentes que tienen prohibido enviar mensajes a la organización para determinar qué acción ejecutar, si procede, con un mensaje entrante. Para obtener más información, vea [Filtrado de remitentes](sender-filtering-exchange-2013-help.md).

2.  **Agente de Id. de remitente**   El id. del remitente depende de la dirección IP del servidor de envío y de la dirección responsable pretendida (PRA) del remitente para determinar si es falso o no. Para obtener más información, vea [Id. del remitente](sender-id-exchange-2013-help.md).

3.  **Agente de filtro de contenido**   El filtrado de contenido permite evaluar el contenido de un mensaje. Para obtener más información, vea [Filtrado de contenido](content-filtering-exchange-2013-help.md).
    
    La cuarentena de correo electrónico no deseado es una función del agente de filtro de contenido que reduce el riesgo de pérdida de mensajes legítimos que se clasifican incorrectamente como correo electrónico no deseado. La cuarentena de correo no deseado proporciona una ubicación de almacenamiento temporal para mensajes identificados como correo no deseado y que no deben ser entregados a un buzón de correo de usuario dentro de la organización. Para obtener más información, vea [Cuarentena de correo electrónico no deseado](spam-quarantine-exchange-2013-help.md).
    
    El filtrado de contenido también actúa sobre la característica de agregación de lista segura. La agregación de listas seguras recopila datos de las listas seguras contra correo no deseado que configuran los usuarios de Microsoft Outlook y Outlook Web App, y los pone a disposición del agente de filtrado de contenido. Para obtener más información, vea [Agregación de lista segura](safelist-aggregation-exchange-2013-help.md).

4.  **Agente de análisis de protocolo**   El agente de análisis de protocolo es el agente subyacente que implementa la función de reputación del remitente. La reputación del remitente se basa en datos persistentes acerca de la dirección IP del servidor de envío para determinar la acción que se debe ejecutar, si procede, ante un mensaje entrante. El nivel de reputación del remitente (SRL) se calcula a partir de varias características del remitente obtenidas del análisis del mensaje y de pruebas externas. Para obtener más información, vea [Reputación del remitente y agente de análisis de protocolo](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).

Volver al principio

## Agentes contra correo electrónico no deseado en servidores de transporte perimetral

Si en su organización hay un servidor de transporte perimetral instalado en la red perimetral, todos los agentes contra correo no deseado que están disponibles en un servidor de buzones de correo se instalan y se habilitan de forma predeterminada en el servidor de transporte perimetral. Sin embargo, los siguientes agentes contra correo no deseado solo están disponibles en un servidor de transporte perimetral:

  - **Agente de filtrado de conexión**   El filtrado de conexión inspecciona la dirección IP del servidor remoto que está intentando enviar mensajes para determinar la acción que se debe ejecutar, si procede, ante un mensaje entrante. El filtrado de conexiones usa una lista de direcciones IP permitidas y bloqueadas, junto con servicios de proveedor de listas de direcciones IP permitidas y bloqueadas, para determinar si se debe admitir o no la dirección IP de la conexión. Para obtener más información, vea [Filtrado de conexiones en servidores de transporte perimetral](connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

  - **Agente de filtrado de destinatarios**   El filtrado de destinatarios compara los destinatarios del mensaje en el comando RCPT TO: SMTP con una lista de remitentes bloqueados definida por un administrador. Si se encuentra una coincidencia, no se permite que el mensaje entre en la organización. El filtro de destinatario también compara los destinatarios de los mensajes entrantes con el directorio de destinatarios local para determinar si el mensaje se dirige a destinatarios válidos. Cuando un mensaje se dirige a destinatarios no válidos, se rechaza. Para obtener más información, vea [Filtrado de destinatarios en servidores de transporte perimetral](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).
    

    > [!NOTE]
    > Aunque el agente de filtrado de destinatarios está disponible en los servidores de buzones de correo, no debe configurarlo. Cuando el filtrado de destinatarios en un servidor de buzones de correo detecta un destinatario bloqueado o no válido en un mensaje que incluye otros destinatarios válidos, el mensaje se rechaza. Si instala agentes contra el correo no deseado en un servidor de buzones de correo, el agente de filtrado de destinatarios se habilita de manera predeterminada. Sin embargo, no está configurado para bloquear ningún destinatario.



  - **Agente de filtrado de datos adjuntos**   Esta característica bloquea los mensajes en función del nombre del archivo de los datos adjuntos, la extensión del nombre del archivo o el tipo de contenido MIME del archivo. Puede configurarlo para bloquear un mensaje y sus datos adjuntos, para quitar los datos adjuntos y permitir el paso del mensaje o para eliminar el mensaje y sus datos adjuntos sin avisar. Para obtener más información, vea [Filtrado de datos adjuntos en servidores de transporte perimetral](attachment-filtering-on-edge-transport-servers-exchange-2013-help.md).

Este es el orden predeterminado en el que los agentes contra correo no deseado se aplican en un servidor de transporte perimetral, en función del valor de prioridad predeterminado del agente contra correo no deseado y del evento SMTP de la canalización de transporte en el que se registra el agente:

1.  Agente de filtro de conexión

2.  Agente de filtro de remitentes

3.  Agente de filtro de destinatarios

4.  Agente de Id. de remitente

5.  Agente de filtro de contenido

6.  Agente de análisis de protocolo para la reputación del remitente

7.  Agente de filtrado de datos adjuntos

Volver al principio

## Marcas de correo no deseado

Las marcas de correo electrónico no deseado le ayudan a diagnosticar los problemas relacionados con el correo no deseado mediante la aplicación de metadatos de diagnóstico, o marcas, como información específica del remitente, resultados de la validación del puzzle y resultados del filtrado de contenido, a los mensajes, mientras pasan a través de las características contra correo electrónico no deseado que filtran los mensajes entrantes de Internet.  Para obtener más información, vea [Marcas de correo no deseado](anti-spam-stamps-exchange-2013-help.md).

Volver al principio

## Estrategia para el enfoque contra correo electrónico no deseado

Es necesario planear y calcular cuidadosamente la estrategia para configurar las características contra correo electrónico no deseado y establecer la agresividad de la configuración de los agentes contra correo electrónico no deseado. Si establece todos los filtros de las características contra correo electrónico no deseado en sus niveles más agresivos y configura dichas características para rechazar los mensajes sospechosos, hay una mayor probabilidad de que también rechace mensajes que no son correo electrónico no deseado. Por otro lado, si no establece los filtros contra correo electrónico no deseado en un nivel lo suficientemente agresivo, y no establece el umbral del nivel de confianza contra correo no deseado (SCL) lo suficientemente bajo, es probable que no disminuya el correo electrónico no deseado que entra en la organización.

Es recomendable rechazar un mensaje cuando Exchange detecte un mensaje incorrecto mediante el agente de filtrado de conexión, el agente de filtrado de destinatarios o el agente de filtrado de remitentes. Esta opción es mejor que poner dichos mensajes en cuarentena o asignar metadatos a los mismos, como soluciones contra correo electrónico no deseado. Los agentes de filtrado de conexión y de destinatarios bloquean automáticamente los mensajes identificados por los filtros respectivos. El agente de filtrado de remitente se puede configurar.

Se recomienda esta práctica dado que el SCL subyacente en el filtrado de conexión, filtrado de remitente o filtrado de destinatario es relativamente alto. Por ejemplo, con el filtrado de remitente, en el que el administrador ha configurado el bloqueo de determinados remitentes, no hay razón alguna para asignar los datos del filtrado de remitente a tales mensajes y continuar procesándolos. En la mayoría de las organizaciones, se deben rechazar los mensajes bloqueados. (Si no desea rechazar los mensajes, no debe colocarlos en la lista de remitentes bloqueados.)

La misma lógica se aplica a los servicios de la lista de bloqueo en tiempo real y al filtrado de destinatario, si bien la confianza subyacente no es tan alta como en la lista de direcciones IP bloqueadas. Tenga en cuenta que cuanto más avanza un mensaje en la ruta del flujo de correo, mayor es la probabilidad de falsos positivos, porque las características contra correo electrónico no deseado están evaluando más variables. Por tanto, es posible que observe que si configura las primeras características contra correo electrónico no deseado en la cadena contra correo electrónico no deseado de forma más agresiva, puede reducir la mayor parte del correo electrónico no deseado. En consecuencia, se ahorrarán recursos de procesamiento, de ancho de banda y de disco de modo que se puedan procesar más mensajes ambiguos.

En última instancia, deberá organizar la supervisión de la efectividad general de las características contra correo electrónico no deseado. Una supervisión cuidadosa le permitirá seguir ajustando dichas características para que funcionen bien juntas en su entorno. Con este enfoque, al empezar deberá diseñar una configuración no muy agresiva de las características contra correo electrónico no deseado. Esto permite reducir el número de falsos positivos. A medida que supervise y ajuste las características contra correo electrónico no deseado, determinará mejor el tipo y los ataques de correo electrónico no deseado que experimenta la organización.

Volver al principio

## Vea también


[Protección contra correo no deseado de Office 365](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us)

