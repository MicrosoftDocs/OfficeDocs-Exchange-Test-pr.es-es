---
title: Solución de problemas del conjunto de mantenimiento de POP
TOCTitle: Solución de problemas del conjunto de mantenimiento de POP
ms:assetid: 6114e9fe-d037-4cb9-a643-933eb5fabc45
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.pop(v=EXCHG.150)
ms:contentKeyID: 53181914
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento de POP

 

_**Se aplica a:**  Exchange Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento de POP supervisa el mantenimiento general y la disponibilidad del servicio POP3 y la conectividad del cliente POP3 de Microsoft Exchange. El conjunto de mantenimiento de POP se relaciona estrechamente con los siguientes conjuntos de mantenimiento:

  - [Solución de problemas del conjunto de mantenimiento POP.Protocol](troubleshooting-pop-protocol-health-set.md)

  - [Solución de problemas del conjunto de mantenimiento POP.Proxy](troubleshooting-pop-proxy-health-set.md)

Si recibe una alerta que especifica que el servicio de POP no es correcto, esto indica un problema que puede evitar que los usuarios tengan acceso a sus buzones con POP3 en el entorno de Exchange.

## Explicación

El servicio POP se supervisa mediante los siguientes monitores y sondeos.


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
<td><p>PopCTPProbe</p></td>
<td><p>POP</p></td>
<td><p>Active Directory</p>
<p>Autenticación</p>
<p>Autenticación del servidor de buzones de correo</p>
<p>Información adicional</p>
<p>Alta disponibilidad</p>
<p>Red</p></td>
<td><p>PopCTPMonitor (conjunto de mantenimiento de POP)</p></td>
</tr>
<tr class="even">
<td><p>PopProxyTestProbe</p></td>
<td><p>POP.Proxy</p></td>
<td><p>Ninguno</p></td>
<td><p>PopProxyTestMonitor (conjunto de mantenimiento de POP.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>PopDeepTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticación</p>
<p>Información adicional</p>
<p>Alta disponibilidad</p></td>
<td><p>PopDeepTestMonitor (conjunto de mantenimiento de POP.Protocol)</p></td>
</tr>
<tr class="even">
<td><p>PopSelfTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Ninguno</p></td>
<td><p>PopSelfTestMonitor (conjunto de mantenimiento de POP.Protocol)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (conjunto de mantenimiento de POP)</p></td>
</tr>
</tbody>
</table>


## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifique que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento de POP sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "POP"}
    
    2.  Revise el resultado del comando para determinar qué monitor notificó el error. El valor de **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **PopCTPMonitor**. El sondeo asociado con ese monitor es **PopCTPProbe**. Para ejecutar ese sondeo en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe POP\PopCTPProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Correcto**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de PopTestDeepMonitor y PopSelfTestMonitor

Normalmente, esta alerta de monitor se emite para servidores de buzones de correo.

1.  Reinicie el servicio back-end de POP3. Para obtener más información, consulte [Iniciar y detener los servicios POP3](https://technet.microsoft.com/es-es/library/aa997475\(v=exchg.150\)).

2.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

3.  Si aún hay un error en el sondeo, realice la conmutación por error de las bases de datos hospedadas en el servidor de buzones de correo mediante el siguiente comando:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  Después de quitar todas las bases de datos del servidor de buzones de correo, debe comprobar que las bases de datos se hayan movido correctamente. Para comprobarlo, ejecute el siguiente comando:
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status

5.  Asegúrese de que el servidor no hospede copias activas de la base de datos. Luego, reinicie el servidor.

6.  Después del reinicio correcto del servidor, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c en la sección Comprobar que el problema aún persiste.

7.  Si el sondeo se realiza correctamente, realice la conmutación por error de las bases de datos mediante la ejecución del siguiente comando:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

8.  Si el sondeo continúa sin funcionar, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Acciones de recuperación de POPCTPMonitor

Normalmente, esta alerta de monitor se emite para servidores de CA (CAS).

1.  Reinicie el servicio POP3 en los servidores que están ejecutando el rol de CAS. Para obtener más información, consulte [Iniciar y detener los servicios POP3](https://technet.microsoft.com/es-es/library/aa997475\(v=exchg.150\)).

2.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

3.  Si el problema persiste, ejecute los siguientes comandos en Windows PowerShell:
    
    1.  ``` 
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $true
        ```
    
    2.  Reinicie el servicio POP3 en los servidores que están ejecutando el rol de CAS.
    
    3.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.
    
    4.  Ejecute el siguiente comando y, luego, encuentre la ubicación del archivo de registro:
        
            Get-PopSettings -server <CAS server name>
    
    5.  Ejecute el siguiente comando para determinar qué buzón presta servicio al comando. Para hacerlo, compare las marcas de tiempo con el sondeo:
        
            Get-ServerHealth <mailbox server name> | ?{ $_.HealthSetName -like "POP*"}
    
    6.  Si se informa que alguno de estos servidores no es correcto, siga los pasos detallados en la sección Acciones de recuperación de PopTestDeepMonitor y PopSelfTestMonitor.

4.  Si se informa que el servidor de buzones de correo es correcto, reinicie el CAS.

5.  Después del reinicio del servidor, vuelva a ejecutar el sondeo asociado, como se describe en el paso 2c en la sección Comprobar que el problema aún persiste.

6.  Desactive el registro de protocolo mediante la ejecución del siguiente comando:
    
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  Reinicie el servicio POP3 en los servidores que están ejecutando el rol de CAS. Para obtener más información, consulte [Iniciar y detener los servicios POP3](https://technet.microsoft.com/es-es/library/aa997475\(v=exchg.150\)).

8.  Si el sondeo continúa sin funcionar, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Acciones de recuperación de PopProxyTestMonitor

1.  Reinicie el servicio POP3 en los servidores que están ejecutando el rol de CAS. Para obtener más información, consulte [Iniciar y detener los servicios POP3](https://technet.microsoft.com/es-es/library/aa997475\(v=exchg.150\)).

2.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

3.  Si se siguen produciendo errores en el sondeo, reinicie el CAS.

4.  Después del reinicio del servidor, vuelva a ejecutar el sondeo asociado, como se describe en el paso 2c en la sección Comprobar que el problema aún persiste.

5.  Si el sondeo continúa sin funcionar, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Acciones de recuperación de AverageCommandProcessingTimeGt60sMonitor

Normalmente, esta alerta de monitor se emite para servidores de buzones de correo o CA.

1.  Reinicie el servicio POP3 en los servidores de CA o de buzones de correo. Para obtener más información, consulte [Iniciar y detener los servicios POP3](https://technet.microsoft.com/es-es/library/aa997475\(v=exchg.150\)).

2.  Espere diez minutos para ver si el mantenimiento del monitor se mantiene correcto. Después de 10 minutos, ejecute el siguiente comando (en el ejemplo, se utiliza server1.contoso.com).
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "POP*"}

3.  Si el problema persiste, deberá reiniciar el servidor. Si el servidor es un CAS, simplemente reinícielo. Si el servidor es un servidor de buzones de correo, debe realizar la conmutación por error de la base de datos y comprobar los resultados. Para ello, siga estos pasos:
    
    1.  Realice la conmutación por error de las bases de datos hospedadas en el servidor mediante el siguiente comando:
        
            Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Nota**   En este y en todos los ejemplos de código siguientes, remplace *server1.contoso.com* con el nombre real del servidor.
    
    2.  Compruebe que todas las bases de datos se hayan quitado del servidor que informa el problema. Para comprobarlo, ejecute el siguiente comando:
        
            Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status
        
        Si el resultado del comando no muestra ninguna copia activa en el servidor, reinicie el servidor.

4.  Después del reinicio del servidor, espere diez minutos y, luego, vuelva a ejecutar el comando que se muestra en el paso 2 para ver si el mantenimiento del monitor continúa siendo correcto.

5.  Si el monitor es correcto y este es un servidor de buzones de correo, realice la conmutación por error del servidor de buzones de correo mediante la ejecución del siguiente comando:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

6.  Si el sondeo continúa sin funcionar, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Iniciar y detener los servicios POP3](https://technet.microsoft.com/es-es/library/aa997475\(v=exchg.150\))

[Test-PopConnectivity](https://technet.microsoft.com/es-es/library/bb738143\(v=exchg.150\))

