---
title: 'Desarrollar paquetes de reglas de información confidencial: Exchange 2013 Help'
TOCTitle: Desarrollar paquetes de reglas de información confidencial
ms:assetid: c4ab8707-0839-4855-9390-3dbcb43475a7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ674704(v=EXCHG.150)
ms:contentKeyID: 49895898
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Desarrollar paquetes de reglas de información confidencial

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-07-28_

El esquema XML y la guía en este tema lo ayudarán a comenzar a crear sus propios archivos XML básicos de prevención de pérdida de datos (DLP) que definen sus propios tipos de información confidencial en un paquete de reglas de clasificación. Una vez creado un archivo XML bien formado, puede importarlo usando el Centro de Administración de Exchange o el Shell de administración de Exchange para ayudar a crear una solución DLP Exchange Server 2013 Microsoft. Un archivo XML que es una plantilla de la directiva de DLP personalizada puede contener el XML que sea su paquete de reglas de clasificación. Para obtener información general sobre cómo definir sus propias plantillas de DLP como archivos XML, consulte [Definir sus propios tipos de información y plantillas de DLP](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

**Contenido**

Información general del proceso de creación de reglas

Descripción de la regla

Estructura de la regla básica

Uso de idiomas locales en el archivo XML

Definición de esquemas XML del paquete de reglas de clasificación

Más información

## Información general del proceso de creación de reglas

El proceso de creación de reglas se compone de los siguientes pasos generales.

1.  Preparar un conjunto de documentos de prueba representativas de su entorno de destino. Las características clave que se deben considerar para el conjunto de documentos de prueba incluyen: Un subconjunto de documentos que contenga la entidad o la afinidad para la cual se está creando la regla y un subconjunto de documentos que no contenga la entidad ni la afinidad para la cual se está creando la regla.

2.  Identificar las reglas que cumplen los requisitos de aceptación (precisión y recuperación) para identificar el contenido necesario. Es posible que esto requiera el desarrollo de varias condiciones dentro de una regla, unidas con lógica booleana, las cuales conjuntamente satisfacen los requisitos mínimos para identificar documentos de destino.

3.  Establecer el nivel de confianza recomendado para las reglas según los requisitos de aceptación (precisión y recuperación). Se puede considerar el elemento de confianza recomendado como el nivel de confianza predeterminado para la regla.

4.  Validar las reglas ejemplificando una directiva con ellas y supervisando el contenido de la prueba de muestra. Según los resultados, ajustar las reglas o el nivel de confianza para maximizar el contenido detectado mientras se minimizan los falsos positivos y negativos. Continuar el ciclo de validación y los ajustes de regla hasta que se logre una detección satisfactoria del nivel de contenido para las muestras positiva y negativa.

Para obtener información acerca de la definición del esquema de XML para los archivos de plantilla de la directiva, consulte [Desarrollo de archivos de plantilla de directivas de DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

## Descripción de la regla

Se pueden crear dos tipos de reglas principales para el motor de detección de información confidencial DLP: Entidad y afinidad. El tipo de regla seleccionado se basa en el tipo de lógica de procesamiento que se debería aplicar al procesamiento del contenido según lo descrito en las secciones anteriores. Las definiciones de regla se configuran en un documento XML en el formato descrito por las reglas XSD estandarizadas. Las reglas describen tanto el tipo de contenido que debe coincidir como el nivel de confianza que la coincidencia descrita representa en el contenido de destino. El nivel de confianza especifica la probabilidad de que la entidad esté presente si se encuentra un patrón o la probabilidad de que la afinidad esté presente si se encuentra evidencia en el contenido.

## Estructura de la regla básica

La definición de la regla está hecha de tres componentes principales:

1.  **Entidad** define la lógica de coincidencia y recuento para esa regla

2.  **Afinidad** define la lógica de coincidencia para la regla

3.  **Cadenas localizadas** localización de los nombres de las reglas y sus descripciones

Se utilizan tres elementos auxiliares que definen los detalles del procesamiento y en referencia con los componentes principales: Palabra clave, Regex y función. Al usar referencias, se puede utilizar una sola definición de los elementos auxiliares, como el número de seguro social, en diferentes reglas de la entidad o la afinidad. La estructura de la regla básica en formato XML puede verse como sigue.

```xml
  <?xml version="1.0" encoding="utf-8"?>
  <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
  
    <RulePack id="DAD86A92-AB18-43BB-AB35-96F7C594ADAA">
      <Version major="1" minor="0" build="0" revision="0"/>
      <Publisher id="619DD8C3-7B80-4998-A312-4DF0402BAC04"/>
      <Details defaultLangCode="en-us">
        <LocalizedDetails langcode="en-us">
          <PublisherName>DLP by EPG</PublisherName>
          <Name>CSO Custom Rule Pack</Name>
          <Description>This is a rule package for a EPG demo.</Description>
        </LocalizedDetails>
      </Details>
    </RulePack>
  
    <Rules>
  
      <!-- Employee ID -->
      <Entity id="E1CC861E-3FE9-4A58-82DF-4BD259EAB378" patternsProximity="300" recommendedConfidence="75">
        <Pattern confidenceLevel="75">
          <IdMatch idRef="Regex_employee_id" />
          <Match idRef="Keyword_employee" />
        </Pattern>
      </Entity>
  
      <Regex id="Regex_employee_id">(\s)(\d{9})(\s)</Regex>
      <Keyword id="Keyword_employee">
        <Group matchStyle="word">
          <Term>Identification</Term>
          <Term>Contoso Employee</Term>
        </Group>
      </Keyword>
  
  
      <LocalizedStrings>
  
        <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB378">
          <Name default="true" langcode="en-us">
            Employee ID
          </Name>
          <Description default="true" langcode="en-us">
            A custom classification for detecting Employee ID's
          </Description>
        </Resource>
  
      </LocalizedStrings>
    </Rules>
  </RulePackage>
```

## Reglas de la entidad

Las reglas de la entidad están destinadas a identificadores bien definidos, como Número de seguro social, y se representan mediante un conjunto de patrones que se pueden contar. Las reglas de la entidad devuelven un recuento y el nivel de confianza de una coincidencia, donde el recuento es la cantidad total de instancias de la entidad que se encontró y el nivel de confianza es la probabilidad de que dicha entidad exista en el documento en particular. La entidad contiene el atributo "id" como su identificador único. El identificador se utiliza para la localización, el control de versiones y la consulta. El id de la identidad debe ser GUID y no debe estar duplicado en otras entidades o afinidades. Se hace referencia a este en la sección de cadenas localizadas.

Las reglas de la entidad contienen el atributo opcional Proximidad de patrones (valor predeterminado = 300), que se utiliza cuando se aplica la lógica booleana para especificar la proximidad de varios patrones necesarios para satisfacer la condición de coincidencia. El elemento Entidad contiene uno o más elementos de patrones secundarios, donde cada patrón es una representación idéntica de la entidad como entidad de tarjeta de crédito o entidad de licencia de conductor. El elemento del patrón tiene un atributo necesario de nivel de confianza que representa la precisión del patrón según un conjunto de datos de muestra. El elemento del patrón puede tener tres elementos secundarios:

1.  Coincidencia de id: es necesario.

2.  Coincidencia

3.  Cualquiera

Si cualquiera de los elementos del patrón devuelve "true", se cumple con el patrón. El recuento del elemento Entidad es igual a la suma de todos los recuentos de patrón detectados.

![Fórmula matemática para el recuento de entidades](images/JJ674704.25309939-98bc-4460-8f89-8560bbad7981(EXCHG.150).gif "Fórmula matemática para el recuento de entidades")

donde k es la cantidad de elementos del patrón de la entidad.

Un elemento del patrón debe tener exactamente un elemento Coincidencia de id. Coincidencia de id representa el identificador que el patrón debe hacer coincidir, por ejemplo un número de tarjeta de crédito o número ITIN. El recuento de un patrón es la cantidad de Coincidencias de id que coinciden con el elemento del patrón. El elemento Coincidencia de id ancla la ventana de proximidad para los elementos Coincidencia.

Otro subelemento opcional del elemento del patrón es el elemento Coincidencia que representa evidencia corroborativa que es necesaria hacer coincidir para respaldar el hallazgo del elemento Coincidencia de id. Por ejemplo, la regla de confianza más alta puede requerir que, además de encontrar un número de tarjeta de crédito, existan artefactos adicionales en el documento, dentro de la ventana de proximidad de una tarjeta de crédito, como dirección y nombre. Estos artefactos adicionales estarían representados mediante el elemento Coincidencia o el elemento Todos (estos se describen en detalle en la sección Coincidencia de métodos y técnicas). Se pueden incluir varios elementos Coincidencia en un definición de patrón que se puede incluir directamente en el elemento del patrón o combinar usando el elemento Todos para definir la semántica de coincidencia. Devuelve true si se encuentra una coincidencia en la ventana de proximidad anclada alrededor del contenido de Coincidencia de id.

Los elementos Coincidencia de id y Coincidencia no definen los detalles de qué contenido debe coincidir pero hace referencia a este a través del atributo idRef. Esto promueve la reutilización de definiciones en varias construcciones de patrón.

```xml
  <Entity id="..." patternsProximity="300" > 
      <Pattern confidenceLevel="85">
          <IdMatch idRef="FormattedSSN" />
          <Any minMatches="1">
              <Match idRef="SSNKeyword" />
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
      </Pattern>  
      <Pattern confidenceLevel="65">
          <IdMatch idRef="UnformattedSSN" />
          <Match idRef="SSNKeyword" />
          <Any minMatches="1">        
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
      </Pattern>
  </Entity> 
```

El elemento id de entidad, representado en el XML anterior por “…” debe ser un GUID y se hace referencia a este en la sección Cadenas localizadas.

## Ventana de proximidad del patrón de entidad

La entidad tiene el valor de atributo opcional Proximidad (número entero, valor predeterminado = 300) usado para definir los patrones. Para cada patrón, el valor de atributo define la distancia (en caracteres Unicode) desde el lugar de la Coincidencia de id para todas las otras Coincidencias especificadas para ese patrón. La ventana de proximidad se ancla mediante el lugar de Coincidencia de id, y la ventana se extiende de izquierda a derecha de la Coincidencia de id.

![Patrón de texto con elementos coincidentes resaltados](images/JJ674704.65d52989-f50f-4097-b39a-9612f860d727(EXCHG.150).gif "Patrón de texto con elementos coincidentes resaltados")

El siguiente ejemplo muestra cómo la ventana de proximidad afecta al algoritmo de coincidencia donde el elemento Coincidencia de id SSN requiere por lo menos una de las coincidencias de corroboración de dirección, nombre o fecha. Solo SSN1 y SSN4 coinciden porque para SSN2 y SSN3 no se encontró evidencia de corroboración, o solo se encontró evidencia parcial, dentro de la ventana de proximidad.

![Ejemplos de coincidencia y no coincidencia de regla de proximidad](images/JJ674704.8117deb3-d8c8-4d4e-a011-ac5f9990b08e(EXCHG.150).gif "Ejemplos de coincidencia y no coincidencia de regla de proximidad")

Tenga en cuenta que el cuerpo del mensaje y los datos adjuntos se tratan como elementos independientes. Esto significa que la ventana de proximidad no se extiende más allá del final de cada uno de estos elementos. Cada elemento (cuerpo o datos adjuntos), debe contener tanto su propio elemento Coincidencia de id como su evidencia de corroboración.

## Nivel de confianza de la entidad

El nivel de confianza del elemento Entidad es la combinación de todos los niveles de confianza del patrón satisfechos. Se combinan utilizando la siguiente ecuación:

![Fórmula matemática para el nivel de confianza de entidades](images/JJ674704.9b8bb9c8-3ded-4ea5-a609-71d8034b1017(EXCHG.150).gif "Fórmula matemática para el nivel de confianza de entidades")

donde k es la cantidad de elementos del patrón para la entidad y un patrón que no coincide devuelve un nivel de confianza de 0.

En cuanto a la muestra del código de la estructura del elemento Entidad de ejemplo, ambos patrones coinciden, el nivel de confianza de la entidad es 94.75 % según el siguiente cálculo:

CLentidad= 1-\[(1-CLPatrón1) x (1-CLPatrón1)\]

*= 1-\[(1-0.85) x (1-0.65)\]*

*= 1-(0.15 x 0.35)*

*= 94.75%*

De manera similar, si solo coincide el segundo patrón, el nivel de confianza de la entidad es 65 % según el siguiente cálculo:

CLentidad= 1-\[(1 – CLPatrón1) X (1 – CLPatrón1)\]

*= 1 – \[(1 – 0) X (1 – 0.65)\]*

*= 1 – (1 X 0.35)*

*= 65%*

Los valores de confianza se asignan en las reglas para patrones individuales según un conjunto de documentos de prueba validados como parte del proceso de creación de reglas.

## Reglas de afinidad

Las reglas de afinidad están destinadas al contenido sin identificadores bien definidos, por ejemplo Sarbanes-Oxley o contenido financiero empresarial. Para este contenido no se puede encontrar un solo identificador consistente, por lo que el análisis requiere determinar si hay un conjunto de evidencias. Las reglas de afinidad no devuelven un recuento sino que devuelven el nivel de confianza asociado, si lo encuentra. El contenido de afinidad se representa como una colección de evidencias independientes. La evidencia es una agregación de coincidencias necesarias dentro de cierta proximidad. Para la regla de afinidad, la proximidad se define mediante el atributo evidencesProximity (el valor predeterminado es 600) y el nivel de confianza mínimo es el atributo nivel de confianza límite.

Las reglas de afinidad contienen el atributo id para su identificador único que se utiliza para la localización, el control de versiones y la consulta. A diferencia de las reglas de entidad, debido a que las reglas de afinidad no dependen de identificadores bien definidos, no contienen el elemento Coincidencia de id.

Cada regla de afinidad contiene uno o más elementos Evidencia secundaria que definen la evidencia que se encontrará y el nivel de confianza que contribuye a la regla de afinidad. No se considera encontrada la afinidad si el nivel de confianza que se obtiene está por debajo del nivel límite. Cada evidencia representa de manera lógica la evidencia de corroboración para este "tipo" y el atributo Nivel de confianza es la precisión de esa evidencia en el conjunto de datos de prueba.

Los elementos Evidencia tienen uno o más elementos de coincidencia o cualquiera. Si todos los elementos Coincidencia y Todos coinciden, se encuentra la evidencia y el nivel de confianza contribuye al cálculo del nivel de confianza de las reglas. La misma descripción corresponde a los elementos Coincidencia o Todos para las reglas de afinidad y las reglas de entidad.

```xml
  <Affinity id="..." 
            evidencesProximity="1000"
            thresholdConfidenceLevel="65">
      <Evidence confidenceLevel="40">
          <Any> 
              <Match idRef="AssetsTerms" /> 
              <Match idRef="BalanceSheetTerms" /> 
              <Match idRef="ProfitAndLossTerms" /> 
          </Any> 
      </Evidence>
      <Evidence confidenceLevel="40">
          <Any minMatches="2"> 
              <Match idRef="TaxTerms" /> 
              <Match idRef="DollarAmountTerms" /> 
              <Match idRef="SECTerms" /> 
              <Match idRef="SECFilingFormTerms" /> 
              <Match idRef="DollarTotalRegex" /> 
          </Any> 
      </Evidence>
  </Affinity>
```

## Ventana de proximidad de afinidad

La ventana de proximidad por afinidad se calcula de forma diferente que para los patrones de entidad. La proximidad de afinidad sigue un modelo de ventana deslizante. El algoritmo de proximidad de afinidad intenta encontrar la cantidad máxima de evidencias que coinciden en dicha ventana. Las evidencias en la ventana de proximidad deben tener un nivel de confianza mayor al límite definido para la regla de afinidad que se encontrará.

![Texto cerca de una coincidencia de regla de afinidad](images/JJ674704.2601ec86-0094-43fa-8d22-9d97f7465942(EXCHG.150).gif "Texto cerca de una coincidencia de regla de afinidad")

## Nivel de confianza de afinidad

El nivel de confianza de afinidad es igual a la combinación de evidencias encontradas dentro de la ventana de proximidad para la regla de afinidad. Si bien es similar al nivel de confianza de la regla de entidad, la diferencia clave es la aplicación de la ventana de proximidad. De manera similar a las reglas de entidad, el nivel de confianza del elemento Afinidad es la combinación de todos los niveles de confianza de evidencia satisfechos, pero para la regla de afinidad solo representa la combinación más alta de elementos Evidencia encontrados dentro de la ventana de proximidad. Los niveles de confianza de evidencia se combinan utilizando la siguiente ecuación:

![Fórmula matemática para la confianza de la regla de afinidad](images/JJ674704.8a5da4ca-af02-4c5a-ab60-0072dc7e7a0f(EXCHG.150).gif "Fórmula matemática para la confianza de la regla de afinidad")

donde k es la cantidad de elementos Evidencia para la afinidad que coincide dentro de la ventana de proximidad.

En cuanto a la estructura de la regla de afinidad de ejemplo de la Figura 4, si todas las evidencias coinciden dentro de la ventana de proximidad deslizante, el nivel de confianza de la afinidad es 85.6 % según el siguiente cálculo. Este supera el límite de la regla de afinidad de 65, lo que hace que la regla coincida.

CLafinidad= 1 – \[(1 – CLevidencia 1) X (1 – CLevidencia 2) X (1 – CLevidencia 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0.4) X (1 – 0.4)\]*

*= 1 – (0.4 X 0.6 X 0.6)*

*= 85.6%*

![Ejemplo de coincidencia de regla de afinidad con nivel de confianza alto](images/JJ674704.e17b2e22-18c3-40c4-8f19-0993bb556675(EXCHG.150).gif "Ejemplo de coincidencia de regla de afinidad con nivel de confianza alto")

Con la misma definición de regla de ejemplo, si solo la primera evidencia coincide porque la segunda evidencia se encuentra fuera de la ventana de proximidad, el nivel de confianza de la afinidad más alto es 60 % según el cálculo siguiente y la regla de afinidad no coincide ya que no se cumple con el límite de 65.

CLafinidad= 1 – \[(1 – CLevidencia 1) X (1 – CLevidencia 2) X (1 – CLevidencia 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0) X (1 – 0)\]*

*= 1 – (0.4 X 1 X 1)*

*= 60%*

![Ejemplo de coincidencia de regla de afinidad con nivel de confianza bajo](images/JJ674704.077095b1-6eb0-40df-b254-f33437725720(EXCHG.150).gif "Ejemplo de coincidencia de regla de afinidad con nivel de confianza bajo")

## Ajuste de los niveles de confianza

Uno de los aspectos clave del proceso de creación de reglas es el ajuste de los niveles de confianza tanto para reglas de entidad como de afinidad. Después de crear las definiciones de reglas, ejecute la regla en el contenido representativo y recopile los datos de precisión. Compare los resultados devueltos para cada patrón o evidencia con los resultados esperados de los documentos de prueba.

![Tabla de comparación de pruebas de coincidencia de regla](images/JJ674704.25a7d9a1-d02f-447e-a88b-8e78bdc0413a(EXCHG.150).gif "Tabla de comparación de pruebas de coincidencia de regla")

Si las reglas cumplen con los requisitos de aceptación, es decir, el patrón o la evidencia tienen un índice de confianza por encima del límite establecido (p. ej. 75 %), la expresión de coincidencia es completa y se puede seguir con el siguiente paso.

Si el patrón o la evidencia no cumplen con el nivel de confianza, vuelva a crearla (p ej. agregue más evidencia de corroboración, elimine o agregue patrones o evidencias adicionales, etc.) y repita el paso.

A continuación, ajuste el nivel de confianza para cada patrón o evidencia de sus reglas según los resultados del paso anterior. Para cada patrón o evidencia, agregue el número de verdaderos positivos (VP), un subconjunto de los documentos que contienen la entidad o afinidad para las cuales se está creando la regla y que generó una coincidencia, y el número de falsos positivos (FP), un conjunto de documentos que no contienen la entidad ni la afinidad para las cuales se está creando la regla y que también generó una coincidencia. Establezca el nivel de confianza para cada patrón o evidencia utilizando el siguiente cálculo:

*Nivel de confianza = verdaderos positivos / (verdaderos positivos + falsos positivos)*


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Patrón o evidencia</th>
<th>Verdaderos positivos</th>
<th>Falsos positivos</th>
<th>Nivel de confianza</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>P1o E1</p></td>
<td><p>4</p></td>
<td><p>1</p></td>
<td><p>80%</p></td>
</tr>
<tr class="even">
<td><p>P2o E2</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Pno En</p></td>
<td><p>9</p></td>
<td><p>10</p></td>
<td><p>47%</p></td>
</tr>
</tbody>
</table>


## Uso de idiomas locales en el archivo XML

El esquema de la regla admite el almacenamiento del nombre y la descripción localizados para cada elemento Entidad y Afinidad. Cada elemento Entidad y Afinidad debe contener un elemento correspondiente en la sección Cadenas localizadas. Para localizar cada elemento, incluya un elemento Recurso como elemento de cadenas localizadas secundario para almacenar el nombre y las descripciones de varios configuraciones regionales de cada elemento. El elemento Recursos incluye un atributo idRef necesario que coincida con el atributo idRef correspondiente para cada elemento que se está localizando. Los elementos Configuración regional secundarios del elemento Recurso contienen el nombre y descripciones localizados para cada región específica.

```xml
  <LocalizedStrings>
      <Resource idRef="guid">
          <Locale langcode="en-US" default="true"> 
              <Name>affinity name en-us</Name> 
              <Description>
                  affinity description en-us
              </Description> 
          </Locale> 
          <Locale langcode="de"> 
              <Name>affinity name de</Name> 
              <Description>
                  affinity description de
              </Description> 
          </Locale> 
      </Resource>
  </LocalizedStrings>
```

## Definición de esquemas XML del paquete de reglas de clasificación

```xml
  <?xml version="1.0" encoding="utf-8"?>
  <xs:schema xmlns:mce="http://schemas.microsoft.com/office/2011/mce"
              targetNamespace="http://schemas.microsoft.com/office/2011/mce" 
              xmlns:xs="http://www.w3.org/2001/XMLSchema"
              elementFormDefault="qualified"
              attributeFormDefault="unqualified"
              id="RulePackageSchema">
    <xs:simpleType name="LangType">
      <xs:union memberTypes="xs:language">
        <xs:simpleType>
          <xs:restriction base="xs:string">
            <xs:enumeration value=""/>
          </xs:restriction>
        </xs:simpleType>
      </xs:union>
    </xs:simpleType>
    <xs:simpleType name="GuidType" final="#all">
      <xs:restriction base="xs:token">
        <xs:pattern value="[0-9a-fA-F]{8}\-([0-9a-fA-F]{4}\-){3}[0-9a-fA-F]{12}"/>
      </xs:restriction>
    </xs:simpleType>
    <xs:complexType name="RulePackageType">
      <xs:sequence>
        <xs:element name="RulePack" type="mce:RulePackType"/>
        <xs:element name="Rules" type="mce:RulesType">
          <xs:key name="UniqueRuleId">
            <xs:selector xpath="mce:Entity|mce:Affinity"/>
            <xs:field xpath="@id"/>
          </xs:key>
          <xs:key name="UniqueProcessorId">
            <xs:selector xpath="mce:Regex|mce:Keyword"></xs:selector>
            <xs:field xpath="@id"/>
          </xs:key>
          <xs:key name="UniqueResourceIdRef">
            <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
            <xs:field xpath="@idRef"/>
          </xs:key>        
          <xs:keyref name="ReferencedRuleMustExist" refer="mce:UniqueRuleId">
            <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
            <xs:field xpath="@idRef"/>
          </xs:keyref>
          <xs:keyref name="RuleMustHaveResource" refer="mce:UniqueResourceIdRef">
            <xs:selector xpath="mce:Entity|mce:Affinity"/>
            <xs:field xpath="@id"/>
          </xs:keyref>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
    <xs:complexType name="RulePackType">
      <xs:sequence>
        <xs:element name="Version" type="mce:VersionType"/>
        <xs:element name="Publisher" type="mce:PublisherType"/>
        <xs:element name="Details" type="mce:DetailsType">
          <xs:key name="UniqueLangCodeInLocalizedDetails">
            <xs:selector xpath="mce:LocalizedDetails"/>
            <xs:field xpath="@langcode"/>
          </xs:key>
          <xs:keyref name="DefaultLangCodeMustExist" refer="mce:UniqueLangCodeInLocalizedDetails">
            <xs:selector xpath="."/>
            <xs:field xpath="@defaultLangCode"/>
          </xs:keyref>
        </xs:element>
        <xs:element name="Encryption" type="mce:EncryptionType" minOccurs="0" maxOccurs="1"/>
      </xs:sequence>
      <xs:attribute name="id" type="mce:GuidType" use="required"/>
    </xs:complexType>
    <xs:complexType name="VersionType">
      <xs:attribute name="major" type="xs:unsignedShort" use="required"/>
      <xs:attribute name="minor" type="xs:unsignedShort" use="required"/>
      <xs:attribute name="build" type="xs:unsignedShort" use="required"/>
      <xs:attribute name="revision" type="xs:unsignedShort" use="required"/>
    </xs:complexType>
    <xs:complexType name="PublisherType">
      <xs:attribute name="id" type="mce:GuidType" use="required"/>
    </xs:complexType>
    <xs:complexType name="LocalizedDetailsType">
      <xs:sequence>
        <xs:element name="PublisherName" type="mce:NameType"/>
        <xs:element name="Name" type="mce:RulePackNameType"/>
        <xs:element name="Description" type="mce:OptionalNameType"/>
      </xs:sequence>
      <xs:attribute name="langcode" type="mce:LangType" use="required"/>
    </xs:complexType>
    <xs:complexType name="DetailsType">
      <xs:sequence>
        <xs:element name="LocalizedDetails" type="mce:LocalizedDetailsType" maxOccurs="unbounded"/>
      </xs:sequence>
      <xs:attribute name="defaultLangCode" type="mce:LangType" use="required"/>
    </xs:complexType>
    <xs:complexType name="EncryptionType">
      <xs:sequence>
        <xs:element name="Key" type="xs:normalizedString"/>
        <xs:element name="IV" type="xs:normalizedString"/>
      </xs:sequence>
    </xs:complexType>
    <xs:simpleType name="RulePackNameType">
      <xs:restriction base="xs:token">
        <xs:minLength value="1"/>
        <xs:maxLength value="64"/>
      </xs:restriction>
    </xs:simpleType>
    <xs:simpleType name="NameType">
      <xs:restriction base="xs:normalizedString">
        <xs:minLength value="1"/>
        <xs:maxLength value="256"/>
      </xs:restriction>
    </xs:simpleType>
    <xs:simpleType name="OptionalNameType">
      <xs:restriction base="xs:normalizedString">
        <xs:minLength value="0"/>
        <xs:maxLength value="256"/>
      </xs:restriction>
    </xs:simpleType>
    <xs:simpleType name="RestrictedTermType">
      <xs:restriction base="xs:string">
        <xs:minLength value="1"/>
        <xs:maxLength value="512"/>
      </xs:restriction>
    </xs:simpleType>
    <xs:complexType name="RulesType">
      <xs:sequence>
        <xs:choice maxOccurs="unbounded">
          <xs:element name="Entity" type="mce:EntityType"/>
          <xs:element name="Affinity" type="mce:AffinityType"/>
        </xs:choice>
        <xs:choice minOccurs="0" maxOccurs="unbounded">
          <xs:element name="Regex" type="mce:RegexType"/>
          <xs:element name="Keyword" type="mce:KeywordType"/>
        </xs:choice>
        <xs:element name="LocalizedStrings" type="mce:LocalizedStringsType"/>
      </xs:sequence>
    </xs:complexType>
    <xs:complexType name="EntityType">
      <xs:sequence>
        <xs:element name="Pattern" type="mce:PatternType" maxOccurs="unbounded"/>
      </xs:sequence>
      <xs:attribute name="id" type="mce:GuidType" use="required"/>
      <xs:attribute name="patternsProximity" type="mce:ProximityType" use="required"/>
      <xs:attribute name="recommendedConfidence" type="mce:ProbabilityType"/>
      <xs:attribute name="workload" type="mce:WorkloadType"/>
    </xs:complexType>
    <xs:complexType name="PatternType">
      <xs:sequence>
        <xs:element name="IdMatch" type="mce:IdMatchType"/>
        <xs:choice minOccurs="0" maxOccurs="unbounded">
          <xs:element name="Match" type="mce:MatchType"/>
          <xs:element name="Any" type="mce:AnyType"/>
        </xs:choice>
      </xs:sequence>
      <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
    </xs:complexType>
    <xs:complexType name="AffinityType">
      <xs:sequence>
        <xs:element name="Evidence" type="mce:EvidenceType" maxOccurs="unbounded"/>
      </xs:sequence>
      <xs:attribute name="id" type="mce:GuidType" use="required"/>
      <xs:attribute name="evidencesProximity" type="mce:ProximityType" use="required"/>
      <xs:attribute name="thresholdConfidenceLevel" type="mce:ProbabilityType" use="required"/>
      <xs:attribute name="workload" type="mce:WorkloadType"/>
    </xs:complexType>
    <xs:complexType name="EvidenceType">
      <xs:sequence>
        <xs:choice maxOccurs="unbounded">
          <xs:element name="Match" type="mce:MatchType"/>
          <xs:element name="Any" type="mce:AnyType"/>
        </xs:choice>
      </xs:sequence>
      <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
    </xs:complexType>
    <xs:complexType name="IdMatchType">
      <xs:attribute name="idRef" type="xs:string" use="required"/>
    </xs:complexType>
    <xs:complexType name="MatchType">
      <xs:attribute name="idRef" type="xs:string" use="required"/>
    </xs:complexType>
    <xs:complexType name="AnyType">
      <xs:sequence>
        <xs:choice maxOccurs="unbounded">
          <xs:element name="Match" type="mce:MatchType"/>
          <xs:element name="Any" type="mce:AnyType"/>
        </xs:choice>
      </xs:sequence>
      <xs:attribute name="minMatches" type="xs:nonNegativeInteger" default="1"/>
      <xs:attribute name="maxMatches" type="xs:nonNegativeInteger" use="optional"/>
    </xs:complexType>
    <xs:simpleType name="ProximityType">
      <xs:restriction base="xs:positiveInteger">
        <xs:minInclusive value="1"/>
      </xs:restriction>
    </xs:simpleType>
    <xs:simpleType name="ProbabilityType">
      <xs:restriction base="xs:integer">
        <xs:minInclusive value="1"/>
        <xs:maxInclusive value="100"/>
      </xs:restriction>
    </xs:simpleType>
    <xs:simpleType name="WorkloadType">
      <xs:restriction base="xs:string">
        <xs:enumeration value="Exchange"/>
        <xs:enumeration value="Outlook"/>
      </xs:restriction>
    </xs:simpleType>
    <xs:complexType name="RegexType">
      <xs:simpleContent>
        <xs:extension base="xs:string">
          <xs:attribute name="id" type="xs:token" use="required"/>
        </xs:extension>
      </xs:simpleContent>
    </xs:complexType>
    <xs:complexType name="KeywordType">
      <xs:sequence>
        <xs:element name="Group" type="mce:GroupType" maxOccurs="unbounded"/>
      </xs:sequence>
      <xs:attribute name="id" type="xs:token" use="required"/>
    </xs:complexType>
    <xs:complexType name="GroupType">
      <xs:sequence>
        <xs:choice>
          <xs:element name="Term" type="mce:TermType" maxOccurs="unbounded"/>
        </xs:choice>
      </xs:sequence>
      <xs:attribute name="matchStyle" default="word">
        <xs:simpleType>
          <xs:restriction base="xs:NMTOKEN">
            <xs:enumeration value="word"/>
            <xs:enumeration value="string"/>
          </xs:restriction>
        </xs:simpleType>
      </xs:attribute>
    </xs:complexType>
    <xs:complexType name="TermType">
      <xs:simpleContent>
        <xs:extension base="mce:RestrictedTermType">
          <xs:attribute name="caseSensitive" type="xs:boolean" default="false"/>
        </xs:extension>
      </xs:simpleContent>
    </xs:complexType>
    <xs:complexType name="LocalizedStringsType">
      <xs:sequence>
        <xs:element name="Resource" type="mce:ResourceType" maxOccurs="unbounded">
          <xs:key name="UniqueLangCodeUsedInNamePerResource">
            <xs:selector xpath="mce:Name"/>
            <xs:field xpath="@langcode"/>
          </xs:key>
          <xs:key name="UniqueLangCodeUsedInDescriptionPerResource">
            <xs:selector xpath="mce:Description"/>
            <xs:field xpath="@langcode"/>
          </xs:key>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
    <xs:complexType name="ResourceType">
      <xs:sequence>
        <xs:element name="Name" type="mce:ResourceNameType" maxOccurs="unbounded"/>
        <xs:element name="Description" type="mce:DescriptionType" minOccurs="0" maxOccurs="unbounded"/>
      </xs:sequence>
      <xs:attribute name="idRef" type="mce:GuidType" use="required"/>
    </xs:complexType>
    <xs:complexType name="ResourceNameType">
      <xs:simpleContent>
        <xs:extension base="xs:string">
          <xs:attribute name="default" type="xs:boolean" default="false"/>
          <xs:attribute name="langcode" type="mce:LangType" use="required"/>
        </xs:extension>
      </xs:simpleContent>
    </xs:complexType>
    <xs:complexType name="DescriptionType">
      <xs:simpleContent>
        <xs:extension base="xs:string">
          <xs:attribute name="default" type="xs:boolean" default="false"/>
          <xs:attribute name="langcode" type="mce:LangType" use="required"/>
        </xs:extension>
      </xs:simpleContent>
    </xs:complexType>
  </xs:schema>
```

## Más información

[Prevención de pérdida de datos](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Definir sus propios tipos de información y plantillas de DLP](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

