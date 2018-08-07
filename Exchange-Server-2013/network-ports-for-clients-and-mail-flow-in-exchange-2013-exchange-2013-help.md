---
title: 'Puertos red para clientes y flujo correo en Exchange 2013: Exchange 2013 Help'
TOCTitle: Puertos de red para los clientes y flujo de correo en Exchange 2013
ms:assetid: fec09455-e99e-42eb-8b32-1ddc08d9a19e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb331973(v=EXCHG.150)
ms:contentKeyID: 64141274
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Puertos de red para los clientes y flujo de correo en Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En este tema se proporciona información sobre los puertos de red que usa MicrosoftExchange Server 2013 para la comunicación con clientes de correo electrónico, servidores de correo de Internet y otros servicios externos a la organización de Exchange local. Antes de entrar en el tema, debe comprender las siguientes reglas básicas:

  - No se admite la restricción o modificación del tráfico de red entre los servidores internos de Exchange, los servidores internos de Exchange o los servidores internos de Lync o Skype Empresarial ni los servidores internos de Exchange y los controladores de dominio internos de Active Directory en ningún tipo de topología. Si tiene firewalls o dispositivos de red que puedan restringir o modificar este tipo de tráfico de red, debe configurar reglas que permitan una comunicación libre y sin restricciones entre estos servidores (reglas que permitan tráfico de red entrante y saliente en cualquier puerto, incluidos los puertos RPC aleatorios, así como cualquier protocolo que nunca altere los bits en la conexión).

  - Los servidores de transporte perimetral casi siempre se encuentran en una red perimetral, por lo que se espera que usted restrinja el tráfico de red entre el servidor de transporte perimetral e Internet, y entre el servidor de transporte perimetral y su organización de Exchange interna. En este tema se describen estos puertos de red.

  - Se espera que restrinja el tráfico de red entre los clientes externos y servicios y la organización interna de Exchange. También está bien si decide restringir el tráfico de red entre clientes internos y servidores internos de Exchange. En este tema se describen estos puertos de red.

**Contenido**

Puertos de red necesarios para clientes y servicios

Puertos de red necesarios para el flujo de correo (sin servidores de transporte perimetral)

Puertos de red necesarios para el flujo de correo con servidores de transporte perimetral

Puertos de red necesarios para las implementaciones híbridas

Puertos de red necesarios para la mensajería unificada

## Puertos de red necesarios para clientes y servicios

En el diagrama y la tabla siguientes se describen los puertos de red necesarios para que los clientes de correo electrónico tengan acceso a buzones y otros servicios en la organización de Exchange.

**Notas:** 

  - El destino de estos clientes y servicios es un servidor de acceso de cliente. Podría tratarse de un servidor de acceso de cliente independiente o un servidor de acceso de cliente y un servidor de buzones de correo instalados en el mismo equipo.

  - Aunque el diagrama muestra los clientes y servicios de Internet, los conceptos son los mismos para los clientes internos (por ejemplo, los clientes de un bosque de cuentas que tienen acceso a los servidores de Exchange en un bosque de recursos). De forma similar, esta tabla no tiene una columna de origen porque el origen podría ser cualquier ubicación externa a la organización de Exchange (por ejemplo, Internet o un bosque de cuentas).

  - Los servidores de transporte perimetral no tienen nada que ver con el tráfico de red que está asociado con estos clientes y servicios.

