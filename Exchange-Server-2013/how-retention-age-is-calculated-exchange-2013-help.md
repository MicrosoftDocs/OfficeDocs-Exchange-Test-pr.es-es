---
title: 'Cómo calcular la antigüedad de retención: Exchange 2013 Help'
TOCTitle: Cómo calcular la antigüedad de retención
ms:assetid: a7daf7aa-0411-4b26-a422-eefd1b113f9f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb430780(v=EXCHG.150)
ms:contentKeyID: 49895819
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cómo calcular la antigüedad de retención

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-07-27_

El Asistente para carpeta administrada (MFA) es uno de los muchos procesos del *asistente de buzón* que se ejecutan en los servidores de buzones de correo. Su trabajo consiste en procesar buzones a los que se ha aplicado una directiva de retención, agregar las etiquetas de retención incluidas en la directiva para el buzón y procesar los elementos en el buzón. Si los elementos tienen una etiqueta de retención, el asistente comprueba la antigüedad de esos elementos. Si un elemento ha superado su *antigüedad de retención*, realiza la *acción de retención* especificada. Entre las acciones de retención se incluye mover un elemento al archivo del usuario, eliminar el elemento y permitir su recuperación o eliminar el elemento de forma permanente.

Vea [Etiquetas de retención y directivas de retención](retention-tags-and-retention-policies-exchange-2013-help.md) para obtener más información.

## Determinación de la antigüedad de diferentes tipos de elementos

La antigüedad de retención de los elementos de buzón se calcula a partir de la fecha de entrega o de la fecha de creación de los elementos como borradores que no se entregan pero que el usuario crea. Cuando el Asistente para carpeta administrada procesa los elementos de un buzón de correo, coloca una fecha de inicio y una fecha de expiración en todos los elementos que poseen etiquetas de retención con las acciones de retención **Eliminar y permitir la recuperación** o **Eliminar permanentemente**. En los elementos que poseen una etiqueta de archivo también se estampa una fecha de movimiento.

Los elementos en la carpeta Elementos eliminados y los elementos que puedan tener una fecha de inicio y finalización, como los elementos de calendario (reuniones y citas) y las tareas, se administran de forma distinta tal como se muestra en esta tabla.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Si el tipo de elemento es...</th>
<th>Y el elemento es...</th>
<th>La antigüedad de retención se calcula según...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Mensaje de correo electrónico</p></li>
<li><p>Documento</p></li>
<li><p>Fax</p></li>
<li><p>Elemento del diario</p></li>
<li><p>Convocatoria de reunión, respuesta o cancelación</p></li>
<li><p>Llamada perdida</p></li>
</ul></td>
<td><p>Elemento que no está en la carpeta Elementos eliminados</p></td>
<td><p>Fecha de entrega o fecha de creación</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>Mensaje de correo electrónico</p></li>
<li><p>Documento</p></li>
<li><p>Fax</p></li>
<li><p>Elemento del diario</p></li>
<li><p>Convocatoria de reunión, respuesta o cancelación</p></li>
<li><p>Llamada perdida</p></li>
</ul></td>
<td><p>Elemento en la carpeta Elementos eliminados</p></td>
<td><ul>
<li><p>Fecha de entrega o de creación, a menos que el elemento se haya eliminado de una carpeta que no tenga una etiqueta de retención heredada o implícita.</p></li>
<li><p>Si un elemento está en una carpeta que no tiene aplicada una etiqueta de retención heredada o implícita, el MFA no procesa el elemento y, por lo tanto, no marca en él una fecha de inicio. Cuando el usuario elimina un elemento de este tipo y el MFA lo procesa por primera vez en la carpeta Elementos eliminados, marca la fecha actual como fecha de inicio.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Calendario</p></td>
<td><p>Elemento que no está en la carpeta Elementos eliminados</p></td>
<td><ul>
<li><p>Los elementos de calendario no periódicos expiran según su fecha de finalización.</p></li>
<li><p>Los elementos de calendario periódicos expiran según la fecha de finalización en que sucedió por última vez. Los elementos de calendario recurrentes sin una fecha de finalización no expiran.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Calendario</p></td>
<td><p>Elemento en la carpeta Elementos eliminados</p></td>
<td><ol>
<li><p>Un elemento de calendario expira según su <code>message-received date</code>, si es que la tiene.</p></li>
<li><p>Si un elemento de calendario no tiene una <code>message-received date</code>, dicho elemento expirará según su <code>message-creation date</code>.</p></li>
<li><p>Si un elemento de calendario no tiene una <code>message-received date</code> ni <code>message-creation date</code>, dicho elemento no expirará.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Tarea</p></td>
<td><p>Elemento que no está en la carpeta Elementos eliminados</p></td>
<td><ul>
<li><p>Tareas no repetidas:</p>
<ol>
<li><p>Una tarea no repetida expira según su <code>message-received date</code>, si es que la tiene.</p></li>
<li><p>Si una tarea no recurrente no tiene una <code>message-received date</code>, dicha tarea expirará según su <code>message-creation date</code>.</p></li>
<li><p>Si una tarea no recurrente no tiene una <code>message-received date</code> ni una<code></code><code>message-creation date</code>, dicha tarea no expirará.</p></li>
</ol></li>
<li><p>Una tarea recurrente expira según la <code>end date</code> en que ocurrió por última vez. Si una tarea recurrente no tiene una <code>end date</code>, dicha tarea no expirará.</p></li>
<li><p>Una tarea regenerada (es decir, una tarea recurrente que se regenera un tiempo especificado después de que finaliza la instancia anterior de la tarea) no expira.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tarea</p></td>
<td><p>Elemento en la carpeta Elementos eliminados</p></td>
<td><ol>
<li><p>Una tarea expira según su <code>message-received date</code>, si es que la tiene.</p></li>
<li><p>Si una tarea no tiene una <code>message-received date</code>, dicha tarea expirará según su <code>message-creation date</code>.</p></li>
<li><p>Si una tarea no tiene una <code>message-received date</code> ni una <code>message-creation date</code>, dicha tarea no expirará.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Contacto</p></td>
<td><p>En cualquier carpeta</p></td>
<td><p>Los contactos no se marcan con una fecha de inicio o de expiración, por lo que el Asistente para carpeta administrada los omite y estos no expiran.</p></td>
</tr>
<tr class="even">
<td><p>Dañado</p></td>
<td><p>En cualquier carpeta</p></td>
<td><p>El Asistente para carpeta administrada omite los elementos dañados y estos no expiran.</p></td>
</tr>
</tbody>
</table>


