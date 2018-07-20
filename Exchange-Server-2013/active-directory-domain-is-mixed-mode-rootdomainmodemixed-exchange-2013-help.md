---
title: 'Dominio de Active Directory es mixto mode_RootDomainModeMixed: Exchange 2013 Help'
TOCTitle: Dominio de Active Directory es mixto mode_RootDomainModeMixed
ms:assetid: 9f60096e-3eaa-40d8-bde5-13ada5855702
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.rootdomainmodemixed(v=EXCHG.150)
ms:contentKeyID: 48268488
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dominio de Active Directory es mixto mode\_RootDomainModeMixed

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque existe un dominio de Active Directory que no está establecido en modo nativo de Microsoft Windows®°2000 Server o mejor.

Con la instalación de Exchange 2007 se crearán grupos de seguridad universales que solamente pueden existir en dominios en modo nativo (o mejor) de Windows 2000 Server.

Para solucionar este problema, siga estos pasos para elevar el nivel funcional del dominio como mínimo al nivel nativo de Windows 2000 Server y, a continuación, vuelva a ejecutar la instalación de Exchange 2007.

Para elevar el nivel funcional del dominio

1.  Abra Dominios y confianzas de Active Directory.

2.  En el árbol de la consola, haga clic con el botón secundario en el dominio del que quiera elevar la funcionalidad y, a continuación, haga clic en **Elevar el nivel funcional del dominio**.

3.  En **Seleccione un nivel funcional del dominio disponible**, use uno de los siguientes procedimientos:
    
      - Para elevar el nivel funcional del dominio a Windows 2000 Server nativo, haga clic en **Windows 2000 nativo** y, a continuación, en **Elevar**.
    
      - Para elevar el nivel funcional del dominio a Windows Server® 2003, haga clic en **Windows Server 2003** y, a continuación, en **Elevar**.


> [!WARNING]
> <BR>En caso de que tenga o vaya a tener controladores de dominio que ejecuten Windows NT®&nbsp;4.0 y versiones anteriores, no eleve el nivel funcional del dominio a Windows&nbsp;2000 Server nativo. Una vez establecido el nivel funcional del dominio en Windows&nbsp;2000 Server nativo, no podrá cambiarse a Windows&nbsp;2000 Server mixto.<BR>En caso de que tenga o vaya a tener controladores de dominio que ejecuten Windows NT&nbsp;4.0 y versiones anteriores o Windows&nbsp;2000 Server, no eleve el nivel funcional del dominio a Windows Server&nbsp;2003. Una vez establecido el nivel funcional del dominio en Windows Server&nbsp;2003, no podrá cambiarse a Windows&nbsp;2000 Server mixto o Windows&nbsp;2000 Server nativo.


