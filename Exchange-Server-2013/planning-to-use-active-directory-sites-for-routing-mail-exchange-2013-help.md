---
title: 'Planeamiento uso Active Directory para enrutamiento correo: Exchange 2013 Help'
TOCTitle: Planeamiento de uso de Active Directory para el enrutamiento de correo
ms:assetid: 0f697cee-bcaa-4c69-b80c-7a2afd1817d2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996299(v=EXCHG.150)
ms:contentKeyID: 52062003
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planeamiento de uso de Active Directory para el enrutamiento de correo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-05-21_

Microsoft Exchange Server 2013 reconoce los sitios de Active Directory y los grupos de disponibilidad de bases de datos (DAG) como límites de enrutamiento. Sin embargo, Exchange 2013 continúa usando la topología de sitios de Active Directory para determinar cómo se transportan los mensajes entre los servidores de Exchange en diferentes DAG o sitios de la organización. Para obtener más información, consulte [Enrutamiento de correo](mail-routing-exchange-2013-help.md).

El servicio de transporte de un servidor de buzones proporciona el transporte de mensajes dentro de la organización de Exchange. Al implementar una organización pura de Exchange 2013 o al introducir Exchange 2013 en una organización pura de Exchange Server 2010, no es necesaria una configuración adicional para establecer un enrutamiento en el bosque.

**Contenido**

Cómo usa Exchange 2013 la pertenencia al sitio de Active Directory

Determinar la pertenencia al sitio de Active Directory

Introducción a los vínculos de sitios IP

Ubicación de servidores de Exchange 2013 en sitios de Active Directory

## Cómo usa Exchange 2013 la pertenencia al sitio de Active Directory

Exchange 2013 es una aplicación preparada para sitios. Las aplicaciones preparadas para sitios pueden determinar su propia pertenencia al sitio de Active Directory y de otros servidores al consultar a Active Directory. Exchange 2013 usa la pertenencia al sitio para determinar qué controladores de dominio y qué servidores de catálogo global debe usar para procesar las consultas a Active Directory. Además, cuando un servidor que ejecuta Exchange tiene que determinar la pertenencia al sitio de Active Directory de otro servidor de Exchange, puede consultar a Active Directory para recuperar el nombre del sitio.

En Exchange 2013, el servicio de topología de Active Directory de Microsoft Exchange es responsable de actualizar el atributo de sitio del objeto servidor de Exchange. Dado que la pertenencia al sitio de Active Directory es un atributo de objeto de servidor, Exchange no tiene que consultar al DNS para resolver la dirección del servidor para una subred que esté asociada con un sitio de Active Directory. El marcado del atributo de sitio de Active Directory en un objeto del servidor de Exchange permite también que se asigne la pertenencia al sitio de Active Directory a un servidor que no sea un miembro de dominio, como un servidor de transporte perimetral suscrito.

