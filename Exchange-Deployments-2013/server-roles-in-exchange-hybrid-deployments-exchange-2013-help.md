---
title: 'Roles de servidor en implementaciones híbridas de Exchange: Exchange 2013 Help'
TOCTitle: Roles de servidor en implementaciones híbridas de Exchange
ms:assetid: 7a7eaf17-d2b0-4d62-90a2-45a0d2faca54
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659051(v=EXCHG.150)
ms:contentKeyID: 49895004
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Roles de servidor en implementaciones híbridas de Exchange

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Puede configurar implementaciones híbridas basadas en Exchange 2013 y Exchange 2016. Los roles que se deben configurar para admitir una implementación híbrida dependen de la versión de Exchange que esté usando.

## Implementación híbrida de Exchange 2016

Al configurar una implementación híbrida en una organización de Exchange 2016, no es necesario instalar servidores de Exchange adicionales en la organización de Exchange existente. Los servidores de buzones de correo coordinan la comunicación entre su organización de Exchange 2016 existente y la organización de Exchange Online. Esta comunicación incluye las características de mensajería y transporte de mensajes entre las organizaciones local y de Exchange Online. Se recomienda la instalación de más de un servidor de Exchange en la organización local a fin de aumentar la confiabilidad y la disponibilidad de las características de implementación híbrida.

Exchange 2016 solo tiene un rol de servidor necesario, el rol de buzón. Además de hospedar los buzones de destinatarios locales, el rol de buzón realiza todas las funciones necesarias para admitir una implementación híbrida con Exchange Online. Esto incluye manejar todos los mensajes de correo seguros entre la organización local y la organización de Exchange Online, así como manejar las reglas de transporte, las políticas de registro en diario y la entrega de mensajes en los buzones de usuario en una implementación híbrida. El servidor de buzones de correo también maneja todas las características de conectividad de cliente y relación de organización, como el uso compartido de disponibilidad.

