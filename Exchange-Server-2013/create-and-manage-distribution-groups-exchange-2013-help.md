---
title: 'Crear y administrar grupos de distribución: Exchange 2013 Help'
TOCTitle: Crear y administrar grupos de distribución
ms:assetid: c4c43493-55e1-46d2-bd4b-d6f6cecd747f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124513(v=EXCHG.150)
ms:contentKeyID: 48268677
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDistributionGroupWizardForm.CreateDistributionGroupIntroductionWizardPage
ms.translationtype: HT
---

# Crear y administrar grupos de distribución

 

_**Se aplica a:** Exchange Online, Exchange Server 2016, Office 365_

_**Última modificación del tema:** 2016-12-09_

Use el Centro de Administración de Exchange (EAC) o el Shell de administración de Exchange para crear un nuevo grupo de distribución en su organización de Exchange o para habilitar el correo a un grupo existente en Active Directory.

Estos son dos tipos de grupos que pueden usarse para distribuir mensajes:

  - Los *grupos de distribución universal habilitados para correo* (también llamados *grupos de distribución*) solo se usan para distribuir mensajes.

  - Los *grupos de seguridad universal habilitados para correo* (también llamados *grupos de seguridad*) pueden usarse tanto para distribuir mensajes, como para conceder permisos de acceso a los recursos en Active Directory. Para obtener más información, consulte [Administrar grupos de seguridad habilitados para correo](manage-mail-enabled-security-groups-exchange-2013-help.md).

Es importante tener en cuenta las diferencias terminológicas entre Active Directory y Exchange. En Active Directory, un grupo de distribución es cualquier grupo que no tiene ningún contexto de seguridad con independencia de que esté habilitado para correo. Sin embargo, en Exchange, todos los grupos habilitados para correo se denominan grupos de distribución con independencia de que tengan un contexto de seguridad.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 a 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de distribución" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Si su organización ha configurado una directiva de nomenclatura de grupos, esta se aplica solo a los grupos creados por los usuarios. Si usted u otros administradores utilizan el Centro de Administración de Exchange para crear grupos de distribución, la directiva de nomenclatura de grupos se ignora y no se aplica al nombre del grupo. No obstante, si utiliza el Shell para crear o cambiar el nombre de un grupo de distribución, la directiva se aplica a menos que use el parámetro *IgnoreNamingPolicy* para invalidar la directiva de nomenclatura de grupos. Para obtener más información, vea:
    
      - [Crear una directiva de nomenclatura de grupos de distribución](create-a-distribution-group-naming-policy-exchange-2013-help.md)
    
      - [Invalidar la directiva de nomenclatura de grupos de distribución](override-the-distribution-group-naming-policy-exchange-2013-help.md)

## ¿Qué desea hacer?

## Crear un grupo de distribución

## Usar el Centro de Administración de Exchange para crear grupos de distribución

1.  En el EAC, vaya a **Destinatarios** \> **Grupos**.

2.  Haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") \> **Grupo de distribución**.

3.  
    

    > [!TIP]
    > <IMG title="Nueva prueba de Grupos de Office 365" alt="Nueva prueba de Grupos de Office 365" src="images/Bb124513.3ea82c95-9dda-450f-823b-cd0772249d81(EXCHG.150).png"><BR>Ahora puede crear un grupo de Office 365 en lugar de un grupo de distribución si tiene un plan de Office 365 para empresas o un plan de Exchange Online. Los grupos de Office 365 tienen las características de un grupo de distribución y muchas más. Con los grupos de Office 365, puede enviar correos electrónicos a un grupo, compartir un calendario común, tener una biblioteca para almacenar y trabajar en archivos y carpetas de grupo. Haga clic en <STRONG>Nuevo</STRONG><IMG title="Agregar icono" alt="Agregar icono" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">&nbsp;&gt;&nbsp;<STRONG>Grupo de Office 365</STRONG> para comenzar y consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=800653">Grupos de Office 365 - ayuda para administradores</A>.<BR>Si tiene grupos de distribución existentes que quiera migrar a grupos de Office 365, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=824756">Migrar listas de distribución a grupos de Office 365: ayuda para administradores</A>.<BR>Si desea crear un grupo de distribución, haga clic o pulse en el asistente para <STRONG>Nuevo grupo de distribución</STRONG>.



