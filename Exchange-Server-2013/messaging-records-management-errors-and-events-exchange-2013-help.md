---
title: 'Errores y eventos de administración de registros de mensajes: Exchange 2013 Help'
TOCTitle: Errores y eventos de administración de registros de mensajes
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 51406522
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Errores y eventos de administración de registros de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

La administración de registros de mensajería (MRM) genera eventos que se pueden visualizar en el Visor de eventos. Esto le permite solucionar problemas y comprobar el rendimiento del asistente para carpeta administrada. El Visor de eventos realiza un seguimiento de los siguientes tipos de eventos según el orden de importancia siguiente:

1.  Eventos de error

2.  Eventos de advertencia

3.  Eventos informativos

## Eventos y errores de MRM

En las tablas siguientes se proporcionan listas de eventos que se pueden utilizar para solucionar problemas de MRM. Los tipos de registro son los siguientes:

  - Los eventos etiquetados como **LogAlways** se registran siempre de forma individual.

  - Los eventos etiquetados como **LogPeriodic** sólo se registran una vez en cada periodo de cinco minutos, no cada vez que se producen. De esta manera, se evita el exceso en entradas en el registro.

### Eventos de MRM en la categoría Asistente para carpeta administrada

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
<th><strong>Id. de evento</strong></th>
<th><strong>Categoría</strong></th>
<th><strong>Tipo de evento</strong></th>
<th><strong>Registro</strong></th>
<th><strong>Valor o descripción</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10003</p></td>
<td><p>Asistente para carpeta administrada</p></td>
<td><p>Error</p></td>
<td><p>LogPeriodic</p></td>
<td><p>No se ha podido obtener el objeto de configuración del servidor desde Active Directory. &lt;<em>Detalles de la excepción</em>&gt;. Busque problemas de conectividad de la red del controlador de dominios o configuraciones de DNS incorrectas.</p></td>
</tr>
<tr class="even">
<td><p>10004</p></td>
<td><p>Asistente para carpetas administradas</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>La directiva de retención de la carpeta &lt;<em>folder</em>&gt; del buzón &lt;<em>mailbox</em>&gt; no se aplicará. El asistente para carpeta administrada no puede procesar la configuración de contenido administrado &lt;<em>content setting</em>&gt; de la carpeta administrada &lt;<em>managed folder</em>&gt;. El parámetro RetentionAction está establecido en MoveToFolder, pero no se ha especificado una carpeta de destino. Especifique una carpeta de destino.</p></td>
</tr>
<tr class="odd">
<td><p>10005</p></td>
<td><p>Asistente para carpetas administradas</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>La directiva de retención no se aplicará a la carpeta &lt;<em>folder</em>&gt; del buzón &lt;<em>mailbox</em>&gt;. No se ha podido procesar la configuración de contenido administrado &lt;<em>content setting</em>&gt; para la carpeta administrada &lt;<em>managed folder</em>&gt;. El parámetro RetentionAction está establecido en MoveToFolder, pero la carpeta de destino &lt;<em>folder</em>&gt; es la misma que la carpeta de origen &lt;<em>folder</em>&gt;. Especifique una carpeta de destino que sea diferente a la carpeta de origen.</p></td>
</tr>
<tr class="even">
<td><p>10009</p></td>
<td><p>Asistente para carpetas administradas</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>El asistente para carpeta administrada omitió el proceso de todas las bases de datos en el servidor local porque no podía leer los parámetros de registro de auditoría de Active Directory. Volverá a intentarlo más tarde en la ventana Programación. Base de datos actual: &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10010</p></td>
<td><p>Asistente para carpetas administradas</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>El asistente para carpeta administrada omitió el proceso de todas las bases de datos en el servidor local porque el registro de auditoría está habilitado, pero falta su ruta de acceso en Active Directory. Volverá a intentarlo más tarde en la ventana Programación. Base de datos actual: &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10011</p></td>
<td><p>Asistente para carpetas administradas</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>El asistente para carpeta administrada no ha podido configurar el registro de auditoría. Se detendrá el proceso de la base de datos actual: '%1'. Volverá a intentarlo más tarde en la ventana Programación. Detalles de la excepción: &lt;<em>detalles</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10012</p></td>
<td><p>Asistente para carpetas administradas</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>El asistente para carpeta administrada no ha podido escribir en el registro de auditoría. Se detendrá el proceso de la base de datos actual: &lt;<em>database</em>&gt;. Más adelante, intentará volver a escribir en el registro de auditoría en la ventana Programación. Detalles de la excepción: &lt;<em>detalles</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10017</p></td>
<td><p>Asistente para carpetas administradas</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>Se ha producido una excepción en el asistente para carpeta administrada mientras procesaba el buzón: &lt;<em>mailbox</em>&gt; Carpeta: Nombre: &lt;<em>folder name</em>&gt; Id: &lt;<em>folder ID</em>&gt; Elemento: Id: &lt;<em>IDs</em>&gt;. Excepción: &lt;<em>exception</em>&gt;.</p></td>
</tr>
</tbody>
</table>


