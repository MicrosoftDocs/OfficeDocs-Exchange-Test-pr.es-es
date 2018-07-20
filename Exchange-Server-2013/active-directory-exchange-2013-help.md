---
title: 'Active Directory: Exchange 2013 Help'
TOCTitle: Active Directory
ms:assetid: 8e8464df-2d1d-4d68-82de-b0c158c549c3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123715(v=EXCHG.150)
ms:contentKeyID: 49895768
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Microsoft Exchange Server 2013 utiliza Active Directory para almacenar y compartir la información de directorios con Windows. El diseño de bosque de Active Directory para Exchange 2013 es similar al de Exchange Server 2010, exceptuando algunos detalles que se mencionan a continuación.

## Active Directory, controlador

El controlador de Active Directory es el principal componente de Microsoft Exchange que permite a los servicios Exchange crear, modificar, eliminar y consultar datos de Servicios de dominio de Active Directory (AD DS). En xExchange 2013, todos los accesos a Active Directory se realizan a través del mismo controlador de Active Directory. Anteriormente, en Exchange 2010, DSAccess proporcionaba servicios de búsqueda de directorios para componentes como SMTP, el Agente de transferencia de mensajes (MTA) y el almacén de Exchange.

El controlador de Active Directory también usa la topología de Microsoft ExchangeActive Directory (MSExchangeADTopology), que permite que el controlador de Active Directory use datos de topología del Acceso del servicio de directorio (DSAccess). Estos datos incluyen la lista de controladores de dominio disponibles y los servidores de catálogo global disponibles para gestionar las solicitudes de Exchange. Para más información acerca del controlador de Active Directory, consulte [Active Directory Replication Services](https://go.microsoft.com/fwlink/p/?linkid=110942).

## Cambios en el esquema de Active Directory

Exchange 2013 añade atributos nuevos al esquema de servicio de dominios de Active Directory y también modifica otras clases y atributos existentes. Para obtener más información acerca de los cambios en Active Directory al instalar Exchange 2013, consulte [Cambios en el esquema de Active Directory de Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

## Más información

Para obtener más información acerca de cómo Exchange 2013 almacena y recupera la información en Active Directory para que pueda planear su acceso al mismo, consulte [Acceso a Active Directory](access-to-active-directory-exchange-2013-help.md).

Para obtener más información acerca del diseño de bosque de Active Directory, consulte [Planeamiento de una implementación de los Servicios de dominio de Active Directory](https://go.microsoft.com/fwlink/p/?linkid=264957).

Para obtener más información acerca de los equipos que ejecutan Windows en un dominio de Active Directory y de cómo implementar Exchange 2013 en un dominio con un espacio de nombres distinto, consulte [Escenarios de espacios de nombres distintos](disjoint-namespace-scenarios-exchange-2013-help.md).

