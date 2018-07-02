---
title: 'Alta disponibilidad y resistencia de sitios: Exchange 2013 Help'
TOCTitle: Alta disponibilidad y resistencia de sitios
ms:assetid: 6628285e-d07c-443d-866b-be784ad1ed1e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638137(v=EXCHG.150)
ms:contentKeyID: 48268227
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Alta disponibilidad y resistencia de sitios

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-15_

Puede proteger sus bases de datos de buzones de correo de Exchange Server 2013 y los datos que contienen configurando los servidores de buzones de correo y las bases de datos para que tengan alta disponibilidad y resistencia de sitios. Exchange 2013 minimiza el coste y la complejidad de la implementación de una solución de mensajería altamente disponible y resistente, al tiempo que proporciona mayores niveles de disponibilidad de servicio y datos, y admitir buzones de mayor tamaño.

Exchange 2013 permite a los clientes de todos los tamaños y segmentos implementar de manera económica un servicio de continuidad de mensajería en su organización mediante la integración de funcionalidades de replicación nativas y una arquitectura de alta disponibilidad disponibles por primera vez con Exchange 2010. Para obtener una lista de los cambios respecto a Exchange 2010 y Exchange 2007, vea [Cambios en la alta disponibilidad y resistencia de sitios respecto a versiones anteriores](changes-to-high-availability-and-site-resilience-over-previous-versions-exchange-2013-help.md).

**Contenido**

Terminología básica

Grupos de disponibilidad de base de datos

Copias de bases de datos de buzones de correo

Active Manager

Resistencia de sitios

API de replicación de terceros

Documentación de alta disponibilidad y resistencia de sitios

## Terminología básica

Los siguientes términos clave son importantes a la hora de entender qué es la alta disponibilidad o la resistencia de sitios:

  - *Active Manager*  
    Componente interno de Exchange que se ejecuta en el servicio de replicación de Microsoft Exchange responsable de supervisar errores y de tomar acciones correctivas a través de la conmutación por error en un grupo de disponibilidad de bases de datos (DAG).

<!-- end list -->

  - *AutoDatabaseMountDial*  
    Valor de propiedad de un servidor de buzones de correo que determina si una copia de base de datos pasiva se monta automáticamente como una nueva copia activa, en función del número de archivos de registro que le falten a la copia que se va a montar.

<!-- end list -->

  - *Replicación continua, modo de bloque*  
    En el modo de bloque, como cada actualización se escribe en el búfer de registro activo de la copia de base de datos activa, también se incluye en un búfer de registro de cada una de las copias de buzones pasivos en el modo de bloque. Cuando se llena el búfer de registro, cada copia de base de datos genera, inspecciona y crea el siguiente archivo de registro en la secuencia de generación.

<!-- end list -->

  - *Replicación continua, modo de archivo*  
    En el modo de archivo, los archivos de registro de transacciones cerradas se transfieren de la copia de bases de datos activa a una o más copias de bases de datos pasivas.

<!-- end list -->

  - *Grupo de disponibilidad de base de datos*  
    Grupo de hasta 16 servidores de buzones de correo de Exchange 2013 que hospeda un conjunto de bases de datos replicadas.

<!-- end list -->

  - *Movilidad de la base de datos*  
    La capacidad de una base de datos de buzones de correo de Exchange 2013 de replicarse y montarse en otros servidores de buzones de correo de Exchange 2013.

<!-- end list -->

  - *Centro de datos*  
    Normalmente, esto se refiere a un sitio de Active Directory, aunque también puede referirse a un sitio físico. En el contexto de esta documentación, el centro de datos equivale al sitio de Active Directory.

<!-- end list -->

  - *modo de coordinación de activación de centro de datos*  
    Propiedad de la configuración del DAG que, cuando está habilitada, fuerza al servicio de replicación de Microsoft Exchange a que adquiera permisos para montar bases de datos en el inicio.

