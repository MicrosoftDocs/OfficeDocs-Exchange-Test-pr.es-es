---
title: 'Creación y administración de buzones de sala: Exchange 2013 Help'
TOCTitle: Creación y administración de buzones de sala
ms:assetid: f70752ad-fce0-4e14-8428-fc5ac63f6c54
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ215781(v=EXCHG.150)
ms:contentKeyID: 48268888
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creación y administración de buzones de sala

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-02-02_

Tiempo estimado para finalizar: 5 minutos.

Un buzón de sala es un buzón de recursos que está asignado a una ubicación física, como una sala de conferencias, un auditorio o una sala de aprendizaje. Una vez que el administrador crea los buzones de correo de recursos, los usuarios pueden reservar salas fácilmente, incluidos los buzones de correo de sala en convocatorias de reunión. Para obtener más detalles, eche un vistazo a [Destinatarios](recipients-exchange-2013-help.md).

Para obtener información sobre otro tipo de buzón de recursos, consulte [Administrar buzones de correo de equipamiento](manage-equipment-mailboxes-exchange-2013-help.md).

## ¿Qué desea hacer?

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).


> [!IMPORTANT]
> Si ejecuta Exchange&nbsp;2013 en un escenario híbrido, procure crear buzones de sala en la ubicación que corresponda. Cree localmente los buzones de sala de la organización local y los buzones de sala de Exchange&nbsp;Online, en la nube.




## Creación de un buzón de correo de sala

## Usar el Centro de administración de Exchange para crear un buzón de sala

1.  En el Centro de administración de Exchange, navegue a **Destinatarios** \> **Recursos**.

2.  Para crear un buzón de sala, haga clic en **Nuevo** ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") \> **Buzón de sala**.

3.  Use las opciones de la página para especificar la configuración del nuevo buzón de recursos.
    
      - **\* Nombre de sala**   Use este cuadro para escribir un nombre para el buzón de sala. Es el nombre que aparece en la lista de buzones de correo de recursos en el Centro de administración de Exchange y en la libreta de direcciones de su organización. Este nombre es necesario y no puede superar los 64 caracteres.
        

        > [!TIP]
        > Aunque hay otros campos que describen los detalles de la sala, por ejemplo, Ubicación y Capacidad, considere la posibilidad de resumir los detalles más importantes en el nombre de sala mediante una convención de nomenclatura coherente. ¿Por qué? De este modo, los usuarios pueden ver fácilmente los detalles cuando seleccionen la sala en la libreta de direcciones en la convocatoria de reunión.

    
      - **\* Dirección de correo electrónico**   Un buzón de sala tiene una dirección de correo electrónico para poder recibir solicitudes de reserva. La dirección de correo electrónico está formada por un alias en la parte izquierda del símbolo @, que debe ser exclusivo en el bosque, y un nombre de dominio a la derecha. La dirección de correo electrónico es obligatoria.
    
      - **Ubicación**, **Teléfono**, **Capacidad**   Puede usar estos campos para indicar los detalles acerca de la sala. No obstante, tal como se explicó anteriormente, puede incluir parte de esta información o toda ella en el nombre de la sala para que los usuarios puedan verla.

4.  Cuando haya terminado, haga clic en **Guardar** para crear el buzón de sala.

Una vez que haya creado el buzón de sala, puede editarlo para actualizar información sobre opciones de reserva, sugerencias de correo electrónico y delegación de buzones. Consulte la sección Usar el Centro de administración de Exchange más abajo para cambiar las propiedades de los buzones de sala

## Usar Exchange PowerShell para crear un buzón de sala

