---
title: 'Administrar acceso del usuario a aplicaciones para Outlook: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Administrar el acceso del usuario a aplicaciones para Outlook
ms:assetid: e5833dec-a23a-439e-ac03-92671817bff8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ943757(v=EXCHG.150)
ms:contentKeyID: 52062076
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar el acceso del usuario a aplicaciones para Outlook

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2018-04-17_

Puede usar el EAC o Exchange Online PowerShell para administrar el acceso de los usuarios a los complementos de Outlook.

  - Con el Centro de administración de Exchange (EAC), puede administrar la configuración de acceso a complementos básicos para los usuarios en la organización. Por ejemplo, puede configurar si un complemento está habilitado o deshabilitado para los usuarios. También puede especificar si un complemento es necesario u opcional para ellos.

  - Con Exchange Online PowerShell, puede administrar todas las opciones de configuración que puede con el EAC, así como otras opciones. Por ejemplo, puede limitar la disponibilidad a usuarios específicos en su organización.

Para otras tareas de administración, consulte [Aplicaciones para Outlook](add-ins-for-outlook-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Para obtener información sobre cómo usar Windows PowerShell para conectarse a Exchange Online, vea [Conexión a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada “Complementos para Outlook” en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Especificación del estado de un complemento (disponible, habilitado o deshabilitado)

## Uso del EAC para especificar si un complemento está disponible, habilitado o deshabilitado

1.  En el EAC, vaya a **Organización** \> **Complementos**.

2.  En la vista de lista, seleccione el complemento del que quiera cambiar la configuración y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  Si no quiere que los usuarios usen el complemento, desactive la casilla **Hacer que este complemento esté disponible para los usuarios de la organización** y, a continuación, haga clic en **Guardar**.

4.  Si quiere que los usuarios puedan usar el complemento, seleccione **Hacer que este complemento esté disponible para los usuarios de la organización** y, a continuación, seleccione la opción que quiera.
    
      - **Opcional, habilitado de manera predeterminada**   Use esta configuración si quiere permitir que los usuarios desactiven el complemento.
    
      - **Opcional, deshabilitado de manera predeterminada**   Use esta configuración si quiere permitir que los usuarios activen el complemento.
    
      - **Obligatorio, siempre habilitado. Los usuarios no pueden deshabilitar este complemento**   Use esta configuración si no quiere que los usuarios desactiven el complemento.

5.  Haga clic en **Guardar**.

## Uso de Exchange Online PowerShell para especificar si un complemento está disponible, habilitado o deshabilitado

Puede usar Exchange Online PowerShell para especificar si un complemento está disponible, habilitado o deshabilitado.


> [!NOTE]
> Ejecute el siguiente comando para buscar los nombres para mostrar y los identificadores de complemento de todos los complementos de Outlook instalados en su organización.



    Get-app -Organizationadd-in | Format-List DisplayName,add-inID

Si quiere que un complemento esté deshabilitado y oculto para todos sus usuarios, ejecute el siguiente comando.

    Set-app <add-in ID> -Organizationadd-in -Enabled $false

Si quiere que el complemento esté habilitado de manera predeterminada, pero que los usuarios lo puedan desactivar, ejecute el siguiente comando.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Enabled

Si quiere que el complemento esté deshabilitado de manera predeterminada, pero que los usuarios lo puedan activar, ejecute el siguiente comando.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Disabled

Si quiere que el complemento sea necesario para los usuarios, ejecute el siguiente comando.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser AlwaysEnabled

Para obtener información detallada sobre la sintaxis y los parámetros, consulte [Set-App](https://technet.microsoft.com/es-es/library/jj218630\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

1.  En el EAC, vaya a **Organización** \> **Complementos**.

2.  Revise los valores en las columnas **Predeterminado de usuario** y **Proporcionado a**.

O bien

1.  En Exchange Online PowerShell, ejecute `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*`.

2.  Revise los valores de **DefaultStateForUser** y **Habilitado**.

## Límite de disponibilidad a usuarios específicos

## Usar Exchange Online PowerShell para limitar la disponibilidad a usuarios específicos

Si quiere que solo los miembros de su grupo de distribución del equipo de marketing puedan usar el complemento de LinkedIn, ejecute los siguientes comandos.
```
    $a = Get-DistributionGroupMember Marketing
```
```
    Set-app <add-in ID for the LinkedIn add-in> -Organizationadd-in -ProvidedTo SpecificUsers -UserList $a.Identity -DefaultStateForUser Enabled}
```

Para obtener información detallada sobre la sintaxis y los parámetros, consulte [Set-App](https://technet.microsoft.com/es-es/library/jj218630\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que limitó correctamente el acceso a usuarios específicos, haga lo siguiente:

1.  En Exchange Online PowerShell, ejecute `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*,ProvidedTo,UserList`.

2.  Revise el valor de **ProvidedTo**.

