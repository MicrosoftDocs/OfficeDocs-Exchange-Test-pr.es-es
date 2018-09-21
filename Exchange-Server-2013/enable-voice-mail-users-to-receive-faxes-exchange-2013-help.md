---
title: 'Permitir que los usuarios de correo de voz reciban faxes: Exchange 2013 Help'
TOCTitle: Permitir que los usuarios de correo de voz reciban faxes
ms:assetid: 451ab0ea-21e1-4c1f-ae62-4ba7cdfd1e4d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232022(v=EXCHG.150)
ms:contentKeyID: 52062023
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permitir que los usuarios de correo de voz reciban faxes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-04-07_

La mensajería unificada (MU) de Microsoft Exchange permite entregar mensajes de correo de voz en el buzón de un usuario y además permite a los usuarios recibir faxes en su buzón. En la mensajería unificada, se envía un mensaje de fax al buzón de correo del usuario como mensaje de correo electrónico que contiene un archivo de imagen adjunto con la extensión .tif. El usuario puede abrir el archivo adjunto mediante una aplicación de software que permite abrir y ver archivos de imagen con una extensión .tif. En este tema se explica el envío de faxes y cómo funciona en la mensajería unificada.


> [!NOTE]
> Aunque la mensajería unificada no permite a los usuarios enviar faxes, se pueden usar muchas soluciones de terceros, como un servicio de fax por Internet, servicios de fax por correo electrónico o una aplicación de servidor de fax de terceros, para enviar faxes.



**Contenido**

Introducción al servicio de fax

Métodos para enviar y recibir faxes

T.38

Introducción al servicio de fax con la mensajería unificada

Recepción de faxes entrantes

Métodos de referencia de llamadas de fax

Configuración del servicio de fax

Números de teléfono y servicio de fax

Registro en diario de los mensajes de fax de mensajería unificada

## Introducción al servicio de fax

Fax es una abreviatura de la palabra facsímil. Se trata de una tecnología que se usa para transferir documentos por vía electrónica. En general, los faxes se envían y se reciben con aparatos de fax o módems de envío de fax por equipo mediante la Red telefónica conmutada (PSTN), que es una red de telefonía o basada en circuitos. Sin embargo, se pueden usar otras opciones para enviar y recibir faxes.

En la actualidad, muchas organizaciones desean que sus usuarios puedan enviar y recibir faxes. Las organizaciones usan uno o más de los métodos descritos en la siguiente lista, para enviar o recibir faxes a través de la PSTN o a través de Internet. Cada uno de estos métodos tiene sus ventajas y sus desventajas.

  - Máquinas de fax tradicionales y faxes por equipos informáticos

  - Envío de faxes con servidores o puertas de enlace de fax

  - Faxes con una red de voz sobre IP (VoIP)

  - Envío de faxes con una aplicación cliente de correo electrónico

Para enviar un mensaje por fax, es posible que los usuarios de una organización tengan que hacer lo siguiente:

  - Imprimir una copia del documento que se enviará por fax y usar un equipo de fax físico para enviarlo.

  - Guardar el documento en su equipo y usar un módem de fax para enviar el fax, aunque esto requiere una línea de teléfono conectada al ordenador.

  - Usar un servicio de fax por Internet que les permita enviar por fax un documento desde una aplicación de software específica del proveedor.

  - Enviar un fax saliente a un servidor de fax con una aplicación de software que esté configurada para usar el servidor de fax.

Para recibir un fax, es posible que los usuarios de una organización tengan que hacer lo siguiente:

  - Recibir un fax en un equipo de fax físico instalado dentro de la organización.

  - Recibir un fax con un módem de fax instalado en el equipo.

  - Recibir un fax desde un servicio de fax por Internet.

  - Recibir un fax desde un servidor de fax configurado en una red.

  - Recibir un fax desde un servidor asociado de fax que use mensajería unificada para enviar faxes con una red VoIP.

Introducción al servicio de fax

## Métodos para enviar y recibir faxes

Existen diversas opciones para enviar y recibir faxes, entre las que se incluyen las siguientes:

