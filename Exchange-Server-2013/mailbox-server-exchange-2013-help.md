---
title: 'Servidor de buzones de correo: Exchange 2013 Help'
TOCTitle: Servidor de buzones de correo
ms:assetid: 1aacc1c9-c81b-47d4-b222-ee73956cf968
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150491(v=EXCHG.150)
ms:contentKeyID: 48267857
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servidor de buzones de correo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-19_

En Microsoft Exchange Server 2010, el rol de servidor Buzón de correo hospedaba las bases de datos de carpetas públicas y de buzones y también proporcionaba almacenamiento de mensajes. Ahora, en Exchange Server 2013, el rol de servidor Buzón de correo también incluye los protocoles de acceso de clientes, el servicio de transporte, las bases de datos de buzones y los componentes de mensajería unificada.

En Exchange 2013, el rol servidor Buzón de correo interactúa directamente con Active Directory, el servidor de acceso de clientes y los clientes de Microsoft Outlook en el siguiente proceso:

  - El servidor Buzón de correo usa LDAP para obtener acceso a la información de la configuración del destinatario, del servidor y de la organización desde Active Directory.

  - El servidor de acceso de cliente envía solicitudes de los clientes al servidor de buzones de correo y devuelve datos del mismo a los clientes. El servidor de acceso de clientes también tiene acceso a los archivos de la libreta de direcciones en línea (OAB) en el servidor de buzones de correo mediante el uso compartido de archivos de NetBIOS. El servidor de acceso de clientes envía mensajes, datos de disponibilidad, configuraciones de perfil de cliente y los datos OAB entre el cliente y el servidor de buzones de correo.

  - Los clientes de Outlook dentro del firewall, acceden al servidor Acceso de clientes para enviar y recuperar mensajes. Los clientes de Outlook que están fuera del firewall pueden tener acceso al servidor de acceso de clientes mediante Outlook Anywhere (que utiliza el RPC sobre el componente proxy HTTP).

  - Se puede acceder a los buzones de correo de las carpetas públicas a través de RPC por HTTP, independientemente de si el cliente está fuera o dentro del firewall.

  - El PC con permisos de solo administrador recupera la información de la topología de Active Directory desde el servicio de topología de Microsoft Exchange Active Directory. También recupera información de directivas de direcciones de correo electrónico y de listas de direcciones.

  - El servidor de acceso de cliente utiliza LDAP o la interfaz del proveedor de servicio de nombres (NSPI) para conectar con el servidor de Active Directory y recuperar la información de Active Directory del usuario.

**Arquitectura e interacción del servidor de acceso de clientes y buzón de correo**

![Interacción de los servidores de acceso de cliente y de buzones de correo](images/JJ150491.d14577bf-14f9-40fa-bd49-a92932eb003a(EXCHG.150).gif "Interacción de los servidores de acceso de cliente y de buzones de correo")

Para obtener más información, consulte la sección "Cambios en la arquitectura de Exchange 2013" en [Novedades en Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

## Nuevas características de buzón de correo

La lista siguiente describe brevemente algunas novedades y características mejoradas en el rol de buzón de Exchange 2013:

  - Evolución del grupo de disponibilidad de bases de datos de Exchange 2010 (DAG):
    
      - El código de registro de transacciones se ha refactorizado para errores rápidos con un punto de comprobación más profundo en las copias de bases de datos pasivas.
    
      - Para ser compatibles con la resiliencia mejorada del sitio, los servidores pueden estar en ubicaciones diferentes.

  - Exchange 2013 hospeda ahora algunos componentes de acceso de cliente, los componentes de transporte y los de mensajería unificada.

  - El almacén de Exchange se ha rescrito en código administrado para mejorar el rendimiento en reducción y fiabilidad de E/S adicional.

  - Cada base de datos de Exchange 2013 ahora se ejecuta en sus propio proceso.

  - Búsqueda inteligente ha remplazado la infraestructura de búsqueda en varios buzones de correo de Exchange 2010.

## Proteger los servidores de buzones

De forma predeterminada, la comunicación por HTTP, Microsoft Exchange ActiveSync, POP3 e IMAP4 entre los servidores de buzones y otros roles de servidores de Exchange, controladores de dominio y servidores de catálogo global está cifrada. Además, debe asegurarse de que los servidores de buzones no sean accesibles por Internet.

## Más información

[Mensajería unificada](unified-messaging-exchange-2013-help.md)

[Flujo de correo](mail-flow-exchange-2013-help.md)

[Alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-exchange-2013-help.md)

[Directiva de mensajería y conformidad](messaging-policy-and-compliance-exchange-2013-help.md)

[Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

[Administrar bases de datos de buzones en Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)

[Directiva de mensajería y conformidad](messaging-policy-and-compliance-exchange-2013-help.md)

[Destinatarios](recipients-exchange-2013-help.md)

[Colaboración](collaboration-exchange-2013-help.md)

