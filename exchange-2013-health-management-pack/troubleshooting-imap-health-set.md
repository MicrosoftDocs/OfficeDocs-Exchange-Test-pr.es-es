---
title: Solución de problemas del conjunto de mantenimiento de IMAP
TOCTitle: Solución de problemas del conjunto de mantenimiento de IMAP
ms:assetid: 2a06e671-4cc2-4ce5-bf53-6243ea140f20
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.imap(v=EXCHG.150)
ms:contentKeyID: 53181906
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento de IMAP

 

_**Se aplica a:**  Exchange Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento IMAP supervisa la disponibilidad de la infraestructura proxy de IMAP4 en el servidor de acceso de cliente (CAS). El conjunto de mantenimiento IMAP está estrechamente relacionado con los conjuntos de mantenimiento siguientes:

[Solución de problemas del conjunto de mantenimiento IMAP.Protocol](troubleshooting-imap-protocol-health-set.md)

[Solución de problemas del conjunto de mantenimiento de IMAP.Proxy](troubleshooting-imap-proxy-health-set.md)

Si recibe una alerta de que IMAP no está en buen estado, significa que existe un problema que puede impedir a los usuarios acceder a sus buzones usando IMAP.

## Explicación

El servicio IMAP4 se supervisa con los monitores y las sondas siguientes.


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
<td><p>ImapCTPProbe</p></td>
<td><p>IMAP</p></td>
<td><p>Active Directory</p>
<p>Autenticación</p>
<p>Autenticación del servidor de buzones de correo</p>
<p>Alta disponibilidad</p>
<p>Conexión de red</p></td>
<td><p>ImapCTPMonitor (conjunto de mantenimiento IMAP)</p></td>
</tr>
<tr class="even">
<td><p>ImapProxyTestProbe</p></td>
<td><p>IMAP.Proxy</p></td>
<td><p>Active Directory</p>
<p>Autenticación</p></td>
<td><p>ImapProxyTestMonitor (conjunto de mantenimiento IMAP.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>ImapDeepTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticación</p>
<p>Información adicional</p>
<p>Alta disponibilidad</p></td>
<td><p>IMAP.Protocol (conjunto de mantenimiento IMAP.Protocol)</p></td>
</tr>
<tr class="even">
<td><p>ImapSelfTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticación</p></td>
<td><p>IMAP.Protocol (conjunto de mantenimiento IMAP.Protocol)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (conjunto de mantenimiento IMAP)</p></td>
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
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento IMAP sobre server1.contoso.com, ejecute el comando siguiente:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    2.  Revise la salida del comando para saber qué monitor informó del error. El valor **AlertValue** del monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar la sonda asociada para el monitor que no está en buen estado. Consulte la tabla de la sección Explicación para encontrar la sonda asociada. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **ImapCTPMonitor**. La sonda asociada con ese monitor es **ImapCTPProbe**. Para ejecutar esa sonda en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe IMAP\ImapCTPProbe -Server server1.contoso.com | Format-List
    
    4.  En la salida del comando, revise el valor **Resultado** de la sonda. Si el valor es **Correcto**, el problema era un error temporal y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de ImapTestDeepMonitor e ImapSelfTestMonitor

1.  Reinicie el servicio IMAP4 de Exchange en el servidor backend. Para más información sobre cómo parar e iniciar el servicio IMAP4, vea [Iniciar y detener los servicios IMAP4](https://technet.microsoft.com/es-es/library/bb124022\(v=exchg.150\)).

2.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

3.  Si el problema persiste, debe conmutar las bases de datos hospedadas en el servidor de buzones con el comando siguiente:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  Compruebe que todas las bases de datos se hayan quitado del servidor que informa del problema. Para comprobarlo, ejecute el siguiente comando:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Si la salida del comando no muestra ninguna copia activa en el servidor, reinicie el servidor.

5.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

6.  Si la sonda funciona correctamente, conmute las bases de datos ejecutando el siguiente comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  Si la sonda sigue sin funcionar, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Acciones de recuperación de ImapCTPMonitor

Por lo general, esta alerta de monitor se emite en servidores CAS.

1.  Reinicie el servicio IMAP4 de Exchange en el servidor backend. Para más información sobre cómo parar e iniciar el servicio IMAP4, vea [Iniciar y detener los servicios IMAP4](https://technet.microsoft.com/es-es/library/bb124022\(v=exchg.150\))

2.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2.c. de la sección Comprobar que el problema persiste.

3.  Si el problema persiste, debe activar el registro del protocolo de IMAP para intentar resolverlo. Para ello, siga estos pasos:
    
    1.  En Windows PowerShell, ejecute el siguiente comando:
        
            Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $true
    
    2.  Reinicie el servicio IMAP4 de Exchange en el servidor backend. Para más información sobre cómo parar e iniciar el servicio IMAP4, vea [Iniciar y detener los servicios IMAP4](https://technet.microsoft.com/es-es/library/bb124022\(v=exchg.150\))
    
    3.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.
    
    4.  Ejecute el siguiente comando y, luego, determine la ubicación del archivo de registro. Para comprobarlo, ejecute el siguiente comando:
        
            Get-ImapSettings -server <CAS server name>
    
    5.  Determine el buzón que está cumpliendo este comando. El nombre del servidor de buzones es el valor para el valor `_Mbx:` del mensaje de error.
    
    6.  Ejecute el siguiente comando:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "IMAP*"}
        
        **Nota**: En este comando, cambie *mailbox1.contoso.com* por el nombre real del servidor de buzones.
    
    7.  Si se informa del mal estado de alguno de los monitores mencionados en la salida del comando, primero debe ocuparse de esos monitores. Siga los pasos de solución de problemas descritos en la sección Acciones de recuperación de ImapTestDeepMonitor e ImapSelfTestMonitor.

4.  Si se informa de que el servidor de buzones de correo es correcto, reinicie el CAS.

5.  Una vez que el servidor se reinicie, vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

6.  Desactive el registro del protocolo. Para hacerlo, ejecute el siguiente comando de Windows PowerShell:
    
        Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  Reinicie el servicio IMAP4.

8.  Si la sonda sigue sin funcionar, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Acciones de recuperación de ImapProxyTestMonitor

1.  Reinicie el servicio IMAP4.

2.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

3.  Si la sonda sigue dando error, reinicie el CAS.

4.  Una vez que el servidor se reinicie, vuelva a ejecutar la soda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

5.  Si la sonda sigue sin funcionar, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Acciones de recuperación de AverageCommandProcessingTimeGt60sMonitor RequestsQueuedGt500Monitor

Por lo general, esta alerta de monitor se emite en servidores de buzones y de CA.

1.  Reinicie el servicio IMAP4 de Exchange en el servidor backend o CAS. Para más información sobre cómo parar e iniciar el servicio IMAP4, vea [Iniciar y detener los servicios IMAP4](https://technet.microsoft.com/es-es/library/bb124022\(v=exchg.150\))

2.  Espere diez minutos para ver si el mantenimiento del monitor se mantiene correcto. Después de 10 minutos, ejecute el siguiente comando:
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    **Nota**: En este comando, cambie *server1.contoso.com* por el nombre real del servidor.

3.  Espere 10 minutos y, luego, ejecute el comando que se muestra en el paso 2 nuevamente para ver si el monitor se mantiene en buen estado.

4.  Si el problema persiste, debe reiniciar el servidor. Si el servidor es del tipo CAS, simplemente reinicie el servidor. Si el servidor es un servidor de buzones, haga lo siguiente:
    
    1.  Conmute las bases de datos que se hospedan en el servidor. Para comprobarlo, ejecute el siguiente comando:
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Nota**: En este ejemplo de código y en todos los subsiguientes, cambie *server1.contoso.com* por el nombre real del servidor.
    
    2.  Compruebe que todas las bases de datos se hayan trasladado fuera del servidor que informa del problema. Para comprobarlo, ejecute el siguiente comando:
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        Si la salida del comando no muestra ninguna copia activa en el servidor, reinicie el servidor.

5.  Después del reinicio del servidor, espere diez minutos y, luego, vuelva a ejecutar el comando que se muestra en el paso 2 para ver si el mantenimiento del monitor continúa siendo correcto.

6.  Si el monitor se mantiene en buen estado, y si se trata de un servidor de buzones, conmute las bases de datos ejecutando el comando siguiente:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  Si la sonda sigue sin funcionar, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[POP3 e IMAP4](https://technet.microsoft.com/es-es/library/jj657728\(v=exchg.150\))

[Habilitar IMAP4 en Exchange 2013](https://technet.microsoft.com/es-es/library/bb124489\(v=exchg.150\))

[Test-ImapConnectivity](https://technet.microsoft.com/es-es/library/bb738126\(v=exchg.150\))

