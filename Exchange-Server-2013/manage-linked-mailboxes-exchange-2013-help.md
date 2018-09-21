---
title: 'Administrar buzones vinculados: Exchange 2013 Help'
TOCTitle: Administrar buzones vinculados
ms:assetid: 76e12d4a-1c3a-42e2-b64c-c09d36e81bd3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673532(v=EXCHG.150)
ms:contentKeyID: 49895722
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar buzones vinculados

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-27_

Los buzones vinculados son buzones a los que los usuarios obtienen acceso en un bosque de confianza diferente. Es posible que los buzones vinculados sean necesarios para organizaciones que eligen implementar Exchange en un bosque de recursos. El caso del bosque de recursos permite a una organización centralizar Exchange en un único bosque, a la vez que permite tener acceso a la organización de Exchange con cuentas de usuario en uno o más bosques de confianza (denominados *bosques de cuentas*). La cuenta de usuario que tendrá acceso al buzón vinculado no existe en el bosque en el que se ha implementado Exchange. Por ello, hay una cuenta de usuario deshabilitada en el mismo bosque de Exchange que está creada y asociada al buzón vinculado correspondiente.

La figura siguiente ilustra la relación entre la cuenta de usuario vinculada usada para tener acceso al buzón vinculado (ubicado en el bosque de cuentas) y la cuenta de usuario deshabilitada en el bosque de recursos de Exchange asociada al buzón vinculado.

**Buzones vinculados**

