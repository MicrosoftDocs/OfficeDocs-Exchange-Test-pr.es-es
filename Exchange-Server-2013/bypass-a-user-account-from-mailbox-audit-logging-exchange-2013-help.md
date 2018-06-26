---
title: 'Omitir una cuenta de usuario desde el registro de auditoría de buzones: Exchange 2013 Help'
TOCTitle: Omitir una cuenta de usuario desde el registro de auditoría de buzones
ms:assetid: 98a87071-fe31-4b67-beb8-a73799e54df2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff461934(v=EXCHG.150)
ms:contentKeyID: 49895796
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Omitir una cuenta de usuario desde el registro de auditoría de buzones

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2013-05-21_

Cuando habilite un registro de auditoría de buzón para buzón, se registran eventos de acceso a buzón especificados (por ejemplo, acceso a una carpeta o a un mensaje o la eliminación permanente de un mensaje). Sin embargo, el acceso de algunas cuentas autorizadas, tales como cuentas usadas por herramientas de terceros o por controles legales, pueden crear una gran cantidad de entradas de registro de auditoría de buzón que, posiblemente, no sean importantes para la organización.

Puede configurar una cuenta de usuario o de equipo para omitir el registro de auditoría de buzón de correo de manera que no se registren el acceso o las acciones llevadas a cabo con la cuenta de usuario o de equipo en cualquier buzón. Al omitir las cuentas de usuario o de equipo de confianza que necesitan tener acceso frecuente a los buzones, puede reducir la información irrelevante en los registros de auditoría de buzones.


> [!WARNING]
> Si utiliza el registro de auditoría de buzón de correo para controlar el acceso y las acciones en buzones, deberá supervisar las asociaciones de omisión de auditoría de buzón con regularidad. Si se añade una asociación de omisión de auditoría de buzón de correo para una cuenta, dicha cuenta podrá obtener acceso a cualquier buzón de la organización para el que se le hayan asignado permisos de acceso sin que se genere ninguna entrada de registro de auditoría de buzón de correo para dicho acceso, ni para ninguna acción realizada (como la eliminación de mensajes).



Para otras tareas de administración relacionadas con el registro de auditoría de buzones de correo, consulte [Procedimientos de registro de auditoría de buzones](mailbox-audit-logging-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría de buzones" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Cuando una cuenta se configura para que omita el registro de auditoría de buzón, no se registrará el acceso al buzón que realice esa cuenta. No puede configurar una cuenta para que omita el registro de acceso a un buzón específico.

  - No puede usar el Centro de administración de Exchange (EAC) para habilitar o deshabilitar la omisión del registro de auditoría de buzón de correo para una cuenta. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para habilitar o deshabilitar la omisión del registro de auditoría de buzón de correo para una cuenta

Si desea ver un ejemplo sobre cómo habilitar la omisión del registro de auditoría de buzón de correo para una cuenta, consulte [Examples](https://technet.microsoft.com/es-es/ff696758\(exchg.150\)#examples) en [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/es-es/library/ff696758\(v=exchg.150\)).

Si desea ver un ejemplo sobre cómo deshabilitar la omisión del registro de auditoría de buzón de correo para una cuenta, consulte [Examples](https://technet.microsoft.com/es-es/ff696758\(exchg.150\)#examples) en [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/es-es/library/ff696758\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Después de omitir una cuenta de usuario del registro de auditoría de buzón de correo, puede comprobar la configuración de la omisión ejecutando el cmdlet [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/es-es/library/ff696741\(v=exchg.150\)).

Si desea ver ejemplos sobre cómo comprobar las asociaciones de omisión de auditoría de buzón de correo, consulte [Examples](https://technet.microsoft.com/es-es/ff696741\(exchg.150\)#examples) en [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/es-es/library/ff696741\(v=exchg.150\)).

