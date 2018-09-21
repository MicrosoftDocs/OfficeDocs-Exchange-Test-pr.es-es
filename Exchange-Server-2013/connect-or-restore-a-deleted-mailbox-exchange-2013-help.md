---
title: 'Conectar o restaurar un buzón eliminado: Exchange 2013 Help'
TOCTitle: Conectar o restaurar un buzón eliminado
ms:assetid: a5e6ac44-5901-4eab-9017-c6fae80a0f83
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ863438(v=EXCHG.150)
ms:contentKeyID: 50556838
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectar o restaurar un buzón eliminado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-05-04_

Puede usar el EAC o el Shell para conectar un buzón de correo eliminado en una cuenta de usuario de Active Directory. Cuando elimina un buzón de correo, Exchange retiene el buzón en la base de datos del buzón y conmuta el buzón de correo a un estado de deshabilitado. También se elimina la cuenta de usuario de Active Directory asociada. El buzón de correo se retiene hasta que expira el período de retención del buzón de correo eliminado, que es de 30 días de forma predeterminada, y, a continuación, se elimina permanentemente (o *se purga*) de la base de datos de buzones de correo.

Hasta que un buzón de correo se elimina permanentemente de la base de datos de buzones de Exchange, puede usar el EAC o el Shell para conectarlo a una cuenta de usuario de Active Directory. También puede usar el Shell para restaurar los contenidos del buzón de correo eliminado en un buzón de correo existente.

