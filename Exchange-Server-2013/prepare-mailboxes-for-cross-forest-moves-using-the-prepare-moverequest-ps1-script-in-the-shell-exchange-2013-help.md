---
title: 'Preparar buzones para moverlos entre bosques con el script Prepare-MoveRequest.ps1 en el Shell: Exchange 2013 Help'
TOCTitle: Preparar buzones para moverlos entre bosques con el script Prepare-MoveRequest.ps1 en el Shell
ms:assetid: 2cea59fb-69b7-4a2f-833f-de4d93cf1810
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee861103(v=EXCHG.150)
ms:contentKeyID: 49895542
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Preparar buzones para moverlos entre bosques con el script Prepare-MoveRequest.ps1 en el Shell

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2017-11-22_

**Resumen:** aprender a administrar operaciones de mover buzones entre bosques y migraciones en Exchange 2013 mediante la secuencia de comandos de MoveRequest.ps1 de preparación en el Shell de administración de Exchange.

Microsoft Exchange 2013 es compatible con operaciones de mover buzones y migraciones mediante los cmdlets **New-MoveRequest** y **New-MigrationBatch** . También puede mover el buzón a través de centro de administración de Exchange (EAF). Puede mover un Exchange 2010 o un buzón de Exchange de 2013 un bosque de origen Exchange a un bosque de destino Exchange 2013.

Para ejecutar los cmdlets **New-MoveRequest** y **New-MigrationBatch**, debe existir un usuario de correo en el bosque de Exchange de destino y el usuario de correo debe contar con un conjunto mínimo de atributos de Active Directory obligatorios.

El script de Windows PowerShell que se describe en este tema admite esta tarea mediante la sincronización de usuarios de buzones de correo desde un bosque de origen de Exchange 2013 hasta bosques de destino de Exchange 2013 como usuarios habilitados para correo. El script copia los atributos de Active Directory de los usuarios de buzón de correo en el bosque de origen hacia el bosque de destino y, a continuación, usa el cmdlet **Update-Recipient** para convertir los objetos de destino en usuarios habilitados para correo.

