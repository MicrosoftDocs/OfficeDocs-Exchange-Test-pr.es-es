---
title: Solución de problemas del conjunto de mantenimiento Autodiscover
TOCTitle: Solución de problemas del conjunto de mantenimiento Autodiscover
ms:assetid: bc933621-df73-4d1d-bdef-825b98be8e09
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.autodiscover(v=EXCHG.150)
ms:contentKeyID: 53181920
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento Autodiscover

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El conjunto de mantenimiento Autodiscover supervisa el estado general del servicio Detección automática de los clientes.

Si recibe una alerta que especifica que el servicio Detección automática no es correcto, esto indica un problema que puede impedir que los usuarios tengan acceso a su buzón utilizando el proceso de Detección automática.

## Explicación

El servicio Detección automática se supervisa mediante los siguientes monitores y sondas.


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
<td><p>AutodiscoverCtpProbe</p></td>
<td><p>Detección automática</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverCtpMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información sobre los monitores y las sondas, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Esta sonda puede producir un error por cualquiera de los siguientes motivos habituales:

  - El grupo de aplicaciones de Detección automática (MSExchangeAutodiscoverAppPool) que se hospeda en el servidor de acceso de cliente (CAS) supervisado no responde. O bien, el grupo de aplicaciones de Detección automática hospedado en uno o más servidores de buzones no responde.

  - El CAS está experimentando problemas de red y no puede conectarse al controlador de dominio o el servidor de buzones.

  - Las credenciales de la cuenta de supervisión son incorrectas.

  - Los controladores de dominio no están respondiendo.

## Acción del usuario

Es posible que el servicio se recuperara después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifique que el estado del conjunto de mantenimiento es incorrecto, compruebe primero que el problema aún existe. Si persiste, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje arrojan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra el Shell de administración de Exchange y ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento de la detección automática sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover"}
    
    2.  Repase el resultado del comando para averiguar qué monitor notificó el error. El valor **AlertValue** para el monitor que emitió la alerta es `Unhealthy`.
    
    3.  Vuelva a ejecutar la sonda asociada del monitor que tenga el estado incorrecto. Consulte la tabla en la sección Explicación para encontrar la sonda asociada. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con errores es **AutodiscoverCtpMonitor**. La sonda asociada con ese monitor es **AutodiscoverCtpProbe**. Para ejecutar esa sonda en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe Autodiscover\AutodiscoverCtpProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, repase el valor **Resultado** de la sonda. Si el valor es **Satisfactorio**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de AutodiscoverCtpMonitor

Cuando se recibe una alerta de un conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

  - Nombre del servidor que envió la alerta

  - Nombre del servidor de buzones que la sonda estaba supervisando

  - Fecha y hora en que ocurrió la alerta

  - Mecanismo de autenticación utilizado e información de credenciales

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica sobre el encabezado HTTP

Puede utilizar la información en el seguimiento de excepción completo para intentar resolver el problema. La excepción generada por la sonda contiene un motivo de error que describe por qué la sonda falló. Por ejemplo, el motivo de error podría ser uno de los siguientes:

  - **X-FEServer**   Indica en qué CAS se ejecutó la sonda

  - **X-CalculatedBETarget**   Indica el servidor de buzones al que se enruta la solicitud

  - **X-DiagInfo**   Indica el servidor de buzones que recibió la solicitud

Para resolver este problema, siga estos pasos:

1.  Repase los registros de protocolo en los servidores de buzones y CA. Los registros de protocolo del CAS se encuentran de forma predeterminada en la carpeta ***\<directorio de instalación del servidor Exchange\>*\\Logging\\HttpProxy\\Autodiscover**. Los archivos de registro de protocolo del servidor de buzones se encuentran de forma predeterminada en la carpeta ***\<directorio de instalación del servidor Exchange\>*\\Logging\\Autodiscover**.

2.  Cree una cuenta de usuario de prueba y, luego, inicie sesión en el CAS con dicha cuenta. Por ejemplo, inicie sesión con: https://*\<servername\>*/autodiscover/autodiscover.xml.
    
    Si el nombre de cuenta de prueba pasa, es posible que haya un problema que afecte al servidor de buzones que hospeda el buzón supervisado.
    
    Intente repetir los pasos anteriores mediante una cuenta de prueba en el servidor de buzones. Si eso falla, pruebe de nuevo con otro CAS para comprobar que el problema ocurre en un CAS específico, y no en el servidor de buzones.

3.  Compruebe la conectividad de red entre los servidores de buzones y CA. Utilice ping.exe para confirmar que todos los servidores responden.

4.  Compruebe si hay alertas en el conjunto de mantenimiento Autodiscover.Proxy que puedan indicar un problema que afecte un servidor de buzones específico. Para obtener más información, consulte [Solución de problemas del conjunto de mantenimiento Autodiscover.Proxy](troubleshooting-autodiscover-proxy-health-set.md).

5.  Compruebe si hay alertas en el conjunto de mantenimiento Autodiscover.Protocol que puedan indicar un problema que afecte un servidor de buzones específico. Para obtener más información, consulte [Solución de problemas del conjunto de mantenimiento Autodiscover.Protocol](troubleshooting-autodiscover-protocol-health-set.md).

6.  Inicie el Administrador de IIS y, luego, conéctese al servidor que notifica el problema. Compruebe que el grupo de aplicaciones **MSExchangeAutodiscoverAppPool** se está ejecutando en los servidores de buzones y CA.

7.  En el Administrador de IIS, haga clic en **Grupos de aplicaciones** y, luego, recicle el grupo de aplicaciones **MSExchangeAutodiscoverAppPool** ejecutando el siguiente comando del Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  Vuelva a ejecutar la sonda asociada, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

9.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset o ejecutando el siguiente comando:
    
        Iisreset /noforce

10. Vuelva a ejecutar la sonda asociada, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

11. Si el problema aún persiste, reinicie el servidor.

12. Tras reiniciar el servidor, vuelva a ejecutar la sonda asociada, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

13. Si el sondeo continúa dando error, es posible que necesite asistencia para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