**Máquinas tradicionales de fax y servicio de fax basado en PC**   Para enviar y recibir faxes se puede usar un escáner, un módem de fax en un PC, una impresora con capacidades de fax integradas o una máquina de fax dedicada. Todas estas opciones se pueden usar para transmitir datos en forma de pulsos mediante una línea telefónica a otro dispositivo de fax, normalmente otro equipo de fax o un equipo que tiene instalado un módem de fax. A continuación, los impulsos se transforman en imágenes o se usan para imprimir la imagen en papel.

El método del fax tradicional requiere al menos una línea telefónica en el dispositivo de envío y recepción y los faxes se reciben o envían de uno en uno. Un inconveniente de enviar y recibir faxes mediante un módem de fax es que el equipo tiene que estar conectado y en él tiene que estar funcionando un software para fax o un servicio de fax. Este tipo de faxes basados en PC no usan Internet para enviar o recibir faxes.

**Faxes tradicionales y basados en PC**

![Envío de fax tradicional](images/Bb232022.7bdc1cab-9504-4314-a6e0-eccdfe2a9cd6(EXCHG.150).gif "Envío de fax tradicional")

**Servidores o puertas de enlace de fax y servicios de fax por Internet**   Hay varias formas de enviar y recibir faxes a través de Internet. Entre estas se incluyen el uso de una aplicación de software en un equipo o un cliente de correo electrónico para recibir faxes. En la mayoría de los casos, este tipo de envío y recepción de faxes implica el uso de un servidor o una puerta de enlace de fax para realizar la conversión entre los faxes y el correo electrónico. Este método cada vez es más popular, porque permite a las organizaciones quitar o no tener que comprar equipos de fax adicionales. También elimina la necesidad de instalar líneas de teléfono adicionales. Este método de envío y recepción de faxes incluye la creación de un documento con una página de portada de fax con la información identificativa correcta y el envío del documento a un equipo de fax tradicional. Por ejemplo, el usuario usa una aplicación de software como Microsoft Word o Microsoft Outlook para crear y enviar el fax al servidor o la puerta de enlace de fax. El servidor o la puerta de enlace de fax recibe el fax y, a continuación, lo envía por una línea de teléfono tradicional a un equipo de fax o a un módem de fax instalado en un equipo.

**Faxes con servidores de fax o puertas de enlace**

![Envío de fax con servidores de fax/puertas de enlace](images/Bb232022.d6fa2402-b4ca-4313-956c-62e5fe7731ad(EXCHG.150).gif "Envío de fax con servidores de fax/puertas de enlace")

Los servicios de fax por Internet permiten a un usuario enviar faxes desde su PC mediante Internet. Se puede usar una aplicación de software como Word u Outlook para crear y enviar el fax a un servicio de fax de Internet. Existen muchas compañías que ofrecen servicios de envío y recepción de faxes por Internet mediante suscripción o mediante el cobro de una tarifa por cada mensaje de fax enviado. Los servicios de fax por Internet ofrecen las siguientes ventajas:

  - No hace falta un equipo de fax.

  - No es necesario instalar software ni hardware.

  - No es necesaria una línea telefónica dedicada.

  - Confidencialidad.

  - Es posible enviar varios faxes al mismo tiempo.

  - Los faxes se pueden recibir cuando el equipo está apagado.

La siguiente figura muestra cómo se pueden usar los servicios de fax por Internet para enviar y recibir faxes.

**Servicios de fax por Internet**

![Servicios de fax de Internet](images/Bb232022.5d0fb3d6-95f4-4fbf-80e5-64f5de553e65(EXCHG.150).gif "Servicios de fax de Internet")

**Servicio de fax mediante una aplicación cliente de correo electrónico**   Se pueden enviar y recibir faxes mediante una máquina de fax a través de Internet y luego se reciben en un cliente de correo electrónico como Outlook.

