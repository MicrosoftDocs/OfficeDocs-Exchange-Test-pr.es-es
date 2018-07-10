---
title: 'Configurar el registro de la tabla de enrutamiento: Exchange 2013 Help'
TOCTitle: Configurar el registro de la tabla de enrutamiento
ms:assetid: 7184f8f7-4eb8-468a-aafe-b2d72868f820
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201696(v=EXCHG.150)
ms:contentKeyID: 49895705
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el registro de la tabla de enrutamiento

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

El inicio de sesión de la tabla de enrutamiento hace un registro periódico de una instantánea de la tabla de enrutamiento que utiliza Microsoft Exchange Server 2013 para enrutar los mensajes a sus destinos.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas "Servidor de transporte" y "Servidor de transporte perimetral" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para configurar el intervalo de tiempo del recálculo automático de la tabla de enrutamiento, modifique el archivo de configuración de la aplicación XML EdgeTransport.exe.config. Los cambios que guarde en este archivo se aplican después de reiniciar el servicio de transporte de Microsoft Exchange. Al reiniciar este servicio, el flujo de correo del servidor se interrumpe temporalmente.

  - Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para configurar el inicio de sesión de la tabla de enrutamiento

Ejecute el siguiente comando:

    Set-TransportService <ServerIdentity> -RoutingTableLogMaxAge <dd.hh:mm:ss> -RoutingTableLogMaxDirectorySize <Size>  -RoutingTableLogPath <LocalFilePath>

En este ejemplo se establece la siguiente configuración de registro de la tabla de enrutamiento en el servidor de buzones de correo llamado Mailbox01:

  - Establece la ubicación de los archivos de registro de la tabla de enrutamiento en D:\\Registro de tabla de enrutamiento. Tenga en cuenta que si la carpeta no existe, se creará para usted.

  - Establece el tamaño máximo de la carpeta de registro de tabla enrutamiento en 70 MB.

  - Establece la antigüedad máxima de un archivo de registro de tabla enrutamiento en 45 días.

<!-- end list -->

    Set-TransportService Mailbox01 -RoutingTableLogPath "D:\Routing Table Log" -RoutingTableLogMaxDirectorySize 70MB -RoutingTableLogMaxAge 45.00:00:00


> [!NOTE]
> Si establece el parámetro <EM>RoutingTableLogMaxAge</EM> en el valor <CODE>00:00:00</CODE>, evitará la eliminación automática de los archivos de registro de la tabla de enrutamiento debido a su antigüedad.



## ¿Cómo saber si el proceso se ha completado correctamente?

Par verificar que ha configurado correctamente el registro de la tabla de enrutamiento, haga lo siguiente:

1.  En el Shell, ejecute el siguiente comando:
    
        Get-TransportService <ServerIdentity> | Format-List RoutingTableLog*

2.  Verifique que los valores mostrados son los valores que ha configurado.

## Uso del símbolo del sistema para configurar el intervalo para el recálculo automático de la tabla de enrutamiento del archivo EdgeTransport.exe.config

1.  En una ventana del Símbolo del sistema, abra el archivo de configuración de aplicación EdgeTransport.exe.config en el Bloc de notas mediante el comando siguiente:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Modifique la clave siguiente en la sección `<appSettings>`.
    
        <add key="RoutingConfigReloadInterval" value="<hh:mm:ss>" />
    
    Por ejemplo, para cambiar el intervalo de recálculo automático de la tabla de enrutamiento a 10 horas, use el valor siguiente:
    
        <add key="RoutingConfigReloadInterval" value="10:00:00" />

3.  Cuando haya terminado, guarde y cierre el archivo EdgeTransport.exe.config.

4.  Reinicie el servicio de transporte de Microsoft Exchange ejecutando el siguiente comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha configurado correctamente el intervalo para el recálculo automático de la tabla de enrutamiento, verifique que el registro de la misma se haya actualizado durante el intervalo de tiempo que ha especificado.

Recuerde que la tabla de enrutamiento se recalculará y se registrará antes que el valor que especifica la clave *RoutingConfigReloadInterval* si se produce alguna de las condiciones siguientes:

  - Al detectar un cambio en la configuración de enrutamiento. Por ejemplo, se agrega, quita o modifica un conector de envío o de recepción, o se produce la renovación del token Kerberos a las seis horas.

  - Se ha iniciado el servicio de transporte de Microsoft Exchange.

