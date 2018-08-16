---
title: 'Opciones configuración de almacenamiento de Exchange 2013: Exchange 2013 Help'
TOCTitle: Opciones de configuración de almacenamiento de Exchange 2013
ms:assetid: 37cdeacf-74f9-4399-9860-4d1dbec12bb1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee832792(v=EXCHG.150)
ms:contentKeyID: 49895568
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Opciones de configuración de almacenamiento de Exchange 2013

 

_**Se aplica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Comprender los requisitos y las opciones de almacenamiento del rol de servidor de buzones de correo en Exchange Server 2013 es una parte importante de la solución de diseño de almacenamiento del servidor de buzones de correo.

**Contenido**

Arquitecturas de almacenamiento

Tipos de discos físicos

Prácticas recomendadas para las configuraciones de almacenamiento compatibles

## Arquitecturas de almacenamiento

La siguiente tabla describe las arquitecturas de almacenamiento compatibles y proporciona una guía de las prácticas recomendadas para cada tipo de arquitectura de almacenamiento según corresponda.

### Arquitecturas de almacenamiento compatibles

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Arquitectura de almacenamiento</th>
<th>Descripción</th>
<th>Práctica recomendada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Almacenamiento de conexión directa (DAS)</p></td>
<td><p>DAS es un sistema de almacenamiento digital conectado directamente a un servidor o estación de trabajo, sin intervención de una red de almacenamiento. Por ejemplo, los transportes DAS incluyen interfaz estándar de equipos pequeños conectados en serie (SCSI) y conexión de tecnología avanzada en serie (ATA).</p></td>
<td><p>No disponible.</p></td>
</tr>
<tr class="even">
<td><p>Red de área de almacenamiento (SAN): Interfaz estándar de equipos pequeños de Internet (iSCSI)</p></td>
<td><p>La SAN es una arquitectura que conecta dispositivos de almacenamiento de equipos remotos (como matriz de discos y bibliotecas de cinta) con servidores de modo que los dispositivos se muestran como conectados localmente al sistema operativo (por ejemplo, almacenamiento en bloque). Las SAN de (iSCSI) encapsulan comandos SCSI dentro de paquetes de IP y utilizan infraestructura de redes como transporte de almacenamiento (por ejemplo, Ethernet).</p></td>
<td><p>No compartir discos físicos de copia de seguridad de datos de Exchange con otras aplicaciones.</p>
<p>Utilizar redes de almacenamiento dedicadas.</p>
<p>Utilizar varias rutas de acceso de red para las configuraciones independientes.</p></td>
</tr>
<tr class="odd">
<td><p>SAN: Canal de fibra</p></td>
<td><p>Las SAN de canal de fibra encapsulan los comandos SCSI dentro de paquetes de canal de fibra y, en general, utilizan redes de canal de fibra especializadas como transporte de almacenamiento.</p></td>
<td><p>No compartir discos físicos de copia de seguridad de datos de Exchange con otras aplicaciones.</p>
<p>Utilizar varias rutas de acceso de red de canal de fibra para las configuraciones independientes.</p>
<p>Siga las prácticas recomendadas del proveedor para ajustar los adaptadores de bus host (HBA) de canal de fibra, por ejemplo, profundidad de la cola y destino de la cola.</p></td>
</tr>
</tbody>
</table>


Una unidad de almacenamiento conectado a la red (NAS) es un equipo independiente conectado a una red, cuyo único propósito consiste en suministrar servicios de almacenamiento de datos basados en archivos a otros dispositivos de la red. El sistema operativo y otro tipo de software en la unidad NAS proporcionan funcionalidad del almacenamiento de datos, sistemas de archivos y acceso a los archivos y la administración de esas funcionalidades (por ejemplo, almacenamiento de archivos).

Todo el almacenamiento utilizado por Exchange para almacenar datos de Exchange debe ser almacenamiento de nivel de bloque porque Exchange 2013 no admite el uso de volúmenes de NAS que no estén en el escenario SMB 3.0 indicado en el tema [Virtualización de Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md). Además, en un entorno virtualizado, no se admite el almacenamiento de NAS que se presenta al invitado como almacenamiento de nivel de bloque a través del hipervisor.

No se recomienda utilizar niveles de almacenamiento porque podría afectar negativamente al rendimiento del sistema. Por este motivo, no permita que el controlador de almacenamiento mueva automáticamente los archivos a los que más se accede a un almacenamiento "más rápido".

Arquitecturas de almacenamiento

## Tipos de discos físicos

La siguiente tabla proporciona una lista de los tipos de discos físicos compatibles y una guía de las prácticas recomendadas para cada tipo de disco físico según corresponda.

