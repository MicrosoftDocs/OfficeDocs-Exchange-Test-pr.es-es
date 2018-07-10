---
title: 'Enrutamiento de correo: Exchange 2013 Help'
TOCTitle: Enrutamiento de correo
ms:assetid: 6fd39079-9655-4fd9-9269-c7462c76e0a7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998825(v=EXCHG.150)
ms:contentKeyID: 48268265
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Enrutamiento de correo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

La tarea principal del servicio de transporte que existe en todos los servidores de buzones de correo de la organización de Microsoft Exchange Server 2013 es enrutar los mensajes que se reciben de los usuarios y los orígenes externos hacia su destino final. Las decisiones de enrutamiento se toman durante la categorización de los mensajes. El categorizador es un componente del servicio de transporte de un servidor de buzones de correo que procesa todos los mensajes entrantes y determina qué hacer con ellos en función de la información acerca de su destino.

El enrutamiento en Exchange 2013 es ahora totalmente compatible con los grupos de disponibilidad de base de datos (DAG) y usa la pertenencia de DAG como límite de enrutamiento. ¿Por qué? En Exchange 2013, todos los servidores de buzones de correo hospedan el servicio de transporte. Por lo tanto, cuando un servidor de buzones de correo pertenece a un DAG, el mecanismo primario para enrutar los mensajes está estrechamente alineado con el DAG. Un DAG resulta ineficiente cuando se extiende en varios sitios de Active Directory, mediante el uso del sitio de Active Directory como límite de enrutamiento principal. Exchange 2013 también usa la pertenencia del sitio de Active Directory como límite de enrutamiento para los servidores de buzones de correo que no pertenecen a ningún DAG y para la interoperabilidad de enrutamiento con versiones anteriores de Exchange. Otros cambios notables en el enrutamiento de Exchange 2013 incluyen:

  - El servicio de transporte de un servidor de buzones de correo nunca se comunica directamente con una base de datos de buzones de correo. En cambio, sí se comunica con el servicio de transporte de buzones en el servidor de buzones de correo. Únicamente el servicio de transporte de buzón de correo se comunica con la base de datos de buzones de correo en el servidor de buzones de correo local. Cuando el servidor de buzones de correo es miembro de un DAG, únicamente el servicio de transporte de buzón de correo en el servidor de buzones de correo que tiene la copia activa de la base de datos de buzones de correo acepta el mensaje para el destinatario final.

  - Únicamente el servicio de transporte de buzón de correo usa llamadas a procedimientos remotos (RPC) al intercambiar mensajes con la base de datos de buzones de correo. Cuando el servidor de buzones de correo es miembro de un DAG, el servicio de transporte de buzón de correo solo usa llamadas a procedimientos remotos (RPC) para comunicarse localmente con las copias activas de las bases de datos de buzones de correo. En otras palabras, RPC nunca se usa para la comunicación entre servidores. En cambio, el servicio de transporte de buzones y el servicio de transporte de diferentes servidores de buzones de correo siempre se comunican mediante SMTP.

  - Exchange 2013 usa colas más precisas para destinos remotos. En lugar de usar una cola para todos los destinos en un sitio de Active Directory remoto, Exchange 2013 pone en cola los mensajes para destinos específicos dentro del sitio de Active Directory, como los conectores de envío individuales.

  - Los conectores vinculados han quedado obsoletos. Un conector vinculado era un conector de recepción vinculado a un conector de envío. Todos los mensajes que recibía el conector de recepción se reenviaron automáticamente al conector de envío.

**Contenido**

Componentes de enrutamiento

  - Destinos de enrutamiento

  - Grupos de entrega

  - Colas

Enrutamiento de mensajes

  - Enrutamiento de mensajes entre sitios de Active Directory

  - Enrutamiento en el servicio de transporte front-end en servidores de acceso de cliente.

  - Enrutamiento en el servicio de transporte de buzones en los servidores de buzones de correo

  - Enrutamiento en el servicio de transporte de los servidores de transporte perimetral

## Componentes de enrutamiento

