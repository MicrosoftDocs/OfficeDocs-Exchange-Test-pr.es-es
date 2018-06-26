---
title: 'Tareas de administración del directorio virtual de Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Tareas de administración del directorio virtual de Exchange ActiveSync
ms:assetid: f0b339b7-e184-4392-a133-20523183459d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125170(v=EXCHG.150)
ms:contentKeyID: 49896006
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Tareas de administración del directorio virtual de Exchange ActiveSync

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-05_

Puede administrar varias opciones de configuración de la aplicación Exchange ActiveSync en Exchange Server 2013 mediante el directorio virtual de Exchange ActiveSync. Internet Information Services (IIS) usa un directorio virtual para permitir el acceso a una aplicación web, como Exchange ActiveSync. Parte de la configuración del directorio virtual que puede administrar para Exchange ActiveSync incluye la autenticación, la seguridad y la generación de informes.

## Configuración del directorio virtual de Exchange ActiveSync

Puede modificar las siguientes propiedades y opciones de configuración en el directorio virtual de Exchange ActiveSync:

  - **InternalURL** InternalURL es la URL que los clientes internos pueden usar para acceder al directorio virtual. Generalmente, tiene el formato https://servername/Microsoft-Server-ActiveSync. Por ejemplo, si el nombre NetBIOS es Sequoia, InternalURL será https://sequoia/Microsoft-Server-ActiveSync.

  - **ExternalURL** ExternalURL es la URL que los clientes externos pueden usar para acceder al directorio virtual. Se debe poder acceder a esta URL desde afuera de la red interna. Por ejemplo, ExternalURL puede ser https://www.contoso.com/.

  - **Configuración de autenticación** Los dos métodos de autenticación que puede configurar para el directorio virtual de Exchange ActiveSync son Autenticación básica y Autenticación de certificados de cliente.

