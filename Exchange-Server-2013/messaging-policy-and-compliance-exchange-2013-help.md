---
title: 'Directiva de mensajería y conformidad: Exchange 2013 Help'
TOCTitle: Directiva de mensajería y conformidad
ms:assetid: 65f20a20-27a4-4f6e-9b27-f8705d65b8d9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998599(v=EXCHG.150)
ms:contentKeyID: 48268221
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Directiva de mensajería y conformidad

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El correo electrónico se ha convertido en un medio de comunicación confiable y siempre presente para los profesionales de la información en las organizaciones de cualquier tamaño. Los buzones y los almacenes de mensajería han pasado a considerarse repositorios de datos valiosos. Para las organizaciones resulta importante crear directivas de mensajería que dicten el uso correcto de los sistemas de mensajería, proporcionen instrucciones al usuario sobre cómo actuar con las directivas y, si es necesario, suministren detalles sobre los tipos de comunicación que no están permitidos.

Asimismo, las organizaciones deben crear directivas para administrar el ciclo de vida del correo electrónico, conservar los mensajes durante un período de tiempo en función de los requisitos empresariales, legales y reglamentarios, guardar los registros de correo electrónico para fines jurídicos y de investigación y poder afrontar la búsqueda y el suministro de los registros de correo electrónico necesarios para cumplir las solicitudes de exhibición de documentos electrónicos.

También se debe proteger la pérdida de información confidencial como la propiedad intelectual, secretos empresariales, planes de negocio o información de identificación personal (PII) que la organización recopila o administra.

## Cumplimiento y directiva de mensajería en Exchange 2013

