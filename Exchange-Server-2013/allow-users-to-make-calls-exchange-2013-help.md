---
title: 'Permitir que los usuarios realicen llamadas: Exchange 2013 Help'
TOCTitle: Permitir que los usuarios realicen llamadas
ms:assetid: b6e696ce-c848-475b-a598-9035677497e2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232172(v=EXCHG.150)
ms:contentKeyID: 51406539
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir que los usuarios realicen llamadas

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-03-09_

*Llamada externa* es el proceso mediante el cual los usuarios llaman a un plan de marcado de mensajería unificada usando un número de Outlook Voice Access, y colocan o transfieren una llamada a un número de teléfono interno o externo. La mensajería unificada usa muchas configuraciones de llamadas externas para marcar llamadas para los usuarios. Para configurar las llamadas externas, hay que configurar reglas de marcado, grupos de reglas de marcado y autorizaciones de marcado en los planos de marcado de mensajería unificada y, a continuación, autorizar las llamadas externas en los planos de marcado de mensajería unificada, en las directivas de buzones de correo de mensajería unificada y en los operadores automáticos. También puede configurar los planes de marcado de mensajería unificada para, así, tener códigos de acceso o de marcado, un prefijo numérico nacional y formatos numéricos internacionales o regionales/nacionales que le permitan controlar las llamadas externas en su organización. En este tema se tratan las reglas de marcado, los grupos de reglas de marcado y las autorizaciones de marcado, además de su uso para autorizar y controlar las llamadas externas en su organización.

**Contenido**

Información general

Types of users

Outdialing settings

Configuring outdialing

Applying configured dialing rule groups

Applying dialing rules

## Información general

Las llamadas externas se producen cuando:

  - Se efectúa una llamada a un número de teléfono externo.

  - Se transfiere una llamada a un operador automático.

  - Se transfiere una llamada a un usuario en su organización.

  - Un usuario habilitado para mensajería unificada usa la característica Reproducir en teléfono.

Para que la llamada externa funcione correctamente, hay que configurar correctamente los siguientes parámetros:

  - **Reglas de marcado**   Las reglas de marcado definen el número que marca el usuario habilitado para mensajería unificada y el número real que marcará la central de conmutación (PBX) o IP-PBX.

  - **Grupos de reglas de marcado**   Los grupos de reglas de marcado determinan el tipo de llamadas que pueden realizar los usuarios de un grupo de marcado.

  - **Autorizaciones de marcado**   Las autorizaciones de marcado determinan las restricciones que se van a imponer para evitar que los usuarios generen gastos innecesarios de teléfono o realicen llamadas a larga distancia.

Para habilitar la llamada externa para usuarios que realizan llamadas a un operador automático, deberá:

  - Asegurarse de que las puertas de enlace VoIP representadas por una puerta de enlace IP de mensajería unificada vinculada a un plan de marcado permita las llamadas salientes.

  - Crear grupos de reglas de marcado creando reglas de marcado en el plan de marcado de mensajería unificada.

  - Agregar autorizaciones de marcado para grupos de reglas de marcado regionales/nacionales e internacionales en el plan de marcado de mensajería unificada, en la directiva de buzones de correo de mensajería unificada o en el operador automático asociado al mismo plan de marcado que la puerta de enlace IP de mensajería unificada.

## Tipos de usuario

Hay dos tipos de usuario que pueden usar la característica de llamada externa en mensajería unificada: autenticados o no autenticados. No se autentica ninguno de los usuarios que llaman a un operador automático de Mensajería unificada. Si un usuario llama a un número de Outlook Voice Access, se considera como no autenticado porque no ha proporcionado ni su número de extensión ni su PIN, ni tampoco ha iniciado sesión en su buzón de correo. Los usuarios se autentican después de proporcionar su número de extensión y PIN e iniciar sesión correctamente en su buzón de correo.

Cuando los usuarios llaman a un número de Outlook Voice Access configurado en un plan de marcado de mensajería unificada e intentan realizar o transferir una llamada sin iniciar sesión en su buzón de correo, a dicha llamada solo se le aplica la configuración de llamada externa del plan de marcado de mensajería unificada. Si un usuario anónimo o no autenticado llama a un operador automático de mensajería unificada, se aplicarán a la llamada la configuración tanto de llamada externa del operador automático como del plan de marcado asociado al operador automático.

