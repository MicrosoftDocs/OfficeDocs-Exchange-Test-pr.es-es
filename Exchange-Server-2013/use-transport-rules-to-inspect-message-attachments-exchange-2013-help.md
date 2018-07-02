---
title: 'Usar reglas de transporte para inspeccionar datos adjuntos de mensajes: Exchange 2013 Help'
TOCTitle: Usar reglas de transporte para inspeccionar datos adjuntos de mensajes
ms:assetid: c0de687e-e33c-4e8a-b253-771494678795
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ674307(v=EXCHG.150)
ms:contentKeyID: 49895888
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Usar reglas de transporte para inspeccionar datos adjuntos de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-27_

Puede configurar reglas de transporte para inspeccionar los datos adjuntos de correo de su organización. Exchange ofrece reglas de transporte que permiten examinar los datos adjuntos del correo como parte de la seguridad de la mensajería y las necesidades de conformidad normativa. Cuando inspeccione datos adjuntos, puede actuar en los mensajes inspeccionados en función del contenido o las características de esos datos adjuntos. A continuación se muestran algunas tareas relacionadas con datos adjuntos que pueden realizarse mediante reglas de transporte:

  - Buscar archivos en datos adjuntos comprimidos, tales como archivos .zip y .rar y, en caso de que exista texto que coincide con el modelo especificado, agregar una declinación de responsabilidad al final del mensaje.

  - Inspeccionar el contenido de los datos adjuntos y si hay coincidencia con las palabras clave especificadas, redirigir el mensaje a un moderador para que lo apruebe antes de su entrega.

  - Comprobar los mensajes con datos adjuntos que no se puede inspeccionar y, a continuación, impedir que se envíe el mensaje completo.

  - Comprobar los datos adjuntos que superen un determinado tamaño y, a continuación, notificar el problema al remitente si decide impedir que se entregue el mensaje.

  - Crear notificaciones que avisen a los usuarios si envían un mensaje que coincide con una regla de transporte.

  - Bloquear todos los mensajes que contengan datos adjuntos. Para ver más ejemplos, consulte [Escenarios comunes de bloqueo de datos adjuntos](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md).

Los administradores de Exchange pueden crear reglas de transporte desde el **Centro de administración de Exchange**\>**Flujo del correo**\>**Reglas**. Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento. Una vez que ha empezado a crear una nueva regla, puede consultar la lista completa de condiciones relacionadas con datos adjuntos haciendo clic en **Más opciones**\>**Cualquier adjunto** en **Aplicar esta regla si**. En el siguiente diagrama se muestran las opciones relacionadas con datos adjuntos.

![Cuadro de diálogo para seleccionar reglas relacionadas con datos adjuntos](images/JJ674307.2ae4a179-bfd2-4a0e-abe1-53ed4e9e3368(EXCHG.150).jpg "Cuadro de diálogo para seleccionar reglas relacionadas con datos adjuntos")

