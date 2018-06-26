---
title: 'Conservación local y retención por juicio: Exchange 2013 Help'
TOCTitle: Conservación local y retención por juicio
ms:assetid: 71031c06-852d-44d8-b558-dff444eaef8c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff637980(v=EXCHG.150)
ms:contentKeyID: 48268262
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conservación local y retención por juicio

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-11-15_


> [!NOTE]
> Hemos pospuesto la fecha límite del 1 de julio de 2017 para crear nuevas conservaciones locales en Exchange Online (en los planes independientes de Office 365 y Exchange Online). Pero más tarde este año o a principios del año que viene no podrá crear nuevas conservaciones locales en Exchange Online. Como alternativa al uso de conservaciones locales, puede usar <A href="https://go.microsoft.com/fwlink/?linkid=780738">casos de eDiscovery</A> o <A href="https://go.microsoft.com/fwlink/?linkid=827811">directivas de retención</A> en el Centro de seguridad y cumplimiento de Office 365. Después de retirar las nuevas conservaciones locales, podrá seguir modificando las conservaciones locales existentes y se admitirá la creación de conservaciones locales en las implementaciones híbridas de Exchange Server 2013 y de Exchange. También podrá seguir colocando los buzones de correo en retención por juicio.



Cuando existen sospechas fundadas de posibles litigios, se solicita a las organizaciones que conserven toda la información almacenada electrónicamente (ESI), incluso el correo electrónico que sea relevante para el caso. A menudo, dichas sospechas tienen lugar antes de que se conozcan los pormenores del caso, por lo que se suele conservar gran cantidad de material. Es posible que las organizaciones necesiten conservar todo el correo electrónico relacionado con un tema concreto o el perteneciente a ciertos usuarios. Según las prácticas de detección electrónica (eDiscovery) de la organización, puede adoptar las siguientes medidas para conservar el correo electrónico:

  - Pedir a los usuarios finales que no eliminen ningún mensaje para conservar el correo electrónico. No obstante, los usuarios pueden eliminar igualmente correo electrónico de forma intencionada o sin darse cuenta.

  - Suspender los mecanismos de eliminación automatizados como, por ejemplo, la administración de registros de mensajes (MRM). Esta medida podría generar una acumulación excesiva de correo electrónico en el buzón de correo del usuario y afectar negativamente a su productividad. Además, el hecho de suspender la eliminación automatizada no impide que los usuarios eliminen manualmente el correo electrónico.

  - Algunas organizaciones copian o mueven el correo electrónico a un archivo para asegurarse de que no se elimina ni altera ni manipula. Esta medida incrementa los costos porque es necesario copiar o mover los mensajes de forma manual a un archivo, o a productos de terceros usados para reunir y almacenar el correo electrónico fuera de Exchange.

Si el correo electrónico no se conserva, la organización puede quedar expuesta a riesgos legales o financieros, como la inspección de procesos de detección y conservación de datos, sentencias judiciales adversas, sanciones o multas.

Puede usar la retención local o por juicio para realizar las tareas siguientes:

  - Colocar buzones de usuario en retención y conservar elementos del buzón inmutablemente.

  - Preservar los elementos de buzón eliminados por los usuarios o por procesos de supresión automática como MRM.

  - Usar la retención local basada en consultas para buscar y conservar elementos que coincidan con criterios especificados.

  - Conservar elementos indefinidamente o durante un tiempo concreto.

  - Marcar un usuario en varias suspensiones en función de investigaciones o casos distintos.

  - Mantener activa la administración MRM de modo que las retenciones resulten transparentes para el usuario.

  - Habilitar búsquedas de la exhibición de documentos electrónicos de elementos en retención

**Contenido**

Casos de retención local

Conservación local y retención por juicio

Marcar un buzón en retención local

Colocar todas las carpetas públicas en retención

Retenciones y la carpeta Elementos recuperables

Retenciones y cuotas de buzón

Suspensiones y reenvío de correo electrónico

Preservar el contenido de Lync archivado

Eliminar un buzón en retención

Migrar buzones en retención de Exchange 2013 a Office 365

## Casos de retención local

