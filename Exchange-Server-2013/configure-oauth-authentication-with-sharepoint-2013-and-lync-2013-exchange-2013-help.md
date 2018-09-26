---
title: 'Configuración de la autenticación de OAuth con SharePoint 2013 y Lync 2013: Exchange 2013 Help'
TOCTitle: Configuración de la autenticación de OAuth con SharePoint 2013 y Lync 2013
ms:assetid: ca3c78a3-80cc-4df2-859f-0106bbd57a07
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ649094(v=EXCHG.150)
ms:contentKeyID: 49895915
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración de la autenticación de OAuth con SharePoint 2013 y Lync 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-03-03_

Exchange Server 2013 permite que otras aplicaciones utilicen OAuth para autenticar a Exchange. Las aplicaciones deben estar configuradas como aplicaciones de socios en Exchange 2013.

En Exchange 2013, la configuración de OAuth con aplicaciones de socios como SharePoint 2013 y Lync Server 2013 se admiten solo al usar el script `Configure-EnterpriseApplication.ps1`. Al automatizar la tarea, el script facilita la configuración de autenticación con las aplicaciones de socios y disminuye los errores de configuración. Este script realiza las siguientes tareas:

1.  Configura una aplicación de socios de Enterprise que envía automáticamente tokens OAuth para que se autentiquen correctamente en Exchange.

2.  Asigna funciones del Control de acceso basado en roles (RBAC) a la aplicación de socio para autorizarla a solicitar una API del Servicio web de Exchange específica.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos.

  - La aplicación del socio debe publicar un documento de metadatos de autenticación para Exchange 2013 para establecer una confianza directa a esta aplicación y aceptar solicitudes de autenticación.

  - Ejemplos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada «Configurar aplicaciones de socio» en el tema [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurar la autenticación OAuth con una aplicación de socio

Este procedimiento utiliza el script `Configure-EntepririseApplication.ps1` para configurar una autenticación con aplicaciones de socios. El acceso a los recursos depende de los permisos asignados a la aplicación del socio o al usuario que realiza una suplantación mediante RBAC.

Después de configurar la autenticación OAuth de Exchange, la aplicación de socio puede utilizar los recursos de Exchange 2013. Si Exchange 2013 también necesita acceso a los recursos ofrecidos por la aplicación de socio, también debe configurar la autenticación OAuth en la aplicación de socio.

Este ejemplo configura la autenticación OAuth para SharePoint 2013.

```powershell
Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://sharepoint.contoso.com/_layouts/15/metadata/json/1 -ApplicationType SharePoint
```

Este ejemplo configura la autenticación OAuth para Lync Server 2013.

```powershell
Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://lync.contoso.com/metadata/json/1 -ApplicationType Lync
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha configurado correctamente una aplicación de socio de Enterprise para autenticar en Exchange 2013, ejecute el cmdlet [Get-PartnerApplication](https://technet.microsoft.com/es-es/library/jj218721\(v=exchg.150\)) en el Shell para recuperar la configuración. También puede ejecutar el cmdlet [Test-OAuthConnectivity](https://technet.microsoft.com/es-es/library/jj218623\(v=exchg.150\)) para probar la conectividad OAuth con una aplicación de socio para un usuario.

## Más información

  - En implementaciones híbridas, puede usar la autenticación de OAuth entre la organización de Exchange 2013 local y la organización de Exchange Online. Para más información, vea [Uso de la autenticación de OAuth para admitir la exhibición de documentos electrónicos en una implementación híbrida de Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md).

  - En implementaciones locales, puede configurar la autenticación de servidor a servidor entre Exchange 2013 y SharePoint 2013 para que los administradores y los responsables de cumplimiento puedan usar el Centro de exhibición de documentos electrónicos en SharePoint 2013 para buscar buzones de correo de Exchange 2013. Para más información, vea [Configurar Exchange para el Centro de exhibición de documentos electrónicos de SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