Obtenga más información sobre la planeación de capacidad de Exchange 2016 en la entrada sobre cómo [ajustar el tamaño de las implementaciones de Exchange 2016](http://go.microsoft.com/fwlink/p/?linkid=301990).

## Implementación híbrida de Exchange 2013

Al configurar una implementación híbrida en una organización de Exchange 2013, no es necesario instalar servidores Exchange adicionales en la organización de Exchange existente. El servidor Acceso de cliente y el servidor Buzón de correo coordinan la comunicación entre su organización Exchange 2013 existente y la organización Exchange Online. Esta comunicación incluye las características de mensajería y transporte de mensajes entre las organizaciones local y de Exchange Online. Se recomienda la instalación de más de un servidor Exchange en la organización local a fin de aumentar la fiabilidad y disponibilidad de las características de implementación híbrida.

A continuación, se muestra un descripción general rápida de los roles de servidor de Exchange 2013 en una implementación híbrida:

  - **Rol de servidor Acceso de clientes**   El rol de servidor Acceso de clientes proporciona la misma funcionalidad que normalmente suministran los servidores de acceso de clientes en una organización de Exchange 2013 con algunas incorporaciones obligatorias para admitir una implementación híbrida. El servidor Acceso de cliente también maneja todos los mensajes seguros enviados entre la organización local y la organización Exchange Online; asimismo maneja las reglas de transporte, las políticas de registro diario y el envío de mensajes a los buzones de usuario en una implementación híbrida. De manera predeterminada, se configura un conector de recepción dedicado en el servidor de acceso de cliente para admitir el transporte de correo híbrido seguro. Toda la conectividad de cliente, incluido el acceso de cliente de Outlook, Outlook Web App y Outlook Anywhere pasa por el rol de servidor Acceso de clientes. Las características de relación entre la organización local y la organización de Exchange, como el uso compartido de la disponibilidad, también son administradas por el rol de servidor de acceso de cliente.
    
    Para obtener más información, vea [Servidor de acceso de cliente](https://technet.microsoft.com/es-es/library/dd298114\(v=exchg.150\)).

  - **Función del servidor Buzón de correo**   Función del servidor Buzón de correo aloja los buzones destinatarios locales y se comunica con la organización Exchange Online por proxy mediante el servidor de acceso de cliente local. De manera predeterminada, se configura un conector de envío dedicado en el rol de servidor buzón de correo para admitir el transporte de correo híbrido seguro.
    
    Para obtener más información, vea [Servidor de buzones de correo](https://technet.microsoft.com/es-es/library/jj150491\(v=exchg.150\)).

Según la configuración de implementación híbrida que quiera, un servidor de Exchange 2013 requerirá la instalación de uno o ambos roles de servidor:

  - **Servidor Exchange único**   Si elige instalar un único servidor Exchange en su organización local, deberá instalar la función de servidor Acceso de cliente así como la función de servidor Buzón de correo en ese único servidor.

  - **Más de un servidor Exchange**   Si elige instalar más de un servidor Exchange en su organización local, podrá instalar los roles de servidor en servidores independientes en la organización local. Por ejemplo, puede instalar un servidor Exchange que tenga la funciones Acceso de cliente y Buzón de correo instaladas e instalar también otro servidor Exchange que solamente tenga instalada la función de servidor Acceso de cliente. Sin embargo, la mejor práctica y la configuración de servidor recomendada consiste en instalar los servidores de Acceso de cliente y de Buzón de correo en *todos* los servidores implementados en la organización local.

Para obtener más información acerca de la Exchange 2013 planificación de capacidad, vea [Descripción de varias configuraciones del rol del servidor en la planificación de capacidad](http://go.microsoft.com/fwlink/?linkid=266576).

## Funciones del servidor de Exchange en implementaciones híbridas

Los servidores Exchange le brindan varias funciones importantes a su organización local en una implementación híbrida:

  - **Federación**   Los servidores de Exchange permiten crear una confianza de federación para una organización local con Microsoft Federation Gateway. Microsoft Federation Gateway es un servicio gratuito basado en la nube ofrecido por Microsoft que funciona como agente de confianza entre la organización local y la organización de Office 365. La federación es un requisito para crear una relación de organización entre las organizaciones local y de Exchange Online.
    
    Para obtener más información, vea [Federación](https://technet.microsoft.com/es-es/library/dd335047\(v=exchg.150\)).

  - **Relaciones de organización**   Los servidores de Exchange 2013 con el rol de acceso de clientes y los servidores de Exchange 2016 con el rol de buzones de correo permiten la creación de relaciones de organización entre las organizaciones local y de Exchange Online. Las relaciones de organización se requieren para muchos otros servicios en una implementación híbrida, incluido el uso compartido de información de disponibilidad en el calendario, el seguimiento de mensajes y los movimientos de buzones entre las organizaciones local y de Exchange Online.
    
    Para obtener más información, vea [Uso compartido](https://technet.microsoft.com/es-es/library/dd638083\(v=exchg.150\)).

  - **Transporte de mensajes**   Los servidores Exchange con la función de servidor buzón y acceso de cliente son responsables del transporte de mensajes en una implementación híbrida. Cuando se usan conectores de envío y recepción, éstos actúan como los extremos de conexión para los mensajes externos entrantes y también entregan los mensajes salientes a Internet y a la organización Exchange Online.
    
    Para obtener más información, vea [Opciones de transporte en las implementaciones híbridas de Exchange](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Seguridad de transporte de mensajes**   Los servidores Exchange con la función de servidor acceso de cliente y buzón permiten garantizar la comunicación de mensajes entre las organizaciones local y de Exchange Online mediante la funcionalidad de seguridad de dominio de Exchange. Es posible aumentar la seguridad usando el cifrado y la autenticación de seguridad de capa de transporte mutua para las comunicaciones de mensajes.
    
    Obtenga más información en [Comprender la seguridad de dominio](http://go.microsoft.com/fwlink/p/?linkid=266581).

  - **Outlook en la web (también conocido como Outlook Web App en Exchange 2013)**   Los servidores de Exchange 2013 con el rol de acceso de cliente y los servidores de Exchange 2016 con el rol de buzones de correo admiten la configuración de un único extremo de dirección URL para conexiones externas a buzones locales y de Exchange Online. En los buzones locales, los servidores de Exchange se configuran para atender las solicitudes de Outlook en la web. En los buzones de correo de una organización de Exchange Online, los servidores de Exchange se configuran para mostrar automáticamente un vínculo al extremo de Outlook en la web en la organización de Exchange Online.
    
    Para obtener más información, vea [Outlook Web App](https://technet.microsoft.com/es-es/library/jj657718\(v=exchg.150\)).

