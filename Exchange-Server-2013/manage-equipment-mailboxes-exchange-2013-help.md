---
title: 'Administrar buzones de correo de equipamiento: Exchange 2013 Help'
TOCTitle: Administrar buzones de correo de equipamiento
ms:assetid: e5f58b3a-83e1-4742-8846-85103a44ee18
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ215770(v=EXCHG.150)
ms:contentKeyID: 48268807
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar buzones de correo de equipamiento

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-10-09_

Un *buzón de equipamiento* es un buzón de recursos asignado a un recurso sin una ubización específica, por ejemplo, un equipo portátil, un proyector, un micrófono o un automóvil de la empresa. Después de que un administrador crea un buzón de correo de equipamiento, los usuarios pueden reservar fácilmente el equipamiento al incluir el correspondiente buzón de correo de equipamiento en una solicitud de reunión. Puede usar el EAC y el Shell para crear un buzón de correo de equipamiento o cambiar las propiedades de buzón de correo de equipamiento. Para obtener más información, consulte [Destinatarios](recipients-exchange-2013-help.md).

Para obtener información sobre otro tipo de buzón de recursos, el buzón de sala, consulte [Creación y administración de buzones de sala](create-and-manage-room-mailboxes-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 a 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Crear en buzón de correo de equipamiento

## Usar el EAC para crear un buzón de correo de equipamiento

1.  En el EAC, vaya a **Destinatarios** \> **Recursos**.

2.  Para crear un buzón de correo de equipamiento, haga clic en **Nuevo** \> **Buzón de equipamiento**. Para crear un buzón de sala, haga clic en **Nuevo** \> **Buzón de sala**.

3.  Use las opciones de la página para especificar la configuración del nuevo buzón de recursos.
    
      - **Nombre de equipamiento \***   Use este cuadro para escribir un nombre para el buzón de correo de equipamiento. Es el nombre que aparece en la lista de buzones de correo de recursos en el EAC y en la libreta de direcciones de su organización. Este nombre es necesario y no puede superar los 64 caracteres.
        

        > [!TIP]
        > Aunque hay otros campos que describen los detalles de la sala, por ejemplo, Capacidad, considere la posibilidad de resumir los detalles más importantes en el nombre del equipamiento mediante una convención de nomenclatura coherente. ¿Por qué? De este modo, los usuarios pueden ver fácilmente los detalles cuando seleccionen el equipamiento en la libreta de direcciones en la solicitud de reunión.

    
      - **Dirección de correo electrónico \***   Un buzón de correo de equipamiento tiene una dirección de correo electrónico, de modo que puede recibir solicitudes de reserva. La dirección de correo electrónico está formada por un alias en la parte izquierda del símbolo @, que debe ser exclusivo en el bosque, y un nombre de dominio a la derecha. La dirección de correo electrónico es obligatoria.

4.  Cuando haya terminado, haga clic en **Guardar** para crear el nuevo buzón de correo de equipamiento.

Una vez que haya creado el buzón de equipamiento, puede editarlo para actualizar información sobre opciones de reserva, sugerencias de correo electrónico y delegados. Consulte la sección Cambiar propiedades del buzón de correo de equipamiento a continuación para cambiar las propiedades del buzón de sala.

## Usar el Shell para crear un buzón de equipamiento

En este ejemplo se crea un buzón de equipamiento con la siguiente configuración:

  - El buzón de equipamiento reside en Mailbox Database 1.

  - El nombre del equipamiento es MotorVehicle2, y el nombre se mostrará en la LGD como vehículo de motor 2.

  - La dirección de correo electrónico es MotorVehicle2@contoso.com.

  - El buzón está en la unidad organizativa de equipamiento.

  - El parámetro *Equipment* especifica que este buzón de correo se creará como un buzón de correo de equipamiento.

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name MotorVehicle2 -OrganizationalUnit Equipment -DisplayName "Motor Vehicle 2" -Equipment

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-Mailbox](https://technet.microsoft.com/es-es/library/aa997663\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó un buzón de usuario correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Recursos**. El buzón de nuevo usuario aparece en la lista de buzones. En **Tipo de buzón de correo**, el tipo es **Equipamiento**.

  - En el Shell, ejecute el siguiente comando para mostrar información acerca del nuevo buzón de correo de equipamiento.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Cambiar las propiedades del buzón de correo de equipamiento

Después de crear un buzón de correo de equipamiento, puede hacer cambios y configurar propiedades adicionales mediante el EAC o el Shell.

## Usar el EAC para cambiar las propiedades de los buzones de correo de equipamiento

1.  En el EAC, vaya a **Destinatarios** \> **Recursos**.

2.  En la lista de buzones de correo de recursos, haga clic en el buzón de correo de equipamiento para el que desea cambiar las propiedades y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del buzón de correo de equipamiento, haga clic en las siguientes secciones para ver o cambiar las propiedades.
    
      - General
    
      - Delegados
    
      - Opciones de reserva
    
      - Información de contacto
    
      - Dirección de correo electrónico
    
      - Información sobre correo

## General

Use la sección **General** para ver o cambiar la información básica del recurso.

  - **Nombre de equipamiento \***   Es el nombre que aparece en la lista de buzones de correo de recursos en el EAC y en la libreta de direcciones de su organización. Si lo cambia, no puede superar los 64 caracteres.

  - **Dirección de correo electrónico \***   Este cuadro de solo lectura muestra la dirección de correo electrónico para el buzón de correo de equipamiento. Puede cambiarlo en la sección Dirección de correo electrónico.

  - **Capacidad**   Use este cuadro para escribir la cantidad máxima de personas que pueden usar este recurso, si corresponde. Por ejemplo, si el buzón de correo de equipamiento corresponde a un automóvil compacto, puede escribir **4**.

Haga clic en **Más opciones** para ver o cambiar estas propiedades adicionales:

  - **Unidad organizativa**   Este cuadro de solo lectura muestra la unidad organizativa (OU) que contiene la cuenta del buzón de correo de equipamiento. Debe usar usuarios de Active Directory y equipos para mover la cuenta a otra unidad organizativa.

  - **Base de datos de buzones de correo**   Este cuadro de solo lectura muestra el nombre de la base de datos de buzones de correo que hospeda el buzón de correo de equipamiento. Use la página **Migración** en el EAC para mover el buzón de correo a otra base de datos.

  - **Alias \*** Use este cuadro para cambiar el alias para el buzón de correo de equipamiento.

  - **Ocultar otras listas de direcciones**   Seleccione esta casilla para evitar que el buzón de correo de equipamiento aparezca en la lista de direcciones y en otras listas de direcciones definidas en su organización de Exchange. Cuando active esta casilla, los usuarios aún podrán enviar mensajes de reserva al buzón de correo de equipamiento mediante la dirección de correo electrónico.

  - **Departamento**   Use esta casilla para especificar un nombre de departamento con el que se asocia al recurso. Puede usar esta propiedad para crear condiciones de destinatarios para grupos de distribución dinámicos y listas de direcciones.

  - **Compañía**   Use esta casilla para especificar una compañía con la que se asocia al recurso. Como en el caso de la propiedad "Departamento", puede usar esta propiedad para crear condiciones de destinatarios para grupos de distribución dinámicos y listas de direcciones.

  - **Directiva de la libreta de direcciones**   Use esta opción para especificar una directiva de libreta de direcciones (ABP) para el recurso. Las ABP contienen una lista global de direcciones (GAL), una libreta de direcciones sin conexión (OAB), una lista de salas y un conjunto de listas de direcciones. Para obtener más información, consulte [Directivas de la libreta de direcciones](address-book-policies-exchange-2013-help.md).
    
    En la lista desplegable, seleccione la directiva que desea asociar con este buzón.

  - **Atributos personalizados**   Esta sección muestra los atributos personalizados definidos para el buzón de correo de equipamiento. Para especificar valores de atributo personalizados, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Se pueden especificar hasta 15 atributos personalizados para el destinatario.

## Delegados

Use esta sección para ver o cambiar cómo el buzón de correo de equipamiento maneja las solicitudes de reserva y para definir quién puede aceptar o rechazar solicitudes de reserva si no se realiza de manera automática.

  - **Solicitudes de reserva**   Seleccione una de las siguientes opciones para manejar las solicitudes de reserva.
    
      - **Aceptar o rechazar solicitudes de reserva automáticamente**   Una solicitud de reunión válida reserva automáticamente el recurso. Si hay un conflicto de programación con una reserva existente, o si la solicitud de reserva infringe los límites de programación del recurso, por ejemplo, la duración de la reserva es demasiado larga, se deniega automáticamente la convocatoria de reunión.
    
      - **Seleccionar delegados que pueden aceptar o rechazar solicitudes de reserva**   Los delegados de recurso son responsables de aceptar o rechazar las solicitudes de reunión que se envían al buzón de correo de equipamiento. Si asigna a más de un delegado de recursos, solo uno de ellos debe actuar en una convocatoria de reunión específica.

  - **Delegados**   Si seleccionó la opción que requiere que las solicitudes de reserva se envíen a los delegados, se indican los delegados seleccionados. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") o en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") para agregar delegados a la lista o para quitarlos.

