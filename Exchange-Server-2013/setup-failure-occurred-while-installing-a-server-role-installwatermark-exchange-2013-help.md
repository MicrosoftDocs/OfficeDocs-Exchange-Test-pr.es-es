---
title: 'Error de instalación al instalar un rol del servidor_InstallWatermark: Exchange 2013 Help'
TOCTitle: Error de instalación al instalar un rol del servidor_InstallWatermark
ms:assetid: ad89ebd5-f9bb-40c1-8811-09b145c2b341
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.installwatermark(v=EXCHG.150)
ms:contentKeyID: 48268553
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Error de instalación al instalar un rol del servidor\_InstallWatermark

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error de instalación anterior al instalar una función del servidor.

El programa de instalación de Exchange 2007 requiere que la instalación incorrecta de una función del servidor se repita correctamente, o se quite del proceso de instalación, para que puedan continuar las demás tareas de instalación.

Para resolver este problema, reinstale las funciones del servidor con errores o quítelas.

**Para reinstalar la función del servidor con errores desde la línea de comandos**

1.  Abra una ventana de símbolo del sistema y desplácese a los archivos de instalación.

2.  Ejecute el comando siguiente :
    
    ```powershell
    Setup /roles:<Failed Server Role>
    ```
    
    Haga una selección entre una o más de las siguientes funciones en una lista separada por comas:
    
    ClientAccess (o CA, o C) (Acceso de cliente)
    
    EdgeTransport (o ET, o E) (Transporte perimetral)
    

    > [!NOTE]
    > La función del servidor Transporte perimetral no puede coexistir con ninguna otra función del servidor en el mismo equipo.

    

    > [!NOTE]
    > Debe implementar el rol de servidor Transporte perimetral en la red perimetral y fuera del bosque de Active Directory.

    
    HubTransport (o HT, o H) (Transporte de concentradores)
    
    Mailbox (o MB, o M) (Buzón de correo)
    
    UnifiedMessaging (o UM, o U) (Mensajería unificada)
    
    ManagementTools (o MT, o T) (Herramientas de administración)
    

    > [!NOTE]
    > Si especifica ManagementTools, se instalará la Consola de administración de Exchange, los cmdlets de Exchange para el Shell de administración de Exchange, el archivo de Ayuda de Exchange, la herramienta Exchange Best Practices Analyzer y el ayudante para resolución de problemas de Exchange. Si instala cualquier otra función del servidor, las herramientas de administración se instalarán automáticamente.

    
    Por ejemplo, para agregar la función del servidor Transporte de concentradores a un servidor de buzones existente, escriba lo siguiente: **%LocalExchangeInstallationDir%\\bin\\Setup.com /role:HubTransport /Mode:Install**


> [!NOTE]
> Si se instaló correctamente cualquier función del servidor de Exchange Server&nbsp;2007, el Asistente para instalación se ejecutará en el modo de mantenimiento. Si no se instalaron de forma correcta funciones del servidor de Exchange 2007 anteriormente, el Asistente para instalación se iniciará en el punto en que se detuvo.



**Para usar el Asistente para instalación de Exchange Server 2007 en modo de mantenimiento para reinstalar la función del servidor con errores**

1.  Inicie sesión en el servidor en el que desea volver a instalar una función del servidor.

2.  Abra el Panel de control y haga doble clic en **Agregar o quitar programas**.

3.  En la página **Cambiar o quitar programas**, seleccione **Microsoft Exchange Server** y después haga clic en **Cambiar**.

4.  En el Asistente para instalación de Exchange Server 2007, en la página **Modo de mantenimiento de Exchange**, haga clic en **Siguiente**.

5.  En la página **Selección de función de servidor**, active las casillas de las funciones del servidor que desee instalar y después haga clic en **Siguiente**.
    

    > [!NOTE]
    > La función del servidor Transporte perimetral no puede coexistir con ninguna otra función del servidor en el mismo equipo.

    

    > [!NOTE]
    > Debe implementar el rol de servidor Transporte perimetral en la red perimetral y fuera del bosque de Active Directory.

    

    > [!NOTE]
    > Si selecciona Herramientas de administración, se instalará la Consola de administración de Exchange, los cmdlets de Exchange para el Shell de administración de Exchange y el archivo de Ayuda de Exchange. Las herramientas de administración se instalarán automáticamente si instala cualquier otra función de servidor.



6.  Si seleccionó **Servidor concentrador de transporte** y va a instalar Exchange 2007 en un bosque con una organización existente de Exchange Server 2003 o Exchange 2000 Server, en la página **Configuración del flujo de correo**, seleccione en la organización existente un servidor cabeza de puente que forme parte del grupo de enrutamiento de Exchange 2003 o Exchange 2000 para el que desee crear un conector de grupo de enrutamiento.

7.  En la página **Comprobaciones de la preparación**, compruebe el estado para determinar que las comprobaciones de requisitos previos de la organización y el servidor remoto hayan finalizado correctamente. Si finalizaron correctamente, haga clic en **Instalar** para instalar Exchange 2007.

8.  En la página **Finalización**, haga clic en **Finalizar**.

**Para usar el Asistente para instalación de Exchange Server 2007 para reinstalar la función del servidor con errores si no se instaló correctamente ninguna otra función del servidor antes**

1.  Siga las instrucciones en "Cómo realizar una instalación personalizada con el programa de instalación de Exchange Server 2007" ([https://go.microsoft.com/fwlink/?LinkId=86648](https://go.microsoft.com/fwlink/?linkid=86648)) en la documentación del producto de Exchange Server 2007.

**Para quitar la función del servidor con errores**

1.  Siga las instrucciones en "Como quitar funciones de servidor de Exchange 2007" ([https://go.microsoft.com/fwlink/?LinkId=86649](https://go.microsoft.com/fwlink/?linkid=86649)) en la documentación del producto de Exchange Server 2007.

## Para obtener más información

Para obtener más información acerca de cómo instalar Exchange 2007 en modo desatendido, consulte "Cómo instalar Exchange 2007 en modo desatendido" ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)).

