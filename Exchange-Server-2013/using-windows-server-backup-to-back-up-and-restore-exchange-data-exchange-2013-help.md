---
title: 'Uso de copias de seguridad de Windows Server para realizar copias de seguridad y restaurar datos de Exchange: Exchange 2013 Help'
TOCTitle: Uso de copias de seguridad de Windows Server para realizar copias de seguridad y restaurar datos de Exchange
ms:assetid: 0fac891a-5713-42b6-afd5-c91b2b88f966
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876851(v=EXCHG.150)
ms:contentKeyID: 48267805
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Uso de copias de seguridad de Windows Server para realizar copias de seguridad y restaurar datos de Exchange

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

[Mejor arquitectura](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx) para Exchange Server 2013 de Microsoft aprovecha un concepto conocido como Exchange nativo de protección de datos. Exchange Protección de datos nativa se basa en características de nativo Exchange para proteger los datos de buzón, sin el uso de backups tradicionales. Pero si desea crear copias de seguridad, incluye un complemento para Windows Server Backup (WSB) que le permite crear copias de seguridad basado en Volume Shadow Copy Service VSS para Exchange de Exchange datos de Exchange. Para realizar copias de seguridad para Exchange, debe tener instalada la característica de WSB.

El complemento, WSBExchange.exe, se ejecuta como un servicio llamado Extensión de Microsoft Exchange para Copias de seguridad de Windows Server (el nombre abreviado de este servicio es WSBExchange). Este servicio se instala automáticamente y se configura para iniciarse manualmente en todos los servidores de buzones de correo. El complemento permite que WSB cree copias de seguridad de VSS compatibles con Exchange.

Antes de usar WSB para realizar copias de seguridad de los datos de Exchange, le recomendamos que se familiarice con las siguientes características y opciones del complemento:

  - Las copias de seguridad que se realizan con WSB tienen lugar en el nivel del volumen, y la única manera de realizar o restaurar una copia de seguridad en el nivel de la aplicación es seleccionar un volumen completo. Para hacer una copia de seguridad de una base de datos y su secuencia de registro, debe hacer también una copia de seguridad del volumen completo que contiene la base de datos y los registros, no solo de las carpetas individuales. No se pueden hacer copias de seguridad de los datos sin hacer también una copia de seguridad de todo el volumen que los contiene.

  - La copia de seguridad se debe ejecutar de forma local en el servidor del que se hace la copia, y no se puede usar el complemento para las copias de seguridad de VSS remotas. No existe administración remota de WSB ni del complemento. No obstante, puede usar Servicios de Escritorio remoto o Terminal Services para administrar copias de seguridad de forma remota.

  - La copia de seguridad se puede crear en una unidad local o en un recurso compartido de red remoto.

  - Solo se deben crear copias de seguridad completas. El truncamiento de registro se realizará solamente después de que se haya creado correctamente una copia de seguridad completa con VSS de un volumen o carpetas que contengan una base de datos de Exchange.

  - Al restaurar datos, solo es posible restaurar datos de Exchange. Estos datos se pueden restaurar en su ubicación original o en una ubicación alternativa. Si se restauran los datos en su ubicación original, WSB y el complemento controlarán el proceso de recuperación de forma automática, incluidos el desmontaje de las bases de datos existentes y la reproducción de registros en la base de datos restaurada.

  - El proceso de restauración no admite la base de datos de recuperación (RDB). Si quiere usar una RDB, debe restaurar los datos en otra ubicación y después, copiar o restaurar manualmente los datos de esa ubicación en la estructura de carpetas de RDB.

  - Al restaurar datos de Exchange, todas las bases de datos de las que se hizo copia de seguridad se deben restaurar juntas. No puede restaurar una única base de datos.

  - Las reconstrucciones completas se admiten cuando se usa WSB; sin embargo, el enfoque de recuperación recomendado para los servidores de Exchange es recuperar el servidor de Exchange y, a continuación, restaurar los datos. Si está usando una aplicación de copia de seguridad de terceros (que no es de Microsoft), es posible que el proveedor de aplicaciones de copia de seguridad admita reconstrucciones completas de Exchange.

La tabla siguiente describe la compatibilidad de las opciones de copia de seguridad y recuperación disponibles para Exchange 2013 con WSB.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Si quiere...</th>
<th>Entonces...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Realizar una copia de seguridad de todo el servidor...</p></td>
<td><p>Se realizará una copia de seguridad VSS y no se truncarán los registros de transacciones de las bases de datos en el servidor.</p></td>
</tr>
<tr class="even">
<td><p>Realizar una copia de seguridad personalizada y seleccionar uno o varios volúmenes para hacer la copia de seguridad...</p></td>
<td><p>Puede seleccionar una copia de seguridad completa VSS, permitiendo que los registros de transacciones de las bases de datos en los volúmenes seleccionados se trunquen al finalizar una copia de seguridad correcta.</p></td>
</tr>
<tr class="odd">
<td><p>Realizar una copia de seguridad personalizada y seleccionar una o varias carpetas para hacer la copia de seguridad...</p></td>
<td><p>Se puede seleccionar una copia de seguridad completa VSS y los archivos de registro se truncarán; sin embargo, la restauración de la copia de seguridad se limitará a restauración del archivo, porque opción de restaurar en el nivel de aplicación no estará disponible.</p></td>
</tr>
</tbody>
</table>


Para obtener instrucciones detalladas para realizar una copia de seguridad de Exchange con WSB, vea [Usar Copias de seguridad de Windows Server para realizar copias de seguridad de Exchange](use-windows-server-backup-to-back-up-exchange-exchange-2013-help.md).

Para obtener instrucciones detalladas para restaurar los datos de una copia de seguridad realizada con WSB, vea [Usar Copias de seguridad de Windows Server para restaurar una copia de seguridad de Exchange](use-windows-server-backup-to-restore-a-backup-of-exchange-exchange-2013-help.md).

