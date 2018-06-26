---
title: 'Carpetas predeterminadas que admiten etiquetas de la directiva de retención: Exchange 2013 Help'
TOCTitle: Carpetas predeterminadas que admiten etiquetas de la directiva de retención
ms:assetid: d2e2064f-4102-4018-b688-504d09da6d39
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn783294(v=EXCHG.150)
ms:contentKeyID: 62835918
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Carpetas predeterminadas que admiten etiquetas de la directiva de retención

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-04-20_

Puede usar [Etiquetas de retención y directivas de retención](retention-tags-and-retention-policies-exchange-2013-help.md) para administrar el ciclo de vida de los correos electrónicos. Las políticas de retención contienen etiquetas de retención, que es la configuración que se puede usar para especificar cuándo se debe mover un mensaje automáticamente al archivo o cuándo se debe eliminar.

Una etiqueta de la directiva de retención (RPT) es un tipo de etiqueta de retención que se puede aplicar a las carpetas predeterminadas en un buzón de correo, como **Bandeja de entrada** y **Elementos eliminados**.

![Crear una etiqueta de política de retención (RPT)](images/Dn783294.b59a96fd-94e1-4c9b-bff6-97a1bd98dfe7(EXCHG.150).png "Crear una etiqueta de política de retención (RPT)")

## Carpetas predeterminadas compatibles

Puede crear RPT para las carpetas predeterminadas de la siguiente tabla.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de la carpeta</th>
<th>Detalles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Archivar</p></td>
<td><p>Esta carpeta es el destino predeterminado de los mensajes archivados con el botón Archivar de Outlook. La característica Archivar proporciona una forma rápida para que los usuarios quiten los mensajes de su bandeja de entrada sin eliminarlos.</p>
<p>Este RPT solo está disponible en Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p>Calendario</p></td>
<td><p>Esta carpeta predeterminada se usa para almacenar citas y reuniones.</p></td>
</tr>
<tr class="odd">
<td><p>Otros correos</p></td>
<td><p>Esta carpeta contiene mensajes de correo electrónico que tienen una prioridad baja. Desorden busca sus acciones anteriores para determinar los mensajes que es posible que ignore. A continuación, mueve los mensajes a la carpeta <strong>Desorden</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Historial de conversación</p></td>
<td><p>Microsoft Lync (anteriormente Microsoft Office Communicator) crea esta carpeta. Si bien Outlook no la considera una carpeta predeterminada, Exchange la considera una carpeta especial y por lo tanto se le pueden aplicar RPT.</p></td>
</tr>
<tr class="odd">
<td><p>Elementos eliminados</p></td>
<td><p>Esta carpeta predeterminada se usa para almacenar elementos eliminados de otras carpetas en buzón de correo. Los usuarios de Outlook y Outlook Web App pueden vaciar manualmente esta carpeta. Los usuarios también pueden configurar Outlook para vaciar la carpeta al momento de cerrar Outlook.</p></td>
</tr>
<tr class="even">
<td><p>Borradores</p></td>
<td><p>Esta carpeta predeterminada se usa para almacenar borradores que el usuario no envió. Outlook Web App también usa esta carpeta para guardar mensajes enviados por el usuario, pero que no se entregaron al servidor Transporte de concentradores.</p></td>
</tr>
<tr class="odd">
<td><p>Bandeja de entrada</p></td>
<td><p>Esta carpeta predeterminada se usa para almacenar los mensajes entregados a un buzón de correo.</p></td>
</tr>
<tr class="even">
<td><p>Diario</p></td>
<td><p>Esta carpeta predeterminada contiene acciones seleccionadas por el usuario. Outlook registra automáticamente estas acciones y las coloca en una vista de escala de tiempo.</p></td>
</tr>
<tr class="odd">
<td><p>Correo no deseado</p></td>
<td><p>Esta carpeta predeterminada se usa para guardar los mensajes que el filtro de contenido de un servidor de Exchange o el filtro contra correo no deseado de Outlook marcan como correo no deseado.</p></td>
</tr>
<tr class="even">
<td><p>Notas</p></td>
<td><p>Esta carpeta contiene notas creadas por los usuarios de Outlook. Las notas también están visibles en Outlook Web App.</p></td>
</tr>
<tr class="odd">
<td><p>Bandeja de salida</p></td>
<td><p>Esta carpeta predeterminada se usa para almacenar temporalmente mensajes enviados por el usuario hasta que se los entrega al servidor Transporte de concentradores. Se guarda una copia de los mensajes enviados en la carpeta predeterminada Elementos enviados. Dado que los mensajes en general permanecen en esta carpeta por un período breve, no es necesario crear una RPT para esta carpeta.</p></td>
</tr>
<tr class="even">
<td><p>Fuentes RSS</p></td>
<td><p>Esta carpeta predeterminada contiene fuentes RSS.</p></td>
</tr>
<tr class="odd">
<td><p>Elementos recuperables</p></td>
<td><p>Se trata de una carpeta oculta en el subárbol no relacionado con IPM. Contiene las subcarpetas Eliminaciones, Versiones, Purgas, Retenciones de detección y Auditorías. Las etiquetas de retención de esta carpeta mueven elementos de la carpeta Elementos recuperables del buzón de correo principal del usuario a la carpeta Elementos recuperables del buzón de archivo del usuario. Solo puede asignar la acción de retención <strong>Mover a archivo</strong> a etiquetas de esta carpeta. Para obtener más información, vea <a href="recoverable-items-folder-exchange-2013-help.md">Carpeta Elementos recuperables</a>.</p></td>
</tr>
<tr class="even">
<td><p>Elementos enviados</p></td>
<td><p>Esta carpeta predeterminada se usa para almacenar mensajes que se entregaron a un servidor Transporte de concentradores.</p></td>
</tr>
<tr class="odd">
<td><p>Problemas de sincronización</p></td>
<td><p>Esta carpeta contiene los registros de sincronización. Para obtener más información, vea <a href="https://go.microsoft.com/fwlink/p/?linkid=198215">Carpetas de errores de sincronización</a>.</p></td>
</tr>
<tr class="even">
<td><p>Tareas</p></td>
<td><p>Esta carpeta predeterminada se usa para almacenar tareas. Para crear una etiqueta de directiva de retención (RPT) para la carpeta Tareas, debe usar Shell de administración de Exchange. Para obtener más información, consulte <a href="https://technet.microsoft.com/es-es/library/dd335226(v=exchg.150)">New-RetentionPolicyTag</a>. Una vez creada la etiqueta de directiva de retención para la carpeta Tareas, puede administrarla mediante el Centro de administración de Exchange.</p></td>
</tr>
</tbody>
</table>


