---
title: 'Servidor de acceso de cliente: Exchange 2013 Help'
TOCTitle: Servidor de acceso de cliente
ms:assetid: 87e206ab-7a7b-4b4f-be1a-5035713c74d2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298114(v=EXCHG.150)
ms:contentKeyID: 48268372
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Servidor de acceso de cliente

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-07-02_

En Microsoft Exchange 2013, ha habido importantes cambios en la arquitectura de los roles de servidores de Exchange. En lugar de los cinco roles de servidor que proporcionaban Exchange 2010 y Exchange 2007, en Exchange 2013, el número de roles de servidor se ha reducido a tres: el servidor de acceso de cliente y el servidor de buzones de correo y, con el Service Pack 1, el rol de servidor de transporte perimetral.


> [!NOTE]
> Exchange&nbsp;2013 puede trabajar también con el rol de servidor de transporte perimetral de Exchange 2010.



El servidor de buzones de correo de Exchange 2013 incluye muchos de los componentes de servidor incluidos en Exchange 2010: protocolos de acceso de cliente, servicios de transporte, bases de datos de buzones de correo y mensajería unificada (el servidor de acceso de cliente redirige el tráfico SIP generado de las llamadas entrantes al servidor de buzones de correo). Para obtener información acerca del servidor de buzones de correo Exchange 2013, consulte [Servidor de buzones de correo](mailbox-server-exchange-2013-help.md).

El servidor de acceso de cliente proporciona servicios de autenticación, de redirección limitada y de proxy, además de los protocolos de acceso de cliente habituales: HTTP, POP, IMAP y SMTP. El servidor de acceso de cliente es un servidor delgado y sin estado que no realiza ningún proceso de representación de datos. Nunca se encuentra nada en cola ni almacenado en el servidor de acceso de clientes. Para obtener información acerca de la nueva arquitectura de Exchange 2013, consulte [Novedades en Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).


> [!WARNING]
> Los servidores de acceso de cliente no admiten en redes perimetrales y deben implementarse dentro del entorno interno de Active Directory. Cada sitio de Active Directory que contiene un servidor de buzones deberá también contener un servidor de acceso de clientes.



Como resultado de estos cambios arquitectónicos, ha habido ciertos cambios en la conectividad del cliente. En primer lugar, RPC/TCP ya no es un protocolo de acceso directo compatible. Esto significa que la conectividad de Outlook en su totalidad debe realizarse utilizando RPC mediante HTTP (también conocido como Outlook en cualquier lugar), o con Exchange 2013 SP1 y Outlook 2013 SP1, MAPI a través de HTTP. Como resultado de estos cambios, no es necesario tener el servicio de acceso de cliente de RPC en el servidor de acceso de cliente. Además, se necesitan menos espacios de nombre para una solución con capacidad de recuperación de sitios en comparación con Exchange 2010, y ya no es necesario proporcionar afinidad para el servicio de acceso de cliente de RPC. Además, los clientes de Outlook ya no se conectarán a un servidor de nombre de dominio completo (FQDN) como lo hacían en todas las versiones anteriores de Exchange. Con la detección automática, Outlook encuentra un nuevo punto de conexión formado por el GUID del buzón del usuario + @ + la parte del dominio de la dirección SMTP principal del usuario. Este cambio minimiza la probabilidad de que los usuarios vean el temido mensaje "Su administrador ha realizado un cambio en el buzón". Solamente Outlook 2007 y las versiones posteriores son compatibles con Exchange 2013.

## Funcionalidad del servidor de acceso de cliente

El servidor de acceso de cliente de Exchange 2013 funciona de forma muy similar a la de una puerta principal, admitiendo todas las solicitudes de clientes y redirigiéndolos a la base de datos activa de buzones de correo. El servidor de acceso de cliente proporciona una funcionalidad de protección de red como la Capa de sockets seguros (SSL) y la autenticación de cliente. Además, administra las conexiones de clientes a través de la redirección y la funcionalidad de proxy. El servidor de acceso de cliente autentica las conexiones de cliente y, en la mayoría de casos, enviará una solicitud al servidor de buzones que contiene actualmente la copia activa de la base de datos que contiene el buzón del usuario. En algunos casos, el servidor de acceso de cliente podrá redirigir la solicitud a un servidor de acceso de cliente más adecuado, ya sea a uno con una ubicación diferente o que ejecute una versión más reciente de Exchange Server.

El servidor de acceso de cliente tiene las siguientes características:

  - **Servidor sin estado** En las versiones anteriores de Exchange, muchos de los protocolos de acceso de cliente requerían una afinidad de sesión. Por ejemplo, Outlook Web App requería que todas las solicitudes de un cliente concreto se gestionaran a través de un servidor de acceso de cliente concreto en una matriz de carga equilibrada de los servidores de acceso de cliente. En Exchange 2013, el servidor de acceso de cliente no tiene estado. En otras palabras, dado que todos los procesos del buzón ocurren en el servidor de buzones de correo, no tiene importancia cuál de los servidores de acceso de cliente de una matriz de servidores de acceso de cliente recibe cada solicitud de cliente individual. El cambio en la funcionalidad implica que la afinidad de sesión ya no es necesaria a nivel de balanceo de carga. Esto permite que las conexiones entrantes a los servidores de acceso de cliente se equilibren mediante sencillas técnicas que proporciona la tecnología de equilibrio de cargas, como la de DNS round-robin. También permite que los dispositivos de equilibrio de cargas de hardware admita un mayor número de conexiones concurrentes.

  - **Agrupación de conexiones** Los servidores de acceso de cliente gestionan la autenticación de cliente y envían los datos AuthN al servidor de buzones. La cuenta que utilizan los servidores de acceso de cliente para conectarse a los servidores de buzones es una cuenta privilegiada, miembro del grupo de servidores de Exchange. Esto permite que los servidores de acceso de cliente agrupen las conexiones con eficacia en los servidores de buzones. Una matriz de servidores de acceso de cliente puede gestionar millones de conexiones de clientes de Internet, pero se utilizan muchas menos conexiones para dirigir las solicitudes a los servidores de buzones de correo que en las versiones anteriores de Exchange. Esto mejora la eficacia en el procesamiento y la latencia de un extremo a otro.

## Tareas de administración en el servidor de acceso de cliente

En Exchange 2013, hay varias tareas clave que se pueden realizar en el servidor de acceso de cliente. La administración de certificados digitales se realiza principalmente en el servidor de acceso de cliente, además de algunas tareas de administración de protocolos de cliente para Exchange ActiveSync, POP3 e IMAP4.

