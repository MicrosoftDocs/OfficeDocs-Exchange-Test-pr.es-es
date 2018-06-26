---
title: 'Procedimientos recomendados para configurar las reglas de flujo de correo: Exchange Online Protection Help'
TOCTitle: Procedimientos recomendados para configurar las reglas de flujo de correo
ms:assetid: abd863c3-c0ce-42f3-9470-a573adc3cbba
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn960147(v=EXCHG.150)
ms:contentKeyID: 65236557
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Procedimientos recomendados para configurar las reglas de flujo de correo

 

_**Se aplica a:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Siga estas recomendaciones para las reglas de transporte de Exchange a fin de evitar errores comunes de configuración. Cada recomendación está vinculada a un tema en el que se incluyen un ejemplo e instrucciones paso a paso.

## Probar las reglas

Para asegurarse de que no se producen comportamientos inesperados en el correo electrónico de los usuarios, así como para garantizar que se cumple el propósito comercial, legal o de cumplimiento de la regla, pruébela exhaustivamente. Existen muchas opciones y las reglas pueden interactuar entre sí, por lo que es importante probar los mensajes que espera que coincidan con la regla, así como los que no coincidan con la regla en caso de que una regla sea, sin pretenderlo, demasiado general. Para conocer todas las opciones de prueba de reglas, consulte [Probar una regla de flujo de correo](test-a-mail-flow-rule-exchange-2013-help.md).

## Ámbito de la regla

Asegúrese de que la regla se aplica únicamente a los mensajes que desee. Por ejemplo:

  - **Restringir una regla a los mensajes que entran o salen de la organización**
    
    De forma predeterminada, las reglas nuevas se aplican a los mensajes enviados o recibidos por personas de su organización. Por lo tanto, si desea que la regla se aplique solo en una dirección, asegúrese de especificarlo en las condiciones de la regla. Para obtener un ejemplo, consulte [Escenarios comunes de bloqueo de datos adjuntos](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md).

  - **Restringir una regla según el dominio del remitente o del destinatario**
    
    De forma predeterminada, las reglas nuevas se aplican a los mensajes enviados o recibidos en cualquier dominio. A veces deseará que una regla se aplique a todos los dominios excepto uno, o solamente a un dominio. Para ver ejemplos, consulte [Crear una lista de remitentes seguros o bloqueados basada en dominios o usuarios mediante reglas de transporte](https://technet.microsoft.com/es-es/library/dn198251\(v=exchg.150\)).

Para obtener una lista completa de todas las condiciones y excepciones que están disponibles para las reglas de transporte, consulte:

  - [Excepciones (predicados) y las condiciones de la regla de flujo de correo en Exchange Online](https://technet.microsoft.com/es-es/library/jj919235\(v=exchg.150\))

  - [Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

  - [Mail excepciones (predicados) y las condiciones de la regla de flujo de Exchange Online Protection](https://technet.microsoft.com/es-es/library/jj919234\(v=exchg.150\))

## Cuándo se necesitan dos reglas

A veces se necesitan dos reglas para hacer lo que se desea. Las reglas de transporte se procesan en orden, por lo que se pueden aplicar varias reglas al mismo mensaje. Se necesitarán dos reglas si, por ejemplo, una de las acciones es bloquear el mensaje y hay otra acción que también desea aplicar, como enviar una copia del mensaje al administrador del remitente o cambiar al asunto del mensaje de notificación. La primera regla podría enviar una copia al administrador del remitente y cambiar al asunto, mientras que la segunda regla podría bloquear el mensaje.

Si se usan dos reglas así, asegúrese de que las condiciones sean idénticas. Para ver ejemplos, consulte el ejemplo 3 de [Escenarios comunes de aprobación de mensajes](common-message-approval-scenarios-exchange-2013-help.md), el ejemplo 3 de [Escenarios comunes de bloqueo de datos adjuntos](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md) y [Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md).

## No repetir una acción en cada correo electrónico de una conversación

La cadena de correo electrónico de una conversación puede incluir muchos mensajes, y repetir la acción en cada mensaje del hilo podría ser molesto. Por ejemplo, si tiene una acción como la adición de una renuncia, quizá desee aplicarla únicamente al primer mensaje del hilo. Si es así, agregue una excepción para los mensajes que ya incluyan el texto de renuncia. Para obtener un ejemplo, consulte [Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md).

## Cuándo hay que detener el procesamiento de reglas

A veces es conveniente detener el procesamiento de reglas una vez que se produce una coincidencia. Por ejemplo, si tiene una regla para bloquear mensajes con datos adjuntos y otra para insertar una renuncia en los mensajes que coinciden con un patrón, probablemente deba detener el procesamiento de reglas después de que se bloquee el mensaje, ya que no es necesaria ninguna otra acción.

Para detener el procesamiento de reglas una vez que se desencadena una regla, seleccione en la regla la casilla **Detener el procesamiento de más reglas**.

## Si tiene una gran cantidad de palabras clave o patrones para buscar coincidencias, cárguelos desde un archivo

Por ejemplo, quizá desee evitar el envío de mensajes de correo electrónico si contienen una lista de palabras inaceptables o malsonantes. Puede crear un archivo de texto que contenga estas palabras y frases y, a continuación, configurar una regla de transporte con Windows PowerShell que bloquee los mensajes que las usen.

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


Para obtener un ejemplo de un archivo de texto con expresiones regulares y los comandos de Windows PowerShell del módulo de Exchange, consulte [Usar reglas de flujo de correo para enrutar el correo electrónico en función de una lista de palabras, expresiones o patrones](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md).

Para obtener información sobre cómo especificar patrones mediante expresiones regulares, consulte la [referencia de expresiones regulares](https://go.microsoft.com/fwlink/p/?linkid=532394).

