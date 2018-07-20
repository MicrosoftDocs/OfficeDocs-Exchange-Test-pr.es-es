---
title: Solución de problemas del conjunto de mantenimiento OWA.Proxy
TOCTitle: Solución de problemas del conjunto de mantenimiento OWA.Proxy
ms:assetid: 1eaa26ad-b489-402a-ad2d-bfae3b083f42
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.owa.proxy(v=EXCHG.150)
ms:contentKeyID: 53181902
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento OWA.Proxy

 

_**Se aplica a:**  Exchange Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento OWA.Proxy supervisa el mantenimiento general del servicio Outlook Web App.

Si recibe una alerta que indica que OWA.Proxy no está en buen estado, significa que existe un problema que puede impedir a los usuarios usar el servicio Outlook Web App.

## Explicación

El servicio Outlook Web App se supervisa con los monitores y las sondas siguientes.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>Conjunto de mantenimiento</th>
<th>Dependencias</th>
<th>Monitores asociados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OWAProxyTestProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OWAanonymouscalendarProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Para más información sobre monitores y sondas, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Esta sonda puede fallar por cualquiera de los siguientes motivos comunes:

  - El grupo de aplicaciones hospedado en el servidor de acceso de cliente (CAS) supervisado no funciona correctamente.

  - Las credenciales de la cuenta de supervisión son incorrectas.

  - Los controladores de dominio no responden.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta de que el conjunto de mantenimiento no está en buen estado, primero compruebe si el problema aún existe. Si el problema persiste, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje dan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje dan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del sistema de estado OWA.Proxy sobre server1.contoso.com, ejecute el comando siguiente:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
    
    2.  Revise la salida del comando para saber qué monitor informó del error. El valor **AlertValue** del monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar la sonda asociada para el monitor que no está en buen estado. Consulte la tabla de la sección Explicación para encontrar la sonda asociada. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **OWAProxyTestMonitor**. La sonda asociada con ese monitor es **OWAProxyTestProbe**. Para ejecutar esa sonda en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  En la salida del comando, revise el valor **Resultado** de la sonda. Si el valor es **Correcto**, el problema era un error temporal y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de OWAProxyTestMonitor

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo contiene la siguiente información:

  - Nombre del CAS que envió la alerta

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica de encabezado HTTP  
    
    **Nota**: Puede usar la información del seguimiento de excepción completo para resolver el problema.

  - Fecha y hora en que ocurrió el problema

Para resolver este problema, siga estos pasos:

1.  Consulte los registros de protocolo en los servidores de CA. Los registros de protocolo se ubican en la carpeta del *\<directorio de instalación del servidor exchange\>*\\Logging\\HttpProxy*\\\<protocol\>* en el CAS.

2.  Cree una cuenta de usuario de prueba y, luego, inicie sesión en el CAS con dicha cuenta. Por ejemplo, inicie sesión con: https:// *\<nombre del servidor\>*/owa.

3.  Inicie el administrador de IIS y conéctese al servidor que ha avisado del problema para determinar si los grupos de aplicaciones **MSExchangeServicesAppPools** se ejecutan en el CAS.

4.  Haga clic en **Grupos de aplicaciones** y recicle los grupos de aplicaciones **MSExchangeOWAAppPool** y **MSExchangeOWACalendarAppPool** ejecutando el comando siguiente del Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWACalendarAppPool

5.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

6.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset.

7.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

8.  Si el problema persiste, reinicie el servidor.

9.  Una vez que el servidor se reinicie, vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

10. Si la sonda sigue sin funcionar, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

[Administración de Outlook Web App](https://technet.microsoft.com/es-es/3814b665-01e8-4881-9a44-163f14789ee4\(exchg.150\)#managing)

