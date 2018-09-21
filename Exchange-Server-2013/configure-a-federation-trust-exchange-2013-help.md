---
title: 'Configurar una confianza de federación: Exchange 2013 Help'
TOCTitle: Configurar una confianza de federación
ms:assetid: 7c2b539f-faed-4374-8578-9f329ca628db
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657462(v=EXCHG.150)
ms:contentKeyID: 49895735
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar una confianza de federación

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-07-26_

Una confianza de federación establece una relación de confianza entre una organización de Exchange 2013 de Microsoft y el sistema de autenticación de Azure Active Directory. Al configurar una confianza de federación, podrá configurar el uso compartido federado con otras organizaciones federadas de Exchange y compartir la información de calendarios de disponibilidad entre los destinatarios. El uso compartido federado se puede configurar entre dos organizaciones de Exchange 2013 federadas o entre una organización de Exchange 2013 federada y otras organizaciones de Exchange 2010 federadas. También puede configurar el uso compartido con una organización de Office 365.


> [!NOTE]
> Crear una confianza de federación es uno de los varios pasos que se deben seguir para configurar el uso compartido en su organización de Exchange. Para revisar todos los pasos, consulte <A href="configure-federated-sharing-exchange-2013-help.md">Configuración del uso compartido federado</A>.



Para otras tareas de administración relacionadas con la federación, consulte [Procedimientos de la Federación](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esta característica de Exchange Server 2013 no es totalmente compatible con Office 365 operado por 21Vianet en China y pueden aplicarse ciertas limitaciones en las características. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/?linkid=313640">Acerca de Office 365 operado por 21Vianet</A>.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  30 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada de permisos de "Federación y certificados" en el tema de [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) .

  - El dominio utilizado para establecer una confianza de federación debe poder resolverse desde Internet. Esto requiere que el dominio se registre en un registrador de dominios y que la zona DNS del dominio se hospede en un servidor DNS al que se pueda obtener acceso desde Internet. Si la organización recibe correo electrónico de Internet para el dominio, ya se cumplen estos requisitos.

  - Necesitará agregar un registro TXT a su DNS público. Revise los requisitos para agregar un registro TXT con la organización que aloja sus registros de DNS públicos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Ambas organizaciones de Exchange de una relación de uso compartido federado deben usar el mismo sistema de autenticación de Azure AD para sus confianzas de federación. Este requisito se aplica cuando se configura el uso compartido federado entre dos organizaciones de Exchange local o entre una organización de Exchange local y una organización de Exchange hospedada por [Office 365](https://go.microsoft.com/fwlink/?linkid=392576).

  - Al crear una confianza de federación con el sistema de autenticación de Azure AD para la organización de Exchange 2013, la confianza de federación usará la instancia de empresa del sistema de autenticación de Azure AD. Sin embargo, otras organizaciones federadas de Exchange con versiones anteriores de Exchange y confianzas de federación existentes podrán utilizar la instancia de empresa o de usuario del sistema de autenticación de Azure AD.
    
    Las organizaciones de Exchange indicadas a continuación usan de forma predeterminada la instancia de empresa del sistema de autenticación de Azure AD:
    
      - Exchange 2013 organizaciones que utilizan el Asistente **Habilitar la confianza de federación** y certificados autofirmados para una confianza de federación.
    
      - Las organizaciones de Exchange 2010 SP1 o posterior mediante el asistente **Nueva confianza de federación** y certificados autofirmados para una confianza de federación.
    
      - Las organizaciones de Exchange hospedadas por Office 365, como Exchange Online.
    
    Las organizaciones de Exchange indicadas a continuación usan de forma predeterminada la instancia de usuario del sistema de autenticación de Azure AD:
    
      - La versión RTM de organizaciones de Exchange 2010 que usan certificados emitidos por otras entidades de certificación.
    
    Se recomienda que todas las organizaciones de Exchange usen la instancia de empresa del sistema de autenticación de Azure AD para las confianzas de federación. Antes de configurar el uso compartido federado entre las dos organizaciones de Exchange, debe comprobar qué instancia del sistema de autenticación de Azure AD está usando cada organización de Exchange para cualquier confianza de federación existente. Para determinar qué instancia del sistema de autenticación de Azure AD está usando una organización de Exchange para una confianza de federación existente, ejecute el siguiente comando de Shell.
    
    ```powershell
Get-FederationInformation -DomainName <hosted Exchange domain namespace>
```
    
    La instancia de empresa devuelve un valor de `<uri:federation:MicrosoftOnline>` para el parámetro *TokenIssuerURIs*.
    
    La instancia de usuario devuelve un valor de `<uri:WindowsLiveID>` para el parámetro *TokenIssuerURIs*.
    
    Para configurar compartir federado con una organización Exchange que tiene una confianza de federación existente que está utilizando la instancia de negocio del sistema de autenticación Azure AD, siga los pasos descritos en este tema. Estos pasos son todo lo que necesita realizar para crear confianzas de federación que pueden utilizarse para habilitar compartir federada entre dos organizaciones Exchange 2013 o entre una organización de Exchange 2013 y una organización Exchange 2010 que ya está utilizando el instancia de negocio del sistema de autenticación Azure AD.
    
    Para configurar el uso compartido federado entre su organización de Exchange 2013 y una organización de Exchange que tiene una confianza de federación existente y utiliza la instancia de usuario del sistema de autenticación de Azure AD, la organización de Exchange que utiliza la instancia de usuario debe instalar Exchange 2010 SP2 o posterior, o bien actualizar a Exchange 2013. Si decide instalar Exchange 2010 SP2 o posterior, utilice el Asistente **Nueva confianza de federación** para eliminar y volver a crear los dominios y confianzas de federación federadas ya existentes. Al volver a crear las confianzas de federación, se usará la instancia de empresa del sistema de autenticación de Azure AD.

## Usar el EAC para crear y configurar una confianza de federación

1.  En un servidor de Exchange 2013 de la organización local, navegue hasta **Organización** \> **Uso compartido**.

2.  Haga clic en **Habilitar** para iniciar el Asistente **Habilitar confianza de federación**.

3.  Una vez finalizado el asistente, haga clic en **Cerrar**.

4.  En la sección **Confianza de federación** de la ficha **Uso compartido**, haga clic en **Modificar**.

5.  En **Dominios habilitados para uso compartido**, junto a **Paso 1**, haga clic en **Examinar**.

6.  En **Seleccionar dominios aceptados**, seleccione el dominio compartido principal en la lista y, a continuación, haga clic en **Aceptar**.
    

    > [!NOTE]
    > El dominio seleccionado se utilizará para configurar el OrgId de la confianza de federación. Para obtener más información acerca de OrgId, consulte <A href="federation-exchange-2013-help.md">Federación</A>.



7.  Tome nota de la prueba de dominio federado que se genera para el dominio principal compartido. Podrá utilizar esta cadena para crear un registro TXT en el servidor DNS público.
    

    > [!IMPORTANT]
    > La prueba de dominio federado es una cadena de caracteres alfanuméricos. Para evitar errores de entrada, se recomienda copiar la cadena de la EAF y pegarlo en un editor de texto como el Bloc de notas. Puede copiar desde el editor de texto en el Portapapeles y, a continuación, péguelo en el campo de <STRONG>texto</STRONG> al crear el registro TXT. Si el registro TXT se crea utilizando una incorrecta federados cadena de prueba de dominio, el sistema de autenticación Azure AD no podrá comprobar la prueba de propiedad del dominio y no podrá agregarlo al identificador de organización federada.



8.  En el **paso 2**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar dominios adicionales a la confianza federada para las direcciones de correo electrónico que será utilizada por los usuarios de la organización que requieren características de uso compartidos federados. Por ejemplo, si tiene usuarios que usan un subdominio de su dirección de correo electrónico como sales.contoso.com, agregaría el dominio sales.contoso.com a la confianza de federación.
    

    > [!NOTE]
    > Se creará una prueba de dominio federado para cada dominio adicional seleccionado. Deberá crear registros TXT por separado en su DNS público para cada dominio adicional.



9.  Con las cadenas de las pruebas de dominio federado de cada dominio, cree registros TXT para cada uno de dichos dominios en su servidor DNS público. Según la programación de actualizaciones de su host DNS público, la replicación de los cambios de DNS puede tardar 15 minutos o más.

10. Después de crear y replicar los registros TXT, haga clic en **Actualizar**.

## Usar el Shell para crear y configurar una confianza de federación

1.  Ejecute este comando para crear un identificador de clave de asunto único para el certificado de confianza de federación:
    
        $ski = [System.Guid]::NewGuid().ToString("N")

2.  Para crear un certificado autofirmado para la confianza de federación, utilice esta sintaxis:
    
        New-ExchangeCertificate -FriendlyName "<Descriptive Name>" -DomainName <domain> -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
    
    Este ejemplo crea un certificado autofirmado para la confianza de federación con el sistema de autenticación Azure AD. El certificado utiliza el valor de nombre descriptivo federados uso compartido de Exchange y se recupera el valor del dominio de la variable de entorno **USERDNSDOMAIN** .
    
        New-ExchangeCertificate -FriendlyName "Exchange Federated Sharing" -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski

3.  Para crear la confianza de federación e implementar automáticamente el certificado autofirmado que creó en el paso anterior a los servidores de Exchange en su organización, utilice esta sintaxis:
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "<FriendlyName>"} | New-FederationTrust -Name "<Descriptive Name>"
    
    Este ejemplo crea la confianza de federación denominada Azure autenticación de Active Directory y despliega el certificado autofirmado denominado federados uso compartido de Exchange.
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "Exchange Federated Sharing"} | New-FederationTrust -Name "Azure AD Authentication"

