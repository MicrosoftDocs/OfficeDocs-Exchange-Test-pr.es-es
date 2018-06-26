---
title: 'Flujo de correo: Exchange 2013 Help'
TOCTitle: Flujo de correo
ms:assetid: 14df5e1a-a5f7-4b0d-ba97-f53b76f0e7e0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996349(v=EXCHG.150)
ms:contentKeyID: 48267827
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Flujo de correo

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

En Microsoft Exchange Server 2013, el flujo de correo se produce a través de la canalización de transporte. La *canalización de transporte* es un conjunto de servicios, conexiones, componentes y colas que funcionan conjuntamente para enrutar todos los mensajes a un categorizador situado en el servicio de transporte en un servidor de buzones de correo dentro de la organización.

¿Busca una lista de todos los temas de flujo de correo? Vea Documentación de flujo de correo.

Para obtener información sobre cómo configurar el flujo de correo en una organización de Exchange 2013 nueva, vea [Configurar el flujo de correo y el acceso de cliente](configure-mail-flow-and-client-access-exchange-2013-help.md).

**Contenido**

La canalización de transporte

Servicio de transporte en servidores de buzones de correo

Documentación de flujo de correo

## La canalización de transporte

La canalización de transporte consta de los siguientes archivos:

  - **Servicio de transporte front-end en servidores de acceso de cliente**   Este servicio funciona como un proxy sin estado para todo el tráfico SMTP externo entrante y saliente (opcionalmente) para la organización de Exchange 2013. El servicio de transporte front-end no inspecciona el contenido de los mensajes, no se comunica con el servicio de transporte de buzones en los servidores de buzones de correo ni pone en la cola a ningún mensaje localmente.

  - **Servicio de transporte en los servidores de buzones de correo**   Este servicio es prácticamente idéntico al servidor de transporte de concentradores en versiones previas de Exchange. El servicio de transporte administra todo el flujo de mensajes de SMTP para la organización, categoriza los mensajes e inspecciona el contenido de estos. A diferencia de las versiones anteriores de Exchange, el servicio de transporte nunca se comunica directamente con las bases de datos de los buzones de correo. La tarea ahora es administrada por el servicio de transporte de buzón. El servicio de transporte enruta mensajes entre el servicio de transporte de buzones de correo, el servicio de transporte, el servicio de transporte front-end y (según la configuración) el servicio de transporte en los servidores de transporte perimetral. El servicio de transporte en los servidores de buzones de correo se describe con más detalle más adelante en este tema.

  - **Servicio de transporte de buzones en los servidores de buzones de correo**   Este servicio consta de dos servicios independientes: el servicio de transporte de envío de buzón de correo y el servicio de entrega de transporte de buzón de correo. El servicio de entrega de transporte de buzón de correo recibe mensajes de SMTP desde el servicio de transporte en el servidor de buzones de correo local o en otros servidores de buzones de correo, y se conecta con la base de datos del buzón de correo usando una llamada a procedimiento remoto (RPC) de Exchange para enviar el mensaje. El servicio de envío de transporte de buzones conecta la base de datos de buzones de correo local con RPC para recuperar mensajes y envía los mensajes por SMTP al servicio de transporte en el servidor de buzones de correo local o en otros servidores de buzones de correo. El servicio de envío de transporte de buzones tiene acceso a la misma información de topología de enrutamiento que el servicio de transporte. Como el servicio de transporte front-end, el servicio de transporte de buzones de correo tampoco coloca en cola a los mensajes localmente.

  - **Servicio de transporte en los servidores de transporte perimetral**   Este servicio es muy similar al servicio de transporte en los servidores de buzones de correo. Si tiene un servidor Transporte perimetral instalado en la red perimetral, el flujo de todo el correo procedente de Internet o que se dirige a Internet se produce a través del servidor Transporte perimetral del servicio de transporte. Este servicio se describe de forma más detallada más adelante en este mismo tema.

En la figura que aparece a continuación, se muestran las relaciones entre los componentes de la canalización de transporte de Exchange 2013.

**Introducción a la canalización de transporte de Exchange 2013.**

![Diagrama de descripción general sobre la canalización del transporte](images/Aa996349.6f548b64-6ac2-4e98-9098-69ad6cd9f569(EXCHG.150).gif "Diagrama de descripción general sobre la canalización del transporte")

