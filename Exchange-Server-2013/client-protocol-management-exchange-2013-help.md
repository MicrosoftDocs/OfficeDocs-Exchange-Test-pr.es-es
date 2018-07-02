---
title: 'Administración de protocolos de cliente: Exchange 2013 Help'
TOCTitle: Administración de protocolos de cliente
ms:assetid: 89ba6d24-d1d3-46d5-a0ae-61f0d4c6df21
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657727(v=EXCHG.150)
ms:contentKeyID: 49895757
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administración de protocolos de cliente

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

La administración de los protocolos de cliente de Exchange ActiveSync, Outlook Web App, POP3, IMAP4, el servicio Detección automática, servicios Web Exchange y el servicio de Disponibilidad se realiza en tres áreas diferentes: el Centro de administración de Exchange (EAC), el Shell de administración de Exchange y el Administrador de Internet Information Services (IIS). La configuración que se administra en cada ubicación varía en función del protocolo de cliente.

## Administración de la configuración de Outlook Web App

La mayoría de parámetros que afectan a la disponibilidad de las características de Outlook Web App hacia los usuarios se pueden configurar en el directorio virtual de Outlook Web App o en una directiva de buzones de correo del mismo. Al utilizar las directivas de buzones de correo de Outlook Web App, podrá definir las características disponibles para los usuarios individuales. La configuración de la directiva de buzones de correo sobrescribe la configuración del directorio virtual. Para obtener más información acerca de la administración de Outlook Web App, consulte [Outlook Web App](outlook-web-app-exchange-2013-help.md).

## Administrar la configuración de Exchange ActiveSync

En Exchange 2010, todos los protocolos de acceso de clientes se implementaban y administraban en un rol de servidor único: el rol de servidor de acceso de cliente. La administración de protocolos se realizaba en una única instancia de IIS. Había un objeto único en el directorio virtual de Active Directory para cada protocolo de cliente y se utilizaba un conjunto único de cmdlets para configurar el directorio virtual.

En Exchange 2013, la administración de protocolos de cliente para Exchange ActiveSync está dividida entre el servidor de acceso de cliente y el servidor de buzones de correo. Dado el cambio en la arquitectura, puede ejecutar diferentes tareas de administración del directorio virtual tanto en el servidor de acceso de cliente como en el servidor de buzones de correo. Si estos dos servidores no están instalados en el mismo equipo físico, los parámetros utilizados con los cmdlets del directorio virtual cambiarán en función del rol de servidor en el que los esté ejecutando.

