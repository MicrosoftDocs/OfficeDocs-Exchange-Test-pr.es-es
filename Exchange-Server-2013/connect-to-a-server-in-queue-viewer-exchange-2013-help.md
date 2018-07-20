---
title: 'Conectar a un servidor en el visor de cola: Exchange 2013 Help'
TOCTitle: Conectar a un servidor en el visor de cola
ms:assetid: 6c1ad574-9ab5-4dcc-9398-ec10eca4fd11
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998669(v=EXCHG.150)
ms:contentKeyID: 49895692
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectar a un servidor en el visor de cola

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

El uso del Visor de cola en el cuadro de herramientas de Exchange de un servidor de Microsoft Exchange Server 2013 ubicado dentro de la organización de Exchange permite conectarse a otros servidores de buzones. De forma predeterminada, cuando se abre el Visor de cola en un servidor de buzones, el Visor se conecta a la base de datos en cola del servidor local. No obstante, puede iniciar más de una instancia del Visor de cola de modo que cada instancia se concentre en un servidor diferente. También puede organizar las ventanas del Visor de cola en mosaico para poder supervisar con mayor facilidad más de un servidor de buzones a la vez.

Asimismo, puede especificar el servidor que PowerShell en remoto usa para ejecutar las tareas especificadas en el Visor de cola. Este servidor no tiene que coincidir con el servidor remoto que administre en el Visor de cola.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Colas" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Los procedimientos descritos en este tema no se aplican a los servidores de transporte perimetral. Cuando usa el Visor de cola en un servidor Transporte perimetral, no puede cambiar el foco de la herramienta.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el cuadro de herramientas de Exchange para especificar el servidor que desea administrar en el Visor de cola

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange Server 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **Herramientas de flujo de correo**, haga doble clic en **Visor de cola**.

3.  En el panel de acciones, haga clic en **Conectar al servidor**.

4.  En la ventana **Conectar al servidor**, haga clic en **Examinar** para ver una lista de los servidores de buzones disponibles.

5.  En la ventana **Seleccionar servidor de Exchange**, seleccione un servidor de buzones. Para buscar un servidor de buzones, utilice uno de los siguientes procedimientos:
    
      - Escriba el nombre exacto del servidor o las primeras letras del nombre del servidor en el campo **Buscar** y, a continuación, haga clic en **Buscar ahora**. Seleccione un servidor en el panel de resultados.
    
      - Seleccione el menú **Ver** y, a continuación, haga clic en **Mostrar filtro**. En las columnas **Nombre** o **Versión**, haga clic en el icono de filtro y, a continuación, seleccione el operador de filtro. Especifique el criterio de filtro en el campo **Escribir texto aquí**. Presione ENTRAR. Seleccione un servidor en el panel de resultados.

6.  Haga clic en **Aceptar** para cerrar la ventana **Seleccionar servidor de Exchange**.

7.  Una vez seleccionado un servidor, en la ventana **Conectar al servidor**, active la casilla **Establecer como servidor predeterminado** si desea que el Visor de cola se centre primero en este servidor cuando se abra.

8.  En la ventana **Conectar al servidor**, haga clic en **Conectar**.

## Usar el cuadro de herramientas de Exchange para especificar el servidor que utiliza el Visor de cola para ejecutar PowerShell en remoto

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange Server 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **Herramientas de flujo de correo**, haga doble clic en **Visor de cola**.

3.  En el panel de acciones, haga clic en **Propiedades**.

4.  En el cuadro de diálogo **Visor de cola - \<nombre del servidor\> Propiedades**, elija una de las siguientes opciones:
    
      - **Conectarse a un servidor seleccionado automáticamente**   Seleccione esta opción para conectarse de forma automática al servidor donde administre las colas para ejecutar PowerShell en remoto.
    
      - **Seleccionar un servidor para conectar a**   Seleccione esta opción para especificar un servidor para ejecutar PowerShell en remoto. Si selecciona esta opción, haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar servidor de Exchange**. Seleccione el servidor en el que desea ejecutar PowerShell en remoto y, a continuación, haga clic en **Aceptar**.

## ¿Cómo saber si el proceso se ha completado correctamente?

Debería poder administrar las colas en el servidor de buzones especificado.

