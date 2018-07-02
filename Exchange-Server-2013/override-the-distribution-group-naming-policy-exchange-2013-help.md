---
title: 'Invalidar la directiva de nomenclatura de grupos de distribución: Exchange 2013 Help'
TOCTitle: Invalidar la directiva de nomenclatura de grupos de distribución
ms:assetid: 9eb23fc9-3f59-4d09-9077-85c89a051ee0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ218685(v=EXCHG.150)
ms:contentKeyID: 49115855
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Invalidar la directiva de nomenclatura de grupos de distribución

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-10-13_

La directiva de nomenclatura de grupos para grupos de distribución solo se aplica a los grupos que crean los usuarios. Si usted u otros administradores utilizan el centro de administración de Exchange (EAC) para crear grupos de distribución, la directiva de nomenclatura de grupos se ignora y no se aplica al nombre del grupo.

Sin embargo, si utiliza el Shell de administración de Windows para crear o cambiar el nombre de un grupo de distribución, la directiva de nomenclatura de grupos también se aplica a los grupos creados por los administradores, a menos que utilice el parámetro *IgnoreNamingPolicy* para invalidar dicha directiva.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Grupos de distribución" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para invalidar la directiva de nomenclatura de grupos al crear un grupo nuevo

Para invalidar el grupo de política de nomenclatura, ejecute el siguiente comando.

    New-DistributionGroup -Name <Group Name> -IgnoreNamingPolicy

Por ejemplo, si la directiva de nomenclatura de grupos para su organización es **DG\_\<Group Name\>\_Users**, ejecute el comando siguiente para crear un grupo denominado **All Administrators**.

    New-DistributionGroup -Name "All Administrators" -IgnoreNamingPolicy

Cuando Microsoft Exchange crea este grupo, utiliza **All Administrators** para los parámetros *Name* y *DisplayName*.

## Usar el Shell para invalidar la directiva de nomenclatura de grupos al renombrar un grupo

Para invalidar la directiva de nomenclatura de grupos al cambiar el nombre de un grupo existente con el Shell, ejecute el comando siguiente.

    Set-DistributionGroup -Identity <Old Group Name> -Name <New Group Name> -DisplayName <New Group Name> -IgnoreNamingPolicy

Por ejemplo, supongamos que crea la directiva de nomenclatura de grupos a última hora de la noche y que a la mañana siguiente se da cuenta de que ha escrito mal la cadena de texto del prefijo. Por la mañana, ve que ya se ha creado un nuevo grupo con el prefijo mal escrito. Podrá corregir la directiva de nomenclatura de grupos en el EAC, pero tendrá que utilizar el Shell para cambiar el nombre del grupo mal escrito. Ejecute el siguiente comando.

    Set-DistributionGroup -Identity "Goverment_Contracts_NWRegion" -Name "Government_ContractEstimates_NWRegion" -DisplayName "Government_ContractEstimates_NWRegion" -IgnoreNamingPolicy


> [!IMPORTANT]
> Cuando cambie el nombre de un grupo, no se olvide de incluir el parámetro <EM>DisplayName</EM>. Si no lo hace, el nombre anterior se seguirá mostrando en la libreta de direcciones compartida y en las líneas Para:, Cc: y De: de los mensajes de correo electrónico.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha logrado crear o cambiar el nombre de un grupo de distribución que omitirá la directiva de nombramiento del grupo, ejecute los siguientes comandos.

    Get-DistributionGroup <Name> | FL DisplayName

    Get-OrganizationConfig | FL DistributionGroupNamingPolicy

Sabrá si ha funcionado cuando el formato del nombre para mostrar del grupo sea distinto al que su organización aplica en la directiva de nomenclatura de grupo.

