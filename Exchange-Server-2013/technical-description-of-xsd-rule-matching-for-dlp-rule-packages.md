---
title: 'Coincidencia de métodos y técnicas para paquetes de reglas: Exchange 2013 Help'
TOCTitle: Coincidencia de métodos y técnicas para paquetes de reglas
ms:assetid: 09fe9278-d077-452c-b7e5-729b3dc70b1b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ674702(v=EXCHG.150)
ms:contentKeyID: 49895448
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Coincidencia de métodos y técnicas para paquetes de reglas

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-07-28_

Este tema describe técnicas para hacer coincidir patrones y elementos de evidencia dentro de un archivo XML de prevención de pérdida de datos (DLP) diseñado para contener su propio paquete de reglas de tipo de información confidencial. Cuando haya creado un archivo XML bien formado, puede importar el archivo usando el Centro de administración de Exchange (EAC) o el Shell de administración de Exchange para crear la solución de DLP de Microsoft Exchange Server 2013. Antes de poder usar los métodos de coincidencias que se describen aquí, debería tener un archivo XML DLP empezado. Para obtener información acerca de la definición de sus propias plantillas DLP y archivos XML, consulte [Definir sus propios tipos de información y plantillas de DLP](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

## El elemento de la coincidencia

El elemento de `Match` se utiliza dentro de los elementos `Pattern` y `Evidence` para representar la palabra clave subyacente, regex o función que debe coincidir. La definición de la misma coincidencia se almacena fuera del elemento `Rule` y se le hace referencia a través del atributo de `idRef` necesario. Se pueden incluir varios elementos de `Match` en una definición de patrón que se puede incluir directamente en el elemento de `Pattern` o combinado usando el elemento de `Any` para definir la semántica de la coincidencia.

    <?xml version="1.0" encoding="utf-8"?>
    <Rules packageId="...">
            ...
    <Entity id="...">
      <Pattern confidenceLevel="85">
                 <IdMatch idRef="FormattedSSN" />
                 <Match idRef="USDate" />
                 <Match idRef="USAddress" />
      </Pattern>
    </Entity>
            ...
             <Keyword id="FormattedSSN "> ... </Keyword>
             <Regex id=" USDate "> ... </Regex>
             <Regex id="USAddress"> ... </Regex>
            ...
    
    </Rules>

## Definición de coincidencias basadas en palabras clave

Un requisito de regla común es hacer coincidencias basadas en expresiones de cadenas de palabras clave conocidas. Esto se logra mediante el uso del elemento `Keyword`. El elemento Palabra clave tiene un atributo de “id” que se usa como referencia en las reglas de entidad o afinidad correspondientes. Un único elemento de palabra clave se puede referenciar en varias reglas de entidad y afinidad.

La coincidencia se puede realizar con una coincidencia exacta o algoritmos basados en coincidencias de palabras. La coincidencia exacta usa un algoritmo que distingue mayúsculas de minúsculas y que busca el texto en el idioma indicado. La coincidencia de palabras aplica un algoritmo de coincidencia basado en límites de palabras. Los términos que se deben hacer coincidir se pueden incluir en línea en la definición Keyword usando el subelemento Term.


> [!TIP]
> Use el estilo de coincidencia basado en constante, en lugar de la coincidencia de regex, para una mejor eficiencia y rendimiento. Use la coincidencia de regex solo en los casos donde las coincidencias basadas en constante no son suficientes y se requiere la flexibilidad de las expresiones regulares.



    <Keyword id="Word_Example">
        <Group matchStyle="word">
           <Term>card verification</Term>
           <Term>cvn</Term>
           <Term>cid</Term>
           <Term>cvc2</Term>
           <Term>cvv2</Term>
           <Term>pin block</Term>
           <Term>security code</Term>
        </Group>
    </Keyword>
    ...
    <Keyword id="String_Example">
        <Group matchStyle="string">
           <Term>card</Term>
           <Term>pin</Term>
           <Term>security</Term>
        </Group>
    </Keyword>

## Definición de expresiones regulares basadas en coincidencias

Otro método común de hacer coincidir se basa en las expresiones regulares. La flexibilidad de la coincidencia de expresiones regulares lo convierte en una elección habitual para implementar las coincidencias de datos como los números de licencia de conductor, direcciones. La sintaxis de las expresiones regulares se usa para definir los patrones regex. La tabla aquí proporciona algunos ejemplos de algunos de los tokens de expresiones regulares más habituales disponibles.


> [!TIP]
> Use el estilo de coincidencia basado en constante, en lugar de la coincidencia de regex, para una mejor eficiencia y rendimiento. Use la coincidencia de regex solo en los casos donde las coincidencias basadas en constante no son suficientes y se requiere la flexibilidad de las expresiones regulares.




<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Símbolo</th>
<th>Significado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>c</p></td>
<td><p>Haga coincidir el carácter literal &quot;c&quot; una vez, a no ser que sea uno de los caracteres especiales.</p></td>
</tr>
<tr class="even">
<td><p>^</p></td>
<td><p>Hacer coincidir el principio de una línea.</p></td>
</tr>
<tr class="odd">
<td><p>.</p></td>
<td><p>Hacer coincidir cualquier carácter que no sea una línea nueva.</p></td>
</tr>
<tr class="even">
<td><p>$</p></td>
<td><p>Hacer coincidir el final de una línea.</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>OR lógico entre expresiones.</p></td>
</tr>
<tr class="even">
<td><p>()</p></td>
<td><p>Subexpresiones de grupos.</p></td>
</tr>
<tr class="odd">
<td><p>[]</p></td>
<td><p>Definir una clase de caracteres.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>Hacer coincidir la expresión anterior cero o más veces.</p></td>
</tr>
<tr class="odd">
<td><p>+</p></td>
<td><p>Hacer coincidir la expresión anterior una o más veces.</p></td>
</tr>
<tr class="even">
<td><p>?</p></td>
<td><p>Hacer coincidir la expresión anterior cero o una vez.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n</em>}</p></td>
<td><p>Hacer coincidir la expresión anterior <em>n</em> veces.</p></td>
</tr>
<tr class="even">
<td><p>{<em>n,</em>}</p></td>
<td><p>Hacer coincidir la expresión anterior al menos <em>n</em> veces.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n, m</em>}</p></td>
<td><p>Hacer coincidir la expresión anterior al menos <em>n</em> y un máximo de <em>m</em> veces.</p></td>
</tr>
<tr class="even">
<td><p>\d</p></td>
<td><p>Hacer coincidir un dígito.</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>Hacer coincidir un carácter que no sea un dígito.</p></td>
</tr>
<tr class="even">
<td><p>\w</p></td>
<td><p>Hacer coincidir un carácter alfabético incluyendo el carácter de subrayado.</p></td>
</tr>
<tr class="odd">
<td><p>\W</p></td>
<td><p>Hacer coincidir un carácter que no sea un carácter alfabético.</p></td>
</tr>
<tr class="even">
<td><p>\s</p></td>
<td><p>Hacer coincidir un carácter de espacio en blanco (cualquiera de \t, \n, \r o \f).</p></td>
</tr>
<tr class="odd">
<td><p>\S</p></td>
<td><p>Haga coincidir un carácter que no sea un espacio en blanco.</p></td>
</tr>
<tr class="even">
<td><p>\t</p></td>
<td><p>Tabulador.</p></td>
</tr>
<tr class="odd">
<td><p>\n</p></td>
<td><p>Salto de línea.</p></td>
</tr>
<tr class="even">
<td><p>\r</p></td>
<td><p>Retorno de carro.</p></td>
</tr>
<tr class="odd">
<td><p>\f</p></td>
<td><p>Avance de página.</p></td>
</tr>
<tr class="even">
<td><p>\<em>m</em></p></td>
<td><p>Escape <em>m</em>, donde <em>m</em> es uno de los meta caracteres descrito anteriormente: ^, ., $, |, (), [], *, +, ?, \ o /.</p></td>
</tr>
</tbody>
</table>


