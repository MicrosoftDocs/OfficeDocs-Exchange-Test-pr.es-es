---
title: 'Enrutar el correo entre sitios de Active Directory: Exchange 2013 Help'
TOCTitle: Enrutar el correo entre sitios de Active Directory
ms:assetid: 86b423e3-7bec-4430-9a5a-4f84ce9d82ea
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ916681(v=EXCHG.150)
ms:contentKeyID: 52062042
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Enrutar el correo entre sitios de Active Directory

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Un sitio de Active Directory es un componente de configuración lógica basado en los aspectos físicos de la red. El principal motivo para crear un sitio de Active Directory es definir qué subredes de la red están conectadas de manera que se optimice el control del tráfico de replicación de Active Directory. Microsoft Exchange Server 2013 reconoce los grupos de disponibilidad de base de datos (DAG) y los sitios de Active Directory como límites de enrutamiento, y los servidores de Exchange 2013 toman decisiones de enrutamiento basándose en la topología del sitio de Active Directory.

De forma predeterminada, un bosque de Active Directory contiene solamente un sitio de Active Directory. El nombre predeterminado para este sitio de Active Directory es `Default-First-Site-Name`. Si no se crean otros sitios de Active Directory, todos los equipos que forman parte del dominio en el bosque son miembros de `Default-First-Site-Name`. No es necesario configurar una asociación subred-sitio. Si se crean otros sitios de Active Directory, debe especificar las subredes que se asignan a ese sitio de Active Directory.

**Contenido**

Determinar la pertenencia al sitio

Vínculos de sitio IP

Controlar costes de vínculo a sitios IP

Implementar sitios de concentradores

Detección de topologías

## Determinar la pertenencia al sitio

Cada sitio de Active Directory se asocia con una o varias subredes IP. Un administrador asigna la pertenencia al sitio de Active Directory a los equipos configurados como controladores de dominio y servidores de catálogo global. Otros equipos miembros del dominio, como los servidores de Exchange, se asignan como miembros del sitio de Active Directory de forma automática cuando se configuran para usar una dirección IP que se encuentra en una subred IP asociada a un sitio de Active Directory. Se supone que los equipos que son miembros del mismo sitio de Active Directory tienen buena conectividad de red. Un servidor siempre es miembro de un solo sitio de Active Directory.

Si una aplicación puede determinar que el equipo donde está instalada y otros equipos del bosque pertenecen al sitio de Active Directory y, después, puede usar esa información para controlar el flujo de comunicación, se trata de una aplicación preparada para sitios. Cuando las aplicaciones preparadas para sitios deben usar los servicios de otro servidor, como un controlador de dominio o un servidor de catálogo global, se da prioridad a los servidores que pertenecen al mismo sitio de Active Directory que el equipo que está solicitando esos servicios.

Exchange 2013 es una aplicación preparada para sitios y usa la topología de Active Directory para el enrutamiento de mensajes y para comunicarse con los servicios que se ejecutan en otros equipos de Exchange 2013. El sitio de Active Directory no es sólo un límite de enrutamiento. Es también un límite de detección de servicios.

La determinación de la pertenencia a un sitio de un equipo miembro de un dominio depende de una serie de consultas DNS en las que se compara la dirección IP local con las subredes definidas y, después, se determina la asociación de la pertenencia al sitio correspondiente. Para reducir la sobrecarga que conllevan las consultas de DNS, se ha agregado al esquema de Active Directory de Exchange 2013 el atributo **msExchServerSite** para el objeto de servidor de Exchange. El valor de este atributo es el nombre distintivo del sitio de Active Directory de un servidor de Exchange. Este atributo es una propiedad de cada objeto de servidor de Exchange. Cuando se almacena la afinidad de pertenencia a un sitio como un atributo del objeto de servidor, la topología actual se puede leer directamente desde Active Directory en lugar de utilizar consultas de DNS, y se habilita una asociación de pertenencia al sitio para un equipo que no sea del dominio, por ejemplo, un servidor de transporte perimetral suscrito.

