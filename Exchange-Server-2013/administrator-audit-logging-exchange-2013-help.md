---
title: 'Registro de auditoría de administrador: Exchange 2013 Help'
TOCTitle: Registro de auditoría de administrador
ms:assetid: 22b17eb8-d8ee-4599-b202-d6a7928c20d9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335144(v=EXCHG.150)
ms:contentKeyID: 50556751
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registro de auditoría de administrador

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2018-03-05_

Puede usar el registro de auditoría de administrador en Microsoft Exchange Server 2013 para registrar cuando un usuario o un administrador realizan cambios en la organización. Al mantener un registro de los cambios, puede realizar un seguimiento de los cambios de la persona que realizó el cambio, aumentar los registros de cambios con registros detallados de los cambios implementados, cumplir con los requisitos reglamentarios y las solicitudes de detección, y mucho más.

De manera predeterminada, el registro de auditoría está habilitado en las nuevas instalaciones de Exchange 2013.

**Contenido**

What gets audited

Audit logging configuration

Audit logs

Manual audit log entries

Active Directory replication

Admin Audit Log agent

## Qué se audita

Se auditan los cmdlets que se ejecutan directamente en el Shell de administración de Exchange. Además, las operaciones realizadas con el Centro de administración de Exchange (EAC) también se registran, ya que ejecutan cmdlets en segundo plano.

Cmdlets, independientemente de dónde esté ejecute, se auditan si un cmdlet es el cmdlet auditoría lista y uno o más parámetros en ese cmdlet están en la lista de parámetros de auditoría. El registro de auditoría está pensado para mostrar qué acciones se han tomado para modificar objetos de una organización Exchange en lugar de los objetos que se han visto.


> [!IMPORTANT]
> Es posible que no se registre un cmdlet si se produce un error antes de que el cmdlet llame al agente de extensión de cmdlet del registro de auditoría de administrador. Si se produce un error después de llamar al agente de registro de auditoría de administración, el cmdlet se registra junto con el error asociado. Para obtener más información, vea la sección Admin Audit Log Agent más adelante en este tema:<BR>Los cambios realizados con las herramientas de administración de Microsoft Exchange Server 2010 se registran; sin embargo, los cambios realizados con las herramientas de administración de Microsoft Exchange Server 2007, no.<BR>Los cambios en la configuración del registro de auditoría se actualizan cada 60&nbsp;minutos en los equipos que tienen el Shell abierto en el momento de realizar un cambio en la configuración. Si desea aplicar los cambios de inmediato, cierre y vuelva a abrir el Shell en cada equipo.<BR>Un comando puede tardar hasta 15 minutos a partir de su ejecución en aparecer en los resultados de búsqueda del registro de auditoría. Esto se debe a que las entradas del registro de auditoría deben indexarse antes de que puedan realizarse búsquedas en ellas. Si un comando no aparece en el registro de auditoría del administrador, espere unos minutos y vuelva a hacer la búsqueda.



## Configuración del registro de auditoría

De forma predeterminada, si está habilitado el registro de auditoría, una entrada de registro se crea cada vez que se ejecute cualquier cmdlet. Si no desea auditar todos los cmdlets que se ejecutan, puede configurar el registro de auditoría para auditar sólo los cmdlets y parámetros que le interesa. Registro de auditoría se configura con el cmdlet **Set-AdminAuditLogConfig** . Los parámetros que se hace referencia en las secciones siguientes se utilizan con este cmdlet.


> [!IMPORTANT]
> Los cambios realizados en la configuración del registro de auditoría del administrador siempre se registran, independientemente de si el cdmlet <STRONG>Set-AdministratorAuditLog</STRONG> está incluido en la lista de cmdlets que se auditan y de si el registro de auditoría está habilitado o deshabilitado.



Cuando se ejecuta un comando, Exchange inspecciona el cmdlet que se usó. Si el cmdlet que se ejecutó coincide con alguno de los cmdlets proporcionados con el parámetro *AdminAuditLogConfigCmdlets*, Exchange comprueba luego los parámetros especificados en el parámetro *AdminAuditLogConfigParameters*. Si uno o más parámetros de la lista de parámetros coinciden, Exchange registra el cmdlet que se ejecutó en el buzón de correo especificado usando el parámetro *AdminAuditLogMailbox*. En las siguientes secciones, se ofrece más información acerca de los aspectos de la configuración del registro de auditoría.

