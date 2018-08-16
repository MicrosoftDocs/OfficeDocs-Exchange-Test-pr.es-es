---
title: 'Configurar límites tamaño mensaje específicos del cliente: Exchange 2013 Help'
TOCTitle: Configurar límites de tamaño de mensaje específicos del cliente
ms:assetid: fef9ca78-b68f-4342-ada0-881ab985ce3c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh529949(v=EXCHG.150)
ms:contentKeyID: 52062081
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar límites de tamaño de mensaje específicos del cliente

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-01-26_

En Microsoft Exchange Server 2013, hay varios límites de tamaño de mensajes diferentes a medida que viajan por la organización de Exchange. Para obtener más información, vea [Límites de tamaño de mensaje](message-size-limits-exchange-2013-help.md).

En cambio, hay límites de tamaño de mensajes específicos de los clientes que puede configurar para Outlook Web App y los clientes de correo electrónico que usen ActiveSync o Servicios web de Exchange (EWS). Si modifica los límites de tamaño del mensaje en el nivel de la organización, debe comprobar los límites del tamaño del mensaje de Outlook Web App, ActiveSync y que los servicios Web Exchange estén configurados correctamente. Estos valores se configuran en los archivos web.config en los servidores de acceso de cliente y en los servidores de buzones de correo. Estos límites se describen en las tablas siguientes:

### ActiveSync

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de servidor</th>
<th>Archivo de configuración</th>
<th>Claves y valores predeterminados</th>
<th>Tamaño</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acceso de cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   No está presente de manera predeterminada (ver comentarios).</p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Acceso de cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>kilobytes</p></td>
</tr>
<tr class="odd">
<td><p>Buzón</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   No está presente de manera predeterminada (ver comentarios).</p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Buzón</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>kilobytes</p></td>
</tr>
<tr class="odd">
<td><p>Buzón</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>&lt;add key=&quot;MaxDocumentDataSize&quot; value=&quot;10240000&quot;&gt;</code></p></td>
<td><p>bytes</p></td>
</tr>
</tbody>
</table>


**Comentarios sobre los límites de ActiveSync**

De manera predeterminada, no hay ninguna clave *maxAllowedContentLength* en los archivos `web.config` de ActiveSync. Pero, el tamaño máximo de mensaje de ActiveSync se ve afectado por el valor de **maxAllowedContentLength** que se aplica a todos los sitios web del servidor. El valor predeterminado es 30 000 000 bytes (30 MB). Para ver estos valores para ActiveSync en los servidores de acceso de cliente y en los servidores de buzones de correo en el Administrador de IIS, siga estos pasos:

1.  Realice uno de los pasos siguientes:
    
      - En los servidores de acceso de cliente, abra el **Administrador de IIS**, vaya a **Sitios**\>**Sitio web predeterminado** y seleccione **Microsoft-Server-ActiveSync**.
    
      - En los servidores de buzones de correo, abra el **Administrador de IIS**, vaya a **Sitios**\>**Exchange Back End** y seleccione **Microsoft-Server-ActiveSync**.

2.  Compruebe que la **Vista Características** está seleccionada y haga doble clic en **Editor de configuración** en la sección **Administración**.

3.  Haga clic en la flecha desplegable en el campo **Sección**, vaya a **system.webServer**\>**seguridad** y seleccione **requestFiltering**.

4.  En los resultados, expanda **requestLimits** y verá **maxAllowedContentLength** y el valor predeterminado 30000000 (bytes).

Para cambiar el valor de **maxAllowedContentLength**, escriba un nuevo valor en bytes y haga clic en **Aplicar**. Deberá cambiar el valor en los servidores de acceso de cliente y en los servidores de buzones de correo. Después de cambiar el valor en el Administrador de IIS, se escribe una nueva clave *maxAllowedContentLength* en el archivo `web.config` correspondiente (`%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config` en los servidores de acceso de cliente y `%ExchangeInstallPath%ClientAccess\Sync\web.config` en los servidores de buzones de correo).

Para cambiar el tamaño máximo de los mensajes para los clientes de ActiveSync, deberá cambiar el valor de *maxRequestLength* en el archivo `web.config` en los servidores de acceso de cliente y en los servidores de buzones de correo, de *MaxDocumentDataSize* en el archivo `web.config` en los servidores de buzones de correo y de *maxAllowedContentLength* en el Administrador de IIS en los servidores de acceso de cliente y en los servidores de buzones de correo.

### Servicios web de Exchange

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de servidor</th>
<th>Archivo de configuración</th>
<th>Claves y valores predeterminados</th>
<th>Tamaño</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acceso de cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Buzón</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="odd">
<td><p>Buzón</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p>14 instancias de <code>maxReceivedMessageSize=&quot;67108864&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
</tbody>
</table>


**Comentarios sobre los límites de los servicios Web Exchange**

  - Hay 14 instancias diferentes del valor `maxReceivedMessageSize="67108864"` que corresponden a diferentes combinaciones de enlaces (http y https) y métodos de autenticación.

  - Para cambiar el tamaño máximo de mensaje para los clientes de servicios Web Exchange, debe cambiar el valor de *maxAllowedContentLength* en ambos archivos `web.config`, y las 14 instancias de `maxReceivedMessageSize="67108864"` en el archivo `web.config` en los servidores de buzones de correo.

  - En el archivo `web.config` en los servidores de buzones de correo también hay dos instancias del valor `maxReceivedMessageSize="1048576"` para los enlaces de **UMLegacyMessageEncoderSoap11Element** que no es necesario modificar.

  - *maxRequestLength* es una opción de configuración de ASP.NET que está presente en ambos archivos web.config pero que servicios Web Exchange no usa, por lo que no es necesario modificarla.

