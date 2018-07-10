---
title: Solución de problemas del conjunto de mantenimiento UM.CallRouter
TOCTitle: Solución de problemas del conjunto de mantenimiento UM.CallRouter
ms:assetid: 444a9038-0952-4823-98fb-99fa59f4a378
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.um.callrouter(v=EXCHG.150)
ms:contentKeyID: 53181905
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento UM.CallRouter

 

_**Se aplica a:**  Exchange Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento del enrutador de llamadas de mensajería unificada de Microsoft Exchange supervisa el mantenimiento general del servicio de enrutador de llamadas de mensajería unificada.

Si recibe una alerta que especifica que la mensajería unificada es incorrecta, esto indica un problema que puede evitar que los usuarios utilicen el servicio de mensajería unificada en su organización. El conjunto de mantenimiento de mensajería unificada se relaciona estrechamente con los siguientes conjuntos de mantenimiento:

[Solución de problemas del conjunto de mantenimiento de mensajería unificada](troubleshooting-um-health-set.md)

[Solución de problemas del conjunto de mantenimiento UM.Protocol](troubleshooting-um-protocol-health-set.md)

## Explicación

El servicio de UM.Protocol se supervisa mediante los siguientes monitores y sondeos


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
<td><p>UMCallRouterTestProbe</p></td>
<td><p>UM.CallRouter</p></td>
<td><p>Servicios de dominio de Active Directory (AD DS)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifique que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento UM.CallRouter sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.CallRouter"}
    
    2.  Revise el resultado del comando para determinar qué monitor notificó el error. El valor de **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **UMCallRouterTestMonitor**. El sondeo asociado con ese monitor es **UMCallRouterTestProbe**. Para ejecutar ese sondeo en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe UM.CallRouter\UMCallRouterTestMonitor -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Correcto**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Pasos para la solución de problemas

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

  - Nombre del servidor que envió la alerta

  - Fecha y hora cuando ocurrió la alerta

  - Mecanismo de autenticación utilizado e información de credenciales

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica del encabezado HTTP
    
    **Nota**   Puede utilizar la información en el seguimiento de excepción completo para ayudar a resolver el problema. La excepción generada por el sondeo contiene un motivo de error que describe la causa del error del sondeo.

**Se produjeron errores en las opciones de SIP para el servicio de enrutador de llamadas de mensajería unificada**

Determine si el servicio de enrutador de llamadas de mensajería unificada está deshabilitado. Si el servicio de enrutador de llamadas de mensajería unificada no se inició o está deshabilitado, reinícielo.

**Más del 50 % de las llamadas entrantes fueron rechazadas por el enrutador de llamadas de mensajería unificada en la última hora**

Consulte los registros de eventos en el servidor de acceso de cliente (CAS) para determinar si los objetos de mensajería unificada, como **umipgateway** y **umhuntgroup**, están configurados correctamente.

Si los registros de eventos no contienen información suficiente, es posible que deba habilitar los registros de evento de mensajería unificada en el nivel experto y, luego, consultar los archivos de registro de seguimiento de mensajería unificada.

**Se produjeron errores en más del {0} % del proxy de notificaciones de llamadas perdidas en el enrutador de llamadas de mensajería unificada en la última hora**

Consulte los registros de eventos en el CAS para determinar si los objetos de mensajería unificada, como **umipgateway** y **umhuntgroup**, están configurados correctamente.

Si los registros de eventos no contienen información suficiente, es posible que deba habilitar los registros de evento de mensajería unificada en el nivel experto y, luego, consultar los archivos de registro de seguimiento de mensajería unificada.

**El certificado del enrutador de llamadas de mensajería unificada de Microsoft Exchange está cerca de su fecha de caducidad**

Renueve el certificado del servicio de enrutador de llamadas de mensajería unificada en el CAS.

**Pasos adicionales para la solución de problemas:**  

1.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa el problema para determinar si el grupo de aplicaciones **MSExchangeServicesAppPool** se está ejecutando.

2.  En el Administrador de IIS, haga clic en **Grupo de aplicaciones** y, luego, recicle el grupo de aplicaciones **MSExchangeServicesAppPool** mediante la ejecución del siguiente comando desde el Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

4.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset o mediante la ejecución del siguiente comando:
    
        Iisreset /noforce

5.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

6.  Si el problema aún persiste, reinicie el servidor.

7.  Después de reiniciar el servidor, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

8.  Si el sondeo continúa sin funcionar, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

