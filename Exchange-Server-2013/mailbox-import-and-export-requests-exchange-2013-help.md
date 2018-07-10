---
title: 'Solicitudes de importación y exportación de buzones: Exchange 2013 Help'
TOCTitle: Solicitudes de importación y exportación de buzones
ms:assetid: 157a7d88-d3aa-4056-9a50-df67451b14be
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633455(v=EXCHG.150)
ms:contentKeyID: 49895486
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solicitudes de importación y exportación de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Usando los conjuntos de cmdlets **MailboxImportRequest** o **MailboxExportRequest** cmdlet establecidos en el Shell de administración de Exchange, puede importar datos o exportar datos a archivos .pst. Después de iniciar una solicitud de importación o exportación de buzones de correo, el servicio de replicación de buzón (MRS) de Microsoft Exchange completa el proceso asincrónicamente. MRS reside en todos los servidores de acceso de clientes de Exchange 2010 y es el servicio responsable de mover buzones de correo y de importar y exportar archivos .pst.

**Contenido**

Motivos para importar y exportar datos de buzones de correo

Ventajas de usar solicitudes de importación y exportación

Consideraciones

Importación de datos del buzón de correo

Exportación de datos del buzón de correo

## Motivos para importar y exportar datos de buzones de correo

Es posible que desee importar o exportar datos de buzones de correo por las siguientes razones:

  - **Satisfacer los requisitos de cumplimiento**   Puede exportar contenido de un buzón de correo a un archivo .pst con fines de detección legal. Después de que se completa la exportación, puede importar el contenido a un buzón de correo usado específicamente con fines de cumplimiento.

  - **Crear una instantánea de un buzón de correo hasta un momento dado**   Al crear una instantánea de buzones de correo específicos, se evita retener un conjunto de copias de seguridad para una base de datos de buzones de correo.

  - **Mover un archivo .pst de un usuario en su buzón de correo o archivo personal**   Los usuarios de Microsoft Outlook pueden guardar, de manera local, sus correos electrónicos como archivos .pst. Mediante el uso del cmdlet [New-MailboxImportRequest](https://technet.microsoft.com/es-es/library/ff607310\(v=exchg.150\)), puede mover datos de un archivo .pst de un usuario a su buzón de correo o archivo personal. Este es un método sencillo para transferir correos electrónicos del equipo local de un usuario a servidores de Exchange.

## Ventajas de usar solicitudes de importación y exportación

Las ventajas de usar las solicitudes de importación y exportación en Exchange 2013 incluyen las siguientes:

  - Un proveedor de .pst está incluido en Exchange 2013 que puede leer y escribir archivos .pst.

  - Las solicitudes de importación y exportación son asíncronas. MRS lleva a cabo el proceso, que aprovecha los marcos de cola y limitación.

  - Los archivos .pst se pueden importar directamente al archivo personal de un usuario.

  - Los archivos .pst múltiples se pueden importar o exportar al mismo tiempo.

  - Los archivos .pst pueden encontrarse en cualquier unidad de red de uso compartido a la cual tengan acceso los servidores de Exchange.

  - Exchange 2013 es compatible con estos archivos .pst: Archivos Unicode creados por Office Outlook 2007 y Outlook 2010

## Consideraciones

Antes de importar o exportar datos de buzones de correo, considere lo siguiente:

  - Para importar o exportar datos de buzones de correo, se debe instalar una carpeta de red de uso compartido a la que sus servidores de Exchange. Además, debe otorgar permisos de lectura/escritura al grupo Subsistema de confianza de Exchange para que ese grupo pueda tener acceso a la red de uso compartido donde se importan y se exportan los datos de buzones de correo. Si no otorga este permiso, recibirá un mensaje de error en el que se informa que Exchange no puede establecer una conexión con el buzón de correo de destino.

  - El tamaño de archivo .pst máximo admitido por Outlook es 50 gigabytes (GB). Por lo tanto, recomendamos que no importe un archivo .pst con tamaño superior a 50 GB. Puede crear archivos .pst para buzones de correo con un tamaño superior a 50 GB al especificar carpetas específicas para incluir o excluir o mediante el uso de un filtro de contenido.

  - MRS lleva a cabo las solicitudes de importación y exportación y procesa las solicitudes de traslado y las solicitudes de restauración de buzón de correo. Todas las solicitudes están en cola y limitadas por MRS.

  - La importación y exportación de datos de buzones de correo puede demorar varias horas, según el tamaño del archivo, el ancho de banda de la red y la limitación de MRS.

  - No se pueden importar datos a una carpeta pública ni a una base de datos de carpetas públicas.

## Importación de datos del buzón de correo

Use el conjunto de cmdlets **MailboxImportRequest** para importar datos de un archivo .pst a un buzón de correo o a un archivo personal. A continuación, se encuentra una lista de opciones que puede especificar al importar datos de buzones de correo desde un archivo .pst:


> [!NOTE]
> El buzón de correo al que importe los datos debe existir. No puede importar datos a una cuenta de usuario que no tiene un buzón de correo.



  - Puede importar datos a una cuenta de usuario diferente a la cuenta desde la cual se exportaron los datos. Por ejemplo, puede exportar datos desde juancarlos@contoso.com e importarlos al de descubrimientolegal@contoso.com.

  - Puede importar elementos sólo al archivo personal del usuario al especificar el parámetro *IsArchive*.

  - Si existen mensajes de carpetas asociados en el archivo .pst, puede importarlos mediante el uso del parámetro *AssociatedMessagesCopyOption*. Los mensajes asociados contienen datos ocultos con información sobre reglas, vistas y formularios. Si existen estos mensajes en el archivo .pst, se importan todos los mensajes de la red de seguridad.

  - Puede incluir o excluir carpetas específicas mediante el uso del parámetro *IncludeFolders* o el parámetro *ExcludeFolders*.

  - Puede excluir la carpeta de elementos recuperables mediante el uso del parámetro *ExcludeDumpster*. De manera predeterminada, una solicitud de importación incluye la carpeta de elementos recuperables del usuario siempre que se encuentre presente en el archivo .pst.

## Cmdlets de solicitud de importación de buzones de correo

Use los siguientes cmdlets para las solicitudes de importación de buzones de correo.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607310(v=exchg.150)">New-MailboxImportRequest</a></p></td>
<td><p>Inicia el proceso de importación de un archivo .pst a un buzón de correo o archivo personal. Puede crear más de una solicitud de importación por buzón de correo. Cada solicitud debe tener un único nombre.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607317(v=exchg.150)">Set-MailboxImportRequest</a></p></td>
<td><p>Cambia las opciones de solicitud de importación después de que se crea la solicitud o realice una recuperación de un error de solicitudes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607309(v=exchg.150)">Suspend-MailboxImportRequest</a></p></td>
<td><p>Suspende una solicitud de importación en cualquier momento después de crear la solicitud, pero antes de que llegue al estado &quot;Completada&quot;.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607306(v=exchg.150)">Resume-MailboxImportRequest</a></p></td>
<td><p>Reanuda una solicitud de importación que está suspendida o con errores.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607311(v=exchg.150)">Remove-MailboxImportRequest</a></p></td>
<td><p>Quita total o parcialmente las solicitudes de importación completadas. Las solicitudes de importación completadas no se borran automáticamente. Para quitarlas, debe usar este cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607368(v=exchg.150)">Get-MailboxImportRequest</a></p></td>
<td><p>Consulte información general acerca de una solicitud de importación.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607315(v=exchg.150)">Get-MailboxImportRequestStatistics</a></p></td>
<td><p>Consulte información detallada acerca de una solicitud de importación.</p></td>
</tr>
</tbody>
</table>


## Exportación de datos del buzón de correo

Use el conjunto de cmdlets **MailboxExportRequest** para exportar datos de buzones de correo a un archivo .pst. Puede exportar un buzón de correo o varios buzones de correo, pero sólo se escribe una solicitud a la vez en cada archivo .pst. A continuación, se encuentra una lista de opciones que puede especificar al exportar datos de buzones de correo a un archivo .pst:

  - Puede exportar datos de archivos personales mediante el uso del parámetro *IsArchive*.

  - Puede filtrar los mensajes que se exportan mediante el uso del parámetro *ContentFilter*. Puede filtrar según contenido, archivos adjuntos, remitentes, destinatarios, categoría de la bandeja de entrada, importancia, tipo y tamaño del mensaje, y su fecha de envío, recepción o expiración.

  - Puede especificar carpetas para incluir o excluir mediante el uso del parámetro *IncludeFolders* o el parámetro *ExcludeFolders*. Si exporta datos desde un buzón de correo de Exchange 2013, también puede excluir la carpeta de elementos recuperables mediante el uso del parámetro *ExcludeDumpster*.

  - Puede exportar mensajes asociados mediante el uso del parámetro *AssociatedMessagesCopyOption*. Los mensajes asociados contienen datos ocultos con información sobre reglas, vistas y formularios. De manera predeterminada, los elementos asociados no se pueden copiar al archivo .pst.

## Cmdlets de solicitud de exportación de buzones de correo

Use los siguientes cmdlets para las solicitudes de exportación de buzones de correo.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607299(v=exchg.150)">New-MailboxExportRequest</a></p></td>
<td><p>Inicia el proceso de exportar datos de un buzón de correo principal o un archivo personal a un archivo .pst. Puede crear más de una solicitud de exportación por buzón de correo. Cada solicitud debe tener un único nombre.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607312(v=exchg.150)">Set-MailboxExportRequest</a></p></td>
<td><p>Cambia las opciones de solicitud de exportación después de que se crea la solicitud o realiza una recuperación de un error de solicitudes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607305(v=exchg.150)">Suspend-MailboxExportRequest</a></p></td>
<td><p>Suspende una solicitud de exportación en cualquier momento después de crear la solicitud, pero antes de que llegue al estado &quot;Completada&quot;.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607476(v=exchg.150)">Resume-MailboxExportRequest</a></p></td>
<td><p>Reanuda una solicitud de exportación que está suspendida o con errores.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607464(v=exchg.150)">Remove-MailboxExportRequest</a></p></td>
<td><p>Quita total o parcialmente las solicitudes de exportación completadas. Las solicitudes de exportación completadas no se borran automáticamente. Para quitarlas, debe usar este cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607479(v=exchg.150)">Get-MailboxExportRequest</a></p></td>
<td><p>Consulte información general acerca de una solicitud de exportación.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/ff607316(v=exchg.150)">Get-MailboxExportRequestStatistics</a></p></td>
<td><p>Consulte información detallada acerca de una solicitud de exportación.</p></td>
</tr>
</tbody>
</table>

