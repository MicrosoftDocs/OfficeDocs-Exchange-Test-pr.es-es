---
title: 'Propiedades de mensajes indexadas por búsqueda de Exchange: Exchange 2013 Help'
TOCTitle: Propiedades de mensajes indexadas por la búsqueda de Exchange
ms:assetid: a9754dc1-44aa-4076-8b59-a5d39246d5b0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ983804(v=EXCHG.150)
ms:contentKeyID: 52062055
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Propiedades de mensajes indexadas por la búsqueda de Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-04-17_

Exchange Search indiza muchas propiedades de elementos, incluyendo el remitente, los destinatarios, el cuerpo del mensaje y los documentos adjuntos de los mensajes de correo electrónico.

## Propiedades indizadas por Exchange Search

La siguiente tabla incluye una lista de todas las propiedades de los elementos indizados por Exchange Search.


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
<th>Propiedad</th>
<th>Tipo</th>
<th>Consultable</th>
<th>Permite realizar búsquedas</th>
<th>Recuperable</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Account</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Assistantname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Datos adjuntos</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Attachmentfilenames</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Attachmentmetaproperties</p></td>
<td><p>Cadena</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Attachmentcount</p></td>
<td><p>Entero</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Bcc</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Businessaddress</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Businessmainphone</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Businessphonenumber</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Carphonenumber</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Categoría</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Companyname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Compositeitemid</p></td>
<td><p>Cadena</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Conversationid</p></td>
<td><p>Entero</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Conversationtopic</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Departmentname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Displayname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Displaynameprefix</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Documentid</p></td>
<td><p>Entero</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Emailaddress</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Emaildisplayname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Emailoriginaldisplayname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Errorcode</p></td>
<td><p>Entero</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Fileas</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Firstname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Folderid</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>From</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Homeaddress</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Homephone</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>Entero</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Ispartiallyprocessed</p></td>
<td><p>Booleano</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Ispermanentfailure</p></td>
<td><p>Booleano</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Itemclass</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Tipo</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Lastattempttime</p></td>
<td><p>DateTime</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Lastname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Mailboxguid</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Manager</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Meetinglocation</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Middlename</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Mobilephonenumber</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Nickname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Officelocation</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Otheraddress</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Participantes</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Primarytelephonenumber</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>DateTime</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Receivedby</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Receivedrepresenting</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Recipients</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>DateTime</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Sharinginfo</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>Entero</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Tasktitle</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Title</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Umaudionotes</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Watermark</p></td>
<td><p>Entero</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Yomicompanyname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Yomifirstname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Yomilastname</p></td>
<td><p>Cadena</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


**Notas sobre propiedades indizadas**:

  - **Propiedades consultables** puede ser usada en consultas AQS por clientes de búsqueda como Outlook Web App en `property:value` pares, por ejemplo, `from:bsuneja@cotoso.com`. Un subconjunto de las propiedades consultables enumeradas en la tabla anterior puede usarse también en las consultas de búsqueda de exhibición de documentos electrónicos local. Para obtener una lista de estas propiedades, consulte [Propiedades de mensajes y operadores de búsqueda para la exhibición de documentos electrónicos local](https://docs.microsoft.com/es-es/exchange/security-and-compliance/in-place-ediscovery/message-properties-and-search-operators).

  - Las **propiedades que permiten realizar búsquedas** son propiedades que no se pueden especificar en parejas `property:value`, pero una búsqueda por palabras clave devuelve el valor si se encuentra en alguna propiedad que permita realizar búsquedas. Por ejemplo, no puede usar `body:Contoso` para buscar la cadena `contoso` solo en el cuerpo del mensaje. Sin embargo, una búsqueda para dicha cadena devolverá todos los elementos donde la propiedad se encuentre en la propiedad que permita la búsqueda.

  - Las **propiedades recuperables** como `documenteid` y `ispartiallyprocessed` se devuelven con cada búsqueda.

