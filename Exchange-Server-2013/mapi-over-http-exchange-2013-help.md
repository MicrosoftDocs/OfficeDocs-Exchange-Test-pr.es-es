---
title: 'MAPI sobre HTTP: Exchange 2013 Help'
TOCTitle: MAPI sobre HTTP
ms:assetid: 4663b5db-5b30-4a5a-a302-be6fef7fe5da
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn635177(v=EXCHG.150)
ms:contentKeyID: 61204106
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# MAPI sobre HTTP

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-05-10_

Interfaz de programación de aplicaciones de mensajería (MAPI) sobre HTTP es un nuevo protocolo de transporte implementado en MicrosoftExchange Server 2013 Service Pack 1 (SP1). MAPI sobre HTTP traslada la capa de transporte al modelo HTTP estándar de la industria para mejorar la confiabilidad y la estabilidad de las conexiones de Outlook y Exchange. Esto permite un mayor nivel de visibilidad de los errores de transporte y una capacidad de recuperación mayor. Entre la funcionalidad adicional se incluye compatibilidad para una función de pausa y reanudación explícitas. Esto permite a los clientes compatibles cambiar de red o reactivarse después de la hibernación, manteniendo el mismo contexto de servidor.

Implementar MAPI sobre HTTP no significa que sea el único protocolo que se puede usar para que Outlook acceda a Exchange. Los clientes de Outlook que no sean compatibles con MAPI sobre HTTP pueden seguir usando Outlook en cualquier lugar (RPC sobre HTTP) para acceder a Exchange a través de un servidor de acceso de cliente habilitado para MAPI.

## Ventajas de MAPI sobre HTTP

MAPI sobre HTTP ofrece las siguientes ventajas a los clientes compatibles:

  - Permite innovar en la autenticación en el futuro usando un protocolo basado en HTTP.

  - Proporciona tiempos de reconexión más rápidos después de una interrupción de las comunicaciones porque solo se necesita reconstruir las conexiones TCP, no las conexiones RPC. Algunos ejemplos de una interrupción de las comunicaciones son:
    
      - Hibernación de dispositivos
    
      - Cambio de una red cableada a una red inalámbrica o móvil

  - Ofrece un contexto de sesión que no depende de la conexión. El servidor mantiene el contexto de sesión durante un período de tiempo configurable, aunque el usuario cambie de red.

## Implementar MAPI sobre HTTP

Tenga en cuenta los siguientes requisitos para habilitar MAPI sobre HTTP.

  - **Compatibilidad**   Compruebe que se admiten las versiones de configuración previstas.

  - **Requisitos previos**   Compruebe que el entorno se ha actualizado y preparado para MAPI sobre HTTP.

  - **Configuración**   Configure los directorios virtuales y habilite MAPI para su organización.

## Compatibilidad

Use la siguiente matriz para comprobar que sus clientes y servidores admiten MAPI sobre HTTP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Producto</th>
<th>Exchange 2013 SP1</th>
<th>Exchange 2013 RTM</th>
<th>Exchange 2010 SP3</th>
<th>Exchange 2007 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 SP1</p></td>
<td><ul>
<li><p>MAPI sobre HTTP</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
<td><p>Outlook en cualquier lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2013 RTM</p></td>
<td><p>Outlook en cualquier lugar</p></td>
<td><p>Outlook en cualquier lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2010SP2 y actualizaciones KB2956191 y KB2965295 (14 de abril de 2015)</p></td>
<td><ul>
<li><p>MAPI sobre HTTP<span></span></p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
<td><p>Outlook en cualquier lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2010 SP2 y versiones anteriores</p></td>
<td><p>Outlook en cualquier lugar</p></td>
<td><p>Outlook en cualquier lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Outlook en cualquier lugar</p></td>
<td><p>Outlook en cualquier lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook en cualquier lugar</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Requisitos previos

Complete los siguientes pasos para preparar los clientes y servidores para admitir MAPI sobre HTTP.

1.  Actualice los clientes de Outlook a Outlook 2013 SP1 o Outlook 2010 SP2 y las actualizaciones KB2956191 y KB2965295 (14 de abril de 2015).

2.  Actualice los servidores de buzones de correo y de acceso de cliente a Exchange 2013 SP1. Para obtener información acerca de cómo actualizar, vea [Actualizar Exchange 2013 a la actualización acumulativa o Service Pack más reciente](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md).
    

    > [!NOTE]
    > Todos los servidores de acceso de cliente deben actualizarse a Exchange&nbsp;2013 SP1 antes de habilitar MAPI sobre HTTP. De lo contrario, Outlook puede producir un error al conectarse a los buzones.<BR>Si no se actualizan todos los servidores de buzones de correo de un grupo de disponibilidad de la base de datos (DAG), se pueden producir retrasos en el correo electrónico y un cliente puede necesitar que se reinicie Outlook en caso de conmutación por error de una base de datos.



