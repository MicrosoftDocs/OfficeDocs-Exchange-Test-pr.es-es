---
title: 'Grupos de búsqueda de mensajería unificada: Exchange 2013 Help'
TOCTitle: Grupos de búsqueda de mensajería unificada
ms:assetid: 026129a1-b0b5-410a-bed6-2d49f85205b3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa995918(v=EXCHG.150)
ms:contentKeyID: 50556730
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Grupos de búsqueda de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-18_

Un grupo de extensiones de telefonía proporciona una forma de distribuir las llamadas telefónicas desde un solo número a varias extensiones o números de teléfono. En la mensajería unificada, un grupo de extensiones de mensajería unificada es una representación lógica de un grupo de extensiones de telefonía y enlaza una puerta de enlace IP de mensajería unificada a un plan de marcado de mensajería unificada.

¿Está buscando tareas de administración relacionadas con los grupos de extensiones de mensajería unificada? Consulte [Procedimientos de grupo de captura de mensajería unificada](um-hunt-group-procedures-exchange-2013-help.md).

**Contenido**

¿Qué es un grupo de extensiones?

¿Qué es un número piloto?

¿Qué es un grupo de extensiones de mensajería unificada?

## ¿Qué es un grupo de extensiones?

*Grupo de extensiones* es un término empleado para describir un grupo de central de conmutación (PBX) o IP-PBX, o bien números de extensión que comparten los usuarios. Los grupos de extensiones se usan para distribuir las llamadas de forma eficaz dentro o fuera de una unidad de negocio determinada. Al crear y definir un grupo de extensiones se reduce la posibilidad de que la persona que efectúe una llamada entrante reciba una señal de línea ocupada cuando se recibe la llamada.

Los grupos de extensiones se usan para ubicar una línea abierta, extensión o canal cuando se recibe una llamada entrante. Las llamadas se "distribuyen" a la siguiente línea disponible cuando una línea telefónica principal está ocupada o no contesta. La parte llamante obtiene una señal de línea ocupada o se envía al correo de voz si no hay extensiones abiertas en el grupo. Por ejemplo, una PBX o IP-PBX se puede configurar para tener 10 números de extensión para el departamento de ventas. Los 10 números de extensión del departamento de ventas se deben configurar como un grupo de extensiones.

La configuración de un grupo de extensiones simple incluye un nombre, un número de extensión, una lista de miembros del grupo disponibles y un método de selección del grupo de extensiones. El método de selección del grupo de extensiones determina el orden en el que se presentan las llamadas entrantes a los miembros del grupo de extensiones.

Hay varios algoritmos o métodos que una PBX o IP PBX puede usar para ubicar una línea abierta, extensión o canal. Entre ellos se incluyen:

  - **Extensión de grupo o llamar a todas las extensiones**    Cuando se recibe una llamada entrante en el número de extensión del grupo de extensiones, la PBX o IP PBX llama a todos los números de extensiones del grupo.

  - **Empezar por el número más bajo o extensiones lineales**   Es la configuración por defecto en la mayoría de PBX e IP PBX. Con este método, las llamadas se dirigen a la primera línea inactiva por orden secuencial, empezando por la primera línea del grupo. Esta configuración se encuentra más a menudo en los teléfonos multilínea en pequeñas empresas.

  - **Operación por turnos o extensiones circulares**   Con este método, las llamadas se dirigen a la primera línea inactiva, empezando por la línea después de la que atendió la última llamada. Cuando las llamadas se distribuyen usando el método "operación por turnos", si una llamada se entrega a la línea 1, la siguiente pasa a la línea 2, la siguiente a la línea 3, etcétera. Este proceso continúa incluso si una de las líneas anteriores queda libre. Cuando se alcanza el final del grupo de extensiones, se vuelve a empezar por la primera línea. Las líneas solo se saltan si todavía están ocupadas con una llamada anterior. Las extensiones circulares o la operación por turnos distribuyen las interrupciones de forma equilibrada en todas las llamadas, minimizando la posibilidad de una interrupción grave en el servicio.

  - **Más inactiva o extensiones de distribución uniforme**    Con este método, la llamada se dirige a la primera línea disponible del grupo que ha estado inactivo durante más tiempo. Este método usa el período de tiempo que la persona que recibe la llamada ha estado ocupada en vez de si la línea está disponible. Este método normalmente se usa en grandes centros de llamadas donde las llamadas entrantes las responden personas y la carga se distribuye de forma uniforme entre los grupos de números de extensiones.

Puede configurar uno o varios grupos de extensiones. Cada grupo de extensiones debe incluir un mínimo de dos líneas. Si un número ya se usa en un grupo de extensiones, no estará disponible para otro.

A continuación tiene ejemplos de grupos de extensiones de telefonía simples y cómo funcionan.

**Ejemplo 1**

La extensión 300 (número piloto) está programada para que cuando se reciba una llamada, suene la extensión 301, a continuación la 302, a continuación la 303, a continuación la 304.

1.  La extensión 301 está ocupada.

2.  La extensión 302 suena y no responde.

3.  La extensión 303 contesta la llamada.

4.  La extensión 304 está libre y a la espera de una llamada entrante.

**Ejemplo 2**

La extensión 1000 (número piloto) está programada para que cuando se reciba una llamada, suenen de la extensión 2000 a la 2003 a la vez.

1.  La extensión 2000 está libre.

2.  La extensión 2001 está libre.

3.  La extensión 2002 está libre.

4.  La extensión 2003 contesta la llamada entrante.

¿Qué es un grupo de extensiones?

## ¿Qué es un número piloto?

