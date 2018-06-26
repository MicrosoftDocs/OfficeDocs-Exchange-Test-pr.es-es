---
title: 'Administrar grupos de distribución dinámica: Exchange 2013 Help'
TOCTitle: Administrar grupos de distribución dinámica
ms:assetid: 8ef85d0a-41df-4b5c-b8e7-ca8d09c048ca
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123722(v=EXCHG.150)
ms:contentKeyID: 48267687
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDynamicGroupWizardForm.CreateDynamicGroupInformationWizardPage
ms.translationtype: HT
---

# Administrar grupos de distribución dinámica

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Los grupos de distribución dinámicos son objetos de grupo de Active Directory habilitados para correo que se crean para acelerar el envío masivo de mensajes de correo electrónico y demás información dentro de una organización de Microsoft Exchange.

A diferencia de los grupos de distribución regular, que contienen un conjunto definido de miembros, la lista de miembros para grupos de distribución dinámica se calcula cada vez que se envía un mensaje al grupo, en base a los filtros y condiciones definidos. Cuando se envía un mensaje de correo electrónico a un grupo de distribución dinámico, éste se entrega a todos los destinatarios de la organización que coincidan con los criterios definidos para ese grupo.


> [!IMPORTANT]
> Un grupo de distribución dinámico incluye todos los destinatarios de Active Directory&nbsp;con valores de atributo que coincidan con su filtro. Si las propiedades de un destinatario se modifican para que coincidan con el filtro, el destinatario podría pasar inadvertidamente a ser un miembro del grupo y empezar a recibir mensajes enviados al grupo. Unos procesos de aprovisionamiento de cuentas coherentes y bien definidos reducirán las probabilidades de que esto ocurra.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 a 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de distribución dinámica" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Crear un grupo de distribución dinámico

## Uso del EAC para crear un grupo de distribución dinámico

1.  En el Centro de administración de Exchange (EAC), navegue hasta **Destinatarios**  \> **Grupos** \> **Nuevo** \> **Grupo de distribución dinámico**.

2.  
    
    En la página **Nuevo grupo de distribución dinámico**, complete los siguientes cuadros:
    
      - **\* Nombre para mostrar** Utilice este cuadro para introducir el nombre para mostrar. Este nombre aparece en la libreta de direcciones compartida, en las líneas Para: cuando se envía un correo electrónico a este grupo, y en la lista Grupos en el EAC. El nombre para mostrar es obligatorio y debe ser sencillo para que los usuarios puedan identificarlo. También deben ser únicos en el bosque.
        

        > [!NOTE]
        > La directiva de nombres de grupos no se aplica a los grupos de distribución dinámicos.

    
      - **\* Alias**   Escriba en este cuadro el nombre del alias del grupo. El alias no puede superar 64 caracteres y debe ser único en el bosque. Cuando un usuario escribe el alias en la línea Para: de un mensaje de correo electrónico, se resuelve en el nombre para mostrar del grupo.
    
      - **Descripción**   Utilice este cuadro para describir el grupo, de forma que los usuarios sepan cuál es el propósito del grupo. Esta información aparece en la libreta de direcciones compartida.
    
      - **Unidad organizativa**   Puede seleccionar una unidad organizativa (OU) diferente a la que aparece de forma predeterminada (en el ámbito de destinatarios). Si el ámbito de destinatario definido está establecido en el bosque, el valor predeterminado será el contenedor Usuarios del dominio Active Directory que contiene el equipo en el que se ejecuta EAC. Si el ámbito del destinatario está establecido en un dominio específico, el contenedor de usuarios se selecciona de modo predeterminado. Si el ámbito del destinatario está establecido en una unidad organizativa específica (OU), esa OU se selecciona de modo predeterminado.
        
        Para seleccionar otra OU, haga clic en **Examinar**. En el cuadro de diálogo se muestran todas las OU del bosque dentro del ámbito especificado. Seleccione la unidad organizativa que desee y haga clic en **Aceptar**.
    
      - **Propietario** Es opcional introducir un propietario de un grupo de distribución dinámico. Puede agregar propietarios haciendo clic en **Explorar** y, a continuación, seleccionando los usuarios de la lista.

