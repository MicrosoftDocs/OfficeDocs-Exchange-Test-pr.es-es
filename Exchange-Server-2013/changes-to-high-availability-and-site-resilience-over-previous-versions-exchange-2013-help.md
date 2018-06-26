---
title: 'Cambios en la alta disponibilidad y resistencia de sitios respecto a versiones anteriores: Exchange 2013 Help'
TOCTitle: Cambios en la alta disponibilidad y resistencia de sitios respecto a versiones anteriores
ms:assetid: de53c00b-091c-4a31-aacc-1bd40c756ce2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn789066(v=EXCHG.150)
ms:contentKeyID: 62519857
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambios en la alta disponibilidad y resistencia de sitios respecto a versiones anteriores

 

_**Se aplica a:**Exchange Server 2013 SP1_

_**Última modificación del tema:**2015-04-07_

Exchange 2013 usa DAG y copias de bases de datos de buzones de correo, junto con otras funciones, tales como recuperación de un solo elemento, directivas de retención y copias de bases de datos retrasadas para suministrar protección de datos nativa de Exchange, alta disponibilidad y resistencia de sitios. La plataforma de alta disponibilidad, el Almacén de información de Exchange y el Motor de almacenamiento extensible (ESE) se han mejorado para suministrar una mayor disponibilidad, facilitar la administración y reducir los costos. Entre estas mejoras se incluyen:

  - **Reducción de IOPS mediante Exchange 2010**   Esto permite aprovechar discos más grandes en términos de capacidad y de E/S de disco máxima por segundo (IOPS) de la forma más eficiente posible.

  - **Disponibilidad administrada** Con la disponibilidad administrada, las funciones orientadas a la recuperación y supervisión interna se integran estrechamente para evitar errores, restaurar de manera proactiva los servicios, iniciar conmutaciones por error de servidores de forma automática o alertar a los administradores para que tomen medidas. El enfoque se centra en la supervisión y administración de la experiencia del usuario final y no solo en el tiempo activo de componente y servidor para ayudar a mantener el servicio disponible en forma continua.

  - **Almacén administrado**   Almacén administrado es el nombre de los procesos de Almacén de información, recientemente rescritos en Exchange 2013. El nuevo almacén administrado se escribe en C\# y se integra estrechamente con el servicio de replicación de Microsoft Exchange (MSExchangeRepl.exe) para suministrar mayor disponibilidad mediante una resistencia mejorada.

  - **Soporte para varias bases de datos por disco** Exchange 2013 incluye mejoras que le permiten brindar soporte a varias bases de datos (combinaciones de copias activas y pasivas) en el mismo disco y así aprovechar discos más grandes en términos de capacidad de la manera más eficiente posible.

  - **AutoReseed** La funcionalidad de reinicialización automática permite restaurar rápidamente la redundancia de base de datos después de un error en el disco. Si se produce un error en el disco, la copia de bases de datos almacenada en ese disco se copia desde la copia de base de datos activa a un disco de reserva en el mismo servidor. Si se almacenan varias copias de bases de datos en el disco con error, pueden volver a inicializarse todas automáticamente en un disco de reserva. Esto posibilita inicializaciones más rápidas dado que es probable que las bases de datos activas se encuentren en varios servidores y los datos se copien en paralelo.

  - **Recuperación automática de errores de almacenamiento**   Esta funcionalidad continúa la innovación introducida en Exchange 2010 para permitir que el sistema se recupere de errores que afectan la resistencia o la redundancia. Además de los comportamientos de comprobación de errores de Exchange 2010, Exchange 2013 incluye comportamientos de recuperación adicionales para tiempos de E/S largos, consumos excesivos de memoria por parte de MSExchangeRepl.exe y casos graves en los que el sistema se encuentra en un estado tan incorrecto que los subprocesos no pueden programarse.

  - **Mejoras en copias retrasadas**   Las copias retrasadas ahora pueden ocuparse en cierta medida de sí mismas con la reproducción automática de registros. Las copias retrasadas reproducirán automáticamente los archivos de registro en una variedad de situaciones, como la aplicación de revisiones o cuando queda poco espacio en el disco. Si el sistema detecta que la aplicación de revisiones es necesaria para una copia retrasada, los registros se volverán a reproducir automáticamente en la copia retrasada al aplicar las revisiones de página. Las copias retrasadas también invocarán esta característica de reproducción automática cuando se alcance un umbral de espacio de disco bajo, y cuando la copia retrasada se haya detectado como la única copia disponible durante un período de tiempo específico. Además, las copias retrasadas pueden aprovechar la Red de seguridad, lo que hace que la recuperación o la activación sean más fáciles.

  - **Mejoras en la alerta de copia única**   La alerta de copia única introducida en Exchange 2010 ya no es un script programado por separado. Ahora está integrada en los componentes de disponibilidad administrada en el sistema y es una función nativa de Exchange.

  - **Configuración automática de red de DAG**   El sistema puede configurar automáticamente las redes de DAG basándose en las opciones de configuración. Además de las opciones de configuración manual, las redes DAG también pueden distinguir entre MAPI y redes de replicación y configurar redes de DAG automáticamente.