En Exchange Server 2010, el concepto de retención legal se refiere a la retención de todos los datos del buzón de un usuario de forma indefinida o hasta que se quite dicha retención. En Exchange 2013, la conservación local introduce un nuevo modelo que permite especificar los parámetros siguientes:

  - **Qué retener**   Puede especificar qué elementos desea retener mediante parámetros de consulta como palabras clave, remitentes y destinatarios, fechas de inicio y finalización, así como especificar los tipos de mensajes (como mensajes de correo electrónico o elementos de calendario) que desea retener.

  - **Duración de la retención**   Puede especificar una duración para la retención de elementos.

Con este nuevo modelo, la retención local le permite crear directivas de retención granulares para preservar los elementos de buzón en los casos siguientes:

  - **Retención indefinida**   El escenario de retención indefinida es similar a la retención por juicio. Se usa para preservar los elementos de buzón de correo, de modo que pueda cumplir con los requisitos de la exhibición de documentos electrónicos. Durante el período de juicio o investigación, los elementos no se eliminan. Dado que la duración no se conoce de antemano, no se configura ninguna fecha de finalización. Para retener todos los elementos de correo indefinidamente, no especifique ningún parámetro de consulta ni la duración cuando cree una conservación local.

  - **Conservación local basada en consultas**   Si su organización conserva elementos según parámetros de consulta específicos, puede usar una conservación local basada en consultas. Puede especificar parámetros de consulta como, por ejemplo, palabras clave, fechas de inicio y finalización, direcciones de remitentes y destinatarios, y tipos de mensajes. Después de crear una conservación local basada en consulta, se preservarán todos los elementos de buzón existentes y futuros que coincidan con la consulta y los elementos creados en el futuro (incluidos los mensajes recibidos en una fecha posterior).
    

    > [!IMPORTANT]
    > Los elementos marcados porque no se pueden buscar, por lo general debido a un error al indexar datos adjuntos, también se conservan porque no se puede determinar si coinciden con los parámetros de consulta. Para obtener más información acerca de los elementos que no se pueden buscar, vea <A href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange</A>.



  - **Retención basada en tiempo**   Tanto la conservación local como la retención por juicio le permiten especificar el tiempo durante el cual se retendrán los elementos. La duración se calcula desde la fecha en que un elemento de buzón se recibe o se crea.
    
    Si la organización requiere que todos los elementos de buzón se preserven durante un período de tiempo concreto (por ejemplo, durante 7 años), puede crear una retención basada en tiempo. En Exchange 2013, puede especificar un tiempo de retención para los elementos en retención. La antigüedad de los elementos suspendidos se basa en la fecha en que se recibieron. Por ejemplo, considere un buzón colocado en una conservación local basada en tiempo y que tenga un período de retención configurado en 365 días. Si un elemento del buzón se elimina después de 300 días de la fecha de su recepción, se mantiene por 65 días adicionales antes de eliminarse de manera permanente. Puede usar una conservación local basada en tiempo junto con una directiva de retención para asegurarse de que los elementos se conserven durante un tiempo especificado y se supriman permanentemente pasado ese tiempo.

Puede usar Conservación local para colocar un usuario en varias conservaciones. Si un usuario se encuentra en varias conservaciones locales, se combinan las consultas de búsqueda de cualquier conservación basada en consultas (con operadores **OR**). En este caso, el número máximo de palabras clave en todas las conservaciones basadas en consulta de un buzón es de 500. Si hay más de 500 palabras clave, todo el contenido del buzón se coloca en conservación (y no solo el contenido que coincide con los criterios de búsqueda). Todo el contenido se conserva hasta que el número total de palabras clave es de 500 o menos.

Volver al principio

## Conservación local y retención por juicio

La retención por juicio, una característica de retención que se incorporó en Exchange 2010 para conservar los datos para la exhibición de documentos electrónicos, todavía está disponible en Exchange 2013. La retención por juicio utiliza la propiedad **LitigationHoldEnabled** de un buzón. Mientras que la conservación local ofrece una funcionalidad de retención detallada basada en los parámetros de consulta y en la capacidad para realizar varias retenciones, la retención por juicio solo permite poner todos los elementos en retención. También puede especificar el período durante el cual se conservarán los elementos cuando un buzón se ponga en retención por juicio. La duración se calcula desde la fecha en que un elemento de buzón se recibe o se crea. Si no se establece una duración, los elementos se conservan indefinidamente o hasta que se quite la retención.

