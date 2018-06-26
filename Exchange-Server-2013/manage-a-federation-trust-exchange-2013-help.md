---
title: 'Administrar una confianza de federación: Exchange 2013 Help'
TOCTitle: Administrar una confianza de federación
ms:assetid: 0439839f-2052-4bc9-9d30-aa6e7d51b733
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673036(v=EXCHG.150)
ms:contentKeyID: 49895445
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar una confianza de federación

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-01-01_

Una confianza de federación establece una relación de confianza entre una organización de Microsoft Exchange 2013 y el sistema de autenticación de Azure Active Directory, y admite el uso compartido de recursos federados con otras organizaciones federadas de Exchange. Normalmente, no debería tener que administrar ni modificar la confianza de federación una vez creada. Sin embargo, puede que haya ciertas circunstancias que requieran la adición o eliminación de dominios federados o el restablecimiento del dominio usado para configurar el identificador de organización (OrgID) para la confianza de federación.


> [!NOTE]
> La modificación de una confianza de federación, especialmente el dominio compartido primario usado para definir el "OrgID", puede afectar a la compartición federada entre las organizaciones de Exchange o la implementación híbrida con las organizaciones de Office 365.



Para otras tareas de administración relacionadas con la federación, consulte [Procedimientos de la Federación](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esta característica de Exchange Server 2013 no es totalmente compatible con Office 365 operado por 21Vianet en China y pueden aplicarse ciertas limitaciones en las características. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/?linkid=313640">Acerca de Office 365 operado por 21Vianet</A>.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  30 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada de permisos *Federation and certificates* en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Deberá agregar un registro TXT a su DNS público para cada dominio federado nuevo que se agregue a la confianza de federación. Revise los requisitos para agregar un registro TXT con la organización que aloja sus registros de DNS públicos.

  - Para los fines de este tema, se creó una confianza de federación existente con la siguiente configuración:
    
      - **Contoso.com** es el dominio compartido primario para la confianza de federación. (Este dominio no se cambiará.)
    
      - Los dominios federados **service.contoso.com** y **sales.contoso.com** se incluyen en la confianza de federación existente.
    
      - **Marketing.contoso.com** es un dominio aceptado en la organización de Exchange.

  - Este tema también trata otras tareas de administración de la federación, como la visualización y administración de certificados que se usan para la confianza de federación y la visualización de la información del parámetro de confianza de federación en el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Usar el EMC para administrar una confianza de federación

1.  En un servidor Exchange 2013 en su organización local, vaya a **Organización** \> **Uso compartido**.

2.  En la sección **Confianza de federación**, haga clic en **Modificar**.

3.  En **Dominios habilitados para uso compartido**, omita el **Paso 1** ya que el dominio compartido primario no se carga.

4.  En el **Paso 2**, seleccione el dominio **service.contoso.com** y, a continuación, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") para quitar el dominio de la confianza federada.

5.  En el **Paso 2**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

6.  En **Selecciona dominios aceptados** , seleccione **marketing.contoso.com** de la lista de dominios aceptados y, a continuación, haga clic en **Aceptar** para agregar el dominio a la confianza federada.
    

    > [!IMPORTANT]
    > Se creará una cadena de prueba de dominio federada para el dominio <STRONG>marketing.contoso.com</STRONG>. Debe crear un registro TXT independiente en su DNS público para este dominio.



7.  Usando la cadena de prueba de dominio creada para el dominio **marketing.contoso.com**, cree un registro TXT en su servidor de DNS público. Según la programación de actualizaciones de su host DNS público, la replicación de los cambios de DNS puede tardar 15 minutos o más.

8.  Tras la creación y replica del registro TXT, haga clic en **Actualizar**.

## Usar el Shell para administrar una confianza de federación

1.  Este ejemplo quita el dominio de service.contoso.com de la confianza de federación.
    
        Remove-FederatedDomain -DomainName service.contoso.com

2.  Este ejemplo agrega el dominio marketing.contoso.com a la confianza de federación.
    
        Add-FederatedDomain -DomainName marketing.contoso.com

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Remove-FederatedDomain](https://technet.microsoft.com/es-es/library/dd298128\(v=exchg.150\)) y [Add-FederatedDomain](https://technet.microsoft.com/es-es/library/dd351208\(v=exchg.150\)).

Ejecute los comandos de Shell siguientes para administrar otros aspectos de una confianza de federación:

1.  **Ver el "OrgID" federado y los dominios federados**
    
    En este ejemplo se muestra el "OrgId" federado de la organización de Exchange y otra información relacionada, incluyendo los dominios federados y el estado.
    
        Get-FederatedOrganizationIdentifier

2.  **Visualización de certificados de federación**
    
    En este ejemplo se muestra el certificado anterior, el actual y el posterior que usa la confianza de federación "Autenticación de Azure AD".
    
        Get-FederationTrust "Azure AD authentication" | Select Org*certificate

3.  **Consulta del estado de los certificados de federación**
    
    En este ejemplo se muestra el estado de los certificados de federación de todos los servidores de buzones de correo y de acceso de clientes de la organización.
    
        Test-FederationTrustCertificate

4.  **Configuración de la confianza de federación para usar un certificado como certificado siguiente**
    
    En este ejemplo se configura la confianza de federación "Autenticación de Azure AD" para usar el certificado con la huella digital como certificado siguiente. Una vez implementado el certificado en todos los servidores de Exchange de la organización, puede usar el conmutador *PublishCertificate* para configurar la confianza de federación y usar este certificado como el certificado actual.
    
        Set-FederationTrust "Azure AD authentication" -Thumbprint AC00F35CBA8359953F4126E0984B5CCAFA2F4F17

5.  **Configuración de la confianza de federación para usar el certificado siguiente como certificado actual**
    
    En este ejemplo se configura la confianza de federación "Autenticación de Azure AD" para usar el certificado siguiente como certificado actual, y la publica en el sistema de autenticación de Azure AD.
    
        Set-FederationTrust "Azure AD authentication" -PublishFederationCertificate
    

    > [!WARNING]
    > Antes de configurar la confianza de federación para usar el certificado posterior como certificado actual, debe comprobar que el certificado esté implementado en todos los servidores de Exchange de su organización. Use el cmdlet <A href="https://technet.microsoft.com/es-es/library/dd335228(v=exchg.150)">Test-FederationTrustCertificate</A> para comprobar el estado de implementación del certificado.



6.  **Actualizar los metadatos de federación y el certificado desde el sistema de autenticación de Azure AD**
    
    En este ejemplo se actualizan los metadatos de federación y el certificado del sistema de autenticación de Azure AD para la confianza de federación "Autenticación de Azure AD".
    
        Set-FederationTrust "Azure AD authentication" -RefreshMetadata

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [Get-FederatedOrganizationIdentifier](https://technet.microsoft.com/es-es/library/dd298149\(v=exchg.150\))

  - [Get-FederationTrust](https://technet.microsoft.com/es-es/library/dd351262\(v=exchg.150\))

  - [Test-FederationTrustCertificate](https://technet.microsoft.com/es-es/library/dd335228\(v=exchg.150\))

  - [Set-FederationTrust](https://technet.microsoft.com/es-es/library/dd298034\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

La finalización correcta del Asistente para **Dominios habilitados para uso compartido** es su primera indicación de que ha configurado la confianza de federación correctamente.

Para comprobarlo todavía más, haga lo siguiente:

1.  Ejecute el siguiente comando de Shell para verificar la información de confianza de federación.
    
        Get-FederationTrust | format-list

2.  Ejecute el siguiente comando de Shell para verificar que se puede recuperar la información de la federación de su organización. Por ejemplo, para comprobar que los dominios sales.contoso.com y marketing.contoso.com se devuelven en el parámetro *DomainNames*.
    
        Get-FederationInformation -DomainName <your primary sharing domain>


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