El protocolo T.37 se diseñó para permitir que un equipo de fax enviara mensajes de fax a través de Internet a un cliente de correo electrónico. Los faxes se envían a través de Internet como documentos adjuntos de correo electrónico, normalmente como archivos .tif o .pdf. Para este tipo de faxes es necesario un equipo de fax compatible con iFax o T.37, además de una dirección de correo electrónico para los equipos de fax de envío y recepción. Para poder trabajar con equipos de fax y módems de fax tradicionales, todos los equipos de fax T.37 son compatibles con el envío y la recepción estándar de faxes mediante una línea telefónica. No obstante, en algunos casos los equipos de fax T.37 se pueden usar cuando también se usa una puerta de enlace de fax. La siguiente figura muestra cómo se pueden usar los equipos de fax basados en T.37 y los clientes de correo electrónico para enviar y recibir faxes.

**Envío de fax con correo electrónico**

![Envío de fax con correo electrónico](images/Bb232022.086f086b-dc39-4439-a694-7a98e03e65d1(EXCHG.150).gif "Envío de fax con correo electrónico")

**Servicio de fax mediante una red VoIP**   VoIP es una tecnología que proporciona hardware y software que permite a los usuarios usar una red basada en IP como medio de transmisión de llamadas telefónicas. En una red VoIP, los datos de voz y fax se envían en paquetes mediante el uso de la IP en lugar de usar transmisiones de circuitos tradicionales o líneas de conmutación de circuitos de la PSTN. La puerta de enlace VoIP que conecta a su red IP usa VoIP para enviar paquetes de datos de voz entre un servidor de acceso de cliente que ejecuta el servicio de enrutamiento de llamadas de mensajería unificada de Microsoft Exchange y un servidor de buzones que ejecuta el servicio de mensajería unificada de Microsoft Exchange y un sistema de central de conmutación (PBX). También se puede usar una IP PBX para llevar a cabo funciones en una puerta de enlace VoIP y en una PBX.

Hay dos tipos básicos de redes: de conmutación de circuitos y de conmutación de paquetes. Una red de conmutación de circuitos es una red en la que existe una conexión dedicada. Una conexión dedicada es un circuito o un canal establecido entre dos nodos para que se puedan comunicar. Cuando se establece una llamada entre dos nodos, esa conexión solo la pueden usar estos dos nodos. Cuando uno de los dos nodos termina la llamada, la conexión se cancela. En las redes de conmutación de circuitos, como la PSTN, se transmiten múltiples llamadas a través del mismo medio de transmisión. Con frecuencia, el medio empleado en PSTN es el cobre. No obstante, también se puede emplear cable de fibra óptica.

En las redes de conmutación de paquetes, como Internet o una red de área local (LAN), los paquetes se enrutan a su destino por la ruta más rápida, pero no todos los paquetes que viajan entre dos hosts siguen la misma ruta, ni siquiera los que pertenecen a un mismo mensaje. Esto prácticamente garantiza que los paquetes llegarán en diferentes momentos y desordenados. En una red de conmutación de paquetes, los paquetes (mensajes o fragmentos de mensajes) se enrutan individualmente entre los nodos en vínculos de datos que pueden estar compartidos por otros nodos. En la conmutación de paquetes, a diferencia de la conmutación de circuitos, las diferentes conexiones con nodos de la red comparten el ancho de banda disponible. Las redes de conmutación de paquetes hicieron posible que exista Internet y, al mismo tiempo, ha hecho que las redes de datos, especialmente las redes IP basadas en LAN y las redes de VoIP, estén más disponibles de forma más generalizada.

Introducción al servicio de fax

## T.38

T.38 es un protocolo y un estándar de envío de fax que permite el envío de fax sobre una red basada en IP. Una red basada en IP que use el protocolo T.38 usa el Protocolo simple de transferencia de correo (SMTP) y las Extensiones multipropósito de correo Internet (MIME) para enviar un mensaje al buzón de correo del destinatario. T.38 permite transmisiones de fax IP para dispositivos de fax habilitados para IP y puertas de enlace de fax. Los dispositivos pueden incluir hosts basados en red de IP, como equipos e impresoras clientes. En la mensajería unificada de Exchange, las imágenes de fax son documentos independientes codificados como archivos .tif y adjuntos a un mensaje de correo electrónico. Tanto el mensaje de correo electrónico como el archivo .tif adjunto se envían al buzón habilitado para mensajería unificada del usuario.

