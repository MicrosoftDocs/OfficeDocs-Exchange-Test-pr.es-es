---
title: Solución de problemas del conjunto de mantenimiento MailboxTransport
TOCTitle: Solución de problemas del conjunto de mantenimiento MailboxTransport
ms:assetid: 02bfa4cf-6929-437e-bae5-079ea1b92373
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.mailboxtransport(v=EXCHG.150)
ms:contentKeyID: 54652477
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento MailboxTransport

 

_**Se aplica a:**Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento **MailboxTransport** supervisa el estado general de los servicios de envío de transporte de buzones y entrega de transporte de buzones en servidores de buzones de correo. Estos servicios son responsables de enviar correo hacia y desde las bases de datos de buzones de correo. Para obtener más información, vea [Flujo de correo](https://technet.microsoft.com/es-es/library/aa996349\(v=exchg.150\)).

Si recibe una alerta que indica que el conjunto de mantenimiento **MailboxTransport** no está en buen estado, indica un problema que puede impedir que se envíe o se reciba correo desde las bases de datos de buzones de correo.

## Explicación

El servicio **MailboxTransport** se supervisa con los monitores y los sondeos siguientes.


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
<td><p>MailboxDeliveryAvailability</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxDeliveryAvailabilityAggregationProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityAggregationMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxDeliveryInstanceAvailabilityProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryInstanceAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxTransportDeliveryServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportDeliveryServiceRunningMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxTransportSubmissionServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportSubmissionServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>Mapi.Submit.Probe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>Mapi.Submit.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryInterceptorStoreDriverAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportUserQuarantineMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MBTSubmissionInterceptorSubmissionAgentMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor50</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor70</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionInterceptorSubmissionAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver560Monitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento **MailboxTransport** no está en buen estado, compruebe primero que el problema todavía existe. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en la siguiente sección.

## Comprobar el problema

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor que se muestran en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para ayudar a identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra el Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar información detallada del conjunto de mantenimiento **MailboxTransport** acerca de mailbox1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "MailboxTransport"}
    
    2.  Revise el resultado del comando para determinar qué monitor notificó el error. El valor **AlertValue** para el monitor que emitió la alerta será **Unhealthy**.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Vea la tabla en la sección [Explicación](troubleshooting-activesync-health-set.md) para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **MailboxDeliveryAvailabilityMonitor**. La sonda asociada con ese monitor es **MailboxDeliveryAvailability**. Para ejecutar este sondeo en mailbox1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe MailboxTransport\MailboxDeliveryAvailabilityMonitor -Server mailbox1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise la sección "Resultado" del sondeo. Si el valor es **Correcto**, el problema fue un error transitorio y ya no existe.

