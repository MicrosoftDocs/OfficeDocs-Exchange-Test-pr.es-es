---
title: Solución de problemas del conjunto de mantenimiento OWA.Protocol
TOCTitle: Solución de problemas del conjunto de mantenimiento OWA.Protocol
ms:assetid: fe172da8-65d3-43e0-ba62-d36a1b05fc11
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.owa.protocol(v=EXCHG.150)
ms:contentKeyID: 53181928
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento OWA.Protocol

 

_**Se aplica a:**  Exchange Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento OWA.Protocol supervisa el protocolo Outlook Web App en el servidor de buzones de correo.

Si recibe una alerta que especifica que el OWA.Protocol no es correcto, esto indica un problema que puede evitar que los usuarios tengan acceso a su buzón utilizando Outlook Web App.

## Explicación

El servicio OWA se supervisa mediante los siguientes monitores y sondeos.


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
<td><p>OwaSelfTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Ninguno</p></td>
<td><p>OwaSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OwaDeepTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Active Directory</p>
<p>Información adicional</p></td>
<td><p>OwaDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


El sondeo **OwaSelfTestProbe** envía una sola solicitud HTTP a la siguiente dirección: https://localhost:444/owa/exhealth.check. El sondeo confirma que el grupo de aplicaciones responde mediante la devolución de un código de estado **200 Correcto**. Este sondeo no tiene ninguna dependencia en otros componentes de Exchange.

El sondeo **OwaDeepTestProbe** se ejecuta en cada base de datos de buzones usando las copias en el servidor actual. El sondeo determina que se puede realizar un inicio de sesión completo en ese servidor. Para ello, simula el tipo de tráfico generado por un servidor de accedo de cliente (CAS) en ese servidor específico. El sondeo depende de los Servicios de dominio de Active Directory (AD DS) para la autenticación y del almacén de buzones para acceder a los buzones. Para obtener más información acerca de monitores y sondeos, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Se puede producir un error en este sondeo por cualquiera de los siguientes motivos comunes:

  - El grupo de aplicaciones OWA que se hospeda en el CAS supervisado no responde o el grupo de aplicaciones que se hospeda en el servidor de buzones no responde.

  - El servidor de buzones o CA está experimentando problemas de red y no puede conectarse al otro servidor o a un controlador de dominio.

  - Las credenciales de la cuenta de supervisión son incorrectas.

  - La base de datos del usuario no está montada o el almacén de información no está disponible para ese buzón.

  - El almacén de información no responde.

  - Los controladores de dominio no están respondiendo.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifique que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento OWA.Protocol sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Protocol"}
    
    2.  Revise el resultado del comando para determinar qué monitor notificó el error. **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, supongamos que el monitor con errores fue **OwaSelfTestMonitor**. El sondeo asociado con ese monitor es **OwaSelfTestProbe**. Para ejecutar ese sondeo en server1.contoso.com, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe OWA.Protocol\OwaSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Correcto**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

  - Nombre del servidor que envió la alerta

  - Tipo de sondeo con error (SelfTest o DeepTest)

  - Fecha y hora cuando ocurrió la alerta

  - La ruta de acceso completa a la carpeta que contiene los seguimientos de solicitudes HTTP completos del sondeo
    
      
    De forma predeterminada, estos archivos están ubicados en las siguientes carpetas:
    
      - SelfTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\ProtocolProbe
    
      - DeepTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\MailboxProbe

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica de encabezado HTTP  
    
    **Nota**   Puede utilizar la información en el seguimiento de excepción completo para ayudar a resolver el problema. La excepción generada por el sondeo contiene un motivo de error que describe por qué se produjo un error en el sondeo. El motivo del error puede ser cualquiera de los siguientes:
    
      - **MissingKeyword**   No se encontró una palabra clave esperada en la respuesta del servidor. En este caso, la excepción contiene las palabras clave esperadas.
    
      - **NameResolution**   La resolución DNS no puede resolver un nombre de servicio determinado.
    
      - **NetworkConnection**   El sondeo recibe un error de conexión de red cuando intenta conectarse al grupo de aplicaciones OWA en CAFE.
    
      - **UnexpectedHttpResponseCode**   La respuesta contenía un código HTTP inesperado. Por ejemplo, el servidor devolvió el código HTTP **503**.
    
      - **RequestTimeout**   El servidor tardó demasiado en responder una solicitud de cliente.
    
      - **UnexpectedHttpResponseCode**   La respuesta devolvió un código HTTP inesperado. Por ejemplo, el servidor devolvió el código HTTP **503**.
    
      - **ScenarioTimeout**   El sondeo finalizó correctamente, pero tardó más de un minuto en hacerlo. Normalmente, esto indica que se está sobrecargando un sistema.
    
      - **OwaErrorPage**   OWA devolvió una página de error. El nombre del error que generó el problema suele aparecer en el mensaje de la excepción.
    
      - **OwaMailboxErrorPage**   OWA devolvió una página de error que contenía un error relacionado con el almacén de buzones. Normalmente, esto indica que el almacén de buzones está inactivo o que se están desmontando buzones.
    
    El seguimiento de la excepción contiene un campo importante denominado **FailingComponent**, en el que el sondeo intenta determinar y categorizar el error. Por ejemplo, el sondeo puede devolver cualquiera de los siguientes valores:
    
      - **Mailbox**   El sondeo puede acceder a OWA, pero no puede conectarse al almacén de buzones. En este caso, se produjo un error en el sondeo, o la latencia de acceso al buzón provocó que el sondeo generara el error **ScenarioTimeout**. Cuando se produce este tipo de error, debe comprobar el mantenimiento de los servidores de buzones.
    
      - **Active Directory**   El sondeo puede acceder a OWA, pero no puede conectarse a AD DS. En este caso, se produjo un error en el sondeo o quizás las latencias de llamada de AD DS ocasionaron que se agotara su tiempo de espera. Cuando se produce este tipo de error, debe comprobar el mantenimiento de los controladores de dominio y las conexiones de red entre los servidores de buzones y CA, y los controlados de dominio.
    
      - **OWA**   Esto suele indicar que se generó un error dentro de la capa de OWA. Cuando se produce este tipo de error, debe comprobar el mantenimiento del proceso de OWA en los servidores de buzones y CA, y el mantenimiento de las conexiones de red.
    
    La excepción también contiene la solicitud HTTP más reciente y la información de respuesta que se recibió antes de que se produjera el error en el sondeo.  
      
    El cuerpo de escalación contiene la ruta de acceso a los registros del sondeo que se pueden utilizar para comprobar todas las solicitudes web HTTP y las respuestas que se enviaron cuando se produjo el error en el sondeo. Este archivo solo contiene datos de los sondeos con error porque solo se registran los intentos con error. Puede utilizar esta información para obtener una visión más completa de por qué se produjo un error en la prueba.