## Opciones de reserva

Use la sección **Opciones de reserva** para ver o cambiar la configuración de la directiva de reserva que define cuándo se puede programar el recurso, cuánto tiempo se puede reservar y con qué anticipación se puede reservar.

  - **Permitir reuniones que se repiten**   Esta configuración permite o evita la repetición de reuniones para el recurso. De forma predeterminada, esta configuración está habilitada, por lo que se permiten las reuniones de repetición.

  - **Permitir la programación solo durante las horas laborables**   Esta configuración acepta o rechaza las solicitudes de reunión que no están programadas durante las horas laborables definidas para el recurso. De manera predeterminada, esta opción está deshabilitada, así que las solicitudes de reunión se permiten fuera del horario laboral. De manera predeterminada, el horario laboral es de 8:00 A.M. a 5:00 P.M. del lunes a viernes. Puede configurar las horas laborables del buzón de correo de equipamiento en la sección Apariencia en la página Calendario.

  - **Rechazar siempre si la fecha de finalización sobrepasa este límite**   Esta opción controla el comportamiento de las reuniones que se repiten que van más allá de la fecha especificada por la opción de tiempo de reserva máximo.
    
      - Si habilita esta opción, una solicitud de reserva que se repite se rechaza automáticamente si la reserva empieza en la fecha o después de la fecha especificada por el valor en el cuadro **Plazo de reserva máximo**, y se amplía más allá de la fecha específica. Esta es la configuración predeterminada.
    
      - Si deshabilita esta opción, una solicitud de reserva que se repite se acepta automáticamente si las solicitudes de reserva empiezan en la fecha o después de la fecha especificada por el valor en el cuadro **Plazo de reserva máximo**, y se amplía más allá de la fecha específica. Sin embargo, la cantidad de reservas se reduce, de manera que no sucedan después de la fecha especificada.

  - **Plazo de reserva máximo (días)**   Esta configuración especifica la cantidad máxima de días de anticipación con que se puede reservar el recurso. Una entrada válida es un entero entre el 0 y el 1.080. El valor predeterminado es 180 días.

  - **Duración máxima (horas)**   Esta configuración especifica la duración máxima que se puede reservar el recurso en una solicitud de reserva. El valor predeterminado es 24 horas.
    
    Para las solicitudes de reserva de repetición, la duración máxima de reserva se aplica a la duración de cada instancia de solicitud de reserva que se repite.