Cuando el servicio de transporte de un servidor de buzones de correo de Exchange 2013 recibe un mensaje, es necesario categorizarlo. La primera fase de la categorización del mensaje es la resolución de destinatarios. Una vez resuelto el destinatario, se puede determinar el destino final. En la siguiente fase, enrutamiento, se determina cuál es el mejor camino a ese destino. Se generalizó el enrutamiento en Exchange 2013 para aumentar la flexibilidad y reducir la complejidad al incorporar los conceptos de destinos de enrutamiento y grupos de envío.

## Destinos de enrutamiento

En Exchange 2013, el destino final de un mensaje se denomina *destino de enrutamiento*. En Exchange 2013 existen los siguientes destinos de enrutamiento:

  - **Una base de datos de buzones de correo**   Este es el destino de enrutamiento de todos los destinatarios con un buzón en el servidor de buzones de correo en la organización de Exchange. En Exchange 2013, las carpetas públicas son un tipo de buzón de correo, de modo que el enrutamiento de mensajes a destinatarios de carpetas públicas es lo mismo que el enrutamiento de mensajes a destinatarios de buzón de correo.

  - **Un conector**   Un conector se considera un conector de envío para los mensajes SMTP cuando se utiliza como destino de enrutamiento. Un conector de agente de entrega o un conector externo se utiliza como destino de enrutamiento para los mensajes que no son SMTP.

  - **Un servidor de expansión de grupos de distribución**   Este es el destino de enrutamiento cuando un grupo de distribución tiene designado un servidor de expansión que es responsable de ampliar la lista de pertenencias del grupo. Un servidor de expansión de grupo de distribución es, en todos los casos, un servidor de transporte de concentradores o un servidor de buzones de correo de Exchange 2013.

Tenga en cuenta que estos mismos destinos de enrutamiento ya existían en las versiones anteriores de Exchange.

Volver al principio

## Grupos de entrega

Cada destino de enrutamiento en Exchange 2013 tiene un conjunto de uno o más servidores de transporte con la responsabilidad de entregar mensajes a ese destino de enrutamiento. Esta conjunto de servidores de transporte se denomina *grupo de entrega*. Un servidor de transporte puede ser un servidor de buzones de correo de Exchange 2013 o un servidor Exchange 2010 o Exchange 2007 con el rol del servidor Transporte de concentradores instalado. Cuando el destino de enrutamiento es una base de datos de buzones de correo, los servidores de transporte del grupo de entrega tienen la misma versión de Exchange que la base de datos de buzones de correo. Cuando el destino de enrutamiento es un conector o un servidor de expansión de grupo de distribución, el grupo de entrega puede contener una combinación de servidores de buzones de correo de Exchange 2013 y servidores de transporte de concentradores de Exchange 2010 o Exchange 2007. El modo en que se enruta el mensaje depende de la relación entre el servidor de transporte de origen y el grupo de entrega de destino:

  - Si el servidor de transporte de origen está en el grupo de entrega de destino, el destino de enrutamiento será el próximo salto del mensaje. El servidor de transporte de origen envía el mensaje al conector o la base de datos de buzones de correo en un servidor de transporte del grupo de envío. Tenga en cuenta que cuando un servidor de expansión de grupo de distribución es el destino de enrutamiento, el grupo de distribución ya está expandido por la cantidad de veces que los mensajes alcanzan la etapa de enrutamiento de la categorización en el servidor de expansión de grupo de distribución. Por lo tanto, el destino de enrutamiento del servidor de expansión de grupo de distribución siempre es un conector o una base de datos de buzones de correo.

  - Si el servidor de transporte de origen está fuera del grupo de entrega de destino, el mensaje se retransmite mediante la ruta de acceso de enrutamiento de menor costo hacia el grupo de entrega de destino. En función del tamaño y la complejidad de la topología de Exchange, el mensaje se retransmite a otros servidores de transporte mediante la ruta de acceso de enrutamiento de menor costo, o se retransmite directamente a un servidor de transporte en el grupo de entrega de destino.

