---
title: 'Descripción de ámbitos exclusivos: Exchange 2013 Help'
TOCTitle: Descripción de ámbitos exclusivos
ms:assetid: 32492622-3b01-4e3b-8288-ed39525eea75
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638110(v=EXCHG.150)
ms:contentKeyID: 49895558
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Descripción de ámbitos exclusivos

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Los *ámbitos exclusivos* consisten en una clase especial de ámbito de administración explícito que se puede asociar con asignaciones de funciones de administración. Los ámbitos exclusivos se han ideado para situaciones en que existe un grupo con objetos de gran valor, por ejemplo, el buzón de correo de un presidente ejecutivo, y desea controlar estrechamente la obtención de acceso a dicho buzón para administrar esos objetos.

Como su nombre indica, la *asignación de funciones exclusivas* consiste en la asignación de funciones de ámbito exclusivo.

Al crear un ámbito exclusivo, los únicos que pueden modificar los objetos que concuerdan con el ámbito son quienes tienen asignados dicho ámbito exclusivo o uno equivalente. Las asignaciones de funciones que no están asignadas a ese ámbito exclusivo o uno equivalente no pueden modificar los objetos que coincidan con el ámbito, ni siquiera aunque sus propias funciones posean ámbitos que pudieran incluir los objetos. Los ámbitos exclusivos anulan cualquier otro ámbito normal que no es exclusivo. Es un comportamiento similar al modo de denegar una entrada de control de acceso (ACE) en funciones de lista de control de acceso de Active Directory.

El concepto de *ámbito exclusivo equivalente* se refiere a otro ámbito exclusivo que coincide con algunos de los objetos que tiene otro ámbito exclusivo. Los ámbito no necesariamente deben coincidir con toda la serie de objetos. Los dos ámbitos pueden poder modificar algunos o todos los objetos que tienen en común.

## Creación de ámbitos exclusivos

Los ámbitos exclusivos se pueden crear como cualquier otro ámbito explícito. Se puede especificar un ámbito relativo integrado previamente, un filtro de destinatarios, de base de datos, de servidores o una lista de servidores. A diferencia de los ámbitos normales, que no surten efecto hasta que se asocia un ámbito con una asignación de funciones de administración, el aspecto de denegación de un ámbito exclusivo se aplica de manera inmediata. Eso significa que, nada más crearse un ámbito exclusivo, de manera inmediata los usuarios no pueden obtener acceso a ninguno de sus objetos hasta que se haya creado la asignación de funciones.

Tras haberse creado la asignación, el ámbito exclusivo concede acceso a quienes tengan asignado el ámbito y la función de administración. Si otro ámbito exclusivo equivalente coincide con los mismos objetos, la asignación de funciones asociada con ese ámbito exclusivo también puede obtener acceso a los objetos.

Para obtener más información acerca de los filtros de ámbitos de administración, consulte [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).


> [!IMPORTANT]
> Los tiempos de replicación de Active Directory se deben tener en cuenta a la hora de hacer cambios en los componentes de funciones de administración, incluidos los ámbitos exclusivos.



Si tiene objetos que forman parte de más de un ámbito exclusivo, la asignación a cualquiera de los ámbitos exclusivos concede acceso a los objetos. Para obtener más información, consulte Exclusive and regular scope interaction más adelante en este tema.

Los ámbitos exclusivos controlan únicamente el destinatario explícito o el ámbito de escritura de configuración de una asignación de funciones. El destinatario implícito o el ámbito de lectura de configuración de la función asignada a un usuario o un grupo siguen siendo válidos. Eso significa que se aplican los enunciados siguientes:

  - Los que estén asignados a una función siguen viendo objetos que coinciden con el ámbito de lectura implícito de la función.

  - Los que estén asignados a otras funciones pueden ver objetos pertenecientes a un ámbito exclusivo si los ámbitos de lectura de las otras funciones incluyen los objetos. Ahora bien, los únicos que pueden modificar los objetos son quienes tengan asignada una función asociada con el ámbito exclusivo.

Los ámbitos exclusivos solo son válidos con funciones administrativas o de especialistas; no son aptos para funciones de usuario final. Para obtener más información acerca de las funciones, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

## Interacción del ámbito exclusivo y normal

