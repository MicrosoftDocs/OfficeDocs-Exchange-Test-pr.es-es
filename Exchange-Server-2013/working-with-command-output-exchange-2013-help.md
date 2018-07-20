---
title: 'Trabajar con salidas de comandos: Exchange 2013 Help'
TOCTitle: Trabajar con salidas de comandos
ms:assetid: 8320e1a5-d3f5-4615-878d-b23e2aaa6b1e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123533(v=EXCHG.150)
ms:contentKeyID: 49116341
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Trabajar con salidas de comandos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

El Shell de administración de Exchange ofrece varios métodos que puede usar para dar formato a la salida de comandos. En este tema se explican los siguientes asuntos:

  - How to format data   Controlar el formato de los datos que se ven mediante los cmdlets **Format-List**, **Format-Table** y **Format-Wide**.

  - How to output data   Determinar si la salida de los datos se realiza en la ventana de la consola del Shell o en un archivo mediante los cmdlets **Out-Host** y **Out-File**. En este tema se incluye un script de ejemplo para enviar datos a Microsoft Internet Explorer.

  - How to filter data   Filtrar datos utilizando cualquiera de los siguientes métodos de filtrado:
    
      - Filtrado del servidor, disponible en determinados cmdlets.
    
      - Filtrado del cliente, disponible en todos los cmdlets canalizando los resultados de un comando al cmdlet **Where-Object**.

