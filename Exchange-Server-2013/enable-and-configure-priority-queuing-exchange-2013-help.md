---
title: 'Habilitar y configurar colas de prioridad: Exchange 2013 Help'
TOCTitle: Habilitar y configurar colas de prioridad
ms:assetid: 1975d85d-2f1d-4852-8d19-e74ba4ba3853
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ891104(v=EXCHG.150)
ms:contentKeyID: 51406479
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar y configurar colas de prioridad

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-12-16_

*Prioridad en las colas* es una característica de Microsoft Exchange Server 2013 que permite que la prioridad de mensajes configurada por el remitente de Microsoft Outlook o Outlook Web Access influya en el procesamiento del mensaje por el servicio de transporte del servidor de buzones. Cuando la cola de prioridad está habilitada, los mensajes de prioridad alta se transmiten a los destinos antes que los mensajes de prioridad normal y éstos, a su vez, se transmiten a sus destinos antes que los de prioridad baja. Para obtener más información, consulte [Prioridad en las colas](priority-queuing-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Los permisos de Exchange no se aplican a los procedimientos de este tema. Estos procedimientos se realizan en el sistema operativo de Exchange Server.

  - Los cambios que guarde en el archivo de configuración de la aplicación EdgeTransport.exe.config se aplican tras reiniciar el servicio de transporte de Microsoft Exchange.

  - Al reiniciar este servicio, el flujo de correo del servidor se interrumpe temporalmente.

  - Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el símbolo del sistema para habilitar y configurar la prioridad en cola en el archivo EdgeTransport.exe.config

1.  En una ventana del Símbolo del sistema, abra el archivo de configuración de aplicación EdgeTransport.exe.config en el Bloc de notas mediante el comando siguiente:
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

2.  Busque las claves siguientes en la sección `<appSettings>`.
    
        <add key="PriorityQueuingEnabled" value="false" />
        <add key="MaxPerDomainHighPriorityConnections" value="3" />
        <add key="MaxPerDomainNormalPriorityConnections" value="15" />
        <add key="MaxPerDomainLowPriorityConnections" value="2" />
        <add key="HighPriorityMessageExpirationTimeout" value="8:00:00" />
        <add key="NormalPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="LowPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="HighPriorityDelayNotificationTimeout" value="00:30:00" />
        <add key="NormalPriorityDelayNotificationTimeout" value="4:00:00" />
        <add key="LowPriorityDelayNotificationTimeout" value="8:00:00" />
        <add key="MaxHighPriorityMessageSize" value="250KB" />
    
    Para habilitar la prioridad en cola del servicio de transporte del servidor de buzones, use el siguiente valor:
    
    ```command line
<add key="PriorityQueuingEnabled" value="true" />
```
    
    Configure los valores de prioridad en cola restantes o déjelos con los valores predeterminados.

3.  Cuando haya terminado, guarde y cierre el archivo EdgeTransport.exe.config.

4.  Reinicie el servicio de transporte de Microsoft Exchange ejecutando el siguiente comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha habilitado y configurado correctamente la prioridad en cola, haga lo siguiente:

1.  Compruebe que la clave **PriorityQueueinEnabled** del archivo EdgeTransport.exe.config tiene el valor `"true"`.

2.  Use Outlook para crear un mensaje de prueba de prioridad alta superior al valor especificado por la clave **MaxHighPriorityMessageSize** y compruebe que el mensaje llega como mensaje de prioridad normal.

3.  Intente comprobar que los mensajes de mayor prioridad llegan antes que los mensajes de baja prioridad enviados al mismo destinatario o destino. Puede intentar usar varios buzones para enviar varios mensajes de prueba parecidos con diferentes valores de prioridad al mismo destinatario de forma simultanea.

