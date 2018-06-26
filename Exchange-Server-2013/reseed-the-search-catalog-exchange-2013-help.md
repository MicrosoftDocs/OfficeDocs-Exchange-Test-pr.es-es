---
title: 'Reinicializar el catálogo de búsqueda: Exchange 2013 Help'
TOCTitle: Reinicializar el catálogo de búsqueda
ms:assetid: 9d873bd4-0422-4975-b5e2-82a347479115
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633475(v=EXCHG.150)
ms:contentKeyID: 52062052
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Reinicializar el catálogo de búsqueda

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Si se daña el catálogo del índice de contenido de una copia de base de datos de buzones de correo, es posible que deba reinicializar el catálogo. El siguiente evento indica en el registro de eventos de la aplicación los índices de contenido dañados.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Id. de evento</th>
<th>Nivel</th>
<th>Origen</th>
<th>Detalles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>123</p></td>
<td><p>Error</p></td>
<td><p>ExchangeStoreDB</p></td>
<td><p>En &lt;<em>marca de tiempo</em>&gt;, la copia de &lt;<em>identidad</em>&gt; de la base de datos del almacén de información de Microsoft Exchange de este servidor experimentó un catálogo de búsqueda dañado. Vea el registro de eventos del servidor para ver otros eventos de &quot;ExchangeStoreDb&quot; y &quot;MSExchange Search Indexer&quot; y obtener información más específica sobre el error. Se recomienda reinicializar el catálogo mediante la tarea &quot;Update-MailboxDatabaseCopy&quot;.</p></td>
</tr>
</tbody>
</table>


Si la copia de la base de datos de buzones de correo se encuentra en un servidor que forma parte de un grupo de disponibilidad de base de datos (DAG), puede reinicializar el catálogo del índice de contenido de otro miembro de DAG.

Si la copia de la base de datos de buzones de correo es la única copia, debe crear manualmente un nuevo catálogo del índice de contenido.

Para otras tareas de administración relacionadas con Exchange Search, vea [Procedimientos de búsqueda de Exchange](exchange-search-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 minutos. El tiempo de reinicialización real puede variar en función del tamaño del catálogo del índice de contenido que se reinicializa.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Exhange Search" en el tema de [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Reinicializar el catálogo del índice de contenido si la base de datos de buzones de correo forma parte de un DAG

Use uno de los procedimientos siguientes si la base de datos de buzones de correo se encuentra en un servidor que forma parte de un DAG.

## Reinicializar el catálogo del índice de contenido desde cualquier origen

Este ejemplo reinicializa el catálogo del índice de contenido para la DB1 de la copia de la base de datos en el servidor de buzones de correo MBX1 de cualquier servidor de origen del DAG que tenga una copia de la base de datos.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)).

## Reinicializar el catálogo del índice de contenido desde un origen específico

En este ejemplo, se reinicializa el catálogo del índice de contenido para la copia de la base de datos DB1 en el servidor de buzones de correo MBX1 desde el servidor de buzones de correo MBX2, el cual también tiene una copia de la base de datos.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2 -CatalogOnly

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)).

## Reinicializar el catálogo del índice de contenido si solo hay una copia de la base de datos de buzones de correo

Si solo hay una copia de la base de datos de buzones de correo, debe reinicializar manualmente el catálogo de búsqueda volviendo a crear el catálogo del índice de contenido.

1.  Ejecute los siguientes comandos para detener los servicios de búsqueda de Microsoft Exchange y de controlador de host de búsqueda de Microsoft Exchange.
    
        Stop-Service MSExchangeFastSearch
    
        Stop-Service HostControllerService

2.  Elimine, mueva o cambie el nombre de la carpeta que contiene el catálogo del índice de contenido de Exchange. Esta carpeta se llama `%ExchangeInstallPath\Mailbox\<name of mailbox database>_Catalog\<GUID>12.1.Single`. Por ejemplo, podría cambiar el nombre de la carpeta `C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox Database 0657134726_Catalog\F0627A72-9F1D-494A-839A-D7C915C279DB12.1.Single_OLD`.
    

    > [!NOTE]
    > Al eliminar esta carpeta habrá más espacio en disco disponible. O quizás quiera cambiar el nombre o mover la carpeta para guardarla para solucionar problemas.



3.  Ejecute los siguientes comandos para reiniciar los servicios de búsqueda de Microsoft Exchange y de controlador de host de búsqueda de Microsoft Exchange.
    
        Start-Service MSExchangeFastSearch
    
        Start-Service HostControllerService
    
    Después de reiniciar estos servicios, Exchange Search volverá a crear el catálogo del índice de contenido.

## ¿Cómo puedo saber si el proceso se ha completado correctamente?

Exchange Search podría tardar un poco en reinicializar el catálogo del índice de contenido. Ejecute el siguiente comando para mostrar el estado del proceso de reinicialización:

    Get-MailboxDatabaseCopyStatus | FL Name,*Index*

Cuando la reinicialización del catálogo de búsqueda está en curso, el valor de la propiedad *ContentIndexState* es **Rastreando**. Cuando la reinicialización finaliza, este valor cambia a **Correcto**.

