---
title: 'Formatos de archivo indizados por la búsqueda de Exchange: Exchange 2013 Help'
TOCTitle: Formatos de archivo indizados por la búsqueda de Exchange
ms:assetid: e5110ac1-28e1-4554-acc3-85d08c997bc5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633485(v=EXCHG.150)
ms:contentKeyID: 52062071
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Formatos de archivo indizados por la búsqueda de Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-07-21_

En MicrosoftExchange Server 2013 y en Exchange Online, Exchange Search incluye filtros para indizar los tipos de formatos de archivo más habituales incluidos como datos adjuntos de los mensajes. También puede instalar filtros para indizar otros tipos de archivos.


> [!NOTE]
> En Exchange&nbsp;2013, no es necesario instalar y registrar Microsoft Office Filter Pack.



Al administrar o usar Exchange Search y las características dependientes (como [Exhibición de documentos electrónicos en contexto](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/integrate-sensitive-information-rules)), tenga en cuenta la diferencia entre los elementos no aptos para la búsqueda y los formatos de archivo deshabilitados para indizar o el contenido que no se puede indizar:

  - **Elementos que no se pueden buscar**  Cuando la búsqueda de Exchange no puede indizar un tipo de archivo determinado por la razón que sea (por ejemplo, porque no se ha instalado un filtro en particular), se produce un error al buscar ese tipo de archivo. Los mensajes que contienen dichos datos adjuntos se marcan como *parcialmente indizados*. Los elementos no aptos para la búsqueda se pueden recuperar mediante el cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/es-es/library/dd351154\(v=exchg.150\)). Al copiar los resultados de la búsqueda de exhibición de documentos electrónicos en contexto a un buzón de correo o al exportar los resultados de la búsqueda a un archivo PST, puede incluir elementos no aptos para la búsqueda. Para obtener más información, vea [Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - **Formatos de archivo con contenidos que no se pueden indizar**   Ciertos tipos de archivos como Windows Media Video (WMV) no incluyen contenidos que se puedan indizar y, por lo tanto, no se indizan. Los mensajes con datos adjuntos de estos tipos de archivos también se devuelven como elementos no aptos para la búsqueda en las búsquedas de exhibición de documentos electrónicos en contexto.

  - **Formatos de archivo deshabilitados** En organizaciones locales, un administrador puede deshabilitar el indizado de un formato de archivo especificado. Los mensajes que contienen datos adjuntos en un formato deshabilitado se devuelven como elementos no aptos para la búsqueda.


> [!IMPORTANT]
> Aunque los datos adjuntos de un mensaje no sean aptos para la búsqueda o tengan un formato de archivo que no se pueda indizar, el asunto del mensaje, el cuerpo del mensaje y otros metadatos se pueden indizar para que el mensaje se pueda devolver en las búsquedas.



Para tareas de administración adicionales relacionadas con Exchange Search en las organizaciones locales, vea [Procedimientos de búsqueda de Exchange](exchange-search-procedures-exchange-2013-help.md).

## Filtros predeterminados

En la lista siguiente se enumeran los filtros de búsqueda predeterminados instalados en un servidor de buzones de correo de Exchange 2013 y en Exchange Online. Puede recuperar la lista de filtros predeterminados mediante el cmdlet [Get-SearchDocumentFormat](https://technet.microsoft.com/es-es/library/jj873755\(v=exchg.150\)).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Filtro</th>
<th>Extensión de archivo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mensaje de correo electrónico</p></td>
<td><p>.eml</p></td>
</tr>
<tr class="even">
<td><p>Formato de intercambio de gráficos</p></td>
<td><p>.gif</p></td>
</tr>
<tr class="odd">
<td><p>JPEG</p></td>
<td><p>.jpeg</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Excel</p></td>
<td><p>.xls, .xlt, .xlsx, .xlsm, .xlb, .xlc, .xlsb</p></td>
</tr>
<tr class="odd">
<td><p>Archivo de Excel</p></td>
<td><p>odbcexcel</p></td>
</tr>
<tr class="even">
<td><p>Microsoft InfoPath</p></td>
<td><p>.infopathml</p></td>
</tr>
<tr class="odd">
<td><p>Cuaderno de Microsoft Office</p></td>
<td><p>.obt, obd</p></td>
</tr>
<tr class="even">
<td><p>Microsoft PowerPoint</p></td>
<td><p>.pptx, .pptm, .ppt, .ppsx, .ppsm, .pps, .ppam, .potm, .pot, .potx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Publisher</p></td>
<td><p>.pub</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Word</p></td>
<td><p>.doc, .docm, .dotx, .dotm, .dot, .docx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft XML Paper Specification</p></td>
<td><p>.xps</p></td>
</tr>
<tr class="even">
<td><p>OneNote</p></td>
<td><p>.one</p></td>
</tr>
<tr class="odd">
<td><p>Presentación de OpenDocument</p></td>
<td><p>.odp</p></td>
</tr>
<tr class="even">
<td><p>Hoja de cálculo de OpenDocument</p></td>
<td><p>.ods</p></td>
</tr>
<tr class="odd">
<td><p>Texto de OpenDocument</p></td>
<td><p>.odt</p></td>
</tr>
<tr class="even">
<td><p>Elemento de Outlook</p></td>
<td><p>.msg</p></td>
</tr>
<tr class="odd">
<td><p>Portable Document Format</p></td>
<td><p>.pdf</p></td>
</tr>
<tr class="even">
<td><p>Texto enriquecido</p></td>
<td><p>.rtf</p></td>
</tr>
<tr class="odd">
<td><p>Text</p></td>
<td><p>.txt</p></td>
</tr>
<tr class="even">
<td><p>vCalendar</p></td>
<td><p>.vcs</p></td>
</tr>
<tr class="odd">
<td><p>vCard</p></td>
<td><p>.vcf</p></td>
</tr>
<tr class="even">
<td><p>Visio</p></td>
<td><p>.vdw, .vsd, .vss, .vst, .vsx, .vtx, .vssx, .vssm, .vsdm, .vstx, .vstm, .vdx</p></td>
</tr>
<tr class="odd">
<td><p>Archivo Web</p></td>
<td><p>.mhtml</p></td>
</tr>
<tr class="even">
<td><p>Página web</p></td>
<td><p>.html</p></td>
</tr>
<tr class="odd">
<td><p>Documento XML</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="even">
<td><p>Archivo ZIP</p></td>
<td><p>.zip</p></td>
</tr>
</tbody>
</table>


## Formatos de archivo deshabilitados

En la lista siguiente se enumeran los filtros de búsqueda que están deshabilitados para la indización predeterminada en un servidor de buzones de correo de Exchange 2013 y en Exchange Online. En Exchange 2013, los administradores pueden usar el cmdlet [Set-SearchDocumentFormat](https://technet.microsoft.com/es-es/library/jj873756\(v=exchg.150\)) para deshabilitar o volver a habilitar un formato de archivo compatible de indización. El cmdlet no está disponible en Exchange Online.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Filter</th>
<th>Extensión de archivo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVI</p></td>
<td><p>.avi</p></td>
</tr>
<tr class="even">
<td><p>Mapa de bits</p></td>
<td><p>.bmp</p></td>
</tr>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>.mp3</p></td>
</tr>
<tr class="even">
<td><p>MPEG</p></td>
<td><p>.mpeg</p></td>
</tr>
<tr class="odd">
<td><p>PNG</p></td>
<td><p>.png</p></td>
</tr>
<tr class="even">
<td><p>Onda de audio de Microsoft Windows</p></td>
<td><p>.wav</p></td>
</tr>
</tbody>
</table>