### Tipos de discos físicos compatibles

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de disco físico</th>
<th>Descripción</th>
<th>Procedimiento recomendado o admitido</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serie ATA (SATA)</p></td>
<td><p>SATA es una interfaz serie para discos ATA e IDE (electrónica de dispositivos integrados). Los discos SATA están disponibles en varios factores de forma, velocidades y capacidades.</p>
<p>En general, elija discos SATA para el almacenamiento de buzones de correo de Exchange 2013 cuando tenga los requisitos de diseño siguientes:</p>
<ul>
<li><p>Gran capacidad</p></li>
<li><p>Rendimiento moderado</p></li>
<li><p>Consumo moderado de energía</p></li>
</ul></td>
<td><p>Se admiten:  Discos con sector de 512 bytes para Windows Server 2008 y Windows Server 2008 R2. Además, los discos 512e se admiten en Windows Server 2008 R2 con lo siguiente:</p>
<ul>
<li><p>La revisión descrita en el <a href="https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=982018">artículo de Microsoft Knowledge Base 982018</a>. Hay disponible una actualización que mejora la compatibilidad de Windows 7 y Windows Server 2008 R2 con discos de formato avanzado.</p></li>
<li><p>Windows Server 2008 R2 con Service Pack 1 (SP1) y Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 y versiones posteriores es compatible con los discos con sectores de 4 kilobytes (KB) nativos y con los discos 512e. Para la compatibilidad es necesario que todas las copias de una base de datos residan en el mismo tipo de disco físico. Por ejemplo, no se admite la configuración en la que se hospede una copia de la base de datos en un disco con sectores de 512 bytes y otra copia de la misma base de datos en un disco 512e o 4K.</p>
<p>Práctica recomendada: Considere utilizar discos SATA de tipo empresarial que generalmente tienen características más avanzadas relacionadas con el calor, la vibración y la confiabilidad.</p></td>
</tr>
<tr class="even">
<td><p>SCSI conectados en serie</p></td>
<td><p>SCSI conectada en serie (Serial Attached SCSI) es una interfaz serie para discos SCSI. Los discos SCSI conectados en serie están disponibles en varios factores de forma, velocidades y capacidades.</p>
<p>En general, elija discos SCSI conectados en serie para el almacenamiento de buzones de correo de Exchange 2013 cuando tenga los requisitos de diseño siguientes:</p>
<ul>
<li><p>Capacidad moderada</p></li>
<li><p>Alto rendimiento</p></li>
<li><p>Consumo moderado de energía</p></li>
</ul></td>
<td><p>Se admiten:  Discos con sector de 512 bytes para Windows Server 2008 y Windows Server 2008 R2. Además, los discos 512e se admiten en Windows Server 2008 R2 con lo siguiente:</p>
<ul>
<li><p>La revisión descrita en el <a href="https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=982018">artículo de Microsoft Knowledge Base 982018</a>. Hay disponible una actualización que mejora la compatibilidad de Windows 7 y Windows Server 2008 R2 con discos de formato avanzado.</p></li>
<li><p>Windows Server 2008 R2 con Service Pack 1 (SP1) y Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 y versiones posteriores es compatible con los discos con sectores de 4 kilobytes (KB) nativos y con los discos 512e. Para la compatibilidad es necesario que todas las copias de una base de datos residan en el mismo tipo de disco físico. Por ejemplo, no se admite la configuración en la que se hospede una copia de la base de datos en un disco con sectores de 512 bytes y otra copia de la misma base de datos en un disco 512e o 4K.</p>
<p>Procedimiento recomendado: debe deshabilitar el almacenamiento en caché de escritura de disco físico cuando se usa sin un SAI (UPS).</p></td>
</tr>
<tr class="odd">
<td><p>Canal de fibra</p></td>
<td><p>El canal de fibra es una interfaz eléctrica utilizada para conectar discos a los SAN basados en canal de fibra. Los discos de canal de fibra están disponibles en varias velocidades y capacidades.</p>
<p>En general, elija discos de canal de fibra para el almacenamiento de buzones de correo de Exchange 2013 cuando tenga los requisitos de diseño siguientes:</p>
<ul>
<li><p>Capacidad moderada</p></li>
<li><p>Alto rendimiento</p></li>
<li><p>Conectividad de SAN</p></li>
</ul></td>
<td><p>Se admiten:  Discos con sector de 512 bytes para Windows Server 2008 y Windows Server 2008 R2. Además, los discos 512e se admiten en Windows Server 2008 R2 con lo siguiente:</p>
<ul>
<li><p>La revisión descrita en el <a href="https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=982018">artículo de Microsoft Knowledge Base 982018</a>. Hay disponible una actualización que mejora la compatibilidad de Windows 7 y Windows Server 2008 R2 con discos de formato avanzado.</p></li>
<li><p>Windows Server 2008 R2 con Service Pack 1 (SP1) y Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 y versiones posteriores es compatible con los discos con sectores de 4 kilobytes (KB) nativos y con los discos 512e. Para la compatibilidad es necesario que todas las copias de una base de datos residan en el mismo tipo de disco físico. Por ejemplo, no se admite la configuración en la que se hospede una copia de la base de datos en un disco con sectores de 512 bytes y otra copia de la misma base de datos en un disco 512e o 4K.</p>
<p>Procedimiento recomendado: debe deshabilitar el almacenamiento en caché de escritura de disco físico cuando se usa sin un SAI (UPS).</p></td>
</tr>
<tr class="even">
<td><p>Unidad de estado sólido (SSD) (disco flash)</p></td>
<td><p>El SSD es un dispositivo de almacenamiento de datos que utiliza memoria en estado sólido para almacenar datos persistentes. Un SSD emula una interfaz de unidad de disco duro. Los discos SSD están disponibles en una variedad de velocidades (diferentes capacidades de rendimiento de E/S) y capacidades.</p>
<p>En general, elija discos SSD para el almacenamiento de buzones de correo de Exchange 2013 cuando tenga los requisitos de diseño siguientes:</p>
<ul>
<li><p>Poca capacidad</p></li>
<li><p>Rendimiento extremadamente alto</p></li>
</ul></td>
<td><p>Se admiten:  Discos con sector de 512 bytes para Windows Server 2008 y Windows Server 2008 R2. Además, los discos 512e se admiten en Windows Server 2008 R2 con lo siguiente:</p>
<ul>
<li><p>La revisión descrita en el <a href="https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=982018">artículo de Microsoft Knowledge Base 982018</a>. Hay disponible una actualización que mejora la compatibilidad de Windows 7 y Windows Server 2008 R2 con discos de formato avanzado.</p></li>
<li><p>Windows Server 2008 R2 con Service Pack 1 (SP1) y Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 y versiones posteriores es compatible con los discos con sectores de 4 kilobytes (KB) nativos y con los discos 512e. Para la compatibilidad es necesario que todas las copias de una base de datos residan en el mismo tipo de disco físico. Por ejemplo, no se admite la configuración en la que se hospede una copia de la base de datos en un disco con sectores de 512 bytes y otra copia de la misma base de datos en un disco 512e o 4K.</p>
<p>Procedimiento recomendado: debe deshabilitar el almacenamiento en caché de escritura de disco físico cuando se usa sin un SAI (UPS).</p>
<p>En general, los servidores de buzones de correo de Exchange 2013 no necesitan tener características de rendimiento de almacenamiento de SSD.</p></td>
</tr>
</tbody>
</table>