## Reducción de IOPS en Exchange 2010

En Exchange 2010, las copias de bases de datos pasivas tienen una profundidad de punto de comprobación muy baja, lo cual es necesario para efectuar una conmutación por error rápida. Además, la copia pasiva realiza una lectura previa agresiva de los datos para mantener una profundidad de punto de comprobación de 5 megabytes (MB). Como resultado del uso de una profundidad de punto de comprobación baja, y de realizar estas operaciones agresivas de lectura previa, el valor de IOPS para una copia de base de datos pasiva es igual al de una copia activa en Exchange 2010.

En Exchange 2013, el sistema es capaz de proporcionar una conmutación por error rápida con una profundidad de punto de comprobación alta en la copia pasiva (100 MB). Como las copias pasivas tienen una profundidad de punto de comprobación de 100 MB, se han desajustado para que no sean tan agresivas. Debido al aumento de la profundidad de punto de comprobación y al desajuste de las lecturas previas agresivas, el porcentaje de IOPS para una copia pasiva es de un 50 % del IOPS de copias activas en Exchange 2013.

La presencia de una profundidad de punto de comprobación más alta en la copia pasiva también origina otros cambios. En la conmutación por error en Exchange 2010, la caché de la base de datos se descarga porque la base de datos se convierte de una copia pasiva a una activa. En Exchange 2013, se reescribió el registro de ESE para que la caché persista durante la transición de copia pasiva a activa. Dado que ESE no necesita descargar la cache, la conmutación por error se realiza más deprisa.

Otro de los cambios se realizó en el proceso de mantenimiento de bases de datos en segundo plano (BDM). BDM ahora procesa entre 1 y 2 MB por segundo y por copia.

Como consecuencia de todos estos cambios, Exchange 2013 ofrece una disminución importante de IOPS respecto a Exchange 2010.

## Disponibilidad administrada

La disponibilidad administrada consta de la integración de una supervisión activa e integrada y de la plataforma de alta disponibilidad de Exchange 2013. Gracias a la disponibilidad administrada, el sistema puede tomar una decisión sobre cuándo conmutar por error una base de datos en función del estado del servicio. La disponibilidad administrada es una infraestructura interna que se implementa en los roles de servidor Buzón de correo y Acceso de cliente en Exchange 2013. Esta función incluye tres componentes principales asíncronos que funcionan de manera permanente. El primer componente es el motor de sondeo, responsable de tomar medidas en el servidor y recopilar los datos. Los resultados de estas medidas se reflejan en el segundo componente, el monitor. El monitor contiene la lógica empresarial que usa el sistema en función de lo que se considere como un estado correcto en los datos recopilados. De manera similar a un motor de reconocimiento de patrones, el monitor busca los diferentes patrones en todas las medidas recopiladas y, luego, decide si algo es correcto o no. Por último, existe el motor de respuesta, que es responsable de las acciones de recuperación. Cuando hay algo incorrecto, la primera acción es intentar recuperar dicho componente. Esto puede incluir acciones de recuperación de varias etapas; por ejemplo, el primer intento puede ser reiniciar el grupo de aplicaciones; el segundo, reiniciar el servicio; el tercero, reiniciar el servidor y, el próximo, desconectar el servidor de modo que ya no acepte tráfico. Si las acciones de recuperación fracasan, el sistema escala el problema a la persona a través de las notificaciones de registro de eventos.

La disponibilidad administrada se implementa mediante dos servicios:

  - **Exchange Health Manager Service (MSExchangeHMHost.exe)**   Es un proceso de controlador que se usa para gestionar procesos de trabajo. Se usa para crear, ejecutar e iniciar y detener procesos de trabajo, según sea necesario. También se usa para recuperar procesos de trabajo en caso de que se bloqueen, para evitar que los procesos de trabajo sean un punto único de error.

  - **Proceso de Exchange Health Manager Worker (MSExchangeHMWorker.exe)**   Es el proceso de trabajo responsable de realizar las tareas de tiempo de ejecución.

