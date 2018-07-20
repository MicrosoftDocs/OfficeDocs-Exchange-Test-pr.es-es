---
title: 'Datos de replicación de EdgeSync: Exchange 2013 Help'
TOCTitle: Datos de replicación de EdgeSync
ms:assetid: c7dd137d-7ed4-4f16-9895-f354c449cf9b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232177(v=EXCHG.150)
ms:contentKeyID: 61183331
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Datos de replicación de EdgeSync

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Cuando se implementa un servidor de transporte perimetral, este no tiene acceso a Active Directory. Pero el servidor de transporte perimetral necesita datos de Active Directory para realizar ciertas tareas, como la agregación de listas seguras y la búsqueda de destinatarios, y para implementar la seguridad de dominio mediante la autenticación de Seguridad de la capa de transporte mutua (MTLS). Para replicar estos datos en el servidor de transporte perimetral usamos EdgeSync. Después, el servidor de transporte perimetral almacena toda la información replicada en Active Directory Lightweight Directory Services (AD LDS).

Este tema se centra en los datos replicados desde Active Directory hacia AD LDS en un servidor de transporte perimetral suscrito a un sitio de Active Directory. Si quiere saber más sobre EdgeSync y las suscripciones perimetrales, vea [Suscripciones perimetrales](edge-subscriptions-exchange-2013-help.md).

Los datos que se replican en AD LDS y se usan en el servidor de transporte perimetral se clasifican en cuatro tipos:

Edge Subscription information

Configuration information

Recipient information

Topology information

## Información de suscripción perimetral

Exchange 2013 extiende los esquemas de Active Directory y AD LDS para proporcionar atributos en el objeto **ms-Exch-ExchangeServer**, y poder representar los datos necesarios para controlar la sincronización de EdgeSync. Estos atributos proporcionan tres funciones a EdgeSync:

  - Aprovisionamiento y mantenimiento automáticos de las credenciales usadas para proteger la conexión LDAP entre un servidor de buzones de correo y un servidor de transporte perimetral suscrito.

  - Arbitraje del proceso de bloqueo y concesión de sincronización, lo que garantiza que solo un servidor intentará sincronizarse con un servidor de transporte perimetral individual a la vez. Para más información sobre el proceso de bloqueo y concesión, vea [Suscripciones perimetrales](edge-subscriptions-exchange-2013-help.md).

  - Optimización de la sincronización de EdgeSync para mantener un registro del estado de sincronización actual. Una visualización sencilla del estado de sincronización permite evitar una sincronización manual excesiva.

Las extensiones de esquema de la tabla de abajo son específicas de las suscripciones perimetrales. Los valores asignados a estos atributos se mantienen en la suscripción perimetral y EdgeSync, ya que no están diseñados para ser modificados manualmente.

### Extensiones de esquema de suscripción perimetral

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del atributo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ms-Exch-Server-EKPK-Public-Key</strong></p></td>
<td><p>La clave pública actual para el certificado que usa el servidor. Este valor se almacena en los servidores de transporte perimetral y en los servidores de buzones de correo. La clave pública se usa para cifrar credenciales que sirven para autenticar el servidor durante la comunicación LDAP y SMTP.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-EdgeSync-Credential</strong></p></td>
<td><p>La lista de credenciales que EdgeSync usa para establecer una sesión LDAP autenticada con AD LDS. En los servidores de buzones de correo, este atributo solo contiene credenciales que el servidor de buzones de correo usa para autenticar los servidores de transporte perimetral suscritos. En los servidores de transporte perimetral, este atributo contiene las credenciales para cada servidor de buzones de correo en el sitio de Active Directory suscrito que participa en la sincronización de EdgeSync. Este atributo solo está presente en servidores de buzones de correo que ejecutan la sincronización de EdgeSync y en servidores de transporte perimetral suscritos.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ms-Exch-Edge-Sync-Lease</strong></p></td>
<td><p>Se usa para arbitrar entre los servidores de buzones de correo cuando varios servidores de buzones de correo intentan replicar en el mismo servidor de transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-Edge-Sync-Status</strong></p></td>
<td><p>Solo está presente en AD LDS en el objeto del servidor de transporte perimetral. Este atributo realiza un seguimiento del estado de replicación en una instancia AD LDS e incluye información sobre la replicación.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Información de configuración

