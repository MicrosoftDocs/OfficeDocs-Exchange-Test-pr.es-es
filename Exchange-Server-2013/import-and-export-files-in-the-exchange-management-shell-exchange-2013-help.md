---
title: 'Importar y exportar archivos Shell administración Exchange: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Importación y exportación de archivos en el Shell de administración de Exchange
ms:assetid: b4b669e8-a3aa-4b0b-ad34-f1f15d9c9369
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638170(v=EXCHG.150)
ms:contentKeyID: 50556867
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importación y exportación de archivos en el Shell de administración de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Microsoft Exchange Server 2013 utiliza la comunicación remota de la interfaz de la línea de comandos de Windows PowerShell para establecer una conexión entre el servidor o la estación de trabajo desde la que administra Exchange y el servidor que ejecuta Exchange 2013 que está administrando. En Exchange 2013, esto se denomina Shell de administración de Exchange remoto o Shell remoto. Incluso si administra el servidor local de Exchange 2013, el shell remoto se utiliza para realizar la conexión. Para obtener más información acerca del shell local y remoto, consulte [Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\)).

El modo de importar y exportar archivos hacia y desde un servidor Exchange en Exchange 2013 varía respecto a cómo se hace en Exchange Server 2007. Esto se debe al uso del Shell remoto en Exchange 2013. Este tema expone por qué este nuevo proceso es necesario y cómo importar y exportar archivos entre un servidor o una estación de trabajo local y un servidor Exchange 2013.

## Sesiones de Windows PowerShell

Para comprender por qué es necesario utilizar una sintaxis especial para importar y exportar archivos en un shell remoto, es preciso saber cómo se ha implementado el shell en Exchange 2013. El shell utiliza sesiones de Windows PowerShell, que son los entornos en los que las variables, los cmdlets y otros componentes pueden compartir información. Cada vez que se abre una nueva ventana del shell, se crea una nueva sesión. Los cmdlets que se ejecutan en cada ventana pueden tener acceso a variables y otro tipo de información almacenada en esa ventana, pero no pueden tener acceso a las variables de otras ventanas de shell abiertas. Esto es porque cada uno está contenido en su propia sesión de Windows PowerShell. Las sesiones de Windows PowerShell también se llaman espacios de ejecución.

El shell remoto de Exchange 2013 tiene dos sesiones, la sesión local y la sesión remota. La sesión local es la sesión de Windows PowerShell que se ejecuta en el equipo local. Esa sesión contiene todos los cmdlets que se suministran con Windows PowerShell. También tiene acceso a su sistema de archivos local.

La sesión remota es la sesión de Windows PowerShell que se ejecuta en el servidor remoto de Exchange. Esa sesión es donde se ejecutan todos los cmdlets de Exchange. Y tiene acceso al sistema de archivos del servidor de Exchange.

Cuando se conecta a un servidor Exchange remoto, se establece una conexión entre la sesión local de su equipo y la sesión remota del servidor Exchange. Esta conexión permite ejecutar cmdlets de Exchange en el servidor remoto de Exchange en la sesión local, aunque el equipo local no tenga instalado ningún cmdlet de Exchange. Aunque parezca que los cmdlets de Exchange se están ejecutando en el equipo local, en realidad se están ejecutando en el servidor Exchange.


> [!IMPORTANT]
> Incluso si se abre el shell en un servidor de Exchange&nbsp;2013, se realiza el mismo proceso de conexión y se crean dos sesiones. Esto significa que es necesario utilizar la misma sintaxis nueva para importar y exportar archivos, independientemente de si se abre el Shell en un servidor Exchange&nbsp;2013 o desde una estación de trabajo cliente remota.



Los cmdlets de Exchange que se ejecutan en la sesión remota en el servidor remoto de Exchange no tienen acceso al sistema de archivos local. Esto significa que no se pueden utilizar cmdlets de Exchange por sí mismos para importar o exportar archivos hacia o desde el sistema local de archivos. Es necesario utilizar una sintaxis adicional para transferir los archivos hacia y desde el sistema local de archivos, de forma que los cmdlets de Exchange que se ejecutan en el servidor remoto de Exchange puedan utilizar los datos. Para obtener más información acerca de la sintaxis necesaria, consulte el apartado "Importación y exportación de archivos en el Shell remoto", más adelante en este tema.

## Importación y exportación de archivos en el Shell remoto

La importación y exportación de archivos requiere una sintaxis específica porque los servidores de buzones y de acceso de clientes usan el Shell remoto y no tienen acceso al sistema de archivos del equipo local.