El servicio de topología de Active Directory de Microsoft Exchange rellena el valor del atributo **msExchServerSite** y lo mantiene actualizado. Cuando se inicia un equipo con Windows, el servicio de Net Logon determina si el equipo pertenece al sitio. El servicio de Net Logon usa esa información para buscar los controladores de dominio ubicados en el mismo sitio de Active Directory que el equipo local y, después, dirige las solicitudes de autorización y autenticación a esos servidores. El servicio de topología de Active Directory de Microsoft Exchange usa la llamada API **DsGetSiteName** para recuperar el valor de pertenencia al sitio del servicio Net Logon y escribe el nombre distintivo del sitio de Active Directory en el atributo **msExchServerSite** para el objeto del servidor Exchange en Active Directory.

En la tabla siguiente se muestra cómo podría definir una organización los sitios de Active Directory. En este ejemplo, se definen tres sitios de Active Directory; cada uno de los sitios de Active Directory está asociado a más de una subred IP.

**Ejemplo de una asociación entre un sitio de Active Directory y una subred**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del sitio de Active Directory</th>
<th>Subredes IP asociadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sitio A</p></td>
<td><p>192.168.1.0/24</p>
<p>192.168.2.0/24</p></td>
</tr>
<tr class="even">
<td><p>Sitio B</p></td>
<td><p>192.168.3.0/24</p>
<p>192.168.4.0/24</p></td>
</tr>
<tr class="odd">
<td><p>Sitio C</p></td>
<td><p>192.168.5.0/24</p>
<p>192.168.6.0/24</p></td>
</tr>
</tbody>
</table>


Si un servidor denominado Mailbox01 tiene la dirección IP 192.168.1.1, es miembro del sitio A. Si cambia la dirección IP de un servidor, cambiaría el sitio al que pertenece. Si cambia la dirección IP de Mailbox01 a 192.168.2.1, no cambiará la pertenencia al sitio de Active Directory del servidor porque esta subred también está asociada al sitio A. Sin embargo, si mueve el servidor y la dirección IP cambia a 192.168.3.1, el servidor se consideraría miembro del sitio B.

También se puede producir un cambio de pertenencia a un sitio si cambia la asociación de las subredes con los sitios de Active Directory. Por ejemplo, si quita la asociación de la subred 192.168.3.0 y el sitio B y la asocia al sitio A, la pertenencia de un servidor que tenga la dirección IP 192.168.3.1 también cambiará al sitio A. Siempre que se produce un cambio en la pertenencia a un sitio, Exchange debe actualizar sus datos de configuración para tener en cuenta el cambio cuando Exchange tome decisiones de enrutamiento. Se produce un período de latencia entre el momento en que se produce el cambio en la pertenencia a un sitio de Active Directory y el momento en que el cambio de topología se propaga completamente.

Volver al principio

## Vínculos de sitio IP

Los vínculos a sitios son rutas lógicas entre sitios de Active Directory. Un objeto de vínculo a sitio representa un conjunto de sitios que se pueden comunicar con un coste uniforme. Los vínculos a sitios no corresponden a la ruta real que toman los paquetes de red en la red física. Sin embargo, normalmente, el costo que el administrador asigna al vínculo a sitio está relacionado con la confiabilidad, la velocidad y el ancho de banda disponible en la red subyacente. Por ejemplo, el administrador de Active Directory podría asignar un coste menor a una conexión de red con una velocidad de 100 megabits por segundo (Mbps) que a una conexión de red con una velocidad de 10 Mbps.

De forma predeterminada, todos los vínculos a sitios son transitivos. Esto significa que si el sitio A tiene un vínculo al sitio B y el sitio B tiene un vínculo al sitio C, el sitio A está vinculado al sitio C. El vínculo transitivo entre los sitios A y C también se denomina *puente de vínculo a sitios*.

Exchange usa sólo vínculos de sitios IP para determinar su topología de enrutamiento de sitio de Active Directory. El componente de enrutamiento de Exchange considerará el coste que se asigna al vínculo a sitios IP cuando se calcule una tabla de enrutamiento. Estos costos se usan para calcular la ruta de enrutamiento menos costosa al destino final de un mensaje.

Cada sitio de Active Directory debe estar asociado con al menos un vínculo a sitios IP. Existe un único vínculo a sitios IP predeterminado, llamado `DEFAULTIPSITELINK`. Cuando cree un sitio de Active Directory, debe asociarlo a un vínculo a sitios IP. Puede crear otros vínculos a sitios IP para implementar la topología que desee o puede asociar todos los sitios de Active Directory a `DEFAULTIPSITELINK`. Cada sitio de Active Directory que forma parte de un vínculo a sitios IP se puede comunicar directamente con todos los demás sitios del vínculo con un coste uniforme.