3.  
    
    Utilice la sección **Miembros** para especificar los tipos de destinatarios del grupo y configurar las reglas que determinarán la pertenencia. Seleccione uno de los siguientes cuadros:
    
      - **Todos los tipos de destinatarios**   Elija esta opción para enviar mensajes que cumplan con los criterios definidos para este grupo a todos los tipos de destinatarios.
    
      - **Solo los siguientes tipos de destinatarios**   Se enviarán los mensajes que cumplen con los criterios definidos para este grupo a uno o más de los siguientes tipos de destinatarios:
        
          - **Usuarios con buzones de Exchange**   Seleccione esta casilla si desea incluir los usuarios que tienen buzones de Exchange. Los usuarios con buzones de Exchange son los que tienen una cuenta de dominio de usuario y un buzón de correo en la organización de Exchange.
        
          - **Usuarios con direcciones de correo electrónico externas**   Seleccione esta casilla si desea incluir los usuarios con direcciones de correo electrónico externas. Los usuarios con cuentas de correo electrónico externas tienen cuentas de dominio de usuario en Active Directory, pero usan cuentas de correo electrónico que son externas a la organización. Esto permite incluirlos en la lista global de direcciones (GAL) y agregarlos a las listas de distribución.
        
          - **Buzones de recursos**   Active esta casilla si desea incluir los buzones de recursos de Exchange. Los buzones de correo de recursos permiten administrar recursos corporativos a través de un buzón de correo, como una sala de conferencias o un vehículo de empresa.
        
          - **Contactos con direcciones de correo electrónico externas**   Seleccione esta casilla si desea incluir los contactos con direcciones de correo electrónico externas. Los contactos con cuentas de correo electrónico externas no tienen cuentas de dominio de usuario en Active Directory, pero la dirección de correo electrónico externa está disponible en la LGD.
        
          - **Grupos habilitados para correo**   Active esta casilla si desea incluir los grupos de seguridad o de distribución habilitados para correo. Los grupos con correo habilitado son similares a los grupos de distribución. Los mensajes de correo electrónico enviados a las cuentas de dichos grupos se entregarán a varios destinatarios.

4.  
    
    Haga clic en **Agregar una regla** para definir los criterios de pertenencia de este grupo.

5.  Seleccione uno de los siguientes atributos de destinatario en la lista desplegable y añádale un valor. Si el valor del atributo seleccionado coincide con el valor definido, el destinatario recibirá un mensaje enviado a este grupo.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Atributo</th>
    <th>Enviar mensaje a un destinatario si...</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Contenedor de destinatarios</strong></p></td>
    <td><p>El objeto de destinatario reside en el dominio especificado o unidad organizativa.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Estado o provincia</strong></p></td>
    <td><p>El valor especificado coincide con estado o propiedad de la provincia del destinatario.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Company</strong></p></td>
    <td><p>El valor especificado coincide con la propiedad de la empresa del destinatario.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Departamento</strong></p></td>
    <td><p>El valor especificado coincide con la propiedad del departamento del destinatario.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>AttributeN personalizado</strong> (donde N es un número del 1 al 15)</p></td>
    <td><p>El valor especificado coincide con la propiedad de CustomAttributeN del destinatario.</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!IMPORTANT]
    > Los valores que establezca para los atributos seleccionados deben coincidir exactamente con los que aparecen en las propiedades del destinatario. Por ejemplo, si introduce <STRONG>Washington</STRONG> para <STRONG>Estado o provincia</STRONG>, pero el valor de la propiedad del destinatario es <STRONG>WA</STRONG>, no se cumplirá la condición. Además, los valores de texto que especifique no distinguen mayúsculas de minúsculas. Por ejemplo, si especifica <STRONG>Contoso</STRONG> para el atributo <STRONG>Empresa</STRONG>, un destinatario recibirá mensajes aunque su valor sea <STRONG>contoso</STRONG>.



