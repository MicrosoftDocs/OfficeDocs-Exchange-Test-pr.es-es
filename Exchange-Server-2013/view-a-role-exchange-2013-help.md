---
title: 'Ver una función: Exchange 2013 Help'
TOCTitle: Ver una función
ms:assetid: 1875b15f-22db-4ede-b310-ea894d6211c8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335117(v=EXCHG.150)
ms:contentKeyID: 49895495
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver una función

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Las funciones de administración se pueden enumerar de diferentes maneras, según la información que desee. Por ejemplo, puede elegir devolver solamente funciones de un tipo de funciones específico, funciones que contienen sólo cmdlets y parámetros o puede ver los detalles de una función de administración específica. Para obtener más información acerca de las funciones de administración en Microsoft Exchange Server 2013, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

Si desea ver una lista de todas las entradas de funciones de administración de una función, consulte [Ver entradas de papel](view-role-entries-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Este tema usa canalización y los cmdlets **Format-List** y **Format-Table**. Para obtener más información acerca de estos conceptos, consulte los siguientes temas:
    
      - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))
    
      - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Vea una función de administración específica

Puede ver los detalles de una función específica si recupera una función específica mediante el cmdlet **Get-ManagementRole** y canaliza la salida al cmdlet **Format-List**.

Para ver los detalles de una función específica, utilice la siguiente sintaxis.

    Get-ManagementRole <role name> | Format-List

En este ejemplo, se recuperan los detalles acerca de la función de administración de destinatarios de correo.

    Get-ManagementRole "Mail Recipients" | Format-List

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRole](https://technet.microsoft.com/es-es/library/dd351125\(v=exchg.150\)).

## Enumere todas las funciones de administración

Puede ver una lista de todas las funciones de administración de su organización si no especifica ninguna función cuando ejecuta el cmdlet **Get-ManagementRole**. De manera predeterminada, el nombre y el tipo de cada función se incluye en los resultados.

En este ejemplo, se devuelve una lista de todas las funciones de la organización.

    Get-ManagementRole

Para especificar una lista de propiedades específicas de todas las funciones de su organización, puede canalizar los resultados del cmdlet **Format-Table** y especificar las propiedades que desea en la lista de resultados. Use la siguiente sintaxis.

    Get-ManagementRole | Format-Table <property 1>, <property 2...>

En este ejemplo, se devuelve una lista de todas las funciones de su organización e incluye la propiedad **Name** y toda propiedad con la palabra **Implicit** en el comienzo del nombre de la propiedad.

    Get-ManagementRole | Format-Table Name, Implicit*

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRole](https://technet.microsoft.com/es-es/library/dd351125\(v=exchg.150\)).

## Enumerar funciones de administración que contienen un cmdlet específico

Puede devolver una lista de las funciones que contengan un cmdlet que especifica si usa el parámetro *Cmdlet* en el cmdlet **Get-ManagementRole**.

Para devolver una lista de funciones que contengan el cmdlet que especifica, use la siguiente sintaxis.

    Get-ManagementRole -Cmdlet <cmdlet>

En este ejemplo, se devuelve una lista de funciones que contienen el cmdlet de **New-Mailbox**.

    Get-ManagementRole -Cmdlet New-Mailbox

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRole](https://technet.microsoft.com/es-es/library/dd351125\(v=exchg.150\)).

## Enumerar funciones de administración que contienen un parámetro específico

Puede devolver una lista de las funciones que contengan uno o más parámetros especificados si usa el parámetro *CmdletParameters* en el cmdlet **Get-ManagementRole**. Se devuelven solo las funciones que contienen todos los parámetros que especifique.

Cuando usa el parámetro *CmdletParameters*, puede elegir incluir el parámetro *Cmdlet*. Si incluye el parámetro *Cmdlet*, solo se devuelven las funciones que contienen los parámetros que especifica en el cmdlet especificado. Si no desea incluir el parámetro *Cmdlet*, solo se devuelven las funciones que contienen los parámetros que especifica, independientemente del cmdlet en los que están.

Para devolver una lista de funciones que contienen los parámetros que especifica, use la siguiente sintaxis.

    Get-ManagementRole [-Cmdlet <cmdlet>] -CmdletParameters <parameter 1>, <parameter 2...>

En este ejemplo, se devuelve una lista de funciones que contienen los parámetros *Database* y *Server*, independientemente de los cmdlets que existan en ellos.

    Get-ManagementRole -CmdletParameters Database, Server

En este ejemplo, se devuelve una lista de funciones en la que existe el parámetro *EmailAddresses* solo en el cmdlet **Set-Mailbox**.

    Get-ManagementRole -Cmdlet Set-Mailbox -CmdletParameters EmailAddresses

Además, puede usar un carácter comodín (\*) con los parámetros *Cmdlet* o *CmdletParameters* para que coincidan parcialmente con el cmdlet y los nombres de parámetros.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRole](https://technet.microsoft.com/es-es/library/dd351125\(v=exchg.150\)).

## Enumerar funciones de administración de un tipo de función específica

Puede devolver una lista de las funciones basada en un tipo de función especifico si usa el parámetro *RoleType* en el cmdlet **Get-ManagementRole**.

Para devolver una lista de funciones que coincidan con el tipo de función que especifica, use la siguiente sintaxis.

    Get-ManagementRole -RoleType <roletype>

En este ejemplo, se devuelve una lista de funciones basadas en el tipo de función `UmMailboxes`.

    Get-ManagementRole -RoleType UmMailboxes

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRole](https://technet.microsoft.com/es-es/library/dd351125\(v=exchg.150\)).

## Enumerar las funciones secundarias inmediatas de una función primaria

Puede devolver una lista de las funciones que sean una función secundaria inmediata de la función primaria especificada si usa el parámetro *GetChildren* en el cmdlet **Get-ManagementRole**. Solo se devuelven las funciones que contienen una función especificada como función primaria.

Para devolver una lista de las funciones secundarias inmediatas a la función primaria, use la siguiente sintaxis.

    Get-ManagementRole <parent role name> -GetChildren

En este ejemplo, se devuelve una lista de funciones secundarias inmediatas a la función Recuperación de desastres.

    Get-ManagementRole "Disaster Recovery" -GetChildren

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRole](https://technet.microsoft.com/es-es/library/dd351125\(v=exchg.150\)).

## Enumerar todas las funciones secundarias que siguen a una función primaria

Puede devolver una lista de una cadena entera de funciones desde una función primaria especificada hasta la última función primaria si usa el parámetro *Recurse* en el cmdlet **Get-ManagementRole**. El parámetro *Recurse* informa al cmdlet **Get-ManagementRole** para que haya recursividad en todas las relaciones primarias y secundarias que encuentre hasta alcanzar la última función secundaria. La función primaria se incluye en la lista que se devuelve.

En este ejemplo, se devuelve una lista de todas las funciones secundarias de una función primaria.

    Get-ManagementRole <parent role name> -Recurse

En este ejemplo, se devuelven todas las funciones secundarias de la función de destinatarios de correo.

    Get-ManagementRole "Mail Recipients" -Recurse

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRole](https://technet.microsoft.com/es-es/library/dd351125\(v=exchg.150\)).