Para obtener más información acerca de los buzones de correo desconectados y realizar otras tareas de administración, consulte los siguientes temas:

  - [Buzones desconectados](disconnected-mailboxes-exchange-2013-help.md)

  - [Deshabilitar o eliminar un buzón de correo](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Conectar un buzón de correo deshabilitado](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Eliminar permanentemente un buzón de correo](permanently-delete-a-mailbox-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Crear una nueva cuenta de usuario en Active Directory para conectarle el buzón eliminado. O use el cmdlet **Get-User** en el Shell para verificar que la cuenta del usuario de Active Directory al cual desea conectar el buzón de correo eliminado existe y todavía no está asociado a otro buzón de correo. Para conectar un buzón de correo eliminado a una cuenta de usuario, la cuenta debe existir y el valor de la propiedad *RecipientType* debe ser `User`, lo que indica que la cuenta todavía no tiene un buzón de correo habilitado.
    
    Para las organizaciones de Exchange locales, también puede verificar esta información en usuarios y equipos de Active Directory.
    

    > [!IMPORTANT]
    > Al conectar buzones de correo enlazados eliminados, buzones de correo de recursos o buzones compartidos, la cuenta del usuario de Active Directory a la cual conecta el buzón de correo se debe deshabilitar.



  - Para verificar que el buzón de correo eliminado al cual desea conectar una cuenta de usuario existe en la base de datos del buzón de correo y que no se trata de un buzón de correo eliminado temporalmente, ejecute el siguiente comando.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    El buzón de correo eliminado debe existir en la base de datos de buzones de correo y el valor de la propiedad *DisconnectReason* debe ser `Disabled`. Si el buzón de correo no se ha purgado de la base de datos, el comando no devolverá ningún resultado.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## ¿Qué desea hacer?

## Conectar un buzón eliminado

Al conectar un buzón de correo eliminado, asocia el buzón con una cuenta de usuario que no tiene el correo habilitado, lo que significa que no tiene un buzón de correo existente. Para conectar un buzón de correo eliminado a una cuenta de usuario que tiene un buzón de correo, debe restaurar el buzón de correo eliminado. Para obtener más información, consulte Restaurar un buzón de correo eliminado más adelante en este tema.

## Usar el EAC para conectar un buzón eliminado

El siguiente procedimiento muestra cómo conectar un buzón de correo de usuario a una cuenta de usuario. También puede usar este procedimiento para conectar buzones de correo enlazados, buzones de correo de recursos y buzones de correo compartidos que se han eliminado para una cuenta de usuario.

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  Haga clic en **Más** ![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") y, a continuación, haga clic en **Conectar un Buzón de correo**.
    
    Se mostrará una lista de buzones de correo desconectados en el servidor de Exchange de su organización de Exchange.
    

    > [!NOTE]
    > Esta lista de buzones de correo desconectados incluye buzones de correo deshabilitados, buzones de correo eliminados y buzones de correo eliminados temporalmente.



3.  Haga clic en el buzón de correo eliminado que desee conectar a un usuario y, a continuación, haga clic en **Conectar**.

4.  En la ventana que pregunta si está seguro de querer conectar el buzón de correo, haga clic en **Sí**.
    
    Se muestra una lista de cuentas de usuario que no están habilitados para correo.

5.  Haga clic en el usuario al cual desee conectar el buzón eliminado y, a continuación, haga clic en **Aceptar**.
    
    Exchange conectará el buzón de correo eliminado a la cuenta de usuario que seleccione.

## Usar el Shell para conectar un buzón eliminado

Use el cmdlet **Connect-Mailbox** en el Shell para conectar un buzón de correo eliminado a una cuenta de usuario que no tenga el correo habilitado. Tiene que especificar el tipo de buzón de correo que está conectando. Los siguientes ejemplos muestran la sintaxis para volver a conectar buzones de correo de usuario, enlazados, de sala, de equipo y compartidos. En todos los ejemplos, el parámetro *Alias* opcional se usa para especificar el alias del correo electrónico, que es la parte de la dirección de correo electrónico a la izquierda del símbolo (@). Si no incluye el parámetro *Alias*, se usa el valor especificado en el parámetro *User* o *LinkedMasterAccount* para crear el alias de la dirección de correo electrónico del buzón de correo reconectado.


> [!NOTE]
> Como se indicó anteriormente, al conectar buzones de correo enlazados, de recursos o compartidos, la cuenta del usuario de Active Directory a la cual enlaza el buzón de correo se debe deshabilitar.



En este ejemplo se conecta un buzón de correo de usuario. El parámetro *Identity* especifica el nombre para mostrar del buzón de correo eliminado retenido en la base de datos de buzones de correo denominada MBXDB01. El parámetro *User* especifica la cuenta de usuario de Active Directory que desea conectar al buzón de correo.

```powershell
Connect-Mailbox -Identity "Paul Cannon" -Database MBXDB01 -User "Robin Wood" -Alias robinw
```


> [!NOTE]
> También puede usar valores para las propiedades de <CODE>LegacyDN</CODE> o <CODE>MailboxGuid</CODE> para identificar el buzón de correo eliminado.



En este ejemplo se conecta un buzón vinculado. El parámetro *Identity* especifica el buzón de correo eliminado en la base de datos de buzones de correo denominada MBXDB02. El parámetro *LinkedMasterAccount* especifica la cuenta de usuario de Active Directory en el bosque de cuentas al cual desea conectar el buzón de correo. El parámetro *LinkedDomainController* especifica un controlador de dominios en el bosque de cuentas.

    Connect-Mailbox -Identity "Temp User" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount danpark@fabrikam.com -Alias dpark

En este ejemplo se conecta un buzón de sala.

    Connect-Mailbox -Identity "rm2121" -Database "MBXResourceDB" -User "Conference Room 2121" -Alias ConfRm2121 -Room

En este ejemplo se conecta un buzón de equipo.

    Connect-Mailbox -Identity "MotorPool01" -Database "MBXResourceDB" -User "Van01 (12 passengers)" -Alias van01 -Equipment

En este ejemplo se conecta un buzón de correo compartido.

    Connect-Mailbox -Identity "Printer Support" -Database MBXDB01 -User "Corp Printer Support" -Alias corpprint -Shared


> [!NOTE]
> También puede usar los valores <CODE>LegacyDN</CODE> o <CODE>MailboxGuid</CODE> para identificar el buzón de correo eliminado.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Connect-Mailbox](https://technet.microsoft.com/es-es/library/aa997878\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó un buzón de correo eliminado conectado a una cuenta de usuario, siga uno de estos procedimientos:

  - En el EAC, haga clic en **Destinatarios**, vaya a la página adecuada al tipo de buzón de correo que haya conectado, haga clic en **Refrescar** ![Icono Actualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icono Actualizar"), y compruebe que el buzón de correo aparezca.

  - En Usuarios y equipos de Active Directory, haga clic con el botón secundario a la cuenta de usuario conectada al buzón de correo y, a continuación, haga clic en **Propiedades**. En la pestaña **General**, observe que el cuadro **Correo electrónico** contiene la dirección electrónica del buzón de correo conectado.

  - En el Shell, ejecute el siguiente comando.
    
    ```powershell
Get-User <identity>
```
    
    El valor **UserMailbox** de la propiedad *RecipientType* indica que la cuenta de usuario y el buzón de correo están conectados. También puede ejecutar el comando **Get-Mailbox \<identity\>** para verificar que el buzón de correo estaba conectado.

## Restaurar un buzón de correo eliminado

Puede usar el Shell para restaurar un buzón de correo eliminado en un buzón de correo existente usando el cmdlet **New-MailboxRestoreRequest**. Al restaurar un buzón de correo eliminado, sus contenidos se copian en un buzón de correo existente, que se denomina *buzón de correo de destino*. Cuando se restaura un buzón de correo eliminado, se retiene en la base de datos de buzones de correo hasta que un administrador lo elimina permanentemente o lo purga cuando expira el período de retención del buzón de correo eliminado.

Cuando una solicitud de restauración de buzones de correo se completa correctamente, se retiene durante 30 días, de forma predeterminada, antes de que se quite. Puede quitarlo más rápidamente con el cmdlet **Remove-StoreMailbox**.


> [!NOTE]
> No puede usar el EAC para restaurar un buzón de correo eliminado.



## Usar el Shell para restaurar un buzón eliminado

Para crear una solicitud de restauración de buzones de correo, debe usar el nombre para mostrar, el nombre distintivo heredado (DN) o el GUID del buzón de correo del buzón de correo eliminado. Use el cmdlet **Get-MailboxStatistics** para mostrar los valores de las propiedades `DisplayName`, `MailboxGuid` y `LegacyDN` del buzón de correo eliminado que desee restaurar. Por ejemplo, ejecute el siguiente comando para devolver esta información a todos los buzones de correo deshabilitados y eliminados de su organización.

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "Disabled"} | fl DisplayName,MailboxGuid,LegacyDN,Database

Este ejemplo restaura el buzón de correo eliminado, que se identifica con el parámetro *SourceStoreMailbox* y se encuentra en la base de datos de buzones de correo MBXDB01, en el buzón de correo de destino de Debra Garcia. El parámetro *AllowLegacyDNMismatch* se usa para que el buzón de correo de origen se pueda restaurar en otro buzón de correo, uno que no tenga el mismo valor DN heredado.

    New-MailboxRestoreRequest -SourceStoreMailbox e4890ee7-79a2-4f94-9569-91e61eac372b -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

Este ejemplo restaura el buzón de correo de archivo eliminado de Pilar Pinilla en su buzón de correo de archivo actual. El parámetro *AllowLegacyDNMismatch* no es necesario porque un buzón de correo principal y su buzón de correo de archivo correspondiente tienen el mismo DN heredado.

    New-MailboxRestoreRequest -SourceStoreMailbox "Personal Archive - Pilar Pinilla" -SourceDatabase "MDB01" -TargetMailbox pilarp@contoso.com -TargetIsArchive

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)).

