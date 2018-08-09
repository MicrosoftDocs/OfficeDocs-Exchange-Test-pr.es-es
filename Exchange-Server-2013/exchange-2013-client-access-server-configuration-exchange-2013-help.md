---
title: 'Configurar el servidor acceso cliente de Exchange 2013: Exchange 2013 Help'
TOCTitle: Configuración del servidor de acceso de cliente de Exchange 2013
ms:assetid: 01432ae4-2a00-44a4-a4dd-4eb8d7e6cfae
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh529912(v=EXCHG.150)
ms:contentKeyID: 49895432
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuración del servidor de acceso de cliente de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-07-25_

Tras instalar el servidor de acceso de clientes de Exchange 2013, hay varias tareas de configuración que puede realizar. Aunque el servidor de acceso de clientes de Exchange 2013 no gestiona el procesamiento de los protocolos de cliente, se deben aplicar varias configuraciones al servidor de acceso de clientes, incluyendo la configuración del directorio virtual y la configuración de los certificados.

## Configurar certificados de servidor

En Exchange 2013, puede usar el Asistente para certificados para solicitar un certificado digital de una entidad de certificación. Después de haber solicitado un certificado digital, deberá instalarlo en el servidor de acceso de clientes.

No es necesario que instale certificados digitales en los servidores de buzones de correo de su organización. Se instala un certificado autofirmado de forma predeterminada en los servidores de buzones de correo y no es necesario sustituirlo. Los servidores de acceso de clientes de su organización implícitamente confían en el certificado autofirmado de los servidores de buzones de correo. Para obtener más información, consulte [Interfaz de usuario de administración de certificados de Exchange 2013](exchange-2013-certificate-management-ui-exchange-2013-help.md).

## Configuración de los directorios virtuales

Hay varios ajustes que puede configurar en los directorios virtuales para la libreta de direcciones sin conexión (OAB), Servicios Web de Exchange, Exchange ActiveSync, Outlook Web App y el Centro de administración de Exchange. Para obtener más información acerca de la administración de los directorios virtuales, consulte [Administración de directorios virtuales](virtual-directory-management-exchange-2013-help.md). Puede configurar los directorios virtuales utilizando los siguientes comandos.

  - Exchange 2013 ofrece dos conjuntos de configuraciones de conectividad HTTP para configurar Outlook en cualquier lugar para que los administradores puedan configurar un extremo interno y otro externo.
    
    Para administrar Outlook en cualquier lugar con una sola dirección URL para la conectividad, debe indicar el nombre de host, si se requiere o no SSL y especificar un AuthPackage usando el comando siguiente en el Shell de administración de Exchange:
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    También hay que especificar un extremo accesible externamente usando el siguiente comando en el Shell de administración de Exchange:
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -ExternalHostname "externalServer.company.com" -ExternalClientAuthenticationMethod Basic -ExternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    

    > [!TIP]
    > Aunque Exchange 2013 es compatible con la autenticación de HTTP Negotiate para Outlook en cualquier lugar, esta solo se debe usar cuando todos los servidores del entorno ejecutan Exchange 2013.



  - Para configurar Exchange ActiveSync, ejecute el siguiente comando.
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2013>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl "https://mail.contoso.com/Microsoft-Server-ActiveSync"

  - Para configurar el directorio virtual de Servicios Web de Exchange, ejecute el siguiente comando.
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalUrl https://mail.contoso.com/EWS/Exchange.asmx

  - Para configurar la libreta de direcciones sin conexión, ejecute el siguiente comando.
    
        Set-OABVirtualDirectory -Identity "<CAS2013>\OAB (Default Web Site)" -ExternalUrl "https://mail.contoso.com/OAB"

  - Para configurar el punto de conexión de servicio, ejecute el comando siguiente.
    
        Set-ClientAccessServer -Identity <CAS2013> -AutoDiscoverServiceInternalURI https://autodiscover.contoso.com/AutoDiscover/AutoDiscover.xml

## Actualizar desde el acceso de cliente de Exchange 2007 y 2010

Use esta sección para configurar el acceso externo a los protocolos del servidor de acceso de cliente de Exchange 2013. Ejecute los comandos del Shell de administración de Exchange de la sección anterior de directorios virtuales de configuración, así como los comandos siguientes.

Deberá ejecutar los siguientes comandos para configurar los directorios virtuales de Exchange 2013.

1.  Para configurar una URL externa para Outlook Web App, ejecute el siguiente comando en el Shell de administración de Exchange.
    
        Set-OwaVirtualDirectory "<CAS2013>\OWA (Default Web Site)" -ExternalUrl https://mail.contoso.com/OWA
    
    Ejecute los siguientes comandos en el símbolo del sistema después de establecer el directorio virtual de Outlook Web App.
      ```
        Net stop IISAdmin /y
      ```
      ```
        Net start W3SVC
      ```
      
2.  Para configurar el acceso externo al EAC, ejecute el comando siguiente en el Shell de administración de Exchange.
    
        Set-EcpVirtualDirectory "<CAS2013>\ECP (Default Web Site)" -ExternalUrl https://mail.contoso.com/ECP -InternalURL https://mail.contoso.com/ECP 

3.  Para configurar el servicio de disponibilidad, ejecute el comando siguiente en el Shell de administración de Exchange.
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalURL https://mail.contoso.com/EWS/Exchange.asmx

Para comprobar que se ha configurado correctamente la dirección URL externa para Exchange ActiveSync o Outlook Web App, puede utilizar el analizador de conectividad remota, una herramienta gratuita basada en Web proporcionada por Microsoft. Puede encontrar el analizador de conectividad remota [aquí](http://go.microsoft.com/fwlink/?linkid=154308).

Para comprobar si la autenticación se ha configurado correctamente para Exchange ActiveSync o Outlook Web App, también puede usar ExRCA.

Para comprobar si el acceso directo a archivos se ha configurado correctamente para Outlook Web App, inicie sesión como usuario en Outlook Web App usando la opción de PC público y luego intente acceder y guardar un archivo adjunto a un mensaje de correo.

## Configurar protocolos en los servidores de acceso de cliente de Exchange 2007

Deberá ejecutar los siguientes comandos para configurar los directorios virtuales de Exchange 2007.

  - Para configurar una dirección URL externa en el directorio virtual de Exchange ActiveSync, ejecute el comando siguiente en el Shell de administración de Exchange.
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2007>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl https://mail.contoso.com/Microsoft-Server-ActiveSync

  - Para configurar una dirección URL externa en el directorio virtual de Outlook Web App, ejecute el comando siguiente en el Shell de administración de Exchange.
    
        Set-OwaVirtualDirectory -Identity "<CAS2007>\owa (Default Web Site)" -ExternalUrl https://legacy.contoso.com/owa

