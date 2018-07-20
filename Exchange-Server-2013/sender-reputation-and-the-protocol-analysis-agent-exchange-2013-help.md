---
title: 'Reputación del remitente y agente de análisis de protocolo: Exchange 2013 Help'
TOCTitle: Reputación del remitente y agente de análisis de protocolo
ms:assetid: c4c34235-d545-41e7-ac2f-1dd43aaa3708
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124512(v=EXCHG.150)
ms:contentKeyID: 49895900
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Reputación del remitente y agente de análisis de protocolo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-16_

La reputación del remitente forma parte de una funcionalidad contra correo no deseado de Exchange que bloquea los mensajes de acuerdo con varias características del remitente. La reputación del remitente depende de los datos que se conserven de él para decidir la acción que se debe llevar a cabo con el mensaje entrante, si se debe efectuar alguna. El agente de análisis de protocolo es el agente subyacente que se encarga de la función de reputación del remitente.

Cuando configura agentes contra correo electrónico no deseado en un servidor de Exchange, estos actúan en los mensajes de forma acumulativa con el fin de reducir el número de mensajes no solicitados que entran en la organización.

**Contenido**

Cálculo del nivel de reputación del remitente

Uso del SRL

Cómo habilitar y configurar la detección de servidores proxy abiertos

Establecimiento del umbral de bloqueo del SRL

## Cálculo del nivel de reputación del remitente

El nivel de reputación del remitente (SRL) se calcula a partir de las siguientes estadísticas:

  - **Análisis de HELO/EHLO**   Los comandos SMTP HELO y EHLO están pensados para proporcionar el nombre de dominio (por ejemplo, Contoso.com) o la dirección IP del servidor SMTP remitente al servidor SMTP receptor. Los usuarios malintencionados o *spammers* suelen falsificar la instrucción HELO/EHLO de diferentes formas. Por ejemplo, escriben una dirección IP que no coincide con la dirección IP desde la que se originó la conexión. Los spammers también ponen dominios que se admiten de forma local en el servidor de destino en la instrucción HELO para intentar aparentar que los dominios están en la organización. En otros casos, los spammers cambian el dominio que se pasa a la instrucción HELO. El comportamiento típico de un usuario legítimo puede consistir en usar un conjunto de dominios diferente, pero relativamente constante, en las instrucciones HELO.
    
    Así pues, el análisis de la instrucción HELO/EHLO por remitente puede indicar que probablemente sea un spammer. Por ejemplo, un remitente que proporciona muchas instrucciones HELO/EHLO únicas en un período específico probablemente será un spammer. También es muy probable que sean spammers los remitentes que constantemente proporcionan una dirección IP en la instrucción HELO que no coincide con la dirección IP de origen, tal y como se determina en el agente de filtrado de conexión. También es muy probable que lo sean los remitentes remotos que constantemente proporcionan un nombre de dominio local en la instrucción HELO que está en la misma organización que el servidor de Exchange.

  - **Búsqueda de DNS inversa**   La reputación del remitente también comprueba que la dirección IP de origen desde la que este transmitió el mensaje coincida con el nombre de dominio registrado que envía en el comando SMTP HELO o EHLO.
    
    La reputación del remitente lleva a cabo una consulta de DNS inversa enviando la dirección IP de origen al DNS. El resultado que devuelve el DNS es el nombre de dominio registrado mediante el uso de la autoridad de nombres de dominio de esa dirección IP. La reputación del remitente compara el nombre de dominio que devuelve el DNS con el nombre de dominio que el remitente envió en el comando SMTP HELO/EHLO. Si los nombres de dominio no coinciden, es probable que el remitente sea un spammer y que su clasificación general de SRL aumente.
    
    El agente de Id. del remitente realiza una tarea similar, pero el éxito de este agente depende de los remitentes legítimos para actualizar su infraestructura de DNS e identificar a todos los servidores SMTP que envían correo electrónico en la organización. Al realizar una búsqueda inversa de DNS se puede identificar a potenciales spammers.

  - **Análisis de clasificaciones SCL de los mensajes de un remitente en particular** Cuando el agente de filtro de contenido procesa un mensaje, le asigna una clasificación de nivel de confianza de correo no deseado (SCL). La clasificación SCL es un número comprendido entre el 0 y el 9. Una clasificación SCL alta indica que el mensaje tiene más posibilidades de ser correo no deseado. Los datos de cada remitente y las clasificaciones que obtienen sus mensajes se guardan para que la reputación del remitente los analice. La reputación del remitente calcula estadísticas para un remitente de acuerdo con la relación entre todos los mensajes de ese remitente que han obtenido una clasificación SCL baja en el pasado y todos los mensajes de ese remitente que han obtenido una clasificación SCL alta en el pasado. Asimismo, a la clasificación SRL general se aplica el número de mensajes con una clasificación SCL alta que ese remitente ha enviado el último día.

  - **Prueba de proxy abierto del remitente** Un *proxy abierto* es un servidor proxy que acepta solicitudes de conexión de cualquiera, desde cualquier lugar, y reenvía el tráfico tal y como se origina en los hosts locales. Los servidores proxy retransmiten tráfico TCP a través de hosts de servidores de seguridad para proporcionar a las aplicaciones de usuario un acceso transparente a través del firewall. Debido a que los protocolos proxy son ligeros e independientes de los protocolos de las aplicaciones de usuario, hay muchos servicios que los pueden usar. También se pueden usar para compartir una sola conexión a Internet entre diferentes hosts y normalmente se configuran para que solo los puedan atravesar los hosts de confianza en el interior del firewall. Un remitente legítimo puede ser un proxy abierto debido a una configuración incorrecta o malware.
    
    Los proxies abiertos constituyen la vía perfecta para que los usuarios malintencionados oculten su identidad verdadera e inicien ataques por denegación de servicio (DoS) o envíen correo no deseado. Dado que cada vez hay más servidores proxy configurados como abiertos de forma predeterminada, los proxies abiertos son cada vez más habituales. Además, los usuarios malintencionados pueden usar varios proxies abiertos para ocultar la dirección IP de origen.
    
    Si la reputación del remitente realiza una prueba de proxy abierto, lo hace mediante la aplicación de formato a una solicitud SMTP para intentar volver a conectarse al servidor de Exchange desde el proxy abierto. Si se recibe una solicitud SMTP desde el proxy, la reputación del remitente comprueba que el proxy es un proxy abierto y actualiza la estadística de prueba de proxy abierto para ese remitente.

