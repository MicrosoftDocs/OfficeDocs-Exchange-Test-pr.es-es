---
title: 'Administrar archivos locales en Exchange 2013: Exchange 2013 Help'
TOCTitle: Administrar archivos locales en Exchange 2013
ms:assetid: 49ef4a3e-d209-4fb2-80a3-6132b0f69bd0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ651146(v=EXCHG.150)
ms:contentKeyID: 49895611
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar archivos locales en Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-02-01_

El archivado local permite recuperar el control de los datos de mensajería de la organización mediante la eliminación de los archivos de almacenamiento personal (.pst). Asimismo, permite satisfacer los requisitos de retención de mensajes y de exhibición de documentos electrónicos de la organización. Con el archivado habilitado, los usuarios pueden almacenar mensajes en un buzón de archivo, al que puede acceder mediante MicrosoftOutlook y Outlook Web App.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Archivo local" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - No se admite que el buzón de correo principal de un usuario resida en una versión de Exchange más antigua que el archivo del usuario. Si el buzón de correo principal de un usuario sigue estando en Exchange 2010, deberá moverlo a Exchange 2013 al mismo tiempo que mueve el archivo a Exchange 2013.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear un buzón y habilitar un archivo local

## Uso de EAC

1.  Vaya a **Destinatarios**\>**Buzones de correo**.

2.  Haga clic en **Nuevo**\>**Buzón de usuario**.

3.  En la página **Nuevo buzón de usuario**, en el cuadro **Alias**, escriba el alias para el usuario.
    

    > [!NOTE]
    > Si deja la casilla en blanco, el valor que escriba en el cuadro <STRONG>Nombre de inicio de sesión de usuario</STRONG> se usará como alias.



4.  
    
    Seleccione una de las opciones para:
    
      - **Usuario existente** Haga clic en este botón y luego haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar usuario – Todo el bosque**. Este cuadro de diálogo muestra una lista de cuentas de usuario de Active Directory del bosque que no están habilitadas para correo o no tienen buzones de Exchange. Seleccione la cuenta de usuario que desea habilitar para correo y, a continuación, haga clic en **Aceptar**. Si selecciona esta opción, no es necesario proporcionar información de la cuenta del usuario debido a que esa información ya existe en Active Directory.
    
      - **Nuevo usuario** Seleccione este botón para crear una nueva cuenta de usuario en Active Directory y cree un buzón para el usuario. Si selecciona esta opción, tendrá que proporcionar la información de la cuenta del usuario que se requiera.
    

    > [!NOTE]
    > La cuenta de Active Directory&nbsp;que está asociada a los buzones de usuario debe residir en el mismo bosque que el servidor de Exchange. Para crear un buzón para una cuenta de usuario que está en un bosque de confianza, debe crear un buzón vinculado. Para obtener información detallada, vea <A href="manage-linked-mailboxes-exchange-2013-help.md">Administrar buzones vinculados</A>.



5.  
    
    Haga clic en **Más opciones** para configurar los siguientes parámetros.
    
      - **Base de datos de buzones de correo** Haga clic en **Examinar** para seleccionar una base de datos de buzones de correo donde desea almacenar el buzón. Si no selecciona una base de datos, Exchange le asignará una automáticamente.
    
      - **Archivar** Active esta casilla para crear un buzón de archivado para el buzón. Si crea un buzón de archivo, los objetos del buzón se moverán automáticamente del buzón de usuario primario al archivo, según la configuración de directiva de retención predeterminada o la que defina.
        
        Haga clic en **Examinar** para seleccionar una base de datos que resida en el bosque local para almacenar el buzón de archivo.
        
        Para obtener más información, vea [Archivado local en Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).
    
      - **Directiva de libreta de direcciones** Utilice esta lista para seleccionar una directiva de libreta de direcciones (ABP) para el buzón. Las ABP contienen una lista global de direcciones (GAL), una libreta de direcciones sin conexión (OAB), una lista de salas y un conjunto de listas de direcciones. Cuando se asigna una ABP a usuarios de buzones de correo, les proporciona acceso a una GAL personalizada en Outlook y Outlook Web App. Para obtener más información, vea [Directivas de la libreta de direcciones](address-book-policies-exchange-2013-help.md).

6.  
    
    Cuando haya finalizado, haga clic en **Guardar** para crear el buzón.

## Usar el Shell

