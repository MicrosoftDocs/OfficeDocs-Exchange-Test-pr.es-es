---
title: 'Administrar los buzones de usuario: Exchange 2013 Help'
TOCTitle: Administrar los buzones de usuario
ms:assetid: 957ca61c-1fa1-42ab-a0e6-8488e4782566
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123809(v=EXCHG.150)
ms:contentKeyID: 48268454
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailboxWizardForm.NewMailboxIntroductionWizardPage
ms.translationtype: HT
---

# Administrar los buzones de usuario

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-05-27_

Después de haber creado un buzón de correo de usuario, puede hacer cambios y configurar propiedades adicionales mediante el uso del EAC o del Shell.

También puede cambiar las propiedades de varios buzones de usuario al mismo tiempo. Para obtener más información, consulte Editar en masa buzones de usuario.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada tarea de buzón de usuario: 2 a 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Cambiar las propiedades del buzón de usuario

## Uso de la Consola de administración de Exchange para cambiar las propiedades de los buzones de usuario

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En la lista de buzones de usuario, haga clic en el buzón cuyas propiedades desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del buzón, haga clic en las siguientes secciones para ver o cambiar las propiedades.
    
      - General
    
      - Uso del buzón de correo
    
      - Información de contacto
    
      - Organización
    
      - Dirección de correo electrónico
    
      - Características de buzón
    
      - Miembro de
    
      - Información sobre correo
    
      - Delegación de buzones

## General

Utilice la sección **General** para ver o cambiar la información básica sobre el usuario.

  - **Nombre**, **Inicial**, **Apellidos**

  - **\* Nombre** Se trata del nombre indicado en Active Directory. Si cambia este nombre, no debe superar los 64 caracteres.

  - **\* Nombre para mostrar** Este nombre aparece en la libreta de direcciones de la organización, en las líneas Para: y De: del correo electrónico y en la lista Buzón. Este nombre no puede contener espacios en blanco antes o después del nombre para mostrar.

  - **\* Alias** Especifica el alias de correo electrónico del usuario. El alias del usuario es la porción de la dirección de correo electrónico ubicada a la izquierda del símbolo arroba (@). Debe ser exclusivo en el bosque.

  - **\* Nombre de inicio de sesión del usuario**   Este es el nombre que utiliza el usuario para iniciar sesión en su buzón y en el dominio. Normalmente, el nombre de inicio de sesión del usuario es el alias del mismo que aparece en la parte izquierda del símbolo @, mientras que el nombre de domino de la cuenta de usuario es el de la parte derecha del símbolo @.
    

    > [!NOTE]
    > Este cuadro tiene la etiqueta <STRONG>Id. de usuario</STRONG> en Exchange Online.



  - **Requerir cambio de contraseña en el próximo inicio de sesión**   Seleccione esta casilla de verificación si desea que el usuario restablezca la contraseña la próxima vez que inicie sesión en el buzón.
    

    > [!NOTE]
    > Esta casilla no está disponible en Exchange Online.



  - **Ocultar de las listas de direcciones** Seleccione esta casilla para impedir que el destinatario aparezca en la lista de direcciones y otras listas definidas en la organización de Exchange. Cuando active esta casilla, los usuarios aún podrán enviar mensajes al destinatario mediante la dirección de correo electrónico.

Haga clic en **Más opciones** para ver o cambiar estas propiedades adicionales:

  - **Unidad organizativa** Este cuadro de solo lectura muestra la unidad organizativa (OU) que contiene la cuenta de usuario. Debe usar Usuarios y equipos de Active Directory para mover la cuenta de usuario a una OU diferente.
    

    > [!NOTE]
    > Este cuadro no está disponible en Exchange Online.



  - **Base de datos de buzones de correo**   Este cuadro de solo lectura muestra el nombre de la base de datos de buzón que hospeda el buzón. Para desplazar el buzón a una base de datos diferente, selecciónelo en la lista de buzones y, a continuación, haga clic en **Mover buzón a otra base de datos** en el panel Detalles.
    

    > [!NOTE]
    > Esta opción no está disponible en Exchange Online.



  - **Atributos personalizados**   Esta sección muestra los atributos personalizados que se han definido para el buzón de usuario. Para especificar valores de atributo personalizados, haga clic en **Editar**. Se pueden especificar hasta 15 atributos personalizados para el destinatario.