Para obtener más información sobre la administración de la configuración del registro de auditoría, vea [Administrar el registro de auditoría de administrador](manage-administrator-audit-logging-exchange-2013-help.md).

Volver al principio

## Cmdlets

Puede controlar qué cmdlets se auditarán. Para ello, debe proporcionar una lista de los cmdlets que desea registrar, junto sus parámetros. Cuando configura el registro de auditoría, puede especificar si desea auditar todos cmdlets o puede indicar los cmdlets que desea auditar mediante el parámetro *AdminAuditLogConfigCmdlets*. Puede especificar un nombre de cmdlet completo, como **New-Mailbox**, o puede especificar un nombre de cmdlet parcial y escribir el nombre entre caracteres comodín, por ejemplo, un asterisco (`*`). Por ejemplo, si desea registrar cuándo se ejecuta un cmdlet que contiene la cadena `Transport`, puede especificar el valor `*Transport*`. Puede usar una combinación de nombres de cmdlet completos y parciales al mismo tiempo para adaptar la configuración del registro de auditoría a sus necesidades.

## Parámetros

Además de especificar qué cmdlets desea registrar, también puede indicar que los cmdlets sólo se deberán registrar si se usan determinados parámetros en esos cmdlets. Use el parámetro *AdminAuditLogConfigParameters* para especificar los parámetros que se deben registrar. Al igual que con los cmdlets, puede especificar un nombre de parámetro completo, como `Database`, o un nombre de parámetro parcial y escribir el nombre entre caracteres comodín (`*`), como `*Address*`, o una combinación de ambos.

## Límite de antigüedad del registro de auditoría

De forma predeterminada, el registro de auditoría está configurado para almacenar entradas de registro de auditoría durante 90 días. Después de 90 días, se elimina la entrada del registro de auditoría. Puede cambiar el límite de antigüedad del registro de auditoría mediante el parámetro *AdminAuditLogAgeLimit*. Puede especificar el número de días, horas, minutos y segundos que se deben conservar en las entradas del registro de auditoría. Para especificar un valor, use el formato `dd.hh:mm:ss`, donde se aplica lo siguiente:

  - **dd**   El número de días que se conservará la entrada del registro de auditoría.

  - **hh**   El número de horas que se conservará la entrada del registro de auditoría.

  - **mm**   El número de minutos que se conservará la entrada del registro de auditoría.

  - **ss**   El número de segundos que se conservará la entrada del registro de auditoría.

Debe especificar varios años utilizando el campo `dd`. Por ejemplo, 365 días equivale a un año; 730 días equivale a dos años; 913 días equivale a dos años y seis meses. Por ejemplo, para definir el límite de antigüedad del registro de auditoría en dos años y seis meses, use la sintaxis `913.00:00:00`.


> [!WARNING]
> Puede definir el límite de antigüedad del registro de auditoría en un valor menor que el límite de antigüedad actual. Para ello, se eliminan todas las entradas del registro cuya antigüedad supera el nuevo límite de antigüedad.<BR>Si define el límite de antigüedad en 0, Exchange&nbsp;elimina todas las entradas del registro de auditoría.<BR>Se recomienda otorgar permiso para configurar el límite de antigüedad del registro de auditoría solamente a los usuarios de mayor confianza.



## Registro detallado

De manera predeterminada, el registro de auditoría de administrador registra solo el nombre del cmdlet, sus parámetros (y los valores especificados), el objeto que se modificó y quién, cuándo y en qué servidor se ejecutó el cmdlet. El registro de auditoría de administrador no registra qué propiedades se modificaron en el objeto. Si desea que el registro de auditoría también incluya las propiedades del objeto que se modificaron, puede habilitar el registro detallado. Para hacerlo, configure el parámetro *LogLevel* en `Verbose`. Cuando habilita el registro detallado, además de la información registrada de manera predeterminada, se incluyen en el registro de auditoría las propiedades modificadas en un objeto, incluidos sus valores antiguos y nuevos.

