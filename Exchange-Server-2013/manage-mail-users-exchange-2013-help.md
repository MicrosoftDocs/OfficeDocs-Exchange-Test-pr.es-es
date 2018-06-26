---
title: 'Administrar usuarios de correo: Exchange 2013 Help'
TOCTitle: Administrar usuarios de correo
ms:assetid: bb8b8804-f730-4ad7-9173-896a4965b90f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124381(v=EXCHG.150)
ms:contentKeyID: 48268610
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailUserWizardForm.NewMailUserIntroductionWizardPage
ms.translationtype: HT
---

# Administrar usuarios de correo

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Los usuarios de correo son similares a los contactos de correo. Ambos tienen direcciones de correo electrónico externas y contienen información acerca de personas no pertenecientes a la organización de Exchange o de Exchange Online que se puede mostrar en la libreta de direcciones compartida y en otras listas de direcciones. No obstante, a diferencia de un contacto de correo, un usuario de correo tiene credenciales de inicio de sesión de la organización de Exchange o de Office 365 y puede tener acceso a los recursos. Para obtener más información, consulte [Destinatarios](recipients-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Crear un usuario de correo

## Uso de EAC para crear usuarios de correo

1.  En el EAC, vaya a **Destinatarios**  \> **Contactos** \> **Nuevo** \> **Usuario de correo**.

2.  En la página **Nuevo usuario de correo**, en el cuadro **\* Alias**, escriba el alias para el usuario de correo. El alias no puede superar 64 caracteres y debe ser único en el bosque. Este cuadro es obligatorio.

3.  Realice uno de lo siguiente para especificar el tipo de dirección de correo electrónico para el usuario de correo:
    
      - Para especificar una dirección de correo electrónico SMTP para la dirección de correo electrónico externa del usuario de correo, haga clic en **SMTP**.
        

        > [!NOTE]
        > Exchange valida las direcciones SMTP para comprobar el formato adecuado. Si la entrada no coincide con el formato SMTP, se muestra un mensaje de error al hacer clic en <STRONG>Guardar</STRONG> para crear un usuario de correo.

    
      - Para especificar un tipo de dirección personalizada, haga clic en el botón de opción y luego escriba el tipo de dirección personalizada. Por ejemplo, puede especificar una dirección X.500, GroupWise o Lotus Notes.

4.  En el cuadro **\* Dirección de correo electrónico externa**, escriba la dirección de correo electrónico externa del usuario de correo. El correo electrónico que se envíe a este usuario de correo electrónico se reenviará a esta dirección de correo electrónico. Este cuadro es obligatorio.

5.  
    
    Seleccione una de las opciones para:
    
      - **Usuario existente**   Seleccione esta opción para habilitar el correo de un usuario existente.
        
        Haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar usuario – Todo el bosque**. Este cuadro de diálogo muestra una lista de cuentas de usuario de la organización que no están habilitadas para correo o que no tienen buzones de correo. Seleccione la cuenta de usuario que desee habilitar para correo y, a continuación, haga clic en **Aceptar**. Si selecciona esta opción, no es necesario proporcionar información de la cuenta del usuario debido a que esa información ya existe en Active Directory.
    
      - **Nuevo usuario**   Seleccione esta opción para crear una nueva cuenta del usuario en Active Directory y habilitar para correo al usuario. Si selecciona esta opción, tendrá que proporcionar la información de la cuenta del usuario que se requiera.

6.  
    
    Si seleccionó **Nuevo usuario** en el paso 5, complete los siguientes cuadros en la página **Nuevo usuario de correo**. De lo contrario, vaya al Paso 7.
    
      - **Nombre**   Use este cuadro para escribir el nombre del usuario de correo.
    
      - **Iniciales**   Use este cuadro para escribir las iniciales del usuario de correo.
    
      - **Apellido**   Use este cuadro para escribir el apellido del usuario de correo.
    
      - **\* Nombre para mostrar**   Use este cuadro para escribir el nombre para mostrar para el usuario. Este es el nombre que se incluye en la lista de contactos de EAC y en la libreta de direcciones de la organización. Este cuadro se rellena de forma predeterminada con los nombres que escribe en los cuadros **Nombre**, **Iniciales** y **Apellido**. Aunque no haya usado dichos cuadros, debe escribir un nombre en este cuadro, ya que es obligatorio. El nombre no puede superar los 64 caracteres.
    
      - **\* Nombre**   Use este cuadro para escribir el nombre del usuario de correo. Se trata del nombre que se muestra en el servicio de directorio. Este cuadro se rellena con los nombres que escribe en los cuadros **Nombre**, **Iniciales** y **Apellido**. Aunque no haya usado dichos cuadros, debe escribir un nombre, ya que este cuadro es obligatorio. Este nombre tampoco puede superar los 64 caracteres.
        

        > [!NOTE]
        > El cuadro <STRONG>Nombre</STRONG> solo está disponible en Exchange Server 2013. No está disponible en Exchange Online.

    
      - **Unidad organizativa**   Se puede seleccionar una unidad organizativa (OU) que no sea la predeterminada (que es el ámbito del destinatario). Si el ámbito del destinatario definido corresponde al bosque, el valor predeterminado será el contenedor de usuarios del dominio que contiene el equipo en el que se ejecuta el EAC. Si el ámbito del destinatario está establecido en un dominio específico, el contenedor de usuarios se selecciona de modo predeterminado. Si el ámbito del destinatario está establecido en una unidad organizativa específica (OU), esa OU se selecciona de modo predeterminado.
        
        Para seleccionar otra OU, haga clic en **Examinar**. En el cuadro de diálogo se muestran todas las OU del bosque dentro del ámbito especificado. Seleccione la unidad organizativa que desee y haga clic en **Aceptar**.
        

        > [!NOTE]
        > El cuadro <STRONG>Unidad organizativa</STRONG> solo está disponible en Exchange Server 2013. No está disponible en Exchange Online.

    
      - **\* Nombre de inicio de sesión de usuario**   Use este cuadro para escribir el nombre que el usuario de correo usará para iniciar sesión en el dominio. El nombre de inicio de sesión del usuario consta de un nombre de usuario a la izquierda del símbolo arroba (@) y un sufijo a la derecha. Por lo general, el sufijo es el nombre de dominio en el que reside la cuenta de usuario.
        

        > [!NOTE]
        > En Exchange Online, este cuadro se etiqueta como <STRONG>Id. de usuario</STRONG>.

    
      - **\* Nueva contraseña**   Use este cuadro para escribir la contraseña que el usuario de correo debe usar para iniciar sesión en el dominio.
        

        > [!NOTE]
        > Asegúrese de que la contraseña que proporciona cumple los requisitos de longitud, complejidad e historial de la contraseña del dominio en el que está creando la cuenta de usuario.

    
      - **\* Confirmar contraseña**   Use este cuadro para confirmar la contraseña que escribió en el cuadro **Contraseña**.
    
      - **Requerir cambio de contraseña en el próximo inicio de sesión**   Seleccione este cuadro de verificación si desea que el usuario de correo restablezca la contraseña cuando inicie sesión por primera vez en el dominio.
        
        Si activa este cuadro, la primera vez que el nuevo usuario de correo inicie una sesión aparecerá un cuadro de diálogo en el que se le solicitará que cambie la contraseña. El usuario de correo no podrá realizar ninguna tarea hasta que haya cambiado la contraseña correctamente.

7.  
    
    Cuando haya terminado, haga clic en **Guardar** para crear el usuario de correo.

## Uso del Shell para crear usuarios de correo

En este ejemplo, se crea una cuenta de usuario habilitada para correo para Jeffrey Zeng en Exchange Server 2013 con los siguientes detalles:

  - El nombre y el nombre para mostrar es Jeffrey Zeng.

  - El alias es jeffreyz.

  - La dirección de correo electrónico externa es jzeng@tailspintoys.com.

  - El nombre es Jeffrey y el apellido es Zeng.

  - El nombre de inicio de sesión es jeffreyz@contoso.com.

  - La contraseña es Pa$$word1.

  - El usuario de correo se creará en la OU predeterminada. Para especificar una OU distinta, puede usar el parámetro *OrganizationalUnit*.

<!-- end list -->

    New-MailUser -Name "Jeffrey Zeng" -Alias jeffreyz -ExternalEmailAddress jzeng@tailspintoys.com -FirstName Jeffrey -LastName Zeng -UserPrincipalName jeffreyz@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

En este ejemplo se crea una cuenta de usuario con correo habilitado para Rene Valdes en Exchange Online.

    New-MailUser -Name "Rene Valdes" -Alias renev -ExternalEmailAddress renevaldes@fineartschool.edu -FirstName Rene -LastName Valdes -MicrosoftOnlineServicesID renev@contoso.com -Password (ConvertTo-SecureString -String 'P@ssw0rd' -AsPlainText -Force)

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó un usuario de correo correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Contactos**. El nuevo usuario de correo aparece en la lista de contactos. En **Tipo de contacto**, el tipo es **Usuario de correo**.

  - En el Shell, ejecute el siguiente comando para mostrar información acerca del nuevo usuario de correo.
    
        Get-MailUser <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## Cambiar las propiedades de usuario de correo

Después de haber creado un usuario de correo, puede hacer cambios y configurar propiedades adicionales mediante el uso del EAC o del Shell.

También puede cambiar las propiedades de varios buzones de usuario al mismo tiempo. Para obtener más información, consulte Uso del EAC para editar masivamente usuarios de correo.

El tiempo estimado para completar esta tarea variará en función de la cantidad de propiedades que desee ver o cambiar.

## Uso de la Consola de administración de Exchange para cambiar las propiedades de los buzones de usuario

1.  En el EAC, vaya a **Destinatarios** \> **Contactos**.

2.  En la lista de contactos, haga clic en el usuario de correo al que quiera cambiarle las propiedades y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del usuario de correo, haga clic en una de las siguientes secciones para ver o cambiar las propiedades.
    
      - General
    
      - Información de contacto
    
      - Organización
    
      - Direcciones de correo electrónico
    
      - Configuración de flujo de correo
    
      - Miembro de
    
      - Información sobre correo

## General

Use la sección **General** para ver o cambiar información básica del usuario de correo.

  - **Nombre**, **Iniciales**, **Apellido**

  - **\* Nombre**   Se trata del nombre indicado en Active Directory. Si cambia este nombre, no debe superar los 64 caracteres.

  - **\* Nombre para mostrar**    Este nombre aparece en la libreta de direcciones de la organización, en Para: y De: líneas en el correo electrónico y en la lista de contactos en el EAC. Este nombre no puede contener espacios en blanco antes o después del nombre para mostrar.

  - **\* Nombre de inicio de sesión de usuario**   El usuario puede utilizar este nombre para iniciar sesión en el dominio. En Exchange Online, este es el identificador de usuario que el usuario usa para iniciar sesión en Office 365.

  - **Ocultar de las listas de direcciones**   Seleccione este cuadro para evitar que el usuario de correo aparezca en la lista de direcciones y en otras listas de direcciones definidas en su organización de Exchange. Cuando active esta casilla, los usuarios aún podrán enviar mensajes al destinatario mediante la dirección de correo electrónico.

  - **Requerir cambio de contraseña en el próximo inicio de sesión**   Seleccione este cuadro de verificación si desea que el usuario restablezca la contraseña la próxima vez que inicie sesión en el dominio.
    

    > [!NOTE]
    > Este cuadro no está disponible en Exchange Online.



Haga clic en **Más opciones** para ver o cambiar estas propiedades adicionales:

  - **Unidad organizativa**   Este cuadro de solo lectura muestra la unidad organizativa (OU) que contiene la cuenta de usuario de correo. Debe usar usuarios de Active Directory y equipos para mover la cuenta a otra unidad organizativa.
    

    > [!NOTE]
    > Este cuadro no está disponible en Exchange Online.



  - **Atributos personalizados**   En esta sección se muestran los atributos personalizados definidos por el usuario de correo. Para especificar los valores de los atributos personalizados, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Se pueden especificar hasta 15 atributos personalizados para el destinatario.

## Información de contacto

Use la sección **Información de contacto** para ver o cambiar la información de contacto del usuario. La información de esta página se muestra en la libreta de direcciones. Haga clic en **Más opciones** para mostrar cuadros adicionales.


> [!TIP]
> Puede usar el cuadro <STRONG>Estado o provincia</STRONG> para crear condiciones de destinatario para grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones.



## Organización

Use la sección **Organización** para registrar información detallada acerca de la función del usuario en la organización. Esta información se muestra en la libreta de direcciones. Asimismo, puede crear un gráfico de organización virtual al que se pueda obtener acceso desde clientes de correo electrónico como Outlook.

  - **Título   **Use este cuadro para ver o cambiar el título del destinatario.

  - **Departamento** Use este cuadro para ver o cambiar el departamento en el que trabaja el usuario. Puede usar este cuadro para crear condiciones de destinatario para grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones.

  - **Compañía** Use este cuadro para ver o cambiar la compañía en la que trabaja el usuario. Puede usar este cuadro para crear condiciones de destinatario para grupos de distribución dinámicos, directivas de direcciones de correo electrónico o listas de direcciones.

  - **Administrador**   Para agregar un administrador, haga clic en **Examinar**. En **Seleccionar administrador**, seleccione una persona y, a continuación, haga clic en **Aceptar**.

  - **Informes directos**   Este cuadro no se puede modificar. Un *subordinado directo* es un usuario que está bajo las órdenes de un administrador específico. En caso de que haya indicado un administrador para el usuario, ese buzón de correo se mostrará como subordinado directo en la información del buzón de correo del administrador en cuestión. Por ejemplo, Kari administra a Chris y Kate, por lo tanto Kari está especificada en el cuadro **Administrador** para Chris y Kate, y Chris y Kate aparecen en el cuadro **Informes directos** en las propiedades de la cuenta de Kari.

## Direcciones de correo electrónico

Use la sección **Direcciones de correo electrónico** para ver o cambiar las direcciones de correo electrónico asociadas con el usuario de correo. Esto incluye la dirección SMTP principal del usuario de correo, las direcciones de correo electrónico externas y todas las direcciones proxy asociadas. La dirección SMTP principal (también denominada *dirección de respuesta predeterminada*) se muestra en negritas en la lista de direcciones, con el valor **SMTP** en mayúsculas en la columna **Tipo**. De manera predeterminada, después de que se crea el usuario de correo, la dirección SMTP principal y la dirección de correo electrónico externa son iguales.

  - **Agregar **  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una dirección de correo electrónico nueva para este buzón de correo. Seleccione uno de los siguientes tipos de dirección:
    
      - **SMTP**   Este es el tipo de dirección predeterminado. Haga clic en este botón y luego escriba la nueva dirección SMTP en el cuadro **\* Dirección de correo electrónico**.
    
      - **Tipo de dirección personalizada**   Haga clic en este botón y escriba uno de los tipos de dirección de correo electrónico que no sean SMTP admitidos en el cuadro de texto **\* Dirección de correo electrónico**.
        

        > [!NOTE]
        > Con excepción de las direcciones X.400, Exchange no valida las direcciones personalizadas para comprobar el formato correcto. Debe asegurarse de que la dirección personalizada que especifica cumpla los requisitos de formato para el tipo de dirección.



  - **Configure la dirección de correo electrónico externa**   Use este cuadro para cambiar la dirección externa del usuario de correo. El correo electrónico que se envíe a este usuario de correo electrónico se reenviará a esta dirección de correo electrónico.

  - **Actualizar automáticamente las direcciones de correo electrónico según la directiva de dirección de correo electrónico aplicada al destinatario.**   Seleccione esta casilla para que las direcciones de correo electrónico del destinatario se actualicen automáticamente según los cambios realizados en las directivas de direcciones de correo electrónico de su organización. Esta casilla está activada de forma predeterminada.
    

    > [!NOTE]
    > Esta casilla no está disponible en Exchange Online.



## Configuración de flujo de correo

Use la **Configuración de flujo de correo** para ver o cambiar la siguiente configuración:

  - **Restricciones en el tamaño de mensajes**   Estas configuraciones controlan el tamaño de los mensajes que el usuario de correo puede enviar y recibir. Haga clic en **Ver detalles** para ver y cambiar el tamaño máximo de los mensajes enviados y recibidos.
    
      - **Mensajes enviados**   Para indicar el tamaño máximo de los mensajes enviados por este usuario, active la casilla **Tamaño máximo de mensaje (en KB)** y escriba un valor en el cuadro. El tamaño del mensaje debe estar entre 0 y 2.097.151 KB. Si el usuario envía un mensaje que supera el tamaño indicado, se le devolverá con un mensaje de error descriptivo.
    
      - **Mensajes recibidos**   Para indicar el tamaño máximo de los mensajes recibidos por este usuario, active la casilla **Tamaño máximo de mensaje (en KB)** y escriba un valor en el cuadro. El tamaño del mensaje debe estar entre 0 y 2.097.151 KB. Si el usuario recibe un mensaje que supera el tamaño indicado, se devuelve al emisor con un mensaje de error descriptivo.

  - **Restricciones en la entrega de mensajes**   Estas configuraciones controlan quién puede enviar mensajes de correo electrónico a este usuario de correo. Haga clic en **Ver detalles** para ver y cambiar esta restricción.
    
      - **Aceptar mensajes de**   Esta sección sirve para indicar quién puede enviar mensajes a este usuario.
        
          - **Todos los remitentes**   Seleccione esta opción para especificar que el usuario puede aceptar mensajes de todos los remitentes. Se incluyen los remitentes de la organización de Exchange y los remitentes externos. Esta opción está seleccionada de forma predeterminada. Esta opción incluye a los usuarios externos solo si desactiva la casilla **Requerir la autenticación de todos los remitentes**. Si activa esta casilla, se rechazarán los mensajes de los usuarios externos.
        
          - **Solo los remitentes de la siguiente lista** Seleccione esta opción para especificar que el usuario puede aceptar mensajes únicamente de un grupo específico de remitentes de la organización de Exchange. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")para mostrar la página **Seleccionar destinatarios**, que muestra una lista de todos los destinatarios en la organización de Exchange. Seleccione los destinarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").
        
          - **Requerir la autenticación de todos los remitentes**   Seleccione esta opción para impedir que usuarios anónimos envíen mensajes al usuario.
    
      - **Rechazar mensajes de**   Use esta sección para bloquear a ciertos usuarios y que no envíen mensajes al usuario.
        
          - **Ningún remitente**   Elija esta opción para especificar que el buzón no rechazará mensajes de ningún remitente de la organización de Exchange. Esta opción está seleccionada de forma predeterminada.
        
          - **Remitentes de la siguiente lista** Seleccione esta opción para especificar que el buzón rechazará mensajes de un grupo específico de remitentes de la organización de Exchange. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para mostrar la página **Seleccionar destinatarios**, que muestra una lista de todos los destinatarios en la organización de Exchange. Seleccione los destinarios que desee, asígnelos a la lista y luego haga clic en **Aceptar**. También puede buscar un destinatario específico. Para ello, escriba el nombre del destinatario en la casilla de búsqueda y luego haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar").