## Uso del buzón de correo

Utilice la sección **Uso del buzón** para ver o cambiar la cuota de almacenamiento del buzón y la configuración de retención de elementos eliminados del buzón. Estas opciones se configuran de forma predeterminada cuando se crea el buzón. Usan los valores configurados para la base de datos de buzón y se aplican a todos los buzones de esa base de datos. Puede personalizar esta configuración para cada buzón en vez de usar la configuración predeterminada de la base de datos del buzón.

  - **Última sesión iniciada**   En este cuadro de solo lectura se muestra la última vez que el usuario inició sesión en el buzón.

  - **Uso de buzón de correo**   Esta área muestra el tamaño total del buzón y el porcentaje de la cuota total del buzón que se usó.


> [!NOTE]
> Para obtener la información que se muestra los dos cuadros previos, EAC consulta la base de datos de buzón que hospeda el buzón. Si el EAC no puede comunicarse con el almacén de Exchange que contiene la base de datos de buzones, estos campos estará vacíos. Se muestra un mensaje de advertencia si el usuario no ha iniciado sesión en el buzón por primera vez.



Haga clic en **Más opciones** para ver o cambiar la cuota de almacenamiento del buzón y la configuración de retención de elementos eliminados del buzón.


> [!NOTE]
> Esta configuración no está disponible en el EAC en Exchange Online.



  - **Configuración de la cuota de almacenamiento**   Para personalizar esta configuración del buzón y no usar los valores predeterminados de la base de datos del mismo, haga clic en **Personalizar la configuración de este buzón**, escriba un valor nuevo y, finalmente, haga clic en **Guardar**.
    
    El intervalo de valor para la configuración de la cuota de almacenamiento oscila entre 0 y 2047 gigabytes (GB).
    
      - **Emitir una advertencia al llegar a (GB)**   Este cuadro muestra el límite máximo de almacenamiento antes de que se emita una advertencia al usuario. Si el tamaño del buzón alcanza o supera el valor especificado, Exchange envía un mensaje de advertencia al usuario.
    
      - **Prohibir envío al llegar a (GB)**   Este cuadro muestra el límite del buzón para *prohibir el envío*. Si el tamaño del buzón alcanza o supera el límite especificado, Exchange impide que el usuario envíe nuevos mensajes y muestra un mensaje de error descriptivo.
    
      - **Prohibir envío y recepción al llegar a (GB)**   Este cuadro muestra el límite del buzón para *prohibir el envío y recepción*. Si el tamaño del buzón alcanza o supera el límite especificado, Exchange impide que el usuario del buzón envíe mensajes nuevos y no entregará ningún mensaje nuevo en el buzón. Todos los mensajes que se envíen al buzón se devolverán al remitente con un mensaje de error descriptivo.

  - **Configuración de la retención de elementos eliminados**   Para personalizar esta configuración del buzón y no usar los valores predeterminados de la base de datos del mismo, haga clic en **Personalizar la configuración de este buzón**, escriba un valor nuevo y, finalmente, haga clic en **Guardar**.
    
      - **Guardar los elementos eliminados durante (días)**   Este cuadro muestra la cantidad de tiempo que se retienen los elementos eliminados antes de que se eliminen permanentemente y el usuario no pueda recuperarlos. Al crear el buzón, este valor se basa en los valores de retención de elementos eliminados configurados para la base de datos de buzones. De manera predeterminada, se configura una base de datos de buzón para que retenga los elementos eliminados por 14 días. El intervalo de valores para esta propiedad oscila entre 0 y 24855 días.
    
      - **No eliminar permanentemente los elementos hasta después de realizada la copia de seguridad de la base de datos**   Seleccione esta casilla de verificación para evitar que los buzones y los mensajes de correo electrónico se eliminen hasta que se haya realizado la copia de seguridad de la base de datos de buzones en la que está ubicado el buzón.

## Información de contacto

Use la sección **Información de contacto** para ver o cambiar la información de contacto del usuario. La información de esta página se muestra en la libreta de direcciones. Haga clic en **Más opciones** para mostrar cuadros adicionales.


