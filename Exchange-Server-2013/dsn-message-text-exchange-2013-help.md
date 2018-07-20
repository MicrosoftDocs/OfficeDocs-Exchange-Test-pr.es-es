---
title: 'Texto del mensaje de DSN: Exchange 2013 Help'
TOCTitle: Texto del mensaje de DSN
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 49895993
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Texto del mensaje de DSN

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Puede incluir texto en un mensaje personalizado de notificación de estado de entrega (DSN) en Microsoft Exchange Server 2013 y dar formato a ese texto en HTML.

Puede incluir cualquier información que desee mostrar al destinatario del mensaje DSN. Por ejemplo, puede incluir una descripción detallada de DSN, información de contacto para la ayuda técnica y un vínculo al sitio Web del departamento de soporte técnico. Cada mensaje de DSN puede contener un máximo de 512 caracteres.

Como los mensajes de DSN se pueden mostrar en HTML, puede incrustar etiquetas de formato HTML en el texto DSN. Por ejemplo, si desea pasar a negrita parte del texto del mensaje de DSN, escriba el texto entre las etiquetas HTML \<B\> y \</B\>. En la tabla siguiente se muestran algunos ejemplos de etiquetas HTML válidas que se pueden usar en el texto del mensaje de DSN.

### Etiquetas HTML válidas para su uso en mensajes de DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Etiqueta HTML</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;B&gt;</p></td>
<td><p>Inicio de negritas</p></td>
</tr>
<tr class="even">
<td><p>&lt;/B&gt;</p></td>
<td><p>Final de negrita</p></td>
</tr>
<tr class="odd">
<td><p>&lt;A HREF=&quot;url&quot;&gt;</p></td>
<td><p>Inicio de hipervínculo</p></td>
</tr>
<tr class="even">
<td><p>&lt;/A&gt;</p></td>
<td><p>Fin de hipervínculo</p></td>
</tr>
<tr class="odd">
<td><p>&lt;BR&gt;</p></td>
<td><p>Salto de vínculo</p></td>
</tr>
<tr class="even">
<td><p>&lt;EM&gt;</p></td>
<td><p>Inicio de cursivas</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/EM&gt;</p></td>
<td><p>Fin de cursiva</p></td>
</tr>
<tr class="even">
<td><p>&lt;P&gt;</p></td>
<td><p>Inicio de párrafo</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/P&gt;</p></td>
<td><p>Fin de párrafo</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> De manera predeterminada, Exchange envía mensajes de DSN HTML, pero usted puede configurar si Exchange enviará los mensajes de DSN HTML a remitentes internos, remitentes externos o ambos. Para configurar este comportamiento, modifique el parámetro <EM>InternalDsnSendHtml</EM> y el parámetro <EM>ExternalDsnSendHtml</EM> con el comando <STRONG>Set-TransportService</STRONG>.<BR>Si el parámetro <EM>InternalDsnSendHtml</EM> se establece en <CODE>$false</CODE>, Exchange suprime las etiquetas HTML en los mensajes de DSN enviados a remitentes internos. Si el parámetro <EM>ExternalDsnSendHtml</EM> se establece en <CODE>$false</CODE>, Exchange suprime las etiquetas HTML en los mensajes de DSN enviados a remitentes externos.



Los siguientes caracteres que Exchange usa en el texto de los mensajes de DSN tienen significados especiales:

  - Signo mayor que (\>)

  - Signo menor que (\<)

  - Ampersand (&)

  - Comillas (")

Estos caracteres se usan para determinar dónde comienzan y terminan las etiquetas HTML, y dónde comienza o termina el texto que se muestra a los remitentes. Si desea mostrar estos caracteres en los mensajes de DSN, debe usar los códigos de escape de la tabla siguiente.

Por ejemplo, si desea mostrar el mensaje `"Please contact the Help Desk at <1234>."`, debe agregar `"Please contact the Help Desk at &lt;1234&gt;." ` al texto del mensaje de DSN.

### Códigos de escape de caracteres de mensajes de DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Código de escape</th>
<th>Carácter</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;lt;</p></td>
<td><p>&lt;</p></td>
</tr>
<tr class="even">
<td><p>&amp;gt;</p></td>
<td><p>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;</p></td>
<td><p>&quot;</p></td>
</tr>
<tr class="even">
<td><p>&amp;amp;</p></td>
<td><p>&amp;</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> Si incluye una etiqueta HTML en el texto del mensaje de DSN que contiene comillas ("), como <CODE>&lt;A HREF="url"&gt;</CODE>, debe usar comillas simples (') en todo texto del mensaje de DSN. Recibirá un mensaje de error si usa dobles comillas rodeando todo el texto del mensaje de DSN y la etiqueta HTML.


