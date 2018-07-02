---
title: 'Crear un ámbito de administración personalizado para las búsquedas de exhibición de documentos electrónicos local: Exchange 2013 Help'
TOCTitle: Crear un ámbito de administración personalizado para las búsquedas de exhibición de documentos electrónicos local
ms:assetid: 1543aefe-3709-402c-b9cd-c11fe898aad1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn741464(v=EXCHG.150)
ms:contentKeyID: 62219859
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear un ámbito de administración personalizado para las búsquedas de exhibición de documentos electrónicos local

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-01-21_

Puede usar un ámbito de administración personalizado para permitir que determinadas personas o grupos usen la exhibición de documentos electrónicos local para buscar un subconjunto de los buzones de la organización de Exchange 2013 o Exchange Online. Por ejemplo, quizás quiera permitir que un administrador de detección realice búsquedas solo en los buzones de los usuarios de un departamento o una ubicación en particular. Para ello, puede crear un ámbito de administración personalizado. Este ámbito de administración personalizado usa un filtro de destinatarios para controlar los buzones de correo en los que se pueden realizar búsquedas. Los ámbitos de filtro de destinatario usan filtros para dirigirse a destinatarios específicos en función del tipo de destinatario o de otras propiedades del destinatario.

Para la exhibición de documentos electrónicos local, la única propiedad de un buzón de usuario que puede usar para crear un filtro de destinatarios para un ámbito personalizado es la pertenencia al grupo de distribución (el nombre real de la propiedad es *MemberOfGroup*). Si usa otras propiedades, como *CustomAttributeN*, *Department* o *PostalCode*, la búsqueda no se realiza correctamente si la ejecuta un miembro del grupo de roles que ha asignado el ámbito personalizado.

