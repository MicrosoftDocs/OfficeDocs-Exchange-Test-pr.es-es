---
title: 'Configurar Get-QueueDigest: Exchange 2013 Help'
TOCTitle: Configurar Get-QueueDigest
ms:assetid: f730c520-4ba5-4a15-8846-132bff500bb8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn505733(v=EXCHG.150)
ms:contentKeyID: 59637140
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar Get-QueueDigest

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-12-16_

El cmdlet **Get-QueueDigest** le permite ver información sobre algunas de las colas de su organización de Exchange, o de todas ellas, usando un solo comando.

De forma predeterminada, los resultados que devuelve el cmdlet **Get-QueueDigest** tienen una antigüedad de entre uno y dos minutos. Estos valores se controlan con la siguiente configuración:

  - **La clave QueueLoggingInterval de EdgeTransport.exe.config**   Esta clave especifica la frecuencia con la que los datos de la cola se registran y están disponibles en **Get-QueueDigest**. El valor predeterminado es `00:01:00` (un minuto). Para especificar un valor, escríbalo como un intervalo de tiempo: *hh:mm:ss*, donde *h* = horas, *m* = minutos y *s* = segundos. De manera predeterminada, esta clave no existe en el archivo EdgeTransport.exe.config.

  - **Parámetro QueueDiagnosticsAggregationInterval en Set-TransportConfig**   Este parámetro especifica la frecuencia con la que los datos de la cola se comparten entre los servidores de buzones de correo. El valor predeterminado es `00:01:00` (un minuto). Para especificar un valor, escríbalo como un intervalo de tiempo: *hh:mm:ss*, donde *h* = horas, *m* = minutos y *s* = segundos.

La suma de los valores de la clave **QueueLoggingInterval** y el parámetro *QueueDiagnosticsAggregationInterval* determina la antigüedad máxima de los resultados devueltos por **Get-QueueDigest**.

Además, **Get-QueueDigest** devuelve los resultados de diferentes maneras en función del tipo de cola y del estado de la cola. Por ejemplo, las siguientes colas se muestran en los resultados si contienen al menos un mensaje:

  - La cola de envío, la cola inalcanzable y la cola de mensajes dudosos (colas persistentes).

  - Colas de entrega en el estado Suspendido (colas suspendidas manualmente por un administrador).

De manera predeterminada, las colas de entrega que tienen el estado Activo, Conectando, Listo o Reintentar solo se devuelven en los resultados si la cola contiene 10 o más mensajes. La clave **QueueLoggingThreshold** del archivo EdgeTransport.exe.config controla este valor. Puede especificar un valor entero mayor o menor. De manera predeterminada, esta clave no existe en el archivo EdgeTransport.exe.config.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Para ver los permisos de Exchange que necesita para ejecutar **Set-TransportConfig** en el Shell de administración de Exchange, consulte la entrada “Configuración del transporte” en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Los permisos de Exchange no se aplican a las acciones de modificar el archivo EdgeTransport.exe.config y reiniciar el servicio de transporte de Microsoft Exchange. Estos procedimientos se realizan en el sistema operativo del servidor Exchange.

  - Los cambios que guarde en el archivo EdgeTransport.exe.config se aplicarán después de reiniciar el servicio de transporte de Microsoft Exchange. Al reiniciar el servicio, el flujo de correo del servidor se interrumpe temporalmente.

  - Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.

  - Los cambios que realice con **Set-TransportConfig** afectarán a todos los servidores de buzones de correo de la organización. Los cambios que realice en el archivo EdgeTransport.exe.config afectarán solamente al servidor de buzones de correo local.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurar Get-QueueDigest

1.  En una ventana del símbolo del sistema, abra el archivo EdgeTransport.exe.config en el Bloc de notas ejecutando el comando siguiente:
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

2.  Agregue una de las siguientes claves, o las dos, a la sección `<appSettings>`.
    
        <add key="QueueLoggingThreshold" value="<integer>" />
        <add key="QueueLoggingInterval" value="<hh:mm:ss>" />
    
    Por ejemplo, para configurar el valor **QueueLoggingThreshold** como 1 y el valor **QueueLoggingInterval** como 30 segundos, use los siguientes valores:
    
        <add key="QueueLoggingThreshold" value="1" />
        <add key="QueueLoggingInterval" value="00:00:30" />

3.  Cuando haya terminado, guarde y cierre el archivo EdgeTransport.exe.config.

4.  Reinicie el servicio de transporte de Microsoft Exchange ejecutando el siguiente comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

5.  Para cambiar el valor del parámetro *QueueDiagnosticsAggregationInterval* en el Shell de administración de Exchange, use la siguiente sintaxis:
    
    ```powershell
Set-TransportConfig -QueueDiagnosticsAggregationInterval <hh:mm:ss>
```
    
    Por ejemplo, para cambiar el valor a 30 segundos, ejecute el siguiente comando:
    
    ```powershell
Set-TransportConfig -QueueDiagnosticsAggregationInterval 00:00:30
```

## ¿Cómo puede saber si funcionó?

Para comprobar si configuró correctamente **Get-QueueDigest**, siga estos pasos:

1.  Compruebe los valores de las claves **QueueLoggingThreshold** y **QueueLoggingInterval** en el archivo EdgeTransport.exe.config. Si estas claves no están, se usarán los valores predeterminados.

2.  Compruebe el valor del parámetro *QueueDiagnosticsAggregationInterval* ejecutando el siguiente comando:
    
        Get-TransportConfig | Format-List *queue*

