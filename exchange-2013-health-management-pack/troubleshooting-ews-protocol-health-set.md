---
title: Solución de problemas del conjunto de mantenimiento de EWS.Protocol
TOCTitle: Solución de problemas del conjunto de mantenimiento de EWS.Protocol
ms:assetid: 826b2d5b-adbb-4bf5-94b6-0a8de2e3aac0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.ews.protocol(v=EXCHG.150)
ms:contentKeyID: 53181913
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento de EWS.Protocol

 

_**Se aplica a:**Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento de EWS.Protocol supervisa el protocolo de comunicaciones de servicios Web Exchange (EWS) en el servidor de buzones de correo. El conjunto de mantenimiento de EWS.Protocol se relaciona estrechamente con los siguientes conjuntos de mantenimiento:

[Solución de problemas del conjunto de mantenimiento EWS](troubleshooting-ews-health-set.md)

[Solución de problemas del conjunto de mantenimiento EWS.Proxy](troubleshooting-ews-proxy-health-set.md)

Si recibe una alerta que especifica que el EWS.Protocol está en mal estado, esto indica un problema que puede evitar que sus usuarios tengan acceso a Exchange.

## Explicación

El conjunto de mantenimiento de EWS.Protocol está compuesto por los siguientes sondeos:

1.  EwsSelfTestProbe

2.  EwsDeepTestProbe

EwsSelfTestProbe no depende del almacén de información. Sin embargo, el sondeo EwsDeepTestProbe depende del almacén de información. Ambos sondeos realizan operaciones de EWS en el servidor de buzones de correo y utilizan el mismo método de autenticación que el servidor de acceso de cliente (CAS). EwsSeftTestProbe invoca al método **ConvertId** y EwsDeepTestProbe invoca al método **GetFolder**.


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
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Información adicional</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

Cuando recibe una alerta de este conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

1.  Nombre del servidor de buzones de correo en el que se originó la alerta

2.  Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica sobre encabezados HTTP

3.  Hora en que ocurrió el incidente

## Problemas comunes

Este sondeo puede fallar por cualquiera de los siguientes motivos comunes:

  - El grupo de aplicaciones de EWS en el servidor de buzones de correo supervisado no está funcionando correctamente.

  - Los controladores de dominio no responden o no se pueden comunicar con el servidor de buzones de correo.

  - La base de datos del usuario no está montada o el almacén de información no está disponible para un buzón de correo específico.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento de EWS.Protocol sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Protocol"}
    
    2.  Revise el resultado del comando para determinar qué monitor informó el error. El valor **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor de error es **EWSSelfTestMonitor**. El sondeo asociado con ese monitor es **EWSSelfTestProbe**. Para ejecutar ese sondeo en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe EWS.Protocol\EWSSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Satisfactorio**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de EWSSelfTestMonitor y EWSDeepTestMonitor

Normalmente, esta alerta de monitor se emite para servidores de buzones de correo.

1.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa del problema para determinar si MSExchangeServicesAppPool se está ejecutando tanto en el servidor de buzones de correo como en el CA.

2.  Ubique el MailboxDatabase de los sondeos con errores y, luego, compruebe que MailboxDatabase esté activo para MailboxServer y que el almacén de información sea correcto.

3.  Haga clic en **Grupo de aplicaciones** y, luego, recicle el grupo de aplicaciones de **MSExchangeServicesAppPool** mediante la ejecución del siguiente comando desde el Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c en la sección Comprobar que el problema aún persiste.

5.  Si el problema persiste, reinicie el servicio IIS mediante la utilidad IISReset.

6.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c en la sección Comprobar que el problema aún persiste.

7.  Si el problema persiste, consulte los archivos de registro de protocolo de los servidores de buzones de correo. En el servidor de buzones de correo, los registros residen en la carpeta *\<directorio de instalación de exchange server\>*\\Logging\\Ews.

8.  Cree una cuenta de usuario de prueba y, luego, inicie sesión con dicha cuenta contra el servidor de buzones de correo proporcionado en el puerto 444 https://*\<NombreDeServidor\>*:444/ews/exchange.asmx. Si la prueba es correcta, un problema puede afectar a la base de datos del buzón de correo específico o al servidor de buzones de correo donde está ubicado el buzón supervisado. Intente repetir este paso con una cuenta de prueba en esa base de datos.

9.  Compruebe las alertas en el conjunto de mantenimiento de EWS.Protocol que puedan indicar un problema que afecte al servidor de buzones de correo específico.

10. Si el problema aún persiste, reinicie el servidor. Para hacerlo, primero realice la conmutación por error de las bases de datos hospedadas en el servidor mediante el siguiente comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    En este y todos los ejemplos de código siguientes, reemplace *server1.contoso.com* por el nombre real del servidor.

11. Compruebe que todas las bases de datos se hayan quitado del servidor que reporta el problema. Para comprobarlo, ejecute el siguiente comando:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Si el resultado del comando no muestra copias activas en el servidor, se puede reiniciar el servidor sin problema. Reinicie el servidor.

12. Una vez que el servidor se reinicia, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c en la sección Comprobar que el problema aún persiste.

13. Si el sondeo tiene éxito, realice la conmutación por error de las bases de datos mediante la ejecución del siguiente comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

14. Si el sondeo continúa fallando, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

