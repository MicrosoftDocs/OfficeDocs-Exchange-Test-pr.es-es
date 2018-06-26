---
title: 'Contrapresión: Exchange 2013 Help'
TOCTitle: Contrapresión
ms:assetid: 03003544-e802-4988-9427-5fc4da64dcb8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201658(v=EXCHG.150)
ms:contentKeyID: 52062000
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Contrapresión

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

La contrapresión es una característica de supervisión de recursos del sistema del servicio de transporte de Microsoft Exchange que está presente en los servidores de buzones de correo y en los servidores de transporte perimetral de Microsoft Exchange 2013.

Exchange puede detectar cuándo los recursos vitales, como la memoria y el espacio de disco duro disponibles, están bajo presión; cuando esto ocurre, lleva a cabo una acción para evitar que el servicio deje de estar disponible. La contrapresión impide que los recursos del sistema se sobrecarguen completamente. Así, el servidor de Exchange intenta procesar los mensajes existentes antes de aceptar más mensajes nuevos. Cuando el uso de los recursos del sistema vuelve al nivel habitual, el servidor de Exchange reanuda gradualmente el funcionamiento normal y vuelve a aceptar mensajes nuevos.

En Exchange 2013, cuando el servicio de transporte de un servidor de buzones de correo o de transporte perimetral está bajo presión de recursos, se aceptan las conexiones entrantes, pero los mensajes entrantes transmitidos a través de estas conexiones se aceptan a una velocidad más baja o se rechazan. Cuando un host SMTP intenta conectarse a un servidor de Exchange que está bajo presión de recursos, la conexión se hace correctamente. Sin embargo, cuando el host emita el comando **MAIL FROM** para entregar un mensaje, en función del recurso que esté bajo presión, el servicio de transporte retrasará la confirmación del comando **MAIL FROM** o rechazará la conexión.

**Contenido**

Recursos supervisados

Acciones realizadas por el transporte de Exchange cuando está bajo presión de los recursos

Opciones de configuración de contrapresión en el archivo EdgeTransport.exe.config

Información de registro de la contrapresión

## Recursos supervisados

Los recursos del sistema siguientes se supervisan como parte de la característica presión de reserva:

  - Espacio disponible en el disco duro en el que se almacena la base de datos de colas de mensajes.

  - Espacio disponible en el disco duro en el que se almacenan los registros de transacciones de la base de datos de colas de mensajes.

  - Número de transacciones no utilizadas de base de datos de cola de mensajes en la memoria.

  - Memoria que se utiliza para el proceso EdgeTransport.exe.

  - Memoria que se utiliza para todos los demás procesos.

  - Número de mensajes en la cola de envío.

Por cada recurso de sistema supervisado en un servidor de buzones de correo o de transporte perimetral, se aplican los tres niveles siguientes de uso de recursos:

  - **Normal**   El recurso no se está utilizando en exceso. El servidor acepta conexiones y mensajes nuevos.

  - **Medio**   El recurso se está sobreutilizando ligeramente. Se aplica presión de reserva al servidor con limitaciones. Puede fluir correo de remitentes en el dominio con autorización. Sin embargo, dependiendo del recurso que esté bajo presión, el servidor usa el retraso del tráfico de red (tarpitting) para retrasar la respuesta del servidor o rechaza los comandos **MAIL FROM** entrantes de otros orígenes.

  - **Alto**   El recurso se está utilizando en exceso. Se aplica toda la presión de reserva. Se para todo el flujo de mensajes y el servidor rechaza todos los comandos **MAIL FROM** entrantes nuevos.

En las siguientes secciones explicamos cómo gestiona Exchange la situación cuando un recurso determinado está bajo presión.

## Espacio libre en disco duro para la base de datos de colas de mensajes

De forma predeterminada, la base de datos de cola de mensajes se almacena en % ExchangeInstallPath%TransportRoles\\data\\Queue. Exchange supervisa el uso del espacio en el disco duro para esta ubicación. El nivel alto de uso del espacio en disco duro se calcula con la fórmula siguiente:

