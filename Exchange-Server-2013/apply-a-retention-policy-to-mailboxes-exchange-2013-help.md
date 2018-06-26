---
title: 'Aplicar una directiva de retención a los buzones: Exchange 2013 Help'
TOCTitle: Aplicar una directiva de retención a los buzones
ms:assetid: 6ccc80db-d201-44f7-8d4b-473a89c14b2f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298052(v=EXCHG.150)
ms:contentKeyID: 49895693
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aplicar una directiva de retención a los buzones

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2014-10-01_

Es posible usar directivas de retención para agrupar una o más etiquetas de retención y aplicarlas a los buzones para hacer respetar las configuraciones de retención de mensajes. Un buzón no puede tener más de una directiva de retención.


> [!WARNING]
> Los mensajes caducan según la configuración definida en las etiquetas de retención vinculadas a la directiva. Esta configuración incluye acciones como el movimiento de mensajes al archivo o su eliminación permanente. Antes de aplicar una directiva de retención a uno o más buzones, se recomienda comprobar la directiva e inspeccionar cada etiqueta de retención relacionada con ella.



Para consultar otras tareas de administración relacionadas con la administración de registros de mensajes (MRM), vea [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Entrada "Aplicación de directivas de retención" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para aplicar una directiva de retención a un buzón

1.  Vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione el buzón en el que desea aplicar la directiva de retención y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **Buzón de usuario**, haga clic en **Características de buzón de correo**.

4.  En la lista **Directiva de retención**, seleccione la directiva que desea aplicar al buzón y, a continuación, haga clic en **Guardar**.

## Usar el EAC para aplicar una directiva de retención a varios buzones

1.  Vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, use las teclas Mayús o Ctrl para seleccionar varios buzones.

3.  En el panel de detalles, haga clic en **Más opciones**.

4.  En **Directiva de retención**, haga clic en **Actualizar**.

5.  En **Directiva de retención de asignación masiva**, seleccione la directiva de retención que desea aplicar a los buzones y, a continuación, haga clic en **Guardar**.

## Usar el Shell para aplicar una directiva de retención a un buzón

En este ejemplo, se aplica la directiva de retención RP-Finanzas del buzón de Navarro.

    Set-Mailbox "Morris" -RetentionPolicy "RP-Finance"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## Usar el Shell para aplicar una directiva de retención a varios buzones

En este ejemplo, se aplica la nueva directiva de retención New-Retention-Policy a todos los buzones que tienen la directiva anterior Old-Retention-Policy.

    $OldPolicy={Get-RetentionPolicy "Old-Retention-Policy"}.distinguishedName
    Get-Mailbox -Filter {RetentionPolicy -eq $OldPolicy} -Resultsize Unlimited | Set-Mailbox -RetentionPolicy "New-Retention-Policy"

En este ejemplo se aplica la directiva de retención RetentionPolicy-Corp a todos los buzones de correo de la organización de Exchange.

    Get-Mailbox -ResultSize unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Corp"

En este ejemplo se aplica la directiva de retención RetentionPolicy-Finance a todos los buzones de correo de la unidad organizativa Finance.

    Get-Mailbox -OrganizationalUnit "Finance" -ResultSize Unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Finance"

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) y [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se aplicó la directiva de retención, ejecute el cmdlet [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) a fin de recuperar la directiva de retención para el buzón o los buzones.

En este ejemplo se recupera la directiva de retención al buzón de Navarro.

    Get-Mailbox Morris | Select RetentionPolicy

Este comando recupera todos los buzones que tienen aplicada la directiva de retención RP-Finance.

    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionPolicy -eq "RP-Finance"} | Format-Table Name,RetentionPolicy -Auto