En la siguiente tabla se ofrece una descripción general de la directiva de mensajería y las características de cumplimiento en Microsoft Exchange Server 2013 y se incluyen vínculos a otros temas que le ayudarán a aprender más sobre estas características y a administrarlas.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Descripción</th>
<th>Recursos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de registros de mensajes (MRM)</p></td>
<td><p>Para cumplir las regulaciones aplicables o los requisitos legales o empresariales, las organizaciones incluyen directivas de ciclo de vida de correo electrónico como parte de su directiva de mensajería. Entre las preguntas comunes que deberían ser abordadas por estas directivas, se incluyen:</p>
<ul>
<li><p>¿Cuánto tiempo deben conservarse los mensajes?</p></li>
<li><p>¿Dónde deben conservarse los mensajes?</p></li>
<li><p>¿Deben conservarse todos los mensajes durante el mismo período?</p></li>
</ul>
<p>Exchange 2013 incluye características de administración de registros de mensajes (MRM) que permiten implementar directivas de ciclo de vida de correo electrónico en las organizaciones. Puede usar MRM para aplicar una configuración de retención uniforme a todos los mensajes, usar directivas de retención personalizadas para aplicar una configuración de retención de línea base al buzón y, de manera opcional, permitir a los usuarios que clasifiquen los mensajes de modo que los puedan conservar durante un tiempo determinado.</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">Administración de registros de mensajes</a></p></td>
</tr>
<tr class="even">
<td><p>Archivo en contexto</p></td>
<td><p>El <em>archivo en contexto</em> permite recuperar el control de los datos de mensajería de la organización mediante la eliminación de los archivos de almacenamiento personal (.pst), lo que permite a los usuarios almacenar mensajes en un <em>buzón de archivo</em> al que se puede tener acceso desde Outlook 2010 o posterior y Outlook Web App.</p></td>
<td><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Archivado local en Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Retención en contexto</p></td>
<td><p>Cuando existen sospechas fundadas de posibles litigios, se solicita a las organizaciones que conserven toda la información almacenada electrónicamente (ESI), incluso el correo electrónico que sea relevante para el caso. La retención en contexto permite buscar y conservar los mensajes que coinciden con los parámetros de consulta. Los mensajes se protegen de la eliminación, modificación o alteración y se pueden conservar de manera indefinida o durante un período de tiempo específico.</p></td>
<td><p><a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Conservación local y retención por juicio</a></p></td>
</tr>
<tr class="even">
<td><p>Exhibición de documentos electrónicos en contexto</p></td>
<td><p>La exhibición de documentos electrónicos en contexto permite buscar datos en buzones en la organización de Exchange, obtener una vista previa de los resultados de la búsqueda y copiarlos en un buzón de detección.</p></td>
<td><p><a href="in-place-ediscovery-exchange-2013-help.md">Exhibición de documentos electrónicos en contexto</a></p></td>
</tr>
<tr class="odd">
<td><p>Registro en diario</p></td>
<td><p>El registro en diario puede ayudar a la organización a responder a los requisitos de cumplimiento legal, normativo y organizativo mediante el registro de las comunicaciones de correo electrónico entrantes y salientes. Al planear la retención y el cumplimento normativo de mensajes, es importante comprender el registro en diario, cómo se adapta a las directivas de cumplimiento normativo de la organización y cómo Exchange 2013 permite asegurar los mensajes registrados en diario.</p></td>
<td><p><a href="journaling-exchange-2013-help.md">Registro en diario</a></p></td>
</tr>
<tr class="even">
<td><p>Transport Rules</p></td>
<td><p>Con las reglas de transporte puede buscar condiciones específicas para los mensajes que pasen por su organización y realizar acciones con ellos. Las reglas de transporte permiten aplicar directivas de mensajes a los mensajes de correo electrónico, asegurar mensajes, proteger sistemas de mensajes y evitar la fuga de información.</p></td>
<td><p><a href="mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md">Reglas de transporte o de flujo de correo</a></p></td>
</tr>
<tr class="odd">
<td><p>Prevención de pérdida de datos (DLP)</p></td>
<td><p>Las funcionalidades de DLP ayudan a proteger los datos confidenciales e informa a los usuarios en cuanto a las directivas y regulaciones. DLP también permite evitar que los usuarios envíen información confidencial por error a usuarios no autorizados. Al configurar directivas DLP, puede identificar y proteger los datos confidenciales mediante el análisis del contenido del sistema de mensajería, que incluye varios tipos de archivo asociados. Las plantillas de la directiva DLP suministradas en Exchange 2013 se basan en normas de regulación, como las normas de identificación de información personal (PII) o las normas de seguridad de datos del sector de tarjetas de pago (PCI-DSS). Las DLP se pueden ampliar, lo que permite incluir otras directivas importantes en su organización. Además, la nueva característica de sugerencias de directiva permite informar a los usuarios sobre infracciones de las directivas antes de que se envíen datos confidenciales.</p></td>
<td><p><a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">Prevención de pérdida de datos</a></p></td>
</tr>
<tr class="even">
<td><p>Information Rights Management (IRM)</p></td>
<td><p>Information Rights Management (IRM) ofrece una protección en línea o sin conexión persistente para los datos adjuntos y mensajes de correo electrónico que usen Active Directory Rights Management Services (AD RMS).</p></td>
<td><p><a href="information-rights-management-exchange-2013-help.md">Information Rights Management</a></p></td>
</tr>
<tr class="odd">
<td><p>S/MIME</p></td>
<td><p>Las extensiones seguras multipropósito al correo de Internet (S/MIME) permiten a los usuarios que tengan buzones de Office 365, Exchange 2013 y Exchange Online enviar correo electrónico firmado y cifrado dentro de su organización para ayudar a proteger la información confidencial. Para habilitar S/MIME para los buzones de Office 365, los administradores pueden sincronizar los certificados de usuario entre Office 365 y su servidor local y, después, configurar Outlook Online para que admita S/MIME.</p></td>
<td><p><a href="s-mime-for-message-signing-and-encryption-exchange-2013-help.md">S/MIME para la firma y el cifrado de mensajes</a></p></td>
</tr>
<tr class="even">
<td><p>Registro de auditoría de buzones de correo</p></td>
<td><p>Dado que los buzones de correo pueden contener información confidencial, información de alto impacto comercial (HBI) e información de identificación personal (PPI), es importante que realice un seguimiento de quién inicia sesión en los buzones de correo de su organización y las acciones que se llevan a cabo. Resulta especialmente importante que realice un seguimiento del acceso a los buzones por parte de usuarios que no sean los propietarios del buzón en cuestión (conocidos como usuarios delegados). Mediante el registro de auditoría de buzones de correo, podrá registrar el acceso a los buzones de correo por parte de sus propietarios, delegados (incluidos los administradores con permisos de acceso total al buzón) y administradores.</p></td>
<td><p><a href="mailbox-audit-logging-exchange-2013-help.md">Registro de auditoría de buzones de correo</a></p>
<p><a href="exchange-auditing-reports-exchange-2013-help.md">Informes de auditoría de Exchange</a></p></td>
</tr>
<tr class="odd">
<td><p>Registro de auditoría de administrador</p></td>
<td><p>Los registros de auditoría de administrador le permiten mantener un registro de los cambios realizados por los administradores a la configuración de los servidores Exchange y de la organización y a los destinatarios de Exchange. Es posible usar el registro de auditoría de administrador como parte del proceso de control de cambios o para registrar los cambios y el acceso a la configuración y los destinatarios para propósitos de cumplimiento.</p></td>
<td><p><a href="administrator-audit-logging-exchange-2013-help.md">Registro de auditoría de administrador</a></p></td>
</tr>
</tbody>
</table>