## Usar el Shell para restaurar un buzón de carpeta pública eliminado

Si se elimina de forma permanente un buzón de carpetas públicas que desea restaurar y el buzón está dentro del límite de retención de elementos eliminados (consulte [Configurar la retención de elementos eliminados y las cuotas de elementos recuperables](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)), puede usar el cmdlet `Connect-Mailbox`, seguido del cmdlet `Update-StoreMailboxState`. Para obtener más información acerca de la sintaxis y los parámetros, vea [Connect-Mailbox](https://technet.microsoft.com/es-es/library/aa997878\(v=exchg.150\)) y [Update-StoreMailboxState](https://technet.microsoft.com/es-es/library/jj860462\(v=exchg.150\)).

Necesitará el GUID del buzón de carpeta pública eliminado, así como el GUID o nombre de la base de datos de buzones que contenía el buzón de carpeta pública. Si no tiene esta información, puede llevar a cabo los siguientes pasos:

1.  Para obtener el nombre de dominio completo (FQDN) del controlador de dominio y bosque de Active Directory, ejecute el siguiente cmdlet:
    
    ```powershell
Get-OrganizationConfig | fl OriginatingServer
```

2.  Con la información devuelta por el paso 1, busque el contenedor de objetos eliminados en Active Directory para el GUID del buzón de carpeta pública y el GUID o nombre de la base de datos de buzones de correo en la que se encontraba el buzón de carpeta pública eliminado.
    

    > [!TIP]
    > Puede buscar objetos eliminados mediante un script personalizado o mediante el uso de la herramienta Ldp, que se puede abrir escribiendo <STRONG>ldp.exe</STRONG> en un símbolo del sistema de Powershell.



Si conoce el GUID del buzón de carpeta pública eliminado y el nombre o GUID de la base de datos del buzón en la que se encontraba el buzón de carpeta pública, ejecute los comandos siguientes para restaurar el buzón de carpeta pública.

1.  Cree un nuevo objeto de Active Directory ejecutando los comandos siguientes (es posible que deba proporcionar las credenciales adecuadas):
    
        New-MailUser <mailUserName> -ExternalEmailAddress <emailAddress> 
        
        Get-MailUser <mailUserName> | Disable-MailUser
    
    Donde `<mailUserName>`, `<emailAddress>` y `<mailUserName>` son valores que usted elige. Tendrá que usar el mismo valor `<mailUserName>` en el paso siguiente.

2.  Conecte el buzón de carpeta pública eliminado para el objeto de Active Directory que acaba de crear ejecutando el siguiente comando:
    
        Connect-Mailbox -Identity <public folder mailbox GUID> -Database <database name or GUID> -User <mailUserName>
    

    > [!NOTE]
    > El parámetro <CODE>Identity</CODE> especifica el objeto de buzón en la base de datos de Exchange para conectarlo a un objeto de usuario de Active Directory. En el ejemplo anterior, se especifica el GUID de buzón de carpeta pública, pero también puede usar el valor de nombre para mostrar o el valor de LegacyExchangeDN.



3.  Ejecute `Update-StoreMailboxState` en el buzón de carpeta pública, con base en el ejemplo siguiente:
    
        Update-StoreMailboxState -Identity <public folder mailbox GUID> -Database <database name or GUID>
    
    Como en el paso 2, el parámetro `Identity` acepta valores de LegacyExchangeDN, nombre para mostrar o GUID para el buzón de carpeta pública.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se ha restaurado correctamente un buzón de carpeta pública eliminado, ejecute el cmdlet **Get-PublicFolder -GetChildren -\<GUID del buzón de carpeta pública\>**. Si la restauración se realizó correctamente, este cmdlet funcionará.

Para obtener más información, vea:

  - [Connect-Mailbox](https://technet.microsoft.com/es-es/library/aa997878\(v=exchg.150\))

  - [Update-StoreMailboxState](https://technet.microsoft.com/es-es/library/jj860462\(v=exchg.150\))