La mensajería unificada depende de la capacidad de la puerta de enlace para traducir o convertir protocolos basados en multiplexión por división de tiempo (TDM) o conmutación de circuitos telefónicos, como Red digital de servicios integrados (ISDN o RDSI) o QSIG, de una PBX en protocolos basados en IP o VoIP, como el Protocolo de inicio de sesión (SIP), el Protocolo de transporte en tiempo real (RTP) o T.38 para la recepción de mensajes de fax. La puerta de enlace VoIP es parte integral del funcionamiento de la mensajería unificada. La puerta de enlace VoIP es responsable de la detección de los tonos de fax. Los servidores de acceso de cliente y de buzones dependen de la puerta de enlace VoIP para enviar una notificación de que un fax ha sido detectado. A continuación, los servidores de acceso de cliente y de buzones volverán a negociar la sesión de medios y usarán el protocolo T.38.

Introducción al servicio de fax

## Introducción al envío y recepción de faxes con la mensajería unificada

En la mensajería unificada, el usuario recibe imágenes de fax como documentos independientes codificados como archivos de imagen .tif y anexos como datos adjuntos a un mensaje de correo electrónico. Tanto el mensaje de correo electrónico como el archivo .tif adjunto se envían al buzón habilitado para mensajería unificada del usuario.

Enviar un mensaje de fax al buzón del usuario tiene varias ventajas. Entre ellas se incluyen las siguientes:

  - Puede reducir el número de equipos de fax físicos o tradicionales.

  - El número de líneas de teléfono usadas para enviar y recibir faxes en una organización se puede reducir, porque el servidor de buzones puede poner en lista de espera muchos faxes y enviar cada uno cuando una de las líneas telefónicas quede disponible.

  - Los faxes recibidos como un archivo de imagen .tif tienen mejor calidad que un fax tradicional. Los faxes entrantes se pueden imprimir en una impresora local o compartida.

  - Los faxes enviados al buzón de correo del usuario son más seguros, porque es menos probable que una persona distinta del destinatario los recoja en comparación con los faxes en papel.

  - Los usuarios pueden recibir faxes sin dejar su mesa.

  - Los mensajes de fax que se reciben se pueden supervisar, para asegurarse de que se ajustan a las directivas de seguridad de la organización.

Un mensaje de fax se puede enviar solo a un usuario habilitado para mensajería unificada. La mensajería unificada no puede reenviar los mensajes de fax a una lista de distribución. Si necesita tener esta funcionalidad, debe seguir estos pasos:

1.  Crear un buzón para que responda la llamada de fax. Este será el buzón para la lista de distribución.

2.  Habilitar para mensajería unificada el buzón de la lista de distribución.

3.  Crear una regla para ese buzón habilitado para mensajería unificada. Se configurará la regla para reenviar todos los mensajes a la lista de distribución seleccionada.

Introducción al servicio de fax

## Recepción de faxes entrantes

La recepción de un fax en una red VoIP es diferente de la recepción en un equipo de fax estándar o con un servidor de fax situado en una red basada en IP. Para permitir el envío y la recepción de faxes a través de una red VoIP, es necesario tener una puerta de enlace VoIP o una PBX IP compatible con el protocolo T.38, además de un servidor que también sea compatible con T.38. El protocolo T.38 permite las transmisiones de fax a través de IP para hosts basados en red IP, por ejemplo, equipos cliente, impresoras multifunción con fax y servidores, como un servidor de buzones.


> [!IMPORTANT]
> El envío y la recepción de faxes mediante T.38 o G.711 no se admiten en entornos en los que estén integrados la mensajería unificada y Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server.



Cuando un PBX recibe una llamada, la reenvía a la extensión adecuada. Si no se responde desde el número de extensión del usuario, la PBX reenvía la llamada a una puerta de enlace VoIP, que reenvía la llamada al servidor de buzones correspondiente. El servidor de buzones determina si la llamada es una llamada de voz o de fax, en función del protocolo usado para la llamada. Cuando se usa el protocolo SIP, el servidor de buzones procesa la llamada como si fuera un mensaje de voz. No obstante, si se usa el protocolo T.38 desde la puerta de enlace VoIP, el servidor de buzones reconoce que la llamada procede de un fax y procesa la llamada tal como se ha descrito en el párrafo anterior. Un servidor de buzones reenvía las llamadas de fax entrantes a un servidor asociado de fax dedicado que, luego, relaciona la llamada de fax con el remitente del fax y lo recibe en nombre del usuario habilitado para mensajería unificada. A continuación, el servidor asociado de fax envía el fax incluido como datos adjuntos .tif en un mensaje SMTP al buzón de correo del destinatario.