4.  
    
    En la página **Nuevo grupo de distribución**, complete los siguientes cuadros de texto:
    
      - **\* Nombre para mostrar**   Use este cuadro de texto para escribir el nombre para mostrar. Este nombre aparece en la libreta de direcciones de su organización, en las líneas Para: cuando se envía un correo electrónico a este grupo, y en la lista Grupos en el EAC. El nombre para mostrar es obligatorio y debe ser sencillo para que los usuarios puedan identificarlo. También deben ser únicos en el bosque.
    
      - **\* Alias**   Use este cuadro de texto para escribir el nombre de alias del grupo. El alias no puede superar los 64 caracteres y debe ser único en el bosque. Cuando un usuario escribe el alias en la línea Para: de un mensaje de correo electrónico, se resuelve en el nombre para mostrar del grupo.
    
      - **Unidad organizativa** (Solo verá esta opción en Exchange 2013 local) Puede seleccionar una unidad organizativa (OU) que no sea la predeterminada (que es el ámbito del destinatario). Si el ámbito de destinatario definido corresponde al bosque, el valor predeterminado será el contenedor Usuarios del dominio de Active Directory que contiene el equipo en el que se ejecuta EAC. Si el ámbito del destinatario está establecido en un dominio específico, el contenedor de usuarios se selecciona de modo predeterminado. Si el ámbito del destinatario está establecido en una unidad organizativa específica (OU), esa OU se selecciona de modo predeterminado.
        
        Para seleccionar otra OU, haga clic en **Examinar**. En el cuadro de diálogo se muestran todas las OU del bosque dentro del ámbito especificado. Seleccione la unidad organizativa que desee y haga clic en **Aceptar**.
    
      - **\* Propietarios**   De forma predeterminada, la persona que crea un grupo pasa a ser el propietario. Todos los grupos deben tener al menos un propietario. Puede agregar propietarios haciendo clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").
    
      - **Miembros**   Esta sección sirve para agregar miembros e indicar si se necesita aprobación para los usuarios que se unan al grupo o lo dejen.
        
        Los propietarios de un grupo no tienen que ser miembros de éste. Use **Agregar propietarios de grupo como miembros** para agregar o quitar propietarios como miembros.
        
        Para agregar miembros al grupo, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Cuando haya terminado de agregar los miembros, haga clic en **Aceptar** para volver a la página **Nuevo grupo de distribución**.
        
        En **Elige si para incorporarse al grupo se necesita la aprobación del propietario**, indique si se requiere aprobación para que usuarios puedan unirse al grupo. Seleccione uno de los siguientes parámetros:
        
          - **Abierto: Cualquiera puede unirse al grupo sin la aprobación de los propietarios del grupo**. Se trata del valor predeterminado.
        
          - **Cerrado: sólo los propietarios del grupo pueden agregar miembros. Se rechazarán automáticamente todas las solicitudes para unirse**
        
          - **Aprobación del propietario: Todas las solicitudes se aprueban manualmente o son rechazadas por los propietarios del grupo**   Si selecciona esta opción, el propietario o los propietarios del grupo recibirán un mensaje de correo electrónico en el que se solicita la aprobación para unirse al grupo.
        
        En **Elige si el grupo está abierto para abandonarlo**, indique si se requiere aprobación para que los usuarios dejen el grupo. Seleccione uno de los siguientes parámetros:
        
          - **Abierto: Cualquiera puede dejar el grupo sin necesidad de aprobación por parte de los propietarios del grupo**.   Se trata del valor predeterminado.
        
          - **Cerrado: sólo los propietarios del grupo pueden quitar miembros. Se rechazarán automáticamente todas las solicitudes para abandonar**.

5.  Cuando haya terminado, haga clic en **Guardar** para crear el grupo de distribución.


