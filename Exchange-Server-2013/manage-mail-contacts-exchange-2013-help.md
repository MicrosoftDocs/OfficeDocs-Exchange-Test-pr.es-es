---
title: 'Administrar contactos de correo: Exchange 2013 Help'
TOCTitle: Administrar contactos de correo
ms:assetid: 74c72aed-e9ff-4927-8eb7-c08a86e79ae0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998858(v=EXCHG.150)
ms:contentKeyID: 48268287
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailContactWizardForm.NewMailContactIntroductionWizardPage
ms.translationtype: MT
---

# Administrar contactos de correo

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-10-04_

Los contactos de correo son objetos de servicio de directorio habilitados para correo que contienen información acerca de personas u organizaciones que existen fuera de su organización de Exchange Online. Cada contacto de correo tiene una dirección de correo electrónico externa. Para obtener más información acerca de los contactos de correo, consulte [Destinatarios](recipients-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Crear un contacto de correo

## Usar el EAC para crear un contacto de correo

1.  En el EAC, vaya a **Destinatarios** \> **Contactos**.

2.  Haga clic en **Nuevo** ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") \> **Contacto de correo**.

3.  Complete los siguientes cuadros en la página **Nuevo contacto de correo**:
    
      - **Nombre**   Use este cuadro para escribir el nombre del contacto.
    
      - **Iniciales**   Use este cuadro para escribir las iniciales del contacto.
    
      - **Apellido**   Use este cuadro para escribir el apellido del contacto.
    
      - **\* Nombre para mostrar** Use este cuadro para escribir el nombre del contacto para mostrar. Este es el nombre que se incluye en la lista de contactos de EAC y en la libreta de direcciones de la organización. Este cuadro se rellena de forma predeterminada con los nombres que escribe en los cuadros **Nombre**, **Iniciales** y **Apellido**. Aunque no haya usado dichos cuadros, debe escribir un nombre en este cuadro, ya que es obligatorio. El nombre no puede superar los 64 caracteres.
    
      - **\* Nombre** Use este cuadro para escribir un nombre para el contacto. Este es el nombre que se muestra en el servicio de directorio. Tal como sucede con el nombre para mostrar, este cuadro se rellena de forma predeterminada con los nombres que escriba en los cuadros **Nombre**, **Iniciales** y **Apellido**. Aunque no haya usado dichos cuadros, debe escribir un nombre en este cuadro, ya que es obligatorio. El nombre no puede superar los 64 caracteres.
    
      - **\* Alias   **Use este cuadro para escribir un alias (64 caracteres como máximo) para el contacto. Este cuadro es obligatorio.
    
      - **\* Dirección de correo electrónico externa**   Use este cuadro para escribir la cuenta de correo externa del contacto. Este cuadro es obligatorio. El correo electrónico que se envíe a este contacto se reenviará a esta dirección de correo electrónico.
    
      - **Unidad organizativa**   Puede seleccionar una unidad organizativa (OU) diferente de la que aparece de forma predeterminada, que es el ámbito del destinatario. Si el ámbito del destinatario definido corresponde al bosque, el valor predeterminado será el contenedor Usuarios del dominio que contiene el equipo en el que se ejecuta el EAC. Si el ámbito del destinatario está establecido en un dominio específico, el contenedor de usuarios se selecciona de modo predeterminado. Si el ámbito del destinatario está establecido en una unidad organizativa específica (OU), esa OU se selecciona de modo predeterminado.
        
        Para seleccionar otra OU, haga clic en **Examinar**. En el cuadro de diálogo se muestran todas las OU del bosque dentro del ámbito especificado. Seleccione la unidad organizativa que desee y haga clic en **Aceptar**.
        

        > [!NOTE]
        > La casilla <STRONG>Unidad organizativa</STRONG> solo está disponible en Exchange Server 2013. No está disponible en Exchange Online.



4.  Cuando haya terminado, haga clic en **Guardar**.

## Usar el Shell para crear un contacto de correo

En este ejemplo se crea un contacto de correo para Debra Garcia en Exchange Server 2013.

    New-MailContact -Name "Debra Garcia" -ExternalEmailAddress dgarcia@tailspintoys.com -OrganizationalUnit Users

En este ejemplo se crea un contacto de correo para Alan Shen en Exchange Online.

    New-MailContact -Name "Alan Shen" -ExternalEmailAddress alans@fourthcoffee.com

En este ejemplo se habilita para correo un contacto existente en Exchange Server 2013 denominado Karen Toh.

    Enable-MailContact -Identity "Karen Toh" -ExternalEmailAddress ktoh@tailspintoys.com

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó un contacto de correo correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Contactos**. El nuevo contacto de correo aparecerá en la lista de contactos. Bajo **Tipo de contacto**, el tipo es **Contacto de correo**.

  - En el Shell, ejecute el comando siguiente para mostrar información sobre el nuevo contacto de correo.
    
        Get-MailContact <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## Cambiar las propiedades de contactos de correo

## Uso de la EAC para cambiar las propiedades de los contactos de correo

1.  En el EAC, vaya a **Destinatarios** \> **Contactos**.

2.  En la lista de contactos y usuarios de correo, haga clic en el contacto de correo cuyas propiedades desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de los contactos de correo, haga clic en las siguientes secciones para ver o cambiar las propiedades.
    
      - General
    
      - Contact Information
    
      - Organization
    
      - Email Options (no disponible en Exchange Online)
    
      - MailTip

## General

Utilice esta sección **General** para ver o cambiar la información básica sobre el contacto de correo.

  - **Nombre**, **Inicial**, **Apellidos**

  - **\* Nombre** Se trata del nombre indicado en Active Directory. Si cambia este nombre, no debe superar los 64 caracteres.

  - **\* Nombre para mostrar**   Este nombre aparece en la libreta de direcciones de la organización, en las líneas Para: y De: del correo electrónico y en la lista Buzón. Este nombre no puede contener espacios en blanco antes o después del nombre para mostrar.

  - **\* Alias** Se trata de alias del contacto de correo. Si lo modifica, debe ser por uno exclusivo de la organización y no puede superar los 64 caracteres.

  - **\*Dirección de correo electrónico externa** Es la dirección SMTP principal del contacto de correo y de su cuenta externa. El correo electrónico que se envíe a este contacto se reenviará a esta dirección de correo electrónico.

  - Haga clic en **Más opciones** para ver la OU que contiene la cuenta del contacto de correo. Debe usar los usuarios y los equipos de Active Directory para desplazar el contacto a una OU distinta.

## Información de contacto

Utilice la sección **Información de contacto** para ver o modificar la información de contacto del destinatario, como la dirección de correo electrónico y los números de teléfono. Esta información se muestra en la libreta de direcciones.

## Organización

Use la sección **Organización** para registrar información detallada acerca del rol del contacto de correo en la organización. Esta información se muestra en la libreta de direcciones. Asimismo, puede crear un gráfico de organización virtual al que se pueda obtener acceso desde clientes de correo electrónico como Outlook.

  - **Título** Use este cuadro para ver o cambiar el título del contacto.

  - **Departamento** Use este cuadro para ver o cambiar el departamento en el que trabaja el contacto. Puede usar este cuadro para crear condiciones de destinatarios para grupos de distribución dinámicos y listas de direcciones.

  - **Compañía** Use este cuadro para ver o cambiar la compañía en la que trabaja el contacto. Puede usar este cuadro para crear condiciones de destinatarios para grupos de distribución dinámicos.

  - **Administrador**   Para agregar un administrador, haga clic en **Examinar**. En **Seleccionar administrador**, seleccione la persona y, a continuación, haga clic en **Aceptar**.

  - **Subordinados directos**   Este campo no se puede modificar. Un *subordinado directo* es un destinatario que está bajo las órdenes de un administrador específico. En caso de que haya indicado un administrador para el destinatario, éste aparecerá como subordinado directo en la información del buzón de correo del administrador. Por ejemplo, Toby administra a Ann y a Spencer, que son contactos de correo. De este modo, Toby está especificado en el cuadro **Administrador** en las propiedades de organización de Ann y Spencer, y Ann y Spencer aparecen en el cuadro **Subordinados directos** en las propiedades del buzón de Toby.

## Opciones de correo electrónico

Utilice la sección **Opciones de correo electrónico** para agregar o quitar direcciones de proxy para el contacto de correo o bien para editar las ya existentes. La dirección SMTP principal del contacto de correo también aparece en esta sección, pero no se puede modificar. Para hacerlo, deberá modificar la dirección de correo electrónico externa del contacto, en la sección **General**.


> [!NOTE]
> La sección <STRONG>Opciones de correo</STRONG> sólo está disponible en Exchange Server 2013. No está disponible en Exchange Online.



## Información sobre correo

Utilice la sección **Sugerencia de correo** para agregar una sugerencia de correo y avisar a los usuarios de posibles problemas antes de enviar un mensaje a este destinatario. La información sobre correo es texto que se muestra en la barra de información cuando este destinatario se agrega a los campos Para, CC o CCO de un nuevo mensaje de correo electrónico.


> [!NOTE]
> La información sobre correo puede incluir etiquetas HTML, pero no se permiten los scripts. La longitud de la información de una sugerencia de correo electrónico personalizada no puede superar los 175 caracteres mostrados. Las etiquetas HTML no se cuentan en el límite.



## Usar el Shell para cambiar las propiedades del contacto de correo

Las propiedades de un contacto de correo se almacenan tanto en Active Directory como en Exchange. En general, utilice los cmdlets **Get-Contact** y **Set-Contact** para ver y cambiar las propiedades de la información de organización y contacto. Utilice los cmdlets **Get-MailContact** y **Set-MailContact** para ver o cambiar las propiedades del correo, por ejemplo, las direcciones de correo electrónico, la información sobre correo, los atributos personalizados y si el contacto está oculto en las listas de direcciones.

Para obtener más información al respecto, consulte los temas siguientes:

  - [Get-Contact](https://technet.microsoft.com/es-es/library/aa998258\(v=exchg.150\))

  - [Set-Contact](https://technet.microsoft.com/es-es/library/bb124535\(v=exchg.150\))

  - [Get-MailContact](https://technet.microsoft.com/es-es/library/bb124717\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/es-es/library/aa995950\(v=exchg.150\))

A continuación aparecen algunos ejemplos de cómo usar el Shell para cambiar las propiedades del contacto de correo.

En este ejemplo se configuran las propiedades Título, Departamento, Compañía y Administrador del contacto de correo Kai Axford.

    Set-Contact "Kai Axford" _-Title Consultant -Department "Public Relations" -Company Fabrikam -Manager "Karen Toh"

En este ejemplo se establece la propiedad CustomAttribute1 en un valor de PartTime para todos los contactos de correo. Asimismo, los oculta en la libreta de direcciones de la organización.

    Get-MailContact | Set-MailContact -CustomAttribute1 PartTime -HiddenFromAddressListsEnabled $true

En este ejemplo se establece la propiedad CustomAttribute15 en un valor de TemporaryEmployee para todos los contactos de correo del departamento de Relaciones Públicas.

    Get-Contact -Filter "Department -eq 'Public Relations'" | Set-MailContact -CustomAttribute15 TemporaryEmployee

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si cambió las propiedades de un contacto de correo correctamente, haga lo siguiente:

  - En el EAC, seleccione el contacto y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para visualizar la propiedad que ha modificado.

  - En el Shell, use los cmdlet **Get-Contact** y **Get-MailContact** para verificar los cambios. Una ventaja de usar Shell es que puede ver varias propiedades de varios contactos de correo. En el ejemplo anterior, en el que todos los contactos de correo tenían la propiedad CustomAttribute1 establecida en PartTime y estaban ocultos en la libreta de direcciones, ejecute el comando siguiente para verificar los cambios.
    
        Get-MailContact | Fl Name,CustomAttribute1,HiddenFromAddressListsEnabled
    
    En el ejemplo anterior, en el que CustomAttribute15 estaba establecido para todos los contactos de correo del departamento de Relaciones Públicas, ejecute el comando siguiente para verificar los cambios.
    
        Get-Contact -Filter "Department -eq 'Public Relations'" | Get-MailContact | FL Name,CustomAttribute15

## Edición masiva de contactos de correo

Puede utilizar el EAC para cambiar las propiedades seleccionadas de varios contactos de correo. Cuando seleccione dos o más contactos de correo de la lista de contactos del EAC, las propiedades que se pueden editar masivamente aparecen en el panel Detalles. Cuando cambia una de estas propiedades, el cambio se aplica a todos los destinatarios seleccionados.

Al editar masivamente los contactos de correo, puede cambiar las siguientes áreas de propiedades:

  - **Información de contacto**   Cambie las propiedades compartidas, como la calle, el código postal y el nombre de la ciudad.

  - **Organización** Cambie las propiedades compartidas, como el nombre de departamento, el nombre de la compañía y el administrador al que informan los contactos de correo o usuarios de correo seleccionados.

## Uso del EAC para editar masivamente contactos de correo

1.  En el EAC, vaya a **Destinatarios** \> **Contactos**.

2.  En la lista de contactos, seleccione dos o más contactos de correo. No se puede editar en masa una combinación de contactos de correo y usuarios de correo.
    

    > [!TIP]
    > Para eliminar varios contactos de correo adyacentes, mantenga presionada la tecla Mayús, haga clic en el primer contacto y, seguidamente, haga clic en el último contacto que desea editar. Para seleccionar varios contactos de correo, mantenga presionada la tecla Ctrl y haga clic en cada uno de los contactos que desee seleccionar.



3.  En el panel Detalles, bajo **Edición en masa**, haga clic en **Actualizar** bajo **Información de contacto** u **Organización**.

4.  Realice los cambios en la página de propiedades y, a continuación, guarde los cambios.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si editó masivamente los contactos de correo correctamente, siga uno de estos procedimientos:

  - En el EAC, seleccione cada uno de los contactos de correo que ha editado masivamente y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para visualizar las propiedades que ha modificado.

  - En el Shell, use el cmdlet **Get-Contact** para verificar los cambios. Por ejemplo, supongamos que ha editado masivamente una característica en el EAC para cambiar al administrador y la oficina de todos los contactos de correo de una compañía proveedora llamada A. Datum Corporation. Para comprobar estos cambios, puede ejecutar el siguiente comando en el Shell.
    
        Get-Contact -ResultSize unlimited -Filter {(Company -eq 'Adatum')} | fl Name,Office,Manager


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

