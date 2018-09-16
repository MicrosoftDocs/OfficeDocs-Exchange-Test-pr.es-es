---
title: 'Habilitar o deshabilitar el acceso POP3 para un usuario: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el acceso POP3 para un usuario
ms:assetid: 57e12f07-3b14-45bd-9a82-e6032d14214f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb691018(v=EXCHG.150)
ms:contentKeyID: 49895642
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar el acceso POP3 para un usuario

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-01-06_

Puede habilitar o deshabilitar POP3 para un usuario.


> [!NOTE]
> Después de habilitar o deshabilitar POP3 para un usuario, debe reiniciar el servicio POP3 de Microsoft Exchange y el servicio back-end POP3 de Microsoft Exchange. Para obtener más información acerca de cómo reiniciar el servicio POP3, consulte <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Iniciar y detener los servicios POP3</A>.



Para obtener más información acerca de la administración de buzones de usuario, vea [Administrar los buzones de usuario](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/include-text-with-email-sent-when-voicemail-is-enabled).

Para obtener más información acerca de POP3 e IMAP4, vea [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar o deshabilitar POP3 para un usuario

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En el panel de resultados, seleccione el usuario para el que desee habilitar o deshabilitar POP3 y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En el cuadro de diálogo **Buzón de usuario**, en el árbol de la consola, haga clic en **Características de buzón de correo**.
    
    En el panel de resultados, en **Conectividad de correo electrónico**, realice una de las siguientes acciones:
    
      - Para deshabilitar POP3 para el usuario, en **POP3: habilitado**, haga clic en **Deshabilitar**.
    
      - Para habilitar POP3 para el usuario, en **POP3: deshabilitado**, haga clic en **Habilitar**.

4.  Haga clic en **Guardar**.

## Usar el comando de shell para habilitar o deshabilitar POP3 para un usuario

En este ejemplo, se habilita POP3 para el usuario Juan Carlos Rivas.

    Set-CASMailbox -Identity "John Smith" -POPEnabled $true

En este ejemplo, se deshabilita POP3 para el usuario Juan Carlos Rivas.

    Set-CASMailbox -Identity "John Smith" -POPEnabled $false

## ¿Cómo saber si el proceso se ha completado correctamente?

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En el panel de resultados, seleccione el usuario para el que desee habilitar o deshabilitar POP3 y, a continuación, haga clic en **Editar**.

3.  En el cuadro de diálogo **Buzón de usuario**, en el árbol de la consola, haga clic en **Características de buzón de correo**.
    
    En el panel de resultados, busque en **Conectividad de correo electrónico**.
    
      - Si POP3 está habilitado para el usuario, verá **POP3: habilitado**.
    
      - Si POP3 está deshabilitado para el usuario, verá **POP3: deshabilitado**.

4.  Haga clic en **Guardar**.

