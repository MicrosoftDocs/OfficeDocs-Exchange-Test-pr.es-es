---
title: 'Deshabilitar o eliminar un buzón de correo: Exchange 2013 Help'
TOCTitle: Deshabilitar o eliminar un buzón de correo
ms:assetid: 31ad25d6-2942-4fd9-aecb-cdf9654163d2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ863434(v=EXCHG.150)
ms:contentKeyID: 50556765
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Deshabilitar o eliminar un buzón de correo

 

_**Se aplica a:** Exchange Server 2013 SP1_

_**Última modificación del tema:** 2015-03-09_

Puede usar el EAC o el Shell para deshabilitar o eliminar un buzón en Exchange 2013. Cuando se deshabilita o se elimina un buzón de correo, Exchange retiene el buzón en la base de datos de buzones de correo y cambia el estado del buzón a deshabilitado. Los buzones de correo deshabilitados y eliminados se conservan en la base de datos de buzones de correo hasta que expira el período de retención del buzón de correo eliminado, que, de manera predeterminada, es de 30 días. Una vez que el período de retención expira, el buzón de correo de elimina permanentemente o se *purga*.

Si necesita eliminar un buzón en Exchange Online, vea [Eliminar o restaurar buzones de usuario en Exchange Online](https://technet.microsoft.com/es-es/library/dn186233\(v=exchg.150\)).


> [!NOTE]
> Los buzones de correo eliminados o deshabilitados se denominan <EM>buzones desconectados</EM>.



La principal diferencia entre eliminar y deshabilitar un buzón de correo es que, cuando lo deshabilita, los atributos de Exchange se eliminan de la cuenta de usuario de Active Directory correspondiente, pero la cuenta de usuario se conserva. Cuando elimina un buzón de correo, tanto los atributos de Exchange como la cuenta de usuario de Active Directory se eliminan. Esta diferencia también determina sus opciones para reconectar o restaurar buzones de correo deshabilitados o eliminados.

En la siguiente tabla, se muestra qué tipos de buzones de Exchange puede deshabilitar y eliminar.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de buzón</th>
<th>¿Se puede deshabilitar?</th>
<th>¿Se puede eliminar?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Buzón de archivo</p></td>
<td><p>Sí</p></td>
<td><p>No*</p></td>
</tr>
<tr class="even">
<td><p>Buzón vinculado</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Buzón de recursos (sala o equipo)</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Buzón compartido</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Buzón de usuario</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


\* Si un buzón de archivo está habilitado, se eliminará cuando el buzón de correo principal se elimine. Para obtener información acerca de la deshabilitación de buzones de archivo, vea [Administrar archivos locales en Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

Si un administrador elimina una cuenta de usuario que tiene un buzón de correo, el almacén de información de Exchange detectará en un momento dado que el buzón ya no está conectado a una cuenta de usuario y lo marcará para su eliminación, incluso si el buzón está en retención. Si desea conservar el buzón de correo, debe hacer lo siguiente:

1.  En lugar de eliminar la cuenta de usuario, deshabilítela.

2.  Cambie las propiedades del buzón para restringir su uso y tener acceso al buzón de correo. Por ejemplo, establezca las cuotas de envío y recepción en 1, bloquee quién puede enviar mensajes al buzón y restrinja quién puede tener acceso al buzón.

3.  Retenga el buzón hasta que se hayan eliminado todos los datos o hasta que ya no sea necesaria la retención.

Para otras tareas de administración relacionadas con buzones de correo desconectados, vea estos temas:

  - [Buzones desconectados](disconnected-mailboxes-exchange-2013-help.md)

  - [Conectar un buzón de correo deshabilitado](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Conectar o restaurar un buzón eliminado](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Eliminar permanentemente un buzón de correo](permanently-delete-a-mailbox-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Deshabilitación de un buzón de correo

Como se mencionó anteriormente, cuando deshabilita un buzón de correo, los atributos de Exchange se eliminan de la cuenta de usuario de Active Directory correspondiente, pero la cuenta de usuario se conserva.

## Uso del EAC para deshabilitar un buzón de correo

El siguiente procedimiento muestra cómo deshabilitar un buzón de usuario. Use el mismo procedimiento para deshabilitar otros tipos de buzón después de navegar a la página correspondiente en el EAC.

1.  En el EAC, vaya a **Destinatarios** \>**Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón de correo que desea deshabilitar.

3.  Haga clic en **Más**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") y, a continuación, en **Deshabilitar**.

4.  Aparece una advertencia que le pregunta si está seguro de querer deshabilitar el buzón de correo. Haga clic en **Sí** para deshabilitar el buzón.

El buzón de correo se elimina de la lista de buzones.

## Usar el Shell para deshabilitar un buzón de correo

Use el siguiente comando para deshabilitar buzones de correo de usuario, buzones vinculados, buzones de recurso y buzones compartidos.

    Disable-Mailbox <identity>

Cuando ejecute este comando, aparecerá un mensaje que le solicitará que confirme que desea deshabilitar el buzón de correo.

A continuación, se muestran algunos ejemplos de comandos para deshabilitar buzones de correo.
```
    Disable-Mailbox danj
```
```
    Disable-Mailbox "Conf Room 31/1234 (12)"
```
```
    Disable-Mailbox sharedmbx@contoso.com
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya deshabilitado un buzón de correo correctamente, siga uno de estos pasos:

  - En el EAC, haga clic en **Destinatarios**, navegue a la página correspondiente para el tipo de buzón de correo que deshabilitó y compruebe que el buzón ya no figure.

  - En Usuarios y equipos de Active Directory, haga clic con el botón secundario del mouse en la cuenta de usuario del buzón de correo que deshabilitó y, a continuación, haga clic en **Propiedades**. En la ficha **General**, compruebe que el campo **Correo electrónico** esté en blanco. Esto comprueba que el buzón de correo esté deshabilitado pero la cuenta de usuario aún exista.

  - En el Shell, ejecute el siguiente comando.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    El valor `Disabled` en la propiedad *DisconnectReason* indica que el buzón de correo está deshabilitado.
    

    > [!NOTE]
    > Cuando elimina un buzón de correo, el valor en la propiedad <EM>DisconnectReason</EM> también es <CODE>Disabled</CODE>. Sin embargo, la cuenta de usuario de Active Directory correspondiente se elimina.



  - En el Shell, ejecute el siguiente comando.
    
        Get-User <identity>
    
    Tenga en cuenta que el valor para la propiedad *RecipientType* es `User`, en vez de `UserMailbox`, que es el valor para los usuarios con buzones de correo habilitados. Esto también comprueba que el buzón de correo esté deshabilitado pero la cuenta de usuario se conserve.

## Eliminación de un buzón de correo

Como se mencionó anteriormente, cuando se elimina un buzón de correo, tanto los atributos de Exchange como la cuenta de usuario de Active Directory se eliminan. El buzón de correo (y el buzón de archivo, si está habilitado) se eliminarán de manera permanente de la base de datos de buzones de correo cuando expire el período de retención del buzón de correo.

## Uso del EAC para eliminar un buzón de correo

El siguiente procedimiento muestra cómo eliminar un buzón de usuario. Use el mismo procedimiento para eliminar otros tipos de buzón después de navegar a la página correspondiente en el EAC.

1.  En el EAC, vaya a **Destinatarios** \>**Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón que desea eliminar y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

3.  Aparece una advertencia que le pregunta si está seguro de querer eliminar el buzón de correo. Haga clic en **Sí** para eliminar el buzón.

El buzón de correo se elimina de la lista de buzones.

## Uso del Shell para eliminar un buzón de correo

Use el siguiente comando para eliminar buzones de correo de usuario, buzones vinculados, buzones de recurso y buzones compartidos.

    Remove-Mailbox <identity>

Cuando ejecute este comando, aparecerá un mensaje que le solicitará que confirme que desea eliminar el buzón de correo y la cuenta de usuario de Active Directory correspondiente.

A continuación, se muestran algunos ejemplos de comandos para eliminar buzones de correo.
```
    Remove-Mailbox pilarp@contoso.com
```
```
    Remove-Mailbox "Fleet Van (16)"
```
```
    Remove-Mailbox corpprint
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya eliminado un buzón de usuario correctamente, siga uno de estos conjuntos de procedimientos de verificación.

1.  En el EAC, haga clic en **Destinatarios**, navegue a la página correspondiente para el tipo de buzón de correo que eliminó, y compruebe que el buzón ya no figure.

2.  En Usuarios y equipos de Active Directory, compruebe que la cuenta de usuario correspondiente ya no figure.

O bien

1.  Ejecute el siguiente comando para comprobar que el buzón se haya eliminado.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    El valor `Disabled` en la propiedad *DisconnectReason* indica que el buzón de correo se ha eliminado.
    

    > [!NOTE]
    > Cuando deshabilita un buzón de correo, el valor en la propiedad <EM>DisconnectReason</EM> también es <CODE>Disabled</CODE>. Sin embargo, la cuenta de usuario de Active Directory correspondiente se conserva.



2.  Ejecute el siguiente comando para comprobar que la cuenta de usuario de Active Directory se haya eliminado.
    
        Get-User <identity>
    
    El comando devolverá un error que indica que no se pudo encontrar el usuario, lo que comprobará que la cuenta se eliminó.