## Factores a considerar al elegir los tipos de discos

Existen diversas ventajas e inconvenientes a la hora de elegir los tipos de disco para el almacenamiento de Exchange 2013. El disco correcto es aquel que tiene equilibrio de rendimiento (secuencial y aleatorio) con capacidad, confiabilidad, utilización de energía y costo de capital. La siguiente tabla de tipos de discos físicos compatibles brinda información para ayudarlo al considerar estos factores.

Desde el punto de vista del rendimiento, usar discos grandes y más lentos para el almacenamiento de Exchange es aceptable, siempre que los discos puedan mantener una latencia promedio de lectura y escritura de latencia de 20 ms o menos con carga.

### Factores de elección del tipo de disco

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Velocidad de disco (en RPM)</th>
<th>Factor de forma de disco</th>
<th>Interfaz o transporte</th>
<th>Capacidad</th>
<th>Rendimiento de E/S aleatorio</th>
<th>Rendimiento de E/S secuencial</th>
<th>Utilización de energía</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5.400</p></td>
<td><p>2,5 pulgadas</p></td>
<td><p>SATA</p></td>
<td><p>Media</p></td>
<td><p>Deficiente</p></td>
<td><p>Deficiente</p></td>
<td><p>Excelente</p></td>
</tr>
<tr class="even">
<td><p>5.400</p></td>
<td><p>3,5 pulgadas</p></td>
<td><p>SATA</p></td>
<td><p>Excelente</p></td>
<td><p>Deficiente</p></td>
<td><p>Deficiente</p></td>
<td><p>Por encima de la media</p></td>
</tr>
<tr class="odd">
<td><p>7.200</p></td>
<td><p>2,5 pulgadas</p></td>
<td><p>SATA</p></td>
<td><p>Media</p></td>
<td><p>Media</p></td>
<td><p>Media</p></td>
<td><p>Excelente</p></td>
</tr>
<tr class="even">
<td><p>7.200</p></td>
<td><p>2,5 pulgadas</p></td>
<td><p>SCSI conectados en serie</p></td>
<td><p>Media</p></td>
<td><p>Media</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Excelente</p></td>
</tr>
<tr class="odd">
<td><p>7.200</p></td>
<td><p>3,5 pulgadas</p></td>
<td><p>SATA</p></td>
<td><p>Excelente</p></td>
<td><p>Media</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Por encima de la media</p></td>
</tr>
<tr class="even">
<td><p>7.200</p></td>
<td><p>3,5 pulgadas</p></td>
<td><p>SCSI conectados en serie</p></td>
<td><p>Excelente</p></td>
<td><p>Media</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Por encima de la media</p></td>
</tr>
<tr class="odd">
<td><p>7.200</p></td>
<td><p>3,5 pulgadas</p></td>
<td><p>Canal de fibra</p></td>
<td><p>Excelente</p></td>
<td><p>Media</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Media</p></td>
</tr>
<tr class="even">
<td><p>10.000</p></td>
<td><p>2,5 pulgadas</p></td>
<td><p>SCSI conectados en serie</p></td>
<td><p>Por debajo de la media</p></td>
<td><p>Excelente</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Por encima de la media</p></td>
</tr>
<tr class="odd">
<td><p>10.000</p></td>
<td><p>3,5 pulgadas</p></td>
<td><p>SATA</p></td>
<td><p>Media</p></td>
<td><p>Media</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Por encima de la media</p></td>
</tr>
<tr class="even">
<td><p>10.000</p></td>
<td><p>3,5 pulgadas</p></td>
<td><p>SCSI conectados en serie</p></td>
<td><p>Media</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Por debajo de la media</p></td>
</tr>
<tr class="odd">
<td><p>10.000</p></td>
<td><p>3,5 pulgadas</p></td>
<td><p>Canal de fibra</p></td>
<td><p>Media</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Por encima de la media</p></td>
<td><p>Por debajo de la media</p></td>
</tr>
<tr class="even">
<td><p>15.000</p></td>
<td><p>2,5 pulgadas</p></td>
<td><p>SCSI conectados en serie</p></td>
<td><p>Deficiente</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
<td><p>Media</p></td>
</tr>
<tr class="odd">
<td><p>15.000</p></td>
<td><p>3,5 pulgadas</p></td>
<td><p>SCSI conectados en serie</p></td>
<td><p>Media</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
<td><p>Por debajo de la media</p></td>
</tr>
<tr class="even">
<td><p>15.000</p></td>
<td><p>3,5 pulgadas</p></td>
<td><p>Canal de fibra</p></td>
<td><p>Media</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
<td><p>Deficiente</p></td>
</tr>
<tr class="odd">
<td><p>SSD: tipo empresarial</p></td>
<td><p>No aplicable</p></td>
<td><p>SATA, SCSI conectados en serie, canal de fibra</p></td>
<td><p>Deficiente</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
</tr>
</tbody>
</table>