## Ejemplos


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Si el usuario...</th>
<th>Las etiquetas de retención de la carpeta...</th>
<th>El Asistente para carpeta administrada...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li><p>Recibe un mensaje en la Bandeja de entrada el 26.01.13.</p></li>
<li><p>Elimina el mensaje el 27.02.13.</p></li>
</ol>
<p></p></td>
<td><ul>
<li><p>Bandeja de entrada: Eliminar en 365 días</p></li>
<li><p>Elementos eliminados: Eliminar en 30 días</p></li>
</ul>
<p></p></td>
<td><ol>
<li><p>Procesa el mensaje en la Bandeja de entrada el 26.01.13, lo marca con una <em>fecha de inicio</em> del 26.01.13 y una <em>fecha de expiración</em> del 26.01.14.</p></li>
<li><p>Procesa el mensaje de nuevo en la carpeta Elementos eliminados el 27.02.13. Vuelve a calcular la fecha de expiración con base en la misma fecha de inicio (26.01.13).</p></li>
<li><p>Debido a que la antigüedad del elemento es superior a 30 días, expira inmediatamente.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Recibe un mensaje en la Bandeja de entrada el 26.01.13.</p></li>
<li><p>Elimina el mensaje el 27.02.13.</p></li>
</ol></td>
<td><ul>
<li><p>Bandeja de entrada: Ninguno (heredado o implícito)</p></li>
<li><p>Elementos eliminados: Eliminar en 30 días</p></li>
</ul></td>
<td><ol>
<li><p>Procesa el mensaje en la carpeta Elementos eliminados el 27.02.13 y determina que el elemento no tiene una fecha de inicio. Marca la fecha actual como la fecha de inicio y el 27.03.13 como la fecha de expiración.</p></li>
<li><p>El elemento expira el 27.03.13, 30 días después de que el usuario lo eliminara o moviera a la carpeta Elementos eliminados.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## Más información

  - En Exchange Online, el Asistente para carpeta administrada procesa un buzón una vez cada siete días. Esto puede provocar que los elementos expiren hasta siete días después de la fecha de expiración que se ha marcado en el elemento.

  - Los elementos de los buzones que se colocan en suspensión de retención no se procesan mediante el Asistente para carpeta administrada hasta que la suspensión se quita.

  - Si un buzón se coloca en Conservación local o en Retención por juicio, los elementos que expiran se eliminan de la Bandeja de entrada pero se conservan en la carpeta Elementos recuperables hasta que el buzón se elimina de [Conservación local y retención por juicio](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - En implementaciones híbridas, las mismas etiquetas de retención y directivas de retención deben existir en las organizaciones locales y de Exchange Online para poder mover y hacer expirar elementos de forma coherente en ambas organizaciones. Vea [Exportar e importar etiquetas de retención](export-and-import-retention-tags-exchange-2013-help.md) para obtener más información.

