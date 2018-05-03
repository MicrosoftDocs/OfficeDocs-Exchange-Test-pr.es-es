---
title: Solución de problemas del conjunto de mantenimiento de ActiveSync
TOCTitle: Solución de problemas del conjunto de mantenimiento de ActiveSync
ms:assetid: 8a0b8b26-b4ef-41b8-8f71-8271c1735a69
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.activesync(v=EXCHG.150)
ms:contentKeyID: 53181912
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento de ActiveSync

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento de Exchange ActiveSync supervisa el estado general del servicio de ActiveSync para los clientes móviles de su organización. El conjunto de mantenimiento de ActiveSync está estrechamente relacionado con los conjuntos de mantenimiento siguientes:

[Solución de problemas del conjunto de mantenimiento de ActiveSync.Protocol](troubleshooting-activesync-protocol-health-set.md)

[Solución de problemas del conjunto de mantenimiento ActiveSync.Proxy](troubleshooting-activesync-proxy-health-set.md)

Si recibe una alerta que especifica que el conjunto de mantenimiento de ActiveSync no está en buen estado, significa que existe un problema que puede evitar que los usuarios obtengan acceso a sus buzones de correo mediante ActiveSync.

## Explicación

El servicio de ActiveSync se controla mediante los monitores y los sondeos siguientes.


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
<td><p>ActiveSyncCTPProbe</p></td>
<td><p>ActiveSync</p></td>
<td><p>Active Directory</p>
<p>Autenticación</p>
<p>Autenticación del servidor de buzones de correo</p>
<p>Información adicional</p>
<p>Alta disponibilidad</p>
<p>Red</p></td>
<td><p>ActiveSyncCTPMonitor (conjunto de mantenimiento de ActiveSync)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncProxyTestProbe</p></td>
<td><p>ActiveSync.Proxy</p></td>
<td><p>-</p></td>
<td><p>ActiveSyncProxyTestMonitor (conjunto de mantenimiento de ActiveSync.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSyncDeepTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticación</p>
<p>Información adicional</p>
<p>Alta disponibilidad</p></td>
<td><p>ActiveSyncDeepTestMonitor (conjunto de mantenimiento de ActiveSync)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncSelfTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticación</p></td>
<td><p>ActiveSyncSelfTestMonitor (conjunto de mantenimiento de ActiveSync.Protocol)</p>
<p>RequestsQueuedGt500Monitor (conjunto de mantenimiento de ActiveSync)</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando recibe una alerta que especifica que el conjunto de mantenimiento de ActiveSync no está en buen estado, compruebe primero que el problema todavía exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar el problema

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor que se muestran en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para ayudar a identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento de ActiveSync acerca de server1.contoso.com, ejecute el comando siguiente:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ActiveSync"}
    
    2.  Revise el resultado del comando para determinar qué monitor informó del error. El valor **AlertValue** para el monitor que emitió la alerta será **Unhealthy**.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene el estado incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **ActiveSyncCTPMonitor**. El sondeo asociado con ese monitor es **ActiveSyncCTPProbe**. Para ejecutar este sondeo en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe ActiveSync\ActiveSyncCTPProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise la sección de "Resultado" del sondeo. Si el valor es **Satisfactorio**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de ActiveSyncDeepTestMonitor y ActiveSyncSelfTestMonitor

Normalmente, esta alerta de monitor se emite para servidores de buzones de correo. Para realizar acciones de recuperación, siga estos pasos:

1.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa del problema. Haga clic en **Grupos de aplicaciones** y, luego, recicle el grupo de aplicaciones de ActiveSync que se denomina **MSExchangeSyncAppPool**.

2.  Vuelva a ejecutar el sondeo asociado tal y como se muestra en el paso 2c de la sección Comprobar el problema.

3.  Si el problema aún persiste, recicle todo el servicio de IIS con la utilidad IISReset.

4.  Vuelva a ejecutar el sondeo asociado tal y como se muestra en el paso 2c de la sección Comprobar el problema.

5.  Si el problema aún persiste, reinicie el servidor. Para ello, realice primero la conmutación por error de las bases de datos hospedadas en el servidor mediante el comando siguiente:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    En este y todos los ejemplos de código siguientes, reemplace *server1.contoso.com* por el nombre real del servidor.

6.  A continuación, compruebe que todas las bases de datos se hayan trasladado fuera del servidor que informa del problema. Para comprobarlo, ejecute el siguiente comando:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status

7.  Si el resultado del comando del paso 6 no muestra ninguna copia activa en el servidor, reinicie el servidor. Si el resultado efectivamente muestra copias activas, ejecute nuevamente los pasos 5 y 6.

8.  Una vez que el servidor se reinicia, vuelva a ejecutar el sondeo asociado tal y como se muestra en el paso 2c de la sección Comprobar el problema.

9.  Si el sondeo tiene éxito, realice la conmutación por error de las bases de datos mediante la ejecución del siguiente comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

10. Si el sondeo continúa con error, es posible que necesite más ayuda para resolver el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Acciones de recuperación de ActiveSyncCTPMonitor

Normalmente, esta alerta de monitor se emite para servidores de CA (CAS).

1.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa del problema. Haga clic en **Grupos de aplicaciones** y, luego, recicle el grupo de aplicaciones de ActiveSync que se denomina **MSExchangeSyncAppPool**.

2.  Vuelva a ejecutar el sondeo asociado tal y como se muestra en el paso 2c de la sección Comprobar el problema.

3.  Si el problema aún persiste, recicle todo el servicio de IIS con la utilidad IISReset.

4.  Vuelva a ejecutar el sondeo asociado tal y como se muestra en el paso 2c de la sección Comprobar el problema.

5.  Si el problema persiste, debe comprobar el estado en el servidor de buzón correspondiente. El nombre del servidor de buzones de correo es el valor `_Mbx:` que se menciona en el mensaje de error.
    
    1.  Ejecute el siguiente comando para el servidor de buzones adecuado. Por ejemplo, ejecute el siguiente comando en un servidor de buzones de correo que lleva el nombre de mailbox1.contoso.com:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "ActiveSync*"}
    
    2.  Si se informa del mal estado de alguno de los monitores mencionados en el resultado del comando, primero debe ocuparse de esos monitores. Para hacerlo, siga los pasos de solución de problemas descritos en la sección Acciones de recuperación de ActiveSyncDeepTestMonitor y ActiveSyncSelfTestMonitor.