Los servidores de Exchange 2013 usan la información de pertenencia al sitio de Active Directory del siguiente modo:

  - **Envío de correo:**  el servicio de envío de transporte de buzones en un servidor de buzones de Exchange 2013 usa la información de pertenencia al sitio de Active Directory para determinar los otros servidores de buzones de Exchange 2013 que están en el mismo sitio de Active Directory. Si el servidor de buzones de origen no pertenece a un DAG, o si el DAG no abarca varios sitios de Active Directory, el servicio de envío de transporte de buzones del servidor de buzones de origen envía mensajes para enrutar y transportar al servicio de transporte de un servidor de buzones de Exchange 2013 del mismo sitio de Active Directory.

  - **Entrega de correo:**  el servicio de transporte de un servidor de buzones de Exchange 2013 realiza la resolución de destinatarios y consulta a Active Directory para hacer coincidir una dirección de correo con una cuenta de destinatario. La información de la cuenta del destinatario incluye el nombre de dominio completo (FQDN) de la base de datos de buzones del usuario. El servicio de transporte consulta a Active Directory para determinar el sitio de Active Directory de la base de datos de buzones del usuario. Si esta base de datos no pertenece a un DAG, entregará un mensaje al servidor de buzones. De lo contrario, se retransmitirá el mensaje a otro servidor de buzones que se encuentre en el mismo sitio que el servidor de buzones de destino para su entrega.

  - **Enrutamiento de mensajes:**  el servicio de transporte de los servidores de buzones de Exchange 2013 extrae información de Active Directory para determinar cómo debe enrutar el correo dentro de una organización. Exchange 2013 usa el concepto de *grupos de entrega* para saber dónde y cómo enrutar los mensajes. En función del destino, el mensaje podría enrutarse al servicio de transporte o al servicio de entrega de transporte de buzones de un servidor de buzones de Exchange 2013, o bien a un servicio de transporte de concentradores que tenga una versión anterior de Exchange. Para obtener más información, consulte [Enrutamiento de correo](mail-routing-exchange-2013-help.md).

  - **Envío de mensajes de mensajería unificada:**  el servicio de mensajería unificada de los servidores de buzones de Exchange 2013 usa la información de pertenencia al sitio de Active Directory para encontrar los otros servidores de buzones que se encuentran en el mismo sitio de Active Directory. El servicio de mensajería unificada envía los mensajes para enrutar al servicio de transporte de un servidor de buzones que está dentro del sitio de Active Directory. El servidor del servicio de transporte hace la resolución de destinatarios y consulta a Active Directory para hacer coincidir un número de teléfono, número E.164 o dirección SIP con una cuenta de destinatario. Después de completar la resolución de destinatarios, el servicio de transporte envía el mensaje al buzón del destinatario como si fuera un mensaje de correo normal.

  - **Conexiones de cliente al servidor de acceso de cliente:**  cuando el servidor de acceso de cliente recibe una solicitud de conexión de un usuario, consulta a Active Directory para determinar qué servidor de buzones hospeda el buzón del usuario. Después, el servidor de acceso de cliente extrae la pertenencia al sitio de Active Directory de dicho servidor de buzones y envía por proxy la conexión al servidor de buzones.

## Determinar la pertenencia al sitio de Active Directory

Los clientes de Active Directory asumen una pertenencia al sitio al hacer coincidir la dirección IP asignada con una subred definida en Sitios y servicios de Active Directory, y asociada a un sitio de Active Directory. Luego, el cliente usa esta información para saber qué controladores de dominio y servidores de catálogo global existen en ese sitio, y se comunica con aquellos servidores de directorio con fines de autenticación y autorización. Exchange 2013 aprovecha esta relación prefiriendo recuperar información sobre los destinatarios desde los servidores de directorio del mismo sitio que el servidor de Exchange 2013.

Se considera que todos los PC que forman parte del mismo sitio de Active Directory están bien conectados, con una conexión de red fiable y de alta velocidad. De manera predeterminada, cuando se implementa primero un bosque de Active Directory, hay un único sitio denominado `Default-First-Site-Name`. Si el administrador no ha configurado manualmente otros sitios, todos los PC clientes y servidores del bosque se consideran miembros de `Default-First-Site-Name`.

Cuando se haya definido más de un sitio, el administrador de Active Directory debe definir las subredes presentes en la organización y asociarlas con sitios de Active Directory.

El servicio Topología de Active Directory de Microsoft Exchange comprueba el atributo de pertenencia al sitio del objeto servidor de Exchange cuando se inicia el servidor. Si no se ha actualizado el atributo del sitio, el servicio de topología de Active Directory de Microsoft Exchange marca el atributo con el nuevo valor. El servicio Topología de Active Directory de Microsoft Exchange comprueba el valor de atributo de sitio cada 15 minutos y actualiza el valor si la pertenencia al sitio ha cambiado. El servicio Topología de Active Directory de Microsoft Exchange utiliza el servicio de Net Logon para obtener la pertenencia al sitio actual. El servicio de Net Logon actualiza la pertenencia al sitio cada cinco minutos. Esto quiere decir que puede transcurrir un período de latencia de hasta 20 minutos entre el momento en el que cambia la pertenencia al sitio y el momento en el que se marca el nuevo valor en el atributo del sitio.