Cuando suscribe un servidor de transporte perimetral a una organización, puede administrar desde dentro de la organización los objetos de configuración que son comunes al servidor de transporte perimetral y a la organización de Exchange. Después, estos cambios se replican al servidor de transporte perimetral mediante EdgeSync. Este proceso ayuda a mantener una configuración coherente en todos los servidores implicados con el procesamiento de mensajes.

Un subconjunto de los datos de configuración para la organización de Exchange también se debe mantener en el servidor de transporte perimetral. Durante la sincronización de EdgeSync, los datos de configuración que necesita el servidor de transporte perimetral se escriben en la partición de configuración de AD LDS. Los datos de configuración escritos en AD LDS incluyen:

  - **Servidores de buzones de correo**   El nombre de dominio completo (FQDN) de cada servidor de buzones de correo en el sitio de Active Directory suscrito se pone a disposición del almacén de AD LDS local en el servidor de transporte perimetral. Esta información se usa para derivar una lista de servidores de host inteligente para el conector de envío entrante.

  - **Dominios aceptados**   Todos los dominios de retransmisión autorizados, internos y externos configurados para la organización de Exchange se escriben en AD LDS. Tener los dominios aceptados disponibles para el transporte perimetral permite que la organización de Exchange realice un filtrado de dominio y rechace el tráfico SMTP no válido en su organización tan pronto como sea posible. Para más información sobre los dominios aceptados, vea [Dominios aceptados](accepted-domains-exchange-2013-help.md).

  - **Clasificaciones de mensaje**   Si las clasificaciones de mensaje están disponibles en el servidor de transporte perimetral, los agentes de transporte y la conversión del contenido pueden actuar en las clasificaciones de mensajes en la red perimetral. Por ejemplo, el agente de filtro de datos adjuntos puede aplicar la clasificación Datos adjuntos quitados cuando elimina datos adjuntos, y enviar texto informativo a un usuario de Microsoft Outlook o a un usuario de Outlook Web App para notificar al destinatario lo que ocurrió. Los agentes desarrollados para aplicaciones de terceros pueden usar las clasificaciones de mensajes de forma similar.

  - **Dominios remotos**   Todas las entradas de dominio remoto configuradas para la organización de Exchange se escriben en AD LDS. Las entradas de dominio remoto controlan la configuración de mensajes de fuera de la oficina y la configuración del formato de mensaje para un dominio remoto. Para más información sobre los dominios remotos, vea [Dominios remotos](remote-domains-exchange-2013-help.md).

  - **Conectores de envío**   De manera predeterminada, al crear una suscripción perimetral se crean automáticamente los conectores de envío necesarios para habilitar el flujo de correo de un extremo a otro, entre la organización de Exchange e Internet en el momento en que se suscribe el servidor de transporte perimetral. Todos los conectores de envío existentes en el servidor de transporte perimetral se eliminarán. Si quiere configurar más conectores de envío, configure el conector de envío dentro de la organización de Exchange y, después, seleccione la suscripción perimetral como servidor de origen del conector. Para más información, vea [Suscripciones perimetrales](edge-subscriptions-exchange-2013-help.md).

  - **Servidores SMTP internos**   El valor del atributo *InternalSMTPServers* se almacena en el objeto **TransportConfig** en la organización de Exchange y en el servidor de transporte perimetral local. Durante la sincronización de EdgeSync, el valor almacenado en el objeto del servidor de transporte perimetral se sobrescribe con el valor almacenado en este objeto correspondiente a la organización de Exchange. Este atributo especifica una lista de direcciones IP del servidor SMTP interno o intervalos de direcciones IP que el Id. del remitente y el filtro de conexión deben ignorar.

  - **Listas de dominio seguro**   Los atributos *TLSReceiveDomainSecureList* y *TLSSendDomainSecureList* se almacenan en el objeto **TransportConfig** para la organización de Exchange y el servidor de transporte perimetral. Durante la sincronización de EdgeSync, el valor almacenado en el objeto del servidor de transporte perimetral se sobrescribe con el valor almacenado en este objeto correspondiente a la organización de Exchange. Estos atributos especifican la lista de dominios remotos configurados para la autenticación TLS mutua.