Para obtener más información sobre los ámbitos de administración, vea:

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

  - [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Como se ha indicado anteriormente, solo puede usar la pertenencia a grupos como el filtrado de destinatarios para crear un ámbito de filtrado de destinatarios personalizado que se usará para la exhibición de documentos electrónicos. No se puede usar ninguna otra propiedad de destinatario para crear un ámbito personalizado para las búsquedas de exhibición de documentos electrónicos. Tenga en cuenta que tampoco se puede usar la pertenencia a grupos en un grupo de distribución dinámica.

  - Realice los pasos 1 a 3 para permitir que un administrador de detección exporte los resultados de la búsqueda para una búsqueda de exhibición de documentos electrónicos que use un ámbito de administración personalizado.

  - Si el administrador de detección no necesita obtener una vista previa de los resultados de la búsqueda, puede omitir el paso 4.

  - Si el administrador de detección no necesita copiar los resultados de la búsqueda, puede omitir el paso 5.

## Paso 1: organizar a los usuarios en grupos de distribución para la exhibición de documentos electrónicos

Para buscar un subconjunto de buzones en su organización o para restringir el ámbito de los buzones de origen en los que puede buscar un administrador de detección, deberá agrupar los subconjuntos de buzones en uno o varios grupos de distribución. Cuando cree un ámbito de administración personalizado en el paso 2, usará estos grupos de distribución como el filtro de destinatarios para crear un ámbito de administración personalizado. Esto permite que el administrador de detección busque únicamente en los buzones de los usuarios que son miembros de un grupo especificado.

Puede usar grupos de distribución existentes para la exhibición de documentos electrónicos o crear nuevos grupos. Vea Más información al final de este tema para obtener sugerencias sobre cómo crear grupos de distribución que se puedan usar para limitar las búsquedas de exhibición de documentos electrónicos.

## Paso 2: crear un ámbito de administración personalizado

Ahora creará un ámbito de administración personalizado que está definido por la pertenencia a un grupo de distribución (con el filtro de destinatarios *MemberOfGroup*). Cuando se aplica este ámbito a un grupo de roles usado para la exhibición de documentos electrónicos, los miembros del grupo de roles pueden buscar los buzones de usuarios que son miembros del grupo de distribución que se usó para crear el ámbito de administración personalizado.

Este procedimiento usa comandos del Shell de administración de Exchange para crear un ámbito personalizado llamado Ámbito de exhibición de documentos electrónicos de usuarios de Ottawa. Especifica el grupo de distribución denominado Usuarios de Ottawa para el filtro de destinatarios del ámbito personalizado.

1.  Ejecute este comando para obtener y guardar las propiedades del grupo de usuarios de Ottawa como una variable, que se usa en el próximo comando.
    
        $DG = Get-DistributionGroup -Identity "Ottawa Users"

2.  Ejecute este comando para crear un ámbito de administración personalizado en función de la pertenencia al grupo de distribución de usuarios de Ottawa.
    
        New-ManagementScope "Ottawa Users eDiscovery Scope" -RecipientRestrictionFilter "MemberOfGroup -eq '$($DG.DistinguishedName)'"
    
    El nombre distintivo del grupo de distribución, que forma parte de la variable **$DG**, se usa para crear el filtro de destinatarios para el nuevo ámbito de administración.

## Paso 3: crear un grupo de roles de administración

En este paso, debe crear un nuevo grupo de roles de administración y asignar el ámbito personalizado que creó en el paso 2. Agregue los roles de suspensión legal y de búsqueda en el buzón de modo que los miembros del grupo de roles puedan realizar búsquedas en la exhibición de documentos electrónicos local y colocar los buzones en retención por juicio o conservación local. También puede agregar miembros a este grupo de roles para que puedan realizar búsquedas en los buzones de los miembros del grupo de distribución que se usó para crear el ámbito personalizado en el paso 2.

En los siguientes ejemplos, el grupo de seguridad de administradores de la exhibición de documentos electrónicos de usuarios de Ottawa se agregará como miembro del grupo de roles. Puede usar el Shell o el EAC para este paso.

## Use el Shell para crear un grupo de roles de administración

Ejecute este comando para crear un nuevo grupo de roles que use el ámbito personalizado creado en el paso 2. El comando también agrega los roles de suspensión legal y de búsqueda en el buzón y agrega a los administradores de la exhibición de documentos electrónicos de usuarios de Ottawa como miembros del nuevo grupo de roles.

    New-RoleGroup "Ottawa Discovery Management" -Roles "Mailbox Search","Legal Hold" -CustomRecipientWriteScope "Ottawa Users eDiscovery Scope" -Members "Ottawa Users eDiscovery Managers"

## Usar el EAC para crear un grupo de roles de administración

1.  En el EAC, vaya a **Permisos** \> **Roles de administrador** y luego haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En **Nuevo grupo de roles**, proporcione la siguiente información:
    
      - **Nombre**   Especifique un nombre descriptivo para el nuevo grupo de roles. Para este ejemplo, usamos **Administración de detección de Ottawa**.
    
      - **Ámbito de escritura**   Seleccione el ámbito de administración personalizado que creó en el paso 2. Este ámbito se aplicará al nuevo grupo de roles.
    
      - **Roles**   Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y agregue los roles **Suspensión legal** y **Búsqueda en el buzón** al nuevo grupo de roles.
    
      - **Miembros**   Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y seleccione los usuarios, el grupo de seguridad o los grupos de roles que quiere agregar como miembros del nuevo grupo de roles. Para este ejemplo, los miembros del grupo de seguridad **Administradores de la exhibición de documentos electrónicos de usuarios de Ottawa** podrán buscar solo en los buzones de los usuarios que son miembros del grupo de distribución de **usuarios de Ottawa**.

3.  Haga clic en **Guardar** para crear el grupo de roles.
    
    Aquí hay un ejemplo de cómo se verá la ventana **Nuevo grupo de roles** cuando haya finalizado.
    
    ![Crear un nuevo grupo de roles para un ámbito personalizado](images/Dn741464.a6e3419f-d5d9-404f-890d-ad35f499756f(EXCHG.150).gif "Crear un nuevo grupo de roles para un ámbito personalizado")  

## Paso 4 (opcional): agregar administradores de detección como miembros del grupo de distribución usado para crear el ámbito de administración personalizado

Solo debe llevar a cabo este paso si quiere que un administrador de detección obtenga una vista previa de los resultados de la búsqueda de la exhibición de documentos electrónicos.

Ejecute este comando para agregar el grupo de seguridad de administradores de la exhibición de documentos electrónicos de usuarios de Ottawa como miembro del grupo de distribución de usuarios de Ottawa.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Users eDiscovery Managers"

También puede usar el EAC para agregar miembros a un grupo de distribución. Para más información, vea [Crear y administrar grupos de distribución](create-and-manage-distribution-groups-exchange-2013-help.md).

## Paso 5 (opcional): agregar un buzón de correo de detección como miembro del grupo de distribución usado para crear el ámbito de administración personalizado

Solo debe llevar a cabo este paso si quiere que un administrador de detección pueda copiar los resultados de la búsqueda de la exhibición de documentos electrónicos.

Ejecute este comando para agregar un buzón de correo de detección llamado Buzón de correo de detección de Ottawa como miembro del grupo de distribución de usuarios de Ottawa.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Discovery Mailbox"


> [!NOTE]
> Para abrir un buzón de correo de detección y ver los resultados de la búsqueda, los administradores de detección deben tener asignados permisos de acceso total al buzón de correo de detección. Para más información, vea <A href="create-a-discovery-mailbox-exchange-2013-help.md">Crear un buzón de correo de detección</A>.



## ¿Cómo saber si el proceso se ha completado correctamente?

Aquí le presentamos algunas formas de comprobar si ha implementado correctamente los ámbitos de administración personalizados para la exhibición de documentos electrónicos. Cuando realice la comprobación, asegúrese de que el usuario que ejecuta las búsquedas en la exhibición de documentos electrónicos sea miembro del grupo de roles que usa el ámbito de administración personalizado.

  - Cree una búsqueda de exhibición de documentos electrónicos y seleccione el grupo de distribución que se usó para crear el ámbito de administración personalizado como origen de los buzones de correo en los que se realizará la búsqueda. Debe poder buscarse correctamente en todos los buzones de correo.

  - Cree una búsqueda de exhibición de documentos electrónicos y busque los buzones de correo de los usuarios que no son miembros del grupo de distribución que se usó para crear el ámbito de administración personalizado. La búsqueda debe presentar un error porque el administrador de detección solo puede buscar los buzones de correo de los usuarios que son miembros del grupo de distribución que se usó para crear el ámbito de administración personalizado. En este caso, aparecerá un error como "No se puede buscar el buzón \<*name of mailbox*\> porque el usuario actual no tiene permiso para obtener acceso al buzón".

  - Cree una búsqueda de exhibición de documentos electrónicos y busque los buzones de correo de los usuarios que son miembros del grupo de distribución que se usó para crear el ámbito de administración personalizado. En la misma búsqueda, incluya los buzones de correo de los usuarios que no son miembros. Podrá realizar la búsqueda parcialmente. Podrá buscar sin problemas los buzones de correo de los miembros del grupo de distribución usado para crear el ámbito de administración personalizado. No podrá realizar la búsqueda de los buzones de los usuarios que no son miembros del grupo.

## Más información

  - Debido a que los grupos de distribución se usan en este escenario para limitar las búsquedas de exhibición de documentos electrónicos y no para el envío de mensajes, considere lo siguiente al crear y configurar los grupos de distribución para la exhibición de documentos electrónicos:
    
      - Cree grupos de distribución con una pertenencia cerrada para que solo los propietarios del grupo puedan agregar o quitar miembros del grupo. Si quiere crear el grupo en el Shell, use la sintaxis `MemberJoinRestriction closed` y `MemberDepartRestriction closed`.
    
      - Habilite la moderación del grupo de modo que todos los mensajes enviados al grupo primero lleguen a los moderadores del grupo para que puedan aprobar o rechazar el mensaje según corresponda. Si quiere crear el grupo en el Shell, use la sintaxis `ModerationEnabled $true`. Si quiere usar el EAC, puede habilitar la moderación después de que se crea el grupo.
    
      - Oculte el grupo de distribución de la libreta de direcciones compartida de la organización. Use el EAC o el cmdlet **Set-DistributionGroup** una vez que se creó el grupo. Si está usando el Shell, use la sintaxis `HiddenFromAddressListsEnabled $true`.
    
    En el siguiente ejemplo, el primer comando crea un grupo de distribución con pertenencia cerrada y moderación habilitada. El segundo comando oculta el grupo de la libreta de direcciones compartida.
    
        New-DistributionGroup -Name "Vancouver Users eDiscovery Scope" -Alias VancouverUserseDiscovery -MemberJoinRestriction closed -MemberDepartRestriction closed -ModerationEnabled $true
    
        Set-DistributionGroup "Vancouver Users eDiscovery Scope" -HiddenFromAddressListsEnabled $true
    
    Para obtener más información sobre la creación y la administración de los grupos de distribución, vea [Crear y administrar grupos de distribución](create-and-manage-distribution-groups-exchange-2013-help.md).

  - Si bien solo puede usar la pertenencia a grupos de distribución como filtro de destinatarios para un ámbito de administración personalizado que se usa para la exhibición de documentos electrónicos, puede usar otras propiedades de los destinatarios para agregar usuarios al grupo de distribución. Aquí hay algunos ejemplos de cómo usar los cmdlets **Get-Mailbox** y **Get-Recipient** para obtener un grupo específico de usuarios en función de atributos comunes de usuarios o buzones de correo.
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "VancouverSubsidiary"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -OrganizationalUnit "namsr01a002.sdf.exchangelabs.com/Microsoft Exchange Hosted Organizations/contoso.onmicrosoft.com"

  - Luego, puede usar los ejemplos anteriores para crear una variable que se puede usar con el cmdlet **Add-DistributionGroupMember** para agregar un grupo de usuarios a un grupo de distribución. En el siguiente ejemplo, el primer comando crea una variable que contiene todos los buzones del usuario que tienen el valor **Vancouver** para la propiedad *Department* en su cuenta de usuario. El segundo comando agrega estos usuarios al grupo de distribución de usuarios de Vancouver.
    
        $members = Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "Vancouver"'
    
        $members | ForEach {Add-DistributionGroupMember "Ottawa Users" -Member $_.Name}

  - Puede usar el cmdlet **Add-RoleGroupMember** para agregar un miembro a un grupo de roles existente que se usa para limitar las búsquedas en la exhibición de documentos electrónicos. Por ejemplo, el siguiente comando agrega el usuario admin@ottawa.contoso.com al grupo de roles de administración de detección de Ottawa.
    
        Add-RoleGroupMember "Vancouver Discovery Management" -Member paralegal@vancouver.contoso.com
    
    También puede usar el EAC para agregar miembros a un grupo de roles. Para obtener más información, consulte la sección \&quot;Agregar miembros a un grupo de funciones\&quot; en [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

  - En Exchange Online, no se puede usar un ámbito de administración personalizado para la exhibición de documentos electrónicos para buscar buzones inactivos. Esto es porque un buzón inactivo no puede ser miembro de un grupo de distribución. Por ejemplo, supongamos que un usuario es miembro de un grupo de distribución que se usó para crear un ámbito de administración personalizado para la exhibición de documentos electrónicos. A continuación, el usuario abandona la organización y su buzón de correo queda inactivo (al colocar una retención por juicio o una conservación local y, a continuación, eliminar la cuenta de usuario de Office 365 correspondiente). El resultado es que se ha quitado el usuario como miembro de cualquier grupo de distribución, incluido el grupo que se usó para crear el ámbito de administración personalizado utilizado para la exhibición de documentos electrónicos. Si un administrador de detección (que es miembro del grupo de roles asignado el ámbito de administración personalizado) intenta buscar el buzón inactivo, la búsqueda producirá un error. Para buscar buzones inactivos, un administrador de detección debe ser miembro del grupo de roles de administración de detección o cualquier grupo de roles que tenga permisos para buscar en toda la organización.
    
    Para obtener más información sobre buzones inactivos, consulte [Buzones de correo inactivos en Exchange Online](https://technet.microsoft.com/es-es/library/dn798632\(v=exchg.150\)).

