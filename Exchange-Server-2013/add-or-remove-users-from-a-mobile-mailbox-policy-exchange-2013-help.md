---
title: 'Agregar o quitar usuarios de una directiva de buzón móvil: Exchange 2013 Help'
TOCTitle: Agregar o quitar usuarios de una directiva de buzón móvil
ms:assetid: 4ca8e395-c074-4165-b788-16fae3e2ccab
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997929(v=EXCHG.150)
ms:contentKeyID: 49895617
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agregar o quitar usuarios de una directiva de buzón móvil

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-07-16_

Una directiva de buzón de dispositivo móvil le permite aplicar un conjunto común de configuraciones de seguridad y de dispositivo móvil a un grupo de usuarios. Puede crear varias directivas de buzón de dispositivo móvil.


> [!WARNING]
> Cuando se instala Microsoft Exchange Server 2013, se crea un directiva de buzón de dispositivo móvil predeterminada y todos los usuarios se asignan automáticamente a esta directiva.



Para consultar otras tareas de administración relacionadas con las directivas de buzón de dispositivo móvil, vea [Directivas de buzón de dispositivo móvil](mobile-device-mailbox-policies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Directiva de buzón de correo de dispositivo móvil" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Debe haber una directiva de buzón de dispositivo móvil disponible en el EAC en **Móvil** \> **Directivas de buzón de dispositivos móviles**.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Cambiar la directiva de buzón de dispositivo móvil de un usuario

Puede usar el EAC o el Shell para cambiar la directiva de buzón de dispositivo móvil de un usuario.

## Uso del EAC para cambiar la directiva de buzón de dispositivo móvil de un usuario

El EAC permite cambiar la directiva de buzón de dispositivo móvil de un usuario.

1.  En el EAC, haga clic en **Destinatarios** \> **Buzones de correo** y, a continuación, seleccione un buzón.

2.  En el panel de detalles, vaya a **Características de voz y teléfono** y seleccione **Ver detalles** para mostrar la pantalla **Detalles de dispositivo móvil**.

3.  Se mostrará la directiva de buzón de dispositivo móvil que está asignada actualmente. Para cambiar la directiva de buzón de dispositivo móvil, haga clic en **Examinar**.

4.  Elija la directiva de buzón de dispositivo móvil adecuada en la lista, haga clic en **Aceptar** y después en **Guardar**.

## Uso del Shell para agregar un usuario a una directiva de buzón de dispositivo móvil

Para cambiar la directiva de buzón de dispositivo móvil de un usuario, utilice el cmdlet **Get-CASMailbox** en el Shell.

1.  En el Shell, ejecute el siguiente comando.
    
        Get-CASMailbox -Identity tony@contoso.com -ActiveSyncMailboxPolicy "Sales" 

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que cambió correctamente la directiva de buzón de dispositivo móvil de un usuario, elija una de las siguientes opciones:

1.  En el EAC, haga clic en **Destinatarios** \> **Buzones de correo** y, a continuación, seleccione un destinatario específico. En el panel de detalles, vaya a **Características de voz y teléfono** y haga clic en **Ver detalles**.

2.  En el Shell, ejecute el siguiente comando.
    
        Get-CASMailbox -Identity tony@contoso.com 

## Cambiar la directiva de buzón de dispositivo móvil para varios usuarios al mismo tiempo

Si desea cambiar la directiva de buzón de dispositivo móvil para varios usuarios al mismo tiempo, puede usar la función de edición masiva en el EAC, o bien utilizar el Shell para cambiar la directiva de buzón de dispositivo móvil para un conjunto filtrado de usuarios.

## Uso de la herramienta de edición masiva en el EAC para cambiar la directiva de buzón de dispositivo móvil para varios usuarios

La función de edición masiva permite actualizar la directiva de buzón de dispositivo móvil para varios usuarios a la vez.

1.  En el EAC, haga clic en **Destinatarios** \> **Buzones de correo**.

2.  Seleccione varios usuarios.

3.  En el panel de detalles, vaya a **Exchange ActiveSync** y haga clic en **Actualizar una directiva**.

4.  Haga clic en **Examinar** para elegir una directiva de buzón de dispositivo móvil.

5.  Haga clic en **Aceptar** y, a continuación, en **Guardar**.

## Uso del Shell para cambiar la directiva de buzón de dispositivo móvil de un conjunto filtrado de usuarios

Puede usar el Shell para cambiar la directiva de buzón de dispositivo móvil de un conjunto filtrado de usuarios. Los usuarios se pueden filtrar en función de varios atributos.

1.  En el Shell, ejecute el siguiente comando.
    
        Get-Mailbox | where { $_.CustomAttribute1 -match "Manager"
         } | Set-CASMailbox -activesyncmailboxpolicy(Get-ActiveSyncMailboxPolicy "Contoso").Identity
    

    > [!NOTE]
    > Puede sustituir <CODE>CustomAttribute1</CODE> con cualquiera de las propiedades del objeto <STRONG>Get-Mailbox</STRONG>. Para ver la lista completa, escriba: <CODE>Get-Mailbox username |fl</CODE>.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que cambió correctamente la directiva de buzón de dispositivo móvil de un usuario, elija una de las siguientes opciones:

1.  En el EAC, haga clic en **Destinatarios** \> **Buzones de correo** y, a continuación, seleccione un destinatario específico. En el panel de detalles, vaya a **Características de voz y teléfono** y haga clic en **Ver detalles**.

2.  En el Shell, ejecute el siguiente comando.
    
    ```powershell
Get-CASMailbox -Identity tony@contoso.com
```

