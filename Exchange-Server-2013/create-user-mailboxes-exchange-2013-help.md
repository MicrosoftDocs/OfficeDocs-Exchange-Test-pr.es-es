---
title: 'Crear buzones de usuario: Exchange 2013 Help'
TOCTitle: Crear buzones de usuario
ms:assetid: 51a8b4c6-a53e-41c5-8bb1-ea4c0eaa0174
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ991919(v=EXCHG.150)
ms:contentKeyID: 52062026
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear buzones de usuario

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2013-04-12_

Los buzones son el tipo de destinatario más frecuente que usan las personas que trabajan con datos en una organización de Exchange. Cada buzón está asociado a una cuenta de usuario de Active Directory. El usuario puede usar el buzón para enviar y recibir mensajes, así como para almacenar mensajes, citas, tareas, notas y documentos. Use el EAC o el Shell para crear buzones de correo de usuarios.

También puede crear buzones para los usuarios existentes que tengan una cuenta de usuario de Active Directory pero no un buzón correspondiente. Esto se conoce como *habilitar un buzón* para usuarios existentes.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada tarea de buzón de usuario: 2 a 5 minutos.

  - Cuando crea un buzón de usuario nuevo, no puede usar un apóstrofo (') ni comillas (") en el alias o nombre de inicio de sesión del usuario porque no están admitidos estos caracteres. Aunque podría no recibir un error si crea un nuevo buzón con caracteres no admitidos, estos caracteres pueden producir problemas más adelante. Por ejemplo, los usuarios que tienen asignados permisos de acceso para un buzón creado con un carácter no admitido pueden experimentar problemas o un comportamiento inesperado.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Crear un buzón de usuario

## Usar el EAC para crear un buzón de usuario

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  Haga clic en **Nuevo** \> **Buzón de usuario**.

3.  En la página **Nuevo buzón de usuario**, en el cuadro **Alias**, escriba el alias del usuario, que especifica el alias de correo electrónico del usuario. El alias del usuario es la porción de la dirección de correo electrónico ubicada a la izquierda del símbolo arroba (@). Debe ser exclusivo en el bosque.
    

    > [!NOTE]
    > Si deja este cuadro vacío, se usa para el alias de correo electrónico el valor de la parte del nombre de usuario del <STRONG>Nombre de inicio de sesión del usuario</STRONG>.



4.
    Seleccione una de las opciones para:
    
      - **Usuario existente**   Seleccione habilitar el correo y crear un buzón para un usuario existente.
        
        Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar usuario – Todo el bosque**. Este cuadro de diálogo muestra una lista de cuentas de usuario de Active Directory del bosque que no están habilitadas para correo o no tienen buzones de Exchange. Seleccione la cuenta de usuario que desee habilitar para correo y, a continuación, haga clic en **Aceptar**. Si selecciona esta opción, no es necesario proporcionar información de la cuenta del usuario debido a que esa información ya existe en Active Directory.
    
      - **Nuevo usuario**   Seleccione crear una nueva cuenta de usuario en Active Directory y cree un buzón para el mismo. Si selecciona esta opción, tendrá que proporcionar la información de la cuenta del usuario que se requiera.
    

    > [!NOTE]
    > La cuenta de Active Directory&nbsp;que está asociada a los buzones de usuario debe residir en el mismo bosque que el servidor de Exchange. Para crear un buzón para una cuenta de usuario que está en un bosque de confianza, debe crear un buzón vinculado. Vea <A href="manage-linked-mailboxes-exchange-2013-help.md">Administrar buzones vinculados</A>.



5.      
    Si seleccionó **Nuevo usuario** en el paso 4, complete los siguientes cuadros en la página **Buzón de nuevo usuario**. De lo contrario, vaya al Paso 7.
    
      - **Nombre**   Use este cuadro para escribir el nombre del usuario.
    
      - **Iniciales**   Use este cuadro para escribir las iniciales del usuario.
    
      - **Apellido**   Use este cuadro para escribir el apellido del usuario.
    
      - **\* Nombre para mostrar**   Use este cuadro para escribir el nombre para mostrar para el usuario. Este es el nombre que se incluye en la lista de buzones de EAC y en la libreta de direcciones compartida. Este cuadro se rellena de forma predeterminada con los nombres que escribe en los cuadros **Nombre**, **Iniciales** y **Apellido**. Aunque no haya usado dichos cuadros, debe escribir un nombre en este cuadro, ya que es obligatorio. El nombre no puede superar los 64 caracteres.
    
      - **\* Nombre**   Use este cuadro para escribir un nombre para el usuario. Se trata del nombre indicado en Active Directory. Este cuadro también se rellena de forma predeterminada con los nombres que escribe en los cuadros **Nombre**, **Iniciales** y **Apellido**. Aunque no haya usado dichos cuadros, debe escribir un nombre, ya que este cuadro es obligatorio. Este nombre tampoco puede superar los 64 caracteres.
    
      - **Unidad organizativa**   Se puede seleccionar una unidad organizativa (OU) que no sea la predeterminada (que es el ámbito del destinatario). Si el ámbito de destinatario definido corresponde al bosque, el valor predeterminado será el contenedor Usuarios del dominio de Active Directory que contiene el equipo en el que se ejecuta EAC. Si el ámbito del destinatario está establecido en un dominio específico, el contenedor de usuarios se selecciona de modo predeterminado. Si el ámbito del destinatario está establecido en una unidad organizativa específica (OU), esa OU se selecciona de modo predeterminado.
        
        Para seleccionar otra OU, haga clic en **Examinar**. En el cuadro de diálogo se muestran todas las OU del bosque dentro del ámbito especificado. Seleccione la unidad organizativa y haga clic en **Aceptar**.
    
      - **\* Nombre de inicio de sesión del usuario**   Use este cuadro para escribir el nombre que usará el usuario para iniciar sesión en el buzón y en el dominio. El nombre de inicio de sesión del usuario consta de un nombre de usuario a la izquierda del símbolo arroba (@) y un sufijo a la derecha. Por lo general, el sufijo es el nombre de dominio en el que reside la cuenta de usuario. Tenga en cuenta que no puede usar un apóstrofo (') ni comillas (") en el nombre de inicio de sesión del usuario porque no están admitidos estos caracteres.
        

        > [!NOTE]
        > Si el valor del nombre de usuario es diferente al valor usado en el cuadro <STRONG>Alias</STRONG>, la dirección de correo electrónico del usuario y el nombre de inicio de sesión de usuario serán diferentes.

    
      - **\* Nueva contraseña**   Use este cuadro para escribir la contraseña que el usuario debe usar para iniciar sesión en el buzón.
        

        > [!NOTE]
        > Asegúrese de que la contraseña que proporciona cumple los requisitos de longitud, complejidad e historial de la contraseña del dominio en el que va a crear la cuenta de usuario.

    
      - **\* Confirmar contraseña**   Use este cuadro para confirmar la contraseña que escribió en el cuadro **Contraseña**.
    
      - **Requerir cambio de contraseña en el próximo inicio de sesión**   Seleccione esta casilla de verificación si desea que el usuario restablezca la contraseña cuando inicie sesión por primera vez en el buzón.
        
        Si activa esta casilla de verificación, la primera vez que el nuevo usuario inicie una sesión se le pedirá que cambie la contraseña mediante un cuadro de diálogo. El usuario no podrá realizar ninguna tarea hasta que haya modificado la contraseña correctamente.

6.      
    Haga clic en **Más opciones** para configurar los siguientes cuadros. De lo contrario, vaya al Paso 7 para guardar el buzón de nuevo usuario.
    
      - **Especificar la base de datos de buzones**   Use esta opción para especificar una base de datos de buzones en vez de permitir que Exchange seleccione la base de datos. Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar base de datos de buzones**. En este cuadro de diálogo se enumeran todas las bases de datos de buzones de la organización de Exchange. De manera predeterminada, las bases de datos de buzones se ordenan por el nombre. También puede hacer clic en el título de la columna correspondiente para ordenar las bases de datos por versión o nombre del servidor. Seleccione la base de datos de buzones que desee usar y haga clic en **Aceptar**.
    
      - **Crear almacenamiento de archivo local para este usuario**   Seleccione esta casilla de verificación para crear un buzón de archivo para el buzón. Si crea un buzón de archivo, los objetos del buzón se moverán automáticamente del buzón de usuario primario al archivo, según las configuración de directiva de retención predeterminada o la que defina.
        
        Haga clic en **Examinar** para seleccionar una base de datos que resida en el bosque local para almacenar el buzón de archivo.
        
        Para obtener más información, consulte [Archivado local en Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Directiva de la libreta de direcciones**   Utilice esta opción para especificar una directiva de libreta de direcciones (ABP) para el buzón. Las ABP contienen una lista global de direcciones (GAL), una libreta de direcciones sin conexión (OAB), una lista de salas y un conjunto de listas de direcciones. Cuando se asigna una ABP a usuarios de buzones, les proporciona acceso a una GAL personalizada en Outlook y Outlook Web App. Para obtener más información, consulte [Directivas de la libreta de direcciones](address-book-policies-exchange-2013-help.md).
        
        En la lista desplegable, seleccione la directiva que desea asociar con este buzón.

7.  
    
    Cuando haya terminado, haga clic en **Guardar** para crear el buzón.

## Usar el Shell para crear un buzón de usuario

En este ejemplo se crea una cuenta y un buzón de usuario nuevos para Pilar Pinilla con los detalles siguientes:

  - El alias es pilarp

  - El nombre es Pilar y el apellido es Pinilla

  - El nombre y el nombre para mostrar es Pilar Pinilla

  - El nombre de inicio de sesión de usuario es pilarp@contoso.com

  - La contraseña es Pa$$word1

  - El buzón se creará en la OU predeterminada. Para especificar una OU distinta, puede usar el parámetro *OrganizationalUnit*.

<!-- end list -->

    New-Mailbox -Alias pilarp -Name "Pilar Pinilla" -FirstName Pilar -LastName Pinilla -DisplayName "Pilar Pinilla" -UserPrincipalName pilarp@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

Para obtener información acerca de la sintaxis y los parámetros, consulte [New-Mailbox](https://technet.microsoft.com/es-es/library/aa997663\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó un buzón de usuario correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Buzones de correo**. El buzón de nuevo usuario aparece en la lista de buzones. Bajo **Tipo de buzón de correo**, el tipo es **Usuario**.

  - En el Shell, ejecute el comando siguiente para mostrar información sobre el nuevo buzón del nuevo usuario.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Crear un buzón para un usuario existente

También puede crear buzones para los usuarios existentes que tengan una cuenta de usuario de Active Directory pero no un buzón correspondiente. Esto se conoce como *habilitar un buzón* para usuarios existentes. Tras haber habilitado el buzón de un usuario existente, éste podrá enviar y recibir mensajes de correo electrónico.

## Usar el EAC para crear un buzón para un usuario existente

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  Haga clic en **Nuevo** \> **Buzón de usuario**.

3.  En la página **Nuevo buzón de usuario**, en el cuadro **Alias**, escriba el alias del usuario, que especifica el alias de correo electrónico del usuario. El alias del usuario es la porción de la dirección de correo electrónico ubicada a la izquierda del símbolo arroba (@). Debe ser exclusivo en el bosque.
    

    > [!NOTE]
    > Si deja este cuadro vacío, se usa para el alias de correo electrónico el valor de la parte del nombre de usuario del <STRONG>Nombre de inicio de sesión del usuario</STRONG>.



4.  Haga clic en **Usuario existente**.

5.  Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar usuario – Todo el bosque**. Este cuadro de diálogo muestra una lista de cuentas de usuario de Active Directory del bosque que no están habilitadas para correo o no tienen buzones de Exchange. Seleccione la cuenta de usuario que desee habilitar para correo y, a continuación, haga clic en **Aceptar**.
    
    Al crear un buzón para un usuario existente, no tiene que proporcionar información de la cuenta porque ésta ya existe en Active Directory.
    

    > [!NOTE]
    > La cuenta de Active Directory&nbsp;que está asociada a los buzones de usuario debe residir en el mismo bosque que el servidor de Exchange. Para crear un buzón para una cuenta de usuario que está en un bosque de confianza, debe crear un buzón vinculado. Vea <A href="manage-linked-mailboxes-exchange-2013-help.md">Administrar buzones vinculados</A>.



6.  Haga clic en **Más opciones** para configurar los siguientes cuadros. De lo contrario, vaya al Paso 7 para guardar el buzón de nuevo usuario.
    
      - **Especificar la base de datos de buzones**   Use esta opción para especificar una base de datos de buzones en vez de permitir que Exchange la seleccione. Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar base de datos de buzones**. En este cuadro de diálogo se enumeran todas las bases de datos de buzones de la organización de Exchange. De manera predeterminada, las bases de datos de buzones se ordenan por el nombre. También puede hacer clic en el título de la columna correspondiente para ordenar las bases de datos por versión o nombre del servidor. Seleccione la base de datos de buzones que desee usar y haga clic en **Aceptar**.
    
      - **Crear almacenamiento de archivo local para este usuario**   Seleccione esta casilla de verificación para crear un buzón de archivo para el buzón. Si crea un buzón de archivo, los objetos del buzón se moverán automáticamente del buzón de usuario primario al archivo, según las configuración de directiva de retención predeterminada o la que defina.
        
        Haga clic en **Examinar** para seleccionar una base de datos que resida en el bosque local para almacenar el buzón de archivo.
        
        Para obtener más información, consulte [Archivado local en Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Directiva de la libreta de direcciones**   Utilice esta opción para especificar una directiva de libreta de direcciones (ABP) para el buzón. Las ABP contienen una lista global de direcciones (GAL), una libreta de direcciones sin conexión (OAB), una lista de salas y un conjunto de listas de direcciones. Cuando se asigna una ABP a usuarios de buzones, les proporciona acceso a una GAL personalizada en Outlook y Outlook Web App. Para obtener más información, consulte [Directivas de la libreta de direcciones](address-book-policies-exchange-2013-help.md).
        
        En la lista desplegable, seleccione la directiva que desea asociar con este buzón.

7.  Cuando haya terminado, haga clic en **Guardar** para crear el buzón.

## Usar el Shell para crear un buzón para un usuario existente

En este ejemplo se crea un buzón para el usuario existente estherv@contoso.com en la base de datos de Exchange denominada UsersMailboxDatabase.

    Enable-Mailbox estherv@contoso.com -Database UsersMailboxDatabase

Además, puede usar el cmdlet **Enable-Mailbox** para habilitar para correo a varios usuarios. Para ello, se deben canalizar los resultados del cmdlet **Get-User** en el cmdlet **Enable-Mailbox**. Cuando ejecute el cmdlet **Get-User**, deberá devolver solo los usuarios que ya no estén habilitados para correo. Para ello, es necesario especificar el valor Usuario con el parámetro *RecipientTypeDetails*. Además, podrá limitar los resultados devueltos mediante el parámetro *Filter* para solicitar solamente los usuarios que cumplan con los criterios que especifique. A continuación, canalice los resultados al cmdlet **Enable-Mailbox**.

Por ejemplo, el comando siguiente habilita el buzón para usuarios que todavía no tienen correo habilitado y que tienen un valor en la propiedad **UserPrincipalName**, lo que le ayuda a no convertir de forma inadvertida una cuenta de sistema en un buzón.

    Get-User -RecipientTypeDetails User -Filter { UserPrincipalName -ne $Null } | Enable-Mailbox

Para obtener información acerca de la sintaxis y los parámetros, consulte [Enable-Mailbox](https://technet.microsoft.com/es-es/library/aa998251\(v=exchg.150\)) y [Get-User](https://technet.microsoft.com/es-es/library/aa996896\(v=exchg.150\)).

Para obtener más información acerca de la canalización, consulte [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó correctamente un buzón para un usuario existente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Buzones de correo**. El nuevo usuario habilitado con buzón aparece en la lista de buzones. Bajo **Tipo de buzón de correo**, el tipo es **Usuario**.

  - En el Shell, ejecute el comando siguiente para mostrar información sobre el nuevo usuario con buzón habilitado.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
    
    Tenga en cuenta que el valor de la propiedad *RecipientTypeDetails* es `UserMailbox`.