## Miembro de

Utilice la sección **Miembro de** para ver una lista de los grupos de distribución o los grupos de seguridad a los que pertenece el usuario. La información de pertenencia no se puede cambiar en esta página. Tenga en cuenta que el usuario puede coincidir con los criterios de uno o más grupos de distribución dinámicos de la organización. No obstante, los grupos de distribución dinámicos no se muestran en esta página porque su pertenencia se calcula cada vez que se usan.

## Información sobre correo

Utilice la sección **Sugerencia de correo** para agregar una sugerencia de correo y avisar a los usuarios de posibles problemas antes de enviar un mensaje a este destinatario. La información sobre correo es texto que se muestra en la barra de información cuando este destinatario se agrega a los campos Para, CC o CCO de un nuevo mensaje de correo electrónico.


> [!NOTE]
> La información sobre correo puede incluir etiquetas HTML, pero no se permiten los scripts. La longitud de la información de una sugerencia de correo electrónico personalizada no puede superar los 175 caracteres mostrados. Las etiquetas HTML no se cuentan en el límite.



## Uso del Shell para cambiar las propiedades de usuarios de correo

Las propiedades de un usuario de correo se almacenan en Active Directory y en Exchange. En general, use los cmdlets **Get-User** y **Set-User** para ver y cambiar las propiedades de la información de la organización y de contacto. Use los cmdlets **Get-MailUser** y **Set-MailUser** para ver y cambiar las propiedades relacionadas con el correo, como las direcciones de correo electrónico, las sugerencias de correo electrónico, los atributos personalizados y si el usuario de correo está oculto en las listas de direcciones.

