---
title: 'Opciones de transporte en las implementaciones híbridas de Exchange: Exchange 2013 Help'
TOCTitle: Opciones de transporte en las implementaciones híbridas de Exchange
ms:assetid: da605a78-5429-4de8-8b04-bc4c45a41ba1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659055(v=EXCHG.150)
ms:contentKeyID: 49895009
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Opciones de transporte en las implementaciones híbridas de Exchange

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

En las implementaciones híbridas, puede tener buzones que residen en su organización local de Exchange y también en una organización de Exchange Online. Un componente crítico para que estas dos organizaciones independientes aparezcan como una organización combinada para los usuarios y los mensajes que se intercambian es el transporte híbrido. Con el transporte híbrido, los mensajes que se envían entre los destinatarios de cualquiera de las organizaciones se autentican, se cifran y se transfieren mediante la Seguridad de la capa de transporte (TLS) y aparecen como "internos" para los componentes de Exchange tales como las reglas de transporte, el registro en diario y las directivas de bloqueo de correo no deseado. El Asistente para configuración híbrida configura automáticamente el transporte híbrido.

Para que la configuración de transporte híbrida funcione con el Asistente para configuración híbrida, el extremo SMTP local que acepta las conexiones procedentes de Exchange Online debe ser un servidor de buzones de correo (Exchange 2016 o versiones posteriores), un servidor de acceso de cliente (Exchange 2013), un servidor de transporte de concentradores (Exchange 2010 o versiones anteriores) o un servidor de transporte perimetral (Exchange 2010 o versiones posteriores).


> [!IMPORTANT]
> No coloque servidores, servicios o dispositivos entre sus servidores de Exchange locales y Office 365 que procesen o modifiquen el tráfico SMTP. El flujo de correo seguro entre la organización de Exchange local y Office 365 depende de la información contenida en los mensajes enviados en la organización. Se admiten los firewalls que permiten el tráfico SMTP en el puerto TCP 25 sin ninguna modificación. Si un servidor, servicio o dispositivo procesa un mensaje enviado entre su organización de Exchange local y Office 365, esta información se elimina. Si esto ocurre, el mensaje ya no se considerará interno de la organización y estará sujeto al filtrado de correo no deseado, a las reglas de transporte y del diario y a otras directivas que podrían no aplicársele.



Los mensajes entrantes enviados a destinatarios en ambas organizaciones desde remitentes de Internet siguen una ruta entrante común. Los mensajes salientes que se envían desde las organizaciones a destinatarios externos de Internet, pueden seguir una ruta saliente común o se pueden enviar mediante rutas independientes.

Deberá elegir cómo enrutar el correo entrante y saliente cuando planifique y configure su implementación híbrida. La ruta que toman los mensajes entrantes y salientes cuando se envían a destinatarios y desde los destinatarios de las organizaciones local y de Exchange Online depende de lo siguiente:

  - ¿Desea enrutar el correo entrante de Internet tanto de los buzones locales como de los buzones de Exchange Online a través de Exchange Online o de la organización local?
    
    La ruta que siguen los mensajes entrantes para ambas organizaciones depende de diversos factores, como el lugar donde se encuentra la mayoría de los buzones, la decisión de proteger la organización local mediante la exploración de malware y de correo electrónico no deseado de Office 365, el lugar donde se configura la infraestructura de cumplimiento de normas, etcétera.

  - ¿Desea enrutar el correo saliente para destinatarios externos de su organización de Exchange Online a través de la organización local (transporte de correo centralizado) o desea enrutarlo directamente a Internet?
    
    Con el transporte de correo centralizado, puede enrutar todo el correo de los buzones de correo de la organización de Exchange Online a través de la organización local antes de entregarlos a Internet. Este enfoque resulta útil en escenarios de cumplimiento donde los servidores locales deben procesar todo el correo entrante y saliente de Internet. De forma alternativa, puede configurar Exchange Online para entregar mensajes para destinatarios externos directamente a Internet.
    

    > [!NOTE]
    > El transporte de correo centralizado solo se recomienda para las organizaciones con necesidades de transporte específicas relacionadas con el cumplimiento. Nuestra recomendación para organizaciones típicas de Exchange es no habilitar el transporte de correo centralizado, ya que puede aumentar considerablemente la cantidad de mensajes procesados por los servidores locales, aumentar el ancho de banda usado y crear una dependencia innecesaria en los servidores locales.



  - ¿Desea implementar un servidor de transporte perimetral en su organización local?
    
    Si no quiere exponer directamente en Internet los servidores de Exchange internos unidos a dominios, puede implementar servidores de transporte perimetral en la red perimetral. Para obtener más información sobre cómo agregar un servidor de transporte perimetral a la implementación híbrida, consulte [Servidores de transporte perimetral con implementaciones híbridas](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md).

