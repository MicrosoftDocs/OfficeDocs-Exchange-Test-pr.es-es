---
title: 'Instalar Exchange 2013 utilizando el asistente de configuración: Exchange 2013 Help'
TOCTitle: Instalar Exchange 2013 utilizando el asistente de configuración
ms:assetid: da690d47-3384-4430-a69e-0cd4d3bf80a7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124778(v=EXCHG.150)
ms:contentKeyID: 48268753
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.ExSetupUI.SetupWizardForm.IntroductionPage
ms.translationtype: HT
---

# Instalar Exchange 2013 utilizando el asistente de configuración

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-06-19_

En este tema se explica cómo usar el asistente para instalación de Microsoft Exchange Server 2013 para instalar los roles de buzón de correo y de acceso de cliente de Exchange 2013 en un equipo. Para obtener más información acerca de la planificación e implementación de Exchange 2013, vea [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Si quiere instalar el rol de transporte perimetral de Exchange 2013 en un equipo, vea [Instalar el rol de transporte perimetral de Exchange 2013 mediante el asistente de instalación](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md). El rol de transporte perimetral no se puede instalar en el mismo equipo que las funciones de servidor de buzón o de acceso de cliente.


> [!TIP]
> ¿Conoce el asistente para la implementación de Exchange Server? Es una herramienta en línea gratuita que le ayuda a implementar rápidamente Exchange 2013 en su organización realizando unas cuantas preguntas y creando una lista de comprobación de implementación personalizada solo para usted. Si desea más información, vaya a <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Asistente para la implementación de Exchange Server</A>.




> [!NOTE]
> Después de instalar los roles del servidor en un equipo que ejecute Exchange&nbsp;2013, no puede usar el Asistente para instalación de Exchange&nbsp;2013 para agregar roles de servidor adicionales a este equipo. Si desea agregar más roles de servidor a un equipo, debe usar Agregar o quitar programas en el Panel de control o usar Setup.exe en una ventana de símbolo del sistema.



Para obtener información acerca de las tareas posteriores a la instalación, consulte [Tareas posteriores a la instalación de Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 60 minutos

  - Asegúrese de haber leído las notas de la versión antes de instalar Exchange 2013. Para obtener más información, vea [Notas de la versión de Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Cada organización requiere, como mínimo, un servidor de acceso de cliente y un servidor de buzones en el bosque de Active Directory. Además, cada sitio de Active Directory que contiene un servidor de buzones deberá también contener, como mínimo, un servidor de acceso de cliente. Si separa sus roles de servidor, le recomendamos instalar el rol del servidor de buzones primero.

  - El equipo donde instale Exchange 2013 debe tener un sistema operativo compatible (como Windows Server 2008 R2 con Service Pack 1 (SP1) o Windows Server 2012) y suficiente espacio en disco, y tiene que ser miembro de un dominio de Active Directory. También tiene que cumplir otros requisitos. Para obtener información acerca de los requisitos del sistema, consulte [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Para ejecutar la instalación de Exchange 2013, debe instalar Microsoft .NET Framework 4.5, Windows Management Framework 3.0 y otro software necesario. Para comprender los requisitos previos para todos los roles de servidor, consulte [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Debe asegurarse de que la cuenta que use tenga delegada la pertenencia al grupo Administradores de esquema, si no ha preparado previamente el esquema de Active Directory. Si va a instalar el primer servidor de Exchange 2013 en la organización, la cuenta que use deberá pertenecer al grupo Administradores de empresa. Si ya ha preparado el esquema y no va a instalar el primer servidor de Exchange 2013 en la organización, la cuenta que use deberá ser miembro del grupo de roles de administración de la organización de Exchange 2013.
    
    Los administradores que pertenecen al grupo de roles de configuración delegada pueden implementar servidores de Exchange 2013 que ya han sido aprovisionados por un miembro del grupo de roles de administración de la organización.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Después de instalar Exchange en un servidor, no debe modificar el nombre del servidor. No se admite el cambio de nombre de un servidor después de haber instalado el rol del servidor de Exchange.



## Instalar Exchange Server 2013

Si va a instalar el primer servidor Exchange 2013 en la organización y no ha completado los pasos de preparación de Active Directory, la cuenta que use deberá pertenecer al grupo Administradores de empresa. Si no ha preparado el esquema de Active Directory con antelación, dicha cuenta también deberá ser miembro del grupo Administradores de esquema. Para obtener información acerca de cómo preparar Active Directory para Exchange 2013, consulte [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md). Si ha completado el esquema y los pasos de preparación de Active Directory, la cuenta que use debe ser miembro del grupo de roles de administración de instalación delegada o del grupo de roles de administración de organización.


> [!NOTE]
> Para descargarla última versión de Exchange&nbsp;2013, consulte <A href="updates-for-exchange-2013-exchange-2013-help.md">Actualizaciones para Exchange 2013</A>.



1.  Inicie sesión en el equipo en el que desea instalar Exchange 2013.

2.  Desplácese a la ubicación de red de los archivos de instalación de Exchange 2013.

3.  Para iniciar el programa de instalación de Exchange 2013, haga doble clic en `Setup.exe`
    

    > [!IMPORTANT]
    > Si se ha habilitado el control de acceso del usuario (UAC), debe hacer clic con el botón secundario en <CODE>Setup.exe</CODE> y seleccionar <STRONG>Ejecutar como administrador</STRONG>.



4.  En la página **Buscar actualizaciones**, elija si desea que el programa de instalación se conecte a Internet y descargue las actualizaciones de seguridad y del producto para Exchange 2013. Si selecciona **Conectarse a Internet y buscar actualizaciones**, el programa de instalación descargará las actualizaciones y las aplicará antes de continuar. Si selecciona **No buscar actualizaciones por ahora**, podrá descargar e instalar las actualizaciones manualmente más tarde. Le recomendamos que descargue e instale las actualizaciones ahora. Haga clic en **Siguiente** para continuar.

5.  
    
    En la página **Introducción** comienza el proceso de instalar Exchange en la organización. Lo guiará por la instalación. Aparecerán varios vínculos a contenido útil para la implementación. Se recomienda visitar estos vínculos antes de continuar con la instalación. Haga clic en **Siguiente** para continuar.

6.  
    
    En la página **Contrato de licencia**, revise las condiciones del contrato de licencia del software. Si acepta los términos, seleccione **Acepto los términos del contrato de licencia** y, a continuación, haga clic en **Siguiente**.

7.  
    
    En la página **Configuración recomendada**, seleccione si desea utilizar la configuración recomendada. Si selecciona **Usar la configuración recomendada**, Exchange enviará automáticamente a Microsoft informes de error e información acerca del hardware del equipo y sobre cómo se usa Exchange. Si selecciona **No usar la configuración recomendada**, estas opciones permanecen deshabilitadas, pero usted puede habilitarlas en cualquier momento después de que se completa la instalación. Para obtener más información acerca de esta configuración y de cómo se utiliza la información que se envía a Microsoft, haga clic en **?**.

8.  
    
    En la página de **selección del rol de servidor**, elija si desea instalar el **rol de buzones de correo**, el **rol de acceso de cliente**, ambos roles o solo el de **herramientas de administración** en el equipo. Puede agregar funciones de servidor adicionales si opta por no instalarlas durante esta instalación. Una organización debe tener al menos un rol de buzón y un rol de servidor de acceso de cliente instalados. Se pueden instalar en el mismo equipo o en equipos diferentes. Las herramientas de administración se instalan automáticamente si instala cualquier rol de servidor.
    
    Seleccione **Instalar automáticamente las características y los roles de Windows Server necesarios para instalar Exchange Server** para que el asistente para instalación instale los requisitos previos necesarios de Windows. Es posible que deba reiniciar el equipo para completar la instalación de algunas características de Windows. Si no selecciona esta opción, deberá instalar las características de Windowsmanualmente.
    

    > [!NOTE]
    > Esta opción solo instala las características de Windowsque requiere Exchange. Debe instalar otros requisitos previos manualmente. Para obtener más información, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</A>.

    
    Haga clic en **Siguiente** para continuar.

9.  En la página de **ubicación y espacio de la instalación**, acepte la ubicación de instalación predeterminada o haga clic en **Examinar** para elegir una ubicación nueva. Asegúrese de que tiene suficiente espacio en disco disponible en la ubicación donde desea instalar Exchange. Haga clic en **Siguiente** para continuar.

10. 
    
    Si se trata del primer servidor de Exchange de la organización, en la página **Organización de Exchange**, escriba un nombre para la organización de Exchange. El nombre de la organización de Exchange sólo puede contener los siguientes caracteres:
    
      - De la A a la Z
    
      - de la a a la z
    
      - De 0 a 9
    
      - Espacio (menos en posiciones delantera o trasera)
    
      - Guión o signo menos
        

        > [!NOTE]
        > El nombre de la organización no puede contener más de 64 caracteres. El nombre de la organización no se puede dejar en blanco.

    
    Si desea utilizar el modelo de permisos divididos de Active Directory, seleccione **Aplicar el modelo de seguridad de permisos divididos de Active Directory a la organización de Exchange**.
    

    > [!WARNING]
    > En la mayoría de las organizaciones no es necesario aplicar el modelo de permisos divididos de Active Directory. Si necesita separar la administración de las entidades de seguridad de Active Directory de la configuración de Exchange, elija el modelo de permisos divididos de control de acceso basado en roles (RBAC). Para obtener más información, haga clic en <STRONG>?</STRONG>.

    
    Haga clic en **Siguiente** para continuar.

11. Si instala el rol de buzones de correo, en la página **Configuración de protección de malware**, elija si desea habilitar o deshabilitar el análisis de malware. Si deshabilita la detección de malware, podrá habilitarla en el futuro. Haga clic en **Siguiente** para continuar.

12. 
    
    En la página **Comprobaciones de la preparación**, compruebe el estado para determinar que las comprobaciones de requisitos previos de la organización y el servidor remoto hayan finalizado correctamente. Si no ha sido así, deberá resolver todos los errores detectados antes de poder instalar Exchange 2013. No es necesario salir del programa de instalación para resolver algunos de los errores relacionados con los requisitos previos. Después de resolver los errores detectados, haga clic en **Atrás** y, a continuación, en **Siguiente** para volver a ejecutar la comprobación de requisitos previos. Asegúrese de revisar también las advertencias que se hayan detectado. Si todas las comprobaciones de disponibilidad finalizaron correctamente, haga clic en **Siguiente** para instalar Exchange 2013.

13. 
    
    En la página **Finalización**, haga clic en **Finalizar**.

14. Reinicie el equipo después de que se haya completado Exchange 2013.

15. Complete la implementación realizando las tareas indicadas en [Tareas posteriores a la instalación de Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha instalado Exchange 2013 correctamente, consulte [Comprobar una instalación de Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

