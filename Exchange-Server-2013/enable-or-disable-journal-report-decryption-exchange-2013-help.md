﻿---
title: 'Habilitar o deshabilitar el descifrado de informes de diario: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el descifrado de informes de diario
ms:assetid: 1dedbe73-2c1a-4b14-8799-5091aaec7965
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638092(v=EXCHG.150)
ms:contentKeyID: 49895504
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o deshabilitar el descifrado de informes de diario

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Descifrado de informe diario habilitación permite al agente de diario adjunte el descifrado de un mensaje protegido por derechos al informe diario. Antes de habilitar el descifrado de informe de diario, debe agregar el buzón de entrega federada al grupo de superusuarios configurado en el servidor de [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) .

Para ver tareas de administración adicionales relacionadas con la Configuración de Information Rights Management (IRM), consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Protección de derechos" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Los miembros del grupo de superusuarios obtienen una licencia de uso de propietario cuando solicitan una licencia al clúster de AD RMS. Esto les permite descifrar todos los contenidos protegidos por RMS que fueron creados por ese clúster de AD RMS.

  - Un clúster de AD RMS debe estar instalado en el bosque Active Directory.

  - Agregar el buzón de entrega federada al grupo de superusuarios en un clúster de AD RMS. Para obtener información detallada, consulte [Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para habilitar el descifrado de informes diarios. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para habilitar el descifrado de informes de diarios

En este ejemplo, se habilita el descifrado de informes de diarios para la organización de Exchange.

    Set-IRMConfiguration -JournalReportDecryptionEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## Usar el Shell para deshabilitar el descifrado de informes de diarios

En este ejemplo, se deshabilita el descifrado de informes de diarios para la organización de Exchange.

    Set-IRMConfiguration -JournalReportDecryptionEnabled $false

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha habilitado o deshabilitado el descifrado de informes diarios, ejecute el cmdlet **Get-IRMConfiguration** y compruebe el valor de la propiedad *JournalDecryptionEnabled*.

Para ver un ejemplo sobre cómo comprobar la configuración de IRM, consulte [Examples](https://technet.microsoft.com/es-es/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) en **Get-IRMConfiguration**.

