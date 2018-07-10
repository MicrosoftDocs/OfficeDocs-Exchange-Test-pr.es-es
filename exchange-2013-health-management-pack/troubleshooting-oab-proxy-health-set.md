---
title: Solución de problemas del conjunto de mantenimiento OAB.Proxy
TOCTitle: Solución de problemas del conjunto de mantenimiento OAB.Proxy
ms:assetid: b717fc00-a787-44d6-8ccb-0eb4b2ea9e73
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.oab.proxy(v=EXCHG.150)
ms:contentKeyID: 53181921
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento OAB.Proxy

 

_**Se aplica a:**  Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento OAB.Proxy supervisa la disponibilidad de la infraestructura de proxy de la libreta de direcciones sin conexión en el servidor de acceso de cliente (CAS).

Si recibe una alerta que especifica que el OAB.Proxy no es correcto, es indicativo de un problema que puede impedir que utilice el OAB.

## Explicación

El servicio OAB se supervisa mediante los siguientes monitores y sondas.


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
<td><p>OABProxyTestProbe</p></td>
<td><p>OAB.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OABProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información sobre los monitores y las sondas, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Esta sonda puede producir un error por cualquiera de los siguientes motivos habituales:

  - El grupo de aplicaciones hospedado en el CAS supervisado no funciona correctamente.

  - Las credenciales de la cuenta de supervisión son incorrectas.

  - Los controladores de dominio no están respondiendo.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra el Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento OAB.Proxy sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OAB.Proxy"}
    
    2.  Repase el resultado del comando para averiguar qué monitor notificó el error. El valor **AlertValue** del monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar la sonda asociada para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar la sonda asociada. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con errores es **OABProxyTestMonitor**. La sonda asociada a ese monitor es **OABProxyTestProbe**. Para ejecutar esa sonda en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe |OAB.Proxy\OABProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, repase el valor **Resultado** de la sonda. Si el valor es **Satisfactorio**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de OABProxyTestMonitor

Cuando se recibe una alerta de un conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

  - Nombre del CAS que envió la alerta

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica de encabezado HTTP  
    
    **Nota**   Puede utilizar la información en el seguimiento de excepción completo para intentar resolver el problema.

  - Fecha y hora en que ocurrió el problema

Para resolver este problema, siga estos pasos:

1.  Consulte los registros de protocolo en el CAS. Los registros de protocolo están en la carpeta *\<directorio de instalación del servidor Exchange\>*\\Logging\\HttpProxy*\\\<protocolo\>* del CAS.

2.  Cree una cuenta de usuario de prueba y, luego, inicie sesión en el CAS con dicha cuenta. Por ejemplo, inicie sesión con: https:// *\<nombre del servidor\>*/owa.

3.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa el problema para determinar que el grupo de aplicaciones de **MSExchangeOABAppPool** se esté ejecutando en el servidor CAS.

4.  Haga clic en **Grupo de aplicaciones** y, luego, recicle el grupo de aplicaciones **MSExchangeOABAppPool** ejecutando el siguiente comando desde el Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOABAppPool

5.  Vuelva a ejecutar la sonda asociada, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

6.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset.

7.  Vuelva a ejecutar la sonda asociada, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

8.  Si el problema aún persiste, reinicie el servidor.

9.  Tras reiniciar el servidor, vuelva a ejecutar la sonda asociada, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

10. Si el sondeo continúa dando error, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Libretas de direcciones sin conexión](https://technet.microsoft.com/es-es/library/bb232155\(v=exchg.150\))

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

