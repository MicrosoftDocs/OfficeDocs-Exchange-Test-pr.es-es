---
title: 'Crear informes de incidentes para detecciones de directivas de DLP: Exchange 2013 Help'
TOCTitle: Crear informes de incidentes para detecciones de directivas de DLP
ms:assetid: 8e807f94-384c-43f5-be6f-06c5587175a0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150534(v=EXCHG.150)
ms:contentKeyID: 48267682
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear informes de incidentes para detecciones de directivas de DLP

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

En Exchange Server 2013, puede establecer una acción para crear un informe de incidentes dentro del conjunto de reglas de directivas de DLP. Además, puede indicar a quién debe enviarse el informe y qué hacer con el mensaje original. El informe de incidentes puede contener la siguiente información.

## Contenido de un informe de administración de incidentes

La acción **Generar informe de incidentes** les permite a los usuarios enviar informes de incidentes a un buzón de administración de incidentes. Se generará un solo informe de incidentes para cada mensaje solamente si la acción **Generar informe de incidentes** se aplica a una directiva.

La siguiente es una lista completa de los nombres de línea en una plantilla de informe de incidentes. La columna formato describe cómo reconocer cada campo en el informe. La columna de campo opcional especifica qué campos pueden no estar en el informe para que cada regla coincida. La columna Específico de DLP muestra qué campos existen como resultados de la función de DLP.


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
<td><p><strong>Nombre de</strong> <strong>línea</strong></p></td>
<td><p><strong>Descripción</strong></p></td>
<td><p><strong>Formato</strong></p></td>
<td><p><strong>Campo opcional</strong></p></td>
<td><p><strong>Específico de DLP</strong></p></td>
</tr>
<tr class="even">
<td><p>Id. de mensaje</p></td>
<td><p>Id. del mensaje original enviado</p></td>
<td><p>Id. de mensaje: Id. de mensaje</p></td>
<td><p>Obligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Remitente</p></td>
<td><p>Verdadero remitente del mensaje original</p></td>
<td><p>Remitente: Dirección de correo electrónico del remitente</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Asunto</p></td>
<td><p>Asunto del mensaje original</p></td>
<td><p>Asunto: cadena de asunto de entrada de usuario final</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Para</p></td>
<td><p>Destinatario o destinatarios del mensaje original</p>
<p>Cada línea Para solamente contendrá un solo destinatario, y puede haber hasta 10 destinatarios en el informe de incidentes. Si existen destinatarios adicionales, la siguiente línea Para mostrará el número de destinatarios faltantes.</p></td>
<td><p>Para: Dirección de correo electrónico del destinatario</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>Dirección de correo electrónico CC del mensaje original; la línea es opcional</p>
<p>Cada línea CC solamente contendrá una dirección de correo electrónico CC, y solamente se mostrarán hasta 10 direcciones de correo electrónico CC en el informe de incidentes. Si existen direcciones CC adicionales, la siguiente línea CC mostrará el número de direcciones CC faltantes.</p></td>
<td><p>CC: Dirección de correo electrónico del destinatario CC</p></td>
<td><p>Opcional</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>CCO</p></td>
<td><p>Dirección de correo electrónico de CCO del mensaje original; la línea es opcional</p>
<p>Cada línea CCO solamente contendrá una dirección de correo electrónico CCO, y solamente se mostrarán hasta 10 direcciones CCO en el informe de incidentes. Si existen direcciones de correo electrónico CCO adicionales, la siguiente línea CCO mostrará el número de direcciones de correo electrónico CCO faltantes.</p></td>
<td><p>CCO: Dirección de correo electrónico del destinatario CCO</p></td>
<td><p>Opcional</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Gravedad</p></td>
<td><p>Auditoría de la gravedad de la coincidencia de la regla; muestra la gravedad más alta si coincidieron varias reglas.</p></td>
<td><p>Gravedad: Alta, Media o Baja</p></td>
<td><p>Opcional</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Anular</p></td>
<td><p>Muestra si se informó alguna anulación para el mensaje y la justificación de la anulación, si fue suministrada.</p></td>
<td><p>Anular: Sí, justificación: Cadena de justificación de entrada de IW</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Falso positivo</p></td>
<td><p>Muestra si un falso positivo fue reportado por el mensaje.</p></td>
<td><p>Falso positivo: Sí</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Clasificación de datos</p></td>
<td><p>Clasificaciones de datos detectados encontradas en el mensaje original; la línea es opcional.</p>
<p>Cada línea de clasificación de datos solamente contendrá una clasificación detectada junto con su recuento, confianza y nivel mínimo de confianza recomendado. En el informe del incidente se mostrarán hasta 5 clasificaciones detectadas. Si la clasificación detectada fue una afinidad, no se aplica el valor de recuento y tampoco se mostrará.</p></td>
<td><p>Clasificación de datos: tipo de información confidencial, recuento: instancias de la información confidencial que se encuentra en el mensaje, confianza: valor porcentual, nivel mínimo de confianza recomendado: valor porcentual</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Coincidencia de la regla</p></td>
<td><p>Muestra todas las reglas que coincidieron con el mensaje original.</p>
<p>Incluye el nombre de la regla que coincidió, la directiva de DLP (opcional) en donde reside la regla, las acciones que se tomaron en el mensaje debido a la regla, las clasificaciones de datos en la regla que provocaron la coincidencia y la definición de la regla.</p></td>
<td><p>Coincidencia de la regla: nombre de la regla, Directiva de DLP: Nombre de la Directiva de DLP si corresponde, acción: acción individual, clasificación de datos: tipo de información confidencial, definición: definición de regla si corresponde</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Coincidencia de Id</p></td>
<td><p>Muestra la clasificación de datos que coincidieron, el contenido exacto del mensaje que coincidió y la evidencia principal de la coincidencia de la clasificación de datos; la línea es opcional.</p></td>
<td><p>Coincidencia de Id.: tipo de información confidencial, valor: valor real de los datos confidenciales, contexto: texto alrededor de los datos confidenciales en el mensaje</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


## Más información

[Ver informes de detección de directivas de DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

