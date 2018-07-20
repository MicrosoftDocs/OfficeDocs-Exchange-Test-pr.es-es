---
title: 'Federación: Exchange 2013 Help'
TOCTitle: Federación
ms:assetid: 0046e2eb-6940-4941-bd5b-cbe6bffa3b94
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335047(v=EXCHG.150)
ms:contentKeyID: 48267746
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Federación

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

A menudo, los trabajadores de la información necesitan colaborar con destinatarios externos, proveedores, asociados y clientes, y comparten la información de disponibilidad (conocida como disponibilidad de calendario). La federación en Microsoft Exchange Server 2013 ayuda con estos esfuerzos de colaboración. *Federación* hace referencia a la infraestructura de confianza subyacente que es compatible con *el uso compartido federado*, un método sencillo para que los usuarios compartan la información de calendario con los destinatarios en otras organizaciones federadas externas. Para obtener más información acerca del uso compartido federado, consulte [Uso compartido](sharing-exchange-2013-help.md).


> [!IMPORTANT]
> Esta característica de Exchange Server 2013 no es totalmente compatible con Office 365 operado por 21Vianet en China y pueden aplicarse ciertas limitaciones en las características. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/?linkid=313640">Acerca de Office 365 operado por 21Vianet</A>.



**Contenido**

Terminología básica

Sistema de autenticación de Azure AD

Confianza de federación

Identificador de organización federada

Ejemplo de federación

Requisitos de certificados para la federación

Transición a un certificado nuevo

Consideraciones de firewall para federación

## Terminología básica

En la tabla siguiente se definen los componentes básicos asociados a la federación en Exchange 2013.

  - **identificador de aplicación (AppID)**  
    Un número único generado por el sistema de autenticación de Azure Active Directory para identificar las organizaciones de Exchange. El AppID se genera automáticamente cuando se crea una confianza de federación el sistema de autenticación de Azure Active Directory.

<!-- end list -->

  - **token de delegación**  
    Un token de lenguaje de marcado de aserción de seguridad (SAML) emitido por el sistema de autenticación de Azure Active Directory que permite que los usuarios de una organización federada sean de confianza para otra organización federada. Un token de delegación contiene la dirección de correo electrónico del usuario, un identificador inmutable e información asociada con la oferta para la que se emitió el token para acción.

<!-- end list -->

  - **organización federada externa**  
    Una organización de Exchange externa que se establece como confianza de federación con el sistema de autenticación de Azure Active Directory.

<!-- end list -->

  - **uso compartido federado**  
    Grupo de características de Exchange que aprovechan una confianza de federación con el sistema de autenticación de Azure Active Directory para funcionar en organizaciones de Exchange, incluidas las implementaciones de Exchange entre locales. Juntas, estas características se usan para realizar solicitudes autenticadas entre los servidores en nombre de los usuarios en varias organizaciones de Exchange.

<!-- end list -->

  - **dominio federado**  
    Dominio relevante aceptado que se agrega al identificador de la organización (OrgID) para una organización de Exchange.

<!-- end list -->

  - **cadena de cifrado de prueba de dominio**  
    Cadena protegida criptográficamente que utiliza una organización de Exchange para brindar pruebas de que su organización posee un dominio que se usa con el sistema de autenticación de Azure Active Directory. La cadena se genera automáticamente cuando se usa el Asistente para **Habilitar confianzas de federación** o se puede generar con el cmdlet **Get-FederatedDomainProof**.

<!-- end list -->

  - **directiva de uso compartido federado**  
    Directiva de nivel de organización que permite y controla el uso compartido de persona a persona establecido por el usuario de la información del calendario.

<!-- end list -->

  - **federación**  
    Acuerdo basado en la confianza entre dos de organizaciones de Exchange para lograr un propósito común. Con la federación, ambas organizaciones desean que aserciones de autenticación de una organización sean reconocidas por la otra.

<!-- end list -->

  - **confianza de federación**  
    Relación con el sistema de autenticación de Azure Active Directory que define los siguientes componentes para su organización de Exchange:
    
      - Espacio de nombres de cuenta
    
      - Identificador de aplicación (AppID)
    
      - Identificador de organización (OrgID)
    
      - Dominios federados
    
    Para configurar el uso compartido federado con otras organizaciones federadas de Exchange, se debe establecer la federación con el sistema de autenticación de Azure Active Directory.

<!-- end list -->

  - **organización no federada**  
    Organizaciones que no tienen un agente de federación establecido con el sistema de autenticación de Azure Active Directory.