> [!TIP]
> Puede usar el cuadro <STRONG>Estado/provincia</STRONG> para crear condiciones de destinatario para grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones.



Los usuarios de buzones de correo pueden usar Outlook u Outlook Web App para ver y cambiar su propia información de contacto. No obstante, no podrán cambiar la información en los cuadros **Notas** ni **Página web**.

## Organización

Use la sección **Organización** para registrar información detallada acerca de la función del usuario en la organización. Esta información se muestra en la libreta de direcciones. Asimismo, puede crear un gráfico de organización virtual al que se pueda obtener acceso desde clientes de correo electrónico como Outlook.

  - **Título   **Use este cuadro para ver o cambiar el título del destinatario.

  - **Departamento** Use este cuadro para ver o cambiar el departamento en el que trabaja el usuario. Puede usar este cuadro para crear condiciones de destinatario para grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones.

  - **Compañía** Use este cuadro para ver o cambiar la compañía en la que trabaja el usuario. Puede usar este cuadro para crear condiciones de destinatario para grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones.

  - **Administrador**   Para agregar un administrador, haga clic en **Examinar**. En **Seleccionar administrador**, seleccione la persona y, a continuación, haga clic en **Aceptar**.

  - **Subordinados directos**   Este campo no se puede modificar. Un *subordinado directo* es un usuario que está bajo las órdenes de un administrador específico. En caso de que haya indicado un administrador para el usuario, ese buzón de correo se mostrará como subordinado directo en la información del buzón de correo del administrador en cuestión. Por ejemplo, Kari administra a Chris y a Kate, de modo que el buzón de Kari está especificado en el cuadro **Administrador** de los buzones de Chris y Kate; asimismo, Chris y Kate aparecen en el cuadro **Subordinados directos** en las propiedades del buzón de Kari.

## Dirección de correo electrónico