6.  En la ventana **Especificar palabras o frases**, introduzca el valor en el cuadro de texto. Haga clic en **Agregar** y, a continuación, en **Aceptar**.

7.  Para añadir otra regla para definir los criterios de pertenencia, haga clic en **Agregar una regla** bajo la regla anterior que ha creado.
    

    > [!IMPORTANT]
    > Si añade varias reglas para definir la pertenencia, un destinatario tendrá que cumplir con los criterios de cada regla para poder recibir un mensaje enviado al grupo. En resumen, cada regla está conectada al operador booleano <STRONG>AND</STRONG>.



8.  Cuando haya terminado, haga clic en **Guardar** para crear el grupo de distribución dinámico.


> [!NOTE]
> Si desea especificar reglas para los atributos que sean distintas a las disponibles en el EAC, deberá utilizar el Shell para crear un grupo de distribución dinámico. Tenga en cuenta que los ajustes de filtro y condición para los grupos de distribución dinámicos que tienen filtros de destinatario personalizados solo se pueden administrar utilizando el Shell. Para obtener un ejemplo de cómo crear un grupo de distribución dinámico con una consulta personalizada, consulte la siguiente sección sobre cómo usar el Shell para crear un grupo de distribución dinámico.



## Uso de Shell para crear un grupo de distribución dinámico

En este ejemplo se crea el grupo de distribución dinámico "Mailbox Users DDG" que solo contiene usuarios de buzón de correo.

    New-DynamicDistributionGroup -IncludedRecipients MailboxUsers -Name "Mailbox Users DDG" -OrganizationalUnit Users

En este ejemplo se crea un grupo de distribución dinámico con un filtro de destinatarios personalizado. El grupo de distribución dinámico contiene todos los usuarios de buzón de un servidor denominado Server1.

    New-DynamicDistributionGroup -Name "Mailbox Users on Server1" -OrganizationalUnit Users -RecipientFilter {((RecipientTypeDetails -eq 'UserMailbox' -and ServerName -eq 'Server1'))}