## Importación de archivos en el Shell remoto

La sintaxis para importar archivos en Exchange 2013 se utiliza siempre que se desee enviar, desde el equipo o servidor local, un archivo a un cmdlet que se ejecuta en un servidor de Exchange 2013. Los cmdlets que aceptan datos procedentes de un archivo del equipo local tienen un parámetro llamado *FileData* (o algo parecido). Para determinar el parámetro correcto que hay que utilizar, consulte la información de ayuda del cmdlet que esté utilizando.

El shell tiene que saber qué archivo se desea enviar al cmdlet de Exchange 2013, así como qué parámetro aceptará los datos. Para ello, utilice la siguiente sintaxis:

    <Cmdlet> -FileData ([Byte[]]$(Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0))

Por ejemplo, el siguiente comando importa el archivo C:\\MyData.dat en el parámetro *FileData* del cmdlet ficticio **Import-SomeData**.

    Import-SomeData -FileData (Byte[]]$(Get-Content -Path "C:\MyData.dat" -Encoding Byte -ReadCount 0))

Al ejecutar el comando se producirán las siguientes acciones:

1.  El shell remoto acepta el comando.

2.  El shell remoto evalúa el comando y determina que existe un comando incrustado en el valor que se está proporcionando al parámetro *FileData*.

3.  El shell remoto deja de evaluar el comando **Import-SomeData** y ejecuta el comando **Get-Content**. El comando **Get-Content** lee los datos del archivo MyData.dat.

4.  El shell remoto almacena temporalmente los datos procedentes del comando **Get-Content** como un objeto de `Byte[]`, de forma que se puedan pasar al cmdlet **Import-SomeData**.

5.  Se reanuda la ejecución del comando **Import-SomeData**. El shell remoto envía la solicitud para ejecutar el cmdlet **Import-SomeData** al servidor remoto de Exchange 2013, junto con el objeto que se creó con el cmdlet **Get-Content**.

6.  En el servidor remoto de Exchange 2013, se ejecuta el cmdlet **Import-SomeData** y los datos almacenados en el objeto temporal que creó el cmdlet **Get-Content** se pasan al parámetro *FileData*. El cmdlet **Import-SomeData** procesa la entrada y realiza las acciones que sean necesarias.

Algunos cmdlets utilizan la siguiente sintaxis alternativa, que realiza lo mismo que la sintaxis anterior.

    [Byte[]]$Data = Get-Content -Path <local path to file> -Encoding Byte -ReadCount 0
    Import-SomeData -FileData $Data

El mismo proceso ocurre con esta sintaxis alternativa. La única diferencia reside en que, en vez de realizar toda la operación de una vez, los datos obtenidos del archivo local se almacenan en una variable a la que se puede hacer referencia, una vez creada. A continuación, la variable se utiliza en el comando de importación para pasar el contenido del archivo local al cmdlet **Import-SomeData**. Utilizar este proceso en dos fases resulta útil si se desea utilizar los datos del archivo local en más de un comando.

Al importar archivos, existen limitaciones que hay que tener en cuenta. Para obtener más información, consulte el apartado "Limitaciones de la importación de archivos", más adelante en este mismo tema.

Para obtener información específica acerca de cómo importar datos en Exchange 2013, consulte los temas de Ayuda de la característica que esté administrando.

## Limitaciones de la importación de archivos

Es necesario imponer límites cuando se importan datos al shell remoto para así proteger la integridad de los datos que se están transfiriendo. Las transferencias en curso no se pueden reanudar, si se interrumpen. Además, debido a que los datos que se están transfiriendo se almacenan en la memoria del servidor remoto, es necesario proteger al servidor de un agotamiento de la memoria originado por cantidades excesivamente grandes de datos.

Por estos motivos, la cantidad de datos que se transfieren a un servidor remoto de Exchange 2013 desde un equipo o un servidor local se limita a lo siguiente:

  - 500 MB para cada cmdlet que se ejecuta

  - 75 MB por cada objeto que se pasa a un cmdlet

Si se supera cualquiera de estos límites, la ejecución del cmdlet y su canalización asociada se detendrán, y se recibirá un error. Tenga en cuenta los ejemplos de la siguiente tabla para comprender cómo funcionan estos límites.