100 \* (*hard disk size* - *fixed constant*) / *hard drive size*

El valor de la *fixed constant* es 500 megabytes (MB).

Los resultados de esta fórmula se expresan como porcentaje del espacio total del disco duro que se está usando. Los resultados de la fórmula se redondean siempre al valor entero más próximo. De forma predeterminada, el nivel medio de uso del disco duro es un 2 % inferior al nivel alto. De forma predeterminada, el nivel normal de uso del disco duro es un 4 % inferior al nivel alto.

Volver al principio

## Espacio libre en el disco duro para los registros de transacciones de la base de datos de colas de mensajes

De forma predeterminada, los registros de transacciones de la base de datos de colas de mensajes se almacenan en % ExchangeInstallPath%TransportRoles\\data\\Queue. Exchange supervisa el uso del espacio en el disco duro para esta ubicación. El archivo de configuración de la aplicación %ExchangeInstallPath%Bin\\EdgeTransport.exe.config incluye una clave *DatabaseCheckPointDepthMax* que tiene un valor predeterminado de 384 MB. Esta clave controla el tamaño total permitido de todos los registros de transacciones no confirmadas que existen en el disco duro. Esta clave se usa en la fórmula con la que se calcula el uso del disco duro.


> [!NOTE]
> El valor de la clave <EM>DatabaseCheckPointDepthMax</EM> se aplica a todas las bases de datos del Motor de almacenamiento extensible (ESE) relacionadas con el transporte que hay en el servidor de buzones de correo o de transporte perimetral. Esto incluye la base de datos de cola de mensajes y la base de datos de filtros de IP.



De forma predeterminada, el nivel alto de uso del disco duro se calcula con la fórmula siguiente:

100 \* (*hard drive size* - Mín. (5 GB, 3\**DatabaseCheckPointDepthMax*)) / *hard drive size*

Los resultados de la fórmula se redondean siempre al valor entero más próximo. De forma predeterminada, el nivel medio de uso del disco duro es un 2 % inferior al nivel alto. El nivel normal de utilización del disco duro es un 4 % inferior al nivel alto.

Volver al principio

## Número de transacciones sin confirmar de la base de datos de colas de mensajes en la memoria

En la memoria se conserva una lista de los cambios efectuados en la base de datos de cola de mensajes hasta que los cambios se guardan en un registro de transacciones. Luego, la lista se guarda en la propia base de datos de cola de mensajes. Estas transacciones destacadas de la base de datos de cola de mensajes que se conservan en la memoria se conocen como *rellenos de versión*. El número de cubos de versión podría alcanzar niveles excesivamente altos debido a un enorme e inesperado volumen de mensajes entrantes, ataques de correo no deseado o problemas con la integridad de la base de datos de colas de mensajes o con el rendimiento del disco duro.

Cuando Exchange empieza a recibir mensajes, estos se agrupan en lotes y se preparan como cubos de versión. Si un mensaje entrante contiene datos adjuntos de gran tamaño, puede separarse en varios lotes. Estos lotes que se están procesando se conocen como *batch points*. El número de batch points pendientes puede superar los umbrales definidos, especialmente si hay un gran volumen de mensajes entrantes no esperados con datos adjuntos de gran tamaño.

Cuando los cubos de versión o batch points están bajo presión, el servidor de Exchange iniciará las conexiones entrantes de limitación de peticiones retrasando la confirmación de mensajes entrantes. Exchange reducirá la tasa del flujo de mensajes entrantes retrasando el tráfico de red (tarpitting), lo que genera un retraso en los comandos **MAIL FROM**. Si persiste la condición de presión del recurso, Exchange aumentará gradualmente el retraso del tráfico de red (tarpitting). Cuando el recurso se vuelve a usar con normalidad, Exchange empieza a reducir gradualmente el retraso en la confirmación y facilita el funcionamiento normal. De forma predeterminada, Exchange empezará a retrasar la confirmación de mensajes 10 segundos cuando se encuentre bajo la presión de los recursos. Si los recursos siguen estando bajo presión, el retraso va incrementándose en 5 segundos hasta llegar a los 55 segundos.

