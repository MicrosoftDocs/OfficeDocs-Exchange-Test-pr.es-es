---
title: 'Configuración de la descarga de SSL en Exchange 2013: Exchange 2013 Help'
TOCTitle: Configuración de la descarga de SSL en Exchange 2013
ms:assetid: 654cc2c2-918b-48fc-9532-9c8e3012810d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn635115(v=EXCHG.150)
ms:contentKeyID: 61204109
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración de la descarga de SSL en Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-08-22_

La siguiente información le ayudará a configurar la descarga de SSL para los protocolos y los servicios relacionados en los servidores de acceso de cliente de Exchange 2013 con Service Pack 1 (SP1) instalado. Si tiene varios servidores de acceso de cliente, debe realizar los pasos necesarios para cada protocolo o servicio en cada servidor de acceso de cliente con el Service Pack 1 instalado en la organización local. Además, cada servidor de acceso de cliente de la organización debe estar configurado de forma idéntica. Si va a actualizar a actualizaciones acumulativas o Service Packs más recientes y quiere continuar usando la descarga de SSL, debe realizar los pasos siguientes después de aplicar las actualizaciones en sus servidores de acceso de cliente de Exchange 2013.

Una de las mayores ventajas para la descarga de SSL es que permite administrar con más facilidad los certificados que se utilizan. En lugar de tener certificados SSL independientes para cada servidor acceso de cliente con SP1 instalado, se utiliza un certificado SSL y se importa a todos los servidores de acceso de cliente. El certificado utilizado puede ser un certificado SSL existente o recién creado.


> [!WARNING]
> Si usa el Administrador de Internet Information Services (IIS), el Shell de administración de Exchange o una interfaz de la línea de comandos para configurar la descarga de SSL, observe que hay un <STRONG>Sitio web predeterminado</STRONG> y un sitio <STRONG>Back-end de Exchange</STRONG>. Para la descarga de SSL, configure solo el <STRONG>Sitio web predeterminado</STRONG> y no realice ningún cambio en el sitio <STRONG>Back-end de Exchange</STRONG>.



**Contenido**

Configurar la descarga de SSL para Outlook Web App

Configurar la descarga de SSL para el centro de administración de Exchange (EAC)

Configurar la descarga de SSL para Outlook en cualquier lugar

Configurar la descarga de SSL para la libreta de direcciones sin conexión (OAB)

Configurar la descarga de SSL para Exchange ActiveSync (EAS)

Configurar la descarga de SSL para servicios Web Exchange (EWS)

Configurar la descarga de SSL para el servicio de detección automática

Configurar la descarga de SSL para el servicio de proxy de replicación de buzones (MRSProxy)

Configurar la descarga de SSL para los clientes de Outlook (directorio virtual MAPI)

Mediante un script para habilitar la descarga de SSL para todos los protocolos y servicios

Configurar la coexistencia con Exchange 2007 y Exchange 2010