## Cmdlets de prueba

Los cmdlets que comienzan con el verbo **Test** no se registran de forma predeterminada. Puede indicar que los cmdlets **Test** se registren configurando el parámetro *TestCmdletLoggingEnabled* en `$true`. Si bien puede habilitar el registro de los cmdlets de prueba, se recomienda hacerlo solamente durante períodos breves, dado que los cmdlets de prueba pueden producir una gran cantidad de información.

## Registros de auditoría

Cada vez que se registra un cmdlet, se crea una entrada en el registro de auditoría. Los registros de auditoría se almacenan en un buzón de correo oculto de arbitraje dedicado, al que solamente se puede obtener acceso mediante el EAC o los cmdlets **Search-AdminAuditLog** o **New-AdminAuditLogSearch**. No se puede abrir mediante Microsoft Outlook Web App o Microsoft Outlook. Las siguientes secciones proporcionan información sobre los siguientes aspectos:

  - Qué se incluye en los registros

  - Informes disponibles en la página **de auditoría** del EAC

  - Cmdlets de búsqueda de registros de auditoría

## Contenido del registro de auditoría

Todas las entradas del registro de auditoría contienen la información que se describe en la siguiente tabla. El registro de auditoría contiene una o varias entradas de registro de auditoría. La cantidad de entradas del registro de auditoría está controlada por el límite de antigüedad del registro de auditoría especificado con el cmdlet **Set-AdminAuditLogConfig**. Se eliminan todas las entradas del registro de auditoría que superan el límite de antigüedad.

### Campos de entrada del registro de auditoría

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Campo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>RunspaceId</code></p></td>
<td><p>Exchange utiliza este campo de manera interna.</p></td>
</tr>
<tr class="even">
<td><p><code>ObjectModified</code></p></td>
<td><p>Este campo contiene el objeto modificado por el cmdlet especificado en el campo <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletName</code></p></td>
<td><p>Este campo contiene en nombre del cmdlet ejecutado por el usuario en el campo <code>Caller</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletParameters</code></p></td>
<td><p>Este campo contiene los parámetros especificados cuando se ejecutó el cmdlet en el campo <code>CmdletName</code>. Además, en este campo se almacena el valor especificado con el parámetro (si corresponde), aunque no es visible en los resultados predeterminados. Para obtener más información acerca de cómo tener acceso a información adicional en este campo, vea <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">Buscar los informes de cambios del grupo de roles o auditorías de administrador</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p>Este campo contiene las propiedades modificadas en el objeto en el campo <code>ObjectModified</code>. Además, en este campo se almacenan el valor anterior de la propiedad y el nuevo valor almacenado, aunque no están visibles en los resultados predeterminados. Para obtener más información acerca de cómo tener acceso a información adicional en este campo, vea <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">Buscar los informes de cambios del grupo de roles o auditorías de administrador</a>.</p>

> [!IMPORTANT]
> Este campo solo está completo si el parámetro <EM>LogLevel</EM> en el cmdlet <STRONG>Set-AdminAuditLogConfig</STRONG> está configurado en <CODE>Verbose</CODE>.


</td>
</tr>
<tr class="even">
<td><p><code>Caller</code></p></td>
<td><p>Este campo contiene la cuenta de usuario del usuario que ejecutó el cmdlet en el campo <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Succeeded</code></p></td>
<td><p>Este campo especifica si el cmdlet del campo <code>CmdletName</code> se ejecutó correctamente. El valor es <code>True</code> o <code>False</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Error</code></p></td>
<td><p>Este campo contiene el mensaje de error generado si el cmdlet del campo <code>CmdletName</code> no se pudo completar correctamente.</p></td>
</tr>
<tr class="odd">
<td><p><code>RunDate</code></p></td>
<td><p>Este campo contiene la fecha y la hora en las que se ejecutó el cmdlet en el campo <code>CmdletName</code>. La fecha y la hora se almacenan en formato de hora universal coordinada (UTC).</p></td>
</tr>
<tr class="even">
<td><p><code>OriginatingServer</code></p></td>
<td><p>Este campo indica el servidor en el cual se ejecutó el cmdlet especificado en el campo <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Exchange utiliza este campo de manera interna.</p></td>
</tr>
<tr class="even">
<td><p><code>IsValid</code></p></td>
<td><p>Exchange utiliza este campo de manera interna.</p></td>
</tr>
<tr class="odd">
<td><p><code>ObjectState</code></p></td>
<td><p>Exchange utiliza este campo de manera interna.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Informes de auditoría del EAC