Use la sección **Dirección de correo electrónico** para ver o cambiar las direcciones de correo electrónico asociadas al buzón del usuario. Esto incluye la dirección de SMTP principal del usuario y cualquier dirección de proxy asociada. La dirección SMTP principal (también denominada *dirección de respuesta predeterminada* se muestra en negrita en la lista de direcciones, con el valor **SMTP** en mayúsculas en la columna **Tipo**.

  - **Agregar **  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una dirección de correo electrónico nueva para este buzón. Seleccione uno de los siguientes tipos de dirección:
    
      - **Dirección SMTP**   Este es el tipo de dirección predeterminado. Haga clic en este botón y luego escriba la nueva dirección SMTP en la casilla **\* Dirección de correo electrónico**.
    
      - **EUM**   El servicio de mensajería unificada de Microsoft Exchange utiliza una dirección EUM (mensajería unificada de Exchange) para ubicar usuarios habilitados para MU en una organización de Exchange. Las direcciones EUM constan del número de extensión y el plan de marcado de MU para el usuario habilitado para MU. Haga clic en este botón y escriba el número de extensión en el cuadro **Dirección/extensión**. Luego, haga clic en **Examinar** y seleccione un plan de marcado para el usuario.
    
      - **Tipo de dirección personalizada**   Haga clic en este botón y escriba uno de los tipos de dirección de correo electrónico que no sean SMTP admitidos en la casilla **\* Dirección de correo electrónico**.
        

        > [!NOTE]
        > Con excepción de las direcciones X.400, Exchange no valida las direcciones personalizadas para comprobar el formato adecuado. Debe asegurarse de que la dirección personalizada que especifica cumpla los requisitos de formato para el tipo de dirección.

    
      - **Hacer que esta sea la dirección de respuesta**   En Exchange Online, puede activar esta casilla para que la nueva dirección de correo electrónico sea la dirección SMTP principal del buzón de correo. Esta casilla no está disponible en el EAC en Exchange 2013.

  - **Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada a este destinatario   **Seleccione esta casilla para que las direcciones de correo electrónico del destinatario se actualicen automáticamente según los cambios realizados en las directivas de direcciones de correo electrónico de su organización. Esta casilla está activada de forma predeterminada.
    

    > [!NOTE]
    > Esta casilla no está disponible en Exchange Online.



  - **Hacer que esta sea la dirección de respuesta**

## Características de buzón

Use la sección **Características de buzón** para ver o cambiar la configuración y las características de buzón siguientes:

  - **Directiva de uso compartido**   En este cuadro se muestra la directiva de uso compartido que se aplica al buzón. Las directivas de uso compartido permiten controlar la manera en que los usuarios de una organización comparten el calendario y la información de contacto con los usuarios externos a la organización de Exchange. La directiva de uso compartido predeterminada se asigna a los buzones cuando se crean. Para cambiar la directiva de uso compartido asignada al usuario, seleccione una directiva diferente en la lista desplegable.

  - **Directiva de asignación de roles**   En este cuadro se muestra la directiva de asignación de roles asignada al buzón. La directiva de asignación de roles especifica los roles de control de acceso basados en roles (RBAC) que se asignan al usuario y controla la configuración de buzones y de grupos de distribución específica que los usuarios pueden modificar. Para cambiar la directiva de asignación de roles asignada al usuario, seleccione una directiva diferente en la lista desplegable.

  - **Directiva de retención**   En este cuadro se muestra la directiva de retención asignada al buzón. Una directiva de retención es un grupo de etiquetas de retención que se aplica al buzón del usuario. Le permiten controlar cuánto tiempo mantener los elementos de los buzones de correo de los usuarios y definir qué acción realizar en los elementos que han alcanzado cierta edad. Las directivas de retención no se asignan a los buzones cuando se crean. Para asignar una directiva de retención al usuario, selecciónela en la lista desplegable.

  - **Directiva de libreta de direcciones**   En este cuadro se muestra la directiva de libreta de direcciones que se aplica al buzón. Una directiva de libreta de direcciones le permite segmentar a los usuarios en grupos específicos para proporcionar vistas personalizadas de la libreta de direcciones. Para aplicar o cambiar la directiva de libreta de direcciones aplicada al buzón, seleccione una de la lista desplegable.

  - **Mensajería unificada**   Esta función está deshabilitada de forma predeterminada. Al habilitar la mensajería unificada (MU), el usuario podrá usar las características de la MU de la organización y un conjunto predeterminado de propiedades de la misma se aplicarán al usuario. Haga clic en **Habilitar** para habilitar la mensajería unificada en el buzón. Para obtener información acerca de cómo habilitar la MU, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).
    

    > [!NOTE]
    > Para habilitar la mensajería unificada, debe tener un plan de marcado de mensajería unificada y una directiva de buzones de mensajería unificada.



  - **Dispositivos móviles**   Utilice esta sección para ver y cambiar las configuraciones de Exchange ActiveSync, que está habilitado de manera predeterminada. Exchange ActiveSync permite obtener acceso al buzón de Exchange desde dispositivos móviles. Haga clic en **Deshabilitar Exchange ActiveSync** para deshabilitar esta característica en el buzón.

  - **Outlook Web App**   Esta función está habilitada de forma predeterminada. Outlook Web App permite obtener acceso al buzón de Exchange desde cualquier explorador web. Haga clic en **Deshabilitar** para deshabilitar Outlook Web App en el buzón. Haga clic en **Editar detalles** para agregar o cambiar una directiva de buzones de Outlook Web App en el buzón.

  - **IMAP**   Esta función está habilitada de forma predeterminada. Haga clic en **Deshabilitar** para deshabilitar IMAP en buzón de correo.

  - **POP3**   Esta función está habilitada de forma predeterminada. Haga clic en **Deshabilitar** para deshabilitar POP3 en buzón de correo.

  - **MAPI**   Esta función está habilitada de forma predeterminada. MAPI permite obtener acceso a un buzón de Exchange desde un cliente MAPI, como Outlook. Haga clic en **Deshabilitar** para deshabilitar MAPI en buzón de correo.

  - **Retención por juicio**   Esta función está deshabilitada de forma predeterminada. La suspensión de litigio preserva los elementos de buzón eliminados y registra las modificaciones que se les realizaron a los elementos de buzón. Los elementos eliminados y todas las copias de los elementos modificados se devuelven en una búsqueda de detección. Haga clic en **Habilitar** para aplicar la retención por juicio en el buzón de correo. Si el buzón tiene una retención por juicio, haga clic en **Deshabilitar** para eliminar dicha retención. Los buzones en retención por juicio son buzones inactivos y no se pueden eliminar. Para eliminar el buzón, quite la retención por juicio. Si el buzón está retenido por juicio, haga clic en **Editar detalles** para ver y cambiar la siguiente configuración de retención por juicio:
    
      - **Fecha de retención**   Este cuadro de solo lectura indica la fecha y hora en que se retuvo el buzón por juicio.
    
      - **Retenido por**   En este cuadro de solo lectura se indica el usuario que retuvo el buzón por un juicio.
    
      - **Nota**   Use este cuadro para notificar al usuario la retención por juicio, explicar el motivo por el que se ha aplicado la retención por juicio al buzón de correo o proporcionar instrucciones adicionales al usuario, como por ejemplo informarle de que la retención por juicio no afectará al uso cotidiano del correo electrónico.
    
      - **URL**   Use este campo para indicar una dirección URL a un sitio web que ofrezca información o instrucciones acerca de la retención por juicio que tiene aplicada el buzón de correo.
        

        > [!NOTE]
        > El texto de estos campos aparecen en el buzón de correo del usuario únicamente si usa Outlook 2010 o versiones posteriores. No aparece en Outlook Web App ni en otros clientes de correo electrónico. Para ver el texto de los cuadros Nota y URL en Outlook, haga clic en la ficha <STRONG>Archivo</STRONG> y, en la página <STRONG>Información</STRONG>, bajo <STRONG>Configuración de la cuenta</STRONG>, aparecerá el comentario de la retención por juicio.



  - **Archivado** Si no existe ningún buzón de correo de archivo para el usuario, esta característica está deshabilitada. Para habilitar un buzón de archivo, haga clic en **Habilitar**. Si el usuario posee un buzón de archivo, se muestran el tamaño del buzón de archivo y las estadísticas de uso. Haga clic en **Editar detalles** para ver y cambiar la siguiente configuración de buzones de archivo:
    
      - **Estado**   En este cuadro de solo lectura se indica si existe un buzón de archivo.
    
      - **Base de datos**   En este cuadro de solo lectura se muestra el nombre de la base de datos de buzones que hospeda el buzón de archivo. Este cuadro no está disponible en Exchange Online.
    
      - **Nombre**   Escriba el nombre del buzón de archivo en este cuadro. El nombre aparecerá debajo de la lista de carpetas en Outlook o en Outlook Web App.
    
      - **Cuota de archivo (GB)**   Este cuadro muestra el tamaño total del buzón de archivo. Para cambiar el tamaño, escriba un valor nuevo en el cuadro o selecciónelo en la lista desplegable.
    
      - **Emitir advertencia al llegar a (GB)**   En este cuadro aparece el límite de almacenamiento máximo para el buzón de archivo antes de que se envíe una advertencia al usuario. Si el tamaño del buzón de archivo alcanza o supera el valor especificado, Exchange enviará un mensaje de advertencia al usuario. Para cambiar el límite, escriba un valor nuevo en el cuadro o selecciónelo en la lista desplegable.
        

        > [!NOTE]
        > La cuota de archivo y la cuota de emisión de advertencia para el buzón de archivo no se pueden modificar en Exchange Online.



  - **Opciones de entrega**   Utilice esta opción para reenviar mensajes de correo electrónico a otros destinatarios y enviados al usuario, y para establecer el número máximo de destinatarios a los que el usuario puede enviar un mensaje. Haga clic en **Ver detalles** para ver y cambiar esta configuración.
    
      - **Dirección de reenvío**   Seleccione la casilla **Habilitar el reenvío** y, a continuación, haga clic en **Examinar** para ver la página **Seleccionar usuario de correo y buzón**. En esta página podrá seleccionar el destinatario al que desea reenviar todos los correos electrónicos que se envíen a este buzón.
    
      - **Entregar los mensajes a la dirección de reenvío y al buzón**   Active esta casilla para que los mensajes se entreguen a la dirección de reenvío y al buzón de correo del usuario.
    
      - **Límite de destinatarios**   Esta configuración establece el número máximo de destinatarios a los que el usuario puede enviar un mensaje. Seleccione la casilla **Núm. máximo de destinatarios** para limitar el número de destinatarios permitidos en las líneas Para:, Cc: y Cco: de un mensaje de correo electrónico y, a continuación, especifique el número máximo de destinatarios.
        

        > [!NOTE]
        > Para las organizaciones locales de Exchange, el límite de destinatarios es ilimitado. Para las organizaciones de Exchange Online, el límite es de 500 destinatarios.



  - **Restricciones de tamaño de mensaje**   Estas configuraciones controlan el tamaño de los mensajes que el usuario puede enviar y recibir. Haga clic en **Ver detalles** para ver y cambiar el tamaño máximo de los mensajes enviados y recibidos.
    

    > [!NOTE]
    > Esta configuración no se puede modificar en Exchange Online.

    
      - **Mensajes enviados**   Para indicar el tamaño máximo de los mensajes enviados por este usuario, seleccione la casilla **Tamaño máximo de mensaje (en KB)** y escriba un valor en el cuadro. El tamaño del mensaje debe estar entre 0 y 2.097.151 KB. Si el usuario envía un mensaje que supera el tamaño indicado, se le devolverá con un mensaje de error descriptivo.
    
      - **Mensajes recibidos**   Para indicar el tamaño máximo de los mensajes recibidos por este usuario, seleccione la casilla **Tamaño máximo de mensaje (en KB)** y escriba un valor en el cuadro. El tamaño del mensaje debe estar entre 0 y 2.097.151 KB. Si el usuario recibe un mensaje que supera el tamaño indicado, se devuelve al emisor con un mensaje de error descriptivo.

  - **Restricción de entrega de mensajes**   Estas configuraciones controlan quién puede enviar mensajes de correo electrónico a este usuario. Haga clic en **Ver detalles** para ver y cambiar estas restricciones.
    
      - **Aceptar mensajes de**   Esta sección sirve para indicar quién puede enviar mensajes al usuario.
        
          - **Todos los remitentes**   Seleccione esta opción para especificar que el usuario puede aceptar mensajes de todos los remitentes. Se incluyen los remitentes de la organización de Exchange y los remitentes externos. Esta opción está seleccionada de forma predeterminada. Esta opción incluye a los usuarios externos solo si desactiva la casilla **Requerir la autenticación de todos los remitentes**. Si activa esta casilla, se rechazarán los mensajes de los usuarios externos.
        
          - **Solo los remitentes de la siguiente lista** Seleccione esta opción para especificar que el usuario puede aceptar mensajes únicamente de un grupo específico de remitentes de la organización de Exchange. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")para mostrar la página **Seleccionar destinatarios**, que muestra una lista de todos los destinatarios en la organización de Exchange. Seleccione los destinarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").
        
          - **Requerir la autenticación de todos los remitentes**   Seleccione esta opción para impedir que usuarios anónimos envíen mensajes al usuario.
    
      - **Rechazar mensajes de**   Use esta sección para bloquear a ciertos usuarios y que no envíen mensajes al usuario.
        
          - **Ningún remitente**   Elija esta opción para especificar que el buzón no rechazará mensajes de ningún remitente de la organización de Exchange. Esta opción está seleccionada de forma predeterminada.
        
          - **Remitentes de la siguiente lista** Seleccione esta opción para especificar que el buzón rechazará mensajes de un grupo específico de remitentes de la organización de Exchange. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para mostrar la página **Seleccionar destinatarios**, que muestra una lista de todos los destinatarios en la organización de Exchange. Seleccione los destinarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").

