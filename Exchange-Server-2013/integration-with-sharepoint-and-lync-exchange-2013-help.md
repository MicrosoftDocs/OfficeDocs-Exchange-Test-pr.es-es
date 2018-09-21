---
title: 'Integración con SharePoint y Lync: Exchange 2013 Help'
TOCTitle: Integración con SharePoint y Lync
ms:assetid: 056b29f6-e0e9-4974-b763-002518857a93
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150480(v=EXCHG.150)
ms:contentKeyID: 48267764
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Integración con SharePoint y Lync

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

MicrosoftExchange Server 2013 incluye muchas características que se integran con Microsoft SharePoint 2013 y Microsoft Lync 2013. Juntos, estos productos ofrecen un conjunto de características que posibilitan escenarios como la exhibición de documentos electrónicos de empresas y la colaboración mediante buzones de sitio.

## Archivo, retención y Exhibición de documentos electrónicos

El archivado de correos electrónicos y documentos, que los conserva durante el período requerido para satisfacer los cumplimientos normativos y los requisitos empresariales, y la capacidad de buscarlos rápidamente para satisfacer los requisitos de Exhibición de documentos electrónicos es fundamental en la mayoría de organizaciones. Exchange 2013, SharePoint 2013 y Lync Server 2013 juntos proporcionan un archivado integrado, una retención y una funcionalidad de Exhibición de documentos electrónicos, que le permite conservar datos importantes en contexto en los buzones de correo de Exchange, documentos de SharePoint y sitios web, y contenido de Lync archivado. El Centro de exhibición de documentos electrónicos en SharePoint 2013 permite a los administradores de detección autorizados realizar una búsqueda de exhibición de documentos electrónicos de los contenidos en estos almacenes, obtener una vista previa de los resultados de búsqueda y exportar los datos para revisiones legales.

## Archivado del contenido de Lync Server 2013 en Exchange 2013