En este ejemplo se crea un buzón de sala con la configuración siguiente:

  - El buzón de sala reside en Mailbox Database 1.

  - El nombre del buzón de correo es ConfRoom1. Este nombre también se usará para crear la dirección de correo electrónico de la sala.

  - El nombre para mostrar en el Centro de administración de Exchange y la libreta de direcciones será Sala de conferencias 1.

  - El modificador *Room* especifica que este buzón se creará como un buzón de sala.

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name ConfRoom1 - -DisplayName "Conference Room 1" -Room

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-Mailbox](https://technet.microsoft.com/es-es/library/aa997663\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Puede asegurarse de que ha creado el buzón de sala correctamente de dos maneras distintas:

  - En el Centro de administración de Exchange, navegue a **Destinatarios** \> **Recursos**. El nuevo buzón de sala aparece en la lista de buzones de correo. En **Tipo de buzón**, el tipo es **Sala**.

  - En Exchange PowerShell, ejecute el siguiente comando para mostrar información sobre el nuevo buzón de sala.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Crear una lista de salas

Si quiere tener más de cien salas o ya creó más de cien, use una lista de salas para que sea más fácil organizarlas. Si su compañía dispone de varios edificios con salas que se pueden reservar para reuniones, le resultará útil crear listas de salas para cada edificio. Las listas de salas son grupos de distribución con una marca especial que puede usar de la misma forma que usa los grupos de distribución. Pero solo puede crear listas de salas con el Shell de administración de Exchange.

## Usar Exchange PowerShell para crear una lista de sala

En este ejemplo crearemos una lista de salas para el edificio 32.

    New-DistributionGroup -Name "Building 32 Conference Rooms" -OrganizationalUnit "contoso.com/rooms" -RoomList

## Usar Exchange PowerShell para agregar una sala a una lista de salas

En este ejemplo agregaremos confroom3223 a la lista de salas del edificio 32.

    Add-DistributionGroupMember -Identity "Building 32 Conference Rooms" -Member confroom3223@contoso.com

## Usar Exchange PowerShell para convertir un grupo de distribución en una lista de salas

Puede que, en el pasado, creara grupos de distribución que contuvieran las salas de conferencias. No tiene que volver a crearlos, sino que los convertiremos rápidamente en una lista de salas.

En este ejemplo convertiremos el grupo de distribución de salas de conferencias del edificio 34 en una lista de salas.

    Set-DistributionGroup -Identity "Building 34 Conference Rooms" -RoomList

## Cambiar las propiedades del buzón de sala

Después de crear un buzón de sala, puede efectuar cambios y establecer propiedades adicionales mediante el Centro de administración de Exchange o Exchange PowerShell.

## Usar el Centro de administración de Exchange para cambiar las propiedades de buzón de sala

1.  En el Centro de administración de Exchange, navegue a **Destinatarios** \> **Recursos**.

2.  En la lista de buzones de recursos, haga clic en el buzón de sala cuyas propiedades desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del buzón de sala, haga clic en una de las siguientes secciones para ver o cambiar las propiedades.
    
      - General
    
      - Delegados
    
      - Opciones de reserva
    
      - Información de contacto
    
      - Dirección de correo electrónico
    
      - Información sobre correo

## General

Use la sección **General** para ver o cambiar información básica del recurso.

  - **\* Nombre de sala**   Este nombre aparece en la lista de buzones de recursos en el Centro de administración de Exchange y en la libreta de direcciones de su organización. Si lo cambia, no puede superar los 64 caracteres.

  - **\* Nombre de correo electrónico**   Este cuadro de solo lectura muestra la dirección de correo electrónico para el buzón de sala. Puede cambiarla en la sección Dirección de correo electrónico.

  - **Capacidad**   Use este cuadro para escribir el número máxima de personas que pueden ocupar a sala de forma segura.

Haga clic en **Más opciones** para ver o cambiar estas propiedades adicionales:

  - **Unidad organizativa**   Este cuadro de solo lectura muestra la unidad organizativa (UO) que contiene la cuenta para el buzón de sala. Debe usar usuarios de Active Directory y equipos para mover la cuenta a otra unidad organizativa.

  - **Base de datos de buzones de correo**   Este cuadro de solo lectura muestra el nombre de la base de datos de buzones de correo que hospeda el buzón de sala. Use la página **Migración** en el Centro de administración de Exchange para mover el buzón de correo a otra base de datos.

  - **\* Alias** Use este cuadro para cambiar el alias para el buzón de sala.

  - **Ocultar de las listas de direcciones**   Active esta casilla para evitar que el buzón de sala aparezca en la libreta de direcciones y otras listas de direcciones definidas en su organización de Exchange. Después de activar esta casilla, los usuarios aún podrán enviar mensajes de reserva al buzón de sala mediante la dirección de correo electrónico.

  - **Departamento**   Use este cuadro para especificar un nombre de departamento con el cual está asociada la sala. Puede usar esta propiedad para crear condiciones de destinatarios para grupos de distribución dinámicos y listas de direcciones.

  - **Compañía**   Use este cuadro para especificar un nombre de compañía con la cual está asociada la sala. Como en el caso de la propiedad "Departamento", puede usar esta propiedad para crear condiciones de destinatarios para grupos de distribución dinámicos y listas de direcciones.

  - **Directiva de la libreta de direcciones**   Use esta opción para especificar una directiva de libreta de direcciones (ABP) para el buzón de sala. Las ABP contienen una lista global de direcciones (GAL), una libreta de direcciones sin conexión (OAB), una lista de salas y un conjunto de listas de direcciones. Para obtener más información, consulte [Directivas de la libreta de direcciones](address-book-policies-exchange-2013-help.md).
    
    En la lista desplegable, seleccione la directiva que desea asociar con este buzón.

  - **Atributos personalizados**   Este sección muestra los atributos personalizados definidos para el buzón de sala. Para especificar valores de atributos personalizados, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Se pueden especificar hasta 15 atributos personalizados para el destinatario.

## Delegados

Use esta sección para ver o cambiar cómo el buzón de sala administra las solicitudes de reserva y para definir quién puede aceptar o rechazar las solicitudes de reserva si esto no se realiza automáticamente.

  - **Solicitudes de reserva**   Seleccione una de las siguientes opciones para administrar las solicitudes de reserva.
    
      - **Aceptar o rechazar las solicitudes de reserva automáticamente**   Una solicitud de reunión válida reserva automáticamente la sala. Si hay un conflicto de programación con una reserva existente, o si la solicitud de reserva infringe los límites de programación del recurso, por ejemplo, la duración de la reserva es demasiado larga, se deniega automáticamente la convocatoria de reunión.
    
      - **Seleccionar delegados que pueden aceptar o rechazar solicitudes de oferta**   Los delegados de recursos son los responsables de aceptar o rechazar las solicitudes de reunión que se envían al buzón de sala. Si asigna a más de un delegado de recursos, solo uno de ellos debe actuar en una convocatoria de reunión específica.

  - **Delegados**   Si seleccionó la opción que requiere que las solicitudes de reserva se envíen a los delegados, se enumerarán los delegados especificados. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") o **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") para agregar o quitar delegados de esta lista.

