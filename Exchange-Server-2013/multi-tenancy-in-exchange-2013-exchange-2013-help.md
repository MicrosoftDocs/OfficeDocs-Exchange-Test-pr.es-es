---
title: 'Arquitectura multiempresa en Exchange 2013: Exchange 2013 Help'
TOCTitle: Arquitectura multiempresa en Exchange 2013
ms:assetid: df09257d-dd98-4f59-b830-1818cedda15c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ862352(v=EXCHG.150)
ms:contentKeyID: 50556897
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Arquitectura multiempresa en Exchange 2013

 

_**Se aplica a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Una implementación de Exchange 2013 con varios inquilinos (hospedada) se define como aquella en la que la organización de Exchange se configura para hospedar varias organizaciones o unidades de negocio discretas (inquilinos) que, por lo general, no comparten correo electrónico, datos, usuarios, listas globales de direcciones (LGD) ni cualquier otro objeto que se use habitualmente en Exchange. Este uso compartido del hardware, del software y de los recursos (siempre que se mantenga una separación lógica entre los inquilinos) permite a las organizaciones aprovecharse de la sencillez de una implementación de Exchange estándar mientras se proporcionan los servicios y la funcionalidad de varios inquilinos para satisfacer las necesidades de hospedaje.

## Arquitectura multiempresa en organizaciones de Exchange 2013

En Exchange 2013, se ofrece soporte continuo mediante el hospedaje de una instalación estándar y local de Exchange similar al enfoque utilizado en Exchange 2010 Service Pack 2 (SP2). Se ha suspendido el conmutador de modo `/hosting` y se ha enfatizado el uso de las directivas de libretas de direcciones (ABP) junto con las soluciones de administración de hospedaje y las herramientas de automatización suministradas por fabricantes de software independiente (ISV) aprobados. Estas soluciones se basan en un marco de directrices y prácticas de configuración aprobadas por Microsoft y ofrecerán a las organizaciones de Exchange una manera más sencilla y sólida de suministrar servicios y características de alojamiento.

Exchange 2013 admite la arquitectura multiempresa y aprovecha los siguientes componentes y características principales:

  - **Active Directory**   En lugar de tener contenedores de *ExchangeOrganization* independientes para cada unidad de negocio en una organización de Exchange multiempresa, se admite la arquitectura multiempresa de Exchange 2013 mediante el uso de un solo contenedor de Active Directory de *ExchangeOrganization*. Esto permite contar con una estructura de Active Directory más sencilla y elimina los posibles problemas de permisos relacionados con Active Directory.
    
    Para obtener más información acerca de los cambios de Active Directory en Exchange 2013, consulte [Active Directory](active-directory-exchange-2013-help.md).

  - **Directivas de libretas de direcciones (ABP)**   Incluidas por primera vez en Exchange 2010 SP2, las directivas de libretas de direcciones se usan en Exchange 2013 para controlar el acceso de los usuarios a una lista de direcciones, a una lista global de direcciones (LGD) o a libretas de direcciones sin conexión (OAB) en la organización de Exchange. Las directivas de libretas de direcciones agrupan los diversos objetos de Active Directory en un único objeto virtual que se puede asignar a usuarios individuales, o bien se puede crear una agrupación lógica de estos recursos junto con una estructura organizativa multiempresa. La funcionalidad de las directivas de libretas de direcciones en Exchange 2013 es similar a la de Exchange 2010 SP2.
    
    Para obtener más información acerca de las directivas de libretas de direcciones en Exchange 2013, consulte [Directivas de la libreta de direcciones](address-book-policies-exchange-2013-help.md).

  - **Soluciones de administración de hospedaje**   Los administradores que usan Exchange 2013 para proporcionar una solución de Exchange hospedada podrán beneficiarse del uso de un enfoque de administración de hospedaje personalizado. Debido a ciertas limitaciones del Centro de administración de Exchange (EAC), Microsoft colabora con otros proveedores para ayudarles a desarrollar soluciones de automatización y de panel de control que cumplan las directrices y el marco de trabajo aprobado para las organizaciones de Exchange 2013 hospedadas. Se recomienda que las organizaciones que configuren una solución de Exchange hospedada aprovechen estas herramientas para administrar sus organizaciones hospedadas siempre que la situación lo requiera.
    
    Para obtener más información acerca de las soluciones de administración hospedada, incluidos los proveedores de soluciones validados, consulte [Instrucciones y soluciones multiempresa y de hospedaje en Exchange Server 2013](https://go.microsoft.com/fwlink/?linkid=275036)

