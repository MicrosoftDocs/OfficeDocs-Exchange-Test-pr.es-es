---
title: 'Habilitar o deshabilitar el correo de un usuario de correo: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el correo electrónico de un usuario de correo
ms:assetid: 1e2571d4-ff84-4fda-bb1d-825e96e1bd26
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996598(v=EXCHG.150)
ms:contentKeyID: 50556746
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar el correo electrónico de un usuario de correo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-11-14_

Puede deshabilitar el correo electrónico para un usuario de correo existente en su organización de Exchange. Cuando deshabilita el correo electrónico de un usuario de correo, se elimina de la libreta de direcciones de su organización y de Exchange. Si el usuario de correo es un miembro de un grupo de distribución, el usuario deja de recibir el correo enviado al grupo. Asimismo, los atributos de Exchange se eliminan del objeto de usuario en Active Directory, pero el objeto de usuario y sus atributos que no pertenecen a Exchange (como la información de contacto y de la organización) se conservan en Active Directory.

Después de deshabilitar el correo electrónico de un usuario de correo, puede volver a habilitar el correo del usuario mediante el cmdlet **Enable-MailUser** en el Shell. También puede usar este cmdlet para habilitar el correo de cualquier usuario de Active Directory.


> [!NOTE]
> Los usuarios de correo (también denominados <EM>usuarios habilitados para correo</EM>) son diferentes a los usuarios en su organización que tienen un buzón de correo. La principal diferencia es que los usuarios de correo representan a los usuarios fuera de su organización de Exchange que tienen una dirección de correo electrónico externa. No tienen un buzón de correo de su organización. Para obtener más información acerca de las diferencias entre los usuarios que tienen buzones de correo en su organización y los usuarios de correo, consulte <A href="recipients-exchange-2013-help.md">Destinatarios</A>.