Cuando un buzón se pone en una o más conservaciones locales y en retención por juicio (sin período de duración) al mismo tiempo, todos los elementos se conservan indefinidamente o hasta que se quiten las retenciones. Si quita la retención por juicio y el usuario todavía tiene una o más conservaciones locales, los elementos que coincidan con los criterios de la conservación local se conservarán durante el período de tiempo especificado en la configuración de la retención. Cuando se traslada un buzón que está en retención por juicio en Exchange 2010 a un servidor de buzones de correo de Exchange 2013, la configuración de la retención por juicio seguirá aplicándose, lo que garantiza que los requisitos de cumplimiento se cumplirán durante y después del traslado.


> [!NOTE]
> Si coloca un buzón en conservación local o retención por juicio, la conservación o retención se aplica al buzón principal y al buzón de archivo. Si coloca un buzón principal local en conservación o retención en una implementación híbrida de Exchange, el buzón de archivo basado en la nube (si está habilitado) también se coloca en conservación o retención.



Para más información, visite:

  - [Poner un buzón en retención por juicio](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - [Poner todos los buzones en retención](place-all-mailboxes-on-hold-exchange-2013-help.md)

## Marcar un buzón en retención local

Los usuarios autorizados que se hayan agregado al grupo de roles de control de acceso basado en roles (RBAC) de [Administración de la detección](discovery-management-exchange-2013-help.md) o se les hayan asignado los roles de administración de la retención legal y búsqueda de buzón pueden marcar a los usuarios en conservación local. Esta tarea se puede delegar en administradores de registros, responsables de cumplimiento normativo o abogados del departamento jurídico de la organización, a la vez que se asigna el menor número de privilegios posible. Para obtener más información acerca de cómo asignar el grupo de roles Discovery Management, vea [Asignar permisos de exhibición de documentos electrónicos en Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).


> [!IMPORTANT]
> En Exchange 2010, el rol de retención legal proporcionaba permisos suficientes a un usuario para poner los buzones en retención por juicio. En Exchange&nbsp;2013, puede usar los mismos permisos para colocar buzones de correo en una conservación local indefinida o basada en tiempo. No obstante, para crear una retención local basada en consulta, el usuario tiene que tener asignado el rol de búsqueda de buzones. El grupo de roles Discovery Management tiene ambos roles asignados.



En Exchange 2013, la funcionalidad de retención local está integrada en las búsquedas de exhibición de documentos electrónicos local. Puede usar el Asistente de **exhibición de documentos electrónicos local y retención** en el Centro de administración de Exchange o el cmdlet **New-MailboxSearch** y otros relacionados en el Shell de administración de Exchange para marcar un buzón en retención local. Para obtener más información acerca de cómo colocar un buzón en conservación local, vea [Crear o quitar una conservación local](create-or-remove-an-in-place-hold-exchange-2013-help.md).


> [!NOTE]
> Si usa el Archivado de Exchange Online para aprovisionar un archivo basado en la nube para sus buzones locales, deberá administrar la conservación local desde la organización de Exchange&nbsp;2013 local. La configuración de retención se propaga automáticamente al archivo basado en la nube mediante DirSync. Como se ha indicado anteriormente, cuando se coloca en retención un buzón local, el archivo en la nube correspondiente también se coloca en retención.



Muchas organizaciones requieren que, cuando se coloque a los usuarios en retención, se les notifique. Asimismo, cuando un buzón de correo está en retención, no es necesario suspender las directivas de retención aplicables al usuario de dicho buzón. Los usuarios podrían no advertir que están en retención porque los mensajes se siguen eliminando como se espera. Si la organización requiere que los usuarios en retención estén informados, puede agregar un mensaje de notificación en la propiedad **Comentario de retención** del usuario del buzón y usar la propiedad **RetentionUrl** para enlazarlo a una página web con más información. Outlook 2010 y las versiones posteriores muestran la notificación y la URL en el área Backstage. Debe usar el Shell para agregar y administrar estas propiedades para un buzón.

Volver al principio

## Colocar todas las carpetas públicas en retención

En Exchange Online, puede colocar carpetas públicas en retención con una conservación local. No se admite el uso de la retención por juicio para carpetas públicas. Cuando crea una conservación local, la única opción es colocar una conservación en todas las carpetas públicas de la organización. El resultado es que una conservación local se coloca en todos los buzones de carpetas públicas.

Además, al colocar carpetas públicas en un conservación local, también se conservarán los mensajes de correo electrónico relacionados con el proceso de sincronización de la jerarquía de carpetas públicas. Esto puede dar lugar a la conservación de miles de elementos de correo electrónico relacionados con la sincronización de la jerarquía. Estos mensajes pueden llenar la cuota de almacenamiento de la carpeta Elementos recuperables de los buzones de correo de las carpetas públicas. Para evitar esto, puede crear una conservación local basada en consulta y agregar el siguiente par de `property:value` a la consulta de búsqueda:

    NOT(subject:HierarchySync*)

El resultado es que no se pondrá en espera ningún mensaje (relacionado con la sincronización de la jerarquía de carpetas públicas) que contenga la frase "HierarchySync" en la línea de asunto.

## Retenciones y la carpeta Elementos recuperables

La conservación local y la retención por juicio usan la carpeta Elementos recuperables para conservar los elementos. Esta carpeta sustituye la característica popularmente conocida como *contenedor* en las versiones anteriores de Exchange. La carpeta Elementos recuperables está oculta en la vista predeterminada de Outlook, Outlook Web App y otros clientes de correo electrónico. Para obtener más información acerca de la carpeta Elementos recuperables, vea [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

De manera predeterminada, cuando un usuario elimina un mensaje de una carpeta que no es la carpeta Elementos eliminados, dicho mensaje se mueve a esta última. Esto se denomina *movimiento*. Cuando un usuario *elimina temporalmente* un elemento (para lo cual debe presionar las teclas MAYÚS y SUPR) o lo elimina de la carpeta Elementos eliminados, el mensaje se mueve a la carpeta Elementos recuperables, por lo que desaparece de la vista del usuario.

Los elementos de la carpeta Elementos recuperables se conservan durante el periodo de retención de elementos eliminados que está configurado en la base de datos de buzones de correo del usuario. De manera predeterminada, dicho periodo está establecido en 14 días para las bases de datos de buzones de correo. También se puede configurar una cuota de almacenamiento para la carpeta Elementos recuperables. Así, la organización queda protegida ante un posible ataque por denegación de servicio (DoS) debido al rápido crecimiento de la carpeta Elementos recuperables y, por tanto, de la base de datos de buzones de correo. Si un buzón de correo no se pone en conservación local o en retención por juicio, los elementos se eliminan permanentemente de la carpeta Elementos recuperables por el procedimiento "primero en entrar, primero en salir" siempre que se exceda la cuota de advertencia de dicha carpeta o si el elemento ha permanecido en la carpeta más tiempo del que establece el período de retención de elementos eliminados.

La carpeta Elementos recuperables contiene las subcarpetas siguientes, que se usan para almacenar los elementos eliminados en distintos sitios y facilitar la conservación local y la retención por juicio:

  - **Deletions**   Los elementos quitados de la carpeta Elementos eliminados o los eliminados temporalmente de otras carpetas se mueven a la subcarpeta Eliminaciones, donde el usuario los puede ver con la característica Recuperar elementos eliminados de Outlook y Outlook Web App. De manera predeterminada, los elementos permanecen en esta carpeta hasta que finaliza el periodo de retención de elementos eliminados que se ha configurado para la base de datos de buzones de correo o hasta que el buzón caduca.

  - **Purges**   Cuando un usuario elimina un elemento de la carpeta Elementos recuperables (mediante la herramienta Recuperar elementos eliminados de Outlook y Outlook Web App), el elemento se mueve a esta carpeta. Los elementos que superan el periodo de retención de elementos eliminados configurado en la base de datos de buzones de correo o en el buzón también se mueven a la carpeta Purgas. Los usuarios no pueden ver los elementos de esta carpeta aunque utilicen la herramienta Recuperar elementos eliminados. Cuando el asistente de buzones de correo procesa el buzón de correo, los elementos de la carpeta Purgas se eliminan de la base de datos de buzones de correos. Al poner al usuario del buzón de correo en retención por juicio, el asistente de buzones no elimina los elementos de esta carpeta.

  - **DiscoveryHold**   Si un usuario se marca en retención local, los elementos eliminados se desplazan a esta carpeta. Cuando el asistente del buzón procesa el buzón de correo, analiza los mensajes de esta carpeta. Los elementos que coinciden con la consulta de retención local se retienen hasta el período de retención especificado en la consulta. Si no se especifica un período de retención, los elementos se conservarán indefinidamente o hasta que se quite la retención del usuario.

  - **Versions**   Cuando un usuario se pone en conservación local o en retención por juicio, los elementos del buzón deben estar protegidos de cualquier manipulación o modificación por parte del usuario o de un proceso. Esto se consigue mediante un proceso *copy-on-write*. Cuando un usuario o proceso modifican las propiedades concretas de un elemento del buzón de correo, se guarda una copia del elemento original en la carpeta Versiones antes de que se confirme el cambio. El proceso se repite para los cambios posteriores. Los elementos contenidos en la carpeta Versiones también se indexan y se devuelven en las búsquedas de la exhibición de documentos electrónicos local. Después de quitar la retención, el Asistente para carpeta administrada elimina las copias de la carpeta Versiones.

### Propiedades que desencadenan la copia en escritura

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de elemento</th>
<th>Propiedades que desencadenan la copia en escritura</th>
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
<li><p>Remitentes/destinatarios</p></li>
<li><p>Fechas de envío/recepción</p></li>
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
<td><p>Elementos de la carpeta Borradores predeterminada</p></td>
<td><p>Ninguno (los elementos de la carpeta Borradores están exentos de copia en escritura)</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> El proceso Copy-on-write está deshabilitado para los elementos del calendario en el buzón de correo del organizador cuando se reciben respuestas de reunión por parte de los asistentes y se actualiza la información de seguimiento de la reunión. Para los elementos de calendario y los elementos que tienen establecido un aviso, la copia en escritura está deshabilitada para las propiedades ReminderTime y ReminderSignalTime. La copia en escritura no captura los cambios en estas propiedades. La copia de escritura no captura los cambios en las fuentes RSS.



Aunque los usuarios no vean las carpetas DiscoveryHold, Purgas y Versiones, la Búsqueda de Exchange indexa todos los elementos de la carpeta Elementos recuperables y se pueden encontrar mediante la exhibición de documentos electrónicos local. Cuando un usuario de buzón se quita de la conservación local o retención por juicio, es el Asistente para carpetas administradas el que purga los elementos de las carpetas DiscoveryHold, Purges y Versions.

Volver al principio

## Retenciones y cuotas de buzón

Los elementos de la carpeta Elementos recuperables no se tienen en cuenta al calcular la cuota del buzón de correo de un usuario. En Exchange, la carpeta Elementos recuperables tiene su propia cuota. Para Exchange, los valores predeterminados para las propiedades de buzón *RecoverableItemsWarningQuota* y *RecoverableItemsQuota* se establecen en 20 y 30 GB respectivamente. Para modificar estos valores para una base de datos de buzones de correo para Exchange Server 2013, utilice el cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)). Para modificarlos en buzones de correo individuales, use el cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

