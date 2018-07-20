---
title: Solución de problemas del conjunto de mantenimiento OWA
TOCTitle: Solución de problemas del conjunto de mantenimiento OWA
ms:assetid: eae9dbd7-2ce6-43ce-b9a1-b114fd0c3ab4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.owa(v=EXCHG.150)
ms:contentKeyID: 53181924
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento OWA

 

_**Se aplica a:**  Exchange Server 2013_

_**Última modificación del tema:**  2015-03-09_

El conjunto de mantenimiento de Outlook Web App (OWA) supervisa el mantenimiento general del servicio Outlook Web App.

Si recibe una alerta que especifica que Outlook Web App es incorrecto, esto indica un problema que puede impedir que los usuarios tengan acceso a su buzón utilizando Outlook Web App.

## Explicación

El servicio Outlook Web App se supervisa mediante los monitores y sondeos siguientes.


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
<td><p>OwaCtpProbe</p></td>
<td><p>Outlook Web App</p></td>
<td><p>Active Directory</p>
<p>Información adicional</p></td>
<td><p>OwaCtpMonitor</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de monitores y sondeos, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Se pueden producir errores en este sondeo por varias razones. A continuación, se muestran algunas de las razones más comunes:

  - El grupo de aplicaciones de Outlook Web App que se hospeda en el servidor de acceso de cliente (CAS) supervisado no responde o el grupo de aplicaciones que se hospeda en el servidor de buzones no responde.

  - El CAS está experimentando problemas de red y no puede conectarse al controlador de dominio o al servidor de buzones.

  - Las credenciales de la cuenta de supervisión son incorrectas.

  - La base de datos del usuario no está montada o el almacén de información no está disponible para ese buzón.

  - El almacén de información no responde.

  - Los controladores de dominio no están respondiendo.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifique que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que generó la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Para recuperar los detalles del conjunto de mantenimiento de Outlook Web App sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA"}
    
    2.  Revise el resultado del comando para determinar qué monitor notificó el error. El valor de **AlertValue** para el monitor que emitió la alerta es `Unhealthy`.
    
    3.  Vuelva a ejecutar el sondeo asociado para el monitor que tiene estado incorrecto. Consulte la tabla en la sección Explicación para encontrar el sondeo asociado. Para comprobarlo, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por ejemplo, para crear un sondeo de supervisión de Exchange ActiveSync en *server1.contoso.com*, ejecute el siguiente comando:
        
            Invoke-MonitoringProbe -Identity ActiveSync.Protocol\ActiveSyncSelfTestProbe -Server server1.contoso.com
    
    4.  En el resultado del comando, revise el valor **Resultado** del sondeo. Si el valor es **Correcto**, el problema fue un error transitorio y ya no existe. En caso contrario, consulte los pasos de recuperación descritos en las secciones siguientes.

## Acciones de recuperación de OwaCtpMonitor

Una alerta de correo electrónico de un conjunto de mantenimiento contiene la siguiente información:

  - Nombre del servidor que envió la alerta

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica de encabezado HTTP  
    
    **Nota**   Puede utilizar la información en el seguimiento de excepción completo para ayudar a resolver el problema. La excepción generada por el sondeo contiene un motivo de error que describe la causa del error del sondeo. Por ejemplo, la excepción contiene lo siguiente:
    
      - **MissingKeyword**   No se encontró una palabra clave esperada en la respuesta del servidor. En este caso, la excepción contiene las palabras clave esperadas.
    
      - **NameResolution**   La resolución DNS no puede resolver un nombre de servidor determinado.
    
      - **NetworkConnection**   El sondeo recibe un error de conexión de red cuando intenta conectarse al grupo de aplicaciones OWA en CAFE.
    
      - **UnexpectedHttpResponseCode**   La respuesta devolvió un código HTTP inesperado. Por ejemplo, el servidor devolvió el código HTTP **503**.
    
      - **RequestTimeout**   El servidor tardó demasiado en responder una solicitud de cliente.
    
      - **ScenarioTimeout**   El sondeo finalizó correctamente, pero tardó más de un minuto en hacerlo. Normalmente, esto indica que se está sobrecargando el sistema.
    
      - **OwaErrorPage**Outlook Web App devolvió una página de error. El nombre del error que generó el problema suele aparecer en el mensaje de la excepción.
    
      - **OwaMailboxErrorPage**Outlook Web App devolvió una página de error que contiene un error relacionado con el almacén de buzones. Normalmente, esto indica que el almacén de buzones está inactivo o que se están desmontando buzones.
    
    El seguimiento de la excepción contiene un campo importante denominado **FailingComponent**. El sondeo intenta determinar el error, como en el siguiente ejemplo:
    
      - **Mailbox**   El sondeo puede acceder a Outlook Web App, pero no puede conectarse al almacén de buzones. En este caso, se produjo un error en el sondeo, o la latencia de acceso al buzón provocó que se produjera un error en el sondeo y que se generara el error **ScenarioTimeout**. Cuando se produce este tipo de errores, debe comprobar el mantenimiento de los servidores de buzones.
    
      - **Active Directory**   El sondeo puede acceder a Outlook Web App, pero no puede conectarse a Active Directory. En este caso, se produjo un error en el sondeo o quizás las latencias de llamada de Active Directory ocasionaron que se agotara el tiempo de espera de este. Cuando se produce este tipo de errores, debe comprobar el mantenimiento de los controladores de dominio y las conexiones de red entre los servidores de buzones y CA, y los controlados de dominio.
    
      - **Owa**   Esto suele indicar que se generó un error dentro de la capa de Outlook Web App. Cuando se produce este tipo de errores, debe comprobar el mantenimiento del proceso de Outlook Web App en los servidores de buzones y CA, y el mantenimiento de las conexiones de red.
    
    La excepción también contiene la solicitud HTTP más reciente y la información de respuesta que se recibió antes de que se produjera el error en el sondeo. El cuerpo de escalación contiene la ruta de acceso a los registros del sondeo. Puede utilizar esta información para determinar todas las solicitudes web HTTP y las respuestas que se enviaron cuando se produjo el error en el sondeo. Este archivo solo contiene datos de los sondeos con error porque solo se registran los intentos con error. Puede utilizar esta información para obtener una visión más completa de por qué se produjo un error en la prueba.

  - Cuánto bajo la métrica de disponibilidad (x %).

  - La ruta de acceso completa a la carpeta que contiene los seguimientos de solicitudes HTTP completos del sondeo. De forma predeterminada, esta información se encuentra en la carpeta *\<ExchangeServer\>*\\Logging\\Monitoring\\OWA\\ClientAccessProbe.

  - La hora y la fecha en que se produjo la alerta.

