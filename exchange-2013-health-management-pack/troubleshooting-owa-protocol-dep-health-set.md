---
title: Solución de problemas del conjunto de mantenimiento OWA.Protocol.Dep
TOCTitle: Solución de problemas del conjunto de mantenimiento OWA.Protocol.Dep
ms:assetid: f39c63d5-f161-4eee-9415-05f3355e7cc7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.owa.protocol.dep(v=EXCHG.150)
ms:contentKeyID: 54652514
ms.date: 01/15/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento OWA.Protocol.Dep

 

_**Se aplica a:**Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**2015-11-10_

El conjunto de mantenimiento **OWA.Protocol.DEP** supervisa el estado general de los servicios de mensajería instantánea (MI) de Outlook Web App integrados entre Lync 2013 y Exchange 2013. Para obtener más información sobre cómo habilitar la mensajería instantánea en Outlook Web App, vea [Integración de Microsoft Lync Server 2013 y Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418).

Si recibe una alerta que indica que el conjunto de mantenimiento **OWA.Protocol.DEP** no está en buen estado, indica que hay un problema que puede impedir que la mensajería instantánea funcione correctamente en Outlook Web App.

## Explicación

El servicio **OWA.Protocol.DEP** se supervisa con los monitores y los sondeos siguientes.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sondeo</th>
<th>Conjunto de mantenimiento</th>
<th>Monitores asociados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>OwaIMInitializationFailedMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>WacDiscoveryFailureEventMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento **OWA.Protocol.DEP** no está en buen estado, compruebe primero que el problema todavía existe. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Acciones de recuperación de errores: "InstantMessageOCSProvider.InitializeEndpointManager. No registry setting for IM Provider". (InstantMessageOCSProvider.InitializeEndpointManager. No hay ninguna opción del Registro para el proveedor de mensajería instantánea).

Este error indica que falta una clave del Registro necesaria en el servidor de buzones de correo. Esta clave del Registro debe haberse configurado cuando se instaló la API Microsoft Unified Communications Managed (UCMA) 4.0 en el servidor. La clave del Registro que falta es:

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\MSExchange OWA\InstantMessaging

Esta clave debe contener una cadena **ImplementationDLLPath** cadena que apunta al archivo DLL de `Microsoft.Rtc.Internal.Ucweb`. La ubicación predeterminada es `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP\Microsoft.Rtc.Internal.Ucweb.dll`.

