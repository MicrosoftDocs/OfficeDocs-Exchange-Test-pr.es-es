---
title: 'Iniciar y detener los servicios IMAP4: Exchange 2013 Help'
TOCTitle: Iniciar y detener los servicios IMAP4
ms:assetid: a52db4bd-69a6-47b2-acf3-d9d8571c7a87
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124022(v=EXCHG.150)
ms:contentKeyID: 49895813
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Iniciar y detener los servicios IMAP4

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-05_

Por defecto, los dos servicios IMAP4, el servicio Microsoft Exchange IMAP4 y el servicio Microsoft Exchange IMAP4 Backend no se inician en equipos que ejecutan MicrosoftExchange Server 2013. Es necesario iniciar estos dos servicios para permitir que sus clientes de correo electrónico se conecten con Exchange usando IMAP4. Cuando se inician estos servicios, Exchange 2013 acepta comunicaciones no protegidas del cliente IMAP4 en el puerto 143 y mediante el puerto 993 a través de SSL (Capa de sockets seguros).

El servicio Microsoft Exchange IMAP4 se ejecuta en ordenadores Exchange 2013 que ejecuten el rol de servidor de Acceso de clientes. El servicio Microsoft Exchange IMAP4 Backend se ejecuta en equipos Exchange 2013 que ejecuten el rol de servidor Buzón de correo. En entornos donde los roles de Acceso de clientes y Buzón de correo se ejecutan en el mismo equipo, administrará ambos servicios en el mismo equipo.

Para obtener más información acerca de POP3 e IMAP4, vea [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de POP3 e IMAP4" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del complemento de los servicios de la Consola de administración de Microsoft para iniciar o detener el servicio IMAP4

Para iniciar los servicios de IMAP4:

1.  En un equipo que ejecute el rol de servidor Administrador de clústeres, en el menú **Inicio**, seleccione **Programas**, vaya a **Herramientas administrativas** y haga clic en **Servicios**. Haga clic con el botón secundario del ratón en **Microsoft Exchange IMAP4** y, a continuación, haga clic en **Iniciar**.

2.  En un equipo que ejecute el rol de servidor Buzón de correo, en el menú **Inicio**, seleccione **Programas**, vaya a **Herramientas administrativas** y haga clic en **Servicios**. Haga clic con el botón secundario del ratón en **Microsoft Exchange IMAP4 Backend** y, a continuación, haga clic en **Iniciar**.

Para detener los servicios de IMAP4:

1.  En un equipo que ejecute el rol de servidor Administrador de clústeres, en el menú **Inicio**, seleccione **Programas**, vaya a **Herramientas administrativas** y haga clic en **Servicios**. Haga clic con el botón secundario del ratón en **Microsoft Exchange IMAP4** y, a continuación, haga clic en **Detener**.

2.  En un equipo que ejecute el rol de servidor Buzón de correo, en el menú **Inicio**, seleccione **Programas**, vaya a **Herramientas administrativas** y haga clic en **Servicios**. Haga clic con el botón secundario del ratón en **Microsoft Exchange IMAP4 Backend**, y, a continuación, haga clic en **Detener**.

## Usar el Shell para iniciar o detener los servicios IMAP4

Para iniciar los servicios de IMAP4:

1.  En el equipo que ejecuta el rol de servidor de acceso de clientes, desde el Shell, ejecute el siguiente comando para iniciar el servicio Microsoft Exchange IMAP4.
    
    ```powershell
Start-service msExchangeIMAP4
```

2.  En el equipo que ejecuta el rol de servidor Buzón de correo, desde el Shell, ejecute el siguiente comando para iniciar el servicio Microsoft Exchange IMAP4 Backend.
    
    ```powershell
Start-service msExchangeIMAP4BE
```

Para detener los servicios de IMAP4:

1.  En el equipo que ejecuta el rol de servidor de acceso de clientes, desde el Shell, ejecute el siguiente comando para detener el servicio Microsoft Exchange IMAP4.
    
    ```powershell
Stop-service msExchangeIMAP4
```

2.  En el equipo que ejecuta el rol de servidor Buzón de correo, desde el Shell, ejecute el siguiente comando para detener el servicio Microsoft Exchange IMAP4 Backend.
    
    ```powershell
Stop-service msExchangeIMAP4BE
```

## Uso del comando net start para iniciar o detener el servicio IMAP4

Para iniciar los servicios de IMAP4:

1.  En el equipo que ejecuta el rol de servidor Acceso de clientes, en el símbolo del sistema, ejecute el siguiente comando para iniciar el servicio Microsoft Exchange IMAP4.
    
    ```powershell
net start msExchangeIMAP4
```

2.  En el equipo que ejecuta el rol de servidor Buzón de correo, en el símbolo del sistema, ejecute el siguiente comando para iniciar el servicio Microsoft Exchange IMAP4 Backend.
    
    ```powershell
net start msExchangeIMAP4BE
```

Para detener los servicios de IMAP4:

1.  En el equipo que ejecuta el rol de servidor Acceso de clientes, en el símbolo del sistema, ejecute el siguiente comando para detener el servicio Microsoft Exchange IMAP4.
    
    ```powershell
Net Stop MSExchangeIMAP4
```

2.  En el equipo que ejecuta el rol de servidor Buzón de correo, en el símbolo del sistema, ejecute el siguiente comando para detener el servicio Microsoft Exchange IMAP4 Backend.
    
    ```powershell
Net Stop MSExchangeIMAP4BE
```

## ¿Cómo saber si el proceso se ha completado correctamente?

1.  En el servidor de acceso de clientes de Exchange, abra el Administrador de tareas de Windows. En la pestaña **Servicios**, el estado de **MSExchangeIMAP4** aparecerá como **En ejecución** si el servicio Microsoft Exchange IMAP4 se está ejecutando.

2.  En el servidor de Buzón de correo Exchange, abra Administrador de tareas de Windows. En la pestaña **Servicios**, el estado de **MSExchangeIMAP4BE** aparecerá como **En ejecución** si el servicio Microsoft Exchange IMAP4 se está ejecutando.

