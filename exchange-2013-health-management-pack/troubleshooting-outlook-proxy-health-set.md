---
title: Solución de problemas del conjunto de mantenimiento de Outlook.Proxy
TOCTitle: Solución de problemas del conjunto de mantenimiento de Outlook.Proxy
ms:assetid: a85585c9-433e-4aa4-b016-28782a18144e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.outlook.proxy(v=EXCHG.150)
ms:contentKeyID: 53181917
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento de Outlook.Proxy

 

_**Se aplica a:**  Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento de Outlook.Proxy supervisa la disponibilidad de la infraestructura del proxy de Outlook en cualquier lugar en el servidor de acceso de cliente (CAS).

Si recibe una alerta que especifica que el servicio de Outlook.Proxy no es correcto, esto indica un problema que puede evitar que los usuarios tengan acceso a su correo.

## Explicación

El servicio de Outlook.Proxy se supervisa mediante los siguientes monitores y sondeos.


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
<td><p>OutlookProxyTestProbe</p></td>
<td><p>Outlook.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OutlookProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Este sondeo puede fallar por cualquiera de los siguientes motivos comunes:

  - El grupo de aplicaciones hospedado en el CAS supervisado no funciona correctamente.

  - Las credenciales de la cuenta de supervisión son incorrectas.

  - Los controladores de dominio no están respondiendo.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento de Outlook.Proxy sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Outlook.Proxy"}
    
    2.  Revise el resultado del comando para determinar qué monitor informó del error. El valor **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor de error es **OutlookProxyTestMonitor**. El sondeo asociado con ese monitor es **OutlookProxyTestProbe**. Para ejecutar ese sondeo en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe Outlook.Proxy\OutlookProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Satisfactorio**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de OutlookProxyTestMonitor

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

  - Nombre del CAS que envió la alerta

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica de encabezado HTTP  
    
    **Nota**   Puede utilizar la información en el seguimiento de excepción completo para ayudar a resolver el problema.

  - La hora y la fecha cuando ocurrió el problema.

Para resolver este problema, siga estos pasos:

1.  Consulte los registros de protocolo en los servidores de CA. Los registros de protocolo se ubican en la carpeta del *\<directorio de instalación del servidor exchange\>*\\Logging\\HttpProxy*\\\<protocolo\>* en el CAS.

2.  Cree una cuenta de usuario de prueba y, luego, inicie sesión en el CAS con dicha cuenta. Por ejemplo, inicie sesión con: https:// *\<NombreDeServidor\>*/owa.

3.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa el problema para determinar que el grupo de aplicaciones de **MSExchangeOABAppPool** se esté ejecutando en el servidor CAS.

4.  Haga clic en **Grupo de aplicaciones** y, luego, recicle el grupo de aplicaciones de **MSExchangeRpcProxyAppPool** mediante la ejecución del siguiente comando desde el Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeRpcProxyAppPool

5.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c en la sección Comprobar que el problema aún persiste.

6.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset.

7.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c en la sección Comprobar que el problema aún persiste.

8.  Si el problema aún persiste, reinicie el servidor.

9.  Una vez que el servidor se reinicia, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c en la sección Comprobar que el problema aún persiste.

10. Si el sondeo continúa dando error, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Outlook en cualquier lugar](https://technet.microsoft.com/es-es/library/bb123741\(v=exchg.150\))

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

