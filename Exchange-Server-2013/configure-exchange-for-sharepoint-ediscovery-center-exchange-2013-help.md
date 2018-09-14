---
title: 'Configurar Exchange para Centro de eDiscovery SharePoint: Exchange 2013 Help'
TOCTitle: Configurar Exchange para el Centro de exhibición de documentos electrónicos de SharePoint
ms:assetid: 795c1a3b-295c-4ee5-ade9-52cf3fda3f19
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ218665(v=EXCHG.150)
ms:contentKeyID: 49116324
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar Exchange para el Centro de exhibición de documentos electrónicos de SharePoint

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Microsoft Exchange Server 2013 incluye características que funcionan con Microsoft SharePoint Server 2013 y Microsoft Lync Server 2013, conocidas como *aplicaciones de socios*. Para garantizar que dichas aplicaciones puedan acceder a los recursos de cada uno, deberá configurar la autenticación de servidor a servidor.

En este tema se detalla cómo configurar la autenticación de servidor a servidor entre Exchange 2013 y SharePoint 2013, de modo que los usuarios puedan utilizar el Centro de exhibición de documentos electrónicos de SharePoint 2013 para realizar búsquedas del contenido de buzones de correo de Exchange Server 2013. Para habilitar por completo esta funcionalidad, deberá completar los pasos adicionales en SharePoint 2013. Para obtener más información, consulte [Configurar la exhibición de documentos electrónicos en SharePoint 2013](https://go.microsoft.com/fwlink/?linkid=257727).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea:  30 minutos.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Se permite instalar Exchange 2013 y SharePoint 2013 en distintos dominios o bosques. No se requiere una relación de confianza de Windows entre bosques de Exchange y SharePoint, ya que, en esta circunstancia, Exchange y SharePoint se basarán en el protocolo OAuth 2.0 para su respectiva confianza.

  - El sitio de SharePoint 2013 debe estar configurado para usar la Capa de sockets seguros (SSL).

  - La [API administrada de servicios Web Exchange](https://go.microsoft.com/fwlink/?linkid=257726) debe estar instalada en cada uno de los servidores que ejecutan SharePoint 2013. Restablezca Internet Information Server (IIS) después de la instalación.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Configurar la autenticación de servidor a servidor para Exchange 2013 en un servidor que ejecuta SharePoint Server 2013

Ejecute el comando siguiente para crear Exchange 2013 como emisor de token de seguridad de confianza en SharePoint 2013.

    New-SPTrustedSecurityTokenIssuer -Name Exchange -MetadataEndPoint https://<Exchange Server Name or FQDN>/autodiscover/metadata/json/1

## Paso 2: Configurar la autenticación de servidor a servidor para SharePoint 2013 un servidor que ejecuta Exchange 2013

Realice este paso en un servidor de Exchange 2013. Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configurar aplicaciones de socio" en el tema [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md).

Ejecute este comando para configurar la aplicación de socio de SharePoint.

    cd c:\'Program Files'\Microsoft\'Exchange Server'\V15\Scripts
    .\Configure-EnterprisePartnerApplication.ps1 -AuthMetadataUrl <path to SharePoint AuthMetadataUrl> -ApplicationType SharePoint

## Paso 3: Agregar usuarios autorizados al grupo de roles de administración de detección

Añada usuarios que necesiten realizar una búsqueda de exhibición de documentos electrónicos mediante SharePoint 2013 al grupo de roles de administración de detección en Exchange 2013. Para obtener información más detallada, consulte [Asignar permisos de exhibición de documentos electrónicos en Exchange](https://docs.microsoft.com/es-es/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions).


> [!WARNING]
> La adición de usuarios al grupo de roles de administración de detección permitirá que utilicen la exhibición de documentos electrónicos local para realizar búsquedas en todos los buzones de Exchange&nbsp;2013 y que accedan al contenido de correos potencialmente delicados de los buzones de usuarios. De manera predeterminada, este permiso no se asigna a ningún usuario, incluidos los miembros del grupo de roles de administración de la organización. Consulte este aspecto con los departamentos legal y de Recursos Humanos de la organización antes de asignar este permiso a algún usuario.