<!-- end list -->

  - **identificador de organización (OrgID)**  
    Define cuáles de los dominios de aceptados relevantes configurados en una organización están habilitados para federación. Solamente los destinatarios que tienen direcciones de correo electrónico con dominios federados configurados en "OrgID" son reconocidos por el sistema de autenticación de Azure Active Directory y pueden usar características de uso compartido federado. Este "OrgID" es una combinación de una cadena predefinida y el primer dominio aceptado seleccionado para la federación en el Asistente para **Habilitar confianzas de federación**. Por ejemplo, si especifica el dominio federado contoso.com como el dominio principal SMTP de su organización, el espacio de nombres de la cuenta FYDIBOHF25SPDLT.contoso.com se creará automáticamente como el "OrgID" para la confianza de generación.

<!-- end list -->

  - **relación de organización**  
    Relación de uno a uno entre dos organizaciones federadas de Exchange que permite a los destinatarios compartir información de disponibilidad (de calendario). Una relación de organización requiere una confianza de federación con el sistema de autenticación de Azure Active Directory y reemplaza la necesidad de usar bosques de Active Directory o confianzas de dominio entre las organizaciones de Exchange.

<!-- end list -->

  - **Azure Active Directory sistema de autenticación**  
    Un servicio de identidad basado en la nube, gratuito que actúa como agente de confianza entre las organizaciones federadas de Microsoft Exchange. Es responsable de emitir tokens de delegación para los destinatarios de Exchange cuando solicitan información a los destinatarios en otras organizaciones federadas de Exchange. Para más información, consulte [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500).

## Sistema de autenticación de Azure AD

El sistema de autenticación de Azure Active Directory, un servicio gratuito basado en nube ofrecido por Microsoft, actúa como agente de confianza entre su organización local de Exchange 2013 y otras organizaciones federadas de Exchange 2010 y Exchange 2013 . Si desea configurar la federación en su organización de Exchange, debe establecer una confianza de federación única con el sistema de autenticación de Azure Active Directory, para que pueda convertirse en un socio de federación con su organización. Con esta confianza, el sistema de autenticación de Azure AD emite tokens de delegación del lenguaje de marcado de aserción de seguridad (SAML) para los usuarios autenticados por Active Directory (conocidos como *proveedores de identidades*). Estos tokens de delegación permiten a los usuarios de una organización federada de Exchange ser de confianza de otra organización federada de Exchange. Con el sistema de autenticación de Azure AD actuando como agente de confianza, las organizaciones no necesitan establecer varias relaciones de confianza individuales con otras organizaciones y los usuarios pueden obtener acceso a los recursos externos mediante un inicio de sesión único (SSO). Para más información, consulte [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500).

Terminología básica

## Confianza de federación

Para usar las características de uso compartido federado de Exchange 2013, debe establecer una confianza de federación entre su organización de Exchange 2013 y el sistema de autenticación de Azure AD. Al establecer una confianza de federación con el sistema de autenticación de Azure AD, se intercambia el certificado de seguridad digital de su organización con el sistema de autenticación de Azure AD y se obtiene el certificado del sistema de autenticación de Azure AD y los metadatos de federación. Puede establecer una confianza de federación mediante el Asistente para **Habilitar confianzas de federación** en el Centro de administración de Exchange (EAC) o el cmdlet **New-FederationTrust** en el Shell de administración de Exchange. El Asistente para **Habilitar confianzas de federación** crea automáticamente un certificado autofirmado y este se usa para firmar y cifrar tokens de delegación desde el sistema de autenticación de Azure AD que permiten que las organizaciones federadas externas confíen en los usuarios. Para obtener información detallada acerca de los requisitos del certificado, consulte Requisitos de certificados para la federación más adelante en este tema.

Al crear una confianza de federación con el sistema de autenticación de Azure AD, se genera automáticamente un *identificador de aplicación* (AppID) para la organización de Exchange y se proporciona en la salida del cmdlet **Get-FederationTrust**. El sistema de autenticación de Azure AD usa el identificador de aplicación para identificar su organización de Exchange. También lo usa la organización de Exchange para ofrecer pruebas de que su organización posee un dominio para usar con el sistema de autenticación de Azure AD. Esto se realiza al crear un registro de texto (TXT) en la zona Sistema de nombres de dominio (DNS) público para cada dominio federado.

Terminología básica

## Identificador de organización federada

El *identificador de organización federada* (OrgID) define los dominios aceptados autoritativos configurados en la organización de que están habilitados para la federación. Solamente los destinatarios que tienen direcciones de correo electrónico con dominios aceptados configurados en "OrgID" son reconocidos por el sistema de autenticación de Azure AD y pueden usar características de uso compartido federado. Al crear una nueva confianza de federación, se crea automáticamente un OrgID con el sistema de autenticación de Azure AD. Este "OrgID" es una combinación de una cadena predefinida y el dominio seleccionado aceptado como dominio compartido primario en el asistente. Por ejemplo, en el Asistente para editar dominios compartidos habilitados, si especifica el dominio federado **contoso.com** como dominio compartido primario de su organización, el espacio de nombres de la cuenta **FYDIBOHF25SPDLT.contoso.com** se creará automáticamente como "OrgID" para la confianza de federación de su organización de Exchange.

