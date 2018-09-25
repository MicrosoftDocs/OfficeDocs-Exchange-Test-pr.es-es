---
title: 'Configurar el registro de protocolo: Exchange 2013 Help'
TOCTitle: Configurar el registro de protocolo
ms:assetid: c81cac9c-b990-492a-b899-5be8d08a6068
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124531(v=EXCHG.150)
ms:contentKeyID: 49895904
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el registro de protocolo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-03-15_

El registro de protocolo registra las conversaciones del SMTP que se producen entre conectores de envío y recepción como parte de la entrega de mensajes.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas "Servicio de transporte", "Servicio de transporte frontend", "Servicio de transporte de buzones de correo", "Conectores de recepción" y "Conectores de envío" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Puede usar el Centro de administración de Exchange (EAC) para habilitar o deshabilitar el registro de protocolo para los conectores de envío y recepción en el servicio de transporte de los servidores de buzones de correo y para los conectores de recepción en el servicio de transporte de front-end en los servidores de acceso de cliente. También puede usar la consola EAC para configurar las rutas de registro de protocolo para el servicio de transporte solamente. Para todo otro protocolo de opciones de registro, deberás usar el Shell.

  - El registro de protocolo está habilitado o deshabilitado en cada conector individual. Todos los conectores de recepción en el servidor de Exchange comparten los mismos archivos de registro de protocolo y las opciones de registro de protocolo. Estas configuraciones de registro de protocolo son independientes de los archivos de registro de protocolo del conector de envío y de las opciones de registro de protocolo que están en el mismo servidor.

  - > [!WARNING]
    > No realice este procedimiento en un servidor de transporte perimetral que se haya suscrito a la organización de Exchange por medio de EdgeSync. En su lugar, realice los cambios en el servicio de transporte en el servidor Buzón de correo. Los cambios se replicarán en el servidor de transporte perimetral cuando se produzca la próxima sincronización de EdgeSync.



  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso de la consola EAC para configurar el registro de protocolo

Para usar la consola EAC para habilitar o deshabilitar el registro de protocolo en un conector de envío o un conector de recepción en el servicio de transporte en un servidor Buzón de correo, o en un conector de recepción en un servicio de transporte frontend de un servidor Acceso de cliente, realice lo siguiente:

1.  En la consola de EAC, navegue a **Flujo de correo** \> **Conectores de envío** o **Flujo de correo** \> **Conectores de recepción**.

2.  Seleccione el conector que desee configurar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la ficha **General**, en **Nivel de registro de protocolo**, seleccione una de las siguientes opciones:
    
      - **Ninguno** Registro de protocolo deshabilitado en el conector.
    
      - **Detallado** Registro de protocolo está habilitado en el conector.
    
    Cuando haya terminado, haga clic en **Guardar**.

Para usar la consola EAC para configurar las rutas de registro de protocolo para los conectores de envío y los conectores de recepción en el servicio de transporte de un servidor Buzón de correo, realice lo siguiente:

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  Seleccione el servidor Buzón de correo que desee configurar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **Registros de transporte**.

4.  En la sección **Registro de protocolo**, cambie una de las siguientes configuraciones:
    
      - **Ruta del registro de protocolo de envío**   El valor que especifica debe estar en el servidor de Exchange local. Si la carpeta no existe, se creará cuando usted haga clic en **Guardar**.
    
      - **Ruta del registro de protocolo de recepción**   El valor que especifica debe estar en el servidor de Exchange local. Si la carpeta no existe, se creará cuando usted haga clic en **Guardar**.
    
    Cuando haya terminado, haga clic en **Guardar**.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha utilizado correctamente la consola EAC para configurar la configuración del registro de protocolo, realice lo siguiente:

1.  Busque la ubicación que especificó para el conector de envío o los registros de protocolo del conector de recepción.

2.  Si habilitó el registro de protocolo, verifique que se crea un archivo de registro. Si ha deshabilitado un registro de protocolo, verifique que el último archivo de registro se ha dejado de actualizar.

## Utilice el Shell para habilitar o deshabilitar el registro de protocolo en un conector de envío o un conector de recepción

Para habilitar o deshabilitar un registro de protocolo en un conector de envío o un conector de recepción, ejecute el siguiente comando:

```powershell
<Set-SendConnector |Set-ReceiveConnector> <ConnectorIdentity> -ProtocolLoggingLevel <Verbose | None>
```

En este ejemplo se habilita el registro de protocolo para el conector de recepción denominado "Connection from contoso.com".

```powershell
Set-ReceiveConnector "Connection from Contoso.com" -ProtocolLoggingLevel Verbose
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que habilitó o deshabilitó correctamente el registro de protocolo, realice lo siguiente:

1.  En el Shell, ejecute el siguiente comando:
    
    ```powershell
    <Get-SendConnector |Get-ReceiveConnector> | Format-List Name,ProtocolLoggingLevel
    ```

2.  Verifique que los valores mostrados son los valores que ha configurado.

## Uso del Shell para habilitar o deshabilitar el registro de protocolos en el conector de envío interno de la organización

Para habilitar o deshabilitar el registro de protocolo en el conector de envío interno de la organización implícito e invisible que existe en el servicio de transporte en un servidor Buzón de correo y en el servicio de transporte frontend en un servidor Acceso de cliente, ejecute el siguiente comando:

```powershell
<Set-TransportService | Set-FrontEndTransportService> -IntraOrgConnectorProtocolLoggingLevel <Verbose | None>
```

Este ejemplo habilita el registro de protocolo en el conector de envío interno de la organización en el servicio de transporte de un servidor Buzón de correo denominado Mailbox01.

```powershell
Set-TransportService Mailbox01 -IntraOrgConnectorProtocolLoggingLevel Verbose
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que habilitó o deshabilitó correctamente el registro de protocolo en el conector de envío interno de la organización, realice lo siguiente:

