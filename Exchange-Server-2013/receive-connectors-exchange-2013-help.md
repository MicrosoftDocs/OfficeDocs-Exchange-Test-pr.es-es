---
title: 'Conectores de recepción: Exchange 2013 Help'
TOCTitle: Conectores de recepción
ms:assetid: 17751a60-39fe-433f-84d2-bfc14ff4ba51
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996395(v=EXCHG.150)
ms:contentKeyID: 49895492
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectores de recepción

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Los conectores de recepción controlan el flujo de los mensajes entrantes a su organización de Exchange. Se configuran en equipos que ejecutan Microsoft Exchange Server 2013 con el servicio de transporte o en el servicio front-end en un servidor de acceso de clientes. Se pueden crear en el Centro de administración de Exchange (EAC) o en el Shell de administración de Exchange.

De forma predeterminada, los conectores de recepción necesarios para el flujo de correo interno se crean automáticamente cuando un servidor de acceso de clientes o un servidor de buzones de correo está instalado.

Los servidores de Exchange 2013 que ejecutan el servicio de transporte necesitan conectores de recepción para recibir mensajes de Internet, de clientes de correo electrónico y de otros servidores de correo electrónico. Los conectores de recepción controlan las conexiones entrantes a la organización de Exchange.

Cada conector de recepción escucha las conexiones entrantes que coinciden con la configuración del conector de recepción. Un conector de recepción escucha las conexiones que se reciben a través de una determinada dirección IP local y un determinado puerto, así como desde un intervalo de direcciones IP especificado. Puede crear un conector de recepción si desea controlar los servidores que reciben mensajes de una determinada dirección IP o de un determinado intervalo de direcciones IP, y si desea configurar propiedades de conectores especiales para los mensajes que se reciben de una dirección IP determinada; por ejemplo, que permitan mayor tamaño de mensajes o más destinatarios por mensaje. También puede analizar el conector de recepción con el parámetro *TlsCertificateName* del cmdlet **Set-ReceiveConnector**, que le permite especificar el certificado para usar con el conector.

Los conectores de recepción se aplican a un único servidor y determinan cómo ese servidor en concreto escucha las conexiones. Cuando se crea un conector de recepción en un servidor de buzones de correo que ejecute el servicio de transporte, el conector de recepción se almacena en Active Directory como objeto secundario del servidor en el que se creó.

Si necesita conectores de recepción adicionales para escenarios concretos, puede crearlos mediante la Consola de administración de Exchange (EAC) o el Shell de administración de Exchange. Cada conector de recepción debe usar una combinación exclusiva de enlaces de dirección IP, asignaciones de número de puerto e intervalos de dirección IP remotos desde los que se acepta el correo.

Para obtener información acerca de cómo crear un conector de recepción, consulte [Procedimientos con conectores de recepción](receive-connector-procedures-exchange-2013-help.md).

**Contenido**

Conectores de recepción predeterminados creados durante la instalación

Conectores de recepción predeterminados creados en un servidor de buzones de correo que ejecuta el servicio de transporte

Conectores de recepción predeterminados creados en un servidor de transporte front-end

Recibir los tipos de conectores

Grupos de permisos del conector de recepción

Recibir las especificaciones del tipo de conector

Permisos del conector de recepción

Configuración de la autenticación del conector de recepción

Nuevas funciones de conector de recepción en Exchange 2013

## Conectores de recepción predeterminados creados durante la instalación

Ciertos conectores de recepción se crean de forma predeterminada al instalar el rol de servidor Buzón de correo.

## Conectores de recepción predeterminados creados en un servidor de buzones de correo que ejecuta el servicio de transporte

Cuando se instala un servidor de buzones de correo que ejecute el servicio de transporte, se crean dos conectores de recepción. Para realizar una operación habitual, no se necesitan conectores de recepción adicionales y, en la mayoría de los casos, no es necesario modificar la configuración de los conectores de recepción predeterminados. Estos conectores son:

  - **Nombre de servidor\<predeterminado\>**   Acepta conexiones de servidores de buzones de correo que ejecuten el servicio de transporte desde servidores perimetrales.

  - **Nombre de servidor\<proxy de cliente\>**   Acepta conexiones de servidores front-end. Normalmente, los mensajes se envían a un servidor front-end por SMTP.

Cada conector tiene asignado un valor de *TransportRole*. Puede usarlo para determinar el rol del conector en el que se ejecuta. Puede ser muy útil en casos donde ejecute varios roles en un único servidor. En el caso de cada conector de recepción mencionado anteriormente, su valor de *TransportRole* es **HubTransport**.

