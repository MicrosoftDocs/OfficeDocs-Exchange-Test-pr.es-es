---
title: 'Requisitos previos de Exchange 2013: Exchange 2013 Help'
TOCTitle: Requisitos previos de Exchange 2013
ms:assetid: e21cf744-7813-48b3-9293-5cecd89a6c25
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb691354(v=EXCHG.150)
ms:contentKeyID: 48268806
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Requisitos previos de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-03-20_

Este tema describe los pasos para instalar los requisitos previos necesarios de los sistemas operativos Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2 con Service Pack 1 (SP1) para los roles de servidor Transporte perimetral, Acceso de clientes y Buzón de correo de Microsoft Exchange 2013. También describe los requisitos previos necesarios para instalar las herramientas de administración de Exchange 2013 en equipos cliente Windows 8, Windows 8.1 y Windows 7.

  - ¿Qué necesita saber antes de comenzar?

  - Preparación de Active Directory

  - Requisitos previos de Windows Server 2012 R2 y Windows Server 2012
    
      - Roles de servidor de acceso de cliente y de buzón
    
      - Rol de servidor Transporte perimetral

  - Requisitos previos de Windows Server 2008 R2 SP1
    
      - Roles de servidor de acceso de cliente y de buzón
    
      - Rol de servidor Transporte perimetral

  - Requisitos previos de Windows 7 (solo herramientas de administración) (solo herramientas de administración)

  - Requisitos previos de Windows 8 y Windows 8.1 (solo herramientas de administración) (solo herramientas de administración)

