---
title: 'Azure Ayudar a identificar mi problema con comprobaciones automáticas: registros DNS: Exchange 2013 Help'
TOCTitle: 'Azure Ayudar a identificar mi problema con comprobaciones automáticas: registros DNS'
ms:assetid: 1ef42cde-4df4-401a-b8f2-494630996ca8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn793619(v=EXCHG.150)
ms:contentKeyID: 62630014
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Azure Ayudar a identificar mi problema con comprobaciones automáticas: registros DNS

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Uno de los problemas de configuración más comunes consiste en configurar incorrectamente los registros DNS. Puede usar las siguientes comprobaciones automáticas para validar la configuración y actualizar su entorno.

Si ya posee una cuenta de usuario de Office 365, seleccione Iniciar sesión. No necesita una cuenta de identificación de Azure. Quizás se le pida una cuenta de usuario nuevamente cuando se ejecutan las comprobaciones. Si es así, la cuenta de usuario está en el formato de nombredeusuario@iniciosesióndeoffice365.dominio y la contraseña.

## Requisitos previos

Comprobaremos si tiene instalados Ayudante para el inicio de sesión de Azure Active Directory y Módulo Azure Active Directory para Windows PowerShell.

El Ayudante para el inicio de sesión de Azure Active Directory viene en dos versiones: [32 bits](https://go.microsoft.com/fwlink/?linkid=286261) y [64 bits](https://go.microsoft.com/fwlink/?linkid=286262).

El Módulo Azure Active Directory para Windows PowerShell viene en dos versiones: [32 bits](https://go.microsoft.com/fwlink/?linkid=286258) y [64 bits](https://go.microsoft.com/fwlink/?linkid=286259).

## Comprobaciones de registros DNS


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Aplicación</p></td>
<td><p>Síntoma</p></td>
<td><p>Comprobación</p></td>
</tr>
<tr class="even">
<td><p>Dominios</p></td>
<td><p>Mi dominio personalizado (por ejemplo, contoso.com) no parece estar configurado con Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Dominios</p></td>
<td><p>Mi dominio personalizado (por ejemplo, contoso.com) no parece estar configurado con Office 365 (usé un registro CNAME).</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="even">
<td><p>Dominios</p></td>
<td><p>Mi dominio personalizado (por ejemplo, contoso.com) no parece estar configurado con Office 365 (usé un registro TXT).</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Mensajería instantánea</p></td>
<td><p>Mis usuarios tienen problemas para que su cliente Lync funcione.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834901">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="even">
<td><p>Mensajería instantánea</p></td>
<td><p>Mis usuarios tienen problemas para que su cliente Lync funcione con otras organizaciones.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834902">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Correo</p></td>
<td><p>No logro que Outlook se configure automáticamente con Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834897">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="even">
<td><p>Correo</p></td>
<td><p>Mi correo electrónico no parece estar enrutado a Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834898">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Correo</p></td>
<td><p>Mi organización recibe una gran cantidad de correo no deseado.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834903">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="even">
<td><p>Correo</p></td>
<td><p>No logro hacer que funcione la implementación híbrida de Exchange.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834904">Ejecutar esta comprobación</a></p></td>
</tr>
</tbody>
</table>

