---
title: 'Implementación de certificados para mensajería unificada: Exchange 2013 Help'
TOCTitle: Implementación de certificados para mensajería unificada
ms:assetid: 95658f6f-eac2-4674-90e7-f2d3f25c5242
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee681661(v=EXCHG.150)
ms:contentKeyID: 52062049
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implementación de certificados para mensajería unificada

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-29_

Puede usar Seguridad de la capa de transporte mutua (Mutual TLS) para habilitar la mensajería unificada (UM) para cifrar datos enviados entre sus servidores de Microsoft Exchange 2013 y puertas de enlace VoIP, IP PBX y controladores de borde de sesión (SBC), o puede usar Microsoft Lync Server. Los certificados enlazan la identidad del propietario del certificado con un par de claves electrónicas (pública y privada) que se utilizan para cifrar y firmar la información digitalmente.

Si está usando planes de marcado SIP protegida o Protegida en su organización de Exchange 2010, tendrá que importar los certificados que utilizaban los servidores de acceso de cliente de Exchange 2013 que ejecutaban el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange y los servidores de buzón de correo que ejecutaban el servicio de mensajería unificada de Microsoft Exchange. Puede utilizar uno de los siguientes certificados para los servicios de mensajería unificada y de enrutador de llamadas de mensajería unificada:

  - Un certificado (Exchange) autofirmado

  - Un certificado de infraestructura de clave pública (PKI) interno

  - Un certificado de confianza de terceras partes

Por defecto, cuando instala la mensajería unificada se crea y utiliza un certificado autofirmado. Este certificado autofirmado puede utilizarse con puertas de enlace VoIP, IP PBX y SBC, pero no si integra la mensajería unificada con Lync Server. Si implementa certificados para utilizarlos con Lync Server, necesita utilizar el Asistente para certificados de Exchange o el cmdlet **New-ExchangeCertificate** para obtener un certificado emitido por una autoridad de certificación PKI o interna (CA), o para adquirir un certificado comercial o de terceros que tenga confianza mutua por parte de la mensajería unificada y Lync Server.

## Implementar certificados para puertas de enlace VoIP, IP PBX y SBC

Para que la mensajería unificada pueda cifrar datos enviados entre puertas de enlace VoIP, IP PBX y SBC, debe seguir estos pasos:

  - Use certificados de UM autofirmados o cree un certificado nuevo de Exchange y obtenga un certificado PKI interno, o adquiera un certificado comercial de un tercero que pueda usar para Mutual TLS entre la mensajería unificada y las puertas de enlace VoIP, las IP PBX y los SBC.

  - Importe el certificado que se utilizará en todos los servidores de acceso de cliente y los servidores de buzón de correo de su organización.

  - Habilite el certificado que utilizarán los servicios de mensajería unificada.

  - Importe el certificado a sus puertas de enlace VoIP, IP PBX y SBC.

  - Configure el plan de marcado de mensajería unificada como Protegida o SIP protegida.

  - Configure el modo de inicio de la mensajería unificada en los servidores de acceso de cliente y de buzones de correo en su organización.

  - Cree puertas de enlace IP de mensajería unificada con un nombre de dominio completo (FQDN).

  - Configure el puerto de escucha en las puertas de enlace IP de UM para usar el puerto 5061 TLS.

  - Reinicie el servicio del enrutador de llamadas de mensajería unificada en todos los servidores de acceso de cliente y reinicie el servicio de mensajería unificada de Microsoft Exchange en todos los servidores de buzón de correo.

## Implementar certificados para Lync Server

Para cifrar datos enviados entre la mensajería unificada y Lync Server debe hacer lo siguiente:

  - Cree una solicitud de certificado de Exchange nueva y obtenga un certificado PKI interno, o bien adquiera un certificado de confianza de terceros. El certificado debe tener confianza mutua por parte de la mensajería unificada y Lync Server.

  - Importe el certificado que se utilizará en todos los servidores de acceso de cliente y los servidores de buzón de correo de su organización.

  - Habilite el certificado que utilizarán los servicios de mensajería unificada.

  - Importe el certificado a los equipos con Lync Server.

  - Configure el plan de marcado de mensajería unificada de URI SIP como Protegida o SIP protegida.

  - Configure el modo de inicio de la mensajería unificada en los servidores de acceso de cliente y de buzón de correo en su organización.

  - Ejecute OcsUmUtil.exe desde un equipo con Lync Server.

  - Reinicie el servicio del enrutador de llamada de mensajería unificada en todos los servidores de acceso de cliente y reinicie el servicio de mensajería unificada de Microsoft Exchange en todos los servidores de buzones en su organización. Para obtener información detallada, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

  - Reinicie el servicio front-end de Lync Server en todos los Lync Servers que formen parte de un grupo front-end de Enterprise Edition o reinicie los servidores front-end de Standard Edition. Puede usar el cmdlet **Stop-CsWindowsService** para parar los servicios de Lync Server y el cmdlet **Start-CsWindowsService** para iniciar los servicios de Lync Server.
    
    Los cmdlets **Start-CsWindowsService** y **Stop-CsWindowsService** son parecidos a los cmdlets genéricos de Windows PowerShell **Start-Service** y **Stop-Service**. Si quiere, puede usar el cmdlet **Start-Service** o **Stop-Service** para iniciar y parar un servicio de Lync Server. Sin embargo, los cmdlets **Start-CsWindowsServiceStop-CsWindowsService** incluyen un parámetro *ComputerName* que facilita parar e iniciar un servicio de Lync Server en un equipo remoto. Para ello, debe incluir el parámetro *ComputerName* seguido del nombre de dominio completo (FQDN) del equipo remoto. Los cmdlets **Start-Service** y **Stop-Service** no tienen un parámetro comparable.
    

    > [!NOTE]
    > Para integrar completamente la mensajería unificada y Lync Server, también debe ejecutar el script ExchUcUtil.ps1 en cualquier servidor de acceso de clientes o de buzones en su organización


