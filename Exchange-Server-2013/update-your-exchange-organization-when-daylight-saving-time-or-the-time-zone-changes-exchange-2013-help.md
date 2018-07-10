---
title: 'Actualizar la organización de Exchange cuando cambia el horario de verano o la zona horaria: Exchange 2013 Help'
TOCTitle: Actualizar la organización de Exchange cuando cambia el horario de verano o la zona horaria
ms:assetid: 5b12615c-24cf-4f46-bf3c-2334dc734ef8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh530051(v=EXCHG.150)
ms:contentKeyID: 66452413
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Actualizar la organización de Exchange cuando cambia el horario de verano o la zona horaria

 

_**Se aplica a:** Exchange Online, Exchange Server, Exchange Server 2010, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Si la región o el país en que residen la organización o algunos de los usuarios cambió la directiva de reconocer el horario de verano (DST) o cambió la diferencia horaria local de hora universal coordinada (UTC), deberá actualizar Microsoft Windows, Microsoft Exchange, Microsoft Outlook u otros programas según estos cambios.

Para obtener más información sobre los cambios de DST en el mundo, incluidos los vínculos, vea [Centro de ayuda y soporte técnico para el horario de verano de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=99640). También visite los sitios web de soporte técnico de los otros proveedores de software para ver si requieren actualizaciones adicionales.

Incluso si su zona no cambió, si interactúa con otros equipos o usuarios de manera global, el equipo debe poder realizar cálculos de fecha y hora precisos para eventos en otras partes del mundo.

Al instalar las actualizaciones de zonas horarias lo antes posible, se minimiza la cantidad de reuniones y citas que se programan durante la transición del horario viejo al nuevo.

## ¿Cómo realiza esto?

## Paso 1: Instalar la actualización de Windows de DST en todos los equipos cliente y de escritorio

Debido a que el sistema de autenticación de Office 365 se actualiza cuando cambia el DST o una zona horaria, todos los equipos cliente de Office 365 deben actualizarse. De lo contrario, es posible que tengan problemas de conectividad.

  - Asegúrese de que todos los equipos cliente y de escritorio tengan instalada la actualización de DST de Windows. Para obtener más información, vea [Cómo configurar el horario de verano en sistemas operativos Microsoft Windows](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=914387).

## Paso 2: Instalar la actualización de Windows de DST en todos los servidores

1.  Actualice todos los servidores locales con la actualización de DST de Windows.

2.  Si está ejecutando Office 365, actualice los servidores que interactúan con el sistema de autenticación de Office 365, como los servidores DirSync o AD FS. Estos servidores deben actualizarse para garantizar el tiempo de actividad.

**Nota** Si está actualizando clústeres de servidores, asegúrese de seguir el proceso habitual para actualizar los clústeres. En primer lugar, debe actualizar el servidor pasivo, conmutar por error al servidor pasivo (que se vuelve activo) y, después, actualizar el servidor que anteriormente estaba activo (y ahora es pasivo). Para obtener más información sobre cómo actualizar clústeres de servidores y clústeres de servidores alta disponibilidad, vea Actualizar clústeres de Exchange Server y servidores alta disponibilidad y [How to update Windows Server failover clusters (Cómo actualizar clústeres de conmutación por error de Windows Server)](https://support.microsoft.com/es-es/kb/174799).

## Paso 3: Actualizar Exchange y Outlook, donde sea necesario, en los equipos cliente y de escritorio

1.  Si sus usuarios están usando Outlook 2007 o clientes anteriores, determine qué herramientas de zonas horarias de Exchange o Outlook se deben ejecutar, mediante la tabla y el siguiente procedimiento.

2.  Envíe un mensaje a los usuarios que deben actualizar sus equipos, con el vínculo a la herramienta correspondiente.

En la siguiente tabla se muestra el momento en que los usuarios deben ejecutar la [Herramienta de actualización de calendario de Exchange](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879) o la [Herramienta de actualización de datos de zona horaria para Microsoft Office Outlook](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667). Averigüe qué versión ejecutan los servidores de la organización y determine qué programas cliente ejecutan los usuarios.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>Versión del cliente</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><strong>Versión de la organización</strong></p></td>
<td><p><strong>Outlook 2003 u Outlook 2007</strong></p></td>
<td><p><strong>Outlook 2010</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2003 local</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Herramienta de calendario de Exchange</a> o</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Herramienta de actualización de datos de zona horaria para Microsoft Office Outlook</a></p></td>
<td><p>No se requiere ninguna acción.</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2007 local</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Herramienta de calendario de Exchange</a> o</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Herramienta de actualización de datos de zona horaria para Microsoft Office Outlook</a></p></td>
<td><p>No se requiere ninguna acción.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2010 local</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Herramienta de calendario de Exchange</a> o</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Herramienta de actualización de datos de zona horaria para Microsoft Office Outlook</a></p></td>
<td><p>No se requiere ninguna acción.</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2013 local</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Herramienta de actualización de datos de zona horaria para Microsoft Office Outlook</a></p></td>
<td><p>No se requiere ninguna acción.</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPOS-S (Exchange 2007)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Herramienta de actualización de datos de zona horaria para Microsoft Office Outlook</a></p></td>
<td><p>No se requiere ninguna acción.</p></td>
</tr>
<tr class="even">
<td><p><strong>BPOS-D (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Herramienta de actualización de datos de zona horaria para Microsoft Office Outlook</a></p></td>
<td><p>No se requiere ninguna acción.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Office 365 (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Herramienta de actualización de datos de zona horaria para Microsoft Office Outlook</a> (no es compatible con Outlook 2003)</p></td>
<td><p>No se requiere ninguna acción</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 (Exchange 2013)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Herramienta de actualización de datos de zona horaria para Microsoft Office Outlook</a> (no es compatible con Outlook 2003)</p></td>
<td><p>No se requiere ninguna acción</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