![Puertos de red necesarios para clientes y servicios](images/Bb331973.f5ba3439-f001-43c8-848e-0e3fd0fce931(EXCHG.150).png "Puertos de red necesarios para clientes y servicios")


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Finalidad</th>
<th>Puertos</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Los siguientes clientes y servicios usan las conexiones web cifradas:</p>
<ul>
<li><p>Servicio Detección automática</p></li>
<li><p>Exchange ActiveSync</p></li>
<li><p>Servicios Web Exchange (EWS)</p></li>
<li><p>Distribución de libreta de direcciones sin conexión</p></li>
<li><p>Outlook en cualquier lugar (RPC sobre HTTP)</p></li>
<li><p>Outlook MAPI sobre HTTP</p></li>
<li><p>Outlook Web App</p></li>
</ul></td>
<td><p>443/TCP (HTTPS)</p></td>
<td><p>Para obtener más información acerca de estos clientes y servicios, vea los siguientes temas:</p>
<ul>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Servicio Detección automática</a></p></li>
<li><p><a href="exchange-activesync-exchange-2013-help.md">Exchange ActiveSync</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/?linkid=529544">Referencia EWS para Exchange</a></p></li>
<li><p><a href="offline-address-books-exchange-2013-help.md">Libretas de direcciones sin conexión</a></p></li>
<li><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook en cualquier lugar</a></p></li>
<li><p><a href="mapi-over-http-exchange-2013-help.md">MAPI sobre HTTP</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Novedades de Outlook Web App en Exchange 2013</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Los siguientes clientes y servicios usan conexiones web no cifradas:</p>
<ul>
<li><p>Publicación del calendario de Internet</p></li>
<li><p>Outlook Web App (redireccionamiento a 443/TCP)</p></li>
<li><p>Detección automática (reserva cuando 443/TCP no está disponible)</p></li>
</ul></td>
<td><p>80/TCP (HTTP)</p></td>
<td><p>Siempre que sea posible, se recomienda usar conexiones web cifradas en 443/TCP para ayudar a proteger los datos y las credenciales. Sin embargo, tal vez descubra que algunos servicios deben configurarse para usar conexiones web sin cifrar en 80/TCP con el servidor de acceso de cliente.</p>
<p>Para obtener más información acerca de estos clientes y servicios, vea los siguientes temas:</p>
<ul>
<li><p><a href="enable-internet-calendar-publishing-exchange-2013-help.md">Habilitar la publicación del calendario de Internet</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Novedades de Outlook Web App en Exchange 2013</a></p></li>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Servicio Detección automática</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>IMAP4, clientes</p></td>
<td><p>143/TCP (IMAP), 993/TCP (IMAP seguro)</p></td>
<td><p>IMAP4 está deshabilitado de forma predeterminada. Para obtener más información, vea <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">POP3 e IMAP4 en Exchange Server 2013</a>.</p>
<p>El servicio IMAP4 en las conexiones de proxy de servidor de acceso de cliente con el servicio backend IMAP4 en un servidor de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>POP3, clientes</p></td>
<td><p>110/TCP (POP3), 995/TCP (POP3 seguro)</p></td>
<td><p>POP3 está deshabilitado de forma predeterminada. Para obtener más información, vea <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">POP3 e IMAP4 en Exchange Server 2013</a>.</p>
<p>El servicio POP3 en las conexiones de proxy de servidor de acceso de cliente con el servicio backend POP3 en un servidor de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>Clientes SMTP (autenticados)</p></td>
<td><p>587/TCP (SMTP autenticado)</p></td>
<td><p>El conector de recepción predeterminado denominado &quot;<em>&lt;Nombre del servidor&gt;</em> de front-end de cliente&quot; escucha los envíos del cliente SMTP autenticados en el puerto 587 del servidor de acceso de cliente.</p>
<p><strong>Nota:</strong></p>
<p>Si tiene clientes de correo que pueden enviar correo SMTP autenticado únicamente en el puerto 25, puede modificar el valor de los enlaces del adaptador de red de este conector de recepción para escuchar también los envíos de correo SMTP autenticado en el puerto 25.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Puertos de red necesarios para el flujo de correo

La forma en que el correo se entrega hacia y desde la organización de Exchange depende de la topología de Exchange. El factor más importante es si cuenta con un servidor de transporte perimetral implementado en la red perimetral.

## Puertos de red necesarios para el flujo de correo (sin servidores de transporte perimetral)

En el diagrama y la tabla siguientes se describen los puertos de red necesarios para el flujo de correo en una organización de Exchange que solo tiene servidores Acceso de clientes y Buzón de correo. Aunque el diagrama muestra servidores Acceso de clientes y Buzón de correo por separado, los conceptos son los mismos, independientemente de si ambos servidores, Acceso de clientes y Buzón de correo, están instalados en el mismo equipo o en equipos distintos.

