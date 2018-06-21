---
title: 'Servidores de transporte perimetral en las implementaciones híbridas de Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Servidores de transporte perimetral en las implementaciones híbridas de Exchange 2013/Exchange 2007
ms:assetid: 4e4d7c19-78b8-44bb-bdff-3ea97ea59a5d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn151300(v=EXCHG.150)
ms:contentKeyID: 54652465
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servidores de transporte perimetral en las implementaciones híbridas de Exchange 2013/Exchange 2007

Este tema se está redactando.  

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>Última modificación del tema:</strong>2016-12-09_

Los servidores de transporte perimetral de Microsoft Exchange se implementan en la red perimetral local de una organización. Son equipos no unidos a dominios que administran el flujo de correo de Internet y funcionan como retransmisión SMTP y host inteligente para los servidores de Exchange de la red interna.

Las organizaciones de Exchange 2013 que deseen usar los servidores de transporte perimetral tienen la opción de implementar servidores de transporte perimetral de Exchange Server de 2013 o servidores de transporte perimetral de Exchange 2010 con Service Pack 3 (SP3) para Exchange 2010. Use servidores de transporte perimetral si no desea exponer los servidores de acceso de cliente o de buzones de correo de Exchange 2013 internos directamente a Internet.

Obtenga más información acerca del rol de servidor de transporte perimetral de Exchange 2013 en [Servidores de transporte perimetral](https://technet.microsoft.com/es-es/library/bb124701\(v=exchg.150\)).

Obtenga más información sobre el rol de servidor Transporte perimetral de Exchange 2010 en [Información general del rol de servidor Transporte perimetral](http://go.microsoft.com/fwlink/p/?linkid=183473).

## Servidores de transporte perimetral en organizaciones de implementación híbrida basadas en Exchange 2013

Los mensajes que se enrutan entre las organizaciones locales y las organizaciones de Exchange Online en una implementación híbrida requieren que el servicio Protección en línea de Microsoft Exchange (EOP) se conecte directamente, en nombre de Exchange Online, a los servidores de transporte perimetral que ejecutan Exchange 2013 o Exchange 2010 SP3.


> [!IMPORTANT]
> Si dispone de servidores de transporte perimetral de Exchange 2010 en otras ubicaciones que no van a administrar transporte híbrido, no es necesario actualizarlos a Exchange 2010&nbsp;SP3. Sin embargo, si en el futuro desea que EOP se conecte a otros servidores de transporte perimetral para el transporte híbrido, deberá actualizarlos con Exchange 2010&nbsp;SP3 o actualizarlos a servidores de transporte perimetral de Exchange&nbsp;2013.



## Agregar un servidor de transporte perimetral a una implementación híbrida

La implementación de un servidor de transporte perimetral en su organización local cuando configure una implementación híbrida es opcional. Cuando configure su implementación híbrida, el Asistente de configuración híbrida le permite seleccionar uno o más servidores de acceso de cliente y de buzones para el transporte de correo híbrido o seleccionar que uno o más servidores locales de transporte perimetral administren el transporte de correo híbrido en la organización de Exchange Online.

Al agregar un servidor de transporte perimetral a una implementación híbrida, éste se comunica con EOP en nombre de los servidores internos de buzones de correo y de acceso de cliente de Exchange 2013. El servidor de transporte perimetral actúa como retransmisión entre el servidor de buzones de correo local y el EOP para los mensajes salientes desde la organización local hacia Exchange Online. El servidor de transporte perimetral actúa como retransmisión entre el servidor de acceso de cliente local para los mensajes entrantes desde la organización de Exchange Online hacia la organización local. El servidor de transporte perimetral controla toda la seguridad de conexiones que anteriormente controlaban los servidores de acceso de cliente. La búsqueda de destinatarios, las directivas de cumplimiento y otras inspecciones de mensajes continúan realizándose en los servidores de acceso de cliente.

## Flujo de correo sin un servidor de transporte perimetral

El diagrama y el proceso a continuación describen la ruta que recorren los mensajes entre una organización local y Exchange Online cuando no se ha implementado un servidor de transporte perimetral:

1.  Los mensajes salientes de la organización local se envían a los destinatarios de la organización de Exchange Online desde un servidor de buzones de correo de Exchange 2007 a un servidor de transporte de concentradores de Exchange 2007.

2.  El servidor de transporte de concentradores de Exchange 2007 envía el mensaje al servidor de buzones de correo de Exchange 2013.

3.  El servidor de buzones de correo de Exchange 2013 envía el mensaje directamente a la compañía de EOP de Exchange Online.

4.  EOP entrega el mensaje a la organización de Exchange Online. En este ejemplo, los roles de servidor Buzón de correo y Acceso de clientes se instalan en el mismo servidor Exchange 2013.

Los mensajes enviados desde la organización de Exchange Online a los destinatarios de la organización local siguen la ruta inversa.

**Flujo de correo en una implementación híbrida sin un servidor de transporte perimetral implementado**

![Organización local sin servidor perimetral](images/Dn151300.e7206c51-b61c-41e3-a446-9270f131fbaa(EXCHG.150).png "Organización local sin servidor perimetral")

## Flujo de correo con un servidor de transporte perimetral

El siguiente proceso describe la ruta que siguen los mensajes entre la organización local y Exchange Online cuando hay un servidor de transporte perimetral instalado. Los mensajes de la organización local a los destinatarios de la organización de Exchange Online se envían desde los servidores de buzones de correo de Exchange 2007:

1.  Los mensajes salientes de la organización local se envían a los destinatarios de la organización de Exchange Online desde un servidor de buzones de correo de Exchange 2007 a un servidor de transporte de concentradores de Exchange 2007.

2.  El servidor de transporte de concentradores de Exchange 2007 envía el mensaje al servidor de buzones de correo de Exchange 2013.

3.  El servidor de buzones de correo de Exchange 2013 envía el mensaje a un servidor de transporte perimetral de Exchange 2013 o Exchange 2010 SP3.

4.  El servidor de transporte perimetral envía el mensaje a la empresa de Exchange Online EOP.

5.  EOP entrega el mensaje a la organización de Exchange Online. En este ejemplo, los roles de servidor Buzón de correo y Acceso de clientes se instalan en el mismo servidor Exchange 2013.

Los mensajes enviados desde la organización de Exchange Online a los destinatarios de la organización local siguen la ruta inversa.

**Flujo de correo en una implementación híbrida con un servidor de transporte perimetral de Exchange 2013 o 2010 SP3 implementado**

![Organización local con servidor perimetral](images/Dn151300.91bf5390-c4d7-4aa9-b911-0c1c559d4365(EXCHG.150).png "Organización local con servidor perimetral")

