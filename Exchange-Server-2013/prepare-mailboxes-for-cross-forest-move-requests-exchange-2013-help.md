---
title: 'Preparar los buzones para las solicitudes de movimiento entre bosques: Exchange 2013 Help'
TOCTitle: Preparar los buzones para las solicitudes de movimiento entre bosques
ms:assetid: fdbed4fc-a77e-40d5-a211-863b05d74784
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633491(v=EXCHG.150)
ms:contentKeyID: 49896039
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Preparar los buzones para las solicitudes de movimiento entre bosques

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-11-22_

**Resumen:**  aprender acerca de cómo preparar los buzones para traslados entre bosques en Exchange 2013.

Microsoft Exchange 2013 es compatible con operaciones de mover buzones y migraciones mediante el Shell de administración de Exchange, en concreto los cmdlets **New-MoveRequest** y **New-MigrationBatch** . También puede mover el buzón a través de centro de administración de Exchange (EAF). Tenga en cuenta que puede mover buzones de Exchange 2010 y 2013 de Exchange en un bosque de Exchange de 2013.

Para mover un buzón de un bosque Exchange a un bosque de Exchange 2013, el bosque de destino Exchange 2013 debe contener un usuario habilitado para correo válido con un conjunto especificado de atributos Active Directory. Si hay al menos un servidor de acceso de cliente de Exchange 2013 implementado en el bosque, el bosque se considera un bosque Exchange 2013.

Para preparar el movimiento de los buzones de correo, debe crear usuarios habilitados para correo con los atributos necesarios en el bosque de destino. A continuación se describen los dos métodos recomendados para crear usuarios habilitados para correo con los atributos necesarios:

  - Si ha implementado Microsoft Identity Lifecycle Manager (ILM) para la sincronización de la lista global de direcciones entre bosques (GAL), el método recomendado consiste en usar Service Pack 1 (SP1) para ILM 2007 Feature Pack 1 (FP1). Hemos creado un código de ejemplo que puede usar para aprender a personalizar ILM y sincronizar el usuario del buzón de origen con el usuario del buzón de destino.
    
    Para obtener más información, incluyendo cómo descargar el código de ejemplo, vea [Preparar buzones para movimientos entre bosques mediante código de ejemplo](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md).

  - Si creó el usuario de correo de destino mediante una herramienta de Active Directory que no sea ILM/MIIS, use el cmdlet **Update-Recipient** con el parámetro *Identity* para ejecutar el servicio de Libreta de direcciones, a fin de generar **LegacyExchangeDN** para el usuario de correo de destino. Hemos creado una secuencia de comandos modelo de Windows PowerShell que lee de Active Directory, escribe en él e invoca el cmdlet **Update-Recipient**.
    
    Para obtener más información acerca del uso de este script de ejemplo, vea [Preparar buzones para moverlos entre bosques con el script Prepare-MoveRequest.ps1 en el Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md).

Después de crear el usuario de correo de destino, puede ejecutar los cmdlet **New-MoveRequest** o **New-MigrationBatch** para mover el buzón al bosque de Exchange 2013 de destino.

Para obtener más información acerca de las solicitudes remotas de movimiento, vea los siguientes temas:

  - [New-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219166\(v=exchg.150\))

  - [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\))