Existen los siguientes tipos de grupos de entrega en Exchange 2013:

  - **DAG enrutable**   Este es un conjunto de servidores de buzones de correo de Exchange 2013 que pertenecen a un DAG. Las bases de datos de buzones de correo en el DAG son los destinos de enrutamiento a los que presta servicio este grupo de entrega. Una vez que el mensaje llega al servicio de transporte de un servidor de buzones de correo que pertenece al DAG, el servicio de transporte enruta el mensaje al servicio de transporte de buzones del servidor de buzones de correo del DAG que actualmente retiene la copia activa de la base de datos de buzones de correo de destino. Luego, el servicio de transporte de buzón en el servidor de buzones de correo de destino envía el mensaje a la base de datos de buzones de correo local. Aunque un DAG puede incluir servidores de buzones de correo ubicados en sitios diferentes de Active Directory, el DAG es el límite del grupo de entrega.

  - **Grupo de entrega de buzones**   Se trata de un conjunto de servidores Exchange de la misma versión ubicados en un sitio de Active Directory. El sitio de Active Directory es el límite del grupo de entrega. Los destinos de enrutamiento y los grupos de entrega que prestan servicio están divididos según las principales versiones de Exchange en el sitio de Active Directory. Los servidores de transporte de concentradores de Exchange 2010 ubicados en el sitio de Active Directory prestan servicio a las bases de datos de buzones de correo ubicadas en los servidores de buzones de correo de Exchange 2010. Los servidores de transporte de concentradores de Exchange 2007 ubicados en el sitio de Active Directory prestan servicio a las bases de datos de buzones de correo ubicadas en los servidores de buzones de correo de Exchange 2007. El servicio de transporte de los servidores de buzones de correo de Exchange 2013 del sitio de Active Directory prestan servicio a las bases de datos de buzones de correo ubicadas en los servidores de buzones de correo de Exchange 2013 del sitio de Active Directory que no pertenecen a ningún DAG. El modo en que el mensaje se entrega a la base de datos de buzones de correo depende de la versión de Exchange:
    
      - **Exchange 2013**   Una vez que el mensaje llega al servidor de buzones de correo de destino en el sitio de Active Directory de destino, el servicio de transporte usa SMTP para transferir el mensaje al servicio de transporte de buzones. Luego, el servicio de transporte de buzón de correo envía el mensaje a la base de datos de buzones de correo local mediante RPC.
    
      - **Exchange 2010 o Exchange 2007**   Una vez que el mensaje llega a un servidor de transporte de concentradores aleatorio de la misma versión en el sitio de Active Directory de destino, el controlador de almacenamiento en el servidor de transporte de concentradores usa RPC para escribir el mensaje en la base de datos de buzones de correo.

  - **Servidores de origen de conector**   Este es un conjunto combinado de servidores de transporte de concentradores de Exchange 2010 o Exchange 2007, o servidores de buzones de correo de Exchange 2013 que están asignados como servidores de origen para un conector de envío, un conector de agente de entrega o un conector externo. El conector es el destino de enrutamiento al que presta servicio este grupo de enrutamiento. Cuando un conector está asignado a un servidor específico, solo ese servidor tiene permitido enrutar mensajes al destino que define el conector. Este grupo de entrega puede incluir servidores de transporte de concentradores de Exchange 2010 o Exchange 2007, o servidores de buzones de correo de Exchange 2013 ubicados en diferentes sitios de Active Directory.

  - **Sitio de AD**   En algunas circunstancias, un sitio de Active Directory no es el destino final de un mensaje, sino que el mensaje debe pasar por un servidor de transporte de concentradores de Exchange 2010 o Exchange 2007, o por un servidor de buzones de correo de Exchange 2013 en ese sitio de Active Directory. Estas circunstancias son:
    
      - Cuando el sitio de Active Directory está configurado como un sitio del concentrador. Cuando el sitio del concentrador existe en la ruta de acceso de enrutamiento de menor costo para la entrega de mensajes, los mensajes se ponen en cola y el servidor de transporte en el sitio del concentrador los procesa antes de retransmitirlos a su destino final.
    
      - Cuando un servidor Transporte perimetral está suscrito en el sitio de Active Directory. No se puede obtener acceso directo a estos servidores de transporte perimetral inscritos desde otros sitios de Active Directory. Tenga en cuenta que el servidor Transporte perimetral puede ser Exchange 2013, Exchange 2010 o Exchange 2007.
    

    > [!NOTE]
    > Solo se utiliza la distribución ramificada retrasada cuando el grupo de entrega es un sitio de Active Directory. La distribución ramificada retasada intenta reducir el número de transmisiones de mensajes cuando varios destinatarios comparten una parte de la ruta de acceso de enrutamiento de menor costo.



  - **Lista de servidores**   Este es un conjunto de uno o más servidores de transporte de concentradores de Exchange 2010 o Exchange 2007, o servidores de buzones de correo de Exchange 2013 que están configurados como servidores de expansión de grupos de distribución. El servidor de expansión de grupo de distribución es el destino de enrutamiento al que presta servicio este grupo de envío.