<!-- end list -->

  - *Recuperación ante desastres*  
    Cualquier proceso que sirve para recuperarse manualmente de un error. Puede tratarse de un error que afecta a un único elemento o a toda la ubicación física.

<!-- end list -->

  - *API de replicación de terceros de Exchange*  
    API que Exchange suministra y que permite usar la replicación sincrónica de terceros para un DAG en lugar de la replicación continua.

<!-- end list -->

  - *Alta disponibilidad*  
    Solución que ofrece disponibilidad de servicio, disponibilidad de datos y recuperación automática de los errores que afectan al servicio o a los datos (como un error de red, de almacenamiento o de servidor).

<!-- end list -->

  - *Implementación incremental*  
    La capacidad de implementar una alta disponibilidad y resistencia de sitios después de instalar Exchange 2013.

<!-- end list -->

  - *Copia de base de datos de buzones de correo con retardo*  
    Copia pasiva de una base de datos de buzones de correo que presenta un tiempo de retardo de reproducción de registro superior a cero.

<!-- end list -->

  - *Copia de base de datos de buzones de correo*  
    Base de datos de buzones de correo (archivo .edb y registros), ya sea en estado activo o pasivo.

<!-- end list -->

  - *Resistencia de buzón*  
    Nombre de una solución unificada de alta disponibilidad y resistencia de sitios en Exchange 2013.

<!-- end list -->

  - *Disponibilidad administrada*  
    Conjunto de procesos internos que consta de sondeos, monitores y respondedores que incorporan la supervisión y la alta disponibilidad en todos los roles de servidor y protocolos.

<!-- end list -->

  - *\*over* (pronounced "star over")  
    Abreviatura para *cambio* y *conmutación por error*. Un cambio consiste en la activación manual de una o varias copias de bases de datos. Una conmutación por error consiste en la activación automática de una o varias copias de bases de datos después de un error.

<!-- end list -->

  - *Red de seguridad*  
    Antes conocida como contenedor de transporte, se trata de una característica del servicio de transporte que almacena una copia de todos los mensajes durante *X* días. La configuración predeterminada es 2 días.

<!-- end list -->

  - *Redundancia de instantánea*  
    Característica de servidor de transporte que proporciona redundancia de mensajes para todo el tiempo que estos están en tránsito.

<!-- end list -->

  - *Resistencia de sitios*  
    Configuración que amplía la infraestructura de mensajería a varios sitios de Active Directory para proporcionar una continuidad operativa al sistema de mensajería en el caso de que un error afecte a alguno de los sitios.

Terminología básica

## Grupos de disponibilidad de base de datos

Un DAG es el componente esencial del marco de alta disponibilidad y resistencia de sitios que hay integrado en Exchange 2013. Un DAG es un grupo de hasta 16 servidores de buzones de correo que hospeda un conjunto de bases de datos y proporciona recuperación automática en el nivel de la base de datos de los errores que afectan a los servidores, las redes o las bases de datos individuales. Cualquier servidor en un DAG puede hospedar una copia de una base de datos de buzones de correo de cualquier otro servidor en el DAG. Cuando se agrega un servidor a un DAG, funciona con otros servidores en el DAG para proporcionar recuperación automática de errores que afectan a las bases de datos de buzones de correo, como un error de disco o de servidor. Para obtener más información acerca de los DAG, vea [Grupos de disponibilidad de base de datos (DAG)](database-availability-groups-dags-exchange-2013-help.md).

Terminología básica

## Copias de bases de datos de buzones de correo

Las funciones de alta disponibilidad y de resistencia de sitios se presentaron por primera vez en Exchange 2010 y se usan en Exchange 2013 para crear y mantener copias de bases de datos. Exchange 2013 también aprovecha el concepto de movilidad de bases de datos, que es la conmutación por error en el nivel de la base de datos administrada por Exchange.