Arquitecturas de almacenamiento

## Prácticas recomendadas para las configuraciones de almacenamiento compatibles

Esta sección brinda información de las prácticas recomendadas relacionadas con las configuraciones de controladores de matriz y discos compatibles.

La matriz redundante de discos independientes (RAID), en general, se utiliza para mejorar las características de rendimiento de los discos individuales (mediante el seccionado de datos de varios discos) además de para proporcionar protección de errores de disco individuales. Gracias a los avances de alta disponibilidad de Exchange 2013, la RAID ya no es un componente necesario de diseño de almacenamiento de Exchange 2013. Sin embargo, sigue siendo un componente básico del diseño de almacenamiento de Exchange 2013 en los servidores independientes y las soluciones que requieren tolerancia a errores de almacenamiento.

**Sistema operativo, sistema o volumen de archivo de paginación**

La configuración recomendada para un sistema operativo, sistema o volumen de archivo de paginación es mediante el uso de la tecnología RAID para proteger este tipo de datos. La configuración RAID recomendada es RAID-1 o RAID-1/0; no obstante, se admiten todos los tipos RAID.

**Bases de datos de buzones de correo y volúmenes de registros independientes**

Si implementa una arquitectura de rol de servidor de buzones de correo independiente, se requiere la tecnología RAID para la base de datos de buzones de correo y los volúmenes de registros. La configuración RAID recomendada para volúmenes de buzones de correo es RAID-1/0 (especialmente si usa discos de 5,4 K o 7,2 K); no obstante, se admiten todos los tipos RAID. Para volúmenes de registros, RAID-1 o RAID-1/0 es la configuración RAID recomendada.

Al usar configuraciones RAID-5 o RAID-6 para el sistema operativo, el archivo de paginación o los volúmenes de datos de Exchange, tenga en cuenta lo siguiente:

  - Las configuraciones RAID-5, incluidas las variaciones como RAID-50 y RAID-51, no deben tener más de 7 discos por grupo de matrices, y deben tener el análisis de superficies y la limpieza de controlador de alta prioridad habilitados.

  - Las configuraciones RAID-6 deben tener la limpieza de matriz de alta prioridad y el análisis de superficies habilitados.

Aunque JBOD se admite en arquitecturas de alta disponibilidad con 3 o más copias de bases de datos altamente disponibles, dado que los volúmenes de bases de datos de buzones de correo y de registros son independientes, JBOD no se recomienda.

**Ubicación compartida de base de datos de buzones de correo y de volumen de registros**

La ubicación compartida de la base de datos de buzones de correo y del volumen de registros no se recomienda en arquitecturas independientes. En arquitecturas de alta disponibilidad, hay dos posibilidades para este escenario:

1.  Una sola base de datos por volumen

2.  Varias bases de datos por volumen

**Una sola base de datos por volumen**

Desde la perspectiva de Exchange, JBOD significa almacenar la base de datos y los registros asociados en un solo disco. Para implementar JBOD, se debe implementar un mínimo de tres copias de base de datos de alta disponibilidad. Si se usa un solo disco, se contará con un único punto de posible error, ya que, cuando se produce un error en el disco, la copia de base de datos que reside en ese disco se pierde. Si se cuenta con un mínimo de tres copias de base de datos, se garantiza la tolerancia a errores, dado que se cuenta con dos copias adicionales en caso de error en una copia (o un disco). Sin embargo, la ubicación de tres copias de base de datos de alta disponibilidad, además del uso de copias de base de datos retrasadas, puede afectar el diseño de almacenamiento. La siguiente tabla muestra las pautas para considerar implementaciones de RAID o JBOD.

### Consideraciones para RAID o JBOD

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidores de centro de datos</th>
<th>Dos copias de alta disponibilidad (totales)</th>
<th>Tres copias de alta disponibilidad (totales)</th>
<th>Dos o más copias de alta disponibilidad por centro de datos</th>
<th>Una copia retrasada</th>
<th>Dos o varias copias retrasadas por centro de datos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de centros de datos principales</p></td>
<td><p>RAID</p></td>
<td><p>RAID o JBOD (2 copias)</p></td>
<td><p>RAID o JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID o JBOD</p></td>
</tr>
<tr class="even">
<td><p>Servidores de centros de datos secundarios</p></td>
<td><p>RAID</p></td>
<td><p>RAID (1 copia)</p></td>
<td><p>RAID o JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID o JBOD</p></td>
</tr>
</tbody>
</table>


Para una implementación en JBOD con servidores de centro de datos primario, se necesitan tres o más copias de base de datos de alta disponibilidad en el DAG. Si se combinan copias retrasadas en el mismo servidor que hospeda copias de base de datos de alta disponibilidad (por ejemplo, sin usar servidores dedicados para copias de base de datos retrasadas), se necesitan al menos dos copias de base de datos retrasadas.