### Ejemplos de límite de importación de datos

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Número de objetos</th>
<th>Tamaño del objeto (MB)</th>
<th>Tamaño total (MB)</th>
<th>Resultado de la operación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10</p></td>
<td><p>40</p></td>
<td><p>400</p></td>
<td><p>La operación es satisfactoria porque ni el tamaño de los objetos individuales supera los 75 MB, ni la cantidad total de datos pasados al cmdlet supera los 500 MB.</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>80</p></td>
<td><p>400</p></td>
<td><p>La operación da un error porque, si bien la cantidad total de datos pasados al cmdlet es sólo de 400 MB, el tamaño de cada objeto individual supera el límite de los 75 MB.</p></td>
</tr>
<tr class="odd">
<td><p>120</p></td>
<td><p>5</p></td>
<td><p>600</p></td>
<td><p>La operación da un error porque, si bien cada objeto individual es sólo de 5 MB, el tamaño total de los datos pasados al cmdlet supera el límite de los 500 MB.</p></td>
</tr>
</tbody>
</table>


Debido a las restricciones de tamaño que se han impuesto sobre la cantidad de datos que se pueden transferir entre un servidor remoto de Exchange 2013 y un equipo local, no todos los cmdlets que una vez admitieron la importación admitirán este método de transferencia de datos. Para determinar si un determinado cmdlet admite este método, consulte la información de la Ayuda del cmdlet específico.

Estos límites deberían permitir la mayoría de las operaciones que se suelen realizar en un servidor de Exchange 2013. Si los límites se reducen, es posible que descubra que algunas operaciones normales no se pueden realizar porque superan los nuevos límites. Si los límites se elevan, los datos podrían tardar más en transferirse y quedarían más expuestos a las condiciones transitorias que interrumpen su transferencia. Asimismo, si no se ha instalado memoria suficiente para que el servidor pueda almacenar todo el bloque de datos durante la transferencia, es posible que se agote la memoria. Cada una de estas posibilidades podría dar como resultado la pérdida de datos y, por lo tanto, recomendamos no cambiar los límites predeterminados.

## Exportación de archivos en el Shell remoto

La sintaxis para exportar archivos en Exchange 2013 se utiliza siempre que se desea aceptar los datos procedentes de un cmdlet que se ejecuta en un servidor remoto de Exchange 2013 y guardarlos en el equipo o el servidor local. Los cmdlets que proporcionan datos que se pueden guardar en un archivo local generarán un objeto que contendrá la propiedad **FileData** (u otra parecida). Según el cmdlet, la propiedad **FileData** sólo se rellena en el objeto que se produce en determinadas situaciones. Para determinar la propiedad correcta que hay que utilizar, y cuándo se puede utilizar, consulte la información de la Ayuda del cmdlet que esté usando.

El shell tiene que saber que se desea guardar en el equipo local los datos almacenados en la propiedad **FileData**. Para ello, utilice la siguiente sintaxis:

    <cmdlet> | ForEach { $_.FileData | Add-Content <local path to file> -Encoding Byte }

Por ejemplo, el siguiente comando exporta los datos almacenados en la propiedad **FileData** en el objeto creado por el cmdlet ficticio **Export-SomeData**. Los datos exportados se almacenan en un archivo que se especifica en el equipo local, en este caso, MyData.dat.


> [!NOTE]
> Este procedimiento utiliza el cmdlet, los objetos y la canalización de <STRONG>ForEach</STRONG>. Para obtener más información acerca de cada uno de ellos, consulte <A href="https://technet.microsoft.com/es-es/library/aa998260(v=exchg.150)">Canalización</A> y <A href="https://technet.microsoft.com/es-es/library/aa996386(v=exchg.150)">Datos estructurados</A>.



    Export-SomeData | ForEach { $_.FileData | Add-Content C:\MyData.dat -Encoding Byte }

Al ejecutar el comando se producirán las siguientes acciones:

1.  El shell remoto acepta el comando.

2.  El shell remoto llama al cmdlet **Export-SomeData** en el servidor remoto de Exchange 2013.

3.  El objeto de salida creado por el cmdlet **Export-SomeData** se devuelve a la sesión del shell local a través de la canalización.

4.  A continuación, el objeto de salida se transporta por la canalización hasta el cmdlet **ForEach**, que tiene un bloque de script.

5.  Dentro del bloque de script se tiene acceso a la propiedad **FileData** del objeto actual de la canalización. Los datos contenidos dentro de la propiedad **FileData** se canalizan hasta el cmdlet **Add-Content**.

6.  El cmdlet **Add-Content** guarda los datos enviados desde la propiedad **FileData** en el archivo MyData.dat, dentro del sistema local de archivos.

Para obtener información específica acerca de cómo exportar datos desde Exchange 2013, consulte los temas de Ayuda de la característica que esté administrando.