La movilidad de la base de datos desconecta las bases de datos de los servidores y agrega compatibilidad para un máximo de 16 copias de una sola base de datos. También proporciona una experiencia nativa para crear copias de una base de datos.

El proceso por el cual una copia de base de datos se establece como la base de datos de buzones de correo se denomina *cambio*. En esta misma línea, si se produce un error que afecta a una base de datos o al acceso a la misma y una nueva base de datos pasa a ser la copia activa, se produce lo que se conoce como *conmutación por error*. Este proceso también hace referencia a un error de servidor en el que uno o más servidores conectan las bases de datos que el servidor con el error se encargaba de conectar anteriormente. Cuando se produce un cambio o una conmutación por error, otros servidores de Exchange 2013 perciben dicho cambio casi al instante y redirigen el tráfico de mensajería y cliente a la nueva base de datos activa.

Por ejemplo, si se produce un error en una base de datos activa de un DAG debido a un error de almacenamiento subyacente, Active Manager efectuará una recuperación automática conmutando por error a una copia de base de datos en otro servidor de buzones de correo del DAG. En Exchange 2013, la disponibilidad administrada agrega nuevos comportamientos para recuperarse de la pérdida de acceso de protocolos a una base de datos, incluido el reciclado de los grupos de procesos de trabajo de aplicaciones, el reinicio de servicios y servidores, y el inicio de conmutaciones por error de bases de datos.

Para obtener más información acerca de las copias de bases de datos de buzones de correo, vea [Copias de bases de datos de buzones](mailbox-database-copies-exchange-2013-help.md).

Terminología básica

## Active Manager

Exchange 2013 aprovecha el componente de Active Manager presentado en Exchange 2010 para administrar la replicación continua y el estado de bases de datos, copias de bases de datos y otros aspectos de la alta disponibilidad de servidores de buzones de correo. Para obtener más información acerca de Active Manager, vea [Active Manager](active-manager-exchange-2013-help.md).

Terminología básica

## Resistencia de sitios

Aunque en Exchange 2013 se siguen usando los DAG y los clústeres de conmutación por error de Windows para la resistencia de sitios y la alta disponibilidad del rol de servidor Buzones de correo, la resistencia de sitios no es igual en Exchange 2013. En Exchange 2013 la resistencia de sitios es mucho mejor porque se ha simplificado. Los cambios de arquitectura subyacentes que se efectuaron en Exchange 2013 tienen un impacto considerable en los aspectos de recuperación de una configuración de resistencia de sitios.

En Exchange 2010, la recuperación de buzones (DAG) y de acceso de cliente (matriz del servidor de acceso de cliente) se realizaba de manera conjunta. Si perdía todos los servidores de acceso de cliente, el VIP de la matriz o una parte importante del DAG, se enfrentaba a una situación en la que era necesario realizar un cambio de centro de datos. Este proceso está bien explicado y documentado, aunque conlleva bastante tiempo y requiere la intervención humana para poder iniciarse.

En Exchange 2013, si pierde una matriz de servidor de acceso de cliente por cualquier motivo (por ejemplo, un error en el equilibrador de carga), no es necesario realizar ningún cambio de centro de datos. Con la configuración correcta, la conmutación por error se produce en el nivel del cliente y los clientes se redireccionan automáticamente a un segundo centro de datos que tiene servidores de acceso de cliente operativos. Dichos servidores envían la comunicación mediante proxy de vuelta al servidor de buzones de correo del usuario, al que no le afectará la interrupción (porque no se realiza ningún cambio). En lugar de centrarse en recuperar el servicio, éste se recupera de forma automática y usted podrá dedicarse a solucionar el problema principal (por ejemplo, reemplazar el equilibrador de carga erróneo).

Además, gracias a la simplificación de los espacios de nombres, a la consolidación de los roles de servidor, al desacoplamiento de los requisitos de los roles del servidor del sitio de Active Directory, a la separación de la matriz del servidor de acceso de cliente y la recuperación de DAG y a los cambios en el equilibrio de cargas, Exchange 2013 incorpora algunos cambios que ahora permiten habilitar la recuperación tanto del servidor de acceso de cliente como de DAG para que sea independiente y automática entre los sitios, lo que proporciona escenarios de conmutación por error de centros de datos cuando hay tres ubicaciones.

