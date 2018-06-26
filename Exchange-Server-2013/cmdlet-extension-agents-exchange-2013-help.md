---
title: 'Agentes de extensión de cmdlet: Exchange 2013 Help'
TOCTitle: Agentes de extensión de cmdlet
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50556731
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agentes de extensión de cmdlet

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Los agentes de extensión de cmdlet son componentes de Microsoft Exchange Server 2013 que invocan los cmdlets de Exchange 2013 cuando se ejecutan los cmdlets. Como su nombre indica, los agentes de extensión de cmdlet asisten en el procesamiento de datos o la realización de acciones adicionales en función de los requisitos de los cmdlets, a fin de extender las capacidades de los cmdlets que los invocan. Los agentes de extensión de cmdlet están disponibles en cualquier rol de servidor.

Los agentes pueden modificar, reemplazar o ampliar la funcionalidad de los cmdlets del Shell de administración de Exchange. Una agente puede proporcionar un valor para un parámetro requerido que no se proporciona en un comando, anular un valor proporcionado por un usuario, realizar otras acciones fuera del flujo de trabajo del cmdlet durante la ejecución del cmdlet y más.

Por ejemplo, el cmdlet **New-Mailbox** acepta el parámetro *Database* que especifica la base de datos de buzones en la que se debe crear un nuevo buzón. En Microsoft Exchange Server 2007, si no se especifica el parámetro *Database* al ejecutar el cmdlet **New-Mailbox**, el comando no se ejecuta correctamente. Sin embargo, en Exchange 2013, el cmdlet **New-Mailbox** invoca al agente de `Mailbox Resources Management` cuando se ejecuta el cmdlet. Si no se especifica el parámetro *Database*, el agente de `Mailbox Resources Management` determina automáticamente una base de datos de buzones adecuada en la que se creará el buzón nuevo e inserta dicho valor en el parámetro *Database*.

Los agentes de extensión de cmdlet solo los puede invocar los cmdlets Exchange 2013 y Microsoft Exchange Server 2010. Los cmdlets Exchange 2007 y los cmdlets de otros productos de Microsoft y de terceros pueden invocar agentes de extensión de cmdlet. Los scripts tampoco pueden invocar a los agentes de extensión de cmdlet directamente. Sin embargo, si los scripts contienen cmdlets de Exchange 2013, esos cmdlets siguen llamando a los agentes de extensión de cmdlet.