## Introducción a los vínculos de sitios IP

Las relaciones entre sitios de Active Directory están definidas por los vínculos de sitios IP. El vínculo de sitio IP consta de dos o más sitios de Active Directory. Todos los sitios de Active Directory que forman parte del vínculo se comunican por el mismo costo. Las propiedades de un vínculo de sitio IP incluyen una asignación de costo, un programa y un intervalo. Las propiedades de programación e intervalo solo se usan para determinar la frecuencia de replicación de Active Directory. Exchange 2013 usa la asignación de costos para determinar el enrutamiento de menor costo para el tráfico cuando hay varias rutas para el destino. El costo del enrutamiento se determina al agregar el costo de todos los vínculos de sitio de una ruta de transmisión. El administrador de Active Directory asigna el costo a un vínculo en función de la velocidad de red relativa y el ancho de banda disponible en comparación con otras conexiones disponibles.

De forma predeterminada, el servicio de transporte de un servidor de buzones siempre intenta una conexión directa con el servicio de transporte o de entrega de transporte de buzones de un servidor de buzones en otro sitio de Active Directory. Los mensajes en transporte no se retransmiten a través del servicio de transporte de cada servidor de buzones de una ruta de acceso de vínculo de sitio. Sin embargo, los servidores de buzones de sitios de Active Directory intermedios que hay a lo largo de la ruta de acceso de enrutamiento pueden hacer la retransmisión del mensaje en los siguientes escenarios:

  - La retransmisión directa entre servidores de buzones no se produce si hay un sitio de concentrador en la ruta de acceso de enrutamiento de menor costo. Puede configurar un sitio de Active Directory como sitio de concentrador para que los mensajes se enruten a través de este sitio antes de que se retransmitan al servidor de destino. Los sitios de concentradores se explican más adelante en este tema.

  - Exchange 2013 usa la ruta de acceso de enrutamiento obtenida de la información de un vínculo de sitio IP cuando no se puede establecer la comunicación con el sitio de Active Directory de destino. Si no responde ningún servidor de buzones del sitio de Active Directory de destino, la entrega del mensaje se retira de la ruta de acceso de enrutamiento de menor costo hasta que se realiza una conexión con un servidor de buzones de un sitio de Active Directory a lo largo de la ruta de acceso de enrutamiento. Los mensajes se colocan en la cola de este sitio de Active Directory y la cola queda en estado de reintento. Este comportamiento se denomina *cola en punto de error*.

  - En las organizaciones de Exchange 2013 sin DAG, el servicio de transporte de un servidor de buzones también puede usar la información de vínculo de sitio IP para optimizar el enrutamiento de mensajes que se envían a varios destinatarios. El servidor de buzones retrasa la bifurcación de mensajes hasta que alcanza una bifurcación en las rutas de acceso de enrutamiento para los destinatarios. Un servidor de buzones del sitio de Active Directory que representa la bifurcación de las rutas de acceso de enrutamiento individuales retransmite el mensaje bifurcado a cada destino de destinatarios. Esta funcionalidad se denomina *despliegue retrasado*.

## Designar sitios de concentradores