## Miembro de

Utilice la sección **Miembro de** para ver una lista de los grupos de distribución o los grupos de seguridad a los que pertenece el usuario. La información de pertenencia no se puede cambiar en esta página. Tenga en cuenta que el usuario puede coincidir con los criterios de uno o más grupos de distribución dinámicos de la organización. No obstante, los grupos de distribución dinámicos no se muestran en esta página porque su pertenencia se calcula cada vez que se usan.

## Información sobre correo

Utilice la sección **Sugerencia de correo** para agregar una sugerencia de correo y avisar a los usuarios de posibles problemas si envían un mensaje a este destinatario. La información sobre correo es texto que se muestra en la barra de información cuando este destinatario se agrega a los campos Para, CC o CCO de un nuevo mensaje de correo electrónico.


> [!NOTE]
> La información sobre correo puede incluir etiquetas HTML, pero no se permiten los scripts. La longitud de la información de una sugerencia de correo electrónico personalizada no puede superar los 175 caracteres mostrados. Las etiquetas HTML no se cuentan en el límite.



## Delegación de buzones

La sección **Delegación de buzones** sirve para asignar permisos a otros usuarios (también llamados *delegados*) y permitirles iniciar sesión en el buzón del usuario o enviar mensajes en su nombre. Se pueden asignar los siguientes permisos:

  - **Enviar como**   Esta configuración permite a aquellos usuarios que no sean el propietario usar el buzón para enviar mensajes. Después de asignar este permiso a un delegado, los mensajes que el delegado envíe desde el buzón aparecerán como si los hubiera enviado el propietario del buzón. Sin embargo, el delegado no podrá iniciar sesión en el buzón del usuario con este permiso.

  - **Enviar en nombre de**   Esta configuración también permite que un delegado use el buzón para enviar mensajes. No obstante, después de asignar este permiso a un delegado, la dirección del campo **De:**  de los mensajes enviados por el delegado indicará que el mensaje lo envió el delegado en nombre del propietario del buzón.

  - **Acceso completo**   Esta configuración permite que un delegado inicie sesión en el buzón del usuario y vea su contenido. Sin embargo, después de asignar este permiso a un delegado, no podrá enviar mensajes desde el buzón. Para que un delegado pueda enviar correos electrónicos desde el buzón del usuario, debe asignarle los permisos Enviar como o Enviar en nombre de.