Exchange mantiene un historial del cubo de versiones y del uso de los recursos del batch point. Si el uso de los recursos no se reduce hasta un nivel normal para un numero determinado de intervalos de sondeo, conocido como la profundidad del historial, Exchange parará el retraso del tráfico de red (tarpitting) y empezará a rechazar los mensajes entrantes hasta que el uso de los recursos vuelva a la normalidad. De forma predeterminada, las profundidades de historial de los cubos de versión y los batch points se expresan en intervalos de sondeo de 10 y 300, respectivamente.

Volver al principio

## Memoria usada por el proceso EdgeTransport.exe

De forma predeterminada, el nivel alto de utilización de la memoria por parte del proceso EdgeTransport.exe se calcula con la fórmula siguiente:

75 % de la memoria física total o 1 terabyte, lo que sea inferior

Este cálculo no incluye la memoria virtual disponible en el archivo de paginación del disco duro ni la memoria usada por otros procesos. Los resultados de esta fórmula se expresan en un porcentaje de la memoria total que utiliza el proceso EdgeTransport.exe. Los resultados de la fórmula se redondean siempre al valor entero más próximo.

De forma predeterminada, el nivel medio de utilización de la memoria por parte del archivo EdgeTransport.exe se calcula como el 73% de la memoria física total o un 2% menos que el valor del nivel alto, lo que sea inferior. De forma predeterminada, el nivel normal de utilización de la memoria por parte del archivo EdgeTransport.exe se calcula como el 71% de la memoria física total o un 4% menos que el valor del nivel alto, lo que sea inferior.

Si la utilización de la memoria del proceso EdgeTransport.exe es superior al nivel normal especificado, se impondrá una *recogida de basura*. La recogida de basura es un proceso que comprueba si hay objetos sin usar en la memoria y reclama la memoria que éstos utilizan.

Exchange mantiene un historial del uso de memoria del proceso EdgeTransport.exe. Si el uso no se reduce hasta un nivel normal para un numero determinado de intervalos de sondeo, conocido como profundidad del historial, Exchange empezará a rechazar los mensajes entrantes hasta que el uso del recurso vuelva a la normalidad. De forma predeterminada, la profundidad del historial para la utilización de la memoria de EdgeTransport.exe es de 30 intervalos de sondeo.

Volver al principio

## Memoria utilizada por todos los procesos

De forma predeterminada, el nivel alto de utilización de la memoria por parte de todos los procesos equivale al 94% de la memoria física total. Este valor no incluye la memoria virtual disponible en el archivo de paginación del disco duro.

Cuando se alcanza el nivel de utilización de la memoria especificado, se realiza una *deshidratación de mensajes*. La depuración de mensajes consiste en quitar los elementos innecesarios de los mensajes en cola en la memoria caché. Los mensajes completos se guardan en la memoria caché para mejorar el rendimiento. Al eliminar de la memoria el contenido MIME de los mensajes que están en cola, se reduce la memoria utilizada a expensas de aumentar la latencia, porque los mensajes se leen directamente desde la base de datos de colas de mensajes. De forma predeterminada, la depuración de mensajes está habilitada.

Volver al principio

## Número de mensajes en la cola de envío

La cola de envío está asociada al servicio de transporte de los servidores de buzones de correo y de transporte perimetral de Exchange 2013. El categorizador procesa todos los mensajes de la cola de envío. Esta categorización hace que el mensaje se coloque en la cola de entrega. Para obtener más información, vea [Flujo de correo](mail-flow-exchange-2013-help.md) y [Colas](queues-exchange-2013-help.md). Un gran número de mensajes en la cola de entrega indica que el categorizador está teniendo dificultades para procesar los mensajes.

