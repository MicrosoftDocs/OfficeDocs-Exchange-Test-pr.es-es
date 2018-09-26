---
title: 'Propiedades a las que se puede aplicar un filtro para el parámetro -ContentFilter: Exchange 2013 Help'
TOCTitle: Propiedades a las que se puede aplicar un filtro para el parámetro -ContentFilter
ms:assetid: cf504a59-1938-489c-bb48-b27b2ac3234e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff601762(v=EXCHG.150)
ms:contentKeyID: 50556885
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Propiedades a las que se puede aplicar un filtro para el parámetro -ContentFilter

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-09-10_

En este tema se enumeran las propiedades que se pueden filtrar para el parámetro *ContentFilter*. El parámetro *ContentFilter* se utiliza para exportar a un archivo .pst los mensajes que coinciden con el filtro. El parámetro *ContentFilter* se utiliza en el cmdlet [New-MailboxExportRequest](https://technet.microsoft.com/es-es/library/ff607299\(v=exchg.150\)).

## Propiedades que se pueden filtrar

Muchas de las propiedades del parámetro *ContentFilter* aceptan caracteres comodín. Si utiliza un carácter comodín, use el operador **-like** en lugar del operador **-eq**. El operador **-like** se usa para buscar coincidencias de modelos en tipos enriquecidos, como las cadenas, mientras que el operador **-eq** se usa para buscar coincidencias exactas.

La tabla siguiente contiene una lista de las propiedades que se pueden filtrar para el parámetro *ContentFilter*. En esta tabla se enumera el nombre de la propiedad, una descripción, los valores aceptables y un ejemplo de sintaxis. Para obtener más información acerca de los filtros OPATH, vea [Filtros en los comandos de Shell del destinatario](https://technet.microsoft.com/es-es/library/bb124268\(v=exchg.150\)).


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
<th>Descripción</th>
<th>Valores</th>
<th>Ejemplo de sintaxis</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Todos</p></td>
<td><p>Esta propiedad devuelve todos los mensajes que tienen una cadena concreta en cualquiera de las propiedades indizadas. Por ejemplo, use esta propiedad si desea exportar todos los mensajes que tiene &quot;Ayla&quot; como destinatario o como remitente, o que mencionan ese nombre en el cuerpo del mensaje.</p></td>
<td><p>Cadena</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {All -like '*Ayla*'}
```

</td>
</tr>
<tr class="even">
<td><p>Archivo de datos adjuntos</p></td>
<td><p>Esta propiedad devuelve los mensajes que tienen la cadena especificada en el nombre o en el contenido de un archivo de datos adjuntos.</p></td>
<td><p>Cadena</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {Attachment -like '*.jpg'}
```

</td>
</tr>
<tr class="odd">
<td><p>CCO</p></td>
<td><p>Esta propiedad devuelve los mensajes enviados que tienen el destinatario especificado en el campo CCO.</p></td>
<td><p>Nombre para mostrar</p>
<p>Alias</p>
<p>Dirección SMTP</p>
<p>LegacyDN</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {(BCC -eq 'ayla@contoso.com') -or (BCC -eq 'tony@contoso.com')}
```

</td>
</tr>
<tr class="even">
<td><p>Cuerpo</p></td>
<td><p>Esta propiedad devuelve los mensajes que tienen la cadena especificada en el cuerpo del mensaje.</p></td>
<td><p>Cadena</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {Body -like '*prospectus*'}
```

</td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>Esta propiedad devuelve los mensajes cuya categoría coincide. Las categorías se establecen mediante reglas de la Bandeja de entrada o de los usuarios.</p></td>
<td><p>Cadena</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {Category -like '*Blue*'}
```

</td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>Esta propiedad devuelve los mensajes enviados que tienen el destinatario especificado en el campo CC.</p></td>
<td><p>Nombre para mostrar</p>
<p>Alias</p>
<p>Dirección SMTP</p>
<p>LegacyDN</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {(CC -eq 'ayla@contoso.com') -or (CC -eq 'tony@contoso.com')}
```

</td>
</tr>
<tr class="odd">
<td><p>Caduca</p></td>
<td><p>Esta propiedad devuelve los mensajes que tienen la marca de fecha de caducidad especificada.</p></td>
<td><p>Marca de fecha y hora</p></td>
<td>

```powershell
-ContentFilter {Expires -lt '01/01/2013'}
```

</td>
</tr>
<tr class="even">
<td><p>HasAttachment</p></td>
<td><p>Esta propiedad devuelve los mensajes con o sin datos adjuntos.</p></td>
<td><p>Booleano</p>
<p><code>$true</code> o <code>$false</code></p></td>
<td>

```powershell
-ContentFilter {HasAttachment -eq $true}
```

</td>
</tr>
<tr class="odd">
<td><p>Importancia</p></td>
<td><p>Esta propiedad devuelve los mensajes que tienen un nivel de importancia especificado.</p></td>
<td><p>0 o &quot;Baja&quot;</p>
<p>1 o &quot;Normal&quot;</p>
<p>2 o &quot;Alta&quot;</p></td>
<td>

```powershell
-ContentFilter {Importance -eq 'high'}
```




```powershell
-ContentFilter {Importance -eq 2}
```

</td>
</tr>
<tr class="even">
<td><p>IsFlagged</p></td>
<td><p>Esta propiedad devuelve los mensajes marcados por las reglas de la Bandeja de entrada o de los usuarios.</p></td>
<td><p>Booleano</p>
<p><code>$true</code> o <code>$false</code></p></td>
<td>

```powershell
-ContentFilter {IsFlagged -eq $true}
```

</td>
</tr>
<tr class="odd">
<td><p>IsRead</p></td>
<td><p>Esta propiedad devuelve los mensajes leídos o sin leer.</p></td>
<td><p>Booleano</p>
<p><code>$true</code> o <code>$false</code></p></td>
<td>

```powershell
-ContentFilter {IsRead -eq $true}
```

</td>
</tr>
<tr class="even">
<td><p>MessageKind</p></td>
<td><p>Esta propiedad devuelve los mensajes que son del tipo especificado.</p></td>
<td><p>Calendario</p>
<p>Contacto</p>
<p>Doc</p>
<p>Email</p>
<p>Fax</p>
<p>InstantMessage</p>
<p>Diario</p>
<p>Nota</p>
<p>Entrada</p>
<p>RSSFeed</p>
<p>Tarea</p>
<p>Voicemail</p></td>
<td>

```powershell
-ContentFilter {MessageKind -eq 'Calendar'}
```




```powershell
-ContentFilter {MessageKind -ne 'Email'}
```

</td>
</tr>
<tr class="odd">
<td><p>MessageLocalee</p></td>
<td><p>Esta propiedad devuelve los mensajes de la configuración regional especificada.</p></td>
<td><p>CultureInfo</p></td>
<td>

```powershell
-ContentFilter {MessageLocale -ne 'en-US'}
```




```powershell
-ContentFilter {MessageLocale -eq 'tr-TR'}
```

</td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>Esta propiedad devuelve los mensajes que tienen el destinatario especificado en los campos Para, CCO o CC.</p></td>
<td><p>Nombre para mostrar</p>
<p>Alias</p>
<p>Dirección SMTP</p>
<p>LegacyDN</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {(Participants -eq 'ayla@contoso.com') -or (Participants -eq 'tony@contoso.com')}
```

</td>
</tr>
<tr class="odd">
<td><p>PolicyTag</p></td>
<td><p>Esta propiedad devuelve los mensajes que tienen una etiqueta de directiva. El almacén de Exchange conserva las etiquetas de directiva como GUID. Por consiguiente, la cadena puede contener un valor GUID explícito, que PR_POLICY_TAG busca, o una cadena de caracteres comodín.</p>
<p>Si el valor suministrado no es un GUID, el comando utiliza la información de Active Directory para resolver los nombres en GUID.</p></td>
<td><p>Cadena</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {PolicyTag -ne '00000000-0000-0000-0000-000000000000'}
```

</td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>Esta propiedad devuelve los mensajes recibidos con la marca de tiempo de recepción especificada.</p></td>
<td><p>Marca de fecha y hora</p></td>
<td>

```powershell
-ContentFilter {Received -lt '01/01/2013 9:00'}
```




```powershell
-ContentFilter {(Received -lt '01/01/2013') -and (Received -gt '01/01/2012')}
```

</td>
</tr>
<tr class="odd">
<td><p>Remitente</p></td>
<td><p>Esta propiedad devuelve los mensajes recibidos del remitente especificado.</p></td>
<td><p>Nombre para mostrar</p>
<p>Alias</p>
<p>Dirección SMTP</p>
<p>LegacyDN</p>
<p>Carácter comodín</p></td>
<td>

```powershell
ContentFilter {Sender -eq 'tony'}
```

</td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>Esta propiedad devuelve los mensajes enviados con la marca de tiempo de envío especificada.</p></td>
<td><p>Marca de fecha y hora</p></td>
<td>

```powershell
-ContentFilter {Sent -lt '01/01/2013 9:00'}
```




```powershell
-ContentFilter {(Sent -lt '01/01/2013') -and (Sent -gt '01/01/2012')}
```

</td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>Esta propiedad devuelve los mensajes que tienen un tamaño específico.</p></td>
<td><p>B (bytes)</p>
<p>KB (kilobytes)</p>
<p>MB (megabytes)</p></td>
<td>

```powershell
-ContentFilter {Size -gt '10KB'}
```

</td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>Esta propiedad devuelve los mensajes que tienen la cadena especificada en el asunto del mensaje.</p></td>
<td><p>Cadena</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {Subject -like '*meeting*'}
```

</td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>Esta propiedad devuelve los mensajes enviados que tienen el destinatario especificado en el campo Para.</p></td>
<td><p>Nombre para mostrar</p>
<p>Alias</p>
<p>Dirección SMTP</p>
<p>LegacyDN</p>
<p>Carácter comodín</p></td>
<td>

```powershell
-ContentFilter {To -eq 'aylakol'}
```

</td>
</tr>
</tbody>
</table>

