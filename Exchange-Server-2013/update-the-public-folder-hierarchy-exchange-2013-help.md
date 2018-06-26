---
title: 'Actualizar la jerarquía de carpetas públicas: Exchange 2013 Help'
TOCTitle: Actualizar la jerarquía de carpetas públicas
ms:assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ945055(v=EXCHG.150)
ms:contentKeyID: 52061859
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Actualizar la jerarquía de carpetas públicas

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2014-04-03_

Solo tiene que actualizar la jerarquía de carpetas públicas si desea invocar manualmente el sincronizador de jerarquía y el asistente para buzones de correo. Ambos se invocan al menos una vez cada 24 horas para cada buzón de carpeta pública en la organización. El sincronizador de jerarquía se invoca cada 15 minutos si algún usuario inició sesión en un buzón de correo secundario mediante Microsoft Outlook o un cliente de los servicios web de Microsoft Exchange.

Para otras tareas de administración relacionadas con carpetas públicas en Exchange Online, consulte [Procedimientos de carpetas públicas en Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/jj966272\(v=exchg.150\)).

Para otras tareas de administración relacionadas con carpetas públicas en Exchange Server 2013, consulte [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Carpetas públicas" en el tema [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - No puede realizar este procedimiento en el EAC. Debe usar el Shell.

  - Le recomendamos que cuando ejecute este comando con el parámetro *InvokeSynchronizer*, use el parámetro *SuppressStatus*. Si no usa este parámetro en el comando, la salida mostrará mensajes de estado cada 3 segundos durante un máximo de un minuto. Hasta que pase el minuto, no podrá usar esta instancia del Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Actualizar la jerarquía de carpetas públicas

Este ejemplo actualiza la jerarquía de carpeta pública en el buzón de correo de carpeta pública PF\_marketing y suprime la salida del comando.

    Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus

En este ejemplo se actualizan todos los buzones de correo de carpetas públicas y se suprime la salida del comando.

    Get-Mailbox -PublicFolder | Update-PublicFolderMailbox InvokeSynchronizer -SuppressStatus

