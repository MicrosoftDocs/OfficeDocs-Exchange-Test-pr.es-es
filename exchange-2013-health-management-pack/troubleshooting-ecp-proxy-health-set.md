---
title: Solución de problemas del conjunto de mantenimiento ECP.Proxy
TOCTitle: Solución de problemas del conjunto de mantenimiento ECP.Proxy
ms:assetid: f2289f81-56cb-40b5-9108-8782976cccc8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.ecp.proxy(v=EXCHG.150)
ms:contentKeyID: 53181927
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento ECP.Proxy

 

_**Se aplica a:**  Exchange Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento ECP.Proxy supervisa la disponibilidad de la infraestructura de proxy del Centro de administración de Exchange (EAC) en el servidor de acceso de cliente (CAS). El conjunto de mantenimiento ECP.Proxy se relaciona estrechamente con el siguiente conjunto de mantenimiento:

[Troubleshooting ClientAccess.Proxy Health Set](troubleshooting-clientaccess-proxy-health-set.md)

Si recibe una alerta que especifica que ECP.Proxy no es correcto, esto indica un problema que puede evitar que utilice el EAC.

## Explicación

El servicio EAC se supervisa mediante los siguientes monitores y sondeos:


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
<td><p>ECPProxyTestProbe</p></td>
<td><p>ECP.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>ECPProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Se puede producir un error en este sondeo por cualquiera de los siguientes motivos comunes:

  - El grupo de aplicaciones hospedado en el CAS supervisado no funciona correctamente.

  - Las credenciales de la cuenta de supervisión son incorrectas.

  - Los controladores de dominio no están respondiendo.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifique que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento ECP.Proxy sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ECP.Proxy"}
    
    2.  Revise la salida del comando y determine qué monitor informó el error. El valor de **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con errores es **ECPProxyTestMonitor**. El sondeo asociado con ese monitor es **ECPProxyTestProbe**. Para ejecutar ese sondeo en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe ECP.Proxy\ECPProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Correcto**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de ECPProxyTestMonitor

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

  - Nombre del CAS que envió la alerta

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica del encabezado HTTP
    
    Puede utilizar la información en el seguimiento de excepción completo para ayudar a resolver el problema.

  - Fecha y hora en que ocurrió el problema

Para resolver este problema, siga estos pasos:

1.  Revise los registros de protocolo en los servidores CA. Los registros de protocolo se ubican en la carpeta del *\<directorio de instalación del servidor Exchange\>*\\Logging\\HttpProxy*\\\<protocolo\>* en el CAS.

2.  Cree una cuenta de usuario de prueba y, luego, inicie sesión en el CAS con dicha cuenta. Por ejemplo, inicie sesión con: https://*\<NombreDeServidor\>*/owa.

3.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa el problema. Compruebe que MSExchangeServicesAppPool se ejecuta en el CAS.

4.  Haga clic en **Grupo de aplicaciones** y, luego, recicle el grupo de aplicaciones **MSExchangeECPAppPool** mediante la ejecución del siguiente comando desde el Shell de administración de Exchange:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeECPAppPool

5.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

6.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset.

7.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

8.  Si el problema aún persiste, reinicie el servidor.

9.  Después de reiniciar el servidor, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

10. Si el sondeo continúa sin funcionar, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

