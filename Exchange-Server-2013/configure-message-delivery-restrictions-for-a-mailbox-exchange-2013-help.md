---
title: 'Configurar restricciones entrega mensajes para buzón correo Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configurar restricciones de entrega de mensajes para un buzón de correo
ms:assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb397214(v=EXCHG.150)
ms:contentKeyID: 50556880
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar restricciones de entrega de mensajes para un buzón de correo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-11-29_

Puede usar la EAC o el Shell para establecer restricciones sobre si los mensajes se entregan a destinatarios individuales. Las restricciones de entrega de mensajes resultan útiles para controlar quién puede enviar mensajes a los usuarios de una organización. Por ejemplo, puede configurar un buzón para aceptar o rechazar mensajes enviados por usuarios específicos o aceptar mensajes procedentes solo de usuarios de la organización de Exchange.

Las restricciones en la entrega de mensajes que se describen en este tema se aplican a todos los tipos de destinatario. Para obtener más información acerca de los diferentes tipos de destinatario, consulte [Destinatarios](recipients-exchange-2013-help.md).

Para consultar otras tareas de administración relacionadas con los destinatarios, vea los siguientes temas:

  - [Administrar los buzones de usuario](manage-user-mailboxes-exchange-2013-help.md)

  - [Crear y administrar grupos de distribución](create-and-manage-distribution-groups-exchange-2013-help.md)

  - [Administrar grupos de distribución dinámica](manage-dynamic-distribution-groups-exchange-2013-help.md)

  - [Administrar usuarios de correo](manage-mail-users-exchange-2013-help.md)

  - [Administrar contactos de correo](manage-mail-contacts-exchange-2013-help.md)

## What do you need to know before you begin?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para configurar restricciones de entrega de mensajes

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón para el que desea configurar restricciones de entrega de mensajes y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic en **Características de buzón de correo**.

4.  En **Restricciones en la entrega de mensajes**, haga clic en **Ver detalles** para ver y cambiar las siguientes restricciones de entrega:
    
      - **Aceptar mensajes de**   Esta sección sirve para indicar quién puede enviar mensajes a este usuario.
        
          - **Todos los remitentes**   Esta opción especifica que el usuario puede aceptar mensajes de todos los remitentes. Se incluyen los remitentes de la organización de Exchange y los remitentes externos. Es la opción predeterminada. Incluye a los usuarios externos solo si desactiva la casilla **Requerir la autenticación de todos los remitentes**. Si activa esta casilla, se rechazarán los mensajes de los usuarios externos.
        
          - **Solo los remitentes de la siguiente lista**   Esta opción especifica que el usuario puede aceptar mensajes solo de un grupo específico de remitentes de la organización de Exchange. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para mostrar una lista de todos los destinatarios de la organización de Exchange. Seleccione los destinatarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").
        
          - **Requerir la autenticación de todos los remitentes**   Esta opción impide que usuarios anónimos envíen mensajes al usuario. Aquí se incluyen los usuarios externos que estén fuera de la organización de Exchange.
    
      - **Rechazar mensajes de**   Use esta sección para bloquear a ciertas personas para que no envíen mensajes a este usuario.
        
          - **Sin remitentes**   Esta opción especifica que el buzón de correo no rechazará mensajes de ningún remitente de la organización de Exchange. Es la opción predeterminada.
        
          - **Remitentes de la siguiente lista**   Esta opción especifica que el buzón de correo rechazará mensajes de un grupo específico de remitentes de la organización de Exchange. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para mostrar una lista de todos los destinatarios de la organización de Exchange. Seleccione los destinatarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").

5.  Haga clic en **Aceptar** para cerrar la página **Restricciones en la entrega de mensajes** y, a continuación, haga clic en **Guardar** para guardar los cambios.

## Usar el Shell para configurar las restricciones en la entrega de mensajes

En este ejemplo se muestra cómo usar el Shell para configurar las restricciones en la entrega de mensajes para un buzón. Para otro tipo de destinatarios, use el cmdlet **Set-** correspondiente con los mismos parámetros.

En este ejemplo se configura el buzón de Robin Wood para aceptar mensajes procedentes solo de los usuarios Lori Penor, Jeff Phillips y de los miembros del grupo de distribución Legal Team 1.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"


> [!NOTE]
> Si configura un buzón para que acepte mensajes solamente de remitentes individuales, utilice el parámetro <EM>AcceptMessagesOnlyFrom</EM>. Si configura un buzón para que acepte mensajes solamente de remitentes que son miembros de un grupo de distribución específico, utilice el parámetro <EM>AcceptMessagesOnlyFromDLMembers</EM>.



En este ejemplo se agrega el usuario llamado David Pelton a la lista de usuarios cuyos mensajes aceptará el buzón de Robin Wood.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}

En este ejemplo se configura el buzón de Robin Wood para solicitar que se autentiquen todos los remitentes. Esto significa que el buzón solo aceptará los mensajes enviados por otros usuarios de la organización de Exchange.

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true

En este ejemplo se configura el buzón de Robin Wood para rechazar mensajes procedentes de los usuarios Joe Healy, Terry Adams y de los miembros del grupo de distribución Legal Team 2.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"

En este ejemplo se configura el buzón de Robin Wood para rechazar también los mensajes enviados por los miembros del grupo Legal Team 3.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}


> [!NOTE]
> Si configura un buzón para que rechace mensajes de remitentes individuales, utilice el parámetro <EM>RejectMessagesFrom</EM>. Si configura un buzón para que rechace mensajes de remitentes que son miembros de un grupo de distribución específico, utilice el parámetro <EM>RejectMessagesFromDLMembers</EM>.



Para obtener información detallada sobre la sintaxis y los parámetros relacionados con la configuración de las restricciones de entrega para los distintos tipos de destinatarios, consulte los siguientes temas:

  - [Set-DistributionGroup](https://technet.microsoft.com/es-es/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/es-es/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/es-es/library/aa995950\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/es-es/library/aa995971\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si configuró las restricciones de entrega de mensajes para un buzón de usuario correctamente, siga uno de estos procedimientos:

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón para el que desea comprobar las restricciones de entrega de mensajes y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic en **Características de buzón de correo**.

4.  En **Restricciones en la entrega de mensajes**, haga clic en **Ver detalles** para comprobar las restricciones de entrega para el buzón.

O bien

Ejecute el siguiente comando en el Shell.

    Get-Mailbox <identity> | fl AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

