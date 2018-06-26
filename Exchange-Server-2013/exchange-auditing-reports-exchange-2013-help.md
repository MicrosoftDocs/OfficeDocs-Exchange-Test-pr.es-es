---
title: 'Informes de auditoría de Exchange: Exchange 2013 Help'
TOCTitle: Informes de auditoría de Exchange
ms:assetid: 2b3e1529-1677-4564-be0b-ce22757ddc0d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150497(v=EXCHG.150)
ms:contentKeyID: 48267926
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Informes de auditoría de Exchange

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Use el registro de auditoría para solucionar los problemas de configuración mediante el seguimiento de cambios específicos efectuados por los administradores y como ayuda para cumplir los requisitos normativos, de cumplimiento normativo y de litigio. Microsoft Exchange proporciona dos tipos de registro de auditoría:

  - El *registro de auditoría de administrador* guarda cualquier acción, basada en el cmdlet del Shell de administración de Exchange, que ha realizado un administrador. Esto puede ayudar a solucionar problemas de configuración o a identificar la causa de problemas relacionados con la seguridad o el cumplimiento normativo. En Exchange Online, también se registran las acciones que realizan los administradores de Microsoft y los administradores delegados.

  - El *registro de auditoría de buzones* registra cuando un administrador, un usuario delegado o la persona propietaria del buzón accede a este. Esto puede ayudarle a determinar quién ha accedido a un buzón y qué ha hecho.

En este tema se explica lo siguiente:

  - Exportación de registros de auditoría

  - Ejecución de informes de auditoría

  - Configuración del registro de auditoría
    
      - Habilitación del registro de auditoría de buzones de correo
    
      - Concesión de acceso a los usuarios a los informes de auditoría
    
      - Configuración de Outlook Web App para permitir datos adjuntos de XML

## Exportación de registros de auditoría

