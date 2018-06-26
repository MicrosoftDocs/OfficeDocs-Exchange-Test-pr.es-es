---
title: 'Conservar los destinatarios de grupos de distribución expandidos y CCO para la exhibición de documentos electrónicos: Exchange 2013 Help'
TOCTitle: Conservar los destinatarios de grupos de distribución expandidos y CCO para la exhibición de documentos electrónicos
ms:assetid: eb8ddf15-0080-457e-9d83-e73e193da334
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn770225(v=EXCHG.150)
ms:contentKeyID: 62516670
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conservar los destinatarios de grupos de distribución expandidos y CCO para la exhibición de documentos electrónicos

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**Última modificación del tema:**2017-06-19_

Mantenga en el lugar, retención para litigios y [las políticas de retención de Office 365](http://go.microsoft.com/fwlink/?linkid=827811) (creado en el Centro de seguridad y cumplimiento de Office 365 ) permiten conservar el contenido del buzón para satisfacer los requerimientos de eDiscovery y cumplimiento reglamentario. Información acerca de los destinatarios directamente tratada en para y Cc campos de un mensaje se incluye en todos los mensajes de forma predeterminada, pero su organización requiera la capacidad para buscar y reproducir detalles acerca de todos los destinatarios de un mensaje. Esto incluye:

  - **Destinatarios a los que se dirigió mediante el campo CCO de un mensaje:** los destinatarios CCO se almacenan en el mensaje en el buzón de correo del remitente, pero no se incluyen en los encabezados del mensaje que se entrega a los destinatarios.

  - **Destinatarios del grupo de distribución expandido:** destinatarios que reciben el mensaje porque son miembros de un grupo de distribución al que estaba dirigido el mensaje, ya sea en los campos Para, CC o CCO.

Exchange Online y Exchange Server 2013 (actualización acumulativa 7 y versiones posteriores) conservan la información acerca de CCO y los destinatarios del grupo de distribución expandidas. Puede buscar esta información mediante una búsqueda de eDiscovery In situ en el Centro de administración de Exchange (CEF) o una búsqueda de contenido en el Centro de seguridad y cumplimiento.

## Forma de conservación de los destinatarios CCO y los destinatarios del grupo de distribución expandido

Como se indicó anteriormente, se almacena información acerca de los destinatarios de Bcc'ed con el mensaje en el buzón del remitente. Esta información está indizada y disponible para búsquedas de eDiscovery y suspensiones.

Información acerca de los destinatarios del grupo de distribución expandido se almacena con el mensaje después de colocar un buzón en mantenga In situ o retención para litigios. En Office 365, esta información también se almacena cuando se aplica una política de retención de Office 365 a un buzón. Pertenencia a grupos de distribución se determina en el momento en que se envía el mensaje. La lista expandida de destinatarios almacenada con el mensaje no se ve afectada por los cambios en la pertenencia del grupo después de enviar el mensaje.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>La información sobre...</th>
<th>se almacena en...</th>
<th>¿se almacena de forma predeterminada?</th>
<th>es accesible para...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Destinatarios de Para y CC</p></td>
<td><p>Propiedades del mensaje en los buzones de correo del remitente y los destinatarios</p></td>
<td><p>Sí</p></td>
<td><p>Remitente, destinatarios y responsables de cumplimiento normativo</p></td>
</tr>
<tr class="even">
<td><p>Destinatarios CCO</p></td>
<td><p>Propiedad del mensaje en el buzón de correo del remitente</p></td>
<td><p>Sí</p></td>
<td><p>Remitente y responsables de cumplimento normativo</p></td>
</tr>
<tr class="odd">
<td><p>Destinatarios del grupo de distribución expandido</p></td>
<td><p>Propiedades del mensaje en el buzón de correo del remitente</p></td>
<td><p>No. Información de destinatarios de grupo de distribución expandido se almacenan una vez colocado un buzón en mantenga In situ o retención para litigios o asignado a una directiva de retención de Office 365.</p></td>
<td><p>Responsables de cumplimento normativo</p></td>
</tr>
</tbody>
</table>


## Buscar mensajes enviados a destinatarios CCO y del grupo de distribución expandido

Cuando se buscan mensajes enviados a un destinatario, los resultados de la búsqueda de exhibición de documentos electrónicos ahora incluyen los mensajes enviados a un grupo de distribución del que es miembro el destinatario. En la tabla siguiente se muestran los escenarios en los que los mensajes enviados a destinatarios CCO y del grupo de distribución ampliado se proporcionan en las búsquedas de exhibición de documentos electrónicos.

Escenario 1: John es miembro del grupo de distribución US-Sales En esta tabla se muestran los resultados de búsqueda de la exhibición de documentos electrónicos cuando Bob le envía un mensaje a John directamente o indirectamente mediante un grupo de distribución.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuando busca en el buzón de correo de Bob mensajes enviados...</th>
<th>Y el mensaje se envía con...</th>
<th>¿Los resultados incluyen el mensaje?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>To:John</p></td>
<td><p>John en TO</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>To:John</p></td>
<td><p>US-Sales en TO</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>To:US-Sales</p></td>
<td><p>US-Sales en TO</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Cc:John</p></td>
<td><p>John en CC</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Cc:John</p></td>
<td><p>US-Sales en CC</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Cc:US-Sales</p></td>
<td><p>US-Sales en CC</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


Escenario 2: Bob le envía un correo electrónico a John (Para/CC) y Jack (CCO directamente o indirectamente mediante un grupo de distribución). En la tabla siguiente se muestran los resultados de búsqueda de la exhibición de documentos electrónicos.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuando busca...</th>
<th>Para los mensajes enviados...</th>
<th>¿Los resultados incluyen el mensaje?</th>
<th>Notas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Buzón de correo de Bob</p></td>
<td><p>To/Cc:John</p></td>
<td><p>Sí</p></td>
<td><p>Presenta una indicación de que Jack se incluyó en CCO.</p></td>
</tr>
<tr class="even">
<td><p>Buzón de correo de Bob</p></td>
<td><p>Bcc:Jack</p></td>
<td><p>Sí</p></td>
<td><p>Presenta una indicación de que Jack se incluyó en CCO.</p></td>
</tr>
<tr class="odd">
<td><p>Buzón de correo de Bob</p></td>
<td><p>Bcc:Jack (mediante grupo de distribución)</p></td>
<td><p>Sí</p></td>
<td><p>La lista de miembros del grupo de distribución con CCO, que se expandió cuando se envió el mensaje, es visible en la vista previa de la búsqueda de la exhibición de documentos electrónicos, exportación y registros.</p></td>
</tr>
<tr class="even">
<td><p>Buzón de correo de John</p></td>
<td><p>To/Cc:John</p></td>
<td><p>Sí</p></td>
<td><p>Sin indicación de los destinatarios CCO.</p></td>
</tr>
<tr class="odd">
<td><p>Buzón de correo de John</p></td>
<td><p>Bcc:Jack (directamente o mediante grupo de distribución)</p></td>
<td><p>No</p></td>
<td><p>La información de CCO no se almacena en el mensaje que se entrega a los destinatarios. Debe buscar en el buzón de correo del remitente.</p></td>
</tr>
<tr class="even">
<td><p>Buzón de correo de Jack</p></td>
<td><p>To/Cc:John (directamente o mediante grupo de distribución)</p></td>
<td><p>Sí</p></td>
<td><p>La información de Para/CC se incluye en el mensaje que se entrega a todos los destinatarios.</p></td>
</tr>
<tr class="odd">
<td><p>Buzón de correo de Jack</p></td>
<td><p>Bcc:Jack (directamente o mediante grupo de distribución)</p></td>
<td><p>No</p></td>
<td><p>La información de CCO no se almacena en el mensaje que se entrega a los destinatarios. Debe buscar en el buzón de correo del remitente.</p></td>
</tr>
</tbody>
</table>


## Preguntas más frecuentes

**P. ¿cuándo y dónde se almacena la información de destinatarios de CCO?**  
Se conserva la información de los destinatarios CCO de la r. de forma predeterminada en el mensaje original en el buzón del remitente. Si el destinatario CCO es un grupo de distribución, pertenencia a grupos de distribución sólo se expande si el buzón del remitente está en suspensión o asignado a una política de retención Office 365.

**P. ¿cuándo y dónde es la lista de distribución expandida de destinatarios del grupo almacenados?**  
R. pertenencia se expande en el momento en que se envía el mensaje. La lista de miembros del grupo de distribución expandido se almacena en el mensaje original en el buzón del remitente. El buzón del remitente debe estar en posesión de In situ, retención para litigios, o asignados a una política de retención de Office 365.

**P. ¿Los destinatarios incluidos en Para/CC: pueden ver qué destinatarios figuran en CCO?**  
R. No. Esta información no se incluye en los encabezados del mensaje y no está visible para los destinatarios incluidos en Para/CC. El remitente puede ver el campo CCO almacenado en el mensaje original almacenado en el buzón de correo. Los responsables de cumplimento normativo pueden ver esta información cuando buscan en el buzón de correo del remitente.

**P. ¿Cómo puedo garantizar siempre se conservan los destinatarios del grupo de distribución expandido?**  
A. Para garantizar que los miembros del grupo de distribución expandido se conservan siempre con un mensaje, [Poner todos los buzones en retención](place-all-mailboxes-on-hold-exchange-2013-help.md) o crean una política de retención Office 365 de toda la organización.

**P. ¿Qué tipos de grupos se admiten?**  
R. Se admiten grupos de distribución, grupos de seguridad habilitados para correo y grupos de distribución dinámicos.

**P. ¿Existe un límite en la cantidad de destinatarios del grupo de distribución que se amplía y se almacena en el mensaje?**  
R. Se conservan hasta 10.000 miembros de un grupo de distribución.

**P. ¿Se admiten los grupos de distribución anidados?**  
R. Sí, se expanden 25 niveles de grupos de distribución anidados.

**P. ¿Dónde se puede ver la información de los destinatarios del grupo de distribución expandido y CCO?**  
R. La información de los destinatarios CCO y del grupo de distribución expandido aparece visible para los responsables del cumplimiento normativo cuando se realiza una búsqueda de exhibición de documentos electrónicos. Los destinatarios CCO y del grupo de distribución expandido se incluyen en los resultados de la búsqueda que se hayan copiado en un buzón de correo de detección o se hayan exportado a un archivo PST y en el registro de exhibición de documentos electrónicos incluidos en los resultados de la búsqueda. La información de los destinatarios CCO también se encuentra disponible en la vista previa de la búsqueda.

**P. ¿Qué ocurre si se oculta un miembro de un grupo de distribución de lista global de direcciones de la organización (GAL)?**  
R. No pasa nada. Si los destinatarios están ocultas en la GAL, todavía se incluirán en la lista de destinatarios del grupo de distribución expandido.