## Más información

  - Las RPT son etiquetas de retención para las carpetas predeterminadas. Solo puede seleccionar una acción de eliminación para RPT o **eliminar y permitir la recuperación** o **eliminar permanentemente**.

  - No puede crear una RPT para mover mensajes al archivo. Para mover elementos antiguos al archivo, puede crear una *etiqueta de directiva predeterminada* (DPT), que se aplica al buzón completo, o *etiquetas personales*, que se muestran en Outlook y Outlook Web App (OWA) como directivas de archivo. Los usuarios pueden aplicarlas a las carpetas o los mensajes individuales.

  - No puede aplicar RPT a la carpeta Contactos.

  - Solo puede agregar una RPT para una carpeta predeterminada particular a una directiva de retención. Por ejemplo, si una directiva de retención tiene una etiqueta aplicada en la Bandeja de entrada, no puede agregar otra RPT del tipo Bandeja de entrada a esa directiva de retención.

  - Para obtener más información sobre cómo crear RPT u otros tipos de etiquetas de retención y agregarlas a una directiva de retención, vea [Crear directivas de retención](create-a-retention-policy-exchange-2013-help.md).

  - En Exchange 2013 y Exchange Online, también se aplica una DPT a las carpetas predeterminadas **Calendario** y **Tareas**. Esto puede resultar en elementos que se eliminan o mueven al archivo basado en la configuración de DPT. Para evitar que la configuración de DPT elimine elementos en estas carpetas, cree RPT con la retención deshabilitada. Para evitar que la configuración de DPT mueva elementos en una carpeta predeterminada, puede crear una etiqueta personal deshabilitada con la acción de mover a archivo, agregarla a la directiva de retención y luego hacer que los usuarios la apliquen a la carpeta predeterminada. Para obtener detalles, vea [Evitar el archivado de elementos en una carpeta predeterminada en Exchange 2010](https://go.microsoft.com/fwlink/?linkid=511071).