En Exchange 2010, podría implementar un DAG en dos centros de datos y hospedar el testigo en una tercera base de datos para habilitar la conmutación por error para el rol de servidor Buzón de correo para cualquiera de los centros de datos. Sin embargo, no obtendría la conmutación por error para la solución, porque aún debería cargarse manualmente el espacio de nombres para los roles de los servidores que no sean Buzón de correo.

En Exchange 2013, no es necesario mover el espacio de nombres con el DAG. Exchange aprovecha la tolerancia a errores incorporada en el espacio de nombre mediante el equilibrio de cargas de varias direcciones IP (y, de ser necesario, la capacidad de poner a los servidores fuera de servicio y en funcionamiento). Los clientes HTTP modernos funcionan con esta redundancia de manera automática. La pila HTTP puede aceptar varias direcciones IP para un nombre de dominio completo (FQDN) y, si la primera dirección IP que prueba tiene un error permanente (es decir, no se puede conectar), probará con la próxima dirección IP en la lista. En los errores temporales (la conexión se pierde después de que se establece la sesión, quizás debido a un error intermitente en el servicio en el que, por ejemplo, un dispositivo deja paquetes y debe colocarse fuera de servicio), es posible que el usuario deba actualizar el explorador.

Esto significa que el espacio de nombres ya no es un punto único de error, como sucedía en Exchange 2010. En Exchange 2010, el mayor punto único de error en el sistema de mensajería es posiblemente el FQDN que se proporciona a los usuarios porque les dice dónde ir. En el paradigma de Exchange 2010, cambiar el destino al que el FQDN se dirige no es sencillo porque se debe cambiar el DNS y, luego, controlar la latencia de DNS, lo que, en algunas partes del mundo, representa todo un desafío. También se deben administrar las cachés de nombres en los exploradores, lo que suele tardar aproximadamente 30 minutos.

Uno de los cambios incluidos en Exchange 2013 consiste en habilitar los clientes para que tengan más de un sitio al que dirigirse. Si suponemos que un cliente tiene la capacidad de usar más de un lugar al que dirigirse (casi todos los protocolos de acceso de cliente de Exchange 2013 están basados en HTTP, como Outlook, Outlook en cualquier lugar, EAS, EWS, OWA y EAC, y todos los clientes HTTP admitidos tienen la capacidad de usar varias direcciones IP), la conmutación por error se proporciona en el lado del cliente. Puede configurar DNS para entregar varias direcciones IP a un cliente durante la resolución de nombres. El cliente solicita mail.contoso.com y obtiene, por ejemplo, dos o cuatro direcciones IP. Sin embargo, el cliente usará muchas de las direcciones IP que obtiene de forma confiable. Esto mejora mucho la situación del cliente ya que, si se produce un error en una de las direcciones IP, tiene una o más direcciones IP a las que intentar conectarse. Si el cliente prueba una y genera un error, espera unos 20 segundos y, a continuación, prueba la siguiente de la lista. Por tanto, si pierde el VIP de la matriz de servidor de acceso de cliente, los clientes se recuperan automáticamente en 21 segundos aproximadamente.