## Acciones de recuperación de OwaSelfTestProbe

Dado que este sondeo tiene muy pocas dependencias, suelen producirse errores cuando el proceso del grupo de aplicaciones de OWA no responde.

Para resolver este problema, siga estos pasos:

1.  Haga clic en la dirección URL del registro de seguimiento del sondeo en el cuerpo del mensaje de correo electrónico de alerta para comprobar que se estén generando nuevos errores.

2.  Crea una cuenta de usuario de prueba en el mismo servidor en que está montado el buzón. Intente iniciar sesión para determinar si se puede reproducir el problema.

3.  Compruebe si hay alertas en el conjunto de mantenimiento de OWA que puedan indicar un problema que afecte un servidor de buzones específico. Para obtener más información, consulte [Solución de problemas del conjunto de mantenimiento OWA](troubleshooting-owa-health-set.md).

4.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa el problema para determinar que el grupo de aplicaciones de **MSExchangeOwaAppPool** se esté ejecutando en el servidor CAS.

5.  En el Administrador de IIS, compruebe que se esté ejecutando el sitio web predeterminado.

6.  En el Administrador de IIS, haga clic en **Grupos de aplicaciones** y, luego, recicle el grupo de aplicaciones **MSExchangeOWAAppPool** mediante la ejecución del siguiente comando desde el Shell de administración de Exchange:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

7.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

8.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset o mediante la ejecución del siguiente comando:
    
        Iisreset /noforce

9.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

10. Si el problema aún persiste, reinicie el servidor.

11. Después de reiniciar el servidor, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

12. Si el sondeo continúa sin funcionar, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Acciones de recuperación de OwaDeepTestProbe

1.  Para determinar si el problema aún existe, cree una cuenta de usuario de prueba en el mismo servidor en que está montado el buzón y, luego, intente iniciar sesión en OWA. Por ejemplo, intente iniciar sesión con: https://*\<NombreDeServidor\>*/owa.

2.  Compruebe si hay alertas en el conjunto de mantenimiento de OWA que puedan indicar un problema que afecte un servidor de buzones específico. Para obtener más información, consulte [Solución de problemas del conjunto de mantenimiento OWA](troubleshooting-owa-health-set.md).

3.  Inicie el Administrador de IIS y, luego, conéctese al servidor que informa el problema para determinar que el grupo de aplicaciones de **MSExchangeOwaAppPool** se esté ejecutando en el servidor CAS.

4.  En el Administrador de IIS, compruebe que se esté ejecutando el sitio web predeterminado.

5.  Ubique la base de datos de buzones de los sondeos con errores y compruebe que la base de datos de buzones esté activa en un servidor de buzones y que el almacén de buzones sea correcto. Para ubicar la información del GUID de la base de datos con error, abra la información del seguimiento de excepción completo. Cada error debe contener una entrada similar al siguiente ejemplo:
    
    `Starting Owa probe with Target: https://localhost/owa/, Username:  HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com`

6.  Copie el GUID de HealthMailbox y, luego, ejecute el siguiente comando en el Shell:
    
        Get-Mailbox -Monitoring -Identity <username>
    
    Por ejemplo, ejecute el comando siguiente:
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    En el objeto devuelto, puede ubicar el nombre de la base de datos del usuario y también puede determinar dónde reside la base de datos activa actualmente.

7.  En el Administrador de IIS, haga clic en **Grupo de aplicaciones** y, luego, recicle el grupo de aplicaciones **MSExchangeOWAAppPool** mediante la ejecución del siguiente comando desde el Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

8.  Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

9.  Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset o mediante la ejecución del siguiente comando:
    
        Iisreset /noforce

10. Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

11. Si el problema aún persiste, reinicie el servidor.

12. Después de reiniciar el servidor, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

13. Si el sondeo continúa sin funcionar, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