En una red telefónica, se puede configurar una PBX o IP-PBX para que tenga uno o varios grupos de extensiones. Cada grupo de extensiones creado en una PBX o IP PBX debe tener un *número piloto* asociado. Usar un número piloto ayuda a eliminar las señales de disponibilidad y contribuye a enrutar las llamadas entrantes a los números de extensión disponibles. La PBX o IP-PBX utiliza el número piloto para localizar el grupo de extensiones y, a su vez, localizar el número de extensión del teléfono en que se ha recibido la llamada entrante y las extensiones asignadas al grupo de extensiones. Si no se ha definido un número piloto, la PBX o IP-PBX no puede localizar dónde se ha recibido la llamada entrante.

El número piloto es la dirección, extensión o ubicación del grupo de extensiones dentro de la PBX o IP-PBX. Normalmente es un número de extensión en blanco o un número de extensión procedente de un grupo de extensiones de números de extensión que no tiene ninguna persona ni teléfono asociado. Por ejemplo, puede configurar un grupo de captura en una PBX o IP-PBX para incluir los números de extensión 4100, 4101, 4102, 4103, 4104 y 4105. El número piloto de dicho grupo de captura se configura como la extensión 4100. Cuando se recibe una llamada en el número de extensión 4100, la PBX o IP-PBX busca el siguiente número de extensión disponible para determinar el lugar en que depositar la llamada. En este caso, la PBX o IP-PBX usará el algoritmo de búsqueda programado para buscar los números de extensión 4101, 4102, 4103, 4104 y 4105.

Usar un número piloto ayuda a eliminar las señales de disponibilidad y contribuye a enrutar las llamadas entrantes a los números de extensión disponibles. En mensajería unificada, el número piloto de la PBX o IP PBX se usa como destino. Si ninguno de los números de extensión del grupo de extensiones responde a una llamada entrante, la llamada se dirige al servidor de buzones de correo que ejecuten el servicio de mensajería unificada de Microsoft Exchange.

¿Qué es un grupo de extensiones?

## ¿Qué es un grupo de extensiones de mensajería unificada?

Los grupos de extensiones de mensajería unificada son fundamentales para el funcionamiento del sistema de mensajería unificada. Un grupo de extensiones de mensajería unificada es una representación lógica de un grupo de extensiones de una PBX o IP-PBX existente. Se usa para enlazar una puerta de enlace IP de mensajería unificada con un plan de marcado de mensajería unificada. Un solo grupo de extensiones de mensajería unificada también puede enlazar varias puertas de enlace IP de mensajería unificada con un plan de marcado de mensajería unificada. De forma predeterminada, al crear una puerta de enlace IP de mensajería unificada y asociarla a un plan de marcado de mensajería unificada, se crea un grupo de extensiones de mensajería unificada y también puede crear otros grupos de extensiones. Debe crear al menos un grupo de extensiones de mensajería unificada.

Los grupos de extensiones de mensajería unificada se utilizan para localizar el grupo de extensiones de una PBX o IP-PBX del que se ha recibido la llamada entrante. Un número piloto definido para un grupo de extensiones en la PBX o IP-PBX también debe definirse en el grupo de extensiones de mensajería unificada. El número piloto se utiliza para hacer coincidir la información existente para las llamadas entrantes a través de la información de mensajes de señalización SIP (Protocolo de inicio de sesión) en el mensaje de voz. El número piloto permite que los servidores de Exchange interpreten la llamada con el plan de marcado de llamadas adecuado para enrutar la llamada correctamente. La ausencia de un grupo de extensiones impide que los servidores de Exchange conozcan la ubicación de la llamada entrante. Conocer la ubicación de las llamadas entrantes permite que los servidores de Exchange acepten la información del encabezado de la llamada que se pasa desde la puerta de enlace VoIP, la IP PBX o la PBX con SIP habilitado. Es de vital importancia configurar los grupos de extensiones de mensajería unificada adecuadamente, ya que no se responderán las llamadas entrantes que no coincidan exactamente con el número piloto definido en el grupo de extensiones de mensajería unificada y no se producirá el enrutamiento de las llamadas entrantes.

Al crear un grupo de extensiones de mensajería unificada en implementaciones locales e híbridas, se habilitan todos los servidores de buzones y de acceso de cliente, independientemente de si se han añadido a un plan de marcado de mensajería unificada, para comunicarse con una puerta de enlace VoIP, una IP PBX o una PBX con SIP habilitado. Esto se debe a que todos los servidores de acceso de cliente y de buzones de correo responden a las llamadas entrantes de todos los planes de marcado, en vez de un plan de marcado de mensajería unificada concreto como el servidor de mensajería unificada hacía en versiones anteriores de Exchange. Si elimina el grupo de extensiones de mensajería unificada, la puerta de enlace IP de mensajería unificada no podrá responder a las llamadas entrantes desde una puerta de enlace VoIP, IP PBX o PBX con SIP habilitado ni colocar llamadas saliente a través de la puerta de enlace VoIP, IP PBX o PBX con SIP habilitado usando el número piloto especificado.

Sin embargo, si integra la mensajería unificada con Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server en implementaciones locales e híbridas, debe agregar todos los servidores de acceso de cliente y de buzones de correo a todos los planes de marcado URI de SIP creados para trabajar con Communications Server 2007 R2 o Lync Server. Esto permite el enrutamiento de llamadas y las llamadas externas para que funcionen correctamente.

Para obtener más información acerca de las puertas de enlace IP de mensajería unificada, vea [Puertas de enlace IP de mensajería unificada](um-ip-gateways-exchange-2013-help.md) (en inglés).