La pertenencia al grupo de entrega no es mutuamente exclusiva. Por ejemplo, un servidor de buzones de correo de Exchange 2013 que es miembro de un DAG también puede ser el servidor de origen de un conector de envío definido en el ámbito. Este servidor de buzones de correo pertenecería al grupo de entrega de DAG enrutable para las bases de datos de buzones de correo en el DAG y, también, al grupo de entrega del servidor de origen del conector para el conector de envío definido en el ámbito.

En la siguiente tabla se asignan los destinos de enrutamiento al grupo de entrega en función de la versión de Exchange que corresponda:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Servidor de buzones de correo de Exchange 2013</th>
<th>Servidor de transporte de concentradores de Exchange 2010 o Exchange 2007</th>
<th>Servidor Transporte perimetral en la red perimetral</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Base de datos de buzones de correo en un DAG</p></td>
<td><p>DAG enrutable</p></td>
<td><p>Grupo de entrega de buzón</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="even">
<td><p>Base de datos de buzones de correo fuera de un DAG</p></td>
<td><p>Grupo de entrega de buzón</p></td>
<td><p>Grupo de entrega de buzón</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="odd">
<td><p>Conector</p></td>
<td><p>Servidores de origen del conector</p></td>
<td><p>Servidores de origen del conector</p></td>
<td><p>Sitio de AD</p></td>
</tr>
<tr class="even">
<td><p>Servidor de expansión de grupo de distribución</p></td>
<td><p>Lista de servidores</p></td>
<td><p>Lista de servidores</p></td>
<td><p>n/d</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Colas

Desde el punto de vista del servidor de envío, cada cola de entrega representa el destino de un mensaje concreto. Cuando el servicio de transporte del servidor de buzones de correo de Exchange 2013 selecciona el destino de un mensaje, éste se marca en el destinatario como el atributo **NextHopSolutionKey**. Si se envía un único mensaje a más de un destinatario, cada uno de éstos tiene el atributo **NextHopSolutionKey**. El servidor de recepción también realiza la categorización del mensaje y lo coloca en la cola para su entrega. Después de poner un mensaje en la cola, puede examinar el tipo de entrega para una cola determinada para determinar si un mensaje se volverá a retransmitir cuando llegue al destino del siguiente salto. Todos los valores únicos del atributo **NextHopSolutionKey** corresponden a una cola de entrega por separado.

Para obtener más información, vea la sección "NextHopSolutionKey" en el tema [Colas](queues-exchange-2013-help.md).

Volver al principio

## Enrutamiento de mensajes

Cuando un mensaje debe enviarse a un grupo de entrega remoto, es necesario determinar una ruta de acceso de enrutamiento para el mensaje. Exchange 2013 usa la siguiente lógica para seleccionar la ruta de acceso de enrutamiento de un mensaje. Esta lógica prácticamente no tiene cambios desde Exchange 2010:

1.  Para calcular la ruta de acceso de enrutamiento de menor costo, se suma el costo de los vínculos a sitios IP por los que hay que pasar para alcanzar el destino. Si el destino es un conector, el costo asignado al espacio de nombres se suma al costo para alcanzar el conector seleccionado. Si hay varias rutas de acceso de enrutamiento posibles, se usará la que tenga el menor costo agregado.

2.  Si varias rutas de enrutamiento tienen el mismo costo agregado, se evalúa el número de saltos de cada ruta y se usa la que tenga el menor número de saltos.

3.  Si aún están disponibles varias rutas de acceso de enrutamiento, se considerará el nombre asignado a los sitios de Active Directory antes del destino. Se usará la ruta de enrutamiento cuyo sitio de Active Directory más próximo al destino sea el menor en orden alfanumérico. Si el sitio más próximo al destino es el mismo en todas las rutas de enrutamiento que se están evaluando, se tiene en cuenta el nombre de un sitio anterior.