Cuando la cola de entrega esté bajo presión, el servidor de Exchange iniciará las conexiones entrantes de limitación de peticiones retrasando la confirmación de mensajes entrantes. Exchange reducirá el índice del flujo de mensajes entrantes retrasando el tráfico de red (tarpitting), lo que genera un retraso en los comandos **MAIL FROM**. Si persiste la condición de presión de la cola de envío, Exchange aumentará gradualmente el retraso del tráfico de red (tarpitting). Cuando el uso de la cola de envío vuelve a la normalidad, Exchange empieza a reducir gradualmente el retraso en la confirmación y facilita el funcionamiento normal. De forma predeterminada, Exchange empezará a retrasar la confirmación de mensajes 10 segundos cuando la cola de envío se encuentre bajo presión. Si la cola sigue estando bajo presión, el retraso va aumentando en incrementos de 5 segundos hasta llegar a los 55 segundos.

Exchange guarda un historial del uso de la cola de envío. Si el uso de la cola de envío no se reduce hasta un nivel normal para un numero determinado de intervalos de sondeo, conocido como profundidad del historial, Exchange parará el retraso del tráfico de red (tarpitting) y empezará a rechazar los mensajes entrantes hasta que la cola de envío vuelva a la normalidad. De forma predeterminada, la profundidad del historial para la cola de envío es de 300 intervalos de sondeo.

## Acciones realizadas por el transporte de Exchange cuando está bajo presión de los recursos

En la siguiente tabla se muestran las acciones que hace el transporte de Exchange cuando un recurso determinado está bajo presión.