A pesar de que habitualmente es el dominio SMTP principal en la organización de Exchange, este dominio no tiene que ser un dominio aceptado en su organización de Exchange y no requiere un registro de texto (TXT) con prueba de propiedad del Sistema de nombres de dominio (DNS). El único requisito es que los dominios aceptados seleccionados para ser federados se limiten a un máximo de 32 caracteres. El único objetivo de dicho subdominio es funcionar como espacio de nombres federados para el sistema de autenticación de Azure AD con el fin de mantener identificadores exclusivos para los destinatarios que solicitan tokens de delegación del Lenguaje de marcado de aserción de seguridad (SAML). Para obtener más información acerca de los símbolos de SAML, consulte [Símbolos y notificaciones de SAML](https://go.microsoft.com/fwlink/?linkid=198561)

Puede agregar o quitar los dominios aceptados desde la confianza de generación en cualquier momento. Además, si desea habilitar o deshabilitar todas las funciones de uso compartido de federación en su organización, todo lo que tiene que hacer es habilitar o deshabilitar OrgID para la confianza de federación.


> [!IMPORTANT]
> Si cambia OrgID, los dominios aceptados o AppID que se usó para la confianza de generación, todas las funciones de uso compartido de federación se verán afectadas en su organización. Esto también afecta las organizaciones de Exchange federadas externas, incluidos Exchange Online y las configuraciones de implementación híbrida. Le recomendamos que notifique a todos los socios federados externos sobre los cambios en estas configuraciones de confianza de federación.



Terminología básica

## Ejemplo de federación

Dos organizaciones de Exchange, Contoso, Ltd. y Fabrikam, Inc., desean que sus usuarios puedan compartir la información del calendario de disponibilidad entre ellos. Cada organización crea una confianza de federación con el sistema de autenticación de Azure AD y configura su espacio de nombres para incluir el dominio usado para su dominio de dirección de correo electrónico del usuario.

Los empleados de Contoso usan uno de los siguientes dominios de dirección de correo electrónico: contoso.com, contoso.co.uk, o contoso.ca. Los empleados de Fabrikam usan uno de los siguientes dominios de dirección de correo electrónico: fabrikam.com, fabrikam.org, o fabrikam.net. Ambas organizaciones aseguran de que todos los dominios de correo electrónico aceptados se incluyen en el espacio de nombres de la cuenta para su confianza de federación con el sistema de autenticación de Azure AD. En lugar de requerir un bosque complejo de Active Directory o una configuración de confianza del dominio entre los organizaciones, ambas organizaciones configuran una relación de la organización con la otra para permitir el uso compartido de disponibilidad de calendario.

La siguiente figura ilustra la configuración de federación entre Contoso, Ltd. y Fabrikam, Inc.

**Ejemplo de uso compartido federado**

![Confianzas de federación y uso compartido federado](images/Dd335047.310f0698-b67d-4b0e-91e4-231c6e9db952(EXCHG.150).gif "Confianzas de federación y uso compartido federado")

## Requisitos de certificados para la federación

Para establecer una confianza de federación con el sistema de autenticación de Azure AD, se debe crear un certificado autofirmado o un certificado X.509 firmado por una autoridad de certificación (CA) e instalarlo en el servidor de Exchange 2013 usado para crear la confianza. Le recomendamos encarecidamente usar un certificado autofirmado, el cual se puede crear automáticamente e instalar usando el Asistente para **Habilitar confianzas de federación** en el EAC. Este certificado se usa solamente para firmar y cifrar tokens de delegación usados para el uso compartido federado. Solamente se requiere un certificado para la confianza de delegación. Exchange 2013 distribuye automáticamente el certificado a otros servidores de Exchange 2013 en la organización.

Si desea usar un certificado X.509 firmado por una CA externa, el certificado debe cumplir con los siguientes requisitos:

  - **Autoridad de certificación confiable**   Si es posible, el certificado X.509 SSL (Capa de sockets seguros) debe ser emitido desde una CA confiable de Windows Live. Sin embargo, puede usar certificados emitidos por CA que actualmente no están certificados por Microsoft. Para obtener una lista actual de CA de confianza, consulte [Autoridades de certificación raíz de confianza para confianzas de federación](trusted-root-certification-authorities-for-federation-trusts-exchange-2013-help.md).

  - **Identificador de clave de asunto**   El certificado debe tener un campo de identificador de clave de asunto. La mayoría de los certificados X.509 emitidos por CA comerciales tienen este identificador.

  - **Proveedor de servicios de cifrado (CSP) de CryptoAPI**   El certificado debe usar un CSP de CryptoAPI. Certificados que usan la criptografía API: Los proveedores de próxima generación (CNG) no se admiten para la federación. Si usa Exchange para crear una solicitud de certificado, se usa un proveedor de CryptoAPI. Para obtener más información consulte [criptografía API: Próxima generación](https://go.microsoft.com/fwlink/?linkid=187890).

  - **Algoritmo de firma RSA**   El certificado debe usar RSA como el algoritmo de firma.

  - **Clave privada exportable**   La clave privada usada para generar el certificado debe ser exportable. Puede especificar que la clave privada sea exportable al crear la solicitud de certificado mediante el Asistente para **Nuevo certificado de intercambio** en el EAC o el cmdlet [New-ExchangeCertificate](https://technet.microsoft.com/es-es/library/aa998327\(v=exchg.150\)) en el Shell.

  - **Certificado actual**   El certificado debe ser actual. No puede usar un certificado expirado o revocado para crear una confianza de federación.

  - **Uso mejorado de clave**   El certificado debe incluir el tipo de uso mejorado de clave (EKU) **Autenticación de cliente (1.3.6.1.5.5.7.3.2)**. Este tipo de uso se utiliza para demostrar su identidad en un equipo remoto. Si usa EAC o Shell para generar la solicitud de certificado, este tipo de uso se incluye de forma predeterminada.


> [!NOTE]
> Debido a que el certificado no se usa con fines de autenticación, no cuenta con requisitos de nombre de asunto o nombre de asunto alternativo. Puede usar un certificado con un nombre de asunto que sea el mismo nombre que el nombre de host, el nombre de dominio o cualquier otro nombre.



Terminología básica

## Transición a un certificado nuevo

El certificado usado para crear la confianza de federación está designado como el certificado actual. Sin embargo, es posible que necesite instalar y usar periódicamente un nuevo certificado para la confianza de federación. Por ejemplo, es posible que necesite usar un nuevo certificado si el certificado actual caduca o para cumplir con los nuevos requisitos de seguridad o comerciales. Para garantizar una transición sin problemas a un certificado nuevo, debe instalar el certificado nuevo en el servidor de Exchange 2013 y configurar la confianza de federación para designarlo como el nuevo certificado. Exchange 2013 distribuye automáticamente el nuevo certificado a otros servidores de Exchange 2013 de la organización. Según la topología de Active Directory, la distribución del certificado puede tardar varios minutos. Puede comprar el estado del certificado usando el cmdlet [Test-FederationTrustCertificate](https://technet.microsoft.com/es-es/library/dd335228\(v=exchg.150\)) en el Shell.

Después de comprobar el estado de distribución del certificado, puede configurar la confianza de manera que use el nuevo certificado. Luego de cambiar los certificados, el certificado actual se designa como el certificado anterior y el nuevo certificado se designa como el certificado actual. El nuevo certificado se publica en el sistema de autenticación de Azure AD y todos los nuevos tokens que se intercambian con el sistema de autenticación de Azure AD se cifran con el certificado nuevo.


> [!NOTE]
> Este proceso de transición del certificado es usado solamente por la federación. Si usa el mismo certificado para otras características de Exchange&nbsp;2013 que usan certificados, debe tener en cuenta los requisitos de las características al planear obtener, instalar o cambiar a un certificado nuevo.



Terminología básica

## Consideraciones de firewall para federación

Las características de federación requieren que los servidores de buzones y de acceso de cliente de la organización tengan acceso de salida a Internet mediante HTTPS. Debe permitir el acceso HTTPS de salida (puerto 443 para TCP) desde todos los servidores de buzones y de acceso de cliente de Exchange 2013 de la organización.

Para permitir que una organización externa tenga acceso a la información de disponibilidad de su organización, debe publicar un servidor de acceso de cliente en Internet. Esto requiere acceso HTTPS de entrada desde Internet al servidor de acceso de cliente. Los servidores de acceso de cliente de los sitios de Active Directory que no tienen un servidor de acceso de cliente publicado en Internet pueden usar servidores de acceso de cliente de otros sitios de Active Directory a los que tengan acceso mediante Internet. Los servidores de acceso de cliente que no se publican en Internet deben tener la URL externa del directorio virtual de servicios que se establece con la URL que es visible a las organizaciones externas.

[Volver al principio](sharing-exchange-2013-help.md)

