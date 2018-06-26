---
title: 'Convertir un buzón: Exchange 2013 Help'
TOCTitle: Convertir un buzón
ms:assetid: dfed045e-a740-4a90-aff9-c58d53592f79
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ710164(v=EXCHG.150)
ms:contentKeyID: 49895967
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Convertir un buzón

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-04-26_

La conversión de un buzón a otro tipo de buzón es muy similar a la experiencia de Exchange 2010. Todavía debe usar el cmdlet Set-Mailbox en el shell para realizar la conversión.

Puede convertir los siguientes buzones de un tipo a otro:

  - Buzón de usuario para el buzón de recursos (sala o equipo)

  - De buzón compartido a buzón de usuario

  - De buzón compartido a buzón de recursos

  - De buzón de recursos a buzón de usuario

  - De buzón de recursos a buzón compartido

Tenga en cuenta que, si su organización usa un entorno de Exchange híbrido, debe administrar los buzones mediante las herramientas de administración de Exchange local. Para convertir un buzón a un entorno híbrido, necesitará volver a mover el buzón a Exchange local, convertir el tipo de buzón y, después, moverlo a Office 365 otra vez.


> [!IMPORTANT]
> Si quiere convertir un buzón de usuario a uno compartido, primero debe quitar cualquier dispositivo móvil de dicho buzón, o bien bloquear el acceso el acceso móvil a él tras la conversión. Esto es así porque, una vez que se convierta el buzón en uno compartido, la funcionalidad móvil no funcionará correctamente. Para obtener más información sobre el proceso de bloqueo, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=847873">Quitar un antiguo empleado de Office 365</A>.



## Usar el Shell para convertir un buzón

Tiempo estimado para finalizar:  5 minutos.

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

En este ejemplo, se convierte el buzón compartido, MarketingDept1 a un buzón de usuario.

    Set-Mailbox MarketingDept1 -Type Regular

Puede usar los siguientes valores para el parámetro *Type*:

  - Regular

  - Sala

  - Equipo

  - Compartido

Para obtener información detallada sobre la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el comando se convirtió correctamente, ejecute el siguiente comando de Shell:

    Get-Mailbox -Identity MarketingDept1 | Format-List RecipientTypeDetails

El valor de *RecipientTypeDetails* debe ser *UserMailbox*.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


