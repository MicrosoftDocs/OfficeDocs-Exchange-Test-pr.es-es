---
title: 'Agregar o quitar etiquetas de retención en una directiva de retención'
TOCTitle: Agregar etiquetas de retención o quitar etiquetas de retención de una directiva de retención
ms:assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd362328(v=EXCHG.150)
ms:contentKeyID: 49895577
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agregar etiquetas de retención o quitar etiquetas de retención de una directiva de retención

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-02_

Puede agregar etiquetas de retención a una directiva de retención al crear la directiva o en cualquier momento posterior a la creación. Para obtener información acerca de cómo crear una directiva de retención, incluido cómo agregar etiquetas de retención simultáneamente, vea [Crear directivas de retención](create-a-retention-policy-exchange-2013-help.md).

Una directiva de retención puede contener las siguientes etiquetas de retención:

  - Directiva de retención de una o varias etiquetas (RPTs) para las carpetas predeterminadas admitidas

  - Una etiqueta de directiva predeterminada (DPT) con la acción **Mover a archivo**

  - Un DPT con la acción **Eliminar y permitir recuperación** o **Eliminar permanentemente**

  - Un DPT para el correo de voz

  - Cualquier número de etiquetas personales

Para obtener más información acerca de las etiquetas de retención, vea [Etiquetas de retención y directivas de retención](retention-tags-and-retention-policies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Administración de los registros de mensajes" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Las etiquetas de retención no se aplican al buzón de correo hasta vincularlas con una directiva de retención y el Asistente para carpeta administrada procese el buzón de correo. Vea [Configuración del asistente para carpetas administradas](configure-the-managed-folder-assistant-exchange-2013-help.md) para iniciar el Asistente para carpetas administradas para que procese un buzón.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para agregar o quitar etiquetas de retención

1.  Vaya a **Administración de cumplimiento** \>**Directivas de retención**.

2.  En la vista de lista, seleccione la directiva de retención a la cual desee agregar etiquetas de retención y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **Directivas de retención**, use la siguiente configuración:
    
      - **Agregar** ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")   Haga clic en este botón para agregar una etiqueta de retención para la directiva.
    
      - **Quitar** ![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar")   Seleccione una etiqueta de la lista y haga clic en este botón para quitarla de la directiva.

## Usar el Shell para agregar o quitar etiquetas de retención

Este ejemplo agrega las etiquetas de retención VPs-Default, VPs-Inbox, y VPs-DeletedItems a la directiva de retención RetPolicy-VPs, que ya no tiene etiquetas de retención vinculadas.


> [!WARNING]
> Si la directiva tiene etiquetas de retención vinculadas, este comando reemplazará las etiquetas existentes.



    Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"

En este ejemplo, se agrega la etiqueta de retención VPs-DeletedItems a la directiva de retención RetPolicy-VPs, la cual ya tiene otras etiquetas de retención vinculadas.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

En este ejemplo, se quita la etiqueta de retención VPs la Bandeja de entrada de la directiva de retención RetPolicy-VPs.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

Para obtener más información acerca de la sintaxis y los parámetros, vea [Set-RetentionPolicy](https://technet.microsoft.com/es-es/library/dd335196\(v=exchg.150\)) y [Get-RetentionPolicy](https://technet.microsoft.com/es-es/library/dd298086\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha agregado o quitado correctamente una etiqueta de retención de una directiva de retención, use el cmdlet [Get-RetentionPolicy](https://technet.microsoft.com/es-es/library/dd298086\(v=exchg.150\)) para comprobar la propiedad *RetentionPolicyTagLinks*.

Este ejemplo usa el cmdlet **Get-RetentionPolicy** para recuperar etiquetas de retención agregadas a la directiva de MRM predeterminada y las canaliza al cmdlet **Format-Table** para obtener sólo el nombre de cada etiqueta.

    (Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name