> [!NOTE]
> De manera predeterminada, todos los nuevos grupos de distribución requieren que todos los remitentes estén autenticados. De este modo se evita que remitentes externos envíen mensajes a grupos de distribución. Para configurar un grupo de distribución para que acepte mensajes de todos los remitentes, debe modificar las configuraciones de restricciones de entrega de mensajes para dicho grupo de distribución.



## Uso del Shell para crear grupos de distribución

Este ejemplo crea un grupo de distribución con un alias **itadmin** y el nombre **Administradores de TI**. El grupo de distribución se crea en una unidad organizativa predeterminada y cualquier usuario puede unirse al grupo sin aprobación por parte de los propietarios de este.

    New-DistributionGroup -Name "IT Administrators" -Alias itadmin -MemberJoinRestriction open

Para obtener más información acerca del uso del Shell para crear grupos de distribución, consulte [New-DistributionGroup](https://technet.microsoft.com/es-es/library/aa998856\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó correctamente un grupo de distribución, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios**  \> **Grupos**. El nuevo grupo de distribución aparece en la lista de grupos. En **Tipo de grupo**, el tipo es **Grupo de distribución**.

  - En el Shell, ejecute el siguiente comando para que aparezca información acerca del nuevo grupo de distribución.
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress


> [!NOTE]
> Solo puede crear o habilitar para correo grupos de distribución universal. Para convertir un grupo de dominio local o global en un grupo universal, puede usar el cmdlet <A href="https://technet.microsoft.com/es-es/library/bb123770(v=exchg.150)">Set-Group</A> que usa el Shell. Puede disponer de grupos habilitados para correo migrados de versiones anteriores de Exchange&nbsp;que no sean grupos universales. Puede usar el Centro de administración de Exchange o el Shell para administrar estos grupos



## Modificación de las propiedades del grupo de distribución

## Uso del Centro de Administración de Exchange para modificar las propiedades del grupo de distribución

1.  En el Centro de Administración de Exchange, vaya a **Destinatarios**  \> **Grupos**.

2.  En la lista de grupos, haga clic en el grupo de distribución que desea ver o modificar, y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del grupo, haga clic en una de las siguientes secciones para ver o cambiar las propiedades.
    
      - General
    
      - Propiedad
    
      - Pertenencia
    
      - Aprobación de la pertenencia
    
      - Administración de entregas
    
      - Aprobación de mensajes
    
      - Opciones de correo electrónico
    
      - MailTip
    
      - Delegación del grupo

## General

Utilice esta sección para ver o cambiar la información básica sobre el grupo.

  - **\* Nombre para mostrar**   Este nombre aparece en la libreta de direcciones, en las líneas Para: cuando se envía un correo electrónico a este grupo, y en la lista Grupos. El nombre para mostrar es obligatorio y debe ser sencillo para que los usuarios puedan identificarlo. También tiene que ser único en su dominio.
    
    Si ha implementado una directiva de nomenclatura de grupo, el nombre para mostrar tiene que cumplir al formato de nomenclatura definido por la directiva.

  - **\* Alias**   Esta es la parte de la dirección de correo electrónico que aparece a la izquierda del símbolo (@). Si cambia el alias, la dirección SMTP primaria para el grupo también cambiará y contendrá el nuevo alias. Además, la dirección de correo electrónico con el alias anterior se mantendrá como dirección proxy para el grupo.

  - **Descripción**   Utilice este cuadro para describir el grupo, de forma que los usuarios sepan cuál es el propósito del grupo. Esta descripción aparece en la libreta de direcciones en el panel de detalles en el EAC.

  - **Ocultar este grupo de la lista de direcciones**   Seleccione esta casilla de verificación si no desea que los usuarios vean este grupo en la libreta de direcciones. Para enviar un correo electrónico a este grupo, un remitente tiene que escribir la dirección de correo electrónico o alias del grupo en la línea Para: o en el campo Cc: .
    

    > [!TIP]
    > Considere la posibilidad de ocultar los grupos de seguridad porque normalmente se usan para asignar permisos a los miembros del grupo y no para enviar correo electrónico.



  - **Unidad organizativa**   Este cuadro de solo lectura muestra la unidad organizativa (OU) que contiene el grupo de distribución. Debe usar los usuarios y los equipos de Active Directory para mover el grupo a una OU distinta.

## Propiedad

Utilice esta sección para asignar los propietarios de grupo. El propietario de grupo puede agregar miembros al grupo, aprobar o rechazar solicitudes para unirse al grupo o abandonarlo y aprobar o rechazar los mensajes que se envían al grupo. De forma predeterminada, la persona que crea un grupo pasa a ser el propietario. Todos los grupos deben tener al menos un propietario.

Puede agregar propietarios haciendo clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Asimismo, puede quitar a un propietario al seleccionarlo y hacer clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

## Pertenencia

Utilice esta sección para agregar o quitar miembros. Los propietarios de un grupo no tienen que ser miembros de éste. Bajo **Miembros**, puede agregar miembros haciendo clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Puede quitar a un miembro seleccionando un usuario de la lista de miembros y haciendo clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

## Aprobación de la pertenencia

Use esta sección para indicar si se necesita aprobación para que los usuarios se unan al grupo o lo abandonen.

  - **Elige si para incorporarse al grupo se necesita la aprobación del propietario.**   Seleccione uno de los siguientes parámetros:
    
      - **Abierto: Cualquiera puede unirse a este grupo sin la aprobación de los propietarios del grupo**
    
      - **Cerrado: sólo los propietarios del grupo pueden agregar miembros. Se rechazarán automáticamente todas las solicitudes para unirse**
    
      - **Aprobación del propietario: Todos los pedidos son aprobados o rechazados por los propietarios de grupo.**   Si selecciona esta opción, el propietario o los propietarios del grupo recibirán un correo electrónico en el que se solicita la aprobación para unirse al grupo.

  - **Elegir si el grupo está abierto para salir**. Seleccione uno de los siguientes parámetros:
    
      - **Abierto: Cualquiera puede abandonar este grupo sin la aprobación de sus propietarios   **
    
      - **Cerrado: sólo los propietarios del grupo pueden quitar miembros. Se rechazarán automáticamente todas las solicitudes para abandonar**.

## Administración de entregas

Use esta sección para administrar quién envía correos electrónicos a este grupo.

  - **Solo los remitentes de mi organización**   Seleccione esta opción para permitir que únicamente los remitentes de la organización envíen mensajes al grupo. Esto significa que si alguien de fuera de la organización envía un correo electrónico a este grupo, se rechazará. Esta es la configuración predeterminada.

  - **Remitentes dentro y fuera de mi organización**   Seleccione esta opción para permitir a cualquiera enviar mensajes al grupo.
    
    Puede limitar todavía más quién puede enviar mensajes al grupo, permitiendo solo a remitentes concretos enviar mensajes a este grupo. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, a continuación, seleccione uno o más destinatarios. Si agrega remitentes a esta lista, son los únicos que pueden enviar correo al grupo. Se rechazará el correo enviado por cualquier remitente que no esté en la lista.
    
    Para quitar a un usuario o grupo de la lista, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").
    

    > [!IMPORTANT]
    > Si ha configurado el grupo para permitir que solo los remitentes internos a la organización envíen mensajes al grupo, se rechazarán los correos electrónicos enviados por un contacto de correo, aun cuando se agregue a esta lista.



## Aprobación de mensajes

Use esta sección para establecer las opciones para moderar el grupo. Los moderadores admiten o rechazan los mensajes enviados al grupo antes de que lleguen a los miembros del grupo.

  - **Los mensajes enviados a este grupo tienen que ser aprobados por un moderador** Esta casilla no está seleccionada de forma predeterminada. Si activa esta casilla, los moderadores del grupo revisarán los mensajes entrantes antes de llegar a su destino. Los moderadores de grupo pueden admitir o rechazar mensajes entrantes.

  - **Moderadores de grupo**   Para agregar moderadores de grupo, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para quitar a un moderador, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar"). Si ha activado la casilla "Los mensajes enviados a este grupo tienen que ser aprobados por un moderador" y no elige un moderador, los mensajes enviados al grupo se remitirán al propietario de dicho grupo para su aprobación.

  - **Remitentes que no requieran la aprobación de mensajes**    Para agregar usuarios o grupos que no se vean afectados por la moderación de este grupo, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para quitar a un usuario o un grupo, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

  - **Seleccionar notificaciones de moderación   **Use esta sección para establecer la forma en que se notifica a los usuarios con respecto a la aprobación de mensajes.
    
      - **Notificar a todos los remitentes cuando sus mensajes no son aprobados**   Es la configuración predeterminada. Envíe una notificación a todos los remitentes, de dentro y de fuera de la organización, cuando no se apruebe su mensaje.
    
      - **Enviar notificación a los remitentes de tu organización cuando sus mensajes no se aprueben.**   Si selecciona esta opción, únicamente los usuarios y grupos en su organización recibirán una notificación cuando el moderador no apruebe un mensaje que hayan enviado al grupo.
    
      - **No notificar a nadie cuando no se apruebe un mensaje**   Si selecciona esta opción, no se enviarán notificaciones a los remitentes cuyos mensajes no hayan aprobado los moderadores de grupo.

## Opciones de correo electrónico

Use esta sección para ver o cambiar las direcciones de correo electrónico asociadas con el grupo. Esto incluye las direcciones de SMTP primarias del grupo y cualquier proxy asociado. La dirección SMTP principal (también denominada *dirección de respuesta* ) se muestra en negrita en la lista de direcciones, con el valor **SMTP** en mayúsculas en la columna **Tipo**.

  - **Agregar **  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una dirección de correo electrónico nueva para este buzón. Seleccione uno de los siguientes tipos de dirección:
    
      - **Dirección SMTP**   Este es el tipo de dirección predeterminado. Haga clic en este botón y luego escriba la nueva dirección SMTP en la casilla **\* Dirección de correo electrónico**.
        

        > [!NOTE]
        > Para que la nueva dirección se convierta en la dirección SMTP principal del grupo, seleccione la casilla <STRONG>Convertir en dirección de respuesta</STRONG>.

    
      - **Tipo de dirección personalizada**   Haga clic en este botón y escriba uno de los tipos de dirección de correo electrónico que no sean SMTP admitidos en la casilla **\* Dirección de correo electrónico**.
        

        > [!NOTE]
        > Con excepción de las direcciones X.400, Exchange no valida las direcciones personalizadas para comprobar el formato correcto. Debe asegurarse de que la dirección personalizada que especifica cumpla los requisitos de formato para el tipo de dirección.



  - **Editar**   Para modificar una dirección de correo electrónico asociada con el grupo, selecciónela de la lista y luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    

    > [!NOTE]
    > Para que una dirección existente se convierta en la dirección SMTP principal del grupo, seleccione la casilla de verificación <STRONG>Hacer que esta sea la dirección de respuesta</STRONG>.



  - **Quitar**   Para quitar una dirección de correo electrónico asociada con el grupo, selecciónela de la lista y luego, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

  - **Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada al destinatario.   **Seleccione esta casilla de verificación para que las direcciones de correo electrónico del destinatario se actualicen automáticamente según los cambios realizados en las directivas de direcciones de correo electrónico de su organización. Esta casilla está activada de forma predeterminada.

## MailTip

Use esta sección para agregar una Sugerencia de correo electrónico para alertar a los usuarios sobre potenciales problemas en caso de que envíen un mensaje a este grupo. Una información sobre correo es texto que se muestra en la barra de información cuando este grupo se agrega a las líneas Para, CC o CCO de un nuevo mensaje de correo electrónico. Por ejemplo, puede agregar una información sobre correo a los grupos grandes para advertir a los posibles remitentes de que su mensaje enviará a muchas personas.


> [!NOTE]
> La información sobre correo puede incluir etiquetas HTML, pero no se permiten los scripts. La longitud de la información de una sugerencia de correo electrónico personalizada no puede superar los 175 caracteres mostrados. Las etiquetas HTML no se cuentan en el límite.



## Delegación del grupo

Use esta sección para asignar permisos a un usuario (denominado *delegado*) y permitirle enviar mensajes como grupo o en nombre del grupo. Se pueden asignar los siguientes permisos:

  - **Enviar como**   Este permiso permite al delegado enviar mensajes como grupo. Después de asignar este permiso, el delegado tiene la opción de agregar el grupo a la línea **De** para indicar que el mensaje ha sido enviado por el grupo.

  - **Enviar en nombre de**   Este permiso también permite que el delegado envíe mensaje en nombre del grupo. Después de asignar este permiso, el delegado podrá agregar el grupo en la línea **De**. El mensaje parecerá enviado por el grupo y dirá que fue enviado por el delegado en nombre del grupo.

Para asignar permisos a los delegados, haga clic en **Agregar** debajo del permiso adecuado para que aparezca la página **Seleccionar destinatario**, que muestra una lista de todos los destinatarios en su organización de Exchange que pueden asignarse al permiso. Seleccione los destinatarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico escribiendo el nombre del destinatario en la casilla de búsqueda y luego haciendo clic en **Buscar**.

## Uso del Shell para modificar las propiedades del grupo de distribución

Use los cmdlet **Get-DistributionGroup** y **Set-DistributionGroup** para ver y modificar las propiedades de los grupos de distribución. Una de las ventajas de usar el Shell es la posibilidad de modificar las propiedades que no están disponibles en el Centro de Administración de Exchange y la posibilidad de modificar las propiedades para varios grupos. Para obtener más información acerca de los parámetros que corresponden a las propiedades del grupo de distribución, consulte los siguientes temas:

  - [Get-DistributionGroup](https://technet.microsoft.com/es-es/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/es-es/library/bb124955\(v=exchg.150\))

Aquí le presentamos algunos ejemplos usando el Shell para modificar las propiedades del grupo de distribución.

Estos ejemplos cambian la dirección SMTP principal (también llamada la dirección de respuesta) para el grupo de distribución de empleados de Seattle de employees@contoso.com a sea.employees@contoso.com. La dirección de respuesta anterior se mantendrá como una dirección proxy.

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.employees@contoso.com,smtp:employees@contoso.com

Este ejemplo limita el tamaño máximo de los mensajes que se pueden enviar a todos los grupos de distribución en la organización en 10 megabytes (MB).

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalDistributionGroup')} | Set-DistributionGroup -MaxReceiveSize 10MB

En este ejemplo se habilita la moderación para el grupo de distribución Customer Support y se establece que la moderadora sea Amy. Asimismo, este grupo de distribución moderado notificará a los remitentes, que envíen mensajes de correo electrónico desde dentro de la organización, si sus mensajes no se han aprobado.

    Set-DistributionGroup -Identity "Customer Support" -ModeratedBy "Amy" -ModerationEnabled $true -SendModerationNotifications 'Internal'

En este ejemplo se cambia el grupo de distribución Dog Lovers que ha creado el usuario para que el administrador del grupo tenga que aprobar las solicitudes de los usuarios para unirse al grupo. Además, gracias al parámetro *BypassSecurityGroupManagerCheck*, el administrador del grupo recibirá una notificación indicando que se ha aplicado un cambio en la configuración del grupo de distribución.

    Set-DistributionGroup -Identity "Dog Lovers" -MemberJoinRestriction 'ApprovalRequired' -BypassSecurityGroupManagerCheck

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si modificó correctamente las propiedades de un grupo de distribución, siga uno de estos procedimientos:

  - En el EAC, seleccione el grupo y luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para ver la propiedad o característica que modificó. Según la propiedad que ha modificado, se podrá ver en el panel Detalles para el grupo seleccionado.

  - En el Shell, use el cmdlet **Get-DistributionGroup** para verificar los cambios. Una ventaja de usar el Shell es que puede ver varias propiedades para varios grupos. En el ejemplo anterior en el que se cambió el límite de destinatarios, ejecute el siguiente comando para comprar el valor nuevo.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    Ejecute este comando para el ejemplo anterior donde se modificaron los límites del mensaje.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

