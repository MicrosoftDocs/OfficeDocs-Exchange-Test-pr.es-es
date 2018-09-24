---
title: 'Configuración del asistente para carpetas administradas: Exchange 2013 Help'
TOCTitle: Configuración del asistente para carpetas administradas
ms:assetid: 9fcfb9b6-bd24-4218-a163-bc599cd5476a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123958(v=EXCHG.150)
ms:contentKeyID: 49895805
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuración del asistente para carpetas administradas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-10-01_

El *asistente para carpeta administrada* es un asistente de buzones de Microsoft Exchange que aplica la configuración de retención de mensajes establecida en las directivas de retención.

Si está buscando otras tareas de administración relacionadas con la administración de registros de mensajes (MRM), consulte [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo para completar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Administración de los registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para configurar el asistente para carpeta administrada. Debe usar el Shell

  - En Exchange 2013, el Asistente para carpeta administrada es un asistente basado en limitaciones. Los asistentes basados en limitaciones funcionan constantemente y no es necesario programarlos. Los recursos del sistema que pueden consumir son limitados. Puede configurar el Asistente de carpetas administradas para procesar todos los buzones en un servidor del buzón dentro de un cierto período (conocido como un *ciclo de trabajo)*. El ciclo de trabajo se establece en un día por defecto.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para configurar el Asistente de carpetas administradas

Este ejemplo configura el Asistente de carpetas administradas para procesar todos los buzones en un día.

```powershell
Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-MailboxServer](https://technet.microsoft.com/es-es/library/aa998651\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha logrado configurar el Asistente de carpetas administradas, use el cdmlet [Get-MailboxServer](https://technet.microsoft.com/es-es/library/bb123539\(v=exchg.150\)) para comprobar el parámetro *ManagedFolderWorkCycle*.

Este comando recupera todos los servidores de buzón de correo de la organización y presenta las propiedades del ciclo de trabajo del Asistente de carpetas administradas de cada servidor en formato de tabla. El modificador *Auto* se utiliza para ajustar automáticamente el ancho de columna.

```powershell
    Get-MailboxServer | Format-Table Name,ManagedFolderWorkCycle* -Auto
```

## Usar el Shell para iniciar el Asistente para carpetas administradas

Este ejemplo desencadena el Asistente de carpetas administradas para procesar inmediatamente el buzón de Morris Cornejo.

```powershell
Start-ManagedFolderAssistant -Identity morris.cornejo@contoso.com
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Start-ManagedFolderAssistant](https://technet.microsoft.com/es-es/library/aa998864\(v=exchg.150\)).

