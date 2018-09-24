---
title: Esquema de la regla XML y guía de la estructura de la regla para archivos de directivas de DLP
TOCTitle: Desarrollo de archivos de plantilla de directivas de DLP
ms:assetid: 4b263547-aef4-4ee8-aa4f-fa64a5863189
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ674703(v=EXCHG.150)
ms:contentKeyID: 49895615
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Desarrollo de archivos de plantilla de directivas de DLP

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

En esta introducción se explican los componentes de una definición de esquema XML para los archivos de plantilla de directiva de prevención de pérdida de datos (DLP). También se proporciona un archivo de plantilla en formato XML a modo de ejemplo, que le será útil para comprender la arquitectura general de DLP y el proceso de desarrollo de reglas antes de comenzar. Para obtener más información, vea [Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) y [Definir sus propios tipos de información y plantillas de DLP](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

Para facilitar el uso y la administración de las soluciones de prevención de pérdida de datos, Microsoft Exchange Server 2013 incluye un modelo conceptual conocido como directivas DLP y plantillas de directiva. Las plantillas de directiva DLP proporcionan un diseño preliminar para la directiva DLP que se pretende crear. Para que resulten útiles, las plantillas de directiva DLP deben encapsular todas las directivas y objetos de datos necesarios para cumplir un objetivo de directiva específico, como una regulación o una necesidad empresarial. La plantilla no está destinada a ningún entorno en concreto. Sencillamente, se trata de una definición o modelo de directiva que se puede proporcionar como parte de la configuración del producto o que los proveedores de software independientes o socios pueden suministrar. Por otro lado, las directivas DLP son creaciones de instancias en tiempo de ejecución de las plantillas que son específicas de un entorno de implementación. Un marco de directivas de mensajería existente puede incorporar directivas DLP mediante el uso de reglas de transporte. Las reglas de transporte ofrecen una gran flexibilidad para adaptar y expresar la variedad de soluciones de DLP.

## Estructura y orígenes de plantillas de directiva

Por lo general, las plantillas de directiva DLP están influenciadas por varios orígenes, como las directivas de procesamiento basadas en servidor, las directivas de equipo cliente u otras construcciones de directiva, según se muestra en la siguiente imagen:

![Factores que influyen en las plantillas de directiva](images/JJ674703.12f48e4f-d7b8-4ddd-87e8-8477983252ec(EXCHG.150).gif "Factores que influyen en las plantillas de directiva")

No obstante, las plantillas de directiva DLP se pueden administrar de manera sencilla mediante el Shell de administración de Exchange y las interfaces basadas en Internet, como el Centro de administración de Exchange, que incluye capacidades de importación, exportación, eliminación y consulta. Las directivas DLP se crean mediante una referencia a una plantilla de directiva DLP como parte del proceso de creación. Estas plantillas de directiva DLP referenciadas pueden ser referencias a otras instaladas en el sistema, que se almacenan en los Servicios de dominio de Active Directory o que se proporcionan como una entrada directamente desde las plantillas suministradas externamente.

Las plantillas de directiva DLP se representan como documentos XML. Se utiliza un solo esquema XML para las directivas proporcionadas en Exchange o de manera externa. La estructura conceptual del documento XML se representa en la siguiente tabla, que muestra los elementos más importantes. El conjunto de definiciones de componentes de directiva permite conseguir un objetivo específico de la directiva, como puede ser una regulación o una necesidad empresarial.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento estructural</th>
<th>Significado o ejemplo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Publicador</p></td>
<td><p>Microsoft o socio</p></td>
</tr>
<tr class="even">
<td><p>Version</p></td>
<td><p>15.0.1.0</p></td>
</tr>
<tr class="odd">
<td><p>Nombre de la directiva</p></td>
<td><p>PCI-DSS</p></td>
</tr>
<tr class="even">
<td><p>Descripción</p></td>
<td><p>La directiva DLP PCI-DSS ayuda a detectar la presencia de datos sujetos al Estándar de seguridad de datos PCI (PCI DSS), incluidos los datos como los números de tarjetas de crédito o de débito. El uso de esta directiva no garantiza la conformidad con ninguna regulación. Después de finalizar la prueba, realice los cambios de configuración necesarios en Exchange, de modo que la transmisión de información cumpla con las directivas de su organización. Algunos ejemplos son la configuración de TLS con socios comerciales conocidos o la adición de acciones de reglas de transporte más restrictivas, como la adición de protección de derechos en los mensajes que contienen este tipo de datos.</p></td>
</tr>
<tr class="odd">
<td><p>Metadatos</p></td>
<td><p>Etiquetas para describir las regulaciones locales, el país o región, las palabras clave y mucho más.</p></td>
</tr>
<tr class="even">
<td><p>Conjunto de construcciones de la directiva</p></td>
<td><ol>
<li><p>Definiciones de reglas de transporte, como las condiciones y las acciones.</p></li>
<li><p>Definiciones de comportamiento del cliente de correo electrónico que controlan la experiencia del cliente a través de notificaciones interactivas.</p></li>
<li><p>Referencias de configuración que opcionalmente se deben coordinar con la configuración específica del entorno del cliente.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Conjunto de clasificaciones de datos</p></td>
<td><ol>
<li><p>Especifica las afinidades o entidades de clasificación.</p></li>
<li><p>Las entidades tienen recuento y confianza, las afinidades sólo tienen confianza.</p></li>
<li><p>Incluye su propio conjunto de propiedades y esquema de clasificación.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## Definición del formato de una plantilla de directiva

Las plantillas de directiva DLP se expresan como documentos XML que se adhieren al siguiente esquema. Tenga en cuenta que el XML no distingue entre mayúsculas y minúsculas. Por ejemplo, `dlpPolicyTemplates` funcionará, pero `DlpPolicyTemplates` no funcionará.

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <dlpPolicyTemplates>
    <dlpPolicyTemplate id="F7C29AEC-A52D-4502-9670-141424A83FAB" mode="Audit" state="Enabled" version="15.0.2.0">
      <contentVersion>4</contentVersion>
      <publisherName>Microsoft</publisherName>
      <name>
        <localizedString lang="en">PCI-DSS</localizedString>
      </name>
      <description>
        <localizedString lang="en">Detects the presence of information subject to Payment Card Industry Data Security Standard (PCI-DSS) compliance requirements.</localizedString>
      </description>
      <keywords></keywords>
      <ruleParameters></ruleParameters>
      <ruleParameters/>
      <policyCommands>
        <!-- The contents below are applied/executed as rules directly in PS - -->
        <commandBlock>
          <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP Policy."]]>
        </commandBlock>
        <commandBlock>
          <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "%%DlpPolicyName%%" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP Policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]>
        </commandBlock>
      </policyCommands>
      <policyCommandsResources></policyCommandsResources>
    </dlpPolicyTemplate>
  </dlpPolicyTemplates>
  ```

Si incluye un parámetro para cualquier elemento en el archivo XML que contenga un espacio, deberá entrecomillar el parámetro con comillas dobles o no funcionará correctamente. En el siguiente ejemplo, el parámetro a continuación de `-SentToScope` es válido y no lleva comillas dobles porque es una cadena continua de caracteres sin espacio. Sin embargo, el parámetro provisto para –`Comments` no aparecerá en el Centro de administración de Exchange porque no lleva comillas dobles y contiene espacios.

  ```powershell
  <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments Monitors payment card information sent inside the organization -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
  ```

## Elemento localizedString

El formato de la plantilla ofrece la posibilidad de localizar cadenas en la plantilla que se pueden presentar al usuario final, por ejemplo, como parte de la selección de las plantillas de directiva DLP que se van a instalar. El elemento localizedString se puede usar para proporcionar varias definiciones para los campos Nombre y Descripción.

## Nodo ruleParameters

Se trata de un conjunto opcional de parámetros que se debe suministrar durante la fase de instalación de la plantilla al crear una directiva DLP para asignarla a objetos de implementación específicos. Por ejemplo, un grupo de distribución real que está disponible en la implementación.

## Elemento dlpPolicyTemplate

Este es el elemento raíz de la plantilla de directiva DLP y es necesario en todas las plantillas. En la tabla siguiente se muestran los atributos disponibles:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del atributo</th>
<th>¿Es necesario?</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Versión</p></td>
<td><p>Sí</p></td>
<td><p>Número de versión usado en este documento de plantilla de directiva DLP.</p></td>
</tr>
<tr class="even">
<td><p>State</p></td>
<td><p>No</p></td>
<td><p>Configuración opcional predeterminada para el estado de la directiva.</p></td>
</tr>
<tr class="odd">
<td><p>Mode</p></td>
<td><p>No</p></td>
<td><p>Configuración opcional predeterminada para el modo de la directiva.</p></td>
</tr>
<tr class="even">
<td><p>Id</p></td>
<td><p>No</p></td>
<td><p>GUID para identificar de manera exclusiva esta definición de plantilla de directiva DLP con el siguiente formato: &quot;A29C69BF-4F98-47F1-9A99-5771DFD2C27F&quot;.</p></td>
</tr>
</tbody>
</table>


Los elementos secundarios incluyen la siguiente secuencia de elementos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento secundario</th>
<th>(mínimo, máximo)</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PublisherName</p></td>
<td><p>(1, 1)</p></td>
<td><p>Metadatos para el publicador de la plantilla</p></td>
</tr>
<tr class="even">
<td><p>Name</p></td>
<td><p>(1, 1)</p></td>
<td><p>Nombre localizable de esta plantilla.</p></td>
</tr>
<tr class="odd">
<td><p>Description</p></td>
<td><p>(1, 1)</p></td>
<td><p>Descripción localizable de esta plantilla.</p></td>
</tr>
<tr class="even">
<td><p>Keywords</p></td>
<td><p>(1, 1)</p></td>
<td><p>Lista de palabras clave que se aplica a esta plantilla. Una plantilla puede tener una lista vacía de palabras clave.</p></td>
</tr>
<tr class="odd">
<td><p>RuleParameters</p></td>
<td><p>(0, 1)</p></td>
<td><p>Lista de parámetros de plantilla que se utilizan en la definición de la directiva.</p></td>
</tr>
<tr class="even">
<td><p>PolicyCommands</p></td>
<td><p>(0, 1)</p></td>
<td><p>Lista de definiciones de reglas de transporte de esta directiva. Este elemento es opcional.</p></td>
</tr>
</tbody>
</table>


## Plantilla de directiva DLP: Comandos de directivas

Esta parte de la plantilla de directiva contiene la lista de comandos del Shell de administración de Exchange que se usan para crear instancias de la definición de la directiva. En el proceso de importación se ejecutan los comandos como parte del proceso de creación de instancias. Los comandos de directiva de muestra se proporcionan aquí.

  ```powershell
  <PolicyCommands>
      <!-- The contents below are applied/executed as rules directly in PS - -->
        <CommandBlock> <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "PCI-DSS" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP policy."]]></CommandBlock>
        <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
    </PolicyCommands>
  ```

Los cmdlets tienen el formato de la sintaxis estándar de cmdlets del Shell de administración de Exchange. Los comandos se ejecutan en secuencia. Los nodos de comando pueden contener un bloque de script que está compuesto por varios comandos. En el siguiente ejemplo se muestra cómo incrustar un paquete de reglas de clasificación dentro de una plantilla de directiva DLP y cómo instalar el paquete de reglas como parte del proceso de creación de la directiva. El paquete de reglas de clasificación se incrusta en la plantilla de directiva y, a continuación, se pasa como un parámetro al cmdlet en la plantilla:

```powershell
<CommandBlock>
  <![CDATA[
$rulePack = [system.Text.Encoding]::Unicode.GetBytes('<?xml version="1.0" encoding="utf-16"?>
<rulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">

  <RulePack id="c3f021a3-c265-4dc2-b3a7-41a1800bf518">
    <Version major="1" minor="0" build="0" revision="0"/>
    <Publisher id="e17451d3-9648-4117-a0b1-493a6d5c73ad"/>
    <Details defaultLangCode="en-us">
      <LocalizedDetails langcode="en-us">
        <PublisherName>Contoso</PublisherName>
        <Name>Contoso Sample Rule Pack</Name>
        <Description>This is a sample rule package</Description>
      </LocalizedDetails>
    </Details>
  </RulePack>

  <Rules>
    <Entity id="7cc35258-6b35-4415-baff-a76d1a018980" patternsProximity="300" recommendedConfidence="85" workload="Exchange">     

      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_Contoso" />
        <Any minMatches="1">
          <Match idRef="Regex_conf" />
        </Any>
      </Pattern>
    </Entity>

    <Regex id="Regex_Contoso">(?i)(\bContoso\b)</Regex>
    <Regex id="Regex_conf">(?i)(\bConfidential\b)</Regex>

    <LocalizedStrings>
      <Resource idRef="7cc35258-6b35-4415-baff-a76d1a018980">
        <Name default="true" langcode="en-us">
          Confidential Information Rule
        </Name>
        <Description default="true" langcode="en-us">
          Sample rule pack - Detects Contoso confidential information
        </Description>
      </Resource>
    </LocalizedStrings>
  </Rules>

</RulePackage>

')


New-ClassificationRuleCollection -FileData $rulePack 
New-TransportRule -name "customEntity" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -MessageContainsDataClassifications @{Name="Confidential Information Rule"} -SetAuditSeverity High]]>
</CommandBlock> 
```

Los elementos secundarios incluyen la siguiente secuencia ordenada de elementos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento secundario</th>
<th>(Mínimo, máximo)</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CommandBlock</p></td>
<td><p>(1, n)</p></td>
<td><p>Bloque de comandos que se ejecuta en PowerShell. Los bloques de comandos se ejecutan en secuencia.</p></td>
</tr>
</tbody>
</table>


## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Definir sus propios tipos de información y plantillas de DLP](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[Importar una plantilla de directiva DLP personalizada desde un archivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