¿Está buscando tareas de administración relacionadas con los agentes de extensión de cmdlet? Consulte [Administrar los agentes de extensión de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Prioridad de agente

La prioridad de un agente determina el orden en que se invoca al agente durante la ejecución de un cmdlet. En primer lugar, se invoca a un agente que tiene una prioridad más alta, más cerca de cero. La prioridad de un agente adquiere importancia cuando dos o más agentes intentan establecer el valor de la misma propiedad. Prevalece el agente con la prioridad más alta que intenta establecer el valor de una propiedad y se ignoran todos los intentos subsiguientes para establecer la misma prioridad por parte de agentes con una prioridad inferior. Por ejemplo, si un agente con una prioridad de 3 modifica la propiedad **Name** de un objeto y otro agente con una prioridad de 6 modifica el mismo objeto, se ignora la modificación que realizó el agente con una prioridad de 6.

Si desea utilizar `Scripting agent` para establecer el valor de propiedades que pueden haber establecido otros agentes con prioridad más alta, dispone de las siguientes opciones:

  - Deshabilitar al agente que actualmente establece la propiedad.

  - Establecer `Scripting agent` en una prioridad más alta que el agente existente que desea reemplazar.

  - Conservar las prioridades de los agentes tal cual están y asegurarse de que el script que se ejecuta en `Scripting agent` respete el valor proporcionado por los otros agentes.


> [!WARNING]
> Cambiar la prioridad o reemplazar la funcionalidad de un agente integrado es una operación avanzada. Asegúrese de comprender por completo los cambios que realiza.



Para obtener más información acerca de cómo modificar la prioridad de un agente, consulte [Administrar los agentes de extensión de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Agentes integrados

Exchange 2013 incluye varios agentes que se pueden invocar cuando se ejecuta un cmdlet. La siguiente tabla enumera los agentes y el orden de estos, e indica si los agentes están habilitados de forma predeterminada. No puede agregar ni quitar agentes en o desde un servidor que ejecuta Exchange 2013. Sin embargo, puede usar `Scripting agent` para ejecutar los scripts Windows PowerShell para ampliar la funcionalidad de los cmdlets para usarlo. Para obtener más información acerca de `Scripting agent`, consulte la sección \&quot;Agente de extensión\&quot; más adelante en este tema.

Puede habilitar o deshabilitar la mayoría de agentes o modificar la prioridad de los agentes si desea reemplazar la funcionalidad de un agente específico por la funcionalidad que proporcione en un script personalizado que llame mediante el `Scripting agent`. Sin embargo, algunos agentes no se pueden deshabilitar. Los agentes no se pueden deshabilitar se denominan *agentes del sistemas* y tener sus propiedades *IsSystem* establecidas en `$True`. La siguiente tabla ofrece información acerca de los agentes de extensión del cmdlet Exchange 2013, incluyendo agentes del sistema.

La configuración de los agentes se almacena en el nivel de la organización. Al habilitar o deshabilitar un agente, o al establecer su prioridad, se establece la configuración de dicho agente en todos los servidores de la organización. La excepción es agregar scripts a `Scripting agent`. Debe actualizar los scripts en cada servidor por separado. Para obtener más información acerca de los scripts de configuración para usar con `Scripting agent`, consulte la sección \&quot;Agente de extensión\&quot; más adelante en este tema.


> [!WARNING]
> Si no comprende totalmente las acciones que realiza cada agente y la forma en que interactúan con los cmdlets de Exchange, es posible que la modificación de la prioridad de los agentes, o la habilitación o deshabilitación de los agentes ocasionen efectos no deseados. Antes de modificar la configuración de un agente, asegúrese de comprender perfectamente los cambios y resultados que desea y de comprobar que el script personalizado funcione de la forma esperada.



### Agentes de extensión de cmdlet de Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del agente</th>
<th>Prioridad</th>
<th>Habilitado de forma predeterminada</th>
<th>Agente del sistema</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>True</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>False</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Agente de scripting

Puede usar el agente de extensión de cmdlet `Scripting agent` en Exchange 2013 para insertar su propia lógica de secuencias de comandos en la ejecución de cmdlets de Exchange. Mediante el `Scripting agent`, puede agregar condiciones, reemplazar valores y configurar informes.


> [!WARNING]
> Cuando habilita el agente de extensión de cmdlet de <CODE>Scripting agent</CODE> se invoca al agente cada vez que se ejecuta el cmdlet en un servidor que ejecuta Exchange&nbsp;2013. Esto incluye no solo los cmdlets que usted ejecuta directamente en el Shell de administración de Exchange, sino también cmdlets ejecutados por los servicios de Exchange y el Centro de administración de Exchange (EAC). Le recomendamos encarecidamente que pruebe las secuencias de comandos y cualquier cambio que realice en el archivo de configuración antes de copiar el archivo de configuración actualizado a los servidores de Exchange&nbsp;2013 y habilite el agente de extensión de cmdlet <CODE>Scripting agent</CODE>.



Cada vez que se ejecuta un cmdlet de Exchange el cmdlet invoca al agente de extensión de cmdlet `Scripting agent` del agente de extensión. Cuando se invoca a este agente, el cmdlet verifica si la configuración de alguna de las secuencias de comandos indica que el cmdlet la debe invocar. Si se debe ejecutar una secuencia de comandos para un cmdlet, el cmdlet trata de invocar a cualquier API definida en la secuencia de comandos. Las siguientes API están disponibles y se las invoca en el siguiente orden:

1.  **ProvisionDefaultProperties**   Esta API se puede usar para establecer valores de propiedades de los objetos cuando se los crea. Cuando establece un valor, este valor se envía al cmdlet y el cmdlet establece el valor en la propiedad. Puede completar los valores en las propiedades si el usuario no especificó un valor o puede reemplazar el valor especificado por el usuario. Esta API respeta los valores establecidos por agentes que tienen prioridad mayor. El agente de extensión de cmdlet de `Scripting agent` no sobrescribe los valores establecidos por agentes que tienen prioridad mayor.

2.  **UpdateAffectedIConfigurable**   Esta API se puede usar para establecer valores de propiedades en objetos después de haber finalizado todos los otros procesamientos, pero cuando aún no se invocó a la API `Validate`. Esta API respeta los valores establecidos por agentes que tienen prioridad mayor. El agente de extensión de cmdlet de `Scripting agent` no sobrescribe los valores establecidos por agentes que tienen prioridad mayor.

3.  **Validate**   Esta API se puede usar para validar los valores de las propiedades de un objeto que el cmdlet está a punto de establecer. Se llama a esta API justo antes de que el cmdlet escriba los datos. Puede configurar comprobaciones de validación que permitan o no que el cmdlet funcione correctamente. Si un cmdlet tiene un resultado satisfactorio en las comprobaciones de validación de esta API, el cmdlet puede escribir los datos. Si el cmdlet no tiene un resultado satisfactorio en las comprobaciones de validación, regresa todos los errores definidos por esta API.

4.  **OnComplete**   Esta API se puede usar después de haber finalizado todos los procesamientos del cmdlet. Se puede usar para realizar tareas posteriores al procesamiento, como escribir datos en una base de datos externa.


> [!NOTE]
> No se invoca al agente de extensión de cmdlet del agente de <CODE>Scripting agent</CODE> cuando se ejecutan los cmdlets que tienen el verbo <CODE>Get</CODE>.



## Archivo de configuración del agente de scripting

El archivo de configuración de `Scripting agent` contiene todos los scripts que desea que ejecute el `Scripting agent`. Las secuencias de comandos del archivo de configuración están contenidas dentro de etiquetas XML que definen el comienzo y el fin de la secuencia de comandos y varios parámetros de entrada necesarios para transmitir los datos a la secuencia de comandos. Las secuencias de comandos se escriben mediante la sintaxis de Windows PowerShell. El archivo de configuración es un archivo XML que usa los elementos o atributos de la siguiente tabla.

### Atributos del archivo de configuración del agente de scripting

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Atributo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>No aplicable</p></td>
<td><p>Este elemento contiene todos los scripts que el agente de extensión de cmdlet <code>Scripting agent</code> puede ejecutar. La etiqueta <code>Feature</code> es un elemento secundario de esta etiqueta.</p>
<p>Solo hay una etiqueta <code>Configuration</code> en el archivo de configuración.</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>No aplicable</p></td>
<td><p>Este elemento contiene un conjunto de secuencias de comandos relacionados con una característica. Cada secuencia de comandos, definida en la etiqueta de elemento secundario <code>ApiCall</code>, extiende una parte específica de la canalización de ejecución de cmdlet. Esta etiqueta contiene los atributos <code>Name</code> y <code>Cmdlets</code>.</p>
<p>Puede haber varias etiquetas <code>Feature</code> en la etiqueta <code>Configuration</code>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Este atributo contiene el nombre de la característica. Use este atributo para ayudar a identificar qué característica es extendida por las secuencias de comandos de esta etiqueta.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>Este atributo contiene una lista de los cmdlets Exchange que usa el conjunto de scripts en esta extensión de la característica. Puede especificar varios cmdlets al separar cada uno de ellos con una coma.</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>No aplicable</p></td>
<td><p>Este elemento contiene secuencias de comandos que pueden extender una parte de la canalización de ejecución del cmdlet. Cada secuencia de comandos está definida por el nombre de llamada API de la canalización de ejecución de cmdlet que está extendiendo. Los siguientes son los nombres de API que se pueden extender:</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Este atributo incluye el nombre de la llamada API que está extendiendo la canalización de ejecución de cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>No aplicable</p></td>
<td><p>Este elemento contiene funciones que puede usar cualquier secuencia de comandos del archivo de configuración.</p></td>
</tr>
</tbody>
</table>


Cada servidor Exchange 2013 incluye el archivo ScriptingAgentConfig.xml.sample de la carpeta \<*installation path*\>\\V15\\Bin\\CmdletExtensionAgents. Se le debe cambiar el nombre a este archivo por el nombre ScriptingAgentConfig.xml en cada servidor Exchange 2013 si habilita el agente de extensión de cmdlet del agente de scripting. El archivo de configuración de muestra contiene secuencias de comandos de muestra que puede usar para ayudarle a comprender cómo agregar secuencias de comandos al archivo de configuración.

Después de agregar una secuencia de comandos al archivo de configuración, o después de hacer un cambio en el archivo de configuración, debe actualizar el archivo en cada servidor Exchange 2013 de la organización. Esto se debe hacer para asegurarse de que cada servidor contenga una versión actualizada de las secuencias de comandos que ejecutará el agente de extensión de cmdlet del agente de `Scripting Agent`.

Algunos caracteres que se usan normalmente en las secuencias de comandos también tienen un significado especial en XML. Para usar estos caracteres en la secuencia de comandos, use secuencias de escape. Por ejemplo, los siguientes caracteres usan una secuencia de escape:

  - En lugar de un signo de mayor que ( `>` ), use `&gt;`

  - En lugar de un signo de menor que ( `<` ), use `$lt;`

  - En lugar de una Y comercial ( `&` ), use `&amp;`

## Habilitación del agente de scripting

De forma predeterminada, el agente de extensión de cmdlet `Scripting agent` está deshabilitado. Cuando habilita el `Scripting agent`, el agente está habilitado para toda la organización Exchange 2013. Antes de habilitar el `Scripting agent`, compruebe que se le haya cambiado el nombre al archivo de configuración de`Scripting agent` y que se haya actualizado correctamente con sus secuencias de comandos en cada servidor Exchange 2013. Recibirá un mensaje de error cada vez que un cmdlet se ejecute si no ha cambiado el nombre del archivo de configuración correctamente o copiado un archivo de configuración en este equipo desde otro servidor Exchange 2013.

Para habilitar `Scripting agent`, debe efectuar los pasos siguientes:

1.  Cambie el nombre del archivo ScriptingAgentConfig.xml.sample en **\<ruta de instalación\>\\V15\\Bin\\CmdletExtensionAgents** por el nombre ScriptingAgentConfig.xml en cada servidor Exchange 2013 de la organización.
    

    > [!NOTE]
    > Puede copiar el archivo de configuración de un servidor Exchange&nbsp;2013 a otros servidores Exchange&nbsp;2013. Asegúrese de actualizar el archivo de configuración que desea copiar antes de copiarlo.



2.  Agregue la secuencia de comandos al archivo de configuración que tiene el nombre cambiado en cada servidor Exchange 2013 de la organización.

3.  Habilitar el agente de extensión de cmdlet `Scripting agent`. Para obtener más información sobre cómo habilitar agentes de extensión de cmdlet, consulte [Administrar los agentes de extensión de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Prioridad de agente de scripting

De forma predeterminada, el agente de extensión de cmdlet de `Scripting agent` se ejecuta después de cada dos agentes, a excepción del agente `Scripting agent`. Si desea que una secuencia de comandos que usted creó reemplace a un agente existente, debe deshabilitar al otro agente o cambiar la prioridad de alguno de los agentes para que el agente de extensión de cmdlet de `Scripting agent` se ejecute primero. Para obtener más información acerca de cómo deshabilitar o cambiar la prioridad de los agentes, consulte [Administrar los agentes de extensión de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

