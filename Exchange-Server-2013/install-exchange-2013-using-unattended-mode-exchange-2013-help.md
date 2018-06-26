---
title: 'Instalar Exchange 2013 usando el modo desatendido: Exchange 2013 Help'
TOCTitle: Instalar Exchange 2013 usando el modo desatendido
ms:assetid: 386465e9-41da-4e26-9816-b3b69be1f8bf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997281(v=EXCHG.150)
ms:contentKeyID: 48267996
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Instalar Exchange 2013 usando el modo desatendido

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-06-19_

Para hacer una instalación desatendida, debe instalar Microsoft Exchange Server 2013 desde el símbolo del sistema. Para obtener más información acerca de la planificación e implementación de Exchange 2013, vea [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Se recomienda instalar el rol de transporte perimetral en una red perimetral fuera del bosque interno de Active Directory de su organización. Aunque puede instalar el rol del servidor transporte perimetral en un equipo unido a un dominio, al hacerlo solo se habilita la gestión de las características y configuración de Windows relativa al dominio. El propio rol de transporte perimetral no usa Active Directory. En su lugar usa la característica Active Directory Lightweight Directory Services (AD LDS) Windows para almacenar la información de la configuración y del destinatario. Para obtener más información acerca del rol de transporte perimetral, consulte [Servidores de transporte perimetral](edge-transport-servers-exchange-2013-help.md).


> [!TIP]
> ¿Conoce el asistente para la implementación de Exchange Server? Es una herramienta en línea gratuita que le ayuda a implementar rápidamente Exchange 2013 en su organización realizando unas cuantas preguntas y creando una lista de comprobación de implementación personalizada solo para usted. Si desea más información, vaya a <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Asistente para la implementación de Exchange Server</A>.




> [!NOTE]
> Después de instalar los roles del servidor en un equipo que ejecute Exchange&nbsp;2013, no puede usar el Asistente para instalación de Exchange&nbsp;2013 para agregar roles de servidor adicionales a este equipo. Si desea agregar más roles de servidor a un equipo, debe usar Agregar o quitar programas en el Panel de control o usar Setup.exe en una ventana de símbolo del sistema.<BR>El rol de transporte perimetral no se puede instalar en el mismo equipo que las funciones de servidor de buzón o de acceso de cliente.



Para obtener información acerca de las tareas posteriores a la instalación, consulte [Tareas posteriores a la instalación de Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

La siguiente información concierne a todas las funciones de servidor de Exchange 2013.

  - Asegúrese de haber leído las notas de la versión antes de instalar Exchange 2013. Para obtener más información, vea [Notas de la versión de Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - El equipo en el que se instale Exchange 2013 debe contar con un sistema operativo compatible (como Windows Server 2008 R2 con Service Pack 1 (SP1), Windows Server 2012 R2 o Windows Server 2012), disponer de suficiente espacio en el disco y satisfacer otros requisitos. Para obtener información acerca de los requisitos del sistema, consulte [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Para ejecutar la instalación de Exchange 2013, debe instalar Microsoft .NET Framework 4.5, Windows Management Framework y otro software necesario. Para comprender los requisitos previos para todos los roles de servidor, consulte [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Después de instalar Exchange en un servidor, no debe modificar el nombre del servidor. No se admite el cambio de nombre de un servidor después de haber instalado el rol del servidor de Exchange.



La siguiente información concierne a las funciones de buzón y de acceso de cliente de Exchange 2013 .

  - Tiempo estimado para finalizar: 60 minutos

  - Cada organización requiere, como mínimo, un servidor de acceso de cliente y un servidor de buzones en el bosque de Active Directory. Además, cada sitio de Active Directory que contiene un servidor de buzones deberá también contener, como mínimo, un servidor de acceso de cliente. Si separa sus roles de servidor, le recomendamos instalar el rol del servidor de buzones primero.

  - El equipo en el que se instala Exchange 2013 debe ser miembro de un dominio Active Directory.

  - Debe asegurarse de que la cuenta que use tenga delegada la pertenencia al grupo Administradores de esquema, si no ha preparado previamente el esquema de Active Directory. Si va a instalar el primer servidor de Exchange 2013 en la organización, la cuenta que use deberá pertenecer al grupo Administradores de empresa. Si ya ha preparado el esquema y no va a instalar el primer servidor de Exchange 2013 en la organización, la cuenta que use deberá ser miembro del grupo de roles de administración de la organización de Exchange 2013.
    
    Los administradores que pertenecen al grupo de roles de configuración delegada pueden implementar servidores de Exchange 2013 que ya han sido aprovisionados por un miembro del grupo de roles de administración de la organización.

La siguiente información concierne al rol de servidor de transporte perimetral de Exchange 2013.

  - Tiempo estimado para finalizar: 40 minutos

  - El rol de transporte perimetral está disponible en Exchange 2013 SP1 o posterior.

  - Debe configurar el sufijo DNS principal en el equipo. Por ejemplo, si el nombre de dominio completo del equipo es edge.contoso.com, el sufijo DNS del equipo es contoso.com. Para obtener más información, consulte [Falta el sufijo DNS principal](primary-dns-suffix-is-missing-exchange-2013-help.md).

  - Es necesario actualizar los servidores de Transporte de concentradores de Exchange 2007 and Exchange 2010 antes de poder crear una suscripción de EdgeSync entre ellos y el servidor de transporte perimetral de Exchange 2013. Si no se instala esta actualización, la suscripción de EdgeSync no funcionará correctamente. Para obtener más información, consulte la sección "Escenarios de coexistencia compatibles" en [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Asegúrese de que la cuenta que utiliza es un miembro del grupo Administradores local del equipo en el que está instalando el rol de transporte perimetral.

## Usar Setup.exe para instalar Exchange 2013 en modo desatendido


> [!NOTE]
> Para descargarla última versión de Exchange&nbsp;2013, consulte <A href="updates-for-exchange-2013-exchange-2013-help.md">Actualizaciones para Exchange 2013</A>.



1.  Inicie sesión en el equipo en el que desea instalar Exchange 2013.

2.  Desplácese a la ubicación de red de los archivos de instalación de Exchange 2013.

3.  En el símbolo del sistema, ejecute el comando correspondiente para su organización.
    

    > [!IMPORTANT]
    > Si tiene el control de acceso de usuarios (UAC) habilitado, tiene que ejecutar <CODE>Setup.exe</CODE> desde un símbolo del sistema elevado.

    
        Setup.exe [/Mode:<setup mode>] [/IAcceptExchangeServerLicenseTerms]
        [/Roles:<server roles to install>] [/InstallWindowsComponents] 
        [/OrganizationName:<name for the new Exchange organization>] 
        [/TargetDir:<target directory>] [/SourceDir:<source directory>]
        [/UpdatesDir:<directory from which to install updates>] 
        [/DomainController:<FQDN of domain controller>] [/DisableAMFiltering]
        [/AnswerFile:<filename>] [/DoNotStartTransport] 
        [/EnableErrorReporting] [/CustomerFeedbackEnabled:<True | False>] 
        [/AddUmLanguagePack:<UM language pack name>] 
        [/RemoveUmLanguagePack:<UM language pack name>] 
        [/NewProvisionedServer:<server>] [/RemoveProvisionedServer:<server>] 
        [/MdbName:<mailbox database name>] [/DbFilePath:<Edb file path>] 
        [/LogFolderPath:<log folder path>] [/ActiveDirectorySplitPermissions:<True | False>]
        [/TenantOrganizationConfig:<path>]

4.  El programa de instalación copia los archivos localmente en el equipo donde va a instalar Exchange 2013.

5.  El programa de instalación comprueba los requisitos previos, incluidos todos los requisitos previos específicos en los roles de servidor que está instalando. Si no ha cumplido todos los requisitos previos, el programa de instalación genera un error y devuelve un mensaje que explica las razones del error. Si se han cumplido todos los requisitos previos, el programa de instalación instala Exchange 2013.

6.  Reinicie el equipo después de que se haya completado Exchange 2013.

7.  Complete la implementación haciendo las tareas indicadas en [Tareas posteriores a la instalación de Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Ejemplos

Los siguientes son ejemplos del uso de Setup.exe:

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /OrganizationName:MyOrg /IAcceptExchangeServerLicenseTerms**
    
    Este comando crea una organización Exchange 2013 en Active Directory denominada MyOrg, instala el rol del servidor de acceso de clientes, el rol del servidor de buzón de correo y las herramientas de administración, y también acepta los términos de licencias de Exchange 2013.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /TargetDir:"C:\\Exchange Server" /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala el rol de servidor de acceso de clientes, el rol de servidor de buzón de correo y las herramientas de administración en el directorio "C:\\Exchange Server". Este comando asume que ya se ha preparado una organización de Exchange 2013.

  - **Setup.exe /mode:Install /r:CA,MB /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala el rol de servidor de acceso de clientes, el rol de servidor de buzón de correo y las herramientas de administración en la ubicación de instalación predeterminada.

  - **Setup.exe /mode:Install /r:EdgeTransport /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala el rol de servidor de transporte perimetral y las herramientas administrativas en la ubicación de instalación predeterminada.

  - **Setup.exe /mode:Install /r:ET /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala el rol de servidor de transporte perimetral y las herramientas administrativas en la ubicación de instalación predeterminada.

  - **Setup.exe /mode:Uninstall /IAcceptExchangeServerLicenseTerms**
    
    Este comando quita completamente Exchange 2013 del servidor y quita también la configuración de Exchange de este servidor de Active Directory.

  - **Setup.exe /PrepareAD /on:"My Org" /IAcceptExchangeServerLicenseTerms**
    
    Este comando crea una organización de Exchange llamada My Org y prepara Active Directory para Exchange 2013.

  - **C:\\ExchangeServer\\bin\\Setup.exe /m:Install /r:ClientAccess /SourceDir:d:\\amd64 /IAcceptExchangeServerLicenseTerms**
    
    Este comando agrega el rol de servidor Acceso de clientes a un servidor de Exchange 2013 existente, usando D:\\amd64 como directorio de origen.

  - **Setup.exe /role:ClientAccess,Mailbox /UpdatesDir:"C:\\ExchangeServer\\New Patches" /IAcceptExchangeServerLicenseTerms**
    
    Este comando actualiza ExchangeServer.msi con actualizaciones desde el directorio especificado y, a continuación, instala el rol de servidor de acceso de clientes, el rol de servidor de buzón de correo y las herramientas de administración. Si se incluye un conjunto de paquete de idiomas en este directorio, también se incluye el paquete de idiomas.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /DomainController:DC01 /IAcceptExchangeServerLicenseTerms**
    
    Este comando usa el controlador de dominio DC01 para consultar y realizar modificaciones en Active Directory al tiempo que instala el rol del servidor de acceso de clientes, el rol del servidor de buzón de correo y las herramientas de administración.

  - **Setup.exe /mode:Install /role:ClientAccess /AnswerFile:c:\\ExchangeConfig.txt /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala el rol de servidor de acceso de clientes usando la configuración en el archivo ExchangeConfig.txt.

  - **Setup.exe /rprs:Exchange03 /IAcceptExchangeServerLicenseTerms**
    
    Este comando quita el objeto Exchange03 de Active Directory.

  - **Setup.exe /AddUmLanguagePack:ko-KR /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala el paquete de idioma coreano de mensajería unificada desde el directorio %ExchangeSourceDir%\\ServerRoles\\UnifiedMessaging.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha instalado Exchange 2013 correctamente, consulte [Comprobar una instalación de Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