Para solucionar este problema, vuelva a instalar UCMA 4.0 o cree manualmente la clave del Registro. Puede descargar UCMA 4.0 aquí: [Unified Communications Managed API 4.0 Runtime](http://go.microsoft.com/fwlink/p/?linkid=260990).

## Acciones de recuperación de errores: "InstantMessageOCSProvider.InitializeEndpointManager. IM provider not found" (InstantMessageOCSProvider.InitializeEndpointManager. Proveedor de mensajería instantánea no encontrado).

Este error indica que falta el archivo DLL de `Microsoft.Rtc.Internal.Ucweb` en el servidor de buzones de correo. Este archivo debería haberse instalado cuando se instaló UCMA 4.0 en el servidor. La ubicación predeterminada es `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP`.

Para solucionar este problema, vuelva a instalar UCMA 4.0. Para obtener más información, vea [Unified Communications Managed API 4.0 Runtime](http://go.microsoft.com/fwlink/p/?linkid=260990).

## Acciones de recuperación de errores: "Instant Messaging Server name is set to null or empty on web.config" (El nombre del servidor de mensajería instantánea está establecido en NULL o vacío en web.config).

Este error indica que el servidor Lync 2013 no está definido en el archivo de configuración (web.config) de la aplicación de Outlook Web App en el servidor de buzones de correo. Este archivo `web.config` está ubicado en `%ExchangeInstallPath%ClientAccess\Owa` y debe contener una clave llamada **IMServerName** que especifica el FQDN del servidor de Lync 2013. Para solucionar este problema, siga estos pasos:

1.  En una ventana de símbolo del sistema, abra el archivo web.config de Outlook Web App en el Bloc de notas ejecutando el siguiente comando:
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  Busque una clave llamada **IMServerName**. Si la encuentra, compruebe el FQDN del servidor de Lync 2013. Si no encuentra la clave, siga los pasos siguientes para agregarla.
    
    1.  Busque la etiqueta llamada **\<appSettings\>**.
    
    2.  En el nodo **\<appSettings\>**, agregue la siguiente línea:
        
            <add key="IMServerName" value="Lync Server FQDN" />
        
        Por ejemplo:
        
            <add key="IMServerName" value="lync01.contoso.com" />
    
    3.  Para aplicar los cambios en Outlook Web App, ejecute el siguiente comando:
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## Acciones de recuperación de errores: "Instant Messaging Certificate Thumbprint is null or empty on web.config" (La huella digital del certificado de mensajería instantánea es NULL o está vacía en web.config).

Este error indica que el certificado que se utiliza para integrar Lync 2013 y Outlook Web App no está definido en el archivo de configuración (web.config) de la aplicación de Outlook Web App en el servidor de buzones de correo. Este archivo `web.config` está ubicado en `%ExchangeInstallPath%ClientAccess\Owa`, y debe contener una clave llamada **IMCertificateThumbprint** que especifica la huella digital del certificado (hash).

Puede obtener el valor de huella digital del certificado mediante el cmdlet **Get-ExchangeCertificate**, o en el Centro de administración de Exchange (EAC) en **Servidores**\>**Certificados**.

Para solucionar este problema, siga estos pasos:

1.  En una ventana de símbolo del sistema, abra el archivo web.config de Outlook Web App en el Bloc de notas ejecutando el siguiente comando:
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  Busque una clave llamada **IMCertificateThumbprint**. Si se encuentra, compruebe que el valor de la huella digital es correcto. Si no encuentra la clave, siga los pasos siguientes para agregarla:
    
    1.  Busque la etiqueta llamada **\<appSection\>**.
    
    2.  En el nodo **\<appSection\>**, agregue la siguiente línea:
        
            <add key="IMCertificateThumbprint" value="thumbprint"/>
        
        Por ejemplo:
        
            <add key="IMCertificateThumbprint" value="35CB4C441D55506C88E59B7946B567A4F45B3B5C" />
    
    3.  Para aplicar los cambios en Outlook Web App, ejecute el siguiente comando:
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## Acciones de recuperación de errores: "IM Certificate with thumbprint \<value\> could not be found" (No se encontró el certificado de mensajería instantánea con el \<valor\> de huella digital).

Este error indica que el certificado que se utiliza para integrar Lync 2013 y Outlook Web App no se encuentra en el servidor de buzones de correo. Este certificado debe instalarse en el servidor de buzones de correo y en el servidor de Lync 2013, y debe ser de confianza para ambos servidores. Para obtener más información acerca de los requisitos de certificados, vea la sección Habilitar la mensajería instantánea en Outlook Web App en [Integrar Microsoft Lync Server 2013 y Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418).

Puede comparar el valor de huella digital del error con el certificado usando el cmdlet **Get-ExchangeCertificate**, o en el Centro de administración de Exchange (EAC) en **Servidores**\>**Certificados**.

## Acciones de recuperación de errores: "IM Certificate has expired" (El certificado de mensajería instantánea ha expirado).

Este error indica que el certificado que se utiliza para integrar Lync 2013 y Outlook Web App ha expirado. Para resolver este error, debe renovar el certificado.

Puede comparar el valor de huella digital del error con el certificado usando el cmdlet **Get-ExchangeCertificate**, o en el Centro de administración de Exchange (EAC) en **Servidores**\>**Certificados**.

## Acciones de recuperación de errores: "IM Certificate has not become valid yet" (El certificado de mensajería instantánea aún no es válido).

Este error indica que el certificado que se utiliza para integrar Lync 2013 y Outlook Web App contiene fechas no válidas. Para resolver este error, debe configurar un nuevo certificado y debe agregar el nuevo valor de huella digital en la clave **IMCertificateThumbprint** en `%ExchangeInstallPath%ClientAccess\Owa\web.config`. Para obtener más información acerca de los requisitos de certificados, vea la sección Habilitar la mensajería instantánea en Outlook Web App en [Integrar Microsoft Lync Server 2013 y Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418).

## Acciones de recuperación de errores: "IM Certificate does not have a private key" (El certificado de mensajería instantánea no tiene una clave privada).

Este error indica que el certificado que se utiliza para integrar Lync 2013 y Outlook Web App no tiene una clave privada. Para resolver este error, debe configurar un nuevo certificado que tenga una clave privada y debe agregar el nuevo valor de huella digital en la clave **IMCertificateThumbprint** en `%ExchangeInstallPath%ClientAccess\Owa\web.config`. Para obtener más información acerca de los requisitos de certificados, vea la sección Habilitar la mensajería instantánea en Outlook Web App en [Integrar Microsoft Lync Server 2013 y Microsoft Outlook Web App 2013](http://go.microsoft.com/fwlink/p/?linkid=280418).

