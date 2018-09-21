---
title: 'Habilitar compatibilidad para agentes transporte heredados: Exchange 2013 Help'
TOCTitle: Habilitar la compatibilidad para agentes de transporte heredados
ms:assetid: 00617e87-7199-406e-b4a3-94378f657f1f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ591524(v=EXCHG.150)
ms:contentKeyID: 49115999
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar la compatibilidad para agentes de transporte heredados

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

En Microsoft Exchange Server 2013, los agentes de transporte creados con Microsoft .NET Framework versión 4.0 son compatibles de forma predeterminada. Exchange 2013 es compatible con agentes de soporte creados con versiones previas de .NET Framework, pero la compatibilidad con estos agentes de transporte heredados no está habilitada de forma predeterminada. Para habilitar la compatibilidad con los agentes de transporte heredados, deberá modificar el archivo de configuración de la aplicación XML adecuada. Los archivos que debe modificar dependen del agente de transporte instalado:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Archivos de configuración de la aplicación</th>
<th>Servicio de Microsoft Windows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidor de Acceso del cliente</p></td>
<td><p>%ExchangeInstallPath%Bin\MSExchangeFrontendTransport.exe.config</p></td>
<td><p>Transporte front-end de Microsoft Exchange (MSExchangeFrontendTransport)</p></td>
</tr>
<tr class="even">
<td><p>Servidor de buzones</p></td>
<td><ul>
<li><p>%ExchangeInstallPath%Bin\EdgeTransport.exe.config</p></li>
<li><p>%ExchangeInstallPath%Bin\MSExchangeTransport.exe.config</p></li>
</ul></td>
<td><p>Transporte de Microsoft Exchange (MSExchangeTransport)</p></td>
</tr>
</tbody>
</table>


La compatibilidad de los agentes de transporte heredados está controlada por las claves en los archivos de configuración de la aplicación. De forma predeterminada, ninguna de las claves necesarias está presente en los archivos de configuración de la aplicación. Debe agregar las claves manualmente. La tabla siguiente explica todas las claves con mayor detalle.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tecla</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>useLegacyV2RuntimeActivationPolicy</em></p></td>
<td><p>Esta clave habilita o deshabilita la compatibilidad con los agentes de transporte heredados. Los valores válidos para esta clave son <code>true</code> o <code>false</code>. Si no se especifica esta clave, el valor predeterminado es <code>false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>supportedRuntime version</em></p></td>
<td><p>Esta clave especifica la versión de Microsoft .NET Framework que necesita el agente. Los valores válidos para esta clave son:</p>
<ul>
<li><p><code>v4.0</code> o <code>v4.0.30319</code></p></li>
<li><p><code>v3.5</code> o <code>v3.5.21022</code></p></li>
<li><p><code>v3.0</code> o <code>v3.0.4506</code></p></li>
<li><p><code>v2.0</code> o <code>v2.0.50727</code></p></li>
</ul>
<p>Especifica varios valores usando varias instancias independientes de la clave <em>supportedRuntime version</em>.</p>
<p>Cuando habilite la compatibilidad del agente de transporte heredado con la clave <em>useLegacyV2RuntimeActivationPolicy</em>, siempre debería especificar el valor <code>v4.0</code> además de los valores que necesita el agente de transporte heredado.</p></td>
</tr>
</tbody>
</table>


## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Los permisos de Exchange no se aplican a los procedimientos de este tema. Estos procedimientos se realizan en el sistema operativo de Exchange Server.

  - Los cambios que guarde en un archivo de configuración de la aplicación se aplican después de reiniciar el servicio correspondiente.

  - Cuando reinicie alguno de estos servicios asociados con los archivos de configuración de la aplicación, el flujo de correo en el servidor se interrumpirá temporalmente.

  - Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilice el símbolo del sistema para configurar la compatibilidad de los agentes de transporte heredados

Utilice el siguiente procedimiento para habilitar la compatibilidad de los agentes de transporte heredados:

1.  En la ventana del símbolo del sistema, en el servidor Exchange 2013 donde quiere configurar la compatibilidad del agente de transporte heredado, abra el archivo de configuración de la aplicación adecuada en el Bloc de notas ejecutando el siguiente comando:
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\<AppConfigFile>
```
    
    Por ejemplo, para abrir el archivo EdgeTransport.exe.config en un servidor de buzones de correo, ejecute el siguiente comando:
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

2.  Busque la clave *\</configuration\>* al final del archivo y copie las siguientes claves antes de la clave *\</configuration\>*:
    
        <startup useLegacyV2RuntimeActivationPolicy="true">
           <supportedRuntime version="v4.0" />
           <supportedRuntime version="v3.5" />
           <supportedRuntime version="v3.0" />
           <supportedRuntime version="v2.0" />
        </startup>

3.  Cuando finalice, guarde y cierre el archivo de configuración de la aplicación.

4.  Repita los pasos 1 a 3 para modificar los otros archivos de configuración de la aplicación.

5.  Reinicie el servicio Windows asociado ejecutando el siguiente comando:
    
        net stop <service> && net start <service>
    
    Por ejemplo, si modificó el archivo EdgeTransport.exe.config, debe reiniciar el servicio de transporte de Microsoft Exchange ejecutando el siguiente comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

6.  Repita el paso 5 para reiniciar los servicios asociados con los otros archivos de configuración de la aplicación modificados.

## ¿Cómo saber si el proceso se ha completado correctamente?

Sabrá que este procedimiento funciona si el agente de transporte heredado se instala correctamente. Si intenta instalar un agente de transporte heredado sin realizar el procedimiento de este tema, recibirá un error similar al siguiente:

    Mixed mode assembly is built against version '<version>' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.

