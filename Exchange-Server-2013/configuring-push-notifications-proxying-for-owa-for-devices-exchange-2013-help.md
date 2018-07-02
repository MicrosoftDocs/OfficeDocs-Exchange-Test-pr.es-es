---
title: 'Configuración del proxy de notificaciones de inserción para OWA para dispositivos: Exchange 2013 Help'
TOCTitle: Configuración del proxy de notificaciones de inserción para OWA para dispositivos
ms:assetid: c0f4912d-8bd3-4a54-9097-03619c645c6a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn511017(v=EXCHG.150)
ms:contentKeyID: 59954255
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración del proxy de notificaciones de inserción para OWA para dispositivos

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Cuando se habilitan las notificaciones de inserción para OWA para dispositivos (OWA para iPhone y OWA para iPad) en una implementación local de Microsoft Exchange 2013, el icono de Outlook Web App en el OWA para iPhone y el OWA para iPad del usuario se actualiza para indicar el número de mensajes no leídos en la bandeja de entrada del usuario. Si las notificaciones de inserción no se configuran ni se habilitan, un usuario que tenga OWA para dispositivos no podrá saber que tiene mensajes no leídos en la bandeja de entrada a menos que inicie la aplicación. Cuando se recibe un nuevo mensaje, la notificación de OWA para dispositivos se actualiza en el dispositivo del usuario, con un aspecto similar a este.

![OWA para distintivo de dispositivos](images/Dn511017.f399ba74-5395-4d24-ae7d-d16bf0ac7b35(EXCHG.150).png "OWA para distintivo de dispositivos")

## ¿Cómo habilitar las notificaciones de inserción?

Para habilitar las notificaciones de inserción, los servidores Exchange 2013 locales deben conectarse al Servicio de notificaciones de inserción de Office 365 para poder enviar notificaciones de inserción a iPhones e iPads. Los servidores Exchange 2013 locales enrutan sus notificaciones de actualización a través de los servicios de notificación de Office 365 para que no sea necesaria la inscripción de cuentas de desarrollador a servicios de notificación de inserciones de terceros. En este diagrama te mostramos el proceso que permite que los usuarios de iPhone e iPad reciban actualizaciones en las notificaciones para mensajes no leídos.

![Proceso para notificaciones de inserción](images/Dn511017.36764ce6-7351-492f-a17e-c42b781e2781(EXCHG.150).jpg "Proceso para notificaciones de inserción")

Para habilitar las notificaciones de inserción, el administrador tiene que hacer esto:

1.  Inscribir la organización en Office 365 para empresa.

2.  Actualizar todos los servidores locales a la actualización acumulativa 3 (CU3) de Exchange Server 2013 o una versión posterior.

3.  Configurar una instancia de Exchange 2013 local en la autenticación de Office 365.

4.  Habilitar las notificaciones de inserción desde el servidor Exchange 2013 local hacia Office 365 y comprobar que estas funcionan.

## Inscribir la organización en Office 365 para empresa

Office 365 es un servicio basado en la nube, diseñado para atender las necesidades de las organizaciones en cuanto a seguridad, confiabilidad y productividad de los usuarios. Office 365 hace referencia a los planes de suscripción que incluyen acceso a las aplicaciones de Office, además de otros servicios de productividad habilitados a través de Internet (servicios de nube), como los servicios de conferencias web de Lync y los de correo electrónico para empresas hospedado por Exchange Online.