### Outlook Web App

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de servidor</th>
<th>Archivo de configuración</th>
<th>Claves y valores predeterminados</th>
<th>Tamaño</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acceso de cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Acceso de cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>kilobytes</p></td>
</tr>
<tr class="odd">
<td><p>Buzón</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Buzón</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>kilobytes</p></td>
</tr>
<tr class="odd">
<td><p>Buzón</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 instances of <code>maxReceivedMessageSize=&quot;35000000&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Buzón</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 instances of <code>maxStringContentLength=&quot;35000000&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
</tbody>
</table>


**Comentarios sobre los límites de Outlook Web App**

  - En el archivo `web.config` en los servidores de buzones de correo, hay dos instancias diferentes de los valores `maxReceivedMessageSize="35000000"` y `maxStringContentLength="35000000"` que se corresponden con los enlaces http y https.

  - Para cambiar el tamaño máximo de mensaje para los clientes de Outlook Web App, debe cambiar todos estos valores en los dos archivos, incluidas las dos instancias de *maxReceivedMessageSize* y *maxStringContentLength* en el archivo `web.config` en los servidores de buzones de correo.

  - En el archivo `web.config` en los servidores de buzones de correo también hay una instancia del valor `maxStringContentLength="102400"` para el enlace **MsOnlineShellService** que no es necesario modificar.

Para todos los límites de tamaño de los mensajes, debe establecer valores mayores a los tamaños actuales que desee aplicar. Este incremento de los valores es necesario para justificar el incremento del tamaño del mensaje inevitable que se produce después de aplicar codificación Base64 a los datos adjuntos del mensaje y otros datos binarios. La codificación Base64 incrementa el tamaño del mensaje en aproximadamente un 33 %, de manera que los valores que especifique para los límites del tamaño del mensaje son aproximadamente un 33 % más grandes que los tamaños de mensaje realmente utilizables. Por ejemplo, si especifica un valor de tamaño de mensaje máximo de 64 MB, puede esperar un valor de tamaño de mensaje máximo realista de aproximadamente 48 MB.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Los permisos de Exchange no se aplican a los procedimientos de este tema. Estos procedimientos se realizan en el sistema operativo de Exchange Server.

  - Los cambios que guarde en el archivo de configuración Web.config se aplican después de reiniciar IIS.

  - Para permitir un incremento del 33 % en el tamaño debido a la codificación Base64, multiplique su nuevo valor de tamaño máximo deseado en megabytes por 4/3. Para convertir el valor en kilobytes, multiplíquelo por 1024. Para convertir el valor en bytes, multiplíquelo por 1048756 (1024\*1024). Tenga en cuenta que el incremento del tamaño causado por la codificación Base64 podría ser superior a 33 % y depende de varios factores, por ejemplo, el tamaño del archivo adjunto, el tipo, la compresión y el cliente de correo electrónico usado para enviar el mensaje.

  - Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Bloc de notas para configurar un límite de tamaño de mensaje específicos del cliente

1.  Abra los archivos web.config correspondientes en el Bloc de notas. Por ejemplo, para abrir los archivos web.config de los clientes de Servicios web de Exchange, ejecute los siguientes comandos:
    
        Notepad %ExchangeInstallPath%ClientAccess\exchweb\ews\web.config
        Notepad %ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config

2.  Encuentre las claves relevantes en los archivos web.config adecuados, tal y como se describe en las tablas anteriormente en el tema. Por ejemplo, para los clientes de Servicios web de Exchange, busque la clave *maxAllowedContentLength* en ambos archivos y las 14 instancias del valor `maxReceivedMessageSize="67108864"` en el archivo `web.config` en los servidores de buzones de correo.
    
        <requestLimits maxAllowedContentLength="67108864" />
        ...maxReceivedMessageSize="67108864"...
    
    Por ejemplo, para permitir un tamaño de mensaje máximo con codificación Base64 de aproximadamente 64 MB, cambie todas las instancias de `67108864` a `89478486` (64\*4/3\*1048756):
    
        <requestLimits maxAllowedContentLength="89478486" />
        ...maxReceivedMessageSize="89478486"...

3.  Cuando haya terminado, guarde y cierre los archivos web.config.

4.  Reinicie IIS ejecutando el siguiente comando:
    
        IISReset /noforce

## Configurar límites de tamaño de mensaje específicos del cliente desde la línea de comandos

En lugar de usar el Bloc de notas, también puede configurar los límites de tamaño de mensaje específicos del cliente desde la línea de comandos. Abra un símbolo del sistema con privilegios elevados en el servidor de Exchange (puede abrir una ventana de símbolo del sistema seleccionando **Ejecutar como administrador**) y ejecutar los comandos adecuados para los límites que quiere configurar.

**Notas**:

  - Los valores de tamaño en los comandos son los valores predeterminados, por lo que necesitará cambiarlos.

  - Observe si el valor está en bytes o en kilobytes.

**ActiveSync**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:appSettings /[key='MaxDocumentDataSize'].value:10240000

**Servicios web de Exchange**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpsBinding'].maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpBinding'].maxReceivedMessageSize:67108864

**Outlook Web App**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].readerQuotas.maxStringContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].readerQuotas.maxStringContentLength:35000000

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha configurado correctamente el límite de tamaño de mensaje específico del cliente, debe enviar un mensaje de prueba hacia y desde un buzón al que el cliente afectado tenga acceso. Puede probar algunos datos adjuntos más pequeños o un archivo adjunto grande para que los mensajes de prueba sean aproximadamente un 33 % inferiores al valor configurado. Por ejemplo, un valor configurado de 85 MB resulta en un tamaño de mensaje máximo realista de aproximadamente 64 MB.

