---
title: 'Uso de la autenticación de OAuth para admitir la exhibición de documentos electrónicos en una implementación híbrida de Exchange: Exchange 2013 Help'
TOCTitle: Uso de la autenticación de OAuth para admitir la exhibición de documentos electrónicos en una implementación híbrida de Exchange
ms:assetid: b069f8db-fbe1-4047-ad97-d00172ee6a12
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn497703(v=EXCHG.150)
ms:contentKeyID: 61292930
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Uso de la autenticación de OAuth para admitir la exhibición de documentos electrónicos en una implementación híbrida de Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Para realizar con éxito búsquedas de exhibición de documentos electrónicos entre locales en una organización híbrida de Exchange 2013, tendrá que configurar la autenticación de OAuth (Open Authorization) entre sus organizaciones de Exchange locales y de Exchange Online para poder usar la exhibición de documentos electrónicos local para buscar buzones locales y basados en la nube. La autenticación de OAuth admite los siguientes escenarios de exhibición de documentos electrónicos en una implementación híbrida de Exchange:

  - Buzones locales de búsqueda que usan el Archivado de Exchange Online para buzones de archivo basados en la nube.

  - Búsqueda de buzones locales y basados en la nube en la misma búsqueda de exhibición de documentos electrónicos.

Para obtener instrucciones paso a paso para configurar la autenticación de OAuth de modo que admita la exhibición de documentos electrónicos, vea [Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## ¿Qué es la autenticación de OAuth?

La autenticación de OAuth es un protocolo de autenticación de servidor a servidor que permite a las aplicaciones autenticarse mutuamente. Con la autenticación de OAuth, las credenciales de usuario y las contraseñas no se pasan de un equipo a otro. En lugar de eso, la autenticación y la autorización se basan en los tokens de seguridad de Exchange, que conceden acceso a un conjunto específico de recursos durante una determinada cantidad de tiempo.

Para la autenticación de OAuth se suelen emplear tres partes: un único servidor de autorización y los dos dominios Kerberos que necesitan comunicarse entre sí. El servidor de autorización (también conocido como el servidor de tokens de seguridad) emite los tokens de seguridad para los dos dominios Kerberos que necesitan comunicarse. Estos tokens comprueban que las comunicaciones que se originan en un dominio Kerberos sean de confianza para el otro dominio. Cuando se usa la autenticación de OAuth entre una organización de Exchange local y Exchange Online, los servicios de control de acceso (ACS) de Microsoft Azure Active Directory proporcionan la función del servidor de autorización en la organización de Office 365. Por ejemplo, durante una búsqueda de exhibición de documentos electrónicos entre locales, ACS de Azure emite tokens que comprueban que un administrador o responsable de cumplimiento normativo de la organización local de Exchange es capaz de tener acceso a los buzones en la organización de Exchange Online y viceversa.

## Escenarios de exhibición de documentos electrónicos en una implementación híbrida

En la tabla siguiente se identifican los escenarios de exhibición de documentos electrónicos en una implementación híbrida de Exchange que requieren autenticación de OAuth.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Escenario de exhibición de documentos electrónicos</th>
<th>¿Requiere autenticación de OAuth?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Buscar buzones locales de Exchange y buzones de Exchange Online en la misma búsqueda de exhibición de documentos electrónicos iniciada desde la organización local de Exchange. Por ejemplo, buscar todos los buzones de la organización en una búsqueda única de exhibición de documentos electrónicos.</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Buscar buzones locales de Exchange que usan el Archivado de Exchange Online para buzones de archivo basados en la nube. Cuando se usa la exhibición de documentos electrónicos local, se buscan los buzones de correo principales y de archivo.</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Buscar buzones de Exchange Online a partir de una búsqueda de exhibición de documentos electrónicos iniciada desde la organización local de Exchange por un administrador o un responsable de cumplimiento normativo.</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Buscar buzones locales mediante una búsqueda de exhibición de documentos electrónicos iniciada desde la organización local de Exchange por un administrador o un responsable de cumplimiento normativo.</p></td>
<td><p>No</p>

> [!NOTE]
> Como se explicó anteriormente, la autenticación de OAuth sería necesaria si se configuraran los buzones locales con los buzones de archivo basados en la nube.


</td>
</tr>
<tr class="odd">
<td><p>Buscar buzones de Exchange Online a partir de una búsqueda de exhibición de documentos electrónicos iniciada desde Exchange Online o el Centro de exhibición de documentos electrónicos en SharePoint Online por un administrador de inquilinos de Office 365 o un responsable de cumplimiento normativo que hayan iniciado sesión en una cuenta de usuario de Office 365.</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Configuración de la autenticación de OAuth para admitir la exhibición de documentos electrónicos

Como se señaló anteriormente, vea [Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md) para ver las instrucciones sobre cómo configurar la autenticación de OAuth para admitir la exhibición de documentos electrónicos en una implementación híbrida de Exchange.

Si OAuth no está configurado para su implementación híbrida de Exchange, no podrá usar la exhibición de documentos electrónicos para buscar buzones de Exchange local y Exchange Online en la misma búsqueda de exhibición de documentos electrónicos. Tendrá que buscar buzones locales a partir de una búsqueda de exhibición de documentos electrónicos iniciada desde la organización local. Del mismo modo, solo podrá buscar buzones de Exchange Online a partir de una búsqueda de exhibición de documentos electrónicos iniciada desde la organización de Exchange Online o mediante el Centro de exhibición de documentos electrónicos en SharePoint Online. Además, no podrá buscar buzones locales principales si su buzón de correo de archivo correspondiente reside en Exchange Online o en una organización de Archivado de Exchange Online.

## Más información

  - También puede usar la autenticación de OAuth para permitir que otras aplicaciones, como SharePoint 2013 y Lync Server 2013, se autentiquen en Exchange 2013. Para obtener más información, vea [Configuración de la autenticación de OAuth con SharePoint 2013 y Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

  - Puede configurar la autenticación de servidor a servidor entre Exchange 2013 y SharePoint 2013 para que los administradores y responsables de cumplimiento normativo puedan usar el Centro de exhibición de documentos electrónicos en SharePoint 2013 para buscar buzones de Exchange 2013. Para obtener más información, vea [Configurar Exchange para el Centro de exhibición de documentos electrónicos de SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

  - Puede configurar una implementación híbrida de Exchange mediante el Asistente para configuración de híbrido en Exchange 2013. Para una lista de comprobación de la configuración de implementación híbrida personalizada, paso a paso, consulte el [Asistente de instalación de Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=277105).

