---
title: 'Contadores de rendimiento de Exchange 2013: Exchange 2013 Help'
TOCTitle: Contadores de rendimiento de Exchange 2013
ms:assetid: 9143dd77-7c30-4769-8de1-28c717cfa9e9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn904093(v=EXCHG.150)
ms:contentKeyID: 63913012
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contadores de rendimiento de Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2017-02-06_

## Contadores de rendimiento de Exchange 2013

En las siguientes secciones se enumeran los contadores de rendimiento útiles que puede usar al solucionar problemas de rendimiento de Exchange 2013.

## Contadores de conectividad del controlador de dominio de Exchange

En las siguientes tablas se muestran los umbrales aceptables, así como información sobre los contadores de conectividad del controlador de dominio de Exchange.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Contador</th>
<th>Descripción</th>
<th>Umbral</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Controladores del dominio MSExchange ADAccess(*)\Tiempo de lectura LDAP</p></td>
<td><p>Muestra el tiempo expresado en milisegundos (ms) que se tarda en enviar una solicitud de lectura LDAP al controlador de dominio especificado y recibir una respuesta.</p></td>
<td><p>Debe ser inferior a 50 ms como promedio. Los picos (valores máximos) no deben ser superiores a 100 ms.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess Domain Controllers(*)\Tiempo de búsqueda LDAP</p></td>
<td><p>Muestra el tiempo (en ms) que se tarda en enviar una solicitud de búsqueda LDAP y recibir una respuesta.</p></td>
<td><p>Debe ser inferior a 50 ms como promedio. Los picos (valores máximos) no deben ser superiores a 100 ms.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ADAccess Processes(*)\Tiempo de lectura LDAP</p></td>
<td><p>Muestra el tiempo expresado en milisegundos que se tarda en enviar una solicitud de lectura LDAP al controlador de dominio especificado y recibir una respuesta.</p></td>
<td><p>Debe ser inferior a 50 ms como promedio. Los picos (valores máximos) no deben ser superiores a 100 ms.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess Processes(*)\Tiempo de búsqueda LDAP</p></td>
<td><p>Muestra el tiempo (en ms) que se tarda en enviar una solicitud de búsqueda LDAP y recibir una respuesta.</p></td>
<td><p>Debe ser inferior a 50 ms como promedio. Los picos (valores máximos) no deben ser superiores a 100 ms.</p></td>
</tr>
</tbody>
</table>


## Contadores de procesos y procesadores

En las siguientes tablas se muestran los umbrales aceptables y la información sobre los procesadores y contadores de procesos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Contador</th>
<th>Descripción</th>
<th>Umbral</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processor(_Total)\% de tiempo de procesador</p></td>
<td><p>Muestra el porcentaje de tiempo que el procesador emplea en ejecutar procesos de aplicaciones o del sistema operativo, es decir, el porcentaje de tiempo que el procesador no está inactivo.</p></td>
<td><p>Debe ser inferior al 75 % como promedio.</p></td>
</tr>
<tr class="even">
<td><p>Processor(_Total)\% de tiempo de usuario</p></td>
<td><p>Muestra el porcentaje de tiempo de procesador que se emplea en modo usuario. El modo usuario es un modo de procesamiento restringido diseñado para aplicaciones, subsistemas del entorno y subsistemas integrales.</p></td>
<td><p>Debe ser inferior al 75 % como promedio.</p></td>
</tr>
<tr class="odd">
<td><p>Processor(_Total)\% de tiempo con privilegios</p></td>
<td><p>Muestra el porcentaje de tiempo de procesador que se emplea en modo privilegiado. El modo privilegiado es un modo de procesamiento diseñado para los componentes del sistema operativo y los controladores que manipulan el hardware. Permite el acceso directo al hardware y a toda la memoria.</p></td>
<td><p>Debe ser inferior al 75 % como promedio.</p></td>
</tr>
<tr class="even">
<td><p>Longitud de cola del sistema\procesador (todas las instancias)</p></td>
<td><p>Indica el número de subprocesos que cada procesador está atendiendo. La longitud de la cola del procesador se puede utilizar para identificar si la contención del procesador o el uso elevado de CPU se deben a que la capacidad del procesador es insuficiente para atender la carga que se le ha asignado. El contador de longitud de cola del procesador muestra el número de subprocesos que están retrasados en la cola Listo del procesador y que esperan su turno para ejecutarse. El valor que aparece es el último valor observado en el momento en que se tomó la medida.</p></td>
<td><p>No debe ser superior a 5 por procesador.</p></td>
</tr>
<tr class="odd">
<td><p>Process(*)\% de tiempo de procesador</p></td>
<td><p>Se puede usar para identificar procesos específicos que consumen CPU.</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


