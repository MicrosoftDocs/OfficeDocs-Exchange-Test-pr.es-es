---
title: 'Usar servidor transporte perimetral de Exchange 2010 o 2007 en Exchange 2013 | Microsoft Docs'
TOCTitle: Usar un servidor de transporte perimetral de Exchange 2010 o 2007 en Exchange 2013
ms:assetid: ce99b4bd-868c-4767-9009-e22c17ac0ac7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150569(v=EXCHG.150)
ms:contentKeyID: 48268679
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Usar un servidor de transporte perimetral de Exchange 2010 o 2007 en Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

El servidor de transporte perimetral está disponible en Microsoft Exchange Server 2013 Service Pack 1 (SP1). No obstante, puede seguir utilizando los servidores de transporte perimetral existentes de Exchange Server 2007 o Exchange Server 2010 que haya implementado en su red perimetral. De manera alternativa, puede instalar un servidor de transporte perimetral nuevo de Exchange 2007 o Exchange 2010 en la red perimetral para una organización nueva o actualizada de Exchange 2013.

A continuación se detalla la información más importante:

  - Un servidor de transporte perimetral de Exchange 2007 o Exchange 2010 espera conectarse a un servidor de transporte de concentradores. En Exchange 2013, el servicio de transporte existe en el servidor Buzón de correo. Por lo tanto, el flujo de correo de Internet se produce entre el servicio de transporte en el servidor de buzones y el servidor de transporte perimetral, que omite correctamente el servidor Acceso de cliente de Exchange 2013.

  - Puede suscribir un servidor de transporte perimetral de Exchange 2007 o Exchange 2010 a un sitio de Active Directory que contenga únicamente servidores de Exchange 2013. Puede importar el archivo de suscripción perimetral y ejecutar EdgeSync en un servidor de buzones independiente de Exchange 2013, o bien en un servidor en el que el servidor de buzones y el servidor de acceso de cliente estén instalados en el mismo equipo. No puede importar el archivo de suscripción perimetral ni ejecutar EdgeSync en un servidor de acceso de cliente de Exchange 2013 independiente.

  - Los procedimientos para implementar un servidor de transporte perimetral nuevo de Exchange 2007 o Exchange 2010 en una organización de Exchange 2013 son prácticamente los mismos que para versiones anteriores de Exchange. Sin embargo, los procedimientos que se ejecuten en el servidor de transporte de concentradores se realizarán en el servidor de buzones en Exchange 2013. Los procedimientos son:
    
      - [Configurar el flujo de correo de Internet por medio de un servidor de transporte perimetral suscrito](https://go.microsoft.com/fwlink/p/?linkid=275859)
    
      - [Configurar el flujo de correo entre un servidor Transporte perimetral y servidores Transporte de concentradores sin usar EdgeSync](https://go.microsoft.com/fwlink/p/?linkid=276661)