Puede usar el cmdlet **Set-AdSite** para configurar un sitio de Active Directory como sitio de concentradores. Si existe un sitio de concentradores junto con la ruta de acceso de enrutamiento menos costosa entre los dos servidores de transporte, los mensajes se enrutan a través del sitio de concentradores para su procesamiento antes de que se retransmitan al servidor de destino. Para que se dé este comportamiento de enrutamiento, el sitio de concentradores debe existir en la ruta de acceso de enrutamiento de menor costo entre dos servidores de transporte. Esta configuración solo se debe usar cuando la topología de red lo exija, por ejemplo, cuando exista algún firewall entre los sitios de Active Directory y para impedir la retransmisión directa de comunicaciones SMTP. Para obtener más información, consulte [Configuración de enrutamiento de correo de Exchange en Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Configuración de un costo específico de Exchange en un vínculo de sitio IP

Puede usar el cmdlet **Set-AdSiteLink** del Shell de administración de Exchange para configurar un costo específico de Exchange para un vínculo de sitio IP de Active Directory. El costo específico de Exchange es un atributo aparte que se utiliza en lugar del costo asignado por Active Directory para determinar la ruta de enrutamiento de Exchange. Esta configuración es útil cuando los costos de vínculo de sitio IP de Active Directory no dan como resultado una topología de enrutamiento de mensajes de Exchange óptima. Para obtener más información, consulte [Configuración de enrutamiento de correo de Exchange en Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Configurar restricciones de tamaño de mensajes en vínculos de sitio IP

De forma predeterminada, Exchange 2013 no impone un límite de tamaño de mensaje máximo a los mensajes que se retransmiten entre servidores de buzones ubicados en sitios de Active Directory diferentes. Si usa el cmdlet **Set-AdSiteLink** para configurar un tamaño de mensaje máximo en un vínculo de sitio IP de Active Directory, el enrutamiento genera un informe de no entrega (NDR) para los mensajes cuyo tamaño supere el límite máximo configurado en cualquier vínculo de sitio de Active Directory de la ruta de acceso de enrutamiento menos costosa. Esta configuración es útil para limitar el tamaño de los mensajes que se envían a sitios remotos de Active Directory y que deben comunicarse a través de conexiones de ancho de banda bajo.

## Ubicación de servidores de Exchange 2013 en sitios de Active Directory

Para que el enrutamiento de mensajes entre los servidores de Exchange 2013 se produzca correctamente, todos los servidores de Exchange implementados en el bosque deben pertenecer a un sitio de Active Directory. Asegúrese de que las direcciones IP que ha asignado estén en subredes asociadas correctamente con sitios de Active Directory.

El primer paso para planear la ubicación de servidores de Exchange 2013 en la topología de sitio de Active Directory es documentar la topología actual. La documentación debe incluir lo siguiente:

  - Sitios

  - Subredes y su asociación de sitios

  - Vínculos de sitio IP y sus sitios miembros

  - Costos de vínculo de sitio IP

  - Servidores de directorio de cada sitio

  - Conexiones de red físicas

  - Ubicaciones de firewall

Una vez que haya realizado el diagrama de estos objetos, planee la ubicación de servidores de Exchange. Al momento de decidir dónde colocar los servidores, tenga en cuenta la siguiente información:

  - Un servidor de buzones necesita comunicarse directamente con un servidor de catálogo global para realizar búsquedas en Active Directory.

  - Le recomendamos implementar más de un servidor de buzones en cada sitio de Active Directory para ofrecer equilibro de carga y tolerancia a errores.

  - DAG y resistencia del sitio

  - El servicio de mensajería unificada de los servidores de buzones envía mensajes de correo de voz al servicio de transporte de los servidores de buzones para la entrega a los buzones. El servidor de acceso de cliente que ejecuta el servicio de enrutamiento de llamadas de mensajería unificada puede encontrarse en un sitio de concentradores o cerca de la puerta de enlace de IP o de voz por IP (VoIP), una central de conmutación (IP PBX), una PBX habilitada con SIP o controladores de borde de sesión (SBC). El servicio de transporte de un servidor de buzones que tiene la misma pertenencia al sitio que el servidor de acceso de cliente recibirá mensajes de correo de voz para el transporte y enrutamiento de mensajes al servicio de transporte de otros servidores de buzones de la organización.

  - Los servidores de acceso de cliente ofrecen un punto de conexión con la organización de Exchange para usuarios que accedan a Exchange de forma remota. En cada sitio de Active Directory que contenga servidores de buzones debe implementarse un servidor de acceso de cliente.

Una vez que haya planeado la ubicación del servidor de Exchange 2013, puede identificar áreas en las que modificar la topología del sitio de Active Directory para mejorar el flujo de la comunicación. Puede ajustar los vínculos de sitio IP y los costos de vínculo de sitio para optimizar la entrega de correo. Una topología eficiente de Active Directory no requiere ningún cambio para admitir Exchange 2013

