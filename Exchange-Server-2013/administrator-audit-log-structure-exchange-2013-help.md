---
title: 'Estructura del registro de auditoría de administrador: Exchange 2013 Help'
TOCTitle: Estructura del registro de auditoría de administrador
ms:assetid: 87e259c9-c884-4d53-bd78-d13f2300d73e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff459251(v=EXCHG.150)
ms:contentKeyID: 50556845
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Estructura del registro de auditoría de administrador

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Los registros de auditoría de administrador contienen un registro de todos los cmdlets y parámetros que se han ejecutando en el Shell de administración de Exchange y el Centro de administración de Exchange (EAC). Estos se crean a demanda cuando ejecuta el informe del registro de auditorías del administrador en el EAC o cuando ejecuta el cmdlet **New-AdminAuditLogSearch** en el Shell. Para obtener más información acerca de los registros de auditoría, consulte [Registro de auditoría de administrador](administrator-audit-logging-exchange-2013-help.md).

Los registros de auditoría son archivos XML y pueden contener varias entradas de registro de auditoría. La tabla siguiente describe cada etiqueta XML y sus atributos asociados.

¿Está buscando tareas de administración relacionadas con los registros de auditoría del administrador? Consulte [Administrar el registro de auditoría de administrador](manage-administrator-audit-logging-exchange-2013-help.md).

### Atributos y etiquetas XML del registro de auditoría

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Atributo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;</code></p>
<p></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Esta es la etiqueta de declaración del documento XML. Esta etiqueta se incluye en todos los archivos XML del registro de auditoría y contiene el número de versión XML y el valor de codificación del carácter.</p></td>
</tr>
<tr class="even">
<td><p><code>SearchResults</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Esta etiqueta contiene todas las entradas de registro de auditoría en el archivo XML. La etiqueta <code>Event</code> es un elemento secundario de esta etiqueta.</p>
<p>Solo hay una etiqueta <code>SearchResults</code> por cada archivo XML.</p></td>
</tr>
<tr class="odd">
<td><p><code>Event</code></p></td>
<td><p><code> </code></p></td>
<td><p>Esta etiqueta contiene la entrada de registro de auditoría para un cmdlet individual. Esta etiqueta contiene los atributos <code>Caller</code>, <code>Cmdlet</code>, <code>ObjectModified</code>, <code>RunDate</code>, <code>Succeeded</code>, <code>Error</code> y <code>OriginatingServer</code>. Las etiquetas <code>CmdletParameters</code> y <code>ModifiedProperties</code> son elementos secundarios de esta etiqueta.</p>
<p>Hay una etiqueta <code>Event</code> por cada entrada de registro de auditoría.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Caller</code></p></td>
<td><p>Este atributo contiene la cuenta de usuario del usuario que ejecuta el cmdlet en el atributo <code>Cmdlet</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Cmdlet</code></p></td>
<td><p>Este atributo contiene el nombre del cmdlet ejecutado por el usuario en el atributo <code>Caller</code>.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>ObjectModified</code></p></td>
<td><p>Este atributo contiene el objeto modificado por el cmdlet especificado en el atributo <code>Cmdlet</code>. La etiqueta <code>ModifiedProperties</code> muestra qué propiedades se modificaron en este objeto.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>RunDate</code></p></td>
<td><p>Este atributo contiene la fecha y la hora en que se ejecutó el cmdlet en el atributo <code>Cmdlet</code>.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Succeeded</code></p></td>
<td><p>Este atributo especifica si el cmdlet en el atributo <code>Cmdlet</code> se ejecutó correctamente. El valor es <code>True</code> o <code>False</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Error</code></p></td>
<td><p>Este atributo contiene el mensaje de error generado si el cmdlet en el atributo <code>Cmdlet</code> no se completó correctamente. Si no se ha producido ningún error, el valor se establece en <code>None</code>.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OriginatingServer</code></p></td>
<td><p>Este atributo contiene el servidor donde se ejecutó el cmdlet en el atributo <code>Cmdlet</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletParameters</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Esta etiqueta contiene todos los parámetros especificados cuando se ejecutó el cmdlet. La etiqueta <code>Parameter</code> es un elemento secundario de esta etiqueta.</p>
<p>Existe una etiqueta <code>CmdletParameters</code> por cada etiqueta <code>Event</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Parameter</code></p></td>
<td><p><code> </code></p></td>
<td><p>Esta etiqueta contiene un parámetro individual que se especificó cuando se ejecutó el cmdlet. Esta etiqueta contiene los atributos <code>Name</code> y <code>Value</code>.</p>
<p>Puede haber varias etiquetas <code>Parameter</code> por cada etiqueta <code>CmdletParameters</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>Este atributo contiene el nombre del parámetro que se especificó en el cmdlet ejecutado.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Value</code></p></td>
<td><p>Este atributo contiene el valor provisto en el parámetro especificado en el atributo <code>Name</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Esta etiqueta contiene todas las propiedades que el cmdlet ejecutado modificó. La etiqueta <code>Property</code> es un elemento secundario de esta etiqueta.</p>
<p>Existe una etiqueta <code>ModifiedProperties</code> por cada etiqueta <code>Event</code>.</p>

