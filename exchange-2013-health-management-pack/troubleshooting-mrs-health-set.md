---
title: Solución de problemas del conjunto de mantenimiento de MRS
TOCTitle: Solución de problemas del conjunto de mantenimiento de MRS
ms:assetid: 21947ed6-1584-4db9-9cd6-f6c1de22e352
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.mrs(v=EXCHG.150)
ms:contentKeyID: 53181904
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento de MRS

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento del Servicio de replicación de buzones (MRS) supervisa el mantenimiento general del servicio de MRS.

## Explicación

El servicio de MRS se supervisa con los siguientes monitores y sondas.


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
<td><p>MRSServiceCrashingProbe</p></td>
<td><p>MRS</p></td>
<td><p>Información adicional</p></td>
<td><p>MRSServiceCrashingMonitor</p></td>
</tr>
</tbody>
</table>


Para más información sobre monitores y sondas, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta de que el conjunto de mantenimiento no está en buen estado, primero compruebe si el problema aún existe. Si el problema persiste, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje dan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje dan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento de MRS sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "MRS"}
    
    2.  Revise la salida del comando para determinar qué monitor informó del error. El valor **AlertValue** del monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar la sonda asociada para el monitor que no está en buen estado. Consulte la tabla de la sección Explicación para encontrar la sonda asociada. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **MRSServiceCrashingMonitor**. La sonda asociada con ese monitor es **MRSServiceCrashingProbe**. Para ejecutar esa sonda en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe MRS\MRSServiceCrashingProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** de la sonda. Si el valor es **Correcto**, el problema era un error temporal y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Problemas comunes

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo contiene la siguiente información:

  - Nombre del servidor que envió la alerta

  - Fecha y hora en las que ocurrió la alerta

  - Mecanismo de autenticación utilizado e información de credenciales

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica sobre el encabezado HTTP
    
    Puede usar la información del seguimiento de excepción completo para ayudar a resolver el problema. La excepción generada por la sonda contiene un motivo de error que describe por qué falló la sonda.

**Buzón de correo bloqueado**

Cuando un buzón de correo está bloqueado, puede que reciba una alerta similar a la siguiente:

*MailboxIdentity: namprd03.prod.outlook.com/Microsoft Exchange Hosted Organizations/example.com/User6 MailboxGuid: Primary (00000000-abcd-01234-5678-1234567890ab) RequestFlags: IntraOrg, Pull, Protected Base de datos: exampledb-db089 Excepción: MapiExceptionADUnavailable: Unable to prepopulate the cache for user …*

Esto indica que un buzón está bloqueado. Para desbloquear el buzón de correo, ejecute el siguiente comando:

    New-MailboxRepairRequest -CorruptionType LockedMoveTarget -Identity <mailboxIdentity> [-Archive]

**Nota**: En este comando, cambie \<*mailboxIdentity*\> por el nombre del buzón proporcionado en el mensaje de correo como **MailboxIdentity**. Si el buzón de correo es un buzón de archivo, hay que incluir la marca **–Archive**. Para determinar si un buzón es principal o de archivo, observe el campo **MailboxGuid** en la alerta.

**Trabajo de migración dañado**

Cuando un trabajo de migración resulte dañado, puede que reciba una alerta similar a la siguiente:

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Detalles: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

El daño se produce cuando los metadatos de la migración encuentran problemas. Cuando se produzca el daño, Microsoft recibirá un informe de Watson que se investigará. Para solucionar este problema, hay que quitar el lote de migración y volver a crear el lote. Para ello, siga estos pasos:

1.  Para quitar el lote dañado, ejecute el siguiente comando:
    
        Remove-MigrationBatch -Identity

2.  Para volver a crear el trabajo del lote, ejecute el siguiente comando:
    
        New-MigrationBatch -Local -Name

Para obtener más información, consulte [Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

**Alerta de MailboxMigration: error crítico**

Cuando ocurra un error crítico durante la migración de correo, puede que reciba una alerta similar a la siguiente:

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Detalles: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

Para resolver este problema, debe reintentar la migración. Para hacerlo, ejecute el siguiente comando o haga clic en el botón **Inicio** en el Centro de administración de Exchange (EAC).

    Call start-migrationbatch -Identity batchName

Cuando se produce este problema, se envía un mensaje de Dr. Watson a Microsoft para su investigación.

**El servicio de replicación de Migration Exchange no se está ejecutando**

Cuando ve el motivo de este error, puede comprobar el mantenimiento del servicio ejecutando el siguiente comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

También puede intentar iniciar el servicio ejecutando el siguiente comando:

    Start-Service msexchangemailboxreplication

**Error en el ping de RCP de MSExchangeMailboxReplication**

Cuando ve el motivo de este error, puede que reciba una alerta similar a la siguiente:

*An issue with MRS was detected at 6/26/2012 6:08:47 AM. Details: MRS RPC Ping check for server \<ServerName\> failed with the following error: The RPC endpoint for the Microsoft Exchange Mailbox Replication service couldn't respond:*

Cuando se produce este error, puede comprobar el mantenimiento del servicio ejecutando el siguiente comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

También puede intentar reiniciar el servicio ejecutando el siguiente comando:

    Restart-Service msexchangemailboxreplication

**El servicio de MSExchangeMailboxReplication se bloquea repetidamente**

Cuando el servicio de MSExchangeMailboxReplication se bloquea o deja de responder, puede que reciba una alerta similar a la siguiente:

*The MRS process has crashed at least 3 times in last 01:00:00. \<b\>Watson Message:\</b\> Watson report about to be sent for process id: 41432, con los parámetros: E12, \<ServerName\>, 15.00.0516.024, MSExchangeMailboxReplication, M.Exchange.MailboxReplicationService, M.E.M.BaseJob.BeginJob, System.ApplicationException, 7ec9, 15.00.0516.024. ErrorReportingEnabled: True.*

Cuando se produce este error, puede comprobar el mantenimiento del servicio ejecutando el siguiente comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

También puede intentar reiniciar el servicio ejecutando el siguiente comando:

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication no analiza colas de MDB**

Cuando el servicio de MSExchangeMailboxReplication no analiza colas, puede que reciba una alerta similar a la siguiente:

*An issue with MRS was detected at 6/12/2012 6:20:44 PM. Detalles: MRS queue scan check for server \<servername\> failed with the following error: The Microsoft Exchange Mailbox Replication Service isn't scanning mailbox database queues for jobs. Last scan age: 04:38:02.1959439..*

Cuando se produce este error, puede comprobar el mantenimiento del servicio ejecutando el siguiente comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

También puede intentar reiniciar el servicio ejecutando el siguiente comando:

    Restart-Service msexchangemailboxreplication

**Pasos adicionales para la solución de problemas**

1.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa del problema para comprobar que el grupo de aplicaciones de **MSExchangeServicesAppPool** se esté ejecutando.

2.  En el Administrador de IIS, haga clic en **Grupo de aplicaciones** y, luego, recicle el grupo de aplicaciones de **MSExchangeServicesAppPool** ejecutando el siguiente comando desde el Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

4.  Si el problema persiste, recicle el servicio IIS usando la utilidad IISReset o ejecutando el siguiente comando:
    
        Iisreset /noforce

5.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

6.  Si el problema persiste, reinicie el servidor.

7.  Una vez que el servidor se reinicie, vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

8.  Si la sonda sigue sin funcionar, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

