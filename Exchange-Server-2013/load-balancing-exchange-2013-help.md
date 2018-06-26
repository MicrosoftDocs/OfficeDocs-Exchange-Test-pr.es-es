---
title: 'Equilibrio de carga: Exchange 2013 Help'
TOCTitle: Equilibrio de carga
ms:assetid: f572c193-6f3a-400e-9085-a9d3e5e18c59
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ898588(v=EXCHG.150)
ms:contentKeyID: 51406571
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Equilibrio de carga

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

El equilibrio de carga es una forma de administrar cuál de sus servidores recibe tráfico. El equilibrio de carga ayuda a distribuir las conexiones de clientes entrantes en una variedad de extremos, por ejemplo, servidores de acceso de cliente, para garantizar que ningún extremo se haga cargo de una parte desproporcionada de la carga. El equilibrio de carga también puede proporcionar redundancia de conmutación por error en caso de que se produzcan errores en uno o más extremos. Usando el equilibrio de carga con Exchange Server 2013, garantiza que los usuarios continúen recibiendo el servicio de Exchange en caso de un error del equipo. El equilibrio de carga también permite que la implementación pueda administrar más tráfico del que puede procesar un servidor al ofrecer un nombre de host único para sus clientes.

El equilibrio de carga sirve para dos propósitos principales. Reduce el impacto de un error en un solo servidor de acceso de cliente en uno de sus sitios de Active Directory. Además, el equilibrio de carga garantiza que la carga de cada uno de los servidores de acceso de cliente esté distribuida uniformemente.

Exchange 2013 también incluye las siguientes soluciones para la redundancia de conmutación por error y de cambios:

  - **Alta disponibilidad**Exchange 2013 usa grupos de disponibilidad de bases de datos (DAG) para mantener varias copias de sus buzones de correo en diferentes servidores sincronizados. De esta forma, si se produce un error en una base de datos de buzones en un servidor, los usuarios se pueden conectar a una copia sincronizada de la base de datos en otro servidor.

  - **Resistencia de sitios** Puede implementar dos sitios de Active Directory en ubicaciones geográficas diferentes, mantener los datos de buzones de correo sincronizados entre ambos y hacer que uno de los sitios se haga cargo de la carga completa en el caso de que se produzca un error en el otro.

  - **Movimientos de buzón en línea** En un movimiento de buzón en línea, los usuarios tienen acceso a sus cuentas de correo electrónico durante el movimiento. Se bloquea el acceso de los usuarios a las cuentas solo durante un breve período al final del proceso, cuando se produce la sincronización final. Puede realizar movimientos de buzones de correo en línea entre bosques o en el mismo bosque.

  - **Redundancia de instantáneas** La redundancia de instantáneas protege la disponibilidad y capacidad de recuperación de mensajes mientras están en tránsito. Con la redundancia de instantáneas, la eliminación de un mensaje de las bases de datos de transporte se retrasa hasta que el servidor Transporte comprueba que todos los saltos que debe ir superando el mensaje se han completado. Si alguno de esos saltos da error antes de que se informe de que la entrega ha sido correcta, el mensaje se reenvía para su entrega al salto que no se completó.

## Cambios en la arquitectura del equilibrio de carga de Exchange Server 2013

En Exchange Server 2010, los procesamientos y las conexiones de clientes los administraba el rol de servidor Acceso de clientes. Esto requería que las conexiones de Outlook externas e internas, así como las conexiones de clientes de terceros y de dispositivos móviles, tengan la carga equilibrada en toda la matriz de servidores de acceso de cliente de una implementación para alcanzar una tolerancia a errores y un uso eficiente de los servidores. Muchos protocolos de acceso de cliente de Exchange 2010 requerían afinidad: una relación entre el cliente y un servidor de acceso de cliente concreto. En particular, Outlook Web App, el Panel de control de Exchange, servicios Web Exchange, Outlook en cualquier lugar, conexiones TCP/IP MAPI de Outlook, Exchange ActiveSync, el servicio de libreta de direcciones de Exchange y PowerShell remoto necesitaban o se beneficiaban de la afinidad del servidor de acceso de cliente a cliente. Las opciones de equilibrio de carga en Exchange 2010 incluían lo siguiente:

  - Equilibrio de carga de red de Windows con afinidad de IP de origen

  - Equilibrio de carga de hardware

Debido a las diferentes necesidades de los protocolos de cliente en Exchange 2010, recomendamos el uso de una solución de equilibrio de carga de 7 capas. El equilibrio de carga de 7 capas, también conocido como equilibrio de carga en el nivel de la aplicación, permitía que la solución de equilibrio de carga use reglas complejas para determinar cómo equilibrar cada solicitud que entraba en el sistema, teniendo en cuenta que toda la conversación entre el cliente y el servidor estaría disponible para la lógica del equilibrador de carga. Estas reglas complejas garantizaban que todas las solicitudes de un cliente concreto fueran al mismo extremo del servidor de acceso de cliente. En Exchange 2010 , si todas las solicitudes de un cliente concreto no iban al mismo extremo para los protocolos que requerían afinidad, la experiencia del usuario se vería afectada negativamente. Para obtener más información acerca de las opciones de equilibrio de carga de Exchange 2010, consulte [Descripción del equilibrio de carga en Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=196447).

