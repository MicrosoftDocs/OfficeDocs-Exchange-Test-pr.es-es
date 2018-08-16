---
title: 'Actualmente hay mensajes en una o varias colas'
TOCTitle: Actualmente hay mensajes en una o varias colas_MessagesInQueue
ms:assetid: 3ffcdc7e-c1b7-49a7-8e5f-b30c0397908d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.messagesinqueue(v=EXCHG.150)
ms:contentKeyID: 48268032
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Actualmente hay mensajes en una o varias colas\_MessagesInQueue

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

La instalación de Microsoft® Exchange Server 2007 muestra esta advertencia porque al intentar desinstalar una función de transporte podría provocar una pérdida de datos en la cola de transporte.

La instalación de Exchange 2007 comprueba para asegurarse que las colas de transporte están vacías antes de eliminar las funciones asociadas con la administración de esas colas.

Si elimina las funciones de transporte antes de la entrega de los mensajes que están todavía en las colas de transporte, puede que esos mensajes se conserven ahí indefinidamente.

Para resolver este problema, inspeccione las colas a las que se ha hecho referencia para asegurarse de que están libres de mensajes antes de continuar con la instalación.

**Para ver el contenido de una cola**

1.  Abra la Consola de administración de Exchange.

2.  En el árbol de consola, haga clic en **Cuadro de herramientas**.

3.  En el panel de resultados, haga clic en **Visor de cola de Exchange**.

4.  En el panel de acciones, haga clic en **Abrir herramienta**.

5.  En el Visor de cola, haga clic en la ficha **Colas**. Se muestra una lista de todas las colas del servidor al que está conectado.

6.  Haga clic con el botón secundario en la cola que desea y seleccione **Propiedades** para ver las propiedades de la cola.

**Para ver los mensajes de una cola**

1.  Siga los pasos 1 a 4.

2.  En el Visor de cola, haga clic en la ficha **Mensajes**. Se muestra una lista de todos los mensajes del servidor al que está conectado. Para ajustar la vista a una sola cola, haga clic en la ficha **Colas**, haga doble clic en el nombre de la cola, y luego haga clic en la ficha Servidor\\Cola que aparece.

3.  Para ver información detallada sobre un mensaje, seleccione el mensaje y después haga clic en **Propiedades** en el panel de acciones.

