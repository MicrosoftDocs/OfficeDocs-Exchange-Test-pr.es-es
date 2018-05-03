---
title: Solución de problemas del conjunto de mantenimiento HubTransport
TOCTitle: Solución de problemas del conjunto de mantenimiento HubTransport
ms:assetid: e3932ce3-836c-4230-9f64-63af1b704d79
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.hubtransport(v=EXCHG.150)
ms:contentKeyID: 54652512
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento HubTransport

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento **HubTransport** supervisa el estado general de la canalización de transporte en los servidores de buzones de correo que se encargan de redirigir el correo de su organización. Para obtener más información, vea [Flujo de correo](https://technet.microsoft.com/es-es/library/aa996349\(v=exchg.150\)).

Si recibe una alerta que indica que el conjunto de mantenimiento **HubTransport** no está en buen estado, indica que hay un problema que puede impedir que el correo se redirija y se entregue.

## Explicación

El servicio **HubTransport** se supervisa con los monitores y los sondeos siguientes.


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
<td><p>ActiveQueueDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ActiveQueueDrainFailureMonitor</p></td>
</tr>
<tr class="even">
<td><p>DiagnosticsAggregationLocalSnapshotProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationLocalSnapshotMonitor</p></td>
</tr>
<tr class="odd">
<td><p>DiagnosticsAggregationWebServiceProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationWebServiceMonitor</p></td>
</tr>
<tr class="even">
<td><p>HubAvailabilityProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>HubAvailabilityMonitor</p></td>
</tr>
<tr class="odd">
<td><p>HubTransportServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransportServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>ShadowQueueDiscardDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ShadowQueueDiscardDrainFailureMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ThrottlingServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>ThrottlingServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>TransportEdgeSync.Service.Probe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportEdgeSync.Service.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>TransportLogSearchRunningProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>BootloaderOutstandingItemsTriggerMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>EdgeTransportBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>FederatedDecryptionAgentFailedToXDecryptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransport.ServiceInconsistentState.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverExpandedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverResolvedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Messages.failed.to.be.made.redundant.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>MessagesDeferredDuringCategorizationMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>MessageTrackingLogsDirQuotaMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchahangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangethrottling</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangetransport</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueExternalAggregateMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueMailboxRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueNonSMTPRetryMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleExcessiveForkingEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>SmtpProxyEhloOptionsDoNotMatchContinueProxyingMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>SubmissionQueueMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TlsDomainClientCertificateSubjectMismatchMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Total.Shadow.Queue.Length.Above.Threshold.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyHighForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyLowForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyNormalForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.CatExpiry.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Critical.Storage.Recovery.Failed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DatabaseMoved.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCert.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCertAuth.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerCertFailed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerDomainCertFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.FailedToCreatePickupDirectory.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.InvalidAcceptedDomain.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.LowDiskSpace.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Messages.Completing.Categorization.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.NDRForUnrestrictedLargeDL.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupDelete.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupIsBadmailingFile.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConn.AuthKerb.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnAuth.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnTLS.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertExpireSoon.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertMismatch.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServiceStartError.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SmtpSendDirectTrustFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TemplateDoesNotExist.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TLSValidate.Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.UnknownTemplateInPublishingLicense.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportCategorizerJobAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDatabaseCorruptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailures544Monitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver520Monitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogGenerationCheckpointDepthMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchLogPathInvalidMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportMaxLocalLoopCountMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPickupReadMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPoisonMessageMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportRejectingMessageSubmissionsMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportServerCertPersonalStoreMonitor</p></td>
</tr>
<tr class="even">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>UnreachableQueueMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ninguna (notificación o verificación)</p></td>
<td><p>HubTransport</p></td>
<td><p>XProxyToTransientInvalidArgumentsMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento **HubTransport** no está en buen estado, compruebe primero que el problema todavía existe. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en la siguiente sección.

## Comprobar el problema

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor que se muestran en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para ayudar a identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra el Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar información detallada del conjunto de mantenimiento **HubTransport** acerca de mailbox1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "HubTransport"}
    
    2.  Revise el resultado del comando para determinar qué monitor notificó el error. El valor **AlertValue** para el monitor que emitió la alerta será **Unhealthy**.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Vea la tabla en la sección [Explicación](troubleshooting-activesync-health-set.md) para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **ActiveQueueDrainFailureMonitor**. El sondeo asociado con ese monitor es **ActiveQueueDrainFailureProbe**. Para ejecutar este sondeo en mailbox1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe HubTransport\ActiveQueueDrainFailureProbe -Server mailbox1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise la sección "Resultado" del sondeo. Si el valor es **Correcto**, el problema fue un error transitorio y ya no existe.