Para asignar permisos a los delegados, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") debajo del permiso adecuado para mostrar una página que muestra una lista de todos los destinatarios en su organización de Exchange a los que se les puede asignar los permisos. Seleccione los destinarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").

## Uso del Shell para cambiar las propiedades de los buzones de usuario

Use los cmdlets **Get-Mailbox** y **Set-Mailbox** para ver y cambiar las propiedades de los buzones de usuario. Una ventaja de usar el Shell es que puede cambiar las propiedades de varios buzones. Para obtener más información sobre los parámetros que corresponden a las propiedades del buzón, vea los siguientes temas:

  - [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\))

A continuación aparecen algunos ejemplos de cómo usar el Shell para cambiar las propiedades del buzón de usuario.

Este ejemplo muestra cómo reenviar los mensajes de correo de Pat Coleman al buzón de Sunil Koduri (sunilk@contoso.com).

    Set-Mailbox -Identity patc -DeliverToMailboxAndForward $true -ForwardingAddress sunilk@contoso.com

En este ejemplo se utiliza el comando **Get-Mailbox** para buscar todos los buzones de usuario de la organización y, a continuación, se usa el comando**Set-Mailbox** para establecer el límite de destinatarios en 500 destinatarios permitidos en los cuadros Para:, Cc: y Cco: de un mensaje de correo electrónico.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -RecipientLimits 500

