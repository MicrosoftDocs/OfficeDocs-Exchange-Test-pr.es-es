---
title: 'Configuración de un dispositivo de Exchange ActiveSync con implementaciones híbridas de Exchange: Exchange 2013 Help'
TOCTitle: Configuración de un dispositivo de Exchange ActiveSync con implementaciones híbridas de Exchange
ms:assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn931281(v=EXCHG.150)
ms:contentKeyID: 64966459
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración de un dispositivo de Exchange ActiveSync con implementaciones híbridas de Exchange

 

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2016-01-27_

Los dispositivos de Exchange ActiveSync ahora se reconfiguran automáticamente al mover un buzón desde una organización local de Exchange a Office 365. Exchange ActiveSync encontrará la nueva ubicación del buzón en Office 365 y actualizará la configuración para poder comunicarse directamente con Office 365. El dispositivo de Exchange ActiveSync no intentará ponerse en contacto con el servidor local de Exchange después de redirigirse correctamente a Office 365. Con algunas excepciones (de las que encontrará más información a continuación), el usuario ya no necesita configurar manualmente su dispositivo para que el correo siga funcionando.

Si desea mover un buzón a Office 365, vea [Mover buzones de correo entre organizaciones locales y de Exchange Online en implementaciones híbridas](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md).

Para obtener más información acerca de implementaciones híbridas, vea [Implementaciones híbridas de Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

Para usar el redireccionamiento automático, los servidores locales deben ejecutar las versiones más recientes de Exchange 2010, Exchange 2013, Exchange 2016 o versiones posteriores. También debe haber utilizado el [Asistente de configuración híbrida](hybrid-configuration-wizard-exchange-2013-help.md) para configurar su implementación híbrida. La funcionalidad de redireccionamiento de Exchange ActiveSync usa la dirección URL de destino de Outlook en la web establecida en el objeto de relación de organización. Este objeto se configura al ejecutar el Asistente de configuración híbrida.

Si su organización cumple los requisitos mencionados anteriormente, los dispositivos móviles deben redirigirse automáticamente a Office 365 cuando se mueva el buzón de un usuario, sin ninguna configuración adicional. Para obtener la mejor experiencia, asegúrese de que los dispositivos móviles de los usuarios usan las últimas versiones de sus sistemas operativos y de sus clientes de correo electrónico. Algunos dispositivos móviles, como los que ejecutan el sistema operativo Android, pueden tardar más de lo esperado en redirigirse. Además, es posible que algunos dispositivos no interpreten correctamente las instrucciones de redirección de Exchange ActiveSync 451 que envía Exchange. Para dichos dispositivos, los usuarios deberán seguir reconfigurando su cuenta de correo electrónica de forma manual o volver a crearla en el dispositivo. Si tiene cualquier pregunta acerca de si un dispositivo es compatible con la redirección de Exchange ActiveSync 451, póngase en contacto con el fabricante del dispositivo.

La redirección automática de Exchange ActiveSync no es compatible en los siguientes escenarios:

  - Desplazamiento de buzones de Office 365 a una organización local de Exchange.

  - Desplazamiento de buzones entre organizaciones locales de Exchange.

  - Desplazamiento de buzones de los servidores de Exchange 2007 a Office 365.

