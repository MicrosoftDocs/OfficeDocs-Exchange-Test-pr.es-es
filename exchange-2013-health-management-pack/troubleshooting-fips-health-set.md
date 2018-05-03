---
title: Solución de problemas del conjunto de mantenimiento FIPS
TOCTitle: Solución de problemas del conjunto de mantenimiento FIPS
ms:assetid: 96e1b096-9cb5-426f-a84e-50d5599e4bbb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.fips(v=EXCHG.150)
ms:contentKeyID: 54652501
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento FIPS

 

_**Se aplica a:**Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento **FIPS** supervisa el estado general de la configuración de Federal Information Processing Standards (FIPS) en los servidores de Exchange. Para obtener más información acerca de FIPS 140, vea [Validación de FIPS 140](http://go.microsoft.com/fwlink/p/?linkid=521913).

Si recibe una alerta que indica que el conjunto de mantenimiento **FIPS** no está en buen estado, indica que hay un problema que puede impedir que el servidor de Exchange use los componentes y procesos compatibles con FIPS 140.

## Explicación

El servicio **FIPS** se supervisa con los monitores y los sondeos siguientes.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>Conjunto de mantenimiento</th>
<th>Monitores asociados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>FIPS</p></td>
<td><p>CrashEvent.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceFailureMonitor.FIPS</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceTimeoutMonitor.FIPS</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetError.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeError.scanningprocess</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento **FIPS** no está en buen estado, compruebe primero que el problema todavía existe. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en la siguiente sección.

## Comprobar el problema

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor que se muestran en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para ayudar a identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra el Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento **FIPS** sobre server1.contoso.com, ejecute el comando siguiente:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "FIPS"}
    
    2.  Revise el resultado del comando para determinar qué monitor notificó el error. El valor **AlertValue** para el monitor que emitió la alerta será **Unhealthy**.