Para ver los conectores de recepción predeterminados y sus valores de parámetros, puede usar el cmdlet [Get-ReceiveConnector](https://technet.microsoft.com/es-es/library/aa998618\(v=exchg.150\)).

## Conectores de recepción predeterminados creados en un servidor de transporte front-end

Durante la instalación, se crean tres conectores de recepción en el servidor de transporte de front-end o en el servidor de acceso de clientes. El conector de recepción de front-end predeterminado está configurado paras aceptar comunicaciones SMTP de todos los intervalos de dirección IP. Además, hay un conector de recepción que puede actuar como un proxy saliente para los mensajes enviados al servidor front-end desde servidores de buzones de correo. Finalmente, hay un conector de recepción seguro configurado para aceptar mensajes cifrados con Seguridad de la capa de transporte (TLS). Estos conectores son:

  - **Nombre de servidor \<de front-end predeterminado\>**   Acepta conexiones de remitentes de SMTP por el puerto 25. Es el punto de entrada de mensajería en su organización habitual.

  - **Nombre de servidor \<front-end de proxy saliente\>**   Acepta mensajes de un conector de envío en un servidor back-end, con proxy front-end habilitado.

  - **Nombre de servidor \<front-end de cliente\>**   Acepta conexiones seguras, con Seguridad de la capa de transporte (TLS) aplicada.

En una instalación típica, no se requieren conectores de recepción adicionales.

## Recibir los tipos de conectores

El tipo de determina la configuración de seguridad predeterminada para cada conector de recepción.

La configuración de seguridad para un conector de recepción especifica los permisos que se conceden a las sesiones que se conectan al conector de recepción y a los mecanismos de autenticación admitidos.

Cuando se usa el EAC para configurar un conector de recepción, la página del nuevo conector de recepción le solicita que seleccione el tipo de conector. En base a su selección, se establecen parámetros para confirmar la configuración elegida. Procedimientos específicos contienen más información sobre la configuración de tipo de conector de recepción. Ejemplos de estos procedimientos son [Creación de un conector de recepción para recibir correo electrónico de Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md) y [Crear un conector de recepción seguro para recibir correos electrónicos de un socio](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md).

## Grupos de permisos del conector de recepción

Un grupo de permisos es un conjunto predefinido de permisos que se concede a entidades de seguridad conocidas y se asigna a un conector de recepción. Entre las entidades de seguridad se incluye a usuarios, equipos y grupos de seguridad. El uso de los grupos de permisos simplifica la configuración de permisos en los conectores de recepción. La propiedad **PermissionGroups** define los grupos o los roles que pueden enviar mensajes al conector de recepción y los permisos que se asignan a aquellos grupos.

Los grupos de permisos incluyen *Anonymous*, *ExchangeUsers*, *ExchangeServers*, *ExchangeLegacyServers* y *Partner*.

## Recibir las especificaciones del tipo de conector

El tipo determina los grupos de permisos predeterminados que están asignados al conector de recepción y los mecanismos de autenticación predeterminado que están disponibles para la autenticación de la sesión. En la lista siguiente se describen los tipos disponibles:

1.  **Cliente**   Normalmente se usa para conectar a clientes que no usan Microsoft Office Outlook. Puede usar autenticación TLS.

2.  **Personalizado**   Normalmente se usa en un escenario entre bosques o en un escenario donde su organización recibe mensajes desde un agente de transferencia de mensajes SMTP.

3.  **Interno**   Usado para las comunicaciones entre los servidores que ejecuten el servicio de transporte o entre los servidores de buzones de correo que ejecuten el servicio de transporte y los agentes de transferencia de terceros.

4.  **Internet**   Usado para recibir correo SMTP de Internet.

5.  **Asociado**   Use este tipo si desea configurar comunicaciones seguras con un asociado.

Cada tipo es adecuado para un escenario de conexión específico. Seleccione el tipo cuya configuración predeterminada sea más adecuada para la configuración que desea. Puede modificar los permisos utilizando los cmdlets **Add-ADPermission** y **Remove-ADPermission**. Si desea obtener más información, consulte los siguientes temas:

  - [Add-ADPermission](https://technet.microsoft.com/es-es/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/es-es/library/aa996048\(v=exchg.150\))

## Permisos del conector de recepción

Los permisos de conectores de recepción se asignan a entidades de seguridad cuando se especifican los grupos de permisos para el conector. Cuando una entidad de seguridad establece una sesión con un conector de recepción, los permisos del conector de recepción determinan si la sesión se acepta y cómo se procesan los mensajes recibidos. Puede establecer permisos de conector de recepción mediante el EAC, o con el parámetro *PermissionGroups* con el cmdlet **Set-ReceiveConnector** en el Shell. Para modificar los permisos predeterminados de un conector de recepción, también puede usar el cmdlet **Add-ADPermission**.

[Permisos del conector de recepción](receive-connector-permissions-exchange-2013-help.md) contiene una tabla que indica las entidades de seguridad y los tipos de permisos en detalle.

## Configuración de la autenticación del conector de recepción

En el EAC, se usa la configuración de autenticación de un conector de recepción para especificar los mecanismos de autenticación admitidos por el servidor de transporte de Exchange 2013. En el Shell, se usa el parámetro *AuthMechanisms* para especificar los mecanismos de autenticación admitidos. Puede configurar más de un mecanismo de autenticación para un conector de recepción. Para obtener más información, consulte [Mecanismos de autenticación del conector de recepción](receive-connector-authentication-mechanisms-exchange-2013-help.md).

## Nuevas funciones de conector de recepción en Exchange 2013

Las siguientes características se añadieron a Exchange 2013:

  - Con el parámetro *TlsCertificateName* puede especificar el certificado de la entidad de certificación (CA) local que se va a usar para el correo seguro. Permite minimizar el riesgo de certificados fraudulentos.

  - El parámetro *TransportRole* designa el rol de servidor asociado a este conector. Se usa generalmente para especificar el rol de servidor cuando se hospedan varios roles de servidor en un sólo equipo.

Consulte [New-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125139\(v=exchg.150\)) para obtener más información acerca de estos parámetros y otros parámetros para los conectores de recepción.