![Puertos de red necesarios para el flujo de correo (sin servidores de transporte perimetral)](images/Bb331973.af54dfd3-fe6b-4b6e-bb8e-b00df94a0be0(EXCHG.150).png "Puertos de red necesarios para el flujo de correo (sin servidores de transporte perimetral)")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Finalidad</th>
<th>Puertos</th>
<th>Origen</th>
<th>Destino</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Correo entrante</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet (cualquiera)</p></td>
<td><p>Servidor de acceso de cliente</p></td>
<td><p>El conector de recepción predeterminado denominado &quot;Front-end predeterminado <em>&lt;Client Access server name&gt;</em>&quot; en el servidor Acceso de clientes escucha el correo SMTP entrante anónimo en el puerto 25.</p>
<p>El correo se retransmite desde el servidor de acceso de cliente a un servidor de buzones de correo mediante el conector de envío interno de la organización implícito e invisible que enruta automáticamente el correo entre los servidores de Exchange de la misma organización.</p></td>
</tr>
<tr class="even">
<td><p>Correo saliente</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidor de buzones de correo</p></td>
<td><p>Internet (cualquiera)</p></td>
<td><p>De forma predeterminada, Exchange no crea ningún conector de envío que permita enviar correo a Internet. Debe crear manualmente los conectores de envío. Para obtener más información, vea <a href="send-connectors-exchange-2013-help.md">Conectores de envío</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Correo saliente (si se enruta a través del servidor de acceso de cliente)</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidor de acceso de cliente</p></td>
<td><p>Internet (cualquiera)</p></td>
<td><p>El correo saliente se enruta a través de un servidor Acceso de clientes solo cuando se configura un conector de envío con <strong>Proxy mediante el servidor Acceso de clientes</strong> en el centro de administración de Exchange o <code>-FrontEndProxyEnabled $true</code> en Shell de administración de Exchange.</p>
<p>En este caso, el conector de recepción predeterminado denominado &quot;f<em>&lt;Nombre del servidor de acceso de cliente&gt;</em> de front-end de proxy saliente&quot; en el servidor de acceso de cliente escucha el correo saliente desde el servidor de buzones de correo. Para obtener más información, vea <a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">Crear un conector de envío para correo electrónico enviado a Internet</a>.</p></td>
</tr>
<tr class="even">
<td><p>DNS para la resolución de nombres del siguiente salto del correo (no mostrado)</p></td>
<td><p>53/UDP,53/TCP (DNS)</p></td>
<td><p>Servidor de Exchange accesible desde Internet (servidores Acceso de clientes o Buzón de correo)</p></td>
<td><p>Servidor DNS</p></td>
<td><p>Consulte la sección Resolución de nombres.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Puertos de red necesarios para el flujo de correo con servidores de transporte perimetral

Un servidor de transporte perimetral suscrito que está instalado en la red perimetral básicamente elimina el flujo de correo SMTP a través del servidor de acceso de cliente. En particular:

  - El correo saliente desde la organización de Exchange nunca fluye a través de un servidor de acceso de cliente. El correo siempre fluye desde un servidor de buzones de correo en el sitio suscrito de Active Directory hacia el servidor de transporte perimetral (independientemente de la versión de Exchange en el servidor de transporte perimetral).

  - El correo entrante nunca fluye a través de un servidor de acceso de cliente independiente. El correo siempre fluye desde el servidor de transporte perimetral hacia un servidor de buzones de correo en el sitio suscrito de Active Directory. Si el servidor de buzones de correo y el servidor de acceso de cliente están instalados en el mismo equipo, el correo de un servidor de transporte perimetral de Exchange 2013 llega primero al equipo en el servicio de transporte de front-end (el rol del servidor de acceso de cliente) antes de fluir al servicio de transporte (el rol del servidor buzones). Los servidores de transporte perimetral de Exchange 2007 o Exchange 2010 siempre entregan correo directamente al servicio de transporte incluso cuando el servidor de buzones de correo y el servidor de acceso de cliente estén instalados en el mismo equipo.