La figura que hay al final de esta sección ilustra la interacción entre los ámbitos exclusivos y la relación con los normales. Los usuarios de la figura tienen asociados todos los atributos siguientes.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Usuario</th>
<th>Ciudad</th>
<th>Cargo</th>
<th>Departamento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Terry</p></td>
<td><p>Vancouver</p></td>
<td><p>Contable</p></td>
<td><p>Contabilidad</p></td>
</tr>
<tr class="even">
<td><p>David</p></td>
<td><p>Vancouver</p></td>
<td><p>Redactor</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="odd">
<td><p>Walter</p></td>
<td><p>Vancouver</p></td>
<td><p>Manager</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="even">
<td><p>Bob</p></td>
<td><p>Vancouver</p></td>
<td><p>Presidente ejecutivo</p></td>
<td><p>Consejo de administración</p></td>
</tr>
<tr class="odd">
<td><p>Christine</p></td>
<td><p>Vancouver</p></td>
<td><p>Presidente</p></td>
<td><p>Consejo de administración</p></td>
</tr>
<tr class="even">
<td><p>Fred</p></td>
<td><p>Vancouver</p></td>
<td><p>Director financiero</p></td>
<td><p>Ejecutivos</p></td>
</tr>
<tr class="odd">
<td><p>Martin</p></td>
<td><p>Vancouver</p></td>
<td><p>Director de tecnología y sistemas</p></td>
<td><p>Ejecutivos</p></td>
</tr>
<tr class="even">
<td><p>Kim</p></td>
<td><p>Vancouver</p></td>
<td><p>Vicepresidente de operaciones</p></td>
<td><p>Ejecutivos</p></td>
</tr>
<tr class="odd">
<td><p>Jennifer</p></td>
<td><p>Vancouver</p></td>
<td><p>Vicepresidente de tecnología</p></td>
<td><p>Ejecutivos</p></td>
</tr>
</tbody>
</table>


Las tres asignaciones de funciones siguientes de la figura se encargan de los usuarios de la tabla anterior. Cada uno tiene un ámbito asociado, algunos de los cuales son exclusivos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Asignación de funciones</th>
<th>Filtro de ámbito</th>
<th>Exclusivo o normal</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administradores de destinatarios</p></td>
<td><p>Ciudad = Vancouver</p></td>
<td><p>Normal</p></td>
</tr>
<tr class="even">
<td><p>Administradores VIP</p></td>
<td><p>Cargo = presidente ejecutivo o director financiero o director de tecnologías y sistemas o presidente</p></td>
<td><p>Exclusivo</p></td>
</tr>
<tr class="odd">
<td><p>Administradores de ejecutivos</p></td>
<td><p>Departamento = Ejecutivos</p></td>
<td><p>Exclusivo</p></td>
</tr>
</tbody>
</table>


La asignación de función Administradores de destinatarios tiene un ámbito que coincide con todos los usuarios porque cada uno de ellos se ubica en Vancouver. Si no hubiera ámbitos exclusivos, la asignación de función Administradores de destinatarios podría encargarse de cualquiera de los usuarios. Sin embargo, esta organización ha creado dos ámbitos exclusivos: Administradores VIP y Administradores de ejecutivos. Estos ámbitos exclusivos limitan a los que pueden administrar a los usuarios que coinciden con sus respectivos filtros de ámbito. La asignación de función Administradores VIP tiene un filtro de ámbito que coincide con cualquier usuario cuyo cargo sea el de presidente ejecutivo, director financiero, director de tecnologías y sistemas o presidente. La asignación de función Administradores de ejecutivos tiene un filtro de ámbito que coincide con cualquier usuario inscrito en el departamento Ejecutivos.

Si se evalúan los ámbitos normales y exclusivos, el resultado es el siguiente:

  - La asignación de función Administradores de destinatarios puede encargarse de los usuarios Terry, David y Walter. Esta asignación de funciones no puede ocuparse de ningún otro usuario porque coinciden con los filtros de ámbito exclusivo de las asignaciones de funciones Administradores VIP y Administradores ejecutivos.

  - La asignación de función Administradores VIP puede encargarse de los usuarios Bob, Christine, Fred y Martin. Esto sucede porque el filtro de ámbito exclusivo relacionado con esta función asignada coincide con los atributos de los objetos. Esta asignación de función no se puede encargar de los usuarios Kim y Jennifer porque sus atributos no coinciden con este ámbito exclusivo.

  - La asignación de función Administradores de ejecutivos puede encargarse de los usuarios Kim, Jennifer, Fred y Martin. Esto sucede porque el filtro de ámbito exclusivo relacionado con esta función asignada coincide con los atributos de los objetos. Esta asignación de función no se puede encargar de los usuarios Bob y Christine porque sus atributos no coinciden con este ámbito exclusivo.

Observe que se puede obtener acceso a Fred y Martin mediante ambos ámbitos exclusivos. Eso se debe a que los atributos de esos usuarios coinciden con los filtros de los dos ámbitos exclusivos.

**Interacción entre ámbitos exclusivos y ámbitos normales**

![Interacción del ámbito exclusivo y normal](images/Dd638110.0aa26d1d-1fa6-44d8-802d-83d75cd2624c(EXCHG.150).jpg "Interacción del ámbito exclusivo y normal")

Para obtener más información acerca de los ámbitos de administración, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

