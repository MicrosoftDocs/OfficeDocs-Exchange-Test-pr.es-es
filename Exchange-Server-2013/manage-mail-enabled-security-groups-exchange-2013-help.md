---
title: 'Administrar grupos de seguridad habilitados para correo: Exchange 2013 Help'
TOCTitle: Administrar grupos de seguridad habilitados para correo
ms:assetid: 80b3b537-4786-4d02-9202-44e373811a25
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123521(v=EXCHG.150)
ms:contentKeyID: 48268347
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar grupos de seguridad habilitados para correo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2017-10-04_

Un grupo de seguridad habilitado para correo puede usarse para distribuir mensajes y conceder permisos de acceso a los recursos en Active Directory. Para obtener más información, consulte [Destinatarios](recipients-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 a 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de distribución" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Crear un grupo de seguridad con correo habilitado

## Uso del EAP para crear un grupo de seguridad

1.  En el EAC, vaya a **Destinatarios** \> **Grupos**.

2.  Haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") \> **grupo de seguridad**.

3.  En la página **Nuevo grupo de seguridad**, complete los campos siguientes:
    
      - **\* Nombre para mostrar** Utilice este cuadro para introducir el nombre para mostrar. Este nombre aparece en la libreta de direcciones compartida, en las líneas Para: cuando se envía un correo electrónico a este grupo, y en la lista Grupos en el EAC. El nombre para mostrar es obligatorio y debe ser sencillo para que los usuarios puedan identificarlo. También deben ser únicos en el bosque.
        

        > [!NOTE]
        > Si se aplica una directiva de nomenclatura de grupo, debe seguir las restricciones impuestas en su organización. Para obtener más información, consulte <A href="create-a-distribution-group-naming-policy-exchange-2013-help.md">Crear una directiva de nomenclatura de grupos de distribución</A>. Si desea reemplazar la directiva de nomenclatura de grupos de la organización, consulte <A href="override-the-distribution-group-naming-policy-exchange-2013-help.md">Invalidar la directiva de nomenclatura de grupos de distribución</A>.

    
      - **\* Alias**   Utilice este cuadro para escribir el alias del grupo de seguridad. El alias no puede superar los 64 caracteres y debe ser único en el bosque. Cuando un usuario escribe el alias en la línea Para: de un mensaje de correo electrónico, se resuelve en el nombre para mostrar del grupo.
    
      - **Descripción**   Utilice este cuadro para describir el grupo de seguridad, de forma que los usuarios sepan cuál es el propósito del grupo.
    
      - **Unidad organizativa**   Puede seleccionar una unidad organizativa (OU) diferente a la que aparece de forma predeterminada (en el ámbito de destinatarios). Si el ámbito de destinatario definido corresponde al bosque, el valor predeterminado será el contenedor Usuarios del dominio de Active Directory que contiene el equipo en el que se ejecuta EAC. Si el ámbito del destinatario está establecido en un dominio específico, el contenedor de usuarios se selecciona de modo predeterminado. Si el ámbito del destinatario está establecido en una unidad organizativa específica (OU), esa OU se selecciona de modo predeterminado.
        
        Para seleccionar otra OU, haga clic en **Examinar**. En el cuadro de diálogo se muestran todas las OU del bosque dentro del ámbito especificado. Seleccione la unidad organizativa y haga clic en **Aceptar**.
    
      - **\* Propietarios**   De forma predeterminada, la persona que crea un grupo pasa a ser el propietario. Todos los grupos deben tener al menos un propietario. Puede agregar propietarios si hace clic en **Agregar**.
    
      - **Miembros**   Esta sección sirve para agregar miembros e indicar si se necesita aprobación para los usuarios que se unan al grupo o lo dejen.
        
        Los propietarios de un grupo no tienen que ser miembros de éste. Use la casilla **Agregar propietarios de grupo como miembros** para agregar o quitar propietarios como miembros.
        
        Para agregar miembros al grupo, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Cuando haya terminado de agregar los miembros, haga clic en **Aceptar** para volver a la página **Nuevo grupo de seguridad**.
        
        Seleccione la casilla **Se necesita la aprobación del propietario** si desea que los propietarios del grupo reciban solicitudes de usuario para unirse al grupo. Si selecciona esta opción, serán los propietarios del grupo los únicos que podrán eliminar a los miembros.

4.  Cuando haya terminado, haga clic en **Guardar** para crear el grupo de seguridad.


> [!NOTE]
> De forma predeterminada, en todos los grupos de seguridad con correo habilitado es necesario que todos los remitentes estén autenticados. De este modo se evita que remitentes externos envíen mensajes a grupos de seguridad con correo habilitado. Para configurar un&nbsp;grupo de seguridad con correo habilitado para que acepte mensajes de todos los remitentes, debe modificar las configuraciones de entrega de mensajes de dicho grupo.



## Usar el Shell para crear un grupo de seguridad

En este ejemplo se crea un grupo de seguridad con el alias fsadmin y el nombre File Server Managers. El grupo de seguridad se ha creado en la OU predeterminada y cualquier se puede unir con la aprobación de los propietarios del grupo.

    New-DistributionGroup -Name "File Server Managers" -Alias fsadmin -Type security

Para obtener más información sobre cómo usar el Shell para crear grupos de seguridad con correo habilitado, consulte [New-DistributionGroup](https://technet.microsoft.com/es-es/library/aa998856\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó grupo de seguridad con correo habilitado, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Grupos**. El nuevo grupo de seguridad con correo habilitado se muestra en la lista de grupos. Bajo **Tipo de grupo**, el tipo es **Grupo de seguridad**.

  - En el Shell, ejecute el comando siguiente para mostrar información sobre el nuevo grupo de seguridad con correo habilitado.
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Cambiar las propiedades del grupo de seguridad con correo habilitado

## Utilice el EAC para cambiar las propiedades de grupo de seguridad con correo habilitado

1.  En el EAC, vaya a **Destinatarios** \> **Grupos**.

2.  En la lista de grupos, haga clic en el grupo de seguridad que desea ver o modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del grupo, haga clic en una de las siguientes secciones para ver o cambiar las propiedades.
    
      - General
    
      - Ownership
    
      - Membership
    
      - Membership approval
    
      - Delivery management
    
      - Message approval
    
      - Email options
    
      - MailTip
    
      - Group delegation

## General

Utilice esta sección para ver o cambiar la información básica sobre el grupo.

  - **\* Nombre para mostrar**   Este nombre aparece en la libreta de direcciones, en las líneas Para: cuando se envía un correo electrónico a este grupo, y en la lista Grupos. El nombre para mostrar es obligatorio y debe ser sencillo para que los usuarios puedan identificarlo. También tiene que ser único en su dominio.

  - **\* Alias**   Esta es la parte de la dirección de correo electrónico que aparece a la izquierda del símbolo (@). Si cambia el alias, la dirección SMTP primaria para el grupo también cambiará y contendrá el nuevo alias. Además, la dirección de correo electrónico con el alias anterior se mantendrá como dirección proxy para el grupo.

  - **Descripción**   Utilice este cuadro para describir el grupo, de forma que los usuarios sepan cuál es el propósito del grupo. Esta descripción aparece en la libreta de direcciones en el panel de detalles en el EAC.

  - **Ocultar este grupo de la libreta de direcciones compartida**   Seleccione esta casilla si no desea que los usuarios vean este grupo en la libreta de direcciones. Si esta casilla está seleccionada, un remitente tiene que escribir la dirección de correo electrónico o alias del grupo en la línea Para: o en el campo Cc: para enviar correo al grupo.
    

    > [!TIP]
    > Considere la posibilidad de ocultar los grupos de seguridad porque normalmente se usan para asignar permisos a los miembros del grupo y no para enviar correo electrónico.



  - **Unidad organizativa**   Este cuadro de solo lectura muestra la unidad organizativa (OU) que contiene el grupo. Debe usar los usuarios y los equipos de Active Directory para mover el grupo a una OU distinta.

## Propiedad

Utilice esta sección para asignar los propietarios de grupo. El propietario del grupo puede agregar miembros al grupo, y aprobar o rechazar solicitudes para unirse al grupo. De forma predeterminada, la persona que crea un grupo pasa a ser el propietario. Todos los grupos deben tener al menos un propietario.

Puede agregar propietarios si hace clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Asimismo, puede quitar a un propietario si lo selecciona y hace clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

## Pertenencia

Utilice esta sección para agregar o quitar miembros. Los propietarios de un grupo no tienen que ser miembros de éste. Bajo **Miembros**, puede agregar miembros haciendo clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Puede quitar a un miembro seleccionando un usuario de la lista de miembros y haciendo clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

## Aprobación de la pertenencia

Use esta sección para especificar si se necesita aprobación del propietario para que los usuarios se unan al grupo. Si selecciona la casilla **Se necesita la aprobación del propietario**, el propietario o propietarios del grupo recibirán un correo electrónico en el que solicitarán la aprobación para unirse al grupo. Como se mencionó anteriormente, únicamente los propietarios pueden quitar a miembros del grupo.


> [!NOTE]
> Esta opción no funciona con los grupos de seguridad habilitados para correo debido a las limitaciones relacionadas con la seguridad.



## Administración de entregas

Use esta sección para administrar quién envía correos electrónicos a este grupo.

  - **Solo los remitentes de mi organización**   Seleccione esta opción para permitir que únicamente los remitentes de la organización envíen mensajes al grupo. Esto significa que si alguien de fuera de la organización envía un correo electrónico a este grupo, se rechazará. Esta es la configuración predeterminada.

  - **Remitentes dentro y fuera de mi organización**   Seleccione esta opción para permitir a cualquiera enviar mensajes al grupo.
    
    Puede limitar todavía más quién puede enviar mensajes al grupo, permitiendo solo a remitentes concretos enviar mensajes a este grupo. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, a continuación, seleccione uno o más destinatarios. Si agrega remitentes a esta lista, son los únicos que pueden enviar correo al grupo. Se rechazará el correo enviado por cualquier remitente que no esté en la lista.
    
    Para quitar a un usuario o grupo de la lista, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").
    

    > [!IMPORTANT]
    > Si ha configurado el grupo para permitir que solo los remitentes internos a la organización envíen mensajes al grupo, se rechazará el correo electrónico enviado por un contacto de correo, aunque se haya agregado a la lista.



## Aprobación de mensajes

Use esta sección para establecer las opciones para moderar el grupo. Los moderadores admiten o rechazan los mensajes enviados al grupo antes de que lleguen a los miembros del grupo.

  - **Los mensajes enviados a este grupo tienen que ser aprobados por un moderador** Esta casilla no está seleccionada de forma predeterminada. Si activa esta casilla, los moderadores del grupo revisarán los mensajes entrantes antes de llegar a su destino. Los moderadores de grupo pueden admitir o rechazar mensajes entrantes.

  - **Moderadores de grupo**   Para agregar moderadores de grupo, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para quitar a un moderador, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar"). Si ha activado la casilla "Los mensajes enviados a este grupo tienen que ser aprobados por un moderador" y no elige un moderador, los mensajes enviados al grupo se remitirán al propietario de dicho grupo para su aprobación.

  - **Remitentes que no requieran la aprobación de mensajes** Para agregar usuarios o grupos que no se vean afectados por la moderación de este grupo, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para quitar a un usuario o un grupo, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

  - **Seleccionar notificaciones de moderación   **Use esta sección para establecer la forma en que se notifica a los usuarios con respecto a la aprobación de mensajes.
    
      - **Envíe una notificación a todos los remitentes si sus mensajes no se aprueban**   Es la configuración predeterminada. Los remitentes internos y externos de la organización recibirán una notificación cuando sus mensajes no se hayan aprobado.
    
      - **Envíe una notificación a los remitentes de su organización cuando sus mensajes no se aprueben**Si selecciona esta opción, únicamente los usuarios y grupos en la organización recibirán una notificación cuando el moderador no apruebe un mensaje que hayan enviado al grupo.
    
      - **No notificar a nadie cuando no se apruebe un mensaje**   Si selecciona esta opción, no se enviarán notificaciones a los remitentes cuyos mensajes no hayan aprobado los moderadores de grupo.

## Opciones de correo electrónico

Use esta sección para ver o cambiar las direcciones de correo electrónico asociadas con el grupo. Esto incluye las direcciones de SMTP primarias del grupo y cualquier proxy asociado. La dirección SMTP principal (también denominada *dirección de respuesta* ) se muestra en negrita en la lista de direcciones, con el valor **SMTP** en mayúsculas en la columna **Tipo**.

  - **Agregar **  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una dirección de correo electrónico nueva para este buzón. Seleccione uno de los siguientes tipos de dirección:
    
      - **Dirección SMTP**   Este es el tipo de dirección predeterminado. Haga clic en este botón y luego escriba la nueva dirección SMTP en la casilla **\* Dirección de correo electrónico**.
        

        > [!NOTE]
        > Para que la nueva dirección se convierta en la dirección SMTP principal del grupo, seleccione la casilla <STRONG>Convertir en dirección de respuesta</STRONG>. Esta casilla aparece únicamente cuando la casilla <STRONG>Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada al destinatario</STRONG> no está seleccionada.

    
      - **Tipo de dirección personalizada**   Haga clic en este botón y escriba uno de los tipos de dirección de correo electrónico que no sean SMTP admitidos en la casilla **\* Dirección de correo electrónico**.
        

        > [!NOTE]
        > Con excepción de las direcciones X.400, Exchange no valida las direcciones personalizadas para comprobar el formato correcto. Debe asegurarse de que la dirección personalizada que especifica cumpla los requisitos de formato para el tipo de dirección.



  - **Editar**   Para cambiar una dirección de correo electrónico asociada al grupo, selecciónela en la lista y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    

    > [!NOTE]
    > Para que una dirección existente se convierta en la dirección SMTP principal del grupo, seleccione la casilla <STRONG>Convertir en dirección de respuesta</STRONG>. Tal como se ha mencionado anteriormente, esta casilla aparece únicamente cuando la casilla <STRONG>Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada a este destinatario</STRONG> no está seleccionada.



  - **Quitar**   Para quitar una dirección de correo electrónico asociada al grupo, selecciónela en la lista y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

  - **Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada a este destinatario   **Seleccione esta casilla para que las direcciones de correo electrónico del destinatario se actualicen automáticamente según los cambios realizados en las directivas de direcciones de correo electrónico de su organización. De forma predeterminada, esta casilla está activada.

## Información sobre correo

Use esta sección para agregar una información sobre correo para avisar a los usuarios de problemas potenciales antes de enviar un mensaje a este grupo. Una información sobre correo es texto que se muestra en la barra de información cuando este grupo se agrega a las líneas Para, CC o CCO de un nuevo mensaje de correo electrónico. Por ejemplo, puede agregar una información sobre correo a los grupos grandes para advertir a los posibles remitentes de que su mensaje enviará a muchas personas.


> [!NOTE]
> La información sobre correo puede incluir etiquetas HTML, pero no se permiten los scripts. La longitud de la información de una sugerencia de correo electrónico personalizada no puede superar los 175 caracteres mostrados. Las etiquetas HTML no se cuentan en el límite.



## Delegación del grupo

Use esta sección para asignar permisos a un usuario (denominado *delegado*) y permitirle enviar mensajes como grupo o en nombre del grupo. Se pueden asignar los siguientes permisos:

  - **Enviar como**   Este permiso permite al delegado enviar mensajes como grupo. Después de asignar este permiso, el delegado tiene la opción de agregar el grupo a la línea **De** para indicar que el mensaje ha sido enviado por el grupo.

  - **Enviar en nombre de**   Este permiso también permite que el delegado envíe mensajes en nombre del grupo. Después de asignar este permiso, el delegado podrá agregar el grupo en la línea **De**. El mensaje parecerá enviado por el grupo y dirá que fue enviado por el delegado en nombre del grupo.

Para asignar permisos a los delegados, haga clic en **Agregar** debajo del permiso adecuado para mostrar la página **Seleccionar destinatario**, que muestra una lista de todos los destinatarios en su organización de Exchange que pueden asignarse al permiso. Seleccione los destinarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").

## Usar el Shell para cambiar las propiedades del grupo de seguridad

Use los cmdlets **Get-DistributionGroup** y **Set-DistributionGroup** para ver y cambiar las propiedades de los grupos de seguridad. Las ventajas de usar el Shell incluyen la capacidad de cambiar las propiedades no disponibles en el EAC y cambiar las propiedades de varios grupos de seguridad. Para obtener más información acerca de cuáles son los parámetros que se corresponden con las propiedades del grupo de distribución, consulte los siguientes temas:

  - [Get-DistributionGroup](https://technet.microsoft.com/es-es/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/es-es/library/bb124955\(v=exchg.150\))

A continuación aparecen algunos ejemplos de cómo usar el Shell para cambiar las propiedades del grupo de seguridad.

En este ejemplo aparece una lista de todos los grupos de seguridad de la organización.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')}

En este ejemplo se cambia la dirección SMTP principal (también denominada dirección de respuesta) del grupo de seguridad Seattle Administrators de admins@contoso.com a seattle.admins@contoso.com. La dirección de respuesta anterior se conservará como dirección proxy.

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.admins@contoso.com,smtp:admins@contoso.com

En este ejemplo se ocultan todos los grupos de seguridad de la organización en la libreta de direcciones.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} | Set-DistributionGroup -HiddenFromAddressListsEnabled $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si cambió las propiedades de un grupo de seguridad correctamente, haga lo siguiente:

  - En el EAC, seleccione el grupo y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para visualizar la propiedad o característica que ha modificado. Según la propiedad que ha modificado, se podrá ver en el panel Detalles para el grupo seleccionado.

  - En el Shell, use el cmdlet **Get-DistributionGroup** para verificar los cambios. Una ventaja de usar el Shell es que puede ver varias propiedades para varios grupos. En el ejemplo anterior en el que todos los grupos de seguridad estaban ocultos en la libreta de direcciones, ejecute el comando siguiente para verificar el valor nuevo.
    
        Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} |
         fl Name,HiddenFromAddressListsEnabled


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Icono reducido de LinkedIn Learning" alt="Icono reducido de LinkedIn Learning" /> <strong>¿Es la primera vez que usa Office 365?</strong><br />
LinkedIn Learning pone a su disposición vídeos gratuitos de cursos de <a href="https://support.office.com/es-es/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>.</p></td>
</tr>
</tbody>
</table>

