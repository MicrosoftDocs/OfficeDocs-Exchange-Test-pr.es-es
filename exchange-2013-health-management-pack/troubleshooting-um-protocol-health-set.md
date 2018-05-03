---
title: Solución de problemas del conjunto de mantenimiento UM.Protocol
TOCTitle: Solución de problemas del conjunto de mantenimiento UM.Protocol
ms:assetid: 8dd9a16f-77a1-4a8d-aea4-5e96ab922dd4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.um.protocol(v=EXCHG.150)
ms:contentKeyID: 53181911
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento UM.Protocol

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento UM.Protocol supervisa el protocolo de la mensajería unificada (UM) en el servidor de buzones de correo.

Si recibe una alerta que especifica que UM.Protocol no está en buen estado, significa que existe un problema que puede evitar que los usuarios utilicen el servicio de mensajería unificada en su organización. El conjunto de mantenimiento UM.Protocol está estrechamente relacionado con los conjuntos de mantenimiento siguientes:

[Solución de problemas del conjunto de mantenimiento de mensajería unificada](troubleshooting-um-health-set.md)

[Solución de problemas del conjunto de mantenimiento UM.CallRouter](troubleshooting-um-callrouter-health-set.md)

## Explicación

El servicio de UM.Protocol se supervisa mediante los monitores y pruebas siguientes.


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
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento UM.Protocol acerca de server1.contoso.com, ejecute el comando siguiente:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  Revise el resultado del comando para determinar qué monitor informó del error. El valor **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **UMSelfTestMonitor**. El sondeo asociado con ese monitor es **UMSelfTestProbe**. Para ejecutar ese sondeo en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Satisfactorio**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Pasos para la solución de problemas

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

  - Nombre del servidor que envió la alerta

  - Fecha y hora cuando ocurrió la alerta

  - Mecanismo de autenticación utilizado e información de credenciales

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica sobre el encabezado HTTP
    
    **Nota**   Puede utilizar la información en el seguimiento de excepción completo para ayudar a resolver el problema. La excepción generada por el sondeo contiene un motivo de error que describe por qué falló el sondeo.

Para obtener más información acerca de la solución de problemas de mensajes de alerta de UM, consulte [Solución de problemas del conjunto de mantenimiento de mensajería unificada](troubleshooting-um-health-set.md)

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

