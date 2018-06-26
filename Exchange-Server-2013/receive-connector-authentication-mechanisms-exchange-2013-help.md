---
title: 'Mecanismos de autenticación del conector de recepción: Exchange 2013 Help'
TOCTitle: Mecanismos de autenticación del conector de recepción
ms:assetid: 926424e1-83e3-4c4b-b2dd-bf814d81e877
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657472(v=EXCHG.150)
ms:contentKeyID: 49895782
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mecanismos de autenticación del conector de recepción

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_


Los mecanismos de autenticación del conector de recepción son los siguientes:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Mecanismo de autenticación</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ninguno</p></td>
<td><p>Sin autenticación.</p></td>
</tr>
<tr class="even">
<td><p>TLS</p></td>
<td><p>Advertise STARTTLS. Necesita de la disponibilidad de un certificado de servidor para ofrecer TLS.</p></td>
</tr>
<tr class="odd">
<td><p>Integrado</p></td>
<td><p>NTLM y Kerberos (autenticación de Windows integrada).</p></td>
</tr>
<tr class="even">
<td><p>BasicAuth</p></td>
<td><p>Autenticación básica. Precisa de un inicio de sesión autenticado.</p></td>
</tr>
<tr class="odd">
<td><p>BasicAuthRequireTLS</p></td>
<td><p>Autenticación básica por TLS. Precisa de un certificado de servidor.</p></td>
</tr>
<tr class="even">
<td><p>ExchangeServer</p></td>
<td><p>Autenticación del servidor de Exchange (API de servicios de seguridad genéricos [GSSAPI] y GSSAPI mutuo).</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthoritative</p></td>
<td><p>La conexión se considera externamente asegurada mediante un mecanismo de seguridad que es externo a Exchange. La conexión puede ser una asociación de protocolo de seguridad de Internet (IPsec) o una red privada virtual (VPN). Como alternativa, los servidores pueden residir en una red controlada físicamente y de confianza. El método de autenticación de <code>ExternalAuthoritative</code> requiere el grupo de permisos de <code>ExchangeServers</code>. Esta combinación de un método de autenticación y un grupo de seguridad permite la resolución de direcciones de correo de remitentes anónimas de los mensajes recibidos a través de este conector.</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de los mecanismos de autenticación del conector de recepción, vea [New-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125139\(v=exchg.150\)).