La página **de auditoría** del EAC tiene diversos informes que proporcionan información sobre varios tipos de cambios de configuración administrativa y de cumplimiento. Los informes siguientes proporcionan información acerca de los cambios de configuración en la organización:

  - **Informe de grupo de roles de administrador**   Este informe le permite buscar cambios de grupos de roles de administración dentro de un período especificado. Los resultados que se devuelven muestran los grupos de funciones que han sido modificados, quien los modificó y cuándo, y qué cambios se realizaron. Se puede devolver un máximo de 3000 entradas. Si es posible que su búsqueda devuelva más de 3000 entradas, use el informe de **Registro de auditoría de administrador** o el cmdlet **Search-AdminAuditLog**.

  - **Registro de auditoría de administrador**   Este informe permite exportar a un archivo XML las entradas del registro de auditoría registradas en un período de tiempo especificado y, a continuación, enviar el archivo por correo electrónico al destinatario que especifique. Para obtener más información acerca del contenido del archivo XML, vea [Estructura del registro de auditoría de administrador](administrator-audit-log-structure-exchange-2013-help.md).

Para obtener información acerca de cómo usar estos informes, vea [Buscar los informes de cambios del grupo de roles o auditorías de administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Para obtener información sobre otros informes incluidos en la página de **auditoría**, vea [Informes de auditoría de Exchange](exchange-auditing-reports-exchange-2013-help.md).

## Cmdlet Search-AdminAuditLog

Cuando ejecuta el cmdlet **Search-AdminAuditLog**, se devuelven todas las entradas del registro de auditoría que coinciden con el criterio de búsqueda especificado. Puede especificar los siguientes criterios de búsqueda:

  - **Cmdlets**   Especifica los cmdlets que desea buscar en el registro de auditoría de administrador.

  - **Parámetros**   Especifica los parámetros, separados por comas, que desea buscar en el registro de auditoría de administrador. Solo puede buscar parámetros si especifica un cmdlet para buscar.

  - **Fecha de finalización**   Reduce el ámbito de los resultados del registro de auditoría de administrador a las entradas de registro correspondientes a la fecha especificada o a las fechas anteriores a esta.

  - **Fecha de inicio**   Reduce el ámbito de los resultados del registro de auditoría de administrador a las entradas de registro correspondientes a la fecha especificada o a las fechas posteriores a esta.

  - **Id. de objeto**   Especifica que solamente se devuelvan las entradas del registro de auditoría de administrador que contengan los objetos modificados especificados

  - **Id. de usuario**   Especifica que solamente se devuelvan las entradas del registro de auditoría de administrador que contengan el identificador especificado del usuario que ejecutó el cmdlet.

  - **Finalización satisfactoria**   Especifica si solamente se deben devolver las entradas de registro de auditoría de administrador que indicaron acierto o error.

Todas las entradas del registro de auditoría contienen la información que se describe en la tabla de Audit Log Contents. De forma predeterminada, solamente se devuelven las primeras 1000 entradas del registro que coinciden con los criterios especificados. Sin embargo, puede invalidar esta configuración predeterminada y habilitar la devolución de una mayor o menor cantidad de entradas con el parámetro *ResultSize*. Puede especificar el valor de `Unlimited` con el parámetro *ResultSize* para que se devuelvan todas las entradas de registro que coincidan con los criterios especificados.

Para obtener más información acerca de cómo usar el cmdlet **Search-AdminAuditLog**, vea [Buscar los informes de cambios del grupo de roles o auditorías de administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

## Cmdlet New-AdminAuditLogSearch

El cmdlet **New-AdminAuditLogSearch** busca el registro de auditoría al igual que el cmdlet **Search-AdminAuditLog**. Sin embargo, en lugar de mostrar los resultados de la búsqueda del registro de auditoría en el Shell, el cmdlet **New-AdminAuditLogSearch** realiza la búsqueda y, a continuación, envía los resultados de la búsqueda por correo electrónico al destinatario que usted especifica. Los resultados se incluyen como datos adjuntos XML en el mensaje de correo electrónico.

Puede usar el mismo criterio de búsqueda con el cmdlet **New-AdminAuditLogSearch** que usa con el cdmlet **Search-AdminAuditLog**. Para ver la lista de criterios de búsqueda, vea Search-AdminAuditLog Cmdlet.

Después de ejecutar el cmdlet **New-AdminAuditLogSearch**, Exchange puede demorar hasta 15 minutos para entregar el informe al destinatario especificado. El informe adjunto en un archivo XML puede tener un máximo de 10 megabytes (MB). El archivo XML contiene la misma información que se describe en la tabla de Audit Log Contents. Para obtener más información acerca de la estructura del archivo XML, vea [Estructura del registro de auditoría de administrador](administrator-audit-log-structure-exchange-2013-help.md).


> [!NOTE]
> Outlook Web App no permite abrir datos adjuntos en formato XML de forma predeterminada. Puede configurar Exchange para poder ver datos XML adjuntos mediante Outlook Web App o puede recurrir a otro cliente de correo electrónico, como Microsoft Outlook, para ver los datos adjuntos. Para saber cómo configurar Outlook Web App para poder ver un archivo adjunto en formato XML, consulte <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Ver o configurar los directorios virtuales de aplicación web de Outlook</A>.



Para obtener más información acerca de cómo usar el cmdlet **New-AdminAuditLogSearch**, consulte [Buscar los informes de cambios del grupo de roles o auditorías de administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Volver al principio

## Entradas manuales del registro de auditoría

Además de registrar los cmdlets Exchange cuando se ejecutan, Exchange 2013 permite escribir manualmente las entradas del registro en el registro de auditoría. Exchange 2013 lo admite mediante el cmdlet **Write-AdminAuditLog**. A continuación, se muestran algunas de las situaciones en las que es posible que desee agregar una entrada registro manualmente:

  - Entrada y salida de script personalizado

  - Información de control de cambios

  - Hora de inicio y finalización de mantenimiento

Con el cmdlet **Write-AdminAuditLog**, especifica una cadena de texto para incluir en el registro de auditoría con el parámetro *Comment*. El parámetro *Comment* acepta una cadena alfanumérica de hasta 500 caracteres. Toda la información capturada cuando se registra un cmdlet de Exchange está incluida en la entrada de registro de auditoría manual junto con la cadena de comentario. Para obtener una descripción de cada campo incluido en el registro de auditoría, vea la tabla de Audit Log Contents.

Puede recuperar entradas del registro de auditoría de la misma manera que recupera otras entradas del Registro, mediante la página de **auditoría** del EAC o mediante los cmdlets **Search-AdminAuditLog** o **New-AdminAuditLogSearch**.

Para ver el contenido del parámetro *Comment* en el cdmlet **Write-AdminAuditLog** en una entrada manual del registro de auditoría, vea [Buscar los informes de cambios del grupo de roles o auditorías de administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

## Replicación de Active Directory

El registro de auditoría de administrador usa la replicación de Active Directory para replicar las opciones de configuración que se especifiquen en los controladores de dominio de la organización. En función de las opciones de replicación, es posible que los cambios que realice no se apliquen de inmediato a todos los servidores que ejecutan Exchange 2013 o Exchange 2010 en la organización.

## Agente del registro de auditoría de administrador

El agente de extensión de cmdlet integrado realiza el registro de auditoría de administrador de las operaciones de cmdlet en Exchange 2013. Este agente lee la configuración del registro de auditoría y, luego, realiza una evaluación de cada cmdlet que se ejecuta en la organización. Si los criterios especificados en la configuración del registro de auditoría coinciden con el cmdlet que se está ejecutando, el agente genera un registro de auditoría.

El agente del registro de auditoría de administrador está habilitado de forma predeterminada. Esta configuración es necesaria para que funcione el registro de auditoría. No se puede deshabilitar y no se puede cambiar su prioridad. Para obtener más información acerca de los agentes de extensión del cmdlet, vea [Agentes de extensión de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