6.  Si todos los monitores del servidor de buzones de correo están en buen estado, reinicie el CAS.

7.  Una vez que el servidor se reinicia, vuelva a ejecutar el sondeo asociado tal y como se muestra en el paso 2c de la sección Comprobar el problema.

8.  Si el sondeo sigue dando error, es posible que necesite más ayuda para resolver el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Acciones de recuperación de RequestsQueuedGt500Monitor

Por lo general, esta alerta de monitor se emite en servidores de CA.

1.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa del problema. Haga clic en **Grupos de aplicaciones** y, luego, recicle el grupo de aplicaciones de ActiveSync que se denomina **MSExchangeSyncAppPool**.

2.  Espere 10 minutos para ver si el monitor se mantiene en buen estado. Después de 10 minutos, ejecute el siguiente comando para el servidor apropiado. Por ejemplo, ejecute el siguiente comando para server1.contoso.com:
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "ActiveSync*"}

3.  Si el problema persiste, recicle todo el servicio de IIS con la utilidad IISReset.

4.  Espere 10 minutos y, luego, ejecute el comando que se muestra en el paso 2 nuevamente para ver si el monitor se mantiene en buen estado.

5.  Si el problema persiste, reinicie el servidor. Si el servidor es un CAS, simplemente reinicie el servidor. Si el servidor es un servidor de buzones de correo, haga lo siguiente:
    
    1.  Realice una conmutación por error de las bases de datos que se hospedan en el servidor. Para comprobarlo, ejecute el siguiente comando:
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Nota**   En este y todos los ejemplos de código siguientes, reemplace *server1.contoso.com* con el nombre real del servidor.
    
    2.  Compruebe que todas las bases de datos se hayan quitado del servidor que reporta el problema. Para comprobarlo, ejecute el siguiente comando:
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        Si el resultado del comando no muestra ninguna copia activa en el servidor, reinicie el servidor.

6.  Después de que se reinicia el servidor, espere 10 minutos y, luego, ejecute el comando que se muestra en el paso 2 nuevamente para determinar si el monitor se mantiene en buen estado.

7.  Si el monitor se mantiene en buen estado y si se trata de un servidor de buzones de correo, realice una conmutación por error de las bases de datos ejecutando el comando siguiente:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

8.  Si el sondeo sigue dando error, es posible que necesite más ayuda para resolver el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Exchange ActiveSync](https://technet.microsoft.com/es-es/library/aa998357\(v=exchg.150\))

[Dispositivos móviles](https://technet.microsoft.com/es-es/library/bb232129\(v=exchg.150\))

[Tareas de administración de directorios virtuales de Exchange ActiveSync](https://technet.microsoft.com/es-es/library/bb125170\(v=exchg.150\))

