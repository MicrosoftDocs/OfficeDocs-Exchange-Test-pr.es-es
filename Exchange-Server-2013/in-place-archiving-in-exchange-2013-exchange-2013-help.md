---
title: 'Archivado local en Exchange 2013: Exchange 2013 Help'
TOCTitle: Archivado local en Exchange 2013
ms:assetid: b5e4c0e9-0558-4b90-bc12-f67adbfb59ac
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd979800(v=EXCHG.150)
ms:contentKeyID: 48268582
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Archivado local en Exchange 2013

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Puede usar *archivos locales* para volver a tener el control de los datos de mensajería de la organización sin necesitar los archivos del almacén personal (.pst) y permitir, así, a los usuarios almacenar mensajes en un *buzón de correo de archivo* al que se puede tener acceso desde Microsoft Outlook 2010 y superior y Microsoft Office Outlook Web App.

En Microsoft Exchange Server 2013, los archivos locales proporcionan a los usuarios una ubicación de almacenamiento alternativa donde almacenar el historial de los datos de mensajería. Un archivo personal en contexto es un buzón de correo adicional (denominado buzón de archivo) habilitado para un usuario de buzón de correo. Los usuarios de Outlook 2007 o posterior y de Outlook Web App disponen de acceso ininterrumpido a su buzón de correo de archivos. Mediante cualquiera de estas aplicaciones cliente, los usuarios pueden visualizar un buzón de archivo y transferir o copiar mensajes entre su buzón de correo principal y el archivo. Los archivos locales presentan una vista uniforme de los datos de mensajería a los usuarios y eliminan la sobrecarga de usuarios que se requiere para administrar los archivos .pst.

Puede aprovisionar el archivo de un usuario en la misma base de datos de buzones de correo que el buzón de correo principal del usuario, otra base de datos de buzones de correo en el mismo servidor Buzón de correo, o bien una base de datos de buzones de correo en otro servidor Buzón de correo en el mismo sitio de Active Directory. En implementaciones híbridas de Exchange 2010 y posteriores, también puede aprovisionar un archivo basado en nube para buzones que se encuentren en los servidores Buzón de correo locales.

**Contenido**

Datos de mensajería y archivos .pst

Acceso de cliente a buzones de archivo

Acceso delegado

Mover mensajes al buzón de correo de archivo

Directivas de retención y de archivo

Directiva de MRM predeterminada

Cuotas de archivo

Archivos locales y otras características de Exchange

Administración de buzones de archivo

## Datos de mensajería y archivos .pst

Outlook usa archivos .pst para almacenar datos localmente en los equipos de los usuarios o los recursos compartidos de red. A diferencia de los archivos de almacén sin conexión (.ost) (que usa Outlook en el modo caché de Exchange para almacenar una copia del buzón de correo para acceso sin conexión), los archivos .pst no se sincronizan con el buzón de correo de Exchange del usuario. Si un usuario mueve mensajes a un archivo .pst, dichos mensajes se quitan del buzón de correo.

