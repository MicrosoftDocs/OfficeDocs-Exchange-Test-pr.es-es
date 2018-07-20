---
title: Solución de problemas del conjunto de mantenimiento EWS
TOCTitle: Solución de problemas del conjunto de mantenimiento EWS
ms:assetid: f5aaacdd-7f4a-4d63-8440-1c564e644dfc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.ews(v=EXCHG.150)
ms:contentKeyID: 53181929
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento EWS

 

_**Se aplica a:**  Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento de Exchange Web Services (EWS) supervisa el mantenimiento general del servicio EWS. El conjunto de mantenimiento de EWS se relaciona estrechamente con los siguientes conjuntos de mantenimiento:

[Solución de problemas del conjunto de mantenimiento de EWS.Protocol](troubleshooting-ews-protocol-health-set.md)

[Solución de problemas del conjunto de mantenimiento EWS.Proxy](troubleshooting-ews-proxy-health-set.md)

Si recibe una alerta que especifica que el EWS es incorrecto, esto indica un problema que puede impedir que los usuarios se comuniquen con el servidor Exchange.

## Explicación

El servicio EWS se supervisa mediante los siguientes monitores y sondeos.


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
<td><p>EwsCtpProbe</p></td>
<td><p>EWS</p></td>
<td><p>Información adicional</p>
<p>Servicios de dominio de Active Directory (AD DS)</p></td>
<td><p>EwsCtpMonitor (conjunto de mantenimiento de EWS)</p></td>
</tr>
<tr class="even">
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Servicios de dominio de Active Directory (AD DS)</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="odd">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Información adicional</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Este sondeo lleva a cabo un inicio de sesión de EWS completo desde el servidor de acceso de cliente (CAS) en un servidor de buzones de correo mediante una cuenta de supervisión. Este sondeo llama al método **GetFolder** de EWS. Para obtener más información acerca de monitores y sondeos, vea [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Se puede producir un error en este sondeo por cualquiera de los siguientes motivos comunes:

  - Existe un error de coincidencia entre el mecanismo de autenticación utilizado por el sondeo y el mecanismo de autenticación que se utiliza en el directorio virtual del CAS.

  - El grupo de aplicaciones EWS del CAS supervisado no responde.

  - El CAS experimenta problemas de red cuando se conecta al servidor de buzones de correo.

  - El CAS experimenta problemas de comunicación cuando se conecta a los controladores de dominio.

  - Los controladores de dominio no están respondiendo.

  - El grupo de aplicaciones EWS hospedado en uno o más servidores de buzones de correo no responde.

  - La base de datos del usuario no está montada o el almacén de información no está disponible para un buzón específico.

  - El servicio Almacén de información en uno o más servidores de buzones de correo está experimentando problemas.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifique que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.
    
    Cuando recibe una alerta de este conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:
    
    1.  Nombre del CAS en el cual se originó la alerta
    
    2.  Nombre del servidor de buzones de correo que el sondeo estaba supervisando como recurso de destino
    
    3.  Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica del encabezado HTTP
    
    4.  Hora en que ocurrió el incidente
    
    5.  Mecanismo de autenticación utilizado e información de credenciales
    
    La información del seguimiento de excepción proporciona la pista más importante acerca de por qué se generan errores en el sondeo. El mensaje de escalación también contiene los siguientes encabezados HTTP:
    
    1.  **X-FEServer**   Indica en qué CAS se ejecutó el sondeo
    
    2.  **X-TargetBEServer**   Indica a qué servidor MBX se enruta la solicitud
    
    3.  **X-DiagInfo**   Indica el servidor MBX que recibió la solicitud

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento de EWS sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS"}
    
    2.  Revise el resultado del comando para determinar qué monitor notificó el error. El valor de **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Vea la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Para el conjunto de mantenimiento de EWS, suponga que el monitor con errores es **EWSCtpMonitor**. El sondeo asociado con ese monitor es **EWSCtpProbe**. Para ejecutar ese sondeo en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe EWS\EWSCtpProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Correcto**, el problema fue un error transitorio y ya no existe. En caso contrario, vea los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de EwsCtpMonitor

1.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa el problema para determinar si el grupo de aplicaciones **MSExchangeServicesAppPool** se está ejecutando en el servidor de buzones de correo y en CA.

2.  Ubique el MailboxDatabase de los sondeos con error. Luego, compruebe que la base de datos de buzones de correo esté activa en el servidor de buzones de correo y que el almacén de información sea correcto.

3.  Haga clic en **Grupos de aplicaciones** y, luego, recicle el grupo de aplicaciones de **MSExchangeServicesAppPool** mediante la ejecución del siguiente comando desde el Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

5.  Si el problema aún persiste, recicle todo el servicio de IIS con la utilidad IISReset.

6.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

7.  Si el problema persiste, revise los archivos de registro de protocolo en los servidores de buzones de correo y CA. Los registros de protocolo del CAS residen en la carpeta *\<directorio de instalación del servidor Exchange\>\\Logging\\HttpProxy\\Ews*. En el servidor de buzones de correo, los registros residen en la carpeta *\<directorio de instalación del servidor Exchange\>\\Logging\\Ews*.

8.  Cree una cuenta de usuario de prueba y, luego, inicie sesión en el CAS determinado con dicha cuenta. Por ejemplo, inicie sesión con: https://\<NombreDeServidor\>/ews/exchange.asmx. Si el problema persiste, pruebe con otro CAS para determinar si el problema ocurre en ese CAS y no en el servidor de buzones de correo. Si el nombre de usuario de prueba se aprueba, es posible que un problema afecte a la base de datos de buzones de correo o al servidor de buzones de correo donde se encuentra el buzón de supervisión. Intente repetir este paso con una cuenta de prueba que exista en la base de datos de buzones de correo.

9.  Compruebe la conectividad de red entre el servidor de buzones de correo y CA.

10. Compruebe las alertas en el conjunto de mantenimiento EWS.Proxy que puedan indicar un problema que afecte a un CAS específico.

11. Compruebe las alertas en el conjunto de mantenimiento EWS.Protocol que puedan indicar un problema que afecte a un servidor de buzones de correo específico.

12. Si el problema aún persiste, reinicie el servidor. Para realizar esta acción, primero ejecute una conmutación por error de las bases de datos hospedadas en el servidor. Para comprobarlo, ejecute el siguiente comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    **Nota**   En este y todos los ejemplos de código siguientes, remplace *server1.contoso.com* con el nombre real del servidor.

13. Compruebe que todas las bases de datos se hayan quitado del servidor que notifica el problema. Para comprobarlo, ejecute el siguiente comando:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Si el resultado del comando no muestra ninguna copia activa en el servidor, reinicie el servidor.

14. Después de reiniciar el servidor, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

15. Si el sondeo funciona correctamente, realice la conmutación por error del servidor de buzones de correo mediante la ejecución del siguiente comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

16. Si el sondeo continúa con error, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

