---
title: 'Planificación alta disponibilidad y resistencia de sitios: Exchange 2013 Help'
TOCTitle: Planificación de alta disponibilidad y resistencia de sitios
ms:assetid: 29bb0358-fc8e-4437-8feb-d2959ed0f102
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638104(v=EXCHG.150)
ms:contentKeyID: 48267927
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Planificación de alta disponibilidad y resistencia de sitios

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Durante la fase de planificación, los arquitectos del sistema, los administradores y otras partes interesadas clave deben identificar los requisitos empresariales y los requisitos arquitectónicos para la implementación; particularmente, los requisitos de alta disponibilidad y resiliencia de sitios.

Existen requisitos generales que deben cumplirse para implementar estas características, así como requisitos de hardware, software y redes.

**Contenido**

General requirements

Hardware requirements

Storage requirements

Software requirements

Network requirements

Witness server requirements

Planning for site resilience

## Requisitos generales

Antes de implementar un grupo de disponibilidad de base de datos (DAG) y crear copias de base de datos de buzones de correo, compruebe que se cumplan las siguientes recomendaciones relativas a todo el sistema:

  - Se debe estar ejecutando el Sistema de nombres de dominio (DNS). En condiciones ideales, el servidor DNS debería admitir actualizaciones dinámicas. Si el servidor DNS no las admite, usted debe crear un registro de host DNS (A) para cada servidor de Exchange. En caso contrario, Exchange no funcionará correctamente.

  - Cada servidor de buzones de correo en un DAG debe ser un servidor miembro en el mismo dominio.

  - No se permite agregar un servidor de buzones de correo Exchange 2013 que también sea un servidor de directorio a un DAG.

  - El nombre que asigna al DAG debe ser un nombre de equipo válido, disponible y único de 15 caracteres o menos.

Volver al principio

## Requisitos de hardware