1.  En el Shell, ejecute el siguiente comando:
    
    ```powershell
    <Get-TransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List IntraOrgConnectorProtocolLoggingLevel
    ```

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Uso del Shell para habilitar o deshabilitar el registro de protocolos en el conector de envío de entrega del buzón de correo

Para habilitar o deshabilitar el registro de protocolo en el conector de envío de entrega de buzón de correo implícito e invisible que existe en el servicio de transporte de buzón de correo en el servidor Buzón de correo, ejecute el siguiente comando:

```powershell
Set-MailboxTransportService -MailboxDeliveryConnectorProtocolLoggingLevel <Verbose | None>
```

Este ejemplo habilita el registro de protocolo en el conector de recepción de entrega de buzón de correo en el servicio de transporte de buzón de correo de un servidor Buzón de correo denominado Mailbox01.

```powershell
Set-MailboxTransportService Mailbox01 -MailboxDeliveryConnectorProtocolLoggingLevel Verbose
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que habilitó o deshabilitó correctamente el registro de protocolo en el conector de envío del buzón, realice lo siguiente:

1.  En el Shell, ejecute el siguiente comando:
    
    ```powershell
    Get-MailboxTransportService <ServerIdentity> | Format-List MailboxDeliveryConnectorProtocolLoggingLevel
    ```

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Uso del Shell para configurar los valores de registro del protocolo

Para configurar los valores del registro del protocolo, ejecute el siguiente comando:

```powershell
<Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ReceiveProtocolLogPath <LocalFilePath> -SendProtocolLogPath <LocalFilePath> -ReceiveProtocolLogMaxFileSize <Size> -SendProtocolLogMaxFileSize <Size> -ReceiveProtocolLogMaxDirectorySize <Size> -SendProtocolLogMaxDirectorySize <Size> -ReceiveProtocolLogMaxAge <dd.hh:mm:ss> -SendProtocolLogMaxAge <dd.hh:mm:ss>
```

Este ejemplo establece la siguiente configuración de registro de protocolo en el servicio de transporte en el servidor Buzón de correo denominado Mailbox01:

  -  Establezca la ubicación de todos los registros del protocolo del conector de recepción en D:\\Hub Receive SMTP Log, y todos los registros de protocolo del conector de envío en D:\\Hub Send SMTP Log. Tenga en cuenta que si la carpeta no existe, se creará para usted.

  -  Establezca el tamaño máximo de un archivo de registro de protocolo del conector de recepción y establezca el tamaño del archivo de registro de protocolo del conector de envío en 20 MB.

  -  Establezca el tamaño máximo de la carpeta de registro de protocolo del conector de recepción y establezca el tamaño de la carpeta de registro de protocolo del conector de envío en 400 MB.

  -  Establezca el tamaño máximo de un archivo de registro de protocolo del conector de recepción y establezca el tamaño del archivo de registro de protocolo del conector de envío en 45 días.

<!-- end list -->

```powershell
Set-TransportService Mailbox01 -ReceiveProtocolLogPath "D:\Hub Receive SMTP Log" -SendProtocolLogPath "D:\Hub Send SMTP Log" -ReceiveProtocolLogMaxFileSize 20MB -SendProtocolLogMaxFileSize 20MB -ReceiveProtocolLogMaxDirectorySize 400MB -SendProtocolLogMaxDirectorySize 400MB -ReceiveProtocolLogMaxAge 45.00:00:00 -SendProtocolLogMaxAge 45.00:00:00
```

> [!NOTE]
> <UL>
> <LI>
> <P>Para configurar los valores del registro de protocolo en el servicio de transporte de buzones de correo en un servidor Buzón de correo, utilice el cmdlet <STRONG>Set-MailboxTransportService</STRONG>. Para configurar los valores del registro de protocolo en el servicio de transporte frontend en un servidor Acceso de cliente, utilice el cmdlet <STRONG>Set-FrontEndTransportService</STRONG>.</P>
> <LI>
> <P>Si el valor del parámetro <EM>SendProtocolLogPath</EM> o <EM>ReceiveProtocolLogPath</EM> se establece en <CODE>$null</CODE>, se deshabilita el registro de protocolo para todos los conectores de envío o de recepción del servidor. No obstante, la configuración de estos parámetros como <CODE>$null</CODE> genera errores de registro de eventos si el registro de protocolo está habilitado para cualquier conector en el servidor, incluyendo el conector de envío dentro de la organización o conector de envío de entrega del buzón de correo.</P>
> <LI>
> <P>Si se establece el valor del parámetro <EM>ReceiveProtocolLogMaxAge</EM> o <EM>SendProtocolLogMaxAge</EM> en <CODE>00:00:00</CODE>, se evita la eliminación automática de los archivos de registro de conectividad debido a la antigüedad.</P></LI></UL>



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que configuró correctamente el registro de protocolo, realice lo siguiente:

1.  En el Shell, ejecute el siguiente comando:
    
    ```powershell
    <Get-TransportService | Get-MailboxTransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List SendConnectorProtocolLog*,ReceiveConnectorProtocolLog*
    ```
    
2.  Verifique que los valores mostrados son los valores que ha configurado.

