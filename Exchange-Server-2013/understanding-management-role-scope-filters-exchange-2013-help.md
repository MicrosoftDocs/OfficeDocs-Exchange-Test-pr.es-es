---
title: 'Descripción de los filtros de ámbito de los roles de administración: Exchange 2013 Help'
TOCTitle: Descripción de los filtros de ámbito de los roles de administración
ms:assetid: 6acc2922-ee9c-41f1-8a0f-10a541e8c273
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298043(v=EXCHG.150)
ms:contentKeyID: 49895686
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de los filtros de ámbito de los roles de administración

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Los filtros de ámbito del rol de administración se pueden usar para definir ámbitos de administración que permitan una gran personalización. Con los filtros de ámbito, se puede crear un ámbito que coincida con la manera en que se segmentan los destinatarios, las bases de datos y los servidores, de manera que los administradores puedan administrar solo aquellos objetos a los que deberían tener acceso. Los filtros de ámbito pueden usar casi cualquier propiedad de objeto de destinatario, base de datos o servidor.

Para usar los filtros de ámbito del rol de administración, debe estar familiarizado con los ámbitos del rol de administración. Para obtener más información sobre los ámbitos de roles de administración, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

Los ámbitos personalizados filtrados de Microsoft Exchange Server 2013 se crean utilizando el cmdlet **New-ManagementScope**. Los dos tipos de ámbitos filtrados, de destinatarios y de configuración (que constan de ámbitos de servidor y base de datos), se dividen en ámbitos normales y exclusivos. En la lista siguiente se muestra qué parámetro del cmdlet **New-ManagementScope** se debe usar para crear cada tipo de ámbito filtrado:

  - **Ámbito filtrado normal de destinatarios**   Para crear este tipo de ámbito filtrado, use el parámetro *RecipientRestrictionFilter*.

  - **Ámbito filtrado exclusivo de destinatarios**   Para crear este tipo de ámbito filtrado, use el parámetro *RecipientRestrictionFilter* con el conmutador *Exclusive*.

  - **Ámbito filtrado normal de configuración basada en servidor**   Para crear este tipo de ámbito filtrado, use el parámetro *ServerRestrictionFilter*.

  - **Ámbito filtrado exclusivo de configuración basada en servidor**   Para crear este tipo de ámbito filtrado, use el parámetro *ServerRestrictionFilter* con el conmutador *Exclusive*.

  - **Ámbito filtrado normal de configuración basada en base de datos**   Para crear este tipo de ámbito filtrado, use el parámetro *DatabaseRestrictionFilter*.

  - **Ámbito filtrado exclusivo de configuración basada en base de datos**   Para crear este tipo de ámbito filtrado, use el parámetro *DatabaseRestrictionFilter* con el conmutador *Exclusive*.

Al crear un ámbito filtrado personalizado, éste intenta hacer coincidir el filtro con los objetos a los que tenga acceso dentro del ámbito de lectura implícito del rol de administración. Si se encuentra un objeto, se lo incluye en los resultados que el filtro devuelve y el ámbito personalizado pone el objeto a disposición del rol de administración. Un filtro no puede devolver resultados que se encuentren fuera del ámbito de lectura implícito del rol de administración.

Si indica un filtro de destinatario mediante el parámetro *RecipientRestrictionFilter*, puede usar el parámetro *RecipientRoot* para indicar la unidad organizativa a la que se debe restringir. Al indicar una OU en el parámetro *RecipientRoot*, el filtro de destinatarios intentará buscar coincidencias entre los destinatarios que residen únicamente en dicha OU, más que entre todos los que están dentro del ámbito implícito de lectura.