## Opciones de reserva

Use la sección **Opciones de reserva** para ver o cambiar la configuración de la directiva de reserva que define cuándo se puede programar la sala, por cuánto tiempo se puede reservar y con cuánta anticipación.

  - **Permitir repetición de reuniones**   Esta configuración permite o evita la repetición de reuniones para la sala. De forma predeterminada, esta configuración está habilitada, por lo que se permiten las reuniones de repetición.

  - **Permitir programación sólo durante el horario laboral**   Esta configuración acepta o rechaza las solicitudes de reuniones que no se realizan durante el horario laboral definido para la sala. De manera predeterminada, esta opción está deshabilitada, así que las solicitudes de reunión se permiten fuera del horario laboral. De manera predeterminada, el horario laboral es de 8:00 A.M. a 5:00 P.M. del lunes a viernes. Puede configurar el horario laboral del buzón de sala en la sección Apariencia de la página Calendario.

  - **Rechazar siempre si la fecha de finalización sobrepasa este límite**   Esta configuración controla el comportamiento de las reuniones que se repiten que se extienden más allá de la fecha especificada por la opción de tiempo máximo de espera para reserva.
    
      - Si habilita esta opción, una solicitud de reserva que se repite se rechaza automáticamente si la reserva empieza en la fecha especificada o después de la fecha especificada por el valor del cuadro **Tiempo máximo de espera para reserva** y se extiende más allá de la fecha especifica. Esta es la configuración predeterminada.
    
      - Si deshabilita esta opción, una solicitud de reserva que se repite se acepta automáticamente si las solicitudes de reserva empiezan en la fecha especificada o después de la fecha especificada por el valor del cuadro **Tiempo máximo de espera para reserva** y se extiende más allá de la fecha especifica. Sin embargo, la cantidad de reservas se reduce, de manera que no sucedan después de la fecha especificada.

  - **Tiempo máximo de espera para reserva (días)**   Esta configuración especifica el número máximo de días anticipados con los que se puede reservar la sala. Una entrada válida es un entero entre el 0 y el 1.080. El valor predeterminado es 180 días.

  - **Duración máxima (horas)**   Esta configuración especifica la duración máxima con la que se puede reservar la sala en una solicitud de reserva. El valor predeterminado es 24 horas.
    
    Para las solicitudes de reserva de repetición, la duración máxima de reserva se aplica a la duración de cada instancia del Centro de administración de Exchange de solicitud de reserva que se repite.