## Contadores de memoria

En las siguientes tablas se muestran los umbrales aceptables y la información sobre los contadores de memoria.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
<td><p>Umbral</p></td>
</tr>
<tr class="even">
<td><p>Memory\Mbytes disponibles</p></td>
<td><p>Muestra la cantidad de memoria física, en megabytes (MB), disponible de inmediato para la asignación a un proceso o para el uso del sistema. Es igual a la suma de la memoria asignada a las listas de página en espera (en caché), libres y a cero. Para una explicación completa del administrador de memoria, vea Microsoft Developer Network (MSDN) o la &quot;Guía de rendimiento del sistema y resolución de problemas&quot; del kit de recursos de Windows Server 2003.</p></td>
<td><p>Debe ser superior al 5 % de RAM total.</p></td>
</tr>
<tr class="odd">
<td><p>Memory\% de bytes reservados en uso</p></td>
<td><p>Muestra la relación entre Memory\Bytes confirmados y Memory\Límite de confirmación. La memoria asignada es la memoria física en uso para la que se ha reservado espacio en el archivo de paginación por si hiciera falta escribirla en el disco. El límite de confirmación viene determinado por el tamaño del archivo de paginación. Si el archivo de paginación aumenta, el límite de confirmación también aumenta y la proporción disminuye. Este contador muestra solo el valor del porcentaje actual; no es un promedio.</p></td>
<td><p>Si este valor es superior a 80 %, es un indicio de que el sistema está probablemente sobrecargado para proporcionar más memoria.</p></td>
</tr>
</tbody>
</table>


## Contadores de .NETFramework

En las siguientes tablas se muestran los umbrales aceptables y la información sobre los contadores de .NET Framework.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
<td><p>Umbral</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR Memory(*)\% de tiempo del GC</p></td>
<td><p>Muestra cuándo se produce la recolección de elementos no utilizados. Si el contador supera el umbral, esto indica que la CPU está realizando labores de limpieza y que no se está usando de manera eficaz para la carga. Agregar memoria al servidor mejoraría esta situación.</p></td>
<td><p>Debe ser inferior al 10 % como promedio.</p></td>
</tr>
<tr class="odd">
<td><p>.NET CLR Exceptions(*)\Número de excepciones producidas/seg</p></td>
<td><p>Muestra el número de excepciones descartadas por segundo. Entre ellas se incluyen tanto las excepciones de .NET Framework como las excepciones sin administrar que se convierten en excepciones de .NET Framework. Por ejemplo, la excepción de referencia a un puntero nulo en un código sin administrar se volvería a descartar en el código administrado como una excepción System.NullReferenceException de .NET Framework. Este contador incluye excepciones controladas y no controladas.</p></td>
<td><p>Debe ser inferior al 5 % del RPS total de pedidos por segundo (RPS) (Web Server(_Total)\Intentos de conexión/s * 0.05).</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR Memory(*)\Número de bytes en todos los montones</p></td>
<td><p>Muestra la suma de otros cuatro contadores: Tamaño del montón de gen. 0, Tamaño del montón de gen. 1, Tamaño del montón de gen. 2 y Tamaño del montón del objeto grande. Este contador indica la memoria actual asignada en bytes de los montones GC.</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