La reputación del remitente compara todas estas estadísticas y calcula un SRL para cada remitente. El SRL es un número comprendido entre el 0 y el 9 que predice la probabilidad de que un remitente específico sea un spammer o usuario malintencionado. El valor 0 indica que probablemente el remitente no sea un spammer, mientras que el valor 9 indica que probablemente lo sea.

Se puede configurar un umbral de bloqueo del 0 al 9, en el que la reputación del remitente emite una solicitud al agente de filtro de remitentes y bloquea al remitente para que no pueda enviar el mensaje a la organización. Cuando se bloquea a un remitente, este se agrega a la lista Remitentes bloqueados durante un período configurable. La forma en la que se tratan los mensajes depende de la configuración del agente de filtro de remitentes. Las siguientes acciones son las que se pueden elegir para tratar los mensajes bloqueados:

  - Rechazar

  - Eliminar y archivar

  - Aceptar y marcar como remitente bloqueado

Si el remitente está incluido en la lista de direcciones IP bloqueadas o en el servicio de reputación de IP de Microsoft, la reputación del remitente emite una solicitud inmediata al agente de filtro del remitente para bloquear al remitente. Para aprovechar esta funcionalidad, debe habilitar y configurar el servicio de actualización contra correo no deseado de Microsoft Exchange.

De forma predeterminada, la reputación del remitente establece una clasificación de 0 para los remitentes que no se han analizado. Cuando un remitente ha enviado 20 o más mensajes, la reputación del remitente calcula un SRL basado en las estadísticas descritas anteriormente en este tema.

Volver al principio

## Uso de SRL

La reputación del remitente actúa en los mensajes en dos fases de la sesión SMTP:

  - **En el comando SMTP MAIL FROM:**    La reputación del remitente solo actúa en un mensaje si está bloqueado o si los agentes de filtro de conexiones, filtro de remitentes, filtro de destinatarios o Id. del remitente han actuado en él anteriormente. En este caso, la reputación del remitente recupera la clasificación SRL actual del remitente a partir del perfil de este, que está almacenado en el servidor de Exchange. Cuando se recupera y evalúa esta clasificación, la configuración del servidor de Exchange dicta el comportamiento que tiene lugar en una conexión particular de acuerdo con el umbral de bloqueo.

  - **Tras el comando SMTP «fin de datos»**   El comando SMTP de fin de transferencia de datos (**EOD**) se emite cuando se han enviado todos los datos reales del mensaje. En este punto de la sesión SMTP, muchos de los agentes contra correo electrónico no deseado ya han procesado el mensaje. Como resultado del procesamiento contra el correo electrónico no deseado, se actualizan las estadísticas de las que depende la reputación del remitente. De esta forma, la reputación del remitente tiene datos para calcular o recalcular una clasificación SRL para el remitente.