3.  En todos los servidores de Exchange 2013, debe instalar Microsoft.NET Framework 4.5.2. Para obtener más información, consulte [Instalación de .NET Framework](https://go.microsoft.com/fwlink/p/?linkid=518380).

4.  En todos los servidores de acceso de cliente de Exchange 2013 SP1, agregue la variable de entorno de Windows **COMPLUS\_DisableRetStructPinning** mediante los siguientes pasos.
    
    1.  En una ventana del símbolo del sistema, ejecute `systempropertiesadvanced` y haga clic en **Variables de entorno**.
    
    2.  En la sección **Variables del sistema**, haga clic en **Nuevo** e introduzca la siguiente información.
        
          - **Nombre de la variable**   `COMPLUS_DisableRetStructPinning`
        
          - **Valor de la variable**   1
    
    3.  Cuando haya terminado, haga clic en **Aceptar**.

## Configuración

Complete los pasos siguientes para configurar MAPI sobre HTTP para su organización.

1.  **Configuración de directorios virtuales**   De forma predeterminada, Exchange 2013 SP1 crea un directorio virtual para MAPI sobre HTTP. Use el cmdlet **Set-MapiVirtualDirectory** para configurar el directorio virtual. Debe configurar una dirección URL interna, una dirección URL externa o ambas. Para obtener más información, vea [Set-MapiVirtualDirectory](https://technet.microsoft.com/es-es/library/dn595082\(v=exchg.150\)).
    
    Por ejemplo, puede configurar el directorio virtual de MAPI predeterminado en el servidor de Exchange local estableciendo el valor de la dirección URL interna en https://contoso.com/mapi y el método de autenticación en `Negotiate`; para ello, ejecute el siguiente comando:
    
    ```powershell
    Set-MapiVirtualDirectory -Identity "Contoso\mapi (Default Web Site)" -InternalUrl https://Contoso.com/mapi -IISAuthenticationMethods Negotiate
    ```

2.  **Configuración de certificados**   El certificado digital que usa su entorno de Exchange debe incluir los mismos valores de *InternalURL* y *ExternalURL* que se han definido en el directorio virtual de MAPI. Para obtener más información sobre la administración de certificados en Exchange 2013, vea [Certificados digitales y SSL](digital-certificates-and-ssl-exchange-2013-help.md). Asegúrese de que el certificado de Exchange sea de confianza en la estación de trabajo cliente de Outlook y que no haya errores de certificado, especialmente al acceder a las direcciones URL configuradas en el directorio virtual de MAPI.

3.  **Actualice las reglas de servidor**   Compruebe que los equilibradores de carga, los servidores proxy inversos y los firewalls estén configurados para que permitan el acceso al directorio virtual de MAPI sobre HTTP.

4.  **Habilite MAPI sobre HTTP en su organización de Exchange**
    
    Ejecute el siguiente comando:
    
    ```powershell
    Set-OrganizationConfig -MapiHttpEnabled $true
    ```

## Pruebe las conexiones de MAPI sobre HTTP

Puede probar la conexión de MAPI sobre HTTP de extremo a extremo usando el cmdlet **Test-OutlookConnectivity**. Para usar el cmdlet **Test-OutlookConnectivity**, el servicio Administrador del estado de Microsoft Exchange (MSExchangeHM) debe estar iniciado.

El siguiente ejemplo prueba la conexión de MAPI sobre HTTP desde el servidor de Exchange llamado ContosoMail.

```powershell
Test-OutlookConnectivity -RunFromServerId ContosoMail -ProbeIdentity OutlookMapiHttpSelfTestProbe
```

Si la prueba es correcta, el resultado que devuelve es similar al del ejemplo siguiente:

```powershell
MonitorIdentity                                          StartTime              EndTime                Result      Error     Exception
---------------                                          ---------              -------                ------      -----     ---------
OutlookMapiHttp.Protocol\OutlookMapiHttpSelfTestProbe    2/14/2014 7:15:00 AM   2/14/2014 7:15:10 AM   Succeeded
```

Para obtener más información, vea [Test-OutlookConnectivity](https://technet.microsoft.com/es-es/library/dd638082\(v=exchg.150\)).

Los registros de la actividad de MAPI sobre HTTP se encuentran en las siguientes ubicaciones:

  - %ExchangeInstallPath%Logging\\MAPI Address Book Service\\

  - %ExchangeInstallPath%Logging\\MAPI Client Access\\

  - %ExchangeInstallPath%Logging\\HttpProxy\\Mapi\\

## Administrar MAPI sobre HTTP

Puede administrar la configuración de MAPI sobre HTTP usando los siguientes cmdlets:

  - [Set-MapiVirtualDirectory](https://technet.microsoft.com/es-es/library/dn595082\(v=exchg.150\))

  - [Get-MapiVirtualDirectory](https://technet.microsoft.com/es-es/library/dn595080\(v=exchg.150\))

  - [New-MapiVirtualDirectory](https://technet.microsoft.com/es-es/library/dn595081\(v=exchg.150\))

  - [Remove-MapiVirtualDirectory](https://technet.microsoft.com/es-es/library/dn595083\(v=exchg.150\))

