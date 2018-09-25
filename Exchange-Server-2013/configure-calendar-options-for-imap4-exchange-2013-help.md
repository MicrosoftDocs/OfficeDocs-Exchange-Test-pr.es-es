---
title: 'Configurar opciones de calendario para IMAP4: Exchange 2013 Help'
TOCTitle: Configurar opciones de calendario para IMAP4
ms:assetid: 6679c8b2-3f0f-449a-a17c-a7b30001538c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998606(v=EXCHG.150)
ms:contentKeyID: 50556804
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar opciones de calendario para IMAP4

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-27_

Puede usar el Shell para configurar los ajustes de acceso al calendario para los usuarios que conectan sus buzones usando conexiones IMAP4. La configuración que especifique determinan de qué manera sus usuarios de IMAP4 pueden obtener acceso a su calendario e intercambiar su información de calendario (por ejemplo, enviar o responder una convocatoria de reunión) con otros usuarios.

Para obtener más información acerca de IMAP4, consulte [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de IMAP4" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para establecer las opciones de calendario para IMAP4

En este ejemplo, se habilitan usuarios de IMAP4 para usar el estándar de iCalendar, un estándar para intercambiar información de calendario.

```powershell
Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

En este ejemplo, se permite que los usuarios de IMAP4 obtengan acceso a la información de calendario desde un servidor interno.

```powershell
Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl
```

En este ejemplo, se permite que los usuarios de IMAP4 obtengan acceso a la información de calendario desde Internet o un servidor externo.

```powershell
Set-ImapSettings -CalendarItemRetrievalOption InternetUrl
```

En este ejemplo, se habilita a los usuarios de IMAP4 a obtener acceso a la información de calendario mediante una URL de Outlook Web App directa. Si está usando `Custom`, debe especificar una URL de Outlook Web App con el parámetro *OWAServerUrl*.

```powershell
Set-Imap4Settings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

Después de especificar las opciones de calendario para IMAP4, debe reiniciar los servicios IMAP4. Para obtener más información acerca de cómo reiniciar los servicios IMAP4, consulte [Iniciar y detener los servicios IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Para obtener más información sobre sintaxis y parámetros, consulte [Set-ImapSettings](https://technet.microsoft.com/es-es/library/aa998252\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que las opciones de calendario se hayan creado correctamente, siga estos pasos:

Ejecute el siguiente comando en el Shell.

```powershell
Get-ImapSettings | format-list
```

Compruebe que la configuración del calendario sea correcta.

## Más información

Después de establecer las opciones de calendario para IMAP4, es posible que también desee realizar las siguientes tareas:

[Configurar las opciones de formato de recepción de mensajes POP3 e IMAP4](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[Establecer límites de tiempo de espera de conexión para IMAP4](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

