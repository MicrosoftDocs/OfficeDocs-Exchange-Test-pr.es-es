---
title: 'Límites de las carpetas públicas: Exchange 2013 Help'
TOCTitle: Límites de las carpetas públicas
ms:assetid: 709b075e-9584-484b-bcaa-e781c26497b4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn594582(v=EXCHG.150)
ms:contentKeyID: 61170916
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Límites de las carpetas públicas

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

En Exchange Server 2013, hemos movido las carpetas públicas desde una arquitectura de bases de datos tradicional a una arquitectura de buzones. Este cambio permite a las carpetas públicas beneficiarse de aspectos como la resistencia del grupo de disponibilidad de la base de datos (DAG) y otras mejoras de los buzones realizadas con los años. Sin embargo, hay nuevos límites y cuestiones de rendimiento que deben tenerse en cuenta. En este documento proporcionamos una orientación general sobre las opciones de configuración que podrían afectar al rendimiento y a la conectividad de las carpetas públicas.

## Límites

La tabla siguiente enumera los límites de las carpetas públicas en Exchange Server 2013 local. A menos que los límites se indiquen específicamente como recomendados, los valores que se indican en esta tabla son los admitidos para las carpetas públicas.


> [!IMPORTANT]
> ¿Busca los límites de Exchange Online para Office 365? Consulte <A href="https://go.microsoft.com/fwlink/?linkid=391188">Límites de Exchange Online</A>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Límites</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Número total de buzones de carpeta pública</p></td>
<td><p>100</p></td>
<td><p>Aunque puede crear más de 100 buzones de carpeta pública, no se admiten. <a href="create-a-public-folder-mailbox-exchange-2013-help.md">Crear un buzón de carpetas públicas</a></p></td>
</tr>
<tr class="even">
<td><p>Carpetas públicas totales en la jerarquía</p></td>
<td><p>1,000,000</p></td>
<td><p>Aunque puede crear más de 1.000.000 de carpetas públicas, no se admiten. Para cualquier implementación de 100.000 carpetas públicas o más, se recomienda leer <a href="considerations-when-deploying-public-folders-exchange-2013-help.md">Consideraciones a la hora de implementar carpetas públicas</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Subcarpetas dentro de la carpeta primaria</p></td>
<td><p>10,000</p></td>
<td><p>Aunque puede crear más de 1.000 subcarpetas en una carpeta principal, no es recomendable que lo haga.</p>
<p>Parámetro <em>FolderHierarchyChildrenCountReceiveQuota</em> en el cmdlet <a href="https://technet.microsoft.com/es-es/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="even">
<td><p>Profundidad de carpetas</p></td>
<td><p>300</p></td>
<td><p>La profundidad de carpetas es el número de niveles de carpetas anidadas que puede existir en una rama de un árbol de carpetas públicas. Parámetro <em>FolderHierarchyDepthRecieveQuota</em> en el cmdlet <a href="https://technet.microsoft.com/es-es/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Número máximo de mensajes por carpeta pública</p></td>
<td><p>1 millón</p></td>
<td><p>Parámetro <em>MailboxMessagesPerFolderCountRecieveQuota</em> en el cmdlet <a href="https://technet.microsoft.com/es-es/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="even">
<td><p>Tamaño máximo de cada carpeta pública individual</p></td>
<td><p>10 GB</p></td>
<td><p>Este límite no incluye las subcarpetas dentro de una sola carpeta.</p>
<p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configurar cuotas de almacenamiento para un buzón</a></p></td>
</tr>
<tr class="odd">
<td><p>Tamaño del buzón de carpetas públicas</p></td>
<td><p>100 GB</p></td>
<td><p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configurar cuotas de almacenamiento para un buzón</a></p></td>
</tr>
<tr class="even">
<td><p>Número de inicios de sesión de usuario por buzón de carpeta pública</p></td>
<td><p>2000 inicios de sesión de usuario simultáneos</p></td>
<td><p>Le recomendamos configurar la jerarquía de modo que no tenga más de 2.000 usuarios por buzón de carpeta pública. Por ejemplo, si tiene 20.000 usuarios, debería tener 10 buzones de carpeta pública.</p></td>
</tr>
<tr class="odd">
<td><p>Retención de elementos movidos</p></td>
<td><p>Se recomiendan 14 días</p></td>
<td><p>Use el parámetro <em>DefaultPublicFolderMovedItemRetention</em> en el cmdlet <strong>Set-OrganizationConfig</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Límite de antigüedad</p></td>
<td><p>Recomendamos establecerlo en el mismo valor predeterminado que usó para los buzones de correo normales.</p></td>
<td><p>Estas configuraciones se pueden establecer en los siguientes niveles:</p>
<ul>
<li><p><strong>Nivel de organización:</strong> Parámetro <em>DefaultPublicFolderAgeLimit</em> en el cmdlet <strong>Set-OrganizationConfig</strong>.</p></li>
<li><p><strong>Nivel de buzón de correo:</strong> Parámetro <em>AgeLimit</em> en el cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p><strong>Nivel de carpeta:</strong> Parámetro <em>AgeLimit</em> en el cmdlet <strong>Set-PublicFolder</strong>.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Retención de elementos eliminados</p></td>
<td><p>Recomendamos establecerlo en el mismo valor predeterminado que usó para los buzones de correo normales.</p></td>
<td><p>Estas configuraciones se pueden establecer en los siguientes niveles:</p>
<ul>
<li><p><strong>Nivel de organización:Parámetro</strong> <em>DefaultPublicFolderMovedItemRetention</em> en el cmdlet <strong>Set-OrganizationConfig</strong>.</p></li>
<li><p><strong>Nivel de buzón de correo:</strong> <em>RetainDeletedItemsFor</em> en el cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p><strong>Nivel de carpeta:</strong> Parámetro <em>RetainDeleteItemsFor</em> en el cmdlet <strong>Set-PublicFolder</strong>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Número máximo de carpetas públicas que se pueden migrar a Exchange 2013</p></td>
<td><p>500,000</p></td>
<td><p>Es el número máximo de carpetas públicas que se pueden mover a Exchange 2013 desde una versión heredada de Exchange en una única migración. Para obtener información sobre la migración de carpetas públicas, vea <a href="use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md">Usar migración por lotes para migrar carpetas públicas a Exchange 2013 desde versiones anteriores</a>.</p></td>
</tr>
</tbody>
</table>