> [!IMPORTANT]
> Esta etiqueta solo se completa si el parámetro <EM>LogLevel</EM> en el cmdlet se establece en <STRONG>Set-AdminAuditLogConfig</STRONG><CODE>Verbose</CODE>.


</td>
</tr>
<tr class="even">
<td><p><code>Property</code></p></td>
<td><p><code> </code></p></td>
<td><p>Esta etiqueta contiene una propiedad individual que se especificó cuando se ejecutó el cmdlet. Esta etiqueta contiene los atributos <code>Name</code>, <code>OldValue</code> y <code>NewValue</code>.</p>
<p>Puede haber varias etiquetas <code>Property</code> por cada etiqueta <code>ModifiedProperties</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>Este atributo contiene el nombre de la propiedad que se modificó cuando se ejecutó el cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OldValue</code></p></td>
<td><p>Este atributo contiene el valor que se encontraba en la propiedad especificada en el atributo <code>Name</code> antes de que esta fuera modificada.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>NewValue</code></p></td>
<td><p>Este atributo contiene el valor al cual fue modificada la propiedad en el atributo <code>Name</code>.</p></td>
</tr>
</tbody>
</table>


## Ejemplo de la entrada de registro de auditoría

A continuación, se muestra un ejemplo de una entrada de registro de auditoría típica. Según la información que se encuentra en la entrada de registro, sabemos que se ha producido lo siguiente:

  - El 10/18/2012 a las 3:48 p.m. hora del verano del Pacífico (UTC-7), el usuario `Administrator` ejecutó el cmdlet **Set-Mailbox**.

  - Cuando se ejecutó el cmdlet **Set-Mailbox**, se proporcionaron los dos parámetros siguientes:
    
      - *Identity* con un valor de `david`
    
      - *ProhibitSendReceiveQuota* con un valor de `10GB`

  - Se modificaron las dos propiedades siguientes en el objeto `david`:
    

    > [!NOTE]
    > Las propiedades modificadas se guardan en el registro de auditoría ya que el parámetro <EM>LogLevel</EM> en el cmdlet <CODE>Set-AdminAuditLogConfig</CODE> cmdlet se estableció en <CODE>Verbose</CODE> en este ejemplo.

    
      - *ProhibitSendReceiveQuota* con un valor nuevo de `10GB`, que reemplazó el valor antiguo de `35GB`

  - La operación se completó correctamente sin errores.

<!-- end list -->

    <?xml version="1.0" encoding="utf-8"?>
    <SearchResults>
    
      <Event Caller="corp.e15a.contoso.com/Users/Administrator" Cmdlet="Set-Mailbox" ObjectModified="corp.e15a.contoso.com/Users/david" RunDate="2012-10-18T15:48:15-07:00" Succeeded="true" Error="None" OriginatingServer="WIN8MBX (15.00.0516.032)">
        <CmdletParameters>
          <Parameter Name="Identity" Value="david" />
          <Parameter Name="ProhibitSendReceiveQuota" Value="10 GB (10,737,418,240 bytes)" />
        </CmdletParameters>
        <ModifiedProperties>
          <Property Name="ProhibitSendReceiveQuota" OldValue="35 GB (37,580,963,840 bytes)" NewValue="10 GB (10,737,418,240 bytes)" />
        </ModifiedProperties>
      </Event>
    </SearchResults>