Para más información, vea [Flujo de correo](mail-flow-exchange-2013-help.md).

En la tabla y el diagrama siguientes se describen los puertos de red necesarios para el flujo de correo en las organizaciones de Exchange que tienen servidores de transporte perimetral. A menos que se indique lo contrario, los conceptos son los mismos si el servidor de acceso de cliente y el servidor de buzones de correo se instalan en el mismo equipo o en equipos distintos.

![Puertos de red necesarios para el flujo de correo con servidores de transporte perimetral](images/Bb331973.110c79b3-dbd9-4cb5-bba1-02048363ee1c(EXCHG.150).png "Puertos de red necesarios para el flujo de correo con servidores de transporte perimetral")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Finalidad</th>
<th>Puertos</th>
<th>Origen</th>
<th>Destino</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Correo entrante: Internet a servidor de transporte perimetral</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet (cualquiera)</p></td>
<td><p>Servidor de transporte perimetral</p></td>
<td><p>El conector de recepción predeterminado denominado &quot;Conector de recepción interno predeterminado <em>&lt;Nombre del servidor de transporte perimetral&gt;</em>&quot; en el servidor de transporte perimetral escucha el correo SMTP anónimo en el puerto 25.</p></td>
</tr>
<tr class="even">
<td><p>Correo entrante: servidor de transporte perimetral en organización de Exchange interna</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidor de transporte perimetral</p></td>
<td><p>Servidores de buzones de correo en el sitio suscrito de Active Directory</p></td>
<td><p>El conector de envío predeterminado denominado &quot;EdgeSync - Entrante para <em>&lt;nombre del sitio de Active Directory&gt;</em>&quot; retransmite correo entrante en el puerto 25 para cualquier servidor de buzones de correo en el sitio suscrito de Active Directory. Para obtener más información, vea la sección &quot;Conectores de envío creados durante el proceso de suscripción perimetral&quot; en el tema <a href="edge-subscriptions-exchange-2013-help.md">Suscripciones perimetrales</a>.</p>
<p>El servicio que recibe el correo depende de si el servidor de buzones de correo y el servidor de acceso de cliente están instalados en el mismo equipo o en equipos distintos.</p>
<ul>
<li><p><strong>Servidor de buzones de correo independiente</strong>   El conector de recepción predeterminado denominado &quot;<em>&lt;Nombre del servidor de buzones de correo&gt;</em> predeterminado&quot; escucha el correo entrante (incluido el correo de los servidores de transporte perimetral) en el puerto 25.</p></li>
<li><p><strong>Servidor de buzones de correo y servidor de acceso de cliente instalados en el mismo equipo</strong>   El conector de recepción predeterminado denominado &quot;<em>&lt;Nombre del servidor de front-end predeterminado&gt;</em>&quot; en el servicio de transporte de front-end (el rol del servidor de acceso de cliente) escucha el correo entrante (incluido el correo de los servidores de transporte perimetral de Exchange 2013) en el puerto 25.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Correo saliente: organización de Exchange interna a servidor de transporte perimetral</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidores de buzones de correo en el sitio suscrito de Active Directory</p></td>
<td><p>Servidores de transporte perimetral</p></td>
<td><p>El correo saliente siempre pasa por alto el servidor de acceso de cliente.</p>
<p>El correo se retransmite desde cualquier servidor de buzones de correo en el sitio suscrito de Active Directory hacia un servidor de transporte perimetral mediante el conector de envío interno de la organización implícito e invisible que enruta automáticamente el correo entre los servidores de Exchange de la misma organización.</p>
<p>El conector de recepción predeterminado denominado &quot;Conector de recepción interno predeterminado <em>&lt;nombre del servidor de transporte perimetral&gt;</em>&quot; en el servicio de transporte perimetral escucha el correo SMTP en el puerto 25 desde cualquier servidor de buzones de correo en el sitio suscrito de Active Directory.</p></td>
</tr>
<tr class="even">
<td><p>Correo saliente: servidor de transporte perimetral a Internet</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidor de transporte perimetral</p></td>
<td><p>Internet (cualquiera)</p></td>
<td><p>El conector de envío predeterminado denominado &quot;EdgeSync - <em>&lt;nombre del sitio de Active Directory&gt;</em> a Internet&quot; retransmite el correo saliente en el puerto 25 desde el servidor de transporte perimetral hacia Internet.</p></td>
</tr>
<tr class="odd">
<td><p>sincronización de EdgeSync</p></td>
<td><p>50636/TCP (LDAP seguro)</p></td>
<td><p>Servidores de buzones de correo en el sitio suscrito de Active Directory que participan en la sincronización de EdgeSync</p></td>
<td><p>Servidores de transporte perimetral</p></td>
<td><p>Cuando el servidor de transporte perimetral está suscrito al sitio de Active Directory, todos los servidores de buzones de correo que existen en ese momento en el sitio participan en la sincronización de EdgeSync. Sin embargo, los servidores de buzones de correo que agregue más adelante no participarán automáticamente en la sincronización de EdgeSync.</p></td>
</tr>
<tr class="even">
<td><p>DNS para la resolución de nombres del siguiente salto del correo (no mostrado)</p></td>
<td><p>53/UDP,53/TCP (DNS)</p></td>
<td><p>Servidor de transporte perimetral</p></td>
<td><p>Servidor DNS</p></td>
<td><p>Consulte la sección Resolución de nombres.</p></td>
</tr>
<tr class="odd">
<td><p>Definición del servidor proxy para la reputación del remitente (sin imagen)</p></td>
<td><p>definido por el usuario</p></td>
<td><p>Servidores de transporte perimetral</p></td>
<td><p>Internet</p></td>
<td><p>La reputación del remitente (el agente de análisis de protocolo) analiza las rutas de los mensajes entrantes con el fin de reducir el correo no deseado. Si su organización usa un servidor proxy para controlar el acceso a Internet, deberá definir los detalles sobre el servidor proxy para que la reputación del remitente pueda funcionar correctamente (en concreto, abrir la detección de servidores proxy y el bloqueo de remitentes). Use los parámetros <em>ProxyServerName</em>, <em>ProxyServerPort</em> y <em>ProxyServerType</em> en el cmdlet <strong>Set-SenderReputationConfig</strong> para definir el servidor proxy de su organización de modo que la reputación del remitente pueda conectarse correctamente a Internet. Para obtener más información, vea <a href="manage-sender-reputation-exchange-2013-help.md">Administrar la reputación del remitente</a>.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Resolución de nombres

