---
title: 'Configuración de faxes entrantes: Exchange 2013 Help'
TOCTitle: Configuración de faxes entrantes
ms:assetid: 5d3cae58-1690-424d-9bef-011911d0b608
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633468(v=EXCHG.150)
ms:contentKeyID: 52061863
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración de faxes entrantes

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

La Mensajería unificada de Microsoft Exchange se basa en las soluciones certificadas de asociados de fax para obtener funcionalidades de fax mejoradas, como fax saliente o enrutamiento de fax. La configuración predeterminada de los servidores Exchange no permite que los faxes entrantes se entreguen a un usuario que está habilitado para la mensajería unificada. En su lugar, el servidor Exchange redirige las llamadas de fax entrantes a una solución certificada de asociados de fax. El servidor de asociados de fax recibe los datos del fax y, a continuación, los envía al buzón de correo del usuario en un mensaje de correo electrónico con el fax incluido como archivo .tif adjunto.

Para obtener más información sobre asociados de fax, consulte [Microsoft PinPoint para asociados de fax](https://go.microsoft.com/fwlink/?linkid=190238)

## Implementación y configuración de fax

La Mensajería unificada reenvía las llamadas de fax entrantes a una solución de asociado de fax dedicado que, luego, relaciona la llamada de fax con el remitente del fax y lo recibe en nombre del usuario habilitado para Mensajería unificada. Sin embargo, para que los usuarios habilitados para mensajería unificada puedan recibir mensajes de fax en sus buzones, debe habilitar primero los faxes entrantes y establecer el URI del asociado de fax en la directiva de buzones de correo de mensajería unificada que está vinculada a los usuarios habilitados para mensajería unificada. Puede autorizar o rechazar faxes entrantes en los planes de marcado de mensajería unificada, las directivas de buzones de mensajería unificada y en el buzón de correo de un usuario habilitado para mensajería unificada. Para obtener más información, consulte los siguientes temas:

  - [Permitir a los usuarios en el mismo plan de marcado para recibir faxes](allow-users-in-the-same-dial-plan-to-receive-faxes-exchange-2013-help.md)

  - [Impedir que los usuarios en el mismo plan de marcado de recibir faxes](prevent-users-in-the-same-dial-plan-from-receiving-faxes-exchange-2013-help.md)

  - [Habilitar el envío de faxes para un grupo de usuarios](enable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [Deshabilitar el envío de faxes para un grupo de usuarios](disable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [Habilitar un usuario recibir faxes](enable-a-user-to-receive-faxes-exchange-2013-help.md)

  - [Evitar que un usuario reciba faxes](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)

## Paso 1: Implementar la mensajería unificada

Antes de que pueda configurar el fax en su organización local o híbrida, debe implementar correctamente los servidores de acceso de clientes y de buzones de correo, y configurar las puertas de enlace de voz sobre IP (VoIP) compatibles. Para obtener información acerca de cómo implementar la mensajería unificada, consulte [Implementar mensajería unificada de Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md). Para más información sobre cómo implementar puertas de enlace VoIP y centrales de conmutación (PBX), consulte [Conectar la mensajería unificada para su sistema telefónico](connect-um-to-your-telephone-system-exchange-2013-help.md).


> [!IMPORTANT]
> El envío y la recepción de faxes mediante T.38 o G.711 no se admite en entornos en los que la mensajería unificada y MicrosoftOffice Communications Server 2007 R2 o Microsoft Lync Server están integrados.



## Paso 2: Configurar servidores de asociados de fax

A continuación, debe habilitar los faxes entrantes y configurar el URI del asociado de fax en cada directiva de buzón de correo de mensajería unificada que necesite en su organización. Para implementar correctamente los faxes entrantes, debe integrar una solución certificada de asociado de fax con la Mensajería unificada de Exchange. Para obtener información detallada, consulte [Asesor de fax para la mensajería unificada de Exchange](fax-advisor-for-exchange-um-exchange-2013-help.md). Para obtener una lista de los asociados de fax, consulte [Microsoft PinPoint para asociados de fax](https://go.microsoft.com/fwlink/?linkid=190238)


> [!NOTE]
> Dado que el servidor del asociado de fax es externo a su organización, deben configurarse los puertos de firewall para admitir los puertos del protocolo T.38 que permiten el envío de faxes por una red basada en IP. De manera predeterminada, el protocolo T.38 utiliza el puerto TCP 6004. También puede utilizar el puerto UDP 6044, pero esto lo definirá el fabricante del hardware. Los puertos de firewall deben configurarse para admitir datos del fax que utilicen los puertos TCP o UDP definidos por el fabricante.



## Paso 3: Permitir el envío de faxes en mensajería unificada

Para que los usuarios puedan recibir faxes con la mensajería unificada, hay tres componentes que tienen que estar configurados correctamente.

  - Planes de marcado de MU

  - Directivas de buzón de MU

  - Buzones de MU

El envío de faxes se puede habilitar o deshabilitar en los planes de marcado y las directivas de buzón de mensajería unificada, o en el buzón de correo del usuario habilitado para mensajería unificada. Las directivas de buzones de mensajería unificada pueden habilitarse o deshabilitarse para el envío de faxes usando tanto el Centro de administración de Exchange (EAC) como el Shell de administración de Exchange. Para habilitar y deshabilitar planes de marcado y usuarios habilitados para mensajería unificada individuales debe utilizar el Shell de administración de Exchange. La siguiente tabla muestra las opciones disponibles y los cmdlets y parámetros que se utilizan para activar y desactivar el envío de faxes.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente de mensajería unificada</th>
<th>¿Habilitar y deshabilitar usando el EAC?</th>
<th>Ejemplo de Shell para permitir el envío de faxes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Plan de marcado</p></td>
<td><p>No</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -faxenabled $true</code></p></td>
</tr>
<tr class="even">
<td><p>Directiva de buzón de mensajería unificada</p></td>
<td><p>Sí</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyPolicy -AllowFax $true</code></p></td>
</tr>
<tr class="odd">
<td><p>Usuario habilitado para mensajería unificada</p></td>
<td><p>No</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -faxenabled $true</code></p></td>
</tr>
</tbody>
</table>


De forma predeterminada, aunque el plan de marcado de mensajería unificada y el buzón del usuario admitan la entrada de faxes, antes se deben habilitar los faxes de entrada en la directiva de buzón de mensajería unificada asignada al usuario habilitado para mensajería unificada y, a continuación, especificar el URI del servidor del asociado de fax.

Para permitir que los usuarios habilitados para MU reciban faxes, debe realizar lo siguiente:

  - Compruebe que cada plan de marcado de MU permita que los usuarios asociados con dicho plan reciban faxes. De forma predeterminada, todos los usuarios que estén asociados con un plan de marcado pueden recibir faxes. Para que los usuarios con mensajería unificada habilitada reciban mensajes de fax en sus buzones, cada puerta de enlace VoIP o IP PBX debe estar configurada para aceptar llamadas de fax entrantes. También debe permitir que los usuarios vinculados con el plan de marcado reciban mensajes de fax. Para obtener más información sobre cómo habilitar usuarios vinculados al plan de marcado para que reciban faxes o para impedir que lo hagan, consulte [Habilitar un usuario recibir faxes](enable-a-user-to-receive-faxes-exchange-2013-help.md).
    

    > [!NOTE]
    > Si impide que se reciban mensajes de fax en un plan de marcado, ninguno de los usuarios asociados con dicho plan podrá recibir faxes, incluso si configura las propiedades de un usuario concreto para que pueda recibirlos. La habilitación o deshabilitación de los faxes en un plan de marcado de MU tiene prioridad sobre la configuración de un usuario individual habilitado para MU.



  - Configure la directiva de buzón de MU asociada con el usuario habilitado para MU. La directiva de buzón de MU debe estar configurada para permitir la funcionalidad de fax entrante, incluidos el URI del asociado de fax y el nombre del servidor de asociado de fax. El parámetro *FaxServerURI* debe tener el formato siguiente: sip:\<*URI del servidor de fax*\>:\<*puerto*\>;\<*transporte*\>, donde "URI del servidor de fax" es un nombre de dominio completo (FQDN) o una dirección IP del servidor del asociado de fax. "Puerto" es el puerto por el cual el servidor de fax recibe las llamadas de fax entrantes y "transporte" es el protocolo de transporte que se usa para el fax entrante (UDP, TCP o TLS). Por ejemplo, puede configurar una directiva de buzón de mensajería unificada para recibir un fax del modo que se describe a continuación.
    
        Set-UMMailboxPolicy MyUMMailboxPolicy -AllowFax $true -FaxServerURI "sip:faxserver.abc.com:5060;transport=tcp"

  - Para obtener información detallada, consulte [El asociado del conjunto de servidor de fax URI para permitir el envío de faxes](set-the-partner-fax-server-uri-to-allow-faxing-exchange-2013-help.md).
    

    > [!WARNING]
    > Aunque puede incluir varias entradas en el formato para el <EM>FaxServerURI</EM> separándolas con un punto y coma, sólo se utilizará una entrada. Este parámetro permite utilizar sólo una entrada y, si añade varias entradas, no podrá equilibrar la carga de las solicitudes de fax.



  - Compruebe que el buzón habilitado para mensajería unificada puede recibir mensajes de fax. De forma predeterminada, todos los usuarios que estén asociados con un plan de marcado pueden recibir faxes. No obstante, puede suceder que un usuario no pueda recibir faxes porque esta opción se ha deshabilitado en su buzón. Para obtener más información acerca de cómo permitir que un usuario habilitado para mensajería unificada reciba mensajes de fax, consulte [Habilitar un usuario recibir faxes](enable-a-user-to-receive-faxes-exchange-2013-help.md).
    
    Puede impedir que un determinado usuario asociado con el plan de marcado reciba mensajes de fax. Para ello, configure las propiedades del usuario utilizando el cmdlet **Set-UMMailbox** en el Shell. También puede utilizar el cmdlet **Set-UMMailboxPolicy** para evitar que varios usuarios reciban mensajes de fax. Para obtener más información acerca de cómo evitar que uno o varios usuarios reciban mensajes de fax, consulte [Evitar que un usuario reciba faxes](prevent-a-user-from-receiving-faxes-exchange-2013-help.md).

## Paso 4: Configurar la autenticación

Además de configurar los planes de marcado de mensajería unificada, las directivas de buzón de mensajería unificada y los usuarios habilitados para mensajería unificada, debe configurar la autenticación entre los servidores Exchange y el servidor del asociado de fax. Los servidores Exchange deben poder autenticar el origen de los mensajes que supuestamente procedan del servidor del asociado de fax. El servidor Exchange no procesará ningún mensaje sin autenticar aunque especifique que procede del servidor del asociado de fax.

Para autenticar la conexión del servidor del asociado de fax con los servidores Exchange, puede utilizar:

  - TLS Mutua

  - La validación del Id. de remitente

  - Un conector de recepción dedicado

Un conector de recepción debería ser suficiente para autenticar los servidores de asociados de fax en su organización. El conector de recepción permitirá que los servidores de Exchange traten todo el tráfico procedente del servidor de asociado de fax como autenticado.

El conector de recepción se configurará en el servidor Exchange que use el servidor del asociado de fax para enviar los mensajes de fax SMTP, y debe configurarse con los valores siguientes:

  - *AuthMechanism: ExternalAuthoritative*

  - *PermissionGroups: ExchangeServers, PartnersFax*

  - *RemoteIPRanges: {the fax server's IP address}*

  - *RequireTLS: False*

  - *EnableAuthGSSAPI: False*

  - *LiveCredentialEnabled: False*

Para obtener información detallada, consulte [Conectores](connectors-exchange-2013-help.md).

Si el servidor del asociado de fax envía tráfico de red a un servidor Exchange por una red pública, por ejemplo, un servidor del asociado de fax hospedado en la nube, es buena idea autenticar el servidor del asociado de fax comprobando el identificador del remitente. Este tipo de autenticación garantiza que la dirección IP de la que procede el mensaje de fax está autorizada para enviar mensajes de correo en nombre del dominio del asociado de fax cuya procedencia especifica el mensaje. El DNS se utiliza para almacenar los registros del identificador del remitente (o los registros del marco de directivas de remitente (SPF)), y los asociados de fax deben publicar sus registros de SPF en la zona de búsqueda directa DNS. Exchange validará las direcciones IP mediante consultas DNS. Sin embargo, el agente del identificador del remitente debe ejecutarse en un servidor de buzones de correo para que se pueda realizar la consulta DNS.

También puede utilizar TLS para cifrar el tráfico de red o TLS mutua para que haya cifrado y autenticación entre el servidor del asociado de fax y los servidores Exchange.

