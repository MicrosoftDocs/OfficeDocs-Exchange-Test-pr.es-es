---
title: 'Habilitar deshabilitar registro auditoría buzón para buzón: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el registro de auditoría de buzones para un buzón
ms:assetid: c4bbfd52-6196-49c7-8c31-777fbbee11f2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff461937(v=EXCHG.150)
ms:contentKeyID: 49895899
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar el registro de auditoría de buzones para un buzón

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-09-30_

El registro de auditoría de buzón permite controlar los inicios de sesión en un buzón así como las acciones realizadas mientras el usuario está conectado. Al habilitar el registro de auditoría de buzón en un buzón, algunas acciones realizadas por los administradores y delegados se registran de forma predeterminada. No se registra ninguna de las acciones realizadas por el propietario del buzón. Para obtener más información acerca de los registros de auditoría de buzones, consulte [Registro de auditoría de buzones de correo](mailbox-audit-logging-exchange-2013-help.md).


> [!WARNING]
> La auditoría de las acciones del propietario del buzón puede generar una gran cantidad de entradas en el registro de auditoría, por lo que está deshabilitada de forma predeterminada. Se recomienda activar solo la auditoría de algunas acciones específicas necesaria para cumplir con los requisitos comerciales o de seguridad.



Para obtener más información acerca de otras tareas adicionales relacionadas con el registro de auditoría del buzón, consulte [Procedimientos de registro de auditoría de buzones](mailbox-audit-logging-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría de buzones" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para habilitar o deshabilitar el registro de auditoría del buzón. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para habilitar o deshabilitar el registro de auditoría de buzones

Puede utilizar el Shell para habilitar o deshabilitar los registros de auditoría del buzón para un buzón de correo. Esto habilita o deshabilita los registros de todas las operaciones especificadas por el administrador, los delegados y el propietario del buzón de correo.

En este ejemplo se habilita el registro de auditoría del buzón de Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $true
```

En este ejemplo se deshabilita el registro de auditoría del buzón de Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $false
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## Uso del Shell para configurar los valores del registro de auditoría del buzón para el acceso del administrador, delegado y propietario

Cuando el registro de auditoría del buzón está habilitado para un buzón de correo, solo se registran las acciones del administrador, delegado y propietario especificadas en la configuración de registros de auditoría para el buzón de correo.

En este ejemplo se especifica que las acciones `SendAs` o `SendOnBehalf` realizadas por usuarios delegados se registrarán en el buzón de Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditDelegate SendAs,SendOnBehalf -AuditEnabled $true
```

En este ejemplo se especifica que las acciones `MessageBind` o `FolderBind` realizadas por administradores se registrarán en el buzón de Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditAdmin MessageBind,FolderBind -AuditEnabled $true
```

En este ejemplo se especifica que la acción `HardDelete` realizada por el propietario del buzón se registrará en el buzón de Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditOwner HardDelete -AuditEnabled $true
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya habilitado correctamente los registros de auditoría del buzón para un buzón de correo y especificado las configuraciones de registro de acceso correctos para un administrador, delegado o propietario, use el cmdlet [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) para recuperar los ajustes de registro de auditoría del buzón para ese buzón de correo.

Este ejemplo recupera los ajustes del buzón de correo de Ben Smith y canaliza los ajustes de auditoría especificados, que incluyen el límite de antigüedad del registro de auditoría, hacia el cmdlet **Format-List**.

    Get-Mailbox "Ben Smith" | Format-List *audit*

