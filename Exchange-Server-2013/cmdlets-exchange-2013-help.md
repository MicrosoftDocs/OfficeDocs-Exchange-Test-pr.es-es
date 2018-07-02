---
title: 'Cmdlets: Exchange 2013 Help'
TOCTitle: Cmdlets
ms:assetid: 1d741dea-1eb8-4909-850f-63d4efaa1a32
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996589(v=EXCHG.150)
ms:contentKeyID: 49116075
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cmdlets

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Un *cmdlet*, pronunciado "command-let", es la unidad de funcionalidad más pequeña del Shell de administración de Exchange. Los cmdlets imitan a los comandos integrados en otros Shells, como el comando `dir` de `cmd.exe`. Al igual que estos comandos familiares, los cmdlets pueden ejecutarse directamente desde la línea de comandos del Shell y funcionar en el contexto del Shell, no como un proceso independiente.


> [!NOTE]
> Desde Microsoft Exchange Server 2007, hubo cambios en la forma en que Exchange&nbsp;2013 usa los cmdlets internamente debido al uso de la funcionalidad remota de Windows PowerShell. Estos cambios impactan poco, o nada, en la forma que necesita usar los cmdlets, pero pueden ofrecer más flexibilidad en la manera que administra los servidores de Exchange.



Los cmdlets suelen estar diseñados en torno a tareas administrativas repetitivas y, en el Shell, se ofrecen cientos de cmdlets destinados a tareas de administración específicas de Exchange. Además, también están disponibles los cmdlets de sistema que no son de Exchange, que se incluyen en el diseño del Shell Windows PowerShell. Para obtener más información sobre cómo abrir el Shell de administración de Exchange, consulte [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)).

Todos los cmdlets del Shell se presentan en pares verbo-nombre. El par verbo-nombre se separa siempre mediante un guión (-) sin espacios, y los nombres del cmdlet son siempre en singular. Los verbos hacen referencia a la acción que emprende el cmdlet. Los nombres hacen referencia al objeto sobre el que el cmdlet emprende la acción. Por ejemplo, en el cmdlet **Get-SystemMessage**, el verbo es **Get**, y el nombre **SystemMessage**. Todos los cmdlet del Shell que administran una característica determinada comparten el mismo nombre. La tabla siguiente proporciona ejemplos de algunos verbos disponibles en el Shell.


> [!NOTE]
> De forma predeterminada, si se omite el verbo, el Shell&nbsp;asume el verbo <STRONG>Get</STRONG>. Por ejemplo, al llamar a <STRONG>Mailbox</STRONG> obtendrá los mismos resultados que cuando llame a <STRONG>Get-Mailbox</STRONG>.



### Ejemplos de verbos en el Shell de administración de Exchange

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Verbo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Disable</strong></p></td>
<td><p>Los cmdlets <strong>Disable</strong> establecen el valor del estado <code>Enabled</code> del objeto especificado de Exchange en <code>$False</code>. De esta forma, el objeto no procesará datos, aunque el objeto exista.</p></td>
</tr>
<tr class="even">
<td><p><strong>Enable</strong></p></td>
<td><p>Los cmdlets <strong>Enable</strong> establecen el valor del estado Habilitado del objeto de Exchange especificado en <code>$True</code>. De esta forma, el objeto puede procesar datos.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get</strong></p></td>
<td><p>Los cmdlets <strong>Get</strong> recuperan información acerca de un objeto específico de Exchange.</p>

> [!NOTE]
> La mayoría de los cmdlets <STRONG>Get</STRONG> solamente devuelven información de resumen al ejecutarlos. Para indicar al cmdlet <STRONG>Get</STRONG> que devuelva información detallada al ejecutar un comando, canalice el comando al cmdlet <STRONG>Format-List</STRONG>. Para obtener más información acerca del comando <STRONG>Format-List</STRONG> consulte <A href="working-with-command-output-exchange-2013-help.md">Trabajar con salidas de comandos</A>. Para obtener más información acerca de la canalización, consulte <A href="https://technet.microsoft.com/es-es/library/aa998260(v=exchg.150)">Canalización</A>.


</td>
</tr>
<tr class="even">
<td><p><strong>Install</strong></p></td>
<td><p>Los cmdlets <strong>Install</strong> instalan un nuevo objeto o función en un servidor Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Move</strong></p></td>
<td><p>Los cmdlets <strong>Move</strong> cambian la posición del objeto de Exchange especificado desde un contenedor o servidor a otro.</p></td>
</tr>
<tr class="even">
<td><p><strong>New</strong></p></td>
<td><p>Los cmdlets <strong>New</strong> crean nuevos objetos de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Remove</strong></p></td>
<td><p>Los cmdlets <strong>Remove</strong> eliminan el objeto de Exchange especificado.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set</strong></p></td>
<td><p>Los cmdlets <strong>Set</strong> modifican las propiedades de un objeto Exchange existente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Test</strong></p></td>
<td><p>Los cmdlets <strong>Test</strong> prueban componentes específicos de Exchange y suministran archivos de registro que puede examinar.</p></td>
</tr>
<tr class="even">
<td><p><strong>Uninstall</strong></p></td>
<td><p>Los cmdlets <strong>Uninstall</strong> quitan un objeto o función de un servidor Exchange.</p></td>
</tr>
</tbody>
</table>


La siguiente lista de cmdlets es un ejemplo de un conjunto de cmdlets completo. Este conjunto de cmdlets se utiliza para administrar la notificación del mensaje de estado de entrega (DSN) y las características del mensaje de cuota de buzón de Exchange 2013:

  - **Get-SystemMessage**

  - **New-SystemMessage**

  - **Remove-SystemMessage**

  - **Set-SystemMessage**