La resolución DNS del próximo salto de correo es una parte fundamental del flujo de correo en cualquier organización de Exchange. Los servidores de Exchange encargados de recibir el correo entrante o de entregar el correo saliente deben poder resolver ambos nombres de host, internos y externos, para enrutar el correo correctamente. Además, todos los servidores internos de Exchange deben poder resolver los nombres de host para enrutar el correo correctamente. Hay muchas formas de diseñar una infraestructura DNS, pero lo más importante es garantizar que la resolución de nombres para el salto siguiente funciona correctamente para todos los servidores de Exchange.

## Puertos de red necesarios para las implementaciones híbridas

Los puertos de red necesarios para que una organización que usa Exchange 2013 y MicrosoftOffice 365 se tratan en la sección "Protocolos de implementación híbrida, puertos y extremos" en [Requisitos previos de implementación híbrida](https://technet.microsoft.com/es-es/library/hh534377\(v=exchg.150\)).

## Puertos de red necesarios para la mensajería unificada

Los puertos de red necesarios para la mensajería unificada se tratan en los temas siguientes:

  - [Protocolos, puertos y servicios de mensajería unificada (UM)](um-protocols-ports-and-services-exchange-2013-help.md)

  - [Póster sobre arquitectura de Exchange Server 2013 SP1](https://go.microsoft.com/fwlink/p/?linkid=518646)

Volver al principio

