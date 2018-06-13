---
title: 'Servidores de transporte perimetral con implementaciones híbridas: Exchange 2013 Help'
TOCTitle: Servidores de transporte perimetral con implementaciones híbridas
ms:assetid: 166b1490-5c56-40df-a17b-e8bb36224fd9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh134662(v=EXCHG.150)
ms:contentKeyID: 48268935
ms.date: 04/26/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servidores de transporte perimetral con implementaciones híbridas

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2018-04-16_

El rol de servidor de transporte perimetral es un rol opcional que normalmente se implementa en un equipo ubicado en una red perimetral de la organización de Exchange. Está pensado para minimizar la superficie de ataque de la organización. Este rol se encarga de todo el flujo de correo de Internet, que proporciona la retransmisión de SMTP y servicios de host inteligente a los servidores de Exchange locales de la organización.

## Servidores de transporte perimetral en organizaciones con implementación híbrida basada en Exchange

Las organizaciones de Exchange 2016 que desean usar servidores de transporte perimetral tienen la opción de implementar servidores de transporte perimetral que ejecuten Exchange 2016 o versiones más recientes, Exchange 2013 o Exchange 2010. Use servidores de transporte perimetral si no desea exponer los servidores internos de Exchange directamente a Internet. Al implementar un servidor de transporte perimetral en una implementación híbrida, Exchange Online se conectará a su servidor de transporte perimetral mediante el servicio Exchange Online Protection para entregar los mensajes. El servidor de transporte perimetral entregará los mensajes al servidor de buzones de correo local de Exchange donde se encuentra el buzón del destinatario.


> [!IMPORTANT]
> No coloque servidores, servicios o dispositivos entre sus servidores de Exchange locales y Office 365 que procesen o modifiquen el tráfico SMTP. El flujo de correo seguro entre la organización de Exchange local y Office 365 depende de la información contenida en los mensajes enviados en la organización. Se admiten los firewalls que permiten el tráfico SMTP en el puerto TCP 25 sin ninguna modificación. Si un servidor, servicio o dispositivo procesa un mensaje enviado entre su organización de Exchange local y Office 365, esta información se elimina. Si esto ocurre, el mensaje ya no se considerará interno de la organización y estará sujeto al filtrado de correo no deseado, a las reglas de transporte y del diario y a otras directivas que podrían no aplicársele.




> [!IMPORTANT]
> Si dispone de otros servidores de transporte perimetral de Exchange en otras ubicaciones que no van a administrar transporte híbrido, no es necesario actualizarlos para que admitan una implementación híbrida. Sin embargo, si en el futuro desea que EOP se conecte a otros servidores de transporte perimetral para el transporte híbrido, estos deberán ejecutar Exchange 2016 o versiones más recientes, Exchange 2010 o Exchange&nbsp;2013.



## Agregar un servidor de transporte perimetral a una implementación híbrida

La implementación de un servidor de transporte perimetral en su organización local cuando configure una implementación híbrida es opcional. Cuando configure su implementación híbrida, el Asistente para configuración híbrida le permite seleccionar uno o más servidores internos de Exchange locales o seleccionar que uno o más servidores locales de transporte perimetral administren el transporte de correo híbrido en la organización de Exchange Online.

Al agregar un servidor de transporte perimetral a una implementación híbrida, este se comunica con EOP en nombre de los servidores internos de Exchange. El servidor de transporte perimetral actúa como retransmisión entre los servidores internos de Exchange y EOP para mensajes salientes de la organización local a la organización de Exchange Online. El servidor de transporte perimetral también actúa como retransmisión entre los servidores internos de Exchange para mensajes entrantes desde la organización de Exchange Online a la organización local. El servidor transporte perimetral controla toda la seguridad de conexiones que anteriormente controlaban los servidores internos de Exchange. La búsqueda de destinatarios, las directivas de cumplimiento y otras inspecciones de mensajes siguen realizándose en los servidores internos de Exchange.

Si agrega un servidor Transporte perimetral a su implementación híbrida, no tendrá que dirigir los correos enviados entre los usuarios locales y los destinatarios de Internet a través del mismo. Solo los mensajes enviados entre las organizaciones locales y las organizaciones de Exchange Online se enrutarán a través del servidor Transporte perimetral.

## Flujo de correo sin un servidor de transporte perimetral

El diagrama y el proceso a continuación describen la ruta que recorren los mensajes entre una organización local y Exchange Online cuando no se ha implementado un servidor de transporte perimetral:

1.  Los mensajes salientes desde la organización local a los destinatarios de la organización de Exchange Online se envían desde un buzón de correo en un servidor interno de Exchange.

2.  El servidor de Exchange envía el mensaje directamente a EOP.

3.  EOP entrega el mensaje a la organización de Exchange Online.

Los mensajes enviados desde la organización de Exchange Online a los destinatarios de la organización local siguen la ruta inversa.

**Flujo de correo en una implementación híbrida sin un servidor de transporte perimetral implementado**

![Flujo de correo electrónico híbrido sin un servidor de transporte perimetral](images/Hh134662.a95b4d1e-fd4a-4952-b891-22f84c9e71a3(EXCHG.150).png "Flujo de correo electrónico híbrido sin un servidor de transporte perimetral")

## Flujo de correo con un servidor de transporte perimetral

El siguiente proceso describe la ruta que siguen los mensajes entre la organización local y Exchange Online cuando hay un servidor de transporte perimetral implementado. Los mensajes de la organización local a los destinatarios de la organización de Exchange Online se envían desde el servidor interno de Exchange:

1.  Los mensajes desde la organización local a los destinatarios de la organización de Exchange Online se envían desde un buzón de correo en un servidor interno de Exchange.

2.  El servidor de Exchange envía el mensaje a un servidor de transporte perimetral que ejecuta una versión compatible de Exchange.

3.  El servidor de transporte perimetral envía el mensaje a EOP.

4.  EOP entrega el mensaje a la organización de Exchange Online.

Los mensajes enviados desde la organización de Exchange Online a los destinatarios de la organización local siguen la ruta inversa.

**Flujo de correo en una implementación híbrida con un servidor de transporte perimetral implementado**

![Flujo de correo electrónico híbrido con un servidor de transporte perimetral](images/Hh134662.821fe099-56f5-4501-8e1a-e184ba07a653(EXCHG.150).png "Flujo de correo electrónico híbrido con un servidor de transporte perimetral")

