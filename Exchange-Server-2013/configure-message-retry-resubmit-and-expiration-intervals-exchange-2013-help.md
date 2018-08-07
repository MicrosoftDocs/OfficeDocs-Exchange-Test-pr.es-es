---
title: 'Configurar los intervalos de reintento, reenvío y expiración de mensajes'
TOCTitle: Configurar los intervalos de reintento, reenvío y expiración de mensajes
ms:assetid: 5420124f-aa4c-4702-b493-40a9a7edb786
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998043(v=EXCHG.150)
ms:contentKeyID: 51406516
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar los intervalos de reintento, reenvío y expiración de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-12-16_

En Microsoft Exchange Server 2013, puede configurar los intervalos de reintento, reenvío y expiración de los mensajes en el servicio de transporte de los servidores de buzones de correo y los servidores de transporte perimetral. Para obtener descripciones de estos ajustes, consulte [Intervalos de reintento, reenvío y expiración de mensajes](message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas "Servidor de transporte" y "Servidor de transporte perimetral" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Utilice EdgeTransport.exe.config para configurar el recuento de reintentos de problemas en cola, el intervalo de reintentos de problemas en cola, el intervalo de reintentos en cola de entrega a los buzones y el tiempo de inactividad máximo antes del intervalo de reenvío.

Para configurar el recuento de reintentos de problemas en cola, el intervalo de reintentos de problemas en cola, el intervalo de reintentos en cola de entrega a los buzones y el tiempo de inactividad máximo antes del intervalo de reenvío, debe modificar las claves en el archivo de configuración de la aplicación XML %ExchangeInstallPath%Bin\\EdgeTransport.exe.config en el servidor de buzones de correo o el servidor de transporte perimetral. Los cambios que guarde en este archivo se aplican después de reiniciar el servicio de transporte de Microsoft Exchange. Al reiniciar este servicio, el flujo de correo del servidor se interrumpe temporalmente.

1.  En una ventana del símbolo del sistema de un servidor de buzones o de un servidor de transporte perimetral, abra el archivo EdgeTransport.exe.config en el Bloc de notas ejecutando el siguiente comando:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Localice las claves siguientes en la sección `<appSettings>`.
    
        <add key="QueueGlitchRetryCount" value="<Integer>" />
        <add key="QueueGlitchRetryInterval" value="<hh:mm:ss>" />
        <add key="MailboxDeliveryQueueRetryInterval" value="<hh:mm:ss>" />
        <add key="MaxIdleTimeBeforeResubmit" value="<hh:mm:ss>" />
    
    En este ejemplo se cambia el recuento de reintentos de problemas en cola a 6, el intervalo de reintentos de problemas en cola a 30 segundos, el intervalo de reintentos en cola de entrega a los buzones a 3 minutos y el tiempo de inactividad máximo antes del intervalo de reenvío a 6 horas.
    
        <add key="QueueGlitchRetryCount" value="6" />
        <add key="QueueGlitchRetryInterval" value="00:00:30" />
        <add key="MailboxDeliveryQueueRetryInterval" value="00:03:00" />
        <add key="MaxIdleTimeBeforeResubmit" value="6:00:00" />

3.  Cuando haya terminado, guarde y cierre el archivo EdgeTransport.exe.config.

4.  Reinicie el servicio de transporte de Microsoft Exchange ejecutando el siguiente comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Configurar el número de reintentos tras error transitorio, el intervalo de reintentos tras error transitorio y el intervalo de reintentos tras error de conexión

El número de reintentos tras error transitorio especifica el número de intentos de conexión que se realizan cuando se producen errores en los intentos de conexión controlados por las claves `QueueGlitchRetryCount` y `QueueGlitchRetryInterval`. El número predeterminado de intentos de reintento tras error transitorio es de 6. El intervalo válido de entrada de este parámetro escila entre 0 y 15. Si define un número de intentos de reintento tras error transitorio igual a 0, el siguiente intento de conexión lo controlará el *intervalo de reintentos de conexión saliente tras error*.

El intervalo de reintentos tras error transitorio especifica el intervalo entre cada intento de conexión, indicado por el número de intentos de reintento tras error transitorio. En un servicio de transporte de un servidor de buzones, el intervalo predeterminado de reintentos tras error transitorio es de 5 minutos. En un servidor Transporte perimetral, el intervalo predeterminado de reintento tras error transitorio es de 10 minutos.

El intervalo de reintento de conexión saliente tras error especifica el intervalo de reintento de los intentos de conexión saliente erróneos anteriores. Los intentos de conexión erróneos anteriores los controlan los intentos de reintento tras error transitorio y el intervalo de reintento tras error transitorio. El valor predeterminado para el intervalo de reintento de conexión saliente tras error en el servicio de transporte de un servidor de buzón es de 10 minutos. El valor predeterminado para un servidor Transporte perimetral es de 30 minutos.

## Usar el EAC para configurar el número de reintentos tras error transitorio, el intervalo de reintentos tras error transitorio o el intervalo de reintentos tras error de conexión saliente

1.  En el Centro de administración de Exchange (EAC), haga clic en **Servidores** \> **Servidores**, seleccione el servidor, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") y, a continuación, haga clic en **Límites de transporte**.

2.  En la sección **Reintentos**, introduzca un valor para el **Intervalo de reintentos tras error de conexión saliente (segundos)**, el **Intervalo de reintentos tras error transitorio (minutos)** o el **Número de reintentos tras error transitorio**.

3.  Cuando haya terminado, haga clic en **Guardar**.

## Usar el Shell para configurar el número de reintentos tras error transitorio, el intervalo de reintentos tras error transitorio o el intervalo de reintentos tras error de conexión saliente

Utilice la sintaxis siguiente para configurar el número de reintentos tras error transitorio, el intervalo de reintentos tras error transitorio y el intervalo de reintentos tras error de conexión saliente en el servicio de transporte de un servidor de buzones o de un servidor de transporte perimetral.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

En este ejemplo se cambian los valores siguientes en el servidor de buzones denominado Mailbox01: en el servidor de transporte perimetral Exchange01.

  - El número de reintentos tras error transitorio se establece en 8.

  - El intervalo de reintentos tras error transitorio se establece en 1 minuto.

  - El intervalo de reintentos tras error de conexión saliente se establece en 45 minutos.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!NOTE]
