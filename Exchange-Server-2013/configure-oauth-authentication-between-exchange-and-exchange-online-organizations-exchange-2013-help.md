---
title: 'Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online: Exchange 2013 Help'
TOCTitle: Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online
ms:assetid: f703e153-98e2-4268-8a6e-07a86b0a1d22
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn594521(v=EXCHG.150)
ms:contentKeyID: 61170824
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Solo en las implementaciones híbridas de Exchange 2013 se configura la autenticación de OAuth cuando se usa el asistente de configuración híbrida. En las implementaciones híbridas mixtas de Exchange 2013/2010 y Exchange 2013/2007, el asistente de configuración híbrida no configura la nueva conexión de autenticación basada en OAuth de la implementación híbrida entre Office 365 y las organizaciones locales de Exchange. Estas implementaciones seguirán usando de forma predeterminada el proceso de la confianza de federación. No obstante, ciertas características de Exchange 2013 solo se encuentran totalmente disponibles en una organización si se usa el nuevo protocolo de autenticación de OAuth de Exchange.

Actualmente, el nuevo proceso de autenticación de OAuth de Exchange habilita las características de Exchange siguientes:

  - Administración de registros de mensajes (MRM)

  - Exhibición de documentos electrónicos local

  - Archivado local de Exchange

Se recomienda que todas las organizaciones mixtas de Exchange que configuran una implementación híbrida con Exchange 2013 y Exchange Online definan la autenticación de OAuth de Exchange tras establecer la implementación híbrida con el asistente de configuración híbrida.


> [!IMPORTANT]
> Si su organización local solo ejecuta servidores de Exchange 2013 con la actualización acumulativa 5 o posterior instalada, ejecute al Asistente para implementación híbrida en lugar de realizar los pasos que se describen en este tema.<BR>Esta característica de Exchange Server 2013 no es totalmente compatible con Office 365 operado por 21Vianet en China y pueden aplicarse ciertas limitaciones en las características. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/?linkid=313640">Acerca de Office 365 operado por 21Vianet</A>.



## ¿Qué es necesario saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Permisos de certificados y federación" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Haber completado la configuración de la implementación híbrida por medio del asistente de configuración híbrida. Para obtener más información, consulte [Implementaciones híbridas de Exchange Server](https://technet.microsoft.com/es-es/library/jj200581\(v=exchg.150\)).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo se configura la autenticación OAuth entre organizaciones de Exchange locales y de Exchange Online?

## Paso 1: Crear un objeto de servidor de autorización para la organización de Exchange Online

En este procedimiento hay que especificar un dominio comprobado para la organización de Exchange Online. Este dominio debe ser el mismo que el que se usó como dominio SMTP principal en las cuentas de correo electrónico en la nube. Durante este procedimiento, se hará referencia a este dominio como *\<su dominio comprobado\>*.

Ejecute el siguiente comando en el Shell de administración de Exchange (Exchange PowerShell) en la organización de Exchange local.

    New-AuthServer -Name "WindowsAzureACS" -AuthMetadataUrl https://accounts.accesscontrol.windows.net/<your verified domain>/metadata/json/1

## Paso 2: Habilitar la aplicación de socio para la organización de Exchange Online

Ejecute el siguiente comando en Exchange PowerShell en la organización de Exchange local.

    Get-PartnerApplication |  ?{$_.ApplicationIdentifier -eq "00000002-0000-0ff1-ce00-000000000000" -and $_.Realm -eq ""} | Set-PartnerApplication -Enabled $true

## Paso 3: Exportar el certificado de autorización local

En este paso, hay que ejecutar un script de PowerShell para exportar el certificado de autorización local, que se importará a continuación a la organización de Exchange Online en el siguiente paso.

1.  Guarde el siguiente texto en un archivo de script de PowerShell llamado, por ejemplo, **ExportAuthCert.ps1**.
    
        $thumbprint = (Get-AuthConfig).CurrentCertificateThumbprint
         
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
         
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.Thumbprint -match $thumbprint}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)

2.  En Exchange PowerShell en la organización de Exchange local, ejecute el script de PowerShell que creó en el paso anterior. Por ejemplo:
    
        .\ExportAuthCert.ps1

## Paso 4: Cargar el certificado de autorización local en ACS de Azure Active Directory