Para que los servidores de centro de datos secundario usen JBOD, se debe contar con al menos dos copias de base de datos de alta disponibilidad en el centro de datos secundario. La pérdida de una copia en el centro de datos secundario no resultará en la necesidad de reinicialización en toda la WAN o en la disponibilidad de un único punto de error posible en caso de que se active el centro de datos secundario. Si se combinan copias de base de datos retrasadas en el mismo servidor que hospeda copias de base de datos de alta disponibilidad (por ejemplo, sin usar servidores dedicados para copias de base de datos retrasadas), se necesitan al menos dos copias de base de datos retrasadas.

Para servidores de copias de base de datos retrasadas, se requieren al menos dos copias de base de datos retrasadas dentro del centro de datos para utilizar JBOD. De lo contrario, la pérdida de un disco provocará la pérdida de la copia de base de datos retrasada y la pérdida del mecanismo de control.

**Varias bases de datos por volumen**

Varias bases de datos por volumen es un nuevo escenario de JBOD disponible en Exchange 2013, que permite que copias activas y pasivas (incluidas las copias retrasadas) se mezclen en un solo disco, lo que a su vez permite un mejor uso del disco. No obstante, para implementar copias retrasadas de este modo, debe habilitarse la reproducción de archivos de registro de copia retrasada. La siguiente tabla muestra directrices y consideraciones de JBOD para varias bases de datos por volumen.

### Consideraciones de JBOD

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidores de centro de datos</th>
<th>3 o varias copias (total)</th>
<th>Dos o varias copias por centro de datos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de centros de datos principales</p></td>
<td><p>JBOD</p></td>
<td><p>JBOD</p></td>
</tr>
<tr class="even">
<td><p>Servidores de centros de datos secundarios</p></td>
<td><p>N/D</p></td>
<td><p>JBOD</p></td>
</tr>
</tbody>
</table>


En la siguiente tabla, se proporcionan instrucciones acerca de las configuraciones de la matriz de almacenamiento de Exchange 2013.

### Tipos de RAID admitidos para el rol de servidor de buzones de correo de Exchange 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de RAID</th>
<th>Descripción</th>
<th>Procedimiento recomendado o admitido</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamaño de la banda de matriz RAID (KB) de disco</p></td>
<td><p>El tamaño de sección es la unidad de distribución de datos por disco en un conjunto RAID. También se denomina <em>tamaño de bloque</em>.</p></td>
<td><p>Práctica recomendada: 256 KB o superior. Seguir las prácticas recomendadas del proveedor de almacenamiento.</p></td>
</tr>
<tr class="even">
<td><p>Configuraciones de la memoria caché de matriz de almacenamiento</p></td>
<td><p>La configuración de caché es proporcionada por un controlador de matriz redundante con caché y batería.</p></td>
<td><p>Procedimiento recomendado: 100 por cien de caché de escritura (caché respaldada por batería o flash) para controladores de almacenamiento de DAS en una configuración RAID o JBOD. 75 por ciento de caché de escritura y 25 por ciento de caché de lectura (caché respaldada por batería o flash) para otros tipos de soluciones de almacenamiento, como SAN. Si su proveedor de SAN tiene otros procedimientos recomendados para la configuración de la caché en su plataforma, siga las instrucciones del proveedor.</p></td>
</tr>
<tr class="odd">
<td><p>Almacenamiento en caché de escritura de disco físico</p></td>
<td><p>La configuración de la memoria caché se encuentra en cada disco individual.</p></td>
<td><p>Se admite: Debe deshabilitar el almacenamiento en caché de escritura de disco físico cuando se utiliza sin un SAI (UPS).</p></td>
</tr>
</tbody>
</table>


En la siguiente tabla, se proporcionan instrucciones acerca de las opciones de archivo de base de datos y registro.