Volver al principio

## Información de destinatario

La información de destinatario que se replica en AD LDS solo incluye un subconjunto de atributos de destinatario. Solo se replican los datos que el transporte perimetral necesita para realizar tareas contra correo no deseado. Los datos de destinatario replicados en AD LDS incluyen:

  - **Destinatarios**   La lista de destinatarios de la organización de Exchange se replica en AD LDS. Cada destinatario se identifica por su GUID de Active Directory asignado. Si configura una cuenta de destinatario para denegar la recepción de correo desde fuera de la organización, ese destinatario no se replica en AD LDS. Si deshabilita o elimina el buzón de correo de un destinatario, ese buzón ya no se replica en AD LDS.

  - **Direcciones proxy**   Todas las direcciones proxy asignadas a cada destinatario se replicarán en AD LDS como datos hash. Se trata de un hash unidireccional que usa el algoritmo hash seguro (SHA) 256. El SHA-256 genera una síntesis del mensaje de 256 bits de los datos originales. Almacenar direcciones proxy como datos hash ayuda a proteger esta información en caso de que el servidor de transporte perimetral o AD LDS estén en peligro. Se hace referencia a las direcciones proxy cuando el servidor de transporte perimetral realiza una tarea de búsqueda de destinatarios contra correo no deseado.

  - **Listas Remitentes seguros, Remitentes bloqueados y Destinatarios seguros**   Las listas Remitentes seguros, Remitentes bloqueados y Destinatarios seguros definidas en cada sesión de Outlook del destinatario se agregan y se replican en AD LDS. Esta configuración se almacena en la base de datos del buzón de correo, donde reside el buzón de correo del destinatario. Una colección de listas seguras del usuario de Outlook es la combinación de los datos de las listas Remitentes seguros, Destinatarios seguros, Remitentes bloqueados y los contactos externos. Al disponer de los datos de la colección de listas seguras en AD LDS, el servidor de transporte perimetral puede filtrar los remitentes según convenga, lo que reduce la sobrecarga operativa que conlleva el filtrado del correo. Esta información se envía como datos hash.
    

    > [!IMPORTANT]
    > Aunque los datos de destinatarios seguros se almacenan en Outlook y se pueden agregar a la colección de listas seguras en la instancia de AD&nbsp;LDS del servidor de transporte perimetral, la funcionalidad de filtrado de contenido no actúa sobre estos datos de destinatarios seguros.



  - **Configuración contra correo no deseado por destinatario**   Con el cmdlet **Set-Mailbox**, puede asignar a determinados usuarios unas opciones de umbral contra correo no deseado que sean distintas de la configuración contra correo no deseado de la organización. Si configura opciones de correo no deseado específicas para los destinatarios, esta configuración invalida la configuración de la organización. Replicando esta configuración en AD LDS, la configuración por destinatario se puede considerar antes de que el mensaje se retransmita a la organización de Exchange. Esta información se envía como datos hash.

Volver al principio

## Información de topología

La información de topología incluye la notificación de servidores de transporte perimetral suscritos o de suscripciones perimetrales quitadas. Estos datos se actualizan cada cinco minutos.

Volver al principio

