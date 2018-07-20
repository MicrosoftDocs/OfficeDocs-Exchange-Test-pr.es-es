---
title: 'Registros de transporte: Exchange 2013 Help'
TOCTitle: Registros de transporte
ms:assetid: f8cf635d-60c2-4aa3-9c06-244c29942cba
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd302434(v=EXCHG.150)
ms:contentKeyID: 49896025
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Registros de transporte

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-01-28_

Los registros de transporte proporcionan información sobre lo que está sucediendo en la canalización de transporte. Los siguientes registros de transporte están disponibles en Microsoft Exchange Server 2013:

**Registros de agente**   El registro de agentes graba las acciones realizadas en un mensaje mediante agentes específicos contra correo electrónico no deseado. El registro de agentes está disponible en el servicio de transporte en un servidor de buzones de correo. Para obtener más información, consulte [Registro de agente contra correo no deseado](anti-spam-agent-logging-exchange-2013-help.md).

**Registros de conectividad**   El registro de conectividad graba los servicios de transporte de la actividad de conexión saliente. Está habilitado el registro de conectividad en el servicio de transporte de front-end en servidores de Acceso de clientes, el servicio de transporte en servidores Buzón de correo y el servicio de transporte de buzones en servidores Buzón de correo. Para obtener más información, consulte [Registro de conectividad](connectivity-logging-exchange-2013-help.md).

**Informes de seguimiento y entrega de mensajes**   El seguimiento de mensajes registra los detalles de toda la actividad de mensajes a medida que estos se transfieren a un servidor de buzones de Exchange 2013 y desde este. El seguimiento de mensajes está disponible en el servicio de transporte en servidores de buzones de correo y en el servicio de transporte de buzones de correo en servidores de buzones de correo. Para obtener más información, consulte [Seguimiento de mensajes](message-tracking-exchange-2013-help.md).

Los informes de entrega usan la información almacenada en el registro de seguimiento de mensajes para buscar información acerca de los mensajes enviados a un buzón específico y desde este. Para obtener más información, consulte [Informes de entrega para administradores](delivery-reports-for-administrators-exchange-2013-help.md).

**Seguimiento de canalización**   El seguimiento de canalización registra instantáneas de mensajes antes y después de que un mensaje se vea afectado por los agentes de transporte en el servicio de transporte de los servidores de buzones y en el servicio de entrega de transporte de buzones de los servidores de buzones. Para obtener más información, consulte [Seguimiento del canal](pipeline-tracing-exchange-2013-help.md).

**Registros de protocolo**   El registro de protocolo graba las conversaciones SMTP que se producen en conectores de envío y recepción como parte de la entrega de mensajes. El registro de protocolo está disponible en el servicio de transporte front-end en servidores de acceso de cliente, el servicio de transporte en servidores de buzones de correo y el servicio de transporte de buzones de correo en servidores de buzones de correo. Para obtener más información, consulte [Registro de protocolos](protocol-logging-exchange-2013-help.md).

**Registros de la tabla de enrutamiento**   El registro de la tabla de enrutamiento graba periódicamente una instantánea de la tabla de enrutamiento que Exchange 2013 usa para enrutar mensajes a los destinos. El registro de la tabla de enrutamiento está disponible en el servicio de transporte en servidores de buzones de correo.

