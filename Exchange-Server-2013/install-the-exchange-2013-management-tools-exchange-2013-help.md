---
title: 'Instalar herramientas de administración de Exchange 2013: Exchange 2013 Help'
TOCTitle: Instalar las herramientas de administración de Exchange 2013
ms:assetid: 71fcbe4c-783b-4f77-aabb-a21aa7a4ef23
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232090(v=EXCHG.150)
ms:contentKeyID: 49116308
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Instalar las herramientas de administración de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-01-28_

Con las herramientas de administración de Microsoft Exchange Server 2013, puede configurar y administrar su organización de Exchange de forma remota. Las herramientas de administración de Exchange 2013 incluyen el Shell de administración de Exchange y el cuadro de herramientas de Exchange. En este tema se explica cómo puede utilizar Setup.exe o el modo de instalación desatendida para instalar las herramientas de administración de Exchange 2013.


> [!NOTE]
> No es necesario realizar este procedimiento para usar el Centro de Administración de Exchange (EAC) de forma remota. El EAC es una consola basada en web que se hospeda en equipos que ejecutan el rol de servidor Acceso de clientes de Exchange&nbsp;2013. Para obtener más información acerca del acceso remoto a EAC, consulte <A href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Centro de administración de Exchange en Exchange 2013</A>.



Para obtener más información acerca de la administración de Exchange 2013, consulte [Centro de administración de Exchange en Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md) y [Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\)).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos

  - Asegúrese de haber leído las notas de la versión antes de instalar Exchange 2013. Para obtener más información, consulte [Notas de la versión de Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - El equipo donde instale las herramientas de administración debe tener un sistema operativo admitido (como Windows Server 2012 o Windows 8), tener suficiente espacio en disco, formar parte de un dominio de Active Directory y cumplir con los demás requisitos. Para obtener información acerca de los requisitos del sistema, consulte [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Para ejecutar la configuración de Exchange 2013, debe instalar Microsoft .NET Framework 4.5, Windows Management Framework 3.0 y demás software requerido. Para comprender los requisitos previos para todos los roles de servidor, consulte [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el programa de instalación para instalar las herramientas de administración de Exchange 2013

1.  Inicie sesión en el equipo en el que desea instalar Exchange 2013.

2.  Desplácese a la ubicación de red de los archivos de instalación de Exchange 2013.

3.  Para iniciar el programa de instalación de Exchange 2013, haga doble clic en `Setup.exe`
    

    > [!IMPORTANT]
    > Si tienen habilitado el control de acceso del usuario (UAC), debe hacer clic con el botón secundario en <CODE>Setup.exe</CODE> y seleccionar <STRONG>Ejecutar como administrador</STRONG>.



4.  En la página **Buscar actualizaciones**, elija si desea que el programa de instalación se conecte a Internet y descargue las actualizaciones de seguridad y del producto para Exchange 2013. Si selecciona **Conectarse a Internet y buscar actualizaciones**, el programa de instalación descargará las actualizaciones y las aplicará antes de continuar. Si selecciona **No buscar actualizaciones por ahora**, podrá descargar e instalar las actualizaciones manualmente más tarde. Le recomendamos que descargue e instale las actualizaciones ahora. Haga clic en **Siguiente** para continuar.

5.  
    
    En la página **Introducción** comienza el proceso de instalar Exchange en la organización. Lo guiará por la instalación. Aparecerán varios vínculos a contenido útil para la implementación. Se recomienda visitar estos vínculos antes de continuar con la instalación. Haga clic en **Siguiente** para continuar.

6.  
    
    En la página **Contrato de licencia**, revise las condiciones del contrato de licencia del software. Si acepta los términos, seleccione **Acepto los términos del contrato de licencia** y, a continuación, haga clic en **Siguiente**.

7.  
    
    En la página **Configuración recomendada**, seleccione si desea utilizar la configuración recomendada. Si selecciona **Usar la configuración recomendada**, Exchange automáticamente enviará a Microsoft informes de error e información acerca del hardware del equipo y acerca de cómo usa usted Exchange. Si selecciona **No usar la configuración recomendada**, estas opciones permanecen deshabilitadas, pero usted puede habilitarlas en cualquier momento después de que se completa la instalación. Para obtener más información acerca de esta configuración y de cómo se utiliza la información que se envía a Microsoft, haga clic en **?**.

8.  
    
    En la página **Selección de función de servidor**, verifique que **Herramientas de administración** esté seleccionado.
    
    Seleccione **Instalar automáticamente las características y los roles de Windows Server necesarios para instalar Exchange Server** para que el Asistente para la instalación instale los requisitos previos necesarios de Windows. Es posible que deba reiniciar el equipo para completar la instalación de algunas características de Windows. Si no selecciona esta opción, deberá instalar las características de Windows manualmente.
    

    > [!NOTE]
    > Esta opción solo instala las características de Windows que requiere Exchange. Debe instalar otros requisitos previos manualmente. Para obtener más información, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</A>.

    
    Haga clic en **Siguiente** para continuar.

9.  En la página de **ubicación y espacio de la instalación**, acepte la ubicación de instalación predeterminada o haga clic en **Examinar** para elegir una ubicación nueva. Asegúrese de que tiene suficiente espacio en disco disponible en la ubicación donde desea instalar Exchange. Haga clic en **Siguiente** para continuar.

10. 
    
    Si se trata de la primera vez que ejecuta la configuración de Exchange 2013 de la organización, en la página **Organización de Exchange**, escriba un nombre para la organización de Exchange. El nombre de la organización de Exchange sólo puede contener los siguientes caracteres:
    
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

11. 
    
    En la página **Comprobaciones de la preparación**, compruebe el estado para determinar que las comprobaciones de requisitos previos de la organización y el servidor remoto hayan finalizado correctamente. Si no ha sido así, deberá resolver todos los errores detectados antes de poder instalar Exchange 2013. No es necesario que salga del programa de instalación para solucionar algunos de los errores en los requisitos previos. Después de resolver los errores detectados, haga clic en **Atrás** y, a continuación, en **Siguiente** para volver a ejecutar la comprobación de requisitos previos. Asegúrese de revisar también cualquier advertencia que se notifique. Si todas las comprobaciones de disponibilidad finalizaron correctamente, haga clic en **Siguiente** para instalar Exchange 2013.

12. 
    
    En la página **Finalización**, haga clic en **Finalizar**.

13. Reinicie el equipo después de que se haya completado Exchange 2013.

## Usar el modo de instalación desatendida para instalar las herramientas de administración de Exchange 2013

1.  Inicie una sesión en el equipo en el que desea instalar las herramientas de administración de Exchange 2013.

2.  Desplácese a la ubicación de red de los archivos de instalación de Exchange 2013.

3.  Ejecute el comando siguiente en el símbolo del sistema.
    

    > [!IMPORTANT]
    > Si tiene control de acceso de usuarios (UAC) habilitado, debe ejecutar <CODE>Setup.exe</CODE> desde un símbolo del sistema elevado.

    
    ```powershell
Setup.exe /Role:ManagementTools /IAcceptExchangeServerLicenseTerms
```

Para obtener más información, consulte [Instalar Exchange 2013 usando el modo desatendido](install-exchange-2013-using-unattended-mode-exchange-2013-help.md).

