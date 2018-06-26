---
title: 'Alta disponibilidad de transporte: Exchange 2013 Help'
TOCTitle: Alta disponibilidad de transporte
ms:assetid: e9ec6d05-f441-4cca-8592-8f7469948299
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657506(v=EXCHG.150)
ms:contentKeyID: 49895991
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Alta disponibilidad de transporte

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-15_

En Microsoft Exchange Server 2013, la alta disponibilidad de transporte es responsable de mantener copias redundantes de los mensajes antes y después de la entrega correcta de estos. Exchange 2013 mejora las características de alta disponibilidad de transporte presentadas en Exchange Server 2010, por ejemplo, la redundancia de instantáneas y el contenedor de transporte, para ayudar a garantizar que los mensajes no se pierdan.

A continuación, se presenta un resumen de las principales mejoras de la alta disponibilidad de transporte en Exchange 2013:

  - La redundancia de instantáneas crea una copia redundante del mensaje en otro servidor antes de la aceptación o la confirmación del mensaje. La compatibilidad o falta de compatibilidad del servidor de envío con la redundancia de instantáneas es irrelevante.

  - La redundancia de instantáneas reconoce grupos de disponibilidad de base de datos (DAG) y sitios de Active Directory como límites de alta disponibilidad de transporte. Esto reduce la cantidad de servidores que pueden alojar copias redundantes de mensajes y elimina el tráfico de mantenimiento de mensajes innecesario en DAG o sitios de Active Directory.
    
    Para obtener más información, consulte [Redundancia de instantánea](shadow-redundancy-exchange-2013-help.md).

  - Se mejoró el contenedor de transporte y ahora se denomina *red de seguridad*. La red de seguridad almacena los mensajes procesados correctamente por el servicio de transporte en servidores de buzones de correo. La red de seguridad funciona mejor para servidores de buzones de correo en un DAG, pero también funciona para varios servidores de buzones de correo en el mismo sitio de Active Directory que no pertenece a un DAG.

  - La red de seguridad ahora se hace redundante en otro servidor. Esto es importante para evitar un único punto de error en Exchange 2013, dado que el servicio de transporte y las bases de datos de buzones de correo se encuentran en el servidor de buzones de correo.
    
    Para obtener más información, consulte [Red de seguridad](safety-net-exchange-2013-help.md).

El siguiente diagrama ofrece una descripción general de alto nivel sobre cómo funciona la alta disponibilidad de transporte en Exchange 2013.

![Información general sobre alta disponibilidad de transporte](images/JJ657506.88f2284d-8afe-4c8f-94a6-cd4c097a55d8(EXCHG.150).gif "Información general sobre alta disponibilidad de transporte")

1.  Un servidor de buzones de correo de Exchange 2013 denominado Mailbox01 recibe un mensaje de un servidor SMTP que está fuera del límite de alta disponibilidad de transporte. El *límite de alta disponibilidad de transporte* es un DAG o un sitio de Active Directory en entornos que no son DAG. El mensaje puede provenir de un servidor SMTP de terceros, de un servidor SMTP de Internet redirigido mediante proxy a través de un servidor de acceso de cliente o de otro servidor de Exchange 2013.

2.  Antes de confirmar la recepción del mensaje, Mailbox01 inicia una nueva sesión SMTP en otro servidor de buzones de correo de Exchange 2013 denominado Mailbox03 que no está dentro del límite de alta disponibilidad de transporte, y Mailbox03 crea una instantánea del mensaje. En entornos DAG, se prefiere un servidor de instantáneas en un sitio de Active Directory remoto. Mailbox01 es el servidor principal que aloja el mensaje principal, y Mailbox03 es el servidor de instantáneas que aloja el mensaje de instantánea.

3.  El servicio de transporte en Mailbox01 procesa el mensaje principal.
    
    1.  En este ejemplo, el buzón de correo del destinatario se encuentra en Mailbox01, de modo que el servicio de transporte transmite el mensaje al servicio de transporte de buzones de correo local.
    
    2.  El servicio de transporte de buzones de correo entrega el mensaje a la base de datos de buzones de correo local.
    
    3.  Mailbox01 pone en cola un estado de descarte para Mailbox03 que indica que el mensaje principal se procesó correctamente, y Mailbox01 mueve una copia del mensaje principal a la red de seguridad principal local. Tenga en cuenta que el mensaje se mueve entre colas dentro de la misma base de datos de cola.

4.  Mailbox03 realiza un sondeo periódico de Mailbox01 sobre el estado de descarte del mensaje principal.

5.  Cuando Mailbox03 determina que Mailbox01 procesó correctamente el mensaje principal, Mailbox03 mueve el mensaje de instantánea a la red de seguridad de instantáneas local. Tenga en cuenta que el mensaje se mueve entre colas dentro de la misma base de datos de cola.

El mensaje se retiene en la red de seguridad principal y la red de seguridad de instantáneas hasta que expire sobre la base de un valor de tiempo de espera configurable. Si se produce una conmutación por error de la base de datos antes de que expire el mensaje, la red de seguridad principal de Mailbox01 vuelve a enviar el mensaje. Si Mailbox01 no está disponible, la red de seguridad de instantáneas de Mailbox03 vuelve a enviar el mensaje.

## Redundancia de mensajes en el servicio de transporte front-end en servidores de acceso de cliente

Un servidor de acceso de cliente no tiene colas de mensajes. Es un servidor proxy sin estado que usa el servicio de transporte front-end para aceptar conexiones SMTP entrantes y redirigirlas mediante proxy al servicio de transporte en un servidor de buzones de correo. El servicio de transporte front-end mantiene abierta la sesión SMTP con el servidor de envío, mientras que el mensaje principal se transmite al servicio de transporte en un servidor de buzones de correo, y el servicio de transporte crea una instantánea del mensaje en un servidor de buzones de correo diferente dentro del límite de alta disponibilidad de transporte. Una vez que el mensaje principal y el mensaje de instantánea se crean correctamente, el comando SMTP de fin de datos se envía nuevamente al servidor SMTP de envío a través de un servidor de acceso de cliente.

