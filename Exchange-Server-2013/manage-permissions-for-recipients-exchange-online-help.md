---
title: 'Administrar permisos para los destinatarios: Exchange 2013 Help'
TOCTitle: Administrar permisos para los destinatarios
ms:assetid: 749cdfe3-496b-453f-96eb-20a0bf28fd52
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ919240(v=EXCHG.150)
ms:contentKeyID: 51406194
ms.date: 05/06/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar permisos para los destinatarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2018-04-20_

Puede usar el EAC o el Shell para asignar permisos a usuarios o grupos (llamados *delegados*) para que puedan abrir o enviar mensajes desde otros buzones. Los permisos pueden asignarse a buzones de usuarios, buzones vinculados, buzones de recurso y buzones compartidos. También puede asignar permisos a grupos de distribución, grupos de distribución dinámicos y grupos de seguridad habilitados para correo para que los delegados puedan enviar mensajes en nombre de dicho grupo. También puede asignar los siguientes permisos a los delegados para acceder a los buzones de correo o enviar mensajes en nombre de buzones o grupos:

  - **Acceso total**   Este permiso permite que un delegado abra el buzón de un usuario y acceda a su contenido. Sin embargo, asignar permisos de Acceso total no permite que el delegado pueda enviar correo desde el buzón. Debe asignar al delegado el permiso Enviar como o Enviar en nombre de para que pueda enviar correo.
    
    El permiso Acceso total no está disponible al configurar permisos para grupos.

  - **Enviar como**   Este permiso permite que los delegados usen el buzón para enviar mensajes. Después de asignar este permiso a un delegado, los mensajes que el delegado envíe desde el buzón aparecerán como si los hubiera enviado el propietario del buzón. Sin embargo, el delegado no podrá iniciar sesión en el buzón del usuario con este permiso. Sólo permite que los usuarios abran el buzón. Si este permiso se asigna a un grupo, los mensajes enviados por el delegado parecerán que han sido enviados por el grupo.

  - **Enviar en nombre de**   Este permiso también permite que un delegado use el buzón para enviar mensajes. Una vez se ha asignado este permiso a un delegado, la dirección **De** en cualquier mensaje enviado por el delegado indica que el mensaje se envió por el delegado en nombre del propietario del buzón.


> [!NOTE]
> Si asigna el permiso Acceso total, Enviar como o Enviar en nombre de para acceder a un buzón que está oculto en la lista de direcciones, el delegado no podrá abrir el buzón ni enviar mensajes.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  2 minutos.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Asignar permisos a un buzón

Como se indicó anteriormente, los permisos a los delegados pueden asignarse a buzones de usuarios, buzones vinculados, buzones de recurso y buzones compartidos. También puede usar el Shell para asignar permisos a delegados para acceder a un buzón de exhibición.

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Permisos y delegación", en la sección "Permisos de aprovisionamiento de destinatarios", en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

## Use el EAC para asignar permisos

El siguiente procedimiento muestra cómo asignar permisos a un buzón de usuario. Debe seguir un procedimiento similar para asignar permisos a buzones de recursos o compartidos: navegue a la página **Recursos** o **Compartido** en el EAC y seleccione el buzón al que asignar permisos.

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones, haga clic en el buzón al que quiere asignar permisos y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic en **Delegación de buzón de correo**.

4.  Para asignar permisos a los delegados, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") debajo del permiso adecuado para mostrar una página que enumera todos los destinatarios en su organización de Exchange a los que se les pueden asignar los permisos. Seleccione los destinatarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").
    
    Para quitar un permiso de un destinatario, seleccione el destinatario bajo el permiso adecuado y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

5.  Haga clic en **Guardar** para guardar los cambios.

## Usar el EAC para asignar permisos en masa

Use los pasos siguientes para asignar permisos en masa.

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  Seleccione los buzones a los que quiere asignar permisos.

3.  Haga clic o pulse **Más opciones** en el panel derecho y, en **Delegación de buzones**, elija **Agregar**.

