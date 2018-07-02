---
title: 'Planificación e implementación: Exchange 2013 Help'
TOCTitle: Planificación e implementación
ms:assetid: 692c59e3-f0b0-4cef-a66e-751aa740abae
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998636(v=EXCHG.150)
ms:contentKeyID: 48268234
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planificación e implementación

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

¿Necesita ayuda para instalar Exchange? En este artículo encontrará información orientativa para planear una implementación de Microsoft Exchange Server 2013, además de vínculos a los artículos que necesitará durante el proceso de implementación.

The following sections contain links to information about planning for and then deploying Microsoft Exchange Server 2013.


> [!IMPORTANT]
> Make sure you read the <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de la versión de Exchange&nbsp;2013</A> topic before you begin your deployment. The release notes contain important information on issues you might encounter during and after your deployment.



**Contenido**

Planning for Exchange 2013

Implementar una instalación de Exchange 2013

Understanding Exchange 2013 Setup

For more information

## Planning for Exchange 2013

Use the following links to access information to help you plan the deployment of Exchange Server 2013 into your organization.


> [!IMPORTANT]
> See Establish a test environment later in this topic about installing Exchange&nbsp;2013 in a test environment.



  - [Servidores de buzones de correo y de acceso de clientes](mailbox-and-client-access-servers-exchange-2013-help.md)  
    Learn about the Mailbox and Client Access server roles that are included with Exchange 2013.

<!-- end list -->

  - [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md)  
    Understand the system requirements that need to be satisfied in your organization before you can install Exchange 2013.

<!-- end list -->

  - [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md)  
    Learn which Windows Server 2008 R2 Service Pack 1 (SP1) or Windows Server 2012 features and the other software that needs to be installed to perform a successful installation of Exchange 2013.

<!-- end list -->

  - [Asistente para la implementación de Exchange Server](exchange-server-deployment-assistant-exchange-2013-help.md)  
    Use this tool to generate a customized checklist for planning, installing, or upgrading to Exchange 2013. Guidance is available for multiple scenarios, including an on-premises, hybrid, or cloud deployment.

<!-- end list -->

  - [Active Directory](active-directory-exchange-2013-help.md)  
    Read this topic to learn about how Exchange 2013 uses Active Directory and how your Active Directory deployment affects your Exchange deployment.

<!-- end list -->

  - [Protección antimalware](anti-malware-protection-exchange-2013-help.md)  
    Read this topic to understand anti-malware protection options for Exchange 2013.

