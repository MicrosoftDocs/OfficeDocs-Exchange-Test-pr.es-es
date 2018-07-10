---
title: 'Usar Copias de seguridad de Windows Server para restaurar una copia de seguridad de Exchange: Exchange 2013 Help'
TOCTitle: Usar Copias de seguridad de Windows Server para restaurar una copia de seguridad de Exchange
ms:assetid: 2d0f31dc-eb32-451a-8852-591269026506
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876864(v=EXCHG.150)
ms:contentKeyID: 48267937
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar Copias de seguridad de Windows Server para restaurar una copia de seguridad de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-06-18_

Puede usar Copias de seguridad de Windows Server para realizar copias de seguridad y restauraciones de bases de datos de Exchange. Exchange incluye un nuevo complemento para Copias de seguridad de Windows Server que permite realizar y restaurar copias de seguridad basadas en el servicio de instantáneas de volumen (VSS) de los datos de Exchange. Para obtener más información, consulte [Uso de copias de seguridad de Windows Server para realizar copias de seguridad y restaurar datos de Exchange](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto, más el tiempo necesario para restaurar los datos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Recuperación de buzones" del tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - La característica Copia de seguridad de Windows Server debe instalarse en el equipo local.

  - Cuando una base de datos se restaura a su ubicación original, puede quedar en un estado de cierre incorrecto y en condiciones en que el sistema la pueda montar. Cuando se restaura en una ubicación alternativa (por ejemplo, al prepararse para usar la base de datos de recuperación), la base de datos debe ponerse manualmente en estado de cierre correcto mediante las Utilidades de base de datos de Exchange (Eseutil.exe).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar Copias de seguridad de Windows Server para restaurar una copia de seguridad de Exchange

1.  Inicie Copias de seguridad de Windows Server.

2.  Seleccione **Copia de seguridad local**.

3.  En el panel Acciones, haga clic en **Recuperar...** para iniciar el Asistente para recuperación.

4.  En la página **Introducción**, realice una de las acciones siguientes:
    
      - Si la copia de seguridad de los datos que se están recuperando se realizó en el servidor local, seleccione **Este servidor (nombreservidor)** y, a continuación, haga clic en **Siguiente**.
    
      - Si los datos que se están recuperando provienen de otro servidor, o si la copia de seguridad que se está recuperando se encuentra en otro equipo, seleccione **Otro servidor** y, a continuación, haga clic en **Siguiente**. En la página **Especificar tipo de ubicación**, seleccione **Unidades locales** o **Carpeta compartida remota** y, a continuación, haga clic en **Siguiente**. Si selecciona **Unidades locales**, elija la unidad que contenga la copia de seguridad en la página **Seleccionar la ubicación de copia de seguridad** y, a continuación, haga clic en **Siguiente**. Si selecciona **Carpeta compartida remota**, escriba la ruta de UNC para los datos de la copia de seguridad en la página **Especificar carpeta remota** y, a continuación, haga clic en **Siguiente**.

5.  En la página **Seleccionar fecha de copia de seguridad**, seleccione la fecha y la hora de la copia de seguridad que desee recuperar y, a continuación, haga clic en **Siguiente**.

6.  En la página **Seleccionar tipo de recuperación**, seleccione **Aplicaciones** y, a continuación, haga clic en **Siguiente**.
    

    > [!NOTE]
    > Si la opción <STRONG>Aplicaciones</STRONG> no está disponible, indica que la copia de seguridad seleccionada para restaurar era una copia de seguridad de nivel de carpeta y no una copia de seguridad de nivel de volumen. Debe realizar copias de seguridad en el nivel de volumen cuando realice copias de seguridad de los datos de Exchange con Copias de seguridad de Windows Server.



7.  En la página **Seleccionar aplicación**, compruebe que Exchange esté seleccionado en el campo **Aplicaciones**. Haga clic en **Ver detalles** para ver los componentes de las copias de seguridad de la aplicación. Si la copia de seguridad que está recuperando es la más reciente, se muestra la casilla **No realizar una recuperación de puesta al día de la base de datos de la aplicación**. Active esta casilla si desea evitar que Copias de seguridad de Windows Server aplique la base de datos que se está recuperando, confirmando todos los registros de transacciones sin confirmar. Haga clic en **Siguiente**.

8.  En la página **Especificar opciones de recuperación**, especifique dónde quiere recuperar los datos y, a continuación, haga clic en **Siguiente**:
    
      - Elija **Recuperar en la ubicación original** si quiere restaurar los datos de Exchange directamente en su ubicación original. Si usa esta opción, no puede elegir qué bases de datos se restauran; se restaurarán todas las bases de datos con copia de seguridad en el volumen en sus ubicaciones originales.
    
      - Seleccione **Recuperar en otra ubicación** para restaurar las bases de datos individuales y sus archivos en una ubicación especificada. Haga clic en **Examinar** para especificar una ubicación alternativa. Si usa esta opción, puede elegir qué bases de datos se restauran. Una vez que se hayan recuperado, los archivos de datos se moverán a una base de datos de recuperación y se devolverán manualmente a su ubicación original, o se montarán en otro lugar de la organización de Exchange mediante [Portabilidad de bases de datos](database-portability-exchange-2013-help.md). Cuando restaure bases de datos en una ubicación alternativa, la base de datos restaurada se encontrará en estado de cierre incorrecto. Cuando haya finalizado el proceso de restauración, tendrá que poner manualmente la base de datos en un estado de cierre correcto mediante Eseutil.exe.

9.  En la página **Confirmación**, revise la configuración de recuperación y haga clic en **Recuperar**.

10. En la página **Progreso de la recuperación**, puede ver el estado y el progreso de la operación de recuperación.

11. Cuando haya finalizado la operación de recuperación, haga clic en **Cerrar**.

## ¿Cómo saber si el proceso se ha completado correctamente?

La página **Progreso de la recuperación** indicará si el proceso de recuperación finalizó correctamente. Para comprobar que los datos se restauraron correctamente, siga estos pasos:

  - Examine el directorio de destino de la copia de seguridad y compruebe que los datos restaurados existan.

  - En el servidor en el que se ejecutó Windows Server Backup, compruebe que el trabajo se realizó con éxito verificando los archivos de copia de seguridad.

  - Abra el Visor de eventos y compruebe que se registró un evento de finalización de restauración en el registro de eventos de aplicaciones.