4.  En la página **Agregar delegación en masa**, haga clic o pulse en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") en el permiso apropiado para mostrar una página en la que se enumeren todos los destinatarios de la organización de Exchange a los que se les puede asignar el permiso. Seleccione los destinatarios que quiera, agréguelos a la lista y, después, haga clic en **Aceptar**.
    
    Para quitar un permiso a los destinatarios, seleccione los destinatarios bajo el permiso adecuado y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

## Usar el EAC para asignar a un usuario permiso para enviar correo electrónico desde el buzón de otro usuario

El siguiente procedimiento muestra cómo asignar un usuario permiso para enviar correo electrónico desde el buzón de otro usuario.

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En la lista de buzones, haga clic en el buzón al que quiere asignar permisos de enviar como y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del buzón, haga clic en **Delegación de buzón de correo**.

4.  Para asignar permisos a los delegados, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") en **Enviar como** o **Enviar en nombre de** para mostrar una página con todos los destinatarios en la organización de Exchange a los que se pueda asignar el permiso. Seleccione los destinatarios que quiera, agréguelos a la lista y, luego, haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en el cuadro de búsqueda y, luego, haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").
    
    El permiso **Enviar como** permite al delegado enviar correo electrónico desde este buzón.
    
    El permiso **Enviar en nombre de** permite al delegado enviar correo electrónico en nombre de este buzón. La línea **De** de los mensajes enviados por un delegado indica que el mensaje lo envió el delegado en nombre del propietario del buzón.
    

    > [!NOTE]
    > Si el usuario necesita también poder abrir y ver el contenido de ese buzón, debe asignarle a ese usuario, además, el permiso <STRONG>Acceso total</STRONG>.



5.  Haga clic en **Guardar** para guardar los cambios.

## Usar el EAC para asignar a un usuario permiso para enviar correo electrónico desde un grupo

El siguiente procedimiento muestra cómo asignar a un usuario permiso para enviar correo electrónico desde un grupo.

1.  En el EAC, vaya a **Destinatarios** \> **Grupos**.

2.  En la lista de grupos, haga clic en el grupo para el que quiere asignar el permiso de enviar como y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del grupo, haga clic en **Delegación de grupo**.

4.  Para asignar permisos a los delegados, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") en **Enviar como** o **Enviar en nombre de** para mostrar una página con todos los destinatarios en la organización de Exchange a los que se pueda asignar el permiso. Seleccione los destinatarios que quiera, agréguelos a la lista y, luego, haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en el cuadro de búsqueda y, luego, haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").
    
    El permiso **Enviar como** permite al delegado enviar correo electrónico desde este grupo.
    
    El permiso **Enviar en nombre de** permite al delegado enviar correo electrónico en nombre de este grupo. La línea **De** de los mensajes enviados por un delegado indica que el mensaje lo envió el delegado en nombre del grupo.

5.  Haga clic en **Guardar** para guardar los cambios.

## Usar el EAC para asignar permisos de acceso total

El siguiente procedimiento muestra cómo asignar permisos de acceso total a un buzón de usuario.

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En la lista de buzones, haga clic en el buzón para el que quiere asignar permisos de acceso total y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del buzón, haga clic en **Delegación de buzón de correo**.

4.  Para asignar permisos a los delegados, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") en **Acceso total** para mostrar una página con una lista de todos los destinatarios de la organización de Exchange a los que se les puede asignar el permiso. Seleccione los destinatarios que quiera, agréguelos a la lista y, luego, haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en el cuadro de búsqueda y, luego, haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").
    
    El permiso **Acceso total** permite a un delegado abrir el buzón de un usuario y acceder al contenido del buzón.
    

    > [!NOTE]
    > Asignar el permiso <STRONG>Acceso total</STRONG> no permite al delegado enviar correo desde el buzón. Para que pueda enviar correo, debe asignar al delegado el permiso <STRONG>Enviar como</STRONG> o <STRONG>Enviar en nombre de</STRONG>.