Usar archivos .pst para administrar los datos de mensajería puede causar los problemas siguientes:

  - **Archivos no administrados**   Por lo general, los archivos .pst son creados por usuarios y residen en sus equipos o en los recursos compartidos de red. La organización no los administra. Por consiguiente, los usuarios pueden crear varios archivos .pst que contengan mensajes idénticos o distintos y almacenarlos en ubicaciones diferentes, sin control de la organización.

  - **Aumento de los costos de detección**   Algunos procesos judiciales y requisitos empresariales o normativos pueden dar lugar a solicitudes de detección. Localizar los datos de mensajería que contienen los archivos .pst ubicados en los equipos de los usuarios puede resultar una tarea manual costosa. Dado que el seguimiento de archivos .pst no administrados puede ser difícil, es posible que los datos .pst no puedan detectarse en muchos de los casos. Es posible que esto exponga a la organización a riesgos legales y financieros.

  - **Incapacidad de aplicar directivas de retención de mensajería**   No se pueden aplicar directivas de retención de mensajería a mensajes ubicados en archivos .pst. Por ello, en función de las normas aplicables o del negocio, es posible que la organización no cumpla con los requisitos normativos.

  - **Riesgo de robo de datos**   Los datos de mensajería almacenados en archivos .pst son vulnerables al robo de datos. Por ejemplo, los archivos .pst suelen almacenarse en dispositivos portátiles tales como equipos portátiles, discos duros extraíbles, y medios portátiles tales como unidades USB, CD y DVD.

  - **Vista fragmentada de los datos de mensajería**   Los usuarios que almacenan información en archivos .pst no obtienen una vista uniforme de sus datos. Por lo general, los mensajes almacenados en archivos .pst solo están disponibles en el equipo donde se encuentra el archivo .pst. Por consiguiente, si los usuarios obtienen acceso a sus buzones de correo mediante Outlook Web App o Outlook en otro equipo, no es posible obtener acceso a los mensajes almacenados en sus archivos .pst.

## Acceso de cliente a buzones de archivo

En la siguiente tabla se indican las aplicaciones cliente que se pueden usar para obtener acceso a buzones de archivo.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cliente</th>
<th>Acceso a buzón de archivo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013, Outlook 2010, Outlook 2007 y Outlook Web App</p></td>
<td><p>Sí. Los usuarios de Outlook 2013, Outlook 2010, Outlook 2007 y Outlook Web App pueden copiar o mover elementos desde su buzón de correo principal a su buzón de correo de archivo, así como usar directivas de retención para mover elementos al archivo.</p>

> [!NOTE]
> Asimismo, los usuarios de Outlook 2010 y superior y Outlook 2007 pueden copiar o mover elementos de archivos .pst a su buzón de correo de archivo. Los usuarios de Outlook 2007 requieren la actualización acumulativa de Office 2007 de febrero de 2011. Existen algunas diferencias de compatibilidad de archivos entre Outlook 2010 y superior y Outlook 2007. Para obtener más información, vea el artículo del Blog del equipo de Exchange, vea <A href="https://blogs.technet.com/b/exchange/archive/2010/12/20/3411710.aspx">Sí Virginia, existe compatibilidad de archivos de Exchange 2010 en Outlook 2007</A>.


</td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> El archivo local es una característica de primer nivel y requiere una licencia de acceso de cliente (CAL) de Exchange Enterprise. Para obtener detalles acerca de licencias de Exchange, vea <A href="https://go.microsoft.com/fwlink/?linkid=237292">Concesión de licencias de Exchange Server</A>. Para obtener detalles sobre las versiones de Outlook necesarias para acceder al buzón de archivo, vea <A href="https://go.microsoft.com/fwlink/?linkid=237276">Requisitos de licencia para las directivas de retención y de archivo personal</A>.



Outlook no crea una copia local de buzón de archivo en el equipo de un usuario, aunque esté configurado para usar el modo caché de Exchange. Los usuarios solo pueden obtener acceso a los buzones de archivo en el modo en línea.

## Acceso delegado

El *acceso delegado* tiene lugar cuando se proporciona acceso a un usuario o a un conjunto de usuarios al buzón de correo de otro usuario. Existen diversos escenarios para proporcionar acceso delegado, como:

  - Proporcionar acceso a uno o más usuarios al buzón de correo de un usuario que ya no trabaja para la organización. En este caso, entre los usuarios a los que se puede proporcionar acceso delegado, se encuentran el jefe o el supervisor del usuario que se ha marchado o cualquier otro usuario que pase a asumir las responsabilidades del antiguo usuario.

  - Proporcionar a uno o más usuarios acceso a un buzón de correo compartido.

  - Proporcionar a los asistentes ejecutivos acceso a los buzones de correo de los ejecutivos a los que ayudan.

