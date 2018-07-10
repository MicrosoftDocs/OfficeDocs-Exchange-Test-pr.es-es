---
title: 'Atributos personalizados: Exchange 2013 Help'
TOCTitle: Atributos personalizados
ms:assetid: 2b043878-0b34-4563-a9c2-28a9efa7447e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423541(v=EXCHG.150)
ms:contentKeyID: 49895533
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Atributos personalizados

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-17_

Microsoft Exchange Server 2013 incluye 15 atributos de extensión. Puede usar estos atributos para agregar información acerca de un destinatario, como un Id. de empleado, una unidad organizativa (UO) u otro valor personalizado para el que no hay un atributo existente. Estos atributos personalizados se etiquetan en Active Directory como **ms-Exch-Extension-Attribute1** a **ms-Exch-Extension-Attribute15**. En el Shell de administración de Exchange, los parámetros correspondientes son *CustomAttribute1* a *CustomAttribute15*. Ningún componente de Exchange usa estos atributos. Se pueden usar para almacenar datos de Active Directory sin necesidad de extender el esquema de Active Directory.

En Exchange Server 2003 y versiones anteriores, si deseaba almacenar esta información en Active Directory, debía crear un atributo mediante la extensión del esquema de Active Directory. La extensión del esquema requiere la planeación, la obtención de identificadores de objetos (OID) para los atributos nuevos y la comprobación del proceso de extensión en un entorno de prueba antes de implementarlo en un entorno de producción. En Exchange 2013, las extensiones del esquema no se pueden usar en filtros de destinatarios usados por listas de direcciones, directivas de direcciones de correo electrónico y grupos de distribución dinámicos.

**Contenido**

Ventajas de los atributos personalizados

Ejemplos de atributos personalizados

Ejemplo de atributo personalizado con el parámetro "ConditionalCustomAttributes"

Ejemplo de atributo personalizado utilizando el parámetro "ExtensionCustomAttributes"

## Ventajas de los atributos personalizados

Entre las ventajas de usar atributos personalizados se incluyen:

  - Se evita la extensión del esquema de Active Directory.

  - Los atributos se crean mediante el programa de instalación de Exchange.

  - Puede usar el Centro de administración de Exchange (EAC) o el Shell de administración de Exchange para administrar los atributos. No es necesario crear controles personalizados ni escribir scripts para completar y mostrar estos atributos.

  - Los atributos son propiedades que se pueden filtrar que pueden usarse en el parámetro *Filter* con los cmdlets de destinatario tales como **Get-Mailbox**. También se pueden usar en el EAC y el Shell para crear filtros para directivas de direcciones de correo electrónico, listas de direcciones y grupos de distribución dinámicos.

## Atributos personalizados con varios valores

En Exchange 2010 Service Pack 2 (SP2), se pueden agregar cinco atributos personalizados de varios valores a Exchange para permitirle almacenar información adicional de destinatarios de correo si los atributos personalizados tradicionales no satisficieron sus necesidades. Los parámetros de *ExtensionCustomAttribute1* a *ExtensionCustomAttribute5* pueden retener 1.300 valores cada uno. Puede especificar varios valores en forma de lista delimitada por comas. Los siguientes cmdlets son compatibles con estos nuevos parámetros:

  - [Set-DistributionGroup](https://technet.microsoft.com/es-es/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/es-es/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/es-es/library/aa995950\(v=exchg.150\))

  - [Set-MailPublicFolder](https://technet.microsoft.com/es-es/library/bb123707\(v=exchg.150\))

  - [Set-RemoteMailbox](https://technet.microsoft.com/es-es/library/ff607302\(v=exchg.150\))

Para obtener más información acerca de las propiedades con varios valores, consulte [Modificación de propiedades multivalor](modifying-multivalued-properties-exchange-2013-help.md).

## Ejemplos de atributos personalizados

En muchas implementaciones de Exchange, la creación de una directiva de direcciones de correo electrónico para todos los destinatarios en una OU es un caso habitual. La OU no es una propiedad que se pueda filtrar que pueda usarse en el parámetro *RecipientFilter* de una directiva de direcciones de correo electrónico o una lista de direcciones.


> [!NOTE]
> Los grupos de distribución dinámicos tienen un parámetro adicional que puede usarse para restringirlo a los destinatarios de una OU o un contenedor en particular.



Si los destinatarios de esa OU no comparten propiedades comunes por las que pueda aplicar el filtro, como departamento o ubicación, puede completar uno de los atributos personalizados con un valor común, tal como se muestra en este ejemplo.

    Get-Mailbox -OrganizationalUnit Sales | Set-Mailbox CustomAttribute1 "SalesOU"

Ahora, puede crear una directiva de direcciones de correo electrónico para todos los destinatarios que tengan la propiedad *CustomAttribute1* que sea igual a SalesOU, como se muestra en este ejemplo.

    New-EmailAddressPolicy -Name "Sales" -RecipientFilter { CustomAttribute1 -eq "SalesOU"} -EnabledEmailAddressTemplates "SMTP:%s%2g@sales.contoso.com"

## Ejemplo de atributo personalizado con el parámetro "ConditionalCustomAttributes"

Al crear grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones, no es necesario usar el parámetro *RecipeintFilter* para especificar los atributos personalizados. En su lugar, puede usar los parámetros *ConditionalCustomAttribute1* a *ConditionalCustomAttribute15*.

Este parámetro crea un grupo de distribución dinámico basado en los destinatarios cuyo *CustomAttribute1* está establecido en "SalesOU".

    New-DynamicDistributionGroup -Name "Sales Users and Contacts" -IncludedRecipients "MailboxUsers,MailContacts" -ConditionalCustomAttribute1 "SalesOU"


> [!NOTE]
> Debe usar el parámetro <EM>IncludedRecipients</EM> si usa un parámetro <EM>Conditional</EM>. Además, no se pueden usar los parámetros <EM>Conditional</EM> si usa el parámetro <EM>RecipientFilter</EM>. Si desea incluir filtros adicionales para crear grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones, debe usar el parámetro <EM>RecipientFilter</EM>.



## Ejemplo de atributo personalizado utilizando el parámetro "ExtensionCustomAttributes"

En este ejemplo, el buzón de correo de Kweku tendrá *ExtensionCustomAttribute1* actualizado para reflejar que se ha inscrito en las siguientes clases educativas: MATH307, ECON202 y ENGL300.

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 MATH307,ECON202,ENGL300

A continuación, se crea un grupo de distribución dinámico para todos los estudiantes inscritos en MATH307 con el parámetro*RecipientFilter* donde *ExtensionCustomAttribute1* es igual a MATH307. Cuando use los parámetros *ExtentionCustomAttributes*, puede usar el operador `-eq` en lugar del operador `-like`.

    New-DynamicDistributionGroup -Name Students_MATH307 -RecipientFilter {ExtensionCustomAttribute1 -eq "MATH307"}

En este ejemplo, los valores de Kweku *ExtensionCustomAttribute1* se actualizan para reflejar que ha agregado la clase ENGL210 y eliminado la clase ECON202.

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 @{Add="ENGL210"; Remove="ECON202"}