En Exchange 2010, los destinatarios de los mensajes siempre se asocian a un solo sitio de Active Directory y solo existe un enrutamiento de menor costo desde el sitio de Active Directory de origen hacia el sitio de Active Directory de destino. En Exchange 2013, un grupo de entrega puede extenderse en varios sitios de Active Directory y puede haber varias rutas de acceso de enrutamiento de menor costo a esos sitios de Active Directory. Exchange 2013 designa un solo sitio de Active Directory en el grupo de entrega de destino como *sitio principal*. El sitio principal es el sitio de Active Directory más cercano en función de la lógica de enrutamiento que se describió anteriormente. Para enrutar mensajes correctamente entre grupos de entrega, Exchange 2013 tiene en cuenta los siguientes puntos:

  - **La presencia de uno o más sitios de concentradores en la ruta de enrutamiento de menor costo**   Si la ruta de enrutamiento de menor costo al sitio principal contiene sitios de concentradores, el mensaje se debe enrutar a través de dichos sitios. Se selecciona el sitio de concentradores más cercano en la ruta de acceso de enrutamiento de menor costo como un nuevo grupo de entrega del tipo **AD site**, el cual incluye todos los servidores de transporte en el sitio de concentradores. Una vez que el mensaje pasa por el sitio de concentradores, el enrutamiento del mensaje continúa en la ruta de acceso de enrutamiento. Si el sitio principal es un sitio de concentradores, será considerado como tal por las siguientes razones:
    
      - Si el grupo de entrega de destino se extiende entre varios sitios de Active Directory, el servidor de origen solo debe intentar conectarse a los servidores del sitio de concentradores.
    
      - Se prefieren los servidores en el sitio de concentradores que realmente pertenecen al grupo de entrega de destino.
    
    Al igual que en las versiones anteriores de Exchange, se ignorarán todos los sitios de concentradores que no estén en la ruta de acceso de enrutamiento de menor costo.

  - **El servidor Exchange de destino que se debe seleccionar en el grupo de enrutamiento de destino**   Cuando el grupo de entrega de destino abarca varios sitios de Active Directory, la ruta de enrutamiento a servidores específicos dentro del grupo de entrega puede tener costos diferentes. Los servidores ubicados en el sitio de Active Directory más cercano se seleccionan como los servidores de destino para el grupo de entrega basado en la ruta de acceso de enrutamiento de menor costo. Además, se selecciona el sitio de Active Directory donde se encuentran esos servidores como sitio principal.

  - **Opciones de reserva cuando se producen errores en los intentos de conexión a los servidores del grupo de enrutamiento de destino**   Si el grupo de entrega de destino abarca varios sitios de Active Directory, la primera opción de reserva es el resto de servidores del grupo de entrega de destino de otros sitios de Active Directory que no se hayan seleccionado como servidores de destino. La selección del servidor se realiza en función del costo de la ruta de acceso de enrutamiento a los otros sitios de Active Directory. Si el grupo de entrega de destino tiene servidores en el sitio de Active Directory local, no hay opciones de reserva porque el mensaje ya está lo más cerca posible al destino de enrutamiento de destino. Si el grupo de entrega de destino tiene servidores en sitios de Active Directory remotos, la opción consiste en tratar de conectarse al resto de servidores en el sitio principal. Si esto no funciona, se usa una ruta de interrupción en la ruta de enrutamiento de menor costo al sitio principal. Exchange 2013 intenta enviar el mensaje lo más cerca posible del destino. Para ello, realiza la interrupción, salto por salto, en la ruta de acceso de enrutamiento de menor costo hasta que se efectúa la conexión.

Volver al principio

## Enrutamiento de mensajes entre sitios de Active Directory

La manera en que Exchange 2013 enruta los mensajes entre los sitios de Active Directory es prácticamente igual a que usa Exchange 2010. Para obtener más información, vea [Enrutar el correo entre sitios de Active Directory](route-mail-between-active-directory-sites-exchange-2013-help.md).

Volver al principio

## Enrutamiento en el servicio de transporte front-end en servidores de acceso de cliente.

