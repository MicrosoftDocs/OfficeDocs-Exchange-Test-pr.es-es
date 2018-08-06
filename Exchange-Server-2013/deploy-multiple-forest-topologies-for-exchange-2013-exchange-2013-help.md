---
title: 'Implementar topologías de varios bosques para Exchange 2013 Exchange 2013 Help | Microsoft Docs'
TOCTitle: Implementar topologías de varios bosques para Exchange 2013
ms:assetid: d51f2b7d-9045-40cf-8b9f-43787a6fff6d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124734(v=EXCHG.150)
ms:contentKeyID: 51406553
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Implementar topologías de varios bosques para Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En este tema se ofrece una introducción a la implementación de Microsoft Exchange Server 2013 en topologías de bosques múltiples. Encontrará información acerca de los siguientes temas:

  - **Topologías de bosques múltiples admitidas**   Exchange 2013 admite dos tipos de topologías de bosques múltiples: bosque de recursos y entre bosques.

  - **Sincronización de LGD**   Si tiene un entorno entre bosques, deberá asegurarse de que la LGD de cualquier bosque determinado contenga los destinatarios de correo de los demás bosques.

  - **Mover buzones entre bosques**    Los cmdlets **New-MoveRequest** y **New-MigrationBatch** en el Shell de administración de Exchange pueden ayudar a mover buzones de correo entre bosques.

  - **Descripción de la administración de varios bosques**   Obtenga más información sobre el modelo de permisos para configurar y administrar los permisos entre los bosques.

## Topologías de bosques múltiples admitidas

Exchange 2013 admite los siguientes tipos de topologías de bosques múltiples:

  - **Entre bosques**   Una topología entre bosques es la que contiene varios bosques de Exchange. Aquí le mostramos información general de lo que debe hacer para implementar Exchange 2013 en una topología con varios bosques:
    
    1.  Debe instalar primero Exchange 2013 en cada bosque. Para obtener más información, consulte [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md).
    
    2.  A continuación, debe sincronizar los destinatarios en cada uno, de forma que la lista global de direcciones (GAL) de cada bosque contenga usuarios de todos los bosques sincronizados. Consulte la sección "Sincronización de GAL" a continuación para obtener más detalles.
    
    3.  Por último, debe configurar el servicio de disponibilidad para que los usuarios de un bosque puedan ver los datos de disponibilidad de los usuarios de otro bosque. Para obtener más información, consulte [Configurar el servicio de disponibilidad para topologías entre bosques](configure-the-availability-service-for-cross-forest-topologies-exchange-2013-help.md).
    
    Para obtener más información acerca de la implementación de Exchange 2013 en una topología entre bosques, vea [Implementar Exchange 2013 en una topología entre bosques](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md).

  - **Bosque de recursos**   Una topología de bosque de recursos es la que contiene un bosque de Exchange y uno o más bosques de cuentas de usuario. Aquí le mostramos información general de lo que debe hacer para implementar Exchange 2013 en una topología con un bosque de recursos:
    
    1.  Debe tener un bosque con Exchange instalado. En el bosque de Exchange, debe tener deshabilitadas las cuentas de usuario que tienen buzones de Exchange.
    
    2.  Debe tener al menos un bosque que contenga cuentas de usuario. Este bosque *no* debe tener instalado Exchange.
    
    3.  A continuación, debe asociar las cuentas de usuario deshabilitadas en el bosque de Exchange con las cuentas de usuario del bosque de cuentas.
    
    Para obtener más información acerca de la implementación de Exchange 2013 en una topología de bosque de recursos, vea [Implementación de Exchange 2013 en una topología de bosques de recursos de Exchange](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md).

## Sincronización de LGD

De forma predeterminada, la GAL contiene destinatarios de correo de un único bosque. Si tiene un entorno entre bosques, le recomendamos que utilice Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) para asegurarse de que la GAL de cualquier bosque determinado contenga los destinatarios de correo de los demás bosques. ILM 2007 FP1 crea usuarios de correo que representan destinatarios de otros bosques, lo que permite, por tanto, que los usuarios los vean en la GAL y envíen correo. Por ejemplo, los usuarios del Bosque A aparecen como un usuario de correo en el Bosque B y viceversa. De este modo, los usuarios del bosque de destino pueden seleccionar el objeto de usuario de correo que representa un destinatario de otro bosque para enviarle correo.

Para habilitar la sincronización de GAL, se crean agentes de administración que importan usuarios con correo habilitado, contactos y grupos de servicios de Active Directory designados dentro de un metadirectorio centralizado. En el metadirectorio, los objetos con correo habilitado se representan como usuarios de correo. Los grupos se representan como contactos sin ninguna pertenencia asociada. Los agentes de administración exportan estos usuarios de correo a una unidad organizativa en el bosque de destino especificado.

Para más información sobre Forefront Identity Manager (FIM), vea [Forefront Identity Manager 2010](https://go.microsoft.com/fwlink/p/?linkid=279864).

## Mover buzones de correo entre bosques

En una topología entre bosques, puede que desee mover los buzones de un bosque a otro. Para hacerlo debe usar el cmdlet **New-MoveRequest** o **New-MigrationBatch** en el Shell de administración de Exchange. Para obtener más información acerca de cómo mover buzones de correo entre bosques, consulte los siguientes temas:

  - [Preparar los buzones para las solicitudes de movimiento entre bosques](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Preparar buzones para moverlos entre bosques con el script Prepare-MoveRequest.ps1 en el Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

  - [Preparar buzones para movimientos entre bosques mediante código de ejemplo](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

## Descripción de la administración de varios bosques

Exchange 2013 usa la nueva funcionalidad de permisos para administrar los entornos de bosques múltiples.

Exchange 2013 utiliza un modelo de permisos de control de acceso basado en roles (RBAC). Los grupos de roles de administración a los que pertenecen los administradores, así como las directivas de asignación de roles de administración que los usuarios finales tienen asignadas, determinan lo que cada administrador y cada usuario final pueden hacer. Para entender bien los permisos de bosques múltiples, es necesario estar familiarizado con RBAC. Para obtener más información sobre los grupos de roles y RBAC, y las directivas de asignación de roles en particular, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

Puede utilizar el modelo de permisos RBAC para configurar y administrar los permisos entre los bosques. Para obtener más información acerca de los permisos de bosques múltiples, consulte los siguientes temas:

  - [Descripción de permisos de bosques múltiples](understanding-multiple-forest-permissions-exchange-2013-help.md)

  - [Administrar grupos de funciones vinculadas](manage-linked-role-groups-exchange-2013-help.md)

  - [Crear grupos de funciones vinculadas que reflejan grupos de funciones integradas](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