Cuando la carpeta Elementos recuperables de un usuario excede la cuota de advertencia de los elementos recuperables (que se indica mediante el parámetro *RecoverableItemsWarningQuota*), se registra un evento en el registro de eventos de la aplicación del servidor de buzones de correo. Cuando la carpeta excede la cuota de elementos recuperables (que se indica mediante el parámetro *RecoverableItemsQuota*), los usuarios no pueden vaciar la carpeta Elementos eliminados ni eliminar permanentemente los elementos del buzón de correo. Además, no se puede utilizar la copia en escritura para crear copias de elementos modificados. Por consiguiente, es esencial supervisar las cuotas de los elementos recuperables de aquellos usuarios de buzones marcados en conservación local.

En Exchange Online, la cuota para la carpeta Elementos recuperables (en el buzón principal del usuario) se aumenta automáticamente a 100 GB al colocar un buzón de correo en retención por juicio o en retención local. Cuando la cuota de almacenamiento de la carpeta Elementos recuperables del buzón principal de un buzón en retención está a punto de alcanzar su límite, puede hacer lo siguiente:

  - **Habilitar el buzón de archivo y activar el archivado de expansión automática** Puede habilitar una capacidad de almacenamiento ilimitada para la carpeta Elementos recuperables. Basta con que habilite el buzón de archivo y luego active la característica de archivado de expansión automática en Exchange Online. Esto se traduce en 100 GB para la carpeta Elementos recuperables del buzón principal y una capacidad ilimitada de almacenamiento de la carpeta Elementos recuperables del archivo del usuario. Vea cómo en: [Habilitar buzones de archivo en el Centro de seguridad y cumplimiento de Office 365](https://go.microsoft.com/fwlink/p/?linkid=863320) y [Habilitar el archivado ilimitado en Office 365](https://go.microsoft.com/fwlink/p/?linkid=844569).
    
    **Notas**:
    
      - Después de habilitar el archivo para un buzón que esté a punto de superar la cuota de almacenamiento de la carpeta Elementos recuperables, podría interesarle ejecutar el Asistente para carpeta administrada a fin de activar manualmente el Asistente para procesar el buzón, de modo que los elementos expirados se muevan a la carpeta Elementos recuperables del buzón de archivo. Vea el paso 4 para obtener instrucciones en [Aumentar la cuota de elementos recuperables para los buzones de correo en retención](https://go.microsoft.com/fwlink/p/?linkid=786479).
    
      - Tenga en cuenta que podrían moverse otros elementos del buzón del usuario al nuevo buzón de archivo. Considere la posibilidad de comunicarle al usuario que esto puede ocurrir después de habilitar el buzón de archivo.

  - **Crear una directiva de retención personalizada para los buzones de correo en suspensión** Además de habilitar el buzón de archivo y el archivado de expansión automática para los buzones en retención por juicio o conservación local, también podría interesarle crear una directiva de retención personalizada para los buzones en suspensión. Esto le permite aplicar una directiva de retención a los buzones en suspensión diferente de la directiva de MRM predeterminada que se aplica a los buzones que no están en suspensión. Además, le permite aplicar etiquetas de retención diseñadas específicamente para buzones en suspensión, lo que incluye la creación de una etiqueta de retención para la carpeta Elementos recuperables.

Para obtener más información, vea [Aumentar la cuota de elementos recuperables para buzones de correo en retención](http://go.microsoft.com/fwlink/p/?linkid=786479).

## Suspensiones y reenvío de correo electrónico

Los usuarios pueden usar Outlook y Outlook Web App para configurar el reenvío de correo electrónico de su buzón. El reenvío de correo electrónico permite que los usuarios configuren su buzón de correo de modo que reenvíe los mensajes de correo electrónico enviados a su buzón a otro buzón dentro o fuera de la organización. El reenvío de correo electrónico puede configurarse de manera que los mensajes enviados al buzón original no se copien en ese buzón, sino que solo se envíen a la dirección de reenvío.

En el caso de que se configure el reenvío de correo electrónico para un buzón y los mensajes no se copien en el buzón original, ¿qué ocurre si el buzón está en suspensión? El comportamiento es diferente en función de si el buzón está en una organización de Exchange 2013 o Exchange Online.

  - **Exchange Online**   La configuración de retención del buzón se comprueba durante el proceso de entrega. Si el mensaje cumple los criterios de retención del buzón, se guarda una copia del mensaje en la carpeta Elementos recuperables. Esto significa que puede usar la exhibición de documentos electrónicos local para buscar en el buzón original los mensajes que se reenviaron a otro buzón.

  - **Exchange 2013**   Si los mensajes se reenvían a otro buzón y no se copian en el buzón original, no se capturan ni se copian en la carpeta Elementos recuperables. Esto significa que los mensajes reenviados no se devolverán en una búsqueda de exhibición de documentos electrónicos local. Para corregir este problema, las organizaciones de Exchange 2013 pueden considerar la posibilidad de impedir que los usuarios configuren el reenvío de correo electrónico.

Volver al principio

## Preservar el contenido de Lync archivado

Exchange 2013, Microsoft Lync 2013 y Microsoft SharePoint 2013 proporcionan una preservación integrada y una experiencia de la exhibición de documentos electrónicos que le permiten preservar y buscar elementos entre los diferentes almacenes de datos. Exchange 2013 le permite archivar el contenido de Lync Server 2013 en Exchange, eliminando el requisito de una base de datos de SQL Server individual para almacenar el contenido de Lync archivado. La función integrada de supresión y exhibición de documentos electrónicos de SharePoint 2013 le permite preservar y buscar entre los datos de todos los almacenes desde una única consola.

Cuando se pone un buzón de Exchange 2013 en conservación local o en retención por juicio, el contenido de Microsoft Lync 2013 (como las conversaciones de mensajería instantánea y los archivos compartidos en una reunión en línea) se archivarán en el buzón. Si realiza una búsqueda en el buzón mediante el centro de exhibición de documentos electrónicos en Microsoft SharePoint 2013 o en la exhibición de documentos electrónicos local de Exchange 2013, también se devolverán en los resultados de búsqueda todos los contenidos de Lync archivados que coincidan con la consulta de búsqueda. También puede restringir la búsqueda al contenido de Lync archivado en el buzón.

Para habilitar el archivado del contenido de Lync en un buzón de Exchange 2013, debe configurar la integración de Lync 2013 con Exchange 2013. Para obtener más información, vea estos temas:

  - [Planificar el archivado](https://technet.microsoft.com/es-es/library/jj205069\(v=ocs.15\))

  - [Implementar el archivado](https://technet.microsoft.com/es-es/library/jj205147\(v=ocs.15\))

Volver al principio

## Eliminar un buzón en retención

Cuando se elimina un buzón que se ha colocado en retención por juicio o en conservación local, el resultado es diferente en función de si el buzón está en una organización de Exchange 2013 o Exchange Online.

  - **Exchange 2013**   Si un administrador elimina una cuenta de usuario que tiene un buzón de correo, el almacén de información de Exchange detectará en un momento dado que el buzón ya no está conectado a una cuenta de usuario y lo marcará para su eliminación, incluso si el buzón está en retención. Si desea conservar el buzón de correo, debe hacer lo siguiente:
    
    1.  En lugar de eliminar la cuenta de usuario, deshabilítela.
    
    2.  Cambie las propiedades del buzón para restringir su uso y tener acceso al buzón de correo. Por ejemplo, establezca las cuotas de envío y recepción en 1, bloquee quién puede enviar mensajes al buzón y restrinja quién puede tener acceso al buzón.
    
    3.  Retenga el buzón hasta que se hayan eliminado todos los datos o hasta que ya no sea necesario conservarlos.

  - **Exchange Online**   Si el buzón de un usuario se coloca en conservación local o en retención por juicio y se elimina la cuenta de Office 365 correspondiente, el buzón se convierte en un *buzón inactivo*, que es un tipo de buzón eliminado temporalmente. Los buzones inactivos se usan para conservar el contenido del buzón de un usuario después de que haya abandonado la organización. Los elementos de un buzón inactivo se conservan mientras dura la retención que se colocó en el buzón antes de que pasara a inactivo. Gracias a ello, los administradores, los responsables de cumplimiento normativo o los administradores de registros pueden usar la exhibición de documentos electrónicos local para acceder al contenido de un buzón inactivo y realizar búsquedas en él. Los buzones inactivos no pueden recibir correos electrónicos y no aparecen en la libreta de direcciones compartida de la organización ni en ninguna otra lista. Para obtener más información, consulte [Buzones de correo inactivos en Exchange Online](https://technet.microsoft.com/es-es/library/dn798632\(v=exchg.150\)).

Volver al principio

## Migrar buzones en retención de Exchange 2013 a Office 365

Si tiene una implementación híbrida de Exchange, se cumplen las siguientes condiciones cuando se mueve (se incorpora) un buzón de Exchange 2013 local a Exchange Online en Office 365:

  - Si el buzón local se encuentra en retención por juicio o conservación local, la configuración de la retención se conserva después de que se haya movido el buzón a Exchange Online.

  - Si el buzón local se encuentra en retención por juicio o conservación local, todo el contenido de la carpeta Elementos recuperables se mueve al buzón de Exchange Online.


> [!NOTE]
> La configuración de retención y el contenido de la carpeta Elementos recuperables también se conservan cuando se mueve (se desincorpora) un buzón de Exchange Online a la organización de Exchange&nbsp;2013 local.



Hay otras formas de migrar datos de correo electrónico locales a Office 365, como usar una migración preconfigurada de Exchange o una migración total de Exchange.

  - La migración total se puede usar para migrar buzones desde Exchange 2003 o Exchange 2007 a Office 365. En estas versiones de Exchange, no existen la carpeta Elementos recuperables (ni su funcionalidad). De esta manera, cuando migra buzones de Exchange 2003 o Exchange 2007 a Office 365, no existe contenido de la carpeta Elementos recuperables para mover.

  - Puede usarse una migración total para migrar buzones de Exchange 2003, Exchange 2007 y Exchange 2010 a Office 365. Como se mencionó anteriormente, los buzones de Exchange 2003 y Exchange 2007 no tienen una carpeta Elementos recuperables que se puede migrar. Dado que la carpeta Elementos recuperables se introdujo en Exchange 2010, el contenido de dicha carpeta se migra a Office 365 cuando se usa una migración total para migrar buzones de Exchange 2010.


> [!TIP]
> Para Exchange&nbsp;2013 y Exchange 2010, se recomienda una implementación híbrida de Exchange para migrar buzones locales a Office 365.



Volver al principio