![Organización de Exchange compleja con bosque de recursos](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organización de Exchange compleja con bosque de recursos")


> [!NOTE]  
> Debe configurarse una confianza entre el bosques de Exchange y al menos un bosque de cuentas antes de crear buzones vinculados. Como mínimo, deberá configurar una confianza saliente unidireccional para que el busque de Exchange confíe en el bosque de cuentas. Para obtener más información, consulte <A href="https://technet.microsoft.com/es-es/library/jj156983(v=exchg.150)">Obtenga más información acerca de la configuración de una confianza de bosque para que sea compatible con los buzones vinculados</A>.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 a 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Debe existir una cuenta de usuario (denominada *cuenta maestra vinculada*) en el bosque de cuentas antes de poder crear un buzón vinculado. Esto sucede porque el buzón vinculado está asociado a un usuario del bosque de cuentas.

  - Si ha configurado una confianza saliente unidireccional en la que el bosque de Exchange confíe en el bosque de cuentas, necesitará las credenciales de administrador del bosque de cuentas para poder crear un buzón vinculado.
    
    Para crear un buzón vinculado sin que se soliciten credenciales de administrador en el bosque de la cuenta, debe crear una confianza bidireccional o crear otra confianza unidireccional saliente en la que el bosque de la cuenta también confíe en el bosque de Exchange. Este paso también requiere credenciales de administrador del bosque de cuentas.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Crear un buzón vinculado

## Usar el EAC para crear un buzón vinculado

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  Haga clic en **Nuevo** \> **Buzón vinculado**.

3.  En la página **Nuevo buzón vinculado**, en el cuadro **Bosque o dominio de confianza**, seleccione el nombre del bosque de cuentas que contiene la cuenta de usuario para la que está creando el buzón vinculado. Haga clic en **Siguiente**.

4.  Si su organización ha configurado una confianza saliente unidireccional en la que los bosques de Exchange confían en el bosque de cuentas, se le pedirán las credenciales de administrador del bosque de cuentas para que pueda acceder al controlador de dominios del bosque de confianza. Escriba el nombre de usuario y la contraseña de una cuenta de administrador en el bosque de cuentas y, a continuación, haga clic en **Siguiente**.
    

    > [!NOTE]  
    > No se le pedirán las credenciales de administrador en caso de que haya creado una confianza bidireccional u otra confianza saliente unidireccional en la que el bosque de cuentas confíe en el bosque de Exchange.



5.  Completa los siguientes cuadros de la página **Seleccionar la cuenta maestra vinculada**.
    
      - **Controlador de dominio vinculado** Seleccione un controlador de dominio del bosque de cuentas. Exchange se conectará a este controlador de dominio para recuperar la lista de cuentas de usuario del bosque de cuentas, de modo que pueda seleccionar la cuenta maestra vinculada.
    
      - **Cuenta maestra vinculada**   Haga clic en **Explorar**, seleccione una cuenta de usuario en el bosque de cuentas y, a continuación, haga clic en **Aceptar**. El nuevo buzón vinculado estará asociado a esta cuenta.

6.  Haga clic en **Siguiente** y complete los cuadros siguientes en la página **Escribir información general**.
    
      - **\* Nombre**   Use este cuadro para escribir un nombre para el usuario. Este será el nombre utilizado como nombre para mostrar en el EAC y en la libreta de direcciones de la organización, así como el nombre que aparezca en Active Directory. Este nombre es obligatorio.
    
      - **Unidad organizativa**   Puede seleccionar una unidad organizativa (OU) diferente a la que aparece de forma predeterminada (en el ámbito de destinatarios). Si el ámbito de destinatario definido corresponde al bosque, el valor predeterminado será el contenedor Usuarios del dominio de Active Directory que contiene el equipo en el que se ejecuta EAC. Si el ámbito del destinatario está establecido en un dominio específico, el contenedor de usuarios se selecciona de modo predeterminado. Si el ámbito del destinatario está establecido en una unidad organizativa específica (OU), esa OU se selecciona de modo predeterminado.
        
        Para seleccionar otra OU, haga clic en **Examinar**. En el cuadro de diálogo se muestran todas las OU del bosque d Exchange dentro del ámbito especificado. Seleccione la unidad organizativa que desee y haga clic en **Aceptar**.
    
      - **\* Nombre de inicio de sesión del usuario**   Utilice este cuadro para escribir el nombre de inicio de sesión del usuario, un paso obligatorio para crear un buzón vinculado. Escriba aquí el nombre de usuario. Este nombre se utilizará para la parte izquierda de la dirección de correo electrónico del buzón vinculado, en caso de que no especifique un alias.
        

        > [!NOTE]  
        > Dado que la cuenta de usuario creada en el bosque de Exchange está deshabilitada al crear un buzón vinculado, el usuario no utilizará el nombre de inicio de sesión para iniciar sesión en el buzón vinculado. Estos inician sesión mediante sus credenciales del bosque de cuentas.



7.  Haga clic en **Más opciones** para configurar los siguientes cuadros. De lo contrario, vaya al Paso 8 para guardar el nuevo buzón vinculado.
    
      - **Alias**   Escriba el alias, que especifica el alias de correo electrónico para el buzón vinculado. El alias del usuario es la porción de la dirección de correo electrónico ubicada a la izquierda del símbolo arroba (@). Debe ser exclusivo en el bosque.
        

        > [!NOTE]  
        > Si deja este cuadro vacío, se usa para el alias de correo electrónico el valor de la parte del nombre de usuario del <STRONG>Nombre de inicio de sesión del usuario</STRONG>.

    
      - **Nombre**, **Inicial**, **Apellidos**
    
      - **Base de datos de buzones**   Use esta opción para especificar una base de datos de buzones en vez de permitir que Exchange seleccione la base de datos. Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar base de datos de buzones**. En este cuadro de diálogo se enumeran todas las bases de datos de buzones de la organización de Exchange. De manera predeterminada, las bases de datos de buzones se ordenan por el nombre. También puede hacer clic en el título de la columna correspondiente para ordenar las bases de datos por versión o nombre del servidor. Seleccione la base de datos de buzones que desee usar y haga clic en **Aceptar**.
    
      - **Directiva de la libreta de direcciones**   Utilice esta opción para especificar una directiva de libreta de direcciones (ABP) para el buzón vinculado. Las ABP contienen una lista global de direcciones (GAL), una libreta de direcciones sin conexión (OAB), una lista de salas y un conjunto de listas de direcciones. Cuando se asigna una ABP a usuarios, esta les proporciona acceso a una LGD personalizada en Outlook y Outlook Web App. Para obtener más información, consulte [Directivas de la libreta de direcciones](https://docs.microsoft.com/es-es/exchange/address-books/address-book-policies/address-book-policies).
        
        En la lista desplegable, seleccione la directiva que desea asociar con este buzón.

8.  Cuando haya terminado, haga clic en **Guardar** para crear el nuevo buzón vinculado.

## Usar el Shell para crear un buzón vinculado

En este ejemplo se crea un buzón vinculado para Ayla Kol en el bosque de recursos de Exchange CONTOSO. El dominio FABRIKAM está el bosque de cuentas. La cuenta de administrador FABRIKAM\\administrador se utiliza para acceder al controlador de dominio vinculado.

    New-Mailbox -Name "Ayla Kol" -LinkedDomainController "DC1_FABRIKAM" -LinkedMasterAccount " FABRIKAM\aylak" -OrganizationalUnit Users -UserPrincipalName aylak@contoso.com -LinkedCredential:(Get-Credential FABRIKAM\administrator)

Para obtener información acerca de la sintaxis y los parámetros, consulte [New-Mailbox](https://technet.microsoft.com/es-es/library/aa997663\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó un buzón vinculado correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Buzones**. El nuevo buzón vinculado aparece en la lista de buzones. Bajo **Tipo de buzón de correo**, el tipo es **Vinculado**.

  - En el Shell, ejecute el comando siguiente para mostrar información sobre el nuevo buzón vinculado.
    
    ```powershell
Get-Mailbox <Name> | FL Name,RecipientTypeDetails,IsLinked,LinkedMasterAccount
```

## Cambiar las propiedades de los buzones vinculados

Tras crear un buzón vinculado, podrá realizar los cambios y establecer propiedades adicionales mediante el Centro de administración de Exchange (EAC) o el Shell de administración de Exchange.

También puede cambiar las propiedades de varios buzones vinculados al mismo tiempo. Para obtener más información, consulte la sección, "Edición en masa de buzones de usuario" en el tema [Administrar los buzones de usuario](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/include-text-with-email-sent-when-voicemail-is-enabled).


> [!IMPORTANT]
> El tiempo estimado para completar esta tarea variará en función de la cantidad de propiedades que desee ver o cambiar.



## Uso del EAC para cambiar las propiedades de los buzones vinculados

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En la lista de buzones, haga clic en el buzón vinculado cuyas propiedades desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del buzón, haga clic en las siguientes secciones para ver o cambiar las propiedades.
    
      - General
    
      - Uso del buzón de correo
    
      - Dirección de correo electrónico
    
      - Características de buzón
    
      - Miembro de
    
      - Información sobre correo
    
      - Delegación de buzones

## General

Utilice la sección **General** para ver o cambiar la información básica sobre el usuario.

  - **\* Nombre del buzón vinculado** Se trata del nombre indicado en Active Directory. Si cambia este nombre, no debe superar los 64 caracteres.

  - **\* Nombre para mostrar**   Este nombre aparece en la libreta de direcciones de la organización, en las líneas Para: y De: del correo electrónico, y en la lista de buzones del EAC. Este nombre no puede contener espacios en blanco antes o después del nombre para mostrar.

  - **\* Nombre de inicio de sesión del usuario**   Para los buzones de usuario, este es el nombre que utiliza el usuario para iniciar sesión en su buzón y en el dominio. Para los buzones vinculados, la cuenta de usuario correspondiente que se creó en el bosque de Exchange cuando se creó el buzón vinculado está deshabilitada. El usuario utiliza sus credenciales del bosque de cuentas para iniciar sesión en el buzón vinculado.
    
    Si lo cambia, debe ser por un nombre exclusivo de la organización.

  - **Cuenta maestra vinculada**   Este cuadro de solo lectura muestra el usuario (con el formato \\dominio\\formato de nombre de usuario) del bosque de cuentas que está asociado al buzón vinculado. Para cambiar la cuenta maestra vinculada al buzón vinculado, deberá usar el cmdlet **Set-Mailbox** del Shell. Si modifica esta cuenta, el usuario tendrá que utilizar las credenciales de la nueva cuenta maestra vinculada para iniciar sesión en el buzón vinculado. Para obtener información acerca de la sintaxis de comandos para cambiar la cuenta maestra vinculada, consulte Uso del Shell para cambiar las propiedades de los buzones vinculados.

  - **Ocultar de las listas de direcciones** Seleccione esta casilla para impedir que el buzón vinculado aparezca en la lista de direcciones y otras listas definidas en la organización de Exchange. Después de seleccionarla, los usuarios aún podrán enviar mensajes a este usuario con su dirección de correo electrónico.

Haga clic en **Más opciones** para ver o cambiar estas propiedades adicionales:

  - **Unidad organizativa** Este cuadro de solo lectura muestra la unidad organizativa (OU) que contiene la cuenta de usuario. Debe usar Usuarios y equipos de Active Directory para mover la cuenta de usuario a una OU diferente.

  - **Base de datos de buzones de correo**   Este cuadro de solo lectura muestra el nombre de la base de datos de buzón que hospeda el buzón. Para desplazar el buzón a una base de datos diferente, selecciónelo en la lista de buzones y, a continuación, haga clic en **Mover el buzón a una base de datos diferente** en el panel Detalles.

  - **\* Alias** Este nombre especifica el alias de correo electrónico del buzón vinculado. El alias es la parte de la dirección de correo electrónico a la izquierda del símbolo arroba (@). Debe ser exclusivo en el bosque.

  - **Nombre**, **Inicial**, **Apellidos**

  - **Atributos personalizados**   Esta sección muestra los atributos personalizados que se han definido para el buzón vinculado. Para especificar los valores de los atributos personalizados, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Se pueden especificar hasta 15 atributos personalizados para el destinatario.

## Uso del buzón de correo

Utilice la sección **Uso del buzón** para ver o cambiar la cuota de almacenamiento del buzón y la configuración de retención de elementos eliminados del buzón vinculado. Estas opciones se configuran de forma predeterminada cuando se crea el buzón vinculado. Usan los valores configurados para la base de datos de buzón y se aplican a todos los buzones de esa base de datos. Puede personalizar esta configuración para cada buzón en vez de usar la configuración predeterminada de la base de datos del buzón.

  - **Última sesión iniciada**   En este cuadro de solo lectura se muestra la última vez que el usuario inició sesión en el buzón.

  - **Uso de buzón de correo**   Esta área muestra el tamaño total del buzón y el porcentaje de la cuota total del buzón que se usó.


> [!NOTE]  
> Para obtener la información que se muestra los dos cuadros previos, EAC consulta la base de datos de buzón que hospeda el buzón. Si el EAC no consigue comunicarse con el almacén de Exchange que contiene la base de datos de buzones, estos campos estará vacíos. Se muestra un mensaje de advertencia si el usuario no ha iniciado sesión en el buzón por primera vez.



Haga clic en **Más opciones** para ver o cambiar la cuota de almacenamiento del buzón y la configuración de retención de elementos eliminados del buzón.

  - **Configuración de la cuota de almacenamiento**   Para personalizar esta configuración del buzón y no usar los valores predeterminados de la base de datos del mismo, haga clic en **Personalizar la configuración de este buzón**, escriba un valor nuevo y, finalmente, haga clic en **Guardar**.
    
    El intervalo de valor para la configuración de la cuota de almacenamiento oscila entre 0 y 2047 gigabytes (GB).
    
      - **Emitir una advertencia al llegar a (GB)**   Este cuadro muestra el límite máximo de almacenamiento antes de que se emita una advertencia al usuario. Si el tamaño del buzón alcanza o supera el valor especificado, Exchange envía un mensaje de advertencia al usuario.
    
      - **Prohibir envío al llegar a (GB)**   Este cuadro muestra el límite del buzón para *prohibir el envío*. Si el tamaño del buzón alcanza o supera el límite especificado, Exchange impide que el usuario envíe nuevos mensajes y muestra un mensaje de error descriptivo.
    
      - **Prohibir envío y recepción al llegar a (GB)**   Este cuadro muestra el límite del buzón para *prohibir el envío y recepción*. Si el tamaño del buzón alcanza o supera el límite especificado, Exchange impide que el usuario del buzón envíe mensajes nuevos y no entregará ningún mensaje nuevo en el buzón. Todos los mensajes que se envíen al buzón se devolverán al remitente con un mensaje de error descriptivo.

  - **Configuración de la retención de elementos eliminados**   Para personalizar esta configuración del buzón y no usar los valores predeterminados de la base de datos del mismo, haga clic en **Personalizar la configuración de este buzón**, escriba un valor nuevo y, finalmente, haga clic en **Guardar**.
    
      - **Guardar los elementos eliminados durante (días)**   Este cuadro muestra la cantidad de tiempo que se retienen los elementos eliminados antes de que se eliminen permanentemente y el usuario no pueda recuperarlos. Al crear el buzón, esta duración se basa en los valores de retención de elementos eliminados configurados para la base de datos de buzones. De manera predeterminada, se configura una base de datos de buzón para que retenga los elementos eliminados por 14 días. El intervalo de valores para esta propiedad oscila entre 0 y 24855 días.
    
      - **No eliminar permanentemente los elementos hasta después de realizada la copia de seguridad de la base de datos**   Seleccione esta casilla de verificación para evitar que los buzones y los mensajes de correo electrónico se eliminen hasta que se haya realizado la copia de seguridad de la base de datos de buzones en la que está ubicado el buzón.

## Dirección de correo electrónico

Use la sección **Dirección de correo electrónico** para ver o cambiar las direcciones de correo electrónico asociadas al buzón vinculado. Esto incluye las direcciones de SMTP principales del usuario y cualquier dirección de proxy asociada. La dirección SMTP principal (también denominada *dirección de respuesta predeterminada* se muestra en negrita en la lista de direcciones, con el valor **SMTP** en mayúsculas en la columna **Tipo**.

  - **Agregar**  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una dirección de correo electrónico nueva para este buzón. Seleccione uno de los siguientes tipos de dirección:
    
      - **Dirección SMTP**   Este es el tipo de dirección predeterminado. Haga clic en este botón de opción y luego escriba la nueva dirección SMTP en la casilla **\* Dirección de correo electrónico**.
    
      - **EUM**   El servicio de mensajería unificada de Microsoft Exchange utiliza una dirección EUM (mensajería unificada de Exchange) para ubicar usuarios habilitados para MU en una organización de Exchange. Las direcciones EUM constan del número de extensión y el plan de marcado de MU para el usuario habilitado para MU. Haga clic en este botón de opción y escriba el número de extensión en el cuadro **Dirección/extensión**. Luego, haga clic en **Examinar** y seleccione un plan de marcado para el usuario.
    
      - **Tipo de dirección personalizada**   Haga clic en este botón y escriba uno de los tipos de dirección de correo electrónico que no sean SMTP admitidos en la casilla **\* Dirección de correo electrónico**.
        

        > [!NOTE]  
        > Con excepción de las direcciones X.400, Exchange no valida las direcciones personalizadas para comprobar el formato adecuado. Debe asegurarse de que la dirección personalizada que especifica cumpla los requisitos de formato para el tipo de dirección.



  - **Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada a este destinatario** Seleccione esta casilla si desea que las direcciones de correo electrónico del destinatario se actualicen automáticamente cuando se hayan realizado los cambios en las directivas de direcciones de correo electrónico de su organización. Esta casilla está activada de forma predeterminada.

## Características de buzón

Use la sección **Características de buzón** para ver o cambiar la configuración y las características de buzón siguientes:

  - **Directiva de uso compartido**   En este cuadro se muestra la directiva de uso compartido que se aplica al buzón. Las directivas de uso compartido permiten controlar la manera en que los usuarios de una organización comparten el calendario y la información de contacto con los usuarios externos a la organización de Exchange. La directiva de uso compartido predeterminada se asigna a los buzones cuando se crean. Para cambiar la directiva de uso compartido asignada al usuario, seleccione una directiva diferente en la lista desplegable.

  - **Directiva de asignación de roles**   En este cuadro se muestra la directiva de asignación de roles asignada al buzón. La directiva de asignación de roles especifica los roles de control de acceso basados en roles (RBAC) que se asignan al usuario y controla la configuración de buzones y de grupos de distribución que los usuarios pueden modificar. Para cambiar la directiva de asignación de roles asignada al usuario, seleccione una directiva diferente en la lista desplegable.

  - **Directiva de retención**   En este cuadro se muestra la directiva de retención asignada al buzón. Una directiva de retención es un grupo de etiquetas de retención que se aplica al buzón del usuario. Las etiquetas le permiten controlar cuánto tiempo mantener los elementos de los buzones de correo de los usuarios y definir qué acción realizar en los elementos que han alcanzado cierta edad. Las directivas de retención no se asignan a los buzones cuando se crean. Para asignar una directiva de retención al usuario, selecciónela en la lista desplegable.

  - **Directiva de libreta de direcciones**   En este cuadro se muestra la directiva de libreta de direcciones que se aplica al buzón. Una directiva de libreta de direcciones le permite segmentar a los usuarios en grupos específicos para proporcionar vistas personalizadas de la libreta de direcciones. Para aplicar o cambiar la directiva de libreta de direcciones aplicada al buzón, seleccione una de la lista desplegable.

  - **Mensajería unificada**   Esta función está deshabilitada de forma predeterminada. Al habilitar la mensajería unificada (MU), el usuario podrá usar las características de la MU de la organización y un conjunto predeterminado de propiedades de la misma se aplicarán al usuario. Haga clic en **Habilitar** para habilitar la mensajería unificada en el buzón. Para obtener información acerca de cómo habilitar la MU, consulte [Habilitar a un usuario para el correo de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).
    

    > [!NOTE]  
    > Para habilitar la mensajería unificada, debe tener un plan de marcado de mensajería unificada y una directiva de buzones de mensajería unificada.



  - **Dispositivos móviles**   Utilice esta sección para ver y cambiar las configuraciones de Exchange ActiveSync, que está habilitado de manera predeterminada. Exchange ActiveSync permite obtener acceso al buzón de Exchange desde dispositivos móviles. Haga clic en **Deshabilitar Exchange ActiveSync** para deshabilitar esta característica en el buzón.

  - **Outlook Web App**   Esta función está habilitada de forma predeterminada. Outlook Web App permite obtener acceso al buzón de Exchange desde cualquier explorador web. Haga clic en **Deshabilitar** para deshabilitar Outlook Web App en el buzón. Haga clic en **Editar detalles** para agregar o cambiar una directiva de buzones de Outlook Web App en el buzón.

  - **IMAP**   Esta función está habilitada de forma predeterminada. Haga clic en **Deshabilitar** para deshabilitar IMAP en buzón de correo.

  - **POP3**   Esta función está habilitada de forma predeterminada. Haga clic en **Deshabilitar** para deshabilitar POP3 en buzón de correo.

  - **MAPI**   Esta función está habilitada de forma predeterminada. MAPI permite obtener acceso a un buzón de Exchange desde un cliente MAPI, como Outlook. Haga clic en **Deshabilitar** para deshabilitar MAPI en buzón de correo.

  - **Retención por juicio**   Esta función está deshabilitada de forma predeterminada. La suspensión de litigio preserva los elementos de buzón eliminados y registra las modificaciones que se les realizaron a los elementos de buzón. Los elementos eliminados y todas las copias de los elementos modificados se devuelven en una búsqueda de detección. Haga clic en **Habilitar** para aplicar la retención por juicio en el buzón de correo. Si el buzón tiene una retención por juicio, haga clic en **Deshabilitar** para eliminar dicha retención. Si el buzón está retenido por juicio, haga clic en **Editar detalles** para ver y cambiar la siguiente configuración de retención por juicio:
    
      - **Fecha de retención**   Este cuadro de solo lectura indica la fecha y hora en que se retuvo el buzón por juicio.
    
      - **Retenido por**   En este cuadro de solo lectura se indica el usuario que retuvo el buzón por un juicio.
    
      - **Nota**   Use este cuadro para notificar al usuario la retención por juicio, explicar el motivo por el que se ha aplicado la retención por juicio al buzón de correo o proporcionar instrucciones adicionales al usuario, como por ejemplo informarle de que la retención por juicio no afectará al uso cotidiano del correo electrónico.
    
      - **URL**   Use este campo para indicar una dirección URL a un sitio web que ofrezca información o instrucciones acerca de la retención por juicio que tiene aplicada el buzón de correo.
        

        > [!NOTE]  
        > El texto de estos campos aparecen en el buzón de correo del usuario únicamente si usa Outlook 2010 o versiones posteriores. No aparece en Outlook Web App ni en otros clientes de correo electrónico. Para ver el texto de los cuadros Nota y URL en Outlook, haga clic en la ficha <STRONG>Archivo</STRONG> y, en la página <STRONG>Información</STRONG>, bajo <STRONG>Configuración de la cuenta</STRONG>, aparecerá el comentario de la retención por juicio.



  - **Archivado** Si no existe ningún buzón de correo de archivo para el usuario, esta característica está deshabilitada. Para habilitar un buzón de correo de archivo, haga clic en **Habilitar**. Si el usuario posee un buzón de archivo, se muestran el tamaño del buzón de archivo y las estadísticas de uso. Haga clic en **Editar detalles** para ver y cambiar la siguiente configuración de buzones de archivo:
    
      - **Estado**   En este cuadro de solo lectura se indica si existe un buzón de archivo.
    
      - **Base de datos**   En este cuadro de solo lectura se muestra el nombre de la base de datos de buzones que hospeda el buzón de archivo.
    
      - **Nombre**   Escriba el nombre del buzón de archivo en este cuadro. El nombre aparecerá debajo de la lista de carpetas en Outlook o en Outlook Web App.
    
      - **Uso de cuotas**   En esta sección de solo lectura se muestra el tamaño total del buzón de archivo y el porcentaje de la cuota total del buzón de archivo que se usó.
    
      - **Valor de cuota (GB)**   En este cuadro se muestra el tamaño total del buzón de archivo. Para cambiar el tamaño, escriba un valor nuevo en el cuadro o selecciónelo en la lista desplegable.
    
      - **Emitir advertencia al llegar a (GB)**   En este cuadro aparece el límite de almacenamiento máximo para el buzón de archivo antes de que se envíe una advertencia al usuario. Si el tamaño del buzón de archivo alcanza o supera el valor especificado, Exchange enviará un mensaje de advertencia al usuario. Para cambiar el límite, escriba un valor nuevo en el cuadro o selecciónelo en la lista desplegable.

  - **Opciones de entrega**   Utilice las Opciones de entrega para reenviar mensajes de correo electrónico a otros destinatarios y enviados al usuario, y para establecer el número máximo de destinatarios a los que el usuario puede enviar un mensaje. Haga clic en **Editar detalles** para ver y cambiar esta configuración.
    
      - **Dirección de reenvío**   Seleccione la casilla **Habilitar el reenvío** y, a continuación, haga clic en **Examinar** para ver la página **Seleccionar usuario de correo y buzón**. En esta página podrá seleccionar el destinatario al que desea reenviar todos los correos electrónicos que se envíen a este buzón. Los mensajes se entregarán tanto al buzón vinculado como a las direcciones de reenvío.
    
      - **Límite de destinatarios**   Esta configuración establece el número máximo de destinatarios a los que el usuario puede enviar un mensaje. Seleccione la casilla **Núm. máximo de destinatarios** para limitar el número de destinatarios permitidos en las líneas Para:, Cc: y Cco: de un correo electrónico y, a continuación, especifique el número máximo de destinatarios.
        

        > [!NOTE]  
        > Para las organizaciones locales de Exchange, el límite de destinatarios es ilimitado. Para las organizaciones de Exchange Online, el límite es de 500 destinatarios.



  - **Restricciones de tamaño de mensaje**   Estas configuraciones controlan el tamaño de los mensajes que el usuario puede enviar y recibir. Haga clic en **Ver detalles** para ver y cambiar el tamaño máximo de los mensajes enviados y recibidos.
    
      - **Mensajes enviados**   Para indicar el tamaño máximo de los mensajes enviados por este usuario, seleccione la casilla **Tamaño máximo de mensaje (en KB)** y escriba un valor en el cuadro. El tamaño del mensaje debe estar entre 0 y 2.097.151 KB. Si el usuario envía un mensaje que supera el tamaño indicado, se le devolverá con un mensaje de error descriptivo.
    
      - **Mensajes recibidos**   Para indicar el tamaño máximo de los mensajes recibidos por este usuario, seleccione la casilla **Tamaño máximo de mensaje (en KB)** y escriba un valor en el cuadro. El tamaño del mensaje debe estar entre 0 y 2.097.151 KB. Si el usuario recibe un mensaje que supera el tamaño indicado, se devuelve al emisor con un mensaje de error descriptivo.

  - **Restricción de entrega de mensajes**   Estas configuraciones controlan quién puede enviar mensajes de correo electrónico a este usuario. Haga clic en **Editar detalles** para ver y cambiar estas restricciones.
    
      - **Aceptar mensajes de**   Esta sección sirve para indicar quién puede enviar mensajes al usuario.
        
          - **Todos los remitentes**   Seleccione esta opción para especificar que el usuario puede aceptar mensajes de todos los remitentes. Se incluyen los remitentes de la organización de Exchange y los remitentes externos. Esta opción está seleccionada de forma predeterminada. Esta opción incluye a los usuarios externos solo si desactiva la casilla **Requerir la autenticación de todos los remitentes**. Si activa esta casilla, se rechazarán los mensajes de los usuarios externos.
        
          - **Solo los remitentes de la siguiente lista** Seleccione esta opción para especificar que el usuario puede aceptar mensajes únicamente de un grupo específico de remitentes de la organización de Exchange. Haga clic en **Agregar** para ver la página **Seleccionar destinatarios**, que muestra una lista de todos los destinatarios de la organización de Exchange. Seleccione los destinarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**.
        
          - **Requerir la autenticación de todos los remitentes**   Seleccione esta opción para impedir que usuarios anónimos envíen mensajes al usuario.
    
      - **Rechazar mensajes de**   Use esta sección para bloquear a ciertos usuarios y que no envíen mensajes al usuario.
        
          - **Ningún remitente**   Elija esta opción para especificar que el buzón no rechazará mensajes de ningún remitente de la organización de Exchange. Esta opción está seleccionada de forma predeterminada.
        
          - **Remitentes de la siguiente lista** Seleccione esta opción para especificar que el buzón rechazará mensajes de un grupo específico de remitentes de la organización de Exchange. Haga clic en **Agregar** para ver la página **Seleccionar destinatario**, que muestra una lista de todos los destinatarios de la organización de Exchange. Seleccione los destinarios cuyos mensajes desea rechazar, agréguelos a la lista y, a continuación, haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**.

## Miembro de

Utilice la sección **Miembro de** para ver una lista de los grupos de distribución o los grupos de seguridad a los que pertenece el usuario. La información de pertenencia no se puede cambiar en esta página. Tenga en cuenta que el usuario puede coincidir con los criterios de uno o más grupos de distribución dinámicos de la organización. No obstante, los grupos de distribución dinámicos no se muestran en esta página porque su pertenencia se calcula cada vez que se usan.

## Información sobre correo

Utilice la sección **Sugerencia de correo** para agregar una sugerencia de correo y avisar a los usuarios de posibles problemas si envían un mensaje a este destinatario. La información sobre correo es texto que se muestra en la barra de información cuando un destinatario se agrega a los campos Para, CC o CCO de un nuevo mensaje de correo electrónico.


> [!NOTE]  
> La información sobre correo puede incluir etiquetas HTML, pero no se permiten los scripts. La longitud de la información de una sugerencia de correo electrónico personalizada no puede superar los 175 caracteres mostrados. Las etiquetas HTML no se cuentan en el límite.



## Delegación de buzones

La sección **Delegación de buzones** sirve para asignar permisos a otros usuarios (también llamados *delegados*) y permitirles iniciar sesión en el buzón del usuario o enviar mensajes en su nombre. Se pueden asignar los siguientes permisos:

  - **Enviar como**   Esta configuración permite a aquellos usuarios que no sean el propietario usar el buzón para enviar mensajes. Después de asignar este permiso a un delegado, los mensajes que el delegado envíe desde el buzón aparecerán como si los hubiera enviado el propietario del buzón. Sin embargo, el delegado no podrá iniciar sesión en el buzón del usuario con este permiso.

  - **Enviar en nombre de**   Esta configuración también permite que un delegado use el buzón para enviar mensajes. No obstante, después de asignar este permiso a un delegado, la dirección del campo **De:**  de los mensajes enviados por el delegado indicará que el mensaje lo envió el delegado en nombre del propietario del buzón.

  - **Acceso completo**   Esta configuración permite que un delegado inicie sesión en el buzón del usuario y vea su contenido. Sin embargo, después de asignar este permiso a un delegado, no podrá enviar mensajes desde el buzón. Para que un delegado pueda enviar correos electrónicos desde el buzón del usuario, debe asignarle los permisos Enviar como o Enviar en nombre de.

Para asignar permisos a los delegados, haga clic en **Agregar** debajo del permiso adecuado para mostrar la página **Seleccionar destinatario**, que muestra una lista de todos los destinatarios en su organización de Exchange que pueden asignarse al permiso. Seleccione los destinarios a los que desea asignar permisos, agréguelos a la lista y, a continuación, haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**.

## Uso del Shell para cambiar las propiedades de los buzones vinculados

Use los cmdlets **Get-Mailbox** y **Set-Mailbox** para ver y cambiar las propiedades de los buzones vinculados. Una ventaja de usar el Shell es que puede cambiar las propiedades de varios buzones vinculados. Para obtener más información sobre los parámetros que corresponden a las propiedades del buzón, vea los siguientes temas:

  - [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\))

A continuación aparecen algunos ejemplos de cómo usar el Shell para cambiar las propiedades del buzón.

En este ejemplo se utiliza el comando **Get-Mailbox** para buscar todos los buzones vinculados de la organización.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')}

En este ejemplo se utiliza el comando **Set-Mailbox** para limitar el número de destinatarios permitidos en las líneas Para:, Cc: y Cco: de un mensaje de correo electrónico a 500. Este límite se aplica a todos los buzones vinculados de la organización.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | Set-Mailbox -RecipientLimits 500

En este ejemplo se cambia la cuenta maestra vinculada del bosque de cuentas fabrikam.com que está asociada al buzón vinculado de un bosque de Exchange.

    Set-Mailbox -Identity "Ayla Kol" -LinkedDomainController DC1.fabrikam.com -LinkedMasterAccount "fabrikam\robinw" -LinkedCredential:(Get-Credential fabrikam\administrator)

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si cambió las propiedades de un buzón vinculado correctamente, haga lo siguiente:

  - En el EAC, seleccione el buzón vinculado y haga clic en **Editar** para visualizar la propiedad o característica que ha modificado. Según la propiedad que cambie, puede aparecer en el panel Detalles del buzón seleccionado.

  - En el Shell, use el cmdlet **Get-Mailbox** para verificar los cambios. Una de las ventajas de usar el Shell es que puede ver diferentes propiedades para varios buzones vinculados. En el ejemplo anterior en el que se cambió el límite de destinatarios, ejecute el siguiente comando para comprar el valor nuevo.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | fl Name,RecipientLimits
    
    En el ejemplo anterior en el que se cambió la cuenta maestra vinculada, ejecute el siguiente comando para comprar el valor nuevo.
    
    ```powershell
Get-Mailbox "Ayla Kol" | fl LinkedMasterAccount
```