<!-- end list -->

  - [Implementaciones híbridas de Exchange Server](https://technet.microsoft.com/es-es/library/jj200581\(v=exchg.150\))  
    Read this topic to help you with planning a hybrid deployment with Microsoft Office 365 and your on-premises Exchange 2013 organization.

<!-- end list -->

  - [Planificación de alta disponibilidad y resistencia de sitios](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
    Read this topic to help you with planning to achieve your high availability and business continuity requirements.

<!-- end list -->

  - [Integración con SharePoint y Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md)  
    Read this topic to learn about integrating Exchange 2013, Microsoft SharePoint 2013, and Microsoft Lync 2013 to enable cross-product archiving, hold, and eDiscovery; site mailboxes; authentication; Lync presence; and more.

<!-- end list -->

  - [Diseño de mensajería unificada](planning-for-unified-messaging-exchange-2013-help.md)  
    Read this topic to learn more about planning for Exchange 2013 Unified Messaging.

<!-- end list -->

  - [Opciones de configuración de almacenamiento de Exchange 2013](exchange-2013-storage-configuration-options-exchange-2013-help.md)  
    Read this topic to learn about the storage architectures, disk types, and storage configurations supported by the Exchange 2013 Mailbox server role.

<!-- end list -->

  - [Virtualización de Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md)  
    Read this topic to learn more about how you can deploy Exchange 2013 in a virtualized environment.

<!-- end list -->

  - [Arquitectura multiempresa en Exchange 2013](multi-tenancy-in-exchange-2013-exchange-2013-help.md)  
    Read this topic to learn more about how you can configure Exchange 2013 to host multiple and discrete organizations or business units that ordinarily don’t share email, data, users, global address lists (GALs), or other commonly used Exchange objects.

<!-- end list -->

  - [Exchange Development Technologies](https://go.microsoft.com/fwlink/p/?linkid=268448)  
    This topic contains important information about Application Programming Interfaces (APIs) that are available for applications that use Exchange 2013.

## Establish a test environment

Before installing Exchange 2013 for the first time, we recommend that you install it in an isolated test environment. This approach reduces the risk of end-user downtime and negative ramifications to the production environment.

The test environment will act as your “proof of concept” for your new Exchange 2013 design and make it possible to move forward or roll back any implementations before deploying into your production environments. Having an exclusive test environment for validation and testing allows you to do pre-installation checks for your future production environments. By installing in a test environment first, we believe that your organization will have a better likelihood of success in a full production implementation.

For many organizations, the costs of building a test lab may be high because of the need to duplicate the production environment. To reduce the hardware costs associated with a prototype lab, we recommend the use of virtualization by using Windows Server 2008 R2 or Windows Server 2012 Hyper-V technologies. Hyper-V enables server virtualization, allowing multiple virtual operating systems to run on a single physical machine.

Para obtener información detallada sobre Hyper-V, vea [Hyper-V](https://go.microsoft.com/fwlink/p/?linkid=117704). Para información sobre el soporte de Microsoft para Exchange 2013 en la producción de software de virtualización de hardware, vea “Virtualización de hardware” en [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

## Implementar una instalación de Exchange 2013

The deployment phase is the period during which you install Exchange 2013 into your organization. Before you begin the deployment phase, you should plan your Exchange organization. For more information, see the Planning for Exchange 2013 section earlier in this topic.

Use the following links to access the information you need to help you with deploying Exchange 2013.

  - [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md)  
    Learn about the steps you need to take to prepare your Active Directory forest for Exchange 2013 and the changes Exchange makes to your forest.

<!-- end list -->

  - [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)  
    Follow the steps in this topic to use the Exchange 2013 Setup wizard to install Exchange 2013 into a new Exchange organization.

<!-- end list -->

  - [Instalar Exchange 2013 usando el modo desatendido](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)  
    Follow the steps in this topic to use Exchange 2013 unattended setup to install Exchange 2013 into a new Exchange organization.

<!-- end list -->

  - [Instalar el rol de transporte perimetral de Exchange 2013 mediante el asistente de instalación](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)  
    Follow the steps in this topic to use the Exchange 2013 Setup wizard to install the Exchange 2013 Edge Transport role into a perimeter network.

<!-- end list -->

  - [Actualizar Exchange 2013 a la actualización acumulativa o Service Pack más reciente](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)  
    Follow the steps in this topic to apply the latest cumulative update or service pack to Exchange 2013 servers in your organization.

<!-- end list -->

  - [Actualizar de Exchange 2010 a Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)  
    Follow the steps in this topic to install Exchange 2013 into an existing Exchange 2010 organization.

<!-- end list -->

  - [Actualizar de Exchange 2007 a Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)  
    Follow the steps in this topic to install Exchange 2013 into an existing Exchange 2007 organization.

<!-- end list -->

  - [Implementar topologías de varios bosques para Exchange 2013](deploy-multiple-forest-topologies-for-exchange-2013-exchange-2013-help.md)  
    Read this topic for information that will help you deploy Exchange 2013 in an organization that contains more than one Active Directory forest.

<!-- end list -->

  - [Implementación del correo de voz y mensajería unificada](deploying-voice-mail-and-um-exchange-2013-help.md)  
    Read this topic for information that will help you understand deploying Exchange 2013 Unified Messaging, whether a new deployment or an upgrade.

<!-- end list -->

  - [Procedimientos de implementación híbrida](https://technet.microsoft.com/es-es/library/jj200788\(v=exchg.150\))  
    Read this topic for information that will help you deploy Exchange 2013 in an existing hybrid deployment.

<!-- end list -->

  - [Tareas posteriores a la instalación de Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md)  
    Learn about post-installation tasks to complete your Exchange 2013 installation.

## Understanding Exchange 2013 Setup

You can use different types and modes of Exchange 2013 Setup to install and maintain the various editions and versions of Exchange 2013.

## Exchange editions and versions

Exchange 2013 está disponible en dos ediciones de servidor: Standard y Enterprise. Se trata de ediciones con licencia definidas por una clave de producto. Para más información, vea [Licencias de Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=237292).

## Types of Exchange Setup

You have the following options for Exchange 2013 Setup:

  - **Exchange Setup UI**   Running Setup.exe without any command-line switches provides an interactive experience where you are guided by the Exchange 2013 Setup wizard.

  - **Exchange Unattended Setup**   Running Setup.exe with command-line switches enables you to install Exchange from an interactive command line or through a script.

Setup.exe is available from the Exchange 2013 DVD or the downloaded source files.

## Modes of Exchange Setup

Setup for Exchange 2013 includes several installation modes:

  - **Install**   Use this mode when you're installing a new server role or adding a server role to an existing installation (maintenance mode). You can use this mode from both the Exchange Setup wizard and the unattended install.

  - **Uninstall**   Use this mode when you're removing the Exchange installation from a computer. You can use this mode from both the Exchange Setup wizard and the unattended install.

  - **Upgrade**   Select this mode used when you have an existing installation of Exchange and you're installing a cumulative update or service pack. You can use this mode from both the Exchange Setup wizard and the unattended install.
    

    > [!NOTE]
    > Exchange&nbsp;2013 doesn't support in-place upgrades from previous versions of Exchange. This mode is used only to install cumulative updates or service packs.



  - **RecoverServer**   Use this mode when there has been a catastrophic failure of a server, and you need to recover data. You must install a server using the same fully qualified domain name (FQDN) as the failed server, and then run Setup with the **/m:RecoverServer** switch. Don't specify the roles to restore. Setup detects the Exchange Server object in Active Directory and installs the corresponding files and configuration automatically. After you recover the server, you can restore databases and reconfigure any additional settings. To run in **RecoverServer** mode, you can't have Exchange installed on the server. The Exchange server object must exist in Active Directory. You can only use this mode during an unattended installation.


> [!NOTE]
> You must complete one mode of Setup before you can use another mode.



## For more information

[Compatibilidad con IPv6 en Exchange 2013](ipv6-support-in-exchange-2013-exchange-2013-help.md)

[Centro de administración de Exchange en Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)

[Compatibilidad de idioma de Exchange de 2013](exchange-2013-language-support-exchange-2013-help.md)

[Comprobaciones de disponibilidad de Exchange 2013](exchange-2013-readiness-checks-exchange-2013-help.md)

