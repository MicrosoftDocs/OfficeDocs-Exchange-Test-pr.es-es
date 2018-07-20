---
title: 'Permisos del conector de recepción: Exchange 2013 Help'
TOCTitle: Permisos del conector de recepción
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 49895556
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permisos del conector de recepción

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

La tabla siguiente enumera los tipos de permisos y una descripción de cada uno.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Permiso del conector de recepción</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-SMTP-Submit</p></td>
<td><p>Es necesario que se conceda este permiso a la sesión, o será incapaz de enviar mensajes a este conector de recepción. Si una sesión no tiene este permiso, los comandos MAIL FROM y AUTH darán un error.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Any-Recipient</p></td>
<td><p>Este permiso permite a la sesión retransmitir mensajes a través de este conector. Si no se concede este permiso, solo se aceptarán en este conector los mensajes dirigidos a destinatarios incluidos en los dominios aceptados.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Any-Sender</p></td>
<td><p>Con este permiso, la sesión puede omitir la comprobación de suplantación de la dirección del remitente.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Authoritative-Domain-Sender</p></td>
<td><p>Este permiso permite a los remitentes que tienen direcciones de correo electrónico en dominios con autorización establecer una sesión para este conector de recepción.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Authentication-Flag</p></td>
<td><p>Este permiso permite a los servidores de Exchange 2003 enviar mensajes de remitentes internos. Exchange 2010 reconocerá los mensajes como internos. El remitente puede declarar el mensaje como &quot;de confianza&quot;. Los mensajes que entran en su sistema de Exchange a través de envíos anónimos se retransmitirán a través de la organización de Exchange con esta marca en estado &quot;no fiable&quot;.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Routing</p></td>
<td><p>Este permiso permite que la sesión envíe un mensaje que tiene todos los encabezados de recepción intactos. Si no se concede este permiso, el servidor elimina todos los encabezados recibidos.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Headers-Organization</p></td>
<td><p>Este permiso permite que la sesión envíe un mensaje que tiene todos los encabezados de organización intactos. Todos los encabezados de organización empiezan por <strong>X-MS-Exchange-Organization-</strong>. Si no se concede este permiso, el servidor de recepción elimina todos los encabezados de la organización.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Forest</p></td>
<td><p>Este permiso permite que la sesión envíe un mensaje que tiene todos los encabezados de bosque intactos. Todos los encabezados de bosque comienzan con <strong>X-MS-Exchange-Forest-</strong>. Si no se concede este permiso, el servidor de recepción elimina todos los encabezados del bosque.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Exch50</p></td>
<td><p>Este permiso permite que la sesión envíe un mensaje que contenga el comando XEXCH50. Este comando es necesario para la interoperabilidad con Exchange 2003. El comando XEXCH50 brinda datos tales como el nivel de confianza de correo no deseado (SCL) del mensaje.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Message-Size-Limit</p></td>
<td><p>Este permiso permite que la sesión envíe un mensaje que supera la restricción para tamaño de mensaje configurada para el conector.</p></td>
</tr>
<tr class="odd">
<td><p>Ms-Exch-Bypass-Anti-Spam</p></td>
<td><p>Este permiso permite que la sesión omita el filtrado contra correo electrónico no deseado.</p></td>
</tr>
</tbody>
</table>