El elemento "Regex" tiene un atributo de “id” que se usa como referencia en las reglas de entidad o afinidad correspondientes. Un único elemento "Regex" se puede referenciar en varias reglas de entidad y afinidad. La expresión "Regex" se define como el valor del elemento "Regex".

    <Regex id="CCRegex">
         \bcc\#\s|\bcc\#\:\s
    </Regex>
    ...
    <Regex id="ItinFormatted">
        (?:^|[\s\,\:])(?:9\d{2})[- ](?:[78]\d[-       ]\d{4})(?:$|[\s\,]|\.\s)
    </Regex>
    ...
    <Regex id="NorthCarolinaDriversLicenseNumber">
        (^|\s|\:)(\d{1,8})($|\s|\.\s)
    </Regex>

## Combinar elementos de coincidencia múltiple

Una técnica habitual para incrementar la confianza de coincidencia es definir varios elementos de coincidencia, por ejemplo que una o más de las coincidencias se deben producir. El elemento "Cualquier" permite la definición de la lógica basada en varias coincidencias. El elemento "Cualquier" se puede usar como subelemento en el elemento "Patrón". Contiene uno o más elementos secundarios de "Coincidir" y define la lógica de las coincidencias entre ellos. Consulte a continuación ejemplos de códigos XML de los elementos Cualquier con todas las coincidencias, “no” lógicas y contador de coincidencias exactas.