A continuación, tiene que usar Windows PowerShell para cargar el certificado de autorización local que exportó en el paso anterior a Servicios de control de acceso (ACS) de Azure Active Directory. Para ello, tienen que instalarse los cmdlets de Módulo Azure Active Directory para Windows PowerShell. Si no están instalados, vaya a <https://aka.ms/aadposh> para instalar el Módulo Azure Active Directory para Windows PowerShell. Una vez instalado el Módulo Azure Active Directory para Windows PowerShell, complete los siguientes pasos.

1.  Haga clic en el acceso directo del **Módulo Azure Active Directory para Windows PowerShell** para abrir un área de trabajo de Windows PowerShell que tenga los cmdlets de Azure AD instalados. Todos los comandos de este paso se ejecutarán mediante la consola de Windows PowerShell para Azure Active Directory.

2.  Guarde el siguiente texto en un archivo de script de PowerShell llamado, por ejemplo, **UploadAuthCert.ps1**.
    
        Connect-MsolService;
        Import-Module msonlineextended;
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        $objFSO = New-Object -ComObject Scripting.FileSystemObject;
        $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
        $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
        $cer.Import($CertFile);
        $binCert = $cer.GetRawCertData();
        $credValue = [System.Convert]::ToBase64String($binCert);
        
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
        New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue

3.  Ejecute el script de PowerShell que creó en el paso anterior. Por ejemplo:
    
        .\UploadAuthCert.ps1

4.  Después de iniciar el script, se abre un cuadro de diálogo de credenciales. Escriba las credenciales de la cuenta de administrador de inquilinos de la organización de Microsoft Online Azure AD. Tras ejecutar el script, deje abierta la sesión de Windows PowerShell para Azure AD. La usará para ejecutar un script de PowerShell en el paso siguiente.

## Paso 5: Registrar todas las autoridades de nombre de host de los extremos HTTP de Exchange local externos con Azure Active Directory

Deberá ejecutar el script en este paso por cada extremo de la organización de Exchange local al que se vaya a poder acceder públicamente. Recomendamos usar comodines en la medida de lo posible. Imaginemos, por ejemplo, que Exchange está disponible externamente en **https://mail.contoso.com/ews/exchange.asmx**. En este caso, podría usarse un solo comodín: **\*.contoso.com**. Esto incluiría los extremos autodiscover.contoso.com y mail.contoso.com. Sin embargo, no incluye el dominio de nivel superior, **contoso.com**. En los casos en los que se pueda acceder externamente a los servidores de acceso de cliente de Exchange 2013 con la autoridad de nombre de host de primer nivel, esta autoridad de nombre de host también deberá registrarse como **contoso.com**. No existe un límite para registrar autoridades de nombre de host externas adicionales.

Si no está seguro de los extremos de Exchange externos en la organización de Exchange local, puede obtener una lista de los extremos de servicios web configurados externos ejecutando el siguiente comando en Exchange PowerShell en la organización de Exchange local:

    Get-WebServicesVirtualDirectory | FL ExternalUrl


> [!NOTE]
> Para poder ejecutar el siguiente script correctamente, es necesario que Windows&nbsp;PowerShell para Azure Active Directory esté conectado al inquilino de Microsoft&nbsp;Online Azure AD, como se explicó en el paso&nbsp;4 de la sección anterior.



1.  Guarde el siguiente texto en un archivo de script de PowerShell llamado, por ejemplo, **RegisterEndpoints.ps1**. En este ejemplo se usa un comodín para registrar todos los extremos de contoso.com. Reemplace **contoso.com** por una autoridad de nombre de host de la organización de Exchange local.
    
        $externalAuthority="*.contoso.com"
         
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
         
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName;
         
        $spn = [string]::Format("{0}/{1}", $ServiceName, $externalAuthority);
        $p.ServicePrincipalNames.Add($spn);
         
        Set-MsolServicePrincipal -ObjectID $p.ObjectId -ServicePrincipalNames $p.ServicePrincipalNames;

2.  En Windows PowerShell para Azure Active Directory, ejecute el script de Windows PowerShell que creó en el paso anterior. Por ejemplo:
    
        .\RegisterEndpoints.ps1

## Paso 6: Crear un IntraOrganizationConnector entre la organización local y Office 365