En este ejemplo, se crea el usuario Chris Ashton en Active Directory y se crea el buzón en la base de datos de buzones de correo DB01 con archivo habilitado. Se debe restablecer la contraseña en el siguiente inicio de sesión. Para establecer el valor inicial de la contraseña, en este ejemplo se crea una variable ($password), se le pide que escriba una contraseña y se asigna dicha contraseña a la variable como un objeto SecureString.

    $password = Read-Host "Enter password" -AsSecureString
    New-Mailbox -UserPrincipalName chris@contoso.com -Alias chris -Archive -Database "DB01" -Name ChrisAshton -OrganizationalUnit Users -Password $password -FirstName Chris -LastName Ashton -DisplayName "Chris Ashton" 

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [New-Mailbox](https://technet.microsoft.com/es-es/library/aa997663\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó un buzón de usuario con un archivo local correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios**\>**Buzones de correo** y, a continuación, seleccione el buzón de usuario nuevo en la lista. En el panel de detalles, en **Archivado local**, confirme que esté establecido en **Habilitado**. Haga clic en **Ver detalles** para ver las propiedades del archivo, incluido el estado del archivo y la base de datos de buzones de correo en la cual se creó.

  - En el Shell, ejecute el siguiente comando para mostrar información acerca del nuevo buzón de usuario y del archivo.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress,*Archive*

  - En el Shell, use el cmdlet **Test-ArchiveConnectivity** para probar la conectividad con el archivo. Para consultar ejemplos sobre cómo probar la conectividad del archivo, vea la sección Ejemplos de [Test-ArchiveConnectivity](https://technet.microsoft.com/es-es/library/hh529914\(v=exchg.150\)).

## Habilitar un archivo local para un buzón existente

También puede crear archivos para usuarios existentes que tengan un buzón pero que no estén habilitados para archivo. Esto se conoce como *habilitar un archivo* para un buzón existente.

## Uso de EAC

1.  Vaya a **Destinatarios**\>**Buzones de correo**.

2.  Seleccione un buzón.

3.  En el panel de detalles, en **Archivado local**, haga clic en **Habilitar**
    

    > [!TIP]
    > También puede habilitar archivos de forma masiva mediante la selección de varios buzones (utilice las teclas Mayús o Crtl). Después de seleccionar varios buzones de correo, en el panel de detalles, haga clic en <STRONG>Más opciones</STRONG>. Luego, en <STRONG>Archivo</STRONG>, haga clic en <STRONG>Habilitar</STRONG>.



4.  En la página **Crear archivado local**, haga clic en **Aceptar** para que Exchange seleccione una base de datos de buzones de correo automáticamente, o haga clic en **Examinar** para seleccionar una.

## Usar el Shell

En este ejemplo, se habilita el archivo para el buzón de Tony Smith.

    Enable-Mailbox "Tony Smith" -Archive

En este ejemplo se recuperan los buzones de la base de datos DB01 que no tienen ningún archivo local o basado en la nube habilitado y ningún nombre que empiece por DiscoverySearchMailbox. El resultado se canaliza al cmdlet **Enable-Mailbox** para habilitar el archivo de todos los buzones de la base de datos de buzones de correo DB01.

    Get-Mailbox -Database DB01 -Filter {ArchiveGuid -Eq $null -AND ArchiveDomain -eq $null -AND Name -NotLike "DiscoverySearchMailbox*"} | Enable-Mailbox -Archive

Para obtener más información acerca de la sintaxis y los parámetros, vea [Enable-Mailbox](https://technet.microsoft.com/es-es/library/aa998251\(v=exchg.150\)) y [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si habilitó un archivo local para un buzón existente correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Buzones** y, luego, seleccione el buzón en la lista. En el panel de detalles, en **Archivado local**, confirme que esté establecido en **Habilitado**. Haga clic en **Ver detalles** para ver las propiedades del archivo, incluido el estado del archivo y la base de datos de buzones de correo en la cual se creó.

  - En el Shell, ejecute el siguiente comando para mostrar información acerca del nuevo archivo.
    
        Get-Mailbox <Name> | FL Name,*Archive*

  - En el Shell, use el cmdlet **Test-ArchiveConnectivity** para probar la conectividad con el archivo. Para consultar ejemplos sobre cómo probar la conectividad de archivo, vea [Test-ArchiveConnectivity](https://technet.microsoft.com/es-es/library/hh529914\(v=exchg.150\)).

## Deshabilitar un archivo local

Es posible que desee deshabilitar un archivo del usuario o basado en la nube con el fin de solucionar problemas o mover el buzón a una versión de Exchange que no admita el archivado en contexto. Si deshabilita un archivo local, toda la información que se encuentre en el archivo se conservará en la base de datos de buzones de correo hasta que finalice el tiempo de retención del buzón y el archivo se elimine de forma permanente. (De forma predeterminada, Exchange conserva los buzones desconectados, incluidos los buzones de archivo durante 30 días.)


> [!IMPORTANT]
> Al deshabilitar el archivo, éste se quita del buzón y se marca en la base de datos de buzones de correo para eliminarlo.



Si desea volver a conectar el archivado local a ese buzón de correo, puede usar el cmdlet [Connect-Mailbox](https://technet.microsoft.com/es-es/library/aa997878\(v=exchg.150\)) con el parámetro *Archive*.

## Uso de EAC

1.  Vaya a **Destinatarios**\>**Buzones de correo**.

2.  Seleccione un buzón.

3.  En el panel de detalles, en **Archivado local**, haga clic en **Deshabilitar**.
    

    > [!TIP]
    > También puede deshabilitar archivos de forma masiva mediante la selección de varios buzones (utilice las teclas Mayús o Crtl). Después de seleccionar varios buzones de correo, en el panel de detalles, haga clic en <STRONG>Más opciones</STRONG>. Luego, en <STRONG>Archivo</STRONG>, haga clic en <STRONG>Deshabilitar</STRONG>.



## Usar el Shell

En este ejemplo, se deshabilita el archivo para el buzón de María González. No deshabilita el buzón.

    Disable-Mailbox -Identity "Chris Ashton" -Archive

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [Disable-Mailbox](https://technet.microsoft.com/es-es/library/aa997210\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el archivo se deshabilitó correctamente, siga estos pasos:

  - En el EAC, seleccione el buzón. Luego, en el panel de detalles, compruebe su estado de archivo en **Archivado local**.

  - En el Shell, ejecute el siguiente comando para comprobar las propiedades de archivo del usuario de buzón.
    
        Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*
    
    Si el archivo está deshabilitado, se devolverán los siguientes valores para las propiedades relacionadas con el archivo.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Propiedad</th>
    <th>Valor</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ArchiveDatabase (para archivos locales)</p></td>
    <td><p>&lt;En blanco&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>ArchiveState</p></td>
    <td><p><code>None</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>DisabledArchiveDatabase (para archivos locales)</p></td>
    <td><p>&lt;nombre de la base de datos de buzones de correo&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>DisabledArchiveGuid</p></td>
    <td><p>&lt;GUID del archivo deshabilitado&gt;</p></td>
    </tr>
    </tbody>
    </table>


## Conectar un archivo local

Cuando se deshabilita un buzón de archivo, éste pasa a estar desconectado. Un buzón de archivo desconectado permanece en la base de datos de buzones de correo durante un período específico de tiempo. De forma predeterminada, Exchange retiene los archivos desconectados durante 30 días. Durante ese tiempo, puede recuperar el archivo asociándolo a un buzón de correo existente. Puede modificar el período de retención del buzón eliminado con el fin de retener un buzón eliminado o un archivo durante un período superior o inferior.


> [!WARNING]
> Si deshabilita un archivo para un usuario y, a continuación, habilita otro archivo para ese usuario, el usuario obtendrá un archivo nuevo. El archivo nuevo no contendrá los datos que se incluían en el archivo desconectado del usuario. Si desea volver a conectar un usuario a su archivo desconectado, debe realizar primero este procedimiento.




> [!NOTE]
> No puede utilizar el EAC para conectar un archivo desconectado a un usuario de buzón.



## Usar el Shell

1.  Si no conoce el nombre del archivo, puede verlo en el Shell mediante la ejecución del comando siguiente. Este ejemplo recupera la base de datos de buzones de correo DB01, transmite todo al cmdlet **Get-MailboxStatistics** para recuperar las estadísticas de buzón de todos los buzones de la base de datos y, a continuación, usa el cmdlet **Where-Object** para filtrar los resultados y recuperar una lista de los archivos desconectados. El comando muestra información adicional acerca de cada archivo como el GUID y el recuento de elementos.
    
        Get-MailboxDatabase "DB01" | Get-MailboxStatistics | Where {($_.DisconnectDate -ne $null) -and ($_.IsArchiveMailbox -eq $true)} | Format-List

2.  Conectar los archivos al buzón de correo principal. En este ejemplo se conecta el archivo de Chris Ashton a su buzón de correo principal y se usa el GUID como identidad del archivo.
    
        Enable-Mailbox -ArchiveGuid "8734c04e-981e-4ccf-a547-1c1ac7ebf3e2" -ArchiveDatabase "DB01" -Identity "Chris Ashton"

Para obtener información detallada acerca de la sintaxis y los parámetros, vea estos temas:

  - [Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\))

  - [Get-MailboxStatistics](https://technet.microsoft.com/es-es/library/bb124612\(v=exchg.150\))

  - [Enable-Mailbox](https://technet.microsoft.com/es-es/library/aa998251\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el archivo se conectó y se desconectó correctamente a un buzón de usuario, ejecute el siguiente comando del Shell para recuperar las propiedades de archivo del usuario del buzón y comprobar los valores devueltos para las propiedades *ArchiveGuid* y *ArchiveDatabase*:

    Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*