## Contadores de red

En las siguientes tablas se muestran los umbrales aceptables y la información sobre los contadores de red comunes.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
<td><p>Umbral</p></td>
</tr>
<tr class="even">
<td><p>Network Interface(*)\Paquetes de salida con errores</p></td>
<td><p>Indica el número de paquetes salientes que no se pudieron transmitir debido a errores.</p></td>
<td><p>Debe ser 0 en todo momento.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Errores de conexión</p></td>
<td><p>Muestra el número de conexiones TCP para las que el estado actual es ESTABLISHED o CLOSE-WAIT. El número de conexiones TCP que se puede establecer está restringido por el tamaño del bloque no paginado. Cuando el bloque no paginado está agotado, no se pueden establecer conexiones nuevas.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>TCPv4\Conexiones de reinicialización</p></td>
<td><p>Muestra el número de veces que las conexiones TCP han realizado una transición directa al estado CLOSED desde el estado ESTABLISHED o el estado CLOSE-WAIT.</p></td>
<td><p>Un número de restablecimientos cada vez mayor o una progresión continuada en el número de errores pueden indicar que el ancho de banda es insuficiente.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Conexiones de reinicialización</p></td>
<td><p>Muestra el número de veces que las conexiones TCP han realizado una transición directa al estado CLOSED desde el estado ESTABLISHED o el estado CLOSE-WAIT.</p></td>
<td><p>Un número de restablecimientos cada vez mayor o una progresión continuada en el número de errores pueden indicar que el ancho de banda es insuficiente.</p></td>
</tr>
</tbody>
</table>


## Contadores de Net Logon