Si los usuarios llaman al número de Outlook Voice Access configurado en un plan de marcado e inician sesión correctamente en su buzón de correo, se convierten en usuarios autenticados. Cuando están autenticados, la configuración de llamada externa usa las reglas de marcado y la configuración de autorización de marcado de la directiva de buzones de correo de mensajería unificada vinculada a dichos usuarios.

Volver al principio

## Configuración de llamada externa

Debe configurar varios parámetros para aplicar las reglas de llamada externa a su organización. Aparte de los planes de marcado de mensajería unificada, los operadores automáticos de mensajería unificada y las directivas de buzones de correo de mensajería unificada que ha creado con las reglas de marcado y las autorizaciones de marcado correctas, deberá configurar también códigos de acceso, prefijos de números y formatos de números en los planes de marcado de mensajería unificada. Las siguientes configuraciones están establecidas en los planes de marcado, operadores automáticos y directivas de buzón de Mensajería unificada:

  - Códigos de acceso internacional, nacional y a línea externa

  - Prefijos numéricos nacionales

  - Formatos de número nacional/regional e internacional

  - Grupos de reglas de marcado nacional/regional e internacional configurados

  - Grupos de reglas de marcado nacional/regional e internacional permitidos

  - Entradas de reglas de marcado

  - Autorizaciones de marcado

Para que configure correctamente las llamadas externas de su organización, primero debe comprender cómo cada componente se puede usar con las llamadas externas y cómo se debe configurar dicho componente. La siguiente tabla presenta cada componente que se debe configurar en los planes de marcado de mensajería unificada, operadores automáticos de mensajería unificada y directivas de buzones de correo de mensajería unificada para que las llamadas externas funcionen correctamente.

### Componentes de llamada externa

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Códigos de marcado, prefijos numéricos y formatos de número</p></td>
<td><p>La mensajería unificada usa prefijos de números y formatos de números paras determinar el número correcto que se debe marcar para realizar una llamada saliente. Puede configurar códigos de marcado, prefijos numéricos y formatos de número para restringir las llamadas salientes a usuarios que llaman a un operador automático de mensajería unificada asociado a un plan de marcado de mensajería unificada, o bien a usuarios que llaman a un número de Outlook Voice Access configurado en el plan de marcado.</p></td>
</tr>
<tr class="even">
<td><p>Grupos de reglas de marcado</p></td>
<td><p>Los grupos de reglas de marcado se crean con el fin de modificar los teléfonos antes de enviarlos a la PBX de llamadas salientes. Los grupos de reglas de marcado quitan números de los números de teléfono (o los agregan) a los que la mensajería unificada llama. Por ejemplo, puede crear un grupo de reglas de marcado que automáticamente agregue el número 9 como prefijo a un número de teléfono de siete dígitos para así permitirle acceso a una línea externa. En este ejemplo, los usuarios que realicen llamadas salientes no tienen que marcar el número 9 antes del número de teléfono para poder ponerse en contacto con alguien que esté fuera de la organización.</p>
<p>Cada grupo de reglas de marcado contiene reglas de marcado que determinan los tipos de llamadas nacionales/regionales e internacionales que los usuarios pueden realizar dentro de un grupo de reglas de marcado. Los grupos de reglas de marcado se aplican a los usuarios que están asociados a un plan de marcado de mensajería unificada o a operadores automáticos de mensajería unificada, así como a directivas de buzones de correo de mensajería unificada que estén asociadas con el plan de marcado de mensajería unificada. Cada grupo de reglas de marcado debe contener al menos una regla de marcado.</p></td>
</tr>
<tr class="odd">
<td><p>Entradas de reglas de marcado</p></td>
<td><p>Cada regla de marcado se usa para determinar los tipos de llamada que pueden realizar los usuarios de un grupo de reglas de marcado. Una vez creado un grupo de reglas de marcado, hay que configurar una o más reglas de marcado.</p>
<p>Cuando configure cada regla de marcado, debe escribir el nombre de la regla de marcado, el patrón de número para transformar (<em>máscara de número</em>) y el número marcado. También puede escribir un comentario. Los comentarios se pueden usar para describir cómo se usará la regla de marcado o para describir un grupo de usuarios a los que se aplicará la regla de marcado. Cuando se agrega una máscara de número y el número marcado a la regla de marcado, la letra x se puede sustituir por un dígito en el número de teléfono (por ejemplo, 91425xxxxxxx). También tiene a su disposición el uso del símbolo asterisco (*) como un carácter comodín; por ejemplo: 91425*.</p></td>
</tr>
<tr class="even">
<td><p>Autorizaciones de marcado</p></td>
<td><p>Una autorización de marcado usa los grupos de reglas de marcado para aplicar restricciones de marcado a usuarios que están asociados a una directiva determinada de buzón de mensajería unificada, plan de marcado u operador automático. También se pueden usar si desea permitir que los usuarios realicen llamadas a números de teléfono nacionales/regionales e internacionales.</p>
<p>Después de crear las reglas de marcado en un plan de marcado de mensajería unificada, el grupo de reglas de marcado se agrega a una directiva de buzones de correo de mensajería unificada, a un plan de marcado o a un operador automático. Una vez agregado el grupo de reglas de marcado a la directiva de buzones de correo de mensajería unificada, todas las configuraciones o reglas que se hayan definido se aplicarán a los usuarios que tengan habilitada la mensajería unificada y que estén vinculados a la directiva de buzones de correo de mensajería unificada.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Cómo configurar la llamada externa