El atributo "minMatches" opcional se puede usar (valor predeterminado = 1) para definir el número mínimo de elementos "Coincidir" que se deben cumplir para satisfacer una coincidencia. De forma similar, el atributo "maxMatches" se puede usar (valor predeterminado = número de elementos "Coincidir" secundarios) para definir el número máximo de elementos "Coincidir" que se deben cumplir para satisfacer una coincidencia. Estas condiciones se usan combinando operadores lógicos basados en el uso de los atributos "minMatches" y "maxMatches", que permiten las siguientes semánticas:

  - Hacer coincidir todos los elementos "Coincidir" secundarios
    
    No hacer coincidir ningún elemento "Coincidir" secundario
    
    Hacer coincidir un subconjunto exacto de cualquier elemento "Coincidir" secundario

<!-- end list -->

    <Any minMatches="3" maxMatches="3">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any maxMatches="0">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any minMatches="1" maxMatches="1">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

## Aumentar el nivel de confianza con más evidencias

Para las reglas de base de la entidad otra opción para incrementar la confianza es definir varios elementos "Patrón", cada uno con un número en incremento de evidencias confirmativas. Se consigue usando "minMatches" y "maxMatches" para el elemento "Cualquier" para crear patrones independientes con un nivel de confianza en incremento basado en el número en incremento de evidencias confirmativas. Por ejemplo:

  - si se encuentra una pieza de evidencia confirmativa: el nivel de confianza es del 65 %

  - si se encuentran dos piezas: el nivel de confianza es del 75%

  - si se encuentran tres piezas: el nivel de confianza es del 85%

<!-- end list -->

    <Entity id="..." patternsProximity="300" >
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Any maxMatches="1">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="75">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="2" maxMatches="2">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="85">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="3">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity>

## Ejemplo: Regla de la Seguridad Social de EE. UU.

Esta sección incluye una descripción introductoria para la creación de una regla de coincidencia de un número de la seguridad social de EE.UU. Primero, empiece con una descripción sobre cómo identificamos los contenidos que contienen un número de la seguridad social. Se encuentra un número de la Seguridad social si:

1.  "Regex" coincide con un SSN con formato (y está en el intervalo de SSN válido)

2.  Evidencia confirmativa   se debe aproximar a uno de los siguientes casos:
    
    1.  Coincidencia de palabras clave {Seguridad social, Soc Sec, SSN, SSNS, SSN\#, SS\#, SSID}
    
    2.  Texto que representa una dirección en Estados Unidos
    
    3.  Texto que representa una fecha
    
    4.  Texto que representa un nombre

A continuación, traduzca la descripción en la representación del esquema de Regla:

    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77"
             patternsProximity="300" RecommendedConfidence="85">
        <Pattern confidenceLevel="85">
          <IdMatch idRef="FormattedSSN" />
          <Any minMatches="1">
              <Match idRef="SSNKeywords" />
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
        </Pattern>
    </Entity>

## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Definir sus propios tipos de información y plantillas de DLP](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[Importar una plantilla de directiva DLP personalizada desde un archivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

