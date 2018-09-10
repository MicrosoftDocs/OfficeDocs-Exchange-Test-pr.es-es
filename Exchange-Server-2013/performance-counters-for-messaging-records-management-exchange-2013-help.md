---
title: 'Contador rendimiento para administración registro mensaje: Exchange 2013 Help'
TOCTitle: Contadores de rendimiento para la administración de registros de mensajes
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 51406543
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contadores de rendimiento para la administración de registros de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Los contadores de rendimiento de este tema supervisan el Asistente de carpetas administradas al implementar la administración de registros de mensajería (MRM) para Microsoft Exchange Server 2010. Dado que la ejecución del Asistente para carpeta administrada es un proceso que consume cuantiosos recursos, solamente deberá ejecutarlo cuando el servidor pueda tolerar una carga adicional. Cuando ejecute este asistente, también conviene supervisar el rendimiento del servidor. Además de los contadores de rendimiento mencionados en este tema, puede que desee supervisar también otros contadores de rendimiento que supervisan elementos como el rendimiento de disco y el uso de CPU.

Para obtener más información acerca de la supervisión de equipos que ejecutan MRM, consulte [Administración de registros de seguimiento de mensajería](monitoring-https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/messaging-records-management).

## Contadores de rendimiento para MRM

En la siguiente tabla, se describen los contadores de rendimiento para MRM.

### Contadores de rendimiento, objetos de rendimiento y descripción

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Contador de rendimiento</th>
<th>Objeto de rendimiento</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tiempo medio de procesamiento de buzones en segundos</p></td>
<td><p>Asistentes de MSExchange</p></td>
<td><p>Cuenta el tiempo medio de procesamiento de buzones por asistentes basados en tiempo.</p></td>
</tr>
<tr class="even">
<td><p>Buzones procesados</p></td>
<td><p>Asistentes de MSExchange</p></td>
<td><p>Cuenta el número de buzones procesados por asistentes basados en tiempo desde que se inició el servicio.</p></td>
</tr>
<tr class="odd">
<td><p>Buzones procesados/seg</p></td>
<td><p>Asistentes de MSExchange</p></td>
<td><p>Determina la tasa de buzones que los asistentes basados en tiempo procesan por segundo.</p></td>
</tr>
<tr class="even">
<td><p>Elementos eliminados pero recuperables</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Cuenta el número de elementos eliminados por el asistente para carpeta administrada desde el principio del intervalo de programación más reciente. (Los elementos aún son recuperables a través de la carpeta de elementos recuperables.) El número incluye elementos en los buzones de correo programados para ser procesados durante el intervalo de programación y los elementos en los buzones de correo que usted especificó para ser procesados. Este contador se restablece a cero al principio de cada intervalo de programación.</p></td>
</tr>
<tr class="odd">
<td><p>Elementos registrados</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Cuenta el número de elementos registrados en el diario para el Asistente de carpetas administradas desde el inicio de la mayoría de los intervalos de programación recientes. El número incluye elementos en los buzones programados para procesamiento durante el ciclo de trabajo actual y los elementos de los buzones especificados para procesamiento. Este contador se restablece a cero al principio de cada ciclo de trabajo.</p></td>
</tr>
<tr class="even">
<td><p>Elementos marcados como con fecha de retención pasada</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Cuenta el número de elementos marcados como con fecha de retención pasada por el asistente para carpeta administrada desde el principio del intervalo de programación más reciente. El número incluye elementos en los buzones programados para procesamiento durante el intervalo de programación y los elementos de los buzones especificados para procesamiento. Este contador se restablece a cero al principio de cada intervalo de programación.</p></td>
</tr>
<tr class="odd">
<td><p>Elementos movidos</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Cuenta el número de elementos movidos por el asistente para carpeta administrada desde el principio del intervalo de programación más reciente. El número incluye elementos en los buzones programados para procesamiento durante el intervalo de programación y los elementos de los buzones especificados para procesamiento. Este contador se restablece a cero al principio de cada intervalo de programación.</p></td>
</tr>
<tr class="even">
<td><p>Elementos eliminados permanentemente</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Cuenta el número de elementos eliminados permanentemente por el asistente para carpeta administrada desde el principio del intervalo de programación más reciente. El número incluye elementos en los buzones programados para procesamiento durante el intervalo de programación y los elementos de los buzones especificados para procesamiento. Este contador se restablece a cero al principio de cada intervalo de programación.</p></td>
</tr>
<tr class="odd">
<td><p>Elementos sujetos a directiva de retención</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Cuenta el número de elementos sujetos a directiva de retención por el asistente para carpeta administrada desde el principio del intervalo de programación más reciente. El número incluye elementos en los buzones programados para procesamiento durante el intervalo de programación y los elementos de los buzones especificados para procesamiento. Este contador se restablece a cero al principio de cada intervalo de programación. Este contador es la suma de los cuatro contadores relacionados con la caducidad:</p>
<ul>
<li><p>Elementos registrados</p></li>
<li><p>Elementos marcados como con fecha de retención pasada</p></li>
<li><p>Elementos movidos</p></li>
<li><p>Elementos eliminados permanentemente</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsExpired: el tamaño de los elementos sujetos a la directiva de retención (en bytes)</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el tamaño total de los elementos expirados por el Asistente para carpetas administradas (SoftDelete, HardDelete, MoveToArchive).</p>
<p>Se incluyen los siguientes elementos:</p>
<ul>
<li><p>Mensajes sujetos a eliminación o a movimiento a una carpeta personalizada administrada por una directiva de buzón de carpeta</p></li>
<li><p>Mensajes sujetos a eliminación o a movimiento a un archivo por la directiva de retención del usuario</p></li>
<li><p>Mensajes expirados por la directiva del contenedor</p></li>
<li><p>Mensajes limpiados por etiquetas de limpieza del sistema</p></li>
</ul>
<p>Este contador se reinicia a cero en todos los puntos de comprobación de ciclos de trabajo del ciclo de trabajo del Asistente para carpetas administradas.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsSoftDeleted: tamaño de elementos eliminados pero recuperables (en bytes)</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el tamaño total de los elementos eliminados de manera temporal por el Asistente de carpetas administradas.</p>
<p>Se incluyen los siguientes elementos:</p>
<ul>
<li><p>Mensajes eliminados de manera temporal por una directiva de buzón de carpetas administradas</p></li>
<li><p>Mensajes eliminados de manera temporal por una directiva de retención</p></li>
</ul>
<p>Este contador se reinicia a cero en todos los puntos de comprobación de ciclos de trabajo del ciclo de trabajo del Asistente para carpetas administradas.</p></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsPermanentlyDeleted: tamaño de elementos eliminados permanentemente (en bytes)</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el tamaño total de los elementos eliminados de manera temporal por el Asistente de carpetas administradas.</p>
<p>Se incluyen los siguientes elementos:</p>
<ul>
<li><p>Mensajes eliminados de manera permanente por una directiva de buzón de carpetas administradas</p></li>
<li><p>Mensajes eliminados de manera permanente por una directiva de retención</p></li>
<li><p>Mensajes eliminados de manera permanente por la directiva de elementos recuperables</p></li>
</ul>
<p>Este contador se reinicia a cero en todos los puntos de comprobación de ciclos de trabajo del ciclo de trabajo del Asistente para carpetas administradas.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsMoved: tamaño de los elementos movidos debido a una etiqueta de directiva de archivo (en bytes)</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el tamaño total de los elementos movidos a una carpeta o movidos a un archivo por el Asistente para carpetas administradas.</p>
<p>Se incluyen los siguientes elementos:</p>
<ul>
<li><p>Mensajes movidos a una carpeta personalizada administrada por una directiva de buzón de carpetas administradas</p></li>
<li><p>Mensajes movidos al archivo personal por una directiva de retención</p></li>
</ul>
<p>Este contador se reinicia a cero en todos los puntos de comprobación de ciclos de trabajo del ciclo de trabajo del Asistente para carpetas administradas.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsWithPersonalTag: elementos marcados con la etiqueta Personal (expiración o archivo)</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el número de veces que el usuario etiqueta elementos con una etiqueta personal.</p>
<p>Esto incluye etiquetas de archivo y eliminación.</p>
<p>Por ejemplo:</p>
<ul>
<li><p>Un elemento se etiqueta con una etiqueta personal.</p></li>
<li><p>Un elemento con una etiqueta personal se vuelve a etiquetar con otra etiqueta personal.</p></li>
</ul>
<p>Si una carpeta está etiquetada con una etiqueta personal, el contador aumenta con el número total de elementos en la carpeta.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsWithDefaultTag: elementos marcados con la etiqueta predeterminada (expiración o archivo)</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el número de elementos asignados a una etiqueta de directiva predeterminada (DPT) basada en una acción del usuario, por ejemplo, cuando un usuario selecciona un mensaje con una etiqueta personal y selecciona <strong>Usar directiva de carpeta</strong>.</p>
<p>Si se asigna una directiva de retención a un usuario nuevo con una DPT, el contador aumenta con el número de elementos que se asignarán al DPT debido a la directiva de retención.</p>