La disponibilidad administrada usa el almacenamiento persistente para realizar sus funciones:

  - Los archivos de configuración XML se utilizan para inicializar las definiciones de elementos de trabajo durante el inicio de los procesos de trabajo.

  - El registro se usa para almacenar datos de tiempo de ejecución, como los marcadores.

  - La infraestructura de registro de eventos del canal Crimson se usa para almacenar los resultados de los elementos de trabajo.

Para obtener más información acerca de la disponibilidad administrada, vea [Disponibilidad administrada](managed-availability-exchange-2013-help.md).

## Almacén administrado

Todas las versiones previas de Exchange Server, desde Exchange Server 4.0 hasta Exchange Server 2010, han admitido la ejecución de una sola instancia del proceso de almacén de información (Store.exe) en el rol de servidor Buzón de correo. Esta única instancia del almacén hospeda todas las bases de datos en el servidor: activas, pasivas, retrasadas y de recuperación. En las arquitecturas anteriores de Exchange, hay poco aislamiento, si lo hay, entre las distintas bases de datos hospedadas en un servidor de buzones de correo. El problema que existe con una base de datos de un solo buzón es que puede afectar potencialmente de forma negativa a todas las demás bases de datos. Las interrupciones que surgen a raíz del daño del buzón pueden afectar el servicio para todos los usuarios cuyas bases de datos están hospedadas en dicho servidor.

Otro desafío que presenta una única instancia de almacén en las versiones anteriores de Exchange es que el Motor de almacenamiento extensible (ESE) escala bien a 8-12 núcleos del procesador, pero si se supera esta cantidad, los problemas de sincronización en la memoria caché y la comunicación entre los procesadores generan una escala negativa. En la actualidad se usan servidores mucho más grandes por lo que hay disponibles sistemas con más de 16 núcleos. Esto supondría el desafío administrativo de administrar la afinidad de 8-12 núcleos para ESE y usar los demás núcleos para procesos no relacionados con el almacén (por ejemplo, Asistentes, Search Foundation, Disponibilidad administrada, etc.). Además, la arquitectura anterior restringía el escalado para el proceso de almacén.

El proceso Store.exe ha evolucionado considerablemente con el transcurso de los años al igual que Exchange Server, pero como único proceso, su escalabilidad está limitada y representa un único punto de error. Debido a estos límites, Store.exe ya no está disponible en Exchange 2013 y se lo reemplazó por el almacén administrado.

Para más información, vea [Almacén administrado](managed-store-exchange-2013-help.md).

## Varias bases de datos por volumen

Si bien las mejoras en el almacenamiento de Exchange 2013 están diseñadas principalmente para las configuraciones de solo un montón de discos (JBOD), todas las configuraciones de almacenamiento compatibles pueden usarlas. Una de estas características es la capacidad para hospedar varias bases de datos en el mismo volumen. Esta característica está relacionada con la optimización de Exchange para discos de gran tamaño. Las optimizaciones permiten usar los discos de gran tamaño de manera mucho más eficiente en términos de capacidad, IOPS y tiempos de reinicialización, y tienen como objetivo afrontar los desafíos asociados a la ejecución en una configuración de almacenamiento JBOD:

  - Los tamaños de las bases de datos deben ser manejables.

  - Las operaciones de reinicialización deben ser rápidas y confiables.

  - Si bien la capacidad de almacenamiento está aumentando, IOPS no.

  - Los discos que hospedan copias de base de datos pasivas se desaprovechan en términos de IOPS.

  - Las copias retrasadas tienen requisitos de almacenamiento asimétricos.

  - La agilidad limitada existe para recuperarse de las condiciones de espacio en disco insuficiente.

La tendencia de aumentar la capacidad de almacenamiento continúa y se espera que pronto estén disponibles unidades de 8 terabytes. Al usar unidades de 8 terabytes junto a procedimientos recomendados en cuanto al tamaño máximo de bases de datos de Exchange (2 terabytes), se consumirían más de 5 terabytes de espacio en disco. Una solución sería, simplemente, aumentar el tamaño de las bases de datos, pero esto inhibe la administración, ya que agrega mayores tiempos de reinicialización, incluidos, en algunos casos, tiempos de reinicialización no administrables, y pone en riesgo la confiabilidad de la copia de la cantidad de datos en la red.

Además, en el modelo de Exchange 2010, el disco que almacena una copia pasiva queda desaprovechado en términos de IOPS. En el caso de las copias pasivas retrasadas, además de que el disco no se aprovecha del todo en cuanto a IOPS, también es asimétrico en lo que a su tamaño se refiere, en comparación con los discos que se usan para almacenar las copias activas y pasivas no retrasadas.

