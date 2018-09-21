---
title: 'Desactivar o suspender administración registros mensajería: Exchange 2013 Help'
TOCTitle: Desactivar o suspender la administración de registros de mensajería
ms:assetid: 631191aa-3bba-4ebf-a727-c48ed2ebe176
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998580(v=EXCHG.150)
ms:contentKeyID: 52062028
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desactivar o suspender la administración de registros de mensajería

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Última modificación del tema:** 2013-02-14_

A fin de cumplir con necesidades individuales, de TI o comerciales, es posible que deba desactivar o suspender temporalmente la administración de registros de mensajes (MRM). Entre los motivos para que esto suceda se incluyen los siguientes:

  - Si un usuario de buzón de correo se encuentra fuera de la oficina o bien no tener acceso al correo electrónico por algún otro motivo, puede deshabilitar la MRM de ese buzón colocándolo en suspensión de la retención. Cuando un buzón de correo se encuentra en suspensión de la retención, el Asistente de carpetas administradas ya no lo procesa. Cuando el usuario del buzón de correo regresa o puede nuevamente tener acceso a su buzón de correo, puede quitarle la suspensión de la retención.

  - En caso de necesitar probar o solucionar problemas de rendimiento, puede desactivar MRM temporalmente en un servidor en particular, borrando la programación del Asistente para carpetas administradas.

  - Si necesita quitar una etiqueta de retención de un grupo de buzones (aquellos que tengan una directiva de retención con dicha etiqueta aplicada), puede quitar la etiqueta de la directiva.

  - Si desea que una directiva de retención o una directiva de buzones de correo de carpetas administradas deje de aplicarse a un buzón de correo, puede quitarla del mismo.

  - Si la organización decide no usar las características de MRM, es posible desactivarla de manera permanente para toda la organización. Si más adelante decide implementar MRM, tendrá la capacidad de hacerlo.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## ¿Qué desea hacer?

## Colocar buzones en suspensión de la retención

Puede colocar buzones en suspensión de la retención a fin de desactivar la MRM de manera temporaria (por ejemplo, mientras los usuarios están de vacaciones). Esto suspenderá el procesamiento de directivas de retención para el buzón hasta que se deshabilite la suspensión de la retención. Esto es diferente a colocar buzones en conservación local o retención por juicio.

Para obtener información detallada acerca de cómo colocar un buzón de correo en suspensión de retención, consulte [Poner un buzón en retención](https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold).

Para obtener más información acerca de retención local y retención por litigio, consulte [Conservación local y retención por juicio](https://docs.microsoft.com/es-es/exchange/security-and-compliance/in-place-and-litigation-holds).

## Quitar etiquetas de retención de buzones de correo

Para quitar una etiqueta de retención de un buzón de correo, se desvincula la etiqueta de la directiva de retención. Al desvincular una etiqueta de directiva de retención (RPT) de una carpeta predeterminada, se aplicará la etiqueta predeterminada de buzón de correo a todos los elementos de esa carpeta. Cuando se desvincule una etiqueta personal, ya no estará disponible para el usuario. Las etiquetas aplicadas a los mensajes existentes continuarán procesándose a menos que quite la etiqueta de la organización de Exchange.

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Administración de los registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

En este ejemplo del Shell se desvincula la etiqueta de retención Eliminar - 3 días de la directiva de retención Usuarios-corporativos.

    $tags = (Get-RetentionPolicy "Corp-Users").RetentionPolicyTagLinks
    $tags -= "Deleted Items - 3 Days"
    Set-RetentionPolicy "Corp-Users" -RetentionPolicyTagLinks $tags

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-RetentionPolicy](https://technet.microsoft.com/es-es/library/dd298086\(v=exchg.150\)) y [Set-RetentionPolicy](https://technet.microsoft.com/es-es/library/dd335196\(v=exchg.150\)).

## Quitar directivas de retención de buzones

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Aplicación de directivas de retención" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Es posible detener la aplicación de una directiva de retención en un buzón de correo, si se quita la directiva de las propiedades de usuario del buzón de correo.

En este ejemplo del Shell, se quita la directiva de retención del buzón de correo jescolar.

```powershell
Set-Mailbox jpeoples -RetentionPolicy $null.
```

En este ejemplo del Shell, se quita la directiva de retención de todos los buzones de la organización de Exchange.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -ne $null} | Set-Mailbox -RetentionPolicy $null

En este ejemplo del Shell, se quita la directiva de retención Finanzas-Corp de todos los usuarios de buzones que tienen la directiva aplicada.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -eq "Corp-Finance"} | Set-Mailbox -RetentionPolicy $null

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) y [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)).

## Desactivar permanentemente MRM para toda la organización

Para desactivar el MRM de una organización, elimine todas las etiquetas y directivas de retención, excepto la directiva ArbitrationMailbox, que la crea el programa de instalación de Exchange. Una vez realizado este paso, ya no se aplicarán directivas de retención.


> [!WARNING]
> Las directivas de retención también incluyen etiquetas Mover a archivo, que mueven mensajes al buzón de archivo del usuario. Si quita una directiva de retención que tiene una etiqueta Mover a archivo, el Asistente de carpetas administradas ya no moverá mensajes al archivo de aquellos usuarios que tenían la directiva aplicada.<BR>Para evitarlo, quite sólo las etiquetas Eliminar y permitir recuperación y Eliminar permanentemente de la organización y conserve las directivas que tengan las etiquetas Mover a archivo aplicadas. Alternativamente, los usuarios que tengan un archivo habilitado pueden mover manualmente elementos a su buzón de archivo usando Outlook o Outlook Web App.<BR>Antes de quitar las etiquetas de retención o las directivas de retención, es recomendable que compruebe los ajustes de las etiquetas que quitará. No elimine etiquetas con acción de retención Mover a archivo.



Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Administración de los registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> Incluya el modificador <EM>WhatIf</EM> en los comandos siguientes para simular la acción tomada por un comando.



Este ejemplo quita todas las etiquetas de eliminación de una organización de Exchange, excepto la etiqueta Nunca eliminar, que se utiliza en la directiva ArbitrationMailbox creada por el programa de instalación de Exchange.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -ne "MoveToArchive" -and $_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

Este ejemplo quita todas las etiquetas de retención, excepto la etiqueta Nunca eliminar.

    Get-RetentionPolicyTag | ? {$_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

Este comando quita la directiva de retención Corp-Users de una organización de Exchange.

```powershell
Remove-RetentionPolicy Corp-Users
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [Get-RetentionPolicyTag](https://technet.microsoft.com/es-es/library/dd298009\(v=exchg.150\))

  - [Remove-RetentionPolicyTag](https://technet.microsoft.com/es-es/library/dd335092\(v=exchg.150\))

  - [Remove-RetentionPolicy](https://technet.microsoft.com/es-es/library/dd297962\(v=exchg.150\))

