---
title: 'Instalar el rol de transporte perimetral de Exchange 2013 mediante el asistente de instalación: Exchange 2013 Help'
TOCTitle: Instalar el rol de transporte perimetral de Exchange 2013 mediante el asistente de instalación
ms:assetid: b8e51b0b-201e-4c64-92c8-3ac0db04b6e2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn635117(v=EXCHG.150)
ms:contentKeyID: 61204111
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Instalar el rol de transporte perimetral de Exchange 2013 mediante el asistente de instalación

 

_**Se aplica a:**Exchange Server, Exchange Server 2013_

_**Última modificación del tema:**2014-06-19_

En este tema se explica cómo usar el asistente para instalación de Microsoft Exchange Server 2013 para instalar el rol de servidor de transporte perimetral de Exchange 2013 en un equipo. El rol de transporte perimetral está disponible con Exchange 2013 Service Pack 1 (SP1) o posterior. Para obtener más información acerca de la planificación e implementación de Exchange 2013, consulte [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Se recomienda instalar el rol de transporte perimetral en una red perimetral fuera del bosque interno de Active Directory de su organización. Aunque puede instalar el rol del servidor transporte perimetral en un equipo unido a un dominio, al hacerlo solo se habilita la gestión de las características y configuración de Windows relativa al dominio. El propio rol de transporte perimetral no usa Active Directory. En su lugar usa la característica Active Directory Lightweight Directory Services (AD LDS) Windows para almacenar la información de la configuración y del destinatario. Para obtener más información acerca del rol de transporte perimetral, consulte [Servidores de transporte perimetral](edge-transport-servers-exchange-2013-help.md).

Si desea instalar los roles de buzón o de acceso de cliente de Exchange 2013 en un equipo, consulte [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). El rol de transporte perimetral no se puede instalar en el mismo equipo que las funciones de servidor de buzón o de acceso de cliente.


> [!TIP]
> ¿Conoce el asistente para la implementación de Exchange Server? Es una herramienta en línea gratuita que le ayuda a implementar rápidamente Exchange 2013 en su organización realizando unas cuantas preguntas y creando una lista de comprobación de implementación personalizada solo para usted. Si desea más información, vaya a <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Asistente para la implementación de Exchange Server</A>.



Para obtener información acerca de las tareas posteriores a la instalación, consulte [Tareas posteriores a la instalación de Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 40 minutos

  - Asegúrese de haber leído las notas de la versión antes de instalar Exchange 2013. Para obtener más información, consulte [Notas de la versión de Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - El equipo en el que se instale Exchange 2013 debe contar con un sistema operativo compatible (como Windows Server 2008 R2 con SP1, Windows Server 2012 R2 o Windows Server 2012), disponer de suficiente espacio en el disco y satisfacer otros requisitos. Para obtener información acerca de los requisitos del sistema, consulte [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Para ejecutar la instalación de Exchange 2013, debe instalar Microsoft .NET Framework 4.5, Windows Management Framework y otro software necesario. Para comprender los requisitos previos para todos los roles de servidor, consulte [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Debe configurar el sufijo DNS principal en el equipo. Por ejemplo, si el nombre de dominio completo del equipo es edge.contoso.com, el sufijo DNS del equipo es contoso.com. Para obtener más información, consulte [Falta el sufijo DNS principal](primary-dns-suffix-is-missing-exchange-2013-help.md).

  - Es necesario actualizar los servidores de Transporte de concentradores de Exchange 2007 and Exchange 2010 antes de poder crear una suscripción de EdgeSync entre ellos y el servidor de transporte perimetral de Exchange 2013. Si no se instala esta actualización, la suscripción de EdgeSync no funcionará correctamente. Para obtener más información, consulte la sección "Escenarios de coexistencia compatibles" en [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Asegúrese de que la cuenta que utiliza es un miembro del grupo Administradores local del equipo en el que está instalando el rol de transporte perimetral.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Después de instalar Exchange en un servidor, no debe modificar el nombre del servidor. No se admite el cambio de nombre de un servidor después de haber instalado el rol del servidor de Exchange.



## Instalar Exchange Server 2013


> [!NOTE]
> Para descargarla última versión de Exchange&nbsp;2013, consulte <A href="updates-for-exchange-2013-exchange-2013-help.md">Actualizaciones para Exchange 2013</A>.



1.  Inicie sesión en el equipo en el que desea instalar Exchange 2013.

2.  Desplácese a la ubicación de red de los archivos de instalación de Exchange 2013.

3.  Para iniciar el programa de instalación de Exchange 2013, haga doble clic en `Setup.exe`
    

    > [!IMPORTANT]
    > Si se ha habilitado el control de acceso del usuario (UAC), debe hacer clic con el botón secundario en <CODE>Setup.exe</CODE> y seleccionar <STRONG>Ejecutar como administrador</STRONG>.



4.  En la página **Buscar actualizaciones**, elija si desea que el programa de instalación se conecte a Internet y descargue las actualizaciones de seguridad y del producto para Exchange 2013. Si selecciona **Conectarse a Internet y buscar actualizaciones**, el programa de instalación descargará las actualizaciones y las aplicará antes de continuar. Si selecciona **No buscar actualizaciones por ahora**, podrá descargar e instalar las actualizaciones manualmente más tarde. Le recomendamos que descargue e instale las actualizaciones ahora. Haga clic en **Siguiente** para continuar.

5.  
    
    En la página **Introducción** comienza el proceso de instalación de Exchange en la organización. Le guiará a través de la instalación. Aparecerán varios vínculos a contenido útil para la implementación. Se recomienda visitar estos vínculos antes de continuar con la instalación. Haga clic en **Siguiente** para continuar.

6.  
    
    En la página **Contrato de licencia**, revise las condiciones del contrato de licencia del software. Si acepta los términos, seleccione **Acepto los términos del contrato de licencia** y, a continuación, haga clic en **Siguiente**.

7.  
    
    En la página **Configuración recomendada**, seleccione si desea utilizar la configuración recomendada. Si selecciona **Usar la configuración recomendada**, Exchange enviará automáticamente a Microsoft informes de error e información acerca del hardware del equipo y sobre cómo se usa Exchange. Si selecciona **No usar la configuración recomendada**, estas opciones permanecen deshabilitadas, pero usted puede habilitarlas en cualquier momento después de que se complete la instalación. Para obtener más información sobre esta configuración y sobre cómo se utiliza la información que se envía a Microsoft, haga clic en **?**.

8.  
    
    En la página **Selección de rol de servidor**, elija **Transporte perimetral**. Recuerde que no puede agregar los roles de servidor de buzón o de acceso de cliente a un equipo que tenga instalado el rol de transporte perimetral. Las herramientas de administración se instalan automáticamente si instala cualquier rol de servidor.
    
    Seleccione **Instalar automáticamente las características y los roles de Windows Server necesarios para instalar Exchange Server** para que el asistente para instalación instale los requisitos previos necesarios de Windows. Es posible que deba reiniciar el equipo para completar la instalación de algunas características de Windows. Si no selecciona esta opción, deberá instalar las características de Windowsmanualmente.
    

    > [!NOTE]
    > Esta opción solo instala las características de Windowsque requiere Exchange. Debe instalar otros requisitos previos manualmente. Para obtener más información, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</A>.

    
    Haga clic en **Siguiente** para continuar.

9.  En la página **Ubicación y espacio de instalación**, acepte la ubicación de instalación predeterminada o haga clic en **Examinar** para elegir una nueva ubicación. Asegúrese de que tiene suficiente espacio en disco disponible en la ubicación donde desea instalar Exchange. Haga clic en **Siguiente** para continuar.

10. 
    
    En la página **Comprobaciones de disponibilidad**, compruebe el estado para determinar que las comprobaciones de requisitos previos de la organización y el rol del servidor finalizaron correctamente. Si no fue así, deberá resolver todos los errores detectados para poder instalar Exchange 2013. No es necesario salir del programa de instalación para resolver algunos de los errores relacionados con los requisitos previos. Después de resolver los errores detectados, haga clic en **Atrás** y, a continuación, en **Siguiente** para volver a ejecutar la comprobación de requisitos previos. Asegúrese de revisar también las advertencias que se hayan detectado. Si todas las comprobaciones de disponibilidad finalizaron correctamente, haga clic en **Siguiente** para instalar Exchange 2013.

11. 
    
    En la página **Finalización**, haga clic en **Finalizar**.

12. Reinicie el equipo después de que se haya completado Exchange 2013.

13. Complete la implementación realizando las tareas indicadas en [Tareas posteriores a la instalación de Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## ¿Cómo puedo saber si el proceso se ha completado correctamente?

Para comprobar que ha instalado correctamente Exchange 2013, consulte [Comprobar una instalación de Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

