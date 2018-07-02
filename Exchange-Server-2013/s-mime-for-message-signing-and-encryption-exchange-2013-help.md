---
title: 'S/MIME para la firma y el cifrado de mensajes: Exchange 2013 Help'
TOCTitle: S/MIME para la firma y el cifrado de mensajes
ms:assetid: 887c710b-0ec6-4ff0-8065-5f05f74afef3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn626158(v=EXCHG.150)
ms:contentKeyID: 61212725
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# S/MIME para la firma y el cifrado de mensajes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

S/MIME (Extensiones seguras multipropósito al correo de Internet) es un método, o más concretamente un protocolo, ampliamente aceptado para enviar mensajes cifrados y firmados digitalmente. S/MIME permite cifrar mensajes de correo electrónico y firmarlos digitalmente. Cuando se usa S/MIME con un mensaje de correo electrónico, ayuda a las personas que reciben ese mensaje a estar seguras de que lo que ven en sus bandejas de entrada es el mensaje exacto que envió el remitente. También ayudará a las personas que reciben mensajes a estar seguras de que el mensaje proviene del remitente específico y no de alguien que pretende ser el remitente. Para ello, S/MIME proporciona servicios de seguridad criptográfica como autenticación, integridad de mensajes y no rechazo de origen (usando firmas digitales). También ayuda a mejorar la privacidad y la seguridad de los datos (mediante cifrado) en la mensajería electrónica. Para obtener más información sobre la historia y la arquitectura de S/MIME en el contexto del correo electrónico, consulte [Descripción de S/MIME](https://go.microsoft.com/fwlink/?linkid=393948).

Como administrador, puede habilitar la seguridad basada en S/MIME para su organización si tiene buzones en cualquiera Exchange 2013 SP1 o en Exchange Online, que forma parte de Office 365. Use las instrucciones en los temas cuyos vínculos aparecen a continuación junto con el Shell de administración de Exchange para configurar S/MIME. Para usar S/MIME en las versiones admitidas de Outlook o ActiveSync, con Exchange 2013 SP1 o Exchange Online, los usuarios de su organización deben tener certificados emitidos con fines de firma y cifrado, y datos publicados en sus Servicios de dominio de Active Directory (AD DS) locales. Su AD DS debe encontrarse en equipos en una ubicación física bajo su control, y no en una instalación remota o en un servicio basado en la nube en algún lugar de Internet. Para obtener más información sobre AD DS, consulte [Servicios de dominio de Active Directory](https://go.microsoft.com/fwlink/?linkid=394064).

## Consideraciones técnicas y escenarios admitidos

Si su organización usa Exchange 2013 SP1 o Exchange Online, puede configurar S/MIME para trabajar con cualquiera de los siguientes extremos:

  - Outlook 2010

  - Outlook 2013

  - Outlook Web App

  - Exchange ActiveSync (EAS)

Los pasos que debe seguir para configurar S/MIME con cada uno de estos extremos es ligeramente diferente según cuál elija. Por lo general, deberá realizar lo siguiente:

  - Instale una entidad emisora de certificados basada en Windows y configure una infraestructura de clave pública para emitir certificados S/MIME. También se admiten los certificados emitidos por los proveedores de certificados de terceros. Para obtener más información, consulte [Información general de Servicios de certificados de Active Directory](https://technet.microsoft.com/library/hh831740.aspx).

  - Publicar el certificado de usuario en una cuenta local de AD DS en los atributos UserSMIMECertificate y UserCertificate.

  - Para las organizaciones Exchange Online, sincronizar los certificados de usuario de AD DS con Azure Active Directory usando una versión adecuada de DirSync. Estos certificados se sincronizarán desde Azure Active Directory al directorio de Exchange Online y se usarán cuando se cifre un mensaje para un destinatario.

  - Crear una colección virtual de certificados para validar S/MIME. OWA usa esta información para validar la firma de un correo electrónico y garantizar que se ha firmado con un certificado de confianza.

  - Configurar el extremo de Outlook o EAS para usar S/MIME.

## Configurar S/MIME con Outlook Web App

Para configurar S/MIME para Exchange 2013 SP1 o Exchange Online con Outlook Web App hay que realizar estos pasos:

1.  [Configuración de S/MIME para Outlook Web App](configure-s-mime-settings-for-outlook-web-app-exchange-2013-help.md)

2.  [Configurar una colección de certificados virtuales para validar S/MIME](set-up-virtual-certificate-collection-to-validate-s-mime-exchange-2013-help.md)

3.  [Sincronizar certificados de usuario con Office 365 para S/MIME](https://technet.microsoft.com/es-es/library/dn626159\(v=exchg.150\)) Este paso solo se aplica a Exchange Online.

## Tecnologías de cifrado de mensajes relacionadas

Debido al aumento de la importancia de la seguridad de los mensajes, los administradores necesitan comprender los principios y conceptos de la mensajería segura. Esto es especialmente importante por la creciente variedad de nuevas tecnologías relativas a la protección, como S/MIME. Para obtener más información sobre S/MIME y cómo funciona en el contexto del correo electrónico, consulte [Descripción de S/MIME](https://go.microsoft.com/fwlink/?linkid=393948). Diversas tecnologías de cifrado trabajan juntas para proporcionar protección a los mensajes en reposo y en tránsito. S/MIME puede trabajar simultáneamente con las siguientes tecnologías pero no depende de ellas:

  -  
    **Seguridad de la capa de transporte (TLS)** cifra el túnel o la ruta entre los servidores de correo electrónico para ayudar a evitar exámenes y escuchas no autorizados.

  -  
    **Capa de sockets seguros (SSL)** cifra la conexión entre los clientes de correo electrónico y los servidores de Office 365.

  -  
    **BitLocker** cifra los datos de un disco duro en un centro de datos para que si alguien obtiene acceso no autorizado, no pueda leerlos.

## Comparación de S/MIME con Cifrado de mensajes de Office 365

S/MIME requiere una infraestructura de certificados y publicación que suele usarse en situaciones de negocio a negocio y de negocio a consumidor. El usuario controla las claves criptográficas en S/MIME y puede elegir si quiere usarlas para cada mensaje que envíe. Los programas de correo electrónico como Outlook buscan una ubicación de entidades de certificación raíz de confianza para llevar a cabo la firma digital y la comprobación de la firma. Cifrado de mensajes de Office 365 es un servicio de cifrado basado en directiva que un administrador, no un usuario individual, puede configurar para cifrar el correo que se envíe a cualquier persona dentro o fuera de la organización. Es un servicio en línea que se basa en Azure Rights Management (RMS) y no usa una infraestructura de clave pública. Cifrado de mensajes de Office 365 también proporciona funciones adicionales, como la capacidad de personalizar el correo con la marca de la organización. Para obtener más información sobre el Cifrado de mensajes de Office 365, consulte [Cifrado de mensajes de Office 365](https://go.microsoft.com/fwlink/?linkid=392525).

## Más información

[Outlook Web App](outlook-web-app-exchange-2013-help.md)

[Correo seguro (2000)](https://technet.microsoft.com/es-es/library/cc962043.aspx)