Esto funciona como un proxy sin estado para todo el tráfico externo de SMTP entrante y (opcionalmente) saliente para la organización de Exchange 2013. Para los mensajes salientes, el servicio de transporte usa conectores de envío para comunicarse con el servicio de transporte frontend en un servidor de acceso de clientes. De manera específica, los mensajes salientes se envían mediante proxy a través del servicio de transporte front-end cuando el parámetro *FrontEndProxyEnabled* de un conector de envío aplicable está establecido en `$true` o cuando se selecciona la opción **Proxy mediante el servidor de acceso de clientes** en las propiedades del conector de envío del Centro de administración de Exchange (EAC). Se seleccionará cualquier servidor de acceso de clientes en el sitio de Active Directory local. Tenga en cuenta que el servicio de transporte front-end no tiene conectores de envío.

Para los mensajes entrantes, el servidor de transporte frontend debe encontrar rápidamente un solo servicio de transporte en buen estado en un servidor de buzones de correo y así recibir la transmisión de mensajes, independientemente del número o tipo de destinatarios. Si no se realiza esto, los remitentes externos verán los resultados del servicio de correo electrónico como no disponibles. Al igual que el servicio de transporte, el servicio de transporte frontend carga las tablas de enrutamiento basadas en la información de Active Directory y usa los grupos de entrega para determinar cómo se enrutan los mensajes. Sin embargo, las tablas de enrutamiento que usa el servicio de transporte de front-end tienen las siguientes características únicas:

  - El servicio de transporte de front-end nunca se considera como miembro de un grupo de entrega, incluso cuando el servidor Buzón de correo y el servidor Acceso de cliente están instalados en el mismo servidor físico. Esto provoca que el servicio de transporte frontend se comunique únicamente con el servicio de transporte.

  - Las tablas de enrutamiento no incluyen rutas de conector de envío.

  - Las tablas de enrutamiento incluyen una lista especial de servidores de buzones de correo en el sitio de Active Directory local para poder realizar rápidamente la conmutación por error.

El enrutamiento en el servicio de transporte de front-end resuelve los destinatarios de mensajes en las bases de datos de buzones de correo. La lista de servidores de Buzón de correo que utiliza el servicio de transporte de front-end está basada en las bases de datos de los destinatarios del mensaje. Tenga en cuenta que es posible que ninguno de los destinatarios tenga buzones de correo, por ejemplo, si el destinatario es un grupo de distribución o un usuario de correo. Para cada base de datos de buzones de correo, el servicio de transporte de front-end busca el grupo de entrega y la información de enrutamiento relacionada. Los grupos de entrega que usa el servicio de transporte de front-end son:

  - DAG enrutable

  - Grupo de entrega de buzón

  - Sitio de AD

Según el número y el tipo de destinatarios, el servicio de transporte de front-end realiza una de las siguientes acciones:

  - Para los mensajes con un único destinatario de buzón de correo, seleccione un servidor de buzones de correo en el grupo de entrega de destino y otorgue preferencia al servidor de buzones de correo en función de la proximidad al sitio del Directorio activo. El enrutamiento del mensaje al destinatario puede implicar el enrutamiento del mensaje mediante un sitio de concentradores.

  - Para los mensajes con varios destinatarios de buzón de correo, use los primeros 20 destinatarios para seleccionar un servidor de buzones de correo en el grupo de entrega más cercano, en función de la proximidad al sitio del Directorio activo. Tenga en cuenta que la bifurcación de mensajes no ocurre en el transporte de front-end, de manera que solo se selecciona un servidor de Buzón de correo, independientemente del número de destinatarios en un mensaje.

  - Si el mensaje no tiene destinatarios de buzón de correo, seleccione un servidor de buzones de correo aleatorio en el sitio de Active Directory local.

Volver al principio

## Enrutamiento en el servicio de transporte de buzones en los servidores de buzones de correo

Esto consta de dos servicios independientes: el servicio de transporte de envío de buzón de correo y el servicio de entrega de transporte de buzón de correo. Para los mensajes entrantes, el servicio de entrega de transporte de buzones recibe mensajes SMTP del servicio de transporte y se conecta a la base de datos de buzones de correo local mediante RPC para enviar el mensaje. Para los mensajes salientes, el servicio de envío de transporte de buzones se conecta a la base de datos de buzones de correo local mediante RPC para recuperar los mensajes y los envía mediante SMTP al servicio de transporte. El servicio de transporte de buzón de correo no tiene estado y no pone en cola los mensajes localmente.