En este ejemplo se usa el comando **Get-Mailbox** para buscar todos los buzones en la unidad organizativa de Marketing; a continuación, usa el comando **Set-Mailbox** para configurar estos buzones. Los límites de advertencia personalizada, prohibir envío y recepción se establecen en 200 MB, 250 MB y 280 MB, respectivamente, y se prescinde de los límites predeterminados de la base de datos del buzón. Este comando se puede usar para configurar que un conjunto específico de buzones tenga límites superiores o inferiores a los de otros buzones de la organización.

    Get-Mailbox -OrganizationalUnit "Marketing" | Set-Mailbox -IssueWarningQuota 209715200 -ProhibitSendQuota 262144000 -ProhibitSendReceiveQuota 293601280 -UseDatabaseQuotaDefaults $false 

En este ejemplo se usa el cmdlet **Get-Mailbox** para buscar todos los usuarios del departamento de Atención al cliente; a continuación, se usa el cmdlet**Set-Mailbox** para cambiar el tamaño máximo de mensaje en 2 MB al enviar mensajes.

    Get-Mailbox -Filter "Department -eq 'Customer Service'" | Set-Mailbox -MaxSendSize 2097152

En este ejemplo se establece la traducción de la sugerencia de correo electrónico en francés y en chino.

    Set-Mailbox john@contoso.com -MailTipTranslations ("FR: C'est la langue française", "CHT: 這是漢語語言")

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si cambió las propiedades de un buzón de usuario correctamente, haga lo siguiente:

  - En el EAC, seleccione el buzón y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para visualizar la propiedad o característica que ha modificado. Según la propiedad que cambie, puede aparecer en el panel Detalles del buzón seleccionado.

  - En el Shell, use el cmdlet **Get-Mailbox** para verificar los cambios. Una de las ventajas de usar el Shell es que puede ver diferentes propiedades para varios buzones. En el ejemplo anterior en el que se cambió el límite de destinatarios, ejecute el siguiente comando para comprar el valor nuevo.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    Ejecute este comando para el ejemplo anterior donde se modificaron los límites del mensaje.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