Para obtener más información acerca de los cambios en la arquitectura de Exchange 2013, consulte [Novedades en Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

Existen dos tipos de configuraciones que se pueden aplicar al directorio virtual de Exchange ActiveSync:

  - Configuración aplicable a la sesión de buzones

  - Configuración aplicable al servidor y al directorio virtual

La configuración aplicable a la sesión de buzones de correo es una configuración de sesiones de usuario. Cuando un usuario se conecta a un servidor de acceso de cliente, la conexión se dirige al servidor de buzones que contiene el buzón del usuario. Junto con la solicitud dirigida se incluye un identificador exclusivo del directorio virtual. Más adelante, el servidor de buzones de correo recupera la configuración del directorio virtual de Active Directory y la aplica a la sesión. La configuración del directorio virtual se guarda en la caché del servidor de buzones de correo para mejorar su rendimiento.

Si la conexión se dirige a un sitio de Active Directory diferente, la configuración del directorio virtual se cargará desde el servidor de acceso de cliente en el mismo sitio que el servidor de buzones de correo, y no desde el servidor de acceso de cliente donde se originó la conexión.

Las tablas siguientes indican qué configuraciones de directorio virtual se pueden administrar y en qué servidores. Si intenta administrar una configuración concreta en un servidor para el que no es aplicable, recibirá un mensaje de error en el que se le indicará que la propiedad que intenta configurar es de solo lectura para el servidor en el que está operando.

**Configuración del directorio virtual de Exchange ActiveSync en servidores acceso de cliente**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BadItemReportingEnabled</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>BasicAuthEnabled</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>ClientCertAuth</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>CompressionEnabled</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthenticationMethods</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>ExternalURL</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>InternalAuthenticationMethods</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>InternalURL</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertificateAuthorityURL</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>MobileClientCertificateProvisioningEnabled</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertTemplateName</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsActionForUnknownServers</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsAllowedServers</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsBlockedServers</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsInternalDomainSuffixList</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>SendWatsonReport</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
</tbody>
</table>


**Configuración del directorio virtual de Exchange ActiveSync en servidores acceso de cliente y servidores de buzones de correo**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ApplicationRoot</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="even">
<td><p>AppPoolID</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="odd">
<td><p>MetabasePath</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="even">
<td><p>Name</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="odd">
<td><p>Path</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="even">
<td><p>ProxySubVdir</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="odd">
<td><p>VirtualDirectoryName</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="even">
<td><p>WebsiteName</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
</tbody>
</table>


## Administrar la configuración de POP3 e IMAP4

En Exchange 2013, la implementación de los protocolos POP3 e IMAP4 también se ha segmentado entre los roles de servidor de acceso de cliente y servidor de buzones de correo. Debido a la nueva implementación, la conectividad POP3 e IMAP4 se administran cada una a través de un servicio en el servidor de acceso de cliente, así como también a través de un servicio en el servidor de buzones de correo. Los nombres de los servicios que se ejecutan en el servidor de acceso de cliente son los mismos nombres que existían en Exchange 2010: Servicio de Microsoft Exchange IMAP4 y servicio de Microsoft Exchange POP3. Los nombres de los dos servicios nuevos que se ejecutan en el servidor de buzones de correo son el servicio de Microsoft Exchange IMAP4 y el servicio de Microsoft Exchange POP3 Backend.

Tenga en cuenta lo siguiente al administrar la conectividad POP3 e IMAP4 en su organización:

  - Si está ejecutando el rol de servidor de acceso de cliente y el rol del servidor de buzones de correo en el mismo equipo, cualquier cambio que realice en la configuración de POP3 o IMAP4 se aplicará automáticamente a los servicios correctos de POP3 e IMAP4.

  - Si está ejecutando el rol de servidor de acceso de cliente y el rol de servidor de buzones de correo en equipos separados, deberá administrar la configuración en el equipo que administre la configuración que desea cambiar.

Utilice las siguientes tablas para indicar la configuración de POP/IMAP de cada rol de servidor.

**Configuración POP3 e IMAP4 en el servidor acceso de cliente**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AuthenticatedConnectionTimeout</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>Banner</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>ExternalConnectionSettings</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>InternalConnectionSettings</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>MaxCommandSize</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionFromSingleIP</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>MaxConnections</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionsPerUser</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>PreAuthenticatedConnectionTimeout</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>UnencryptedOrTLSBindings</p></td>
<td><p>Acceso de cliente</p></td>
</tr>
</tbody>
</table>


**Configuración POP3 e IMAP4 en el servidor de buzones de correo**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CalendarItemRetrivalOption</p></td>
<td><p>Buzón</p></td>
</tr>
<tr class="even">
<td><p>EnableExactRFC822Size</p></td>
<td><p>Buzón</p></td>
</tr>
<tr class="odd">
<td><p>MessageRetrievalSortOrder</p></td>
<td><p>Buzón</p></td>
</tr>
<tr class="even">
<td><p>OWAServerURL</p></td>
<td><p>Buzón</p></td>
</tr>
<tr class="odd">
<td><p>ProxyTargetPort</p></td>
<td><p>Buzón</p></td>
</tr>
<tr class="even">
<td><p>ShowHiddenFoldersEnabled</p></td>
<td><p>Buzón</p></td>
</tr>
<tr class="odd">
<td><p>SuppressReadReceipt</p></td>
<td><p>Buzón</p></td>
</tr>
</tbody>
</table>


**Configuración POP3 e IMAP4 en servidores de acceso de cliente y de buzones de correo**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="even">
<td><p>EnforceCertificateErrors</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="odd">
<td><p>LogFileLocation</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="even">
<td><p>LogFileRolloverSettings</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="odd">
<td><p>LoginType</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="even">
<td><p>LogPerFileSizeQuota</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="odd">
<td><p>ProotocolLogEnabled</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="even">
<td><p>Server</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>Buzón y acceso de clientes</p></td>
</tr>
</tbody>
</table>