5.  Haga clic en **Guardar** para guardar los cambios.

## Usar el Shell para asignar permisos

Las secciones siguientes muestran cómo usar el Shell para administrar los permisos Acceso total, Enviar como y Enviar en nombre de para los buzones.

## Administrar el permiso Acceso total

Los siguientes ejemplos muestran cómo usar los cmdlets **Add-MailboxPermission** y **Remove-MailboxPermission** para administrar los permisos de Acceso total.

En este ejemplo se asigna al delegado Raymond Sam permisos de Acceso total al buzón de correo de Terry Adams.

    Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType all

En este ejemplo, se asigna a Esther Valle permisos de Acceso total al buzón de búsqueda de exhibición predeterminado de la organización.

    Add-MailboxPermission -Identity "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User estherv -AccessRights FullAccess -InheritanceType all

En este ejemplo se asigna a los miembros del grupo de distribución del departamento de soporte técnico permiso de Acceso total al buzón compartido Helpdesk Tickets.

    Add-MailboxPermission "HelpdeskTickets" -User helpdesk -AccessRights FullAccess -InheritanceType all

En este ejemplo se quitan a Jim Hance los permisos de Acceso total al buzón de Ayla Kol.

    Remove-MailboxPermission -Identity ayla -User "Jim Hance" -AccessRights FullAccess -Inheritance

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [Add-MailboxPermission](https://technet.microsoft.com/es-es/library/bb124097\(v=exchg.150\))

  - [Remove-MailboxPermission](https://technet.microsoft.com/es-es/library/bb125153\(v=exchg.150\))

## Administrar el permiso Enviar como

Los siguientes ejemplos muestran cómo administrar los permisos de Enviar como en Exchange Server 2013 y en Exchange Online. En Exchange 2013, debe usar los cmdlets **Add-ADPermission** y **Remove-ADPermission**; en Exchange Online, debe usar los cmdlets **Add-RecipientPermission** y **Remove-RecipientPermission**. En ambos casos, debe usar el parámetro *Identity* para especificar el nombre del buzón al que debe añadirse o desde el cual debe quitarse el permiso Enviar como, y el parámetro *User* o *Trustee* para especificar el delegado (por ejemplo, un usuario o grupo) al que se le asignará o quitará el permiso Enviar como.


> [!TIP]
> Use el cmdlet <STRONG>Get-Recipient</STRONG> para recuperar la propiedad <EM>Name</EM> para el buzón y el delegado. Use estos valores para asignar el permiso Enviar como.



## Exchange Server 2013

En este ejemplo, se asigna el permiso Enviar como al grupo Helpdesk en el buzón compartido Helpdesk Support Team.

    Add-ADPermission -Identity helpdesksupport -User helpdeskgroup -ExtendedRights "Send As"

En este ejemplo se quita el permiso Enviar como al usuario Pilar Pinilla en el buzón de James Alvord.

    Remove-ADPermission -Identity "James Alvord" -User pilarp -ExtendedRights "Send As"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte:

  - [Add-ADPermission](https://technet.microsoft.com/es-es/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/es-es/library/aa996048\(v=exchg.150\))

## Exchange Online

En este ejemplo, se asigna el permiso Enviar como al grupo Printer Support en el buzón compartido Contoso Printer Support.

    Add-RecipientPermission -Identity "Contoso Printer Support" -Trustee "Printer Support" -AccessRights SendAs

En este ejemplo se quita el permiso Enviar como al usuario Karen Toh en el buzón de Yan Li.

    Remove-RecipientPermission -Identity "Yan Li" -Trustee "Karen Toh" -ExtendedRights SendAs

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte:

  - [Add-RecipientPermission](https://technet.microsoft.com/es-es/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/es-es/library/ff945794\(v=exchg.150\))

## Administrar el permiso Enviar en nombre de

Los siguientes ejemplos muestran cómo usar el cmdlet **Set-Mailbox** para administrar los permisos Enviar en nombre de.

En este ejemplo se asigna al delegado Holly Holt el permiso de Enviar en nombre de al buzón de Sean Chai.

    Set-Mailbox -Identity seanc@contoso.com -GrantSendOnBehalfTo hollyh

En este ejemplo se quita el permiso Enviar en nombre de en el buzón compartido Contoso Executives que se asignó al grupo Temporary Executive Assistants.

    Set-Mailbox "Contoso Executives" -GrantSendOnBehalfTo @{remove="tempassistants@contoso.com"}

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha asignado correctamente permisos a un buzón o a un buzón compartido, puede usar cualquiera de los métodos siguientes:

  - En el EAC:
    
    1.  Vaya a **Destinatarios** \> **Buzón de correo** o **Compartido**, haga clic en el buzón y, a continuación, en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    2.  En la página de propiedades de buzones, haga clic en **Delegación de buzón de correo**.
    
    3.  Si asignó permisos a los destinatarios, verifique que el usuario o grupo esté enumerado en el permiso apropiado. Si quitó permisos, verifique que el destinatario no está enumerado en el permiso adecuado.

O bien

  - En el Shell, ejecute uno de los siguientes comandos, en función del permiso que administró.
    
      - **Acceso completo**
        
            Get-MailboxPermission -Identity <mailbox>
        
        Para verificar si un delegado específico tiene asignado el permiso Acceso total a un buzón, ejecute el comando siguiente.
        
            Get-MailboxPermission -Identity <mailbox> -User <delegate>
    
      - **Enviar como**
        
        En Exchange Server 2013, ejecute el siguiente comando.
        
            Get-ADPermission -Identity <name of mailbox> -User <delegate>
        
        En Exchange Online, ejecute el siguiente comando.
        
            Get-RecipientPermission -Identity <mailbox> -Trustee <delegate>
    
      - **Enviar en nombre de**
        
            Get-Mailbox -Identity <mailbox> | FL GrantSendOnBehalfTo

## Asignar permisos a un grupo

Como se indicó anteriormente, puede asignar los permisos Enviar como y Enviar en nombre de a grupos de distribución, grupos de distribución dinámicos y grupos de seguridad habilitados para correo para permitir que los delegados envíen mensajes como el grupo o en nombre del grupo.

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas "Grupos de distribución" y "Grupos de distribución dinámicos" en la sección "Permisos de aprovisionamiento de destinatarios", en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

## Usar el EAC para asignar permisos

1.  En el Centro de Administración de Exchange, vaya a **Destinatarios**  \> **Grupos**.

2.  En la lista de grupos, haga clic en el grupo al que quiere asignar permisos y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de grupos, haga clic en **Delegación de grupo**.

4.  Para asignar permisos a los delegados, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") debajo del permiso adecuado para mostrar una página que muestra una lista de todos los destinatarios en su organización de Exchange a los que se les puede asignar los permisos. Seleccione los destinatarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").
    
    Para quitar permisos de un destinatario, seleccione el destinatario bajo el permiso adecuado y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

5.  Haga clic en **Guardar** para guardar los cambios.

## Usar el Shell para asignar permisos

Las secciones siguientes muestran cómo usar el Shell para administrar los permisos Enviar como y Enviar en nombre de para los grupos.

## Administrar el permiso Enviar como

Los siguientes ejemplos muestran cómo administrar permisos Enviar como para grupos en Exchange Server 2013 y en Exchange Online. En Exchange 2013, debe usar los cmdlets **Add-ADPermission** y **Remove-ADPermission**. En Exchange Online, debe usar los cmdlets **Add-RecipientPermission** y **Remove-RecipientPermission**. En ambos casos, debe usar el parámetro *Identity* para especificar el nombre del grupo al que debe añadirse o desde el que debe quitarse el permiso Enviar como, y el parámetro *User* o *Trustee* para especificar el delegado (por ejemplo, un usuario o grupo) al que se le asignará o quitará el permiso Enviar como.


> [!TIP]
> Use el cmdlet <STRONG>Get-Recipient</STRONG> para recuperar la propiedad <EM>Name</EM> para el grupo y el delegado. Use estos valores para asignar el permiso Enviar como.



## Exchange Server 2013

Este ejemplo asigna el permiso Enviar como al grupo Sales Admins para el grupo Contoso Sales Info. Así, los miembros del grupo de administración de ventas podrá enviar mensajes como el grupo Contoso Sales Information.

    Add-ADPermission -Identity "Contoso Sales Info" -User "Sales Admins" -ExtendedRights "Send As"

En este ejemplo se quita el permiso Enviar como al usuario Alan Shen en el grupo Corporate IT Admins.

    Remove-ADPermission -Identity "Corporate IT Admins" -User contoso\alans -ExtendedRights "Send As"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte:

  - [Add-ADPermission](https://technet.microsoft.com/es-es/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/es-es/library/aa996048\(v=exchg.150\))

## Exchange Online

En este ejemplo se asigna el permiso Enviar como al grupo Contoso Admins en el grupo de distribución dinámico Emergency Broadcast Messages.

    Add-RecipientPermission -Identity emergencybroadcast@contoso.com -Trustee "Contoso Admins" -AccessRights SendAs

En este ejemplo se quita el permiso Enviar como al usuario Walter Harp en el grupo de seguridad Printer Resources.

    Remove-RecipientPermission -Identity "Printer Resources" -Trustee walterh@contoso.com ExtendedRights SendAs

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte:

  - [Add-RecipientPermission](https://technet.microsoft.com/es-es/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/es-es/library/ff945794\(v=exchg.150\))

## Administrar el permiso Enviar en nombre de

Los siguientes ejemplos muestran cómo usar los cmdlets **Set-DistributionGroup** y **Set-DynamicDistributionGroup** para administrar permisos Enviar en nombre de para grupos.

En este ejemplo se asigna el permiso Enviar en nombre de a la delegada Sara Davis en el grupo de distribución Printer Support.

    Set-DistributionGroup -Identity printersupport@contoso.com -GrantSendOnBehalfTo sarad

En este ejemplo se asigna el permiso Enviar en nombre de al delegado Administrator en el grupo de distribución dinámico All Employees.

    Set-DynamicDistributionGroup -Identity "All Employees" -GrantSendOnBehalfTo administrator

En este ejemplo se quita el permiso Enviar en nombre de en el grupo de distribución dinámico All Employees que se asignó al administrador.

    Set-DynamicDistributionGroup "All Employees" -GrantSendOnBehalfTo @{remove="administrator"}

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte:

  - [Set-DistributionGroup](https://technet.microsoft.com/es-es/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/es-es/library/bb123796\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que asignó permisos correctamente al grupo, siga uno de estos procedimientos:

  - En el EAC:
    
    1.  vaya a **Destinatarios**  \> **Grupos**, haga clic en el grupo y, después, en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    2.  En la página de propiedades de grupos, haga clic en **Delegación de grupo**.
    
    3.  Si asignó permisos a los destinatarios, verifique que el usuario o el grupo esté enumerado en el permiso apropiado. Si quitó permisos, verifique que el destinatario no está enumerado en el permiso adecuado.

O bien

  - En el Shell, ejecute uno de los siguientes comandos en función del permiso que administró.
    
      - **Enviar como**
        
        En Exchange Server 2013, ejecute el siguiente comando.
        
            Get-ADPermission -Identity <name of group> -User <delegate>
        
        En Exchange Online, ejecute el siguiente comando.
        
            Get-RecipientPermission -Identity <group> -Trustee <delegate>
    
      - **Enviar en nombre de**
        
            Get-DistributionGroup -Identity <group> | FL GrantSendOnBehalfTo
        
        O bien
        
            Get-DynamicDistributionGroup -Identity <group> | FL GrantSendOnBehalfTo

