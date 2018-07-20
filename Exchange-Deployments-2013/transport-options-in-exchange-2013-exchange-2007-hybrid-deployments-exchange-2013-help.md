---
title: 'Opciones de transporte en las implementaciones híbridas de Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Opciones de transporte en las implementaciones híbridas de Exchange 2013/Exchange 2007
ms:assetid: 92d9e3ca-8d79-4872-9ff7-0067fcdbd434
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn151301(v=EXCHG.150)
ms:contentKeyID: 54652466
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Opciones de transporte en las implementaciones híbridas de Exchange 2013/Exchange 2007

Este tema se está redactando.  

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>Última modificación del tema:</strong>2016-12-09_

En las implementaciones híbridas, puede tener buzones que residen en su organización local de Exchange y también en una organización de Exchange Online. Un componente crítico para que estas dos organizaciones independientes aparezcan como una organización combinada a los usuarios y los mensajes que se intercambian es el transporte híbrido. Con el transporte híbrido, los mensajes que se envían entre los destinatarios de cualquiera de las organizaciones se autentican, se cifran y se transfieren mediante la Seguridad de la capa de transporte (TLS) y aparecen como "internos" a los componentes de Exchange tales como las reglas de transporte, el diario y las directivas de bloqueo de correo no deseado. El Asistente de configuración híbrida de Exchange 2013 configura automáticamente el transporte híbrido.

Para que la configuración de transporte híbrido funcione con el asistente para la configuración híbrida, el extremo SMTP local que acepta conexiones de Microsoft Exchange Online Protection (EOP), que controla el transporte de la organización de Exchange Online, debe ser un servidor de acceso de cliente de Exchange 2013, un servidor de transporte perimetral de Exchange 2013 o un servidor de transporte perimetral de Exchange Server 2010 Service Pack 3 (SP3).


> [!IMPORTANT]
> No puede haber otros hosts o servicios SMTP entre los servidores de acceso de cliente de Exchange&nbsp;2013 locales o los servidores de transporte perimetral de Exchange&nbsp;2013/Exchange 2010 SP3 y EOP. La información agregada a los mensajes que habilita las características del transporte híbrido se quita cuando pasan por un servidor que no es de Exchange 2013, servidores anteriores a Exchange 2010 SP3 o un host SMTP. Si tiene servidores de transporte perimetral de Exchange 2010 SP2 implementados en su organización y quiere usarlos en el transporte híbrido, deberá actualizarlos a Exchange 2010 SP3.



Los mensajes entrantes enviados a destinatarios de ambas organizaciones desde remitentes externos de Internet siguen una ruta de entrada común. Los mensajes salientes que se envían desde las organizaciones a destinatarios externos de Internet pueden seguir una ruta de salida común o se pueden enviar mediante rutas independientes.

Deberá elegir cómo enrutar el correo entrante y saliente cuando planifique y configure su implementación híbrida. La ruta que toman los mensajes entrantes y salientes cuando se envían a destinatarios y desde los destinatarios de las organizaciones local y de Exchange Online depende de lo siguiente:

  - ¿Desea enrutar el correo entrante de Internet tanto para los buzones de correo locales como de Exchange Online a través de Microsoft Office 365 y EOP, o a través de la organización local?
    
    Puede elegir enrutar el correo de Internet entrante para ambas organizaciones a través de la organización local, o bien a través de EOP y la organización de Exchange Online. La ruta que los mensajes entrantes toman hacia ambas organizaciones depende de que habilite el transporte de correo centralizado en su implementación híbrida.

  - ¿Desea enrutar el correo saliente para destinatarios externos de su organización de Exchange Online a través de la organización local (transporte de correo centralizado) o desea enrutarlo directamente a Internet?
    
    Conocido como transporte de correo centralizado, permite enrutar todo el correo de los buzones de correo de la organización de Exchange Online a través de la organización local antes de entregarlos a Internet. Este enfoque resulta útil en escenarios de compatibilidad donde los servidores locales deben procesar todo el correo entrante y saliente de Internet. De forma alternativa, puede configurar Exchange Online para entregar mensajes para destinatarios externos directamente a Internet.
    

    > [!NOTE]
    > El transporte de correo centralizado solo se recomienda para las organizaciones con necesidades de transporte específicas relacionadas con el cumplimiento. Nuestra recomendación para las organizaciones Exchange típicas es que no se habilite el transporte de correo centralizado.



  - ¿Desea implementar un servidor de transporte perimetral en su organización local?
    
    Si prefiere no exponer directamente en Internet los servidores de Exchange 2013 internos y unidos a un dominio, puede implementar servidores de transporte perimetral de Exchange 2013 o de Exchange 2010  SP3 en su red perimetral. Para obtener más información acerca de cómo agregar un servidor de transporte perimetral a la implementación híbrida, consulte [Servidores de transporte perimetral en las implementaciones híbridas de Exchange 2013/Exchange 2007](edge-transport-servers-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md).