Algunas de las ventajas son las siguientes:

  - En Exchange 2010, si perdía el equilibrador de carga en su centro de datos principal y no tenía otro en el sitio, debía hacer un cambio de centro de datos. En Exchange 2013, si pierde el equilibrador de carga en su centro de datos principal, simplemente, debe desconectarlo (o, quizás, desconectar el VIP) y repararlo o remplazarlo. Los clientes que aún no están usando el VIP en el centro de datos secundario realizarán una conmutación por error automática al VIP secundario sin cambiar el espacio de nombre ni realizar cambios en el DNS. Esto no solo significa que ya no deberá realizar un cambio, sino también que no volverá a perder el tiempo que normalmente perdía con la recuperación del cambio de un centro de datos. En Exchange 2010, debía controlar la latencia de DNS (por lo que se recomendaba establecer el Valor del período de vida (TTL) en 5 minutos, y la introducción de la URL de conmutación por recuperación). En Exchange 2013, esto no es necesario, gracias a la rápida conmutación por error (20 segundos) del espacio de nombre entre VIP (centros de datos).

  - Dado que puede realizar la conmutación por error del espacio de nombre entre centros de datos, lo único que se necesita para lograr una conmutación por error del centro de datos es un mecanismo para la conmutación por error del rol del servidor Buzón de correo en centros de datos. Para obtener una conmutación por error automática para el DAG, simplemente cree una solución donde el DAG se divida en partes iguales entre dos centros de datos y, luego, coloque el servidor testigo en una tercera ubicación para que los miembros del DAG puedan arbitrarla en cualquier centro de datos, independientemente del estado de la red entre los centros de datos que contienen los miembros del DAG. Si solo tiene dos centros de datos y no dispone de una tercera la ubicación física, puede colocar el servidor testigo en una máquina virtual de Microsoft Azure. Vea [Usar una máquina virtual de Microsoft Azure como un servidor testigo del DAG](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md) para más información.

  - En este escenario, los esfuerzos del administrador se enfocan simplemente en solucionar el problema y no se desperdician restaurando el servicio. Simplemente, se arregla el error, mientras el servicio continúa funcionando y se mantiene la integridad de los datos. La urgencia y el nivel de estrés que se sienten cuando se arregla un dispositivo dañado no se comparan con la urgencia y el nivel de estrés que se sienten cuando se trabaja para restaurar el servicio. Es mejor para el usuario final y menos estresante para el administrador.

Puede permitir que se produzcan conmutaciones por error sin tener que realizar retrocesos (a veces denominados conmutaciones por recuperación de manera incorrecta). Si pierde los servidores de acceso de cliente en el centro de datos principal y, como consecuencia, se produce una interrupción de 20 segundos para los clientes, no es necesario que se preocupe por las conmutaciones por recuperación. En este caso, su principal preocupación sería solucionar el problema principal (por ejemplo, reemplazar el equilibrador de carga erróneo). Una vez que esté de nuevo en línea y en funcionamiento, algunos clientes empezarán a usarlo y otros pueden permanecer operativos en el segundo centro de datos.

Exchange 2013 también ofrece una funcionalidad que permite a los administradores manejar los errores intermitentes. Un error intermitente es aquel en el que, por ejemplo, se puede establecer la conexión TCP, pero no ocurre nada después. Los errores intermitentes requieren realizar algún tipo de acción administrativa adicional porque pueden derivarse de un dispositivo de reemplazo que se ha puesto en funcionamiento. Mientras se produce el proceso de reparación, el dispositivo puede estar encendido y aceptar algunas solicitudes, pero puede que no esté listo del todo para prestar servicio a los clientes hasta que se realicen los pasos de configuración necesarios. En esta situación, el administrador puede realizar un cambio de espacio de nombres con tan solo quitar el VIP del dispositivo que se va a reemplazar del DNS. De este modo, durante ese período de servicio, ningún cliente intentará conectarse a él. Después de completarse el proceso de reemplazo, el administrador puede volver a agregar el VIP al DNS y los clientes podrán empezar a usarlo.

Para obtener información sobre cómo planear e implementar la resistencia de sitios, vea [Planificación de alta disponibilidad y resistencia de sitios](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) y [Implementación de alta disponibilidad y resistencia de sitios](deploying-high-availability-and-site-resilience-exchange-2013-help.md).

Terminología básica

## API de replicación de terceros

