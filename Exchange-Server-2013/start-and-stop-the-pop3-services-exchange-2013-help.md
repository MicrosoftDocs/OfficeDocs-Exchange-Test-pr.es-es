---
title: 'Iniciar y detener los servicios POP3: Exchange 2013 Help'
TOCTitle: Iniciar y detener los servicios POP3
ms:assetid: 3d543921-d8c9-4d4b-99a1-82446b585ceb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997475(v=EXCHG.150)
ms:contentKeyID: 49895587
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Iniciar y detener los servicios POP3

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-03-13_

De forma predeterminada, los dos servicios POP3, el servicio Microsoft Exchange POP3 y el servicio Microsoft Exchange POP3, no se inician en equipos que ejecuten MicrosoftExchange Server 2013. Debe iniciar estos dos servicios para permitir que sus clientes de correo electrónico se conecten a Exchange con POP3. Cuando estos servicios se ejecutan, Exchange 2013 acepta comunicaciones de clientes de POP3 no protegidas en el puerto 110 y por el puerto 995 usando capa de sockets seguros (SSL).

El servicio Microsoft Exchange POP3 se ejecuta en equipos con Exchange 2013 que ejecutan el rol de servidor Acceso de clientes. El servicio Microsoft Exchange POP3 Backend se ejecuta en el equipo de Exchange 2013 que ejecuta el rol de servidor Buzón de correo. En entornos donde los roles de Acceso de cliente y Buzón se ejecutan en el mismo equipo, administrará ambos servicios en el mismo equipo.

Para obtener más información acerca de POP3 e IMAP4, consulte [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de POP3 e IMAP4" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el complemento Consola de administración de Microsoft para iniciar y detener el servicio POP3

Para iniciar los servicios de POP3:

1.  En un equipo que ejecute el rol de servidor Acceso de clientes, en el menú **Inicio**, seleccione **Programas**, **Herramientas administrativas** y haga clic en **Servicios**. Haga clic con el botón secundario en **Microsoft Exchange POP3** y, a continuación, haga clic en **Iniciar**.

2.  En un equipo que ejecute el rol de servidor Buzón de correo, en el menú **Inicio**, seleccione **Programas**, **Herramientas administrativas** y haga clic en **Servicios**. En el panel de resultados, haga clic con el botón secundario del mouse en **Microsoft Exchange POP3** y, a continuación, haga clic en **Iniciar**.

Para detener los servicios de POP3:

1.  En un equipo que ejecute el rol de servidor Acceso de clientes, en el menú **Inicio**, seleccione **Programas**, **Herramientas administrativas** y haga clic en **Servicios**. Haga clic con el botón secundario en **Microsoft Exchange POP3** y, a continuación, haga clic en **Detener**.

2.  En un equipo que ejecute el rol de servidor Buzón de correo, en el menú **Inicio**, seleccione **Programas**, **Herramientas administrativas** y haga clic en **Servicios**. Haga clic con el botón secundario en **Microsoft Exchange POP3 Backend** y, a continuación, haga clic en **Detener**.

## Usar el Shell para iniciar o detener los servicios POP3

Para iniciar los servicios de POP3:

1.  En el equipo que ejecuta el rol de servidor Acceso de clientes, del Shell, ejecute el siguiente comando para iniciar el servicio Microsoft Exchange POP3.
    
        Start-service MSExchangePOP3

2.  En el equipo que ejecuta el rol de servidor Buzón de correo, del Shell, ejecute el siguiente comando para iniciar el servicio Microsoft Exchange POP3 Backend.
    
```powershell
Start-service MSExchangePOP3BE
```

Para detener los servicios de POP3:

1.  En el equipo que ejecuta el rol de servidor Acceso de clientes, del Shell, ejecute el siguiente comando para detener el servicio Microsoft Exchange POP3.
    
```powershell
Stop-service MSExchangePOP3
```

2.  En el equipo que ejecuta el rol de servidor Buzón de correo, del Shell, ejecute el siguiente comando para detener el servicio Microsoft Exchange POP3 Backend.
    
```powershell
Stop-service MSExchangePOP3BE
```

## Utilice net start para iniciar o detener los servicios POP3

Para iniciar los servicios de POP3:

1.  En el equipo que ejecuta el rol de servidor Acceso de clientes, del símbolo del sistema, ejecute el siguiente comando para iniciar el servicio Microsoft Exchange POP3.
    
```powershell
Net Start msExchangePOP3
```

2.  En el equipo que ejecuta el rol de servidor Buzón de correo, del símbolo del sistema, ejecute el siguiente comando para iniciar el servicio Microsoft Exchange POP3 Backend.
    
```powershell
Net Start msExchangePOP3BE
```

Para detener los servicios de POP3:

1.  En el equipo que ejecuta el rol de servidor Acceso de clientes, del símbolo del sistema, ejecute el siguiente comando para detener el servicio Microsoft Exchange POP3.
    
```powershell
Net Stop MSExchangePOP3
```

2.  En el equipo que ejecuta el rol de servidor Buzón de correo, del símbolo del sistema, ejecute el siguiente comando para detener el servicio Microsoft Exchange POP3 Backend.
    
```powershell
Net Stop MSExchangePOP3BE
```

## ¿Cómo saber si el proceso se ha completado correctamente?

1.  En el servidor de acceso de clientes de Exchange, abra Administrador de tareas de Windows. En la pestaña **Servicios**, el estado de **MSExchangePOP3** mostrará **En ejecución** si el servicio Microsoft Exchange POP3 se está ejecutando.

2.  En el servidor de buzones de correo de Exchange, abra Windows Task Manager. En la pestaña **Servicios**, el estado de **MSExchangePOP3BE** mostrará **En ejecución** si el servicio Microsoft Exchange POP3 Backend se está ejecutando.