Un grupo de reglas de marcado es una colección de una o más reglas de marcado que se configuran en un plan de marcado de mensajería unificada. En un plan de marcado de mensajería unificada se pueden configurar dos tipos de grupos de reglas de marcado: nacional/regional e internacional. Los grupos de reglas de marcado nacional/regional se aplican a los números de teléfono que se marcan dentro del mismo país o región. Los grupos de reglas de marcado internacional se aplican a los números de teléfono internacionales que se marcan desde un país o región a otro país o región.

Cada plan de marcado de Mensajería unificada contiene uno o más grupos de reglas de marcado. Para aplicar un grupo de reglas de marcado a un conjunto de usuarios, después de crear el grupo de reglas de marcado hay que agregarlo a la lista de grupos de reglas de marcado permitidos en el plan de marcado de mensajería unificada y en los operadores automáticos de mensajería unificada y las directivas de buzones de correo de mensajería unificada que estén asociadas al plan de marcado de mensajería unificada.

Los grupos de reglas de marcado permiten especificar reglas de marcado que quiere aplicar a un grupo de usuarios habilitados para mensajería unificada que pertenecen a una categoría determinada. Por ejemplo, puede usar los grupos de reglas de marcado para especificar qué grupo de usuarios puede realizar llamadas internacionales y qué grupo puede realizar solamente llamadas nacionales o locales. Puede crear un grupo de reglas de marcado mediante el Centro de administración de Exchange (EAC) o el cmdlet **Set-UMDialPlan** en el Shell de administración de Exchange. Al crear un grupo de reglas de marcado, debe definir al menos una regla de marcado para el grupo.

Cuando un usuario marca un número de teléfono, la mensajería unificada toma el número y busca una coincidencia en las reglas de marcado. Si encuentra una coincidencia, la mensajería unificada usa la regla de marcado para determinar el número que se debe marcar buscando un número de teléfono o los dígitos que aparecen en la sección **Número marcado** de la regla de marcado. Se marcará el número que aparece en la casilla **Número marcado** de la regla de marcado.

La siguiente tabla muestra un ejemplo de reglas de marcado y de grupos de reglas de marcado. En este ejemplo, Solo-llamadas-locales y Tarifa-baja son los grupos de reglas de marcado que se han creado. El grupo de reglas de marcado Solo-llamadas-locales tiene dos reglas de marcado: 91425\* y 91206\*, y el grupo de reglas de marcado Tarifa-baja también tiene dos reglas de marcado: 91509 \* y 91360 \*.

