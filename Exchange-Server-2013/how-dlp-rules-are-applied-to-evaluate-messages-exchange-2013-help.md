---
title: 'Cómo se aplican las reglas de DLP para la evaluación de mensajes: Exchange 2013 Help'
TOCTitle: Cómo se aplican las reglas de DLP para la evaluación de mensajes
ms:assetid: 1ac77020-26ff-410c-ab09-4f28a99d67a1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn329050(v=EXCHG.150)
ms:contentKeyID: 56271486
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cómo se aplican las reglas de DLP para la evaluación de mensajes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Puede configurar reglas de información confidencial en sus directivas de prevención de pérdida de datos (DLP) de Microsoft Exchange para detectar datos muy específicos en mensajes de correo electrónico. Este tema le ayudará a comprender cómo se aplican estas reglas y cómo se evalúan los mensajes. Puede evitar las interrupciones de flujos de trabajo a sus usuarios de correo electrónico y obtener un alto nivel de precisión con sus detecciones de DLP si sabe cómo se aplican sus reglas. Como ejemplo, vamos a usar la regla de información de tarjetas de crédito proporcionada por Microsoft. Al activar una regla de transporte o directiva de DLP, el agente de reglas de transporte de Exchange compara todos los mensajes que sus usuarios envían con los conjuntos de reglas que cree.

## Obtener la precisión que necesita

