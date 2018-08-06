---
title: 'Elementos no aptos para búsqueda en eDiscovery de Exchange: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange
ms:assetid: 32550081-9af9-474b-ae7b-28f1e68cad41
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn602498(v=EXCHG.150)
ms:contentKeyID: 61071983
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En la exhibición de documentos electrónicos local de Exchange Server 2013 y Exchange Online, los elementos no aptos para la búsqueda son elementos de buzón que el servicio de búsqueda de Exchange no puede indizar o que se han indizado solo parcialmente. Normalmente, un elemento no apto para la búsqueda contiene un archivo que no se puede indizar adjunto a un mensaje de correo electrónico. Estos son algunos motivos por los que los archivos no se pueden indizar para búsquedas y se devuelven como elementos no aptos para la búsqueda cuando se adjuntan a un mensaje de correo electrónico.

  - El tipo de archivo no se admite para indización porque no hay instalado un filtro de búsqueda (también conocido como *IFilter*) para indizar el formato de archivo.

  - El tipo de archivo está deshabilitado para indización.

  - El tipo de archivo se admite para indización pero se produjo un error de indización en un archivo específico.

  - Un archivo se ha cifrado con tecnologías que no son de Microsoft.

  - Un archivo está protegido por contraseña.

Para que una búsqueda de exhibición de documentos electrónicos se realice correctamente, puede que se le solicite a la organización que revise los elementos no aptos para la búsqueda. Puede especificar si se incluirán los elementos no aptos para la búsqueda cuando se copien los resultados de la búsqueda de la exhibición de documentos electrónicos en un buzón de detección o se exporten los resultados a un archivo PST.

## Tipos de archivo no admitidos para búsquedas

Determinados tipos de archivos, como mapas de bits o MP3, no incluyen contenido que se pueda indizar. Como resultado, el servicio de búsqueda de Exchange no realiza una indización de texto completo en estos tipos de archivo. Estos tipos de archivo se consideran como no admitidos. También hay tipos de archivos para los que se ha deshabilitado la indización de texto completo, ya sea de forma predeterminada o por un administrador. Los tipos de archivo no admitidos y deshabilitados se consideran elementos no aptos para la búsqueda en las búsquedas de exhibición de documentos electrónicos. Estos tipos de archivos, que normalmente se adjuntan a un mensaje de correo electrónico, se incluyen en el conjunto de resultados cuando se incluyen los elementos no aptos para la búsqueda al copiar o exportar los resultados. Para ver una lista de los formatos de archivo admitidos y deshabilitados, consulte [Formatos de archivo indizados por la búsqueda de Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md). En Exchange Server 2013, los administradores pueden deshabilitar la indización de un formato de archivo admitido mediante el cmdlet [Set-SearchDocumentFormat](https://technet.microsoft.com/es-es/library/jj873756\(v=exchg.150\)). Este cmdlet no está disponible en Exchange Online.

Para identificar los elementos no aptos para la búsqueda en un buzón específico, puede ejecutar el cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/es-es/library/dd351154\(v=exchg.150\)) para obtener una lista de los elementos que se copiarían o se exportarían si decide incluir los elementos no aptos para la búsqueda en los resultados de la búsqueda.

## Mensajes con tipos de archivo no admitidos que se devuelven en los resultados de la búsqueda

No todos los mensajes con archivos no admitidos adjuntos se devuelven automáticamente como elementos no aptos para la búsqueda. Esto se debe a que otras propiedades de archivo, como el nombre de archivo, se indizan y están disponibles para la búsqueda. Por ejemplo, una búsqueda de la palabra clave "financiero" devolverá un mensaje con un archivo no admitido adjunto si esa palabra clave aparece en el nombre del archivo. Si la palabra clave solo aparece en el cuerpo del archivo adjunto, el mensaje se devolvería como elemento no apto para la búsqueda.

De forma similar, los mensajes con archivos no admitidos adjuntos se incluyen en los resultados de la búsqueda cuando otras propiedades de un elemento de buzón, indizadas y aptas para la búsqueda, cumplen los criterios de búsqueda. Las propiedades de los mensajes que se indizan para la búsqueda son las fechas de envío y recepción, el remitente y el destinatario, el nombre de archivo de un adjunto, y el texto del cuerpo del mensaje. Por este motivo, aunque un archivo adjunto a un mensaje no se pueda buscar, el mensaje se incluirá en los resultados de la búsqueda normales si el valor de otras propiedades de mensaje coinciden con los criterios de búsqueda. De hecho, es habitual que los mensajes con adjuntos no aptos para la búsqueda se incluyan en los resultados de la búsqueda normales.

Para ver una lista de las propiedades de los mensajes de correo electrónico que se indizan para la búsqueda, consulte [Propiedades de mensajes indexadas por la búsqueda de Exchange](message-properties-indexed-by-exchange-search-exchange-2013-help.md).

## Inclusión de elementos no aptos para la búsqueda en los resultados de la búsqueda

Es posible que su organización deba identificar y realizar un procesamiento adicional en los elementos no aptos para la búsqueda para determinar qué son, qué contienen y si son relevantes. Para incluir elementos no aptos para la búsqueda en los resultados de la búsqueda de la exhibición de documentos electrónicos, puede usar la opción de elementos no aptos para la búsqueda cuando copie o exporte los resultados de la búsqueda. Para incluir elementos no aptos para la búsqueda cuando use la exhibición de documentos electrónicos en contexto de Exchange o Exchange Online, seleccione la opción **Incluir elementos que no se pueden buscar** cuando copie los resultados de la búsqueda a un buzón de detección o cuando los exporte a un archivo PST. Para incluir elementos no aptos para la búsqueda cuando use el centro de exhibición de documentos electrónicos de SharePoint o SharePoint Online, seleccione la opción **Incluir elementos que están cifrados o tienen un formato no reconocido**.

