---
title: 'Configurar límites tamaño mensaje para un buzón de correo: Exchange 2013 Help'
TOCTitle: Configurar límites de tamaño de mensaje para un buzón de correo
ms:assetid: d1220685-14c0-4c4f-abb2-3920f3046212
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124708(v=EXCHG.150)
ms:contentKeyID: 50556887
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar límites de tamaño de mensaje para un buzón de correo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-12_

Puede usar la EAC o el Shell para configurar los límites de tamaño de mensaje de un buzón de usuario. Estos límites controlan el tamaño de los mensajes que un usuario puede enviar o recibir. De manera predeterminada, cuando se crea un buzón, no hay ningún límite de tamaño para los mensajes enviados y recibidos.

Tenga en cuenta que hay otra configuración en una organización de Exchange que determina el tamaño máximo de los mensajes que un buzón puede enviar o recibir (por ejemplo, el tamaño máximo de mensaje configurado en un servidor de buzones). Para obtener más información acerca de las restricciones en el tamaño de los mensajes de Exchange, incluidos los tipos de límites de tamaño de mensaje, su ámbito y el orden de precedencia, consulte [Límites de tamaño de mensaje](message-size-limits-exchange-2013-help.md).

Para otras tareas de administración relacionadas con los buzones de usuario, consulte [Administrar los buzones de usuario](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/include-text-with-email-sent-when-voicemail-is-enabled).


> [!NOTE]
> También puede controlar el tamaño de los mensajes enviados y recibidos por usuarios de correo y desde buzones compartidos.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para configurar los límites de tamaño de mensajes

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón cuyos límites de tamaño de mensaje desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic en **Características de buzón de correo**.

4.  En **Restricciones en el tamaño de mensajes**, haga clic en **Ver detalles** para ver y cambiar los siguientes límites de tamaño de mensajes:
    
      - **Mensajes enviados**   Para indicar el tamaño máximo de los mensajes enviados por este usuario, active la casilla **Tamaño máximo de mensaje (en KB)** y escriba un valor en el cuadro. El tamaño del mensaje debe estar entre 0 y 2.097.151 KB. Si el usuario envía un mensaje que supera el tamaño indicado, se le devolverá con un mensaje de error descriptivo.
    
      - **Mensajes recibidos**   Para indicar el tamaño máximo de los mensajes recibidos por este usuario, active la casilla **Tamaño máximo de mensaje (en KB)** y escriba un valor en el cuadro. El tamaño del mensaje debe estar entre 0 y 2.097.151 KB. Si el usuario recibe un mensaje que supera el tamaño indicado, se devuelve al emisor con un mensaje de error descriptivo.

5.  Haga clic en **Aceptar** y, a continuación, haga clic en **Guardar** para guardar los cambios.

## Usar el Shell para configurar los límites de tamaño de mensajes

En este ejemplo se establece el tamaño máximo de los mensajes enviados en 25 MB y el tamaño máximo de los mensajes recibidos en 35 MB para el buzón de Debra García.

```powershell
Set-Mailbox "Debra Garcia" -MaxSendSize 25mb -MaxReceiveSize 35mb
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si configuró los límites de tamaño de mensajes para un buzón correctamente, siga uno de estos procedimientos:

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón cuyos límites de tamaño de mensaje desea comprobar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic en **Características de buzón de correo**.

4.  En **Restricciones en el tamaño de mensajes**, haga clic en **Ver detalles** para comprobar los límites de tamaño de mensajes para el buzón.

O bien

Ejecute el siguiente comando en el Shell.

```powershell
Get-Mailbox <identity> | fl MaxSendSize,MaxReceiveSize
```

