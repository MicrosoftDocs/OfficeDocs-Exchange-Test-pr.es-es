---
title: Solución de problemas del conjunto de mantenimiento del ECP
TOCTitle: Solución de problemas del conjunto de mantenimiento del ECP
ms:assetid: 0a1cfcd5-585c-4a0a-9d3c-28dc49e16a6c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.ecp(v=EXCHG.150)
ms:contentKeyID: 53181900
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento del ECP

 

_**Se aplica a:**Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento del panel de control de Exchange (ECP) supervisa el mantenimiento general del Centro de administración de Exchange y del servicio de configuración de usuarios de Outlook Web App (OWA). El conjunto de mantenimiento del ECP está estrechamente relacionado con el conjunto de mantenimiento siguiente:

[Solución de problemas del conjunto de mantenimiento ECP.Proxy](troubleshooting-ecp-proxy-health-set.md)

Si recibe una alerta que indica que el conjunto de mantenimiento EAC no funciona bien, significa que existe un problema que puede impedir a los usuarios acceder al EAC.

## Explicación

El servicio del EAC se supervisa con los monitores y pruebas siguientes.


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
<td><p>EacSelfTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EacDeepTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Para más información sobre monitores y sondas, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo contiene la siguiente información:

  - Nombre del servidor que envió la alerta

  - Fecha y hora en las que ocurrió la alerta

  - Información de autenticación y credenciales

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica del encabezado HTTP
    
    **Nota**: Puede usar la información del seguimiento de excepción completo para resolver el problema.

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta de que el conjunto de mantenimiento no está en buen estado, primero compruebe si el problema aún existe. Si el problema persiste, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje dan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje dan la suficiente información de solución de problemas para identificar la raíz del problema. Si no están claros los detalles del mensaje, siga estos pasos:
    
    1.  Abra Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth -Identity <ServerName> -HealthSet <HealthSetName>
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento ECP sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth -Identity server1.contoso.com -HealthSetName ECP
    
    2.  Revise la salida del comando para saber qué monitor informó del error. El valor **AlertValue** del monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar la sonda asociada para el monitor que no está en buen estado. Consulte la tabla de la sección Explicación para encontrar la sonda asociada. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <HealthSetName>\<ProbeName> -Server <ServerName> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **EacSelfTestMonitor**. La sonda asociada con ese monitor es **EacSelfTestProbe**. Para ejecutar esa sonda en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe ECP\EacSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  En la salida del comando, revise el valor **Resultado** de la sonda. Si el valor es **Correcto**, el problema era un error temporal y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de EacSelfTestMonitor y EacDeepTestMonitor

1.  Inicie el administrador de IIS y luego conéctese al servidor que informó del problema. Haga clic en **Grupos de aplicaciones** y recicle el grupo de aplicaciones del ECP llamado **MSExchangeECPAppPool**.

2.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

3.  Si el problema persiste, recicle todo el servicio de IIS con la utilidad IISReset.

4.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

5.  Si la sonda falla, reinicie el servidor.

6.  Una vez que el servidor se reinicie, vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

7.  Si la sonda sigue sin funcionar, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

[Centro de administración de Exchange en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150562\(v=exchg.150\))