Tenga en cuenta lo siguiente cuando copie o exporte elementos no aptos para la búsqueda:

  - Cuando se copian elementos no aptos para la búsqueda en un buzón de detección, los elementos no aptos para la búsqueda se copian en una carpeta diferente llamada **Inencontrable**, situada dentro de la carpeta que contiene los resultados de la búsqueda. Cuando se exportan resultados de la búsqueda que incluyen elementos no aptos para la búsqueda, los elementos no aptos para la búsqueda se exportan a un archivo PST diferente.

  - Cuando se incluyen elementos no aptos para la búsqueda en los resultados de la búsqueda, se devolverán todos los elementos no aptos para la búsqueda de los buzones donde se está buscando, independientemente de los criterios de búsqueda.

  - Si elige incluir todos los elementos de buzón en los resultados de la búsqueda o si una consulta de búsqueda no especifica palabras clave o solo especifica un intervalo de fechas, es posible que los elementos no aptos para la búsqueda no se copien a la carpeta **Inencontrable** si selecciona la opción de incluir los elementos no aptos para la búsqueda. Esto se debe a que todos los elementos, incluidos los elementos no aptos para la búsqueda, se incluirán automáticamente en los resultados de la búsqueda normales.

  - Como se indicó anteriormente, como las propiedades y los metadatos de los mensajes se indizan, una búsqueda de palabra clave puede devolver resultados si esa palabra clave aparece en las propiedades o en los metadatos de un mensaje con un archivo no apto para la búsqueda adjunto a él. En este caso se incluirán también dos copias del mismo elemento de buzón en los resultados de la búsqueda. Para evitar este tipo de duplicación e incluir solo una copia del elemento en los resultados de la búsqueda normales, puede seleccionar la opción **Habilitar la eliminación de duplicados** cuando copie o exporte los resultados de la búsqueda.

  - Incluir elementos no aptos para la búsqueda en los resultados de la búsqueda puede afectar también al número estimado de resultados de la búsqueda que se muestran. Si incluye elementos no aptos para la búsqueda cuando copie los resultados de la búsqueda, el número total de elementos estimado y el tamaño total estimado incluirán los elementos no aptos para la búsqueda.

Para obtener más información sobre cómo incluir elementos no aptos para la búsqueda en los resultados de la búsqueda, consulte:

  - [Crear una búsqueda de exhibición de documentos electrónicos local](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [Exportar los resultados de la búsqueda de exhibición de documentos electrónicos a un archivo PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)

  - [SharePoint: Exportar contenido de exhibición de documentos electrónicos y crear informes](https://go.microsoft.com/fwlink/p/?linkid=324757)

## Más información sobre elementos no aptos para la búsqueda

  - Aunque un archivo de texto sea admitido por el servicio de búsqueda de Exchange y se haya indizado el texto completo, puede haber errores de búsqueda o indización que hagan que un archivo se devuelva como elemento no apto para la búsqueda. Por ejemplo, la búsqueda en un archivo de Excel muy grande podría ser parcialmente correcta, pero se producirá un error cuando se supere el límite de tamaño. En este caso, es posible que el mismo archivo se devuelva con los resultados de la búsqueda y como elemento no apto para la búsqueda.

  - Los archivos adjuntos cifrados con tecnologías de Microsoft se indizan mediante el servicio de búsqueda de Exchange y se buscarán. Los archivos cifrados con tecnologías que no son de Microsoft se devuelven como no aptos para la búsqueda.

  - Los mensajes de correo electrónico cifrados con S/MIME no se indizan y se consideran términos no aptos para la búsqueda. Esto incluye los mensajes cifrados con o sin datos adjuntos.

  - El servicio de búsqueda de Exchange indiza los mensajes protegidos con Information Rights Management (IRM) y, por lo tanto, se incluyen en los resultados de la búsqueda si coinciden con los parámetros de la consulta. Para obtener más información sobre IRM, consulte [Information Rights Management](information-rights-management-exchange-2013-help.md).

  - Como se indicó anteriormente, como las propiedades y los metadatos de los mensajes se indizan, una búsqueda de palabra clave puede devolver resultados si esa palabra clave aparece en los metadatos indizados. Sin embargo, la misma búsqueda de palabra clave puede que no devuelva el mismo elemento si la palabra clave solo aparece en el contenido de un elemento adjunto con un tipo de archivo no admitido. En este caso, el elemento se devolvería solo como elemento no apto para la búsqueda.

  - En la exhibición de documentos electrónicos de Exchange 2010, existe el concepto de *lista segura*. Estos son tipos de archivo que incluyen contenido no apto para la búsqueda y, por lo tanto, el servicio de búsqueda de Exchange no lo indiza; por ejemplo, archivos Windows Media Video (.wmv) y Waveform Audio (.wav). Como estos tipos de archivo no incluyen contenido apto para la búsqueda, no se consideran elementos no aptos para la búsqueda en Exchange 2010. Los elementos de buzón que contienen estos tipos de archivo no se devolvieron como elementos no aptos para la búsqueda y no se copiaron a un buzón de detección.
    
    En Exchange 2013 y en Exchange Online ya no existe una lista segura. Los tipos de archivo están habilitados o deshabilitados para la búsqueda, o no se admiten. Los tipos de archivo deshabilitados o no admitidos se consideran elementos no aptos para la búsqueda.