Siguiendo la práctica que se ha mantenido durante mucho tiempo, Exchange 2013 se ha optimizado para que pueda usar discos grandes (8 terabytes) en una configuración JBOD de manera más eficiente. En Exchange 2013 se incluyen varias bases de datos por disco, lo que permite tener discos del mismo tamaño que almacenen varias copias de bases de datos, incluidas copias retrasadas. El objetivo consiste en distribuir a los usuarios entre el número de volúmenes existente, lo que proporciona un diseño simétrico en el que, durante un funcionamiento normal, los miembros de DAG hospedan una combinación de copias activas, pasivas y retrasadas opcionales en los mismos volúmenes.

A continuación se muestra un ejemplo de una configuración que emplea varias bases de datos por volumen.

**Configuración que usa varias bases de datos por volumen**

![Varias bases de datos por volumen](images/Dn789066.c5e7d6c8-3e77-4f72-a873-5e9aaded9aa3(EXCHG.150).gif "Varias bases de datos por volumen")

En la configuración anterior, se proporciona un diseño simétrico. Los cuatro servidores tienen las cuatro bases de datos hospedadas en un solo disco por servidor. La clave es que el número de copias de cada base de datos debe ser igual al número de copias de base de datos por disco. En el ejemplo anterior, hay cuatro copias de cada base de datos: una copia activa, dos copias pasivas y una copia retrasada. Como hay cuatro copias para cada base de datos, la configuración adecuada es la que tenga cuatro copias por volumen. Además, se configura la preferencia de activación para que se equilibre en el DAG y en los servidores. Por ejemplo, la copia activa tendrá un valor de preferencia de activación de 1, la primera copia pasiva tendrá un valor de preferencia de activación 2, la segunda copia pasiva, de 3 y la copia retrasada, de 4.

Además de conseguir una mejor distribución de los usuarios en los volúmenes existentes, otra ventaja del uso de varias bases de datos por disco consiste en que disminuye el tiempo que se tarda en restaurar la protección de datos en caso de que genere un error que precise una reinicialización (por ejemplo, un error de disco).

A medida que las bases de datos crecen, su reinicialización tarda cada vez más. Por ejemplo, una base de datos de 2 terabytes puede tardar 23 horas en reinicializarse, mientras que una de 8 terabytes puede tardar hasta 93 horas (casi 4 días). Ambas inicializaciones ocurrirían en unos 20 MB por segundo. Generalmente, esto significa que una base de datos muy grande no podría inicializarse dentro de un tiempo operativamente razonable.

En el caso de un escenario con una sola copia de base de datos por disco, la operación de inicialización se enlaza al origen, porque el disco siempre se inicializa desde un solo origen. Al dividir el volumen en varias copias de base de datos y tener la copia activa de las bases de datos pasivas en un volumen especificado almacenado en miembros de DAG independientes, el sistema deja de estar enlazado al origen en el contexto de la reinicialización del disco. Cuando se reemplaza un disco erróneo, se puede reinicializar desde varios orígenes. Esto permite al sistema reinicializar y restaurar la protección de datos para estas bases de datos en un espacio de tiempo mucho más breve.

Al usar varias bases de datos por volumen, se recomienda seguir las siguientes mejores prácticas y los siguientes requisitos:

  - Debe usarse una partición de disco lógico único por disco físico. No cree varias particiones en el disco. Las copias de base de datos y sus archivos complementarios (como los registros de transacción y el índice de contenido) se deben hospedar en un único directorio en la partición única.

  - El número de copias de base de datos configuradas por volumen debe ser igual al número de copias de cada base de datos. Por ejemplo, si tiene cuatro copias de bases de datos, debe usar cuatro copias de base de datos por volumen.

  - Las copias de la base de datos deben tener los mismos vecinos. (Por ejemplo, todos deben compartir el mismo disco en cada servidor).

  - La preferencia de activación en el DAG debe estar equilibrada, de modo que cada copia de base de datos en un disco determinado tenga un valor de preferencia de activación único.

## AutoReseed

La reinicialización automática, o AutoReseed, es una característica que sustituye a las acciones que generalmente suele realizar un administrador como respuesta a un error en el disco, un evento de base de datos dañada u otro problema que precise reinicializar una copia de base de datos. AutoReseed se ha diseñado con el fin de restaurar automáticamente la redundancia de bases de datos después de un error en el disco mediante el uso de discos de reserva que se aprovisionan al sistema.

Para obtener más información, vea [AutoReseed](autoreseed-exchange-2013-help.md). Para obtener información detallada acerca de AutoReseed, vea [Configurar un grupo de disponibilidad de la base de datos AutoReseed](configure-autoreseed-for-a-database-availability-group-exchange-2013-help.md).

