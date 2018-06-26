---
title: 'AutoReseed: Exchange 2013 Help'
TOCTitle: AutoReseed
ms:assetid: 61f9a8be-070e-4c62-b505-52644fcff0c5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn789209(v=EXCHG.150)
ms:contentKeyID: 62523847
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AutoReseed

 

_**Se aplica a:**Exchange Server 2013 SP1_

_**Última modificación del tema:**2015-03-09_

La reinicialización automática, o AutoReseed, es una característica que sustituye a las acciones que generalmente suele realizar un administrador como respuesta a un error en el disco, un evento de base de datos dañada u otro problema que precise reinicializar una copia de base de datos. AutoReseed se ha diseñado con el fin de restaurar automáticamente la redundancia de bases de datos después de un error en el disco mediante el uso de discos de reserva que se aprovisionan al sistema.

## Introducción a AutoReseed

En una configuración de AutoReseed se usa una estructura de presentación de almacenamiento estándar, y el administrador elige el punto de inicio. AutoReseed consiste en restaurar la redundancia lo antes posible cuando se produce un error en una unidad. Esto conlleva la preasignación de un conjunto de volúmenes (incluidos los volúmenes de reserva) y de bases de datos mediante puntos de montaje. En el caso de un error de disco en el que el disco ya no esté disponible para el sistema operativo, o no se pueda escribir en él, el sistema asigna un volumen de reserva y las copias de bases de datos afectadas se reinicializan automáticamente.

1.  El servicio de replicación de Microsoft Exchange detecta copias de manera periódica que tengan el estado de FailedAndSuspended. Si todas las copias de bases de datos en un volumen configurado para AutoReseed están en un estado FailedandSuspended durante 15 minutos consecutivos, se inicia el flujo de trabajo de AutoReseed.

2.  AutoReseed intentará reanudar las copias erróneas y suspendidas hasta tres veces, con una suspensión de 5 minutos entre cada intento. A veces, después de que se reanuda una copia de base de datos de FailedandSuspended, la copia permanece en estado de error. Esto puede suceder por diversas razones, por lo que este paso está diseñado para controlar dichos casos. AutoReseed suspenderá automáticamente una copia de base de datos que ha estado en error durante 10 minutos consecutivos para mantener el flujo de trabajo en ejecución. Si las acciones de suspender y reanudar no tienen como resultado una copia de base de datos en buen estado, el flujo de trabajo continúa.

3.  Cuando encuentra una copia con ese estado, realiza algunas comprobaciones de requisitos previos. Por ejemplo, comprobará que haya disponible un disco de reserva, que la base de datos y sus archivos de registro estén configurados en el mismo volumen y en las ubicaciones adecuadas que coincidan con las convenciones de nomenclatura requeridas.

4.  Si las comprobaciones de los requisitos previos son correctas, la función Disk Reclaimer del servicio de replicación de Microsoft Exchange asigna, reasigna y formatea un disco de reserva según los plazos de la siguiente tabla. AutoReseed intentará asignar un volumen de reserva hasta 5 veces, con suspensiones de 1 hora entre cada intento.

5.  Una vez que se ha asignado una reserva, AutoReseed realizará una operación InPlaceSeed mediante el conmutador de inicialización SafeDeleteExistingFiles. Todas las bases de datos que había en el disco afectado se reinicializan usando la copia activa de la base de datos como origen de inicialización.

6.  Una vez completada la operación de inicialización, el servicio de replicación de Microsoft Exchange comprueba que la copia recién inicializada es correcta.

Una vez que se agoten todos los reintentos, se detiene el flujo de trabajo. Si, después de 3 días, la copia de base de datos sigue en estado FailedandSuspended, el estado del flujo de trabajo se restablece y vuelve a iniciar desde el paso 1. Este comportamiento de restablecer y reanudar es útil (e intencionado) ya que pueden transcurrir unos días antes de que se reemplace un disco con errores, un controlador, etc.

En este momento, si el error fue un error de disco, se requiere la intervención manual de un operador o administrador para quitar y remplazar el disco erróneo y volver a configurarlo como reserva.

AutoReseed se configura mediante tres propiedades del DAG. Dos de las propiedades se refieren a los dos puntos de montaje que están en uso. Exchange 2013 aprovecha el hecho de que Windows Server admite varios puntos de montaje por volumen. La propiedad *AutoDagVolumesRootFolderPath* hace referencia al punto de montaje que contiene todos los volúmenes disponibles. Esto incluye volúmenes que hospedan bases de datos y volúmenes de reserva. La propiedad *AutoDagDatabasesRootFolderPath* hace referencia al punto de montaje que contiene las bases de datos. La tercera propiedad de DAG, *AutoDagDatabaseCopiesPerVolume*, se usa para configurar el número de copias de base de datos por volumen.