> [!NOTE]
> Si un usuario tiene una directiva de retención con una DPT, los nuevos mensajes que llegan mediante el transporte obtienen una etiqueta predeterminada y el contador no realiza un seguimiento de esto.


</td>
</tr>
<tr class="even">
<td><p>TotalItemsWithSystemCleanupTag: elementos marcados con la etiqueta de limpieza del sistema</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el número de elementos con la etiqueta de limpieza del sistema. Esto incluye los elementos de metadatos de buzón que no son visibles para los usuarios.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsExpiredByDefaultExpiryTag: elementos expirados debido a una etiqueta de expiración predeterminada</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el número de elementos expirados (eliminados temporalmente o definitivamente) por el Asistente de carpetas administradas debido a una etiqueta no personal (predeterminada o del sistema) en una directiva de retención.</p>
<p>esto no incluye los elementos expirados por la limpieza de elementos recuperables o la limpieza del sistema.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsExpiredByPersonalExpiryTag: elementos expirados debido a una etiqueta de expiración personal</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el número de elementos expirados (eliminados temporalmente o definitivamente) por el Asistente de carpetas administradas debido a una etiqueta personal (predeterminada o del sistema) en la directiva de retención.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsMovedByDefaultArchiveTag: elementos movidos debido a una etiqueta de archivo predeterminada</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el número de elementos movidos al archivo por el Asistente de carpetas administradas debido a una etiqueta de archivo no personal (predeterminada o del sistema) en una directiva de retención.</p>
<p>Esto no incluye los elementos movidos a la carpeta de elementos recuperables en el archivo por la limpieza de los elementos recuperables.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsMovedByPersonalArchiveTag: elementos movidos debido a una etiqueta de archivo</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el número de elementos movidos al archivo por el Asistente de carpetas administradas debido a una etiqueta de archivo personal en una directiva de retención.</p></td>
</tr>
<tr class="odd">
<td><p>TotalMovedDumpsterItems: elementos movidos a contenedores de buzones</p></td>
<td><p>Asistente de carpetas administradas de MSExchange</p></td>
<td><p>Indica el número de elementos movidos a la carpeta de elementos recuperables en el archivo por la limpieza de los elementos recuperables.</p></td>
</tr>
</tbody>
</table>

