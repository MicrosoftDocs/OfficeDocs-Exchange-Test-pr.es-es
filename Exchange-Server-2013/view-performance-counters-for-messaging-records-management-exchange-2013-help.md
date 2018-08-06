---
title: 'Ver contador rendimiento para administrar registro mensaje: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Ver los contadores de rendimiento para la administración de registros de mensajes
ms:assetid: ec374d31-2797-4f8b-8c96-3839d01a662c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb397227(v=EXCHG.150)
ms:contentKeyID: 51406569
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ver los contadores de rendimiento para la administración de registros de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2009-12-09_

Puede usar el Monitor de confiabilidad y rendimiento (Perfmon.exe) de Windows para seleccionar y ver los contadores de rendimiento correspondientes a la administración de registros de mensajería (MRM). Al utilizar los contadores de rendimiento, podrá supervisar el Asistente para carpetas administradas mientras este ejecuta procesos de MRM que consumen muchos recursos.

Para obtener una lista de los contadores de rendimiento para MRM, consulte [Contadores de rendimiento para la administración de registros de mensajes](performance-counters-for-messaging-records-management-exchange-2013-help.md).

¿Está buscando otras tareas relacionadas con la supervisión de MRM? Consulte [Administración de registros de seguimiento de mensajería](monitoring-messaging-records-management-exchange-2013-help.md).

## Usar el Monitor de confiabilidad y rendimiento de Windows para ver contadores de rendimiento de MRM

Para ejecutar este procedimiento, la cuenta que use debe tener delegada la pertenencia al grupo Administradores local.

1.  Para iniciar el Monitor de confiabilidad y rendimiento de Windows, haga clic en **Iniciar**, haga clic en **Ejecutar** y, a continuación, escriba **perfmon**.

2.  En el árbol de la consola, vaya a **Herramientas de supervisión** \> **Monitor de rendimiento**.

3.  En la barra de herramientas, haga clic en el botón "más" (+). Aparecerá el cuadro de diálogo **Agregar contadores**.

4.  En la lista **Seleccionar contador de equipo**, elija una de las siguientes opciones:
    
      - Si está llevando a cabo este procedimiento en un equipo local, seleccione **\<Equipo local\>**. Ésa es la selección predeterminada.
    
      - Si realiza este procedimiento de forma remota, seleccione el servidor que desea supervisar.

5.  En la lista de contadores de rendimiento, expanda **Asistentes de Microsoft Exchange: por base de datos** o el **Asistente para carpetas administradas de MSExchange**.

6.  Seleccione los contadores de rendimiento que desea supervisar.

7.  En el caso de los contadores de rendimiento que hay en **Asistentes de Microsoft Exchange: por base de datos**, para ver los contadores de todas las bases de datos de buzones, en **Instancias del objeto seleccionado**, haga clic en **Todas las instancias**. O bien, para especificar una o más bases de datos, seleccione instancias de la lista.

8.  Para agregar los contadores seleccionados para que aparezcan en el Monitor de confiabilidad y rendimiento de Windows, y para empezar a recopilar datos de rendimiento, haga clic en **Agregar**.

