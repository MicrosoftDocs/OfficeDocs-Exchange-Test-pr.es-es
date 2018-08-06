---
title: 'Usar reglas flujo correo enrutar correo según lista palabra expresión patrón | Microsoft Docs'
TOCTitle: Usar reglas de flujo de correo para enrutar el correo electrónico en función de una lista de palabras, expresiones o patrones
ms:assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn951131(v=EXCHG.150)
ms:contentKeyID: 65234701
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar reglas de flujo de correo para enrutar el correo electrónico en función de una lista de palabras, expresiones o patrones

 

_**Se aplica a:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Última modificación del tema:** 2017-10-30_

Para ayudar a los usuarios a cumplir con las políticas de correo electrónico de su organización, puede utilizar las reglas de transporte de Exchange para determinar cómo se enrutan los mensajes que contienen palabras específicas o patrones. Para una breve lista de palabras o frases, puede utilizar el Centro de administración de Exchange. Para obtener una lista más larga, puedes usar el módulo para Windows PowerShellExchange para leer la lista de un archivo de texto.

  - Example 1: Use a short list of unacceptable words

  - Example 2: Use a long list of unacceptable words

Si su organización usa la prevención de pérdida de datos (DLP), consulte [Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) y vea otras opciones para identificar y dirigir el correo electrónico que contiene información confidencial.

## Ejemplo 1: Usar una lista breve de palabras inaceptables

Si la lista de palabras o frases es breve, puede crear una regla mediante el Centro de administración de Exchange. Por ejemplo, si desea asegurarse de que nadie envía un correo electrónico con palabras incorrectas o con errores ortográficos del nombre de su compañía, internos acrónimos o nombres de productos, podría crear una regla para bloquear el mensaje e indicar al remitente. Tenga en cuenta que las palabras, frases y patrones no distinguen mayúsculas de minúsculas.

En este ejemplo se bloquean los mensajes con errores ortográficos comunes.

![Regla que muestra el bloqueo de un mensaje basado en patrones de texto](images/Dn951131.a8489cbb-be59-4890-ae30-1431703eeb88(EXCHG.150).png "Regla que muestra el bloqueo de un mensaje basado en patrones de texto")

## Ejemplo 2: Usar una lista larga de palabras inaceptables

Si su lista de palabras, frases o patrones es larga, puede colocarlos en un archivo de texto con cada palabra, frase o patrón en su propia línea. Utilice el módulo Exchange para Windows PowerShell para leer en la lista de palabras clave en una variable, crear una regla de transporte y asignar la variable con las palabras clave a la condición de regla de transporte. Por ejemplo, la siguiente secuencia de comandos toma una lista de errores ortográficos de un archivo denominado misspelled\_companyname.txt.

    $keywords=Import-Content  .\misspelled_companyname.txt
    New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."

## Uso de frases y patrones en el archivo de texto

El archivo de texto puede contener expresiones regulares para patrones. Estas expresiones no distinguen entre mayúsculas y minúsculas. Algunas expresiones regulares comunes son las siguientes:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Expresión</strong></p></td>
<td><p><strong>Coincidencias</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>Cualquier carácter individual</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>Cualquier carácter adicional</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>Cualquier dígito decimal</p></td>
</tr>
<tr class="odd">
<td><p>[<em>grupo_caracteres</em>]</p></td>
<td><p>Cualquier carácter individual en<em>grupo_caracteres</em>.</p></td>
</tr>
</tbody>
</table>


Por ejemplo, este archivo de texto contiene errores ortográficos comunes de Microsoft.

    [mn]sft
    [mn]icrosft
    [mn]icro soft
    [mn].crosoft

Para obtener información sobre cómo especificar patrones mediante expresiones regulares, consulte la [referencia de expresiones regulares](https://go.microsoft.com/fwlink/p/?linkid=532394).

