---
title: 'Directivas de buzones de Outlook Web App: Exchange 2013 Help'
TOCTitle: Directivas de buzones de Outlook Web App
ms:assetid: 213b8b7a-1c29-49ee-8c98-d0364ddf4f9d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335142(v=EXCHG.150)
ms:contentKeyID: 49895516
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Directivas de buzones de Outlook Web App

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2012-10-05_

Use las directivas de buzones de MicrosoftOutlook Web App para crear directivas en el nivel de la organización que permitan administrar el acceso a las características de Outlook Web App.

**Contenido**

Directivas de buzones de Outlook Web App

Creación o eliminación de las directivas de buzón de correo de Outlook Web App

Configuración de las directivas de buzones de Outlook Web App

Aplicación de las directivas de buzones de Outlook Web App

## Directivas de buzones de Outlook Web App

En Exchange 2013, puede crear varias directivas de buzones de Outlook Web App y aplicarlas a los buzones individuales. Cuando una directiva de buzones de Outlook Web App se aplica a un buzón, ésta invalida la configuración del directorio virtual.

Las características de Outlook Web App también se pueden administrar configurando los directorios virtuales de Outlook Web App. La configuración de los directorios virtuales los usaran los buzones a los cuales no se haya aplicado ninguna directiva de buzón de correo.

## Creación o eliminación de las directivas de buzón de correo de Outlook Web App

Se crea una directiva de buzones de correo de Outlook Web App predeterminada automáticamente cuando se instala Exchange. De forma predeterminada, todas las opciones están habilitadas en la directiva de buzones de Outlook Web App predeterminada. Puede crear todas las directivas de buzones de Outlook Web App que sean necesarias para satisfacer las necesidades de la organización.


> [!NOTE]
> La directiva de buzones de Outlook Web App predeterminada no se aplica a cualquier buzón de forma automática.



Para obtener información acerca de la creación o eliminación de directivas de buzones de correo, consulte [Crear una directiva de buzones de Outlook Web App](create-an-outlook-web-app-mailbox-policy-exchange-2013-help.md) y [Quitar una directiva de buzón de Outlook Web App de Exchange](remove-an-outlook-web-app-mailbox-policy-from-exchange-exchange-2013-help.md).

## Configuración de las directivas de buzones de Outlook Web App

El valor predeterminado de directiva de buzón de correo de Outlook Web App tiene todas las opciones habilitadas de forma predeterminada. Para obtener información acerca de la configuración de las directivas de buzones de correo de Outlook Web App, consulte [Ver o configurar las propiedades de directiva de buzón de Outlook Web App](view-or-configure-outlook-web-app-mailbox-policy-properties-exchange-2013-help.md).

## Aplicación de las directivas de buzones de Outlook Web App

Solo se puede aplicar una directiva de buzones de Outlook Web App a un buzón.

Si no hay directivas de buzones de Outlook Web App aplicadas a un buzón, se aplicará la configuración definida en el directorio virtual.

Una directiva de buzones de correo de Outlook Web App se puede aplicar a un buzón de correo que use el Centro de administración de Exchange (EAC) para modificar un buzón de correo existente, o usando el Shell y el cmdlet [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\)) para aplicar una directiva de buzones de correo. Para obtener más información, consulte [Aplicar o quitar una directiva de buzón de Outlook Web App en un buzón](apply-or-remove-an-outlook-web-app-mailbox-policy-on-a-mailbox-exchange-2013-help.md).