### Acciones de contrapresión adoptadas por los servidores de buzones de correo y de transporte perimetral al responder a la presión de los recursos

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso bajo presión</th>
<th>Nivel de utilización</th>
<th>Acciones realizadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Espacio en el disco duro para base de datos de cola de mensajes</p></td>
<td><p>Medio</p></td>
<td><ul>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Espacio en el disco duro para base de datos de cola de mensajes</p></td>
<td><p>Alto</p></td>
<td><ul>
<li><p>Rechazar mensajes entrantes de otros servidores de Exchange</p></li>
<li><p>Rechazar envíos de mensajes desde las bases de datos de buzones de correo por el servicio de envío de transporte de buzones de los servidores de buzones de correo</p></li>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Espacio en el disco duro para registros de transacciones de base de datos de cola de mensajes</p></td>
<td><p>Medio</p></td>
<td><ul>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Espacio en el disco duro para registros de transacciones de base de datos de cola de mensajes</p></td>
<td><p>Alto</p></td>
<td><ul>
<li><p>Rechazar mensajes entrantes de otros servidores de Exchange</p></li>
<li><p>Rechazar envíos de mensajes desde las bases de datos de buzones de correo por el servicio de envío de transporte de buzones de los servidores de buzones de correo</p></li>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Cubos de versión</p></td>
<td><p>Medio</p></td>
<td><p>Introducir o incrementar el retraso del bloqueo del correo masivo para mensajes entrantes. Si no se alcanza un nivel normal para la profundidad del historial de todo el cubo de versión, realice las siguientes acciones:</p>
<ul>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cubos de versión</p></td>
<td><p>Alto</p></td>
<td><p>Introducir o incrementar el retraso del bloqueo del correo masivo para mensajes entrantes. Si no se alcanza un nivel normal para la profundidad del historial de todo el cubo de versión, realice las siguientes acciones:</p>
<ul>
<li><p>Rechazar mensajes entrantes de otros servidores de Exchange</p></li>
<li><p>Rechazar envíos de mensajes desde las bases de datos de buzones de correo por el servicio de envío de transporte de buzones de los servidores de buzones de correo</p></li>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Batch point</p></td>
<td><p>Medio</p></td>
<td><p>Introducir o incrementar el retraso del bloqueo del correo masivo para mensajes entrantes. Si no se alcanza un nivel normal para la profundidad del historial de todo el batch point, realice las siguientes acciones:</p>
<ul>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Batch point</p></td>
<td><p>Alto</p></td>
<td><p>Introducir o incrementar el retraso del bloqueo del correo masivo para mensajes entrantes. Si no se alcanza un nivel normal para la profundidad del historial de todo el batch point, realice las siguientes acciones:</p>
<ul>
<li><p>Rechazar mensajes entrantes de otros servidores de Exchange</p></li>
<li><p>Rechazar envíos de mensajes desde las bases de datos de buzones de correo por el servicio de envío de transporte de buzones de los servidores de buzones de correo</p></li>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Memoria utilizada por el proceso de EdgeTransport.exe</p></td>
<td><p>Medio</p></td>
<td><ul>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
<li><p>Forzar recolección de elementos no utilizados</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memoria utilizada por el proceso de EdgeTransport.exe</p></td>
<td><p>Alto</p></td>
<td><ul>
<li><p>Rechazar mensajes entrantes de otros servidores de Exchange</p></li>
<li><p>Rechazar envíos de mensajes desde las bases de datos de buzones de correo por el servicio de envío de transporte de buzones de los servidores de buzones de correo</p></li>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Memoria utilizada por todos los procesos</p></td>
<td><p>Medio</p></td>
<td><ul>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
<li><p>Forzar recolección de elementos no utilizados</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memoria utilizada por todos los procesos</p></td>
<td><p>Alto</p></td>
<td><ul>
<li><p>Rechazar mensajes entrantes de otros servidores de Exchange</p></li>
<li><p>Rechazar envíos de mensajes desde las bases de datos de buzones de correo por el servicio de envío de transporte de buzones de los servidores de buzones de correo</p></li>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
<li><p>Vaciar la caché de DNS mejorada de la memoria</p></li>
<li><p>Iniciar la deshidratación de mensajes</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Número de mensajes en la cola de envío</p></td>
<td><p>Medio</p></td>
<td><p>Introducir o incrementar el retraso del bloqueo del correo masivo para mensajes entrantes. Si no se alcanza un nivel normal para la profundidad del historial de toda la cola de envío, haga las siguientes acciones:</p>
<ul>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
<li><p>Forzar recolección de elementos no utilizados</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Número de mensajes en la cola de envío</p></td>
<td><p>Alto</p></td>
<td><p>Introducir o incrementar el retraso del bloqueo del correo masivo para mensajes entrantes. Si no se alcanza un nivel normal para la profundidad del historial de toda la cola de envío, haga las siguientes acciones:</p>
<ul>
<li><p>Rechazar mensajes entrantes de otros servidores de Exchange</p></li>
<li><p>Rechazar envíos de mensajes desde las bases de datos de buzones de correo por el servicio de envío de transporte de buzones de los servidores de buzones de correo</p></li>
<li><p>Rechazar mensajes entrantes de servidores que no sean de Exchange</p></li>
<li><p>Rechazar envíos de mensajes de directorios de recogida y reproducción</p></li>
<li><p>Vaciar la caché de DNS mejorada de la memoria</p></li>
<li><p>Iniciar la deshidratación de mensajes</p></li>
</ul></td>
</tr>
</tbody>
</table>


Volver al principio

## Opciones de configuración de contrapresión en el archivo EdgeTransport.exe.config

Todas las opciones de configuración de contrapresión están disponibles en el archivo de configuración de la aplicación XML %ExchangeInstallPath%Bin\\EdgeTransport.exe.config.


> [!WARNING]
> Estas opciones aparecen sólo a modo de referencia. No se recomienda realizar modificaciones en la configuración de contrapresión del archivo EdgeTransport.exe.config. Las modificaciones de la configuración de contrapresión pueden ocasionar un rendimiento insuficiente o la pérdida de datos. Es recomendable que investigue y corrija la causa raíz de los eventos de contrapresión que puedan surgir.



