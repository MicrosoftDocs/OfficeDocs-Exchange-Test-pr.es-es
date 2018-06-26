---
title: 'Configuración predeterminada para directorios virtuales de Exchange: Exchange 2013 Help'
TOCTitle: Configuración predeterminada para directorios virtuales de Exchange
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 52062063
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración predeterminada para directorios virtuales de Exchange

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Exchange Server 2013 configura automáticamente varios directorios virtuales de Internet Information Services (IIS) durante la instalación. Este tema contiene información sobre la configuración de autenticación de IIS predeterminada y la configuración de Capa de sockets seguros (SSL) predeterminada para los servidores de buzones de correo y acceso de cliente.

## Servidor de Acceso del cliente

La tabla siguiente muestra una lista de la configuración predeterminada en un servidor de acceso de cliente de Exchange 2013.

### Configuración de SSL y autenticación de IIS de servidor de acceso de cliente predeterminado

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Directorio virtual</th>
<th>Método de autenticación</th>
<th>Configuración de SSL</th>
<th>Método de administración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sitio web predeterminado</p></td>
<td><ul>
<li><p>Anónimo</p></li>
</ul></td>
<td><ul>
<li><p>Necesario</p></li>
</ul></td>
<td><p>Consola de administración de IIS</p></td>
</tr>
<tr class="even">
<td><p>aspnet_client</p></td>
<td><ul>
<li><p>Autenticación anónima</p></li>
</ul></td>
<td><ul>
<li><p>SSL requerido</p></li>
<li><p>Requiere cifrado de 128 bits</p></li>
</ul></td>
<td><p>Consola de administración de IIS</p></td>
</tr>
<tr class="odd">
<td><p>Detección automática</p></td>
<td><ul>
<li><p>Autenticación anónima</p></li>
<li><p>Autenticación básica</p></li>
<li><p>Autenticación de Windows</p></li>
</ul></td>
<td><ul>
<li><p>SSL requerido</p></li>
<li><p>Requiere cifrado de 128 bits</p></li>
</ul></td>
<td><p>Consola de administración de Exchange</p></td>
</tr>
<tr class="even">
<td><p>ecp</p></td>
<td><ul>
<li><p>Autenticación anónima</p></li>
<li><p>Autenticación básica</p></li>
</ul></td>
<td><ul>
<li><p>SSL requerido</p></li>
<li><p>Requiere cifrado de 128 bits</p></li>
</ul></td>
<td><p>Shell o centro de administración de Exchange (EAC)</p></td>
</tr>
<tr class="odd">
<td><p>EWS</p></td>
<td><ul>
<li><p>Autenticación anónima</p></li>
<li><p>Autenticación de Windows</p></li>
</ul></td>
<td><ul>
<li><p>SSL requerido</p></li>
<li><p>Requiere cifrado de 128 bits</p></li>
</ul></td>
<td><p>Consola</p></td>
</tr>
<tr class="even">
<td><p>Microsoft-Server-ActiveSync</p></td>
<td><ul>
<li><p>Autenticación básica</p></li>
</ul></td>
<td><ul>
<li><p>SSL requerido</p></li>
<li><p>Requiere cifrado de 128 bits</p></li>
</ul></td>
<td><p>EAC o Shell</p></td>
</tr>
<tr class="odd">
<td><p>OAB</p></td>
<td><ul>
<li><p>Autenticación de Windows</p></li>
</ul></td>
<td><ul>
<li><p>No se requiere</p></li>
</ul></td>
<td><p>EAC o Shell</p></td>
</tr>
<tr class="even">
<td><p>owa</p></td>
<td><ul>
<li><p>Autenticación básica</p></li>
</ul></td>
<td><ul>
<li><p>SSL requerido</p></li>
<li><p>Requiere cifrado de 128 bits</p></li>
</ul></td>
<td><p>EAC o Shell</p></td>
</tr>
<tr class="odd">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Autenticación anónima</p></li>
</ul></td>
<td><ul>
<li><p>No se requiere</p></li>
</ul></td>
<td><p>Consola</p></td>
</tr>
<tr class="even">
<td><p>Rpc</p></td>
<td><ul>
<li><p>Autenticación básica</p></li>
<li><p>Autenticación de Windows</p></li>
</ul></td>
<td><ul>
<li><p>SSL requerido</p></li>
<li><p>Requiere cifrado de 128 bits</p></li>
</ul></td>
<td><p>Consola</p></td>
</tr>
<tr class="odd">
<td><p>RpcWithCert</p></td>
<td><p>De manera predeterminada, todos los métodos de autenticación están deshabilitados.</p></td>
<td><ul>
<li><p>Necesario</p></li>
</ul></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## Servidor de buzones de correo

En la tabla siguiente se muestra una lista de la configuración predeterminada en un servidor de buzones de correo de Exchange 2013 independiente.

### Autenticación de IIS de servidor de buzones de correo predeterminado y configuración de SSL

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Directorio virtual</th>
<th>Método de autenticación</th>
<th>Configuración de SSL</th>
<th>Método de administración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sitio web predeterminado</p></td>
<td><ul>
<li><p>Autenticación anónima</p></li>
</ul></td>
<td><ul>
<li><p>SSL requerido</p></li>
<li><p>Requiere cifrado de 128 bits</p></li>
</ul></td>
<td><p>El usuario no puede configurar este directorio virtual.</p></td>
</tr>
<tr class="even">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>Autenticación anónima</p></li>
</ul></td>
<td><ul>
<li><p>No se requiere</p></li>
</ul></td>
<td><p>Consola</p></td>
</tr>
</tbody>
</table>

