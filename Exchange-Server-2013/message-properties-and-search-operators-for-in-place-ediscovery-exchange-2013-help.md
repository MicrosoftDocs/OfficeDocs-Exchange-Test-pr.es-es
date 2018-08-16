---
title: 'Propiedades de mensajes y operadores de búsqueda para eDiscovery local'
TOCTitle: Propiedades de mensajes y operadores de búsqueda para la exhibición de documentos electrónicos local
ms:assetid: 402b74e4-8853-4c51-9737-1a9c19f8e3dd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn774955(v=EXCHG.150)
ms:contentKeyID: 62622198
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Propiedades de mensajes y operadores de búsqueda para la exhibición de documentos electrónicos local

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En este tema se describen las propiedades de los mensajes de correo electrónico de Exchange que se pueden buscar mediante la exhibición de documentos electrónicos y la retención local en Exchange Server 2013 y Exchange Online. En este tema también se describen los operadores de búsqueda booleanos y otras técnicas de consulta de búsqueda que se pueden usar para refinar los resultados de la búsqueda de exhibición de documentos electrónicos.

La exhibición de documentos electrónicos local usa el lenguaje de consulta de palabras clave (KQL). Para más detalles, vea [Referencia de sintaxis de lenguaje de consulta de palabras clave](https://go.microsoft.com/fwlink/?linkid=269603).

## Propiedades que permiten búsqueda en Exchange

En la tabla siguiente se enumeran las propiedades de los mensajes de correo electrónico que se pueden buscar mediante una búsqueda de exhibición de documentos electrónicos local o mediante el cmdlet **New-MailboxSearch** o **Set-MailboxSearch**. La tabla incluye un ejemplo de la sintaxis *propiedad:valor* de cada propiedad y una descripción de los resultados de búsqueda devueltos por los ejemplos.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Propiedad</th>
<th>Descripción de la propiedad</th>
<th>Ejemplos</th>
<th>Resultados de la búsqueda devueltos por los ejemplos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>Los nombres de los archivos adjuntos a un mensaje de correo electrónico.</p></td>
<td><p>attachment:informeanual.ppt</p>
<p>attachment:anual*</p></td>
<td><p>Los mensajes con un archivo adjunto denominado informeanual.ppt.</p>
<p>En el segundo ejemplo, el uso del comodín devuelve los mensajes con la palabra &quot;anual&quot; en el nombre de un archivo adjunto.</p></td>
</tr>
<tr class="even">
<td><p>Bcc</p></td>
<td><p>El campo CCO de un mensaje de correo electrónico.1</p></td>
<td><p>bcc:pilarp@contoso.com</p>
<p>bcc:pilarp</p>
<p>bcc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>Todos los ejemplos devuelven los mensajes que incluyen a Pilar Pinilla en el campo CCO.</p></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>Las categorías para buscar. Los usuarios pueden definir las categorías mediante Outlook o Outlook Web App. Los valores posibles son:</p>
<ul>
<li><p>azul</p></li>
<li><p>verde</p></li>
<li><p>naranja</p></li>
<li><p>púrpura</p></li>
<li><p>rojo</p></li>
<li><p>amarillo</p></li>
</ul></td>
<td><p>category:=&quot;Categoría roja&quot;</p></td>
<td><p>Los mensajes a los que se ha asignado la categoría roja en los buzones de origen.</p></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>El campo CC de un mensaje de correo electrónico.1</p></td>
<td><p>cc:pilarp@contoso.com</p>
<p>cc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>En ambos ejemplos, los mensajes que especifican a Pilar Pinilla en el campo CC.</p></td>
</tr>
<tr class="odd">
<td><p>De</p></td>
<td><p>El remitente de un mensaje de correo electrónico.1</p></td>
<td><p>from:pilarp@contoso.com</p>
<p>from:contoso.com</p></td>
<td><p>Los mensajes enviados por el usuario especificado o enviados desde un dominio especificado.</p></td>
</tr>
<tr class="even">
<td><p>Importance</p></td>
<td><p>La importancia de un mensaje de correo electrónico, que un remitente puede especificar al enviar un mensaje. De manera predeterminada, los mensajes se envían con importancia normal, a menos que el remitente establezca la importancia como <strong>alta</strong> o <strong>baja</strong>.</p></td>
<td><p>importance:alta</p>
<p>importance:media</p>
<p>importance:baja</p></td>
<td><p>Los mensajes que están marcados con importancia alta, importancia media o importancia baja.</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>El tipo de mensaje para buscar. Valores posibles:</p>
<ul>
<li><p>contactos</p></li>
<li><p>documentos</p></li>
<li><p>correo electrónico</p></li>
<li><p>faxes</p></li>
<li><p>mensajería instantánea</p></li>
<li><p>diarios</p></li>
<li><p>reuniones</p></li>
<li><p>notas</p></li>
<li><p>entradas</p></li>
<li><p>fuentes rss</p></li>
<li><p>tareas</p></li>
<li><p>correo de voz</p></li>
</ul></td>
<td><p>kind:email</p>
<p>kind:email OR kind:im OR kind:voicemail</p></td>
<td><p>Los mensajes de correo electrónico que cumplen los criterios de búsqueda. El segundo ejemplo devuelve los mensajes de correo electrónico, las conversaciones de mensajería instantánea y los mensajes de voz que cumplen los criterios de búsqueda.</p></td>
</tr>
<tr class="even">
<td><p>Participantes</p></td>
<td><p>Todos los campos de personas en un mensaje de correo electrónico. Estos campos son De, Para, CC y CCO.1</p></td>
<td><p>participants:garthf@contoso.com</p>
<p>participants:contoso.com</p></td>
<td><p>Los mensajes enviados por o a garthf@contoso.com.</p>
<p>El segundo ejemplo devuelve todos los mensajes enviados por o a un usuario en el dominio contoso.com.</p></td>
</tr>
<tr class="odd">
<td><p>Received</p></td>
<td><p>La fecha en la que un destinatario recibió un mensaje de correo electrónico.</p></td>
<td><p>received:15/04/2014</p>
<p>received&gt;=01/01/2014 AND received&lt;=31/03/2014</p></td>
<td><p>Mensajes que se recibieron el 15 de abril de 2014. El segundo ejemplo devuelve todos los mensajes recibidos entre el 1 de enero de 2014 y el 31 de marzo de 2014.</p></td>
</tr>
<tr class="even">
<td><p>Destinatarios</p></td>
<td><p>Todos los campos de destinatarios en un mensaje de correo electrónico. Estos campos son Para, CC y CCO.1</p></td>
<td><p>recipients:garthf@contoso.com</p>
<p>recipients:contoso.com</p></td>
<td><p>Mensajes enviados a garthf@contoso.com.</p>
<p>El segundo ejemplo devuelve los mensajes enviados a todos los destinatarios en el dominio contoso.com.</p></td>
</tr>
<tr class="odd">
<td><p>Sent</p></td>
<td><p>La fecha en la que un remitente envió un mensaje de correo electrónico.</p></td>
<td><p>sent:01/07/2014</p>
<p>sent&gt;=01/06/2014 AND sent&lt;=01/07/2014</p></td>
<td><p>Mensajes que se enviaron en la fecha especificada o que se enviaron dentro del intervalo de fechas especificado.</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>El tamaño de un elemento, en bytes.</p></td>
<td><p>tamaño&gt;26214400</p>
<p>size:1..1048576</p></td>
<td><p>Mensajes de más de 25 MB.</p>
<p>El segundo ejemplo devuelve los mensajes que tienen un tamaño comprendido entre 1 y 1.048.576 bytes (1 MB).</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>El texto en la línea de asunto de un mensaje de correo electrónico.</p></td>
<td><p>subject:&quot;Finanzas trimestrales&quot;</p>
<p>subject:northwind</p></td>
<td><p>Mensajes que contienen la frase exacta &quot;Finanzas trimestrales&quot; en cualquier lugar de la línea de asunto.</p>
<p>El segundo ejemplo devuelve todos los mensajes que contienen la palabra northwind en la línea de asunto.</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>El campo Para de un mensaje de correo electrónico.1</p></td>
<td><p>to:annb@contoso.com</p>
<p>to:annb</p>
<p>to:&quot;Ann Beebe&quot;</p></td>
<td><p>Todos los ejemplos devuelven mensajes en los que Ann Beebe está especificada en la línea Para.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp;En el caso del valor de una propiedad de destinatario, puede usar la dirección SMTP, el nombre para mostrar o el alias para especificar un usuario. Por ejemplo, para especificar el usuario Ann Beebe, puede usar annb@contoso.com, annb o "Ann Beebe".



## Operadores de búsqueda compatibles

Los operadores de búsqueda booleanos, tales como **AND** y **OR**, ayudan a definir búsquedas de buzón más precisas mediante la inclusión o exclusión de palabras específicas en la consulta de búsqueda. Otras técnicas, como el uso de operadores de propiedad (como \>= o ..), comillas, paréntesis y comodines, le ayudan a precisar las consultas de búsqueda de exhibición de documentos electrónicos. En la siguiente tabla se muestran los operadores que puede usar para restringir o ampliar los resultados de la búsqueda.


> [!IMPORTANT]
> Debe usar operadores booleanos en mayúsculas en una consulta de búsqueda. Por ejemplo, use <STRONG>AND</STRONG> en lugar de <STRONG>and</STRONG>. El uso de operadores en minúsculas en las consultas de búsqueda devolverá un error.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Operador</th>
<th>Uso</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AND</p></td>
<td><p>palabra clave 1 AND palabra clave 2</p></td>
<td><p>Devuelve los mensajes que incluyen todas las palabras clave especificadas o expresiones <code>property:value</code>.</p></td>
</tr>
<tr class="even">
<td><p>+</p></td>
<td><p>palabra clave 1 + palabra clave 2 + palabra clave 3</p></td>
<td><p>Devuelve elementos que contienen <em>o</em><code>keyword2 </code>o <code>keyword3</code><em>y</em> que también contienen <code>keyword1</code>. Por tanto, este ejemplo es equivalente a la consulta <code>(keyword2 OR keyword3) AND keyword1</code>.</p>
<p>Tenga en cuenta que la consulta <code>keyword1 + keyword2</code> (con un espacio después del símbolo <strong>+</strong>) no es lo mismo que usar el operador <strong>AND</strong>. Esta consulta sería equivalente a <code>&quot;keyword1 + keyword2&quot;</code> y devolvería elementos con la frase <code>&quot;keyword1 + keyword2&quot;</code> exacta.</p></td>
</tr>
<tr class="odd">
<td><p>OR</p></td>
<td><p>palabra clave 1 OR palabra clave 2</p></td>
<td><p>Devuelve los mensajes que incluyen una o varias de las palabras clave especificadas o expresiones <code>property:value</code>.</p></td>
</tr>
<tr class="even">
<td><p>NOT</p></td>
<td><p>palabra clave 1 NOT palabra clave 2</p>
<p>NOT from:&quot;Ann Beebe&quot;</p></td>
<td><p>Excluye los mensajes especificados por una palabra clave o una expresión <code>property:value</code>. Por ejemplo, <code>NOT from:&quot;Ann Beebe&quot;</code> excluye los mensajes enviados por Ann Beebe.</p></td>
</tr>
<tr class="odd">
<td><p>-</p></td>
<td><p>palabra clave 1 - palabra clave 2</p></td>
<td><p>Igual que el operador <strong>NOT</strong>. Esta consulta devuelve los elementos que contienen <code>keyword1</code> y excluye los elementos que contienen <code>keyword2</code>.</p></td>
</tr>
<tr class="even">
<td><p>NEAR</p></td>
<td><p>palabra clave 1 NEAR(n) palabra clave 2</p></td>
<td><p>Devuelve los mensajes con palabras cercanas entre sí, donde &quot;n&quot; indica el número de palabras que las separan. Por ejemplo, <code>best NEAR(5) worst</code> devuelve los mensajes en los que la palabra &quot;worst&quot; está a cinco palabras de &quot;best&quot;. Si no se especifica ningún número, la distancia predeterminada es de ocho palabras.</p></td>
</tr>
<tr class="odd">
<td><p>:</p></td>
<td><p>propiedad:valor</p></td>
<td><p>Los dos puntos (:) en la sintaxis <code>property:value</code> especifican que el valor de la propiedad que se busca equivale al valor especificado. Por ejemplo, <code>recipients:garthf@contoso.com</code> devuelve cualquier mensaje enviado a garthf@contoso.com.</p></td>
</tr>
<tr class="even">
<td><p>&lt;</p></td>
<td><p>propiedad&lt;valor</p></td>
<td><p>Indica que la propiedad que se busca es menor que el valor especificado. 1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;</p></td>
<td><p>propiedad&gt;valor</p></td>
<td><p>Indica que la propiedad que se busca es mayor que el valor especificado.1</p></td>
</tr>
<tr class="even">
<td><p>&lt;=</p></td>
<td><p>propiedad&lt;=valor</p></td>
<td><p>Indica que la propiedad que se busca es menor o igual que un valor especificado.1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;=</p></td>
<td><p>propiedad&gt;=valor</p></td>
<td><p>Indica que la propiedad que se busca es mayor o igual que un valor especificado.1</p></td>
</tr>
<tr class="even">
<td><p>..</p></td>
<td><p>property:value1..value2</p></td>
<td><p>Indica que la propiedad que se busca es mayor o igual que el valor 1 y menor o igual que el valor 2.1</p></td>
</tr>
<tr class="odd">
<td><p>&quot; &quot;</p></td>
<td><p>&quot;valor razonable&quot;</p>
<p>subject:&quot;Finanzas trimestrales&quot;</p></td>
<td><p>Use comillas dobles (&quot; &quot;) para buscar una frase o término exacto en la palabra clave y consultas de búsqueda <code>property:value</code>.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>cat*</p>
<p>subject:set*</p></td>
<td><p>Las búsquedas con caracteres comodín de prefijo (donde el asterisco se coloca al final de una palabra) coinciden con cero o más caracteres en palabras clave o consultas <code>property:value</code>. Por ejemplo, <code>subject:set*</code> devuelve los mensajes que contienen la palabra set, setup y setting (y otras palabras que empiezan con &quot;set&quot;) en la línea de asunto.</p></td>
</tr>
<tr class="odd">
<td><p>( )</p></td>
<td><p>(razonable OR libre) AND from:contoso.com</p>
<p>(IPO OR inicial) AND (acciones OR cuotas)</p>
<p>(finanzas trimestrales)</p></td>
<td><p>Los paréntesis agrupan frases booleanas, elementos <code>property:value</code> y palabras clave. Por ejemplo, <code>(quarterly financials)</code> devuelve los elementos que contienen las palabras trimestral y finanzas.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp;Use este operador para las propiedades que tengan valores numéricos o de fecha.



## Caracteres no admitidos en las consultas de búsqueda

Los caracteres no admitidos en las consultas de búsqueda normalmente provocan un error de búsqueda o devuelven resultados no intencionados. Los caracteres no admitidos a menudo están ocultos y normalmente se agregan a una consulta cuando copia la consulta o partes de esta desde otras aplicaciones (como Microsoft Word o Microsoft Excel), y las copia al cuadro de palabras clave en la página de consulta de la búsqueda de In-Place eDiscovery.

Aquí se muestra una lista de los caracteres no admitidos para una consulta de búsqueda de In-Place eDiscovery.

  - **Comillas inteligentes**   Las comillas inteligentes simples y dobles (también denominadas *comillas inglesas*) no se admiten. Solo pueden usarse las comillas tipográficas en una consulta de búsqueda.

  - **Caracteres de control no imprimibles**   Los caracteres de control no imprimibles no representan un símbolo escrito, como un carácter alfanumérico. Los ejemplos de caracteres de control no imprimibles incluyen caracteres que aplican formato al texto o que separan líneas de texto.

  - **Marcas de izquierda a derecha y de derecha a izquierda**   Estos caracteres de control se usan para indicar la dirección del texto en los idiomas que se escriben de izquierda a derecha (como el inglés y el español) y en los que se escriben de derecha a izquierda (como el árabe y el hebreo).

  - **Operadores booleanos en minúsculas**   Como se ha explicado anteriormente, tiene que usar operadores booleanos en mayúsculas, como **AND** y **OR**, en una consulta de búsqueda. Tenga en cuenta que la sintaxis de consulta a menudo indicará que se está usando un operador booleano, aunque pueden usarse operadores en minúsculas; por ejemplo, `(WordA or WordB) and (WordC or WordD)`.

**¿Cómo puede evitar los caracteres no admitidos en sus consultas de búsqueda?**La mejor manera de evitar los caracteres no admitidos es escribir la consulta en el cuadro de palabras clave. De manera alternativa, puede copiar una consulta de Word o Excel y, después, pegarla en un archivo de un editor de texto sin formato, como Microsoft Notepad. Después, guarde el archivo de texto y seleccione **ANSI** en la lista desplegable **Codificación**. Esto quitará cualquier carácter no admitido y de formato. Después, puede copiar y pegar la consulta del archivo de texto al cuadro de consulta de palabras clave.

## Trucos y sugerencias de búsqueda

  - Las búsquedas de palabras clave no distinguen entre mayúsculas y minúsculas. Por ejemplo, tanto si escribe **gato** como **GATO**, obtendrá los mismos resultados.

  - Un espacio entre dos palabras clave o dos expresiones `property:value` equivale a usar **AND**. Por ejemplo, `from:"Sara Davis" subject:reorganization` devuelve todos los mensajes enviados por Sara Davis que contienen la palabra **reorganización** en la línea del asunto.

  - Use una sintaxis que coincida con el formato `property:value`. Los valores no distinguen entre mayúsculas y minúsculas, y no pueden tener un espacio después del operador. Si hay un espacio, solo se buscará el texto completo del valor proporcionado. Por ejemplo, **to: pilarp** busca "pilarp" como palabra clave, en vez de buscar mensajes que se enviaron a pilarp.

  - Al buscar una propiedad de destinatario, como Para, De, Cc o los destinatarios, puede utilizar una dirección SMTP, un alias o un nombre para mostrar para indicar un destinatario. Por ejemplo, puede utilizar pilarp@contoso.com, pilarp o "Pilar Pinilla".

  - Puede usar solo búsquedas con caracteres comodín de prefijo, por ejemplo, **cat\*** o **set\***. No se admiten las búsquedas con caracteres comodín de sufijo (\*cat) o las búsquedas con caracteres comodín de subcadena (\*cat\*).

  - Al buscar una propiedad, use comillas dobles (" ") si el valor de búsqueda consta de varias palabras. Por ejemplo, **subject:presupuesto T1** devuelve los mensajes que contienen **presupuesto** en la línea de asunto y que contienen **T1** en cualquier parte del mensaje o en cualquiera de las propiedades del mensaje. El uso de **subject:"presupuesto T1"** devuelve todos los mensajes que contienen **presupuesto T1** en cualquier lugar de la línea de asunto.