Con Lync Server 2013 implementado en una organización con Exchange 2013, puede configurar Lync para que archive el contenido de la mensajería instantánea y de las reuniones en línea como presentaciones compartidas o documentos en el buzón de correo de un usuario de Exchange 2013. El archivado de datos de Lync en Exchange 2013 le permite aplicar directivas de retención. El contenido archivado de Lync también se muestra en las búsquedas de exhibición de documentos electrónicos. Para obtener más detalles acerca del archivado de Lync y cómo implementarlo, consulte los siguientes temas:

  - [Planear el archivado](https://go.microsoft.com/fwlink/p/?linkid=265005)

  - [Implementar el archivado](https://go.microsoft.com/fwlink/p/?linkid=265006)

## Datos de búsqueda de Exchange, SharePoint y Lync usando el Centro de exhibición de documentos electrónicos de SharePoint 2013

Exchange 2013 permite a SharePoint 2013 buscar contenido de buzón de correo de Exchange usando el API de búsqueda federada. SharePoint 2013 proporciona un Centro de exhibición de documentos electrónicos para permitir que el personal autorizado realice exhibición de documentos electrónicos. Microsoft Search Foundation proporciona un indexado común y una infraestructura de búsqueda para Exchange 2013 y SharePoint 2013 y le permite usar la misma sintaxis de consulta para ambas aplicaciones. Esto garantiza que una búsqueda de exhibición de documentos electrónicos realizada en SharePoint 2013 devolverán el mismo contenido de Exchange 2013 que la misma búsqueda realizada usando Exhibición de documentos electrónicos en contexto en Exchange 2013. El Centro de exhibición de documentos electrónicos de SharePoint 2013 también le permite exportar los contenidos devueltos en una búsqueda de exhibición de documentos electrónicos, incluyendo la exportación del contenido de Exchange 2013 en un archivo PST.

Para obtener información detallada, consulte los siguientes temas:

  - [Exhibición de documentos electrónicos en contexto](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/integrate-sensitive-information-rules)

  - [Conservación local y retención por juicio](https://docs.microsoft.com/es-es/exchange/security-and-compliance/in-place-and-litigation-holds)

  - [Configurar eDiscovery en SharePoint Server 2013](https://go.microsoft.com/fwlink/p/?linkid=257727)

  - [Novedades de la exhibición de documentos electrónicos en SharePoint Server 2013](https://go.microsoft.com/fwlink/?linkid=275091)

  - [Configurar Exchange para el Centro de exhibición de documentos electrónicos de SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)

## Buzones del sitio

En muchas organizaciones, la información reside en dos almacenes diferentes: correo electrónico en Microsoft Exchange y documentos en SharePoint, con dos interfaces diferentes para acceder a ella. Esto provoca una experiencia de usuario distinta e impide una colaboración eficaz. Los buzones de sitio permiten a los usuarios colaborar de forma efectiva al unir los correos electrónicos de Exchange y los documentos de SharePoint. Para los usuarios, un buzón de sitio sirve de archivador central, que proporciona un lugar donde archivar los correos electrónicos y documentos de un proyecto, a los que pueden acceder y pueden editar los miembros del sitio. Los buzones de sitio aparecen en Outlook 2013 y le brindan al usuario fácil acceso al correo electrónico y los documentos para los proyectos importantes. Asimismo, se puede acceder al mismo tipo de contenido directamente desde el propio sitio SharePoint.

Bajo la cubierta de un buzón de sitio, el contenido se conserva donde pertenece. Exchange almacena el correo electrónico, brindándole al usuario la misma vista de mensaje para las conversaciones por correo electrónico que utilizan cada día en sus propios buzones. SharePoint almacena los documentos, permitiendo la coautoría y la posibilidad de crear versiones de un documento. Exchange sincroniza la cantidad suficiente de metadatos de SharePoint para crear la vista de documentos en Outlook (p. ej. título del documento, fecha de última modificación, último autor modificado, tamaño).

Los buzones de sitio se aprovisionan y gestionan desde SharePoint 2013. Para obtener información detallada, consulte los siguientes temas:

  - [Buzones de correo del sitio](site-mailboxes-exchange-2013-help.md)

  - [Configurar buzones de sitio en SharePoint Server 2013](https://go.microsoft.com/fwlink/p/?linkid=258264)

## Almacén de contactos unificado

El Almacén de contactos unificado (UCS) es una característica que proporciona una experiencia de contactos uniforme a través de los productos de Microsoft Office. Esta característica permite a los usuarios almacenar toda la información de contacto en su buzón de correo de Exchange 2013 de forma que la misma información de contacto esté disponible globalmente en Lync, Exchange, Outlook y Outlook Web App.

Después de instalar Lync Server 2013 en un entorno con Exchange 2013 y de haber configurado la autenticación de servidor a servidor entre los dos, los usuarios pueden iniciar la migración de los contactos existentes de Lync Server 2013 a Exchange 2013. Para obtener más información, consulte [Planear e implementar almacén de contactos unificados](https://go.microsoft.com/fwlink/p/?linkid=275092).

## Fotos de usuario

Fotografías del usuario es una característica que le permite almacenar fotos de usuario en alta resolución en Exchange 2013 a las cuales pueden acceder las aplicaciones cliente, que incluyen Outlook, Outlook Web App, SharePoint 2013, Lync 2013, y clientes de correo electrónico móvil. También se almacena una fotografía de baja resolución en Active Directory. Como pasa con los Almacenes de contactos unificados, las fotografías del usuario permiten que su organización mantenga fotografías de perfil de usuario uniformes que pueden usar las aplicaciones cliente sin la necesidad de que cada aplicación tenga sus propias fotografías de usuario y diferentes formas de agregarlas y gestionarlas. Los usuarios pueden gestionar sus propias fotografías usando Outlook Web App, SharePoint 2013 o Lync 2013. Para obtener más información acerca de la administración de fotografías en Outlook Web App, consulte [Mi cuenta](https://go.microsoft.com/fwlink/p/?linkid=269646).

## Presencia de Lync en Outlook Web App

En entornos de Exchange 2013 con Lync Server 2013 instalado, puede configurarlos para habilitar los usuarios para que vean información de presencia en Outlook Web App. Los usuarios pueden ver sus contactos y grupos de mensajería instantánea en el panel de navegación de Outlook Web App, responder a e iniciar sesiones de mensajería instantánea desde Outlook Web App y gestionar sus contactos y grupos de mensajería instantánea.

## Autenticación OAuth

Exchange 2013, SharePoint 2013 y Lync Server 2013 proporcionan una rica funcionalidad entre productos descrita anteriormente con el protocolo de autenticación OAuth para la autenticación de servidor a servidor. El uso del mismo protocolo de autenticación permite a estas aplicaciones autenticarse entre ellas de forma uniforme y segura. El mecanismo de autenticación admite la autenticación como una aplicación que usa el contexto de una cuenta vinculada donde la solicitud de acceso se realiza en el contexto de usuario.

OAuth es un protocolo de autorización estándar usado por muchos sitios y servicios web. Permite a los clientes acceder a los recursos que proporciona un servidor de recursos que debe aportar un nombre de usuario y una contraseña. La autenticación la realiza un servidor de autorización de confianza del propietario del recurso, que proporciona el cliente con un token de acceso. El token garantiza el acceso a un conjunto específico de recursos durante un período especificado. Para obtener más información acerca de la implementación de OAuth de Exchange 2013, consulte [\[MS-XOAUTH\]: Extensiones del protocolo de autorización OAuth 2.0](https://go.microsoft.com/fwlink/p/?linkid=275093).

**OAuth en las implementaciones locales**

Dentro de una implementación local, Exchange 2013, SharePoint 2013 y Lync Server 2013 no necesitan un servidor de autorización para emitir tokens. Cada una de estos tokens autofirmados emitidos por las aplicaciones puede acceder a los recursos que proporcione la aplicación. La aplicación que proporciona acceso a los recursos, por ejemplo Exchange 2013, debe confiar en los tokens autofirmados por la aplicación que llama. La confianza se establece creando una configuración de *aplicación asociada* de la aplicación llamante, que incluye el "ApplicationID", el certificado y "AuthMetadataUrl" de la aplicación llamante. Exchange 2013, SharePoint 2013 y Lync Server 2013 publican su documento de metadatos de autorización en una dirección URL conocida.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Servidor</strong></p></td>
<td><p><strong>AuthMetadataUrl</strong></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/autodiscover/metadata/json/1</code></p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/metadata/json/1</code></p></td>
</tr>
<tr class="even">
<td><p>SharePoint 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/_layouts/15/metadata/json/1</code></p></td>
</tr>
</tbody>
</table>


**Certificado de autenticación de Exchange 2013**

El programa de instalación de Exchange 2013 crea un certificado autofirmado con el nombre Certificado de autenticación de Microsoft Exchange Server. El certificado se replica en todos los servidores front-end en la organización de Exchange 2013. La huella digital del certificado se especifica en la configuración de autenticación de Exchange 2013, junto con su nombre de servicio, un GUID conocido que representa Exchange 2013 local. Exchange utiliza la configuración de autorización para publicar su documento de metadatos de autenticación.


> [!IMPORTANT]
> El certificado de autenticación del servidor predeterminado creado por Exchange&nbsp;2013 es válido durante cinco años. Debe asegurarse de que la configuración de autorización incluya un certificado actual.



Cuando Exchange 2013 recibe una solicitud de acceso de una aplicación asociada a través de los Servicios Web de Exchange (EWS), analiza el encabezado `www-authenticate` de la solicitud de https, que contiene el token de acceso firmado por el servidor que llama usando su clave privada. El módulo de autenticación valida el token de acceso utilizando la configuración de la aplicación de asociado. Garantiza el acceso a los recursos según los permisos RBAC que se garantizan a la aplicación. Si el token está en nombre de un usuario, se comprueban los permisos RBAC garantizados al usuario. Por ejemplo, si un usuario realiza una búsqueda de exhibición de documentos electrónicos usando el Centro de exhibición de documentos electrónicos en SharePoint 2013, Exchange comprueba si el usuario es un miembro del grupo de roles de administración de la detección o tiene un rol de búsqueda en buzones de correo y los buzones que se buscan están dentro del ámbito de asignación de roles RBAC. Para obtener más información, consulte [Permisos](permissions-exchange-2013-help.md).

## Administrar la autenticación "OAuth"

En Exchange 2013, hay dos objetos de configuración que debe administrar para la autenticación "OAuth" con aplicaciones asociadas:

  - **AuthConfig** "AuthConfig" lo crea el programa de instalación de Exchange 2013 y se usa para publicar los metadatos de autenticación. No tiene que administrar la configuración de autenticación excepto para aprovisionar un nuevo certificado cuando un certificado existente está a punto de expiración. Cuando esto se produce, puede renovar el certificado existente y configurar el nuevo certificado como certificado siguiente en "AuthConfig" junto con su fecha efectiva. El nuevo certificado se replica automáticamente en otros Exchange 2013 de la organización, el documento de metadatos de autenticación se actualiza con los detalles del certificado nuevo y "AuthConfig" pasa al certificado nuevo en la fecha efectiva.

  - **Aplicaciones asociadas** Para habilitar aplicaciones asociadas para que soliciten tokens de acceso de Exchange 2013, debe crear una configuración de aplicación asociada. Exchange 2013 proporciona el script `Configure-EnterprisePartnerApplication.ps1`, que le permite crear de forma rápida y fácil configuraciones de aplicaciones asociadas y minimizar los errores de configuración. Para obtener información más detallada, consulte [Configuración de la autenticación de OAuth con SharePoint 2013 y Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

