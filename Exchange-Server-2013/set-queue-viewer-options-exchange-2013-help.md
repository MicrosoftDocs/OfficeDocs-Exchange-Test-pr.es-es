---
title: 'Establecer las opciones del visor de colas: Exchange 2013 Help'
TOCTitle: Establecer las opciones del visor de colas
ms:assetid: 03a9134c-0714-4c13-b286-92bccc7ec05e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa995934(v=EXCHG.150)
ms:contentKeyID: 49895441
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Establecer las opciones del visor de colas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Puede configurar las opciones del Visor de cola para ajustar el número de elementos que se muestran en la página y el intervalo de actualización automática. El intervalo de actualización automática determina la frecuencia con que se actualizan los resultados del Visor de cola.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Colas" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el cuadro de herramientas de Exchange configurar las opciones del Visor de cola

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange Server 2013** \> **Cuadro de herramientas de Exchange**.

2.  En **Herramientas de flujo de correo**, haga doble clic en **Visor de cola**.

3.  En Visor de cola, haga clic en **Ver** \> **Opciones** para configurar los siguientes ajustes en el cuadro de diálogo **Opciones del Visor de cola**:
    
    1.  En el campo **Intervalo de actualización (segundos)**, introduzca la frecuencia con la que el Visor de cola debería actualizar la pantalla.
        

        > [!NOTE]
        > El intervalo de actualización automática predeterminado es de 30 segundos y no se puede establecer un intervalo inferior. Si deshabilita la función de actualización automática desactivando la casilla de comprobación <STRONG>Pantalla Actualización automática</STRONG> de la página <STRONG>Opciones del Visor de cola</STRONG>, debe actualizar manualmente los resultados que se muestran en el Visor de cola haciendo clic en <STRONG>Actualizar</STRONG>.

    
    2.  En el campo **Número de elementos para mostrar en cada página**, escriba el número máximo de elementos que se mostrarán en el Visor de cola. Este número debe ser entre 1 y 10 000. Si la cantidad de elementos supera el límite, los elementos se ven en pantalla en grupos con el número máximo permitido de elementos. Por ejemplo, la figura siguiente muestra una cola con 14 mensajes y el Visor de cola configurado para mostrar 10 elementos en cada página. En la parte superior derecha aparece el número de objetos en la página. En la parte inferior de la página aparece el número total de objetos que hay en la cola. Mediante los controles de navegación puede ver los demás elementos de la cola.

4.  Cuando haya terminado, haga clic en **Aceptar**.
    
    **Visor de cola**
    
    ![Visor de cola con más elementos que el límite de elementos](images/Aa995934.e82196e6-002a-4e9e-823d-b244b0bd25e2(EXCHG.150).gif "Visor de cola con más elementos que el límite de elementos")  

## ¿Cómo saber si el proceso se ha completado correctamente?

Sabrá que el procedimiento ha funcionado si el Visor de cola utiliza el intervalo de actualización y el número de elementos por configuración de página.