Se debe definir una dirección de destino para los buzones que se hospedan en Exchange Online. Esta dirección de destino se crea automáticamente al crear el inquilino de Office 365. Por ejemplo, si el dominio de una organización hospedado en el inquilino de Office 365 es "contoso.com", la dirección de servicio de destino será "contoso.mail.onmicrosoft.com".

Con Exchange PowerShell, ejecute el siguiente cmdlet en la organización local:

    New-IntraOrganizationConnector -name ExchangeHybridOnPremisesToOnline -DiscoveryEndpoint https://outlook.office365.com/autodiscover/autodiscover.svc -TargetAddressDomains <your service target address>

## Paso 7: Crear un IntraOrganizationConnector entre el inquilino de Office 365 y la organización de Exchange local

Se debe definir una dirección de destino para los buzones que se hospedan en la organización local. Si la dirección SMTP principal de la organización es "contoso.com", sería "contoso.com".

También hay que definir un extremo externo de detección automática para la organización local. Si su compañía es "contoso.com", sería por lo general uno de los siguientes:

  - https://autodiscover.\<su dominio SMTP principal\>/autodiscover/autodiscover.svc

  - https://\<su dominio SMTP principal\>/autodiscover/autodiscover.svc


> [!NOTE]
> Puede usar el cmdlet <A href="https://technet.microsoft.com/es-es/library/dn551183(v=exchg.150)">Get-IntraOrganizationConfiguration</A> en los inquilinos tanto local como de Office&nbsp;365 para averiguar cuáles son los valores de extremo que el cmdlet <A href="https://technet.microsoft.com/es-es/library/dn551178(v=exchg.150)">New-IntraOrganizationConnector</A> necesita.



Con Windows PowerShell, ejecute el siguiente cmdlet:

    $UserCredential = Get-Credential
    
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    
    Import-PSSession $Session
    
    New-IntraOrganizationConnector -name ExchangeHybridOnlineToOnPremises -DiscoveryEndpoint <your on-premises Autodiscover endpoint> -TargetAddressDomains <your on-premises SMTP domain>

## Paso 8: Configurar un AvailabilityAddressSpace para los servidores anteriores a Exchange 2013 SP1

Al configurar una implementación híbrida en una organización anterior a Exchange 2013, debe instalar al menos un servidor de Exchange 2013 SP1 (o superior) con los roles de servidor de Buzón de correo y Acceso de clientes en la organización de Exchange existente. Los servidores de Buzón de correo y Acceso de clientes de Exchange 2013 actúan como servidores front-end y coordinan las comunicaciones entre la organización local de Exchange existente y la organización de Exchange Online. En estas comunicaciones se incluyen las características de mensajería y transporte de mensajes entre la organización local y de Exchange Online. Se recomienda instalar varios servidores de Exchange 2013 en la organización local para aumentar la fiabilidad y la disponibilidad de las características de la implementación híbrida.

En las implementaciones mixtas con Exchange 2013/2010 o Exchange 2013/2007, se recomienda establecer todos los servidores front-end con conexión a Internet de la organización local como servidores de Acceso de clientes que ejecutan Exchange 2013 SP1 o una versión posterior. Todas las solicitudes de servicios Web Exchange (EWS) procedentes de Office 365 y Exchange Online deben conectarse a uno o varios servidores de Acceso de clientes de Exchange 2013 de la implementación local. Además, todas las solicitudes de EWS procedentes de las organizaciones de Exchange locales para Exchange Online deben redirigirse mediante proxy a través de un servidor de Acceso de clientes que ejecute Exchange 2013 SP1 o una versión posterior. Como los servidores de Acceso de clientes de Exchange 2013 deben controlar estas solicitudes adicionales entrantes y salientes, es importante disponer de un número suficiente de servidores de Acceso de clientes de Exchange 2013 para controlar la carga de procesamiento y permitir la redundancia de la conexión. El número de servidores de Acceso de clientes necesario dependerá de la cantidad media de solicitudes de EWS y variará en función de la organización.

