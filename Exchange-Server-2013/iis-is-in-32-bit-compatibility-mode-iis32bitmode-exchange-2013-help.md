---
title: 'IIS está en modo_IIS32BitMode de compatibilidad con 32 bits Exchange 2013 Help | Microsoft Docs'
TOCTitle: IIS está en modo de compatibilidad con 32 bits_IIS32BitMode
ms:assetid: 742dfc32-353c-46a2-830e-68aed6a68ce0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.iis32bitmode(v=EXCHG.150)
ms:contentKeyID: 48268284
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS está en modo de compatibilidad con 32 bits\_IIS32BitMode

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque ISS (Microsoft Internet Information Service) se está ejecutando en modo de 32 bits en este equipo de 64 bits.

Exchange 2007 requiere que IIS esté en modo de 64 bits cuando se ejecuta en un equipo de 64 bits.

Para solucionar este problema, cambie IIS al modo de 64 bits y vuelva a ejecutar el programa de instalación de Microsoft Exchange.

Para cambiar IIS al modo de 64 bits

1.  Abra un símbolo del sistema.

2.  Escriba lo siguiente:
    
    **cscript c:\\inetpub\\adminscripts\\adsutil.vbs SET /w3svc/AppPools/Enable32BitAppOnWin64 False**

3.  Presione Entrar

