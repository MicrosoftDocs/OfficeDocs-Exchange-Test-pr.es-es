---
title: 'Caracteres no admitidos en los nombres de objetos de Exchange 2013: Exchange 2013 Help'
TOCTitle: Caracteres no admitidos en los nombres de objetos de Exchange 2013
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 54652442
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Caracteres no admitidos en los nombres de objetos de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Este artículo describe los caracteres que no se pueden utilizar en nombres de objetos o componentes en Exchange 2013. Cuando crea nombres para objetos o componentes en Exchange 2013, los nombres no pueden contener caracteres incompatibles, incluso aunque pueda crear un objeto con un carácter incompatible. Además, si intenta importar o conectar con objetos cuyos nombres contienen caracteres incompatibles, puede que reciba un mensaje de error o que se produzca un comportamiento inesperado.

## Caracteres incompatibles

En la siguiente tabla se enumeran los caracteres que son compatibles para usar en los nombres de objetos o componentes relacionados con Exchange. En la tabla también aparece la situación en la cual pueden ocurrir problemas si se usan caracteres incompatibles. Tenga en cuenta que existe una longitud máxima de 64 caracteres para cada objeto que aparece en la tabla.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Objeto o componente de Exchange</th>
<th>Situación de Exchange</th>
<th>Caracteres incompatibles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nombre de dominio de correo electrónico</p></td>
<td><p>Conector de Protocolo simple de transferencia de correo (SMTP)</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Nombre de host del espacio de direcciones del conector</p></td>
<td><p>Flujo de correo</p></td>
<td><p><code>..</code> (dos puntos)</p></td>
</tr>
<tr class="odd">
<td><p>Nombre de host para servidores de Exchange</p></td>
<td><p>SMTP</p></td>
<td><p><code>_</code> (guión bajo)</p></td>
</tr>
<tr class="even">
<td><p>Nombre de la organización o del sitio</p></td>
<td><p>Ejecución del programa de instalación o movimiento de buzones</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Nombre del directorio interno de la organización</p></td>
<td><p>Directorio</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Nombre del árbol de carpetas públicas</p></td>
<td><p>Visualización y creación de la carpeta pública</p></td>
<td><p><code>: ;</code></p></td>
</tr>
<tr class="odd">
<td><p>Nombre de destinatario</p></td>
<td><p>SMTP</p></td>
<td><p><code>' &quot;</code></p></td>
</tr>
<tr class="even">
<td><p>Dirección SMTP de la directiva de destinatarios</p></td>
<td><p>Visualización de la jerarquía de carpetas públicas</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Nombre de host de la dirección SMTP de la directiva de destinatarios</p></td>
<td><p>Flujo de correo</p></td>
<td><p><code>..</code> (dos puntos)</p></td>
</tr>
<tr class="even">
<td><p>Nombre del directorio interno del sitio</p></td>
<td><p>Visualización de la jerarquía de carpetas públicas</p></td>
<td><p><code>? ( ) *</code></p></td>
</tr>
<tr class="odd">
<td><p>Nombre de host inteligente</p></td>
<td><p>SMTP</p></td>
<td><p>Espacios delante o detrás</p></td>
</tr>
</tbody>
</table>