En la página **Administración del cumplimiento** \> **Auditoría** del centro de administración de Exchange (EAC), puede buscar y exportar entradas del registro de auditoría de administrador y del registro de auditoría de buzón.

  - **Exportación del registro de auditoría de administrador**   Cualquier acción que realiza un administrador y se basa en un cmdlet de Shell y que no comienza con los verbos **Get**, **Search** o **Test** se registra en el registro de auditoría del administrador. Las entradas del registro de auditoría incluyen el cmdlet que se ejecutó, el parámetro y los valores utilizados con el cmdlet, así como el momento en el que la operación se realizó correctamente. Puede buscar y exportar las entradas del informe de auditoría de administrador. Al exportar los resultados de la búsqueda, Microsoft Exchange los guarda en un archivo XML y lo adjunta a un mensaje de correo electrónico. Para obtener más información, consulte:
    
      - [Buscar los informes de cambios del grupo de roles o auditorías de administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)
    
      - [Ver y exportar el registro de auditoría del administrador externo](https://technet.microsoft.com/es-es/library/dn505728\(v=exchg.150\))
    

    > [!NOTE]
    > De manera predeterminada, las entradas del registro de auditoría del administrador se mantienen durante 90 días. Cuando una entrada tiene una antigüedad mayor que 90 días, se elimina. No se puede cambiar esta configuración en una organización basada en la nube. En cambio, es posible cambiarla en una organización de Exchange local mediante el cmdlet <STRONG>Set-AdminAuditLog</STRONG>.



  - **Exportación de los registros de auditoría de buzones** Cuando el registro de auditoría de buzones está habilitado para un buzón, Microsoft Exchange guarda un registro de las acciones que se realizan en los datos del buzón por parte de los usuarios que no son propietarios, el cual se almacena en una carpeta oculta del buzón de correo que se está auditando. El registro de auditoría de buzones también puede configurar las acciones del propietario del registro. Las entradas de este registro indican quién ha accedido al buzón y cuándo lo ha hecho, las acciones que ha realizado y si la acción se ha realizado correctamente. Al buscar entradas en el registro de auditoría de buzones y exportarlas, Microsoft Exchange guarda los resultados de la búsqueda en un archivo XML y lo adjunta a un mensaje de correo electrónico. Para obtener más información, vea [Exportar registros de auditoría de buzones](export-mailbox-audit-logs-exchange-2013-help.md).

## Ejecución de informes de auditoría

Cuando se ejecutan algunos de los siguientes informes en la página **Auditoría** del EAC, los resultados se muestran en el panel de detalles del informe.

  - **Realización de un informe de acceso al buzón de correo del que no se es propietario** Use este informe para buscar los buzones de correo a los que ha tenido acceso otra persona que no sea su propietario. Para obtener más información, consulte [Ejecución de un informe de acceso al buzón de correo del que no se es propietario](run-a-non-owner-mailbox-access-report-exchange-online-help.md).

  - **Realización de un informe de grupo de roles de administrador** Use este informe para buscar los cambios realizados en los grupos de roles de administrador. Para obtener más información, consulte [Buscar los informes de cambios del grupo de roles o auditorías de administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

  - **Realización de un informe de exhibición de documentos y conservación locales** Use este informe para encontrar buzones de correo que se han colocado o eliminado de la conservación local. Para obtener más información, vea:
    
      - [Conservación local y retención por juicio](in-place-hold-and-litigation-hold-exchange-2013-help.md)
    
      - [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md)

  - **Realización de un informe de retención por juicio por buzón** Use este informe para encontrar buzones de correo colocados o eliminados de la retención por juicio. Para obtener más información, consulte.
    
      - [Ejecutar un informe de retención por litigio por buzón](run-a-per-mailbox-litigation-hold-report-exchange-2013-help.md)
    
      - [Poner un buzón en retención por juicio](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - **Ejecutar el registro de auditoría del administrador**   Use este informe para ver entradas del registro de auditoría del administrador. En lugar de exportar el registro de auditoría del administrador, que puede tardar hasta 24 horas para recibir en un mensaje de correo electrónico, puede ejecutar este informe en el EAC. Este informe registra los cambios de configuración que realizan los administradores en la organización. Se mostrarán hasta 5000 entradas en varias páginas. Para restringir la búsqueda, puede especificar un intervalo de fechas. Para obtener más información, consulte:
    
      - [Ver el registro de auditoría del administrador](view-the-administrator-audit-log-exchange-2013-help.md)
    
      - [Registro de auditoría de administrador](administrator-audit-logging-exchange-2013-help.md)

  - **Ejecutar el registro de auditoría del administrador externo**   Este informe solo está disponible Exchange Online y Exchange Online Protection. Las acciones realizadas por los administradores de Microsoft o los administradores delegados se registran en el registro de auditoría del administrador. Use el informe de registro de auditoría del administrador externo para buscar y ver las acciones que realizaron los administradores ajenos a la organización en la configuración de su organización de Exchange Online. Para obtener más información, consulte [Ver y exportar el registro de auditoría del administrador externo](https://technet.microsoft.com/es-es/library/dn505728\(v=exchg.150\)).

## Configuración del registro de auditoría

Para poder ejecutar los informes de auditoría y exportarlos, tiene que configurar el registro de auditoría para su organización.

## Habilitación del registro de auditoría de buzones de correo

Tiene que habilitar el registro de auditoría de buzones de correo para el que desee ejecutar un informe de acceso al buzón de correo del que no se es propietario. Si el registro de la auditoría de buzones de correo no está habilitado para un buzón, no obtendrá ningún resultado para cuando ejecute un informe o exporte dicho registro.

Para habilitar el registro de auditoría de buzones de correo para un solo buzón, ejecute el siguiente comando en el Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Para habilitar la auditoría de buzones de correo para todos los buzones de la organización, ejecute los siguientes comandos.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

Para obtener más información sobre la configuración de las acciones que se registran, vea:

  - **Exchange 2013**   [Habilitar o deshabilitar el registro de auditoría de buzones para un buzón](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)

  - **Exchange Online**   [Habilitar la auditoría de buzones de correo en Office 365](https://go.microsoft.com/fwlink/p/?linkid=626109)

## Concesión de acceso a los usuarios a los informes de auditoría

De forma predeterminada, los administradores pueden obtener acceso y ejecutar cualquiera de los informes de la página Auditoría del EAC. Sin embargo, otros usuarios, como el administrador de registros o el personal jurídico, deben tener asignados los permisos necesarios.

La manera más fácil de conceder acceso de los usuarios consiste en agregarlos al grupo de funciones de administración de registros. También puede usar el Shell para conceder acceso a un usuario a la página **Auditoría** en el EAC mediante la asignación del rol Registros de auditoría al usuario.

## Adición de un usuario al grupo de funciones de administración de registros

1.  Vaya a **Permisos** \> **Roles de administrador**.

2.  En la lista de grupos de roles, haga clic en **Administración de registros** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **Miembros**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En el cuadro de diálogo **Seleccionar miembros**, seleccione el usuario. Puede buscar un usuario escribiendo el nombre para mostrar completo o parte de éste y haciendo clic en **Búsqueda**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar"). También puede hacer clic en los encabezados de columna **Nombre** o **Nombre para mostrar** para ordenar la lista.

5.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, a continuación, en **Aceptar** para volver a la página de grupo de roles.

6.  Haga clic en **Guardar** para guardar los cambios realizados en el grupo de roles.

En el panel "Detalles", el usuario aparece en **Miembros** y puede acceder a la página "Auditoría" en el EAC, ejecutar informes de auditoría y exportar registros de auditoría.

## Asignar el rol Registros de auditoría a un usuario

Ejecute el siguiente comando para asignar el rol Registros de auditoría a un usuario.

    New-ManagementRoleAssignment -Role "Audit Logs" -User <Identity>

Esto permite que el usuario seleccione **Administración del cumplimiento** \> **Auditoría** en el EAC y ejecute cualquier informe. El usuario también puede exportar el registro de auditoría de buzón, así como exportar y ver el registro de auditoría del administrador.


> [!NOTE]
> Para permitir que un usuario ejecute informes de auditoría pero no exporte los registros de auditoría, use el comando anterior para asignar el rol Registros de auditoría con permiso de vista.



## Configuración de Outlook Web App para permitir datos adjuntos de XML

Al exportar el registro de auditoría de buzones de correo o el registro de auditoría de administrador, Microsoft Exchange adjunta el registro de auditoría, que es un archivo XML, a un mensaje de correo electrónico. Sin embargo, Outlook Web App bloquea los datos adjuntos de XML de forma predeterminada. Si desea usar Outlook Web App para acceder a estos registros de auditoría, debe configurar Outlook Web App para permitir archivos adjuntos de XML.

Ejecute el siguiente comando para permitir datos adjuntos de XML en Outlook Web App.

    Set-OwaMailboxPolicy -Identity Default -AllowedFileTypes '.rpmsg','.xlsx','.xlsm','.xlsb','.tiff','.pptx','.pptm','.ppsx','.ppsm','.docx','.docm','.zip','.xls','.wmv','.wma','.wav','.vsd','.txt','.tif','.rtf','.pub','.ppt','.png','.pdf','.one','.mp3','.jpg','.gif','.doc','.bmp','.avi','.xml'

