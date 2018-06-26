---
title: 'Configurar las opciones de calendario para POP3: Exchange 2013 Help'
TOCTitle: Configurar las opciones de calendario para POP3
ms:assetid: ac3d60a0-8697-4c06-9e93-f8d2c4b157b6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124133(v=EXCHG.150)
ms:contentKeyID: 50556853
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar las opciones de calendario para POP3

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-11-27_

Puede usar el Shell para configurar los parámetros de acceso al calendario de los usuarios que conectan sus buzones de correo con conexiones POP3. La configuración que especifique determina cómo sus usuarios de POP3 pueden acceder a su calendario e intercambiar información del calendario (por ejemplo, enviar o responder a una solicitud de reunión) con otros usuarios.

Para obtener más información acerca de POP3, consulte [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración POP3" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Shell para establecer las opciones de calendario de POP3

Este ejemplo permite a los usuarios de POP3 usar el estándar iCalendar, un estándar para intercambiar información de calendario.

    Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar

En este ejemplo, se habilita a los usuarios de POP3 para tener acceso a la información de calendario interno desde un servidor interno.

    Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 

En este ejemplo, se habilita a los usuarios de POP3 para tener acceso a la información de calendario desde Internet en un servidor externo.

    Set-PopSettings -CalendarItemRetrievalOption InternetUrl

En este ejemplo, se habilita a los usuarios de POP3 para tener acceso a la información de calendario mediante una URL directa de Outlook Web App. Si usa `Custom`, debe especificar una URL de Outlook Web App con el parámetro *OWAServerUrl*.

    Set-PopSettings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"

Una vez haya especificado las opciones de calendario para POP3, debe reiniciar los servicios POP3. Para obtener más información acerca de cómo reiniciar los servicios POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obtener más información sobre sintaxis y parámetros, consulte [Set-POPSettings](https://technet.microsoft.com/es-es/library/aa997154\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se han establecido correctamente las opciones de calendario, siga estos pasos:

Ejecute el siguiente comando en el Shell.

    Get-PopSettings | format-list

Compruebe que la configuración del calendario sea correcta.

## Más información

Después de establecer las opciones de calendario de POP3, quizá también desee:

[Configurar las opciones de formato de recepción de mensajes POP3 e IMAP4](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[Establecer límites de tiempo de espera de conexión para POP3](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

