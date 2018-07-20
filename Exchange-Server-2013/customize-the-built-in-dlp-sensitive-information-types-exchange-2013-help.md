---
title: 'Personalizar los tipos de información confidencial de DLP integrados: Exchange 2013 Help'
TOCTitle: Personalizar los tipos de información confidencial de DLP integrados
ms:assetid: 3f8bf141-2e7c-4ea7-b102-dfd6c41539da
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn781122(v=EXCHG.150)
ms:contentKeyID: 62757550
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Personalizar los tipos de información confidencial de DLP integrados

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-05-26_

Cuando busca información confidencial en el correo electrónico, es necesario describir esa información en lo que se denomina una *regla*. Prevención de pérdida de datos (DLP) incluye un paquete de 51 reglas para los tipos más comunes de información confidencial que se pueden usar inmediatamente. Para usar estas reglas, deberá incluirlas en una directiva. Quizás quiera ajustar estas reglas integradas para satisfacer las necesidades específicas de su organización y, para hacerlo, puede crear un tipo personalizado de información confidencial. En este tema se muestra cómo personalizar el archivo XML que contiene la colección de reglas existente para detectar una amplia variedad de posible información de tarjeta de crédito.

Puede tomar este ejemplo y aplicarlo a otros tipos integrados de información confidencial. Para obtener una lista de los tipos de información confidencial predeterminados y las definiciones de XML, vea el tema [Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

Este tema le guía por las secciones siguientes sobre las personalizaciones de las reglas XML:

  - Exportar el archivo XML de las reglas actuales

  - Busque la regla que quiere modificar en el archivo XML

  - Modificar el XML y crear un nuevo tipo de información confidencial

  - Quitar el requisito de evidencias confirmativas de un tipo de información confidencial

  - Buscar palabras clave que son específicas de su organización

  - Cargar la regla

Para aprender qué son las diferentes partes de las reglas y qué hacen, vea el Glosario de términos al final de este tema.

## Exportar el archivo XML de las reglas actuales

Para exportar el XML, necesitará usar Shell de administración de Exchange o . Para Exchange Server 2013, vea [Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\)). Para Exchange Online, vea [Conectarse a Exchange Online mediante PowerShell remoto](https://technet.microsoft.com/es-es/library/jj984289\(v=exchg.150\)).

1.  En Shell de administración de Exchange o Exchange Online PowerShell, escriba **Get-ClassificationRuleCollection** para visualizar las reglas de la organización en la pantalla. Si no ha creado las suyas propias, solo verá las reglas integradas predeterminadas, con la etiqueta "Paquete de reglas de Microsoft".

2.  Guarde las reglas de su organización en una variable; para ello, escriba **$ruleCollections = Get-ClassificationRuleCollection**. Almacenar algo en una variable hace que esté fácilmente disponible más adelante en un formato que funciona para los comandos de PowerShell remoto.

3.  Escriba **Set-Content -path "C:\\custompath\\exportedRules.xml" -Encoding Byte -Value $ruleCollections.SerializedClassificationRuleCollection** para crear un archivo XML con formato con todos esos datos. (**Set-content** es la parte del cmdlet que escribe el XML en el archivo).
    

    > [!IMPORTANT]
    > Asegúrese de que usa la ubicación del archivo donde realmente se almacena el paquete de reglas. <STRONG>C:\custompath\</STRONG> es un marcador de posición.



## Busque la regla que quiere modificar en el archivo XML

Los cmdlets anteriores exportaron toda la *colección de reglas*, que incluye las 51 reglas predeterminadas que proporcionamos. A continuación, tendrá que buscar específicamente la regla Número de tarjeta de crédito que quiere modificar.

1.  Use un editor de texto para abrir el archivo XML exportado en la sección anterior.

2.  Desplácese hasta la etiqueta **\<Rules\>**, que es el comienzo de la sección que contiene las reglas de DLP. (Como este archivo XML contiene la información de toda la colección de reglas, contiene otra información al principio que debe pasar para llegar a las reglas).

3.  Busque **Func\_credit\_card** para encontrar la definición de la regla Número de tarjeta de crédito. (En el XML, los nombres de regla no pueden contener espacios, por lo que normalmente se reemplazan por caracteres de subrayado y, a veces, los nombres de regla se abrevian). Un ejemplo de esto es la regla Número de seguridad social de EE. UU., que abreviado es "SSN". La regla XML Número de tarjeta de crédito debe ser como la muestra de código siguiente.
    
        <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085"
               patternsProximity="300" recommendedConfidence="85">
              <Pattern confidenceLevel="85">
               <IdMatch idRef="Func_credit_card" />
                <Any minMatches="1">
                  <Match idRef="Keyword_cc_verification" />
                  <Match idRef="Keyword_cc_name" />
                  <Match idRef="Func_expiration_date" />
                </Any>
              </Pattern>
            </Entity>

Ahora que ha encontrado la definición de la regla Número de tarjeta de crédito en el XML, puede personalizar el código XML de la regla para que se adapte a sus necesidades. (Para obtener información sobre las definiciones XML, vea el Glosario de términos al final de este tema).

## Modificar el XML y crear un nuevo tipo de información confidencial

En primer lugar, deberá crear un nuevo tipo de información confidencial porque las reglas predeterminadas no se pueden modificar directamente. Puede hacer muchas cosas con los tipos de información confidencial personalizados, tal y como se describe en [Desarrollar paquetes de reglas de información confidencial](technical-description-of-xml-schema-for-dlp-rule-packages.md). En este ejemplo, lo haremos sencillo y solo se eliminarán las evidencias confirmativas y se agregarán palabras clave a la regla Número de tarjeta de crédito.

Todas las definiciones de regla XML se basan en la siguiente plantilla general. Tiene que copiar y pegar el XML de definición de Número de tarjeta de crédito en la plantilla, modificar algunos valores (tenga en cuenta los marcadores de posición “. . .” en el siguiente ejemplo) y, después, cargar el XML modificado como una nueva regla que se pueda usar en directivas.

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id=". . .">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id=". . ." /> 
        <Details defaultLangCode=". . .">
          <LocalizedDetails langcode=" . . . ">
             <PublisherName>. . .</PublisherName>
             <Name>. . .</Name>
             <Description>. . .</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
       <!-- Paste the Credit Card Number rule definition here.--> 
    
          <LocalizedStrings>
             <Resource idRef=". . .">
               <Name default="true" langcode=" . . . ">. . .</Name>
               <Description default="true" langcode=". . ."> . . .</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

Ahora tiene algo parecido al siguiente XML. Como los paquetes de reglas y las reglas se identifican por sus GUID únicos, tiene que generar dos GUID: uno para el paquete de reglas y otro para reemplazar el GUID de la regla Número de tarjeta de crédito. (El GUID del ID de entidad en la muestra de código siguiente es una de las cuatro definiciones de regla integradas que tiene que reemplazar por una nueva). Hay varias maneras de generar GUID, pero puede hacerlo fácilmente en PowerShell escribiendo **\[guid\]::NewGuid()**.

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id="8aac8390-e99f-4487-8d16-7f0cdee8defc">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id="8d34806e-cd65-4178-ba0e-5d7d712e5b66" />
        <Details defaultLangCode="en">
          <LocalizedDetails langcode="en">
            <PublisherName>Contoso Ltd.</PublisherName>
            <Name>Financial Information</Name>
            <Description>Modified versions of the Microsoft rule package</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f"
           patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    
          <LocalizedStrings>
             <Resource idRef="db80b3da-0056-436e-b0ca-1f4cf7080d1f"> 
    <!-- This is the GUID for the preceding Credit Card Number entity because the following text is for that Entity. -->
               <Name default="true" langcode="en-us">Modified Credit Card Number</Name>
               <Description default="true" langcode="en-us">Credit Card Number that looks for additional keywords, and another version of Credit Card Number that doesn't require keywords (but has a lower confidence level)</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

## Quitar el requisito de evidencias confirmativas de un tipo de información confidencial

Ahora que tiene un tipo de información confidencial que puede cargar a su entorno de Exchange, el siguiente paso es hacer que la regla sea más específica. Modifique la regla para solo parezca un número de 16 dígitos que pasa la suma de comprobación pero no requiere evidencia (confirmativa) adicional (por ejemplo, palabras clave). Para ello, tiene que quitar la parte del código XML que busca la evidencia confirmativa. La evidencia confirmativa es muy útil para reducir falsos positivos porque, normalmente, hay determinadas palabras claves o una fecha de caducidad cerca del número de tarjeta de crédito. Si quita esa evidencia, debe ajustar también la seguridad que tiene de haber encontrado un número de tarjeta de crédito; para ello, reduzca **confidenceLevel**, que es 85 en el ejemplo.

    <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="300"
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
          </Pattern>
        </Entity>

## Buscar palabras clave que son específicas de su organización

Quizás quiera requerir evidencia confirmativa pero con palabras claves diferentes o adicionales, y quizás quiera cambiar dónde buscar esa evidencia. Puede ajustar el valor de **patternsProximity** para aumentar o reducir el radio donde se buscará la evidencia confirmativa alrededor del número de 16 dígitos. Para agregar sus propias palabras clave, debe definir una lista de palabras clave y hacer referencia a ella en su regla. El siguiente código XML agrega las palabras clave "company card" y "Contoso card" para que los mensajes que contengan esas frases a menos de 150 caracteres de un número de tarjeta de crédito se identifiquen como número de tarjeta de crédito.

    <Rules>
    <! -- Modify the patternsProximity to be "150" rather than "300." -->
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="150" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
    <!-- Add the following XML, which references the keywords at the end of the XML sample. -->
              <Match idRef="My_Additional_Keywords" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    <!-- Add the following XML, and update the information inside the <Term> tags with the keywords that you want to detect. -->
        <Keyword id="My_Additional_Keywords">
          <Group matchStyle="word">
            <Term caseSensitive="false">company card</Term>
            <Term caseSensitive="false">Contoso card</Term>
          </Group>
        </Keyword>

## Cargar la regla

Para cargar la regla, siga el procedimiento siguiente.

1.  Guárdela como un archivo .xml con codificación Unicode. Es importante porque la regla no funcionará si se guarda con una codificación diferente.

2.  Conéctese a Shell de administración de Exchange o Exchange Online PowerShell. Para Exchange Server 2013, vea [Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\)). Para Exchange Online, vea [Conectarse a Exchange Online mediante PowerShell remoto](https://technet.microsoft.com/es-es/library/jj984289\(v=exchg.150\)).

3.  En Shell de administración de Exchange o Exchange Online PowerShell, escriba **New-ClassificationRuleCollection -FileData (Get-Content -Path "C:\\custompath\\MyNewRulePack.xml " -Encoding Byte)**.
    

    > [!IMPORTANT]
    > Asegúrese de que usa la ubicación del archivo donde realmente se almacena el paquete de reglas. <STRONG>C:\custompath\</STRONG> es un marcador de posición.



4.  Para confirmar, escriba **S** y presione **Entrar**.

5.  Compruebe que la nueva regla se cargó; para ello, escriba **Get-DataClassification**, que ahora muestra el nombre de la regla.

Para comenzar a usar la nueva regla para detectar información confidencial, tiene que agregarla a una directiva DLP. Para saber cómo agregar la regla a una directiva, vea [Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md).

## Glosario de términos

Estas son las definiciones de los términos que encontró en este procedimiento.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Término</th>
<th>Definición</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Entidad</p></td>
<td><p>Las entidades son lo que llamamos tipos de información confidencial, como números de tarjeta de crédito. Cada entidad tiene un GUID único como ID. Si copia un GUID y lo busca en el código XML, encontrará la definición de regla XML y todas las traducciones localizadas de esa regla XML. Para encontrar esta definición, puede buscar el GUID de la traducción y, después, buscar por ese GUID.</p></td>
</tr>
<tr class="even">
<td><p>Funciones</p></td>
<td><p>El archivo XML hace referencia a <strong>Func_credit_card</strong>, que es una función en código compilado. Las funciones se usan para ejecutar regexe complejos y verificar que las sumas de comprobación de nuestras reglas integradas coinciden). Como esto se produce en el código, algunas de las variables no aparecen en el archivo XML.</p></td>
</tr>
<tr class="odd">
<td><p>IdMatch</p></td>
<td><p>Este es el identificador para el que el patrón está intentando encontrar coincidencias, por ejemplo, un número de tarjeta de crédito. Encontrará más información sobre esta etiqueta y sobre la etiqueta <strong>Match</strong> en <a href="technical-description-of-xml-schema-for-dlp-rule-packages.md">Entity rules</a>.</p></td>
</tr>
<tr class="even">
<td><p>Lista de palabras clave</p></td>
<td><p>El archivo XML también hace referencia a <strong>keyword_cc_verification</strong> y <strong>keyword_cc_name</strong>, que son listas de palabras en las que buscamos coincidencias dentro de <strong>patternsProximity</strong> para la entidad. Actualmente no se muestran en el archivo XML.</p></td>
</tr>
<tr class="odd">
<td><p>Patrón</p></td>
<td><p>El patrón contiene la lista de lo que el tipo confidencial está buscando. Incluye palabras clave, regexe y funciones internas (que realizan tareas como verificar sumas de comprobación). Los tipos de información confidencial pueden tener varios patrones con confianzas únicas. Esto resulta útil para crear un tipo de información confidencial que devuelve una confianza alta si se encuentra evidencia confirmativa y una confianza menor si se encuentra poca o ninguna evidencia confirmativa.</p></td>
</tr>
<tr class="even">
<td><p>Patrón confidenceLevel</p></td>
<td><p>Este es el nivel de confianza en el que el motor de DLP encontró una coincidencia. Este nivel de confianza está asociado con una coincidencia del patrón si se cumplen los requisitos del patrón. Esta es la medida de la confianza que debe tener en cuenta al usar las reglas de transporte de Exchange (ETR).</p></td>
</tr>
<tr class="odd">
<td><p>patternsProximity</p></td>
<td><p>Cuando encontramos lo que parece un patrón de número de tarjeta de crédito, <strong>patternsProximity</strong> es la proximidad alrededor de la cual buscaremos una evidencia confirmativa.</p></td>
</tr>
<tr class="even">
<td><p>recommendedConfidence</p></td>
<td><p>Este es el nivel de confianza que recomendamos para esta regla. La confianza recomendada se aplica a entidades y afinidades. En el caso de las entidades, este número nunca se evalúa con el valor de <strong>confidenceLevel</strong> del patrón. Es simplemente una sugerencia para ayudar a elegir un nivel de confianza si quiere aplicar uno. Para las afinidades, el valor de <strong>confidenceLevel</strong> del patrón debe ser mayor que el número de <strong>recommendedConfidence</strong> para que se invoque una acción de ETR. El valor de <strong>recommendedConfidence</strong> es el nivel de confianza predeterminado que se usa en las ETR que invoca una acción. Si quiere, puede cambiar manualmente la ETR que se invocará según el nivel de confianza del patrón.</p></td>
</tr>
</tbody>
</table>


## Más información

  - [Cómo se aplican las reglas de DLP para la evaluación de mensajes](how-dlp-rules-are-applied-to-evaluate-messages-exchange-2013-help.md)

  - [Crear una nueva directiva de DLP personalizada](create-a-custom-dlp-policy-exchange-2013-help.md)

  - [Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

