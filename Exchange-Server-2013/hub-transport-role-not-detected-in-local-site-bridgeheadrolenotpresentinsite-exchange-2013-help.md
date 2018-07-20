---
title: 'Función de concentrador de transporte no detectado en local site_BridgeheadRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: Función de concentrador de transporte no detectado en local site_BridgeheadRoleNotPresentInSite
ms:assetid: f318c947-81a8-4c18-975a-0f1e7868042a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.bridgeheadrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 48268857
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Función de concentrador de transporte no detectado en local site\_BridgeheadRoleNotPresentInSite

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 muestra esta advertencia porque no se pudo detectar una función del servidor de transporte de concentradores existente en el sitio local del servicio de directorio de Active Directory®.

Ha elegido instalar la función de servidor de buzones antes de que esté instalada una instancia de la función de transporte de concentradores en el sitio de Active Directory.

Los servicios de transporte concentrador de Exchange 2007 se han implementeado en el Active Directory de su organización. Los servicios de transporte de concentradores manejan todo el flujo de correo dentro de la organización, aplican reglas organizativas de enrutamiento de flujo de correo y se ocupan de entregar los mensajes en el buzón del destinatario.

Los usuarios podrán iniciar sesión en sus buzones, pero no se podrá enviar ni recibir correo desde este servidor de buzones hasta que no se haya instalado la función de transporte de concentradores.