Para usar la funcionalidad descrita en este tema, debe estar familiarizado con los siguientes conceptos:

  - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))

  - [Variables de shell](https://technet.microsoft.com/es-es/library/bb124036\(v=exchg.150\))

  - [Operadores de comparación](https://technet.microsoft.com/es-es/library/bb125229\(v=exchg.150\))

## Cómo dar formato a datos

Si llama a cmdlets de formato al final del canal, puede invalidar el formato predeterminado para controlar qué datos se muestran y cómo aparecen dichos datos. Los cmdlets de formato son **Format-List**, **Format-Table** y **Format-Wide**. Cada uno de ellos tiene su propio estilo de salida particular que difiere de los restantes cmdlets de formato.

## Format-List

El cmdlet **Format-List** toma una entrada del canal y muestra como resultado una lista en columna vertical de todas las propiedades especificadas de cada objeto. Se pueden especificar las propiedades que se desean mostrar mediante el parámetro *Property*. Si se llama al cmdlet **Format-List** sin especificar ningún parámetro, se muestran todas las propiedades. El cmdlet **Format-List** ajusta las líneas en lugar de truncarlas. Uno de los mejores usos que se le puede dar al cmdlet **Format-List** es el de invalidar la salida predeterminada de un cmdlet para que se pueda recuperar información adicional o más específica.

Por ejemplo, cuando se llama al cmdlet **Get-Mailbox**, solo se ve una cantidad de información limitada en un formato de tabla. Si se canaliza la salida del cmdlet **Get-Mailbox** al cmdlet **Format-List** y se agregan parámetros para la información adicional o más específica que se desea visualizar, se puede recuperar el resultado deseado.

También puede especificar un carácter comodín "\*" con un nombre de propiedad parcial. Si incluye un carácter comodín, puede hacer coincidir varias propiedades sin tener que escribir el nombre de cada propiedad individualmente. Por ejemplo, `Get-Mailbox | Format-List -Property Email* ` devuelve todas las propiedades que empiezan con `Email`.

Los ejemplos siguientes muestran las distintas formas de ver los mismos datos devueltos por el cmdlet **Get-Mailbox**.

    Get-Mailbox TestUser1
    
    Name                      Alias                ServerName       ProhibitSendQuo
                                                                    ta
    ----                      -----                ----------       ---------------
    TestUser1                 TestUser1            mbx              unlimited

En el primer ejemplo, se llama al cmdlet **Get-Mailbox** sin ningún formato específico para que la salida predeterminada se realice en formato de tabla y contenga un conjunto predeterminado de propiedades.

    Get-Mailbox TestUser1 | Format-List -Property Name,Alias,EmailAddresses
    
    Name           : TestUser1
    Alias          : TestUser1
    EmailAddresses : {SMTP:TestUser1@contoso.com}

En el segundo ejemplo, la salida del cmdlet **Get-Mailbox** se canaliza al cmdlet **Format-List**, junto con propiedades específicas. Como puede ver, el formato y el contenido del resultado son notablemente distintos.

    Get-Mailbox TestUser1 | Format-List -Property Name, Alias, Email*
    Name                      : Test User
    Alias                     : TestUser1
    EmailAddresses            : {SMTP:TestUser1@contoso.com}
    EmailAddressPolicyEnabled : True

En el último ejemplo, la salida del cmdlet **Get-Mailbox** se canaliza al cmdlet **Format-List** como en el segundo ejemplo. No obstante, en el último ejemplo, se usa un carácter comodín para hacer coincidir todas las propiedades que empiezan con `Email`.

Si se pasa más de un objeto al cmdlet **Format-List**, todas las propiedades especificadas para un objeto se muestran y se agrupan por objeto. El orden de visualización depende del parámetro predeterminado del cmdlet. El parámetro predeterminado más frecuente es el parámetro *Name* o el parámetro *Identity*. Por ejemplo, cuando se llama al cmdlet **Get-Childitem**, el orden de visualización predeterminado es por nombre de archivo en orden alfabético. Para cambiar este comportamiento, debe llamar al cmdlet **Format-List** junto con el parámetro *GroupBy*, y al nombre de un valor de propiedad por el que desee agrupar el resultado. Por ejemplo, el siguiente comando enumera todos los archivos de un directorio y, luego, los agrupa según la extensión.

    Get-Childitem | Format-List Name,Length -GroupBy Extension
    
        Extension: .xml
    
    Name   : Config_01.xml
    Length : 5627
    
    Name   : Config_02.xml
    Length : 3901
    
    
        Extension: .bmp
    
    Name   : Image_01.bmp
    Length : 746550
    
    Name   : Image_02.bmp
    Length : 746550
    
    
        Extension: .txt
    
    Name   : Text_01.txt
    Length : 16822
    
    Name   : Text_02.txt
    Length : 9835

En este ejemplo, el cmdlet **Format-List** ha agrupado los elementos según la propiedad *Extension* especificada por el parámetro *GroupBy*. Puede usar el parámetro *GroupBy* con cualquier propiedad válida para los objetos en la secuencia de canalización.

## Format-Table

El cmdlet **Format-Table** le permite mostrar elementos en un formato de tabla con encabezados etiquetados y columnas de datos de propiedad. De forma predeterminada, muchos cmdlets, por ejemplo, los cmdlets **Get-Process** y **Get-Service**, usan el formato de tabla para el resultado. Entre los parámetros para el cmdlet **Format-Table**, se incluyen los parámetros *Properties* y *GroupBy*. Estos parámetros funcionan exactamente igual que lo harían con el cmdlet **Format-List**.

Además, el cmdlet **Format-Table** usa el parámetro *Wrap*. Este parámetro permite visualizar las líneas largas de información de propiedad de forma completa en lugar de truncarlas al final. A fin de ver cómo se usa el parámetro *Wrap* para mostrar información devuelta, compare la salida del comando **Get-Command** en los siguientes dos ejemplos.

En el primer ejemplo, cuando el cmdlet **Get-Command** se usa para mostrar información de comando acerca del cmdlet **Get-Process**, se trunca la información de la propiedad *Definition*.

    Get-Command Get-Process | Format-Table Name,Definition
    
    Name                                    Definition
    ----                                    ----------
    get-process                             get-process [[-ProcessName] String[]...

En el segundo ejemplo, se agrega el parámetro *Wrap* al comando para forzar la visualización del contenido completo de la propiedad *Definition*.

    Get-Command Get-Process | Format-Table Name,Definition -Wrap
    
    Get-Process                             Get-Process [[-Name] <String[]>] [-Comp
                                            uterName <String[]>] [-Module] [-FileVe
                                            rsionInfo] [-Verbose] [-Debug] [-ErrorA
                                            ction <ActionPreference>] [-WarningActi
                                            on <ActionPreference>] [-ErrorVariable
                                            <String>] [-WarningVariable <String>] [
                                            -OutVariable <String>] [-OutBuffer <Int
                                            32>]
                                            Get-Process -Id <Int32[]> [-ComputerNam
                                            e <String[]>] [-Module] [-FileVersionIn
                                            fo] [-Verbose] [-Debug] [-ErrorAction <
                                            ActionPreference>] [-WarningAction <Act
                                            ionPreference>] [-ErrorVariable <String
                                            >] [-WarningVariable <String>] [-OutVar
                                            iable <String>] [-OutBuffer <Int32>]
                                            Get-Process [-ComputerName <String[]>]
                                            [-Module] [-FileVersionInfo] -InputObje
                                            ct <Process[]> [-Verbose] [-Debug] [-Er
                                            rorAction <ActionPreference>] [-Warning
                                            Action <ActionPreference>] [-ErrorVaria
                                            ble <String>] [-WarningVariable <String
                                            >] [-OutVariable <String>] [-OutBuffer
                                            <Int32>]

Al igual que en el caso del cmdlet **Format-List**, también puede especificar un carácter comodín "`*`" con un nombre de propiedad parcial. Al incluir un carácter comodín, puede hacer coincidir varias propiedades sin tener que escribir cada nombre de propiedad individualmente.

## Format-Wide

El cmdlet **Format-Wide** permite un control de resultados mucho más simple que otros cmdlets de formato. De forma predeterminada, el cmdlet **Format-Wide** intenta mostrar tantas columnas de valores de propiedad como sea posible en una línea de resultado. Puede controlar el número de columnas y cómo se usa el espacio del resultado agregando parámetros.

Mediante el uso más básico, al llamar al cmdlet **Format-Wide** sin ningún parámetro, el resultado se organiza en una cantidad de columnas que se ajusta a la página. Por ejemplo, si ejecuta el cmdlet **Get-Childitem** y canaliza su resultado al cmdlet **Format-Wide**, verá la siguiente información:

    Get-ChildItem | Format-Wide
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml                           Config_02.xml
    Config_03.xml                           Config_04.xml
    Config_05.xml                           Config_06.xml
    Config_07.xml                           Config_08.xml
    Config_09.xml                           Image_01.bmp
    Image_02.bmp                            Image_03.bmp
    Image_04.bmp                            Image_05.bmp
    Image_06.bmp                            Text_01.txt
    Text_02.txt                             Text_03.txt
    Text_04.txt                             Text_05.txt
    Text_06.txt                             Text_07.txt
    Text_08.txt                             Text_09.txt
    Text_10.txt                             Text_11.txt
    Text_12.txt

Generalmente, al llamar al cmdlet **Get-Childitem** sin ningún parámetro, se muestran los nombres de todos los archivos del directorio en una tabla de propiedades. En este ejemplo, después de la canalización del resultado del cmdlet **Get-Childitem** al cmdlet **Format-Wide**, el resultado se mostró en dos columnas de nombres. Tenga en cuenta que solamente se puede mostrar un tipo de propiedad a la vez, y este debe estar especificado mediante el nombre de propiedad que sigue al cmdlet **Format-Wide**. Si agrega el parámetro *Autosize*, el resultado cambia de dos columnas a tantas como se ajusten al ancho de la pantalla.

    Get-ChildItem | Format-Wide -AutoSize
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml   Config_02.xml   Config_03.xml   Config_04.xml   Config_05.xml
    Config_06.xml   Config_07.xml   Config_08.xml   Config_09.xml   Image_01.bmp
    Image_02.bmp    Image_03.bmp    Image_04.bmp    Image_05.bmp    Image_06.bmp
    Text_01.txt     Text_02.txt     Text_03.txt     Text_04.txt     Text_05.txt
    Text_06.txt     Text_07.txt     Text_08.txt     Text_09.txt     Text_10.txt
    Text_11.txt     Text_12.txt

En este ejemplo, la tabla se organiza en cinco columnas, en lugar de dos. El parámetro *Column* brinda un mayor control al permitir especificar el número máximo de columnas para mostrar la información del siguiente modo:

    Get-ChildItem | Format-Wide -Column 4
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml       Config_02.xml       Config_03.xml       Config_04.xml
    Config_05.xml       Config_06.xml       Config_07.xml       Config_08.xml
    Config_09.xml       Image_01.bmp        Image_02.bmp        Image_03.bmp
    Image_04.bmp        Image_05.bmp        Image_06.bmp        Text_01.txt
    Text_02.txt         Text_03.txt         Text_04.txt         Text_05.txt
    Text_06.txt         Text_07.txt         Text_08.txt         Text_09.txt
    Text_10.txt         Text_11.txt         Text_12.txt

En este ejemplo, mediante el parámetro *Column*, el número de columnas no puede ser distinto de cuatro.

## Cómo dar salida a los datos

## Cmdlets Out-Host y Out-File

El cmdlet **Out-Host** es un cmdlet predeterminado no visto al final del canal. Después de aplicar todo el formato, el cmdlet **Out-Host** envía el resultado final a la ventana de consola para visualización. No tiene que llamar explícitamente al cmdlet **Out-Host**, dado que es el resultado predeterminado. Puede invalidar el envío del resultado a la ventana de consola llamando al cmdlet **Out-File** como último cmdlet del comando. El cmdlet **Out-File** escribe, a continuación, el resultado en el archivo que especifica en el comando, como se muestra en el ejemplo siguiente:

    Get-ChildItem | Format-Wide -Column 4 | Out-File c:\OutputFile.txt

En este ejemplo, el cmdlet **Out-File** escribe la información que se muestra en el comando **Get-ChildItem | Format-Wide -Column 4** en un archivo denominado `OutputFile.txt`. También puede redirigir el resultado del canal a un archivo mediante el operador de redirección, que es el corchete angular de cierre ( `>` ). Para anexar el resultado del canal de un comando a un archivo existente sin reemplazar el archivo original, use el corchete angular de cierre doble ( `>>` ), como en el ejemplo siguiente:

    Get-ChildItem | Format-Wide -Column 4 >> C:\OutputFile.txt

En este ejemplo, el resultado del cmdlet **Get-Childitem** se canaliza al cmdlet **Format-Wide** para dar formato y, después, se escribe al final del archivo `OutputFile.txt`. Tenga en cuenta que si el archivo `OutputFile.txt` no existe, éste se crearía al usar los corchetes angulares de cierre dobles (`>>`).

Para obtener más información acerca de los canales, vea [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\)).

Para obtener más información acerca de la sintaxis utilizada en los ejemplos anteriores, vea [Sintaxis](https://technet.microsoft.com/es-es/library/bb123552\(v=exchg.150\)).

## Visualización de datos en Internet Explorer

Dada la flexibilidad y la facilidad de creación de scripting en el Shell de administración de Exchange, puede extraer los datos devueltos por los comandos y darles formato y salida de forma casi ilimitada.

El ejemplo siguiente muestra cómo se puede usar un script simple para enviar los datos devueltos por un comando y mostrarlos en Internet Explorer. Este script extrae los objetos que pasan por el canal, abre una ventana de Internet Explorer y ,a continuación, muestra los datos en Internet Explorer:

    $Ie = New-Object -Com InternetExplorer.Application
    $Ie.Navigate("about:blank")
    While ($Ie.Busy) { Sleep 1 }
    $Ie.Visible = $True
    $Ie.Document.Write("$Input")
    # If the previous line doesn't work on your system, uncomment the line below.
    # $Ie.Document.IHtmlDocument2_Write(\"$Input\")
    $Ie

Para usar este script, guárdelo en el directorio `C:\Program Files\Microsoft\Exchange Server\V15\Scripts` del equipo donde se ejecutará. Nombre al archivo `Out-Ie.ps1`. Después de guardar el archivo, puede usar el script como un cmdlet normal.


> [!NOTE]
> Para ejecutar scripts en Exchange&nbsp;2013, éstos deben agregarse a un rol de administración sin ámbito y usted debe recibir la asignación de un rol de administración, ya sea directa o indirectamente, o mediante un grupo de roles de administración. Para obtener más información, consulte <A href="understanding-management-roles-exchange-2013-help.md">Descripción de los roles de administración</A>.



El script `Out-Ie` supone que los datos que recibe son código HTML válido. Para convertir los datos que desea ver en código HTML, debe canalizar los resultados del comando al cmdlet **ConvertTo-Html**. A continuación, puede canalizar los resultados de dicho comando al script `Out-Ie`. El siguiente ejemplo muestra cómo visualizar un listado de directorios en una ventana de Internet Explorer:

    Get-ChildItem | Select Name,Length | ConvertTo-Html | Out-Ie

## Cómo filtrar datos

El Shell ofrece acceso a una gran cantidad de información acerca de servidores, buzones, Active Directory y otros objetos de su organización. Aunque el acceso a esta información ayuda a comprender mejor el entorno, esta cantidad de información puede ser agobiante. El Shell le permite controlar esta información y solamente devuelve los datos que desea ver por medio del filtrado. Se dispone de los tipos de filtrado siguientes:

  - **Filtrado del servidor**   El filtrado del servidor toma el filtro que especifique en la línea de comandos y lo envía al servidor de Exchange en el que realice la consulta. Dicho servidor procesa la consulta y devuelve solo los datos que coincidan con el filtro especificado.
    
    El filtrado del servidor solamente se lleva a cabo en objetos en los que se pueden devolver decenas o centenas de miles de resultados. Por tanto, solo los cmdlets de administración de destinatarios como, por ejemplo, el cmdlet **Get-Mailbox**, y los cmdlets de administración de colas como, por ejemplo, el cmdlet **Get-Queue**, son compatibles con el filtrado del servidor. Estos cmdlets son compatibles con el parámetro *Filter*. Este parámetro toma la expresión del filtro que se especifica y la envía al servidor para que sea procesada.

  - **Filtrado del cliente**   El filtrado del cliente se lleva a cabo en los objetos de la ventana de consola local en la que se está trabajando actualmente. Cuando se usa el filtrado del cliente, el cmdlet recupera todos los objetos que coinciden con la tarea que se está realizando en la ventana de consola local. Luego, el Shell toma todos los resultados devueltos, aplica el filtro del cliente a dichos resultados y devuelve solamente los resultados que coincidan con su filtro. Todos los cmdlets son compatibles con el filtrado del cliente. Éste se llama mediante la canalización de los resultados de un comando al cmdlet **Where-Object**.

## Filtrado del servidor

La implementación del filtrado del servidor es específica del cmdlet en el que está admitido. El filtrado del servidor solamente se habilita sobre propiedades específicas en los objetos devueltos. Para obtener más información, consulte la ayuda de los cmdlets siguientes:


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-ActiveSyncDevice</p></td>
<td><p>Get-ActiveSyncDeviceClass</p></td>
<td><p>Get-CASMailbox</p></td>
<td><p>Get-Contact</p></td>
<td><p>Get-DistributionGroup</p></td>
</tr>
<tr class="even">
<td><p>Get-DynamicDistributionGroup</p></td>
<td><p>Get-Group</p></td>
<td><p>Get-Mailbox</p></td>
<td><p>Get-MailboxStatistics</p></td>
<td><p>Get-MailContact</p></td>
</tr>
<tr class="odd">
<td><p>Get-MailPublicFolder</p></td>
<td><p>Get-MailUser</p></td>
<td><p>Get-Message</p></td>
<td><p>Get-MobileDevice</p></td>
<td><p>Get-Queue</p></td>
</tr>
<tr class="even">
<td><p>Get-QueueDigest</p></td>
<td><p>Get-Recipient</p></td>
<td><p>Get-RemoteMailbox</p></td>
<td><p>Get-RoleGroup</p></td>
<td><p>Get-SecurityPrincipal</p></td>
</tr>
<tr class="odd">
<td><p>Get-StoreUsageStatistics</p></td>
<td><p>Get-UMMailbox</p></td>
<td><p>Get-User</p></td>
<td><p>Get-UserPhoto</p></td>
<td><p>Remove-Message</p></td>
</tr>
<tr class="even">
<td><p>Resume-Message</p></td>
<td><p>Resume-Queue</p></td>
<td><p>Retry-Queue</p></td>
<td><p>Suspend-Message</p></td>
<td><p>Suspend-Queue</p></td>
</tr>
</tbody>
</table>


## Filtrado del cliente

El filtrado del cliente se puede usar con cualquier cmdlet. Esto incluye a aquéllos que son compatibles con el filtrado del servidor. Como se ha descrito anteriormente en este tema, el filtrado del cliente acepta todos los datos devueltos por un comando anterior en el canal y, a cambio, devuelve solo los resultados que coinciden con el filtro que se especifica. El cmdlet **Where-Object** realiza este filtrado. **Where** puede ser la forma abreviada.

Conforme los datos pasan por el canal, el cmdlet **Where** recibe los datos del objeto anterior y, a continuación, filtra los datos antes de pasarlos al siguiente objeto. El filtrado se basa en un bloque de script definido en el comando **Where**. El bloque de script filtra los datos basados en las propiedades y los valores del objeto.

El cmdlet **Clear-Host** se usa para borrar la ventana de consola. En este ejemplo, puede encontrar todos los alias definidos para el cmdlet **Clear-Host** si ejecuta el siguiente comando:

    Get-Alias | Where {$_.Definition -eq "Clear-Host"}
    
    CommandType     Name                            Definition
    -----------     ----                            ----------
    Alias           clear                           clear-host
    Alias           cls                             clear-host

El cmdlet **Get-Alias** y el comando **Where** trabajan conjuntamente para devolver la lista de alias que se han definido solamente para el cmdlet **Clear-Host**. La siguiente tabla describe todos los elementos del comando **Where** que se usan en el ejemplo.

### Elementos del comando Where

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>{ }</code></p></td>
<td><p>Las llaves delimitan el bloque de script que define al filtro.</p></td>
</tr>
<tr class="even">
<td><p><code>$_</code></p></td>
<td><p>Esta variable especial se inicia automáticamente y se enlaza con los objetos del canal.</p></td>
</tr>
<tr class="odd">
<td><p><code>Definition</code></p></td>
<td><p>La propiedad <code>Definition</code> es la propiedad de los objetos del canal actual que almacena el nombre de la definición de alias. Cuando se usa <code>Definition</code> con la variable <code>$_</code>, hay un punto delante del nombre de propiedad.</p></td>
</tr>
<tr class="even">
<td><p><code>-eq</code></p></td>
<td><p>Este operador de comparación para &amp;quot;igual que&amp;quot; se usa para especificar que el resultado debe coincidir exactamente con el valor de la propiedad que se suministra en la expresión.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;<strong>Clear-Host</strong>&quot;</p></td>
<td><p>En este ejemplo, &quot;<strong>Clear-Host</strong>&quot; es el valor para el que está analizando el comando.</p></td>
</tr>
</tbody>
</table>


En el ejemplo, los objetos devueltos por el cmdlet **Get-Alias** representan todos los alias definidos en el sistema. Incluso aunque no los vea desde la línea de comandos, los alias se recopilan y pasan al cmdlet **Where** a través del canal. El cmdlet **Where** usa la información en el bloque de script para aplicar un filtro a los objetos del alias.

La variable especial `$`\_representa los objetos que se están pasando. El Shell inicia automáticamente la variable `$_` y esta se enlaza con el objeto de canal actual. Para obtener más información acerca de esta variable especial, vea [Variables de shell](https://technet.microsoft.com/es-es/library/bb124036\(v=exchg.150\)).

Mediante la notación con "punto" estándar (objeto.propiedad), se agrega la propiedad `Definition` para definir la propiedad exacta del objeto a evaluar. Luego, el operador de comparación `-eq` compara el valor de esta propiedad con `"Clear-Host"`. Solo los objetos que tienen la propiedad `Definition` que coincide con este criterio se pasan a la ventana de la consola para la salida. Para obtener más información acerca de los operadores de comparación, vea [Operadores de comparación](https://technet.microsoft.com/es-es/library/bb125229\(v=exchg.150\)).

Una vez que el comando **Where** ha filtrado los objetos devueltos por el cmdlet **Get-Alias**, se pueden canalizar los objetos filtrados a otro comando. El siguiente comando procesa solamente los objetos filtrados devueltos por el comando Where.

