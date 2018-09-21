---
title: 'Configurar autenticación Kerberos servidores acceso cliente equilibrio carga'
TOCTitle: Configurar la autenticación de Kerberos para servidores de acceso de cliente con equilibrio de carga
ms:assetid: 8f4faeea-a825-438d-97dc-1c398ce7aba5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff808312(v=EXCHG.150)
ms:contentKeyID: 62835917
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar la autenticación de Kerberos para servidores de acceso de cliente con equilibrio de carga

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

**Resumen:**  describe cómo usar autenticación Kerberos con servidores de acceso de cliente de carga equilibrada en Exchange 2013.

Para que pueda usar la autenticación Kerberos con servidores de acceso de cliente de carga equilibrada, necesita completar los pasos de configuración que se describen en este artículo.

## Crear la credencial de cuenta de servicio alternativa en Servicios de dominio de Active Directory

Todos los servidores de acceso de cliente que comparten los mismos espacios de nombres y direcciones URL deben usar las mismas credenciales de cuenta de servicio alternativa. Por lo general, es suficiente tener una cuenta para un bosque para cada versión de Exchange. *Credencial de cuenta de servicio alternativa* o *credencial ASA*.


> [!IMPORTANT]
> Exchange 2010 y Exchange 2013 no pueden compartir la misma credencial ASA. Deberá crear una nueva credencial ASA para Exchange 2013.




> [!IMPORTANT]
> Aunque los registros CNAME se admiten para los espacios de nombres compartidos, Microsoft recomienda el uso de registros A. De esta forma se garantiza que el cliente emite correctamente una solicitud de vale Kerberos basada en el nombre compartido y no en el FQDN del servidor.



Cuando configure la credencial ASA, tenga en cuenta estas directrices:

  - **Tipo de cuenta.** Se recomienda crear una cuenta de equipo en lugar de una cuenta de usuario. Una cuenta de equipo no permite inicio de sesión interactivo y puede tener directivas de seguridad más sencillas que una cuenta de usuario. Si crea una cuenta de equipo, la contraseña no expira, pero de todas formas se recomienda actualizar la contraseña de manera periódica. Puede usar una directiva de grupo local para especificar una antigüedad máxima para la cuenta de equipo y scripts para eliminar periódicamente cuentas de equipo que no cumplan las directivas actuales. Su directiva de seguridad local también determina cuando se necesita cambiar la contraseña. Aunque se recomienda usar una cuenta de equipo, puede crear una cuenta de usuario.

  - **Nombre de cuenta.** No hay requisitos para el nombre de la cuenta. Puede usar cualquier nombre que cumpla con su esquema de nombre.

  - **Grupo de cuentas.** La cuenta que se usa para la credencial ASA no necesita privilegios de seguridad especiales. Si va a usar una cuenta de equipo, la cuenta solo necesita pertenecer al grupo de seguridad Equipos del dominio. Si va a usar una cuenta de usuario, la cuenta solo necesita pertenecer al grupo de seguridad Usuarios del dominio.

  - **Contraseña de cuenta.** La contraseña que usted proporciona al crear la cuenta no se usará. Por ello, cuando cree la cuenta, debe usar una contraseña compleja y asegurarse de que se ajusta a los requisitos de contraseña de su organización.

Procedimiento para crear la credencial ASA como una cuenta de equipo

1.  En un equipo unido a un dominio, ejecute Windows PowerShell o el Shell de administración de Exchange.
    
    Use el cmdlet **Import-Module** para importar el módulo de Active Directory.
    
    ```powershell
Import-Module ActiveDirectory
```

2.  Use el cmdlet **New-ADComputer** para crear una nueva cuenta de equipo de Active Directory mediante esta sintaxis de cmdlet:
    
        New-ADComputer [-Name] <string> [-AccountPassword <SecureString>] [-AllowReversiblePasswordEncryption <System.Nullable[boolean]>] [-Description <string>] [-Enabled <System.Nullable[bool]>]
    
    **Ejemplo:** 
    
        New-ADComputer -Name EXCH2013ASA -AccountPassword (Read-Host 'Enter password' -AsSecureString) -Description 'Alternate Service Account credentials for Exchange' -Enabled:$True -SamAccountName EXCH2013ASA
    
    Donde *EXCH2013ASA* es el nombre de la cuenta, la descripción *Alternate Service Account credentials for Exchange* es la que usted quiera, y el valor del parámetro *SamAccountName*, en este caso *EXCH2013ASA*, debe ser único en el directorio.