Para resolver este problema, siga estos pasos:

1.  Cree una cuenta de usuario de prueba y, luego, inicie sesión en el CAS con dicha cuenta. Por ejemplo, inicie sesión mediante https:// *\<NombreDeServidor\>*/owa.
    
    Si no puede hacerlo, pruebe con otro servidor CA para comprobar que el problema ocurre en un CAS específico y no en el servidor de buzones.

2.  Compruebe la conectividad de red entre los servidores de buzones y CA. Utilice ping.exe para comprobar que todos los servidores respondan.

3.  Compruebe si hay alertas en el conjunto de mantenimiento OWA.Protocol que puedan indicar un problema que afecte a un servidor de buzones específico. Para obtener más información, consulte [Solución de problemas del conjunto de mantenimiento OWA.Protocol](troubleshooting-owa-protocol-health-set.md).

4.  Inicie el Administrador de IIS y, luego, conéctese al servidor que notifica el problema para comprobar que el grupo de aplicaciones MSExchangeOwaAppPool se esté ejecutando en el servidor CAS.

5.  En el Administrador de IIS, compruebe que se esté ejecutando el sitio web predeterminado.

6.  Ubique la base de datos de buzones de los sondeos con error y compruebe que esté activa en un servidor de buzones y que el almacén de buzones sea correcto. Para ubicar la información del GUID de la base de datos con error, abra la información del seguimiento de excepción completo. Cada error debe contener una entrada similar al siguiente ejemplo:
    
    Iniciar sondeo de OWA con destino: https://localhost/owa/, nombre de usuario: *HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com*

7.  Copie el GUID de HealthMailbox y, luego, ejecute el siguiente comando en el Shell:
    
        Get-Mailbox -Monitoring -Identity <username>
    
    Por ejemplo, ejecute el comando siguiente:
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    En el objeto devuelto, puede ubicar el nombre de la base de datos del usuario y también puede determinar dónde reside la base de datos activa actualmente.

8.  Si configuró el redireccionamiento entre sitios, es posible que vea sondeos con error y otros que generan el error MissingKeyword. Esto sucede porque, de manera predeterminada, los sondeos de CA se ejecutan en cuentas de cualquier ubicación y también porque no intentan probar los CAS de sitios diferentes cuando utilizan el redireccionamiento. Para resolver este problema, asegúrese de que los servidores de cada sitio estén en MonitoringGroups. Los servidores CA de un grupo de supervisión determinado se prueban solo con servidores de buzones del mismo grupo.
    
    Para determinar los grupos de supervisión de sus servidores, ejecute el siguiente comando:
    
        Get-ExchangeServer | ft MonitoringGroup
    
    Para modificar el grupo de supervisión en un servidor, utilice el parámetro *MonitoringGroup* junto con el cmdlet **Set-ExchangeServer**. Por ejemplo, utilice lo siguiente:
    
        Set-ExchangeServer -Identity "ServerName" -MonitoringGroup "Primary"

9.  En el Administrador de IIS, haga clic en **Grupos de aplicaciones** y, luego, recicle el grupo de aplicaciones **MSExchangeOWAAppPool** mediante la ejecución del siguiente comando desde el Shell de administración de Exchange:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

10. Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

11. Si el problema persiste, recicle el servicio IIS mediante la utilidad IISReset o mediante la ejecución del siguiente comando:
    
        Iisreset /noforce

12. Vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

13. Si el problema aún persiste, reinicie el servidor.

14. Después de reiniciar el servidor, vuelva a ejecutar el sondeo asociado, como se muestra en el paso 2c de la sección Comprobar que el problema aún persiste.

15. Si el sondeo sigue con error, es posible que necesite ayuda para solucionar el problema. Comuníquese con un profesional de Soporte técnico de Microsoft para resolver este problema. Para comunicase con un profesional del Soporte técnico de Microsoft, visite el [Centro de soluciones de Exchange Server](http://go.microsoft.com/fwlink/p/?linkid=180809). En el panel de navegación, haga clic en **Opciones y recursos de soporte técnico** y use una de las opciones que se enumeran en **Obtener soporte técnico** para comunicarse con un profesional de Soporte técnico de Microsoft. Como su organización puede tener un procedimiento específico para comunicarse directamente con los servicios de soporte técnico de Microsoft, asegúrese de revisar primero las pautas de su organización

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