4.  Utilice esta sintaxis para devolver la prueba de propiedad de dominio registro TXT que resulta necesario para cualquier dominio que se configurará para la confianza de federación.
    
    ```powershell
Get-FederatedDomainProof -DomainName <domain>
```
    
    Este ejemplo devuelve la prueba de propiedad de dominio registro TXT que se requiere para el dominio compartido principal contoso.com.
    
    ```powershell
Get-FederatedDomainProof -DomainName contoso.com
```
    
    **Notas**:
    
      - Cada dominio o subdominio que esté configurado para la confianza de federación requiere una prueba de propiedad del dominio registro TXT, por lo que tendrá que ejecutar este comando varias veces con valores diferentes de *DomainName* .
    
      - Se recomienda que copie la cadena de prueba de dominio haciendo clic en el Shell, seleccione **marca**, seleccionando el valor de **prueba** y presionando ENTRAR, por lo que puede utilizar al crear el registro TXT. Si se crea el registro TXT con una cadena de prueba de dominio federado incorrecta, el sistema de autenticación de Azure AD no puede comprobar la propiedad del dominio y no podrá agregarlo al identificador de organización federada.

5.  Con la información del paso anterior, cree registros TXT en el servidor DNS público en cada dominio que se incluirán en la confianza de federación. Dependiendo de la programación de actualización de los host DNS público, replicación de los cambios DNS puede tardar 15 minutos o más. Continuar después de haber comprobado que los nuevos registros TXT están disponibles.