En esta página, también hay un cuadro que se puede usar para escribir un mensaje que se enviará a los usuarios que realizan solicitudes de reserva de la sala.

## Información de contacto

Use la sección **Información de contacto** para ver o cambiar la información de contacto para la sala. La información de esta página se muestra en la libreta de direcciones.


> [!TIP]
> Puede usar el cuadro <STRONG>Estado/provincia</STRONG> para crear condiciones de destinatario para grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones.



## Dirección de correo electrónico

Use la sección **Dirección de correo electrónico** para ver o cambiar las direcciones de correo electrónico asociadas con el buzón de sala. Esto incluye la dirección SMTP principal del buzón de correo y las direcciones proxy asociadas. Las direcciones SMTP principales (también conocidas como *dirección de respuesta*) se muestran en negrita en la lista de direcciones, con el valor **SMTP** en mayúscula en la columna **Tipo**.

  - **Agregar **   Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una nueva dirección de correo electrónico para este buzón de correo. Seleccione uno de los siguientes tipos de dirección:
    
      - **SMTP**   Este es el tipo de dirección predeterminado. Haga clic en este botón y, a continuación, escriba la nueva dirección SMTP en el cuadro **\* Dirección de correo electrónico**.
    
      - **EUM**   El servicio de mensajería unificada de Microsoft Exchange usa una dirección EUM (mensajería unificada de Exchange) para ubicar destinatarios habilitados para mensajería unificada dentro de una organización de Exchange. Las direcciones EUM constan del número de extensión y el plan de marcado de MU para el usuario habilitado para MU. Haga clic en este botón y escriba el número de extensión en el cuadro **Dirección/extensión**. A continuación, haga clic en **Examinar** y seleccione un plan de marcado para el buzón de correo.
    
      - **Tipo de dirección personalizada**   Haga clic en este botón y escriba uno de los tipos de dirección de correo electrónico que no sean SMTP admitidos en el cuadro **\* Dirección de correo**.
        

        > [!NOTE]
        > Con excepción de las direcciones X.400, Exchange no valida las direcciones personalizadas para comprobar el formato correcto. Debe asegurarse de que la dirección personalizada que especifica cumpla los requisitos de formato para el tipo de dirección.

    

    > [!NOTE]
    > Cuando agrega una dirección de correo electrónico nueva, tiene la opción de convertirla en dirección SMTP principal.



  - **Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada al destinatario.**   Seleccione esta casilla para que las direcciones de correo electrónico del destinatario se actualicen automáticamente según los cambios realizados en las directivas de direcciones de correo electrónico de su organización.