En la figura siguiente, se pueden observar cuatro sitios de Active Directory configurados en el bosque. Se han asociado todos los sitios a `DEFAULTIPSITELINK`. Por lo tanto, cada sitio de Active Directory se comunica directamente con todos los demás sitios con el mismo coste. Se indica más de una ruta de comunicación, pero solo hay definido un vínculo a sitios IP.

**Topología de malla completa con un vínculo de sitio IP único**

![Topología de malla completa con un vínculo de sitio IP único](images/JJ916681.af38d41d-e768-4221-ab4b-b782aa388b73(EXCHG.150).gif "Topología de malla completa con un vínculo de sitio IP único")

En la figura siguiente, se pueden observar cuatro sitios de Active Directory configurados en el bosque. En esta topología, el administrador ha configurado vínculos a sitios IP para crear una *topología de concentrador y radio* de sitios de Active Directory. Todos los sitios radiales se pueden comunicar directamente con el sitio central, y los sitios radiales se pueden comunicar entre sí mediante vínculos a sitios IP transitorios.

**Topología de concentrador y radio de vínculos a sitios IP de Active Directory**

![Topología de concentrador y radio de vínculos de sitio IP](images/JJ916681.eca6cd51-8c2e-4996-81ea-070cd9766ef8(EXCHG.150).gif "Topología de concentrador y radio de vínculos de sitio IP")

Es importante destacar que Exchange usa vínculos a sitios para determinar la ruta de acceso menos costosa, pero siempre intentará entregar los mensajes directamente al servidor Exchange de destino. Por ejemplo, si un usuario en el sitio B de la topología que se muestra en la figura anterior envía un mensaje a otro usuario en el sitio C, el servidor de buzones de correo del sitio B se conectará directamente con el servidor de buzones de correo del sitio C. Si desea forzar los mensajes para que pasen por el sitio A, debe habilitarlo como sitio del concentrador. Para obtener más información acerca de los sitios del concentrador, vea "Implementación de sitios de concentradores" más adelante en este tema.

Los administradores de Active Directory implementan la topología que mejor representa los requisitos de conectividad y comunicación del bosque. Puesto que Exchange usa la misma topología, debe estar seguro de que la topología actual admite una comunicación de mensajería eficaz.

El costo predeterminado para un vínculo a sitio es 100. El costo válido de un vínculo a sitio puede ser cualquier número entre 1 y 99.999. Si especifica vínculos redundantes, siempre se preferirá el vínculo con la menor asignación de costo. Un administrador de organización de Exchange puede asignar un coste específico de Exchange al vínculo a sitios IP. Si se asigna un coste de Exchange a un vínculo a sitios IP, Exchange lo utilizará. De lo contrario, se usa el coste de Active Directory. Para obtener más información acerca de cómo establecer un coste de Exchange en un vínculo a sitios IP, vea "Controlar costes de vínculo a sitios IP" más adelante en este tema. Un administrador que pertenece al grupo Administradores de empresa puede crear vínculos a sitios IP adicionales.

