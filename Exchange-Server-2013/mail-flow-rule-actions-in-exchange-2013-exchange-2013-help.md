---
title: 'Acciones de regla de transporte: Exchange 2013 Help'
TOCTitle: Acciones de las reglas de flujo de correo
ms:assetid: 5d11a955-b1cc-4150-a0b9-a8cc48ba9bde
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998315(v=EXCHG.150)
ms:contentKeyID: 49895658
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Acciones de regla de transporte

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-05-03_

Las acciones en las reglas de flujo de correo (también denominadas reglas de transporte) especifican lo que se desea hacer con los mensajes que cumplen las condiciones de la regla. Por ejemplo, puede crear una regla que reenvíe los mensajes de determinados remitentes a un moderador o agregue un aviso de declinación de responsabilidades o una firma personalizada a todos los mensajes salientes.

Las acciones suelen necesitar propiedades adicionales. Por ejemplo, cuando la regla redirige un mensaje, hay que especificar adónde debe redirigirse el mensaje. Algunas acciones tienen varias propiedades que están disponibles o son necesarias. Por ejemplo, cuando la regla agrega un campo de encabezado al encabezado del mensaje, hay que especificar el nombre y el valor del encabezado. Cuando la regla agrega un aviso de declinación de responsabilidades a los mensajes, es necesario especificar el texto del aviso, pero también puede especificar dónde desea insertar el texto o qué hacer si no se puede agregar el aviso de declinación de responsabilidades al mensaje. Normalmente, puede configurar varias acciones en una regla, pero algunas acciones son excluyentes. Por ejemplo, una regla no se puede rechazar y redirigir el mismo mensaje.

Para obtener más información acerca de las reglas de flujo de correo en Exchange Server 2013, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

