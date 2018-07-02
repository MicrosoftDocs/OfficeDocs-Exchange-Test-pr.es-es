---
title: 'Etiquetas de retención y directivas de retención: Exchange 2013 Help'
TOCTitle: Etiquetas de retención y directivas de retención
ms:assetid: 48c13be5-3f01-4849-a089-766210e54f89
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd297955(v=EXCHG.150)
ms:contentKeyID: 48268077
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Etiquetas de retención y directivas de retención

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En Microsoft Exchange Server 2013 y Exchange Online, la administración de registros de mensajes (MRM) ayuda a las organizaciones a administrar el ciclo de vida del correo electrónico y a reducir los riesgos legales asociados con el correo electrónico y otras comunicaciones. MRM facilita el mantenimiento de mensajes necesario para cumplir con la directiva de la compañía, la normativa del Gobierno o las necesidades legales, y ayuda a quitar el contenido que no disponga de valor legal o empresarial.

Vea en este [vídeo](http://go.microsoft.com/fwlink/?linkid=825854) una introducción rápida sobre cómo aplicar etiquetas de retención y una directiva de retención a un buzón en Exchange Online.

¿Busca procedimientos paso a paso para administrar MRM? Consulte [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

**Contenido**

Estrategia de administración de registros de mensajes

Etiquetas de retención

Directivas de retención

Asistente para carpetas administradas

Suspensión de la retención

## Estrategia de administración de registros de mensajes

En Exchange 2013 y Exchange Online la MRM se lleva a cabo mediante las *etiquetas de retención* y las *directivas de retención*. Antes de abordar los detalles sobre cada una de estas características de retención, es importante entender cómo se usan estas características en toda la estrategia de la MRM. Esta estrategia se basa en:

  - Asignar *etiquetas de directiva de retención* (RPT) a carpetas compartidas, como la Bandeja de entrada y los elementos eliminados.

  - Aplicar *etiquetas de directiva predeterminada* (DPT) a los buzones de correo para administrar la retención de todos los elementos sin etiquetas.

  - Permitir al usuario asignar *etiquetas personales* a carpetas personalizadas y a elementos individuales.

  - Separar la funcionalidad MRM de la administración de la Bandeja de entrada y de los hábitos de archivo de usuarios. No es necesario que los usuarios archiven mensajes en carpetas administradas en función de los requisitos de retención. Los mensajes individuales pueden tener una etiqueta de retención diferente de la etiqueta aplicada a la carpeta en la que se estos mensajes se encuentran.

La figura siguiente ilustra las tareas incluidas en la implementación de esta estrategia.

![Uso de directivas de retención para la retención de mensajería](images/Dd297955.429b51d5-51b8-4816-b8a4-221e0915d0c0(EXCHG.150).gif "Uso de directivas de retención para la retención de mensajería")

Volver al principio

## Etiquetas de retención

Como se ilustra en la figura anterior, las etiquetas de retención se usan para aplicar la configuración de retención a carpetas y a elementos individuales como mensajes de correo electrónico y correo de voz. Estas configuraciones especifican el tiempo que un mensaje permanece en un buzón de correo y la acción que se debe realizar cuando el mensaje alcanza la antigüedad de retención especificada. Cuando el mensaje alcanza la antigüedad de retención, se elimina o se mueve al buzón Archivo local del usuario.

![Configuración de una etiqueta de retención](images/Dd297955.936edd6a-8bc4-4c03-94a3-c240ffe7dd6a(EXCHG.150).png "Configuración de una etiqueta de retención")

Las etiquetas de retención permiten a los usuarios etiquetar sus propias carpetas de buzones y elementos individuales para retención. Ya no es necesario que los usuarios archiven elementos en carpetas administradas proporcionadas por un administrador en función de los requisitos de retención de mensajes.

## Tipos de etiquetas de retención

Las etiquetas de retención se clasifican en los siguientes tres tipos en función de quién puede aplicarlas y en qué parte de un buzón se puede aplicar.


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
<th>Tipo de etiqueta de retención</th>
<th>Se aplica a...</th>
<th>Aplicada por...</th>
<th>Acciones disponibles...</th>
<th>Detalles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Etiqueta de directiva predeterminada (DPT)</p></td>
<td><p>Automáticamente a todo el buzón</p>
<p>Las DPT se aplican a elementos <em>sin etiquetar</em>, que son elementos de buzón que no tienen aplicada una etiqueta de retención directamente o por herencia de la carpeta.</p></td>
<td><p>Administrador</p></td>
<td><ul>
<li><p>Mover a archivo</p></li>
<li><p>Eliminar y permitir recuperación</p></li>
<li><p>Eliminar permanentemente</p></li>
</ul></td>
<td><p>Los usuarios no pueden cambiar las DPT aplicadas a un buzón.</p></td>
</tr>
<tr class="even">
<td><p>Etiqueta de directiva de retención (RPT)</p></td>
<td><p>Automáticamente a una carpeta predeterminada</p>
<p>Las carpetas predeterminadas son carpetas que se crean automáticamente en todos los buzones de correo, por ejemplo: <strong>Bandeja de entrada</strong>, <strong>Elementos eliminados</strong> y <strong>Elementos enviados</strong>. Vea la lista de carpetas predeterminadas admitidas en <a href="default-folders-that-support-retention-policy-tags-exchange-2013-help.md">Carpetas predeterminadas que admiten etiquetas de la directiva de retención</a>.</p></td>
<td><p>Administrador</p></td>
<td><ul>
<li><p>Eliminar y permitir recuperación</p></li>
<li><p>Eliminar permanentemente</p></li>
</ul></td>
<td><p>Los usuarios no pueden cambiar la RTP aplicada a una carpeta predeterminada.</p></td>
</tr>
<tr class="odd">
<td><p>Etiqueta personal</p></td>
<td><p>Manualmente a elementos y carpetas</p>
<p>Los usuarios pueden automatizar el etiquetado usando reglas de la bandeja de entrada para mover un mensaje a una carpeta que tenga una etiqueta determinada o para aplicar una etiqueta personal al mensaje.</p></td>
<td><p>Usuarios</p></td>
<td><ul>
<li><p>Mover a archivo</p></li>
<li><p>Eliminar y permitir recuperación</p></li>
<li><p>Eliminar permanentemente</p></li>
</ul></td>
<td><p>Las etiquetas personales permiten a los usuarios determinar cuánto tiempo se debe retener un elemento. Por ejemplo, el buzón puede tener una DPT para eliminar elementos en varios años, pero un usuario puede crear una excepción para elementos como boletines y notificaciones automatizadas, y aplicar una etiqueta personal para eliminarlos en tres días.</p></td>
</tr>
</tbody>
</table>


## Más información acerca de las etiquetas personales

Las etiquetas personales están disponibles para los usuarios de Outlook 2010 y Outlook Web App como parte de su directiva de retención. En Outlook 2010 y en Outlook Web App, las etiquetas personales con la acción **Mover a archivo** aparecen como **Directiva de archivado**, y las etiquetas personales con la acción **Eliminar y permitir recuperación** o **Eliminar permanentemente** aparecen como **Directiva de retención**, tal y como se muestra en la figura siguiente.

![Etiquetas personales en Outlook 2010 y Outlook Web App](images/Dd297955.2dbaee13-fdd0-4c30-b821-e662ce2587bb(EXCHG.150).gif "Etiquetas personales en Outlook 2010 y Outlook Web App")

Los usuarios pueden aplicar etiquetas personales a las carpetas que creen o a los elementos individuales. Los mensajes que tienen aplicada alguna etiqueta personal siempre se procesan según la configuración de dicha etiqueta. Los usuarios pueden aplicar una etiqueta personal a un mensaje de modo que se mueva o se elimine antes o después de lo que indica la configuración especificada en las DPT o RPT aplicadas a ese buzón del usuario. También puede crear etiquetas personales que tengan deshabilitada la retención. Esto permite a los usuarios etiquetar elementos para que nunca se puedan mover a un archivo ni puedan expirar.


> [!NOTE]
> Los usuarios pueden aplicar directivas de archivo a carpetas predeterminadas, carpetas o subcarpetas creadas por usuarios y elementos individuales. Los usuarios pueden aplicar una directiva de retención a las carpetas o subcarpetas creadas por usuarios y a los elementos individuales (incluidos los elementos y las subcarpetas de una carpeta predeterminada), pero no a las carpetas predeterminadas.



Los usuarios pueden usar el Centro de Administración de Exchange (EAC) para seleccionar etiquetas personales adicionales que no estén vinculadas con su directiva de retención. A continuación, las etiquetas seleccionadas pasan a estar disponibles en Outlook 2010 y en Outlook Web App. Para permitir que los usuarios puedan seleccionar etiquetas adicionales desde el Centro de Administración de Exchange, debe agregar el [Rol MyRetentionPolicies](myretentionpolicies-role-exchange-2013-help.md) a la directiva de asignación de roles del usuario. Para obtener más información acerca de las directivas de asignación de roles para usuarios, vea [Descripción de las directivas de asignación de roles de administración](understanding-management-role-assignment-policies-exchange-2013-help.md). Si permite a los usuarios seleccionar etiquetas personales adicionales, tendrán disponibles todas las etiquetas personales de la organización de Exchange.


> [!NOTE]
> Las etiquetas personales son una característica premium. Los buzones de correo con directivas que contienen este tipo de etiquetas (o bien a raíz de que los usuarios hayan agregado etiquetas a su buzón) requieren una Licencia de acceso de cliente (CAL) de Exchange Enterprise.



Volver al principio

## Antigüedad de retención

Cuando habilita una etiqueta de retención, debe especificar una antigüedad de retención para la etiqueta. Esta antigüedad indica la cantidad de días durante los cuales se debe retener un mensaje antes de que llegue al buzón de correo del usuario.

La antigüedad de retención de los elementos no periódicos (como los mensajes de correo electrónico) se calcula de forma diferente a la de los elementos que tienen una fecha de finalización o elementos periódicos (como reuniones y tareas). Para conocer cómo se calcula la antigüedad de retención de diferentes tipos de elementos, vea [Cómo calcular la antigüedad de retención](how-retention-age-is-calculated-exchange-2013-help.md).

También puede crear etiquetas de retención con retención deshabilitada o deshabilitar las etiquetas después de crearlas. Como los mensajes que tienen una etiqueta deshabilitada no se procesan, no se realiza ninguna acción de retención. Como resultado, los usuarios pueden usar una etiqueta personal deshabilitada como una etiqueta **No mover nunca** o una etiqueta **No eliminar nunca** para reemplazar una DPT o RPT que de lo contrario se aplicaría al mensaje.

## Acciones de retención

Al crear o configurar una etiqueta de retención, puede seleccionar que se realice una de las siguientes acciones de retención cuando un elemento alcance su antigüedad de retención:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Acción de retención</th>
<th>Acción realizada...</th>
<th>Excepto...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Mover a archivo</strong> 1</p></td>
<td><ul>
<li><p>Coloca el mensaje en el buzón de archivo del usuario</p></li>
<li><p>Solo está disponible para etiquetas personales y DPT</p></li>
</ul>
<p>Para obtener información acerca del archivado, vea:</p>
<ul>
<li><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Archivado local en Exchange 2013</a></p></li>
<li><p><a href="https://technet.microsoft.com/es-es/library/dn922147(v=exchg.150)">Buzones de archivo en Exchange Online</a></p></li>
</ul></td>
<td><ul>
<li><p>Si el usuario no tiene un buzón de archivo, no se realiza ninguna acción.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Eliminar y permitir recuperación</strong></p></td>
<td><ul>
<li><p>Emula el comportamiento de vaciar la carpeta Elementos eliminados del usuario.</p></li>
<li><p>Los elementos se mueven a la <a href="recoverable-items-folder-exchange-2013-help.md">Carpeta Elementos recuperables</a> del buzón de correo y se conserva hasta el período de <em>retención de elementos eliminados</em>.</p></li>
<li><p>Proporciona al usuario una segunda oportunidad para recuperar el elemento con el cuadro de diálogo <strong>Recuperar elementos eliminados</strong> de Outlook o Outlook Web App</p></li>
</ul></td>
<td><ul>
<li><p>Si ha establecido el período de retención de elementos eliminados en cero días, los elementos se eliminan permanentemente. Para obtener información, vea <a href="https://technet.microsoft.com/es-es/library/dn163584(v=exchg.150)">Cambiar el tiempo que se conservan los elementos eliminados permanentemente para un buzón de correo de Exchange Online</a>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Eliminar permanentemente</strong></p></td>
<td><ul>
<li><p>Elimina definitivamente los mensajes.</p></li>
<li><p>Los elementos que se eliminan permanentemente no se pueden recuperar.</p></li>
</ul></td>
<td><ul>
<li><p>Si un buzón de correo se coloca en <a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Conservación local y retención por juicio</a> o en Retención por juicio, los elementos se conservan en la carpeta Elementos recuperables según los parámetros de retención. <a href="in-place-ediscovery-exchange-2013-help.md">Exhibición de documentos electrónicos en contexto</a> seguirá devolviendo estos elementos en los resultados de búsqueda.</p>
<p></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Marcar como Límite pasado de retención</strong></p></td>
<td><ul>
<li><p>Marca un mensaje como expirado. En Outlook 2010 y posterior y en Outlook Web App, los elementos expirados se muestran con una de estas notificaciones: &quot;Este elemento ha expirado&quot; y &quot;Este elemento expirará en 0 días&quot;. En Outlook 2007, los elementos marcados como expirados se muestran con texto tachado.</p></li>
</ul></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1 En una implementación híbrida de Exchange, puede habilitar un buzón de archivo basado en la nube para un buzón principal local. Si asigna una directiva de archivo a un buzón local, los elementos se mueven al archivo basado en la nube. Si un elemento se mueve al buzón de archivo, no se conserva una copia del elemento en el buzón local. Si el buzón local se coloca en retención, una directiva de archivo moverá igualmente los elementos al buzón de archivo basado en la nube, donde se conservarán durante el tiempo especificado por la retención.



Para obtener más información acerca de cómo crear etiquetas de retención, vea [Crear directivas de retención](create-a-retention-policy-exchange-2013-help.md).

Volver al principio

## Directivas de retención

Para aplicar una o más etiquetas de retención a un buzón de correo, agregue las etiquetas a una directiva de retención y luego aplique la directiva a los buzones de correo. Un buzón de correo no puede tener más de una directiva de retención. Las etiquetas de retención pueden vincularse a una directiva de retención o desvincularse de ella en cualquier momento, y los cambios se aplican automáticamente a todos los buzones de correo que tienen la directiva aplicada.

Una directiva de retención puede tener las siguientes etiquetas de retención:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de etiqueta de retención</th>
<th>Etiquetas de una directiva</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Etiqueta de directiva predeterminada (DPT)</p></td>
<td><ul>
<li><p>Una DPT con la acción <strong>Mover a archivo</strong></p></li>
<li><p>Una DPT con la acción <strong>Eliminar y permitir recuperación</strong> o <strong>Eliminar permanentemente</strong></p></li>
<li><p>Una DPT para los mensajes de correo de voz con la acción <strong>Eliminar y permitir recuperación</strong> o <strong>Eliminar permanentemente</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Etiquetas de directivas de retención (RPT)</p></td>
<td><ul>
<li><p>Una RPT para cada carpeta predeterminada compatible</p>

> [!NOTE]
> No es posible vincular más de una RPT para una carpeta predeterminada en particular (como <STRONG>Elementos eliminados</STRONG>) a la misma directiva de retención.


</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Etiquetas personales</p></td>
<td><ul>
<li><p>Las etiquetas personales que se desee</p></li>
</ul>

> [!TIP]
> Muchas etiquetas personales de una directiva pueden confundir a los usuarios. Recomendamos no agregar más de 10 etiquetas personales a una directiva de retención.


</td>
</tr>
</tbody>
</table>



> [!NOTE]
> Si bien una directiva de retención no necesita tener ninguna etiqueta de retención vinculada a ella, no recomendamos este escenario. Si los buzones de correo con directivas de retención no tienen ninguna etiqueta de retención vinculada a ellas, esto puede hacer que los elementos del buzón no expiren nunca.



Una directiva de retención puede contener tanto etiquetas de archivo (etiquetas que mueven elementos al buzón de archivo personal) como etiquetas de eliminación (etiquetas que eliminan elementos). Un elemento de buzón también puede tener ambos tipos de etiqueta aplicados. Los buzones de archivo no tienen una directiva de retención independiente. Se aplica la misma directiva de retención al buzón de archivo y al buzón primario.

Al planificar la creación de directivas de retención, debe tener en cuenta si incluirán tanto etiquetas de archivo como etiquetas de eliminación. Tal como se mencionó anteriormente, una directiva de retención puede tener una DPT que usa la acción **Mover a archivo** y una DPT que usa la acción **Eliminar y permitir recuperación** o la acción **Eliminar permanentemente**. La DPT que tiene la acción **Mover a archivo** debe tener una menor antigüedad de retención que la DPT que tiene la acción de eliminación. Por ejemplo, puede usar una DPT que tiene una acción **Mover a archivo** para mover elementos al buzón de archivo a los dos años, y una DPT con una acción de eliminación para eliminar elementos del buzón a los siete años. Los elementos en los buzones de correo principales y de archivo se eliminarán pasados siete años.

Para ver una lista de tareas de administración relacionadas con las directivas de retención, vea [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

## Directiva de retención predeterminada

El programa de instalación de Exchange crea la directiva de retención **Directiva MRM predeterminada**. La Directiva MRM predeterminada se aplica automáticamente a los nuevos buzones de correo en Exchange Online. En Exchange Server, la directiva se aplica automáticamente si crea un archivo para el nuevo usuario y no especifica una directiva de retención.

Puede modificar las etiquetas incluidas en la Directiva MRM predeterminada, por ejemplo cambiando la antigüedad de la retención o la acción de la retención, o bien puede deshabilitar una etiqueta o modificar la directiva agregando o quitando etiquetas de esta. La directiva actualizada se aplica a los buzones la próxima vez que el Asistente para carpetas administradas las procesa.

Para obtener más información, incluida una lista de etiquetas de retención vinculadas a la directiva, vea [Directiva de retención predeterminada en Exchange Online y Exchange Server](default-retention-policy-in-exchange-online-and-exchange-server-exchange-2013-help.md).

Volver al principio

## Asistente para carpetas administradas

El asistente para carpetas administradas, un asistente de buzón que se ejecuta en servidores Buzones, procesa los buzones que tienen aplicada una directiva de retención.

El asistente para carpetas administradas aplica la directiva de retención al inspeccionar los elementos del buzón de correo y al determinar si son elementos sujetos a directivas de retención. A continuación, el asistente marca los elementos sujetos a retención con las etiquetas de retención apropiadas y realiza la acción de retención especificada en los elementos que superaron la antigüedad de retención.

El Asistente para carpeta administrada es un asistente basado en limitaciones. Los asistentes basados en limitaciones funcionan constantemente y no es necesario programarlos. Los recursos del sistema que pueden consumir son limitados. Puede configurar el asistente para carpetas administradas para que procese todos los buzones del servidor Buzón dentro de un determinado período (conocido como *ciclo de trabajo*). Además, en un intervalo especificado (conocido como *punto de control de ciclo de trabajo*), el asistente actualiza la lista de buzones que procesar. Durante la actualización, el asistente agrega a la cola buzones movidos o creados recientemente. También cambia la prioridad de los buzones existentes que no se procesaron de correctamente debido a errores y los coloca más arriba en la cola para que se los pueda procesar durante el mismo ciclo de trabajo.

También puede usar el cmdlet [Start-ManagedFolderAssistant](https://technet.microsoft.com/es-es/library/aa998864\(v=exchg.150\)) para activar manualmente el asistente a fin de que procese un buzón especificado. Para obtener más información, vea [Configuración del asistente para carpetas administradas](configure-the-managed-folder-assistant-exchange-2013-help.md).


> [!NOTE]
> El Asistente para carpetas administradas no realiza ninguna acción en los mensajes que no están sujetos a retención, especificada por la deshabilitación de la etiqueta de retención. También puede deshabilitar una etiqueta de retención para suspender temporalmente el procesamiento de los elementos que tiene esa etiqueta.



## Mover elementos entre carpetas

Un elemento del buzón de correo que se mueve de una carpeta a otra hereda cualquier etiqueta aplicada a la carpeta a la que se mueve. Si se mueve un elemento a una carpeta que no tiene una etiqueta asignada, se le aplica la etiqueta de directiva predeterminada (DPT) a ese elemento. Si un elemento tiene una etiqueta asignada explícitamente, la etiqueta siempre tiene prioridad sobre cualquier etiqueta de nivel de la carpeta o sobre la etiqueta predeterminada.

## Aplicar una etiqueta de retención a una carpeta del archivo

Cuando el usuario aplica una etiqueta personal a una carpeta en el archivo, si existe una carpeta con el mismo nombre en el buzón de correo principal y tiene una etiqueta diferente, la etiqueta de dicha carpeta cambia para que coincida con la del buzón de correo principal. Esto es así por diseño, para evitar confusiones porque los elementos de una carpeta en el archivo tengan un comportamiento de expiración diferente que el de la misma carpeta en el buzón de correo principal del usuario. Por ejemplo, el usuario tiene una carpeta llamada Proyecto Contoso en el buzón de correo principal, con una etiqueta *Eliminar: 3 años* y existe también una carpeta Proyecto Contoso en el buzón de archivo. Si el usuario aplica una etiqueta personal *Eliminar: 1 año* para eliminar los elementos de la carpeta después de 1 año, cuando se vuelve a procesar el buzón de correo, la carpeta cambia de nuevo a la etiqueta Eliminar: 3 años.

## Quitar o eliminar una etiqueta de retención de una directiva de retención

Cuando se elimina una etiqueta de retención de la directiva de retención aplicada al buzón de correo, la etiqueta deja de estar disponible para el usuario y no se podrá aplicar a los elementos en el buzón de correo.

Los elementos existentes que han sido marcados con la etiqueta continúan siendo procesados por el Asistente para carpeta administrada en función de esas configuraciones y se aplica cualquier acción de retención especificada en la etiqueta sobre esos mensajes.

No obstante, si se elimina la etiqueta, se quita la definición de la etiqueta guardada en Active Directory. Esto hace que el asistente para carpetas administradas procese todos los elementos de un buzón y vuelva a estampar los elementos que tienen aplicada la etiqueta eliminada. Según la cantidad de buzones y mensajes, este proceso puede consumir recursos de manera significativa en todos los servidores de buzones de correo que contienen buzones con directivas de retención que incluyen la etiqueta eliminada.


> [!IMPORTANT]
> Si se elimina una etiqueta de retención de una directiva de retención, cualquiera de los elementos existentes en el buzón de correo con la etiqueta aplicada expirarán en función de la configuración de la etiqueta. Para evitar que se aplique la configuración de la etiqueta a cualquier elemento, se debe eliminar la etiqueta. Al eliminar la etiqueta se quita de cualquier directiva de retención en la que esté incluida.



## Deshabilitar una etiqueta de retención

Si deshabilita una etiqueta de retención, el Asistente para carpetas administradas ignora los elementos que tienen esa etiqueta aplicada. A los elementos que tienen una etiqueta de retención que tiene la retención deshabilitada nunca se los mueve ni se los elimina, según la acción de retención especificada. Debido a que estos elementos todavía se consideran elementos etiquetados, la DPT no se aplica a estos elementos. Por ejemplo, si desea solucionar la configuración de las etiquetas de retención, puede deshabilitar temporalmente una etiqueta de retención para que el Asistente para carpeta administrada deje de procesar mensajes con esa etiqueta.


> [!NOTE]
> El usuario verá el período de retención de una etiqueta de retención deshabilitada como <STRONG>Nunca</STRONG>. En caso de que un usuario coloque una etiqueta en un elemento al creer que nunca se lo eliminará, habilitar la etiqueta posteriormente puede causar una eliminación no intencional de elementos que el usuario no deseaba eliminar. Lo mismo sucede con las etiquetas que tienen la acción <STRONG>Mover a archivo</STRONG>.



Volver al principio

## Suspensión de la retención

Si los usuarios no se encuentran trabajando temporalmente y no tienen acceso a su correo electrónico, se puede aplicar la configuración de retención a mensajes nuevos antes de volver al trabajo o tener acceso al correo electrónico. Según la directiva de retención, los mensajes pueden ser eliminados o movidos al archivo personal del usuario. Es posible hacer que las directivas de retención dejen de procesar un buzón de correo por un período determinado si se coloca el buzón de correo en la suspensión de la retención. Si se coloca un buzón de correo en la suspensión de la retención, también, es posible especificar un comentario de retención que informa al usuario del buzón de correo (o a otro usuario autorizado para tener acceso al buzón) sobre el estado de retención, incluso, cuando el estado de retención se programe para comenzar y finalizar. Los comentarios de retención se muestran en clientes compatibles con Outlook. También, es posible localizar el comentario de suspensión de retención en el idioma preferido por el usuario.


> [!NOTE]
> Colocar el buzón de correo en la suspensión de la retención no afecta la manera en que se procesan las cuotas de almacenamiento del buzón de correo. Según el uso del buzón de correo y las cuotas de buzón aplicables, considere temporalmente aumentar la cuota de almacenamiento de buzón para usuarios cuando se encuentran de vacaciones o no tienen acceso al correo electrónico por un tiempo prolongado. Para obtener más información acerca de las cuotas de almacenamiento de buzones de correo, vea <A href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configurar cuotas de almacenamiento para un buzón</A>.



Los usuarios pueden acumular una gran cantidad de correos electrónicos durante largas ausencias del trabajo. Según el volumen de correo electrónico y el tiempo de ausencia, estos usuarios pueden pasar varias semanas clasificando los mensajes. En estos casos, considere el tiempo adicional que les puede llevar a los usuarios ponerse al día con los correos antes de eliminarlos de la suspensión de la retención.

Si la organización nunca ha implementado MRM o si los usuarios no se encuentran familiarizados con sus características, también, puede usar suspensiones de retenciones durante la fase inicial *preparación y entrenamiento* de la implementación de MRM. Puede crear e implementar directivas de retención y entrenar a los usuarios acerca de las directivas sin el riesgo de que se muevan o eliminen los elementos antes de que los usuarios puedan etiquetarlos. Unos pocos días antes de que finalice el período de preparación y entrenamiento, debe recordarles a los usuarios acerca del plazo final de la preparación. Después de que finalice el plazo, puede quitar la suspensión de la retención de los buzones de los usuarios, lo que permite que el asistente para carpetas administradas procese los elementos del buzón y aplique la acción de retención especificada.

Para obtener información detallada acerca de cómo colocar un buzón de correo en suspensión de retención, vea [Poner un buzón en retención](place-a-mailbox-on-retention-hold-exchange-2013-help.md).

Volver al principio