En las siguientes tablas se muestran los umbrales aceptables y la información sobre contadores comunes para supervisar problemas de autenticación NTLM y problemas de MaxConcurrentAPI. Para obtener más información, vea el artículo 2688798 de Microsoft Knowledge Base [Cómo ajustar el rendimiento para la autenticación NTLM con la configuración de MaxConcurrentAPI](https://go.microsoft.com/fwlink/p/?linkid=389728).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
<td><p>Umbral</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Expectante de semáforos</p></td>
<td><p>El número del subproceso que está esperando obtener el semáforo.</p></td>
<td><p>Vea el artículo 2688798 de Microsoft Knowledge Base <a href="https://go.microsoft.com/fwlink/p/?linkid=389728">Cómo ajustar el rendimiento para la autenticación NTLM con la configuración de MaxConcurrentAPI</a>.</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Sustentador de semáforos</p></td>
<td><p>El número del subproceso que está deteniendo el semáforo.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Obtenedores de semáforo</p></td>
<td><p>El número total de veces que el semáforo se ha obtenido a lo largo de la duración de la conexión del canal de seguridad o desde el inicio del sistema para _Total.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Tiempos de espera del semáforo</p></td>
<td><p>El número total de veces que un subproceso ha agotado su tiempo de espera mientras esperaba al semáforo a lo largo de la duración de la conexión del canal de seguridad o desde el inicio del sistema para _Total.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Tiempo medio de espera del semáforo</p></td>
<td><p>El tiempo promedio (en segundos) que el semáforo está en espera en la última muestra.</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


## Contadores de base de datos

En la siguiente tabla se muestran los contadores de requisitos de latencia de E/S de registro activo y sus umbrales aceptables. Cuando se exceden estos umbrales, la experiencia del cliente se degrada. Por ejemplo, los usuarios pueden experimentar demoras en la entrega de mensajes y una reducción del rendimiento del sistema.


> [!NOTE]
> La guía de latencia de almacenamiento normal en Exchange 2013 es muy similar a la guía de Exchange 2010. Se pueden encontrar contadores adicionales de la base de datos en <A href="https://go.microsoft.com/fwlink/p/?linkid=525622">Contadores de servidores de buzones de correo</A>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
<td><p>Umbral</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\Latencia promedio de lecturas de base de datos de E/S (adjunta)</p></td>
<td><p>Muestra el promedio de tiempo en milisegundos (ms) por operación de lectura de base de datos.</p></td>
<td><p>Debe ser inferior a 20 ms como promedio.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\Latencia promedio de escrituras de base de datos de E/S (adjunta)</p></td>
<td><p>Muestra el promedio de tiempo en ms por operación de escritura de base de datos.</p></td>
<td><p>Debe ser inferior a 50 ms como promedio.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\Latencia promedia de escrituras en registro de E/S</p></td>
<td><p>Muestra el promedio de tiempo en ms por operación de escritura en registro.</p></td>
<td><p>Debe ser inferior a 10 ms como promedio.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\Latencia promedio de lecturas de base de datos (recuperación) de E/S</p></td>
<td><p>Muestra el promedio de tiempo en ms por operación de lectura de base de datos pasiva.</p></td>
<td><p>Debe ser inferior a 200 ms como promedio.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\Latencia promedio de escrituras de base de datos de E/S (recuperación)</p></td>
<td><p>Muestra el promedio de tiempo en ms por operación de escritura de base de datos pasiva.</p></td>
<td><p>Debe ser inferior a la latencia de lectura para la misma instancia, medida por MSExchange Database ==&gt; Instances(*)\Contador de latencia promedio (recuperación) de lecturas de la base de datos de E/S.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\Lecturas en base de datos de E/S (adjunta)/seg.</p></td>
<td><p>Muestra el número de operaciones de lectura de base de datos por segundo para cada instancia de base de datos adjunta.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\Escrituras en base de datos de E/S (adjunta)/seg.</p></td>
<td><p>Muestra el número de operaciones de escritura de base de datos por segundo para cada instancia de base de datos adjunta.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\Escrituras en registro de E/S/seg.</p></td>
<td><p>Muestra el número de escrituras en registro por segundo para cada base de datos.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Active Manager(_total)\Base de datos montada</p></td>
<td><p>Muestra el número de copias de base de datos activas en el servidor.</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


## ASP.NET

En las siguientes tablas se muestran los umbrales aceptables y la información sobre los contadores de ASP.NET.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
<td><p>Umbral</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Reinicios de la aplicación</p></td>
<td><p>Muestra el número de veces que la aplicación se ha reiniciado durante la vigencia del servidor web.</p></td>
<td><p>Debe ser 0 en todo momento.</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET\Reinicios del proceso de trabajo</p></td>
<td><p>Muestra el número de veces que un proceso de trabajo se ha reiniciado en el equipo.</p></td>
<td><p>Debe ser 0 en todo momento.</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Tiempo de espera de la solicitud</p></td>
<td><p>Muestra el número de milisegundos que la solicitud más reciente lleva esperando en la cola.</p></td>
<td><p>Debe ser 0 en todo momento.</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET Applications(*)\Solicitudes en la cola de la aplicación</p></td>
<td><p>Indica el número de solicitudes que hay en la cola de solicitudes de la aplicación.</p></td>
<td><p>Debe ser 0 en todo momento.</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET Applications(*)\Solicitudes en ejecución</p></td>
<td><p>Muestra el número de solicitudes que se están ejecutando actualmente.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET Applications(*)\Solicitudes por segundo</p></td>
<td><p>Muestra el número de solicitudes ejecutadas por segundo.</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


## Contadores de acceso de cliente de RPC

En las siguientes tablas se muestran los umbrales aceptables y la información sobre los contadores de acceso de cliente RPC.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
<td><p>Umbral</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Promedio de latencia de RPC</p></td>
<td><p>Indica la latencia promedio de los últimos 1.024 paquetes en milisegundos (ms).</p></td>
<td><p>Debe estar debajo de los 250 milisegundos.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Solicitudes de RPC</p></td>
<td><p>Muestra la cantidad de solicitudes de cliente que el servicio de acceso de cliente de RPC está procesando actualmente.</p></td>
<td><p>No debe ser mayor a 40.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Número de usuarios activos</p></td>
<td><p>Muestra la cantidad de usuarios únicos que mostraron alguna actividad durante los últimos dos minutos.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Número de conexiones</p></td>
<td><p>Muestra la cantidad total de conexiones de cliente mantenidas.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Operaciones RPC/seg.</p></td>
<td><p>Muestra la velocidad con la que se realizan las operaciones RPC, por segundo.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Número de usuarios</p></td>
<td><p>Muestra el número de usuarios que están conectados al servicio.</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


## Contadores Proxy HTTP

En las siguientes tablas se muestra información sobre los contadores Proxy HTTP.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Promedio de latencia de MailboxServerLocator</p></td>
<td><p>Muestra la latencia promedio (ms) de llamadas de servicio web MailboxServerLocator.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Promedio de latencia de autenticación</p></td>
<td><p>Muestra el tiempo promedio que se emplean en la autenticación de solicitudes CAS en las últimas 200 muestras.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Latencia promedio de servidor ClientAccess</p></td>
<td><p>Muestra la latencia promedio (ms) de tiempo de procesamiento CAS (no incluye el tiempo empleado en proxy) en las últimas 200 solicitudes.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Frecuencia de errores de proxy de servidor de buzones de correo</p></td>
<td><p>Muestra el porcentaje de errores relacionados con conectividad entre este servidor de acceso de cliente y los servidores MBX en las últimas 200 muestras.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Solicitudes de proxy pendientes</p></td>
<td><p>Muestra el número de solicitudes proxy pendientes simultáneas.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Solicitudes de proxy por segundo</p></td>
<td><p>Muestra el número de solicitudes proxy procesadas por segundo.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Solicitudes por segundo</p></td>
<td><p>Muestra el número de solicitudes procesadas por segundo.</p></td>
</tr>
</tbody>
</table>


## Contadores del almacén de información

En las siguientes tablas se muestran los umbrales aceptables y la información sobre los contadores del almacén de información.


> [!NOTE]
> La guía de latencia de almacenamiento normal en Exchange 2013 es muy similar a la guía de Exchange 2010. Se pueden encontrar contadores adicionales del almacén de información en <A href="https://go.microsoft.com/fwlink/p/?linkid=525622">Contadores de servidores de buzones de correo</A>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
<td><p>Umbral</p></td>
</tr>
<tr class="even">
<td><p>Solicitudes \RPC almacén de MSExchangeIS (*)</p></td>
<td><p>Indica las solicitudes de RPC globales que se ejecutan dentro del proceso de almacenamiento de información.</p></td>
<td><p>Debe ser inferior a 70 en todo momento.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS Client Type(*)\Promedio de latencia de RPC</p></td>
<td><p>Muestra el promedio de latencia de RPC, en ms, de un servidor para un protocolo de cliente determinado en los últimos 1.024 paquetes.</p></td>
<td><p>Debe ser inferior a 50 ms como promedio para cada cliente.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Store(*)\Promedio de latencia de RPC</p></td>
<td><p>El promedio de latencia de RPC (ms) es el promedio de latencia en milisegundos de solicitudes RPC por base de datos. El promedio se calcula sobre todas las RPC desde que se cargó exrpc32.</p></td>
<td><p>Debe ser inferior a 50 ms en todo momento, con picos inferiores a 100 ms.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS Store(*)\Operaciones RPC/seg</p></td>
<td><p>Muestra el número de operaciones RPC por segundo para cada base de datos.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Client Type(*)\Operaciones RPC/seg</p></td>
<td><p>Muestra el número de operaciones RPC por segundo para cada conexión de tipo cliente.</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


## Contadores del servidor de acceso de cliente

En las siguientes tablas se muestra información sobre los contadores de conexión de cliente y los contadores de Internet Information Services (IIS).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Solicitudes/seg</p></td>
<td><p>Muestra el número de solicitudes HTTP por segundo que se reciben desde el cliente a través de ASP .NET. Determina la velocidad actual de solicitudes de Exchange ActiveSync. Se usa solamente para determinar la carga de usuarios actual.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ActiveSync\Comandos de ping pendientes</p></td>
<td><p>Muestra la cantidad de comandos de ping actualmente pendientes en la cola.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Comandos de sincronización/seg</p></td>
<td><p>Muestra el número de comandos de sincronización que se procesan por segundo. Los clientes usan este comando para sincronizar elementos de una carpeta.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Availability Service\Solicitudes de disponibilidad (seg)</p></td>
<td><p>Muestra el número de solicitudes atendidas por segundo. La solicitud solo puede ser para conocer la disponibilidad o para incluir sugerencias. Una solicitud puede contener varios buzones. Determina la frecuencia con la que se producen las solicitudes del Servicio de disponibilidad.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange OWA\Usuarios únicos actuales</p></td>
<td><p>Muestra el número de usuarios únicos conectados actualmente a Outlook Web App. Este valor supervisa el número de sesiones activas de usuarios únicos, de forma que los usuarios solo se quitan del contador después de que hayan cerrado sesión o si superan el tiempo de espera de sus sesiones. Determina la carga de usuarios actual.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange OWA\Solicitudes/seg</p></td>
<td><p>Muestra el número de solicitudes controladas por Outlook Web App por segundo. Determina la carga de usuarios actual.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeAutodiscover\Solicitudes/seg</p></td>
<td><p>Muestra el número de solicitudes del servicio Detección automática procesadas por segundo. Determina la carga de usuarios actual.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeWS\Solicitudes/seg</p></td>
<td><p>Muestra el número de solicitudes procesadas por segundo. Determina la carga de usuarios actual.</p></td>
</tr>
<tr class="even">
<td><p>Web Service(_Total)\Conexiones actuales</p></td>
<td><p>Muestra el número actual de conexiones establecidas con el servicio web. Determina la carga de usuarios actual.</p></td>
</tr>
<tr class="odd">
<td><p>Web Service(Default Web Site)\Conexiones actuales</p></td>
<td><p>Muestra el número actual de conexiones establecidas con el sitio web predeterminado que corresponde con el número de conexiones que llegan al rol del servidor front-end de CAS. Determina la carga de usuarios actual.</p></td>
</tr>
<tr class="even">
<td><p>WebService(_Total)\Intentos de conexión por segundo</p></td>
<td><p>Muestra la frecuencia de intentos de establecer conexiones con el servicio web. Determina la carga de usuarios actual.</p></td>
</tr>
<tr class="odd">
<td><p>Web Service(_Total)\Otros métodos de solicitudes por segundo</p></td>
<td><p>Muestra la velocidad a la que se realizan las solicitudes HTTP que no usan los métodos OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, MOVE, COPY, MKCOL, PROPFIND, PROPPATCH, SEARCH, LOCK o UNLOCK. Determina la carga de usuarios actual.</p></td>
</tr>
</tbody>
</table>


## Contadores de administración de carga de trabajo

En las siguientes tablas se muestra información sobre los contadores de administración de carga de trabajo de Exchange. Es importante supervisar estos contadores porque la administración de carga de trabajo puede ejecutar tareas en segundo plano fuera de horas pico.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descripción</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement Workloads(*)\ActiveTasks</p></td>
<td><p>Muestra el número de tareas activas que se ejecutan actualmente en segundo plano para la administración de carga de trabajo.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange WorkloadManagement Workloads(*)\CompletedTasks</p></td>
<td><p>Muestra el número de tareas de administración de carga de trabajo que se han completado.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement Workloads(*)\QueuedTasks</p></td>
<td><p>Muestra el número de tareas de administración de carga de trabajo que están actualmente en cola en espera de ser procesadas.</p></td>
</tr>
</tbody>
</table>