## Mensajes de remitentes externos

Los mensajes que entran desde fuera de la organización entran a la canalización de transporte a través del conector de recepción en el servicio de transporte front-end en un servidor de acceso de clientes y luego se enrutan al servicio de transporte en el servidor de buzones de correo.

Si tiene un servidor Transporte perimetral de Exchange 2013 instalado en la red perimetral, los mensajes que entran desde fuera de la organización entran a la canalización de transporte a través del conector de recepción en el servicio de transporte en el servidor Transporte perimetral. Adónde van después los mensajes depende de cómo se configuran los servidores internos de Exchange.

  - **Servidor de buzones de correo y servidor de acceso de cliente instalados en el mismo equipo**   En esta configuración, el servidor de acceso de cliente se usa para el flujo de correo entrante. El flujo de correo se produce desde el servicio de transporte en el servidor Transporte perimetral al servicio de transporte front-end en el servidor de acceso de clientes, y después al servicio de transporte en el servidor de buzones de correo.

  - **Servidor de buzones de correo y servidor de acceso de cliente instalados en equipos distintos**   En esta configuración, el servidor de acceso de cliente se omite para el flujo de correo entrante. El flujo de correo se produce desde el servicio de transporte en el servidor Transporte perimetral al servicio de transporte en el servidor de buzones de correo.


> [!NOTE]
> Si tiene un servidor Transporte perimetral de Exchange 2010 o Exchange 2007 instalado en la red perimetral, el flujo de correo se produce siempre directamente entre el servidor Transporte perimetral y servicio de transporte en el servidor de buzones de correo. Para obtener más información, vea <A href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Usar un servidor de transporte perimetral de Exchange 2010 o 2007 en Exchange 2013</A>.



## Mensajes de remitentes internos

Los mensajes SMTP del interior de la organización entran a la canalización de transporte a través del servicio de transporte en un servidor de buzones de correo de una de las siguientes maneras:

  - Mediante un conector de recepción.

  - Desde el directorio de recogida o reproducción.

  - Desde el servicio de transporte de buzón de correo.

  - Mediante el envío de agente.

El mensaje se enruta según el destino de enrutamiento o grupo de distribución. Para obtener más información, vea [Enrutamiento de correo](mail-routing-exchange-2013-help.md).

Si el mensaje tiene destinatarios externos, el mensaje se enruta desde el servicio de transporte en el servidor de buzones de correo a Internet, o desde el servidor de buzones de correo al servicio de transporte front-end en un servidor de acceso de clientes y después a Internet si el conector de envío está configurado para redirigir las conexiones salientes mediante proxy a través del servidor de acceso de clientes. Para obtener más información, vea [Crear un conector de envío para correo electrónico enviado a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md).

Si tiene un servidor Transporte perimetral instalado en la red perimetral, los mensajes con destinatarios externos nunca se enrutan a través del servicio de transporte front-end en un servidor de acceso de clientes. El mensaje se enruta desde el servicio de transporte de un servidor de buzones de correo al servicio de transporte del servidor Transporte perimetral.

## Servicio de transporte en servidores de buzones de correo

Cada mensaje que se envía o recibe mediante una organización de Exchange 2013 debe categorizarse en el servicio de transporte en un servidor de buzones de correo antes de que se enrute y se entregue. Después de que se haya categorizado un mensaje, se coloca en la cola de entrega para ser enviado a la base de datos del buzón de correo de destino, al grupo de disponibilidad de base de datos (DAG) de destino, al sitio de Active Directory o al bosque de Active Directory o al dominio de destino fuera de la organización.