Para obtener más información acerca de las condiciones y excepciones en las reglas de flujo de correo, consulte [Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Para obtener más información acerca de las acciones en las reglas de flujo de correo en Exchange Online o Exchange Online Protection, consulte [Enviar por correo las acciones de regla de flujo de Exchange Online](https://technet.microsoft.com/es-es/library/jj919237\(v=exchg.150\)) o [Mail acciones de regla de flujo de Exchange Online Protection](https://technet.microsoft.com/es-es/library/jj920117\(v=exchg.150\)).

## Acciones para reglas de flujo de correo en servidores de buzones

En la siguiente tabla, se describen las acciones que están disponibles en las reglas de flujo de correo en servidores de buzones. Los valores válidos para cada propiedad se describen en la sección de valores de propiedad .

**Notas**:

  - Después de seleccionar una acción en el Centro de administración de Exchange (EAC), el valor que finalmente se muestra en el campo **Hacer lo siguiente** suele ser diferente de la ruta de acceso de clic seleccionada. Además, al crear reglas, dependiendo de las selecciones que haga, a veces puede seleccionar un nombre corto de acción en una plantilla (una lista filtrada de acciones) en lugar de seguir la ruta de acceso de clic completa. Los nombres cortos y los valores de ruta de acceso de clic completa se muestran en la columna EAC de la tabla.

  - Los nombres de algunas de las acciones que devuelve el cmdlet **Get-TransportRuleAction** son diferentes de los nombres de parámetro correspondientes y es posible que una acción requiera varios parámetros.


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
<th>Acción en el EAC</th>
<th>Parámetro de acción en el Shell de administración de Exchange</th>
<th>Propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Reenviar el mensaje para su aprobación a estas personas</strong></p>
<p><strong>Reenviar el mensaje para su aprobación</strong> &gt; <strong>a estas personas</strong></p></td>
<td><p><em>ModerateMessageByUser</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Reenvía el mensaje a los moderadores especificados como datos adjuntos envuelto en una solicitud de aprobación. Para obtener más información, consulte <a href="common-message-approval-scenarios-exchange-2013-help.md">Escenarios comunes de aprobación de mensajes</a>. No puede utilizar un grupo de distribución como un moderador.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Reenviar el mensaje para su aprobación al administrador del remitente</strong></p>
<p><strong>Reenviar el mensaje para su aprobación</strong> &gt; <strong>al administrador del remitente</strong></p></td>
<td><p><em>ModerateMessageByManager</em></p></td>
<td><p>N/D</p></td>
<td><p>Reenvía el mensaje para su aprobación al administrador del remitente.</p>
<p>Esta acción solo funciona si el atributo <strong>Manager</strong> del remitente se define en Active Directory. De lo contrario, el mensaje se entrega a los destinatarios sin moderación.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Redirigir el mensaje a estos destinatarios</strong></p>
<p><strong>Redirigir el mensaje a</strong> &gt; <strong>estos destinatarios</strong></p></td>
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Redirige el mensaje a los destinatarios especificados. El mensaje no se entrega a los destinatarios originales y no se envía ninguna notificación al remitente ni a los destinatarios originales.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Rechazar el mensaje con la explicación</strong></p>
<p><strong>Bloquear el mensaje</strong> &gt; <strong>rechazar el mensaje e incluir una explicación</strong>.</p></td>
<td><p><em>RejectMessageReasonText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Devuelve el mensaje al remitente en un informe de no entrega (también denominado mensaje NDR o de devolución) con el texto especificado como el motivo del rechazo. El destinatario no recibe el mensaje original ni la notificación.</p>
<p>El código de estado mejorado que se usa es <code>5.7.1</code>.</p>
<p>Al crear o modificar la regla en el Shell de administración de Exchange, puede especificar el código de DSN mediante el parámetro <em>RejectMessageEnhancedStatusCode</em>.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rechazar el mensaje con el código de estado mejorado</strong></p>
<p><strong>Bloquear el mensaje</strong> &gt; <strong>rechazar el mensaje con el código de estado mejorado de</strong></p></td>
<td><p><em>RejectMessageEnhancedStatusCode</em></p></td>
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>Devuelve el mensaje al remitente en un NDR con el código de Notificación de estado de entrega (DSN) mejorado que se especifique. El destinatario no recibe el mensaje original ni la notificación.</p>
<p>Los códigos de DSN válidos son <code>5.7.1</code> o de <code>5.7.900</code> a <code>5.7.999</code>.</p>
<p>El texto de motivo predeterminado que se usa es <code>Delivery not authorized, message refused</code>.</p>
<p>Al crear o modificar la regla en el Shell de administración de Exchange, puede especificar el texto de motivo del rechazo mediante el parámetro <em>RejectMessageReasonText</em>.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Eliminar el mensaje sin notificarlo a nadie</strong></p>
<p><strong>Bloquear el mensaje</strong> &gt; <strong>eliminar el mensaje sin notificar a nadie</strong></p></td>
<td><p><em>DeleteMessage</em></p></td>
<td><p>N/D</p></td>
<td><p>Elimina el mensaje de correo electrónico sin enviar ninguna notificación al destinatario ni al remitente.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agregar destinatarios en el cuadro CCO</strong></p>
<p><strong>Agregar destinatarios</strong> &gt; <strong>en el cuadro CCO</strong></p></td>
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Agrega uno o más destinatarios al campo <strong>Bcc</strong> del mensaje. Los destinatarios originales no reciben una notificación y no pueden ver las direcciones adicionales.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Agregar destinatarios en el cuadro Para</strong></p>
<p><strong>Agregar destinatarios</strong> &gt; <strong>en el cuadro Para</strong></p></td>
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Agrega uno o más destinatarios al campo <strong>To</strong> del mensaje. Los destinatarios originales pueden ver las direcciones adicionales.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agregar destinatarios en el cuadro CC</strong></p>
<p><strong>Agregar destinatarios</strong> &gt; <strong>en el cuadro CC</strong></p></td>
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Agrega uno o más destinatarios al campo <strong>Cc</strong> del mensaje. Los destinatarios originales pueden ver la dirección adicional.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Agregar el administrador del remitente como un destinatario</strong></p>
<p><strong>Agregar destinatarios</strong> &gt; <strong>agregar el administrador del remitente como un destinatario</strong></p></td>
<td><p><em>AddManagerAsRecipientType</em></p></td>
<td><p><code>AddedManagerAction</code></p></td>
<td><p>Agrega el administrador del remitente al mensaje como el tipo de destinatario especificado (<strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong>) o redirige el mensaje al administrador del remitente sin notificar al remitente ni al destinatario.</p>
<p>Esta acción solo funciona si el atributo <strong>Manager</strong> del remitente se define en Active Directory.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Anexar un aviso de exención de responsabilidad</strong></p>
<p><strong>Aplicar una declinación de responsabilidad al mensaje</strong> &gt; <strong>adjuntar una renuncia de responsabilidad</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>Primera propiedad: <code>DisclaimerText</code></p>
<p>Segunda propiedad: <code>DisclaimerFallbackAction</code></p>
<p>Tercera propiedad (solo Shell de administración de Exchange): <code>DisclaimerTextLocation</code></p></td>
<td><p>Aplica el aviso de declinación de responsabilidades HTML especificado al final del mensaje.</p>
<p>Al crear o modificar la regla en el Shell de administración de Exchange, use el parámetro <em>ApplyHtmlDisclaimerTextLocation</em> con el valor <code>Append</code>.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Anteponer un aviso de exención de responsabilidad</strong></p>
<p><strong>Aplicar una declinación de responsabilidad al mensaje</strong> &gt; <strong>anteponer una renuncia de responsabilidad</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>Primera propiedad: <code>DisclaimerText</code></p>
<p>Segunda propiedad: <code>DisclaimerFallbackAction</code></p>
<p>Tercera propiedad (solo Shell de administración de Exchange): <code>DisclaimerTextLocation</code></p></td>
<td><p>Aplica el aviso de declinación de responsabilidades HTML especificado al principio del mensaje.</p>
<p>Al crear o modificar la regla en el Shell de administración de Exchange, use el parámetro <em>ApplyHtmlDisclaimerTextLocation</em> con el valor <code>Prepend</code>.</p>
<p></p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Quitar este encabezado</strong></p>
<p><strong>Modificar propiedades del mensaje</strong> &gt; <strong>eliminar un encabezado de mensaje</strong>.</p></td>
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Quita el campo de encabezado especificado del encabezado del mensaje.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Establecer el encabezado de mensaje en este valor</strong></p>
<p><strong>Modificar propiedades del mensaje</strong> &gt; <strong>establecer un encabezado de mensaje</strong></p></td>
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>Primera propiedad: <code>MessageHeaderField</code></p>
<p>Segunda propiedad: <code>String</code></p></td>
<td><p>Agrega o modifica el campo de encabezado especificado en el encabezado del mensaje y establece el campo de encabezado en el valor especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Aplicar una clasificación de mensajes</strong></p>
<p><strong>Modificar propiedades del mensaje</strong> &gt; <strong>aplicar una clasificación de mensaje</strong></p></td>
<td><p><em>ApplyClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>Aplica la clasificación de mensaje especificada al mensaje.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Establecer el nivel de confianza contra correo no deseado (SCL) en</strong></p>
<p><strong>Modificar propiedades del mensaje</strong> &gt; <strong>establecer el nivel de confianza de correo no deseado (SCL)</strong>.</p></td>
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Establece el nivel de confianza contra correo no deseado (SCL) del mensaje en el valor especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Aplicar la protección de derechos al mensaje con</strong></p>
<p><strong>Modificar la seguridad de los mensajes</strong> &gt; <strong>aplicar protección de derechos</strong></p></td>
<td><p><em>ApplyRightsProtectionTemplate</em></p></td>
<td><p><code>RMSTemplate</code></p></td>
<td><p>Aplica al mensaje la plantilla de Rights Management Services (RMS) especificada.</p>
<p>RMS requiere licencias de acceso de cliente (CAL) de Exchange Enterprise para cada buzón. Para obtener más información sobre las CAL, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Concesión de licencias de Exchange Server</a>.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Requerir cifrado TLS</strong></p>
<p><strong>Modificar la seguridad de los mensajes</strong> &gt; <strong>Requerir cifrado TLS</strong></p></td>
<td><p><em>RouteMessageOutboundRequireTls</em></p></td>
<td><p><code>n/a</code></p></td>
<td><p>Fuerza el enrutamiento de los mensajes salientes a través de conexiones cifradas TLS.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Anteponer al asunto del mensaje</strong></p></td>
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Agrega el texto especificado al principio del campo <strong>Subject</strong> del mensaje. Considere la posibilidad de usar un espacio o un signo de dos puntos (:) como último carácter del texto especificado para diferenciarlo del texto del asunto original.</p>
<p>Para evitar que se agregue la misma cadena a mensajes que ya contienen el texto en el asunto (por ejemplo, respuestas), agregue la excepción <strong>El asunto incluye</strong> (<em>ExceptIfSubjectContainsWords</em>) a la regla.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Notificar al remitente con una sugerencia de directiva</strong></p></td>
<td><p><em>NotifySender</em></p>
<p><em>RejectMessageReasonText</em></p>
<p><em>RejectMessageEnhancedStatusCode</em> (solo Shell de administración de Exchange)</p></td>
<td><p>Primera propiedad: <code>NotifySenderType</code></p>
<p>Segunda propiedad: <code>String</code></p>
<p>Tercera propiedad (solo Shell de administración de Exchange): <code>DSNEnhancedStatusCode</code></p></td>
<td><p>Notifica al remitente o bloquea el mensaje cuando el mensaje coincide con una directiva DLP.</p>
<p>Cuando use esta acción, debe usar la condición <strong>(</strong>El mensaje incluye información confidencial<em>MessageContainsDataClassification</em>).</p>
<p>Al crear o modificar la regla en el Shell de administración de Exchange, el parámetro <em>RejectMessageReasonText</em> es opcional. Si no usa este parámetro, se usará el texto predeterminado <code>Delivery not authorized, message refused</code>.</p>
<p>En el Shell de administración de Exchange, puede usar también el parámetro <em>RejectMessageEnhancedStatusCode</em> para especificar el código de estado mejorado. Si no usa este parámetro, se usará el código de estado mejorado predeterminado <code>5.7.1</code>.</p>
<p>Esta acción limita las demás condiciones, excepciones y acciones que se pueden configurar en la regla.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Generar informe de incidentes y enviarlo a</strong></p></td>
<td><p><em>GenerateIncidentReport</em></p>
<p><em>IncidentReportContent</em></p></td>
<td><p>Primera propiedad: <code>Addresses</code></p>
<p>Segunda propiedad: <code>IncidentReportContent</code></p></td>
<td><p>Envía un informe de incidentes con el contenido especificado a los destinatarios especificados.</p>
<p>Estos informes se generan para los mensajes que coincidan con directivas de prevención de pérdida de datos (DLP) de la organización.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Notificar al destinatario con un mensaje</strong></p></td>
<td><p><em>GenerateNotification</em></p></td>
<td><p><code>NotificationMessageText</code></p></td>
<td><p>Especifica el texto, las etiquetas HTML y las palabras clave del mensaje que se incluyen en el mensaje de notificación que se envía a los destinatarios del mensaje. Por ejemplo, puede notificar a los destinatarios que la regla rechazó un mensaje o que un mensaje se marcó como correo no deseado y se envió a la carpeta de correo no deseado.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="odd">
<td><p>Sección <strong>Propiedades de esta regla</strong> &gt; <strong>Auditar esta regla con el nivel de gravedad</strong></p></td>
<td><p><em>SetAuditSeverity</em></p></td>
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>Especifica si se debe:</p>
<ul>
<li><p>Evitar la generación de un informe de incidentes y la entrada correspondiente en el registro de seguimiento de mensajes.</p></li>
<li><p>Generar un informe de incidentes y la entrada correspondiente en el registro de seguimiento de mensajes con el nivel de gravedad especificado (alta, media o baja).</p></li>
</ul></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="even">
<td><p>Sección <strong>Propiedades de esta regla</strong> &gt; <strong>Detener el procesamiento de más reglas</strong></p>
<p><strong>Más opciones</strong> &gt; <strong>sección Propiedades de esta regla</strong> &gt; <strong>Detener el procesamiento de más reglas</strong></p></td>
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>N/D</p></td>
<td><p>Especifica que el mensaje, una vez afectado por la regla, queda exento de procesamiento por otras reglas.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Acciones para reglas de flujo de correo en servidores de transporte perimetral

Un pequeño subconjunto de las acciones que están disponibles en los servidores de buzones están también disponibles en los servidores de transporte perimetral, pero también hay algunas acciones que solo están disponibles en los servidores de transporte perimetral. No hay ningún EAC en servidores de transporte perimetral, por lo que solo puede administrar reglas de flujo de correo en el Shell de administración de Exchange del servidor de transporte perimetral local. Las acciones se describen en la siguiente tabla. Los tipos de propiedades se describen en la sección Valores de la propiedad.


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
<th>Parámetro de acción en el Shell de administración de Exchange</th>
<th>Propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Agrega uno o más destinatarios al campo <strong>To</strong> del mensaje. Los destinatarios originales pueden ver las direcciones adicionales.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Agrega uno o más destinatarios al campo <strong>Bcc</strong> del mensaje. Los destinatarios originales no reciben una notificación y no pueden ver las direcciones adicionales.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Agrega uno o más destinatarios al campo <strong>Cc</strong> del mensaje. Los destinatarios originales pueden ver la dirección adicional.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>DeleteMessage</em></p></td>
<td><p>N/D</p></td>
<td><p>Elimina el mensaje de correo electrónico sin enviar ninguna notificación al destinatario ni al remitente.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>Disconnect</em></p></td>
<td><p>N/D</p></td>
<td><p>Finaliza la conexión SMTP entre el servidor de envío y el servidor de transporte perimetral sin generar un mensaje NDR.</p></td>
<td><p>Solo servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>LogEventText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Genera un evento con el texto especificado en el registro de aplicaciones del servidor de transporte perimetral local. La entrada contiene la información siguiente:</p>
<ul>
<li><p><strong>Nivel</strong> <code>Information</code></p></li>
<li><p><strong>Origen</strong> <code>MSExchange Messaging Policies</code></p></li>
<li><p><strong>Id. de evento</strong> <code>4000</code></p></li>
<li><p><strong>Categoría de la tarea</strong> <code>Rules</code></p></li>
<li><p><strong>EventData</strong>   <code>The following message is logged by an action in the rules: &lt;text you specify&gt;.</code></p></li>
</ul></td>
<td><p>Solo servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Agrega el texto especificado al principio del campo <strong>Subject</strong> del mensaje. Considere la posibilidad de usar un espacio o un signo de dos puntos (:) como último carácter del texto especificado para diferenciarlo del asunto original.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>Quarantine</em></p></td>
<td><p>N/D</p></td>
<td><p>Entrega el mensaje al buzón de cuarentena que se define en la configuración de filtrado de contenido en el servidor de transporte perimetral. Para obtener más información, consulte <a href="configure-a-spam-quarantine-mailbox-exchange-2013-help.md">Configurar un buzón de cuarentena de correo no deseado</a>.</p>
<p>Si el buzón de cuarentena no está configurado, el mensaje se devuelve al remitente en un NDR.</p></td>
<td><p>Solo servidores de transporte perimetral</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Redirige el mensaje a los destinatarios especificados. El mensaje no se entrega a los destinatarios originales y no se envía ninguna notificación al remitente ni a los destinatarios originales.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Quita el campo de encabezado especificado del encabezado del mensaje.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>Primera propiedad: <code>MessageHeaderField</code></p>
<p>Segunda propiedad: <code>String</code></p></td>
<td><p>Agrega o modifica el campo de encabezado especificado en el encabezado del mensaje y establece el campo de encabezado en el valor especificado.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Establece el SCL del mensaje en el valor especificado.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>SmtpRejectMessageRejectText</em></p>
<p><em>SmtpRejectMessageRejectStatusCode</em></p></td>
<td><p>Primera propiedad: <code>String</code></p>
<p>Segunda propiedad: <code>SMTPStatusCode</code></p></td>
<td><p>Termina la conexión SMTP entre el servidor de envío y el servidor de transporte perimetral con el código de estado de SMTP especificado y el texto de rechazo especificado. El destinatario no recibe el mensaje original ni la notificación.</p>
<p>Los valores válidos para el código de estado de SMTP son enteros de <code>400</code> a <code>500</code>, tal y como se definen en RFC 3463.</p>
<p>Si especifica el texto de rechazo sin especificar el código de estado de SMTP, se usará el código predeterminado <code>550</code>.</p>
<p>Si especifica el texto de rechazo sin especificar el código de estado de SMTP, el texto que se usará es <code>Delivery not authorized, message refused</code>.</p></td>
<td><p>Solo servidores de transporte perimetral</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>N/D</p></td>
<td><p>Especifica que el mensaje, una vez afectado por la regla, queda exento de procesamiento por otras reglas.</p></td>
<td><p>Servidores de buzones y servidores de transporte perimetral</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
</tbody>
</table>


## Valores de la propiedad

Los valores de propiedad que se utilizan en acciones de reglas de flujo de correo se describen en la tabla siguiente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propiedad</th>
<th>Valores válidos</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>AddedManagerAction</code></p></td>
<td><p>Uno de los siguientes valores:</p>
<ul>
<li><p><strong>Para</strong></p></li>
<li><p><strong>CC</strong></p></li>
<li><p><strong>CCO</strong></p></li>
<li><p><strong>Redirigir</strong></p></li>
</ul></td>
<td><p>Especifica cómo incluir al administrador del remitente en los mensajes.</p>
<ul>
<li><p>Si selecciona <strong>Para</strong>, <strong>CC</strong> o <strong>CCO</strong>, el administrador del remitente se agrega como destinatario en el campo especificado.</p></li>
<li><p>Si selecciona <strong>Redirigir</strong>, el mensaje solo se entrega al administrador del remitente sin notificar al remitente ni al destinatario.</p></li>
</ul>
<p>Esta acción solo funciona si el atributo <strong>Manager</strong> del remitente se define en Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Destinatarios de Exchange</p></td>
<td><p>Según la acción, es posible que pueda especificar cualquier objeto habilitado para correo en la organización o puede limitarse a un tipo de objeto específico. Normalmente, puede seleccionar varios destinatarios, pero solo puede enviar un informe de incidentes a un destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>Uno de los siguientes valores:</p>
<ul>
<li><p>Desactive <strong>Auditar esta regla con el nivel de gravedad</strong> o seleccione <strong>Auditar esta regla con el nivel de gravedad</strong> con el valor <strong>No especificado</strong> (<code>DoNotAudit</code>)</p></li>
<li><p><strong>Baja</strong></p></li>
<li><p><strong>Media</strong></p></li>
<li><p><strong>Alta</strong></p></li>
</ul></td>
<td><p>Los valores <strong>Baja</strong>, <strong>Media</strong> o <strong>Alta</strong> especifican el nivel de gravedad que se asigna en el informe de incidentes y en la entrada correspondiente del registro de seguimiento de mensajes.</p>
<p>El otro valor impide que se genere un informe de incidentes y evita que se escriba la entrada correspondiente en el registro de seguimiento de mensajes.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerFallbackAction</code></p></td>
<td><p>Uno de los siguientes valores:</p>
<ul>
<li><p><strong>Ajustar</strong></p></li>
<li><p><strong>ignorar</strong></p></li>
<li><p><strong>Rechazar</strong></p></li>
</ul></td>
<td><p>Especifica lo que hay que hacer cuando el aviso de declinación de responsabilidades no se puede aplicar a un mensaje. Hay situaciones en las que el contenido de un mensaje no se puede modificar (por ejemplo, el mensaje está cifrado). Las acciones de reserva disponibles son las siguientes:</p>
<ul>
<li><p><strong>Ajustar</strong>: el mensaje original se ajusta en un nuevo sobre de mensajes y el texto del aviso de declinación de responsabilidades se inserta en el nuevo mensaje. Este es el valor predeterminado.</p>
<p><strong>Notas</strong>:</p>
<ul>
<li><p>Las reglas de flujo de correo posteriores se aplicarán al nuevo sobre de mensajes y no al mensaje original. Por lo tanto, deberá configurar estas reglas con una prioridad menor que la de las demás.</p></li>
<li><p>El mensaje original no se entrega si no se puede ajustar en un nuevo sobre de mensajes. Se devolverá al remitente en un NDR.</p></li>
</ul></li>
<li><p><strong>Ignorar</strong>: la regla se ignorará y el mensaje se entregará sin el aviso de declinación de responsabilidades.</p></li>
<li><p><strong>Rechazar</strong>: el mensaje se devolverá al remitente en un NDR.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DisclaimerText</code></p></td>
<td><p>Cadena HTML</p></td>
<td><p>Especifica el texto del aviso de declinación de responsabilidades, que puede incluir etiquetas HTML, etiquetas de hoja de estilo en cascada (CSS) en línea e imágenes mediante la etiqueta IMG. La longitud máxima es de 5000 caracteres.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerTextLocation</code></p></td>
<td><p>Valor único: <code>Append</code> o <code>Prepend</code></p></td>
<td><p>En el Shell de administración de Exchange, el <em>ApplyHtmlDisclaimerTextLocation</em> se usa para especificar la ubicación del texto del aviso de declinación de responsabilidades en el mensaje:</p>
<ul>
<li><p><code>Append</code>   Agregar el aviso de declinación de responsabilidades al final del cuerpo del mensaje. Este es el valor predeterminado.</p></li>
<li><p><code>Prepend</code>   Agregar el aviso de declinación de responsabilidades al principio del cuerpo del mensaje.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>Valor único de código de DSN:</p>
<ul>
<li><p><code>5.7.1</code></p></li>
<li><p>De <code>5.7.900</code> a <code>5.7.999</code></p></li>
</ul></td>
<td><p>Especifica el código de DSN que se utiliza. Puede crear DSN personalizados con el cmdlet <strong>New-SystemMessage</strong>.</p>
<p>Si no se especifica el texto del motivo de rechazo junto con el código de DSN, el texto de motivo predeterminado que se usa es <code>Delivery not authorized, message refused</code>.</p>
<p>Al crear o modificar la regla en el Shell de administración de Exchange, puede especificar el texto de motivo del rechazo mediante el parámetro <em>RejectMessageReasonText</em>.</p></td>
</tr>
<tr class="even">
<td><p><code>IncidentReportContent</code></p></td>
<td><p>Uno o varios de los siguientes valores:</p>
<ul>
<li><p><strong>Remitente</strong></p></li>
<li><p><strong>Destinatarios</strong></p></li>
<li><p><strong>Asunto</strong></p></li>
<li><p><strong>Destinatarios en CC</strong> (<code>Cc</code>)</p></li>
<li><p><strong>Destinatarios en CCO</strong> (<code>Bcc</code>)</p></li>
<li><p><strong>Gravedad</strong></p></li>
<li><p><strong>Información de reemplazo del remitente</strong> (<code>Override</code>)</p></li>
<li><p><strong>Reglas coincidentes</strong> (<code>RuleDetections</code>)</p></li>
<li><p><strong>Informes de falsos positivos</strong> (<code>FalsePositive</code>)</p></li>
<li><p><strong>Incluir clasificaciones de datos</strong> (<code>DataClassifications</code>)</p></li>
<li><p><strong>Contenido coincidente</strong> (<code>IdMatch</code>)</p></li>
<li><p><strong>Correo original</strong> (<code>AttachOriginalMail</code>)</p></li>
</ul></td>
<td><p>Especifica las propiedades del mensaje original que se van a incluir en el informe de incidentes. También puede incluir una combinación de estas propiedades. Además de las propiedades que especifique, siempre se incluye el identificador del mensaje. Las propiedades disponibles son las siguientes:</p>
<ul>
<li><p><strong>Remitente</strong>   El remitente del mensaje original.</p></li>
<li><p><strong>Destinatarios</strong>, <strong>destinatarios en CC</strong> y <strong>Destinatarios en CCO</strong>   Todos los destinatarios del mensaje o solo los destinatarios de los campos <strong>Cc</strong> o <strong>Bcc</strong>. Para cada propiedad, solo los 10 primeros destinatarios se incluyen en el informe de incidentes.</p></li>
<li><p><strong>Asunto</strong>   El campo <strong>Subject</strong> del mensaje original.</p></li>
<li><p><strong>Gravedad</strong>   La gravedad de auditoría de la regla que se activó. Los registros de seguimiento de mensajes incluyen todos los niveles de gravedad de auditoría y se pueden filtrar por gravedad de auditoría. En el EAC, si desactiva la casilla <strong>Auditar esta regla con el nivel de gravedad</strong> (en el Shell de administración de Exchange, el valor del parámetro <em>SetAuditSeverity</em>, <code>DoNotAudit</code>), las coincidencias de regla no aparecerán en los informes de la regla. Si un mensaje es procesado por más de una regla, se incluye la gravedad más alta en los informes de incidentes.</p></li>
<li><p><strong>Información de reemplazo del remitente</strong>   El reemplazo si el remitente decidió reemplazar una sugerencia de directiva. Si el remitente especificó una justificación, se incluyen también los 100 primeros caracteres de la justificación.</p></li>
<li><p><strong>Reglas coincidentes</strong>   La lista de reglas que el mensaje activó.</p></li>
<li><p><strong>Informes de falsos positivos</strong>   El falso positivo si el remitente marcó el mensaje como falso positivo con respecto a una sugerencia de directiva.</p></li>
<li><p><strong>Incluir clasificaciones de datos</strong>   La lista de tipos de información confidencial detectados en el mensaje.</p></li>
<li><p><strong>Coincidencia de contenido</strong>   El tipo de información confidencial detectado, el contenido exacto que coincide con el mensaje y los 150 caracteres anteriores y posteriores a la información identificada como confidencial.</p></li>
<li><p><strong>Correo original</strong>   El mensaje completo que activó la regla se adjunta al informe de incidentes.</p></li>
</ul>
<p>En el Shell de administración de Exchange, puede especificar varios valores separados por comas.</p></td>
</tr>
<tr class="odd">
<td><p><code>MessageClassification</code></p></td>
<td><p>Único objeto de clasificación de mensaje</p></td>
<td><p>En el EAC, selecciónelo en la lista de clasificaciones de mensajes disponibles.</p>
<p>En el Shell de administración de Exchange, use el cmdlet <strong>Get-MessageClassification</strong> para ver los objetos de clasificación de mensajes que están disponibles.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Una única cadena</p></td>
<td><p>Especifica el campo de encabezado de mensaje de SMTP que se agrega, quita o modifica.</p>
<p>El <em>encabezado del mensaje</em> es una colección de campos de encabezado obligatorios y opcionales del mensaje. Por ejemplo, <strong>To</strong>, <strong>From</strong>, <strong>Received</strong> y <strong>Content-Type</strong> son campos de encabezado. Los campos de encabezado oficiales están definidos en RFC 5322. Los campos de encabezado extraoficiales comienzan por <strong>X-</strong> y se denominan <em>encabezados X</em>.</p></td>
</tr>
<tr class="odd">
<td><p><code>NotificationMessageText</code></p></td>
<td><p>Cualquier combinación de texto sin formato, etiquetas HTML y palabras clave</p></td>
<td><p>Especifica el texto que se usa en un mensaje de notificación de destinatarios.</p>
<p>Además de texto sin formato y etiquetas HTML, puede especificar las siguientes palabras clave que usan valores del mensaje original:</p>
<ul>
<li><p><code>%%From%%</code></p></li>
<li><p><code>%%To%%</code></p></li>
<li><p><code>%%Cc%%</code></p></li>
<li><p><code>%%Subject%%</code></p></li>
<li><p><code>%%Headers%%</code></p></li>
<li><p><code>%%MessageDate%%</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>NotifySenderType</code></p></td>
<td><p>Uno de los siguientes valores:</p>
<ul>
<li><p><strong>Notificar al remitente, pero permitirles realizar envíos</strong> (<code>NotifyOnly</code>)</p></li>
<li><p><strong>Bloquear el mensaje</strong> (<code>RejectMessage</code>)</p></li>
<li><p><strong>Bloquear el mensaje a menos que sea un falso positivo</strong> (<code>RejectUnlessFalsePositiveOverride</code>)</p></li>
<li><p><strong>Bloquear el mensaje, pero permitir al remitente invalidarlo y enviarlo</strong> (<code>RejectUnlessSilentOverride</code>)</p></li>
<li><p><strong>Bloquear el mensaje, pero permitir al remitente invalidarlo con una justificación comercial y enviarlo</strong> (<code>RejectUnlessExplicitOverride</code>)</p></li>
</ul></td>
<td><p>Especifica el tipo de sugerencia de directiva que el remitente recibe si el mensaje infringe una directiva DLP. Las opciones de configuración se describen en la lista siguiente:</p>
<ul>
<li><p><strong>Notificar al remitente, pero permitirles realizar envíos</strong>: se notifica al remitente pero el mensaje se entrega normalmente.</p></li>
<li><p><strong>Bloquear el mensaje</strong>   Se rechaza el mensaje y se notifica al remitente.</p></li>
<li><p><strong>Bloquear el mensaje a menos que sea un falso positivo</strong>   El mensaje se rechaza a menos que el remitente lo haya marcado como falso positivo.</p></li>
<li><p><strong>Bloquear el mensaje, pero permitir al remitente invalidarlo y enviarlo</strong>   El mensaje se rechaza a menos que el remitente haya decidido invalidar la restricción de la directiva.</p></li>
<li><p><strong>Bloquear el mensaje, pero permitir al remitente invalidarlo con una justificación comercial y enviarlo</strong>   Es similar al tipo <strong>Bloquear el mensaje, pero permitir al remitente invalidarlo y enviarlo</strong>, pero el remitente también proporciona una justificación para invalidar la restricción de directiva.</p></li>
</ul>
<p>Cuando use esta acción, debe usar la condición <strong>El mensaje incluye información confidencial</strong> (<em>MessageContainsDataClassification</em>).</p></td>
</tr>
<tr class="odd">
<td><p><code>RMSTemplate</code></p></td>
<td><p>Único objeto de plantilla de RMS</p></td>
<td><p>Especifica la plantilla de Rights Management Services (RMS) que se aplica al mensaje.</p>
<p>En el EAC, seleccione la plantilla de RMS de una lista.</p>
<p>En el Shell de administración de Exchange, use el cmdlet <strong>Get-RMSTemplate</strong> para ver las plantillas de RMS que están disponibles.</p>
<p>RMS requiere licencias de acceso de cliente (CAL) de Exchange Enterprise para cada buzón. Para obtener más información sobre las CAL, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Concesión de licencias de Exchange Server</a>.</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>Uno de los siguientes valores:</p>
<ul>
<li><p><strong>Omitir el filtrado de correo no deseado</strong> (<code>-1</code>)</p></li>
<li><p>Enteros (0 - 9)</p></li>
</ul></td>
<td><p>Especifica el nivel de confianza contra correo no deseado (SCL) asignado al mensaje. Un valor SCL alto indica que el mensaje tiene más posibilidades de ser correo no deseado.</p></td>
</tr>
<tr class="odd">
<td><p><code>String</code></p></td>
<td><p>Una única cadena</p></td>
<td><p>Especifica el texto que se aplica a la entrada del registro de eventos, el NDR o el campo de encabezado del mensaje especificado.</p>
<p>En el Shell de administración de Exchange, si el valor contiene espacios, escriba el valor entre comillas (&quot;).</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Más información

[Administrar reglas de flujo de correo](manage-mail-flow-rules-exchange-2013-help.md)

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Enviar por correo las acciones de regla de flujo de Exchange Online](https://technet.microsoft.com/es-es/library/jj919237\(v=exchg.150\)) por Exchange Online

[Mail acciones de regla de flujo de Exchange Online Protection](https://technet.microsoft.com/es-es/library/jj920117\(v=exchg.150\)) para Exchange Online Protection

[Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización en Office 365](https://technet.microsoft.com/es-es/library/dn600323\(v=exchg.150\))