En Exchange 2013, al asignar permisos de acceso completo a un buzón de correo, el delegado al que asigna los permisos también puede obtener acceso al archivo del usuario. Los delegados deben usar Outlook para obtener acceso al buzón de correo y deben conectarse a un servidor de acceso de cliente de Exchange 2010 SP1 o superior para llevar a cabo acciones de Detección automática. La Detección automática es un servicio de Exchange que proporciona opciones de configuración para configurar automáticamente clientes de Outlook. Cuando los delegados usan Outlook para obtener acceso a un buzón de correo de Exchange 2013, tanto el buzón de correo principal como el archivo a los que tienen acceso están visibles en Outlook.

## Mover mensajes al buzón de correo de archivo

Existen diversos métodos para mover mensajes a buzones de archivo:

  - **Mover o copiar mensajes manualmente**   Los usuarios de buzones de correo pueden mover o copiar de forma manual mensajes de su buzón de correo principal o de un archivo .pst a su buzón de archivo. El buzón de archivo aparece como otro buzón de correo o como un archivo .pst en Outlook y en Outlook Web App.

  - **Mover o copiar mensajes mediante reglas de Bandeja de entrada**   Los usuarios de buzones de correo pueden crear reglas de la Bandeja de entrada en Outlook o en Outlook Web App para mover automáticamente mensajes a una carpeta de su buzón de correo de archivo. Para obtener más información, vea [Información acerca de las reglas de Bandeja de entrada](http://help.outlook.com/es-es/140/bb899620.aspx).

  - **Mover mensajes mediante directivas de retención**   Puede usar directivas de retención para mover mensajes automáticamente al archivo. Además, los usuarios pueden aplicar una etiqueta personal para mover mensajes al archivo. Para obtener más información sobre las directivas de retención y de archivo, vea Directivas de retención y de archivo más adelante en este tema.
    

    > [!NOTE]
    > Las etiquetas personales solamente están disponibles en Outlook Web App y en Outlook&nbsp;2010 o posterior.



  - **Importar mensajes de archivos .pst**   En Exchange 2013, puede usar una solicitud de importación de buzón de correo para importar mensajes de un archivo .pst al buzón de correo principal o al buzón de archivo de un usuario. Para obtener información más detallada, vea [Solicitudes de importación y exportación de buzones](mailbox-import-and-export-requests-exchange-2013-help.md). También puede usar la herramienta de captura PST para buscar los archivos .pst en los equipos de su organización e importar los datos del archivo .pst a los archivos de los usuarios.

## Directivas de retención y de archivo

En Exchange 2013, puede aplicar directivas de archivo a un buzón de correo que moverán los mensajes de manera automática del buzón de correo principal de un usuario al buzón de archivo una vez transcurrido un período especificado. Las directivas de archivo se implementan al crear etiquetas de retención que usan la acción de retención **Mover a archivo**.

Los mensajes se mueven a una carpeta en el buzón de archivo que tiene el mismo nombre que la carpeta de origen en el buzón de correo principal. Si no existe una carpeta con el mismo nombre en el buzón de archivo, se crea una cuando el Asistente para carpetas administradas mueve un mensaje. Recrear la misma jerarquía de carpetas en el buzón de archivo permite a los usuarios encontrar los mensajes con facilidad.

Para obtener más información acerca de las directivas de retención, las etiquetas de retención y la acción de retención **Mover a archivo**, vea [Etiquetas de retención y directivas de retención](retention-tags-and-retention-policies-exchange-2013-help.md).

## Directiva de MRM predeterminada

El programa de instalación de Exchange 2013 crea una directiva de retención y de archivo predeterminada llamada **Directiva de MRM predeterminada**. Esta directiva contiene etiquetas de retención con la acción **Mover a archivo**, tal y como se muestra en la tabla siguiente.


> [!NOTE]
> En Exchange 2010, la directiva de retención y de archivo predeterminada creada por el programa de instalación de Exchange se llama <STRONG>Directiva de retención y de archivo predeterminada</STRONG>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de etiqueta de retención</th>
<th>Tipo de etiqueta</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Mover al archivo después de 2 años de forma predeterminada</strong></p></td>
<td><p>Predeterminado (DPT)</p></td>
<td><p>Los mensajes se mueven automáticamente al buzón de archivo después de dos años. Se aplica a elementos de todo el buzón de correo que no tienen una etiqueta de retención aplicada explícitamente o heredada de la carpeta.</p></td>
</tr>
<tr class="even">
<td><p><strong>Mover al archivo después de 1 años en forma personal</strong></p></td>
<td><p>Personal</p></td>
<td><p>Los mensajes se mueven automáticamente al buzón de archivo después de un año.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mover al archivo después de 5 años en forma personal</strong></p></td>
<td><p>Personal</p></td>
<td><p>Los mensajes se mueven automáticamente al buzón de correo de archivo después de cinco años.</p></td>
</tr>
<tr class="even">
<td><p><strong>Nunca mover al archivo en forma personal</strong></p></td>
<td><p>Personal</p></td>
<td><p>Los mensajes nunca se mueven al buzón de correo de archivo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mover a archivo los elementos recuperables después de 14 días</strong></p></td>
<td><p>Carpeta Elementos recuperables</p></td>
<td><p>Los mensajes se mueven de la carpeta Elementos recuperables del buzón de correo principal del usuario a la carpeta Elementos recuperables del buzón de archivo. Los usuarios que deseen intentar recuperar elementos eliminados en el archivo deben usar la característica Recuperar elementos eliminados en el buzón de archivo.</p></td>
</tr>
</tbody>
</table>


Si habilita un archivo local para un usuario de buzón de correo y el buzón todavía no tiene asignada una directiva de retención, se asignará automáticamente la directiva de retención y de archivo predeterminada. Después de que el Asistente para carpetas administradas procese el buzón de correo, estas etiquetas están a disposición del usuario, quien puede etiquetar carpetas o mensajes para moverlos al buzón de archivo. De forma predeterminada, los mensajes de correo electrónico de todo el buzón de correo se mueven una vez transcurridos dos años.

Antes de aprovisionar buzones de archivo para sus usuarios, se recomienda que les informe sobre las directivas de archivo que se aplicarán a sus buzones de correo, además de proporcionarles la formación y la documentación pertinentes para cubrir sus necesidades. En esta sección se proporcionan detalles sobre los aspectos siguientes:

  - Funcionalidad disponible en el archivo, y las directivas de retención y de archivo predeterminadas.

  - Información sobre cuándo se pueden mover automáticamente mensajes al archivo.

  - Información sobre la jerarquía de carpetas creada en el buzón de archivo.

  - Cómo aplicar etiquetas personales (mostradas en el menú directiva de archivo en Outlook y en Outlook Web App).


> [!NOTE]
> Al aplicar una directiva de retención a los usuarios que tienen un buzón de correo de archivo, la directiva de retención reemplaza la directiva de MRM predeterminada. Puede crear una o más etiquetas de retención con la acción <STRONG>Mover a archivo</STRONG> y, a continuación, vincular las etiquetas a la directiva de retención. También puede agregar las etiquetas <STRONG>Mover a archivo</STRONG> predeterminadas (creadas mediante el programa de instalación y vinculadas a la directiva de MRM predeterminada) a cualquier directiva de retención que cree.



Para obtener más información sobre el cumplimiento y el archivado en Outlook 2010 y superior, vea [Plan del cumplimiento y el archivado en Outlook 2010](https://go.microsoft.com/fwlink/?linkid=210902).

## Cuotas de archivo

Los buzones de correo de archivo están diseñados para permitir a los usuarios almacenar el historial de datos de mensajería fuera de su buzón de correo principal. Por lo general, los usuarios usan archivos .pst debido a las bajas cuotas de almacenamiento de buzón de correo y las restricciones que se imponen cuando se superan dichas cuotas. Por ejemplo, se puede impedir que los usuarios envíen mensajes cuando su tamaño de buzón supera la *Cuota de Prohibir envío*. De manera similar, se puede impedir que los usuarios envíen y reciban mensajes cuando su tamaño de buzón de correo supere la *Cuota de Prohibir envío y recepción*.

Para eliminar la necesidad de tener archivos .pst, proporcione a un buzón de archivo límites de almacenamiento que cumplan con los requisitos del usuario. No obstante, quizá desee conservar algo de control sobre las cuotas de almacenamiento y el crecimiento de los buzones de archivo para controlar los costos y la expansión.

Para ayudar con este control, puede configurar buzones de correo de archivo con una *cuota de advertencia de archivo* y una *cuota de archivo*. Cuando un buzón de archivo supera la cuota de advertencia de archivo especificada, se registra un evento de advertencia en el registro de eventos de la aplicación. Cuando un buzón de archivo supera la cuota de archivo especificada, los mensajes ya no se mueven al archivo, se registra un evento de advertencia en el registro de eventos de la aplicación y se envía un mensaje de cuota al usuario del buzón de correo. De forma predeterminada, en Exchange 2013, la cuota de advertencia de archivo está definida en 45 gigabytes (GB) y la cuota de archivo está definida en 50 GB.

En la lista siguiente se indican los eventos registrados y los mensajes de advertencia enviados cuando se cumplen la cuota de advertencia de archivo y la cuota de archivo.


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
<th>Cuota</th>
<th>Id. de evento</th>
<th>Tipo</th>
<th>Origen</th>
<th>Category</th>
<th>Mensaje</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cuota de advertencia de archivo</p></td>
<td><p>10022</p></td>
<td><p>Advertencia</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Asistente para carpetas administradas</p></td>
<td><p>El buzón de archivo &quot;&lt;Nombre para mostrar&gt;:&lt;GUID&gt;:&lt;Base de datos de buzones de correo&gt;:&lt;FQDN de servidor&gt;&quot; ha superado la cuota de advertencia del archivo &quot;&lt;Cuota de advertencia del archivo&gt;&quot;. El tamaño del buzón de archivo es de &quot;&lt;Tamaño&gt;&quot; bytes.</p></td>
</tr>
<tr class="even">
<td><p>Cuota de archivo</p></td>
<td><p>8537</p></td>
<td><p>Advertencia</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>General</p></td>
<td><p>El buzón de archivo de &lt;DN heredado&gt; ha superado el tamaño máximo de buzón de archivo. No puede copiar ni mover elementos al buzón de archivo. Todas las acciones de retención de mensajes que mueven elementos a un buzón de archivo devolverán un error y es posible que el buzón de correo primario tenga elementos con etiquetas de retención caducadas hasta que el buzón de archivo esté dentro del límite de tamaño máximo. Se notificará al propietario del buzón de correo acerca de la condición del buzón de archivo.</p></td>
</tr>
</tbody>
</table>


## Archivos locales y otras características de Exchange

En esta sección se explica la funcionalidad entre archivos locales y varias características de Exchange:

  - **Exchange Search   **La posibilidad de buscar mensajes con rapidez es si cabe incluso más fundamental con los buzones de archivo. Para Exchange Search, no hay ninguna diferencia entre el buzón de correo de archivo y el buzón de correo principal. El contenido de ambos buzones se indiza. Puesto que el buzón de archivo no se almacena en la caché del equipo de ningún usuario (aunque se use Outlook en el modo caché de Exchange), los resultados de búsqueda del archivo siempre se proporcionan mediante Exchange Search. Si se realiza una búsqueda en todo el buzón de Outlook 2010 y superior y Outlook Web App, los resultados de búsqueda incluyen el buzón de correo principal y el buzón de correo de archivo de los usuarios.

  - **Exhibición de documentos electrónicos local**   Cuando un administrador de descubrimiento realiza una búsqueda de exhibición de documentos electrónicos locales, también se busca en los buzones de archivo de los usuarios. No existe ninguna opción para excluir los buzones de archivo al crear una búsqueda de detección desde el Centro de Administración de Exchange (EAC). Si usa el Shell de administración de Exchange para crear una búsqueda de detección, puede excluir el archivo con el modificador *DoNotIncludeArchive*. Para obtener información más detallada, vea [New-MailboxSearch](https://technet.microsoft.com/es-es/library/dd298064\(v=exchg.150\)). Para obtener más información, vea [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > No puede usar la exhibición de documentos electrónicos locales para buscar en un buzón de correo desconectado.



  - **Retención local y Retención por juicio**   Cuando coloca un buzón de correo en retención local o retención por juicio, la retención se coloca tanto en el buzón de correo principal como en el buzón de correo de archivo. Para obtener más información acerca de retención local y retención por litigio, vea [Conservación local y retención por juicio](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - **Carpeta Elementos recuperables   **El buzón de archivo contiene su propia carpeta Elementos recuperables y está sujeto a las mismas cuotas de carpeta Elementos recuperables que el buzón de correo principal. Para obtener más información acerca de los elementos recuperables, vea [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

  - **Archivar contenido de Lync en Exchange**   Puede archivar conversaciones de mensajería instantánea y documentos de reuniones compartidos en línea en el buzón de correo principal del usuario. El buzón de correo debe estar ubicado en un servidor Buzón de correo de Exchange 2013 y debe tener implementado Microsoft Lync 2013 en su organización. Para obtener información más detallada, vea [Integración con SharePoint y Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

## Administración de buzones de archivo

En Exchange 2013, la creación y la administración de buzones de correo de archivos se integran con las tareas comunes de administración de buzones de correo, entre las que se incluyen:

  - **Creación de un buzón de archivo**   Puede crear un buzón de archivo al crear un buzón de correo, o bien puede habilitar un buzón de archivo para un buzón existente. Para obtener información más detallada, vea [Administrar archivos locales en Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

  - **Mover un buzón de correo de archivo**   Puede mover el buzón de correo de archivo de un usuario a otra base de datos de buzones de correo en el mismo servidor Buzón de correo o en otro servidor, independiente del buzón de correo principal. Para mover el buzón de archivo de un usuario, tiene que crear una solicitud de movimiento de buzón de correo. Para obtener información más detallada, vea [Administración de movimientos locales](manage-on-premises-moves-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > No se admite buscar el buzón de un usuario y archivarlo en diferentes versiones de Exchange Server.



  - **Deshabilitación de un buzón de correo de archivo**   Es posible que desee deshabilitar el buzón de correo de archivo de un usuario para solucionar algún problema, o si va a mover el buzón de correo principal a una versión de Exchange que no admita archivos locales. Deshabilitar un archivo es un proceso similar a deshabilitar un buzón de correo principal. Para obtener información más detallada, vea [Administrar archivos locales en Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md). En las implementaciones locales, los buzones de correo de archivo deshabilitados se retienen en la base de datos de buzones de correo hasta que se alcanza el período de retención de buzones eliminados para dicha base de datos. Durante este período, puede volver a conectar el archivo a un usuario de buzón de correo. Cuando se alcanza el período de retención de buzones eliminados, se purga el buzón de archivo desconectado de la base de datos de buzones de correo.

  - **Recuperación de estadísticas de buzones de correo y de carpetas**   Puede recuperar estadísticas de buzones de correo y de carpetas de buzones de correo para el buzón de archivo de un usuario usando el modificador *Archive* con los cmdlets [Get-MailboxStatistics](https://technet.microsoft.com/es-es/library/bb124612\(v=exchg.150\)) y [Get-MailboxFolderStatistics](https://technet.microsoft.com/es-es/library/aa996762\(v=exchg.150\)).

  - **Probar conectividad del archivo**   En Exchange 2013, puede usar el cmdlet de [Test-ArchiveConnectivity](https://technet.microsoft.com/es-es/library/hh529914\(v=exchg.150\)) para probar la conectividad a un archivo local o basado en nube especificado del usuario.