El servicio de transporte en el servidor de buzones de correo está compuesto por los siguientes componentes y procesos:

  - **Recepción SMTP**   Cuando el servicio de transporte recibe los mensajes, se realiza la inspección del contenido del mensaje, se aplican las reglas de transporte y se realiza la inspección de correo electrónico no deseado y antimalware si están habilitados. La sesión SMTP tiene una serie de eventos que funcionan conjuntamente en un orden específico para validar el contenido de un mensaje antes de que sea aceptado. Una vez que un mensaje ha pasado completamente por la recepción SMTP y no ha sido rechazado por eventos de recepción ni por ningún agente antimalware o contra correo electrónico no deseado, se pone en la cola de envío.

  - **Envío**   Envío es el proceso de poner mensajes en la cola de envío. El categorizador recoge un mensaje a la vez para la categorización. El envío se produce de tres maneras:
    
      - Desde la recepción SMTP a través de un conector de recepción.
    
      - A través del directorio de recogida o reproducción. Estos directorios existen en servidores de buzones de correo y en servidores de transporte perimetral. Los archivos de mensaje con formato correcto que se copian en el directorio Pickup o en el directorio Replay se ponen directamente en la cola de envío.
    
      - A través de un agente de transporte.

  - **Categorizador**   El categorizador toma mensajes, de uno en uno, de la cola de envío. El categorizador completa los siguientes pasos:
    
      - Resolución del destinatario, que incluye direccionamiento de nivel superior, expansión y bifurcación.
    
      - Resolución de enrutado.
    
      - Conversión de contenido.
    
    Además, se aplican reglas de flujo de correo definidas por la organización. Después de haber categorizado los mensajes, estos se colocan en la cola de entrega según el destino del mensaje. La base de datos del buzón de destino, DAG, el sitio de Active Directory, el bosque de Active Directory o el dominio externo colocan los mensajes en la cola.

  - **Envío SMTP**   La manera en que se enrutan los mensajes desde el servicio de transporte depende de la ubicación de los destinatarios del mensaje en relación con el servidor de buzones de correo donde se produjo la categorización. El mensaje podría enrutarse a una de las siguientes ubicaciones:
    
      - Al servicio de transporte de buzones en el mismo servidor de buzones de correo.
    
      - Al servicio de transporte de buzones en otro servidor de buzones de correo que forma parte del mismo DAG.
    
      - Al servicio de transporte en un servidor de buzones de correo en otro DAG, sitio de Active Directory o bosque de Active Directory.
    
      - Para entrega en Internet a través de un conector de envío en el mismo servidor de buzones de correo, a través del servicio de transporte en otro servidor de buzones de correo, a través del servicio de transporte front-end en un servidor de acceso de clientes o a través del servicio de transporte en un servidor Transporte perimetral de la red perimetral.

## Servicio de transporte en los servidores de transporte perimetral

Los componentes del servicio de transporte en los servidores de transporte perimetral son idénticos a los componentes del servicio de transporte en los servidores de buzones de correo. No obstante, lo que realmente sucede durante cada fase del procesamiento en los servidores de transporte perimetral es distinto. Las diferencias se describen en la lista siguiente.

  - **Recepción SMTP**   Cuando un servidor de transporte perimetral se suscribe a un sitio interno de Active Directory, el conector de recepción predeterminado se configura automáticamente para aceptar correo de los servidores de buzones de correo internos y de Internet. Cuando llegan mensajes de Internet al servidor Transporte perimetral, los agentes contra correo no deseado filtran las conexiones y el contenido de los mensajes, y ayudan a identificar el remitente y el destinatario mientras la organización acepta el mensaje. Los agentes contra correo no deseado están instalados y habilitados de manera predeterminada. Existen otras características de filtrado de conexión y filtrado de datos adjuntos, pero no hay capacidades integradas de filtrado de malware. Además, el agente de regla perimetral controla las reglas de transporte. En comparación con el agente de regla de transporte en los servidores de buzones de correo, solo un pequeño subconjunto de condiciones de reglas de transporte está disponible en los servidores de transporte perimetral. Pero hay acciones de reglas de transporte únicas relacionadas con las conexiones SMTP que están disponibles solamente en los servidores de transporte perimetral.

  - **Envío**   En un servidor Transporte perimetral, los mensajes entran normalmente a la cola de envío a través del conector de recepción. Sin embargo, el directorio de recogida y el directorio de reproducción también están disponibles.

  - **Categorizador**   En un servidor Transporte perimetral, la categorización es un proceso breve en el que el mensaje se pone directamente en una cola de entrega para entrega a los destinatarios internos o externos.

  - **Envío SMTP**   Cuando un servidor Transporte perimetral se suscribe a un sitio interno de Active Directory, se crean y configuran automáticamente dos conectores de envío. Uno es responsable de enviar correo saliente a los destinatarios de Internet; el otro es responsable de enviar correo entrante de Internet a los destinatarios internos. El correo entrante se envía al servicio de transporte en un servidor de buzones de correo disponible en el sitio de Active Directory con suscripción.