Cuando se envía una señal de fax T.38 entrante desde una puerta de enlace VoIP al servidor de buzones, el servidor de buzones consulta al directorio mediante el protocolo ligero de acceso a directorios (LDAP) para determinar si el destinatario del fax entrante está habilitado para recibir mensajes de fax entrantes y para determinar la dirección SIP del servidor asociado de fax. Después de comprobar esta información, el servidor de buzones envía una solicitud de referencia de la llamada de fax a la puerta de enlace VoIP o al interlocutor SIP que, luego, reenvía la solicitud de fax al servidor asociado de fax. Una vez establecida correctamente la llamada de fax, el remitente del fax envía los medios y datos del fax al servidor asociado de fax. Una vez que el servidor asociado de fax recibe los medios y los datos de fax, usa SMTP para enviar un mensaje de correo electrónico al servidor de buzones. Este mensaje incluye una imagen .tif del mensaje de fax y encabezados X especiales al destinatario de fax correspondiente.

Después de autenticar y enviar el mensaje desde un servidor asociado de fax válido, un asistente de buzón de correo de mensajería unificada en el servidor de buzones de correo realiza una llamada RPC al servidor de mensajería unificada de Microsoft Exchange. Esto garantiza que las propiedades del mensaje de fax coincidan con las de los mensajes de fax creados por el servidor de buzones. Por último, el servidor de buzones vuelve a enviar el mensaje de fax final, que incluye el mensaje de correo electrónico y el adjunto .tif del fax entrante. A continuación, con MAPI RPC, se entrega la versión completa con formato del mensaje de fax en el servidor de buzones que contiene el buzón del destinatario deseado.

Introducción al servicio de fax

## Métodos de referencia de llamadas de fax

Una llamada de fax entrante se puede señalar a un servidor de buzones a través de una nueva invitación de SIP de la puerta de enlace VoIP o de un interlocutor SIP (puerta de enlace multimedia), mediante una notificación de tono de fax de llamada (CNG) realizada por el interlocutor SIP o mediante una detección CNG realizada por el servidor de buzones. Las subsecciones siguientes detallan la referencia de llamada de fax en cada caso.

## Volver a invitar desde un interlocutor SIP

Una llamada entrante a un número piloto de mensajería unificada se dirige a la mensajería unificada como una invitación con un perfil SDP de voz (RTP/audio)

1.  La MU acepta la invitación y se establecen secuencias de medios. Una vez establecida la llamada, la persona que llama inicia la transmisión de fax.

2.  El interlocutor SIP detecta el tono de la llamada de fax (CNG). El interlocutor SIP realiza una nueva invitación a un servidor de buzones, esta vez, especificando un perfil de fax (T.38 o G.711) en el SDP.

3.  La MU responde a la invitación con un 200 OK, que coloca al interlocutor SIP "en espera".

4.  La mensajería unificada emite un evento REFER, que remite el interlocutor SIP (CNG) a un punto de conexión de la solución asociada de fax, que se obtiene de sus datos de configuración.

5.  El interlocutor SIP envía la invitación de la sesión de fax a la solución de asociado de fax.

6.  La solución de asociado de fax acepta la invitación y se establece una sesión de medios con el interlocutor SIP.

## Notificaciones de CNG por un interlocutor SIP

Una llamada entrante a un número piloto de MU se dirige a la MU como una invitación con un perfil SDP de voz (RTP/audio).

1.  La MU acepta la invitación y se establecen secuencias de medios. Una vez establecida la llamada, la persona que llama inicia la transmisión de fax.

2.  El interlocutor SIP detecta el tono de fax de llamada (CNG). El interlocutor SIP notifica al servidor de mensajería unificada sobre el fax mediante el envío de una notificación de CNG en la secuencia RTP, compatible con RFC 4733.

