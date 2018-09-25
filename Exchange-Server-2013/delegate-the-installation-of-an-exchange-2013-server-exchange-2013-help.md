---
title: 'Delegar la instalación de un servidor de Exchange 2013: Exchange 2013 Help'
TOCTitle: Delegar la instalación de un servidor de Exchange 2013
ms:assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201741(v=EXCHG.150)
ms:contentKeyID: 62615187
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Delegar la instalación de un servidor de Exchange 2013

 

_**Se aplica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Última modificación del tema:** 2014-07-31_

Exchange Server 2013 le permite delegar la instalación de los servidores de Exchange a personas que no son miembros del grupo de roles Administración de la organización de Exchange 2013. A menudo esto resulta útil en las empresas de gran tamaño en las que las personas que instalan y configuran los servidores no son las encargadas de administrar servicios como Exchange. Si esto se asemeja a lo que desea hacer, este tema es para usted.

Por lo general, cuando se instala Exchange, las personas que lo instalan deben ser miembros del grupo de roles [Administración de organizaciones](organization-management-exchange-2013-help.md). Esto se debe a que cuando se instala Exchange, se realizan cambios en Active Directory y solo los administradores de Exchange, que son miembros del grupo de roles Administración de la organización, pueden efectuar dichos cambios. En la siguiente lista se muestran los cambios que se realizan:

  - Se crea un objeto del servidor en la partición de configuración **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Nombre de la organización\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Dominio raíz\>**.

  - Se agregan las siguientes entradas de control de acceso (ACE) al objeto de servidor dentro de la partición de configuración para el grupo de roles de instalación delegada:
    
      - Control total del objeto de servidor y sus objetos secundarios
    
      - Denegar la entrada de control de acceso para el derecho extendido Enviar como
    
      - Denegar la entrada de control de acceso para el derecho extendido Recibir como
    
      - Denegar permisos CreateChild y DeleteChild para objetos del Almacén de carpetas públicas de Exchange
    

    > [!NOTE]
    > Las carpetas públicas se administran en el nivel de la organización, por lo tanto, la creación y la eliminación de almacenes de carpetas públicas quedan restringidas a los administradores de Exchange.



  - La cuenta de equipo de Active Directory para el servidor se agrega al grupo Servidores de Exchange.

  - El servidor se agrega como un servidor aprovisionado en el Centro de administración de Exchange.

En empresas grandes, los encargados de instalar y configurar los servidores nuevos generalmente no son administradores de Exchange. Para habilitarlos para que puedan instalar Exchange, un administrador de Exchange puede *aprovisionar* el servidor en Active Directory. Cuando se aprovisiona un servidor, todos los cambios necesarios para que funcione el nuevo servidor de Exchange se realizan en Active Directory de forma independiente de la instalación real de Exchange en un equipo. Un administrador de Exchange puede aprovisionar un servidor nuevo en Active Directory horas o incluso días antes de que se instale Exchange en el equipo nuevo. Una vez que se ha aprovisionado un servidor, la persona que lleva a cabo la instalación solo debe ser miembro del grupo de roles [Configuración delegada](delegated-setup-exchange-2013-help.md) para instalar Exchange. El grupo de roles de instalación delegada solo permite a los miembros instalar servidores aprovisionados.

Tenga en cuenta lo siguiente cuando contemple emplear la instalación delegada:

  - Debe haber instalado al menos un servidor de Exchange 2013 para poder delegar la instalación de servidores adicionales. La persona que instala el primer servidor debe ser administrador de Exchange. Para obtener más información, vea [Lista de comprobación: instalación nueva de Exchange 2013](checklist-perform-a-new-installation-of-exchange-2013-exchange-2013-help.md).

  - Un usuario delegado no puede desinstalar un servidor de Exchange. Para desinstalar un servidor de Exchange, debe ser administrador de Exchange.

## ¿Cómo se aprovisiona un servidor de Exchange 2013?

Para aprovisionar un servidor para Exchange, debe usar la instalación de línea de comandos de Exchange 2013. Si no está muy familiarizado con la ventana de símbolo del sistema de Windows, no se preocupe. En este tema se indican los pasos exactos que debe llevar a cabo. Antes de empezar, le presentamos algunas aspectos que debe tener en cuenta:

  - Debe ser miembro del grupo de roles Administración de la organización para aprovisionar un servidor.

  - Debe contar con la última versión de Exchange 2013. Puede obtener el vínculo de descarga desde [Actualizaciones para Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

El comando que debe usar para aprovisionar el servidor depende de si se ejecuta el programa de instalación desde el equipo que está aprovisionando o si lo está ejecutando desde otro equipo. En los pasos siguientes elija el comando que coincida con la ubicación desde la que está ejecutando la instalación:

1.  Presione la tecla Windows + 'R' para abrir la ventana **Ejecutar**.

2.  En **Abrir**, escriba **cmd.exe** y luego presione Entrar para abrir un **Símbolo del sistema de Windows**.

3.  Cambie los directorios a la ubicación donde descargó y expandió los archivos de instalación de Exchange 2013. Si los archivos de instalación están ubicados en `C:\Downloads\Exchange 2013`, use el siguiente comando.
    
    ```powershell
    CD "C:\Downloads\Exchange 2013"
    ```

4.  Elija el comando que coincida con la ubicación en la que está ejecutando el programa de instalación:
    
      - **Si está ejecutando el programa de instalación en el equipo que se está aprovisionando**, ejecute el siguiente comando:
        
        ```powershell
        Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
        ```
    
      - **Si está ejecutando el programa de instalación en otro equipo**, ejecute el siguiente comando:
        
        ```powershell
        Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms
        ```

5.  Después de aprovisionar el servidor, debe asegurarse de que agregó los usuarios que deben poder instalar Exchange en servidores aprovisionados al grupo de roles de instalación delegada. Para obtener información sobre cómo agregar usuarios a un grupo de roles, vea [Add members to a role group](manage-role-group-members-exchange-2013-help.md).

Una vez que haya finalizado estos pasos, el equipo estará listo para la instalación de Exchange. Exchange 2013 puede instalarse en un servidor aprovisionado mediante los pasos descritos en [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para asegurarse de que el servidor se ha aprovisionado correctamente para Exchange, haga lo siguiente:

1.  Vaya a **Inicio** \> **Herramientas administrativas** y luego abra **Usuarios y equipos de Active Directory**.

2.  Seleccione **Grupos de seguridad de Microsoft Exchange**, haga doble clic en **Servidores Exchange** y luego seleccione la pestaña **Miembros**.

3.  En la pestaña **Miembros**, compruebe si el servidor que acaba de aprovisionar aparece como miembro del grupo de seguridad.

Si el servidor aparece como miembro del grupo de seguridad de servidores de Exchange significa que se ha aprovisionado correctamente. Cualquier persona que sea miembro del grupo de roles de instalación delegada ahora puede instalar Exchange en dicho servidor.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