Muchos planes de Office 365 también incluyen la versión de escritorio de las aplicaciones de Office más avanzadas, para que los usuarios puedan instalarla en varios equipos y dispositivos. Todos los planes de Office 365 se pagan mediante una suscripción mensual o anual. Si quiere saber más sobre el tema o le interesa inscribir su organización en Office 365, vea [¿Qué es Office 365 para empresa?](http://go.microsoft.com/fwlink/?linkid=335705). Para más información sobre cada uno de los servicios que se ofrecen en Office 365, vea [Descripciones de servicio de Office 365](http://go.microsoft.com/fwlink/?linkid=335704).

## Actualizar a CU3 o posterior

La actualización acumulativa 3 (CU3) para Exchange Server 2013 resuelve problemas encontrados en Exchange Server 2013 desde que se lanzó el software en la versión RTM. Contiene todos los problemas y correcciones de CU1 y CU2, e incluye otras correcciones y actualizaciones desde el lanzamiento de CU2. Esta actualización es muy recomendable para todos los clientes locales de Exchange Server 2013, aunque es necesaria para las notificaciones de inserción. Si quiere conocer mejor las actualizaciones acumulativas, incluida la CU3, vea [Actualizaciones para Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

## Configurar una instancia de Exchange 2013 local en la autenticación de Office 365.

En Exchange Server 2013 se emplea un solo método estándar para la autenticación de servidor a servidor. [Exchange Server 2013](http://go.microsoft.com/fwlink/?linkid=290946) (así como [Lync Server 2013](http://go.microsoft.com/fwlink/?linkid=273796) y [SharePoint 2013](http://go.microsoft.com/fwlink/?linkid=335701)) y [Office 2013](http://go.microsoft.com/fwlink/?linkid=335696) admiten el protocolo OAuth (Open Authorization) para la autenticación y la autorización de servidor a servidor. Con OAuth, un protocolo de autorización estándar empleado en muchos de los sitios web más importantes, las credenciales y las contraseñas de los usuarios no se pasan de un equipo a otro. En lugar de eso, la autenticación y la autorización se basan en los tokens de seguridad de OAuth. Estos tokens conceden acceso a un conjunto específico de recursos durante una determinada cantidad de tiempo.

Para la autenticación de OAuth se suelen emplear tres componentes: un único servidor de autorización y los dos dominios Kerberos que necesitan comunicarse entre sí. El servidor de autorización (también conocido como el servidor de tokens de seguridad) emite los tokens de seguridad para los dos dominios Kerberos que necesitan comunicarse. Estos tokens comprueban que las comunicaciones que se originan en un dominio Kerberos sean de confianza para el otro dominio. Por ejemplo, el servidor de autorización podría emitir tokens que comprueben que los usuarios de un determinado dominio Kerberos de Lync Server 2013 pueden acceder a un dominio Kerberos de Exchange 2013 específico, y viceversa.


> [!TIP]
> Un dominio Kerberos actúa como un contenedor de seguridad.



Pero para la autenticación de un servidor local a otro servidor, no es necesario usar un servidor de tokens de terceros. Los productos de servidor, como Lync Server 2013 y Exchange 2013 tienen cada uno un servidor de tokens integrado que puede usarse para la autenticación con otros servidores Microsoft (como SharePoint Server) que admitan la autenticación de servidor a servidor. Por ejemplo, Lync Server 2013 puede emitir y firmar un token de seguridad por sí mismo, y después usarlo para comunicarse con Exchange 2013. En un caso como este, no se necesita ningún servidor de tokens de terceros.

Para configurar la autenticación de servidor a servidor para una implementación local de Exchange Server 2013 hacia Office 365, debe realizar estos dos pasos:

  -  
    **Paso 1: asigne un certificado al emisor de tokens integrado del servidor Exchange local.** En primer lugar, un administrador del servidor Exchange local debe usar este script del Shell de administración de Exchange para crear un certificado si todavía no se creó ninguno, y asignarlo al emisor de tokens integrado del servidor Exchange local. Este es un proceso de un solo paso: después de crear un certificado, deberá reutilizarse para otros escenarios de autenticación, en lugar de reemplazarlo. No olvide actualizar el valor de *$tenantDomain* de forma que refleje su nombre de dominio. Para ello, copie y pegue el siguiente código.
    

    > [!WARNING]
    > Esta acción de copiar y pegar el código en un editor de textos como el Bloc de notas, y guardarlo con una extensión .ps1, facilita la tarea de ejecutar scripts del Shell.

    
        # Make sure to update the following $tenantDomain with your Office 365 tenant domain.
        
        $tenantDomain = "Fabrikam.com"
        
        # Check whether the cert returned from Get-AuthConfig is valid and keysize must be >= 2048
        
        $c = Get-ExchangeCertificate | ?{$_.CertificateDomains -eq $env:USERDNSDOMAIN -and $_.Services -ge "SMTP" -and $_.PublicKeySize -ge 2048 -and $_.FriendlyName -match "OAuth"}
        If ($c.Count -eq 0)
        {
            Write-Host "Creating certificate for oAuth..."
            $ski = [System.Guid]::NewGuid().ToString("N")
            $friendlyName = "Exchange S2S OAuth"
            New-ExchangeCertificate -FriendlyName $friendlyName -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
            $c = Get-ExchangeCertificate | ?{$_.friendlyname -eq $friendlyName}
        }
        ElseIf ($c.Count -gt 1)
        {
            $c = $c[0]
        }
        
        $a = $c | ?{$_.Thumbprint -eq (get-authconfig).CurrentCertificateThumbprint}
        If ($a.Count -eq 0)
        {
            Set-AuthConfig -CertificateThumbprint $c.Thumbprint
        }
        Write-Host "Configured Certificate Thumbprint is:"(get-authconfig).CurrentCertificateThumbprint
        
        # Export the certificate
        
        Write-Host "Exporting certificate..."
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
        
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.FriendlyName -match "OAuth"}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)
        
        # Set AuthServer
        $authServer = Get-AuthServer MicrosoftSts;
        if ($authServer.Length -eq 0)
        {
            Write-Host "Creating AuthServer Config..."
            New-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        elseif ($authServer.AuthMetadataUrl -ne "https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain")
        {
            Write-Warning "AuthServer config already exists but the AuthMetdataUrl doesn't match the appropriate value. Updating..."
            Set-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        else
        {
            Write-Host "AuthServer Config already exists."
        }
        Write-Host "Complete."
    
    El resultado previsto debería ser similar a lo siguiente.
    
        Configured Certificate Thumbprint is: 7595DBDEA83DACB5757441D44899BCDB9911253C
        Exporting certificate...
        Complete.
    

    > [!WARNING]
    > Antes de continuar, son necesarios los cmdlets de Módulo Azure Active Directory para Windows PowerShell. Si los cmdlets de Módulo Azure Active Directory para Windows PowerShell (anteriormente conocidos como Módulo Microsoft Online Services para Windows PowerShell) no se han instalado, puede instalarlos desde <A href="http://aka.ms/aadposh">Administrar Azure AD mediante Windows PowerShell</A>.



  -  
    **Paso 2: configure Office 365 para que se comunique con el servidor Exchange 2013 local.** Configure el servidor de Office 365 con el que se comunicará el servidor Exchange 2013 para convertirse en una aplicación de socio. Por ejemplo, si el servidor Exchange 2013 local necesita comunicarse con Office 365, tendrá que configurar el servidor Exchange local como una aplicación de socio. Una aplicación de socio es cualquier aplicación con la que Exchange 2013 puede intercambiar directamente tokens de seguridad, sin tener que pasar por un servidor de tokens de seguridad de terceros. Un administrador de un servidor Exchange 2013 local debe usar este script del Shell de administración de Exchange para configurar el inquilino de Office 365 con el que se comunicará Exchange 2013 para que sea una aplicación de socio. Durante la ejecución, se mostrará un mensaje que pedirá el nombre de usuario y la contraseña del administrador del dominio de inquilino de Office 365, como por ejemplo, administrador@fabrikam.com. Asegúrese de actualizar el valor de *$CertFile* con la ubicación del certificado, si no se creó en el script anterior. Para ello, copie y pegue el siguiente código.
    
        # Make sure to update the following $CertFile with the path to the cert if not using the previous script.
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        If (Test-Path $CertFile)
        {
            $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
            $objFSO = New-Object -ComObject Scripting.FileSystemObject;
            $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
            $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
            $cer.Import($CertFile);
            $binCert = $cer.GetRawCertData();
            $credValue = [System.Convert]::ToBase64String($binCert);
        
            Write-Host "Please enter the administrator user name and password of the Office 365 tenant domain..."
        
            Connect-MsolService;
            Import-Module msonlineextended;
        
            Write-Host "Adding a key to Service Principal..."
        
            $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
            New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue -StartDate $cer.GetEffectiveDateString() -EndDate $cer.GetExpirationDateString()
        }
        Else
        {
            Write-Error "Cannot find certificate."
        } 
    
    El resultado esperado debe ser como el que mostramos aquí.
    
        Please enter the administrator user name and password of the Office 365 tenant domain...
        Adding a key to Service Principal...
        Complete.

## Habilitar la creación de conexiones proxy de notificaciones de inserción

Después de configurar correctamente la autenticación de OAuth siguiendo los pasos anteriores, un administrador local debe habilitar la creación de conexiones proxy de notificaciones de inserción mediante este script. No olvide actualizar el valor de *$tenantDomain* de forma que refleje su nombre de dominio. Para ello, copie y pegue el siguiente código.

    $tenantDomain = "Fabrikam.com"
    Enable-PushNotificationProxy -Organization:$tenantDomain

El resultado previsto debería ser similar a lo siguiente.

    RunspaceId        : 4f2eb5cc-b696-482f-92bb-5b254cd19d60
    DisplayName       : On Premises Proxy app
    Enabled           : True
    Organization      : fabrikam.com
    Uri               : https://outlook.office365.com/PushNotifications
    Identity          : OnPrem-Proxy
    IsValid           : True
    ExchangeVersion   : 0.20 (15.0.0.0)
    Name              : OnPrem-Proxy
    DistinguishedName : CN=OnPrem-Proxy,CN=Push Notifications Settings,CN=First Organization,CN=Microsoft
                        Exchange,CN=Services,CN=Configuration,DC=Domain,DC=extest,DC=microsoft,DC=com
    Guid              : 8b567958-58a4-403c-a8f0-524d7f1e9279
    ObjectCategory    : fabrikam.com/Configuration/Schema/ms-Exch-Push-Notifications-App
    ObjectClass       : {top, msExchPushNotificationsApp}
    WhenChanged       : 8/27/2013 7:23:47 PM
    WhenCreated       : 8/14/2013 1:30:27 PM
    WhenChangedUTC    : 8/28/2013 2:23:47 AM
    WhenCreatedUTC    : 8/14/2013 8:30:27 PM
    OrganizationId    :
    OriginatingServer : server.fabrikam.com
    ObjectState       : Unchanged

## Comprobar que las notificaciones de inserción funcionan

Después de completar los pasos anteriores, pruebe las notificaciones de inserción siguiendo uno de estos métodos:

  - **Enviar un mensaje de correo electrónico de prueba al buzón de correo del usuario:** 
    
    1.  Configure una cuenta en OWA para dispositivos en un dispositivo móvil para suscribirse a las notificaciones.
    
    2.  Vuelva a la pantalla de inicio del dispositivo, que pone OWA para dispositivos en segundo plano.
    
    3.  Envíe un mensaje de correo electrónico desde otro dispositivo, como un equipo de sobremesa, dirigido a la bandeja de entrada de la cuenta configurada en el dispositivo móvil.
    
    4.  El resultado debería ser una indicación con el recuento de mensajes no leídos en el icono de la aplicación en cuestión de pocos minutos.

  - **Habilitar la supervisión.** Una alternativa para probar las notificaciones de inserción, o para investigar por qué se producen errores, consiste en habilitar la supervisión en un servidor de buzones de correo de la organización. Un administrador del servidor Exchange 2013 local debe usar este script para invocar la supervisión del proxy de notificaciones de inserción. Para ello, copie y pegue el siguiente código.
    
        # Send a push notification to verify connectivity.
        
        $s = Get-ExchangeServer | ?{$_.ServerRole -match "Mailbox"}
        If ($s.Count -gt 1)
        {
            $s = $s[0]
        }
        If ($s.Count -ne 0)
        {
            # Restart the monitoring service to clear the cache from when push was previously disabled.
            Restart-Service MSExchangeHM
        
            # Give the monitoring service enough time to load.
            Start-Sleep -Seconds:120
        
            Invoke-MonitoringProbe PushNotifications.Proxy\PushNotificationsEnterpriseConnectivityProbe -Server:$s.Fqdn | fl ResultType, Error, Exception
        }
        Else
        {
            Write-Error "Cannot find a Mailbox server in the current site."
        }
    
    El resultado previsto debería ser similar a lo siguiente.
    
        ResultType : Succeeded
        Error      :
        Exception  :