Para obtener más información acerca de los movimientos remotos de buzones y los movimientos remotos heredados, vea [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

El resto de este tema describe los atributos del usuario de correo de Active Directory necesarios para un movimiento de buzón. Estos atributos se configuran cuando usa el código o la secuencia de comandos para prepararse para el movimiento del buzón. Sin embargo, puede copiar manualmente estos atributos utilizando un editor de Active Directory.

## Atributos de usuario de Active Directory requeridos para movimientos de buzones

Como ayuda para mover un buzón remoto, el objeto de usuario de correo en el bosque de Exchange 2013 de destino debe tener los atributos de Active Directory que se describen en esta sección:

  - Atributos obligatorios

  - Atributos opcionales

  - Atributos vinculados

  - Atributos de usuario vinculados

  - Atributos del buzón de recursos

  - Atributos adicionales

## Atributos obligatorios

En la tabla siguiente se indica el conjunto mínimo de atributos que se deben configurar en ILM en el usuario de correo de destino para que el cmdlet **New-MoveRequest** funcione correctamente.

### Atributos de usuario de correo

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Los atributos de Active Directory del usuario de correo</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>displayName</strong></p></td>
<td><p>Copie el atributo correspondiente del buzón de origen o genere un valor nuevo.</p></td>
</tr>
<tr class="even">
<td><p><strong>Mail</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mailNickname</strong></p></td>
<td><p>Copie el atributo correspondiente del buzón de origen o genere un valor nuevo.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchArchiveGUID and msExchArchiveName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen. Los atributos sólo están disponibles si el buzón de origen es de Exchange 2010.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMailboxGUID</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>-2147483642 (decimal) //equivalente a 0x80000006 (hex).</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientTypeDetails</strong></p></td>
<td><p>128 (decimal) / 0 x 80 (hex).</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUserCulture</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchVersion</strong></p></td>
<td><p>44220983382016 (decimal).</p></td>
</tr>
<tr class="even">
<td><p><strong>cn</strong></p></td>
<td><p>Copie el atributo correspondiente del buzón de origen o genere un valor nuevo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>proxyAddresses</strong></p></td>
<td><p>Copie el atributo <strong>proxyAddresses</strong> del buzón de origen. Además, copie <strong>LegacyExchangeDN</strong> del buzón de origen como dirección X500 en el atributo <strong>proxyAddresses</strong> del usuario de correo de destino.</p>

> [!NOTE]
> <STRONG>proxyAddresses</STRONG> del usuario del buzón de origen debe contener una dirección SMTP que coincida con el dominio autoritativo del bosque de destino. De este modo, el cmdlet <STRONG>New-MoveRequest</STRONG> puede seleccionar correctamente el valor <STRONG>targetAddress</STRONG> del usuario habilitado para correo de origen (convertido a partir del usuario del buzón de origen una vez completada la solicitud de movimiento de buzón) para garantizar que el enrutamiento del correo sigue operativo.


</td>
</tr>
<tr class="even">
<td><p><strong>sAMAccountName</strong></p></td>
<td><p>Copie el atributo correspondiente del buzón de origen o genere un valor nuevo.</p>
<p>Compruebe que el valor sea exclusivo dentro del dominio del bosque de destino al que pertenece el usuario de correo de destino.</p></td>
</tr>
<tr class="odd">
<td><p><strong>targetAddress</strong></p></td>
<td><p>Establezca una dirección SMTP en el atributo <strong>proxyAddresses</strong> del buzón de origen.</p>
<p>Esta dirección SMTP debe pertenecer al dominio autoritativo del bosque de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>userAccountControl</strong></p></td>
<td><p>Constante: 514 //equivalente a 0x202, ACCOUNTDISABLE | NORMAL_ACCOUNT.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userPrincipalName</strong></p></td>
<td><p>Copie el atributo correspondiente del buzón de origen o genere un valor nuevo. Debido a que el usuario de correo tiene deshabilitado el inicio de sesión, no se utiliza este <strong>userPrincipalName</strong>.</p></td>
</tr>
</tbody>
</table>


## Atributos opcionales

Es obligatorio haber configurado los atributos siguientes para que el cmdlet **New-MoveRequest** funcione correctamente; sin embargo, su sincronización proporciona una mejor experiencia entre los usuarios finales una vez movido el buzón. Puesto que la GAL en el bosque de destino muestra este usuario de correo de destino, establezca los siguientes atributos relacionados con la GAL.

### Atributos relacionados con la GAL

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Los atributos de Active Directory del usuario de correo</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>c</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>co</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>countryCode</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>company</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>department</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>facsimileTelephoneNumber</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>givenName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>homePhone</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>info</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>initials</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>l</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>mobile</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchAssistantName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchHideFromAddressLists</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherHomePhone</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherTelephone</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pager</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>physicalDeliveryOfficeName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalCode</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>sn</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>st</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>streetAddress</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>telephoneAssistant</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>telephoneNumber</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>title</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
</tbody>
</table>


## Atributos vinculados

Un atributo vinculado es un atributo de Active Directory que hace referencia a otros objetos de Active Directory en el bosque local. Los valores del atributo vinculado no se pueden copiar directamente desde un buzón en el bosque de origen a un usuario de correo en el bosque de destino. En primer lugar hay que encontrar los objetos de Active Directory en el bosque de origen a los que hace referencia el atributo del buzón de origen. A continuación hay que encontrar los objetos de Active Directory correspondientes en el bosque de destino para el objeto de Active Directory mencionado anteriormente en el bosque de origen. Finalmente, establezca el atributo del usuario de correo de destino para que haga referencia a los objetos de Active Directory en el bosque de destino.

### Atributos vinculados

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Los atributos de Active Directory del usuario de correo</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>altRecipient</strong></p></td>
<td><p>Se corresponde con <strong>altRecipient</strong> atributo del buzón origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>deliverAndRedirect</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen. Este atributo es un valor booleano que se debe establecer junto con <strong>altRecipient</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Manager</strong>(y sus backlinks)</p></td>
<td><p>Corresponde al atributo del administrador del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>MemberOf</strong>(backlinks)</p></td>
<td><p>Éste es el backlink del atributo de miembro del grupo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>publicDelegates</strong>(y sus backlinks)</p></td>
<td><p>Se corresponde con <strong>publicDelegates</strong> atributo del buzón origen.</p></td>
</tr>
</tbody>
</table>


## Atributos de usuario vinculados

Si desea mover un buzón a un bosque de recursos de Exchange 2013, se considerará que el buzón en el bosque de recursos es un *buzón vinculado*. En este escenario tendrá que crear un usuario de correo vinculado en el bosque de recursos (de destino). Para crear un usuario de correo vinculado debe establecer los atributos que se muestran en la tabla siguiente.

### Atributos de usuario de correo vinculado

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Los atributos de Active Directory del usuario de correo</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchMasterAccountHistory</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMasterAccountSid</strong></p></td>
<td><p>Si el buzón de origen ha de <strong>msExchMasterAccountSid</strong> , cópielo. De lo contrario, copiar de <strong>objectSid</strong> del buzón de origen .</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>Constante:-1073741818 de //equivalent (decimal) a * sin signo * 0xC0000006.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Un buzón vinculado únicamente se puede crear si hay confianza entre el bosque de origen y el de destino.



Si el objeto de origen está deshabilitado y el atributo **msExchMasterAccountSid** está establecido como sí mismo (buzón de recurso, buzón compartido), no indique nada en el usuario de destino.

Si el objeto de origen está deshabilitado y no se ha establecido el atributo **msExchMasterAccountSid**, el buzón no será válido.

Si el objeto de origen está habilitado y se ha establecido el atributo **msExchMasterAccountSid**, el buzón no será válido.

## Atributos del buzón de recursos

Si desea mover un buzón de recursos a un bosque de Exchange 2013, establezca los atributos que se indican en la tabla siguiente para el usuario de correo de destino.

### Atributos del buzón de recursos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Los atributos de Active Directory del usuario de correo</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>Si el buzón de origen es una sala de conferencias:</p>
<ul>
<li><p><strong>Constante</strong>-2147481850 de //equivalent (decimal) a * sin signo * 0x80000706.</p></li>
</ul>
<p>Si el buzón de origen es un buzón de equipos:</p>
<ul>
<li><p><strong>Constante</strong>-2147481594 de //equivalent (decimal) a * sin signo * 0x80000806.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceCapacity</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceDisplay</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceMetaData</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceSearchProperties</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
</tbody>
</table>


## Atributos adicionales

En Exchange 2007, el cmdlet **Move-Mailbox** copió también los atributos que se muestran en la tabla siguiente en el momento de mover un buzón. Si lo desea, puede copiar estos atributos si se requiere su organización.

### Atributos del buzón de recursos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Los atributos de Active Directory del usuario de correo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>comment</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>deletedItemFlags</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>delivContLength</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>departmentNumber</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>description</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>division</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeID</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>employeeNumber</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeType</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>extensionAttribute1-15</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>homePostalAddress</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>internationalISDNNumber</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ipPhone</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>language</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>lmPwdHistory</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>localeID</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mAPIRecipient</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>middleName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticCompanyName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticDepartment</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticDisplayName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticFirstName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticLastName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchBlockedSendersHash</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCExpirySuspensionEnd</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchELCExpirySuspensionStart</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCMailboxFlags</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchExternalOOFOptions</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneFlags</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLDeleteThreshold</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLJunkThreshold</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLQuarantineThreshold</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLRejectThreshold</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMDBRulesQuota</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchPoliciesExcluded</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchSafeRecipientsHash</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchSafeSendersHash</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUMSpokenName</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherFacsimileTelephoneNumber</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherIpPhone</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherMobile</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherPager</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>preferredDeliveryMethod</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>personalPager</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>personalTitle</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>photo</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pOPCharacterSet</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>pOPContentFormat</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalAddress</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>postOfficeBox</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>primaryInternationalISDNNumber</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>primaryTelexNumber</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>showInAdvancedViewOnly</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>street</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>terminalServer</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>textEncodedORAddress</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>thumbnailLogo</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>thumbnailPhoto</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>url</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>userCert</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userCertificate</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>userSMIMECertificate</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>wWWHomePage</strong></p></td>
<td><p>Copie directamente el atributo correspondiente del buzón de origen.</p></td>
</tr>
</tbody>
</table>