En este ejemplo se crea un grupo de distribución dinámico con un filtro de destinatarios personalizado. El grupo de distribución dinámico contiene todos los usuarios de buzón de correo que tienen un valor de "FullTimeEmployee" en la propiedad **CustomAttribute10**.

    New-DynamicDistributionGroup -Name "Full Time Employees" -RecipientFilter {(RecipientTypeDetails -eq 'UserMailbox') -and (CustomAttribute10 -eq 'FullTimeEmployee')}

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-DynamicDistributionGroup](https://technet.microsoft.com/es-es/library/bb125127\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó un grupo de distribución dinámico correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Grupos**. El nuevo grupo de distribución dinámico aparece en la lista de grupos. Bajo **Tipo de grupo**, el tipo es **Grupo de distribución dinámico**.

  - En el Shell, ejecute el comando siguiente para mostrar información sobre el nuevo grupo de distribución dinámico.
    
        Get-DynamicDistributionGroup | FL Name,RecipientTypeDetails,RecipientFilter,PrimarySmtpAddress

## Cambiar las propiedades del grupo de distribución dinámico

## Uso del EAC para modificar las propiedades del grupo de distribución dinámico

1.  En el EAC, vaya a **Destinatarios** \> **Grupos**.

2.  En la lista de grupos, haga clic en el grupo de distribución dinámico que desea ver o modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del grupo, haga clic en una de las siguientes secciones para ver o cambiar las propiedades.
    
      - General
    
      - Propiedad
    
      - Pertenencia
    
      - Administración de entregas
    
      - Aprobación de mensajes
    
      - Opciones de correo electrónico
    
      - Información sobre correo
    
      - Delegación del grupo

## General

Utilice esta sección para ver o cambiar la información básica sobre el grupo.

  - **\* Nombre para mostrar**   Este nombre aparece en la libreta de direcciones, en las líneas Para: cuando se envía un correo electrónico a este grupo, y en la lista Grupos. El nombre para mostrar es obligatorio y debe ser sencillo para que los usuarios puedan identificarlo. También tiene que ser único en su dominio.

  - **\* Alias**   Esta es la parte de la dirección de correo electrónico que aparece a la izquierda del símbolo (@). Si cambia el alias, la dirección SMTP primaria para el grupo también cambiará y contendrá el nuevo alias. Además, la dirección de correo electrónico con el alias anterior se mantendrá como dirección proxy para el grupo.

  - **Descripción**   Utilice este cuadro para describir el grupo, de forma que los usuarios sepan cuál es el propósito del grupo. Esta descripción aparece en la libreta de direcciones en el panel de detalles en el EAC.

  - **Ocultar este grupo de la libreta de direcciones compartida**   Seleccione esta casilla si no desea que los usuarios vean este grupo en la libreta de direcciones. Para enviar un correo electrónico a este grupo, un remitente tiene que escribir la dirección de correo electrónico o alias del grupo en la línea Para: o en el campo Cc: .

  - **Unidad organizativa**   Este cuadro de solo lectura muestra la unidad organizativa (OU) que contiene el grupo de distribución. Debe usar los usuarios y los equipos de Active Directory para mover el grupo a una OU distinta.

## Propiedad

Utilice esta sección para asignar un propietario del grupo. Un grupo de distribución dinámico únicamente puede tener un propietario. El propietario del grupo aparece en la ficha **Administrado por** del objeto en Usuarios y equipos de Active Directory.

Puede agregar propietarios haciendo clic en **Explorar** y, a continuación, seleccionando los usuarios de la lista. Para suprimir el propietario, haga clic en **Borrar** y, a continuación, haga clic en **Guardar**.![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

## Pertenencia

Utilice esta sección para modificar los criterios utilizados para determinar la pertenencia del grupo. Puede eliminar o modificar las reglas de pertenencia existentes y agregar nuevas reglas. Para saber los procedimientos sobre cómo hacerlo, consulte el Uso del EAC para crear un grupo de distribución dinámico de los procedimientos sobre cómo configurar la pertenencia al usar el EAC para crear un nuevo grupo de distribución dinámico.

## Administración de entregas

Use esta sección para administrar quién envía correos electrónicos a este grupo.

  - **Solo los remitentes de mi organización**   Seleccione esta opción para permitir que únicamente los remitentes de la organización envíen mensajes al grupo. Esto significa que si alguien de fuera de la organización envía un mensaje de correo electrónico a este grupo, será rechazado. Esta es la configuración predeterminada.

  - **Remitentes dentro y fuera de mi organización**   Seleccione esta opción para permitir a cualquiera enviar mensajes al grupo.
    
    Puede limitar todavía más quién puede enviar mensajes al grupo, permitiendo solo a remitentes concretos enviar mensajes a este grupo. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, a continuación, seleccione uno o más destinatarios. Si agrega remitentes a esta lista, son los únicos que pueden enviar correo al grupo. Se rechazará el correo enviado por cualquier remitente que no esté en la lista.
    
    Para quitar a un usuario o grupo de la lista, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").
    

    > [!IMPORTANT]
    > Si ha configurado el grupo para permitir que solo los remitentes internos a la organización envíen mensajes al grupo, se rechazará el correo electrónico enviado por un contacto de correo, aunque se haya agregado a la lista.



## Aprobación de mensajes

Use esta sección para establecer las opciones para moderar el grupo. Los moderadores admiten o rechazan los mensajes enviados al grupo antes de que lleguen a los miembros del grupo.

  - **Los mensajes enviados a este grupo tienen que ser aprobados por un moderador** Esta casilla no está seleccionada de forma predeterminada. Si activa esta casilla, los moderadores del grupo revisarán los mensajes entrantes antes de llegar a su destino. Los moderadores de grupo pueden admitir o rechazar mensajes entrantes.

  - **Moderadores de grupo**   Para agregar moderadores de grupo, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para quitar a un moderador, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar"). Si ha activado la casilla "Los mensajes enviados a este grupo tienen que ser aprobados por un moderador" y no elige un moderador, los mensajes enviados al grupo se remitirán al propietario de dicho grupo para su aprobación.

  - **Remitentes que no requieran la aprobación de mensajes**    Para agregar usuarios o grupos que no se vean afectados por la moderación de este grupo, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para quitar a un usuario o un grupo, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

  - **Seleccionar notificaciones de moderación   **Use esta sección para establecer la forma en que se notifica a los usuarios con respecto a la aprobación de mensajes.
    
      - **Envíe una notificación a todos los remitentes si sus mensajes no se aprueban**   Es la configuración predeterminada. Envíe una notificación a todos los remitentes, de dentro y de fuera de la organización, cuando no se apruebe su mensaje.
    
      - • **Envíe una notificación a los remitentes de su organización sólo cuando sus mensajes no se aprueben**Si selecciona esta opción, únicamente los usuarios y grupos en la organización recibirán una notificación cuando el moderador no apruebe un mensaje que hayan enviado al grupo.
    
      - **No notificar a nadie cuando no se apruebe un mensaje**   Si selecciona esta opción, no se enviarán notificaciones a los remitentes cuyos mensajes no hayan aprobado los moderadores de grupo.

## Opciones de correo electrónico

Use esta sección para ver o cambiar las direcciones de correo electrónico asociadas con el grupo. Esto incluye las direcciones de SMTP primarias del grupo y cualquier proxy asociado. La dirección SMTP principal (también denominada *dirección de respuesta* ) se muestra en negrita en la lista de direcciones, con el valor **SMTP** en mayúsculas en la columna **Tipo**.

  - **Agregar **  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una dirección de correo electrónico nueva para este buzón. Seleccione uno de los siguientes tipos de dirección:
    
      - **Dirección SMTP**   Este es el tipo de dirección predeterminado. Haga clic en este botón y luego escriba la nueva dirección SMTP en la casilla **\* Dirección de correo electrónico**.
        

        > [!NOTE]
        > Para que la nueva dirección se convierta en la dirección SMTP principal del grupo, seleccione la casilla <STRONG>Convertir en dirección de respuesta</STRONG>.

    
      - **Tipo de dirección personalizada**   Haga clic en este botón y escriba uno de los tipos de dirección de correo electrónico que no sean SMTP admitidos en la casilla **\* Dirección de correo electrónico**.
        

        > [!NOTE]
        > Con excepción de las direcciones X.400, Exchange no valida las direcciones personalizadas para comprobar el formato adecuado. Debe asegurarse de que la dirección personalizada que especifica cumpla los requisitos de formato para el tipo de dirección.



  - **Editar**   Para cambiar una dirección de correo electrónico asociada al grupo, selecciónela en la lista y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    

    > [!NOTE]
    > Para que una dirección existente se convierta en la dirección SMTP principal del grupo, seleccione la casilla <STRONG>Convertir en dirección de respuesta</STRONG>.



  - **Quitar**   Para quitar una dirección de correo electrónico asociada al grupo, selecciónela en la lista y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

  - **Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada a este destinatario   **Seleccione esta casilla para que las direcciones de correo electrónico del destinatario se actualicen automáticamente según los cambios realizados en las directivas de direcciones de correo electrónico de su organización. Esta casilla está activada de forma predeterminada.

## Información sobre correo

Use esta sección para agregar una información sobre correo para avisar a los usuarios de problemas potenciales antes de enviar un mensaje a este grupo. Una información sobre correo es texto que se muestra en la barra de información cuando este grupo se agrega a las líneas Para, CC o CCO de un nuevo mensaje de correo electrónico. Por ejemplo, puede agregar una información sobre correo a los grupos grandes para advertir a los posibles remitentes de que su mensaje enviará a muchas personas.


> [!NOTE]
> La información sobre correo puede incluir etiquetas HTML, pero no se permiten los scripts. La longitud de la información de una sugerencia de correo electrónico personalizada no puede superar los 175 caracteres mostrados. Las etiquetas HTML no se cuentan en el límite.



## Delegación del grupo

Use esta sección para asignar permisos a un usuario (denominado *delegado*) y permitirle enviar mensajes como grupo o en nombre del grupo. Se pueden asignar los siguientes permisos:

  - **Enviar como**   Este permiso permite al delegado enviar mensajes como grupo. Después de asignar este permiso, el delegado tiene la opción de agregar el grupo a la línea **De** para indicar que el mensaje ha sido enviado por el grupo.

  - **Enviar en nombre de**   Este permiso también permite que el delegado envíe mensajes en nombre del grupo. Después de asignar este permiso, el delegado podrá agregar el grupo en la línea **De**. El mensaje parecerá enviado por el grupo y dirá que fue enviado por el delegado en nombre del grupo.

Para asignar permisos a los delegados, haga clic en **Agregar** debajo del permiso adecuado para mostrar la página **Seleccionar destinatario**, que muestra una lista de todos los destinatarios en su organización de Exchange que pueden asignarse al permiso. Seleccione los destinarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**.

## Uso del Shell para cambiar las propiedades del grupo de distribución dinámico

Use los cmdlets **Get-DynamicDistributionGroup** y **Set-DynamicDistributionGroup** para ver y cambiar las propiedades de los grupos de distribución dinámicos. Las ventajas de usar el Shell incluyen la capacidad de cambiar las propiedades no disponibles en el EAC y cambiar las propiedades de varios grupos. Para obtener más información acerca de los parámetros que corresponden a las propiedades del grupo de distribución dinámico, consulte los siguientes temas:

  - [Get-DynamicDistributionGroup](https://technet.microsoft.com/es-es/library/bb124762\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/es-es/library/bb123796\(v=exchg.150\))

A continuación aparecen algunos ejemplos de cómo usar el Shell para cambiar las propiedades del grupo de distribución dinámico.

En este ejemplo se cambian los siguientes parámetros de todos los grupos de distribución dinámicos de la organización:

  - Ocultar todos los grupos de distribución dinámicos de la libreta de direcciones

  - Establecer el tamaño máximo del mensaje que se puede enviar al grupo en 5 MB

  - Habilitar la moderación

  - Asignar al administrador como moderador del grupo

<!-- end list -->

    Get-DynamicDistributionGroup -ResultSize unlimited | Set-DynamicDistributionGroup -HiddenFromAddressListsEnabled $true -MaxReceiveSize 5MB -ModerationEnabled $true -ModeratedBy administrator

En este ejemplo se añade la dirección de correo electrónico del SMTP, Seattle.Employees@contoso.com, al grupo Todos los empleados.

    Set-DynamicDistributionGroup -Identity "All Employees" -EmailAddresses SMTP:All.Employees@contoso.com, smtp:Seattle.Employees@contoso.com

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si cambió las propiedades de un grupo de distribución dinámico correctamente, haga lo siguiente:

  - En el EAC, seleccione el grupo y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para visualizar la propiedad o característica que ha modificado. Según la propiedad que ha modificado, se podrá ver en el panel Detalles para el grupo seleccionado.

  - En el Shell, use el cmdlet **Get-DynamicDistributionGroup** para verificar los cambios. Una ventaja de usar el Shell es que puede ver varias propiedades para varios grupos. En el primer ejemplo, deberá ejecutar el comando siguiente para verificar los nuevos valores.
    
        Get-DynamicDistributionGroup -ResultSize unlimited | fl Name,HiddenFromAddressListsEnabled,MaxReceiveSize,ModerationEnabled,ModeratedBy
    
    Ejecute este comando para el ejemplo anterior donde se modificaron los límites del mensaje.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