## Editar en masa buzones de usuario

Puede usar el EAC para cambiar las propiedades de varios buzones de correo de usuario. Cuando seleccione dos o más buzones de usuario de la lista de buzones del EAC, las propiedades que se pueden editar masivamente aparecen en el panel Detalles. Cuando cambia una de estas propiedades, el cambio se aplica a todos los buzones seleccionados.

A continuación aparece una lista de las propiedades y características de buzones de usuario que se pueden editar en masa. Recuerde que no todas las propiedades de cada área se pueden modificar.

  - **Información de contacto**   Cambie las propiedades compartidas, como la calle, el código postal y el nombre de la ciudad.

  - **Organización** Cambie las propiedades compartidas, como el nombre de departamento, el nombre de la compañía y el administrador al que informan los usuarios seleccionados.

  - **Atributos personalizados** Cambie o agregue los valores de los atributos personalizados 1 – 15.

  - **Cuota de buzón**   Cambie los valores de cuota de buzón y del período de retención de los elementos suprimidos. Esto no está disponible en Exchange Online.

  - **Conectividad de correo**   Habilite o deshabilite Outlook Web App, POP3, IMAP, MAPI y Exchange ActiveSync.

  - **Archivo** Habilite o deshabilite el buzón de archivo.

  - **Directiva de retención, directiva de asignación de roles y directiva de uso compartido**   Actualice la configuración de cada una de estas características de buzón.

  - **Mover buzones a otra base de datos**   Mueva los buzones seleccionados a una base de datos diferente.

  - **Delegar permisos**   Asignar a los usuarios o grupos permisos para que puedan abrir o enviar mensajes desde otros buzones. Puede asignar a los usuarios o grupos los permisos Acceso total, Enviar como y Enviar en nombre de. Consulte [Administrar permisos para los destinatarios](manage-permissions-for-recipients-exchange-online-help.md) para obtener más información.


> [!NOTE]
> El tiempo estimado para completar esta tarea es de 2 minutos, pero podría durar más si cambia varias propiedades o características.



## Utilizar el EAC para editar en masa los buzones de usuario

1.  En la EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En la lista de buzones de correo, seleccione dos o más buzones.
    

    > [!TIP]
    > Puede seleccionar varios buzones adyacentes manteniendo presionada la tecla MAYÚS y haciendo clic en el primer buzón y, seguidamente, haciendo clic en el último buzón que desea editar. También puede seleccionar varios buzones no adyacentes manteniendo presionada la tecla CTRL y haciendo clic en cada uno de los buzones que desea editar.



3.  En el panel Detalles, bajo **Editar en masa**, seleccione las propiedades o características de los buzones que desea editar.

4.  Realice los cambios en la página de propiedades y, a continuación, guarde los cambios.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si editó correctamente en masa los buzones de usuario, siga uno de estos procedimientos:

  - En el EAC, seleccione cada uno de los buzones que ha editado en masa y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para visualizar las propiedades o características que ha modificado.

  - En el Shell de administración de Exchange, use el cmdlet **Get-Mailbox** para verificar los cambios. Una de las ventajas de usar el Shell es que puede ver diferentes propiedades para varios buzones. Por ejemplo, supongamos que ha usado la característica de edición en masa del EAC para habilitar el buzón de archivo y para asignar una directiva de retención a todos los usuarios de la organización. Para comprobar estos cambios, puede ejecutar el siguiente comando:
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,ArchiveDatabase,RetentionPolicy
    
    Para obtener más información acerca de los parámetros disponibles para el cmdlet **Get-Mailbox**, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)).

