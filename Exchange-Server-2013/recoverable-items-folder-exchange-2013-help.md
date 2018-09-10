---
title: 'Carpeta Elementos recuperables: Exchange 2013 Help'
TOCTitle: Carpeta Elementos recuperables
ms:assetid: efc48fb4-2ed8-4d05-93af-f3505fbc389d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee364755(v=EXCHG.150)
ms:contentKeyID: 49896003
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Carpeta Elementos recuperables

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Para brindar protección contra la eliminación accidental o malintencionada y facilitar los esfuerzos de detección comúnmente realizados antes o durante litigios o investigaciones, Microsoft Exchange Server 2013 y Exchange Online usan la carpeta Elementos recuperables. Esta carpeta sustituye la característica conocida como *contenedor* en las versiones anteriores de Exchange. Las siguientes características de Exchange usan la carpeta Elementos recuperables:

  - Retención de elementos eliminados

  - Recuperación de elementos individuales

  - Retención en contexto

  - Retención por juicio

  - Registro de auditoría de buzones de correo

  - Registro de calendario

**Contenido**

Terminología

Carpeta Elementos recuperables

  - Retención de elementos eliminados

  - Recuperación de elementos individuales

  - Conservación local y retención por juicio

  - Protección de página de copia en escritura y elementos modificados

Cuotas del buzón de correo de elementos recuperables

## Terminología

El conocimiento de los siguientes términos lo ayudará a comprender el contenido en este tema.

  - **Eliminar**  
    Describe cuando se elimina un elemento de una carpeta y se coloca en la carpeta predeterminada Elementos eliminados.

<!-- end list -->

  - **Eliminar permanentemente**  
    Describe cuando se elimina un elemento de la carpeta Elementos eliminados y se coloca en la carpeta Elementos recuperables. Además, describe cuando un usuario Microsoft Outlook elimina un elemento presionando Shirt+Delete, que omite la carpeta Elementos eliminados y coloca el elemento directamente en la carpeta Elementos recuperables.

<!-- end list -->

  - **Purgado**  
    Describe si un elemento está marcado para ser eliminado de la base de datos de buzones de correo. Esta acción también se conoce como *eliminación de forma permanente*.

Volver al principio

## Carpeta Elementos recuperables

La carpeta Elementos recuperables reside en el subárbol que no es IPM de cada buzón. El subárbol que no es IPM es un área de almacenamiento dentro del buzón que contiene datos operativos sobre el buzón. Este subárbol no es visible para los usuarios que usan Outlook, Microsoft OfficeOutlook Web App u otros clientes de correo electrónico.

Este cambio de arquitectura proporciona los siguientes beneficios clave:

  - Cuando un buzón se mueve a otra base de datos de buzones de correo, la carpeta Elementos recuperables también se mueve a esa carpeta.

  - La carpeta Elementos recuperables es indizada por la búsqueda de Exchange y puede detectarse mediante la exhibición de documentos electrónicos local.

  - La carpeta Elementos recuperables tiene su propia cuota de almacenamiento.

  - Exchange puede evitar que los datos se purguen de la carpeta Elementos recuperables.

  - Exchange puede realizar un seguimiento de determinado contenido.

La carpeta Elementos recuperables contiene las siguientes subcarpetas:

  - **Eliminaciones**   Esta subcarpeta contiene todos los elementos eliminados de la carpeta Elementos eliminados. (En Outlook, un usuario puede eliminar un elemento de forma permanente presionando Mayús+Supr). Esta subcarpeta está expuesta a usuarios mediante la función Recuperar elementos eliminados en Outlook y Outlook Web App.

  - **Versiones**   Si está habilitada la conservación local o la retención por juicio, esta subcarpeta contiene las copias originales y modificadas de los elementos eliminados. Los usuarios finales no pueden ver esta carpeta.

  - **Purgas**   Si está habilitada la retención por juicio o la recuperación de elementos individuales, esta subcarpeta contiene todos los elementos que se purgan. Los usuarios finales no pueden ver esta carpeta.

  - **Auditorías**   Si el registro de la auditoría de buzones de correo no está habilitado para un buzón de correo, esta subcarpeta contiene las entradas de registro de auditoría. Para obtener más información acerca de los registros de auditoría de buzones de correo, vea [Registro de auditoría de buzones de correo](mailbox-audit-logging-exchange-2013-help.md).

  - **Retenciones de detección**   Si está habilitada la retención local, esta subcarpeta contiene todos los elementos que cumplen con los parámetros de consulta de retención y que se purgan.

  - **Registro de calendario**   Esta subcarpeta contiene los cambios de calendario que se producen dentro de un buzón de correo. Esta carpeta no está disponible para los usuarios.

