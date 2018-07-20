---
title: 'Condiciones de las reglas de transporte (predicados): Exchange 2013 Help'
TOCTitle: Excepciones (predicados) y condiciones de reglas de flujo de correo
ms:assetid: c918ea00-1e68-4b8b-8d51-6966b4432e2d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638183(v=EXCHG.150)
ms:contentKeyID: 49895910
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Condiciones de las reglas de transporte (predicados)

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-12-20_

Las condiciones y excepciones de reglas de flujo de correo (también denominadas reglas de transporte) identifican los mensajes a los que la regla se aplica o no se aplica. Por ejemplo, si la regla agrega un aviso de declinación de responsabilidades a los mensajes, puede configurar la regla para que solo se aplique a los mensajes que contengan palabras específicas, a los mensajes enviados por usuarios específicos o a todos los mensajes excepto los enviados por los miembros de un grupo específico. En conjunto, las condiciones y excepciones de las reglas de flujo de correo también se denominan *predicados*, ya que para cada condición hay una excepción correspondiente que usa exactamente la misma configuración y sintaxis. La única diferencia es que las condiciones especifican mensajes que se incluyen, mientras que las excepciones especifican mensajes que se excluyen.

La mayoría de las condiciones y excepciones tienen una propiedad que requiere uno o más valores. Por ejemplo, la condición **El remitente es** requiere que se especifique el remitente del mensaje. Algunas condiciones tienen dos propiedades. Por ejemplo, la condición **Un encabezado de mensaje incluye cualquiera de estas palabras** requiere una propiedad que especifique el campo de encabezado del mensaje y una segunda propiedad que especifique el texto que hay que buscar en el campo de encabezado. Algunas condiciones o excepciones no tienen ninguna propiedad. Por ejemplo, la condición **Cualquier adjunto con contenido ejecutable** simplemente busca datos adjuntos de mensajes con contenido ejecutable.

Para obtener más información acerca de las reglas de flujo de correo en Exchange Server 2013, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

