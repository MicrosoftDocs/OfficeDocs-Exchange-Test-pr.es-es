---
title: 'Encontrar dirección URL internas externas para Centro Administración Exchange'
TOCTitle: Encontrar las direcciones URL internas y externas para el Centro de Administración de Exchange
ms:assetid: 3ddb30ff-a405-4b9d-8d77-2d7a3a5ab8fa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ680108(v=EXCHG.150)
ms:contentKeyID: 49895590
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Encontrar las direcciones URL internas y externas para el Centro de Administración de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-04_

Debido a que el Centro de administración de Exchange (EAC) es una consola de administración basada en web en Exchange Server 2013, puede acceder a él con la dirección URL del directorio virtual de ECP en un explorador web. Este tema muestra cómo encontrar la dirección URL del directorio virtual de ECP.


> [!NOTE]
> El ECP es una interfaz de usuario basada en web para Exchange Server 2010. Los cmdlets de EAC para directorios virtuales todavía usa “ECP” en el nombre, y estos cmdlets se pueden usar para administrar los directorios virtuales ECP de Exchange 2010 y Exchange&nbsp;2013.



Para obtener más información acerca de EAC, consulte [Centro de administración de Exchange en Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - No puede usar la EAC para realizar este proceso. Debe usar el Shell.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Conectividad del Centro de administración de Exchange" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use el Shell para encontrar las direcciones URL internas y externas del directorio virtual de ECP

Este ejemplo devuelve el nombre del directorio virtual ECP, la dirección URL interna y la dirección URL externa en una lista de formato.

```powershell
Get-ECPVirtualDirectory | Format-List Name,InternalURL,ExternalURL
```

Cuando se completa un comando, use los valores *InternalURL* o *ExternalURL* de su explorador web para iniciar el EAC.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-EcpVirtualDirectory](https://technet.microsoft.com/es-es/library/dd351058\(v=exchg.150\)).