Para obtener más información acerca de la configuración de sitios de Active Directory, vea el artículo sobre el [diseño de topologías de sitios](https://go.microsoft.com/fwlink/p/?linkid=33551).

Volver al principio

## Controlar costes de vínculo a sitios IP

Los costes de los vínculos a sitios IP de Active Directory se calculan en función de la velocidad de red relativa en comparación con todas las conexiones de red en la WAN y están diseñados para producir una topología de replicación fiable y eficaz. Por lo tanto, en la mayoría de los casos, los costes de los vínculos a sitios IP existentes deberían funcionar bien para el enrutamiento de mensajes de Exchange. Sin embargo, si después de documentar el sitio de Active Directory existente y la topología de vínculos a sitios IP, comprueba que los costes de los vínculos a sitios IP de Active Directory y los patrones de flujo del tráfico de red no son óptimos para Exchange, puede realizar ajustes en los costes que evalúa Exchange. Modificar el coste asignado a un vínculo a sitios IP con herramientas de Active Directory podría afectar a todo el entorno. En su lugar, debe usar el cmdlet **Set-AdSiteLink** del Shell de administración de Exchange para asignar un coste específico de Exchange al vínculo a sitios IP. Por ejemplo, para configurar el valor de coste de 25 específico de Exchange en un vínculo a sitios IP denominado SITELINKAB, ejecute el comando siguiente en el Shell: `Set-AdSiteLink SITELINKAB -ExchangeCost 25`.

Al asignar un coste específico de Exchange a un vínculo a sitios IP, el coste de Exchange reemplaza el coste de Active Directory para enrutamiento de mensajes y el enrutamiento sólo tiene en cuenta el coste de Exchange al evaluar la ruta de enrutamiento de menor coste.

Ajustar los costes del vínculo a sitios IP puede ser útil cuando la topología de enrutamiento de mensaje tiene que ser distinta a la topología de replicación de Active Directory. Los costes de Exchange pueden usarse para forzar que todas las rutas de mensajes utilicen un sitio del concentrador. Los costes de Exchange también pueden usarse para controlar dónde hacen cola los mensajes cuando falla la comunicación con el sitio de Active Directory. En la figura siguiente se muestra una topología de Active Directory con cuatro sitios.

**Topología con costos de Exchange configurados en vínculos a sitio IP**

![Topología con costos de Exchange en vínculos de sitio IP](images/JJ916681.56ac2bab-99de-4ddf-b968-80cd34ab8c21(EXCHG.150).gif "Topología con costos de Exchange en vínculos de sitio IP")

En la figura anterior, la conexión de red entre el sitio C y el sitio D es una conexión con poco ancho de banda que solo se usa para la replicación de Active Directory y no se debe usar para el enrutamiento de mensajes. Sin embargo, los costes de vínculos a sitios IP de Active Directory hacen que ese vínculo se incluya en la ruta de enrutamiento menos costosa desde cualquier otro sitio de Active Directory al sitio D. Por lo tanto, los mensajes se entregan a la cola del sitio D en el sitio C. En cambio, el administrador de Exchange prefiere que la ruta de enrutamiento menos costosa incluya el sitio B de manera que, si el sitio D no está disponible, los mensajes se pongan en cola en el sitio B. Si se configura un coste de Exchange alto en el vínculo a sitios IP entre el sitio C y el sitio D, se impide que ese vínculo se incluya en la ruta menos costosa al sitio D.

Exchange es compatible con la configuración de un límite de tamaño máximo de mensaje en un vínculo a sitios IP de Active Directory. De forma predeterminada, Exchange no impone un límite de tamaño de mensaje máximo a los mensajes que se retransmiten entre servidores Exchange en diferentes sitios de Active Directory. Si usa el cmdlet **Set-AdSiteLink** para configurar un tamaño de mensaje máximo en un vínculo del sitio IP de Active Directory, el enrutamiento genera un informe de no entrega (NDR) para los mensajes cuyo tamaño supere el límite máximo configurado en cualquier vínculo del sitio de Active Directory en la ruta de enrutamiento menos costosa. Esta configuración es útil para limitar el tamaño de los mensajes que se envían a sitios remotos de Active Directory y deben comunicarse a través de conexiones de ancho de banda bajo. Para obtener más información, vea [Límites de tamaño de mensaje](message-size-limits-exchange-2013-help.md).

Volver al principio

## Implementar sitios de concentradores

En su organización de Exchange, es posible que quiera forzar la entrega de todos los mensajes a través de un sitio de Active Directory determinado. Puede usar el Shell para designar un sitio de Active Directory como sitio de concentradores. Cuando hace esto, produce una mayor sobrecarga general porque intervienen más servidores en la entrega del mensaje. Por ejemplo, tomemos un mensaje que se va a enviar desde el sitio A al sitio E. Si la ruta de enrutamiento menos costosa es sitio A-sitio B-sitio C-sitio D-sitio E y designa el sitio C como sitio de concentradores, el mensaje se retransmite desde el sitio A al sitio C y, después, desde el sitio C al sitio E.

Use el cmdlet **Set-AdSite** para especificar un sitio de Active Directory como sitio de concentradores. Cuando existe un sitio de concentradores en la ruta de enrutamiento menos costosa para la entrega de mensajes, estos se ponen en cola y el servicio de transporte los procesa en los servidores de buzones de correo del sitio de concentradores antes de su retransmisión al destino final.

Después de elegir la ruta de enrutamiento menos costosa, el enrutamiento determina si existe un sitio de concentradores a lo largo de esa ruta. Si se ha configurado un sitio de concentradores, los mensajes se detendrán en el servidor de buzones de correo del sitio de concentradores, antes de que se retransmitan al destino. Si hay más de un sitio de concentradores en la ruta de enrutamiento menos costosa, los mensajes se detendrán en cada sitio de concentradores de la ruta.

Esta variación del enrutamiento de retransmisión directa solo tendrá lugar cuando el sitio de concentradores se encuentre en la ruta de enrutamiento menos costosa. En la figura siguiente se muestra el uso correcto de un sitio de concentradores. En este diagrama, el sitio B está configurado como sitio de concentradores. Los mensajes que se retransmiten desde el sitio A al sitio D se retransmiten por el sitio B antes de entregarse al sitio D.

**Entrega de mensajes con un sitio de concentradores**

![Entrega de mensajes con un sitio de concentradores](images/JJ916681.93238bcb-6bbc-4a48-aeb0-09342a421b5b(EXCHG.150).gif "Entrega de mensajes con un sitio de concentradores")

En la figura siguiente se muestra cómo los costos de los vínculos a sitios IP afectan al enrutamiento a un sitio de concentradores. En este escenario, se ha designado el sitio B como sitio de concentradores. Sin embargo, el sitio B no existe en la ruta de enrutamiento menos costosa entre el resto de sitios. Por lo tanto, los mensajes que se retransmiten del sitio A al sitio D nunca se retransmiten por el sitio B. Nunca se utiliza un sitio de Active Directory como sitio de concentradores si no se encuentra en la ruta de enrutamiento menos costosa entre dos sitios.

**Sitio de concentradores configurado erróneamente**

![Sitio de concentradores configurado erróneamente](images/JJ916681.c010d4d8-5cd3-4b79-b7db-0367ba3cc287(EXCHG.150).gif "Sitio de concentradores configurado erróneamente")

Cualquier sitio de Active Directory se puede configurar como un sitio de concentradores. Sin embargo, para que esta configuración funcione correctamente, debe tener al menos un servidor de buzones de correo en el sitio de concentradores.

Volver al principio

## Detección de topologías

La topología de Active Directory está disponible para Exchange a través de los elementos necesarios siguientes:

  - El servicio de topología de Active Directory de Microsoft Exchange.

  - El módulo de detección de topologías del servicio de transporte de Microsoft Exchange.

El servicio de topologías de Active Directory de Microsoft Exchange se ejecuta en todos los servidores de buzones de correo y servidores de acceso de cliente de Exchange 2013. Estos servidores usan el servicio de topología de Active Directory de Microsoft Exchange para detectar los controladores de dominio y los servidores de catálogo global que pueden usar los servidores de Exchange para leer y escribir datos de Active Directory. Exchange 2013 enlaza con los servidores de directorio identificados cuando Exchange tiene que leer o escribir en Active Directory.

El módulo de detección de topologías forma parte del servicio de transporte de Microsoft Exchange y proporciona información acerca de la topología de Active Directory a los servidores Exchange. Esta API detecta los servidores Exchange y los roles en la organización y determina su relación con los objetos de configuración de Active Directory. Los datos de configuración se recuperan de Active Directory y se almacenan en caché para que los servicios de Exchange que se ejecutan en ese equipo puedan tener acceso a ellos.

El módulo de detección de topologías lleva a cabo los siguientes pasos para generar una topología de enrutamiento de Exchange:

1.  Se leen datos de Active Directory. Se recuperan todos los objetos siguientes:
    
      - Sitios de Active Directory.
    
      - Vínculos a sitios IP.
    
      - Todos los servidores Exchange.

2.  Los datos recuperados en el paso 1 se usan para crear la topología inicial y para comenzar a vincular y asignar los objetos de configuración relacionados.

3.  Se establecen coincidencias entre los servidores de Exchange y los sitios de Active Directory; para ello, se recupera el valor del atributo de sitio del objeto de servidor de Exchange almacenado en Active Directory.

4.  Las tablas de enrutamiento se actualizan con la colección de información recuperada.

En este proceso, cada servidor Exchange 2013 conoce a los demás servidores Exchange de la organización y la proximidad que hay entre los servidores Exchange.

Volver al principio

