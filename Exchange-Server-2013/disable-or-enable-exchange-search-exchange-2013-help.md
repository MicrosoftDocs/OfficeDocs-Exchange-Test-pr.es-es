---
title: 'Deshabilitar o habilitar el servicio de búsqueda de Exchange: Exchange 2013 Help'
TOCTitle: Deshabilitar o habilitar el servicio de búsqueda de Exchange
ms:assetid: 195b25be-53fb-4215-90a5-04340d640bcc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996416(v=EXCHG.150)
ms:contentKeyID: 52062007
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Deshabilitar o habilitar el servicio de búsqueda de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-05-07_

De forma predeterminada, el servicio de búsqueda de Exchange está habilitado para todas las nuevas bases de datos de buzones y no precisa configuración adicional. Sin embargo, si desea que la búsqueda de Exchange no realice una indización del contenido del buzón, puede deshabilitarla para bases de datos individuales o para un servidor de buzones completo.


> [!WARNING]
> Deshabilitar la búsqueda de Exchange influye en las funciones y el rendimiento de las búsquedas de texto completo que hacen los usuarios con Outlook en el modo en línea o en dispositivos móviles de Windows.<BR><A href="in-place-ediscovery-exchange-2013-help.md">Exhibición de documentos electrónicos en contexto</A> también se basa en la búsqueda de Exchange. Si deshabilita la búsqueda de Exchange para una base de datos de buzones de correo o para un servidor de buzones, las búsquedas de la exhibición de documentos electrónicos en contexto no devolverán ningún mensaje de la base de datos ni del servidor.



Para otras tareas de administración relacionadas con la búsqueda de Exchange, consulte [Procedimientos de búsqueda de Exchange](exchange-search-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 1 minuto

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Puede habilitar o deshabilitar la búsqueda de Exchange para servidores o bases de datos de buzones de correo, pero no para usuarios de buzones individuales.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## ¿Qué desea hacer?

## Deshabilitar o habilitar la búsqueda de Exchange para una base de datos de buzones

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Exchange Search" en el tema de [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).


> [!NOTE]
> No puede usar el EAC para deshabilitar ni habilitar la búsqueda de Exchange en una base de datos de buzones de correo.



Este comando deshabilita el servicio de búsqueda de Exchange para la base de datos de buzones llamada EXCH01.

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $false

Este comando habilita el servicio de búsqueda de Exchange para la base de datos de buzones llamada EXCH01.

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)).

## Deshabilitar o habilitar la búsqueda de Exchange para un servidor de buzones

Para deshabilitar el servicio de búsqueda de Exchange para un servidor de buzón de correo, debe deshabilitar y detener el servicio de búsqueda de Microsoft Exchange. Del mismo modo, para habilitar el servicio de búsqueda de Exchange para un servidor de buzón de correo, debe habilitar e iniciar el servicio de búsqueda de Microsoft Exchange. Puede usar la consola Servicios o el Shell para hacerlo.

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada “Administrar el servicio de búsqueda de Exchange en un servidor de buzones de correo” en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

**Uso de la consola Servicios**

1.  Vaya hasta **Inicio** \> **Herramientas administrativas** \> **Servicios**.

2.  En el panel de detalles de **Servicios**, haga clic con el botón secundario en el servicio **Búsqueda de Microsoft Exchange** y seleccione **Propiedades**.

3.  En la ficha **General**, en la lista **Tipo de inicio**, seleccione **Deshabilitado** para deshabilitar el servicio o **Automático** para iniciarlo automáticamente.
    

    > [!NOTE]
    > El tipo de inicio influye en el servicio la próxima vez que se realiza un intento de iniciarlo, ya sea automáticamente después de haber reiniciado el servidor o mediante el inicio manual del servicio. En el próximo paso, el servicio se detiene o se inicia manualmente.



4.  Haga clic en **Detener** para detener el servicio o en **Iniciar** para iniciar el servicio.

5.  Haga clic en **Aceptar** para guardar los cambios.

**Uso del Shell**

Ejecute los siguientes comandos para detener y deshabilitar el servicio de búsqueda de Microsoft Exchange.
```
    Stop-Service MSExchangeFastSearch
```
```
    Set-Service MSExchangeFastSearch -StartupType Disabled
```

Ejecute los siguientes comandos para configurar el servicio de búsqueda de Exchange para que se inicie automáticamente y luego inicie el servicio.
```
    Set-Service MSExchangeFastSearch -StartupType Automatic
```
```
    Start-Service MSExchangeFastSearch
```
