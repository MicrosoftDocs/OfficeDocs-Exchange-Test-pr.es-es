---
title: 'Directiva de retención predeterminada en Exchange Online y Exchange Server'
TOCTitle: Directiva de retención predeterminada
ms:assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn775046(v=EXCHG.150)
ms:contentKeyID: 62625607
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Directiva de retención predeterminada en Exchange Online y Exchange Server

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Exchange crea la directiva de retención Directiva de MRM predeterminada en la organización de Exchange Online y Exchange local. La directiva se aplica automáticamente a los nuevos usuarios de Exchange Online. En organizaciones locales, la directiva se aplica cuando se crea un archivo para el buzón. Puede cambiar la directiva de retención aplicada a un usuario en cualquier momento.

Puede modificar las etiquetas incluidas en la Directiva de MRM predeterminada, por ejemplo cambiando la antigüedad de la retención o las acciones de la retención, o bien puede deshabilitar una etiqueta o modificar la directiva agregando o quitando etiquetas de esta. La directiva actualizada se aplica a los buzones la próxima vez que el Asistente para carpeta administrada las procesa.

## Etiquetas de retención vinculadas a la Directiva de MRM predeterminada

La siguiente tabla enumera las etiquetas de retención predeterminadas vinculadas a la directiva de MRM predeterminada.


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
<th>Tipo</th>
<th>Antigüedad de retención (días)</th>
<th>Acción de retención</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mover al archivo después de 2 años de forma predeterminada</p></td>
<td><p>Etiqueta de directiva predeterminada (DPT)</p></td>
<td><p>730</p></td>
<td><p>Mover a archivo</p></td>
</tr>
<tr class="even">
<td><p>Mover elementos recuperables a archivo después de 14 días</p></td>
<td><p>Carpeta Elementos recuperables</p></td>
<td><p>14</p></td>
<td><p>Mover a archivo</p></td>
</tr>
<tr class="odd">
<td><p>Mover al archivo después de 1 años en forma personal</p></td>
<td><p>Etiqueta personal</p></td>
<td><p>365</p></td>
<td><p>Mover a archivo</p></td>
</tr>
<tr class="even">
<td><p>Mover al archivo después de 5 años en forma personal</p></td>
<td><p>Etiqueta personal</p></td>
<td><p>1.825</p></td>
<td><p>Mover a archivo</p></td>
</tr>
<tr class="odd">
<td><p>Nunca mover al archivo en forma personal</p></td>
<td><p>Etiqueta personal</p></td>
<td><p>No aplicable</p></td>
<td><p>Mover a archivo</p></td>
</tr>
<tr class="even">
<td><p>Eliminar después de una semana</p></td>
<td><p>Etiqueta personal</p></td>
<td><p>7</p></td>
<td><p>Eliminar y permitir recuperación</p></td>
</tr>
<tr class="odd">
<td><p>Eliminar después de un mes</p></td>
<td><p>Etiqueta personal</p></td>
<td><p>30</p></td>
<td><p>Eliminar y permitir recuperación</p></td>
</tr>
<tr class="even">
<td><p>Eliminar después de seis meses</p></td>
<td><p>Etiqueta personal</p></td>
<td><p>180</p></td>
<td><p>Eliminar y permitir recuperación</p></td>
</tr>
<tr class="odd">
<td><p>Eliminar después de un año</p></td>
<td><p>Etiqueta personal</p></td>
<td><p>365</p></td>
<td><p>Eliminar y permitir recuperación</p></td>
</tr>
<tr class="even">
<td><p>Eliminar después de cinco años</p></td>
<td><p>Etiqueta personal</p></td>
<td><p>1.825</p></td>
<td><p>Eliminar y permitir recuperación</p></td>
</tr>
<tr class="odd">
<td><p>No eliminar nunca</p></td>
<td><p>Etiqueta personal</p></td>
<td><p>No aplicable</p></td>
<td><p>Eliminar y permitir recuperación</p></td>
</tr>
</tbody>
</table>


## Qué se puede hacer con la Directiva de MRM predeterminada


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Se puede...</th>
<th>En Exchange Online…</th>
<th>En Exchange Server…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aplicar la Directiva de MRM predeterminada automáticamente a los nuevos usuarios</p></td>
<td><p>Sí, se aplica de manera predeterminada. No se requiere ninguna acción.</p></td>
<td><p>Sí, se aplica de manera predeterminada si también se crea un archivo para el nuevo usuario.</p>
<p>Si crea un archivo para el usuario más adelante, la directiva se aplica automáticamente solo si el usuario no tiene una directiva de retención existente.</p></td>
</tr>
<tr class="even">
<td><p>Modificar la antigüedad de retención o acción de retención de una etiqueta de retención vinculada a la directiva</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Deshabilitar una etiqueta de retención vinculada a la directiva</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Agregar una etiqueta de retención a la directiva</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Quitar una etiqueta de retención de la directiva</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Establecer otra directiva como directiva de retención predeterminada para que se aplique automáticamente a los nuevos usuarios</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Más información

  - Una etiqueta de retención se puede vincular a más de una directiva de retención. Para obtener más detalles acerca de la administración de [Etiquetas de retención y directivas de retención](retention-tags-and-retention-policies-exchange-2013-help.md), vea [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

  - La directiva de MRM predeterminada no incluye una DPT para eliminar elementos de forma automática, pero contiene etiquetas personales con la acción para eliminar retenciones que los usuarios pueden aplicar a los elementos del buzón. Si desea eliminar los elementos automáticamente tras un período especificado, puede crear una DPT con la acción de eliminación necesaria y agregarla a la directiva. Para obtener información detallada, vea [Crear directivas de retención](create-a-retention-policy-exchange-2013-help.md) y [Agregar etiquetas de retención o quitar etiquetas de retención de una directiva de retención](add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md).

  - Las directivas de retención se aplican a los usuarios de buzones. La misma directiva se aplica a los buzones de correo y al archivo del usuario.

