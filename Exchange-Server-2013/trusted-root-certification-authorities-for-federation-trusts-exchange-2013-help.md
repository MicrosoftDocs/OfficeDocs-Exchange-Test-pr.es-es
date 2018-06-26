---
title: 'Autoridades de certificación raíz de confianza para confianzas de federación: Exchange 2013 Help'
TOCTitle: Autoridades de certificación raíz de confianza para confianzas de federación
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 48268731
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autoridades de certificación raíz de confianza para confianzas de federación

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2017-07-26_

Para establecer una confianza de federación entre la organización de Exchange Server 2013 de Microsoft y el [sistema de autenticación de Active Directory de Azure](https://go.microsoft.com/fwlink/p/?linkid=135986), necesita un certificado digital instalado en el servidor de Exchange utilizado para crear la confianza. Es más recomendable usar un certificado autofirmado. Un certificado autofirmado creado y se instala automáticamente cuando se utiliza al Asistente para **Habilitar la confianza de federación** en la Centro de administración de Exchange (EAF).

Si no quiere usar el certificado autofirmado recomendado, le aconsejamos que solicite (e instale) un certificado de Capa de sockets seguros (SSL) X.509 a una entidad de certificación (CA) que sea de confianza para Microsoft. Aunque los certificados emitidos por otras CA se pueden usar para establecer una confianza de federación el sistema de autenticación de Azure AD, no están certificados por Microsoft hasta la fecha.

En la siguiente tabla se enumeran las entidades de certificación en las que Microsoft confía actualmente. Estas entidades de certificación se han probado para su uso con Exchange 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre descriptivo de la entidad de certificación</th>
<th>Emitido por</th>
<th>Objetivos planteados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="even">
<td><p>Comodo</p></td>
<td><p>Entidad de certificación Comodo</p></td>
<td><p>Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="odd">
<td><p>CyberTrust</p></td>
<td><p>Entidad de certificación de Baltimore CyberTrust Root</p></td>
<td><p>Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="even">
<td><p>Digicert</p></td>
<td><p>Entidad de certificación Digicert Global Root</p></td>
<td><p>‎Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="odd">
<td><p>Digicert High Assurance EV, Extended Validation</p></td>
<td><p>Entidad de certificación Digicert Global Root</p></td>
<td><p>‎Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="even">
<td><p>Entrust</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="odd">
<td><p>Entrust (2048)</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="even">
<td><p>Equifax</p></td>
<td><p>Entidad de certificación Equifax Secure</p></td>
<td><p>‎‎Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="odd">
<td><p>GlobalSign</p></td>
<td><p>Autoridad de certificación de GlobalSign</p></td>
<td><p>‎Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="even">
<td><p>Go Daddy</p></td>
<td><p>Go Daddy Class 2 Certification Authority</p></td>
<td><p>‎Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="odd">
<td><p>Network Solutions</p></td>
<td><p>Entidad de certificación Network Solutions</p></td>
<td><p>Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="even">
<td><p>PositiveSSL</p></td>
<td><p>Entidad de certificación Comodo</p></td>
<td><p>‎Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="odd">
<td><p>SECOM</p></td>
<td><p>Entidad de certificación SECOM Trust Systems</p></td>
<td><p>‎Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="even">
<td><p>UTN-UserFirst-Hardware</p></td>
<td><p>Entidad de certificación Comodo</p></td>
<td><p>Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="odd">
<td><p>VeriSign</p></td>
<td><p>Entidad de certificación Class 3 Public Primary</p></td>
<td><p>Autenticación de servidor, autenticación de cliente</p></td>
</tr>
<tr class="even">
<td><p>VeriSign</p></td>
<td><p>VeriSign Trust Network</p></td>
<td><p>‎Autenticación de servidor, autenticación de cliente</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de los requisitos de certificado para la Federación, vea [Federación](federation-exchange-2013-help.md).