Imagine que necesita tomar una acción determinada en cuanto a la información de las tarjetas de crédito en los mensajes. Las acciones que lleve a cabo una vez que la encuentre no se tratan en este tema, pero puede obtener más información sobre este aspecto en [Enviar por correo las acciones de regla de flujo de Exchange Online](https://technet.microsoft.com/es-es/library/jj919237\(v=exchg.150\)). Con la máxima precisión posible, necesita asegurar que lo que se detecta en un mensaje es realmente información de tarjetas de crédito, y no algo más que pudiera ser un uso adecuado de grupos de números que se asemejan a los datos una tarjeta de crédito, como un código de reserva o un número de identificación de un vehículo. Para ello, dejemos claro que la siguiente información debe clasificarse como una tarjeta de crédito.

**    Viajes Martín,  
    He recibido la información actualizada de la tarjeta de crédito de Manuel.  
    Manuel Ortega  
    Visa: 4111 1111 1111 1111  
    Caduca: 2/2012  
    Actualice su perfil de viajes.**

Aclaremos también que la siguiente información no debe clasificarse como una tarjeta de crédito.

**    Hola, Alejandro:  
    Espero estar en Hawaii también. Mi código de reserva es 1234 1234 1234 1234 y estaré allí en marzo de 2012.  
    Saludos, Elisa**

El siguiente fragmento de código XML muestra cómo estas necesidades se definen en una regla de información confidencial proporcionada con Exchange y se incrusta con una de las plantillas de directiva DLP proporcionadas.

    <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>

## Coincidencia de patrones en su solución

La definición de reglas XML mostrada anteriormente incluye la coincidencia de patrones, que mejora la probabilidad de que la regla detecte solo la información importante, y no información irrelevante relacionada. Para más información sobre el esquema XML para reglas y plantillas de DLP, vea [Definir sus propios tipos de información y plantillas de DLP](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

En la regla de tarjetas de crédito, hay una sección de código XML para patrones, que incluye una coincidencia de identificadores principales y algunas pruebas adicionales. Todos estos requisitos se explican aquí:

1.  `<IdMatch idRef="Func_credit_card" />  `: requiere una coincidencia de una función, tarjeta de crédito con título, que se define internamente. Esta función incluye un par de validaciones de la forma siguiente:
    
    1.  Coincide con una expresión regular (en este ejemplo, de 16 dígitos) que también podría incluir variaciones como un delimitador de espacios para que también coincida con **4111 1111 1111 1111** o un delimitador de guiones para que también coincida con **4111-1111-1111-1111**.
    
    2.  Evalúa el algoritmo de suma de comprobación Luhn con el número de 16 dígitos para asegurar la probabilidad que la probabilidad de que se trate de un número de tarjeta de crédito sea alta.
    
    3.  Requiere una coincidencia obligatoria, tras la cual se evalúa la prueba adicional.

2.  `<Any minMatches="1">  `: esta sección indica que es necesaria la presencia de al menos uno de los siguientes elementos de prueba.

3.  La prueba puede ser una coincidencia de uno de estos tres elementos:
    
    `<Match idRef="Keyword_cc_verification" />`
    
    `<Match idRef="Keyword_cc_name" />`
    
    `<Match idRef="Func_expiration_date" />`
    
    Esto simplemente significa que se requiere una lista de palabras clave de tarjetas de crédito, los nombres de las tarjetas de crédito o la fecha de caducidad. La fecha de caducidad se define y se evalúa internamente como otra función.

## El proceso de evaluación de contenido con las reglas

Estos cinco pasos representan acciones que Exchange realiza para comparar su regla con los mensajes de correo electrónico. Para nuestro ejemplo de regla de tarjetas de crédito, se llevan a cabo los siguientes pasos.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Paso</th>
<th>Acción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1. Obtener contenido</p></td>
<td><p>Sergio Valladares</p>
<p>Visa: 4111 1111 1111 1111</p>
<p>Vence: 2/2012</p></td>
</tr>
<tr class="even">
<td><p>2. Análisis de expresiones regulares</p></td>
<td><p>4111 1111 1111 1111 -&gt; se detectó un número de 16 dígitos</p></td>
</tr>
<tr class="odd">
<td><p>3. Análisis de funciones</p></td>
<td><ul>
<li><p>4111 1111 1111 1111 -&gt; coincide con suma de comprobación</p></li>
<li><p>1234 1234 1234 1234 -&gt; no coincide</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>4. Pruebas adicionales</p></td>
<td><ol>
<li><p>La palabra clave Visa está próxima al número.</p></li>
<li><p>Una expresión regular para una fecha (2/2012) está próxima al número.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>5. Veredicto</p></td>
<td><ol>
<li><p>Hay una expresión regular que coincide con una suma de comprobación</p></li>
<li><p>Las pruebas adicionales aumentan la confianza.</p></li>
</ol>
<p></p></td>
</tr>
</tbody>
</table>


La forma en que Microsoft ha configurado esta regla hace obligatoria la confirmación de pruebas como palabras clave que son parte del contenido del mensaje del correo electrónico para cumplir la regla. Por tanto, el siguiente contenido de correo electrónico no se detectaría como contenedor de una tarjeta de crédito:

**    Viajes Martín,  
    He recibido la información actualizada de Manuel.  
    Manuel Ortega  
    4111 1111 1111 1111  
    Actualice su perfil de viaje.**

Puede usar una regla personalizada que defina un patrón sin pruebas adicionales, como se muestra en el siguiente ejemplo. Esto detectaría los mensajes solo con número de tarjeta, sin prueba adicional.

``` 
      <Pattern confidenceLevel="85">
         <IdMatch idRef="Func_credit_card" />
      </Pattern>
    </Entity>
```

La ilustración de las tarjetas de crédito de este artículo se puede hacer extensible a otras reglas de información confidencial. Para ver la lista completa de reglas proporcionadas por Microsoft en Exchange, use el cmdlet [Get-ClassificationRuleCollection](https://technet.microsoft.com/es-es/library/jj218696\(v=exchg.150\)) en el Shell de administración de Exchange de la siguiente forma:

    $rule_collection = Get-ClassificationRuleCollection

    $rule_collection[0].SerializedClassificationRuleCollection | Set-Content oob_classifications.xml -Encoding byte

## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\))

[Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\))

[Exchange Online PowerShell](https://technet.microsoft.com/es-es/library/jj200677\(v=exchg.150\))

