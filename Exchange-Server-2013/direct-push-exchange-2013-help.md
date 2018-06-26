---
title: 'Envío directo: Exchange 2013 Help'
TOCTitle: Envío directo
ms:assetid: 373c1629-3d4b-4828-b014-9e103de4ef25
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997252(v=EXCHG.150)
ms:contentKeyID: 48267993
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Envío directo

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2012-07-11_

Direct Push es una característica que se incorpora en Microsoft Exchange Server 2013. Direct Push mantiene un dispositivo móvil actualizado a través de una conexión de red celular o conexión de red inalámbrica. Notifica al dispositivo móvil cuando hay nuevos contenidos preparados para ser sincronizados.

**Contenido**

Información general

Topología de Direct Push

Configuración de Direct Push para que funcione a través del firewall

## Información general

Para que Direct Push funcione, el dispositivo móvil debe ser compatible con Direct Push. Entre estos dispositivos se incluyen los siguientes:

  - Todas las versiones de Windows Phone

  - Los teléfonos móviles que son producidos por los licenciatarios de MicrosoftExchange ActiveSync y están diseñados específicamente para ser compatibles con la tecnología Direct Push

De forma predeterminada, Direct Push está habilitado en Exchange 2013. Los dispositivos móviles compatibles con Direct Push emiten una solicitud HTTPS de larga duración al servidor que ejecuta Microsoft Exchange. El servidor Exchange supervisa la actividad en el buzón de correo del usuario y envía una respuesta al dispositivo móvil si hay algún cambio, por ejemplo, cambios o modificaciones en mensajes de correo electrónico, elementos de calendario, contactos o elementos de tareas. Si ocurren cambios dentro del ciclo de vida de la solicitud HTTPS, el servidor de Exchange emite una respuesta al dispositivo sobre la ocurrencia de cambios para que el dispositivo inicie la sincronización con el servidor de Exchange. El dispositivo emite, a continuación, esta solicitud al servidor. Una vez terminada la sincronización, se genera una nueva solicitud HTTPS de larga duración para iniciar el proceso una vez más. Esto garantiza que el correo electrónico, el calendario, el contacto y los elementos de tareas sean entregados rápidamente al dispositivo móvil y que siempre esté sincronizado con el servidor de Exchange.

## Topología de Direct Push

El envío directo funciona del siguiente modo:

1.  Un dispositivo móvil configurado para sincronizarse con un servidor Exchange 2013 emite una solicitud HTTPS al servidor. Esta solicitud se conoce como PING. La solicitud indica al servidor que notifique al dispositivo si hay cambios en los elementos durante los próximos 15 minutos en cualquier carpeta configurada para sincronizar. De lo contrario, el servidor debe devolver un mensaje HTTP 200 OK. El dispositivo móvil entra, a continuación, en modo de espera. El ciclo de tiempo de 15 minutos es conocido como un *intervalo de latido*.

2.  Si no hay cambios en los elementos en 15 minutos, el servidor devuelve una respuesta HTTP 200 OK. El dispositivo móvil recibe esta respuesta, reanuda la actividad (lo cual se conoce como *activación*) y emite su solicitud de nuevo. De este modo se reinicia el proceso.

3.  Si hay cambios en los elementos o se reciben nuevos elementos dentro de los 15 minutos del intervalo de latido, el servidor envía una respuesta que informa al dispositivo móvil que existe un elemento nuevo o modificado y le proporciona el nombre de la carpeta en la cual reside el elemento nuevo o modificado. Una vez que el dispositivo recibe esta respuesta, emite una solicitud de sincronización para la carpeta que tiene el elemento nuevo o cambiado. Una vez terminada la sincronización, el dispositivo móvil emite una nueva solicitud de PING y todo el proceso comienza una vez más.

El envío directo depende de las condiciones de red que son compatibles con una solicitud HTTPS de larga permanencia. Si la red del portador del dispositivo móvil o el firewall no es compatible con las solicitudes HTTPS de larga permanencia, la solicitud HTTPS se detiene. Los siguientes pasos describen cómo funciona Direct Push cuando una red de portador del dispositivo móvil tiene un valor de tiempo de espera de 13 minutos.

1.  Un dispositivo móvil emite una solicitud HTTPS al servidor. La solicitud indica al servidor que notifique al dispositivo si hay cambios en los elementos durante los próximos 15 minutos en cualquier carpeta configurada para sincronizar. De lo contrario, el servidor debe devolver un mensaje HTTP 200 OK. El dispositivo móvil entra, a continuación, en modo de espera.

2.  Si el servidor no responde tras 15 minutos, el dispositivo móvil se activa y concluye que la conexión al servidor estaba en tiempo de espera debido a la red. El dispositivo vuelve a emitir la solicitud HTTPS, pero en esta ocasión usa un intervalo de 8 minutos.

3.  Después de 8 minutos, el servidor emite un mensaje HTTP 200 OK. A continuación, el dispositivo intenta obtener una conexión más larga mediante la emisión de una nueva solicitud HTTPS al servidor que tiene un intervalo de latido de 12 minutos.

4.  Después de 4 minutos, se recibe un nuevo mensaje de correo electrónico y el servidor responde enviando una solicitud HTTPS que indica al dispositivo que se sincronice. El dispositivo se sincroniza y vuelve a emitir la solicitud HTTPS que tiene un latido de 12 minutos.

5.  Tras 12 minutos, si no hay elementos nuevos o cambiados, el servidor responde mandando un mensaje HTTP 200 OK. El dispositivo se activa y concluye que las condiciones de la red son compatibles con el intervalo de latido de 12 minutos. A continuación, el dispositivo intenta obtener una conexión más larga mediante la nueva emisión de una solicitud HTTPS que tiene un intervalo de latido de 16 minutos.

6.  Después de 16 minutos, no se recibe respuesta del servidor. El dispositivo se activa y concluye que las condiciones de la red no son compatibles con el intervalo de latido de 16 minutos. Puesto que este error ocurrió directamente una vez que el dispositivo intentó incrementar el intervalo de latido, concluye que el intervalo de latido ha alcanzado su máximo límite. El dispositivo emite una solicitud HTTPS que tiene un intervalo de latido de 12 minutos puesto que se trata del último intervalo de latido correcto.

El dispositivo móvil intenta utilizar el intervalo de latido más largo que sea compatible con la red. Así, se prolonga la duración de la batería en el dispositivo y se reduce la cantidad de datos que se transfieren a través de la red. Los portadores móviles pueden especificar un valor de latido máximo, mínimo e inicial en las opciones de registro del dispositivo móvil.

## Configuración de Direct Push para que funcione a través del firewall

Para que Direct Push funcione a través del firewall, debe abrir un puerto TCP 443. Se necesita este puerto para la Capa de sockets seguros (SSL) y se debe abrir entre Internet y el servidor de acceso de cliente.

Además de los puertos de apertura en el firewall, para el funcionamiento óptimo del envío directo, debe incrementar el valor predeterminado de tiempo de espera en el firewall de 15 minutos a 30 minutos. La longitud máxima de la solicitud HTTPS está determinada por las siguientes opciones:

  - El valor de tiempo de espera máximo establecido en los firewall que controlan el tráfico desde el servidor de Internet al servidor de acceso de cliente

  - Los valores de tiempos de espera del firewall que son establecidos por el proveedor de servicios móviles

