---
title: 'Uso de la autenticación de OAuth para admitir el archivado en una implementación híbrida de Exchange: Exchange 2013 Help'
TOCTitle: Uso de la autenticación de OAuth para admitir el archivado en una implementación híbrida de Exchange
ms:assetid: deb882b1-1ae2-40f3-a71c-423fafe3d66a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn689104(v=EXCHG.150)
ms:contentKeyID: 62247842
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Uso de la autenticación de OAuth para admitir el archivado en una implementación híbrida de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Si dispone de una implementación híbrida de Exchange 2013 y usa el Archivado de Exchange Online (EOA) para Exchange Server, debe configurar la autenticación de OAuth entre las organizaciones locales y de Exchange Online tras actualizar a la actualización acumulativa 5 (CU5) de Exchange 2013. EOA ofrece un archivo basado en la nube para los usuarios con buzones locales. En este escenario, el asistente de administración de registros de mensajes (MRM) del servidor de buzones locales aplica directivas de archivado y mueve automáticamente los mensajes desde el buzón de un usuario al archivo basado en la nube. En la CU5 de Exchange 2013 se usa la autenticación de OAuth.

Para obtener instrucciones paso a paso sobre cómo configurar la autenticación de OAuth, vea [Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## ¿Qué es la autenticación de OAuth?

La autenticación de OAuth es un protocolo de autenticación de servidor a servidor que permite a las aplicaciones autenticarse entre sí. Con esta autenticación, las contraseñas y las credenciales de usuario no se pasan de un equipo a otro. En lugar de eso, la autenticación y la autorización se basan en el intercambio de tokens de seguridad, que conceden acceso a un conjunto específico de recursos para una cantidad de tiempo determinada.

En la autenticación de OAuth suelen intervenir tres partes: un único servidor de autorización y los dos dominios kerberos que necesitan comunicarse entre sí. El servidor de autorización (también conocido como el servidor de tokens de seguridad) emite los tokens de seguridad para los dos dominios kerberos que necesitan comunicarse. Estos tokens se aseguran de que las comunicaciones que se originan en un dominio kerberos resulten de confianza en el otro dominio. Al usar la autenticación OAuth entre una organización local de Exchange y Exchange Online, la función del servidor de autorización se proporciona mediante Servicios de control de acceso (ACS) de Azure Active Directory en la organización de Office 365. Por ejemplo, durante una búsqueda de exhibición de documentos electrónicos entre locales, ACS de Azure Active Directory emite tokens que comprueban que un administrador o responsable de cumplimiento normativo de la organización local de Exchange es capaz de tener acceso a los buzones en la organización de Exchange Online y viceversa.

## Configurar la autenticación de OAuth para que resulte compatible con el archivo

Como se ha indicado anteriormente, vea [Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md) para obtener instrucciones sobre cómo configurar la autenticación de OAuth para que resulte compatible con el archivo en una implementación híbrida de Exchange.

Si no se configura OAuth para la implementación híbrida de Exchange, no podrán usarse directivas de archivado para mover automáticamente elementos del buzón principal de un usuario de la organización local al archivo basado en la nube de Exchange Online.

## Más información

  - También debe configurar la autenticación de OAuth si desea realizar búsquedas de exhibición de documentos electrónicos entre locales en los buzones locales y basados en la nube en una misma búsqueda. Vea [Uso de la autenticación de OAuth para admitir la exhibición de documentos electrónicos en una implementación híbrida de Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md).

  - También puede configurar la autenticación de OAuth para que otras aplicaciones (como SharePoint 2013 y Lync Server 2013) puedan autenticarse en Exchange 2013. Para más información, vea [Configuración de la autenticación de OAuth con SharePoint 2013 y Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

  - Puede configurar la autenticación de servidor a servidor entre Exchange 2013 y SharePoint 2013 para que los administradores y los responsables de cumplimento normativo puedan usar el utilizar el centro de exhibición de documentos electrónicos en SharePoint 2013 para realizar búsquedas en buzones de Exchange 2013. Para más información, vea [Configurar Exchange para el Centro de exhibición de documentos electrónicos de SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

  - En Exchange 2013, puede configurar una implementación híbrida de Exchange con el asistente de configuración híbrida. Para acceder a una lista de comprobación de configuración de implementaciones híbridas paso a paso, use el [Asistente de implementación del servidor de Exchange](https://go.microsoft.com/fwlink/p/?linkid=277105).