En esta página también hay un cuadro que puede usar para escribir un mensaje que se enviará a los usuarios que envían solicitudes de reunión para reservar el recurso.

## Información de contacto

Use la sección **Información de contacto** para ver o cambiar la información de contacto para el recurso. La información de esta página se muestra en la libreta de direcciones.


> [!TIP]
> Puede usar el cuadro <STRONG>Estado o provincia</STRONG> para crear condiciones de destinatario para grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones.



## Dirección de correo electrónico

Use la sección **Dirección de correo electrónico** para ver o cambiar las direcciones de correo electrónico asociadas con el buzón de correo de equipamiento. Esto incluye la dirección SMTP principal del buzón de correo y las direcciones proxy asociadas. La dirección SMTP principal (también conocida como la *dirección de respuesta*) se muestra en texto en negrita en la lista de direcciones, con el valor **SMTP** en mayúsculas en la columna **Tipo**.

  - **Agregar **   Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una dirección de correo electrónico nueva para este buzón. Seleccione uno de los siguientes tipos de dirección:
    
      - **SMTP**   Este es el tipo de dirección predeterminado. Haga clic en este botón y, luego, escriba la nueva dirección SMTP en el cuadro **Dirección de correo electrónico \***.
    
      - **EUM**   Una dirección EUM (mensajería unificada de Exchange) la usa el servicio de mensajería unificada de Microsoft Exchange para ubicar usuarios con mensajería unificada habilitada en una organización de Exchange. Las direcciones EUM constan del número de extensión y el plan de marcado de MU para el usuario habilitado para MU. Haga clic en este botón y escriba el número de extensión en el cuadro **Dirección/extensión**. A continuación, haga clic en **Examinar** y seleccione un plan de marcado para el buzón.
    
      - **Tipo de dirección personalizado**   Haga clic en este botón y escriba uno de los tipos admitidos de dirección de correo electrónico no SMTP en el cuadro **Dirección de correo electrónico \***.
        

        > [!NOTE]
        > Con excepción de las direcciones X.400, Exchange no valida las direcciones personalizadas para comprobar el formato correcto. Debe asegurarse de que la dirección personalizada que especifica cumpla los requisitos de formato para el tipo de dirección.

    

    > [!NOTE]
    > Cuando agrega una dirección de correo electrónico nueva, tiene la opción de convertirla en dirección SMTP principal.



  - **Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada a este destinatario**   Seleccione esta casilla para que las direcciones de correo electrónico del destinatario se actualicen automáticamente según los cambios realizados en las directivas de direcciones de correo electrónico de su organización.