Al igual que el servicio de transporte, el servicio de transporte de buzones carga las tablas de enrutamiento basadas en la información de Active Directory y usa los grupos de entrega para determinar cómo se enrutan los mensajes. Sin embargo, hay aspectos del enrutamiento que son específicos del servicio de transporte de buzón de correo:

  - Debido a que el servicio de transporte y el servicio de transporte de buzones existen en el mismo servidor de buzones de correo de Exchange 2013, el servicio de transporte de buzones siempre pertenece al mismo grupo de entrega que el servidor de buzones de correo. Este grupo de entrega se conoce como el *grupo de entrega local*.

  - El servicio de envío de transporte de buzones no envía mensajes automáticamente al servicio de transporte en el servidor de buzones de correo local ni en otros servidores de buzones de correo de su propio grupo de entrega local. El servicio de envío de transporte de buzones tiene acceso a la misma información de topología de enrutamiento que el servicio de transporte, por lo que puede enviar mensajes al servicio de transporte en servidores de buzones de correo que estén fuera del grupo de entrega. Los servidores de Buzón de correo en el grupo de entrega local se utilizan como opciones de reserva y para el envío a destinatarios sin buzón de correo.

  - El servicio de transporte de buzones solo se comunica con el servicio de transporte en los servidores de buzones de correo de Exchange 2013.

  - El servicio de transporte de buzón de correo solo se comunica con las bases de datos de buzones de correo en el servidor de Buzón de correo local de Exchange 2013. El servicio de transporte de buzón de correo nunca se comunica con bases de datos de buzones de correo en otros servidores de Buzón de correo.

Cuando un usuario envía un mensaje desde su buzón de correo, el servicio de envío de transporte de buzón de correo resuelve los destinatarios del mensaje en las bases de datos de buzones de correo. La lista de servidores de Buzón de correo que usa el servicio de envío de transporte de buzón de correo está basada en las bases de datos de buzones de correo de los destinatarios del mensaje. Tenga en cuenta que es posible que ninguno de los destinatarios tenga buzones de correo, por ejemplo, si el destinatario es un grupo de distribución o un usuario de correo. Para cada base de datos de buzones de correo, el servicio de envío de transporte de buzón de correo busca el grupo de entrega y la información de enrutamiento relacionada. Los grupos de entrega que usa el servicio de envío de transporte de buzón de correo son:

  - DAG enrutable

  - Grupo de entrega de buzón

  - Sitio de AD

Según el número y el tipo de destinatarios, el servicio de envío de transporte de buzón de correo realiza una de las siguientes acciones:

  - Para los mensajes con un único destinatario de buzón de correo, seleccione un servidor de buzones de correo en el grupo de entrega de destino y otorgue preferencia al servidor de buzones de correo en función de la proximidad al sitio del Directorio activo. El enrutamiento del mensaje al destinatario puede implicar el enrutamiento del mensaje mediante un sitio de concentradores.

  - Para los mensajes con varios destinatarios de buzón de correo, use los primeros 20 destinatarios para seleccionar un servidor de buzones de correo en el grupo de entrega más cercano, en función de la proximidad al sitio del Directorio activo.

  - Si el mensaje no tiene destinatarios de buzón de correo, seleccione un servidor de Buzón de correo en el grupo de entrega local.

Cuando el servicio de entrega de transporte de buzones recibe un mensaje del servicio de transporte, acepta o rechaza el mensaje para la entrega a una base de datos de buzones de correo local. El servicio de entrega de transporte de buzón de correo puede entregar el mensaje si el destinatario reside en una copia activa de una base de datos de buzones de correo local. Sin embargo, si el destinatario no reside en una copia activa de una base de datos de buzones de correo local, el servicio de entrega de transporte de buzones no podrá entregar el mensaje y deberá proporcionar una respuesta de no entrega al servicio de transporte. Por ejemplo, si la copia activa de la base de datos de buzones de correo se movió recientemente a otro servidor, es posible que el servicio de transporte transmita un mensaje a un servidor de buzones de correo por error que ahora retiene una copia inactiva de la base de datos de buzones de correo. Entre las respuestas de no entrega que el servicio de entrega de transporte de buzón de buzones devuelve al servicio de transporte se incluyen:

  - Reintentar entrega

  - Generar un NDR

  - Volver a enrutar el mensaje

