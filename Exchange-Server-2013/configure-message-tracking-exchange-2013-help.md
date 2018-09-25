---
title: 'Configurar el seguimiento de mensajes: Exchange 2013 Help'
TOCTitle: Configurar el seguimiento de mensajes
ms:assetid: 50eb5213-cf27-4179-b427-38d751ee4a70
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997984(v=EXCHG.150)
ms:contentKeyID: 51406514
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el seguimiento de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-18_

El seguimiento de mensajes registra la actividad de transporte SMTP de todos los mensajes transferidos al servicio de transporte o a los buzones de correo, y desde estos, en un servidor de buzones de Microsoft Exchange Server 2013. Puede utilizar los registros de seguimiento de mensajes para análisis de mensajes, análisis del flujo de correo, elaboración de informes y solución de problemas.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servicio de transporte" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md) o entrada "Configuración del servidor de buzones" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Puede utilizar el Centro de administración de Exchange (EAC) para habilitar o deshabilitar el seguimiento de mensajes o establecer su ruta de registro. Para el resto de las opciones de seguimiento de mensajes, debe utilizar el Shell de administración de Exchange.

  - En un servidor de buzones Exchange 2013, puede usar tanto el cmdlet **Set-TransportService** como **Set-MailboxServer** para configurar las opciones de seguimiento de mensajes. Los procedimientos en este tema usan el cmdlet **Set-TransportService**.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el EAC para configurar el seguimiento de mensajes en los servidores de buzón

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  Seleccione el servidor Buzón de correo que desee configurar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **Registros de transporte**.

4.  En la sección **Registro de seguimiento de mensajes**, realice uno de los siguientes cambios:
    
      - **Habilitar el registro de seguimiento de mensajes**   Para deshabilitar el seguimiento de mensajes en el servidor, desactive la casilla. Para habilitar el seguimiento de mensajes en el servidor, actívela.
    
      - **Ruta del archivo de registro de seguimiento de mensajes**   El valor que especifique debe estar en el servidor Exchange local. Si la carpeta no existe, se creará cuando usted haga clic en **Guardar**.

5.  Haga clic en **Guardar**.

## Usar el Shell para configurar el seguimiento de mensajes

Para configurar el seguimiento de mensajes, ejecute el siguiente comando:

```powershell
Set-TransportService <ServerIdentity> -MessageTrackingLogEnabled <$true | $false> -MessageTrackingLogMaxAge <dd.hh:mm:ss> -MessageTrackingLogMaxDirectorySize <Size> -MessageTrackingLogMaxFileSize <Size> -MessageTrackingLogPath <LocalFilePath> -MessageTrackingLogSubjectLoggingEnabled <$true|$false>
```

En este ejemplo, se establece la siguiente configuración de registro de seguimiento de mensajes en el servidor de buzones denominado Mailbox01:

  -  Establece la ubicación de los archivos de registro de seguimiento de mensajes en D:\\Message Tracking Log. Tenga en cuenta que si la carpeta no existe, se creará para usted.

  -  Establece el tamaño máximo de un archivo de registro de seguimiento de mensajes en 20 MB.

  -  Establece el tamaño máximo del directorio de registro de seguimiento de mensajes en 1,5 GB.

  -  Establece la antigüedad máxima de un archivo de registro de seguimiento de mensajes en 45 días.

<!-- end list -->

```powershell
Set-TransportService Mailbox01 -MessageTrackingLogPath "D:\Hub Message Tracking Log" -MessageTrackingLogMaxFileSize 20MB -MessageTrackingLogMaxDirectorySize 1.5GB -MessageTrackingLogMaxAge 45.00:00:00
```


> [!NOTE]
> <UL>
> <LI>
> <P>La configuración del parámetro <EM>MessageTrackingLogPath</EM> en el valor <CODE>$null</CODE> deshabilita de forma efectiva el seguimiento de mensajes. Sin embargo, si el valor del parámetro <EM>MessageTrackingLogEnabled</EM> es <CODE>$true</CODE>, se generan errores de registros de eventos.</P>
> <LI>
> <P>La configuración del parámetro <EM>MessageTrackingLogMaxAge</EM> en el valor <CODE>00:00:00</CODE> evita la eliminación automática de los archivos de registro de seguimiento de mensajes debido a la antigüedad.</P>
> <LI>
> <P>En servidores de buzones de Exchange&nbsp;2013, el tamaño máximo del directorio de registro de seguimiento de mensajes es el triple del valor del parámetro <EM>MessageTrackingLogMaxDirectorySize</EM>. Aunque los archivos del registro de seguimiento de mensajes generados por los cuatro servicios diferentes tienen cuatro prefijos de nombre distintos, la cantidad y la frecuencia de los datos escritos en los archivos de registros <STRONG>MSGTRKMA</STRONG> son insignificantes en comparación con los otros prefijos de archivos de registro. Para obtener más información, consulte la sección "Estructura de los archivos de registro de seguimiento de mensajes" en el tema <A href="message-tracking-exchange-2013-help.md">Seguimiento de mensajes</A>.</P></LI></UL>



En este ejemplo se deshabilita el registro del asunto del mensaje en el registro de seguimiento de mensajes del servidor de buzones de correo Mailbox01:

```powershell
Set-TransportService Mailbox01 -MessageTrackingLogSubjectLoggingEnabled $false
```

En este ejemplo se deshabilita el seguimiento de mensajes en el servidor de buzones de correo Mailbox01:

```powershell
Set-TransportService Mailbox01 -MessageTrackingLogEnabled $false
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha configurado correctamente el seguimiento de mensajes, siga estos pasos:

1.  En el Shell, ejecute el siguiente comando:
    
    ```powershell
    Get-TransportService <ServerIdentity> | Format-List MessageTrackingLog*
    ```

2.  Verifique que los valores mostrados son los valores que ha configurado.