En Exchange Server 2013, hay dos tipos principales de servidores: el servidor de acceso de cliente y el servidor de buzones de correo. Los servidores de acceso de cliente de Exchange 2013 se usan como servidores proxy ligeros y sin estado que permiten a los clientes conectarse con servidores de buzones de correo de Exchange 2013. Los servidores de acceso de cliente de Exchange 2013 proporcionan un espacio de nombres y una autenticación unificados. Además, los servidores de acceso de cliente de Exchange 2013:

  - Son compatibles con la lógica de redirección y de proxy para protocolos de cliente.

  - Admiten el uso del equilibrio de carga de 4 capas.

Con afinidad de sesión y equilibrio de carga de 7 capas, todas las solicitudes entre el cliente y el servidor se envían al mismo extremo, como lo requieren varios protocolos. Las solicitudes se distribuyen en el nivel de la aplicación. Con el equilibrio de carga de 4 capas, las solicitudes se distribuyen en la capa de transporte. La solución de equilibrio de carga distribuye las solicitudes desde el cliente, que tiene conocimiento de una sola dirección IP (a veces denominada dirección IP virtual o VIP), hacia un conjunto de servidores que realizan el trabajo. La conexión entre el cliente y el servidor se debe establecer antes de que se determine el contenido de la solicitud, a fin de que el equilibrador de carga seleccione un servidor para que reciba la solicitud antes de examinar su contenido. La selección del servidor de destino se puede realizar de varias formas, como “round robin”, donde cada conexión entrante pasa al siguiente servidor de destino en una lista circular, o “menor número de conexiones”, donde el equilibrador de carga envía cada nueva conexión al servidor con menos conexiones establecidas en ese momento. Ahora que la afinidad de sesión no es necesaria, tiene más flexibilidad, opciones y simplicidad respecto de la arquitectura del equilibrio de carga que implemente. El equilibrio de carga sin afinidad de sesión le permite incrementar la capacidad y el uso del equilibrador de carga, ya que el procesamiento no se usa para mantener más opciones de afinidad implicadas, como el equilibrio de carga basado en cookies o el identificador de sesión de la Capa de sockets seguros (SSL).

## Matrices de servidores de acceso de cliente y Exchange 2013

En Exchange 2010, presentamos el concepto de una matriz de acceso de cliente. Después de configurar una matriz de acceso de cliente para un sitio de Active Directory, todos los servidores de acceso de cliente del sitio automáticamente se convertían en miembros de la matriz. En las versiones actuales de Exchange 2013, no se requiere la configuración de una matriz de acceso de cliente, ya que la implementación de un servicio con carga equilibrada y altamente disponible es mucho más simple.

## Soluciones de equilibrio de carga

El uso de equilibradores de carga de hardware todavía es compatible en Exchange 2013. Para más información sobre las soluciones de equilibrio de carga de hardware que han superado las pruebas de soluciones con Exchange 2010 y que probablemente funcionen igual de bien con Exchange 2013, consulte [Implementación del equilibrador de carga de Exchange Server 2010](https://go.microsoft.com/fwlink/p/?linkid=261834). Recuerde que en esta página se muestra una configuración de 7 capas más compleja de los equilibradores de carga de hardware con Exchange 2010. Realizar el equilibro de carga del tráfico de Exchange 2013 puede ser mucho más simple, teniendo en cuenta los cambios de arquitectura mencionados anteriormente en este tema. En vez de configurar la afinidad de sesión para cada protocolo de Exchange, las conexiones entrantes a los servidores de acceso del cliente de Exchange 2013 se pueden dirigir a un servidor disponible mediante el equilibrador de carga sin necesidad de realizar más procesamientos. El equilibrador de carga de hardware todavía juega un rol importante para proporcionar alta disponibilidad del servicio de Exchange, ya que puede detectar cuándo un servidor de acceso de cliente concreto ha dejado de estar disponible y se ha quitado del conjunto de servidores que administrarán las conexiones entrantes.

## Equilibrio de carga de red de Windows

El equilibrio de carga de red de Windows (WNLB) es un equilibrador de carga de software común usado para los servidores Exchange. Existen varias limitaciones asociadas con la implementación de WNLB con Microsoft Exchange.

  - WNLB no se puede usar en servidores Exchange donde también se estén usando DAG de buzón debido a la incompatibilidad de WNLB con los clústeres de conmutación por error de Windows. Si se usa un DAG de Exchange 2013 y desea usar WNLB, debe ejecutar el rol de servidor de acceso de cliente y el rol de servidor de buzón en servidores diferentes.

  - WNLB no detecta las interrupciones de servicio. WNLB solamente detecta las interrupciones del servidor por su dirección IP. Esto significa que si se produce un error en un servicio web específico, como Outlook Web App, pero el servidor sigue funcionando, WNLB no detectará el error y continuará enrutando las solicitudes a ese servidor de acceso de cliente. Se requiere intervención manual para quitar el servidor de acceso de cliente que está experimentando la interrupción desde el conjunto de equilibrios de carga.

  - El uso de WNLB puede provocar el desbordamiento de puertos, lo que a su vez puede saturar las redes.

  - Dado que WNLB solamente realiza afinidad de cliente mediante el uso de la dirección IP, no es una solución eficaz cuando el conjunto de IP de origen es demasiado pequeño. Esto puede ocurrir cuando el conjunto de IP de origen proviene de la subred de una red remota o cuando su organización usa traducción de direcciones de red.