## Recuperación automática de errores de almacenamiento

La recuperación automática de errores de almacenamiento continúa con las novedades presentadas en Exchange 2010 para permitir que el sistema se recupere de los errores que afectan a la resistencia o a la redundancia. Además de los comportamientos de comprobación de errores de Exchange 2010, Exchange 2013 incluye otros comportamientos de recuperación para tiempos de E/S prolongados, un consumo excesivo de memoria por parte del servicio de replicación de Microsoft Exchange (MSExchangeRepl.exe) y otros casos graves en los que no se pueden programar subprocesos.

Incluso en entornos JBOD, los controladores de matrices de almacenamiento pueden tener problemas, como bloquearse o colgarse. Exchange 2010 incluía características de detección de E/S y de recuperación que proporcionaban resistencia mejorada. En la tabla siguiente se muestran estas características.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre</th>
<th>Comprobación</th>
<th>Acción</th>
<th>Umbral</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Detección de E/S de bloqueos de bases de datos de ESE</p></td>
<td><p>Comprobación de ESE de E/S pendientes</p></td>
<td><p>Genera un elemento de error en el canal Crimson para reiniciar el servidor</p></td>
<td><p>240 segundos</p></td>
</tr>
<tr class="even">
<td><p>Latido de canal de elemento erróneo</p></td>
<td><p>Garantiza que los elementos erróneos se pueden escribir en el canal Crimson y leerse de él</p></td>
<td><p>El servicio de replicación late en el canal Crimson y reinicia el servidor con errores</p></td>
<td><p>30 segundos</p></td>
</tr>
<tr class="odd">
<td><p>Latido del disco de sistema</p></td>
<td><p>Comprueba el estado del disco de sistema del servidor</p></td>
<td><p>Envía periódicamente E/S sin búfer al disco del sistema; reinicia el servidor en el tiempo de espera del latido</p></td>
<td><p>120 segundos</p></td>
</tr>
</tbody>
</table>


Exchange 2013 mejora la resistencia de almacenamiento y del servidor mediante nuevos comportamientos para otras condiciones graves. Estas condiciones y comportamientos se describen en la tabla siguiente.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre</th>
<th>Comprobación</th>
<th>Acción</th>
<th>Umbral</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Estado incorrecto del sistema</p></td>
<td><p>No se pueden programar subprocesos, ni siquiera los que no están administrados</p></td>
<td><p>Reiniciar el servidor</p></td>
<td><p>302 segundos</p></td>
</tr>
<tr class="even">
<td><p>Largos tiempos de E/S</p></td>
<td><p>Mediciones de latencia de operación de E/S</p></td>
<td><p>Reiniciar el servidor</p></td>
<td><p>41 segundos</p></td>
</tr>
<tr class="odd">
<td><p>Uso de la memoria del servicio de replicación</p></td>
<td><p>Medir el conjunto de trabajo de MSExchangeRepl.exe</p></td>
<td><ol>
<li><p>Registrar el evento 4395 en el canal Crimson con una solicitud de finalización del servicio</p></li>
<li><p>Iniciar la finalización de MSExchangeRepl.exe</p></li>
<li><p>Si se produce un error en la finalización del servicio, reinicie el servidor</p></li>
</ol></td>
<td><p>4 gigabytes (GB)</p></td>
</tr>
<tr class="even">
<td><p>Evento 129 del sistema (reinicialización del bus)</p></td>
<td><p>Comprobar el evento 129 en el registro de eventos del sistema</p></td>
<td><p>Reiniciar el servidor</p></td>
<td><p>Cuando ocurre el evento</p></td>
</tr>
<tr class="odd">
<td><p>Bloqueo de base de datos del clúster</p></td>
<td><p>El administrador de actualizaciones globales está bloqueado</p></td>
<td><p>Reiniciar el servidor</p></td>
<td><p>Cuando ocurre el evento</p></td>
</tr>
</tbody>
</table>


## Mejoras en las copias retrasadas

Entre las mejoras en las copias retrasadas, se incluyen la integración con Safety Net y la reproducción automática de archivos de registro en ciertos escenarios. Safety Net es una característica de transporte que reemplaza a la función de Exchange 2010 conocida como contenedor de transporte. Safety Net funciona de manera similar al contenedor de transporte, ya que consiste en una cola de entrega que se asocia al servicio de transporte en un buzón de servidores. Esta cola almacena copias de los mensajes que se entregaron correctamente a la base de datos de buzones de correo activa en el servidor de buzones de correo. Cada base de datos de buzones de correo activa del servidor de buzones de correo tiene su propia cola que almacena copias de los mensajes entregados. Puede especificar el tiempo que desea que Safety Net almacene copias de los mensajes entregados correctamente antes de que expiren o se eliminen de forma automática.

