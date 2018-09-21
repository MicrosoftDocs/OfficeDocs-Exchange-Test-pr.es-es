---
title: 'Habilitar IMAP4 en Exchange 2016: Exchange 2013 Help'
TOCTitle: Habilitar IMAP4 en Exchange 2016
ms:assetid: c1ae10dd-14da-4400-b38d-2aeafde8abe6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124489(v=EXCHG.150)
ms:contentKeyID: 49895889
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar IMAP4 en Exchange 2016

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-06-02_

Obtenga información sobre cómo habilitar la conectividad de cliente IMAP4 en Exchange 2016 mediante la Microsoft Management Console (MMC) o los Shell de administración de Exchange (EMS).

Cuando instala Exchange Server 2016, la conectividad de cliente IMAP4 no está habilitada. Para habilitar la conectividad de cliente IMAP4, debe iniciar dos servicios IMAP, el servicio Microsoft Exchange IMAP4 y el servicio back-end Microsoft Exchange IMAP4. Cuando habilita IMAP4, Exchange 2016 acepta comunicaciones de cliente IMAP4 no protegidas en el puerto 143 y en el puerto 993 mediante una Capa de sockets seguros (SSL).

Administre los servicios IMAP4 y back-end IMAP4 en el mismo equipo de Exchange 2016 que ejecuta el rol de servidor Buzón de correo. En Exchange 2016, los servicios de acceso de cliente forman parte del rol de servidor Buzón de correo por lo que ya no administra los servicios de forma independiente.

Para obtener más información sobre cómo configurar POP3 e IMAP4, vea [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de POP3 e IMAP4" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso de Microsoft Management Console (MMC) para habilitar IMAP4

En el equipo que ejecuta el rol de servidor Buzón de correo:

1.  En el complemento **Servicios**, en el árbol de la consola, haga clic en **Servicios (locales)**.

2.  En el panel de resultados, con el botón secundario del mouse en **Microsoft Exchange IMAP4** y, a continuación, haga clic en **Propiedades**.

3.  En el panel de resultados, haga clic con el botón secundario del mouse en **Microsoft Exchange IMAP4 Backend** y, a continuación, haga clic en **Propiedades**.

4.  En la ficha **General**, en el menú **Tipo de inicio**, seleccione **Automático** y, a continuación, haga clic en **Aplicar**.

5.  En **Estado del servicio**, haga clic en **Iniciar** y, a continuación, en **Aceptar**.

## Usar el Shell de administración de Exchange para habilitar IMAP4

En el equipo que ejecuta el rol de servidor Buzón de correo:

1.  Establezca el servicio de Microsoft Exchange IMAP4 para que se inicie automáticamente.
    
    ```powershell
Set-service msExchangeIMAP4 -startuptype automatic
```

2.  Inicie el servicio de Microsoft Exchange IMAP4.
    
    ```powershell
Start-service msExchangeIMAP4
```

3.  Establezca el servicio de Microsoft Exchange IMAP4 Backend para que se inicie automáticamente.
    
    ```powershell
Set-service msExchangeIMAP4BE -startuptype automatic
```

4.  Inicie el servicio de Microsoft Exchange IMAP4 Backend.
    
    ```powershell
Start-service msExchangeIMAP4BE
```

## ¿Cómo saber si el proceso se ha completado correctamente?

En el servidor Buzón de correo de Exchange 2016, abra el Administrador de tareas de Windows. En la pestaña **Servicios**, el estado de **MSExchangeIMAP4** y **MSExchangeIMAP4BE** aparecerá como **En ejecución** si IMAP4 está habilitado.