Para obtener más información acerca de las reglas de transporte, incluida toda la gama de condiciones y acciones que puede elegir, vea [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md). Exchange Online Protection (EOP) y los clientes híbridos pueden beneficiarse de los procedimientos recomendados de las reglas de transporte proporcionados en [Procedimientos recomendados para configurar EOP](https://technet.microsoft.com/es-es/library/jj723164\(v=exchg.150\)). Si está listo para comenzar a crear reglas, vea [Administrar reglas de flujo de correo](manage-mail-flow-rules-exchange-2013-help.md).

## Inspeccionar el contenido de los datos adjuntos

Puede usar las condiciones de reglas de transporte de la siguiente tabla para examinar el contenido de los datos adjuntos de los mensajes. Con estas condiciones solo se inspeccionan los primeros 150 KB de los datos adjuntos. Para empezar a usar estas condiciones al inspeccionar los mensajes, debe agregarlas a una regla de transporte. Para obtener más información acerca de cómo crear y cambiar reglas, vea [Administrar reglas de flujo de correo](manage-mail-flow-rules-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de condición en EAC</th>
<th>Nombre de condición en el Shell</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Cualquier dato adjunto... el contenido incluye alguna de estas palabras</strong></p></td>
<td><p><code>AttachmentContainsWords</code></p></td>
<td><p>Esta condición encuentra los mensajes con datos adjuntos de los tipos de archivo admitidos que contengan la cadena o el grupo de caracteres especificados.</p></td>
</tr>
<tr class="even">
<td><p><strong>Cualquier dato adjunto... el contenido coincide con estos patrones de texto</strong></p></td>
<td><p><code>AttachmentMatchesPatterns</code></p></td>
<td><p>Esta condición encuentra los mensajes con datos adjuntos de los tipos de archivo admitidos que contienen patrones de texto que coinciden con una expresión regular especificada.</p></td>
</tr>
</tbody>
</table>


Los nombres de Shell de administración de Exchange para las condiciones enumeradas aquí son parámetros que requieren el cmdlet `TransportRule`.

  -  
    Encontrará más información sobre el cmdlet en [New-TransportRule](https://technet.microsoft.com/es-es/library/bb125138\(v=exchg.150\)).

  -  
    Encontrará más información acerca de los tipos de propiedades de estas condiciones en [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Las reglas de transporte sólo pueden inspeccionar el contenido de tipos de archivo admitidos. Si el agente de reglas de transporte se encuentra con datos adjuntos que no aparecen en la lista de tipos de archivo admitidos, se activa la condición `AttachmentIsUnsupported`. Los tipos de archivo admitidos se enumeran en la siguiente sección. Cualquier archivo que no aparezca en la lista activará la condición `AttachmentIsUnsupported`.

## Archivos comprimidos

Si el mensaje incluye un archivo comprimido como un archivo ZIP o CAB, el agente de reglas de transporte inspeccionará los archivos incluidos en esos datos adjuntos. Dichos mensajes se procesan de manera similar que los mensajes que poseen varios documentos adjuntos. No se inspeccionan las propiedades de archivos comprimidos. Por ejemplo, si el tipo de archivo de contenedor admite comentarios, ese campo no se inspecciona.

## Tipos de archivo admitidos para la inspección de contenido de reglas de transporte

La siguiente tabla enumera los tipos de archivo admitidos por las reglas de transporte. El sistema detecta automáticamente los tipos de archivos inspeccionando las propiedades de archivo y no la extensión de archivo, lo que impide que los hackers malintencionados puedan eludir el filtrado de reglas de transporte cambiando el nombre de una extensión de archivo. Más adelante en este tema se enumeran los tipos de archivo con código ejecutable que pueden comprobarse en el contexto de las reglas de transporte.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Category</th>
<th>Extensión de archivo</th>
<th>Notas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Office 2013, Office 2010 y Office 2007</p></td>
<td><p>.docm, .docx, .pptm, .pptx, .pub, .one, .xlsb, .xlsm, .xlsx</p></td>
<td><p>Los archivos de Microsoft OneNote y Microsoft Publisher no se admiten de forma predeterminada. Puede habilitar la compatibilidad para estos tipos de archivo mediante la integración de IFilter. Para obtener más información, vea <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Registrar IFilters de Filter Pack con Exchange 2013</a>.</p>
<p>También se inspecciona el contenido de las partes incrustadas en estos tipos de archivo. No obstante, no se analizan los objetos que no estén incrustados, por ejemplo los documentos vinculados.</p></td>
</tr>
<tr class="even">
<td><p>Office 2003</p></td>
<td><p>.doc, .ppt, .xls</p></td>
<td><p>Ninguno</p></td>
</tr>
<tr class="odd">
<td><p>Archivos de Office adicionales</p></td>
<td><p>.rtf, .vdw, .vsd, .vss, .vst</p></td>
<td><p>Ninguno</p></td>
</tr>
<tr class="even">
<td><p>PDF de Adobe</p></td>
<td><p>.pdf</p></td>
<td><p>Ninguno</p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p>.html</p></td>
<td><p>Ninguno</p></td>
</tr>
<tr class="even">
<td><p>XML</p></td>
<td><p>.xml, .odp, .ods, .odt</p></td>
<td><p>Ninguno</p></td>
</tr>
<tr class="odd">
<td><p>Text</p></td>
<td><p>.txt, .asm, .bat, .c, .cmd, .cpp, .cxx, .def, .dic, .h, .hpp, .hxx, .ibq, .idl, .inc, inf, .ini, inx, .js, .log, .m3u, .pl, .rc, .reg, .txt, .vbs, .wtx</p></td>
<td><p>Ninguno</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument</p></td>
<td><p>.odp, .ods, .odt</p></td>
<td><p>No se procesan los archivos .odf. Por ejemplo, si el archivo .odf contiene un documento incrustado, no se inspecciona el contenido del documento incrustado.</p></td>
</tr>
<tr class="odd">
<td><p>Dibujo de AutoCAD</p></td>
<td><p>.dxf</p></td>
<td><p>No se admiten archivos de AutoCAD 2013.</p></td>
</tr>
<tr class="even">
<td><p>Image (Imagen)</p></td>
<td><p>.jpg, .tiff</p></td>
<td><p>Solo se inspecciona el texto de metadatos asociado a estos archivos de imagen. No se realiza reconocimiento óptico de caracteres.</p></td>
</tr>
</tbody>
</table>


## Inspeccionar las propiedades de archivo de los datos adjuntos

Las siguientes condiciones de regla de transporte inspeccionan las propiedades de un archivo adjunto a un mensaje. Para empezar a usar estas condiciones al inspeccionar los mensajes, debe agregarlas a una regla de transporte. A continuación se enumeran los tipos de archivo con código ejecutable que pueden comprobarse en el contexto de las reglas de transporte. Para obtener más información sobre cómo crear o cambiar las reglas, vea [Administrar reglas de flujo de correo](manage-mail-flow-rules-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de condición en EAC</th>
<th>Nombre de condición en el Shell</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>El nombre de archivo de alguno de los datos adjuntos coincide con estos patrones de texto</strong></p></td>
<td><p><code>AttachmentNameMatchesPatterns</code></p></td>
<td><p>Esta condición encuentra los mensajes con datos adjuntos de tipos de archivo compatibles cuando dichos adjuntos tienen un nombre que contiene los caracteres especificados.</p></td>
</tr>
<tr class="even">
<td><p><strong>La extensión de archivo de alguno de los datos adjuntos incluye estas palabras</strong></p></td>
<td><p><code>AttachmentExtensionMatchesWords</code></p></td>
<td><p>Esta condición encuentra los mensajes con datos adjuntos de tipos de archivo compatibles cuando la extensión de nombre de archivo coincide con lo que se especifique.</p></td>
</tr>
<tr class="odd">
<td><p><strong>El tamaño de alguno de los datos adjuntos es mayor o igual que</strong></p></td>
<td><p><code>AttachmentSizeOver</code></p></td>
<td><p>Esta condición encuentra los mensajes con datos adjuntos de tipos de archivo compatibles cuando dichos adjuntos son mayores que el tamaño especificado.</p></td>
</tr>
<tr class="even">
<td><p><strong>Los datos adjuntos no completaron el análisis</strong></p></td>
<td><p><code>AttachmentProcessingLimitExceeded</code></p></td>
<td><p>Esta condición encuentra los mensajes cuando el agente de las reglas de transporte no inspecciona los datos adjuntos.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Cualquier documento adjunto tiene contenido ejecutable</strong></p></td>
<td><p><code>AttachmentHasExecutableContent</code></p></td>
<td><p>Esta condición encuentra los mensajes que contienen archivos ejecutables como datos adjuntos. Aquí se incluyen los tipos de archivo admitidos.</p></td>
</tr>
<tr class="even">
<td><p><strong>Todos los datos adjuntos están protegidos con contraseña</strong></p></td>
<td><p><code>AttachmentIsPasswordProtected</code></p></td>
<td><p>Esta condición encuentra los mensajes con datos adjuntos de tipos de archivo compatibles cuando dichos adjuntos están protegidos mediante contraseña.</p></td>
</tr>
</tbody>
</table>


Los nombres de Shell de administración de Exchange para las condiciones enumeradas aquí son parámetros que requieren el cmdlet `TransportRule`.

  -  
    Encontrará más información sobre el cmdlet en [New-TransportRule](https://technet.microsoft.com/es-es/library/bb125138\(v=exchg.150\)).

  -  
    Encontrará más información acerca de los tipos de propiedades de estas condiciones en [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

## Tipos de archivo ejecutables admitidos para la inspección de reglas de transporte

El agente de transporte usa la detección de tipo verdadero inspeccionando las propiedades de archivo y no solamente las extensiones de archivo. Esto contribuye a impedir que los hackers malintencionados puedan eludir esta regla cambiando el nombre de una extensión de archivo. En la siguiente tabla se enumeran los tipos de archivo ejecutables que admiten esta condición. Si se encuentra un archivo que no se menciona aquí, se desencadena la condición `AttachmentIsUnsupported`.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de archivo</th>
<th>Extensión nativa</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Archivo de almacenamiento autoextraíble creado con el archivador de WinRAR.</p></td>
<td><p>.rar</p></td>
</tr>
<tr class="even">
<td><p>Archivo ejecutable de Windows de 32 bits con una extensión de biblioteca de vínculos dinámicos.</p></td>
<td><p>.dll</p></td>
</tr>
<tr class="odd">
<td><p>Archivo de programa ejecutable autoextraíble.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Archivo de almacenamiento de Java.</p></td>
<td><p>.jar</p></td>
</tr>
<tr class="odd">
<td><p>Archivo ejecutable de desinstalación.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Archivo de acceso directo del programa.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Archivo de código fuente compilado, archivo objeto 3D o archivo de secuencia.</p></td>
<td><p>.obj</p></td>
</tr>
<tr class="even">
<td><p>Archivo ejecutable de Windows de 32 bits.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Archivo de dibujo XML de Microsoft Visio.</p></td>
<td><p>.vxd</p></td>
</tr>
<tr class="even">
<td><p>Archivo del sistema operativo OS/2.</p></td>
<td><p>.os2</p></td>
</tr>
<tr class="odd">
<td><p>Archivo ejecutable de Windows de 16 bits.</p></td>
<td><p>.w16</p></td>
</tr>
<tr class="even">
<td><p>Archivo de sistema operativo de disco.</p></td>
<td><p>.dos</p></td>
</tr>
<tr class="odd">
<td><p>Archivo de prueba de antivirus estándar del Instituto Europeo para la Investigación de Antivirus.</p></td>
<td><p>.com</p></td>
</tr>
<tr class="even">
<td><p>Archivo de información de programa de Windows.</p></td>
<td><p>.pif</p></td>
</tr>
<tr class="odd">
<td><p>Archivo de programa ejecutable de Windows.</p></td>
<td><p>.exe</p></td>
</tr>
</tbody>
</table>


## Ampliar el número de tipos de archivo admitidos

Los tipos de archivo admitidos incluidos en este tema se pueden revisar en cualquier momento mediante la integración de IFilter. Para obtener más información, vea [Registrar IFilters de Filter Pack con Exchange 2013](register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md).

Los tipos de archivo que agrega con este proceso se convierten en tipos de archivo admitidos y ya no activan más la condición `AttachmentIsUnsupported`.

## Directivas de prevención de pérdida de datos y reglas de transporte de datos adjuntos

Para ayudarle a gestionar la información de correo electrónico relevante para su negocio, puede incluir cualquiera de las condiciones relacionadas con los datos adjuntos además de las reglas de una directiva de prevención de pérdidas de datos (DLP). Por ejemplo, si desea permitir que se envíen mensajes con números de pasaportes solo cuando dichos números están protegidos mediante una contraseña. Para realizarlo, haga lo siguiente:

  - Cree una directiva de DLP que inspeccione el correo electrónico en busca de información delicada relacionada con pasaportes. Obtenga más información en [Procedimientos de DLP](dlp-procedures-exchange-2013-help.md).

  - Agregue la excepción **Todos los datos adjuntos están protegidos con contraseña** en el área de la regla de transporte **Excepto si**.

  - Defina la acción que debe llevarse a cabo si un mensaje de correo electrónico contiene números de pasaporte que no están incluidos en el archivo protegido.

Las directivas de DLP y las condiciones relacionadas con los datos adjuntos contribuyen a satisfacer las necesidades de su negocio mediante la definición de dichas necesidades como condiciones de reglas de transporte, excepciones y acciones. Al incluir la inspección de información confidencial en una directiva de DLP, se analizan todos los datos adjuntos de los mensajes buscando exclusivamente esa información. Sin embargo, no se incluirán condiciones relacionadas con datos adjuntos como el tamaño o el tipo de archivo hasta que se agreguen las condiciones enumeradas en este tema. DLP no está disponible en todas las versiones de Exchange. Puede obtener más información en [Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md).

## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/es-es/library/jj919236\(v=exchg.150\)) en Exchange Online

