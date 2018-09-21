---
title: 'Modificación de propiedades multivalor: Exchange 2013 Help'
TOCTitle: Modificación de propiedades multivalor
ms:assetid: dc2c1062-ad79-404b-8da3-5b5798dbb73b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb684908(v=EXCHG.150)
ms:contentKeyID: 49116582
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificación de propiedades multivalor

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Una propiedad con varios valores es una propiedad que puede tener más de un valor. Por ejemplo, la propiedad **BlockedRecipients** del objeto **RecipientFilterConfig** puede aceptar varias direcciones de destinatario, tal y como se muestra en los ejemplos siguientes:

  - john@contoso.com

  - kim@northwindtraders.com

  - david@adatum.com

Dado que la propiedad **BlockedRecipients** acepta más de un valor, se le llama propiedad con varios valores. En este tema se explica cómo usar el Shell de administración de Exchange para agregar o quitar valores de una propiedad con varios valores en un objeto.

Para obtener más información acerca de los objetos, vea [Datos estructurados](https://technet.microsoft.com/es-es/library/aa996386\(v=exchg.150\)). Para obtener más información acerca del Shell, vea [Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\)).

## Modificación de una propiedad multivalor frente a la modificación de una propiedad que acepta un solo valor

El modo en que se modifica una propiedad con varios valores es ligeramente diferente al que se usa para modificar una propiedad que acepta un único valor. Cuando se modifica una propiedad que acepta un sólo valor, se le puede asignar un valor directamente, tal y como se muestra en el comando siguiente.

```powershell
Set-TransportConfig -MaxSendSize 12MB
```

Cuando usa este comando para proporcionar un nuevo valor a la propiedad **MaxSendSize**, el valor almacenado se sobrescribe. Esto no constituye un problema en el caso de las propiedades que aceptan un único valor. Sin embargo, sí lo es en el caso de las propiedades con varios valores. Por ejemplo, supongamos que la propiedad **BlockedRecipients** del objeto **RecipientFilterConfig** está configurada para tener los tres valores que se indicaban en la sección anterior. Al ejecutar el comando `Get-RecipientFilterConfig | Format-List BlockedRecipients`, se muestra lo siguiente.

```powershell
BlockedRecipients : {david@adatum.com, kim@northwindtraders.com, john@contoso.com}
```

Supongamos ahora que ha recibido la solicitud para agregar una nueva dirección SMTP a la lista de destinatarios bloqueados. Ejecuta el comando siguiente para agregar la nueva dirección SMTP.

```powershell
Set-RecipientFilterConfig -BlockedRecipients chris@contoso.com
```

Cuando vuelva a ejecutar el comando `Get-RecipientFilterConfig | Format-List BlockedRecipients`, verá lo siguiente.

```powershell
BlockedRecipients : {chris@contoso.com}
```

Esto no es lo que usted esperaba. Lo que quería era agregar la dirección SMTP nueva a la lista de destinatarios bloqueados existente. Pero en lugar de ello se ha sobrescrito la lista de destinatarios bloqueados existente con la nueva dirección SMTP. Este resultado no esperado es un ejemplo de cómo la modificación de una propiedad con varios valores es diferente de la modificación de una propiedad que acepta un solo valor. Al modificar una propiedad con varios valores se debe estar seguro de que se anexan o quitan valores en lugar de sobrescribir la totalidad de la lista de los mismos. Las siguientes secciones muestran exactamente cómo hacerlo.

## Modificación de propiedades multivalor

La modificación de propiedades con varios valores es similar a la modificación de propiedades con un solo valor. Solo tiene que agregar sintaxis adicional para indicar al Shell que desea agregar o quitar valores a la propiedad con varios valores, en vez de sustituir todo lo que está almacenado en la propiedad. La sintaxis se incluye, junto con el valor o valores que desee agregar o quitar a la propiedad, como un valor en un parámetro cuando ejecuta un cmdlet. En la tabla siguiente se muestra la sintaxis que es preciso agregar a un parámetro de un cmdlet para modificar las propiedades con varios valores.

### Sintaxis de la propiedad con varios valores

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Sintaxis</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agregar uno o más valores a una propiedad con varios valores</p></td>
<td><pre><code>@{Add=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Quitar uno o más valores de una propiedad con varios valores</p></td>
<td><pre><code>@{Remove=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}</code></pre></td>
</tr>
</tbody>
</table>


La sintaxis que elija en la tabla de sintaxis de las propiedades con varios valores se especifica como valor de parámetro en un cmdlet. Por ejemplo, el comando siguiente agrega varios valores en una propiedad con varios valores:

```powershell
Set-ExampleCmdlet -Parameter @{Add="Red", "Blue", "Green"}
```

Cuando use esta sintaxis, los valores que especifique se agregarán o eliminarán de la lista de valores que la propiedad ya tiene. Si retomamos el ejemplo anterior de **BlockedRecipients** expuesto en este tema, ahora podemos agregar chris@contoso.com sin sobrescribir el resto de valores de esta propiedad, ejecutando el comando siguiente:

```powershell
Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"}
```

Si quiere quitar david@adatum.com de la lista de valores, debería ejecutar el comando siguiente:

```powershell
Set-RecipientFilterConfig -BlockedRecipients @{Remove="david@adatum.com"}
```

Se pueden usar combinaciones más complejas como, por ejemplo, agregar o quitar valores de una propiedad al mismo tiempo. Para ello, debe insertar un punto y coma (`;`) entre las acciones `Add` y `Remove`. Por ejemplo:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="carter@contoso.com", "sam@northwindtraders.com", "brian@adatum.com"; Remove="john@contoso.com"}

Si volvemos a ejecutar el comando `Get-RecipientFilterConfig | Format-List BlockedRecipients`, veremos que las direcciones de correo electrónico de Carter, Sam y Brian se han agregado y que la dirección de John se ha eliminado.

    BlockedRecipients : {brian@adatum.com, sam@northwindtraders.com, carter@contoso.com, chris@contoso.com, kim@northwindtraders.com}