## ¿Qué necesita saber antes de comenzar?

  - La información de este tema se aplica al Service Pack 1 y las versiones posteriores de Exchange 2013.

  - El rol de servidor Transporte perimetral se encuentra disponible a partir de Exchange 2013 SP1.

  - Asegúrese de que el nivel funcional del bosque es al menos Windows Server 2003 y de que el maestro de esquema ejecuta Windows Server 2003 con Service Pack 2 o posterior. Para obtener más información acerca de los niveles funcionales de Windows, consulte [Administración de dominios y bosques](https://go.microsoft.com/fwlink/p/?linkid=137037).

  - Debe usarse la opción de instalación completa de Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2 SP1 en todos los servidores que ejecuten herramientas de administración o roles de servidor de Exchange 2013.

  - En primer lugar, debe unir el equipo al dominio y al bosque interno de Active Directory adecuado.

  - Algunos requisitos previos requieren que reinicie el servidor para completar la instalación.

  - Instale las actualizaciones más recientes de Windows en el equipo. Para obtener más información, consulte [Lista de comprobación de seguridad de la implementación](deployment-security-checklist-exchange-2013-help.md).
    

    > [!NOTE]
    > Si va a instalar el rol de servidor Buzón de correo y desea que el servidor sea miembro de un grupo de disponibilidad de base de datos (DAG), deberá ejecutar Windows Server 2012 R2 Standard Edition o Datacenter Edition, Windows Server 2012 Standard Edition o Datacenter Edition, o Windows Server 2008 R2 SP1 Enterprise Edition. Windows Server 2008 R2 SP 1 Standard Edition no admite las características necesarias para DAG.<BR>Si Exchange está instalado en el servidor, no puede actualizar Windows.<BR>Para actualizar a API administrada de comunicaciones unificadas de Microsoft (UCMA) 4.0, primero debe desinstalar las versiones anteriores de UCMA mediante <STRONG>Agregar o quitar programas</STRONG>.




> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Preparación de Active Directory

El equipo que desea usar para preparar Active Directory para Exchange 2013 tiene requisitos previos específicos que se deben cumplir.

Instale el software siguiente, en el orden indicado, en el equipo que se usará para preparar Active Directory:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (incluida en Windows Server 2012 R2)

Después de instalar el software mencionado anteriormente, complete los siguientes pasos para instalar el paquete de administración de herramientas remotas. Después de instalar el paquete de administración de herramientas remotas, podrá usar el equipo para preparar Active Directory. Para más información sobre cómo preparar Active Directory, vea [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md).

1.  Abra Windows PowerShell.

2.  Instale el paquete de administración de herramientas remotas.
    
      - En un equipo con Windows Server 2012 R2 o Windows Server 2012, ejecute el comando siguiente.
        
            Install-WindowsFeature RSAT-ADDS
    
      - En un equipo con Windows Server 2008 R2 SP1, ejecute el comando siguiente.
        
            Add-WindowsFeature RSAT-ADDS

## Requisitos previos de Windows Server 2012 R2 y Windows Server 2012

Los requisitos previos necesarios para instalar Exchange 2013 en un equipo con Windows Server 2012 R2 o Windows Server 2012 varían en función de los roles de Exchange que se deseen instalar. Lea la sección siguiente que coincida con los roles que desea instalar.

## Roles de servidor de acceso de cliente y de buzón

Siga las instrucciones de esta sección para instalar los requisitos previos en equipos con Windows Server 2012 R2 o Windows Server 2012, si desea realizar en ellos una de las acciones siguientes:

  - Instale solo el rol de servidor Buzón de correo en un equipo.

  - Instale únicamente el rol de servidor de acceso de cliente en un equipo.

  - Instale los roles de servidor Buzón de correo y Acceso de clientes en el mismo equipo.

Siga este procedimiento para instalar los roles y las características necesarias de Windows:

1.  Abra Windows PowerShell.

2.  Ejecute el siguiente comando para instalar los componentes necesarios de Windows.
    
        Install-WindowsFeature AS-HTTP-Activation, Desktop-Experience, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS

Una vez instalados los roles del sistema operativo y las características, instale el siguiente software en el orden indicado:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 y posterior <STRONG>requieren</STRONG> .NET Framework 4.6.2. Actualice los servidores a .NET Framework 4.6.2 antes de instalar Exchange 2013 CU16 o recibirá un error. Si .NET Framework 4.5.2 está instalado en los servidores de Exchange, actualice los servidores a Exchange 2013 CU15 antes de instalar .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (incluida en Windows Server 2012 R2)

3.  [Microsoft Unified Communications Managed API 4.0, Runtime principal de 64 bits](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Rol de servidor Transporte perimetral

Siga las instrucciones de esta sección para instalar los requisitos previos en equipos con Windows Server 2012 R2 o Windows Server 2012, si desea instalar el rol de servidor Transporte perimetral.

Siga este procedimiento para instalar los roles y las características necesarias de Windows:

1.  Abra Windows PowerShell.

2.  Ejecute el siguiente comando para instalar los componentes necesarios de Windows.
    
        Install-WindowsFeature ADLDS

Instale la versión de Microsoft .NET Framework correspondiente a la versión de Exchange 2013 que esté instalando.

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 y posterior <STRONG>requieren</STRONG> .NET Framework 4.6.2. Actualice los servidores a .NET Framework 4.6.2 antes de instalar Exchange 2013 CU16 o recibirá un error. Si .NET Framework 4.5.2 está instalado en los servidores de Exchange, actualice los servidores a Exchange 2013 CU15 antes de instalar .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (incluida en Windows Server 2012 R2)

## Requisitos previos de Windows Server 2008 R2 SP1

Los requisitos previos necesarios para instalar Exchange 2013 en un equipo con Windows Server 2008 R2 SP1 varían en función de los roles de Exchange que se deseen instalar. Lea la sección siguiente que coincida con los roles que desea instalar.

## Roles de servidor de acceso de cliente y de buzón

Siga las instrucciones de esta sección para instalar los requisitos previos en equipos Windows Server 2008 R2 SP1 donde desee hacer una de las siguientes acciones:

  - Instale sólo el rol de servidor Buzón de correo en un equipo.

  - Instale únicamente el rol de servidor de acceso de cliente en un equipo.

  - Instale los roles de servidor Buzón de correo y Acceso de clientes en el mismo equipo.

Siga este procedimiento para instalar los roles y las características necesarias de Windows:

1.  Abra Windows PowerShell.

2.  Ejecute el siguiente comando para cargar el módulo del Administrador del servidor.
    
        Import-Module ServerManager

3.  Ejecute el siguiente comando para instalar los componentes necesarios de Windows.
    
        Add-WindowsFeature Desktop-Experience, NET-Framework, NET-HTTP-Activation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Web-Server, WAS-Process-Model, Web-Asp-Net, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, RSAT-ADDS

Una vez instalados los roles del sistema operativo y las características, instale el siguiente software en el orden indicado:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 y posterior <STRONG>requieren</STRONG> .NET Framework 4.6.2. Actualice los servidores a .NET Framework 4.6.2 antes de instalar Exchange 2013 CU16 o recibirá un error. Si .NET Framework 4.5.2 está instalado en los servidores de Exchange, actualice los servidores a Exchange 2013 CU15 antes de instalar .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Runtime principal de 64 bits](https://go.microsoft.com/fwlink/p/?linkid=258269)

4.  [Artículo de la base de conocimientos Microsoft KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

5.  [Artículo de la base de conocimientos KB2619234 (Habilitar la cookie/GUID de la asociación usada por RPC por HTTP que también se usa en la capa RPC en Windows 7 y en Windows Server 2008 R2)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2619234)

6.  [Artículo de la base de conocimientos KB2533623 (La carga de biblioteca no protegida puede permitir la ejecución de código remoto)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2533623)
    

    > [!NOTE]
    > Esta revisión ya está instalada si configuró Windows Update para instalar actualizaciones de seguridad en su equipo.



## Rol de servidor Transporte perimetral

Siga las instrucciones de esta sección para instalar los requisitos previos en equipos con Windows Server 2008 R2 SP1 donde quiera instalar solo el rol de servidor Transporte perimetral.

Siga este procedimiento para instalar los roles y las características necesarias de Windows:

1.  Abra Windows PowerShell.

2.  Ejecute el siguiente comando para cargar el módulo del Administrador del servidor.
    
        Import-Module ServerManager

3.  Ejecute el siguiente comando para instalar los componentes necesarios de Windows.
    
        Add-WindowsFeature NET-Framework, ADLDS

Una vez instalados los roles del sistema operativo y las características, instale el siguiente software en el orden indicado:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 y posterior <STRONG>requieren</STRONG> .NET Framework 4.6.2. Actualice los servidores a .NET Framework 4.6.2 antes de instalar Exchange 2013 CU16 o recibirá un error. Si .NET Framework 4.5.2 está instalado en los servidores de Exchange, actualice los servidores a Exchange 2013 CU15 antes de instalar .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Runtime principal de 64 bits](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Requisitos previos de Windows 7 (solo herramientas de administración)

Siga las instrucciones de esta sección para instalar los requisitos previos en equipos con Windows 7 de 64 bits unidos a dominio, donde desee instalar las herramientas de administración de Exchange.

1.  Abra **Panel de control** y, a continuación, seleccione **Programas**.

2.  Haga clic en **Activar o desactivar las características de Windows**.

3.  Vaya hasta **Internet Information Services** \> **Herramientas de administración web** \> **Compatibilidad con la administración de IIS 6**.

4.  Active la casilla **Consola de administración de IIS 6** y, a continuación, haga clic en **Aceptar**.

Una vez instalados las características del sistema operativo, instale el siguiente software en el orden indicado:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Artículo de la base de conocimientos KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

## Requisitos previos de Windows 8 y Windows 8.1 (solo herramientas de administración)

[.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

