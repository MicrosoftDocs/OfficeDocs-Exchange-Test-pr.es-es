---
title: 'Importación de entradas de reescritura de direcciones en servidores de transporte perimetral: Exchange 2013 Help'
TOCTitle: Importación de entradas de reescritura de direcciones en servidores de transporte perimetral
ms:assetid: bd0942c6-9c66-4b4c-b9bc-2f5f783def76
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb331966(v=EXCHG.150)
ms:contentKeyID: 61061235
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importación de entradas de reescritura de direcciones en servidores de transporte perimetral

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Puede crear de forma masiva la información sobre reescritura de direcciones o importarla en un servidor de transporte perimetral mediante un archivo de valores separados por comas (CSV). En esta lista describimos los escenarios comunes en los que es necesario hacerlo:

  - Va a reemplazar una solución de reescritura de direcciones por un servidor de transporte perimetral.

  - Acepta el contrato de otro proveedor de soluciones que requiere que reescriba sus direcciones de correo electrónico.

  - Realiza la adquisición de otra organización y necesita reescribir temporalmente las direcciones de correo electrónico de la organización que adquirió.

Para crear el archivo CSV puede usar cualquier editor de texto, como el Bloc de notas, o una aplicación como Microsoft Excel. Aplique formato al archivo tal y como lo describimos en este tema, y guárdelo como un archivo .CSV.

La primera fila o *fila de encabezado* del archivo CSV indica los nombres de los parámetros. Los parámetros están separados por comas. En esta tabla se describen los parámetros obligatorios y los opcionales.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Obligatorio u opcional</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>Nombre único y descriptivo de la entrada de reescritura de direcciones.</p></td>
</tr>
<tr class="even">
<td><p><em>InternalAddress</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>La dirección que quiere cambiar. Puede usar estos valores:</p>
<ul>
<li><p>Una única dirección de correo electrónico (maria@contoso.com)</p></li>
<li><p>Un único dominio o subdominio (contoso.com o sales.contoso.com)</p></li>
<li><p>Uno dominio y todos sus subdominios (*.contoso.com)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAddress</em></p></td>
<td><p>Obligatorio</p></td>
<td><p>La dirección de correo electrónico final que quiere tener. Puede usar estos valores:</p>
<ul>
<li><p>Una única dirección de correo electrónico si especificó una sola dirección de correo electrónico para <em>InternalAddress</em></p></li>
<li><p>Un único dominio o subdominio para todos los demás valores de <em>InternalAddress</em></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ExceptionList</em></p></td>
<td><p>Opcional</p></td>
<td><p>Disponible solamente cuando va a reescribir las direcciones de correo electrónico de un dominio y todos sus subdominios (*.contoso.com). Especifica uno o varios subdominios que quiere excluir de la reescritura de direcciones. Encierre el valor entre comillas dobles y use comas para separar varios valores. Por ejemplo, <code>&quot;marketing.contoso.com&quot;</code> o <code>&quot;marketing.contoso.com,legal.contoso.com&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>Opcional</p></td>
<td><p><code>False</code> indica que las direcciones se escriben en correo entrante y saliente. <code>True</code> indica que las direcciones se reescriben solo en correo saliente y tiene que configurar manualmente la dirección de correo electrónico reescrita como una dirección de proxy en los destinatarios afectados.</p>
<p>El valor predeterminado es <code>False</code>, pero debe establecerlo en <code>True</code> si <em>InternalAddress</em> contiene el carácter comodín (*.contoso.com).</p>
<p>El parámetro <em>OutboundOnly</em> en el archivo CSV es <code>True</code> o <code>False</code>, y no es <code>$True</code> ni <code>$False</code>.</p></td>
</tr>
</tbody>
</table>


Cada fila bajo la fila del encabezado representa una entrada de reescritura de dirección individual. Los valores de cada fila deben seguir el mismo orden que los nombres de parámetro de la fila de encabezado. Los valores están separados por comas.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 30 minutos

  - Asegúrese de que comprende las ramificaciones de la reescritura de direcciones. Por ejemplo, la dirección de correo electrónico reescrita debe ser única en su organización de Exchange y es posible que tenga que configurar direcciones del proxy en los destinatarios afectados. Para más información, vea [Reconfiguración de direcciones en los servidores de transporte perimetral](address-rewriting-on-edge-transport-servers-exchange-2013-help.md) y [Administrar la reconfiguración de direcciones en servidores de transporte perimetral](manage-address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Agente de reescritura de direcciones" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Si tiene varios servidores de transporte perimetral, le recomendamos que siga los procedimientos que le explicamos en este tema para importar entradas de reescritura de direcciones en un solo servidor de transporte perimetral y, después, clone la configuración de ese servidor de transporte perimetral en los otros servidores de transporte perimetral de su organización. Para obtener más información acerca de cómo clonar un servidor de transporte perimetral, vea [Configuración clonada del servidor de transporte perimetral](edge-transport-server-cloned-configuration-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo puede realizar esto?

## Paso 1: Cree el archivo CSV.

Cuando cree el archivo CSV, tenga en cuenta esto:

  - Si especifica valores para parámetros opcionales en el archivo CSV, cada fila debe indicar un valor en esa columna. Si quiere crear varias entradas de reescritura de direcciones, y que algunas de ellas tengan parámetros opcionales y otras no, tiene que separar las entradas de reescritura de direcciones en dos archivos CSV independientes y, después, importar cada archivo CSV por separado.

  - Si el archivo CSV contiene caracteres que no son ASCII, asegúrese de guardarlo con codificación UTF-8 o con otra codificación Unicode. En función de la aplicación, es posible que resulte más fácil guardar el archivo CSV con codificación UTF-8 u otra codificación Unicode cuando la configuración regional del equipo coincida con el idioma usado en el archivo CSV.

En el siguiente ejemplo, se muestra cómo se puede rellenar un archivo CSV con los parámetros opcionales *ExceptionList* y *OutboundOnly* incluidos:

    Name,InternalAddress,ExternalAddress,ExceptionList,OutboundOnly
    "Wingtip UK",*.wingtiptoys.co.uk,tailspintoys.com,"legal.wingtiptoys.co.uk,finance.wingtiptoys.co.uk,support.wingtiptoys.co.uk",True
    "Wingtip USA",*.wingtiptoys.com,tailspintoys.com,"legal.wingtiptoys.com,finance.wingtiptoys.com,support.wingtiptoys.com,corp.wingtiptoys.com",True
    "Wingtip Canada",*.wingtiptoys.ca,tailspintoys.com,"legal.wingtiptoys.ca,finance.wingtiptoys.ca,support.wingtiptoys.ca",True

## Paso 2: Importar el archivo CSV

Para importar el archivo CSV, use esta sintaxis:

    Import-Csv <FileNameAndPath> | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

En este ejemplo se importan las entradas de reescritura de direcciones de C:\\My Documents\\ImportAddressRewriteEntries.csv.

    Import-Csv "C:\My Documents\ImportAddressRewriteEntries.csv" | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

## ¿Cómo saber si funcionó lo que hizo en este paso?

Haga esto para comprobar que importó correctamente las entradas de reescritura de direcciones de un archivo CSV:

1.  Para ver todas las entradas de reescritura de direcciones, ejecute el comando `Get-AddressRewriteEntry`.

2.  Para ver los detalles sobre una determinada entrada de reescritura de direcciones, ejecute el comando `Get-AddressRewriteEntry <AddressRewriteIdentity> | Format-List`