La red de seguridad asume parte de la responsabilidad de la redundancia de instantáneas en entornos de DAG. En estos entornos, la redundancia de instantáneas no necesita mantener otra copia del mensaje entregado en una cola de instantáneas mientras espera a que el mensaje entregado se replique en las copias pasivas de las bases de datos de buzones de correo en otros servidores de buzones de correo del DAG. La copia del mensaje entregado ya está almacenada en Safety Net, por lo que la redundancia de instantáneas puede volver a entregar el mensaje desde Safety Net si fuera necesario.

Con la introducción de Safety Net, la activación de una copia de base de datos retrasada se ha facilitado enormemente. Por ejemplo, supongamos que tiene una copia retrasada con un retraso de reproducción de 2 días. En ese caso, tendría que configurar Safety Net para un período de 2 días. Si detecta una situación en la que tenga que usar la copia retrasada, puede suspender su replicación y copiarla dos veces (para mantener la naturaleza retrasada de la base de datos y crear una copia adicional por si la necesita). Después, tome la copia y elimine todos los archivos de registro, salvo los que se encuentren en el intervalo requerido. Monte la copia, lo que desencadenará una solicitud automática a Safety Net para volver a entregar los últimos dos días de correo. Con Safety Net, no es necesario que busque el punto de corrupción. Obtiene el correo de los dos últimos días, menos los datos perdidos comúnmente en una conmutación por error con pérdidas.

Las copias retrasadas se pueden administrar ahora a sí mismas mediante la invocación de la reproducción automática del registro para que reproduzca los archivos de registro en ciertos escenarios:

  - Cuando se alcance un umbral de espacio en disco insuficiente

  - Cuando la copia retrasada tiene un daño físico y se debe revisar por páginas

  - Cuando hay menos de tres copias correctas disponibles (activas o pasivas; las copias de bases de datos retrasadas no cuentan) durante más de 24 horas

En Exchange 2010, la revisión de páginas no está disponible para las copias retrasadas. En Exchange 2013, la revisión de páginas está disponible para las copias retrasadas a través de esta característica de reproducción automática. Si el sistema detecta que la aplicación de revisiones es necesaria para una copia retrasada, los registros se vuelven a reproducir automáticamente en la copia retrasada al realizar la aplicación de revisiones. Las copias retrasadas también invocan esta característica de reproducción automática cuando se alcanza un umbral de espacio de disco bajo y cuando la copia retrasada se detecta como la única copia disponible durante un período específico.

El comportamiento de reproducción de copias retrasadas está deshabilitado de manera predeterminada, pero se puede habilitar mediante la ejecución del siguiente comando.

    Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true

Después de su habilitación, la reproducción ocurre cuando hay menos de tres copias. Puede cambiar el valor predeterminado de 3 modificando el siguiente valor DWORD del Registro.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

Para habilitar la reproducción cuando el espacio en disco insuficiente, debe configurar la siguiente entrada del Registro.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

Después de configurar cualquiera de estas opciones del Registro, reinicie el servicio de administración de Microsoft Exchange DAG para que los cambios surtan efecto.

Como ejemplo, considere un entorno donde una base de datos tiene 4 copias (3 copias de alta disponibilidad y 1 copia retrasada) y se utiliza el valor predeterminado de *ReplayLagManagerNumAvailableCopies*. Si una copia no retrasada está fuera de servicio por cualquier motivo (por ejemplo, se ha suspendido), la copia retrasada reproducirá automáticamente sus archivos de registro en 24 horas.

## Mejoras en la alerta de copia única

Los objetivos clave para las operaciones diarias de mensajería de Exchange 2013 son asegurarse de que los servidores funcionan de forma confiable y de que las copias de base de datos de buzones de correo están en buen estado. Debe supervisar de manera activa el hardware, el sistema operativo Windows y los servicios de Exchange. No obstante, cuando se ejecuta en un entorno de resistencia de buzones de Exchange 2013, es importante supervisar el mantenimiento y el estado del DAG y de las copias de bases de datos de buzones de correo. Resulta de especial importancia realizar una supervisión y administración del riesgo de redundancia de datos en períodos durante los cuales una base de datos replicada se comporte como una copia única. Esto es especialmente fundamental en entornos que no usan la matriz redundante de discos independientes (RAID) y, en cambio, implementan configuraciones de JBOD. En entornos RAID, un error de un solo disco no afecta a las copias de base de datos de buzones de correo activas. Sin embargo, en un entorno JBOD, un error de disco desencadenará una conmutación por error de base de datos.

