---
title: Solución de problemas del conjunto de mantenimiento de RPS.Proxy
TOCTitle: Solución de problemas del conjunto de mantenimiento de RPS.Proxy
ms:assetid: a5058323-5d86-438a-ad4a-fa4292310e98
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.rps.proxy(v=EXCHG.150)
ms:contentKeyID: 53181916
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento de RPS.Proxy

 

_**Se aplica a:**  Exchange Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento de RPS.Proxy supervisa el mantenimiento general del servicio PowerShell remoto.

Si recibe una alerta que especifica que el RPS.Proxy no es correcto, esto indica un problema que puede evitar que utilice el PowerShell remoto para obtener acceso a Exchange.

## Explicación

El servicio de RPS se supervisa mediante los siguientes monitores y sondeos:


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
<td><p>RPSProxyTestProbe</p></td>
<td><p>RPS.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>RPSProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Cuando este sondeo falla, puede haber varias razones para el problema. A continuación se indican algunos de los problemas más comunes:

  - El grupo de aplicaciones hospedado en el servidor CAS supervisado no funciona correctamente.

  - Las credenciales de la cuenta de supervisión son incorrectas.

  - Los controladores de dominio no están respondiendo.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento es incorrecto, lo primero que debe hacer es comprobar que el problema aún exista. Si es así, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan información suficiente de solución de problemas para identificar la causa raíz. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra el Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento de RPS.Proxy sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "RPS.Proxy"}
    
    2.  Revise el resultado del comando y determine qué monitor informó el error. **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene mantenimiento incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para ello, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor de error fue **RPSProxyTestMonitor**. El sondeo asociado a ese monitor es **RPSProxyTestProbe**. Para ejecutar ese sondeo en el servidor server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe RPS.Proxy\RPSProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, consulte **Resultado** del sondeo. Si el valor es **Satisfactorio**, el problema era un error transitorio y ya no existe. De lo contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de RPSProxyTestMonitor

Cuando recibe una alerta de un conjunto de mantenimiento, el correo electrónico contendrá la siguiente información:

  - El nombre del servidor CAS que envía la alerta.

  - Seguimiento de excepción completo, incluidos mensajes de error, datos de diagnóstico e información específica sobre el encabezado HTTP. Puede utilizar la información en el seguimiento de excepción completo para ayudar a solucionar el problema.

  - La hora y la fecha cuando ocurrió el problema.

Para ayudar a solucionar este problema, haga lo siguiente:

1.  Consulte los registros de protocolo en los servidores CAS. Los registros de protocolo se ubican en la carpeta *\<directorio de instalación del servidor exchange\>*\\Logging\\HttpProxy*\\\<protocolo\>* en el servidor CAS.

2.  Cree una cuenta de usuario de prueba y, luego, inicie sesión en el CAS con dicha cuenta, por ejemplo, https:// *\<NombreDeServidor\>*/owa

3.  Inicie el Administrador de IIS y conéctese al servidor que informa del problema para comprobar que MSExchangePowerShellFrontEndAppPool se esté ejecutando en el servidor CAS.

4.  Haga clic en **Grupo de aplicaciones** y, luego, recicle el grupo de aplicaciones de **MSExchangePowerShellFrontEndAppPool** mediante la ejecución del siguiente comando desde el Shell de administración de Exchange:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangePowerShellFrontEndAppPool

5.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2.c. en la sección Comprobar que el problema aún persiste.

6.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset.

7.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2.c. en la sección Comprobar que el problema aún persiste.

8.  Si el problema aún persiste, reinicie el servidor.

9.  Una vez que el servidor se reinicia, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2.c. en la sección Comprobar que el problema aún persiste.

10. Si el sondeo continúa dando error, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