Independientemente de cómo enrute mensajes desde y hacia Internet, todos los mensajes enviados entre las organizaciones local y de Exchange Online se envían usando el transporte seguro. Para obtener más información, consulte Comunicación de confianza más adelante en este tema.

Para obtener más información sobre cómo estas opciones afectan el enrutamiento de mensajes en su organización, consulte [Enrutamiento de transporte en las implementaciones híbridas de Exchange](transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md).

## Exchange Online Protection en implementaciones híbridas

EOP es un servicio en línea proporcionado por Microsoft usado por muchas empresas para proteger las organizaciones locales contra virus, correo no deseado, correos de suplantación de identidad (phishing) e infracciones de directivas. En Office 365, EOP se usa para proteger organizaciones de Exchange Online contra las mismas amenazas. Cuando se registra para Office 365, se crea automáticamente una empresa de EOP qué está vinculada con su organización de Exchange Online.

Una empresa EOP contiene varios de los ajustes del transporte de correo que se pueden configurar para la organización de Exchange Online. Puede especificar qué dominios SMTP provienen de direcciones IP específicas, requieren un certificado TLS y de Capa de sockets seguros (SSL), eluden los filtros contra correo no deseada o las directivas de cumplimiento, etcétera. EOP es la puerta a su organización de Exchange Online. Todos los mensajes, independientemente de su origen, deben pasar mediante EOP antes de llegar a los buzones de correo de la organización de Exchange Online. Además, todos los mensajes enviados a la organización de Exchange Online deben pasar por EOP antes de llegar a Internet.

Cuando configura una implementación híbrida con el asistente para la configuración híbrida, todos los valores de transporte se configuran automáticamente en la organización local y en la empresa EOP para su organización de Exchange Online. El asistente para configuración híbrida configura todos los conectores entrantes y salientes, y otras configuraciones en esta empresa EOP para proteger los mensajes enviados entre las organizaciones local y de Exchange Online, y enruta los mensajes al destino correcto. Si desea configurar los ajustes de transporte personalizados para su organización de Exchange Online, los deberá configurar también en esta empresa EOP.

## Comunicación de confianza

Para ayudar a proteger a los destinatarios de las organizaciones local y de Exchange Online, y para ayudar a garantizar que los mensajes enviados entre las organizaciones no sean interceptados y leídos, el transporte entre la organización local y EOP se configura para usar TLS forzada. El transporte de correo seguro usa los certificados TLS/SSL proporcionados por una entidad de certificación (CA) de terceros. Los mensajes entre EOP y la organización de Exchange Online también usan TLS.

Al usar el transporte TLS forzado, los servidores de envío y recepción analizan el certificado configurado en el otro servidor. El nombre de firmante o uno de los nombres alternativos del firmante (SAN) configurados en los certificados deben coincidir con el FQDN que un administrador haya especificado de manera explícita en el otro servidor. Por ejemplo, si EOP se configura para aceptar y proteger los mensajes enviados desde el FQDN de mail.contoso.com, el servidor local de acceso de cliente o de transporte perimetral debe tener un certificado SSL que incluya mail.contoso.com en el nombre del sujeto o SAN. Si no se cumple este requisito, EOP rechaza la conexión.


> [!NOTE]
> No es necesario que el FQDN usado coincida con el nombre de dominio de la dirección de correo electrónico de los destinatarios. El único requisito es que el FQDN del nombre de sujeto del certificado o SAN debe coincidir con el FQDN que los servidores de recepción o envío están configurados para aceptar.



Además de usar TLS, los mensajes entre las organizaciones se consideran "internos". Este enfoque permite que los mensajes pasen por alto la configuración de bloqueo de correo no deseado y otros servicios.

Obtenga más información sobre los certificados SSL y la seguridad de dominio en [Requisitos de certificados para implementaciones híbridas](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md) y en [Conocer los certificados TLS](http://go.microsoft.com/fwlink/p/?linkid=187237).

