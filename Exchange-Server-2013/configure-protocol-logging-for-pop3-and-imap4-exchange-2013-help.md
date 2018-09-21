---
title: 'Configurar del registro de protocolo para POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Configurar del registro de protocolo para POP3 e IMAP4
ms:assetid: 451b337b-cb6b-4460-8687-be0b19c469bc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997690(v=EXCHG.150)
ms:contentKeyID: 50556787
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar del registro de protocolo para POP3 e IMAP4

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-27_

Puede usar el Shell para habilitar, deshabilitar o modificar la configuración del registro de protocolo para POP3 e IMAP4. De forma predeterminada, el registro de protocolo no está habilitado.

El registro de protocolos le permite revisar las conexiones POP3 e IMAP4 en su entorno de Exchange. Puede resultar útil al solucionar problemas relacionados con el rendimiento de POP3 o IMAP4. Para obtener más información, consulte [Registro de protocolo para POP3 e IMAP4](protocol-logging-for-pop3-and-imap4-exchange-2013-help.md). Para obtener más información acerca de POP3 e IMAP4, consulte [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas “Configuración de POP3” y “Configuración de IMAP4” en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para habilitar el registro de protocolo para POP3 o IMAP4

En este ejemplo, se habilita el registro de protocolo para IMAP4 o POP3 en el servidor de acceso de cliente CAS01.

    Set-ImapSettings -Server "CAS01" -ProtocolLogEnabled $true
    Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true


> [!NOTE]
> Después de cambiar el registro de protocolos para POP3 e IMAP4, debe reiniciar el servicio que esté usando: POP3 o IMAP4. Para obtener más información acerca de cómo reiniciar los servicios POP3 e IMAP4, consulte <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Iniciar y detener los servicios POP3</A> y <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Iniciar y detener los servicios IMAP4</A>.



Para obtener más información acerca de la sintaxis y los parámetros, consulte [Set-ImapSettings](https://technet.microsoft.com/es-es/library/aa998252\(v=exchg.150\)) y [Set-POPSettings](https://technet.microsoft.com/es-es/library/aa997154\(v=exchg.150\)).

## Usar el Shell para deshabilitar el registro de protocolo para POP3 o IMAP4

En este ejemplo, se deshabilita el registro de protocolo para IMAP4 o POP3 en el servidor de acceso de cliente CAS01.

    Set-ImapSettings -Server "CAS01" -protocolLogEnabled $false
    Set-PopSettings -Server "CAS01" -protocolLogEnabled $false


> [!NOTE]
> Después de cambiar el registro de protocolos para POP3 e IMAP4, debe reiniciar el servicio que esté usando: POP3 o IMAP4. Para obtener más información acerca de cómo reiniciar los servicios POP3 e IMAP4, consulte <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Iniciar y detener los servicios POP3</A> y <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Iniciar y detener los servicios IMAP4</A>.



Para obtener más información acerca de la sintaxis y los parámetros, consulte [Set-ImapSettings](https://technet.microsoft.com/es-es/library/aa998252\(v=exchg.150\)) y [Set-POPSettings](https://technet.microsoft.com/es-es/library/aa997154\(v=exchg.150\)).

## Usar el Shell para modificar el registro de protocolo para POP3 o IMAP4

Para modificar la configuración de registro para POP3 o IMAP4, ejecute los cmdlets **Set-ImapSettings** o **Set-PopSettings** con uno o más de los siguientes parámetros.

  - *LogFileLocation*   Este parámetro especifica la ubicación de los archivos de registro del protocolo POP3 o IMAP4. De forma predeterminada, los archivos de registro del protocolo POP3 están ubicados en el directorio C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Pop3. En este ejemplo, se activa el registro del protocolo POP3 en el servidor de acceso de cliente CAS01. También se cambia el directorio de registro del protocolo POP3 por C:\\Pop3Logging.
    
    ```powershell
Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true -LogFileLocation "C:\Pop3Logging"
```

  - *LogFileRollOverSettings*   Este parámetro define la frecuencia con la que el registro del protocolo POP3 o IMAP4 crea un nuevo archivo de registro. De manera predeterminada, se crea un nuevo archivo de registro cada día. Los valores posibles son:
    
    Cada hora
    
    Diariamente
    
    Semanalmente
    
    Mensualmente
    
    Esta configuración se aplica solo cuando el valor del parámetro *LogPerFileSizeQuota* se establece en cero. En este ejemplo, se cambia el registro del protocolo POP3 en el servidor de acceso de cliente CAS01 para crear un nuevo archivo de registro cada hora.
    
    ```powershell
Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 0 -LogFileRollOverSettings Hourly
```

  - *LogPerFileSizeQuota*   Este parámetro define el tamaño máximo del archivo de registro del protocolo POP3 o IMAP4 en bytes. De manera predeterminada, este valor se establece en cero. Cuando este valor se establece en cero, se crea un nuevo archivo de registro de protocolo con la frecuencia especificada en el parámetro *LogFileRollOverSettings*.
    
    En este ejemplo, se cambia el registro del protocolo POP3 en el servidor de acceso de cliente CAS01 para crear un nuevo archivo de registro cuando un archivo de registro alcanza 2 megabytes (MB).
    
    ```powershell
Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 2000000
```
    
    En este ejemplo, se cambia el registro del protocolo POP3 en el servidor de acceso de cliente CAS01 para usar el mismo archivo de registro independientemente de la fecha de creación y el tamaño.
    
    ```powershell
Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota unlimited
```


> [!NOTE]
> Después de cambiar el registro de protocolos para POP3 e IMAP4, debe reiniciar el servicio que esté usando: POP3 o IMAP4. Para obtener más información acerca de cómo reiniciar los servicios POP3 e IMAP4, consulte <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Iniciar y detener los servicios POP3</A> y <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Iniciar y detener los servicios IMAP4</A>.



Para obtener más información acerca de la sintaxis y los parámetros, consulte [Set-ImapSettings](https://technet.microsoft.com/es-es/library/aa998252\(v=exchg.150\)) y [Set-POPSettings](https://technet.microsoft.com/es-es/library/aa997154\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Ejecute el siguiente comando en el Shell para comprobar la configuración del registro del protocolo POP3. Si está habilitado el registro de protocolo POP3, el valor para el parámetro *ProtocolLogEnabled* es `True`. Si está deshabilitado el protocolo POP3, el valor es `False`. También puede asegurarse de que los valores para los parámetros *LogFileLocation*, *LogPerFileSizeQuota* y *LogFileRollOverSettings* sean correctos.

```powershell
Get-PopSettings | format-list
```

Ejecute el siguiente comando en el Shell para comprobar la configuración del registro del protocolo IMAP4. Si está habilitado el registro de protocolo IMAP4, el valor para el parámetro *ProtocolLogEnabled* es `True`. Si está deshabilitado el registro de protocolo IMAP4, el valor es `False`. También puede asegurarse de que los valores para los parámetros *LogFileLocation*, *LogPerFileSizeQuota* y *LogFileRollOverSettings* sean correctos.

```powershell
Get-ImapSettings | format-list
```

## Más información

Después de configurar las opciones de registro de protocolo para POP3 e IMAP4, es posible que también desee:

[Iniciar y detener los servicios IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md)

[Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md)