Independientemente de cómo enrute mensajes desde y hacia Internet, todos los mensajes enviados entre las organizaciones local y de Exchange Online se envían usando el transporte seguro. Para obtener más información, consulte [Trusted communication](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md) más adelante en este tema.

Para obtener más información sobre cómo estas opciones afectan el enrutamiento de mensajes en su organización, consulte [Enrutamiento de transporte en las implementaciones híbridas de Exchange 2013/Exchange 2007](transport-routing-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md).

## Protección en línea de Exchange en implementaciones híbridas

EOP es un servicio en línea proporcionado por Microsoft usado por muchas empresas para proteger las organizaciones locales contra virus, correo no deseado, correos de suplantación de identidad (phishing) e infracciones de directivas. En Office 365, EOP se usa para proteger organizaciones de Exchange Online contra las mismas amenazas. Cuando se registra para Office 365, se crea automáticamente una empresa de EOP vinculada a su organización de Exchange Online.

Una empresa EOP contiene varios de los ajustes del transporte de correo que se pueden configurar para la organización de Exchange Online. Puede especificar qué dominios SMTP deben provenir de direcciones IP específicas, cuáles requieren un certificado de Capa de sockets seguros (SSL) y un TLS, cuáles pueden eludir cualquier directiva de cumplimiento y más. EOP es la puerta a su organización de Exchange Online. Todos los mensajes, independientemente de su origen, deben pasar a través de EOP antes de llegar a los buzones de correo de la organización de Exchange Online. Además, todos los mensajes enviados desde la organización de Exchange Online deben pasar por EOP antes de llegar a Internet.

Cuando configura una implementación híbrida con el Asistente para la configuración híbrida, todos los valores de transporte se configuran automáticamente en la organización local y en la empresa EOP incluida en la organización de Exchange Online. El Asistente para configuración híbrida configura todos los conectores de entrada y de salida y otras configuraciones de esta empresa EOP para proteger los mensajes enviados entre las organizaciones local y de Exchange Online, y enruta los mensajes al destino correcto. Si desea configurar los ajustes de transporte personalizados para su organización de Exchange Online, los deberá configurar también en esta empresa EOP.

## Comunicación de confianza

Para ayudar a proteger a los destinatarios de ambas organizaciones local y de Exchange Online, y para ayudar a garantizar que los mensajes enviados entre las organizaciones no sean interceptados y leídos, el transporte entre la organización local y EOP se configura para usar TLS forzoso. El transporte TLS usa los certificados de Capa de sockets seguros (SSL) proporcionados por una entidad de certificación (CA) de terceros. Los mensajes entre EOP y la organización de Exchange Online también usan TLS.Online organization also use TLS.

Al usar el transporte TLS forzado, los servidores de envío y recepción analizan el certificado configurado en el otro servidor. El nombre del sujeto o uno de los nombres alternativos del firmante (SAN) configurados en los certificados deben coincidir con el FQDN que un administrador haya especificado de manera explícita en el otro servidor. Por ejemplo, si EOP se configura para aceptar y proteger los mensajes enviados desde el FQDN de mail.contoso.com, el servidor local de acceso de cliente o de transporte perimetral debe tener un certificado SSL que incluya mail.contoso.com en el nombre del sujeto o SAN. Si no se cumple este requisito, EOP rechaza la conexión.


> [!NOTE]
> No es necesario que el FQDN usado coincida con el nombre de dominio de la dirección de correo electrónico de los destinatarios. El único requisito es que el FQDN del nombre del sujeto del certificado o SAN debe coincidir con el FQDN que los servidores de recepción o envío tengan configurados para aceptar.



Además de usar TLS, los mensajes entre las organizaciones se consideran "internos". Este enfoque permite que los mensajes pasen por alto la configuración de bloqueo de correo no deseado y otros servicios.

Obtenga más información sobre los certificados SSL y la seguridad de dominio en [Requisitos de certificados para implementaciones híbridas](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md) y en [Descripción de los certificados TLS](http://go.microsoft.com/fwlink/p/?linkid=187237).

