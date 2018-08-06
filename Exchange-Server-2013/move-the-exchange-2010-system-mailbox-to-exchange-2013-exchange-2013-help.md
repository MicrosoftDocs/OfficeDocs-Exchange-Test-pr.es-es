---
title: 'Mover el buzón del sistema de Exchange 2010 a Exchange 2013 Exchange 2013 Help | Microsoft Docs'
TOCTitle: Mover el buzón del sistema de Exchange 2010 a Exchange 2013
ms:assetid: a3b03c4e-0bc7-41a2-885c-e9cac37566c8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn249849(v=EXCHG.150)
ms:contentKeyID: 54914907
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mover el buzón del sistema de Exchange 2010 a Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

En Exchange 2010, el buzón del sistema de Microsoft Exchange es un buzón de arbitraje que se usa para almacenar datos de toda la organización, como registros de auditoría de administrador, metadatos para búsquedas de exhibición de documentos electrónicos y datos de Mensajería unificada, como menús, planes de marcado y saludos personalizados. El buzón del sistema de Microsoft Exchange se denomina **SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}**; el nombre para mostrar es **Microsoft Exchange**.

Al actualizar la organización de Exchange 2010 existente a Exchange 2013, tiene que mover el buzón del sistema de Microsoft Exchange a una base de datos de buzones de un servidor de buzones de Exchange 2013. Debe mover este buzón después de instalar y comprobar Exchange 2013. Si no se mueve este buzón del sistema a Exchange 2013, se producirán los siguientes problemas si Exchange 2010 y Exchange 2013 coexisten en la organización de Exchange:

  - Las tareas de Exchange 2013 no se guardarán en el registro de auditoría de administrador. Al ejecutar el cmdlet **Search-AdminAuditLog** o tratar de exportar el registro de auditoría de administrador en el EAC, recibirá un error que le indicará que no puede crear una búsqueda del registro de auditoría de administrador porque el buzón del sistema, SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}, se encuentra en un servidor que no ejecuta Exchange 2013. Además, se registrará un error de Microsoft Exchange con el id. de evento 5000 en el registro de aplicaciones de Windows cada vez que se ejecute un comando.

  - No se podrán ejecutar búsquedas de exhibición de documentos electrónicos mediante el EAC o el Shell en Exchange 2013. Será posible crear búsquedas de buzones y ponerlas en cola, pero se podrán iniciar. Se registrará un error con el id. de evento 6 en el registro de administración de MsExchange. El error indicará que el cmdlet **Start-MailboxSearch** no se pudo ejecutar correctamente. Sin embargo, podrá explorar los buzones con el Shell y el panel de control de Exchange (ECP) en Exchange 2010.

También tendrá que mover el buzón del sistema de Microsoft Exchange a Exchange 2013 como parte de la actualización de la Mensajería unificada de Exchange 2010 a Exchange 2013.

Para más información sobre la actualización a Exchange 2013, consulte los siguientes temas:

  - [Actualizar de Exchange 2010 a Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)

  - [Actualizar la mensajería unificada (UM) de Exchange 2010 a la mensajería unificada de Exchange 2013](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 20 minutos. El tiempo real puede variar en función del tamaño del buzón del sistema.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada “Permisos de movimiento y migración de buzones” en [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Ejecute el siguiente comando en Exchange 2013 para obtener la identidad y la versión de los servidores de Exchange y las bases de datos de buzones de correo que contienen los buzones del sistema de la organización.
    
        Get-Mailbox -Arbitration | FL Name,DisplayName,ServerName,Database,AdminDisplayVersion
    
    La propiedad **AdminDisplayVersion** indica la versión de Exchange que ejecuta el servidor. El valor `Version 14.x` indica Exchange 2010. El valor `Version 15.x` indica Exchange 2013.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué quiere hacer?

## Usar el EAC para mover el buzón del sistema

1.  En el EAC, vaya a **Destinatarios** \> **Migración**.

2.  Haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, luego, haga clic en **Mover a una base de datos diferente**.

3.  En la página **Nuevo movimiento de buzón local**, haga clic en **Seleccionar los usuarios que quiere mover** y, luego, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En la página **Seleccionar buzón**, agregue el buzón que tenga las siguientes propiedades:
    
      - El nombre para mostrar es **Microsoft Exchange**.
    
      - El alias de la dirección de correo electrónico del buzón es **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**.

5.  Haga clic en **Aceptar** y, luego, en **Siguiente**.

6.  En la página **Configuración de la transferencia**, escriba el nombre del lote de migración y, luego, haga clic en **Examinar** junto al cuadro **Base de datos de destino**.

7.  En la página **Seleccionar base de datos de buzones de correo**, agregue la base de datos de buzones de correo a la que quiera mover el buzón del sistema. Asegúrese de que la versión de la base de datos de buzones de correo que seleccione sea la 15.x, lo que indica que la base de datos se encuentra en un servidor Exchange 2013.

8.  Haga clic en **Aceptar** y, luego, en **Siguiente**.

9.  En la página **Iniciar el lote**, seleccione las opciones para iniciar y completar automáticamente la solicitud de migración y, luego, haga clic en **Nuevo**.

## Usar el Shell para mover el buzón del sistema

En primer lugar, ejecute el siguiente comando en Exchange 2013 para obtener los nombres y las versiones de todas las bases de datos de buzones de correo de la organización.

    Get-MailboxDatabase -IncludePreExchange2013 | FL Name,Server,AdminDisplayVersion

Después de identificar el nombre de las bases de datos de buzones de correo de la organización, ejecute el siguiente comando en Exchange 2013 para mover el buzón del sistema de Microsoft Exchange a una base de datos de buzones de correo ubicada en un servidor Exchange 2013.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | New-MoveRequest -TargetDatabase <name of Exchange 2013 database>

## ¿Cómo puede saber si funcionó?

Para comprobar que movió correctamente el buzón del sistema de Microsoft Exchange a una base de datos de buzones de correo situada en un servidor Exchange 2013, ejecute el siguiente comando en el Shell.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | FL Database,ServerName,AdminDisplayVersion

Si el valor de la propiedad **AdminDisplayVersion** es **Versión 15.x (compilación xxx.x)**, significa que el buzón del sistema reside en una base de datos de buzones de correo situada en un servidor Exchange 2013.

Después de mover el buzón del sistema de Microsoft Exchange a Exchange 2013, también podrá realizar correctamente las siguientes tareas administrativas:

  - Ejecutar el cmdlet **Search-AdminAuditLog**.

  - Exportar el registro de auditoría de administrador en el EAC.

  - Crear e iniciar correctamente búsquedas de exhibición de documentos electrónicos usando el EAC o el Shell en Exchange 2013.