Para crear un ámbito filtrado con las propiedades de filtración que se incluyen en este tema, consulte [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

## Sintaxis de filtros

Tanto los filtros de destinatarios como los de configuración usan la misma sintaxis para crear una consulta de filtro. Todas las consultas de filtro deben tener, como mínimo, los componentes siguientes:

  - **Corchete de apertura**   La llave de apertura, {, indica el inicio de la consulta de filtro.

  - **Propiedad a examinar**   La propiedad es el valor de un objeto que se desea probar. Por ejemplo, puede tratarse de la ciudad o el departamento en un objeto de destinatario, un nombre de servidor o de sitio de Active Directory en un objeto de configuración o un nombre de base de datos en un objeto de configuración de base de datos.

  - **Operador de comparación**   El operador de comparación dirige el modo en la consulta analizará el valor indicado en comparación con el valor almacenado en la propiedad. Por ejemplo, los operadores de comparación pueden ser **Eq**, que significa igual que; **Ne**, que significa distinto de; o **Like**, que significa similar a, etcétera. Para obtener una lista completa de los operadores que puede usar en el Shell de administración de Exchange, consulte [Operadores de comparación](https://technet.microsoft.com/es-es/library/bb125229\(v=exchg.150\)).

  - **Valor a comparar**   El valor que se especifica en la consulta de filtro se comparará con el valor almacenado en la propiedad indicada. El valor especificado debe estar escrito entre comillas ("). Si desea especificar una cadena parcial, puede escribirla entre comodines (\*) y usar un operador de comparación que admita comodines, como por ejemplo **Like**. Cualquier cadena que contenga la cadena parcial coincidirá con la consulta de filtro.

  - **Corchete de cierre**   La llave de cierre, }, indica el final de la consulta de filtro.

Los siguientes componentes son opcionales y le permiten crear consultas de filtro más complejas:

  - **Paréntesis**   Al igual que en la matemática, los paréntesis, ( ), en una consulta de filtro, permiten determinar el orden en el que tendrá lugar una operación. Los paréntesis más internos se evalúan primero y la consulta de filtro procede hacia afuera, hasta los paréntesis más externos.

  - **Operadores lógicos**   Los operadores lógicos unen operaciones de comparación entre sí y hacen que la consulta de filtro evalúe la instrucción completa. Por ejemplo, entre los operadores lógicos están **And**, **Or** y **Not**.

Cuando se los coloca juntos, una consulta sencilla tiene este aspecto `{ City -Eq "Vancouver" }`. Este filtro coincide con todo destinatario cuyo valor de la propiedad **City** sea igual a la cadena "Vancouver".

Una consulta más compleja sería `{ ((City -Eq "Vancouver") -And (Department -Eq "Sales")) -Or (Title -Like "*Manager*") }`. La consulta de filtro se evalúa en el orden siguiente:

1.  Se evalúan las propiedades **City** y **Department**. Cada una de ellas está establecida como `True` o `False`, dependiendo del valor almacenado en cada propiedad.

2.  A continuación, se evalúan los resultados de las instrucciones **City** y **Department**. Si ambos son `True`, la instrucción **And** completa se convierte en `True`. Si uno o ambos son `False`, la instrucción **And** completa se convierte en `False`. Se aplica lo siguiente:
    
      - Si la instrucción **And** se evalúa como `True`, la consulta de filtro completa se convierte en `True`, porque el operador **Or** indica que al menos un lado de la consulta debe ser `True`. El objeto se expone a la asignación de roles.
    
      - Si la instrucción **And** es `False`, la consulta de filtro procede a evaluar la propiedad **Title**.

3.  A continuación, se evalúa la propiedad **Title**. Ésta se encuentra establecida como `True` o `False`, según el valor almacenado en la propiedad **Title**. Se aplica lo siguiente:
    
      - Si la propiedad **Title** se evalúa como `True`, la consulta de filtro completa se convierte en `True`, porque el operador **Or** indica que al menos un lado de la consulta debe ser `True`. El objeto se expone a la asignación de roles.
    
      - Si la propiedad **Title** se evalúa como `False`, la consulta de filtro completa se convierte en `False` y el objeto no se expone a la asignación de roles.

En la tabla siguiente se muestra un ejemplo con valores, que indica cuándo la consulta compleja se evaluaría como `True` y cuándo como `False`.

### Consulta compleja

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ciudad</th>
<th>Departamento</th>
<th>Cargo</th>
<th>Resultado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Ventas (True)</p></td>
<td><p>Director ejecutivo (False)</p></td>
<td><p>Es True porque tanto la propiedad <strong>City</strong> como la propiedad <strong>Department</strong> se evalúan como True. La propiedad <strong>Title</strong> no se evalúa porque ya se cumplen las condiciones de la consulta de filtro.</p></td>
</tr>
<tr class="even">
<td><p>Seattle (False)</p></td>
<td><p>Ventas (True)</p></td>
<td><p>Administrador de TI (True)</p></td>
<td><p>Es True porque la propiedad <strong>Title</strong> se evalúa como True. Los resultados de la comparación de las propiedades <strong>City</strong> y <strong>Department</strong> se eliminan, porque la propiedad <strong>Title</strong> se evalúa como True, lo que cumple las condiciones de la consulta de filtro.</p>

> [!NOTE]
> El cargo Administrador de TI coincide con el filtro, dado que se usó un operador de comparación <STRONG>Like</STRONG>, el cual coincide con cadenas parciales cuando se usan comodines (*) en la consulta de filtro.


</td>
</tr>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Marketing (False)</p></td>
<td><p>Escritor (falsa)</p></td>
<td><p>Es False porque las propiedades <strong>City</strong> y <strong>Department</strong> no se evaluaron ambas como True, y la propiedad <strong>Title</strong> tampoco.</p></td>
</tr>
</tbody>
</table>


## Propiedades de destinatarios que se pueden filtrar

Al crear un filtro de destinatarios, es posible usar casi cualquier propiedad del objeto de destinatario. Para obtener una lista de propiedades de destinatarios a las que se puede aplicar un filtro, consulte [Propiedades a las que se puede aplicar un filtro para el parámetro -RecipientFilter](https://technet.microsoft.com/es-es/library/bb738157\(v=exchg.150\)). Si bien en este tema se tratan las propiedades que se pueden usar con el parámetro *RecipientFilter* en otros cmdlets, la mayoría de las propiedades también funcionan con el parámetro*RecipientRestrictionFilter* en el cmdlet **New-ManagementScope**.

## Propiedades de servidor que se pueden filtrar

Cuando cree un ámbito de administración con el parámetro *ServerRestrictionFilter* puede usar las siguientes propiedades de servidor:

  - **CurrentServerRole**

  - **CustomerFeedbackEnabled**

  - **DataPath**

  - **DistinguishedName**

  - **ExchangeLegacyDN**

  - **ExchangeLegacyServerRole**

  - **ExchangeVersion**

  - **Fqdn**

  - **Guid**

  - **InternetWebProxy**

  - **Name**

  - **NetworkAddress**

  - **ObjectCategory**

  - **ObjectClass**

  - **ProductID**

  - **ServerRole**

  - **ServerSite**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

## Propiedades de base de datos que se pueden filtrar

Cuando cree un ámbito de administración con el parámetro *DatabaseRestrictionFilter*, puede usar las siguientes propiedades de base de datos:

  - **AdminDisplayName**

  - **AllowFileRestore**

  - **BackgroundDatabaseMaintenance**

  - **CircularLoggingEnabled**

  - **DatabaseCreated**

  - **DeletedItemRetention**

  - **Description**

  - **DistinguishedName**

  - **EdbFilePath**

  - **EventHistoryRetentionPeriod**

  - **ExchangeLegacyDN**

  - **ExchangeVersion**

  - **Guid**

  - **IssueWarningQuota**

  - **LogFilePrefix**

  - **LogFileSize**

  - **LogFolderPath**

  - **MasterServerOrAvailabilityGroup**

  - **MountAtStartup**

  - **Name**

  - **ObjectCategory**

  - **ObjectClass**

  - **RetainDeletedItemsUntilBackup**

  - **Server**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