Antes de realizar el paso siguiente, compruebe que:

  - Los servidores híbridos de front-end son de Exchange 2013 SP1 o una versión posterior.

  - Solo dispone de una dirección URL de EWS externa para el o los servidores de Exchange 2013. El inquilino de Office 365 debe conectarse a estos servidores para que funcionen correctamente las solicitudes basadas en la nube de las características híbridas.

  - Los servidores disponen de los roles de servidor Buzón de correo y Acceso de clientes.

  - En todos los servidores de Buzón de correo y Acceso de clientes de Exchange 2010/2007 se ha aplicado el Service Pack (SP) o la actualización acumulativa (CU) más reciente.
    

    > [!NOTE]
    > En el caso de las conexiones de características de implementaciones no híbridas, los servidores existentes de Buzón de correo de Exchange 2010/2007 pueden seguir usando servidores de Acceso de clientes de Exchange 2010/2007 para los servidores de front-end. Solo las solicitudes de características de implementaciones híbridas del inquilino de Office 365 precisan conexión a servidores de Exchange&nbsp;2013.



En los servidores de Acceso de clientes anteriores a Exchange 2013, debe configurarse *AvailabilityAddressSpace* para apuntar al extremo de los servicios Web Exchange de los servidores locales de Acceso de clientes de Exchange 2013 SP1. Este extremo es el que se ha descrito anteriormente en el paso 5, aunque también puede determinarse ejecutando el cmdlet siguiente en el servidor local de Acceso de clientes de Exchange 2013 SP1:

    Get-WebServicesVirtualDirectory | FL AdminDisplayVersion,ExternalUrl


> [!NOTE]
> Si se devuelve información de directorios virtuales de varios servidores, asegúrese de usar un extremo que se haya devuelto para un servidor de Acceso de clientes de Exchange&nbsp;2013 SP1. Mostrará 15.0 (compilación 847.32) o posterior para el parámetro <EM>AdminDisplayVersion</EM>.



Para configurar el *AvailabilityAddressSpace*, use Exchange PowerShell y ejecute el siguiente cmdlet en su organización local:

    Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl <your on-premises External Web Services URL> -ForestName <your Office 365 service target address> -UseServiceAccount $True

## ¿Cómo saber si el proceso se completó correctamente?

Para confirmar si la configuración de OAuth es correcta se usa el cmdlet [Test-OAuthConnectivity](https://technet.microsoft.com/es-es/library/jj218623\(v=exchg.150\)). Este cmdlet comprueba que los extremos de Exchange Online y la implementación local de Exchange pueden autenticar correctamente las solicitudes que se envían entre sí.


> [!IMPORTANT]
> Cuando se conecte a la organización de Exchange Online con PowerShell en remoto, tal vez deba usar el parámetro <EM>AllowClobber</EM> con el cmdlet <STRONG>Import-PSSession</STRONG> para importar los últimos comandos a la sesión local de PowerShell.



Para comprobar si la organización local de Exchange puede conectarse correctamente a Exchange Online, ejecute el comando siguiente en Exchange PowerShell en la organización local:

    Test-OAuthConnectivity -Service EWS -TargetUri https://outlook.office365.com/ews/exchange.asmx -Mailbox <On-Premises Mailbox> -Verbose | fl

Para comprobar si la organización de Exchange Online puede conectarse correctamente a la organización local de Exchange, use [PowerShell en remoto](https://technet.microsoft.com/es-es/library/jj984289\(v=exchg.150\)) para conectarse a la organización de Exchange Online y ejecute el comando siguiente:

    Test-OAuthConnectivity -Service EWS -TargetUri <external hostname authority of your Exchange On-Premises deployment>/metadata/json/1 -Mailbox <Exchange Online Mailbox> -Verbose | fl

Así, por ejemplo, Test-OAuthConnectivity -Service EWS -TargetUri https://lync.contoso.com/metadata/json/1 -Mailbox ExchangeOnlineBox1 -Verbose | fl


> [!IMPORTANT]
> Ignore el error “La dirección&nbsp;SMTP no tiene ningún buzón asociado con ella”; lo único importante es que el parámetro <EM>ResultTask</EM> devuelva un valor <STRONG>Success</STRONG>. Por ejemplo, la última sección de la salida de la prueba debería reflejar lo siguiente:<BR><CODE>ResultType: Success</CODE><BR><CODE>Identity: Microsoft.Exchange.Security.OAuth.ValidationResultNodeId</CODE><BR><CODE>IsValid: True</CODE><BR><CODE>ObjectState: New</CODE>




> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


