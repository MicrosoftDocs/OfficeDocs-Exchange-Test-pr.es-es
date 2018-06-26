---
title: 'Habilitar o deshabilitar IRM para mensajes internos: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar IRM para mensajes internos
ms:assetid: a6a17f57-5304-41f1-954d-7301857d54a1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124077(v=EXCHG.150)
ms:contentKeyID: 49895815
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar IRM para mensajes internos

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-12_

En Microsoft Exchange Server 2013, Information Rights Management (IRM) está habilitado para los mensajes internos de forma predeterminada. Esto permite crear reglas de protección de transporte y reglas de protección de Microsoft Outlook para proteger con IRM los mensajes durante el transporte y en los clientes de Microsoft Outlook 2010 y posteriores. Habilitar IRM para los mensajes internos es un requisito previo para el resto de funciones de IRM de Exchange Server 2013 como el descifrado de transporte, el descifrado de reglas del diario, IRM en Microsoft OfficeOutlook Web App e IRM en Microsoft Exchange ActiveSync.


> [!WARNING]
> Al deshabilitar IRM para los mensajes internos se desactivan todas las funciones de IRM de la organización de Exchange. Las características de IRM del cliente en Outlook, como la capacidad de leer, responder, reenviar y crear mensajes protegidos por IRM utilizando un servidor Active Directory Rights Management Services (AD RMS), no se ven afectadas.



Para tareas de gestión relacionadas con la gestión de IRM, consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Protección de derechos" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - No puede usar el Centro de administración de Exchange (EAC) para habilitar IRM para mensajes internos. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para habilitar IRM para los mensajes internos

En este ejemplo se habilita IRM para los mensajes internos de la organización de Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## Uso del Shell para deshabilitar IRM para los mensajes internos

En este ejemplo se deshabilita IRM para los mensajes internos de la organización de Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $false

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha activado o desactivado IRM para los mensajes internos, use el cmdlet [Get-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd776120\(v=exchg.150\)) para comprobar la configuración.