3.  Use el cmdlet **Set-ADComputer** para habilitar el soporte de cifrado AES 256 que usa Kerberos siguiendo esta sintaxis de cmdlet:
    
        Set-ADComputer [-Name] <string> [-add @{<attributename>="<value>"]
    
    **Ejemplo:** 
    
    ```powershell
Set-ADComputer EXCH2013ASA -add @{"msDS-SupportedEncryptionTypes"="28"}
```
    
    Donde *EXCH2013ASA* es el nombre de la cuenta; el atributo que se debe modificar es *msDS-SupportedEncryptionTypes* con un valor decimal de 28, con lo que se habilitan los siguientes cifrados: RC4-HMAC, AES128-CTS-HMAC-SHA1-96 y AES256-CTS-HMAC-SHA1-96.

Para obtener más información sobre estos cmdlets, consulte [Import-Module](https://technet.microsoft.com/library/hh849725.aspx) y [ADComputer de nuevo](https://technet.microsoft.com/library/ee617245.aspx).

## Escenarios entre bosques

Si tiene una implementación de varios bosques o bosque de recursos, y que los usuarios que estén fuera del bosque de Active Directory que contiene Exchange, necesitará configurar las relaciones de confianza de bosque entre los bosques. Además, para cada bosque de la implementación, debe configurar una regla de enrutamiento que habilita la confianza entre todos los sufijos de nombre en el bosque y entre bosques. Para obtener más información acerca de cómo administrar las confianzas entre bosques, vea [administrar las confianzas de bosque](https://technet.microsoft.com/library/cc772440.aspx).

## Identificar los nombres de entidad de seguridad de servicio para asociar con la credencial de ASA

Una vez creada la credencial ASA, debe asociar los nombres de entidad de seguridad de servicio (SPN) de Exchange con la credencial ASA. La lista de SPN de Exchange puede variar con su configuración, pero al menos debería incluir lo siguiente:

  - **http/**   Use este SPN para Outlook en cualquier lugar, MAPI sobre conectividad de HTTP, servicios Web Exchange, Detección automática y Libreta de direcciones sin conexión.

Los valores SPN deben coincidir con el nombre de servicio en el equilibrador de carga de red y no en los servidores individuales. Para ayudarle a pensar los valores de SPN que debe usar, tenga en cuenta los escenarios siguientes:

  - Single Active Directory site

  - Multiple Active Directory sites

En cada uno de estos escenarios, se da por supuesto que se han implementado nombres de dominio completos (FQDN) con equilibrio de carga para las direcciones URL internas, las direcciones URL externas y el URI interno de la detección automática usado por los miembros del servidor de acceso de cliente. Para más información, consulte Descripción de las conexiones proxy y el redireccionamiento.

## Sitio único de Active Directory

Si tiene un sitio único de Active Directory, su entorno se puede parecer al de la siguiente figura:

![Matriz de entidades emisoras de certificados con AD único y autenticación Kerberos](images/Ff808312.97a1a926-f4ac-4498-bc6b-32e7fb1b70f1(EXCHG.150).jpg "Matriz de entidades emisoras de certificados con AD único y autenticación Kerberos")

En función de los FQDN que usan los clientes internos de Outlook en la figura anterior, necesita asociar los siguientes SPN con la credencial ASA:

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

## Varios sitios de Active Directory

Si tiene varios sitios de Active Directory, su entorno se puede parecer al de la siguiente figura:

![Matriz de entidades emisoras de certificados con varios sitios de AD y autenticación Kerberos](images/Ff808312.95b52bd8-7074-4055-8bd2-e6bf1f112b42(EXCHG.150).jpg "Matriz de entidades emisoras de certificados con varios sitios de AD y autenticación Kerberos")

En función de los FQDN que usan los clientes de Outlook en la figura anterior, necesitaría asociar los siguientes SPN con la credencial ASA que usan los servidores de acceso de cliente en ADSite 1:

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

También necesitaría asociar los siguientes SPN con la credencial ASA que usan los servidores de acceso de cliente en ADSite 2:

  - http/mailsdc.corp.tailspintoys.com

  - http/autodiscoversdc.corp.tailspintoys.com

## Configurar y después comprobar la configuración de la credencial ASA en cada servidor de acceso de cliente

Tras haber creado la cuenta, necesita comprobar que esta se haya replicado en todos los controladores de dominio de AD DS. Específicamente, la cuenta necesita estar presente en cada servidor de acceso de cliente que usará la credencial de ASA. A continuación, configure la cuenta como la credencial ASA en cada servidor de acceso de cliente de la implementación.

Para configurar la credencial ASA, use el Shell de administración de Exchange tal como se describe en uno de estos procedimientos:

  - Implementar la credencial ASA en el primer servidor de acceso de cliente de Exchange 2013

  - Implementar la credencial ASA en otros servidores de acceso de cliente de Exchange 2013

El único método admitido para implementar la credencial ASA es usar el script RollAlternateServiceAcountPassword.ps1. Para obtener más información, consulte [Uso del script RollAlternateserviceAccountCredential.ps1 en el Shell](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md). Una vez ejecutado el script, recomendamos que compruebe que todos los servidores de destino se hayan actualizado correctamente.

## Implementar la credencial ASA en el primer servidor de acceso de cliente de Exchange 2013

1.  Abra el Shell de administración de Exchange en un servidor de Exchange 2013.

2.  Cambie al *\<directorio de instalación de Exchange 2013\>*\\V15\\Scripts.

3.  Ejecute el siguiente comando para implementar la credencial ASA en el primer servidor de acceso de cliente de Exchange 2013:
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-1.corp.tailspintoys.com -GenerateNewPasswordFor tailspin\EXCH2013ASA$

4.  Cuando se le pregunte si quiere cambiar la contraseña de la cuenta de servicio alternativa, conteste **Sí**.

El siguiente es un ejemplo del resultado que aparece al ejecutar el script RollAlternateServiceAccountPassword.ps1.

    ========== Starting at 01/12/2015 10:17:47 ==========
    Creating a new session for implicit remoting of "Get-ExchangeServer" command...
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-1                                                   cas-1.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    
    Prior to pushing new credentials, all existing credentials that are invalid or no longer work will be removed from  the destination servers.
    Pushing credentials to server cas-1
    Setting a new password on Alternate Serice Account in Active Directory
    
    Password change
    Do you want to change password for tailspin\EXCH2013ASA$ in Active Directory at this time?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    Preparing to update Active Directory with a new password for tailspin\EXCH2013ASA$ ...
    Resetting a password in the Active Directory for tailspin\EXCH2013ASA$ ...
    New password was successfully set to Active Directory.
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: {mail.corp.tailspintoys.com}
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-1 Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
              ...
    
    ========== Finished at 01/12/2015 10:20:00 ==========
    
            THE SCRIPT HAS SUCCEEDED

## Implementar la credencial ASA en otros servidores de acceso de cliente de Exchange 2013

1.  Abra el Shell de administración de Exchange en un servidor de Exchange 2013.

2.  Cambie al *\<directorio de instalación de Exchange 2013\>*\\V15\\Scripts.

3.  Ejecute el siguiente comando para implementar la credencial ASA en otro servidor de acceso de cliente de Exchange 2013:
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-2.corp.tailspintoys.com -CopyFrom cas-1.corp.tailspintoys.com

4.  Repita el paso 3 para cada servidor de acceso de cliente donde quiera implementar la credencial ASA.

El siguiente es un ejemplo del resultado que aparece al ejecutar el script RollAlternateServiceAccountPassword.ps1.

    ========== Starting at 01/12/2015 10:34:35 ==========
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-2                                                   cas-2.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    Prior to pushing new credentials, all existing credentials will be removed from the destination servers.
    Pushing credentials to server cas-2
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: cas-2.corp.tailspintoys.com
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-2 Latest: 1/12/2015 10:37:59 AM, tailspin\EXCH2013ASA$
              ...
    
    
    ========== Finished at 01/12/2015 10:38:13 ==========
    
            THE SCRIPT HAS SUCCEEDED

## Comprobar la implementación de la credencial ASA

  - Abra el Shell de administración de Exchange en un servidor de Exchange 2013.

  - Ejecute el siguiente comando para comprobar la configuración en un servidor de acceso de cliente:
    
        Get-ClientAccessServer CAS-3 -IncludeAlternateServiceAccountCredentialStatus | Format-List Name, AlternateServiceAccountConfiguration

  - Repita el paso 2 en cada servidor de acceso de cliente donde quiera comprobar la implementación de la credencial ASA.

El siguiente es un ejemplo del resultado que se muestra cuando se ejecuta el comando Get-ClientAccessServer anterior y aún no se había establecido ninguna credencial ASA.

    Name                                 : CAS-1
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: <Not set>
                                               ...

El siguiente es un ejemplo del resultado que se muestra cuando se ejecuta el comando Get-ClientAccessServer anterior y ya se había establecido una credencial ASA. Se devuelven la credencial ASA anterior y la fecha y hora en que se estableció.

    Name                                 : CAS-3
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: 7/15/2014 12:58:35 PM, tailspin\oldSharedServiceAccountName$
                                               ...

## Asociar nombres de entidad de seguridad de servicio (SPN) con la credencial ASA


> [!IMPORTANT]
> No asocie SPN con una credencial ASA hasta que la haya desplegado en al menos un servidor de Exchange Server, como se describe en Implementar la credencial ASA en el primer servidor de acceso de cliente de Exchange 2013. De lo contrario, se producirán errores de autenticación Kerberos.



Antes de asociar los SPN con la credencial ASA, necesita comprobar que los SPN de destino no estén asociados todavía con una cuenta distinta en el bosque. La credencial ASA debe ser la única cuenta del bosque que tenga estos SPN asociados. Puede comprobar que ninguna otra cuenta en el bosque esté asociada con los SPN ejecutando el comando **setspn** desde la línea de comandos.

Ejecutar el comando setspn para comprobar que un SPN no está asociado todavía con una cuenta en un bosque

1.  Presione **Inicio**. En el cuadro **Buscar**, escriba **Símbolo del sistema** y, en la lista de resultados, seleccione **Símbolo del sistema**.

2.  En el símbolo del sistema, escriba el siguiente comando:
    
    ```powershell
setspn -F -Q <SPN>
```
    
    Donde \<SPN\> es el SPN que desea asociar con la credencial ASA. Por ejemplo:
    
    ```powershell
setspn -F -Q http/mail.corp.tailspintoys.com
```
    
    El comando no debe devolver nada. Si devuelve algo, otra cuenta ya está asociada al SPN. Repita este paso una vez para cada SPN que desea asociar con la credencial ASA.

Asociar un SPN con una credencial ASA mediante el comando setspn

1.  Presione **Inicio**. En el cuadro **Buscar**, escriba **Símbolo del sistema** y, en la lista de resultados, seleccione **Símbolo del sistema**.

2.  En el símbolo del sistema, escriba el siguiente comando:
    
    ```powershell
setspn -S <SPN> <Account>$
```
    
    Donde \<SPN\> es el SPN que desea asociar con la credencial ASA y \<Account\> es la cuenta asociada con la credencial ASA. Por ejemplo:
    
    ```powershell
setspn -S http/mail.corp.tailspintoys.com tailspin\EXCH2013ASA$
```
    
    Ejecute este comando una vez para cada SPN que desea asociar con la credencial ASA.

Ejecutar el comando setspn para comprobar que ha asociado los SPN con las credenciales ASA

1.  Presione **Inicio**. En el cuadro **Buscar**, escriba **Símbolo del sistema** y, en la lista de resultados, seleccione **Símbolo del sistema**.

2.  En el símbolo del sistema, escriba el siguiente comando:
    
    ```powershell
setspn -L <Account>$
```
    
    Donde \<Account\> es la cuenta asociada con la credencial ASA. Por ejemplo:
    
    ```powershell
setspn -L tailspin\EXCH2013ASA$
```
    
    Deberá ejecutar este comando una sola vez.

## Habilitar la autenticación Kerberos para los clientes de Outlook

1.  Abra el Shell de administración de Exchange en un servidor de Exchange 2013.

2.  Para habilitar la autenticación Kerberos para los clientes de Outlook en cualquier lugar, ejecute el siguiente comando en el servidor de acceso de cliente:
    
        Get-OutlookAnywhere -server CAS-1 | Set-OutlookAnywhere -InternalClientAuthenticationMethod  Negotiate

3.  Para habilitar la autenticación Kerberos para clientes de MAPI sobre HTTP, ejecute lo siguiente en el servidor de acceso de cliente de Exchange 2013:
    
        Get-MapiVirtualDirectory -Server CAS-1 | Set-MapiVirtualDirectory -IISAuthenticationMethods Ntlm, Negotiate

4.  Repita los pasos 2 y 3 para cada servidor de acceso de cliente de Exchange 2013 donde quiera habilitar la autenticación Kerberos.

## Validación de la autenticación Kerberos del cliente de Exchange

Tras haber configurado correctamente Kerberos y la credencial ASA, compruebe que los clientes se pueden autenticar correctamente tal como se describe en estas tareas.

## Comprobar si se está ejecutando el servicio de Microsoft Exchange Service Host

El servicio de Microsoft Exchange Service Host (MSExchangeServiceHost) en el servidor de acceso de cliente es responsable de la administración de la credencial ASA. Si dicho servicio no está en ejecución, no es posible llevar a cabo la autenticación Kerberos. De forma predeterminada, el servicio está configurado para iniciarse de forma automática al iniciar el equipo.

Procedimiento para comprobar si se inició el servicio de Microsoft Exchange Service Host

1.  Haga clic en **Inicio**, escriba **services.msc** y seleccione **services.msc** en la lista.

2.  En la ventana **Servicios**, busque el servicio **Microsoft Exchange Service Host** en la lista de servicios.

3.  El estado del servicio debe ser **En ejecución**. Si el estado no es **En ejecución**, haga clic con el botón secundario en el servicio y, a continuación, haga clic en **Inicio**.

## Validación de Kerberos desde el servidor de acceso de cliente

Cuando configuró la credencial ASA en cada servidor de acceso de cliente, ejecutó el cmdlet **set-ClientAccessServer**. Una vez que haya ejecutado este cmdlet, puede usar los registros para comprobar las conexiones correctas de Kerberos.

Procedimiento para validar que Kerberos esté funcionando correctamente mediante el archivo de registro HttpProxy

1.  En un editor de texto, examine la carpeta donde se almacena el registro de HttpProxy. De forma predeterminada, el archivo está almacenado en la siguiente carpeta:
    
    %ExchangeInstallPath%\\Logging\\HttpProxy\\RpcHttp

2.  Abra el archivo de registro más reciente y busque la palabra **Negotiate**. La línea del archivo de registro debe ser similar al siguiente ejemplo:
    
        2014-02-19T13:30:49.219Z,e19d08f4-e04c-42da-a6be-b7484b396db0,15,0,775,22,,RpcHttp,mail.corp.tailspintoys.com,/rpc/rpcproxy.dll,,Negotiate,True,tailspin\Wendy,tailspintoys.com,MailboxGuid~ad44b1e0-e44f-4a16-9396-3a437f594f88,MSRPC,192.168.1.77,EXCH1,200,200,,RPC_OUT_DATA,Proxy,exch2.tailspintoys.com,15.00.0775.000,IntraForest,MailboxGuidWithDomain,,,,76,462,1,,1,1,,0,,0,,0,0,16272.3359,0,0,3,0,23,0,25,0,16280,1,16274,16230,16233,16234,16282,?ad44b1e0-e44f-4a16-9396-3a437f594f88@tailspintoys.com:6001,,BeginRequest=2014-02-19T13:30:32.946Z;BeginGetRequestStream=2014-02-19T13:30:32.946Z;OnRequestStreamReady=2014-02-19T13:30:32.946Z;BeginGetResponse=2014-02-19T13:30:32.946Z;OnResponseReady=2014-02-19T13:30:32.977Z;EndGetResponse=2014-02-19T13:30:32.977Z;,PossibleException=IOException;
    
    Si ve que el valor **AuthenticationType** es **Negotiate**, el servidor está creando correctamente conexiones autenticadas de Kerberos.

## Mantener la credencial ASA

Si necesita actualizar la contraseña en la credencial ASA de forma periódica, use los pasos para configurar la credencial ASA en este artículo. Considere la posibilidad de configurar una tarea programada para realizar el mantenimiento de contraseñas habitual. Asegúrese de supervisar las tareas programadas para garantizar la sustitución oportuna de contraseñas y evitar los posibles cortes de autenticación.

## Apagar la autenticación Kerberos

Para configurar el servidor de acceso de cliente para que no use Kerberos, desasocie o quite los SPN de la credencial ASA. Si se quitan los SPN, la autenticación Kerberos no será intentada por sus clientes, y los clientes configurados para la autenticación Negociar usarán NTLM en su lugar. Los clientes configurados para usar solamente Kerberos no podrán conectarse. Cuando se eliminan los SPN también debe quitar la cuenta.

Para quitar la credencial ASA

1.  Abra el Shell de administración de Exchange en un servidor de Exchange 2013 y ejecute el siguiente comando:
    
    ```powershell
Set-ClientAccessServer CAS-1 -RemoveAlternateServiceAccountCredentials
```

2.  Aunque no tiene que hacer esto inmediatamente, en algún momento tendrá que reiniciar todos los equipos cliente para borrar la memoria caché de vales de Kerberos del equipo.