3.  La mensajería unificada responde a la notificación, emite inmediatamente un evento REFER y remite el interlocutor SIP a un extremo de la solución asociada de fax, que se obtiene de sus datos de configuración.

4.  El interlocutor SIP envía la invitación de la sesión de fax a la solución de asociado de fax.

5.  La solución asociada de fax acepta la invitación.

6.  Se establece una sesión de medios con el interlocutor SIP.

## Detección de CNG por un servidor de buzones

Una llamada entrante a un número piloto de MU se dirige a la MU como una invitación con un perfil SDP de voz (RTP/audio). La MU acepta la invitación y se establecen secuencias de medios.

1.  Una vez establecida la llamada, la persona que llama inicia la transmisión de fax.

2.  El servidor de buzones detecta el tono de fax (CNG) en la secuencia de audio RTP.

3.  La mensajería unificada responde a la notificación, emite inmediatamente un evento REFER y remite el interlocutor SIP a un extremo de la solución asociada de fax, que se obtiene de sus datos de configuración.

4.  El interlocutor SIP envía la invitación de la sesión de fax a la solución de asociado de fax.

5.  La solución asociada de fax acepta la invitación.

6.  Se establece una sesión de medios con el interlocutor SIP.

Introducción al servicio de fax

## Configuración del servicio de fax

Como opción predeterminada, cuando se instala el servidor de buzones, el servidor se configura de forma que permita que las llamadas de fax entrantes se procesen o se entreguen a un usuario habilitado para mensajería unificada. Para configurar la mensajería unificada con un servidor asociado de fax, se debe configurar la directiva de buzón de mensajería unificada y configurar la autenticación entre el servidor de buzones y el servidor asociado de fax. Para más información, consulte [Configuración de faxes entrantes](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-the-maximum-message-duration-for-a-voice-mail-preview-partner).

Introducción al servicio de fax

## Números de teléfono y servicio de fax

La mensajería unificada de Exchange ofrece las opciones de configuración siguientes para que usuarios habilitados para mensajería unificada reciban mensajes de fax:

  - Un número de teléfono de marcación entrante directa (DID) para un usuario individual, usado tanto para correo de fax como para correo de voz.

  - Un número de teléfono DID independiente para un usuario individual que se usa para recibir faxes.

  - Un número de teléfono de fax central para todos los usuarios que reciben todos los faxes.

## Un número de teléfono DID único

