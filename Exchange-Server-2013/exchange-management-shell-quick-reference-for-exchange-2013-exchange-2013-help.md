---
title: 'Guía de referencia rápida del Shell de administración de Exchange para Exchange 2013: Exchange 2013 Help'
TOCTitle: Guía de referencia rápida del Shell de administración de Exchange para Exchange 2013
ms:assetid: 3ea4a105-a93c-48ba-96ce-6170125354e1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ619302(v=EXCHG.150)
ms:contentKeyID: 49116160
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Guía de referencia rápida del Shell de administración de Exchange para Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Este tema describe los cmdlets que se usan con más frecuencia en las versiones RTM y posteriores de Microsoft Exchange Server 2013 y se ofrecen ejemplos de uso.


> [!NOTE]
> Próximamente se añadirá más contenido sobre otras áreas de Exchange&nbsp;2013.



Para obtener más información acerca del Shell de administración de Exchange en Exchange 2013y de los cmdlets disponibles, consulte los temas siguientes:

  - [Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\))

  - [Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

## ¿Sobre qué desea obtener información?

## Acciones de cmdlet comunes

Los verbos siguientes son admitidos por la mayor parte de los cmdlets y están asociados a una acción específica.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>New</p></td>
<td><p>El verbo New crea una instancia de algo como, por ejemplo, una configuración nueva, una base de datos nueva o un conector SMTP nuevo.</p></td>
</tr>
<tr class="even">
<td><p>Remove</p></td>
<td><p>El verbo Remove quita una instancia de algo como, por ejemplo, un buzón o una regla de transporte.</p>
<p>Todos los cmdlets Remove admiten los parámetros <em>WhatIf</em> y <em>Confirm</em>. Para obtener más información acerca de estos parámetros, consulte Important Parameters.</p></td>
</tr>
<tr class="odd">
<td><p>Enable</p></td>
<td><p>El verbo Enable habilita una configuración o el correo de un destinatario.</p></td>
</tr>
<tr class="even">
<td><p>Disable</p></td>
<td><p>El verbo Disable deshabilita una configuración habilitada o deshabilita el correo de un destinatario.</p>
<p>Todas las tareas Disable admiten los parámetros <em>WhatIf</em> y <em>Confirm</em>. Para obtener más información acerca de estos parámetros, consulte Important Parameters.</p></td>
</tr>
<tr class="odd">
<td><p>Set</p></td>
<td><p>El verbo Set modifica la configuración específica de un objeto como, por ejemplo, el alias de un contacto o la retención de un elemento eliminado de una base de datos de buzones.</p></td>
</tr>
<tr class="even">
<td><p>Get</p></td>
<td><p>El verbo Get consulta un objeto específico o un subconjunto de un tipo de objetos como, por ejemplo, un buzón específico, los usuarios de todos los buzones o los usuarios de buzones de un dominio.</p></td>
</tr>
</tbody>
</table>


## Parámetros importantes

Los parámetros siguientes ayudan a controlar cómo se ejecutan los comandos e indican exactamente qué hará un comando antes de que afecte a los datos.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Identity</p></td>
<td><p>El parámetro <em>Identity</em> identifica el objeto único de la tarea. Se usa normalmente con los cmdlets Enable, Disable, Remove, Set y Get. <em>Identity</em> es también un parámetro de posición, lo cual significa que no tiene que especificar <em>Identity</em> al indicar el valor del parámetro en la línea de comandos.</p>
<p>Por ejemplo, <em>Get-Mailbox -Identity usuario1</em> consulta el buzón de <em>usuario1</em>. <em>Get-Mailbox usuario1</em> es equivalente a <em>Get-Mailbox -Identity usuario1</em>.</p></td>
</tr>
<tr class="even">
<td><p>WhatIf</p></td>
<td><p>El parámetro <em>WhatIf</em> indica al cmdlet que simule las acciones que llevaría a cabo en el objeto. Mediante el uso del parámetro <em>WhatIf</em>, puede ver los cambios que se producirían sin tener que aplicarlos realmente. El valor predeterminado es <em>$true</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Confirm</p></td>
<td><p>El parámetro <em>Confirm</em> hace que el cmdlet ponga en pausa el procesamiento y requiere que el administrador reconozca qué hará el cmdlet antes de seguir con el procesamiento. El valor predeterminado es <em>$true</em>.</p></td>
</tr>
<tr class="even">
<td><p>Validate</p></td>
<td><p>El parámetro <em>Validate</em> hace que el cmdlet compruebe que se cumplen todos los requisitos para ejecutar la operación y garantizar que ésta finalice correctamente.</p></td>
</tr>
</tbody>
</table>


## Sugerencias y trucos

Los comandos siguientes están asociados con varias tareas que puede usar para la administración de Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-Command</p></td>
<td><p>Este cmdlet recupera todas las tareas que se pueden ejecutar en Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p>Get-Command *<em>palabra clave</em>*</p></td>
<td><p>Este cmdlet recupera las tareas que tienen <em>palabra clave</em> en el cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p>Get-<em>tarea</em> | Get-Member</p></td>
<td><p>Este cmdlet recupera todas las propiedades y métodos de <em>tarea</em>.</p></td>
</tr>
<tr class="even">
<td><p>Get-<em>tarea</em> | Format-List</p></td>
<td><p>Este cmdlet muestra el resultado de la consulta en una lista de formato. Puede canalizar el resultado de cualquier cmdlet Get a Format-List para visualizar todo el conjunto de propiedades que existen en el objeto devuelto por dicho comando, o puede especificar determinadas propiedades que desee visualizar, separadas por comas, como en el ejemplo siguiente: <em>Get-Mailbox *john* | Format-List alias,*quota</em></p></td>
</tr>
<tr class="odd">
<td><p>Help <em>tarea</em></p></td>
<td><p>Este cmdlet recupera información de ayuda del Shell de administración de Exchange para cualquier tarea de Exchange 2013, como en el ejemplo siguiente: <em>Help Get-Mailbox</em></p></td>
</tr>
<tr class="even">
<td><p>Get-<em>tarea</em> | Format-List &gt; <em>archivo.txt</em></p></td>
<td><p>Este cmdlet exporta el resultado de <em>tarea</em> a un archivo de texto: <em>archivo.txt</em></p></td>
</tr>
</tbody>
</table>


## Permisos


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-RoleGroupMember &quot;<em>Administración de la organización</em>&quot;</p></td>
<td><p>Este comando recupera los miembros del grupo de administración de roles denominado <em>Administración de la organización</em>.</p></td>
</tr>
<tr class="even">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Creación de destinatarios de correo</em>&quot; -GetEffectiveUsers</p></td>
<td><p>Este ejemplo muestra una lista de todos los usuarios a los que el rol de administración <em>Creación de destinatarios de correo</em> ha concedido permiso. Esto incluye usuarios que pertenecen a grupos de roles o grupos de seguridad universales (USG) que tienen el rol Creación de destinatarios de correo. No se incluye a los usuarios que pertenecen a grupos de roles vinculados en otro bosque.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -RoleAssignee <em>Administrador</em> | Get-ManagementRole | Get-ManagementRoleEntry</p></td>
<td><p>Este comando recupera una lista de cmdlets que el usuario <em>Administrador</em> puede ejecutar.</p></td>
</tr>
<tr class="even">
<td><p>ForEach ($RoleEntry in Get-ManagementRoleEntry *\<em>Remove-Mailbox</em> -parameters Identity) {Get-ManagementRoleAssignment -Role $RoleEntry.Role -GetEffectiveUsers -Delegating $False | Where-Object {$_.EffectiveUserName -Ne &quot;All Group Members&quot;} | FL Role, EffectiveUserName, AssignmentChain}</p></td>
<td><p>En este ejemplo se recupera una lista de todos los usuarios que pueden ejecutar el cmdlet <em>Remove-Mailbox</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -WritableRecipient <em>kima</em> -GetEffectiveUsers | FT RoleAssigneeName, EffectiveUserName, Role, AssignmentChain</p></td>
<td><p>En este ejemplo se recupera una lista de todos los usuarios que pueden modificar el buzón de <em>kima</em>.</p></td>
</tr>
<tr class="even">
<td><p>New-ManagementScope &quot;<em>Usuarios de Seattle</em>&quot; -RecipientRestrictionFilter { <em>City</em> -Eq &quot;<em>Seattle</em>&quot; }</p>
<p>New-RoleGroup &quot;<em>Administradores de Seattle</em>&quot; -Roles &quot;<em>Destinatarios de correo</em>&quot;, &quot;<em>Creación de destinatarios de correo</em>&quot;, &quot;<em>Importar o exportar buzones</em>&quot;, -CustomRecipientWriteScope &quot;<em>Usuarios de Seattle</em>&quot;</p></td>
<td><p>Este comando crea un nuevo ámbito de administración y grupo de roles de administración para permitir que los miembros del grupo de roles administren los destinatarios de Seattle.</p>
<p>En primer lugar, se crea el ámbito de administración <em>Usuarios de Seattle</em>, que incluye solo a los destinatarios que tienen <em>Seattle</em> en el atributo <em>Ciudad</em> de su objeto de usuario.</p>
<p>A continuación se crea un grupo nuevo llamado <em>Administradores de Seattle</em> y se asignan los roles <em>Destinatarios de correo</em>, <em>Creación de destinatarios de correo</em> e <em>Importar o exportar buzones</em>. El grupo de roles se configura de modo que sus miembros solo puedan administrar los usuarios que coincidan con el ámbito del filtro de destinatarios <em>Usuarios de Seattle</em>.</p></td>
</tr>
<tr class="odd">
<td><p>New-ManagementScope &quot;<em>Servidores de Vancouver</em>&quot; -ServerRestrictionFilter { <em>ServerSite</em> -Eq &quot;<em>Vancouver</em>&quot; }</p>
<p>$RoleGroup = Get-RoleGroup &quot;<em>Administración de servidores</em>&quot;</p>
<p>New-RoleGroup &quot;<em>Administración de servidores de Vancouver</em>&quot; -Roles $RoleGroup.Roles -CustomConfigWriteScope &quot;<em>Servidores de Vancouver</em>&quot;</p></td>
<td><p>Este comando crea un nuevo ámbito de administración y copia un grupo de roles existente para permitir que los miembros del nuevo grupo de roles administre solo los servidores del sitio Active Directory Vancouver.</p>
<p>En primer lugar, se crea el ámbito de administración <em>Servidores de Vancouver</em>, que incluye solo los servidores situados en el sitio Active Directory <em>Vancouver</em>. El sitio Active Directory se almacena en el atributo <em>ServerSite</em> en los objetos de servidor.</p>
<p>A continuación se crea un nuevo grupo de roles llamado <em>Administración de servidores de Vancouver</em>, que es una copia del grupo de roles <em>Administración de servidores</em>. El nuevo grupo de roles se configura de modo que sus miembros solo puedan administrar los servidores que coincidan con el ámbito del filtro de configuración <em>Servidores de Vancouver</em>.</p></td>
</tr>
<tr class="even">
<td><p>Add-RoleGroupMember &quot;<em>Administración de la organización</em>&quot; -Member <em>davids</em></p></td>
<td><p>Este comando agrega el usuario <em>davids</em> al grupo de roles <em>Administración de la organización</em>.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Creación de destinatarios de correo</em>&quot; -RoleAssignee &quot;<em>Administradores de Seattle</em>&quot; | Remove-ManagementRoleAssignment</p></td>
<td><p>Este comando elimina el rol <em>Creación de destinatarios de correo</em> del grupo de roles <em>Administradores de Seattle</em>. Este comando es útil porque no es necesario saber el nombre de la asignación de roles de administración que asigna el rol al grupo de roles.</p></td>
</tr>
</tbody>
</table>


## Shell remoto


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos</p>
<p>Import-PSSession $Session</p></td>
<td><p>Estos comandos abren una sesión remota del Shell entre un equipo local unido al dominio y un servidor remoto de Exchange 2013 con el FQDN <em>ExServer.contoso.com</em>. Use este comando si desea administrar un servidor remoto de Exchange 2013 y solo desea tener Windows Management Framework, que incluye la interfaz de línea de comandos Windows PowerShell instalada en su equipo local. Este comando usa sus credenciales de inicio de sesión actuales para autenticar el servidor remoto de Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p>$UserCredential = Get-Credential</p>
<p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos -Credential $UserCredential</p>
<p>Import-PSSession $Session</p></td>
<td><p>Estos comandos abren una sesión remota del Shell entre un equipo local unido al dominio y un servidor remoto de Exchange 2013 con el FQDN <em>ExServer.contoso.com</em>. Use este comando si desea administrar un servidor remoto de Exchange 2013 y solo desea tener Windows Management Framework, que incluye la interfaz de línea de comandos Windows PowerShell instalada en su equipo local. Este comando usa los credenciales que haya especificado para autenticar el servidor remoto de Exchange 2013.</p></td>
</tr>
<tr class="odd">
<td><p>Remove-PSSession $Session</p></td>
<td><p>Este comando cierra la sesión remota del Shell establecida entre un equipo local y el servidor remoto de Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p>Import-RecipientDataProperty -Identity &quot;Tony Smith&quot; -SpokenName -FileData <em>([Byte[]]$(Get-Content -Path &quot;M:\AudioFiles\TonySmith.wma&quot; -Encoding Byte -ReadCount 0))</em></p></td>
<td><p>Este comando muestra un ejemplo de la sintaxis, mostrada en cursiva, necesaria para importar un archivo a un servidor remoto de Exchange 2013 usando el parámetro FileData en un cmdlet. La sintaxis encapsula los datos que contiene el archivo <em>M:\AudioFiles\TonySmith.wma</em> y transmite los datos a la propiedad FileData en el cmdlet Import-RecipientDataProperty.</p>
<p>El parámetro FileData acepta datos de archivos de su equipo local que usen esta sintaxis en la mayoría de cmdlets.</p></td>
</tr>
<tr class="odd">
<td><p>Export-RecipientDataProperty -Identity tony@contoso.com -SpokenName <em>| ForEach { $_.FileData | Add-Content C:\tonysmith.wma -Encoding Byte}</em></p></td>
<td><p>Este comando muestra un ejemplo de la sintaxis, mostrada en cursiva, necesaria para exportar un archivo de un servidor remoto de Exchange 2013. La sintaxis encapsula los datos almacenados en la propiedad FileData en el objeto que devuelve el cmdlet y transmite los datos al equipo local. A continuación, los datos se almacenan en el archivo <em>C:\tonysmith.wma</em>.</p>
<p>La mayoría de cmdlets que devuelven objetos con una propiedad FileData usan esta sintaxis para exportar datos a un archivo del equipo local.</p></td>
</tr>
</tbody>
</table>