En Exchange 2010, se introdujo el script CheckDatabaseRedundancy.ps1. Como su nombre indica, la finalidad del script es supervisar la redundancia de las bases de datos de buzones de correo replicadas corroborando que, por lo menos, haya dos copias actuales configuradas que sean correctas, así como avisar a un administrador a través de la generación de registros de evento cuando solo exista una copia correcta de una base de datos replicada. En tal caso, tanto las copias activas como las pasivas se cuentan a la hora de determinar la redundancia.

Entre las condiciones de copia única se incluyen, entre otras, las siguientes:

  - Error de una copia activa para replicarse en cualquier copia pasiva.

  - Error de todas las copias pasivas, que incluye los estados FailedAndSuspended y Failed además de los estados correctos en los que la copia se retrasa en la reproducción o copia de registros. Tenga en cuenta que las copias retrasadas no se consideran como tal si sus registros se reproducen en un margen de diez minutos en comparación con su período de retraso.

  - Error del sistema para conocer de manera precisa la generación de archivos de registro actuales de la copia activa.

Dado que para los administradores resulta fundamental conocer cuándo disponen de una copia correcta de una base de datos, el script CheckDatabaseRedundancy.ps1 se ha reemplazado por una funcionalidad nativa e integrada que forma parte del conjunto de mantenimiento DataProtection de disponibilidad administrada.

Esta funcionalidad nativa también avisa a los administradores a través de notificaciones de registros de eventos aunque, para distinguir las alertas de Exchange 2013 de las de Exchange 2010, Exchange 2013 usa los siguientes identificadores de evento:

  - Evento 4138 (alerta roja)

  - Evento 4139 (alerta verde)

En Exchange 2013, la funcionalidad nativa se ha mejorado para reducir el nivel de ruido de alerta que puede ocurrir cuando varias bases de datos del mismo servidor pasan a una condición de copia única. En Exchange 2010, las alertas de copia única se generan por base de datos. Como resultado, cuando ocurre un problema en el servidor que afecta a varias bases de datos y copias de bases de datos, pueden producirse tormentas de alertas. Dado que varios errores, como los problemas de memoria o del controlador, son de todo el servidor, existe una probabilidad moderadamente alta de que dicha tormenta de alerta ocurra para cada incidente del servidor. En Exchange 2013, las alertas se generan ahora servidor por servidor. Cuando una interrupción afecta a todo el servidor y la redundancia de datos está en peligro para varias copias de base de datos, se genera una sola alerta por servidor.

## Configuración automática de redes de DAG

Una red del DAG es un conjunto de una o más subredes usadas para el tráfico de replicación o el tráfico MAPI. Cada DAG contiene un máximo de una red MAPI y cero más redes de replicación. En Exchange 2010, el sistema crea las redes de DAG iniciales (por ejemplo, DAGNetwork01 y DAGNetwork02) en función de las subredes enumeradas por el servicio de clúster. En los entornos en los que se usan varias redes y las interfaces para una red específica (por ejemplo, la red MAPI) están en la misma subred, el administrador tiene que realizar muy pocas configuraciones adicionales. No obstante, en aquellos entornos en los que las interfaces para una red específica se encuentran en varias subredes, el administrador tiene que realizar una tarea denominada como contracción de redes de DAG.

En Exchange 2013, ya no es necesario contraer redes de DAG. Exchange 2013 sigue usando los mismos mecanismos de detección para distinguir entre la redes MAPI y de replicación, pero ahora contrae automáticamente las redes de DAG según sea necesario.

Además, el sistema administra ahora las redes de DAG de manera automática. Para ver las propiedades de una red de DAG mediante el Centro de administración de Exchange (EAC), configure el DAG para el control de red manual. Para ello, modifique las propiedades del DAG a través del EAC o mediante el cmdlet **Set-DatabaseAvailabilityGroup** para establecer el parámetro *ManualDagNetworkConfiguration* en `True`.

## Cambios en la selección de la mejor copia

La selección de la mejor copia (BCS) es un proceso de algoritmo interno que permite buscar la mejor copia de una base de datos para activarla, y que se selecciona de una lista de posibles copias para activación que incluyen su mantenimiento y estado. Active Manager selecciona la mejor copia disponible (y desbloqueada) para que sea la nueva copia de base de datos activa cuando se produzca un error en la copia activa existente o cuando un administrador realice un cambio sin destino. En Exchange 2010, el proceso BCS evalúa varios aspectos de cada copia de base de datos para determinar la mejor copia para activar. Estos incluían:

  - Copiar longitud de cola

  - Repetir longitud de cola

  - Estado de la base de datos

  - Estado del índice de contenido