## Documentación de flujo de correo

La tabla siguiente contiene vínculos a temas que le ayudarán a aprender acerca de y a administrar el flujo de correo en Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tema</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-routing-exchange-2013-help.md">Enrutamiento de correo</a></p></td>
<td><p>Enrutamiento de correo describe cómo se transmiten los mensajes entre servidores de mensajería.</p></td>
</tr>
<tr class="even">
<td><p><a href="connectors-exchange-2013-help.md">Conectores</a></p></td>
<td><p>Los conectores definen dónde y cómo se transmiten los mensajes desde los servidores de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="domains-exchange-2013-help.md">Dominios</a></p></td>
<td><p>Los dominios aceptados definen los espacios de direcciones SMTP que se usan en la organización de Exchange. Los dominios remotos configuran el formato de los mensajes y la configuración de la codificación de los mensajes que se envían a dominios externos.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-agents-exchange-2013-help.md">Agentes de transporte</a></p></td>
<td><p>Los agentes de transporte actúan como si viajaran a través de la canalización de transporte de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-high-availability-exchange-2013-help.md">Alta disponibilidad de transporte</a></p></td>
<td><p>La alta disponibilidad del transporte describe como Exchange 2013 mantiene copias redundantes de mensajes durante el tránsito y después de la entrega.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-logs-exchange-2013-help.md">Registros de transporte</a></p></td>
<td><p>Los registros de transporte registran lo que pasa a los mensajes cuando fluyen a través de la canalización de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-message-approval-exchange-2013-help.md">Administrar la aprobación de mensajes</a></p></td>
<td><p>El transporte moderado requiere la aprobación de los mensajes enviados a destinatarios específicos.</p></td>
</tr>
<tr class="even">
<td><p><a href="content-conversion-exchange-2013-help.md">Conversión de contenido</a></p></td>
<td><p>La conversión del contenido controla las opciones de conversión de mensajes del formato de codificación neutral para el transporte (TNEF) para destinatarios externos, y opciones de conversión MAPI para destinatarios internos.</p></td>
</tr>
<tr class="odd">
<td><p><a href="dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md">DSN y NDR en Exchange 2013</a></p></td>
<td><p>Las notificaciones del estado de entrega (DSNs) son los mensajes del sistema que se envían a los remitentes de mensajes, por ejemplo, informes de no entrega (NDRs).</p></td>
</tr>
<tr class="even">
<td><p><a href="track-messages-with-delivery-reports-exchange-2013-help.md">Seguimiento de mensajes con informes de entrega</a></p></td>
<td><p>Informes de entrega es una herramienta de seguimiento de mensajes que puede utilizar para buscar el estado de la entrega en los mensajes de correo electrónico con respecto a su envío o recepción por parte de los usuarios en la libreta de direcciones compartida de la organización, con un asunto determinado. Puede realizar el seguimiento de la información de entrega de los mensajes enviados desde un buzón de correo específico de la organización o recibidos desde dicho buzón.</p></td>
</tr>
<tr class="odd">
<td><p><a href="message-size-limits-exchange-2013-help.md">Límites de tamaño de mensaje</a></p></td>
<td><p>Este tema describe los límites de tamaño e individuales de los componentes individuales que se imponen en los mensajes.</p></td>
</tr>
<tr class="even">
<td><p><a href="queue-viewer-exchange-2013-help.md">Visor de cola</a></p></td>
<td><p>Use el Visor de cola en el Cuadro de herramientas de Exchange para ver y actuar sobre las colas y los mensajes en cola.</p></td>
</tr>
<tr class="odd">
<td><p><a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Directorio de recogida y directorio de reproducción</a></p></td>
<td><p>Los directorios de recogida y de reproducción se usan para insertar archivos de mensajes en la canalización de transporte.</p></td>
</tr>
<tr class="even">
<td><p><a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Usar un servidor de transporte perimetral de Exchange 2010 o 2007 en Exchange 2013</a></p></td>
<td><p>Este tema describe las consideraciones del uso del servidor de transporte perimetral de las versiones anteriores de Exchange en Exchange 2013.</p></td>
</tr>
</tbody>
</table>

