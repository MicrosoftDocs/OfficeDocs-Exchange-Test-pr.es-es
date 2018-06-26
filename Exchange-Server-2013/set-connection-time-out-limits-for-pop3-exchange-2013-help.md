---
title: 'Establecer límites de tiempo de espera de conexión para POP3: Exchange 2013 Help'
TOCTitle: Establecer límites de tiempo de espera de conexión para POP3
ms:assetid: 40003115-be4e-4cf1-97b4-f5ca05b314dc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997604(v=EXCHG.150)
ms:contentKeyID: 50556770
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Establecer límites de tiempo de espera de conexión para POP3

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-11-28_

Puede usar el Centro de Administración de Exchange o el Shell para configurar los límites de tiempo de espera de conexión para conexiones POP3 autenticadas y no autenticadas inactivas.

Para obtener más información acerca de POP3, consulte [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración POP3" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para establecer los límites de tiempo de espera de conexión de POP3

1.  En la consola EAC, desplácese hasta **Servidores** **\>** **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **POP3**.

4.  Desplácese hacia abajo y haga clic en **Más opciones**.

5.  En **Configuración de tiempo de espera**, use la siguiente configuración:
    
      - **Tiempo de espera autenticado (segundos)**    Especifica el tiempo que se esperará antes de cerrar una conexión autenticada inactiva. El valor predeterminado es 1,800. Se admiten los valores entre 30 y 86,400.
    
      - **Tiempo de espera no autenticado (segundos)**    Especifica el tiempo que se esperará antes de cerrar una conexión que no está autenticada. El valor predeterminado es 60. Se admiten los valores entre 30 y 3,600.

6.  Haga clic en **Aplicar** y, a continuación, haga clic en **Aceptar** para guardar los cambios.

Una vez definidos los límites de tiempo de espera de conexión para POP3, debe reiniciar los servicios POP3 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar los servicios POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Uso del Shell para establecer los límites de tiempo de espera de conexión de POP3

En este ejemplo, se define el límite de tiempo de espera de conexión para conexiones inactivas autenticadas.

    Set -PopSettings -Identity CAS01 -AuthenticatedConnectionTimeout TimeValue

En este ejemplo, se define el límite de tiempo de espera de conexión para conexiones inactivas no autenticadas.

    Set -PopSettings -Identity CAS01 -PreAuthenticatedConnectionTimeout TimeValue

Una vez definidos los límites de tiempo de espera de conexión para POP3, debe reiniciar los servicios POP3 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar los servicios POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obtener más información sobre sintaxis y parámetros, consulte [Set-POPSettings](https://technet.microsoft.com/es-es/library/aa997154\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si estableció los límites de conexión correctamente, siga uno de estos procedimientos:

1.  En la consola EAC, desplácese hasta **Servidores** **\>** **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **POP3**.

4.  Desplácese hacia abajo y haga clic en **Más opciones**.

5.  En **Configuración de tiempo de espera**, compruebe que la configuración de la conexión sea correcta.

O bien

1.  Ejecute el siguiente comando en el Shell.
    
        Get-PopSettings | format-list

2.  Compruebe que la configuración de la conexión sea correcta.

## Más información

Después de establecer los límites de tiempo de espera de conexión de POP3, es posible que también desee realizar las siguientes tareas:

[Habilitar POP3 en Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[Establecer límites de conexión para POP3](set-connection-limits-for-pop3-exchange-2013-help.md)

