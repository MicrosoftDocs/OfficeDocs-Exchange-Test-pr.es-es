---
title: 'ExecutionPolicy GPO is defined: Exchange 2013 Help'
TOCTitle: ExecutionPolicy GPO is defined
ms:assetid: 63de83e2-9a6b-4f57-85b9-df445bea18dd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.powershellexecutionpolicycheckset(v=EXCHG.150)
ms:contentKeyID: 61204108
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ExecutionPolicy GPO is defined

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-15_

Microsoft Exchange Server 2013 Setup can’t continue because it detected that the **ExecutionPolicy** Group Policy Object (GPO) defines one or both of the following policies:

  - **MachinePolicy**

  - **UserPolicy**

No importa cómo se hayan definido las directivas, solo importa que se hayan definido.

When you run Exchange 2013 Setup, Exchange stops and disables the Windows Management Instrumentation (WMI) service. When either of these policies are defined, the WMI service needs to be enabled to run a Windows PowerShell script. If the policies are defined and the WMI service is stopped, Setup will fail and the server will be left in an inconsistent state.

Para que el programa de instalación pueda continuar, debe quitar temporalmente cualquier definición de **MachinePolicy** o **UserPolicy** en el GPO **ExecutionPolicy**.

Para obtener información sobre cómo eliminar las definiciones de **MachinePolicy** o **UserPolicy** en **ExecutionPolicy** GPO, consulte [el artículo KB981474 de Knowledge Base](https://go.microsoft.com/fwlink/?linkid=3052&kbid=981474).


> [!NOTE]
> Even though this Knowledge Base article was written for Exchange 2010, it also applies to Exchange 2013 cumulative updates and service packs.



¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