Para obtener más información acerca de cómo utilizar y escribir secuencias de comandos, vea [Scripting con el Shell de administración de Exchange](https://technet.microsoft.com/es-es/library/bb123798\(v=exchg.150\)). Para obtener más información acerca de cómo preparar para traslados entre bosques, vea [Preparar los buzones para las solicitudes de movimiento entre bosques](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con las solicitudes remotas de traslado? Vea [Administración de movimientos locales](manage-on-premises-moves-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Busque la secuencia de comandos en la siguiente ubicación: Program Files\\Microsoft\\Exchange Server\\V15\\Scripts

  - Para ejecutar el script de ejemplo, necesita lo siguiente:
    
      - Un bosque de origen de Exchange, donde reside actualmente el buzón. Esto puede ser un buzón de Exchange 2010 o Exchange de 2013.
    
      - El bosque de destino con Exchange 2013 instalado, donde se trasladará el buzón de correo.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el script Prepare-MoveRequest.ps1 para preparar buzones de correo para traslados entre bosques

Ejecutar el script desde el Shell en un rol de servidor que ejecute Exchange 2013 en el bosque Exchange 2013 de destino. La secuencia de comandos copia los atributos del buzón de correo del bosque de origen.

Para asignar una credencial de autenticación específica para el controlador de dominio del bosque remoto, primero debe ejecutar el cmdlet **Get-Credential** de Windows PowerShell y almacenar la entrada de usuario en una variable temporal. Cuando ejecuta el cmdlet **Get-Credential**, este solicita el nombre de usuario y la contraseña de la cuenta usada durante la autenticación con el controlador de dominio del bosque remoto. A continuación, puede utilizar la variable temporal en el script Prepare-MoveRequest.ps1. Para obtener más información sobre el cmdlet **Get-Credential**, vea [Get-Credential](https://go.microsoft.com/fwlink/p/?linkid=142122).


> [!NOTE]
> Asegúrese de utilizar dos credenciales separadas para el bosque local y remoto al llamar esta secuencia de comandos.



1.  Ejecute los siguientes comandos para obtener las credenciales del bosque remoto y del bosque local.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  Ejecute los siguientes comandos para pasar la información de credenciales a los parámetros *LocalForestCredential* y *RemoteForestCredential* del script "Prepare-MoveRequest.ps1".
    
        Prepare-MoveRequest.ps1 -Identity JohnSmith@Fabrikan.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials

## Conjunto de parámetros del script

La siguiente tabla describe el parámetro establecido para el script.

### Conjunto de parámetros del script Prepare-MoveRequest.ps1

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Necesario</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Necesario</p></td>
<td><p>El parámetro <em>Identity</em> identifica de forma única un buzón de correo en el bosque de origen. La identidad puede ser una de las siguientes:</p>
<ul>
<li><p>Nombre común (CN)</p></li>
<li><p>Alias</p></li>
<li><p>Propiedad <strong>proxyAddress</strong></p></li>
<li><p>Propiedad <strong>objectGuid</strong></p></li>
<li><p>Propiedad <strong>DisplayName</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RemoteForestCredential</em></p></td>
<td><p>Necesario</p></td>
<td><p>El parámetro <em>RemoteForestCredential</em> especifica el administrador que tiene permisos para copiar datos del bosque de origen de Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoteForestDomainController</em></p></td>
<td><p>Necesario</p></td>
<td><p>El parámetro <em>RemoteForestDomainController</em> especifica el controlador de dominio en el bosque de origen en el cual reside el buzón de correo.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmailAddressPolicy</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>DisableEmailAddressPolicy</em> especifica si se debe deshabilitar la directiva de direcciones de correo electrónico (EAP) al crear un objeto <strong>MailUser</strong> en el bosque de destino.</p>
<p>Cuando especifica este parámetro, no se aplicará la EAP en el bosque de destino.</p>

> [!NOTE]
> Cuando especifica este parámetro, el objeto <STRONG>MailUser</STRONG> no tendrá una asignación de dirección de correo electrónico en el dominio de bosque local marcado. Normalmente, la EAP marca esto.


</td>
</tr>
<tr class="odd">
<td><p><em>LinkedMailUser</em></p></td>
<td><p>Opcional</p></td>
<td><p>El conmutador <em>LinkedMailUser</em> especifica si se debe crear un MailUser vinculado en el bosque local para el usuario de buzón de correo del bosque remoto.</p>
<p>Si se proporciona el conmutador, el script crea un objeto <strong>MailUser</strong> de destino vinculado al buzón de correo de origen. Si se omite el conmutador, el script crea un objeto <strong>MailUser</strong> de destino normal.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalForestCredential</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>LocalForestCredential</em> le especifica al administrador los permisos para escribir datos en el Active Directory del bosque de destino.</p>
<p>Se recomienda especificar explícitamente este parámetro para evitar problemas de permisos de Active Directory.</p>
<p>Si el bosque remoto y el bosque local tienen una relación de confianza configurada, no use la cuenta de usuario del bosque remoto como credencial del bosque local, aunque la cuenta del usuario remoto puede tener permiso para modificar Active Directory en el bosque local.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalForestDomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>LocalForestDomainController</em> especifica un controlador de dominio en el bosque de destino donde se creará el usuario habilitado para correo.</p>
<p>Le recomendamos que especifique este parámetro para evitar problemas de demora de replicación en el controlador de dominio en el bosque local que podrían ocurrir si se selecciona el controlador de dominio aleatorio.</p></td>
</tr>
<tr class="even">
<td><p><em>MailboxDeliveryDomain</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>MailboxDeliveryDomain</em> especifica un dominio de autoridad del bosque de origen de modo que el script pueda seleccionar la propiedad <strong>proxyAddress</strong> del usuario del buzón de correo de origen correcto como la propiedad <strong>targetAddress</strong> del usuario habilitado para correo de destino.</p>
<p>De manera predeterminada, la dirección SMTP primaria del usuario del buzón de correo de origen está configurada como la propiedad <strong>targetAddress</strong> del usuario habilitado para correo de destino.</p></td>
</tr>
<tr class="odd">
<td><p><em>OverWriteLocalObject</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>OverWriteLocalObject</em> se usa para usuarios creados por la Herramienta de migración de Active Directory. Las propiedades se copian del contacto de correo existente al nuevo usuario de correo creado. Sin embargo, después de esta copia, el script también copia las propiedades del usuario del bosque de origen al nuevo usuario de correo creado.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetMailUserOU</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>TargetMailuserOU</em> especifica la unidad organizativa (OU) donde se creará el usuario habilitado para correo de destino.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseLocalObject</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>UseLocalObject</em> especifica si se debe convertir el objeto local existente al usuario habilitado para correo del correo de destino, en caso de que el script detecte un objeto en el bosque local que entre en conflicto con el usuario habilitado para correo que se necesite crear.</p></td>
</tr>
</tbody>
</table>


## Ejemplos

Esta sección contiene varios ejemplos de cómo usar el script Prepare-MoveRequest.ps1.

## Ejemplo: Único usuario de correo vinculado

El siguiente ejemplo aprovisiona un usuario habilitado para correo vinculado y único en el bosque local, en caso de que la confianza del bosque se encuentre entre el bosque remoto y el local.

1.  Ejecute los siguientes comandos para obtener las credenciales del bosque remoto y del bosque local.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  Ejecute el siguiente comando para pasar la información de credenciales a los parámetros *LocalForestCredential* y *RemoteForestCredential* del script "Prepare-MoveRequest.ps1".
    
        Prepare-MoveRequest.ps1 -Identity JamesAlvord@Contoso.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials -LinkedMailUser 

## Ejemplo: Canalización

Este ejemplo es compatible con la canalización si se proporciona una lista de las identidades de buzón.

1.  Ejecute el siguiente comando.
    
        $UserCredentials = Get-Credential

2.  Ejecute el comando siguiente para pasar la información de credenciales al parámetro *RemoteForestCredential* del script Prepare-MoveRequest.ps1.
    
        "IanP@Contoso.com", "JoeAn@Contoso.com" | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## Ejemplo: Utilizar un archivo .csv para crear usuarios habilitados para correo de forma masiva

Puede generar un archivo .csv que contenga una lista de identidades de buzón de correo del bosque de origen, que le permita canalizar el contenido de este archivo a la secuencia de comandos para crear de forma masiva los usuarios habilitados para correo.

Por ejemplo, el contenido del archivo .csv puede ser:

Identidad

Ian@contoso.com

John@contoso.com

Cindy@contoso.com

En este ejemplo, se le solicita a un archivo .csv crear de forma masiva los usuarios de destino habilitados para correo.

1.  Ejecute el siguiente comando para obtener las credenciales del bosque remoto.
    
        $UserCredentials = Get-Credential

2.  Ejecute el comando siguiente para pasar la información de credenciales al parámetro *RemoteForestCredential* del script Prepare-MoveRequest.ps1.
    
        Import-Csv Test.csv | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## Comportamiento del script por objeto de destino

En esta sección se describe cómo se comporta el script en relación con los varios escenarios de objetos de destino.

## Duplicar objetos habilitados para correo de destino

Cuando la secuencia de comandos intenta crear un usuario habilitado para correo de destino desde el usuario de buzón de correo de origen y detecta un objeto habilitado para correo local duplicado, utiliza la siguiente lógica:

  - Si el atributo **masterAccountSid** del usuario del buzón de origen es igual al atributo **objectSid** o **masterAccountSid** de cualquier objeto de destino:
    
      - Si el objeto de destino no está habilitado para correo, el script devolverá un error, ya que no admite la conversión de un objeto no habilitado para correo con un usuario habilitado para correo.
    
      - Si el objeto de destino está habilitado para correo, el objeto de destino es un duplicado.

  - Si la dirección en las propiedades **proxyAddress** (sólo smtp/x500) del usuario del buzón de correo de origen es igual a una dirección de las propiedades **proxyAddress** (sólo smtp/x500) de un objeto de destino, entonces el objeto de destino es un duplicado.

La secuencia de comandos le avisa al usuario acerca de los objetos duplicados.

Si el objeto habilitado para correo de destino es un contacto o un usuario habilitado para correo, que más probablemente será creado por una implementación de sincronización de lista de direcciones global (GAL) de bosque cruzado (basado en Identity Lifecycle Management 2007 Service Pack 1), el usuario podrá ejecutar el script nuevamente con el parámetro *UseLocalObject* para utilizar el objeto habilitado para correo de destino de migración del buzón de correo.

## Usuario habilitado para correo electrónico

Si el objeto de destino es un usuario habilitado para correo, la secuencia de comando copiará los siguientes atributos del usuario del buzón de correo de origen al usuario habilitado para correo de destino:

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

Si se establece el parámetro *LinkedMailUser*, el script copia el atributo **objectSid**/**masterAccountSid** de origen.

## Contacto habilitado para correo

Si el objeto de destino es un contacto habilitado para correo, la secuencia de comando borrará el contacto existente y copiará todos los atributos a un nuevo usuario habilitado para correo. La secuencia de comandos copia también los siguientes atributos del usuario de buzón de correo de origen:

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

  - **sAMAccountName**

  - **userAccountControl** (configurar en 514 //equivalente a 0x202, ACCOUNTDISABLE | NORMAL\_ACCOUNT)

  - **userPrincipalName**

Si se establece el parámetro *LinkedMailUser*, el script copia el atributo **objectSid**/**masterAccountSid** de origen.

## Atributo "LegacyExchangeDN"

Cuando se solicita al cmdlet **Update-Recipient** convertir el objeto de destino a un usuario habilitado para correo, se generará un nuevo atributo **LegacyExchangeDN** para el usuario habilitado para correo de destino. La secuencia de comandos copia el atributo **LegacyExchangeDN** del usuario habilitado para correo de destino como una dirección x500 a las propiedades **proxyAddress** del usuario de buzón de correo de origen.

