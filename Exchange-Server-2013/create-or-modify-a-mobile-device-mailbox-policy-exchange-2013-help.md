---
title: 'Crear o modificar una directiva de buzón de dispositivo móvil: Exchange 2013 Help'
TOCTitle: Crear o modificar una directiva de buzón de dispositivo móvil
ms:assetid: b4a37a81-25e3-40ff-a18a-a62ae4493635
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124315(v=EXCHG.150)
ms:contentKeyID: 49895852
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear o modificar una directiva de buzón de dispositivo móvil

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-16_

Una directiva de buzón de dispositivo móvil le permite aplicar un conjunto común de configuraciones de seguridad y de dispositivo móvil a un grupo de usuarios. Puede crear varias directivas de buzón de dispositivo móvil. Todos los destinatarios en su organización deben tener una directiva de buzón de correo para dispositivos móviles asignado a ellos. Cuando instala Microsoft Exchange Server 2013, se crea una directiva de buzón de correo para dispositivos móviles y los usuarios nuevos se asignan automáticamente a esta directiva. Para asignar usuarios específicos a una directiva de buzón de correo para dispositivos móviles, consulte [Agregar o quitar usuarios de una directiva de buzón móvil](add-or-remove-users-from-a-mobile-mailbox-policy-exchange-2013-help.md).

Para información adicional relacionada con las directivas de buzón de correo para dispositivos móviles, consulte [Directivas de buzón de dispositivo móvil](mobile-device-mailbox-policies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  10 minutos.

  - Entrada "Directivas de buzón de correo para dispositivos móviles" Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Cree una nueva directiva de buzón de correo para dispositivos móviles

Puede usar la EAC o el Shell para crear una nueva directiva de buzón de correo para dispositivos móviles.

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de buzón de dispositivo móvil" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

## Utilice la EAC para crear una nueva directiva de buzón de correo para dispositivos móviles

Puede crear una nueva directiva de buzón de correo para dispositivos móviles usando la EAC.


> [!NOTE]
> Solamente puede establecer un subconjunto de configuraciones de directivas de buzón de correo para dispositivos móviles en la EAC. Para establecer todas las configuraciones de directivas de buzón para dispositivos móviles, es necesario utilizar el Shell.



1.  En la EAC, haga clic en **Móvil** \> **Directivas de buzón de correo para dispositivos móviles** y luego haga clic en **Nuevo**.

2.  Utilice las diferentes casillas de verificación y las listas desplegables para configurar las configuraciones de la directiva de buzón de correo para dispositivos móviles.
    

    > [!WARNING]
    > Seleccione <STRONG>Esta es la directiva predeterminada</STRONG> para que la nueva directiva de buzón móvil sea la directiva de buzón móvil predeterminada. Después de establecer una directiva de buzón móvil como la directiva predeterminada, a todos los usuarios nuevos se les asignará automáticamente esta directiva cuando sean creados.



3.  Haga clic en **Guardar**.

## Utilice el Shell para crear una nueva directiva de buzón de correo para dispositivos móviles

Puede crear una nueva directiva de buzón de correo para dispositivos móviles usando el cmdlet de New-MobileDeviceMailboxPolicy.


> [!WARNING]
> Existen dos cmdlets que se pueden utilizar para crear una nueva directiva de buzón de correo para dispositivos móviles. El cmdlet <STRONG>New-ActiveSyncMailboxPolicy</STRONG> y los cmdlets <STRONG>New-MobileDeviceMailboxPolicy</STRONG> realizan tareas idénticas. En una versión futura de Microsoft Exchange Server, se eliminará el cmdlet <STRONG>New-ActiveSyncMailboxPolicy</STRONG>. Recomendamos que actualice los scripts y procedimientos para utilizar el cmdlet <STRONG>New-MobileDeviceMailboxPolicy</STRONG>.



1.  En el Shell, ejecute el siguiente comando.
    
```powershell
New-MobileDeviceMailboxPolicy -Name:"Management" -AllowBluetooth:$true -AllowBrowser:$true -AllowCamera:$true -AllowPOPIMAPEmail:$false -PasswordEnabled:$true -AlphanumericPasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:10 -AllowWiFi:$true -AllowStorageCard:$true -AllowPOPIMAPEmail:$false
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó una directiva de buzón de correo para dispositivos móviles correctamente, utilice una de las siguientes opciones:

1.  En la EAC, haga clic en **Móvil** \> **Directivas de buzón de correo para dispositivos móviles** y compruebe que la nueva directiva aparezca en la vista de Lista.

2.  En el Shell, ejecute el siguiente comando.
    
```powershell
Get-MobileDeviceMailboxPolicy -Identity <PolicyName> 
```

## Edite una directiva de buzón de correo para dispositivos móviles existente

Si quiere editar una directiva de buzón de correo para dispositivos móviles, puede utilizar la EAC o el Shell.

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de buzón de dispositivo móvil" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

## Utilice la EAC para editar una directiva de buzón de correo para dispositivos móviles

Puede editar una directiva de buzón de correo para dispositivos móviles usando la EAC.


> [!NOTE]
> Solamente puede editar un subconjunto de configuraciones de directivas de buzón de correo para dispositivos móviles en la EAC. Para editar todas las configuraciones de directivas de buzón de correo para dispositivos móviles, es necesario utilizar el Shell.



1.  En la EAC, haga clic en **Móvil** \> **Directivas de buzón de correo para dispositivos móviles**.

2.  Seleccione una directiva en la vista de Lista y haga clic en el botón **Editar**.

3.  Utilice las fichas **General** y **Seguridad** para editar las configuraciones de directivas de buzón de correo para dispositivos móviles.

4.  Haga clic en **Guardar** para actualizar la directiva.

## Use el Shell para editar las configuraciones de directivas de buzón de correo para dispositivos móviles

Puede usar el Shell para editar una directiva de buzón de correo para dispositivos móviles.


> [!WARNING]
> Existen dos cmdlets que se pueden utilizar para editar una directiva de buzón de correo para dispositivos móviles. El cmdlet Set-ActiveSyncMailboxPolicy y los cmdlets Set-MobileDeviceMailboxPolicy realizan tareas idénticas. En una versión futura de Microsoft Exchange Server, se eliminará el cmdlet <STRONG>Set-ActiveSyncMailboxPolicy</STRONG>. Recomendamos que actualice los scripts y procedimientos para utilizar el cmdlet <STRONG>Set-MobileDeviceMailboxPolicy</STRONG>.



1.  En el Shell, ejecute el siguiente comando.
    
```powershell
Set-MobileDeviceMailboxPolicy -Identity:Default -DevicePasswordEnabled:$true -AlphanumericDevicePasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:ThreeDays -AllowWiFi:$false -AllowStorageCard:$true -AllowPOPIMAPEmail:$false -IsDefault:$true -AllowTextMessaging:$true -Confirm:$true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si editó una directiva de buzón de correo para dispositivos móviles correctamente, asegúrese de hacer lo siguiente:

1.  En la EAC, haga clic en **Móvil** \> **Directivas de buzón de correo para dispositivos móviles** y luego elija una directiva específica. En el panel de Detalles, verá mencionado un número de las configuraciones de la directiva.

2.  En el Shell, ejecute el siguiente comando.
    
```powershell
Get-MobileDeviceMailboxPolicy -Identity <PolicyName>
```