### Reglas de marcado y grupos de reglas de marcado

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre</th>
<th>Máscara de número</th>
<th>Número marcado</th>
<th>Comentario</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Solo-llamadas-locales</p></td>
<td><p>91425*</p></td>
<td><p>91*</p></td>
<td><p>Llamadas locales</p></td>
</tr>
<tr class="even">
<td><p>Solo-llamadas-locales</p></td>
<td><p>91206*</p></td>
<td><p>91*</p></td>
<td><p>Llamadas locales</p></td>
</tr>
<tr class="odd">
<td><p>Tarifa-baja</p></td>
<td><p>91509*</p></td>
<td><p>9*</p></td>
<td><p>Llamadas provinciales</p></td>
</tr>
<tr class="even">
<td><p>Tarifa-baja</p></td>
<td><p>91360*</p></td>
<td><p>9*</p></td>
<td><p>Llamadas provinciales</p></td>
</tr>
</tbody>
</table>


Por ejemplo, cuando un usuario marca 9-1-425-555-1234, la mensajería unificada marca 4255551234. La mensajería unificada quita todos los caracteres no numéricos (en este ejemplo, los guiones) y aplica la máscara del número de la regla de marcado. En este ejemplo, la mensajería unificada aplica la máscara de número 91\*. Esto significa que la mensajería unificada no marca ni el 9 ni el 1, pero sí el resto de dígitos del número de teléfono que aparece a la derecha del número 1; es decir, todos los números representados por el asterisco (\*).

Puede usar el EAC o el Shell para crear y configurar uno o varios grupos de reglas de marcado nacionales/regionales e internacionales, además de reglas de marcado. Sin embargo, si está creando varios o complejos grupos de reglas de marcado y reglas de marcado, puede usar un archivo de valores separados por comas (.csv) en el Shell. Puede importar o exportar una lista de reglas de marcado y grupos de reglas de marcado.

Para importar una lista de reglas de marcado y grupos de reglas de marcado que haya definido en un archivo .csv, ejecute el cmdlet **Set-UMDialPlan** de la siguiente manera.

    Set-UMDialPlan "MyUMDialPlan" -ConfiguredInCountryOrRegionGroups $(IMPORT-CSV c:\dialrules\InCountryRegion.csv)

Para recuperar una lista de grupos de reglas de marcado que están configurados en un plan de marcado de Mensajería unificada, ejecute el cmdlet **Get-UMDialPlan** de la siguiente manera.

    (Get-UMDialPlan -id "MyUMDialPlan").ConfiguredInCountryOrRegionGroups | EXPORT-CSV C:\incountryorregion.csv

El archivo .csv se debe crear y guardar en el formato correcto. Cada línea del archivo .csv representa una regla de marcado. Sin embargo, cada regla de marcado se configura en el mismo grupo de marcado. Cada regla del archivo tiene cuatro secciones, todas ellas separadas por comas. Estas secciones son nombre, máscara de número, número marcado y comentario. Se requieren todas las secciones y debe escribir la información correcta en cada una de ellas excepto en la sección de comentario. No debe haber espacios entre el texto y la coma de la sección siguiente, así como tampoco líneas en blanco entre las reglas o al final de estas. A continuación se ofrece un ejemplo de un archivo .csv que se puede usar para crear reglas de marcado y grupos de reglas de marcado nacional/regional.

**Name,NumberMask,DialedNumber,Comment**

**Low-rate,91425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9xxxxxxx,9xxxxxxx,Local call**

**Any,91\*,91\*,Open access to in-country/region numbers**

**Long-distance,91408\*,91408\*,long distance**

A continuación se ofrece un ejemplo de un archivo .csv que se puede usar para crear grupos de reglas de marcado internacional y entradas de regla de marcado.

**Name,NumberMask,DialedNumber,Comment**

**International, 901144\*, 901144\*, international call**

**International, 901133\*, 901133\*, international call**

Volver al principio

## Aplicación de grupos de reglas de marcado configurados

Los grupos de reglas de marcado se crean en un plan de marcado de Mensajería unificada. Puede crear grupos de reglas de marcado nacional/regional e internacional mediante el EAC o el cmdlet **Set-UMDialPlan** del Shell. Una vez creados los grupos de reglas de marcado pertinentes en un plan de marcado de mensajería unificada y definidas las reglas de marcado, puede aplicar estos grupos a un plan de marcado de mensajería unificada, a un operador automático de mensajería unificada o a usuarios asociados a una directiva de buzones de correo de mensajería unificada, así como autorizar las llamadas externas en función de cómo accede el usuario al sistema de correo de voz.