## Información sobre correo

Use la sección **Información sobre correo** para agregar información sobre correo para alertar a los usuarios de potenciales problemas antes de enviar una solicitud de reserva al buzón de correo de equipamiento. La información sobre correo es texto que se muestra en la barra de información cuando este destinatario se agrega a los campos Para, CC o CCO de un nuevo mensaje de correo electrónico.


> [!NOTE]
> La información sobre correo puede incluir etiquetas HTML, pero no se permiten los scripts. La longitud de la información de una sugerencia de correo electrónico personalizada no puede superar los 175 caracteres mostrados. Las etiquetas HTML no se cuentan en el límite.



## Usar el Shell para cambiar las propiedades de los buzones de correo de equipamiento

Use los siguientes conjuntos de cmdlets para ver y cambiar propiedades de buzones de correo de equipamiento: cmdlets **Get-Mailbox** y **Set-Mailbox** para ver y cambiar propiedades generales y direcciones de correo electrónico para buzones de correo de equipamiento. Use los cmdlets **Get-CalendarProcessing** y **Set-CalendarProcessing** para ver y cambiar delegados y opciones de reserva.

  - **Get-User** y **Set-User**   Use estos cmdlets para ver y configurar propiedades generales, como nombres de departamento y de compañías.

  - **Get-Mailbox** y **Set-Mailbox**   Use estos cmdlets para ver y configurar propiedades de buzón de correo, como direcciones de correo electrónico y la base de datos de buzones de correo.

  - **Get-CalendarProcessing** y **Set-CalendarProcessing**   Use estos cmdlets para ver y configurar opciones de reserva y delegados.

Para obtener más información acerca de estos cmdlets, consulte los siguientes temas:

  - [Get-User](https://technet.microsoft.com/es-es/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/es-es/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/es-es/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/es-es/library/dd335046\(v=exchg.150\))

Estos son algunos ejemplos de uso del Shell para cambiar propiedades de buzones de correo de equipamiento.

En este ejemplo, se cambia el nombre que se muestra y la dirección SMTP principal (denominada dirección de respuesta predeterminada) para el buzón de correo de equipamiento MotorPool 1. La dirección de respuesta anterior se mantiene como una dirección de proxy.

    Set-Mailbox "MotorPool 1" -DisplayName "Motor Pool 1 - Compact" -EmailAddresses SMTP:MP1.compact@contoso.com,smtp:MP.1@contoso.com

En este ejemplo, se configuran buzones de correo de equipamiento para permitir la programación de solicitudes de reserva solo durante las horas laborables.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true

En este ejemplo, se usa el cmdlet **Get-User** para encontrar todos los buzones de correo de equipamiento en el departamento audiovisual y, luego, usa el cmdlet **Set-CalendarProcessing** para enviar solicitudes de reserva a un delegado llamado Ann Beebe para su aceptación o rechazo.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox') -and (Department -eq 'Audio Visual')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Ann Beebe"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que cambió correctamente las propiedades de un buzón de correo de equipamiento, haga lo siguiente:

  - En el EAC, seleccione el buzón de correo y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para ver la propiedad o característica que cambió. Según la propiedad que cambie, puede aparecer en el panel Detalles del buzón seleccionado.

  - En el Shell, use el cmdlet **Get-Mailbox** para comprobar los cambios. Una de las ventajas de usar el Shell es que puede ver diferentes propiedades para varios buzones. En el ejemplo anterior donde se pueden programar solicitudes de reserva solo durante horas laborables, ejecute el siguiente comando para comprobar el nuevo valor.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours

