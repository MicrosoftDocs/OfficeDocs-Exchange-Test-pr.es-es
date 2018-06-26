---
title: 'Habilitar o deshabilitar Exchange ActiveSync para un buzón de correo: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar Exchange ActiveSync para un buzón de correo
ms:assetid: dcf7c05b-b1b9-4b0f-800d-fec9f2ddc9e4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124809(v=EXCHG.150)
ms:contentKeyID: 50556895
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar Exchange ActiveSync para un buzón de correo

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2012-11-13_

Puede usar la EAC o el Shell para habilitar o deshabilitar Microsoft Exchange ActiveSync para un buzón de usuario. Exchange ActiveSync es un protocolo de cliente que permite a los usuario sincronizar un dispositivo móvil con su buzón de Exchange. Exchange ActiveSync se habilita de manera predeterminada cuando se crea un buzón de usuario. Para obtener más información, consulte [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de Exchange ActiveSync" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para habilitar o deshabilitar Exchange ActiveSync

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón para el que desea habilitar o deshabilitar Exchange ActiveSync y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic en **Características de buzón de correo**.

4.  En **Dispositivos móviles**, realice una de las acciones siguientes:
    
      - Para deshabilitar Exchange ActiveSync, haga clic en **Deshabilitar Exchange ActiveSync**.
        
        Aparece una advertencia para que confirme si desea deshabilitar Exchange ActiveSync. Haga clic en **Sí**.
    
      - Para habilitar Exchange ActiveSync, haga clic en **Habilitar Exchange ActiveSync**.

5.  Haga clic en **Guardar** para guardar el cambio.


> [!NOTE]
> Puede habilitar o deshabilitar Exchange ActiveSync para varios buzones de usuario mediante la característica de edición en masa de la EAC. Para obtener más información acerca de cómo realizar esto, consulte la sección de cómo "editar en masa buzones de usuario" en <A href="manage-user-mailboxes-exchange-2013-help.md">Administrar los buzones de usuario</A>.



## Uso del Shell para habilitar o deshabilitar Exchange ActiveSync

En este ejemplo se deshabilita Exchange ActiveSync para el buzón de Yan Li.

    Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false

En este ejemplo se habilita Exchange ActiveSync para el buzón de Elly Nkya.

    Set-CASMailbox -Identity Ellyn@contoso.com -ActiveSyncEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si habilitó o deshabilitó Exchange ActiveSync para un buzón de usuario correctamente, siga uno de estos procedimientos:

  - En la EAC, vaya a **Destinatarios**  \> **Buzones de correo**, haga clic en el buzón y, después, en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

  - En la página de propiedades de buzones, haga clic en **Características de buzón de correo**.

  - En **Dispositivos móviles**, compruebe si Exchange ActiveSync está habilitado o deshabilitado.

O bien

  - Ejecute el siguiente comando en el Shell.
    
        Get-CASMailbox <identity>
    
    Si Exchange ActiveSync está habilitado, el valor de la propiedad *ActiveSyncEnabled* es `True`. Si Exchange ActiveSync está deshabilitado, el valor es `False`.

