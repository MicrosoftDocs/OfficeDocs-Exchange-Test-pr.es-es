---
title: Solución de problemas del conjunto de mantenimiento Autodiscover.Protocol
TOCTitle: Solución de problemas del conjunto de mantenimiento Autodiscover.Protocol
ms:assetid: 06afdcc8-7920-4e88-b85a-98e67a19d221
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.autodiscover.protocol(v=EXCHG.150)
ms:contentKeyID: 53181899
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento Autodiscover.Protocol

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento Autodiscover.Protocol supervisa el protocolo de comunicaciones de detección automática en el servidor de buzones.

Si recibe una alerta que especifica que Autodiscover.Protocol no está en buen estado, significa que existe un problema que puede evitar que los usuarios accedan a sus buzones.

## Explicación

El servicio Autodiscover.Protocol se supervisa con los monitores y las sondas siguientes.


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
<td><p>AutodiscoverSelfTestProbe</p></td>
<td><p>Autodiscover.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverSelfTestMonitor</p></td>
</tr>
</tbody>
</table>


Para más información sobre monitores y sondas, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Esta sonda puede fallar por cualquiera de los siguientes motivos comunes:

  - El grupo de aplicaciones de detección automática (MSExchangeAutodiscoverAppPool) que se hospeda en el servidor de acceso de cliente (CAS) supervisado no responde. El grupo de aplicaciones de detección automática hospedado en uno o varios servidores de buzones no responde.

  - Los controladores de dominio no responden.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta de que el conjunto de mantenimiento no está en buen estado, primero compruebe si el problema aún existe. Si el problema persiste, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje dan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje dan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento Autodiscover.Protocol sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover.Protocol"}
    
    2.  Revise la salida del comando para determinar qué monitor informó del error. El valor **AlertValue** del monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar la sonda asociada para el monitor que no está en buen estado. Consulte la tabla de la sección Explicación para encontrar la sonda asociada. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con error es **AutodiscoverSelfTestMonitor**. La sonda asociada con ese monitor es **AutodiscoverSelfTestProbe**. Para ejecutar esa sonda en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe Autodiscover.Protocol\AutodiscoverSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  En la salida del comando, revise el valor **Resultado** de la sonda. Si el valor es **Correcto**, el problema era un error temporal y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de AutodiscoverSelfTestProbe

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo contiene la siguiente información:

  - Nombre del servidor de buzón que envió la alerta

  - Nombre del servidor de buzón supervisado

  - Fecha y hora en las que ocurrió la alerta

  - Mecanismo de autenticación utilizado e información de credenciales

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica sobre el encabezado HTTP

Puede usar la información del seguimiento de excepción completo para ayudar a resolver el problema. La excepción generada por la sonda contiene un motivo de error que describe por qué falló la sonda.

Para resolver este problema, siga estos pasos:

1.  Registros de protocolo de revisión en los servidores de buzones. De manera predeterminada, los archivos de registro de protocolo del servidor buzones se ubican en la carpeta de ***\<directorio de instalación del servidor Exchange\>*\\Logging\\Autodiscover**.

2.  Cree una cuenta de usuario de prueba y luego inicie sesión en el servidor de buzones con la cuenta de usuario de prueba en la dirección. Por ejemplo, inicie sesión con: https://*\<nombre del servidor\>*:444/autodiscover/autodiscover.xml.
    
    Si pasa el nombre de la cuenta de usuario de prueba, es posible que un problema afecte el servidor de buzones que hospeda el buzón supervisado.

3.  Intente repetir los pasos anteriores usando una cuenta de prueba en el servidor de buzones.

4.  Compruebe si hay alertas en el conjunto de mantenimiento Autodiscover.Proxy que puedan indicar un problema que afecte a un servidor de buzones específico. Para obtener más información, consulte [Solución de problemas del conjunto de mantenimiento Autodiscover.Proxy](troubleshooting-autodiscover-proxy-health-set.md).

5.  Busque alertas en el conjunto de mantenimiento de detección automática que puedan indicar un problema que afecte a servidores de buzones específicos. Para obtener más información, consulte [Solución de problemas del conjunto de mantenimiento Autodiscover](troubleshooting-autodiscover-health-set.md).

6.  Inicie el administrador de IIS y luego conéctese al servidor de buzones que ha informado del problema. Compruebe que el grupo de aplicaciones **MSExchangeAutodiscoverAppPool** esté en ejecución en el servidor de buzones.

7.  En el administrador de IIS, haga clic en **Grupos de aplicaciones** y, luego, recicle el grupo de aplicaciones **MSExchangeAutodiscoverAppPool** ejecutando el comando siguiente del Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

9.  Si el problema persiste, recicle el servicio de IIS con la utilidad IISReset o ejecutando el comando siguiente:
    
        Iisreset /noforce

10. Vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

11. Si el problema persiste, reinicie el servidor.

12. Una vez que el servidor se reinicie, vuelva a ejecutar la sonda asociada como se muestra en el paso 2c de la sección Comprobar que el problema persiste.

13. Si la sonda sigue sin funcionar, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

