---
title: Solución de problemas del conjunto de mantenimiento de mensajería unificada
TOCTitle: Solución de problemas del conjunto de mantenimiento de mensajería unificada
ms:assetid: db947791-63ce-45dd-8634-1dfa5f55e2c2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.um(v=EXCHG.150)
ms:contentKeyID: 53181923
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento de mensajería unificada

 

_**Se aplica a:**  Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento de mensajería unificada (UM) supervisa el mantenimiento general del servicio de la mensajería unificada en su organización.

Si recibe una alerta que especifica que la mensajería unificada es incorrecta, esto indica un problema que puede impedir que los usuarios usen el servicio de la mensajería unificada en su organización. El conjunto de mantenimiento de la mensajería unificada se relaciona estrechamente con los siguientes conjuntos de mantenimiento:

[Solución de problemas del conjunto de mantenimiento UM.CallRouter](troubleshooting-um-callrouter-health-set.md)

[Solución de problemas del conjunto de mantenimiento UM.Protocol](troubleshooting-um-protocol-health-set.md)

## Explicación

El servicio de mensajería unificada se supervisa mediante los siguientes monitores y sondas.


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
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Servicios de dominio de Active Directory (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>UMCallRouterTestProbe</p></td>
<td><p>UM.CallRouter</p></td>
<td><p>Servicios de dominio de Active Directory (AD DS)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
</tr>
</tbody>
</table>


Para más información sobre monitores y sondas, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento UM.Protocol acerca de server1.contoso.com, ejecute el comando siguiente:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  Revise el resultado del comando para determinar qué monitor informó el error. El valor **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar la sonda asociada para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar la sonda asociada. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **UMSelfTestMonitor**. La sonda asociada con ese monitor es **UMSelfTestProbe**. Para ejecutar esa sonda en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Satisfactorio**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Pasos para la solución de problemas

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

  - Nombre del servidor que envió la alerta

  - Fecha y hora cuando ocurrió la alerta

  - Mecanismo de autenticación utilizado e información de credenciales

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica sobre el encabezado HTTP
    
    **Nota**   Puede usar la información del seguimiento completo de excepción para solucionar el problema. La excepción generada por la sonda contiene un motivo de error que describe por qué la sonda presentó errores.

**Las opciones de SIP para el servicio de mensajería unificada son erróneas**

Determine si el servicio de mensajería unificada está deshabilitado. Si el servicio de mensajería unificada no se inició o está deshabilitado, reinicie el servicio de mensajería unificada.

**El servicio de mensajería unificada rechazó más del {0}% de llamadas entrantes en la última hora**

Consulte los registros de eventos en el servidor de acceso de cliente (CAS) para determinar si los objetos de la mensajería unificada, como **umipgateway** y **umhuntgroup**, están configurados correctamente.

Si los registros de eventos no contienen información suficiente, es posible que deba habilitar los registros de evento de la mensajería unificada en el nivel experto y, luego, consultar los archivos de registro de seguimiento de la mensajería unificada.

**El proceso de trabajo de la mensajería unificada rechazó más del {0}% de llamadas entrantes en la última hora**

Consulte los registros de eventos en el CAS para determinar si los objetos de la mensajería unificada, como **umipgateway** y **umhuntgroup**, están configurados correctamente.

Si los registros de eventos no contienen información suficiente, es posible que deba habilitar los registros de evento de la mensajería unificada en el nivel experto y, luego, consultar los archivos de registro de seguimiento de la mensajería unificada.

**Se procesaron correctamente menos del {0} % de los mensajes en la última hora**

Consulte los registros de eventos en el CAS para determinar si los objetos de la mensajería unificada, como **umipgateway** y **umhuntgroup**, están configurados correctamente.

Si los registros de eventos no contienen información suficiente, es posible que deba habilitar los registros de evento de la mensajería unificada en el nivel experto y, luego, consultar los archivos de registro de seguimiento de la mensajería unificada.

**El servicio de mensajería unificada de Microsoft Exchange rechazó una llamada porque la canalización de la mensajería unificada estaba completa**

Consulte los registros de eventos en el CAS para determinar si los objetos de la mensajería unificada, como **umipgateway** y **umhuntgroup**, están configurados correctamente.

Si los registros de eventos no contienen información suficiente, es posible que deba habilitar los registros de evento de la mensajería unificada en el nivel experto y, luego, consultar los archivos de registro de seguimiento de la mensajería unificada.

**El servicio perimetral A/V está mal configurado o no se está ejecutando**

1.  Revise los registros de eventos en el servidor de buzones para intentar determinar por qué son erróneas las llamadas de Lync Server. A continuación, haga lo siguiente:
    
      - Asegúrese de que funcione el grupo Lync seleccionado por el servicio de la mensajería unificada.
    
      - Para usar un Lync Server específico, ejecute el siguiente comando:
        
            Set-UMServer ExchangeUMServer -SIPAccessService <ServerName>

**El servidor de mensajería unificada no pudo obtener credenciales correctamente con el servicio perimetral A/V del servidor de comunicaciones**

Revise los registros de eventos para investigar qué grupo Lync se seleccionó y para comprobar que funcione el grupo Lync seleccionado.

**El perímetro de audio y vídeo del servidor de comunicaciones no pudo abrir un puerto o asignar recursos mientras intentaba establecer una sesión**

Revise los registros de eventos para investigar qué grupo Lync se seleccionó y para comprobar que funcione el grupo Lync seleccionado.

**El certificado de servicio de mensajería unificada de Microsoft Exchange se acerca a su fecha de expiración**

Renueve el certificado del servicio de mensajería unificada en el servidor de buzones.

**Pasos adicionales para la solución de problemas:**  

1.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa el problema para determinar si el grupo de aplicaciones de **MSExchangeServicesAppPool** se está ejecutando.

2.  En el Administrador de IIS, haga clic en **Grupos de aplicaciones** y, luego, recicle el grupo de aplicaciones **MSExchangeServicesAppPool**. Para ello, ejecute el siguiente comando desde Shell de administración de Exchange:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Vuelva a ejecutar la sonda asociada, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

4.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset o ejecutando el siguiente comando:
    
        Iisreset /noforce

5.  Vuelva a ejecutar la sonda asociada, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

6.  Si el problema aún persiste, reinicie el servidor.

7.  Después de reiniciar el servidor, vuelva a ejecutar la sonda asociada, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

8.  Si el sondeo continúa dando error, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