6.  Ejecute este comando para recuperar los metadatos y el certificado de Azure AD:
    
    ```powershell
Set-FederationTrust -RefreshMetadata -Identity "Azure AD authentication"
```

7.  Utilice esta sintaxis para configurar el dominio principal compartido para la confianza de federación que creó en el paso 3. El dominio que especifique se utilizará para configurar el identificador de la organización (OrgID) para la confianza de federación. Para obtener más información acerca de la OrgID, vea el [identificador de organización federada](federation-exchange-2013-help.md).
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "<Federation Trust Name>" -AccountNamespace <Accepted Domain> -Enabled $true
    
    Este ejemplo configura el dominio aceptado contoso.com como la principal comparte el dominio de confianza de federación denominado Azure autenticación de Active Directory.
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "Azure AD authentication" -AccountNamespace contoso.com -Enabled $true

8.  Para agregar otros dominios a la confianza de federación, utilice esta sintaxis:
    
    ```powershell
Add-FederatedDomain -DomainName <AdditionalDomain>
```
    
    Este ejemplo agrega el sales.contoso.com subdominio a la confianza federada, porque los usuarios con direcciones de correo electrónico en el dominio sales.contoso.com requieren características de uso compartidos federados.
    
    ```powershell
Add-FederatedDomain -DomainName sales.contoso.com
```
    
    Recuerde que cualquier dominio o subdominio que agregue a la confianza de federación requiere una prueba de propiedad del dominio registro TXT,

Para información sobre parámetros y la sintaxis detallada, consulte [New-ExchangeCertificate](https://technet.microsoft.com/es-es/library/aa998327\(v=exchg.150\)), [New-FederationTrust](https://technet.microsoft.com/es-es/library/dd351047\(v=exchg.150\)), [Get-FederatedDomainProof](https://technet.microsoft.com/es-es/library/ff717833\(v=exchg.150\)), [Set-FederationTrust](https://technet.microsoft.com/es-es/library/dd298034\(v=exchg.150\)), [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/es-es/library/dd351037\(v=exchg.150\))y [Add-FederatedDomain](https://technet.microsoft.com/es-es/library/dd351208\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Cuando finalicen correctamente los asistentes **Habilitar confianza de federación** y **Dominios habilitados para uso compartido** deberá interpretarlo como la primera indicación de que la confianza de federación se ha configurado tal como esperaba.

Para verificar con más detalle que ha creado y configurado correctamente la confianza de federación, realice lo siguiente:

1.  Ejecute el siguiente comando de Shell para verificar la información de confianza de federación.
    
    ```powershell
Get-FederationTrust | Format-List
```

2.  Reemplace *\<PrimarySharedDomain\>* con su dominio principal compartido y ejecute el siguiente comando de Shell para comprobar que se puede recuperar la información de federación de la organización.
    
    ```powershell
Get-FederationInformation -DomainName <PrimarySharedDomain>
```

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-FederationTrust](https://technet.microsoft.com/es-es/library/dd351262\(v=exchg.150\)) y [Get-FederationInformation](https://technet.microsoft.com/es-es/library/dd351221\(v=exchg.150\)).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


