---
title: 'Realizar una limpieza remota en un teléfono móvil: Exchange 2013 Help'
TOCTitle: Realizar una limpieza remota en un teléfono móvil
ms:assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998614(v=EXCHG.150)
ms:contentKeyID: 52061871
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Realizar una limpieza remota en un teléfono móvil

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2013-02-06_

Los usuarios llevan información confidencial corporativa en los bolsillos todos los días. Si pierden el teléfono móvil, los datos pueden acabar en manos de terceros. En caso de que un usuario pierda el teléfono móvil, puede usar el Centro de administración de Exchange (EAC) o el Shell de administración de Exchange para borrar completamente toda la información personal y corporativa del teléfono.


> [!NOTE]
> En este tema también se proporcionan instrucciones acerca de cómo usar Microsoft&nbsp;Outlook Web App&nbsp;para realizar una eliminación remota de datos en un teléfono. El usuario debe haber iniciado sesión en Outlook Web App para realizar una eliminación remota de datos.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Dispositivos móviles" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Este procedimiento borrará todos los datos del teléfono móvil, como las aplicaciones instaladas, las fotos y la información personal.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Utilizar el EAC para borrar el teléfono de un usuario

Puede utilizar el EAC para borrar el teléfono de un usuario o cancelar un borrado remoto que todavía no se haya completado.

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  Seleccione el usuario y, en **Dispositivos móviles**, elija **Ver detalles**.

3.  En la página **Detalles del dispositivo móvil**, seleccione el dispositivo móvil perdido y, a continuación, seleccione **Borrar datos**.

4.  Seleccione **Guardar**.

## Usar el Shell para borrar el teléfono de un usuario

Puede utilizar el cmdlet **Clear-MobileDevice** en el Shell para borrar el teléfono de un usuario.

El siguiente comando borra el dispositivo denominado WM\_TonySmith y envía un mensaje de confirmación a admin@contoso.com.

    Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"

## Usar Outlook Web App para borrar el teléfono de un usuario

Los usuarios pueden borrar su propio teléfono usando Outlook Web App.

1.  En Outlook Web App, seleccione **Configuración \> Teléfono \> Dispositivos móviles**.

2.  Seleccione el teléfono móvil.

3.  Haga clic o pulse en el icono **Borrar datos del dispositivo**.

## ¿Cómo saber si el proceso se ha completado correctamente?

Hay varias maneras de comprobar si se ha completado el borrado remoto.

  - Ejecute el cmdlet **Clear-MobileDevice** con el parámetro *–NotificationEmailAddresses* configurado. Se enviará un mensaje a la dirección de correo suministrada cuando el borrado remoto se haya completado.

  - En el EAC, compruebe el estado del dispositivo móvil. El estado cambiará de **Borrado pendiente** a **Borrado completado**.

  - En Outlook Web App, compruebe el estado del dispositivo móvil. El estado cambiará de **Borrado pendiente** a **Borrado completado**.

