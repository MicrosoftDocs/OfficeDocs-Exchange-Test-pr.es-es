---
title: 'Modificar una relación de la organización: Exchange 2013 Help'
TOCTitle: Modificar una relación de la organización
ms:assetid: 3713ef83-f01a-41bb-b127-62ca242dd7a4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673055(v=EXCHG.150)
ms:contentKeyID: 49895567
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificar una relación de la organización

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-01-01_

Con una relación de organización, los usuarios de la organización de Exchange pueden compartir la información de disponibilidad del calendario con otra organización de Exchange local o con una organización de Office 365. Posiblemente quiera cambiar la configuración de una relación de organización, ya sea modificar su nombre, deshabilitar el uso compartido de calendario de forma temporal, alterar el nivel de acceso o cambiar los grupos de seguridad que pueden compartir calendarios.

Para poder compartir calendarios con otra organización, debe configurar una relación de autenticación con la nube (también conocida como "federación") y debe cumplir unos requisitos de software mínimos. Para obtener más información acerca del uso compartido federado, consulte [Uso compartido](sharing-exchange-2013-help.md).

Para otras tareas de administración relacionadas con la federación, consulte [Procedimientos de la Federación](federation-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  15 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada de *Calendar and Sharing Permissions* en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Se debe configurar una confianza de federación activa para la organización de Exchange local.

  - La organización externa que quiere configurar en la relación de organización debe tener también una confianza de federación establecida con el sistema de autenticación de Azure AD.

  - Con los procedimientos de este tema se efectúan cambios en una relación de organización llamada Contoso. Los ejemplos ilustran cómo:
    
      - Agregar un dominio llamado service.contoso.com a la organización externa.
    
      - Deshabilitar el uso compartido de disponibilidad de la relación de la organización.
    
      - Cambiar el nivel de acceso de disponibilidad de *Calendar free/busy information with time, subject, and location* a *Calendar free/busy information with time only*.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Usar el EAC para agregar un dominio a una relación de organización

1.  En un servidor de Exchange 2013 de la organización local, vaya a **organización** \> **uso compartido**.

2.  En la vista de lista, en **Uso compartido de la organización**, seleccione la relación de la organización Contoso y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **relación de la organización**, **general** no cambie el **Nombre** de la relación de organización

4.  En el cuadro **Dominios para compartir**, escriba el dominio **service.contoso.com**, y, luego, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

5.  Haga clic en **guardar** para actualizar la relación de la organización.

## Use el EAC para deshabilitar el uso compartido de disponibilidad compartida de la relación de la organización

1.  Vaya a **organización** \> **uso compartido**.

2.  En la vista de lista, en **Uso compartido de la organización**, seleccione la relación de la organización Contoso y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **relación de organización**, haga clic en **uso compartido**

4.  Seleccione **Información de disponibilidad de calendario solo con hora**.

5.  Haga clic en **guardar** para actualizar la relación de la organización.

## Use el EAC para cambiar el nivel de acceso de disponibilidad compartida de la relación de la organización

1.  Vaya a **organización** \> **uso compartido**.

2.  En la vista de lista, en **Uso compartido de la organización**, seleccione la relación de la organización Contoso y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **relación de organización**, haga clic en **uso compartido**

4.  Seleccione **Información de disponibilidad de calendario solo con hora**.

5.  Haga clic en **guardar** para actualizar la relación de la organización.

## Uso del Shell para modificar la relación de organización

  - Este ejemplo agrega el nombre de dominio service.contoso.com a la relación de la organización Contoso.
    
        $domains = (Get-OrganizationRelationship Contoso).DomainNames
        $domains += 'service.contoso.com'
        Set-OrganizationRelationship -Identity Contoso -DomainNames $domains

  - En este ejemplo se deshabilita la relación de la organización Contoso.
    
        Set-OrganizationRelationship -Identity Contoso -Enabled $false

  - En este ejemplo, se habilita el acceso a la información de disponibilidad de calendario para la relación organizativa WoodgroveBank y se establece el nivel de acceso en `AvailabilityOnly` (información de disponibilidad de calendario con tiempo solo).
    
        Set-OrganizationRelationship -Identity Contoso -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-OrganizationRelationship](https://technet.microsoft.com/es-es/library/ee332343\(v=exchg.150\)) y [Set-OrganizationRelationship](https://technet.microsoft.com/es-es/library/ee332326\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya actualizado la relación de la actualización correctamente, ejecute el siguiente comando de Shell y compruebe la información de la relación de la organización.

    Get-OrganizationRelationship | format-list


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


