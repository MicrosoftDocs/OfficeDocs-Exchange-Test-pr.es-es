---
title: 'Configurar el registro de conectividad: Exchange 2013 Help'
TOCTitle: Configurar el registro de conectividad
ms:assetid: 24e46a79-33ea-44e9-b03c-549db1c86a6f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996827(v=EXCHG.150)
ms:contentKeyID: 49895520
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el registro de conectividad

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-18_

El registro de conectividad registra la actividad de conexiones salientes usada para transmitir mensajes desde un servicio de transportes en un servidor Exchange. El registro de conectividad registra el origen de la conexión, el destino y el número de mensajes y bytes transmitidos y la información de fallos de conexión.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas "servicio de transportes", "servicio de transporte de front-end" y "servicio de transporte de buzones" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Puede usar el Centro de administración de Exchange (EAC) para habilitar o deshabilitar el registro de conectividad, o establecer la ruta del registro de conectividad solo para el servicio de transportes. Para el resto de opciones de registro de conectividad en otros servicios de transportes, debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Utilice el EAC para configurar el registro de conectividad en el servicio de transportes

1.  En el EAC, vaya a **Servidores** \> **Servidores**.

2.  Seleccione el servidor de buzones de correo que desee configurar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **Registros de transporte**.

4.  En la sección **Registro de conectividad**, realice uno de los siguientes cambios:
    
      - **Habilitar el registro de seguimiento de mensajes**   Para deshabilitar el registro de seguimiento de mensajes en el servidor, desactive la casilla de verificación. Para habilitar el registro de seguimiento de mensajes en el servidor, seleccione la casilla de verificación.
    
      - **Ruta del archivo de registro de conectividad:**    El valor que especifique debe estar en el servidor Exchange. Si la carpeta no existe, se creará cuando usted haga clic en **Guardar**.
    
    Cuando haya terminado, haga clic en **Guardar**.

## Usar el Shell para configurar el registro de seguimiento de mensajes

Para configurar el registro de seguimiento de mensajes, ejecute el comando siguiente:

```powershell
<Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ConnectivityLogEnabled <$true | $false> -ConnectivityLogMaxAge <dd.hh:mm:ss> -ConnectivityLogMaxDirectorySize <Size> -ConnectivityLogMaxFileSize <Size> -ConnectivityLogPath <LocalFilePath>
```

Este ejemplo establece la siguiente configuración de registro de conectividad en el servidor de transporte en el servidor de buzones de correo denominado "Mailbox01":

  -  Establece la ubicación de los archivos de registro de conectividad al registro de conectividad D:\\Hub. Tenga en cuenta que si la carpeta no existe, se creará para usted.

  -  Establece el tamaño máximo de un archivo de registro de conectividad a 20 MB.

  -  Establece el tamaño máximo del directorio de registro de conectividad a 1,5 GB.

  -  La antigüedad máxima de un archivo de registro de conectividad se establece en 45 días.

<!-- end list -->

```powershell
Set-TransportService Mailbox01 -ConnectivityLogPath "D:\Hub Connectivity Log" -ConnectivityLogMaxFileSize 20MB -ConnectivityLogMaxDirectorySize 1.5GB -ConnectivityLogMaxAge 45.00:00:00
```

> [!NOTE]
> <UL>
> <LI>
> <P>Para configurar los ajustes del archivo de conectividad en el servicio de transporte de buzones de correo, use el cmdlet <STRONG>Set-MailboxTransportService</STRONG>. Para configurar los ajustes del archivo de conectividad en el servicio de transporte front-end, use el cmdlet <STRONG>Set-FrontEndTransportService</STRONG>.</P>
> <LI>
> <P>La configuración del parámetro <EM>ConnectivityLogPath</EM> en el valor <CODE>$null</CODE>, deshabilita de forma efectiva el registro de conectividad. Sin embargo, si el valor del parámetro <EM>ConnectivityLogEnabled</EM> es <CODE>$true</CODE>, se generan errores de registros de eventos.</P>
> <LI>
> <P>La configuración del parámetro <EM>ConnectivityLogMaxAge</EM> al valor <CODE>00:00:00</CODE> evita la eliminación automática de los archivos de registros de conectividad debido a su antigüedad.</P></LI></UL>



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya configurado correctamente los registros de conectividad, siga estos pasos:

1.  En el Shell, ejecute el siguiente comando:
    
    ```powershell
    <Get-TransportService | Get-FrontEndTransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List ConnectivityLog*
    ```
    
2.  Verifique que los valores mostrados son los valores que ha configurado.