Exchange 2013 también incluye una API de replicación de terceros con la que las organizaciones pueden usar soluciones de replicación sincrónica de terceros en lugar de la característica integrada de replicación continua. Microsoft admite soluciones de otros fabricantes que usen esta API, siempre y cuando la solución aporte las funciones necesarias para reemplazar todas las características de replicación continua que se deshabilitan debido al uso de la API. Las soluciones se admiten únicamente si la API se usa con un DAG para administrar y activar copias de bases de datos de buzones de correo. No se admite el uso de la API fuera de estos límites. Además, la solución debe cumplir los requisitos aplicables de compatibilidad de hardware de Windows. (No se requiere la validación de la prueba para la compatibilidad).

Al implementar una solución que usa la replicación integrada de otros fabricantes, debe comprobarse que el proveedor de dicha solución sea el responsable principal de la compatibilidad de la solución. Microsoft admite datos de Exchange para soluciones replicadas y no replicadas. Las soluciones que usan replicación de datos deben cumplir con la directiva de compatibilidad de Microsoft para replicación de datos, como se detalla en el artículo de Microsoft Knowledge Base 895847, [Compatibilidad de la replicación de datos de varios sitios en Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=895847). Además, las soluciones que usan el modelo de recurso de clúster de conmutación por error de Windows deben cumplir los requisitos de compatibilidad de clúster de Windows especificados en el artículo de Microsoft Knowledge Base 943984, [Directiva de compatibilidad de Microsoft para clústeres de conmutación por error de Windows Server 2008 o Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=943984) o [Directiva de compatibilidad de Microsoft para clústeres de conmutación por error de Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2775067).

La directiva de compatibilidad de restauración y copia de seguridad de Microsoft para implementaciones que usan soluciones basadas en API de replicaciones de terceros es la misma que la aplicada en implementaciones de replicaciones continuas nativas.

Si es un socio y busca información sobre la API de replicación de terceros, póngase en contacto con su representante de Microsoft.

Terminología básica

## Documentación de alta disponibilidad y resistencia de sitios

En la siguiente tabla se incluyen vínculos a los temas que le proporcionarán más información acerca de cómo administrar DAG, sobre las copias de bases de datos de buzones de correo, copias de seguridad y restauración para Exchange 2013.


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
<td><p><a href="database-availability-groups-dags-exchange-2013-help.md">Grupos de disponibilidad de base de datos (DAG)</a></p></td>
<td><p>Obtener más información acerca de DAG, Active Manager, el modo de coordinación de activación de centros de datos (DAC) y las copias de bases de datos de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">Planificación de alta disponibilidad y resistencia de sitios</a></p></td>
<td><p>Obtenga más información acerca de aspectos generales, hardware, redes, software, servidores testigo y otros requisitos y procedimientos recomendados para DAG.</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-high-availability-and-site-resilience-exchange-2013-help.md">Implementación de alta disponibilidad y resistencia de sitios</a></p></td>
<td><p>Consultar un escenario de implementación de ejemplo para implementar y configurar DAG.</p></td>
</tr>
<tr class="even">
<td><p><a href="managing-high-availability-and-site-resilience-exchange-2013-help.md">Administración de alta disponibilidad y resistencia de sitios</a></p></td>
<td><p>Obtener más información acerca de las tareas de administración de DAG, cambios y conmutaciones por error y el modo de mantenimiento.</p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-database-availability-groups-exchange-2013-help.md">Supervisión de grupos de disponibilidad de base de datos</a></p></td>
<td><p>Obtener más información sobre los scripts y cmdlets integrados para supervisar DAG y copias de base de datos.</p></td>
</tr>
<tr class="even">
<td><p><a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">Copia de seguridad, restauración y recuperación ante desastres</a></p></td>
<td><p>Obtener más información acerca de la creación de copias de seguridad y restauración de bases de datos de Exchange, bases de datos de recuperación y la recuperación del servidor.</p></td>
</tr>
</tbody>
</table>


Terminología básica

