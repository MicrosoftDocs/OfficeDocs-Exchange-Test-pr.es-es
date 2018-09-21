---
title: 'Permitir usuarios finales ver configuración servidor POP3 IMAP4 y SMTP en OWA'
TOCTitle: Permitir que los de usuarios finales vean la configuración de servidor de POP3, IMAP4 y SMTP en Outlook Web App
ms:assetid: bd22bf7e-3bf7-45e6-8790-919b780166f6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg298947(v=EXCHG.150)
ms:contentKeyID: 50556874
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir que los de usuarios finales vean la configuración de servidor de POP3, IMAP4 y SMTP en Outlook Web App

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-28_

Si tiene usuarios que usan POP3 o IMAP4 para conectar sus buzones de Microsoft Exchange Server 2013, deben conocer la configuración de servidor correcta para conectarse a estos buzones. Después de una instalación predeterminada de Exchange 2013, los usuarios no pueden buscar su propia configuración de servidor IMAP4 o POP3 entrante ni la configuración del servidor SMTP saliente. No obstante, puede configurar Exchange para que los usuarios puedan buscar su propia configuración mediante MicrosoftOutlook Web App.

Después de realizar estos procedimientos, los usuarios pueden buscar su configuración de servidor en Outlook Web App de la siguiente manera:

1.  En Outlook Web App, haga clic en **Configuración** \> **Opciones**.

2.  En **Opciones**, haga clic en **Cuenta** \> **Mi cuenta** \> **Configuración para el acceso POP o IMAP**.

Para obtener más información acerca de POP3 e IMAP4, vea [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para permitir que los usuarios de POP3 e IMAP4 vean la configuración de POP3 e IMAP4 entrante en Outlook Web App

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas "Configuración POP3" y "Configuración IMAP4" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Este ejemplo muestra la configuración de servidor POP3 externa que será vista por los usuarios finales.

```powershell
Set-PopSettings -ExternalConnectionSettings {Dublin01.Contoso.com:995:SSL}
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-POPSettings](https://technet.microsoft.com/es-es/library/aa997154\(v=exchg.150\)).

Este ejemplo muestra la configuración de servidor IMAP4 externa que será vista por los usuarios finales.

```powershell
Set-ImapSettings -ExternalConnectionSettings {Dublin01.Contoso.com:993:SSL}
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ImapSettings](https://technet.microsoft.com/es-es/library/aa998252\(v=exchg.150\)).

Para aplicar estos cambios, debe reiniciar IIS. No necesita reiniciar los servicios de POP3. Para reiniciar IIS, escriba lo siguiente en una línea de comandos:

```powershell
iisreset
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que configuró Exchange para permitir que los usuarios vean la configuración del servidor POP3, siga estos pasos:

1.  Ejecute el siguiente comando en el Shell.
    
    ```powershell
Get-PopSettings | format-list
```

2.  Compruebe que la propiedad *ExternalConnectionSettings* está establecida.

Para comprobar que configuró Exchange para permitir que los usuarios vean la configuración del servidor IMAP4, siga estos pasos:

1.  Ejecute el siguiente comando en el Shell.
    
    ```powershell
Get-ImapSettings | format-list
```

2.  Compruebe que la propiedad *ExternalConnectionSettings* está establecida.

## Usar el Shell para permitir que los usuarios de POP3 e IMAP4 vean la configuración de SMTP saliente en Outlook Web App

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Conectores de recepción" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

En este ejemplo se muestra la configuración interna y externa del servidor SMTP que verán los usuarios finales que utilicen Outlook Web App.

    Get-ReceiveConnector "*Client Frontend*" | Set-ReceiveConnector -Fqdn Server.Contoso.com -AdvertiseClientSettings $true 

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125140\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que configuró Exchange para permitir que los usuarios vean la configuración del servidor SMTP, siga estos pasos:

1.  Ejecute el siguiente comando en el Shell.
    
    ```powershell
Get-ReceiveConnector | format-list
```

2.  Si la propiedad *AdvertiseClientSettings* está establecida en `true`, los usuarios pueden ver su configuración de servidor SMTP en Outlook Web App. Si *AdvertiseClientSettings* está establecido en `false`, los usuarios no pueden ver su configuración de servidor SMTP en Outlook Web App.

## Más información

Después de posibilitar que los usuarios finales vean su configuración de POP3, IMAP4 y SMTP, es posible que también desee:

[Habilitar o deshabilitar el acceso POP3 para un usuario](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[Habilitar o deshabilitar el acceso a IMAP4 para un usuario](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

