---
title: 'Uso Copias seguridad Windows Server hacer copias Exchange: Exchange 2013 Help'
TOCTitle: Usar Copias de seguridad de Windows Server para realizar copias de seguridad de Exchange
ms:assetid: 188a8291-0a41-4ca2-b6d2-94242e2b1ffc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876854(v=EXCHG.150)
ms:contentKeyID: 48267841
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar Copias de seguridad de Windows Server para realizar copias de seguridad de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-06-18_

Puede usar Copias de seguridad de Windows Server para realizar copias de seguridad y restauraciones de bases de datos de Exchange. Exchange incluye un nuevo complemento para Copias de seguridad de Windows Server que permite realizar copias de seguridad basadas en el servicio de instantáneas de volumen (VSS) de los datos de Exchange.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto, más el tiempo que se tarda en hacer una copia de seguridad de los datos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Recuperación de buzones" del tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - La característica Copia de seguridad de Windows Server debe instalarse en el equipo local.

  - Durante la operación de copia de seguridad, se ejecuta una comprobación de coherencia de los archivos de datos de Exchange para garantizar que los archivos se encuentren en buen estado y que puedan usarse en la recuperación. Si la comprobación de coherencia se realiza correctamente, los datos de Exchange estarán disponibles para la recuperación desde la copia de seguridad. Si se produce un error en la comprobación de coherencia, los datos de Exchange no estarán disponibles para la recuperación. Copias de seguridad de Windows Server ejecuta la comprobación de coherencia en la instantánea tomada para la copia de seguridad. Como resultado, antes de copiar los archivos de la instantánea a los medios de copia de seguridad, se conoce la coherencia de la copia de seguridad y se notifica al usuario acerca de los resultados de la comprobación de coherencia.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar Copias de seguridad de Windows Server para realizar copias de seguridad de Exchange

1.  Inicie Copias de seguridad de Windows Server.

2.  Seleccione **Copia de seguridad local**.

3.  En el panel Acciones, haga clic en **Hacer copia de seguridad una vez...** para iniciar el Asistente para hacer copia de seguridad una vez.

4.  En la página **Opciones de copia de seguridad**, seleccione **Opciones diferentes** y, a continuación, haga clic en **Siguiente**.

5.  En la página **Seleccionar configuración de copia de seguridad**, seleccione **Personalizada** y haga clic en **Siguiente**.

6.  En la página **Seleccionar elementos para copia de seguridad**, haga clic en **Agregar elementos** para seleccionar los volúmenes que se incluirán en la copia de seguridad y, a continuación, haga clic en **Aceptar**.
    

    > [!NOTE]
    > Elija volúmenes y no carpetas individuales. La única forma de realizar o restaurar una copia de seguridad en el nivel de aplicación es seleccionar un volumen completo.



7.  Haga clic en **Configuración avanzada**. En la pestaña **Exclusiones**, haga clic en **Agregar exclusión** para agregar los archivos o los tipos de archivos que quiere excluir de la copia de seguridad.
    

    > [!NOTE]
    > De manera predeterminada, los volúmenes que contienen componentes o aplicaciones del sistema operativo se incluyen en la copia de seguridad y no pueden excluirse.



8.  En la pestaña **Configuración de VSS**, seleccione **Copia de seguridad completa de VSS**, haga clic en **Aceptar** y, a continuación, haga clic en **Siguiente**.

9.  En la página **Especificar tipo de destino**, seleccione la ubicación en la que desea almacenar la copia de seguridad y, a continuación, haga clic en **Siguiente**.
    
      - Si elige **Unidades locales**, se muestra la página **Seleccionar destino de la copia de seguridad**. Seleccione una opción en la lista desplegable **Destino de la copia de seguridad** y, a continuación, haga clic en **Siguiente**.
    
      - Si elige **Carpeta compartida remota**, se muestra la página **Especificar carpeta remota**. Especifique una ruta UNC para los archivos de seguridad y configure las opciones de control de acceso. Elija **No heredar** si quiere que la copia de seguridad sea accesible solo a través de una cuenta específica. Indique un nombre de usuario y una contraseña para una cuenta de usuario que tenga permisos de escritura en el equipo que hospeda la carpeta remota y haga clic en **Aceptar**. O bien, elija **Heredar** si quiere que todo el que tenga acceso a la carpeta remota pueda tener acceso a la copia de seguridad. Haga clic en **Siguiente**.

10. En la página **Confirmación**, comprueba la configuración de la copia de seguridad y haga clic en **Copia de seguridad**.

11. En la página **Progreso de la copia de seguridad**, puede consultar el estado y el progreso de la operación de copia de seguridad.

12. Haga clic en **Cerrar** para salir de la página **Progreso de la copia de seguridad** en cualquier momento. Las copias de seguridad en curso continuarán ejecutándose en segundo plano.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha realizado una copia de seguridad correcta de los datos, siga estos pasos:

  - En el servidor en el que se ejecutó Copias de seguridad de Windows Server, se mostrará el estado de la última copia de seguridad, que debería ser Correcta. También puede comprobar que la copia de seguridad se completó correctamente en los registros de Copias de seguridad de Windows Server.

  - Abra el Visor de eventos y compruebe que se registró un evento de finalización de copia de seguridad en el registro de eventos de aplicaciones.

  - Ejecute el siguiente comando en el Shell de administración de Exchange para comprobar que se realizaron correctamente las copias de seguridad de todas las bases de datos de los volúmenes seleccionados:
    
        Get-MailboxDatabase -Server <ServerName> -Status | fl Name,*FullBackup
    
    Las propiedades *SnapshotLastFullBackup* y *LastFullBackup* de la base de datos indican cuándo se realizó la última copia de seguridad correcta y si era una copia de seguridad completa de VSS.