Generalmente, no hay requisitos de hardware especiales que sean específicos de los DAG o las copias de base de datos de buzones de correo. Los servidores usados deben cumplir con todos los requisitos estipulados en los temas para [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md) y [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

Volver al principio

## Requisitos de almacenamiento

Generalmente, no hay requisitos de almacenamiento especiales que sean específicos de los DAG o las copias de base de datos de buzones de correo. Los DAG no requieren ni usan almacenamiento compartido administrado por clúster. El almacenamiento compartido administrado por clúster es compatible con un DAG únicamente cuando éste está configurado para usar una solución que aproveche la API de replicación de terceros integrada en Exchange 2013.

Volver al principio

## Requisitos de software

Los DAG están disponibles en Exchange 2013 Standard Edition y Exchange 2013 Enterprise Edition. Asimismo, un DAG puede incluir una combinación de servidores que ejecuten Exchange 2013 Standard Edition y Exchange 2013 Enterprise Edition.

Cada miembro del DAG también debe ejecutar el mismo sistema operativo. Exchange 2013 se admite en los sistemas operativos Windows Server 2008 R2, Windows Server 2012 y Windows Server 2012 R2. Todos los miembros de un DAG específico deben ejecutar el mismo sistema operativo. Windows Server 2012 R2 se admite únicamente para miembros del DAG que ejecuten Exchange 2013 Service Pack 1 o posterior.

Además de cumplir con los requisitos previos para la instalación de Exchange 2013, existen requisitos del sistema operativo que deben cumplirse. Los DAG usan la tecnología Windows de clúster de conmutación por error y, como resultado, necesitan la versión Enterprise o la versión Datacenter de Windows Server 2008 R2, o la versión Standar o Datacenter de los sistemas operativos Windows Server 2012 o Windows Server 2012 R2.

Volver al principio

## Requisitos de red

Existen requisitos de red específicos que deben cumplirse para cada DAG y para cada miembro del DAG. Cada DAG cuenta con una única *red MAPI*, que es usada por otro miembro DAG para comunicarse con otros servidores (por ejemplo, otros servidores de directorio o servidores Exchange 2013), y ninguna o más *redes de replicación*, que son redes dedicadas al trasvase de registros y la inicialización.

En versiones anteriores de Exchange, se recomienda al menos dos redes (una red MAPI y una red de replicación) para DAG. En Exchange 2013, se admiten varias redes, pero nuestra recomendación depende de la topología de la red física. Si tiene varias redes físicas entre sus miembros DAG que físicamente están separadas entre sí, usar redes MAPI y de replicación independientes proporciona redundancia adicional. Si tiene varias redes que físicamente están parcialmente separadas pero convergen en una única red física (por ejemplo, un único vínculo WAN), se recomienda usar una única red, preferiblemente Ethernet de 10 gigabits, tanto para el tráfico de MAPI como de replicación. Esto ofrece simplicidad para la red y la ruta de acceso de la red.

Tenga en cuenta lo siguiente al diseñar la infraestructura de red para su DAG:

  - Cada miembro del DAG debe tener, como mínimo, un adaptador de red que pueda comunicarse con los demás miembros del DAG. Si usa una única ruta de red, le recomendamos que use Ethernet de 1 gigabit como mínimo, pero preferiblemente Ethernet de 10 gigabit. Asimismo, al usar un único adaptador de red en cada miembro del DAG, recomendamos que diseñe la solución general teniendo en cuenta el adaptador de red único y la ruta.

  - El uso de dos adaptadores de red en cada miembro del DAG le ofrece una red MAPI y una red de replicación, con redundancia para la red de replicación y los siguientes comportamientos de recuperación:
    
      - En caso de que ocurra un error que afecte la red MAPI, ocurrirá una conmutación por error del servidor (siempre que haya copias de base de datos de buzones de correo en buen estado que puedan activarse).
    
      - En caso de que ocurra un error que afecte la red de replicación, si la red MAPI no se ve afectada por el error, las operaciones de trasvase de registros e inicialización se revertirán para usar la red MAPI, aunque dicha red tenga su propiedad *ReplicationEnabled* establecida en False. Cuando se restaure la salud de la red de replicación y ésta esté lista para reanudar las operaciones de trasvase de registro e inicialización, deberá cambiar manualmente a la red de replicación. Para cambiar la replicación de la red MAPI a una red de replicación restaurada, puede suspender y reanudar la replicación mediante los cmdlets **Suspend-MailboxDatabaseCopy** y **Resume-MailboxDatabaseCopy**, o reiniciar el servicio de replicación de Microsoft Exchange. Recomendamos utilizar las operaciones de suspensión y reanudación para evitar el breve corte producido por el reinicio del servicio de replicación de Microsoft Exchange.

  - Cada miembro del DAG debe tener el mismo número de redes. Por ejemplo, si planea usar un único adaptador de red en cada miembro del DAG, todos los miembros del DAG también deben usar un único adaptador de red.

  - Cada DAG debe tener una red MAPI como máximo. La red MAPI debe proporcionar conectividad a los otros servicios y servidores de Exchange, como Active Directory y DNS.

  - Se pueden agregar redes de replicación, según sea necesario. También puede evitar que un adaptador de red individual sea un punto de error único al usar la formación de equipos del adaptador de red o una tecnología similar. Sin embargo, incluso si se usa la formación de equipos, no se evitará que la red misma sea un único punto de error. Además, la formación de equipos agrega una complejidad innecesaria al DAG.

  - Cada red de cada servidor miembro del DAG debe encontrarse en su propia subred de red. Cada servidor del DAG puede encontrarse en una subred diferente, pero las redes MAPI y las redes de replicación deben ser enrutables y suministrar conectividad, de modo que:
    
      - Cada red de cada servidor miembro del DAG se encuentra en su propia subred de red, que es independiente de la subred usada por cada una de las demás redes del servidor.
    
      - Cada red MAPI del servidor miembro del DAG puede comunicarse con cada una de las demás redes MAPI del miembro del DAG.
    
      - Cada red de replicación del servidor miembro del DAG puede comunicarse con cada una de las demás redes de replicación del miembro del DAG.
    
      - No existe un enrutamiento directo que permita el tráfico de latidos de la red de replicación en un servidor miembro del DAG a la red MAPI en otro servidor miembro del DAG, o viceversa, o entre varias redes de replicación del DAG.

  - Independientemente de su ubicación geográfica en relación con otros miembros del DAG, cada miembro del DAG debe contar con una latencia de red de recorrido de ida y vuelta que no supere los 500 milisegundos entre cada uno de los demás miembros. A medida que la latencia de recorrido de ida y vuelta entre dos servidores de buzones de correo que hospedan copias de una base de datos aumenta, el potencial de replicaciones desactualizadas también aumenta. Independientemente de la latencia de la solución, los clientes deben validar que las redes entre todos los miembros de DAG sean capaces de satisfacer la protección de datos y los objetivos de disponibilidad de la implementación. Las configuraciones con valores de latencia más altos pueden requerir un ajuste especial de los parámetros de DAG, replicación y red, como el aumento del número de bases de datos o la disminución del número de buzones por base de datos, para lograr los objetivos deseados.

  - Es posible que los requisitos de latencia de ida y vuelta no sean los más estrictos en cuanto al ancho de banda de red y a la latencia para una configuración de varios centros de datos. Debe evaluar la carga de red total que incluye acceso de cliente, Active Directory, transporte, replicación continua y otro tráfico de aplicación para determinar los requisitos de red necesarios para su entorno.

  - Las redes de DAG admiten el protocolo de Internet versión 4 (IPv4) e IPv6. La versión IPv6 sólo se admite cuando también se usa IPv4; no se admite un entorno de versión IPv6 exclusivamente. Sólo se admite el uso de direcciones IPv6 e intervalos de direcciones IP si están habilitadas las versiones IPv6 e IPv4 en dicho equipo y la red es compatible con ambas versiones de dirección IP. Si Exchange 2013 está implementado en esta configuración, todas las funciones del servidor podrán enviar datos a dispositivos, servidores y clientes que usen direcciones IPv6, así como recibir datos de ellos.

  - La dirección IP privada automática (APIPA) es una función de Windows que asigna automáticamente direcciones IP cuando no hay ningún servidor de protocolo de configuración dinámica de host (DHCP) disponible en la red. Las direcciones APIPA (incluidas las direcciones asignadas manualmente del intervalo de direcciones APIPA) no pueden ser usadas por los DAG ni por Exchange 2013.

## Requisitos de dirección IP y nombre del DAG

Durante la creación, a cada DAG se le asigna un nombre único y una o más direcciones IP estáticas, o se lo configura para usar DHCP. Independientemente de que se usen direcciones asignadas en forma dinámica o estática, cualquier dirección IP asignada al DAG debe encontrarse en la red MAPI.

Cada DAG que se ejecuta en Windows Server 2008 R2 o Windows Server 2012 requiere como mínimo una dirección IP en la red MAPI. Un DAG requiere direcciones IP adicionales cuando la red MAPI se extiende en varias subredes. Los DAG que se ejecutan en Windows Server 2012 R2 y que se crearon sin un punto de acceso administrativo al clúster no necesitan una dirección IP.

En la siguiente figura, se ilustra un DAG en el que todos los nodos del DAG tienen la red MAPI en la misma subred.

**DAG con red MAPI en la misma subred**

![DAG en una única subred](images/Dd638104.bcb7ef68-6d18-4516-a736-b936991c82cb(EXCHG.150).gif "DAG en una única subred")

En este ejemplo, la red MAPI de cada miembro del DAG se encuentra en la subred 172.19.18.*x*. Como resultado, el DAG requiere una dirección IP única en dicha subred.

En la siguiente figura, se ilustra un DAG que tiene una red MAPI que se extiende en dos subredes: 172.19.18.*x* y 172.19.19.*x*.

**DAG con red MAPI en varias subredes**

![DAG ampliado en varias subredes](images/Dd638104.ffb57c64-3cb1-435c-8148-1b7154d1575c(EXCHG.150).gif "DAG ampliado en varias subredes")

En este ejemplo, la red MAPI de cada miembro del DAG se encuentra en una subred independiente. Como resultado, el DAG requiere dos direcciones IP, una para cada subred de la red MAPI.

Cada vez que la red MAPI del DAG se extiende en una subred adicional, debe configurarse una dirección IP adicional para dicha subred del DAG. Cada dirección IP configurada para el DAG se asigna al clúster de conmutación por error subyacente del DAG, y éste la usa. El nombre del DAG también se usa como el nombre para el clúster de conmutación por error subyacente.

En cualquier momento específico, el clúster para el DAG usará sólo una de las direcciones IP asignadas. Los clústeres de conmutación por error de Windows registran esta dirección IP en DNS cuando la dirección IP del clúster y los recursos de nombre de red se conectan. Además de usar una dirección IP y un nombre de red, se crea un objeto de nombre de clúster (CNO) en Active Directory. El sistema usa internamente el nombre, la dirección IP y el CNO para el clúster a fin de proteger el DAG y permitir la comunicación interna. Los administradores y los usuarios finales no necesitan conectarse a la dirección IP ni el nombre del DAG, ni usarlos como interfaz.


> [!NOTE]
> Si bien el sistema usa internamente el nombre de red y la dirección IP del clúster, no existe una dependencia fuerte de la disponibilidad de dichos recursos en Exchange&nbsp;2013. Incluso si el punto de acceso administrativo del clúster subyacente (es decir, los recursos de nombre de red y dirección IP) está desconectado, aún se produce la comunicación interna dentro del DAG mediante el uso de los nombres de servidores del miembro del DAG. Sin embargo, recomendamos que supervise periódicamente la disponibilidad de estos recursos para garantizar que no estén desconectados por más de 30 días. Si el clúster subyacente está desconectado por más de 30 días, es posible que el mecanismo de recolección de elementos no utilizados invalide la cuenta del CNO del clúster en Active Directory.



## Configuración del adaptador de red para DAG

Cada adaptador de red debe configurarse correctamente según su uso previsto. Un adaptador de red que se utiliza para una red MAPI está configurado de forma diferente desde un adaptador de red que se utiliza para una red de replicación. Además de configurar cada adaptador de red correctamente, debe configurar también el orden de conexión de red en Windows para que la red MAPI está en la parte superior de la orden de conexión. Para ver pasos detallados acerca de cómo modificar el orden de conexión de red, consulte [modificar los enlaces de protocolo y el orden de proveedores de red](https://go.microsoft.com/fwlink/p/?linkid=179138).

## Configuración de adaptador de red MAPI

Un adaptador de red destinado para ser usado por una red MAPI debe configurarse como se describe en la siguiente tabla.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Características de red</th>
<th>Configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cliente para redes Microsoft</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="even">
<td><p>Programador de paquetes QoS</p></td>
<td><p>Opcionalmente habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Uso compartido de impresoras y archivos para redes Microsoft</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="even">
<td><p>Protocolo de Internet versión 6 (TCP/IP v6)</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Protocolo de Internet versión 4 (TCP/IP v4)</p></td>
<td><p>Están habilitados</p></td>
</tr>
<tr class="even">
<td><p>Controlador de E/S del asignador de detección de topologías de nivel de vínculo</p></td>
<td><p>Están habilitados</p></td>
</tr>
<tr class="odd">
<td><p>Respondedor de detección de topologías de nivel de vínculo</p></td>
<td><p>Están habilitados</p></td>
</tr>
</tbody>
</table>


Las propiedades de TCP/IP v4 para un adaptador de red MAPI se configuran de la siguiente forma:

  - La dirección IP de la red MAPI de un miembro de DAG se puede asignar o configurar manualmente para usar DHCP. Si se usa DHCP, recomendamos usar reservas persistentes para la dirección IP del servidor.

  - La red MAPI usa habitualmente una puerta de enlace predeterminada, aunque no se requiere una.

  - Se debe configurar al menos una dirección de servidor DNS. Se recomienda el uso de varios servidores DNS para obtener redundancia.

  - La casilla de verificación **Registrar la dirección de esta conexión en DNS** no debe estar seleccionada.

## Configuración de adaptador de red de replicación

Un adaptador de red destinado para ser usado por una red de replicación debe configurarse como se describe en la siguiente tabla.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Características de red</th>
<th>Configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cliente para redes Microsoft</p></td>
<td><p>Deshabilitado</p></td>
</tr>
<tr class="even">
<td><p>Programador de paquetes QoS</p></td>
<td><p>Opcionalmente habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Uso compartido de impresoras y archivos para redes Microsoft</p></td>
<td><p>Deshabilitado</p></td>
</tr>
<tr class="even">
<td><p>Protocolo de Internet versión 6 (TCP/IP v6)</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Protocolo de Internet versión 4 (TCP/IP v4)</p></td>
<td><p>Están habilitados</p></td>
</tr>
<tr class="even">
<td><p>Controlador de E/S del asignador de detección de topologías de nivel de vínculo</p></td>
<td><p>Están habilitados</p></td>
</tr>
<tr class="odd">
<td><p>Respondedor de detección de topologías de nivel de vínculo</p></td>
<td><p>Están habilitados</p></td>
</tr>
</tbody>
</table>


Las propiedades de TCP/IP v4 para un adaptador de red de replicación se configuran de la siguiente forma:

  - La dirección IP de la red de replicación de un miembro de DAG se puede asignar o configurar manualmente para usar DHCP. Si se usa DHCP, recomendamos usar reservas persistentes para la dirección IP del servidor.

  - Las redes de replicación, por lo general, no poseen puertas de enlace predeterminadas; y si la red MAPI cuenta con una, ninguna otra red deberá tener puertas de enlace predeterminadas. El enrutamiento del tráfico de red en una red de replicación puede configurarse mediante el uso de rutas estáticas y persistentes a la red correspondiente en otros miembros del DAG usando direcciones de puerta de enlace con capacidad de enrutamiento entre las redes de replicación. Cualquier otro tráfico que no coincida con esta ruta estará controlado por la puerta de enlace predeterminada configurada en el adaptador para la red MAPI.

  - No deben configurarse las direcciones del servidor DNS.

  - La casilla **Registrar la dirección de esta conexión en DNS** no debe estar seleccionada.

Volver al principio

## Requisitos de servidor testigo

Un *servidor testigo* es un servidor externo al DAG que se usa para alcanzar y mantener quórum cuando el DAG cuenta con un número par de miembros. Los DAG con un número impar de miembros no usan un servidor testigo. Todos los DAG con número par de miembros deben usar un servidor testigo. El servidor testigo puede ser cualquier equipo que ejecute Windows Server. No es necesario que la versión del sistema operativo Windows Server del servidor testigo coincida con el sistema operativo usado por los miembros del DAG.

Se mantiene el quórum en el clúster, debajo del DAG. Un DAG tiene quórum cuando la mayoría de sus miembros están conectados y pueden comunicarse con los demás miembros conectados del DAG. Esta noción de quórum representa un aspecto del concepto de quórum en los clústeres de conmutación por error de Windows. El *recurso de quórum* es un aspecto relacionado y necesario del quórum en los clústeres de conmutación por error. El recurso de quórum es un recurso interno del clúster de conmutación por error que ofrece un medio para arbitrar las decisiones de pertenencia y de estado del clúster. El recurso de quórum también proporciona almacenamiento persistente para almacenar información de configuración. Un asistente del recurso de quórum es el *registro de quórum*, que es una base de datos de configuración para el clúster. Este registro contiene información, como los servidores que forman parte del clúster, los recursos instalados en el clúster y el estado de dichos recursos (por ejemplo, sin están conectados o no).

Es esencial que cada miembro del DAG tenga una vista uniforme de la forma en que está configurado el clúster subyacente del DAG. El quórum actúa como repositorio definitivo de toda la información de configuración relativa al clúster. El quórum se usa también como mecanismo para resolver empates con el fin de evitar el síndrome de *cerebro dividido*. El síndrome de cerebro dividido es una condición que ocurre cuando los miembros del DAG no pueden comunicarse entre ellos pero están en ejecución. El síndrome de cerebro dividido se evita al requerir la disponibilidad e interacción de una mayoría de los miembros del DAG (y en el caso de los DAG con un número par de miembros, el servidor testigo del DAG) en forma permanente para que el DAG esté en funcionamiento.

Volver al principio

## Planificación de resiliencia de sitios

Cada día, más empresas reconocen que el acceso a un sistema de mensajería confiable y disponible es fundamental para alcanzar el éxito. En muchas organizaciones, el sistema de mensajería forma parte de los planes de continuidad comercial; y la implementación de su servicio de mensajería está diseñada teniendo en cuenta la resistencia de sitios. Fundamentalmente, varias soluciones de resistencia de sitios implican la implementación de hardware en un centro de datos secundario.

En última instancia, el diseño general de un DAG, incluido el número de miembros del DAG y el número de copias de base de datos de buzones de correo, dependerá de los acuerdos de nivel de servicio (SLA) de recuperación de cada organización que cubren varios escenarios de conmutación por error. Durante la etapa de planificación, los administradores y los arquitectos de la solución identifican los requisitos para la implementación, en especial, los requisitos de resistencia de sitios. Identifican las ubicaciones que se usarán y los destinos requeridos de los acuerdos de nivel de servicio de recuperación. El SLA identificará dos elementos específicos que deben ser la base del diseño de una solución que ofrece alta disponibilidad y resistencia de sitios: el objetivo de tiempo de recuperación y el objetivo de punto de recuperación. Ambos valores se miden en minutos. El objetivo de punto de recuperación representa el tiempo que se demora en restaurar el servicio. El objetivo de punto de recuperación hace referencia al estado de actualización de los datos después de que se completa la operación de restauración. También puede definirse un SLA para la restauración del centro de datos principal en el servicio completo una vez que se corrigen sus problemas.

Los administradores y los arquitectos de la solución también identificarán el conjunto de usuarios que requerirán protección de resistencia de sitios, y determinarán si la solución de varios sitios tendrá una configuración activa/pasiva o activa/activa. En una configuración activa/pasiva, generalmente, no hay usuarios hospedados en el centro de datos en espera. En una configuración activa/activa, los usuarios se hospedan en ambas ubicaciones, y cierto porcentaje del número total de bases de datos dentro de la solución posee una ubicación activa preferida en un centro de datos secundario. En caso de ocurrir un error en el servicio para los usuarios de un centro de datos, dichos usuarios se activan en el otro centro de datos.

Construir los SLA correspondientes requiere, a menudo, que se respondan las siguientes preguntas básicas:

  - ¿Qué nivel de servicio es necesario en caso de error del centro de datos principal?

  - ¿Los usuarios necesitan los datos o necesitan únicamente los servicios de mensajería?

  - ¿Con qué rapidez se requieren los datos?

  - ¿A cuántos usuarios hay que admitir?

  - ¿Cómo tendrán acceso los usuarios a sus datos?

  - ¿Qué es la activación del centro de datos en espera, SLA?

  - ¿Cómo se traslada de nuevo el servicio al centro de datos principal?

  - ¿Están dedicados los recursos a la solución de resistencia de sitios?

Al responder estas preguntas, comenzará a dar forma al diseño de resistencia de sitios de su solución de mensajería. Uno de los requisitos fundamentales para la recuperación ante errores de sitios es crear una solución que envíe los datos necesarios a un centro de datos de copias de seguridad que hospede el servicio de mensajería de copias de seguridad.

## Planificación de certificado

No existen consideraciones de diseño especiales ni únicas para los certificados al implementar un DAG en un centro de datos único. Sin embargo, al extender un DAG entre varios centros de datos en una configuración de resistencia de sitios, existen ciertas consideraciones específicas en relación con los certificados. Generalmente, el diseño de su certificado dependerá de los clientes en uso, así como de los requisitos del certificado por parte de otras aplicaciones que usan certificados. Sin embargo, hay algunas recomendaciones específicas y procedimientos recomendados que debe seguir en relación con el tipo y el número de certificados.

Como práctica recomendada, debería minimizar el número de certificados que usa para los servidores Exchange y los servidores proxy inversos. Se recomienda usar un único certificado para todos esos extremos del servicio en cada centro de datos. Este enfoque minimiza la cantidad de certificados necesarios, lo que reduce los costes y la complejidad de la solución.

Para los clientes de Outlook Anywhere, recomendamos que use un certificado con nombre alternativo del sujeto (SAN) único para cada centro de datos e incluya varios nombres de host en el certificado. Para garantizar la conectividad de Outlook Anywhere después de un cambio de base de datos, servidor o centro de datos, debe usar el mismo nombre principal del certificado en cada certificado y configurar el objeto de configuración de proveedor de Outlook en Active Directory con el mismo nombre principal, en el formato estándar de Microsoft (msstd). Por ejemplo, si usa el nombre principal del certificado correo.contoso.com, deberá configurar los atributos de la siguiente forma.

    Set-OutlookProvider EXPR -CertPrincipalName "msstd:mail.contoso.com"

Varias aplicaciones que se integran con Exchange cuentan con requisitos de certificados específicos que pueden exigir el uso de certificados adicionales. Exchange 2013 puede coexistir con Office Communications Server (OCS). OCS requiere certificados con 1024 bits o superiores que usen el nombre del servidor OCS para el nombre principal del certificado. Debido a que el uso de un nombre del servidor OCS para el nombre principal del certificado impedirá el funcionamiento correcto de Outlook en cualquier lugar, deberá usar un certificado adicional e independiente para el entorno del OCS.

## Planificación de red

Además de los requisitos de red específicos que deben cumplirse para cada DAG, así como para cada servidor miembro del DAG, existen recomendaciones y requisitos específicos para la configuración de resistencia de sitios. Al igual que con todos los DAG, ya sea que los miembros del DAG estén implementados en un sitio único o en varios sitios, la latencia de red de regreso de recorrido de ida y vuelta entre los miembros del DAG no debe ser superior a 500 milisegundos. Además, existen valores de configuración específicos recomendados para los DAG que se extienden a varios sitios:

  - **Las redes MAPI deben aislarse de las redes de replicación**. Las directivas de red de Windows, las directivas de firewall de Windows o las listas de control de acceso (ACL) del enrutador deben usarse para bloquear el tráfico entre la red MAPI y las redes de replicación. Esta configuración es necesaria para evitar la interferencia de latidos de la red.

  - **Los registros DNS orientados al cliente deben tener un valor de período de vida (TTL) de 5 minutos**. La cantidad de tiempo de inactividad que experimentan los clientes depende no sólo de la rapidez con la que puede ocurrir un cambio, sino también de la rapidez con la que ocurre la replicación de DNS y la rapidez con la que los clientes consultan la información DNS actualizada. Los registros DNS de todos los servicios de cliente de Exchange, incluidos Microsoft Office Outlook Web App, Microsoft Exchange ActiveSync, servicios Web Exchange, Outlook Anywhere, SMTP, POP3, e IMAP4 en los servidores DNS internos y externos, deben configurarse con un TTL de 5 minutos.

  - **Uso de rutas estáticas para configurar la conectividad entre las redes de replicación**. Para proporcionar conectividad de red entre cada uno de los adaptadores de la red de replicación, use rutas estáticas persistentes. Ésta es una configuración única y rápida que se realiza en cada miembro del DAG al usar direcciones IP estáticas. Si usa DHCP a fin de obtener direcciones IP para sus redes de replicación, también puede usarlo para asignar rutas estáticas para la replicación; de esta manera, se simplifica el proceso de configuración.

## Planificación general de resiliencia de sitios

Además de los requisitos mencionados anteriormente para alta disponibilidad, existen otras recomendaciones para la implementación de Exchange 2013 en una configuración de resistencia de sitios (por ejemplo, extender un DAG a varios centros de datos). Lo que realice durante la fase de planificación tendrá un impacto directo en el éxito de su solución de resistencia de sitios. Por ejemplo, un diseño de espacio de nombres deficiente puede causar dificultades con los certificados, y una configuración de certificados incorrecta puede impedir que los usuarios obtengan acceso a los servicios.

Para minimizar el tiempo que demora la activación de un centro de datos secundario y permitir que éste aloje los extremos del servicio de un centro de datos que falló, debe realizarse la planificación adecuada. A continuación puede ver algunos ejemplos:

  - Los objetivos del SLA para la solución de resistencia de sitios debe comprenderse y documentarse correctamente.

  - Los servidores en el centro de datos secundario deben tener la capacidad suficiente para alojar la población de usuarios combinada de ambos centros de datos.

  - El centro de datos secundario debe tener habilitados todos los servicios suministrados en el centro de datos principal (excepto que el servicio no esté incluido como parte del SLA de resistencia de sitios). Esto incluye Active Directory, infraestructura de red (por ejemplo, DNS o TCP/IP), servicios de telefonía (si está en uso la mensajería unificada) e infraestructura del sitio (como energía o refrigeración).

  - Para que ciertos servicios puedan brindarse a los usuarios desde el centro de datos donde se produjo un error, deben tener configurados los certificados del servidor correctos. Ciertos servicios no permiten la instanciación (por ejemplo, POP3 e IMAP4) y sólo permiten el uso de un certificado único. En dichos casos, el certificado debe ser un certificado de SAN que incluya varios nombres, o los diferentes nombres deben ser lo suficientemente similares para que pueda usarse un certificado comodín (suponiendo que las directivas de seguridad de la organización permiten el uso de certificados comodín).

  - Deben definirse los servicios necesarios en el centro de datos secundario. Por ejemplo, si el primer centro de datos tiene tres direcciones URL de SMTP distintas en diferentes servidores de transporte, debe definirse la configuración apropiada en el centro de datos secundario para habilitar al menos un servidor de transporte (si no se habilitan los tres) para alojar la carga de trabajo.

  - Debe haberse realizado la configuración de red necesaria para admitir el cambio de centro de datos. Esto podría significar que debe asegurarse de que la configuración del equilibrio de carga se haya realizado, el DNS global esté configurado y la conexión a Internet esté habilitada con la configuración de enrutamiento apropiada.

  - Debe comprenderse la estrategia para permitir los cambios de DNS necesarios a fin de realizar un cambio de centro de datos. Los cambios de DNS específicos, incluida la configuración de TTL, deben definirse y documentarse para admitir los SLA vigentes.

  - También debe establecerse e incluirse en el SLA una estrategia para probar la solución. La validación periódica de la implementación es la única forma de garantizar que la calidad y la viabilidad de la implementación no se perderán con el tiempo. Recomendamos que, una vez validada la implementación, se documente explícitamente la parte de la configuración que afecte de manera directa el éxito de la solución. Asimismo, recomendamos que mejore los procesos de administración de cambios en relación con dichos segmentos de la implementación.

Volver al principio