Volver al principio

## Enrutamiento en el servicio de transporte de los servidores de transporte perimetral

Si tiene un servidor Transporte perimetral instalado en la red perimetral, el servicio de transporte en el servidor Transporte perimetral proporciona retransmisión SMTP y servicios de host inteligente para todo el flujo de correo de Internet. Los mensajes que proceden y se envían a Internet se ponen en la cola de manera local en el servidor Transporte perimetral. Las colas corresponden a los dominios externos o conectores de envío. Para obtener más información, vea la sección "NextHopSolutionKey" en el tema [Colas](queues-exchange-2013-help.md).

Normalmente, cuando se instala un servidor Transporte perimetral en la red perimetral, se suscribe un servidor Transporte perimetral a un sitio de Active Directory. El sitio de Active Directory contiene los servidores de buzones de correo que retransmitirán mensajes hacia y desde el servidor Transporte perimetral. El proceso de suscripción perimetral crea una afiliación de pertenencia al sitio de Active Directory en el servidor de transporte perimetral. La afiliación al sitio permite a los servidores de buzones de correo del sitio de Active Directory retransmitir mensajes al servidor Transporte perimetral para su entrega en Internet sin necesidad de configurar conectores de envío explícitos.

En las configuraciones de varios sitios, el correo saliente procedente de destinatarios internos a destinatarios externos se enruta primero al sitio de Active Directory con suscripción. El sitio de Active Directory de destino es el grupo de entrega. El destino de enrutamiento es el conector de envío interno de la organización en el servicio de transporte de cualquiera de los servidores de buzones de correo en el sitio de Active Directory con suscripción. El *conector de envío interno de la organización* es el conector de envío especial que existe en el servicio de transporte de cada servidor de buzones de correo. Este conector de envío se crea de manera implícita, es invisible, no necesita administración y se usa para retransmitir mensajes entre los servidores de Exchange.

El correo saliente para los destinatarios externos se enruta desde el servidor de buzones de correo al servidor Transporte perimetral. El servidor de acceso de cliente no participa en el enrutamiento de correo a un servidor Transporte perimetral con suscripción. El correo se transmite desde el conector de envío interno de la organización en el servicio de transporte del servidor de buzones de correo hacia un conector de recepción en el servicio de transporte del servidor Transporte perimetral. En un servidor Transporte perimetral con suscripción, el conector de recepción predeterminado se configura para escuchar conexiones de los servidores internos de buzones en el sitio de Active Directory con suscripción y conexiones anónimas procedentes de Internet. Después de que el servicio de transporte categoriza el mensaje en el servidor Transporte perimetral, el mensaje se pone en la cola de manera local para su entrega en Internet mediante el conector de envío dedicado que se crea durante la suscripción perimetral.

El correo entrante procedente de destinatarios externos llega al transporte perimetral a través del conector de recepción predeterminado, y los mensajes se categorizan y se ponen en la cola para su entrega. Los mensajes se retransmiten a través del conector de envío dedicado que se crea mediante la suscripción perimetral para enviar correo a la organización de Exchange. Adónde van después los mensajes depende de cómo se configuran los servidores internos de Exchange.

  - **Servidor de buzones de correo y servidor de acceso de cliente instalados en el mismo equipo**   En esta configuración, el servidor de acceso de cliente se usa para el flujo de correo entrante. El flujo de correo se produce desde el conector de envío en el servicio de transporte del servidor Transporte perimetral al conector de recepción predeterminado en el servicio de transporte front-end del servidor de acceso de cliente, y después al conector de recepción predeterminado en el servicio de transporte del servidor de buzones de correo.

  - **Servidor de buzones de correo y servidor de acceso de cliente instalados en equipos distintos**   En esta configuración, el servidor de acceso de cliente se omite para el flujo de correo entrante. El flujo de correo se produce desde el conector de envío en el servicio de transporte del servidor de transporte perimetral al conector de recepción predeterminado en el servicio de transporte del servidor de buzones de correo.

Si tiene un servidor Transporte perimetral de Exchange 2007 o Exchange 2010 instalado en la red perimetral, el flujo de correo entrante y saliente siempre se produce directamente entre el servidor Transporte perimetral y el servidor de buzones de correo. El servidor de acceso de cliente no se usa.

Volver al principio