Para obtener más información acerca de las condiciones y excepciones en las reglas de flujo de correo en Exchange Online Protection o Exchange Online, consulte [Excepciones (predicados) y las condiciones de la regla de flujo de correo en Exchange Online](https://technet.microsoft.com/es-es/library/jj919235\(v=exchg.150\)) o [Mail excepciones (predicados) y las condiciones de la regla de flujo de Exchange Online Protection](https://technet.microsoft.com/es-es/library/jj919234\(v=exchg.150\)).

## Condiciones y excepciones para reglas de flujo de correo en servidores de buzones

Las tablas en las secciones siguientes describen las condiciones y excepciones que están disponibles en las reglas de flujo de correo en servidores de buzones. Los tipos de propiedades se describen en la sección tipos de propiedad .

Remitentes

Destinatarios

Asunto o cuerpo del mensaje

Datos adjuntos

Todos los destinatarios

Tipos de información confidencial, valores Para y CC, tamaño y juegos de caracteres del mensaje

Remitente y destinatario

Propiedades del mensaje

Encabezados del mensaje

**Notas**:

  - Después de seleccionar una condición o excepción en el Centro de administración de Exchange (EAC), el valor que finalmente se muestra en el campo **Aplicar esta regla si** o **Excepto si** suele ser distinto (más corto) que el valor de ruta de acceso de clic que haya seleccionado. Además, al crear reglas basadas en una plantilla (una lista filtrada de escenarios), puede a menudo seleccionar un nombre corto de condición en lugar de seguir la ruta de acceso de clic completa. Los nombres cortos y los valores de ruta de acceso de clic completa se muestran en la columna EAC de las tablas.

  - Si selecciona **\[Aplicar a todos los mensajes\]** en el EAC, no puede especificar ninguna condición más. El equivalente en el Shell de administración de Exchange consiste en crear una regla sin especificar ningún parámetro de condición.

  - La configuración y las propiedades son las mismas en las condiciones y excepciones, por lo que el resultado del cmdlet **Get-TransportRulePredicate** no muestra excepciones por separado. Además, los nombres de algunos de los predicados que devuelve este cmdlet son diferentes de los nombres de parámetro correspondientes y es posible que un predicado requiera varios parámetros.

## Remitentes

En el caso de condiciones y excepciones que examinen la dirección del remitente, puede especificar dónde busca la regla la dirección del remitente.

En el EAC, en la sección **Propiedades de esta regla**, haga clic en **La dirección del remitente debe coincidir con el siguiente elemento del mensaje**. Tenga en cuenta que es posible que tenga que hacer clic en **Más opciones** para ver esta configuración. En el Shell de administración de Exchange, el parámetro es *SenderAddressLocation*. Los valores disponibles son los siguientes:

  - **Encabezado**   Solo se examinan los remitentes de los encabezados del mensaje (por ejemplo, los campos **From**, **Sender** o **Reply-To**). Este es el valor predeterminado y es la forma en que funcionaban las reglas de flujo de correo antes de la actualización acumulativa 1 (CU1) para Exchange 2013.

  - **Sobres**    Examinar sólo remitentes desde el sobre del mensaje (el valor de **MAIL FROM** que se utilizó en la transmisión de SMTP, que normalmente se almacena en el campo de **Return-Path** ). Tenga en cuenta que la búsqueda de sobres de mensajes sólo está disponible para las siguientes condiciones (y las correspondientes excepciones):
    
      - **El remitente es** (*From*)
    
      - **El remitente es un miembro de** (*FromMemberOf*)
    
      - **La dirección del remitente incluye** (*FromAddressContainsWords*)
    
      - **La dirección del remitente coincide con** (*FromAddressMatchesPatterns*)
    
      - **El dominio del remitente es** (*SenderDomainIs*)

  - **Encabezado o sobre** (`HeaderOrEnvelope`)   Se examinan los remitentes que aparecen en el encabezado del mensaje y el sobre del mensaje.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condición o excepción en el EAC</th>
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>El remitente es</strong></p>
<p><strong>El remitente</strong> &gt; <strong>es esta persona</strong></p></td>
<td><p><em>From</em></p>
<p><em>ExceptIfFrom</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes enviados por los buzones, los usuarios de correo o los contactos de correo de la Exchange organización que se especifiquen.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El remitente está ubicado</strong></p>
<p><strong>El remitente</strong> &gt; <strong>es externo o interno</strong></p></td>
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Mensajes enviados por remitentes internos o remitentes externos.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El remitente es un miembro de</strong></p>
<p><strong>El remitente</strong> &gt; <strong>es miembro de este grupo</strong></p></td>
<td><p><em>FromMemberOf</em></p>
<p><em>ExceptIfFromMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes enviados por un miembro del grupo especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>La dirección del remitente incluye</strong></p>
<p><strong>El remitente</strong> &gt; <strong>la dirección incluye alguna de estas palabras</strong></p></td>
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes que contienen las palabras especificadas en la dirección de correo electrónico del remitente.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>La dirección del remitente coincide con</strong></p>
<p><strong>El remitente</strong> &gt; <strong>la dirección coincide con cualquiera de estos patrones de texto</strong></p></td>
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes en los que la dirección de correo electrónico contiene patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Las propiedades especificadas del remitente incluyen cualquiera de estas palabras</strong></p>
<p><strong>El remitente</strong> &gt; <strong>tiene propiedades específicas que incluyen alguna de estas palabras</strong></p></td>
<td><p><em>SenderADAttributeContainsWords</em></p>
<p><em>ExceptIfSenderADAttributeContainsWords</em></p></td>
<td><p>Primera propiedad: <code>ADAttribute</code></p>
<p>Segunda propiedad: <code>Words</code></p></td>
<td><p>Mensajes en los que el atributo Active Directory especificado del remitente contiene alguna de las palabras especificadas.</p>
<p>Tenga en cuenta que el atributo <strong>Country</strong> requiere el valor de código de país de dos letras (por ejemplo, DE para Alemania).</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Las propiedades especificadas del remitente coinciden con estos patrones de texto</strong></p>
<p><strong>El remitente</strong> &gt; <strong>tiene propiedades específicas que coinciden con estos patrones de texto</strong></p></td>
<td><p><em>SenderADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfSenderADAttributeMatchesPatterns</em></p></td>
<td><p>Primera propiedad: <code>ADAttribute</code></p>
<p>Segunda propiedad: <code>Patterns</code></p></td>
<td><p>Mensajes en los que el atributo Active Directory especificado del remitente contiene patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El remitente ha invalidado las Sugerencias de directivas</strong></p>
<p><strong>El remitente</strong> &gt; <strong>ha reemplazado a la Sugerencia de directiva</strong></p></td>
<td><p><em>HasSenderOverride</em></p>
<p><em>ExceptIfHasSenderOverride</em></p></td>
<td><p>N/D</p></td>
<td><p>Mensajes en los que el remitente ha elegido invalidar una directiva de prevención de pérdida de datos (DLP). Para obtener más información sobre las directivas DLP, consulte <a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">Prevención de pérdida de datos</a>.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>La dirección IP del remitente está en el rango</strong></p>
<p><strong>El remitente</strong> &gt; <strong>la dirección IP está en uno de estos rangos o coincide exactamente con</strong></p></td>
<td><p><em>SenderIPRanges</em></p>
<p><em>ExceptIfSenderIPRanges</em></p></td>
<td><p><code>IPAddressRanges</code></p></td>
<td><p>Mensajes en los que la dirección IP del remitente coincide con la dirección IP especificada o se encuentra en el intervalo de direcciones IP especificado.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El dominio del remitente es</strong></p>
<p><strong>El remitente</strong> &gt; <strong>el dominio es</strong></p></td>
<td><p><em>SenderDomainIs</em></p>
<p><em>ExceptIfSenderDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>Mensajes en los que el dominio de la dirección de correo electrónico del remitente coincide con el valor especificado.</p>
<p>Si tiene que buscar dominios de remitentes que <em>contengan</em> el dominio especificado (por ejemplo, cualquier subdominio de un dominio), use la condición <strong>La dirección del remitente coincide con</strong> (<em>FromAddressMatchesPatterns</em>) y especifique el dominio mediante la sintaxis: <code>'@domain\.com$'</code>.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Destinatarios


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condición o excepción en el EAC</th>
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>El destinatario es</strong></p>
<p><strong>El destinatario</strong> &gt; <strong>es esta persona</strong></p></td>
<td><p><em>SentTo</em></p>
<p><em>ExceptIfSentTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>En contacto con mensajes, donde uno de los destinatarios es el buzón especificado, el usuario de correo o correo en la organización de Exchange. Los destinatarios pueden estar en los campos <strong>To</strong>, <strong>Cc</strong>o <strong>Bcc</strong> del mensaje.</p>
<p><strong>Nota:</strong> no puede especificar los grupos de distribución o grupos de seguridad de correo. Si necesita actuar sobre los mensajes que se envían a un grupo, utilice la condición <strong>para la caja contiene</strong> (<em>AnyOfToHeader</em>).</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El destinatario está ubicado</strong></p>
<p><strong>El destinatario</strong> &gt; <strong>es externo o interno</strong></p></td>
<td><p><em>SentToScope</em></p>
<p><em>ExceptIfSentToScope</em></p></td>
<td><p><code>UserScopeTo</code></p></td>
<td><p>Mensajes que se envían a destinatarios internos, destinatarios externos en organizaciones asociadas o destinatarios externos en organizaciones no asociadas.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El destinatario es un miembro de</strong></p>
<p><strong>El destinatario</strong> &gt; <strong>es miembro de este grupo</strong></p></td>
<td><p><em>SentToMemberOf</em></p>
<p><em>ExceptIfSentToMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes que contienen destinatarios que son miembros del grupo especificado. El grupo puede incluirse en los campos <strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong> del mensaje.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>La dirección del destinatario incluye</strong></p>
<p><strong>El destinatario</strong> &gt; <strong>la dirección incluye alguna de estas palabras</strong></p></td>
<td><p><em>RecipientAddressContainsWords</em></p>
<p><em>ExceptIfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes que contienen las palabras especificadas en la dirección de correo electrónico del destinatario.</p>
<p><strong>Nota:</strong> Esta condición no considera los mensajes que se envían a direcciones de proxy del destinatario. Solo coincide con los mensajes que se envían a la dirección de correo electrónico principal del destinatario.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>La dirección del destinatario coincide con</strong></p>
<p><strong>El destinatario</strong> &gt; <strong>la dirección coincide con cualquiera de estos patrones de texto</strong></p></td>
<td><p><em>RecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes en los que la dirección de correo electrónico de un destinatario contiene patrones de texto que coinciden con las expresiones regulares especificadas.</p>
<p><strong>Nota:</strong> Esta condición no considera los mensajes que se envían a direcciones de proxy del destinatario. Solo coincide con los mensajes que se envían a la dirección de correo electrónico principal del destinatario.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Las propiedades especificadas del destinatario incluyen cualquiera de estas palabras</strong></p>
<p><strong>El destinatario</strong> &gt; <strong>tiene propiedades específicas que incluyen alguna de estas palabras</strong></p></td>
<td><p><em>RecipientADAttributeContainsWords</em></p>
<p><em>ExceptIfRecipientADAttributeContainsWords</em></p></td>
<td><p>Primera propiedad: <code>ADAttribute</code></p>
<p>Segunda propiedad: <code>Words</code></p></td>
<td><p>Mensajes en los que el atributo Active Directory especificado del destinatario contiene alguna de las palabras especificadas.</p>
<p>Tenga en cuenta que el atributo <strong>Country</strong> requiere el valor de código de país de dos letras (por ejemplo, DE para Alemania).</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Las propiedades especificadas del destinatario coinciden con estos patrones de texto</strong></p>
<p><strong>El destinatario</strong> &gt; <strong>tiene propiedades específicas que coinciden con estos patrones de texto</strong></p></td>
<td><p><em>RecipientADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfRecipientADAttributeMatchesPatterns</em></p></td>
<td><p>Primera propiedad: <code>ADAttribute</code></p>
<p>Segunda propiedad: <code>Patterns</code></p></td>
<td><p>Mensajes en los que el atributo Active Directory especificado del destinatario contiene patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El dominio de un destinatario es</strong></p>
<p><strong>El destinatario</strong> &gt; <strong>el dominio es</strong></p></td>
<td><p><em>RecipientDomainIs</em></p>
<p><em>ExceptIfRecipientDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>Mensajes en los que el dominio de la dirección de correo electrónico del destinatario coincide con el valor especificado.</p>
<p>Si tiene que buscar dominios de destinatarios que <em>contengan</em> el dominio especificado (por ejemplo, cualquier subdominio de un dominio), use la condición <strong>La dirección del destinatario coincide con</strong> (<em>RecipientAddressMatchesPatterns</em>) y especifique el dominio mediante la sintaxis: <code>'@domain\.com$'</code>.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Asunto o cuerpo del mensaje


> [!NOTE]
> La búsqueda de palabras o patrones de texto en el asunto u otros campos del encabezado del mensaje ocurre <EM>después</EM> de que el mensaje se haya decodificado desde el método de codificación de transferencia de contenido MIME que se usó para transmitir el mensaje binario entre los servidores SMTP en texto ASCII. No puede usar condiciones ni excepciones para buscar los valores codificados sin formato (normalmente, Base64) del asunto o de otros campos del encabezado del mensaje.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condición o excepción en el EAC</th>
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>El asunto o el cuerpo incluye</strong></p>
<p><strong>El asunto o el cuerpo</strong> &gt; <strong>el asunto o el cuerpo incluye cualquiera de estas palabras</strong></p></td>
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes que contienen las palabras especificadas en el campo <strong>Subject</strong> o el cuerpo del mensaje.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El asunto o el cuerpo coincide con</strong></p>
<p><strong>El asunto o el cuerpo</strong> &gt; <strong>el asunto o el cuerpo coincide con estos patrones de texto</strong></p></td>
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes en los que el campo <strong>Subject</strong> o el cuerpo del mensaje contienen patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El asunto incluye</strong></p>
<p><strong>El asunto o el cuerpo</strong> &gt; <strong>el asunto incluye cualquiera de estas palabras</strong></p></td>
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes que contengan las palabras especificadas en el campo <strong>Subject</strong>.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El asunto coincide con</strong></p>
<p><strong>El asunto o el cuerpo</strong> &gt; <strong>el asunto coincide con estos patrones de texto</strong></p></td>
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes dónde el campo <strong>Subject</strong> contiene patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Datos adjuntos

Para obtener más información acerca de cómo las reglas de flujo de correo inspeccionar archivos adjuntos de mensajes, consulte [Usar reglas de transporte para inspeccionar datos adjuntos de mensajes](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condición o excepción en el EAC</th>
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>El contenido de algún documento adjunto incluye</strong></p>
<p><strong>Cualquier dato adjunto</strong> &gt; <strong>el contenido incluye alguna de estas palabras</strong></p></td>
<td><p><em>AttachmentContainsWords</em></p>
<p><em>ExceptIfAttachmentContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes en los que un archivo adjunto contiene las palabras especificadas.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El contenido de los datos adjuntos coincide con</strong></p>
<p><strong>Cualquier dato adjunto</strong> &gt; <strong>el contenido coincide con estos patrones de texto</strong></p></td>
<td><p><em>AttachmentMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes en los que un archivo adjunto contiene patrones de texto que coinciden con las expresiones regulares especificadas.</p>
<p><strong>Nota:</strong> sólo los primeros 150 kilobytes (KB) de los archivos adjuntos se analizan.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El contenido de cualquier documento adjunto no se puede inspeccionar</strong></p>
<p><strong>Cualquier dato adjunto</strong> &gt; <strong>no se puede inspeccionar el contenido</strong></p></td>
<td><p><em>AttachmentIsUnsupported</em></p>
<p><em>ExceptIfAttachmentIsUnsupported</em></p></td>
<td><p>N/D</p></td>
<td><p>Mensajes donde Exchange nativamente no reconocen datos adjuntos y el IFilter requerido no está instalado en el servidor de buzón. Para obtener más información, consulte <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Registrar IFilters de Filter Pack con Exchange 2013</a>.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El nombre del archivo adjunto coincide con</strong></p>
<p><strong>Cualquier dato adjunto</strong> &gt; <strong>el nombre de archivo coincide con estos patrones de texto</strong></p></td>
<td><p><em>AttachmentNameMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentNameMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes en los que el nombre de archivo de los datos adjuntos contiene patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>La extensión del archivo adjunto coincide con</strong></p>
<p><strong>Cualquier dato adjunto</strong> &gt; <strong>la extensión del archivo incluye con estas palabras</strong></p></td>
<td><p><em>AttachmentExtensionMatchesWords</em></p>
<p><em>ExceptIfAttachmentExtensionMatchesWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes en los que la extensión de archivo de los datos adjuntos coincide con cualquiera de las palabras especificadas.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Cualquier adjunto es mayor o igual que...</strong></p>
<p><strong>Cualquier dato adjunto &gt; el tamaño es mayor o igual que</strong></p></td>
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Mensajes en los que algún documento adjunto es mayor o igual que el valor especificado.</p>
<p>En el EAC, solo se puede especificar el tamaño en kilobytes (KB).</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El mensaje no finalizó el análisis</strong></p>
<p><strong>Cualquier dato adjunto</strong> &gt; <strong>no se completó el análisis</strong></p></td>
<td><p><em>AttachmentProcessingLimitExceeded</em></p>
<p><em>ExceptIfAttachmentProcessingLimitExceeded</em></p></td>
<td><p>N/D</p></td>
<td><p>Mensajes en los que el motor de reglas no pudo completar el examen de los datos adjuntos. Puede usar esta condición para crear reglas que trabajen conjuntamente para identificar y procesar mensajes en los que el contenido no pudo examinarse por completo.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Cualquier documento adjunto tiene contenido ejecutable</strong></p>
<p><strong>Cualquier dato adjunto</strong> &gt; <strong>tiene contenido ejecutable</strong></p></td>
<td><p><em>AttachmentHasExecutableContent</em></p>
<p><em>ExceptIfAttachmentHasExecutableContent</em></p></td>
<td><p>N/D</p></td>
<td><p>Mensajes en los que un archivo adjunto es un archivo ejecutable. El sistema inspecciona las propiedades del archivo en lugar de confiar en la extensión del archivo.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Todos los datos adjuntos están protegidos con contraseña</strong></p>
<p><strong>Cualquier dato adjunto</strong> &gt; <strong>está protegido con contraseña</strong></p></td>
<td><p><em>AttachmentIsPasswordProtected</em></p>
<p><em>ExceptIfAttachmentIsPasswordProtected</em></p></td>
<td><p>N/D</p></td>
<td><p>Mensajes en los que un archivo adjunto está protegido por contraseña (y, por lo tanto, no se puede examinar). La detección de contraseñas solo funciona para documentos de Office y archivos .zip.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Todos los destinatarios

Las condiciones y excepciones de esta sección proporcionan una única función que afecta a *todos* los destinatarios cuando el mensaje contiene al menos uno de los destinatarios especificados. Por ejemplo, supongamos que tiene una regla que rechaza mensajes. Si usa una condición de destinatarios de la sección Destinatarios, el mensaje solo se rechaza para los destinatarios especificados. Por ejemplo, si la regla encuentra al destinatario especificado en un mensaje, pero el mensaje contiene otros cinco destinatarios. El mensaje se rechaza para ese destinatario y se entrega a los otros cinco destinatarios.

Si agrega una condición de destinatarios de esta sección, ese mismo mensaje se rechaza para el destinatario detectado y los otros cinco destinatarios.

Por el contrario, una excepción de destinatarios de esta sección *evita* que la acción de regla se aplique a *todos* los destinatarios del mensaje, no solo para los destinatarios detectados.

**Nota:**  Esta condición no considera los mensajes que se envían a direcciones de proxy del destinatario. Solo coincide con los mensajes que se envían a la dirección de correo electrónico principal del destinatario.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condición o excepción en el EAC</th>
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Cualquier dirección de destinatario incluye</strong></p>
<p><strong>Cualquier destinatario</strong> &gt; <strong>la dirección incluye cualquiera de estas palabras</strong></p></td>
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes que contienen las palabras especificadas en los campos <strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong> del mensaje.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Cualquier dirección de destinatario coincide con</strong></p>
<p><strong>Cualquier destinatario</strong> &gt; <strong>la dirección coincide con cualquiera de estos patrones de texto</strong></p></td>
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes en los que los campos <strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong> contienen patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Tipos de información confidencial, valores Para y CC, tamaño y juegos de caracteres del mensaje

Las condiciones de esta sección que esperan para valores en los campos **To** y **Cc** se comportan como las condiciones en la sección de todos los destinatarios (*todos los* destinatarios del mensaje se ven afectados por la regla, no sólo el ha detectado destinatarios).

**Nota:**  Esta condición no considera los mensajes que se envían a direcciones de proxy del destinatario. Solo coincide con los mensajes que se envían a la dirección de correo electrónico principal del destinatario.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condición o excepción en el EAC</th>
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>El mensaje contiene información confidencial</strong></p>
<p><strong>El mensaje</strong> &gt; <strong>contiene cualquiera de estos tipos de información confidencial</strong>.</p></td>
<td><p><em>MessageContainsDataClassifications</em></p>
<p><em>ExceptIfMessageContainsDataClassifications</em></p></td>
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>Mensajes que contienen información confidencial, tal y como se define en las directivas de prevención de pérdida de datos (DLP).</p>
<p>Esta condición es necesaria en reglas que usan la acción <strong>Notificar al remitente con una sugerencia de directiva<em>NotifySender</em> (</strong>).</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El cuadro Para contiene</strong></p>
<p><strong>El mensaje</strong> &gt; <strong>El cuadro Para contiene esta persona</strong></p></td>
<td><p><em>AnyOfToHeader</em></p>
<p><em>ExceptIfAnyOfToHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes en los que el campo <strong>To</strong> incluye alguno de los destinatarios especificados.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El cuadro Para contiene a un miembro de</strong></p>
<p><strong>El mensaje</strong> &gt; <strong>El cuadro Para contiene un miembro de este grupo</strong></p></td>
<td><p><em>AnyOfToHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes en los que el campo <strong>To</strong> contiene un destinatario que es miembro del grupo especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El cuadro CC contiene</strong></p>
<p><strong>El mensaje</strong> &gt; <strong>El cuadro Cc contiene esta persona</strong></p></td>
<td><p><em>AnyOfCcHeader</em></p>
<p><em>ExceptIfAnyOfCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes en los que el campo <strong>Cc</strong> incluye alguno de los destinatarios especificados.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El cuadro CC contiene a un miembro de</strong></p>
<p><strong>El mensaje</strong> &gt; <strong>contiene un miembro de este grupo</strong></p></td>
<td><p><em>AnyOfCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes en los que el campo <strong>Cc</strong> contiene un destinatario que es miembro del grupo especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El cuadro Para o CC contiene</strong></p>
<p><strong>El mensaje</strong> &gt; <strong>La casilla CC o Para contiene esta persona</strong></p></td>
<td><p><em>AnyOfToCcHeader</em></p>
<p><em>ExceptIfAnyOfToCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes en los que los campos <strong>To</strong> o <strong>Cc</strong> contienen alguno de los destinatarios especificados.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El cuadro Para o CC contiene un miembro de</strong></p>
<p><strong>El mensaje</strong> &gt; <strong>La casilla CC o Para contiene un miembro de este grupo</strong></p></td>
<td><p><em>AnyOfToCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes en los que los campos <strong>To</strong> o <strong>Cc</strong> contienen un destinatario que es miembro del grupo especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El tamaño del mensaje es mayor o igual que</strong></p>
<p><strong>El mensaje</strong> &gt; <strong>el tamaño es igual o mayor que</strong></p></td>
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Mensajes en los que el tamaño total (mensaje más archivos adjuntos) es mayor o igual al valor especificado.</p>
<p>En el EAC, solo se puede especificar el tamaño en kilobytes (KB).</p>
<p><strong>Nota:</strong> Los límites de tamaño de los mensajes en los buzones se evalúan antes de las reglas de flujo de correo. Un mensaje que es demasiado grande para un buzón se rechazará antes de que una regla con esta condición sea capaz de actuar en el mensaje.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El nombre del conjunto de caracteres del mensaje incluye alguna de estas palabras</strong></p>
<p><strong>El mensaje</strong> &gt; <strong>el nombre del conjunto de caracteres incluye alguna de estas palabras</strong></p></td>
<td><p><em>ContentCharacterSetContainsWords</em></p>
<p><em>ExceptIfContentCharacterSetContainsWords</em></p></td>
<td><p><code>CharacterSets</code></p></td>
<td><p>Mensajes que contienen alguno de los nombres de juego de caracteres especificados.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Remitente y destinatario


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condición o excepción en el EAC</th>
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>El remitente es uno de los destinatarios</strong></p>
<p><strong>El remitente y el destinatario</strong> &gt; <strong>la relación del remitente con un destinatario es</strong></p></td>
<td><p><em>SenderManagementRelationship</em></p>
<p><em>ExceptIfSenderManagementRelationship</em></p></td>
<td><p><code>ManagementRelationship</code></p></td>
<td><p>Mensajes en los que el remitente es el administrador de un destinatario o está administrado por un destinatario.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El mensaje es entre miembros de estos grupos</strong></p>
<p><strong>El remitente y el destinatario</strong> &gt; <strong>el mensaje es entre miembros de estos grupos</strong></p></td>
<td><p><em>BetweenMemberOf1</em> y <em>BetweenMemberOf2</em></p>
<p><em>ExceptIfBetweenMemberOf1</em> y <em>ExceptIfBetweenMemberOf2</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensajes enviados entre miembros de estos grupos.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El administrador del remitente o destinatario es</strong></p>
<p><strong>El remitente y el destinatario</strong> &gt; <strong>el administrador del remitente o destinatario es esta persona</strong></p></td>
<td><p><em>ManagerForEvaluatedUser</em> y <em>ManagerAddress</em></p>
<p><em>ExceptIfManagerForEvaluatedUser</em> y <em>ExceptIfManagerAddress</em></p></td>
<td><p>Primera propiedad: <code>EvaluatedUser</code></p>
<p>Segunda propiedad: <code>Addresses</code></p></td>
<td><p>Mensajes en los que un usuario especificado es el administrador del remitente o el administrador de un destinatario.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Propiedad del remitente y cualquier destinatario compara como</strong></p>
<p><strong>El remitente y el destinatario</strong> &gt; <strong>la propiedad de remitente y destinatario se compara como</strong></p></td>
<td><p><em>ADAttributeComparisonAttribute</em> y <em>ADComparisonOperator</em></p>
<p><em>ExceptIfADAttributeComparisonAttribute</em> y <em>ExceptIfADComparisonOperator</em></p></td>
<td><p>Primera propiedad: <code>ADAttribute</code></p>
<p>Segunda propiedad: <code>Evaluation</code></p></td>
<td><p>Mensajes en los que el atributo Active Directory especificado para el remitente y el destinatario coinciden o no coinciden.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Propiedades del mensaje


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condición o excepción en el EAC</th>
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>El tipo de mensaje es</strong></p>
<p><strong>Las propiedades del mensaje</strong> &gt; <strong>incluir el tipo de mensaje</strong></p></td>
<td><p><em>MessageTypeMatches</em></p>
<p><em>ExceptIfMessageTypeMatches</em></p></td>
<td><p><code>MessageType</code></p></td>
<td><p>Mensajes del tipo especificado.</p>

> [!NOTE]
> Cuando Outlook o Outlook Web App está configurado para reenviar un mensaje, la propiedad <STRONG>ForwardingSmtpAddress</STRONG> se agrega al mensaje. El tipo de mensaje no se cambia a <CODE>AutoForward</CODE>.


</td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El mensaje se clasifica como</strong></p>
<p><strong>Las propiedades del mensaje</strong> &gt; <strong>incluir esta clasificación</strong></p></td>
<td><p><em>HasClassification</em></p>
<p><em>ExceptIfHasClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>Mensajes que tienen la clasificación de mensaje especificada. Se trata de una clasificación de mensaje personalizada que se puede crear en la organización con el cmdlet <strong>New-MessageClassification</strong>.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>El mensaje no está marcado con ninguna clasificación</strong></p>
<p><strong>Las propiedades del mensaje</strong> &gt; <strong>no incluir ninguna clasificación</strong></p></td>
<td><p><em>HasNoClassification</em></p>
<p><em>ExceptIfHasNoClassification</em></p></td>
<td><p>N/D</p></td>
<td><p>Mensajes que no tienen una clasificación de mensaje.</p></td>
<td><p>Exchange 2010 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>El mensaje tiene un SCL mayor o igual que</strong></p>
<p><strong>Las propiedades del mensaje</strong> &gt; <strong>incluir un SCL mayor que o igual a</strong></p></td>
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Mensajes que tienen asignado un nivel de confianza contra correo no deseado (SCL) mayor o igual que el valor especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>La importancia del mensaje se establece en</strong></p>
<p><strong>Las propiedades del mensaje</strong> &gt; <strong>incluir el nivel de importancia</strong></p></td>
<td><p><em>WithImportance</em></p>
<p><em>ExceptIfWithImportance</em></p></td>
<td><p><code>Importance</code></p></td>
<td><p>Mensajes que se marcan con el nivel de importancia especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Encabezados de mensaje


> [!NOTE]
> La búsqueda de palabras o patrones de texto en el asunto u otros campos del encabezado del mensaje ocurre <EM>después</EM> de que el mensaje se haya decodificado desde el método de codificación de transferencia de contenido MIME que se usó para transmitir el mensaje binario entre los servidores SMTP en texto ASCII. No puede usar condiciones ni excepciones para buscar los valores codificados sin formato (normalmente, Base64) del asunto o de otros campos del encabezado del mensaje.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condición o excepción en el EAC</th>
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Un encabezado de mensaje incluye</strong></p>
<p><strong>Un encabezado de mensaje</strong> &gt; <strong>incluye cualquiera de estas palabras</strong></p></td>
<td><p><em>HeaderContainsMessageHeader</em> y <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> y <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>Primera propiedad: <code>MessageHeaderField</code></p>
<p>Segunda propiedad: <code>Words</code></p></td>
<td><p>Mensajes que contienen el campo de encabezado especificado y el valor de ese campo de encabezado contiene las palabras especificadas.</p>
<p>El nombre del campo de encabezado y el valor del campo de encabezado siempre se utilizan conjuntamente.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Un encabezado de mensaje coincide</strong></p>
<p><strong>Un encabezado de mensaje</strong> &gt; <strong>coincide con estos patrones</strong></p></td>
<td><p><em>HeaderMatchesMessageHeader</em> y <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> y <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>Primera propiedad: <code>MessageHeaderField</code></p>
<p>Segunda propiedad: <code>Patterns</code></p></td>
<td><p>Mensajes que contienen el campo de encabezado especificado y el valor de ese campo de encabezado contiene las expresiones regulares especificadas.</p>
<p>El nombre del campo de encabezado y el valor del campo de encabezado siempre se utilizan conjuntamente.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Condiciones y excepciones para reglas de flujo de correo en servidores de transporte perimetral

Las condiciones y excepciones disponibles para reglas de flujo de correo en servidores de transporte perimetral son un pequeño subconjunto de lo que está disponible en los servidores de buzones. No hay ningún EAC en servidores de transporte perimetral, por lo que solo puede administrar reglas de flujo de correo en el Shell de administración de Exchange del servidor de transporte perimetral local. En la tabla siguiente se describen las condiciones y excepciones. Los tipos de propiedades se describen en la sección Tipos de propiedades.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetros de condición y de excepción en el Shell de administración de Exchange</th>
<th>Tipo de propiedad</th>
<th>Descripción</th>
<th>Disponible en</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes que contienen las palabras especificadas en los campos <strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong>.</p>
<p>Cuando un mensaje contiene el destinatario especificado, la acción de regla se aplica (o no) a <em>todos</em> los destinatarios del mensaje. Por ejemplo, el mensaje se rechaza para todos los destinatarios del mensaje, no solo para el destinatario especificado.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes en los que los campos <strong>To</strong>, <strong>Cc</strong> o <strong>Bcc</strong> contienen patrones de texto que coinciden con las expresiones regulares especificadas.</p>
<p>Cuando un mensaje contiene el destinatario especificado, la acción de regla se aplica (o no) a <em>todos</em> los destinatarios del mensaje. Por ejemplo, el mensaje se rechaza para todos los destinatarios del mensaje, no solo para el destinatario especificado.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Mensajes con datos adjuntos en los que algún adjunto es mayor o igual que el valor especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes que contienen las palabras especificadas en la dirección de correo electrónico del remitente.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes en los que la dirección de correo electrónico contiene patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Mensajes enviados por remitentes internos o remitentes externos.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>HeaderContainsMessageHeader</em> y <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> y <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>Primera propiedad: <code>MessageHeaderField</code></p>
<p>Segunda propiedad: <code>Words</code></p></td>
<td><p>Mensajes que contienen el campo de encabezado especificado y el valor de ese campo de encabezado contiene las palabras especificadas.</p>
<p>El nombre del campo de encabezado y el valor del campo de encabezado siempre se utilizan conjuntamente.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>HeaderMatchesMessageHeader</em> y <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> y <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>Primera propiedad: <code>MessageHeaderField</code></p>
<p>Segunda propiedad: <code>Patterns</code></p></td>
<td><p>Mensajes que contienen el campo de encabezado especificado y el valor de ese campo de encabezado contiene las expresiones regulares especificadas.</p>
<p>El nombre del campo de encabezado y el valor del campo de encabezado siempre se utilizan conjuntamente.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Mensajes en los que el tamaño total (mensaje más archivos adjuntos) es mayor o igual al valor especificado.</p></td>
<td><p>Exchange 2013 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Mensajes que tienen asignado un SCL mayor o igual que el valor especificado.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes que contienen las palabras especificadas en el campo <strong>Subject</strong>.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes dónde el campo <strong>Subject</strong> contiene patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensajes que contienen las palabras especificadas en el campo <strong>Subject</strong> o el cuerpo del mensaje.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensajes en los que el campo <strong>Subject</strong> o el cuerpo del mensaje contienen patrones de texto que coinciden con las expresiones regulares especificadas.</p></td>
<td><p>Exchange 2007 o posterior</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Tipos de propiedades

Los tipos de propiedades que se utilizan en las condiciones y excepciones se describen en la tabla siguiente.


> [!NOTE]
> Si la propiedad es una cadena, no se permiten espacios finales.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de propiedad</th>
<th>Valores válidos</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ADAttribute</code></p></td>
<td><p>Seleccionar de una lista predefinida de atributos de Active Directory</p></td>
<td><p>UNRESOLVED_TOKENBLOCK_VAL(PD_Transport_Rules_ADAttributes_Snippet)</p>
<p>En el EAC, para especificar varias palabras o patrones de texto para el mismo atributo, separe los valores con comas. Por ejemplo, el valor <strong>San Francisco, Palo Alto</strong> para el atributo <strong>City</strong> busca &quot;Ciudad es igual a San Francisco&quot; o &quot;Ciudad es igual a Palo Alto&quot;.</p>
<p>En el Shell de administración de Exchange, use la sintaxis <code>&quot;AttributeName1:Value1,Value 2 with spaces,Value3...&quot;,&quot;AttributeName2:Word4,Value 5 with spaces,Value6...&quot;</code>, donde <code>Value</code> es la palabra o el patrón de texto que quiere hacer coincidir.</p>
<p>Por ejemplo, <code>&quot;City:San Francisco,Palo Alto&quot;</code> o <code>&quot;City:San Francisco,Palo Alto&quot;</code>,<code>&quot;Department:Sales,Finance&quot;</code>.</p>
<p>Si especifica varios atributos o varios valores para el mismo atributo, se usará el operador <strong>or</strong>. No use valores con espacios iniciales o finales.</p>
<p>Tenga en cuenta que el atributo <strong>Country</strong> requiere el valor de código de país de dos letras ISO 3166-1 (por ejemplo, DE para Alemania). Para buscar valores, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=331680">https://go.microsoft.com/fwlink/p/?LinkId=331680</a>.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Destinatarios de Exchange</p></td>
<td><p>Según la naturaleza de la condición o excepción, es posible que pueda especificar cualquier objeto habilitado para correo en la organización (por ejemplo, condiciones relacionadas con el destinatario), o puede que esté limitado a un tipo de objeto específico (por ejemplo, grupos para condiciones de pertenencia a grupos). Además, es posible que la condición o excepción requiera un valor o permita varios valores.</p>
<p>En el Shell de administración de Exchange, separe los distintos valores mediante comas.</p>
<p><strong>Nota:</strong> Esta condición no considera los mensajes que se envían a direcciones de proxy del destinatario. Solo coincide con los mensajes que se envían a la dirección de correo electrónico principal del destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>CharacterSets</code></p></td>
<td><p>Matriz de nombres de juego de caracteres</p></td>
<td><p>Uno o más juegos de caracteres de contenido que existen en un mensaje. Por ejemplo:</p>
<ul>
<li><p><code>Arabic/iso-8859-6</code></p></li>
<li><p><code>Chinese/big5</code></p></li>
<li><p><code>Chinese/euc-cn</code></p></li>
<li><p><code>Chinese/euc-tw</code></p></li>
<li><p><code>Chinese/gb2312</code></p></li>
<li><p><code>Chinese/iso-2022-cn</code></p></li>
<li><p><code>Cyrillic/iso-8859-5</code></p></li>
<li><p><code>Cyrillic/koi8-r</code></p></li>
<li><p><code>Cyrillic/windows-1251</code></p></li>
<li><p><code>Greek/iso-8859-7</code></p></li>
<li><p><code>Hebrew/iso-8859-8</code></p></li>
<li><p><code>Japanese/euc-jp</code></p></li>
<li><p><code>Japanese/iso-022-jp</code></p></li>
<li><p><code>Japanese/shift-jis</code></p></li>
<li><p><code>Korean/euc-kr</code></p></li>
<li><p><code>Korean/johab</code></p></li>
<li><p><code>Korean/ks_c_5601-1987</code></p></li>
<li><p><code>Turkish/windows-1254</code></p></li>
<li><p><code>Turkish/iso-8859-9</code></p></li>
<li><p><code>Vietnamese/tcvn</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>DomainName</code></p></td>
<td><p>Matriz de dominios SMTP</p></td>
<td><p>Por ejemplo, <code>contoso.com</code> o <code>eu.contoso.com</code>.</p>
<p>En el Shell de administración de Exchange, puede especificar varios dominios separados por comas.</p></td>
</tr>
<tr class="odd">
<td><p><code>EvaluatedUser</code></p></td>
<td><p>Valor único de <strong>Remitente</strong> o <strong>Destinatario</strong></p></td>
<td><p>Especifica si la regla busca el administrador del remitente o el del destinatario.</p></td>
</tr>
<tr class="even">
<td><p><code>Evaluation</code></p></td>
<td><p>Valor único de <strong>Igual</strong> o <strong>No igual</strong> (<code>NotEqual</code>)</p></td>
<td><p>Al comparar el Active Directory atributo del remitente y los destinatarios, especifica si los valores deben coincidir o no.</p></td>
</tr>
<tr class="odd">
<td><p><code>Importance</code></p></td>
<td><p>Valor único de <strong>Bajo</strong>, <strong>Normal</strong> o <strong>Alto</strong></p></td>
<td><p>El nivel de importancia asignado al mensaje por el remitente en Outlook o Outlook Web App.</p></td>
</tr>
<tr class="even">
<td><p><code>IPAddressRanges</code></p></td>
<td><p>Matriz de direcciones IP o intervalos de direcciones</p></td>
<td><p>Especifique las direcciones IPv4 con la sintaxis siguiente:</p>
<ul>
<li><p><strong>Dirección IP única</strong>   Por ejemplo, <code>192.168.1.1</code>.</p></li>
<li><p><strong>Intervalo de direcciones IP</strong>   Por ejemplo, <code>192.168.0.1-192.168.0.254</code>.</p></li>
<li><p><strong>Intervalo de direcciones IP de Enrutamiento de interdominios sin clases</strong>   Por ejemplo, <code>192.168.0.1/25</code>.</p></li>
</ul>
<p>En el Shell de administración de Exchange, puede especificar varias direcciones IP o varios intervalos separados por comas.</p></td>
</tr>
<tr class="odd">
<td><p><code>ManagementRelationship</code></p></td>
<td><p>Valor único de <strong>Administrador</strong> o <strong>Subordinado directo</strong> (<code>DirectReport</code>)</p></td>
<td><p>Especifica la relación entre el remitente y los destinatarios. La regla comprueba el atributo <strong>Manager</strong> en Active Directory para ver si el remitente es el administrador de un destinatario o si está administrado por un destinatario.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageClassification</code></p></td>
<td><p>Clasificación única de mensaje</p></td>
<td><p>En el EAC, se selecciona en la lista de clasificaciones de mensajes que haya creado.</p>
<p>En el Shell de administración de Exchange, se usa el cmdlet <strong>Get-MessageClassification</strong> para identificar la clasificación de mensajes. Por ejemplo, use el comando siguiente para buscar mensajes con la clasificación <code>Company Internal</code> y anteponga el valor <code>CompanyInternal</code> al asunto del mensaje.</p>
<p><code>New-TransportRule &quot;Rule Name&quot; -HasClassification @(Get-MessageClassification &quot;Company Internal&quot;).Identity -PrependSubject &quot;CompanyInternal&quot;</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Una única cadena</p></td>
<td><p>Especifica el nombre del campo de encabezado. El nombre del campo de encabezado siempre se corresponde con el valor en el campo de encabezado (coincidencia de patrón de word o de texto).</p>
<p>El <em>encabezado del mensaje</em> es una colección de campos de encabezado obligatorios y opcionales del mensaje. Por ejemplo, <strong>To</strong>, <strong>From</strong>, <strong>Received</strong> y <strong>Content-Type</strong> son campos de encabezado. Los campos de encabezado oficiales están definidos en RFC 5322. Los campos de encabezado extraoficiales comienzan por <strong>X-</strong> y se denominan <em>encabezados X</em>.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageType</code></p></td>
<td><p>Valor único de tipo de mensaje</p></td>
<td><p>Especifica uno de los siguientes tipos de mensaje:</p>
<ul>
<li><p><strong>Respuesta automática</strong> (<code>OOF</code>)</p></li>
<li><p><strong>Reenvío automático</strong> (<code>AutoForward</code>)</p></li>
<li><p><strong>Cifrado</strong></p></li>
<li><p><strong>Calendario</strong></p></li>
<li><p><strong>Permiso controlado</strong> (<code>PermissionControlled</code>)</p></li>
<li><p><strong>Correo de voz</strong></p></li>
<li><p><strong>Firmado</strong></p></li>
<li><p><strong>Solicitud de aprobación</strong> (<code>ApprovalRequest</code>)</p></li>
<li><p><strong>Confirmación de lectura</strong> (<code>ReadReceipt</code>)</p></li>
</ul>

> [!NOTE]
> Cuando Outlook o Outlook Web App está configurado para reenviar un mensaje, la propiedad <STRONG>ForwardingSmtpAddress</STRONG> se agrega al mensaje. El tipo de mensaje no se cambia a <CODE>AutoForward</CODE>.


</td>
</tr>
<tr class="odd">
<td><p><code>Patterns</code></p></td>
<td><p>Matriz de expresiones regulares</p></td>
<td><p>Especifica una o varias expresiones regulares que se usan para identificar patrones de texto en valores. Para obtener más información, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=180327">Sintaxis de expresiones regulares</a>.</p>
<p>En el Shell de administración de Exchange, se especifican varias expresiones regulares separadas por comas y cada expresión regular se incluye entre comillas (&quot;).</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>Uno de los siguientes valores:</p>
<ul>
<li><p><strong>Omitir el filtrado de correo no deseado</strong> (<code>-1</code>)</p></li>
<li><p>Enteros (0 - 9)</p></li>
</ul></td>
<td><p>Especifica el nivel de confianza contra correo no deseado (SCL) asignado a un mensaje. Un valor SCL alto indica que el mensaje tiene más posibilidades de ser correo no deseado.</p></td>
</tr>
<tr class="odd">
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>Matriz de tipos de información confidencial</p></td>
<td><p>Especifica uno o más tipos de información confidencial que se definen en la organización. Para obtener una lista de tipos de información confidencial integrados, consulte <a href="what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md">Qué buscan los tipos de información confidencial de Exchange</a>.</p>
<p>En el Shell de administración de Exchange, use la sintaxis <code>@{&lt;SensitiveInformationType1&gt;},@{&lt;SensitiveInformationType2&gt;},...</code>. Por ejemplo, para buscar contenido que incluya al menos dos números de tarjeta de crédito y un número de enrutamiento ABA, use el valor <code>@{Name=&quot;Credit Card Number&quot;; minCount=&quot;2&quot;},@{Name=&quot;ABA Routing Number&quot;; minCount=&quot;1&quot;}</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Size</code></p></td>
<td><p>Valor único de tamaño</p></td>
<td><p>Especifica el tamaño de un archivo adjunto o de todo el mensaje.</p>
<p>En el EAC, solo se puede especificar el tamaño en kilobytes (KB).</p>
<p>En el Shell de administración de Exchange, cuando especifique un valor, califíquelo con una de las siguientes unidades:</p>
<ul>
<li><p><code>B</code> (bytes)</p></li>
<li><p><code>KB</code> (kilobytes)</p></li>
<li><p><code>MB</code> (megabytes)</p></li>
<li><p><code>GB</code> (gigabytes)</p></li>
</ul>
<p>Por ejemplo, <code>20MB</code></p>
<p>Los valores sin calificar normalmente se tratan como bytes, pero los valores pequeños se pueden redondear al kilobyte más cercano.</p></td>
</tr>
<tr class="odd">
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Valor único de <strong>Dentro de la organización</strong> (<code>InOrganization</code>) o de <strong>Fuera de la organización</strong> (<code>NotInOrganization</code>)</p></td>
<td><p>Un remitente se considera que está dentro de la organización si no se cumple ninguna de las siguientes condiciones:</p>
<ul>
<li><p>El remitente es un buzón, un usuario de correo, un grupo o una carpeta pública habilitada para correo que existe en el dominio de Active Directory de la organización.</p></li>
<li><p>Dirección de correo electrónico del remitente está en un dominio aceptado que esté configurado como un dominio autorizado o de un dominio de retransmisión interna, <strong>y</strong> el mensaje se ha enviado o recibido a través de una conexión autenticada. Para obtener más información acerca de los dominios aceptados, consulte <a href="accepted-domains-exchange-2013-help.md">Dominios aceptados</a>.</p></li>
</ul>
<p>Un remitente se considera que está fuera de la organización si no se cumple ninguna de las siguientes condiciones:</p>
<ul>
<li><p>La dirección de correo electrónico del remitente no pertenece a un dominio aceptado.</p></li>
<li><p>La dirección de correo electrónico del remitente pertenece a un dominio aceptado que se configura como dominio de retransmisión externa.</p></li>
</ul>

> [!NOTE]
> Para determinar si los contactos de correo se consideran que están dentro o fuera de la organización, la dirección del remitente se compara con los dominios aceptados de la organización.


</td>
</tr>
<tr class="even">
<td><p><code>UserScopeTo</code></p></td>
<td><p>Uno de los siguientes valores:</p>
<ul>
<li><p><strong>Dentro de la organización</strong> (<code>InOrganization</code>)</p></li>
<li><p><strong>Fuera de la organización</strong> (<code>NotInOrganization</code>)</p></li>
<li><p><strong>En una organización asociada externa</strong> (<code>ExternalPartner</code>)</p></li>
<li><p><strong>En una organización no asociada externa</strong> (<code>ExternalNonPartner</code>)</p></li>
</ul></td>
<td><p>Un destinatario se considera que está dentro de la organización si no se cumple ninguna de las siguientes condiciones:</p>
<ul>
<li><p>El destinatario es un buzón, un usuario de correo, un grupo o una carpeta pública habilitada para correo que existe en el dominio de Active Directory de la organización.</p></li>
<li><p>La dirección de correo electrónico del destinatario pertenece a un dominio aceptado que se configura como dominio autoritario o como dominio de retransmisión interna <strong>y</strong> el mensaje se envió o recibió por una conexión autenticada.</p></li>
</ul>
<p>Un destinatario se considera que está fuera de la organización si no se cumple ninguna de las siguientes condiciones:</p>
<ul>
<li><p>La dirección de correo electrónico del destinatario no pertenece a un dominio aceptado.</p></li>
<li><p>La dirección de correo electrónico del destinatario pertenece a un dominio aceptado que se configura como dominio de retransmisión externa.</p></li>
</ul>
<p>Las organizaciones asociadas externas son dominios externos en los que se ha configurado la seguridad de dominio (autenticación TLS mutua) para enviar correo.</p>
<p>Las organizaciones no asociadas externas son todos los demás dominios externos que no se consideran dominios asociados.</p></td>
</tr>
<tr class="odd">
<td><p><code>Words</code></p></td>
<td><p>Matriz de cadenas</p></td>
<td><p>Especifica una o más palabras que buscar. Las palabras no distinguen mayúsculas de minúsculas y pueden estar entre espacios y signos de puntuación. No se admiten caracteres comodín ni coincidencias parciales.</p>
<p>Por ejemplo, &quot;contoso&quot; coincide con &quot;Contoso.&quot;. Sin embargo, si el texto está rodeado por otros caracteres, no se considera una coincidencia. Por ejemplo, &quot;contoso&quot; no coincide con los valores siguientes:</p>
<ul>
<li><p>Acontoso</p></li>
<li><p>Contosoa</p></li>
<li><p>Acontosob</p></li>
</ul>
<p>Asimismo, el asterisco ( * ) se trata como un carácter literal y no se usa como carácter comodín.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Más información

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Acciones de regla de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Procedimientos de las reglas de transporte o de flujo de correo](mail-flow-or-transport-rule-procedures-exchange-2013-help.md)

[Excepciones (predicados) y las condiciones de la regla de flujo de correo en Exchange Online](https://technet.microsoft.com/es-es/library/jj919235\(v=exchg.150\)) para Exchange Online

[Mail excepciones (predicados) y las condiciones de la regla de flujo de Exchange Online Protection](https://technet.microsoft.com/es-es/library/jj919234\(v=exchg.150\)) para Protección de Exchange Online

