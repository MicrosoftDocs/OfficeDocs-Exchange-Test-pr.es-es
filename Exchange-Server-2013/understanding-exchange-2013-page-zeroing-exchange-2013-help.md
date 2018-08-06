---
title: 'Descripción del llenado con ceros de páginas Exchange 2013: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Descripción del llenado con ceros de las páginas de Exchange 2013
ms:assetid: 0ca7b188-efbc-4c0d-bcfe-5138cffc803c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg549096(v=EXCHG.150)
ms:contentKeyID: 61612642
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción del llenado con ceros de las páginas de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

## Llenado con ceros de las páginas en Exchange 2013

El *llenado con ceros* es un mecanismo de seguridad que escribe ceros o un patrón binario sobre los datos eliminados de modo que sea más difícil recuperar estos datos. En Exchange Server 2013, una base de datos de ESE usa *páginas* como su unidad de almacenamiento y, por ende, implementa el *llenado con ceros de las páginas*. El llenado con ceros de las páginas está habilitado de forma predeterminada y no se puede deshabilitar. Las operaciones de llenado con ceros de páginas se graban en los archivos de registro de transacciones de modo que todas las copias de la base de datos se llenen con ceros de la misma manera. El llenado con ceros de las páginas en una base de datos activa provoca que la página se llene de ceros en una copia pasiva de la base de datos.


> [!NOTE]
> No hay ningún mecanismo para que el Motor de abastecimiento extensible (ESE) clasifique por orden de prioridad la reutilización de las páginas con ceros al asignar un nuevo espacio. Las tablas que tienen espacio secuencial asignado omitirán de manera intencional las páginas con ceros o fragmentadas en favor del uso de páginas nuevas o secuenciales. Este enfoque reduce la IOPs de la base de datos.



En Exchange 2013 el llenado con ceros de las páginas reduce el impacto en el rendimiento de los servidores cuando se realizan funciones de llenado con ceros. Esto incluye:

  - **Capacidad de almacenamiento y red optimizados**   ESE escribe un registro de llenado con ceros de páginas en el archivo del registro de transacciones en lugar de registrar la imagen de la página completa. Este enfoque reduce la E/S de escritura del registro y reduce los requisitos de ancho de banda para enviar los archivos del registro.

  - **E/S de disco optimizada de la base de datos**   En Exchange 2010 RTM y versiones anteriores el llenado con ceros de páginas se producía solamente durante un proceso de mantenimiento programado o de copia de seguridad, y causaba una importante E/S de disco de base de datos. En Exchange 2010 SP1 y versiones posteriores (incluido Exchange 2013), el llenado con ceros de las páginas se realiza de forma predeterminada y en el momento de la transacción. En la mayoría de los casos, el llenado con ceros se produce de inmediato después de la eliminación permanente. Este diseño permite que la base de datos aproveche la capacidad de profundidad de punto de control del motor, lo que garantiza que las páginas desfasadas permanezcan en la memoria caché de la base de datos por un determinado plazo de tiempo de modo que las actualizaciones adicionales en la página que se produzcan en una proximidad cercana de tiempo no provoquen una E/S adicional de escritura de la base de datos. Debido a este diseño, el llenado con ceros de las páginas no tiene un impacto significativo en la E/S de la base de datos, por lo que está habilitado de forma predeterminada.

## Implementación de llenado con ceros de páginas en la base de datos de ESE

El llenado con ceros de las páginas escribe un patrón binario sobre un registro eliminado de forma permanente. El patrón de llenado con ceros de las páginas es específico para la operación del motor de ESE y es diferente para las operaciones de tiempo de ejecución y las operaciones de mantenimiento. La siguiente tabla muestra una lista de las tramas de relleno que corresponden a operaciones de tiempo de ejecución específicas.

### Trama de relleno de llenado con ceros de las páginas de tiempo de ejecución de ESE

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Operación de tiempo de ejecución de ESE</th>
<th>Trama de relleno</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Reemplazar</p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p>Eliminación de valor de registro/largo</p></td>
<td><p>D</p></td>
</tr>
<tr class="odd">
<td><p>Espacio de página liberado</p></td>
<td><p>H</p></td>
</tr>
</tbody>
</table>


La siguiente tabla muestra una lista de las tramas de relleno que corresponden a operaciones específicas que ocurren durante el mantenimiento de la base de datos de ESE en segundo plano.

### Trama de relleno de llenado con ceros de las páginas durante el mantenimiento de las bases de datos de ESE en segundo plano

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Operación de mantenimiento de base de datos de ESE en segundo plano</th>
<th>Trama de relleno</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Eliminación de registro</p></td>
<td><p>D</p></td>
</tr>
<tr class="even">
<td><p>Eliminación de valor largo</p></td>
<td><p>L</p></td>
</tr>
<tr class="odd">
<td><p>Espacio de página liberado de página parcialmente usada</p></td>
<td><p>Z</p></td>
</tr>
<tr class="even">
<td><p>Espacio de página liberado de página no utilizada</p></td>
<td><p>U</p></td>
</tr>
</tbody>
</table>


## Mantenimiento de base de datos en segundo plano