Puede aplicar los grupos de reglas de marcado que ha creado en un plan de marcado de Mensajería unificada para lo siguiente:

  - **Mismo plan de marcado**   La configuración se aplicará a todos los usuarios que llamen al número de Outlook Voice Access, pero que no inicien sesión en su buzón de correo. Para aplicar un grupo de reglas de marcado nacional/regional denominado `MyAllowedDialRuleGroup` al mismo plan de marcado, use el cmdlet **Set-UMDialPlan** del Shell de la siguiente manera.
    
        Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Una o varias directivas de buzones de correo de mensajería unificada   **La configuración de una directiva de buzones de correo de mensajería unificada se aplicará a todos los usuarios que estén vinculados a una directiva de buzones de correo de mensajería unificada. La configuración de una directiva de buzones de correo de mensajería unificada se aplica a todos los usuarios que llaman a un número de Outlook Voice Access e inician sesión en su buzón de correo. Para aplicar un grupo de reglas de marcado nacional/regional denominado `MyAllowedDialRuleGroup` a una única directiva de buzones de correo de mensajería unificada, use la página **Autorización de marcado** en la directiva de buzones de correo de mensajería unificada en el EAC, o bien use el cmdlet **Set-UMMailboxPolicy** en el Shell de la siguiente manera.
    
        Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Uno o varios operadores automáticos asociados al plan de marcado de Mensajería unificada**Esto se aplicará a todos los usuarios que llamen a un operador automático de Mensajería unificada. Para aplicar un grupo de reglas de marcado nacional/regional denominado `MyAllowedDialRuleGroup` a un único operador automático de mensajería unificada, use la página **Autorización de marcado** en el operador automático del EAC o el cmdlet **Set-UMAutoAttendant** en el Shell de la siguiente manera.
    
        Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

En la siguiente tabla se resume la forma en la que se aplican los grupos de reglas de marcado en la mensajería unificada.

### Aplicación de reglas de llamada externa

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de autor de llamada</th>
<th>Ámbito</th>
<th>Configuración de llamada externa aplicada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Número de Outlook Voice Access</p></td>
<td><p>El usuario llama al número de Outlook Voice Access de un plan de marcado e inicia sesión en su buzón de correo</p></td>
<td><p>Directiva de buzón de mensajería unificada</p></td>
</tr>
<tr class="even">
<td><p>Autor de llamada anónimo</p></td>
<td><p>El usuario llama a un número de Outlook Voice Access del plan de marcado</p></td>
<td><p>Plan de marcado de mensajería unificada</p></td>
</tr>
<tr class="odd">
<td><p>Autor de llamada anónimo</p></td>
<td><p>El usuario llama a un número de extensión o un número piloto de un operador automático</p></td>
<td><p>Operador automático de mensajería unificada</p></td>
</tr>
<tr class="even">
<td><p>Autor de llamada interno de la organización</p></td>
<td><p>El usuario llama al número Reproducir en teléfono</p></td>
<td><p>Directiva de buzón de mensajería unificada</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Aplicación de reglas de marcado

El proceso de llamada externa tiene lugar cuando:

  - La mensajería unificada realiza una llamada a un número de teléfono externo de un autor de la llamada.

  - La mensajería unificada transfiere la llamada a un operador automático.

  - La mensajería unificada transfiere una llamada a un usuario de su organización.

  - Un usuario habilitado para mensajería unificada usa la característica Reproducir en teléfono.

En cada situación de llamada externa, la mensajería unificada aplicará las reglas de marcado que se han configurado y, a continuación, realizará la llamada relativa al usuario. Sin embargo, según la situación y cómo haya iniciado la llamada el usuario, puede que la mensajería unificada solo aplique algunas de las reglas de marcado al número de teléfono que se está marcando. En otras situaciones de llamada externa, puede que la mensajería unificada aplique al número de teléfono que se está marcando todas las reglas de llamada externa configuradas.

Volver al principio