### Opciones de configuración de contrapresión

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de clave</th>
<th>Valor predeterminado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>EnableResourceMonitoring</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>ResourceMonitoringInterval</em></p></td>
<td><p><code>00:00:02</code> (2 segundos)</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. Este valor indica que se utilizará la fórmula predeterminada.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. Este valor indica que el valor real es un 2% inferior al valor de <em>PercentageDatabaseDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. Este valor indica que el valor real es un 2% inferior al valor de <em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. Este valor indica que se utilizará la fórmula predeterminada.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. Este valor indica que el valor real es un 2% inferior al valor de <em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. Este valor indica que el valor real es un 2% inferior al valor de <em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedHighThreshold</em></p></td>
<td><p>0. Este valor indica que se utilizará el cálculo predeterminado.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePrivateBytesUsedMediumThreshold</em></p></td>
<td><p>0. Este valor indica que el valor real es un 2% inferior al valor de <em>PercentagePrivateBytesUsedHighThreshold</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedNormalThreshold</em></p></td>
<td><p>0. Este valor indica que el valor real es un 2% inferior al valor de <em>PercentagePrivateBytesUsedMediumThreshold</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsHighThreshold</em></p></td>
<td><p>200</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsMediumThreshold</em></p></td>
<td><p>120</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsNormalThreshold</em></p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsHistoryDepth</em></p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointHighThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointMediumThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointNormalThreshold</em></p></td>
<td><p>1000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointUseCostForPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointBatchSize</em></p></td>
<td><p>40</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointBatchTimeout</em></p></td>
<td><p><code>00:00:00.100</code> (0,1 segundos)</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointItemExpiryInterval</em></p></td>
<td><p><code>00:05:00</code> (5 minutos)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPBaseThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:00</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPMaxThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:55</code> (55 segundos)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPStepThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:05</code> (5 segundos)</p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPStartThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:10</code> (10 segundos)</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePhysicalMemoryUsedLimit</em></p></td>
<td><p>94</p></td>
</tr>
<tr class="odd">
<td><p><em>DehydrateMessagesUnderMemoryPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateBytesHistoryDepth</em></p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueHighThreshold</em></p></td>
<td><p>10000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueMediumThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueNormalThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Información de registro de la contrapresión

En la siguiente lista se describen las entradas del registro de eventos que se generan a raíz de eventos específicos de contrapresión en Exchange:

  - **Entrada de registro de eventos para un aumento en cualquier nivel de utilización de un recurso**
    
    Tipo de evento: Error
    
    Origen del evento: MSExchangeTransport
    
    Categoría del evento: Resource Manager
    
    Id. de evento: 15004
    
    Descripción: La presión de recurso ha aumentado de *Previous Utilization Level* a *Current Utilization Level*.

  - **Entrada de registro de eventos para un descenso en cualquier nivel de utilización de un recurso**
    
    Tipo de evento: Información
    
    Origen del evento: MSExchangeTransport
    
    Categoría del evento: Resource Manager
    
    Id. del evento: 15005
    
    Descripción: La presión de recurso ha descendido de *Previous Utilization Level* a *Current Utilization Level*.

  - **Entrada de registro de eventos cuando exista muy poco espacio disponible en disco**
    
    Tipo de evento: Error
    
    Origen del evento: MSExchangeTransport
    
    Categoría del evento: Resource Manager
    
    Id. del evento: 15006
    
    Descripción: El servicio de transporte de Microsoft Exchange rechaza los mensajes porque el espacio disponible en disco está por debajo del umbral configurado. Puede que sea necesaria una acción administrativa para liberar espacio en disco para que el servicio siga ejecutándose.

  - **Entrada de registro de eventos cuando exista muy poca memoria disponible**
    
    Tipo de evento: Error
    
    Origen del evento: MSExchangeTransport
    
    Categoría del evento: Resource Manager
    
    Id. del evento: 15007
    
    Descripción: El servicio de transporte de Microsoft Exchange ha rechazado los envíos de mensajes porque el servicio sigue consumiendo una cantidad de memoria superior al umbral configurado. Puede que sea necesario reiniciar el servicio para proseguir el funcionamiento normal.

Volver al principio