## Información sobre correo

Use la sección **Sugerencia de correo** para agregar una sugerencia de correo e informar a los usuarios sobre posibles problemas antes de que envíen una solicitud de reserva al buzón de sala. La información sobre correo es texto que se muestra en la barra de información cuando este destinatario se agrega a los campos Para, CC o CCO de un nuevo mensaje de correo electrónico.


> [!NOTE]
> La información sobre correo puede incluir etiquetas HTML, pero no se permiten los scripts. La longitud de la información de una sugerencia de correo electrónico personalizada no puede superar los 175 caracteres mostrados. Las etiquetas HTML no se cuentan en el límite.



## Uso de Exchange PowerShell para cambiar las propiedades del buzón de sala

Use los siguientes conjuntos de cmdlets para ver y cambiar las propiedades del buzón de sala: cmdlets **Get-Mailbox** y **Set-Mailbox** para ver y cambiar las propiedades generales y las direcciones de correo electrónico para los buzones de sala. Use los cmdlets **Get-CalendarProcessing** y **Set-CalendarProcessing** para ver y cambiar los delegados y las opciones de reserva.

  - **Get-User** y **Set-User**   Use estos cmdlets para ver y configurar propiedades generales, como ubicación, departamento y nombres de compañías.

  - **Get-Mailbox** y **Set-Mailbox**   Use estos cmdlets para ver y configurar propiedades de buzones de correo, como direcciones de correo electrónico y base de datos de buzones de correo.

  - **Get-CalendarProcessing** y **Set-CalendarProcessing**   Use estos cmdlets para ver y configurar opciones de reserva y delegados.

Para obtener más información acerca de estos cmdlets, consulte los siguientes temas:

  - [Get-User](https://technet.microsoft.com/es-es/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/es-es/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/es-es/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/es-es/library/dd335046\(v=exchg.150\))

A continuación, se presentan algunos ejemplos de cómo usar Exchange PowerShell para cambiar las propiedades del buzón de sala.

En este ejemplo, se cambia el nombre de visualización, la dirección SMTP principal (denominada dirección de respuesta predeterminada) y la capacidad de la sala. Además, la dirección de respuesta anterior se mantiene como una dirección proxy.

    Set-Mailbox "Conf Room 123" -DisplayName "Conf Room 31/123 (12)" -EmailAddresses SMTP:Rm33.123@contoso.com,smtp:rm123@contoso.com -ResourceCapacity 12

En este ejemplo, se configuran buzones de sala para permitir que las solicitudes de reserva se programen únicamente durante el horario laboral y se configura una duración máxima de 9 horas.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true -MaximumDurationInMinutes 540

En este ejemplo, se usa el cmdlet **Get-User** para buscar todos los buzones de sala que corresponden a salas de conferencia privadas y, a continuación, se usa el cmdlet **Set-CalendarProcessing** para enviar solicitudes de reserva a un delegado denominado Robin Wood para su aceptación o rechazo.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox') -and (DisplayName -like 'Private*')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Robin Wood"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que las propiedades de un buzón de sala se cambiaron correctamente, realice lo siguiente:

  - En el Centro de administración de Exchange, seleccione el buzón y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para visualizar la propiedad o característica que ha modificado. Según la propiedad que cambie, puede aparecer en el panel Detalles del buzón seleccionado.

  - En Exchange PowerShell, use el cmdlet **Get-Mailbox** para verificar los cambios. Una ventaja de usar Exchange PowerShell es que puede consultar varias propiedades de varios buzones. En el ejemplo anterior donde las solicitudes de reserva se podían programar únicamente durante el horario laboral y con una duración máxima de 9 horas, ejecute el siguiente comando para comprobar los nuevos valores.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours,MaximumDurationInMinutes

Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..