A continuación se muestra un ejemplo de configuración de AutoReseed.

**Ejemplo de configuración de AutoReseed**

![Ejemplo de configuración de reinicialización automática](images/Dn789209.e3af7306-f5b4-4ec4-9ccf-222ec452699b(EXCHG.150).gif "Ejemplo de configuración de reinicialización automática")

En este ejemplo hay tres volúmenes, dos de los cuales contienen bases de datos (VOL1 y VOL2) y uno de reserva que está vacío y formateado (VOL3).

Para configurar AutoReseed:

1.  Los tres volúmenes se montan en un solo punto de montaje. En este ejemplo, se usa un punto de montaje de C:\\ExchVols. Este es el directorio utilizado para obtener el almacenamiento para las bases de datos de Exchange.

2.  Se monta el directorio raíz de las bases de datos de buzones de correo como otro punto de montaje. En este ejemplo, se usa un punto de montaje de C:\\ExchDBs. A continuación, se crea una estructura de directorio para que se cree un directorio principal para la base de datos y, en este, se crean dos subdirectorios: un archivo de base de datos y uno para los archivos de registro.

3.  Se crean bases de datos. En el ejemplo anterior se muestra un diseño sencillo mediante el uso de una sola base de datos por volumen. Por lo tanto, en VOL1 hay tres directorios: el directorio principal y dos subdirectorios (uno para el archivo de la base de datos de MDB1 y otro para sus registros). Si bien no se muestra en la imagen de ejemplo, en VOL2, también habría tres directorios: el directorio principal y en él, un directorio para el archivo de la base de datos de MDB2 y uno para sus archivos de registro.

En esta configuración, si se produjera un error en MDB1 o en MDB2, se reinicializaría una copia de la base de datos con error a VOL3 automáticamente.

## Disk Reclaimer

El componente de AutoReseed que asigna y formatea discos de repuesto se llama *Disk Reclaimer*. Disk Reclaimer formatea los discos de repuesto y los prepara para que se reinicialicen automáticamente en intervalos diferentes, según el estado del disco. Para que Disk Reclaimer formatee un disco, se deben cumplir ciertas condiciones:

  - Disk Reclaimer debe estar habilitado. Está habilitado de forma predeterminada, pero puede deshabilitarse mediante [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)).

  - El volumen debe tener un punto de montaje en la ruta de acceso a los volúmenes raíz (de forma predeterminada, C:\\ExchangeVolumes).

  - El volumen no debe tener puntos de montaje en la ruta de acceso a los volúmenes de base de datos (de forma predeterminada, C:\\ExchangeDatabases).

  - Si el volumen contiene archivos, ninguno de ellos debe haber sido tocado durante 24 horas.

Además de las condiciones anteriores, Disk Reclaimer solo intentará formatear un volumen determinado una vez al día. La tabla siguiente describe el comportamiento de formateo de Disk Reclaimer.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Estado del disco y copias de la base de datos</th>
<th>Intervalo de formateo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>El disco no está formateado, está formateado pero vacío o está formateado pero contiene archivos que no se han tocado en 24 horas, y hay copias correctas de bases de datos activas en el sitio local de Active Directory que se pueden usar como origen de inicialización.</p></td>
<td><p>1 día</p></td>
</tr>
<tr class="even">
<td><p>El disco no está formateado, está formateado pero vacío o está formateado pero contiene archivos que no se han tocado en 24 horas, pero no hay copias correctas de bases de datos activas en el sitio local de Active Directory que se puedan usar como origen de inicialización.</p></td>
<td><p>2 días</p></td>
</tr>
<tr class="odd">
<td><p>El disco no está formateado, está formateado pero vacío o está formateado pero contiene archivos que no se han tocado en 24 horas, y hay copias correctas de bases de datos activas en el sitio local de Active Directory que se pueden usar como origen de inicialización, pero hay archivos desconocidos aparte del archivo de base de datos (archivo EDB) y los archivos de registro.</p></td>
<td><p>2 semanas</p></td>
</tr>
<tr class="even">
<td><p>El disco no está formateado, está formateado pero vacío o está formateado pero contiene archivos que no se han tocado en 24 horas, y hay copias correctas de bases de datos activas en el sitio local de Active Directory que se pueden usar como origen de inicialización, pero hay uno o varios archivos de base de datos (archivos EDB) para bases de datos que no están en Active Directory.</p></td>
<td><p>2 semanas</p></td>
</tr>
</tbody>
</table>