El mantenimiento de bases de datos en segundo plano es un proceso que realiza continuamente sumas de comprobación y exámenes en cada base de datos. Su función principal es realizar la suma de comprobación de las páginas de la base de datos, pero también controlar la limpieza de los espacios y el llenado con ceros de los registros y las páginas que no se llenaron con ceros debido a un bloqueo de almacenamiento. El mantenimiento de bases de datos en segundo plano procesa aproximadamente 1 MB por segundo por base de datos. Si el llenado con ceros es una prioridad, puede reducir los tamaños de las bases de datos para garantizar que el llenado con ceros de las páginas se realice para los casos de recuperación de bloqueos en un período de tiempo más corto (por ejemplo, 24 horas).

El mantenimiento de base de datos en segundo plano es un proceso continuo, de modo que no hay eventos asociados con su inicio y finalización. Puede realizar un seguimiento del progreso del mantenimiento de las bases de datos en segundo plano al leer el valor de un contador de rendimiento:

  - Base de datos de MSExchange -\>Instancias -\>Duración de mantenimiento de base de datos

Este contador indica la cantidad de segundos que han pasado desde que se completó el mantenimiento para una base determinada por última vez.

## Proceso de llenado con ceros página de base de datos de ESE

La siguiente tabla analiza los escenarios de eliminación de bases de datos y cuándo se produce el llenado con ceros de páginas.

### Mantenimiento de bases de datos en segundo plano de ESE

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Escenario de eliminación de bases de datos</th>
<th>Proceso de ESE y datos de base de datos de período de tiempo a cero</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Escenario 1: La recuperación de un único elemento está deshabilitada y el usuario purga el elemento de la carpeta de elementos recuperables.</p></li>
<li><p>Escenario 2: La recuperación de un único elemento está deshabilitada y el período de retenciónde Elementos recuperables está configurado en cero.</p></li>
<li><p>Escenario 3: La recuperación de un único elemento está habilitada y el elemento expira sobre la base del período de retención del elemento eliminado.</p></li>
</ul></td>
<td><p>Un subproceso asincrónico escribe un patrón binario sobre los datos eliminados. Esta acción se produce en milisegundos durante la eliminación de registro. Si el proceso del almacén se bloquea cuando el trabajo de llenado con ceros asincrónico aún está pendiente (o se cancela la limpieza de almacenamiento de la versión debido al crecimiento del almacén), el llenado con ceros se completa cuando el mantenimiento de bases de datos en segundo plano procesa esa sección de la base de datos.</p></td>
</tr>
<tr class="even">
<td><p>Ver el escenario: Expiración de elementos de la vista de carpeta de Outlook/Outlook Web App (por ejemplo, vista de conversaciones).</p></td>
<td><p>El llenado con ceros de datos se produce cuando el mantenimiento de la base de datos en segundo plano procesa esa sección de la base de datos.</p></td>
</tr>
<tr class="odd">
<td><p>Mover el buzón o eliminar el escenario del buzón: Buzón de correo de origen eliminado (expiración del buzón de correo eliminado de recuperación del elemento eliminado)</p></td>
<td><p>El llenado con ceros de datos se produce cuando el mantenimiento de la base de datos en segundo plano procesa esa sección de la base de datos.</p></td>
</tr>
</tbody>
</table>


## Supervisión de comportamiento de llenado con ceros de página

Puede medir y supervisar la funcionalidad de llenado con ceros de las páginas mediante dos contadores de ESE:

  - Páginas de base de datos de MSExchange-\>Páginas de mantenimiento de bases de datos llenadas con ceros: indica la cantidad de páginas que llenó con ceros el motor de la base de datos desde que se invocó el contador de rendimiento.

  - Base de datos de MSExchange-\>Páginas de mantenimiento de bases de datos llenadas con ceros por segundo: indica la tasa en la que se llenaron con ceros las páginas.


> [!NOTE]
> Para más información sobre cómo habilitar estos contadores, vea <A href="https://go.microsoft.com/fwlink/?linkid=101194">Cómo habilitar contadores de rendimiento ESE extendidos</A>.



El llenado con ceros de páginas es una función de mantenimiento de la base de datos, de modo que la información de rendimiento relacionada tanto con el llenado con ceros de página para las transacciones de tiempo de ejecución como con el llenado con ceros de página debido al mantenimiento de la base de datos en segundo plano se incluye en estos contadores.

## Tipos de datos de buzones de correo sin llenado con ceros de las páginas

Los siguientes tipos de datos de buzones de correo no tienen ninguna disposición sobre el llenado con ceros de las páginas:

  - Registros de transacciones de base de datos de buzones de correo (.log)
    
    Cuando se eliminan los registros de transacciones (debido a un truncamiento mediante copia de seguridad o registro circular), no hay ningún proceso para llenar con ceros los bloques en el sistema de archivos NTFS que almacenaba los archivos del registro eliminados. Es posible que NTFS reutilice nuevamente ese espacio libre para nuevos registros creados, pero no hay garantía de que esto ocurrirá.

  - Archivos de catálogo de índice de contenido
    
    Exchange 2013 usa Search Foundation para la funcionalidad de indexación de búsqueda. El catálogo del índice de búsqueda está compuesto por varias docenas de archivos almacenados en el mismo volumen que el archivo de base de datos del buzón de correo. Cuando se elimina de forma permanente un mensaje de la base de datos del buzón de correo, el contenido asociado al catálogo de búsqueda no se elimina de inmediato. La eliminación del contenido se produce cuando Search Foundation hace una sombra, o combinación maestra, de varios archivos de catálogo pequeños en un único archivo mayor. Una vez finalizada la combinación maestra, se eliminan los archivos de catálogo más pequeños. No hay ningún proceso para llenar con ceros los bloques que almacenaban los archivos de catálogo eliminados.

