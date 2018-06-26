---
title: 'Configurar el reenvío de correo electrónico para un buzón de correo: Exchange 2013 Help'
TOCTitle: Configurar el reenvío de correo electrónico para un buzón de correo
ms:assetid: c7a7afaf-577e-49d6-8cee-bb4c4a5d570b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351134(v=EXCHG.150)
ms:contentKeyID: 50556882
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el reenvío de correo electrónico para un buzón de correo

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

El reenvío de correo electrónico permite configurar un buzón de correo para reenviar a otro destinatario mensajes de correo electrónico enviados a ese usuario dentro o fuera de la organización.


> [!IMPORTANT]
> Si usa Office 365 para empresas, debe configurar el reenvío de correo electrónico en el <A href="https://go.microsoft.com/fwlink/p/?linkid=834774">Centro de administración de Office 365: Configurar el reenvío de correo electrónico en Office 365</A>



Si su organización usa un entorno híbrido de Exchange o Exchange local, debe usar el Centro de administración de Exchange (EAC) local para crear y administrar buzones compartidos.

## Usar el Centro de administración de Exchange para configurar el reenvío de correo electrónico

Puede usar el Centro de administración de Exchange (EAC) para configurar el reenvío de correo electrónico a un único destinatario interno (mediante un contacto de correo) o a varios (mediante un grupo de distribución).

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic o pulse en el buzón para el que desea configurar el reenvío de correo y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic en **Características de buzón de correo**.

4.  En **Flujo de correo**, seleccione **Ver detalles** para ver o cambiar la configuración para reenviar mensajes de correo electrónico.
    
    En esta página también puede establecer el número máximo de destinatarios a los que el usuario puede enviar mensajes. Para las organizaciones locales de Exchange, el límite de destinatarios es ilimitado. Para las organizaciones de Exchange Online, el límite es de 500 destinatarios.

5.  Active la casilla **Habilitar el reenvío** y luego haga clic en **Examinar**.

6.  En la página **Seleccionar destinatario**, seleccione un usuario al que desea reenviarle el correo electrónico. Active la casilla **Entregar el mensaje en la dirección de reenvío y en el buzón** si desea que tanto el destinatario como la dirección de correo electrónico de reenvío reciban una copia de los mensajes enviados. Haga clic o pulse en **Aceptar** y luego haga clic o pulse en **Guardar**.

¿Qué ocurre si desea reenviar correo electrónico a una dirección de correo electrónico externa a la organización? ¿O reenviar correo a varios destinatarios? También puede hacerlo.

  - **Direcciones externas**Cree un contacto de correo y, a continuación, en los pasos anteriores, seleccione el contacto de correo en la página **Seleccionar destinatario**. ¿Necesita saber cómo crear un contacto de correo? Consulte [Administrar contactos de correo](manage-mail-contacts-exchange-2013-help.md).

  - **Varios destinatarios**Cree un grupo de distribución, agregue destinatarios y, a continuación, en los pasos anteriores, seleccione el contacto de correo en la página **Seleccionar destinatario**. ¿Necesita saber cómo crear un contacto de correo? Consulte [Crear y administrar grupos de distribución](create-and-manage-distribution-groups-exchange-2013-help.md).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para asegurarse de que configuró el reenvío de correo correctamente, siga uno de estos procedimientos:

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic o pulse en el buzón para el que configuró el reenvío de correo electrónico y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic o pulse en **Características de buzón de correo**.

4.  En **Flujo de correo**, haga clic o pulse en **Ver detalles** para ver la configuración de reenvío de correo.

## Información adicional

Este tema es para administradores. Si desea reenviar su correo electrónico a otro destinatario, consulte los siguientes temas:

  - [Reenviar correo electrónico a otra cuenta de correo electrónico](https://go.microsoft.com/fwlink/p/?linkid=510866)

  - [Administrar mensajes de correo electrónico mediante reglas](https://go.microsoft.com/fwlink/p/?linkid=510869)

Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

