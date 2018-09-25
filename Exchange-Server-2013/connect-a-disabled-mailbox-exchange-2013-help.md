---
title: 'Conectar un buzón de correo deshabilitado: Exchange 2013 Help'
TOCTitle: Conectar un buzón de correo deshabilitado
ms:assetid: a8abd399-75fd-4ee2-b2e4-634b55e4f79f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ863439(v=EXCHG.150)
ms:contentKeyID: 50556844
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectar un buzón de correo deshabilitado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-13_

Puede usar el EAC o el Shell para conectar un buzón de correo deshabilitado en una cuenta de usuario de Active Directory. Cuando deshabilita un buzón de correo, Exchange retiene el buzón en la base de datos del buzón y conmuta el buzón de correo a un estado de deshabilitado. Los atributos de Exchange también se quitan de la cuenta del usuario de Active Directory correspondiente, pero la cuenta del usuario se retiene. El buzón de correo se retiene hasta que expira el período de retención del buzón de correo eliminado, que es de 30 días de forma predeterminada, y, a continuación, se elimina permanentemente (o *se purga*) de la base de datos de buzones de correo.

Hasta que un buzón de correo se deshabilita permanentemente de la base de datos de buzones de Exchange, puede usar el EAC o el Shell para volver a conectarlo a la cuenta de usuario de Active Directory original.

Para obtener más información acerca de los buzones de correo desconectados y realizar otras tareas de administración, consulte los siguientes temas:

  - [Buzones desconectados](disconnected-mailboxes-exchange-2013-help.md)

  - [Deshabilitar o eliminar un buzón de correo](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Conectar o restaurar un buzón eliminado](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Eliminar permanentemente un buzón de correo](permanently-delete-a-mailbox-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Ejecute el cmdlet **Get-User** en el Shell para verificar que la cuenta del usuario de Active Directory al cual desea conectar el buzón de correo deshabilitado existe y todavía no está asociado a otro buzón de correo. Para conectar un buzón de correo deshabilitado a una cuenta de usuario, la cuenta debe existir y el valor de la propiedad *RecipientType* debe ser `User`, lo que indica que la cuenta todavía no tiene un buzón de correo habilitado.
    
    Para las organizaciones de Exchange locales, también puede verificar esta información en usuarios y equipos de Active Directory.

  - Ejecute el siguiente comando para verificar que el buzón de correo deshabilitado al cual desea conectar una cuenta de usuario existe en la base de datos del buzón de correo y que no se trata de un buzón de correo eliminado temporalmente.
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    ```
    
    Para poder conectar un buzón de correo deshabilitado, el buzón de correo debe existir en la base de datos de buzones de correo y el valor de la propiedad *DisconnectReason* debe ser `Disabled`. Si el buzón de correo no se ha purgado de la base de datos, el comando no devolverá ningún resultado.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para conectar un buzón deshabilitado

El siguiente procedimiento muestra cómo conectar un buzón de usuario deshabilitado. También puede volver a conectar buzones de correo enlazados deshabilitados y buzones de correo compartidos deshabilitados a la cuenta del usuario correspondiente.

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  Haga clic en **Más**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") y, a continuación, haga clic en **Conectar un Buzón de correo**.
    
    Se mostrará una lista de buzones de correo desconectados en el servidor de Exchange de su organización de Exchange.
    

    > [!NOTE]
    > Esta lista de buzones de correo desconectados incluye buzones de correo deshabilitados, buzones de correo eliminados y buzones de correo eliminados temporalmente.



3.  Haga clic en el buzón de correo deshabilitado que desee volver a conectar y, a continuación, haga clic en **Conectar**.

4.  Ante la ventana que pregunta si está seguro de querer volver a conectar el buzón de correo, haga clic en **Sí**.
    
    Exchange volverá a conectar el buzón de correo deshabilitado a la cuenta de usuario correspondiente.

## Usar el Shell para conectar un buzón deshabilitado

Use el cmdlet **Connect-Mailbox** en el Shell para conectar una cuenta de usuario a un buzón de correo deshabilitado. Tiene que especificar el tipo de buzón de correo que está conectando. Los siguientes ejemplos muestran la sintaxis para volver a conectar buzones de correo de usuario, enlazados y compartidos.

En este ejemplo se conecta un buzón de correo de usuario. El parámetro *Identity* especifica el buzón de correo desconectado en una base de datos de Exchange. El parámetro *User* especifica la cuenta de usuario de Active Directory que desea volver a conectar al buzón de correo.

```powershell
Connect-Mailbox -Identity "Jeffrey Zeng" -Database MBXDB01 -User "Jeffrey Zeng"
```

En este ejemplo se conecta un buzón vinculado. El parámetro *Identity* especifica el buzón de correo desconectado en una base de datos de Exchange. El parámetro *LinkedMasterAccount* especifica la cuenta de usuario de Active Directory en el bosque de cuentas al cual desea volver a conectar el buzón de correo. El parámetro *Alias* especifica el alias, que es la porción de la dirección de correo electrónico ubicada a la izquierda del símbolo (@).

```powershell
Connect-Mailbox -Identity "Kai Axford" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount kai.axford@fabrikam.com -Alias kaia
```

En este ejemplo se conecta un buzón de correo compartido.

```powershell
Connect-Mailbox -Identity "Corporate Shared Mailbox" -Database "Mailbox Database 03" -User "Corporate Shared Mailbox" -Alias corpshared -Shared
```


> [!NOTE]
> Si no incluye el parámetro <EM>Alias</EM> cuando ejecute el cmdlet <STRONG>Connect-Mailbox</STRONG>, el valor especificado en el parámetro <EM>User</EM> o <EM>LinkedMasterAccount</EM> se usa para crear un alias de dirección electrónica para el buzón de correo que se ha vuelto a conectar.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Connect-Mailbox](https://technet.microsoft.com/es-es/library/aa997878\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó un buzón de correo deshabilitado conectado a una cuenta de usuario, siga uno de estos procedimientos:

  - En el EAC, haga clic en **Destinatarios**, vaya a la página adecuada al tipo de buzón de correo que haya vuelto a conectar, haga clic en **Refrescar**![Icono Actualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icono Actualizar"), y compruebe que el buzón de correo aparezca.

  - En Usuarios y equipos de Active Directory, haga clic con el botón secundario a la cuenta de usuario cuyo buzón de correo deshabilitó y, a continuación, haga clic en **Propiedades**. En la pestaña **General**, observe que el cuadro **Correo electrónico** contiene la dirección electrónica del buzón de correo conectado de nuevo.

  - En el Shell, ejecute el siguiente comando.
    
    ```powershell
    Get-User <identity>
    ```
    
    El valor **UserMailbox** de la propiedad *RecipientType* indica que la cuenta de usuario y el buzón de correo están conectados. También puede ejecutar el cmdlet **Get-Mailbox** para verificar que el buzón de correo exista.