> Los parámetros <EM>TransientFailureRetryCount</EM> y <EM>TransientFailureRetryInterval</EM> también pueden utilizarse en el cmdlet <STRONG>Set-FrontEndTransportService</STRONG> para el servicio de transporte front-end en los servidores de acceso de clientes.



## Configurar el número de reintentos tras error transitorio, el intervalo de reintentos tras error transitorio y el intervalo de reintentos tras error de conexión

## Usar el Centro de administración de Exchange para configurar el número de reintentos tras error transitorio, el intervalo de reintentos tras error transitorio y el intervalo de reintentos tras error de conexión saliente

1.  En el EAC, haga clic en **Servidores** \> **Servidores**, seleccione el servidor, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") y, a continuación, haga clic en **Límites de transporte**.

2.  En la sección **Reintentos**, escriba un valor para el **Intervalo de reintentos tras error de conexión saliente (segundos)**, el **Intervalo de reintentos tras error transitorio (minutos)** o el **Número de reintentos tras error transitorio**.

3.  Cuando haya terminado, haga clic en **Guardar**.

## Usar el Shell para configurar el número de reintentos tras error transitorio, el intervalo de reintentos tras error transitorio o el intervalo de reintentos tras error de conexión saliente

Utilice la sintaxis siguiente para configurar el número de reintentos tras error transitorio, el intervalo de reintentos tras error transitorio y el intervalo de reintentos tras error de conexión saliente en el servicio de transporte de un servidor de buzones o de un servidor de transporte perimetral.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

En este ejemplo se cambian los valores siguientes en el servidor de buzones denominado Mailbox01: en el servidor de transporte perimetral Exchange01.

  - El número de reintentos tras error transitorio se establece en 8.

  - El intervalo de reintentos tras error transitorio se establece en 1 minuto.

  - El intervalo de reintentos tras error de conexión saliente se establece en 45 minutos.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!NOTE]
> Los parámetros <EM>TransientFailureRetryCount</EM> y <EM>TransientFailureRetryInterval</EM> también pueden utilizarse en el cmdlet <STRONG>Set-FrontEndTransportService</STRONG> para el servicio de transporte front-end en los servidores de acceso de clientes.



## Uso del Shell para configurar el intervalo de reintentos del mensaje