### Opciones de archivo de base de datos y registro para el rol del servidor de buzones de correo de Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Opciones de archivo de base de datos y registro</th>
<th>Descripción</th>
<th>Independiente: procedimiento recomendado o admitido</th>
<th>Alta disponibilidad: procedimiento recomendado o admitido</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ubicación del archivo: aislamiento de base de datos por registro</p></td>
<td><p>El aislamiento de base de datos por registro se refiere a la colocación de registros y archivos de bases de datos de la misma base de datos del buzón de correo en diferentes volúmenes respaldados por diferentes discos físicos.</p></td>
<td><p>Práctica recomendada: Para lograr la capacidad de recuperación, mueva el archivo de la base de datos (.edb) y los registros de la misma base de datos a volúmenes diferentes respaldados por discos físicos diferentes.</p></td>
<td><p>Se admite: El aislamiento de los registros y las bases de datos no es necesario.</p></td>
</tr>
<tr class="even">
<td><p>Ubicación del archivo: archivos de bases de datos por volumen</p></td>
<td><p>Los archivos de bases de datos por volumen se refieren a la manera en que distribuye archivos de base de datos en los volúmenes de discos.</p></td>
<td><p>Procedimiento recomendado: En función de la metodología de copia de seguridad.</p></td>
<td><p>Se admite: Al usar JBOD, cree un único volumen con directorios separados para las bases de datos y los archivos de registro.</p></td>
</tr>
<tr class="odd">
<td><p>Ubicación del archivo: secuencias de registro por volumen</p></td>
<td><p>Las secuencias de registros por volumen se refieren a la manera en que distribuye archivos de base de datos en los volúmenes de discos.</p></td>
<td><p>Procedimiento recomendado: En función de la metodología de copia de seguridad.</p></td>
<td><p>Se admite: Al usar JBOD, cree un único volumen con directorios separados para las bases de datos y los archivos de registro.</p>
<p>Práctica recomendada: Al usar JBOD, use varias bases de datos por volumen.</p></td>
</tr>
<tr class="even">
<td><p>Tamaño de la base de datos</p></td>
<td><p>El tamaño de la base de datos se refiere al tamaño del archivo de la base de datos (.edb) del disco.</p></td>
<td><p>Se admite: Aproximadamente 16 terabytes.</p>
<p>Procedimiento recomendado:</p>
<ul>
<li><p>200 gigabytes (GB) o menos.</p></li>
<li><p>Aprovisionamiento para el 120 por ciento del tamaño máximo de la base de datos calculado.</p></li>
</ul></td>
<td><p>Se admite: Aproximadamente 16 terabytes.</p>
<p>Procedimiento recomendado:</p>
<ul>
<li><p>2 terabytes como máximo.</p></li>
<li><p>Aprovisionamiento para el 120 por ciento del tamaño máximo de la base de datos calculado.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Método de truncamiento del registro</p></td>
<td><p>El método de truncamiento del registro es el proceso para truncar y eliminar archivos de registro de base de datos antiguos. Existen dos mecanismos:</p>
<ul>
<li><p>Registro circular, en el cual Exchange elimina los registros.</p></li>
<li><p>Truncamiento de registro, que se realiza después de haber realizado copias de seguridad del servicio de instantáneas de volumen completo o incremental.</p></li>
</ul></td>
<td><p>Procedimiento recomendado:</p>
<ul>
<li><p>Utilizar copias de seguridad para el truncamiento del registro (por ejemplo, registro circular deshabilitado).</p></li>
<li><p>Provisión para tres días de la capacidad de generación de registro.</p></li>
</ul></td>
<td><p>Procedimiento recomendado:</p>
<ul>
<li><p>Habilite el registro circular para implementaciones que usan características de protección de datos nativos de Exchange.</p></li>
<li><p>Provisión para tres días más allá de la reproducción de la configuración de la capacidad de generación de registro.</p></li>
</ul></td>
</tr>
</tbody>
</table>


En la siguiente tabla, se proporcionan instrucciones acerca de los tipos de discos de Windows.

### Tipos de discos de Windows para el rol de servidor de buzones de correo de Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de disco de Windows</th>
<th>Descripción</th>
<th>Independiente: procedimiento recomendado o admitido</th>
<th>Alta disponibilidad: procedimiento recomendado o admitido</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Disco básico</p></td>
<td><p>El disco inicializado para un almacenamiento básico se denomina disco básico. Un disco básico contiene volúmenes básicos, como particiones primarias, particiones extendidas y unidades lógicas.</p></td>
<td><p>Se admite.</p>
<p>Procedimiento recomendado: Use discos básicos.</p></td>
<td><p>Se admite.</p>
<p>Procedimiento recomendado: Use discos básicos.</p></td>
</tr>
<tr class="even">
<td><p>Disco dinámico</p></td>
<td><p>El disco inicializado para almacenamiento dinámico se denomina disco dinámico. Un disco dinámico contiene volúmenes dinámicos, como volúmenes simples, extendidos, seccionados, reflejados y de RAID-5.</p></td>
<td><p>Se admite.</p></td>
<td><p>Se admite.</p></td>
</tr>
</tbody>
</table>


En la siguiente tabla, se proporciona orientación sobre las configuraciones de volumen.