## ¿Qué necesita saber antes de comenzar?

  - Instale todos los servidores de acceso de cliente y los servidores de buzones necesarios en la organización.

  - Instale el Service Pack 1 (SP1) en cada servidor acceso de cliente y servidor de buzones de la organización. Para descargar SP1, consulte [Actualizaciones para Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

  - Determine los permisos necesarios para Exchange 2013; para ello, consulte [Permisos de características](feature-permissions-exchange-2013-help.md).

  - Para ver qué permisos necesita para los servidores de acceso de cliente, vea "Permisos de servidor de acceso de cliente" en [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para ver qué permisos necesita para los servidores de acceso de cliente, vea "Permisos de Outlook Web App" en [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Quizás solo pueda usar el Shell para realizar algunos procedimientos. Para obtener información sobre cómo abrir el Shell en su organización de Exchange local, consulte [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)).

  - Para usar un certificado existente en sus servidores de acceso de cliente y en el dispositivo con el que termina las conexiones de SSL, exporte el certificado con la clave privada en un servidor de acceso de cliente e impórtelo o instálelo en el dispositivo. Para más información, consulte [Export-ExchangeCertificate](https://technet.microsoft.com/es-es/library/aa996305\(v=exchg.150\)).

  - Para usar un certificado nuevo, debe usar el EAC o el Shell para crear, importar y habilitar el nuevo certificado. Para más información, consulte [Interfaz de usuario de administración de certificados de Exchange 2013](exchange-2013-certificate-management-ui-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurar la descarga de SSL para Outlook Web App

Para habilitar la descarga de SSL para Outlook Web App, necesitará quitar el requisito de SSL en el directorio virtual **owa** en el **Sitio web predeterminado**:

  - **Paso 1** Puede usar el Administrador de Internet Information Services (IIS) o una línea de comandos para deshabilitar SSL en el directorio virtual **owa**:
    
      - Mediante el Administrador de Internet Information Services (IIS), expanda **Sitios** \> **Sitio web predeterminado** y, después, seleccione el directorio virtual **owa**. En el panel de resultados, en **IIS**, haga doble clic en **Configuración de SSL**. En el panel de resultados **Configuración de SSL**, desactive la casilla **Requerir SSL** y haga clic en **Aplicar** en el panel **Acciones**.
    
      - En la línea de comandos, escriba lo siguiente y, a continuación, presione Entrar.
        
            appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST

  - **Paso 2** Necesita reciclar el grupo de aplicaciones correcto o reiniciar Internet Information Services mediante uno de los métodos siguientes:
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            appcmd Recycle AppPool MSExchangeOWAAppPool
    
      - Con un cmdlet de Windows PowerShell, escriba lo siguiente y presione Entrar.
        
            IIS:\>Restart-WebAppPool MSExchangeOWAAppPool
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            iisreset /noforce
    
      - Mediante el Administrador de Internet Information Services (IIS): En Administrador de Internet Information Services (IIS), en el panel **Acciones**, haga clic en **Reiniciar**.

Volver al principio

## Configurar la descarga de SSL para el centro de administración de Exchange (EAC)

Para habilitar la descarga de SSL para EAC, necesitará quitar el requisito de SSL en el directorio virtual **ecp** en el **Sitio web predeterminado**:

  - **Paso 1** Puede usar el Administrador de Internet Information Services (IIS) o una línea de comandos para deshabilitar SSL en el directorio virtual **ecp**:
    
      - Mediante el Administrador de Internet Information Services (IIS), expanda **Sitios** \> **Sitio web predeterminado** y, después, seleccione el directorio virtual **ecp**. En el panel de resultados, en **IIS**, haga doble clic en **Configuración de SSL**. En el panel de resultados **Configuración de SSL**, desactive la casilla **Requerir SSL** y haga clic en **Aplicar** en el panel **Acciones**.
    
      - En la línea de comandos, escriba lo siguiente y, a continuación, presione Entrar.
        
            appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
        
        ``` 
        ```

  - **Paso 2** Necesita reciclar el grupo de aplicaciones correcto o reiniciar Internet Information Services mediante uno de los métodos siguientes:
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            appcmd Recycle AppPool MSExchangeECPAppPool
    
      - Con un cmdlet de Windows PowerShell, escriba lo siguiente y presione Entrar.
        
            IIS:\>Restart-WebAppPool MSExchangeECPAppPool
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            iisreset /noforce
    
      - Mediante el Administrador de Internet Information Services (IIS): En Administrador de Internet Information Services (IIS), en el panel **Acciones**, haga clic en **Reiniciar**.

Volver al principio

## Configurar la descarga de SSL para Outlook en cualquier lugar

La descarga de SSL para Outlook en cualquier lugar está habilitada de forma predeterminada. Los clientes de Outlook en cualquier lugar pueden recibir correo electrónico de una red privada o pública. De forma predeterminada, se usa el nombre de host interno o el nombre completo del servidor para habilitar los clientes internos de Outlook para conectarse. Pero si no usa Outlook en cualquier lugar internamente, debe quitar el nombre de host interno. Para permitir a los clientes de Outlook tanto el acceso interno como externo, debe configurar los nombres de host internos y externos, establecer el método de autenticación para cada uno y establecer que tanto los clientes internos como los externos requieran SSL. Para configurar el método de autenticación para los clientes externos, puede usar EAC o el Shell de administración de Exchange, pero para los clientes internos, debe usar el Shell:

  - **Paso 1** Puede usar EAC o el Shell si no ha agregado un nombre de host externo para Outlook en cualquier lugar:
    
      - Mediante EAC, vaya a **Servidores**, seleccione el nombre del servidor de acceso de cliente en la lista y haga clic en **Editar**. En la ventana **Servidor de Exchange**, haga clic en **Outlook en cualquier lugar** y, en el cuadro **Especifica el nombre de host externo (por ejemplo, contoso.com) que se usará para conectar con tu organización**, escriba el nombre del host externo. Compruebe que la opción **Permitir la descarga de SSL** está seleccionada y haga clic en **Guardar**.
    
      - Mediante el Shell de administración de Exchange, haga clic en **Inicio** y, en el menú **Inicio**, haga clic en **Shell de administración de Exchange**. En la ventana, escriba lo siguiente y después, presione Entrar:
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -Externalhostname ClientAccessServer1.contoso.com -ExternalClientsRequireSsl:$True -ExternalClientAuthenticationMethod Basic

  - **Paso 2** De manera predeterminada, la descarga de SSL está habilitada. Sin embargo, puede usar EAC o el Shell de administración de Exchange si se ha deshabilitado la descarga de SSL y desea habilitarla:
    
      - Mediante EAC, vaya a **Servidores**, seleccione el nombre del servidor de acceso de cliente en la lista y haga clic en **Editar**. En la ventana **Servidor de Exchange**, haga clic en **Outlook en cualquier lugar**, haga clic en la opción **Permitir la descarga de SSL** y haga clic en **Guardar**.
    
      - Mediante el Shell, escriba lo siguiente y después, presione Entrar.
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -SSLOffloading $true

  - **Paso 3**   De forma predeterminada, **Requerir SSL** no está activada en el directorio virtual **Rpc**, pero si quiere comprobar si SSL está deshabilitada, puede usar el Administrador de Internet Information Services (IIS).
    
      - Mediante el Administrador de Internet Information Services (IIS), expanda **Sitios** \> **Sitio web predeterminado** y, después, seleccione el directorio virtual **Rpc**. En el panel de resultados, en **IIS**, haga doble clic en **Configuración de SSL**. En el panel de resultados **Configuración de SSL**, compruebe que la casilla **Requerir SSL** está desactivada y haga clic en **Aplicar** en el panel **Acciones**.

  - **Paso 4** Necesita reciclar el grupo de aplicaciones correcto o reiniciar Internet Information Services mediante uno de los métodos siguientes:
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            appcmd Recycle AppPool MSExchangeRpcProxyFrontEndAppPool
    
      - Con un cmdlet de Windows PowerShell, escriba lo siguiente y presione Entrar.
        
            IIS:\>Restart-WebAppPool MSExchangeRpcProxyFrontEndAppPool
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            iisreset /noforce
    
      - Mediante el Administrador de Internet Information Services (IIS): En Administrador de Internet Information Services (IIS), en el panel **Acciones**, haga clic en **Reiniciar**.


> [!IMPORTANT]
> Debe esperar a que el proceso de Host de servicio aplique los cambios de Active Directory a Internet Information Services (IIS) cada 15 minutos, aunque reinicie IIS en un servidor de acceso de cliente.



Volver al principio

## Configurar la descarga de SSL para la libreta de direcciones sin conexión (OAB)

Para habilitar la descarga de SSL para la libreta de direcciones sin conexión (OAB), necesitará quitar el requisito de SSL en el directorio virtual **OAB** en el **Sitio web predeterminado**:

  - **Paso 1** Puede usar el Administrador de Internet Information Services (IIS) o una línea de comandos para deshabilitar SSL en el directorio virtual **OAB**:
    
      - Mediante el Administrador de Internet Information Services (IIS), expanda **Sitios** \> **Sitio web predeterminado** y, después, seleccione el directorio virtual **OAB**. En el panel de resultados, en **IIS**, haga doble clic en **Configuración de SSL**. En el panel de resultados **Configuración de SSL**, desactive la casilla **Requerir SSL** y haga clic en **Aplicar** en el panel **Acciones**.
    
      - En la línea de comandos, escriba lo siguiente y, a continuación, presione Entrar.
        
            appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST

  - **Paso 2** Necesita reciclar el grupo de aplicaciones correcto o reiniciar Internet Information Services mediante uno de los métodos siguientes:
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            appcmd Recycle AppPool MSExchangeOABAppPool
    
      - Con un cmdlet de Windows PowerShell, escriba lo siguiente y presione Entrar.
        
            IIS:\>Restart-WebAppPool MSExchangeOABAppPool
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            iisreset /noforce
    
      - Mediante el Administrador de Internet Information Services (IIS): En Administrador de Internet Information Services (IIS), en el panel **Acciones**, haga clic en **Reiniciar**.

Volver al principio

## Configurar la descarga de SSL para Exchange ActiveSync (EAS)

Para habilitar la descarga de SSL para Exchange ActiveSync (EAS), necesitará quitar el requisito de SSL en el directorio virtual **Microsoft-Server-ActiveSync** en el **Sitio web predeterminado**:

  - **Paso 1** Puede usar el Administrador de Internet Information Services (IIS) o una línea de comandos para deshabilitar SSL en el directorio virtual **Microsoft-Server-ActiveSync**:
    
      - Mediante el Administrador de Internet Information Services (IIS), expanda **Sitios** \> **Sitio web predeterminado** y, después, seleccione el directorio virtual **Microsoft-Server-ActiveSync**. En el panel de resultados, en **IIS**, haga doble clic en **Configuración de SSL**. En el panel de resultados **Configuración de SSL**, desactive la casilla **Requerir SSL** y haga clic en **Aplicar** en el panel **Acciones**.
    
      - En la línea de comandos, escriba lo siguiente y, a continuación, presione Entrar.
        
            appcmd set config "Default Web Site/MSExchangeSyncAppPool" /section:access /sslFlags:None /commit:APPHOST

  - **Paso 2** Necesita reciclar el grupo de aplicaciones correcto o reiniciar Internet Information Services mediante uno de los métodos siguientes:
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            appcmd Recycle AppPool MSExchangeSyncAppPool
    
      - Con un cmdlet de Windows PowerShell, escriba lo siguiente y presione Entrar.
        
            IIS:\>Restart-WebAppPool MSExchangeSyncAppPool
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            iisreset /noforce
    
      - Mediante el Administrador de Internet Information Services (IIS): En Administrador de Internet Information Services (IIS), en el panel **Acciones**, haga clic en **Reiniciar**.

Volver al principio

## Configurar la descarga de SSL para servicios Web Exchange (EWS)

Para habilitar la descarga de SSL para servicios Web Exchange (EWS), necesitará quitar el requisito de SSL en el directorio virtual **EWS** en el **Sitio web predeterminado**:

  - **Paso 1** Puede usar el Administrador de Internet Information Services (IIS) o una línea de comandos para deshabilitar SSL en el directorio virtual **EWS**:
    
      - Mediante el Administrador de Internet Information Services (IIS), expanda **Sitios** \> **Sitio web predeterminado** y, después, seleccione el directorio virtual **EWS**. En el panel de resultados, en **IIS**, haga doble clic en **Configuración de SSL**. En el panel de resultados **Configuración de SSL**, desactive la casilla **Requerir SSL** y haga clic en **Aplicar** en el panel **Acciones**.
    
      - En la línea de comandos, escriba lo siguiente y, a continuación, presione Entrar.
        
            appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST

  - **Paso 2** Necesita reciclar el grupo de aplicaciones correcto o reiniciar Internet Information Services mediante uno de los métodos siguientes:
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            appcmd Recycle AppPool MSExchangeServicesAppPool
    
      - Con un cmdlet de Windows PowerShell, escriba lo siguiente y presione Entrar.
        
            IIS:\>Restart-WebAppPool MSExchangeServicesAppPool
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            iisreset /noforce
    
      - Mediante el Administrador de Internet Information Services (IIS): En Administrador de Internet Information Services (IIS), en el panel **Acciones**, haga clic en **Reiniciar**.

Volver al principio

## Configurar la descarga de SSL para el servicio de detección automática

Para habilitar la descarga de SSL para el servicio de detección automática, necesitará quitar el requisito de SSL en el directorio virtual **Autodiscover** en el **Sitio web predeterminado**:

  - **Paso 1** Puede usar el Administrador de Internet Information Services (IIS) o una línea de comandos para deshabilitar SSL en el directorio virtual **Autodiscover**:
    
      - Mediante el Administrador de Internet Information Services (IIS), expanda **Sitios** \> **Sitio web predeterminado** y, después, seleccione el directorio virtual **Autodiscover**. En el panel de resultados, en **IIS**, haga doble clic en **Configuración de SSL**. En el panel de resultados **Configuración de SSL**, desactive la casilla **Requerir SSL** y haga clic en **Aplicar** en el panel **Acciones**.
    
      - En la línea de comandos, escriba lo siguiente y, a continuación, presione Entrar.
        
            appcmd set config "Default Web Site/autodiscover" /section:access /sslFlags:None /commit:APPHOST

  - **Paso 2** Necesita reciclar el grupo de aplicaciones correcto o reiniciar Internet Information Services mediante uno de los métodos siguientes:
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            appcmd Recycle AppPool MSExchangeAutodiscoverAppPool
    
      - Con un cmdlet de Windows PowerShell, escriba lo siguiente y presione Entrar.
        
            IIS:\>Restart-WebAppPool MSExchangeAutodiscoverAppPool
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            iisreset /noforce
    
      - Mediante el Administrador de Internet Information Services (IIS): En Administrador de Internet Information Services (IIS), en el panel **Acciones**, haga clic en **Reiniciar**.

Volver al principio

## Configurar la descarga de SSL para el servicio de proxy de replicación de buzones (MRSProxy)

El servicio de proxy de replicación de buzones (MRSProxy) se instala en todos los servidores de acceso de cliente de Exchange 2013. MRSProxy ayuda a realizar solicitudes locales de traslado entre bosques, así como a trasladar los buzones locales a Office 365, pero MRSProxy está deshabilitado de forma predeterminada. Si va a habilitarlo, debe hacerlo en el bosque de Exchange remoto para traslados locales de buzones entre bosques, o en el bosque de Exchange local para trasladar un buzón a Office 365. Aunque el servicio MRSProxy se ejecuta en los servicios Web Exchange (EWS), no permite configurar la descarga de SSL.

El motivo es que el servicio MRSProxy espera que el tráfico esté firmado o cifrado. Los equilibradores de carga de hardware o los firewalls deben cifrar de nuevo el tráfico de MRSProxy antes de enviarlo a los servidores de acceso de cliente. Si este es el caso, se recomienda configurar un puente SSL para que las descargas funcionen.

**SSL inversa o puente SSL** Si habilita SSL inversa o un puente SSL en equilibradores de carga de hardware, no tendrá que realizar los pasos anteriores en cada servidor CAS. Pero al activar SSL inversa en los equilibradores de carga de hardware, el cifrado y el descifrado de SSL se mantendrán en los servidores de acceso de cliente. En este caso, el cifrado y el descifrado de SSL se producirán en los equilibradores de carga de hardware y en los servidores de acceso de cliente. La decisión de usar SSL inversa (puente SSL) o la descarga de SSL de Exchange 2013 depende de los objetivos de la organización y de los procedimientos de seguridad que deben implementarse. En la siguiente imagen se muestra la conectividad de clientes con puente SSL (SSL inversa).

![Puente SSL](images/Dn635115.a08aacc1-0ab4-46b3-bdae-b9518a3f5748(EXCHG.150).jpg "Puente SSL")

## Configurar la descarga de SSL para los clientes de Outlook (directorio virtual MAPI)

Para habilitar la descarga de SSL para los clientes de Outlook, necesitará quitar el requisito de SSL en el directorio virtual **MAPI** en el **Sitio web predeterminado**:

  - **Paso 1** Puede usar el Administrador de Internet Information Services (IIS) o una línea de comandos para deshabilitar SSL en el directorio virtual **MAPI**:
    
      - Mediante el Administrador de Internet Information Services (IIS), expanda **Sitios** \> **Sitio web predeterminado** y, después, seleccione el directorio virtual **MAPI**. En el panel de resultados, en **IIS**, haga doble clic en **Configuración de SSL**. En el panel de resultados **Configuración de SSL**, desactive la casilla **Requerir SSL** y haga clic en **Aplicar** en el panel **Acciones**.
    
      - En la línea de comandos, escriba lo siguiente y, a continuación, presione Entrar.
        
            appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST

  - **Paso 2** Necesita reciclar el grupo de aplicaciones correcto o reiniciar Internet Information Services mediante uno de los métodos siguientes:
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            appcmd Recycle AppPool MSExchangeMapiFrontEndAppPool
    
      - Con un cmdlet de Windows PowerShell, escriba lo siguiente y presione Entrar.
        
            IIS:\>Restart-WebAppPool MSExchangeMapiFrontEndAppPool
    
      - Mediante una línea de comandos: Vaya a **Inicio** \> **Ejecutar**, escriba **cmd** y presione Entrar. En la ventana de símbolo del sistema, escriba lo siguiente y presione Entrar.
        
            iisreset /noforce
    
      - Mediante el Administrador de Internet Information Services (IIS): En Administrador de Internet Information Services (IIS), en el panel **Acciones**, haga clic en **Reiniciar**.

Volver al principio

## Mediante un script para habilitar la descarga de SSL para todos los protocolos y servicios

Si está trabajando con una organización grande con varios servidores de acceso de cliente de Exchange 2013, quizás sea conveniente acelerar los pasos anteriores que realizó. Puede copiar y pegar los comandos en cualquiera de los siguientes scripts en el Bloc de notas, realizar los cambios, guardar el archivo con la extensión .ps1 y, después, ejecutarlo desde el Shell de administración de Exchange. Dependiendo de sus necesidades, se pueden usar ambos scripts para configurar la descarga de SSL para todos los protocolos y servicios de un solo servidor acceso de cliente o para varios.


> [!NOTE]
> En las entradas del cmdlet <STRONG>Set-OutlookAnywhere</STRONG>, reemplace "MyServer" por el nombre de sus servidores de acceso de cliente.



**Usar Set-WebConfigurationProperty**

    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS:  -Location "Default Web Site/OWA"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/ecp"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/EWS"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Autodiscover"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Microsoft-Server-ActiveSync"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/OAB"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/MAPI"
    iisreset /noforce

**Usar appcmd**


> [!NOTE]
> En las entradas del cmdlet <STRONG>Set-OutlookAnywhere</STRONG>, reemplace "MyServer" por el nombre de sus servidores de acceso de cliente.



    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Autodiscover" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
    iisreset /noforce

Volver al principio

## Configurar la coexistencia con Exchange 2007 y Exchange 2010

En un escenario de coexistencia, en una organización con una mezcla de servidores de Exchange 2003 y de Exchange 2010, uno de los primeros pasos que debe realizar después de implementar los servidores de acceso de cliente de Exchange 2010 es cambiar el DNS para que los usuarios de Exchange 2003 accedan a sus buzones desde un grupo de servidores de acceso de cliente de Exchange 2010. En este escenario, se admite totalmente habilitar la descarga de SSL en el equilibrador de carga que se usa para distribuir el tráfico de cliente entre los servidores de acceso de cliente.

**Coexistencia con otras versiones de Outlook Web App**

Con la descarga de SSL configurada en los servidores de acceso de cliente de Exchange 2013, la coexistencia funciona con Exchange 2007 y Exchange 2010:

  - Para que coexista con Exchange 2007, se requiere un espacio de nombres anterior, y la redirección solo tendrá lugar con Outlook Web App y los servicios Web Exchange. Un servidor proxy redirigirá el servicio de detección automática, Outlook en cualquier lugar y Exchange ActiveSync a versiones anteriores.

  - Para que coexista con Exchange 2010, si ha configurado la dirección URL externa, se utilizará una redirección. De lo contrario, se usará un servidor proxy.

Volver al principio