Para otras tareas de administración relacionadas con usuarios de correo, consulte [Administrar usuarios de correo](manage-mail-users-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Usuarios de correo" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Deshabilitación del correo electrónico para un usuario de correo

Como se mencionó antes, cuando se deshabilita el correo electrónico de un usuario de correo, los atributos de Exchange se eliminan del objeto de usuario de correo correspondiente en Active Directory, pero el usuario se conserva. El usuario de correo se elimina de la lista de usuarios de correo en el EAC, pero puede ver y administrar el objeto de contacto correspondiente en Active Directory usando Usuarios y equipos de Active Directory o usando los cmdlets **Get-MailUser** y **Set-Set-MailUser** en el Shell.

## Uso del EAC para deshabilitar el correo electrónico de un usuario de correo

1.  En el EAC, vaya a **Destinatarios** \> **Contactos**.

2.  En la lista de contactos, haga clic en el usuario de correo al cual desea deshabilitarle el correo electrónico.

3.  Haga clic en **Más**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") y, a continuación, en **Deshabilitar**.

4.  Aparecerá una advertencia que le preguntará si está seguro de querer deshabilitar el usuario de correo seleccionado. Haga clic en **Sí** para deshabilitarlo.

El usuario de correo se eliminará de la lista de contactos.

## Uso del Shell para deshabilitar el correo electrónico de un usuario de correo

En este ejemplo, se deshabilita el correo electrónico del usuario de correo, Juan.

    Disable-MailUser -Identity "Yan Li"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Disable-MailUser](https://technet.microsoft.com/es-es/library/aa998578\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya deshabilitado el correo electrónico de un usuario de correo correctamente, siga uno de estos procedimientos:

1.  En el EAC, navegue a **Destinatarios** \> **Contactos** y compruebe que no aparezca el usuario de correo.

2.  En Usuarios y equipos de Active Directory, haga clic con el botón secundario del mouse en el usuario y, a continuación, haga clic en **Propiedades**. En la ficha **General**, compruebe que el cuadro **Correo electrónico** esté en blanco. Esto comprueba que el correo del usuario de correo no está habilitado.

3.  En el Shell, ejecute el siguiente comando.
    
        Get-MailUser
    
    El usuario de correo al que deshabilitó el correo electrónico no aparecerá en los resultados porque este cmdlet solo devuelve los usuarios con correo habilitado.

4.  En el Shell, ejecute el siguiente comando.
    
        Get-User
    
    El usuario de correo al que deshabilitó el correo electrónico aparece en los resultados porque este cmdlet devuelve todos los objetos de usuario de Active Directory.

## Uso del Shell para habilitar el correo de los usuarios

Es posible usar el cmdlet **Enable-MailUser** para habilitar el correo de los usuarios existentes de Active Directory. Es posible habilitar para correo un solo usuario o usar un archivo CSV para habilitar el correo de varios usuarios.

## Uso del Shell para habilitar un solo usuario

En este ejemplo, se habilita el correo del usuario Sanjay Shah. Debe proporcionar una dirección de correo electrónico externa.

    Enable-MailUser -Identity "Sanjay Shah" -ExternalEmailAddress renev@tailspintoys.com

## Uso del Shell y un archivo CSV para habilitar el correo de varios usuarios

Al habilitar el correo de usuarios en masa, primero debe exportar la lista de usuarios que no están habilitados para correo en un archivo CVS (valores separados por comas) y, luego, agregar direcciones de correo electrónico externas al archivo CSV mediante un editor de texto, como el Bloc de notas, o una aplicación de hojas de cálculo, como Microsoft Excel. Luego, usa el archivo CSV actualizado en el comando de Shell para habilitar el correo de los usuarios enumerados en el archivo CSV.

1.  Ejecute el siguiente comando para exportar una lista de los usuarios existentes cuyo correo no esté habilitado o que no tengan un buzón de correo en su organización a un archivo en el escritorio del administrador denominado UsersToMailEnable.csv.
    
        Get-User | Where { $_.RecipientType -eq "User" } | Out-File "C:\Users\Administrator\Desktop\UsersToMailEnable.csv"
    
    El archivo resultante será parecido al siguiente.
    
        Name            RecipientType
        ----            -------------
        Guest           User
        krbtgt          User
        RMS_SERVICE     User
        David Pelton    User
        Kim Akers       User
        Janet Schorr    User
        Jeffrey Zang    User
        Spencer Low     User
        Toni Poe        User
        ...

2.  Realice los siguientes cambios en el archivo CSV:
    
      - Elimine del archivo CSV a los usuarios cuyo correo no desea habilitar. Por ejemplo, podría eliminar las tres primeras entradas del ejemplo anterior porque son cuentas predeterminadas del sistema.
    
      - Elimine la columna **RecipientType** y todas las instancias de `User`.
    
      - Agregue un encabezado de columna con el nombre **EmailAddress** y, luego, agregue una dirección de correo para cada usuario en el archivo. El nombre y la dirección de correo electrónico externa de cada usuario deben estar separados por una coma.
    
    El archivo CSV actualizado debería ser parecido al siguiente.
    
        Name,EmailAddress
        David Pelton,davidp@contoso.com
        Kim Akers,kakers@tailspintoys.com
        Janet Schorr,janet.schorr@adatum.com
        Jeffrey Zang,jzang@tailspintoys.com
        Spencer Low,spencerl@fouthcoffee.com
        Toni Poe,tonip@contoso.com
        ...

3.  Ejecute el siguiente comando para usar los datos en el archivo CSV para habilitar el correo de los usuarios enumerados en el archivo.
    
        Import-CSV "C:\Users\Administrator\Desktop\UsersToMailEnable.csv" | ForEach-Object {Enable-MailUser -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    Los resultados del comando muestran información sobre los nuevos usuarios habilitados para correo.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya habilitado el correo de usuarios de Active Directory correctamente, realice uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Contactos**. Se muestran nuevos usuarios de correo en la lista de contactos. En **Tipo de contacto**, el tipo es **Usuario de correo**.
    

    > [!NOTE]
    > Es posible que deba hacer clic en <STRONG>Actualizar</STRONG><IMG title="Icono Actualizar" alt="Icono Actualizar" src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif"> para que se muestren los nuevos usuarios de correo.



  - En el Shell, ejecute el siguiente comando para que se muestre información acerca de los nuevos usuarios de correo.
    
        Get-MailUser | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