Use los cmdlets **Get-MailUser** y **Set-MailUser** para ver y cambiar las propiedades de los usuarios de correo. Para obtener información, consulte los siguientes temas:

  - [Get-User](https://technet.microsoft.com/es-es/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/es-es/library/aa998221\(v=exchg.150\))

  - [Get-MailUser](https://technet.microsoft.com/es-es/library/aa997254\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/es-es/library/aa995971\(v=exchg.150\))

Aquí se encuentran algunos ejemplos del uso del Shell para cambiar las propiedades del usuario de correo.

Este ejemplo establece la dirección de correo electrónico externa de Pilar Pinilla.

    Set-MailUser "Pilar Pinilla" -ExternalEmailAddress pilarp@tailspintoys.com

Este ejemplo oculta todos los usuarios de correo de la libreta de direcciones de la organización.

    Get-MailUser | Set-MailUser -HiddenFromAddressListsEnabled $true

Este ejemplo establece la propiedad de la empresa para todos los usuarios de correo de Contoso.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | Set-User -Company Contoso

En este ejemplo se configura la propiedad CustomAttribute1 para el valor ContosoEmployee para todos los usuarios de correo que posee el valor de Contoso en la propiedad Empresa.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Contoso')}| Set-MailUser -CustomAttribute1 ContosoEmployee

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que cambió correctamente las propiedades de los usuarios de correo, realice lo siguiente:

  - En el EAC, seleccione el usuario de correo y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para ver la propiedad que cambió.

  - En el Shell, use los cmdlest **Get-User** y **Get-MailUser** para comprobar los cambios. Una ventaja de usar Shell es que puede ver varias propiedades de varios contactos de correo.
    
        Get-MailUser | Fl Name,CustomAttribute1 
    
    En el ejemplo anterior donde la propiedad Empresa estaba configurada para Contoso para todos los contactos de correo, ejecute el siguiente comando para comprobar los cambios:
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | FL Name,Company
    
    En el ejemplo anterior donde todos los usuarios de correo tenían la propiedad CustomAttribute1 configurada para ContosoEmployee, ejecute el siguiente comando para comprobar los cambios.
    
        Get-MailUser | Fl Name,CustomAttribute1 

## Edición masiva de usuarios de correo

También puede usar el EAC para cambiar las propiedades seleccionadas para varios usuarios de correo. Cuando seleccione dos o más usuarios de correo en la lista de contactos en el EAC, las propiedades que se pueden editar masivamente se muestran en el panel de detalles. Cuando cambia una de estas propiedades, el cambio se aplica a todos los destinatarios seleccionados.

Cuando edite masivamente usuarios de correo, puede cambiar las siguientes áreas de propiedades:

  - **Información de contacto**   Cambie las propiedades compartidas, como la calle, el código postal y el nombre de la ciudad.

  - **Organización**   Cambie las propiedades compartidas, como el nombre de departamento, el nombre de la empresa y el administrador al que informan los contactos de correo o usuarios de correo seleccionados.

## Uso del EAC para editar masivamente usuarios de correo

1.  En el EAC, vaya a **Destinatarios** \> **Contactos**.

2.  En la lista de contactos, seleccione dos o más usuarios de correo. No se puede editar en masa una combinación de contactos de correo y usuarios de correo.
    

    > [!TIP]
    > Se pueden seleccionar varios usuarios de correos adyacentes si se mantiene presionada la tecla Mayús y se hace clic en el primer usuario de correo y, luego, en el último usuario de correo que quiera editar. También se pueden seleccionar varios usuarios de correo si se mantiene presionada la tecla Ctrl y se hace clic en cada uno de los contactos que quiera seleccionar.



3.  En el panel Detalles, en **Edición masiva**, haga clic en **Actualizar** en **Información de contacto** u **Organización**.

4.  Realice los cambios en la página de propiedades y, a continuación, guarde los cambios.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si editó masivamente usuarios de correo correctamente, realice uno de estos procedimientos:

  - En el EAC, seleccione todos los usuarios de correo que editó masivamente y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para ver las propiedades que cambió.

  - En el Shell, use el cmdlet **Get-User** para comprobar los cambios. Por ejemplo, digamos que usó la característica de edición masiva en el EAC para cambiar el administrador y la oficina para todos los usuarios de correo de una empresa de proveedor denominada A. Datum Corporation. Para comprobar estos cambios, puede ejecutar el siguiente comando en Shell:
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Adatum')} | fl Name,Office,Manager

## Usar la sincronización de directorios para administrar los usuarios de correo de Exchange Online

En esta sección se proporciona información sobre cómo administrar usuarios de correo mediante la sincronización de directorios en Exchange Online. La sincronización de directorios está disponible para los clientes híbridos con buzones de correo locales y hospedados en la nube, así como para clientes de Exchange Online de hospedaje completo con Active Directory local.


> [!NOTE]
> Si administra los destinatarios mediante la sincronización de directorios, podrá aún agregar y administrar usuarios en el Centro de administración de Office 365, pero no se sincronizarán con Active Directory local, puesto que en la sincronización de directorios solo se sincronizan los destinatarios de Active Directory local en la nube.




> [!NOTE]
> Se recomienda usar la sincronización de directorios con las siguientes características: 
> <UL>
> <LI>
> <P><STRONG>Listas de remitentes bloqueados y de remitentes seguros de Outlook</STRONG>: cuando se sincronizan con el servicio, estas listas tienen prioridad sobre filtrado de correo no deseado del servicio. Esto permite a los usuarios administrar sus propias listas de remitentes seguros y remitentes bloqueados por usuario o por dominio.</P>
> <LI>
> <P><STRONG>Bloqueo perimetral basado en directorios (DBEB)</STRONG>: para obtener más información sobre DBEB, vea <A href="https://technet.microsoft.com/es-es/library/dn600322(v=exchg.150)">Usar bloqueo perimetral basado en directorios para rechazar mensajes enviados a destinatarios no válidos</A>.</P>
> <LI>
> <P><STRONG>Cuarentena de correo no deseado de usuarios finales</STRONG>: para poder obtener acceso a la cuarentena de correo no deseado de usuarios finales, los usuarios finales deben tener un identificador de usuario de Office 365 y una contraseña válidos. Los clientes con buzones locales deben ser usuarios de correo electrónico válidos.</P>
> <LI>
> <P><STRONG>Reglas de transporte</STRONG>: cuando se usa la sincronización de directorios, los usuarios y grupos existentes de Active Directory se cargan automáticamente a la nube y es posible crear reglas de transporte destinadas a usuarios o grupos específicos sin tener que agregarlos de forma manual a través del EAC o Windows PowerShell remoto. Tenga en cuenta que los <A href="https://go.microsoft.com/fwlink/?linkid=507569">grupos de distribución dinámicos</A> no se pueden sincronizar mediante la sincronización de directorios.</P></LI></UL>



**Antes de empezar**

Obtenga los permisos necesarios y prepárese para la sincronización de directorios, tal como se describe en [Preparar la sincronización de directorios](https://go.microsoft.com/fwlink/p/?linkid=308908).

**Para sincronizar directorios de usuarios**

1.  Active la sincronización de directorios, tal como se describe en [Activar sincronización de directorios](https://go.microsoft.com/fwlink/p/?linkid=308909).

2.  Configure su equipo de sincronización de directorios, tal como se describe en [Configurar el equipo de sincronización de directorios](http://go.microsoft.com/fwlink/p/?linkid=308911).

3.  Sincronice sus directorios, tal como se describe en [Usar el Asistente de configuración para sincronizar los directorios](http://go.microsoft.com/fwlink/?linkid=308912).
    

    > [!IMPORTANT]
    > Cuando finaliza el Asistente de configuración de la herramienta de sincronización de Microsoft Azure Active Directory, se crea la cuenta <STRONG>MSOL_AD_SYNC</STRONG> en el bosque de Active Directory. Esta cuenta se utiliza para leer y sincronizar la información de Active Directory local. Para que la sincronización de directorios se realice correctamente, debe asegurarse de que el TCP 443 esté abierto en el servidor de sincronización de directorios local.



4.  Active los usuarios sincronizados, tal como se describe en [Activar usuarios sincronizados](http://go.microsoft.com/fwlink/p/?linkid=308913).

5.  Administre la sincronización de directorios, tal como se describe en [Administrar la sincronización de directorios](http://go.microsoft.com/fwlink/p/?linkid=308915).

6.  Compruebe que Exchange Online se esté sincronizando correctamente. En el EAC, vaya a **Destinatarios** \> **Contactos** y vea que la lista de usuarios se haya sincronizado correctamente desde el entorno local.