### Eventos de MRM en la categoría Asistentes

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
<th><strong>Id. de evento</strong></th>
<th><strong>Category</strong></th>
<th><strong>Tipo de evento</strong></th>
<th><strong>Registro</strong></th>
<th><strong>Valor o descripción</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9004</p></td>
<td><p>Asistentes</p></td>
<td><p>Advertencia</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; no ha procesado el buzón &lt;<em>mailbox</em>&gt;. La siguiente excepción causó el error: &lt;<em>excepción</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9014</p></td>
<td><p>Asistentes</p></td>
<td><p>Advertencia</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>servicio</em>&gt;. No se han podido procesar los cambios de programación. La siguiente excepción causó el error: &lt;<em>excepción</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9017</p></td>
<td><p>Asistentes</p></td>
<td><p>Información</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; de la base de datos &lt;<em>database</em>&gt; está entrando en una ventana de tiempo programado. Hay &lt;<em>number</em>&gt; buzones para procesar.</p></td>
</tr>
<tr class="even">
<td><p>9018</p></td>
<td><p>Asistentes</p></td>
<td><p>Información</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; de la base de datos &lt;<em>database</em>&gt; está saliendo de una ventana de tiempo programado. Se ha procesado correctamente &lt;<em>number</em>&gt; de &lt;<em>number</em>&gt; buzones. Se han omitido &lt;<em>number</em>&gt; buzones debido a errores. Se ha procesado &lt;<em>number</em>&gt; buzones por separado. No se han procesado &lt;<em>number</em>&gt; buzones debido a la falta de tiempo.</p>

> [!NOTE]
> La próxima vez que se ejecute el asistente para carpeta administrada se reanudará donde se detuvo.


</td>
</tr>
<tr class="odd">
<td><p>9019</p></td>
<td><p>Asistentes</p></td>
<td><p>Advertencia</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Servicio &lt;<em>servicio</em>&gt;. No se ha podido guardar el progreso de &lt;<em>service</em>&gt; en la base de datos &lt;<em>database</em>&gt;. (El asistente no ha podido guardar el punto donde se detuvo para poder reanudar su operación desde ahí cuando se reinicie.) La siguiente excepción causó el error: &lt;<em>excepción</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9020</p></td>
<td><p>Asistentes</p></td>
<td><p>Advertencia</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. &lt;<em>assistant name</em>&gt; no ha podido iniciarse para la base de datos &lt;<em>database</em>&gt;. La siguiente excepción causó el error: &lt;<em>excepción</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9021</p></td>
<td><p>Asistentes</p></td>
<td><p>Información</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; de la base de datos &lt;<em>database</em>&gt; está procesando una solicitud a petición. Hay &lt;<em>number</em>&gt; buzones para procesar.</p></td>
</tr>
<tr class="even">
<td><p>9022</p></td>
<td><p>Asistentes</p></td>
<td><p>Información</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; para la base de datos &lt;<em>database</em>&gt; ha terminado una solicitud a petición. Se han procesado correctamente &lt;<em>number</em>&gt; de &lt;<em>number</em>&gt; buzones. Se han omitido &lt;<em>number</em>&gt; buzones debido a errores.</p></td>
</tr>
<tr class="odd">
<td><p>9023</p></td>
<td><p>Asistentes</p></td>
<td><p>Advertencia</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; no ha podido iniciar el procesamiento de la ventana de tiempo en la base de datos &lt;<em>database</em>&gt;. La siguiente excepción causó el error: &lt;<em>excepción</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9025</p></td>
<td><p>Asistentes</p></td>
<td><p>Información</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; ha omitido &lt;<em>number</em>&gt; buzones de la base de datos &lt;<em>database</em>&gt;. Buzones: &lt;<em>mailboxes</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9026</p></td>
<td><p>Asistentes</p></td>
<td><p>Advertencia</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; no ha podido iniciar el procesamiento a petición en la base de datos &lt;<em>database</em>&gt;. La siguiente excepción causó el error: &lt;<em>excepción</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9027</p></td>
<td><p>Asistentes</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; ha provocado la finalización del proceso &lt;<em>number</em>&gt; veces mientras procesaba el buzón &lt;<em>mailbox</em>&gt; en la base de datos &lt;<em>database</em>&gt;. Este buzón ya no se procesará en la ventana de tiempo solicitada ni en la solicitud a petición. La siguiente excepción causó el error: &lt;<em>excepción</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9028</p></td>
<td><p>Asistentes</p></td>
<td><p>Advertencia</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; ha provocado la finalización del proceso &lt;<em>number</em>&gt; veces mientras procesaba el buzón &lt;<em>mailbox</em>&gt; en la base de datos &lt;<em>database</em>&gt;. La siguiente excepción causó el error: &lt;<em>excepción</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9033</p></td>
<td><p>Asistentes</p></td>
<td><p>Advertencia</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. El servicio &lt;<em>service</em>&gt; de la base de datos &lt;<em>database</em>&gt; ha recibido una solicitud a petición. Sin embargo, no hay buzones para procesar.</p></td>
</tr>
<tr class="odd">
<td><p>9034</p></td>
<td><p>Asistentes</p></td>
<td><p>Información</p></td>
<td><p>LogAlways</p></td>
<td><p>El servicio &lt;<em>service</em>&gt; ha detenido las operaciones basadas en tiempo del asistente para carpeta administrada en la base de datos &lt;<em>database</em>&gt;.</p></td>
</tr>
<tr class="even">
<td><p>9035</p></td>
<td><p>Asistentes</p></td>
<td><p>Advertencia</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>service</em>&gt;. &lt;<em>assistant name</em>&gt; no ha podido procesar &lt;<em>number</em>&gt; buzones debido a la falta de tiempo.</p></td>
</tr>
<tr class="odd">
<td><p>9037</p></td>
<td><p>Asistentes</p></td>
<td><p>Error</p></td>
<td><p>LogAlways</p></td>
<td><p>Servicio &lt;<em>servicio</em>&gt;. Se ha detectado una excepción al procesar una RPC. Método: &lt;<em>method</em>&gt;, Excepción: &lt;<em>excepción</em>&gt;</p></td>
</tr>
</tbody>
</table>

