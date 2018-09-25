---
title: 'Habilitar o deshabilitar el correo electrónico de un contacto de correo: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el correo electrónico de un contacto de correo
ms:assetid: ca47441f-1aa4-4958-aba5-18d51e59837e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124552(v=EXCHG.150)
ms:contentKeyID: 50556884
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar el correo electrónico de un contacto de correo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-12-05_

Puede deshabilitar el correo electrónico para un contacto de correo existente en la organización de Exchange. Cuando se deshabilita el correo electrónico para un contacto de correo, se quita de Exchange y de la libreta de direcciones de la organización. Si el contacto de correo es miembro de un grupo de distribución, el contacto dejará de recibir el correo que se envíe al grupo. Asimismo, los atributos de Exchange se eliminan del objeto de contacto habilitado para correo en Active Directory, pero el contacto y los atributos que no sean de Exchange (como la información de la organización y del contacto) se mantienen.

Después de deshabilitar el correo electrónico para un contacto de correo, puede volver a habilitar al contacto para correo mediante el uso del cmdlet **Enable-MailContact** en el Shell. También puede utilizar este cmdlet para habilitar para correo cualquier contacto de Active Directory.

Para otras tareas de administración relacionadas con los contactos de correo, consulte [Administrar contactos de correo](https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-mail-contacts).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Contactos de correo" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Deshabilitar el correo electrónico para un contacto de correo

Según se mencionó anteriormente, cuando se deshabilita el correo electrónico para un contacto de correo, los atributos de Exchange se eliminan del objeto de contacto de Active Directory correspondiente, pero el contacto se mantiene. El contacto de correo se elimina de la lista de contactos de correo de la EAC, pero puede ver y administrar el objeto de contacto de Active Directory correspondiente mediante el uso de Usuarios y equipos de Active Directory o de los cmdlets **Get-Contact** y **Set-Contact** en el Shell.

## Uso del EAC para deshabilitar el correo electrónico para un contacto de correo

1.  En el EAC, vaya a **Destinatarios** \> **Contactos**.

2.  En la lista de contactos, haga clic en el contacto de correo para el que desea deshabilitar el correo electrónico.

3.  Haga clic en **Más**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") y, a continuación, en **Deshabilitar**.

4.  Aparecerá una advertencia para que confirme si desea deshabilitar el contacto de correo seleccionado. Haga clic en **Sí** para deshabilitarlo.

El contacto de correo se eliminará de la lista de contactos.

## Uso del Shell para deshabilitar el correo electrónico para un contacto de correo

En este ejemplo se deshabilita el correo electrónico del contacto de correo Neil Black.

```powershell
Disable-MailContact -Identity "Neil Black"
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Disable-MailContact](https://technet.microsoft.com/es-es/library/aa997465\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si deshabilitó el correo electrónico para un contacto de correo correctamente, siga uno de estos procedimientos:

1.  En la EAC, vaya a **Destinatarios** \> **Contactos** y compruebe que el contacto de correo ya no aparece en la lista.

2.  En Usuarios y equipos de Active Directory, haga clic con el botón secundario en el contacto y, a continuación, en **Propiedades**. En la pestaña **General**, observe que el cuadro **Correo electrónico** esté en blanco. Esto comprueba que el contacto no está habilitado para correo.

3.  En el Shell, ejecute el siguiente comando.
    
    ```powershell
    Get-MailContact
    ```
    
    El contacto para el que deshabilitó el correo electrónico no se devuelve en los resultados porque este cmdlet solo devuelve los contactos habilitados para correo.

4.  En el Shell, ejecute el siguiente comando.
    
    ```powershell
    Get-Contact
    ```
    
    El contacto para el que deshabilitó el correo electrónico se devuelve en los resultados porque este cmdlet devuelve todos los objetos de contacto de Active Directory.

## Uso del Shell para habilitar contactos para correo

Utilice el cmdlet **Enable-MailContact** para habilitar para correo los contactos de Active Directory existentes. Puede habilitar para correo un solo contacto o usar un archivo CSV para habilitar varios contactos para correo.

## Uso del Shell para habilitar un solo contacto para correo

En este ejemplo se habilita para correo al contacto Rene Valdes. Debe proporcionar una dirección de correo electrónico externa.

```powershell
Enable-MailContact -Identity "Rene Valdes" -ExternalEmailAddress renev@tailspintoys.com
```

## Uso del Shell y de un archivo CSV para habilitar varios contactos para correo

Al habilitar varios contactos para correo de forma masiva, primero debe exportar la lista de contactos que no están habilitados para correo a un archivo CSV (valores separados por comas) y, a continuación, agregar las direcciones de correo electrónico externas al archivo CSV mediante el uso de un editor de texto como el Bloc de notas o de una aplicación de hojas de cálculo, como Microsoft Excel. Después, utilice el archivo CSV actualizado en el comando del Shell para habilitar para correo los contactos del archivo CSV.

1.  Ejecute el siguiente comando para exportar una lista de los contactos existentes que no están habilitados para correo a un archivo en el escritorio del administrador llamado Contacts.csv.
    
    ```powershell
    Get-Contact | Where { $_.RecipientType -eq "Contact" } | Out-File "C:\Users\Administrator\Desktop\Contacts.csv"
    ```
    
    El archivo resultante será parecido al siguiente.
    
```powershell
Name
Walter Harp
James Alvord
Rainer Witt
Susan Burk
Ian Tien
...
```

2.  Agregue un encabezado de columna llamado **EmailAddress** y, a continuación, agregue una dirección de correo para cada contacto del archivo. El nombre y la dirección de correo electrónico externa para cada contacto deben estar separados por una coma. El archivo .CSV actualizado debe ser parecido al siguiente:
    
    ```powershell
    Name,EmailAddress
    James Alvord,james@contoso.com
    Susan Burk,sburk@tailspintoys.com
    Walter Harp,wharp@tailspintoys.com
    Ian Tien,iant@tailspintoys.com
    Rainer Witt,rainerw@fourthcoffee.com
    ...
    ```

3.  Ejecute el siguiente comando para usar los datos del archivo CSV para habilitar para correo los contactos del archivo.
    
    ```powershell
    Import-CSV C:\Users\Administrator\Desktop\Contacts.csv | ForEach-Object {Enable-MailContact -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    ```
    
    Los resultados del comando muestran información acerca de los nuevos contactos habilitados para correo.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si habilitó para correo los contactos de Active Directory correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Contactos**. Los contactos nuevos se muestran en la lista de contactos. Bajo **Tipo de contacto**, el tipo es **Contacto de correo**.
    

    > [!NOTE]
    > Puede que tenga que hacer clic en <STRONG>Actualizar</STRONG><IMG title="Icono Actualizar" alt="Icono Actualizar" src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif"> para mostrar los nuevos contactos de correo.



  - En el Shell, ejecute el comando siguiente para mostrar información sobre los nuevos contactos de correo.
    
    ```powershell
    Get-MailContact | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress
    ```