La ilustración siguiente muestra las subcarpetas en las carpetas Elementos recuperables. También muestra los procesos de retención de elementos eliminados, recuperación de elementos individuales y flujos de trabajo de retención que se describen en las secciones siguientes.

![Carpeta Elementos recuperables](images/Ee364755.a1a08afc-3617-4adb-83ab-a6904516954e(EXCHG.150).gif "Carpeta Elementos recuperables")

Volver al principio

## Retención de elementos eliminados

Se considera que un elemento se elimina de forma permanente en los siguientes casos:

  - Un usuario elimina un artículo o vacía todos los elementos de la carpeta Elementos eliminados.

  - Un usuario presiona Short+Delete para eliminar un artículo de cualquier otra carpeta de buzones.

Los elementos eliminados de forma permanente se mueven a la subcarpeta Eliminaciones de la carpeta Elementos recuperables. Esto proporciona una capa adicional de protección, de manera que los usuarios puedan recuperar los elementos eliminados de forma permanente sin requerir la intervención del servicio técnico. Los usuarios pueden usar la característica Recuperar elementos eliminados en Outlook o Outlook Web App para recuperar un elemento eliminado. Los usuarios también pueden usar esta característica para eliminar un elemento de forma permanente. Para obtener más información, vea:

  - [Restaurar elementos eliminados en Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)

  - [Recuperar elementos eliminados o correo electrónico en Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

Los elementos permanecen en la subcarpeta Eliminaciones hasta alcanzar el período de retención del elemento eliminado. El período de retención predeterminado del elemento eliminado para una base de datos de buzones de correo es de 14 días. Este período puede modificarse para una base de datos de buzones de correo o para un buzón específico. Además del período de retención de un elemento eliminado, la carpeta Elementos recuperables también está sujeta a cuotas. Para obtener más información, vea Cuotas del buzón de correo de elementos recuperables más adelante en este tema.

Después de que transcurra el período de retención del elemento eliminado, el elemento se moverá a la carpeta Purgas y no será visible para el usuario. Cuando el asistente para carpetas administradas procesa el buzón de correo, los elementos de la subcarpeta Purgas se eliminan de la base de datos de buzones de correos y no se pueden recuperar.

Volver al principio

## Recuperación de elementos individuales

Si un elemento se quita de la subcarpeta Eliminaciones, ya sea por un usuario que purga el elemento mediante la característica Recuperar elementos eliminados o por un proceso automático como el Asistente para carpeta administrada, el usuario no puede recuperar el elemento. En versiones anteriores de Exchange, la recuperación de estos elementos requería que el administrador restaure la base de datos de buzones de correo o un buzón desde las copias de seguridad. En general, este proceso retrasaba la recuperación minuto u horas, según el mecanismo de copia de seguridad usado.

En Exchange 2013, puede usar la *recuperación de elementos individuales* para recuperar elementos sin tener que restaurar las bases de datos de buzones de correo mediante medios de copia de seguridad. Esto da como resultado períodos de recuperación considerablemente más breves. Cuando el Asistente para carpeta administrada procesa la carpeta Elementos recuperables de un buzón que tiene habilitada la recuperación de elementos individuales, los elementos en la subcarpeta Purgas se eliminan, siempre que haya caducado el período de retención del elemento eliminado correspondiente a esos elementos.

En la siguiente tabla, se detallan los contenidos y las acciones que se pueden realizar en la carpeta Elementos recuperables si está habilitada la recuperación de elementos individuales.

### Carpeta Elementos recuperables y recuperaciones de elementos individuales

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Estado de la recuperación de elementos individuales</th>
<th>La carpeta Elementos recuperables contiene elementos eliminados de forma permanente</th>
<th>La carpeta Elementos recuperables contiene elementos purgados</th>
<th>Los usuarios pueden eliminar los elementos de la carpeta Elementos recuperables</th>
<th>El Asistente para carpeta administrada elimina automáticamente los elementos de la carpeta Elementos recuperables</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Habilitado</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>Sí. Los usuarios pueden purgar los elementos mediante la característica Recuperar elementos eliminados en Outlook o Outlook Web App. Sin embargo, los elementos purgados no se quitarán de forma permanente de la base de datos de buzones mientras no expire el período de retención de elementos eliminados.</p></td>
<td><p>Sí. De forma predeterminada, todos los elementos se eliminan después de 14 días, a excepción de los elementos del calendario, que se eliminan después de 31 días.</p></td>
</tr>
<tr class="even">
<td><p>Deshabilitado</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>Sí. En este caso, los elementos purgados se marcan para su eliminación permanente de la base de datos de buzones y no se pueden recuperar.</p></td>
<td><p>Sí. De forma predeterminada, todos los elementos se eliminan después de 14 días, a excepción de los elementos del calendario, que se eliminan después de 31 días. Si se alcanza la cuota de advertencia Elementos recuperables antes de que transcurra el período de retención del elemento eliminado, se eliminan los mensajes en el orden &quot;primero en entrar, primero en salir&quot; (FIFO).</p></td>
</tr>
</tbody>
</table>


En Exchange 2013, la recuperación de elementos individuales no está habilitada de forma predeterminada o los buzones se movieron de una versión anterior de Exchange. Se debe usar el Shell de administración de Exchange para habilitar la recuperación de elementos individuales en un buzón y, a continuación, configurar o modificar el período de retención del elemento eliminado. Para obtener información detallada acerca de cómo realizar una recuperación de un único elemento, vea [Recuperar mensajes eliminados en el buzón de un usuario](https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-user-mailboxes/recover-deleted-messages).

Volver al principio

## Conservación local y retención por juicio

En Exchange 2013 y Exchange Online, los administradores de detección pueden usar la exhibición de documentos electrónicos local con permisos delegados de [Administración de la detección](discovery-management-exchange-2013-help.md) para hacer búsquedas de exhibición de documentos electrónicos del contenido de buzones de correo. Exchange 2013 y Exchange Online también presentan la retención local, que se puede usar para conservar los elementos de los buzones de correo que coinciden con los parámetros de consulta y para proteger los elementos de la eliminación por parte de usuarios o procesos automatizados. También puede usar la retención por juicio para preservar todos los elementos de los buzones de correo de los usuarios y proteger los elementos contra la eliminación por parte de usuarios o procesos automatizados.

Al colocar un buzón de correo en conservación local o retención por juicio, se evita que el Asistente para carpeta administrada purgue automáticamente mensajes de las subcarpetas Retenciones de detección y Purgas. Además, está habilitada la protección de página de escritura en copia para el buzón de correo. La protección de página de escritura en copia crea una copia del elemento original antes de que se escriba una modificación en el almacenamiento de Exchange. Después de quitar el buzón de correo de la suspensión por juicio, el Asistente para carpeta administrada reanuda la eliminación automática.

En la siguiente tabla, se detallan los contenidos y las acciones que se pueden realizar en la carpeta Elementos recuperables si está habilitada la retención por juicio.

### Carpeta Elementos recuperables y retenciones

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Estado de retención</th>
<th>La carpeta Elementos recuperables contiene elementos eliminados de forma permanente</th>
<th>La carpeta Elementos recuperables contiene elementos modificados y purgados</th>
<th>Los usuarios pueden eliminar los elementos de la carpeta Elementos recuperables</th>
<th>El Asistente para carpeta administrada elimina automáticamente los elementos de la carpeta Elementos recuperables</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Habilitado</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>Sí. Los usuarios pueden purgar los elementos mediante la característica Recuperar elementos eliminados en Outlook o Outlook Web App. Sin embargo, el Asistente para carpeta administrada no los quita de forma permanente de la base de datos de buzones si el buzón está en suspensión.</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Deshabilitado</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de la exhibición de documentos electrónicos local, la conservación local y la retención por juicio, vea estos temas:

  - [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md)

  - [Conservación local y retención por juicio](https://docs.microsoft.com/es-es/exchange/security-and-compliance/in-place-and-litigation-holds)

Volver al principio

## Protección de página de copia en escritura y elementos modificados

Si un usuario que se coloca en conservación local o retención por juicio modifica propiedades específicas de un elemento de un buzón de correo, se crea una copia del elemento original del buzón de correo antes de que se escriba el elemento cambiado. La copia original se guarda en la subcarpeta Versiones. Este proceso se conoce como *protección de página de escritura en copia*. Esta protección se aplica a los elementos de cualquier carpeta del buzón de correo. Los usuarios no pueden ver la subcarpeta Versiones.

En la siguiente tabla, se enumeran las propiedades de mensajes que desencadenan la protección de página de copia en escritura.

### Propiedades que desencadenan la protección de página de copia en escritura

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de elemento</th>
<th>Propiedades que desencadenan la protección de página de copia en escritura</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mensajes (IPM.Note*)</p>
<p>Entradas (IPM.Post*)</p></td>
<td><ul>
<li><p>Tema</p></li>
<li><p>Cuerpo</p></li>
<li><p>Datos adjuntos</p></li>
<li><p>Remitentes y destinatarios</p></li>
<li><p>Fechas de envío y recepción</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Elementos que no son mensajes ni entradas</p></td>
<td><p>Cualquier cambio en una propiedad visible, excepto los siguientes:</p>
<ul>
<li><p>Ubicación del elemento (cuando un elemento se mueve de una carpeta a otra)</p></li>
<li><p>Cambio de estado de elemento (leído o no leído)</p></li>
<li><p>Cambios realizados en la etiqueta de retención aplicada a un elemento</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Elementos de la carpeta predeterminada Borradores</p></td>
<td><p>Ninguno. Los elementos en la carpeta Borradores están exentos de la protección de la página de copia en escritura.</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> La protección de página de copia en escritura no guarda una versión de la reunión cuando un organizador de la reunión recibe respuestas de los asistentes y se actualiza la información de seguimiento de la reunión. Además, la protección de página de copia en escritura no captura los cambios en las fuentes RSS.



Cuando un buzón de correo ya no está en retención local o retención por litigio, se quitan las copias de los elementos modificados almacenados en la carpeta Versiones.

Volver al principio

## Cuotas del buzón de correo de elementos recuperables

Cuando un elemento se mueve a la carpeta Elementos recuperables, su tamaño se deduce de la cuota del buzón y se agrega al tamaño de la carpeta Elementos recuperables. En Exchange 2013, las bases de datos de buzones de correo tienen una cuota de advertencia configurable de Elementos recuperables (*límite flexible*) de 20 GB y una cuota de Elementos recuperables (*límite máximo*) de 30 GB. De forma predeterminada, todos los buzones de correo en la base de datos heredan estos límites. No obstante, puede configurar buzones individuales con cuotas diferentes. Para obtener más información, vea [Configurar la retención de elementos eliminados y las cuotas de elementos recuperables](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md).

En Exchange Online, los límites predeterminados para la cuota de Elementos recuperables son los mismos que en Exchange 2013: un límite flexible de 20 GB y un límite máximo de 30 GB. Sin embargo, las cuotas de la carpeta Elementos recuperables aumentan automáticamente a 90 y 100 GB, respectivamente, al colocar un buzón en Retención por juicio o Retención local.

Cuando la carpeta Elementos recuperables de un buzón de correo alcanza la cuota Elementos recuperables, no se pueden almacenar más elementos en la carpeta. Esto impacta en la funcionalidad del buzón de correo de las siguientes maneras:

  - Los usuarios de los buzones no pueden eliminar elementos.

  - El asistente para carpetas administradas no puede eliminar elementos basados en la etiqueta de retención o en la configuración de carpetas administradas.

  - Para los buzones de correo que tienen habilitada la recuperación de elementos individuales, la conservación local o la retención por juicio, el proceso de protección de página de copia en escritura no puede mantener versiones de los elementos editados por el usuario.

  - Para los buzones que tienen habilitado el registro de auditoría de buzones de correo, se pueden guardar las entradas del registro de auditoría de buzones en la subcarpeta Auditorías.

Para los buzones de correo que no se colocaron en conservación local o retención por juicio, el Asistente para carpeta administrada purga automáticamente los elementos de la carpeta Elementos recuperables una vez que caduca el período de retención del elemento eliminado. Si la carpeta alcanza la cuota de advertencia Elementos recuperables, el asistente elimina los elementos de manera automática en el orden "primero en entrar, primero en salir" (FIFO).

Cuando la carpeta Elementos recuperables alcanza los valores predeterminados para el límite Soft y Hard, se notifica mediante un registro de evento y un alerta de Microsoft System Center Operations Manager. Este alerta se acciona cuando la carpeta Elementos recuperables alcanza por primera vez los valores predeterminados del límite Soft y Hard, y a partir de ese momento, una vez por día.

En la siguiente tabla, se detallan los eventos registrados cuando la carpeta Elementos recuperables alcanza los valores predeterminados del límite Soft y Hard.

### Errores y advertencias de la cuota Elementos recuperables

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Id. de evento</th>
<th>Tipo</th>
<th>Origen</th>
<th>Mensaje</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10024</p></td>
<td><p>Advertencia</p></td>
<td><p>MSExchangeIS Mailbox Store</p></td>
<td><p>El buzón de correo para &lt;<em>usuario de correo</em>&gt; (<em>GUID</em>) ha excedido la cuota de advertencia Elementos recuperables. Elimine los elementos la carpeta Elementos recuperables o aumente la cuota de advertencia Elementos recuperables y la cuota Elementos recuperables. Si se excede la cuota Elementos recuperables, el usuario no podrá eliminar los elementos del buzón.</p></td>
</tr>
<tr class="even">
<td><p>10023</p></td>
<td><p>Error</p></td>
<td><p>MSExchangeIS Mailbox Store</p></td>
<td><p>El buzón de correo para &lt;<em>usuario de correo</em>&gt; (<em>GUID</em>) ha excedido la cuota máxima Elementos recuperables. No se pueden borrar los elementos de este buzón. El propietario del buzón debe ser notificado sobre el estado del buzón lo antes posible. Elimine los elementos de la carpeta Elementos recuperables o aumente la cuota Elementos recuperables para restaurar la funcionalidad.</p></td>
</tr>
<tr class="odd">
<td><p>10023</p></td>
<td><p>Advertencia</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>El tamaño de Elementos recuperables del buzón de correo: el &lt;<em>usuario de buzón</em>&gt; ha excedido el límite de la cuota de advertencia. Los elementos se eliminaron de las carpetas Elementos recuperables para evitar la interrupción del buzón. Cuota de advertencia Elementos recuperables: 20 GB (21,474,836,480 bytes) Tamaño original de los elementos recuperables: 21475005311 Tamaño actual de los elementos recuperables: 21474823820 Estadísticas de carpetas: - Carpetas procesadas: RecoverableItemsRoot, RecoverableItemsVersions, RecoverableItemsPurges, RecoverableItemsDeletions - Tamaño original de carpetas: 21391661934, 55190914, 1987247, 26157788 (conteos de elementos: 276828, 400, 84, 646) - Tamaño actual de carpetas: 21391480443, 55190914, 1987247, 26157788 (conteos de elementos: 276817, 400, 84, 646)</p></td>
</tr>
</tbody>
</table>


Si el buzón de correo se coloca en conservación local o retención por juicio, la protección de página de copia en escritura no puede mantener versiones de los elementos modificados. Para mantener las versiones de los elementos modificados, se debe reducir el tamaño de la carpeta Elementos recuperables. Se puede usar el cmdlet [Search-Mailbox](https://technet.microsoft.com/es-es/library/dd298173\(v=exchg.150\)) para copiar mensajes de la carpeta Elementos recuperables a un buzón de correo para un buzón de detección y, a continuación, se pueden eliminar los elementos del buzón. También se puede emitir una cuota Elementos recuperables para el buzón de correo. Para obtener información más detallada, vea [Limpiar la carpeta Elementos recuperables](clean-up-the-recoverable-items-folder-exchange-2013-help.md).

Volver al principio

## Más información

  - La copia en escritura solo está habilitada cuando un buzón se encuentra en conservación local o retención por juicio.

  - Si los usuarios necesitan recuperar elementos eliminados de la carpeta Elementos recuperables, remítalos a los siguientes temas:
    
      - [Restaurar elementos eliminados en Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Recuperar elementos eliminados o correo electrónico en Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

Volver al principio