En Exchange 2013, Active Manager realiza los mismos pasos y comprobaciones que BCS para determinar el estado de replicación y, además, ahora incluye el uso de una restricción respecto al orden descendente de los estados de mantenimiento. Como resultado de estos cambios, BCS se denomina ahora selección de la mejor copia y servidor (BCSS).

BCSS incluye varias comprobaciones nuevas de estado que forman parte de los componentes de supervisión de disponibilidad administrada integrados en Exchange 2013. Existen cuatro nuevas comprobaciones adicionales que realiza Active Manager (se indican por orden de realización):

1.  **Todo correcto**   Comprueba que un servidor que hospede una copia de la base de datos afectada tenga todos los componentes de supervisión en estado correcto.

2.  **Hasta correcto normal**   Comprueba que un servidor que hospede una copia de la base de datos afectada tenga todos los componentes de supervisión con prioridad Normal en estado correcto.

3.  **Todo mejor que el origen**   Comprueba que un servidor que hospede una copia de la base de datos afectada tenga los componentes de supervisión en un estado que sea mejor que el servidor actual que hospeda la copia afectada.

4.  **Igual que el origen**   Comprueba que un servidor que hospede una copia de la base de datos afectada tenga los componentes de supervisión en un estado que sea igual que el servidor actual que hospeda la copia afectada.

Si se invoca BCSS como consecuencia de una conmutación por error desencadenada por un componente de supervisión de disponibilidad administrada (por ejemplo, un respondedor de conmutación por error), se aplica una restricción obligatoria adicional en la que el estado del componente del servidor de destino debe ser mejor que el del servidor en el que ocurrió la conmutación por error. Por ejemplo, si un error de Microsoft Office Outlook Web App desencadena una conmutación por error administrada mediante un respondedor de conmutación por error, BCSS debe seleccionar un servidor que hospede una copia de la base de datos afectada en la cual Outlook Web App sea correcto.

## Servicio de administración del DAG

La actualización acumulada 2 (CU2) para la versión RTM de Exchange 2013 contiene un nuevo servicio en servidores de buzones de correo miembros de un DAG. Este servicio se denomina servicio de administración del DAG de Microsoft Exchange (MSExchangeDAGMgmt). Este nuevo servicio contiene funcionalidad de supervisión de DAG interna que anteriormente se ejecutaba dentro del servicio de replicación de Microsoft Exchange (MSExchangeRepl).

## DAG sin un punto de acceso administrativo al clúster

Todos los DAG que ejecutan Windows Server 2008 R2 o Windows Server 2012 requieren al menos una dirección IP en todas las subredes incluidas en la red MAPI. El clúster del DAG con el punto de acceso administrativo al clúster (también conocido como nombre de red del clúster) usa las direcciones IP asignadas al DAG para habilitar la resolución de nombres y la conectividad con el clúster (o de forma más precisa, la conectividad con el miembro del clúster que es propietario actualmente del grupo de recursos principal) usando el nombre del clúster. Windows Server 2012 R2 permite crear un clúster de conmutación por error sin un punto de acceso administrativo. Los clústeres de conmutación por error de Windows sin puntos de acceso administrativos tienen las siguientes características:

  - No hay ninguna dirección IP asignada al clúster y, por lo tanto, tampoco un recurso Dirección IP en el grupo de recursos principal del clúster.

  - No hay un nombre de red asignado al clúster y, por lo tanto, tampoco un recurso Nombre de red en el grupo de recursos principal del clúster

  - El nombre del clúster no está registrado en DNS y no se puede resolver en la red.

  - No hay un objeto de nombre clúster (CNO) creado en Active Directory.

  - El clúster de conmutación por error de Windows no se puede administrar con la herramienta Administración del clúster de conmutación por error. Se debe administrar mediante Windows PowerShell y los cmdlets de PowerShell se deben volver a ejecutar en cada miembro de clúster individual.

Cuando se ejecuta en Windows Server 2012 R2 o posteriores, el Service Pack 1 (SP1) para Exchange 2013 y posteriores permite crear un DAG sin un punto de acceso administrativo al clúster. Puede crear un DAG sin un punto de acceso administrativo mediante el Centro de administración de Exchange o el Shell. Para más información, vea [Creating DAGs](managing-database-availability-groups-exchange-2013-help.md) y [Crear un grupo de disponibilidad de base de datos](create-a-database-availability-group-exchange-2013-help.md).