Al habilitar a un usuario para mensajería unificada mediante la página **Habilitar buzón de correo de mensajería unificada** o el cmdlet **Enable-UMMailbox**, tiene que especificar al menos un número de extensión único para el usuario. Este número de extensión se habilita para un solo usuario y tiene que ser exclusivo dentro de un determinado plan de marcado. La mensajería unificada usa esta extensión para encontrar el usuario correcto y para entregar mensajes de voz y de fax al buzón de correo del usuario. Para más información, consulte [Enable-UMMailbox](https://technet.microsoft.com/es-es/library/aa998033\(v=exchg.150\)).

Con un número DID único, puede configurar el servicio de fax de modo que un usuario use un único número DID para voz y fax. Esta configuración es fácil de administrar y no desperdicia números DID adicionales. Si el usuario está fuera de su sitio o atendiendo el teléfono cuando llega una llamada de fax, la MU responde la llamada, detecta el tono de fax, crea el mensaje de fax y lo envía al usuario.

Si un usuario cuyo servicio de fax está configurado con un número de teléfono DID único recibe una llamada desde un aparato de fax cuando está presente o en el teléfono, podrá:

  - No responder al teléfono cuando suene, de forma que la llamada de fax se envíe y se responda mediante un servidor de buzones; el mensaje de fax se creará y se reenviará al buzón de correo del usuario.

  - Responder a la llamada de fax y, a continuación, transferírsela a sí mismo, de forma que la llamada se reenvíe y se responda mediante un servidor de buzones; el mensaje de fax se creará y se reenviará al buzón de correo del usuario.

  - Esperar que quien llama reintente el envío del fax y dejar que la llamada de fax se transfiera a un servidor de buzones.

En resumen, si se usa un único número DID, es necesario que el usuario realice acciones adicionales para poder recibir mensajes de fax.

Introducción al servicio de fax

## Varios números de teléfono DID

Cuando habilite un usuario para la mensajería unificada, tendrá que introducir al menos un número de extensión para ese usuario. Puede agregar varios números de extensión para un usuario habilitado para mensajería unificada a través del Centro de administración de Exchange (EAC). Para más información, consulte [Agregar un número de extensión](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/add-extension-number).

Agregar varios números de extensión es útil cuando un usuario habilitado para mensajería unificada:

  - Recibe muchos faxes.

  - No desea que lo molesten al tener que responder el teléfono para recibir un fax.

  - No desea escuchar un tono de fax cuando conteste el teléfono.

Agregar varias extensiones es más complejo que usar una única extensión y puede precisar de varios parámetros de configuración en una PBX o IP PBX. Para configurar varios números de extensión para un usuario habilitado para mensajería unificada, es necesario tener números de extensiones DID disponibles que no se estén usando en la organización. No es buena idea usar varios números para un usuario habilitado para mensajería unificada si la organización tiene un número limitado de números de extensión DID disponibles.

La ventaja de usar varios números de extensión DID consiste en que un usuario habilitado para mensajería unificada recibe llamadas de voz en un número de extensión DID y las llamadas de fax en otro número de extensión DID. Usar números DID individuales para llamadas de correo y de fax es más sencillo para el usuario.

Si configura dos números de extensión DID para un determinado usuario, los números de extensión DID pueden proceder de distintos planes de marcado de mensajería unificada. Para usar dos números DID, puede crear un plan de marcado y usar un servidor de buzones como servidor dedicado que recibirá las llamadas de fax y reenviará los mensajes de fax a los usuarios. Para más información, consulte [Crear un plan de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

Tiene las siguientes opciones al configurar varios números de extensión DID para usuarios habilitados para mensajería unificada:

  - **Una extensión para fax sin mensajería unificada y una para voz**   Este tipo de configuración se habilita por usuario y se usa cuando hay números de extensión DID adicionales o sin usar disponibles. Un número de extensión DID se publica como número de correo de voz del usuario y el otro número de extensión DID se publica como número de fax del usuario. Las llamadas de voz que se responden porque el usuario no responde al teléfono o se encuentra con una señal de ocupado se reenvían a un servidor de buzones. Así, el mensaje de voz se crea y se envía al buzón del usuario habilitado para mensajería unificada. El otro número de extensión se puede conectar a un equipo de fax o a un equipo PC que tenga un módem de fax. Con esta configuración, el servidor de buzones no procesa las llamadas de fax y los mensajes de fax no se envían al buzón del usuario habilitado para la mensajería unificada.

  - **Una extensión para fax y una para voz**   Este tipo de configuración se habilita por usuario y se puede usar cuando la organización tiene muchos números de extensión DID disponibles. En esta configuración, ambos números de extensión DID que se responden porque el usuario no responde al teléfono o está ocupado se tienen en cuenta y se reenvían a un servidor de buzones, que creará un mensaje de voz o de fax, según el número de extensión DID al que se haya llamado. Aunque el usuario publique un número para voz y otro para fax, el servidor de buzones detectará el tipo de llamada que se esté recibiendo en el número de extensión DID y podrá crear un mensaje de voz o de fax a partir de las llamadas que se realizan a cualquiera de los números de extensión DID. Esto resulta muy útil cuando un usuario no tiene un equipo de fax independiente o un equipo dedicado que tenga un módem de fax para responder las llamadas de fax entrantes.

  - **Una extensión "fantasma" para fax y una para voz**   Este tipo de configuración se habilita por usuario. Básicamente, consiste en lo mismo que la configuración que usa dos números DID (uno para fax y otro para voz). Sin embargo, en esta configuración, el número que se publica para llamadas de fax para el usuario habilitado para MU se configura en el PBX como una extensión "fantasma". Las llamadas entrantes que se reciban en ese número de extensión DID "fantasma" siempre se reenviarán a un servidor de buzones.
    
    La ventaja de esta clase de configuración consiste en que las llamadas de fax entrantes las responde un servidor de buzones. Cuando el teléfono suena y no se responde, se crea un fax y se reenvía desde el servidor de buzones hasta el buzón de correo del usuario habilitado para mensajería unificada sin molestar al usuario. Esto sucede automáticamente porque no hay un teléfono ni un equipo de fax situado cerca del usuario y este no oye el sonido de la llamada entrante.
    
    Las desventajas de este tipo de configuración son que es necesario tener disponibles extensiones DID adicionales y que hay que configurar la PBX o IP PBX para que reenvíe la llamada a un servidor de buzones.

## Número de teléfono de fax central

Al habilitar a un usuario para mensajería unificada mediante la página **Habilitar buzón de correo de mensajería unificada** o el cmdlet **Enable-UMMailbox**, tiene que especificar al menos un número de extensión único para el usuario. No obstante, si necesita configurar un número de fax central para los faxes entrantes, debe configurar un buzón individual habilitado para la mensajería unificada que se use para recibir todos los faxes.

En algunas organizaciones, especialmente en las que reciben muchos faxes al día, es posible que quiera publicar un número de fax para toda la organización. Este número de fax lo usarán todos los remitentes cuando envíen faxes a los usuarios de la organización.

La publicación de un solo número de fax para toda la organización permite controlar los tipos de faxes que reciben los usuarios. La ventaja de esta configuración es que precisa solo de un único número de extensión DID o un número de teléfono externo. Asimismo, no requiere de un número DID independiente para los faxes de cada usuario habilitado para MU. No obstante, sí que requiere de una "secretaria de faxes" u otra persona que distribuya los faxes entrantes a los usuarios de la organización, de acuerdo con la información que se incluye en la página de portada del fax o en el propio mensaje de fax.


> [!NOTE]
> El uso de un número de fax centralizado con reconocimiento óptico de caracteres (OCR) no está disponible en la mensajería unificada de Exchange. Esa clase de configuración puede usar un número de fax central. Sin embargo, en lugar de tener que ser enrutado al destinatario por una persona, el software de fax recibe el fax, realiza el OCR y luego intenta buscar al destinatario en función de la información de la página de cubierta o el mensaje de fax.



Es útil usar un único número de fax para toda la organización en las siguientes situaciones:

  - Un usuario dentro de la organización recibe demasiados faxes en su buzón de correo y no puede administrarlos con eficacia.

  - Un usuario recibe demasiados faxes no deseados en su buzón.

  - Las necesidades de la empresa son demasiado complejas para garantizar la creación de una regla de transporte que acepte los faxes entrantes y los enrute al buzón correspondiente. Esto podría no ser práctico, por ejemplo, si su organización necesita que se dirijan ciertos faxes a un determinado grupo y otros faxes a otro grupo. Para más información, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

  - El filtrado de mensajes de fax mediante Outlook no resulta eficaz.

Introducción al servicio de fax

## Registro en diario de los mensajes de fax de mensajería unificada

Muchas organizaciones que implementan el registro en diario pueden usar también la mensajería unificada para consolidar su infraestructura de correo electrónico, correo de voz y fax. No obstante, es posible que no desee que el proceso de registro en diario genere informes de diario para los mensajes generados por la mensajería unificada. En este caso, también puede decidir si se van a registrar en diario los mensajes de correo de voz y de notificación de llamadas perdidas controlados por un servidor de buzones o bien si se van a omitir dichos mensajes. Si la organización no requiere el registro en diario de las notificaciones de correo de voz o de llamadas perdidas, puede reducir la cantidad de espacio de disco duro requerido para almacenar los informes de diario si se omiten tales mensajes. Cuando habilite o deshabilite el registro en diario de los mensajes de correo de voz y los mensajes de notificación de llamadas perdidas, el cambio se aplicará a todos los servidores de transporte de la organización. Para más información, consulte [Registro en diario](journaling-exchange-2013-help.md).


> [!NOTE]
> Los mensajes que contienen faxes generados por un servidor de buzones siempre se registran en el diario, incluso si se configura una regla de diario que especifica que no se deben registrar en el diario los mensajes de correo de voz de mensajería unificada y de notificaciones de llamadas perdidas.



Introducción al servicio de fax

