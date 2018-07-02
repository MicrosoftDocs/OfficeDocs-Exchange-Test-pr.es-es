---
title: 'Quitar una regla de protección de Outlook: Exchange 2013 Help'
TOCTitle: Quitar una regla de protección de Outlook
ms:assetid: 569fc3be-b269-43f5-8797-73ab0691e685
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633467(v=EXCHG.150)
ms:contentKeyID: 49895638
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Quitar una regla de protección de Outlook

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Las reglas de protección de Microsoft Outlook permiten proteger mensajes con Information Rights Management (IRM) mediante la aplicación de una plantilla de [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/es-es/library/hh831364.aspx) en Outlook 2010 antes de enviar los mensajes. Para evitar que se aplique una regla de protección de Outlook, deshabilítela. Al quitar una regla de protección de Outlook, se elimina la definición de reglas de Active Directory.

Para consultar otras tareas de administración relacionadas con IRM, vea [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Protección de derechos" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para quitar reglas de protección de Outlook. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para quitar una regla de protección de Outlook

En este ejemplo se quita la regla de protección de Outlook llamada OPR-DG-Finance.

    Remove-OutlookProtectionRule -Identity "OPR-DG-Finance"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-OutlookProtectionRule](https://technet.microsoft.com/es-es/library/dd297961\(v=exchg.150\)).

## Usar el Shell para quitar todas las reglas de protección de Outlook

En este ejemplo se eliminan todas las reglas de protección de Outlook de la organización de Exchange.

    Get-OutlookProtectionRule | Remove-OutlookProtectionRule

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-OutlookProtectionRule](https://technet.microsoft.com/es-es/library/dd298004\(v=exchg.150\)) y [Remove-OutlookProtectionRule](https://technet.microsoft.com/es-es/library/dd297961\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que una regla de protección de Outlook se quitó correctamente, use el cmdlet [Get-OutlookProtectionRule](https://technet.microsoft.com/es-es/library/dd298004\(v=exchg.150\)) para recuperar las reglas de protección de Outlook. Para consultar un ejemplo sobre cómo recuperar las reglas de protección de Outlook, vea [Examples](https://technet.microsoft.com/es-es/dd298004\(exchg.150\)#examples) en **Get-OutlookProtectionRule**.

