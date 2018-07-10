---
title: 'Búsqueda de Exchange: Exchange 2013 Help'
TOCTitle: Búsqueda de Exchange
ms:assetid: 967e2a13-4e54-486a-ac22-08768674abbb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232132(v=EXCHG.150)
ms:contentKeyID: 52062048
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Búsqueda de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-09-17_

El tamaño de los buzones de correo y la cantidad de datos almacenados en los mismos en forma de mensajes y adjuntos es cada vez mayor, por ello resulta crucial que los usuarios puedan buscar y localizar rápidamente los mensajes que necesitan. [Archivado local en Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) ayuda a reducir o eliminar el uso de archivos .pst moviendo los elementos antiguos o de acceso infrecuente a un archivo. De este modo se consigue almacenar más datos de buzones por usuario y la búsqueda en el buzón principal y el archivo se convierte en una importante herramienta de productividad. [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md) permite que los usuarios autorizados busquen contenido en buzones de correo locales o en organizaciones Exchange en la nube para cumplir con las solicitudes de exhibición de documentos electrónicos (eDiscovery), auditorías reglamentarias o investigaciones internas. La exhibición de documentos electrónicos local también usa los índices de contenido creados por Exchange Search.

La búsqueda de Exchange es diferente de la indización de texto completo disponible en Exchange Server 2003. Se realizaron mejoras en cuanto a rendimiento, indización de contenido y búsqueda. Los elementos nuevos se indizan en el canal de transporte o casi inmediatamente después de creados o entregados al buzón de correo, lo que brinda a los usuarios un modo fácil, estable y más confiable de buscar datos de buzón de correo. La indización de contenido está habilitada por defecto y no requiere ninguna instalación ni configuración inicial.

¿Está buscando tareas de administración relacionadas con la búsqueda de Exchange? Vea [Procedimientos de búsqueda de Exchange](exchange-search-procedures-exchange-2013-help.md).

## Novedades

Exchange 2013 introduce los cambios siguientes a Exchange Search:

  - El motor de indización de contenido subyacente ha sido sustituido por Microsoft Search Foundation, que ofrece mejoras de rendimiento y funcionalidad y sirve de motor de indización de contenido subyacente común en Exchange y SharePoint. Sin embargo, la interfaz de administración sigue siendo la misma.

  - Por defecto, Search Foundation admite los formatos de archivo más habituales en adjuntos de correo electrónico. Ya no es necesario que instale Microsoft Office Filter Packs para Exchange Search. Para una lista de los formatos de archivo admitidos por Exchange Search, consulte [Formatos de archivo indizados por la búsqueda de Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md).
    
    Puede agregar compatibilidad a cualquier formato de archivo adicional instalando IFilters, como en Exchange 2010.

  - La indización de contenido es más eficiente porque ahora procesa mensajes en el canal de transporte. En consecuencia, los mensajes enviados a varios destinatarios o grupos de distribución se procesan solamente una vez. Se adjunta un flujo de anotación al mensaje, acelerando considerablemente la indización de contenido al consumir menos recursos.