De forma predeterminada, el intervalo de reintentos de envío de mensajes es de `00:15:00` o 15 minutos. Recomendamos que no modifique el valor predeterminado a no ser que el Servicio de soporte técnico y atención al cliente de Microsoft le aconseje hacerlo.

Utilice la siguiente sintaxis para establecer el intervalo de reintentos de mensaje.

    Set-TransportService <ServerIdentity> -MessageRetryInterval <dd.hh:mm:ss>

En este ejemplo se cambia el intervalo de reintentos de mensaje a 20 minutos en el servidor de buzones denominado Mailbox01.

    Set-TransportService Mailbox01 -MessageRetryInterval 00:20:00

## Configurar las opciones de tiempo de espera DSN de retraso

Puede utilizar el EAC o el Shell para configurar el intervalo de espera de la notificación DSN de retraso. Esta configuración sólo se aplica al servidor de transporte local. Sólo puede utilizar el Shell para habilitar o deshabilitar el envío de mensajes DSN de retraso a remitentes internos y externos. Estos ajustes se aplican a todos los servidores de transporte de la organización.


> [!NOTE]
> En los servidores de transporte de concentradores de Exchange 2007, todos los parámetros <EM>ExternalDSN*</EM> e <EM>InternalDSN*</EM> pueden utilizarse con el cmdlet <STRONG>Set-TransportServer</STRONG>, pero no con el cmdlet <STRONG>Set-TransportConfig</STRONG>. Si tiene algún servidor de transporte de concentradores de Exchange 2007 en la organización, debe realizar cambios en estos valores utilizando el cmdlet <STRONG>Set-TransportServer</STRONG> en cada servidor de transporte de concentradores de Exchange 2007.



## Uso del Centro de administración de Exchange para configurar el intervalo de espera de notificación del mensaje DSN de retraso

1.  En el EAC, haga clic en **Servidores** \> **Servidores**, seleccione el servidor, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") y, a continuación, haga clic en **Límites de transporte**.

2.  En la sección **Notificaciones**, escriba un valor para **Notificar al remitente cuando el mensaje se ha retrasado tras (horas)**.

3.  Cuando haya terminado, haga clic en **Guardar**.

## Uso del Shell para configurar el intervalo de espera de notificación del mensaje DSN de retraso

Utilice la siguiente sintaxis para establecer el intervalo de reintentos de mensaje.

    Set-TransportService <ServerIdentity> -DelayNotificationTimeout <dd.hh:mm:ss>

En este ejemplo se cambia el intervalo de espera de notificación de mensajes DSN de retraso a 6 horas en un servidor de buzones denominado Mailbox01.

    Set-TransportService Mailbox01 -DelayNotificationTimeout 06:00:00

## Usar el Shell para habilitar o deshabilitar el envío de notificaciones de DSN de retraso a los remitentes internos

Utilice la siguiente sintaxis para configurar los ajustes de notificación de DSN de retraso.

    Set-TransportConfig -ExternalDelayDSNEnabled <$true | $false> -InternalDelayDSNEnabled <$true |$false>

En este ejemplo, se impide el envío de notificaciones DSN de retraso a remitentes externos.

    Set-TransportConfig -ExternalDelayDSNEnabled $false

En este ejemplo, se impide el envío de notificaciones DSN de retraso a remitentes internos.

    Set-TransportConfig -InternalDelayDSNEnabled $false

## Configuración del intervalo de espera hasta la expiración del mensaje

## Uso del EAC para configurar el intervalo de espera hasta la expiración del mensaje

1.  En el EAC, haga clic en **Servidores** \> **Servidores**, seleccione el servidor, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") y, a continuación, haga clic en **Límites de transporte**.

2.  En la sección **Expiración del mensaje**, introduzca un valor para **Tiempo máximo desde el envío (días)**.

3.  Cuando haya terminado, haga clic en **Guardar**.

## Uso del Shell para configurar el intervalo de tiempo hasta la expiración del mensaje

Para configurar el intervalo de espera hasta la expiración del mensaje, utilice la sintaxis siguiente.

    Set-TransportService <ServerIdentity> -MessageExpirationTimeout <dd.hh:mm:ss>

En este ejemplo, se cambia el intervalo de espera hasta la expiración del mensaje a 4 días en el servidor Exchange denominado Mailbox01.

    Set-TransportService Mailbox01 -MessageExpirationTimeout 4.00:00:00

