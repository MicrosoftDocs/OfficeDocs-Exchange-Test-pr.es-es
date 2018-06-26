---
title: 'No se puede determinar el nombre del sitio de Active Directory_InvalidADSite: Exchange 2013 Help'
TOCTitle: No se puede determinar el nombre del sitio de Active Directory_InvalidADSite
ms:assetid: ef96e077-08a0-4108-9f7d-0d61758abcd4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.invalidadsite(v=EXCHG.150)
ms:contentKeyID: 48268845
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No se puede determinar el nombre del sitio de Active Directory\_InvalidADSite

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque este servidor no parece que pertenezca a un sitio válido de un servicio de directorio de Active Directory®.

La instalación de Microsoft Exchange requiere que el servidor que se use en la instalación de Exchange 2007 pertenezca a un sitio válido de Active Directory.

Para resolver este problema, compruebe que el servidor local es miembro de un sitio válido de Active Directory y vuelva a ejecutar la instalación de Exchange Server 2007.

Puede usar la opción **/DsGetSite** de la herramienta de línea de comandos Nltest.exe para comprobar y mostrar la pertenencia al sitio. Para obtener más información, consulte "Nltest.exe: Visión general de NLTest" en "Colección de herramientas y configuración" de la *Guía de referencia técnica de Windows Server 2003* ([https://go.microsoft.com/fwlink/?LinkId=27734](https://go.microsoft.com/fwlink/?linkid=27734)) .

Para obtener más información acerca de cómo solucionar problemas de Active Directory, consulte "Solución de problemas en las operaciones de Active Directory" en *Windows Server 2003: Operaciones* (<https://go.microsoft.com/fwlink/?linkid=68099>).

