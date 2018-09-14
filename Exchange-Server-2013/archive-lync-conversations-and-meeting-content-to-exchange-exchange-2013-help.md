---
title: 'Archivar conversaciones Lync contenido reunión en Exchange: Exchange 2013 Help'
TOCTitle: Archivar conversaciones de Lync y contenido de reuniones en Exchange
ms:assetid: 3cff970e-e5ed-4a54-88e6-3665d84b5ed7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn508399(v=EXCHG.150)
ms:contentKeyID: 59678852
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Archivar conversaciones de Lync y contenido de reuniones en Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Puede archivar contenido de Lync Online, como las conversaciones de mensajería instantánea, en el buzón de un usuario en Exchange Online. En implementaciones locales, puede archivar contenido de Lync 2013 en buzones de Exchange 2013. En entornos locales y en línea, es necesario colocar una retención por juicio o una conservación local en el buzón del usuario. Cuando un usuario elimina permanentemente el contenido de Lync cuyo buzón se encuentra en suspensión, el contenido de Lync archivado se conserva en la carpeta Elementos recuperables del buzón del usuario. No es visible para los usuarios, pero se incluye en las búsquedas de eDiscovery.

Cuando coloca un buzón en retención por juicio, se conservan todos los tipos de contenido, incluidos los elementos de Lync. De manera predeterminada, este también es el caso cuando crea una conservación local. En cambio, si quiere usar una conservación local para conservar únicamente los elementos de Lync, puede usar la opción **Seleccionar tipos de mensajes** del Asistente de **eDiscovery y suspensión local** para seleccionar **Elementos de Lync**, como se muestra en la siguiente captura de pantalla.

![Colocar en espera elementos de Lync](images/Dn508399.691d2324-9fac-4689-8527-c78d387e0e3e(EXCHG.150).jpg "Colocar en espera elementos de Lync")


> [!NOTE]
> También puede configurar una conservación local para excluir elementos de Lync. Por ejemplo, las organizaciones pueden preferir conservar elementos de correo de voz y mensajes instantáneos durante un período de tiempo más corto que otros tipos de contenido. Para implementar este tipo de directiva de suspensión, creará una conservación local para conservar el contenido durante un período de tiempo largo (por ejemplo, 7 años) y excluir elementos de Lync de esta suspensión. Después, creará otra conservación local con una duración de la suspensión inferior que conserve solo elementos de Lync. También puede especificar cuánto tiempo debe conservarse el contenido. Para obtener más información sobre la creación de una suspensión con una duración específica, vea <A href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/in-place-and-litigation-holds">Conservación local y retención por juicio</A>.



Vea los temas siguientes para obtener instrucciones paso a paso para colocar un usuario en suspensión:

  - [Crear o quitar una conservación local](create-or-remove-an-in-place-hold-exchange-2013-help.md)

  - [Poner un buzón en retención por juicio](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

Para ver otras tareas de administración relacionadas con el archivado, vea:

  - [Habilitar o deshabilitar un buzón de archivo en Exchange Online](https://technet.microsoft.com/es-es/library/jj984357\(v=exchg.150\))

  - [Administrar archivos locales en Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

## Más información

  - El archivado de contenido de Lync se produce en el servidor, independientemente de si el usuario tiene configurado el cliente de Lync en [Guardar conversaciones de mensajería instantánea de Lync en la carpeta Historial de conversaciones](https://go.microsoft.com/fwlink/p/?linkid=400589).

  - El archivado de contenido de Lync comienza después de colocar el usuario en retención por juicio o conservación local. Para asegurarse de que las comunicaciones de Lync del usuario se archivan desde el momento en que crea su cuenta, coloque la cuenta en suspensión justo después de crearla.

Además, en las implementaciones locales de Exchange 2013 y Lync 2013:

  - Debe configurar la autenticación de OAuth entre Lync 2013 y Exchange 2013. Para obtener más información, vea [Integración con SharePoint y Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

  - También puede archivar contenido de Lync 2013 en Exchange 2013, independientemente de si un usuario se coloca en suspensión. Esto se realiza mediante la configuración de la directiva de archivado de Exchange del usuario. Use el cmdlet `Set-CsUser` en el servidor de Lync 2013 para establecer la propiedad *ExchangeArchivingPolicy* del usuario de Lync en `ArchivingToExchange`.

  - Para obtener más información sobre el archivado de contenido de Lync en implementaciones locales, vea [Planear el archivado](https://go.microsoft.com/fwlink/p/?linkid=400590) de la documentación de Lync 2013.

