---
title: 'Función de acceso de cliente no detectado en local site_ClientAccessRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: Función de acceso de cliente no detectado en local site_ClientAccessRoleNotPresentInSite
ms:assetid: b5bfc6af-9c55-46c0-a293-6078b64e87dd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.clientaccessrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 48268580
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Función de acceso de cliente no detectado en local site\_ClientAccessRoleNotPresentInSite

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 ha mostrado esta advertencia porque una función de acceso de cliente existente no se pudo detectar en el sitio del servicio de directorio local de Active Directory®.

Ha elegido instalar la función de servidor de buzones antes de que esté instalada una instancia de la función de acceso de cliente en el sitio de Active Directory.

La función de servidor de acceso de clientes acepta conexiones con el servidor de Exchange 2007 desde una variedad de clientes diferentes. Los clientes de software como Microsoft Outlook Express y Eudora usan conexiones POP3 o IMAP4 para comunicarse con el servidor de Exchange. Los clientes de hardware, como los dispositivos móviles, usan ActiveSync, POP3 o IMAP4 para comunicarse con el servidor de Exchange.

Si los usuarios tienen acceso a su Bandeja de entrada usando un cliente distinto de Microsoft Office Outlook®, debe instalar la función de servidor de acceso de cliente en su organización Exchange.

Los usuarios podrán iniciar sesión en sus buzones con Outlook pero no podrán usar Outlook Web Access o dispositivos móviles en el mismo buzón hasta que esté presente una función de acceso de cliente en el sitio local de Active Directory.