Para obtener más información, consulte [Administrar la reputación del remitente](manage-sender-reputation-exchange-2013-help.md).

Volver al principio

## Cómo habilitar y configurar la detección de servidores proxy abiertos

La reputación de remitente evalúa varias características de remitente para calcular un SRL. Entre las características que evalúa la reputación de remitente se encuentran los resultados de una prueba de servidores proxy abiertos. Los spammers suelen enrutar mensajes a través de servidores proxy abiertos en Internet. Al hacerlo, pueden enviar mensajes que parecen proceder de otro servidor distinto al suyo.

Cuando la reputación de remitente calcula un SRL, intenta conectarse a la dirección IP de origen del remitente mediante varios protocolos proxy comunes, como son SOCKS4, SOCKS5, HTTP, Telnet, Cisco y Wingate. La reputación del remitente da formato a una solicitud específica del protocolo intentando volver a conectarse al servidor de transporte perimetral desde el servidor proxy abierto y usando una solicitud SMTP. Si se recibe una solicitud SMTP desde el servidor proxy, la reputación del remitente comprueba que el servidor proxy está abierto y ajusta la clasificación de SRL de acuerdo con este resultado. De forma predeterminada, la detección de los servidores proxy abiertos está habilitada en la reputación del remitente.

Para obtener más información sobre cómo habilitar y configurar la detección de servidores proxy abiertos, consulte [Administrar la reputación del remitente](manage-sender-reputation-exchange-2013-help.md).

Volver al principio

## Establecimiento del umbral de bloqueo de SRL

El SRL es un número comprendido entre el 0 y el 9 que predice la probabilidad de que un remitente específico sea un spammer o usuario malintencionado. Debe establecer un umbral para bloquear al remitente mediante SRL. El umbral de bloqueo de SRL define el valor de SRL que se debe superar para que la reputación del remitente bloquee a un remitente. De forma predeterminada, el SRL se establece en 7. Es recomendable supervisar la efectividad del agente en el nivel predeterminado. Es posible que pueda ajustar el valor para satisfacer las necesidades de su organización. Si establece otros agentes contra correo no deseado de forma agresiva, quizás pueda establecer un umbral SRL para la reputación del remitente superior al que habría establecido si el resto de los agentes contra correo no deseado no estuvieran configurados de forma tan agresiva. Para obtener más información sobre cómo ajustar las configuraciones contra correo no deseado para que funcionen conjuntamente para reducir el correo no deseado, consulte [Protección contra correo no deseado](anti-spam-protection-exchange-2013-help.md).

En un servidor de transporte perimetral, si se supera el umbral de bloqueo de SRL en un remitente particular, la reputación del remitente lo agrega a la lista de direcciones de IP bloqueadas del agente de filtro de conexiones. A veces, los spammers envían lotes de correo no deseado desde un único remitente. En esta situación, si la reputación del remitente calcula un SRL que supera el umbral de bloqueo de SRL, el remitente se agrega a la lista de remitentes bloqueados durante un intervalo de tiempo configurable. La duración predeterminada es de 24 horas. Transcurridas estas 24 horas, se quita al remitente de la lista de remitentes bloqueados para que pueda volver a enviar mensajes.

Cuando se agrega un remitente a la lista de direcciones IP bloqueadas, la reputación del remitente elimina el perfil de dicho remitente. La reputación del remitente elimina el perfil porque el perfil existente del remitente bloqueado indica que el SRL del remitente supera el umbral de bloqueo de SRL. Esto provocaría que el remitente bloqueado se agregara de nuevo a la lista de direcciones IP bloqueadas tan pronto como terminara el tiempo de bloqueo del remitente.

Para obtener más información, consulte [Administrar la reputación del remitente](manage-sender-reputation-exchange-2013-help.md).

Volver al principio