### Configuraciones de volumen para el rol de servidor de buzones de correo de Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración de volumen</th>
<th>Descripción</th>
<th>Independiente: procedimiento recomendado o admitido</th>
<th>Alta disponibilidad: procedimiento recomendado o admitido</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tabla de particiones (GPT)</p></td>
<td><p>El GPT es una arquitectura de disco que se expande por el esquema de partición de registro de inicio maestro (MBR). El tamaño máximo de partición con formato NTFS es 256 terabytes.</p></td>
<td><p>Se admite.</p>
<p>Procedimiento recomendado: use particiones GPT.</p></td>
<td><p>Se admite.</p>
<p>Procedimiento recomendado: use particiones GPT.</p></td>
</tr>
<tr class="even">
<td><p>MBR</p></td>
<td><p>Un MBR, o sector de partición, es el sector de inicio de 512 bytes que es el primer sector (LBA Sector 0) de un dispositivo de almacenamiento de datos con particiones como un disco duro. El tamaño máximo de partición con formato NTFS es 2 terabytes.</p></td>
<td><p>Se admite.</p></td>
<td><p>Se admite.</p></td>
</tr>
<tr class="odd">
<td><p>Alineación de partición</p></td>
<td><p>La alineación de partición hace referencia a la alineación de particiones en los límites del sector para un rendimiento óptimo.</p></td>
<td><p>Se admite: El valor predeterminado de Windows Server 2008 R2 y de Windows Server 2012 es 1 megabyte (MB).</p></td>
<td><p>Se admite: El valor predeterminado de Windows Server 2008 R2 y de Windows Server 2012 es 1 MB.</p></td>
</tr>
<tr class="even">
<td><p>Ruta de acceso del volumen</p></td>
<td><p>La ruta de acceso del volumen hace referencia a cómo se obtiene acceso a un volumen.</p></td>
<td><p>Se admite: punto de montaje o letra de unidad.</p>
<p>Práctica recomendada: El volumen de host de montaje debe estar habilitado para RAID.</p></td>
<td><p>Se admite: punto de montaje o letra de unidad.</p>
<p>Práctica recomendada: El volumen de host de montaje debe estar habilitado para RAID.</p></td>
</tr>
<tr class="odd">
<td><p>Sistema de archivos</p></td>
<td><p>El sistema de archivos es un método para almacenar y organizar archivos del equipo y los datos que contienen para facilitar la búsqueda y el acceso a dichos archivos.</p></td>
<td><p>Se admiten: NTFS y ReFS.</p></td>
<td><p>Se admiten: NTFS y ReFS.</p></td>
</tr>
<tr class="even">
<td><p>Desfragmentación de NTFS</p></td>
<td><p>La desfragmentación de NTFS es un proceso que reduce la cantidad de fragmentación en sistemas de archivos de Windows. Lo realiza mediante la organización física de los contenidos del disco para almacenar las piezas de cada archivo cercanas y contiguas.</p></td>
<td><p>Se admite.</p>
<p>Procedimiento recomendado: No es necesario y no se recomienda. En Windows Server 2012, también recomendamos deshabilitar la optimización automática del disco y la desfragmentación.</p></td>
<td><p>Se admite.</p>
<p>Procedimiento recomendado: No es necesario y no se recomienda. En Windows Server 2012, también recomendamos deshabilitar la optimización automática del disco y la desfragmentación.</p></td>
</tr>
<tr class="odd">
<td><p>Tamaño de unidad de asignación de NTFS</p></td>
<td><p>El tamaño de unidad de asignación representa la cantidad más pequeña de espacio en disco que se puede asignar para contener un archivo.</p></td>
<td><p>Se admite: todos los tamaños de unidad de asignación.</p>
<p>Procedimiento recomendado: 64 KB para volúmenes de .edb y de archivos de registro.</p></td>
<td><p>Se admite: todos los tamaños de unidad de asignación.</p>
<p>Procedimiento recomendado: 64 KB para volúmenes de .edb y de archivos de registro.</p></td>
</tr>
<tr class="even">
<td><p>Compresión NTFS</p></td>
<td><p>La compresión NTFS es el proceso de reducción del tamaño real del archivo almacenado en el disco duro.</p></td>
<td><p>Se admite: no es compatible con archivos de registro o bases de datos de Exchange.</p></td>
<td><p>Se admite: no es compatible con archivos de registro o bases de datos de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>Sistema de archivos (EFS) de cifrado de NTFS</p></td>
<td><p>El EFS le permite a los usuarios cifrar archivos individuales, carpetas o unidades de datos completa. Debido a que EFS proporciona un cifrado seguro mediante algoritmos estándar del sector y criptografía mediante claves públicas, los archivos cifrados son confidenciales incluso si un atacante omite la seguridad del sistema.</p></td>
<td><p>Se admite: no es compatible con archivos de registro o bases de datos de Exchange.</p></td>
<td><p>no es compatible con archivos de registro o bases de datos de Exchange.</p></td>
</tr>
<tr class="even">
<td><p>Windows BitLocker (cifrado de volumen)</p></td>
<td><p>Windows BitLocker es una característica para la protección en Windows Server 2008. BitLocker protege contra el robo o la puesta en peligro de los datos en equipos perdidos o robados y ofrece un borrado de datos más seguro cuando los equipos se retiran.</p></td>
<td><p>Se admite: todas las bases de datos y los archivos de registro de Exchange.</p></td>
<td><p>Se admite: Todas las bases de datos y los archivos de registro de Exchange. Los clústeres de conmutación por error de Windows requieren Windows Server 2008 R2 o Windows Server 2008 R2 SP1 y la revisión siguiente: <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=2446607">No puede habilitar BitLocker en un volumen de disco en Windows Server 2008 R2 si el PC es un nodo de clústeres de conmutación por error</a>. Los volúmenes de Exchange que tienen habilitado Bitlocker no se admiten en clústeres de conmutación por error de Windows que ejecutan versiones anteriores de Windows.</p>
<p>Para obtener más información sobre el cifrado BitLocker en Windows 7, vea <a href="https://go.microsoft.com/fwlink/p/?linkid=220898">Cifrado de unidades BitLocker en Windows 7: Preguntas más frecuentes</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Bloqueo de mensajes del servidor (SMB) 3.0</p></td>
<td><p>El protocolo de Bloqueo de mensajes del servidor (SMB) es un protocolo de uso compartido de archivos de red (además de TCP/IP u otros protocoles de red) que permite a las aplicaciones de un PC acceder a archivos y recursos en un servidor remoto. También permite a las aplicaciones comunicarse con cualquier programa servidor configurado para recibir una solicitud de cliente SMB. Windows Server 2012 presenta la nueva versión 3.0 del protocolo SMB con las siguientes características:</p>
<ul>
<li><p>Conmutación por error transparente de SMB</p></li>
<li><p>Escalabilidad horizontal de SMB</p></li>
<li><p>Multicanal de SMB</p></li>
<li><p>Directo de SMB</p></li>
<li><p>Cifrado de SMB</p></li>
<li><p>VSS para recursos compartidos de archivos de SMB</p></li>
<li><p>Leasing de directorios de SMB</p></li>
<li><p>SMB PowerShell</p></li>
</ul></td>
<td><p>Compatibilidad limitada. El escenario compatible es una implementación virtualizada de hardware donde los discos se hospedan en VHD en un recurso compartido SMB 3.0. Estos VHD se presentan en el host a través de un hipervisor. Para obtener más información, vea <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualización de Exchange 2013</a>.</p></td>
<td><p>Compatibilidad limitada. El escenario compatible es una implementación virtualizada de hardware donde los discos se hospedan en VHD en un recurso compartido SMB 3.0. Estos VHD se presentan en el host a través de un hipervisor. Para obtener más información, vea <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualización de Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Espacios de almacenamiento</p></td>
<td><p>Espacios de almacenamiento es una nueva solución de almacenamiento que ofrece capacidades de virtualización para Windows Server 2012. Permite organizar discos físicos en grupos de almacenamiento, que se pueden expandir fácilmente agregando discos. Estos discos se pueden conectar por USB, SATA o SAS. También usa discos virtuales (espacios), que se comportan como discos físicos, con potentes capacidades asociadas, como el aprovisionamiento fino y la resistencia a los errores de los medios físicos subyacentes. Para más información sobre los espacios de almacenamiento, vea <a href="https://technet.microsoft.com/es-es/library/hh831739.aspx">Introducción a los espacios de almacenamiento</a>.</p></td>
<td><p>Se admite. Las mismas restricciones que para los tipos de discos físicos descritas en este tema.</p></td>
<td><p>Se admite. Las mismas restricciones que para los tipos de discos físicos descritas en este tema.</p></td>
</tr>
<tr class="odd">
<td><p>Sistema de archivos resistente (ReFS)</p></td>
<td><p>ReFS es un sistema de archivos recién diseñado para Windows Server 2012 que se ha creado basándose en NTFS. ReFS tiene un alto nivel de compatibilidad con NTFS y ofrece técnicas mejoradas de comprobación de datos y de autocorrección, así como una resistencia a daños integrada de un extremo a otro, especialmente cuando se usa con la característica de espacios de almacenamiento. Para más información sobre ReFS, vea <a href="https://technet.microsoft.com/es-es/library/hh831724.aspx">Información general del Sistema de archivos resistente</a>.</p></td>
<td><p>Compatibilidad con volúmenes que contienen archivos de bases de datos de Exchange, archivos de registro y archivos de indexación de contenido. Si está realizando la implementación en Windows Server 2012, asegúrese de que están instaladas las revisiones siguientes en Windows Server 2012:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Paquete acumulativo de actualizaciones de Windows 8 y Windows Server 2012: abril de 2013</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">El Servicio de disco virtual o las aplicaciones que usan el Servicio de disco virtual se bloquean o se inmovilizan en Windows Server 2012</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">El equipo basado en Windows 8 o en Windows Server 2012 se inmoviliza cuando se ejecuta el comando 'dir' en un volumen ReFS</a></p></li>
</ul>
<p>ReFS no es compatible con volúmenes OS.</p>
<p>Procedimiento recomendado: Las características de integridad de datos se deben deshabilitar en los archivos de base de datos de Exchange (.edb) o en el volumen que hospeda estos archivos.</p></td>
<td><p>Compatibilidad con volúmenes que contienen archivos de bases de datos de Exchange, archivos de registro y archivos de indexación de contenido. Si está realizando la implementación en Windows Server 2012, asegúrese de que están instaladas las revisiones siguientes en Windows Server 2012:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Paquete acumulativo de actualizaciones de Windows 8 y Windows Server 2012: abril de 2013</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">El Servicio de disco virtual o las aplicaciones que usan el Servicio de disco virtual se bloquean o se inmovilizan en Windows Server 2012</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">El equipo basado en Windows 8 o en Windows Server 2012 se inmoviliza cuando se ejecuta el comando 'dir' en un volumen ReFS</a></p></li>
</ul>
<p>ReFS no es compatible con volúmenes OS.</p>
<p>Procedimiento recomendado: Las características de integridad de datos se deben deshabilitar en los archivos de base de datos de Exchange (.edb) o en el volumen que hospeda estos archivos.</p></td>
</tr>
<tr class="even">
<td><p>Desduplicación de datos</p></td>
<td><p>La desduplicación de datos es una técnica nueva que optimiza el uso del almacenamiento en Windows Server 2012. Se trata de un método para buscar y quitar duplicaciones dentro de los datos sin poner en riesgo su fidelidad ni su integridad. El objetivo es almacenar más datos en menos espacio segmentando archivos en pequeños fragmentos de tamaño variable, identificando fragmentos duplicados y manteniendo una copia única de cada fragmento. Las copias redundantes del fragmento se cambian por una referencia a la copia única, los fragmentos se organizan en archivos de contenedor y los contenedores se comprimen para optimizar más el espacio.</p></td>
<td><p>No admitido para archivos de bases de datos de Exchange. Nota: se puede usar para archivos de bases de datos de Exchange que estén completamente sin conexión (usados como copias de seguridad o archivos).</p></td>
<td><p>No admitido para archivos de bases de datos de Exchange. Nota: se puede usar para archivos de bases de datos de Exchange que estén completamente sin conexión (usados como copias de seguridad o archivos).</p></td>
</tr>
</tbody>
</table>


Arquitecturas de almacenamiento

