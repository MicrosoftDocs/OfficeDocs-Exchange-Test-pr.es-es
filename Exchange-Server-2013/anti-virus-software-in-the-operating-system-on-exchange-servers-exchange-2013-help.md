---
title: 'Software antivirus en el sistema operativo de servidores Exchange: Exchange 2013 Help'
TOCTitle: Software antivirus en el sistema operativo de servidores Exchange
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 48268328
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Software antivirus en el sistema operativo de servidores Exchange

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-07-22_

Este tema describe los efectos de los programas antivirus de nivel de archivo en los equipos que ejecutan Microsoft Exchange Server 2013. Si implementa las recomendaciones descritas en este tema, puede ayudar a mejorar la seguridad y la salud de su organización de Exchange.

Los analizadores de archivos se usan con frecuencia. Sin embargo, si no se configuran correctamente, pueden causar problemas en Exchange 2013. Existen dos tipos de analizadores de archivos:

  - *Análisis de archivos residente en memoria* hace referencia a una parte del software antivirus para archivos que está cargada en la memoria en todo momento. Comprueba todos los archivos que se usan en el disco duro y en la memoria del equipo.

  - *Análisis de archivos a petición* hace referencia a una parte del software antivirus para archivos que se puede configurar para analizar los archivos del disco duro manualmente o según una programación. Algunas versiones del software antivirus comienzan el análisis a petición automáticamente cuando se actualizan las firmas de los virus para asegurarse de que todos los archivos se analizan con las últimas firmas.

Cuando se usan analizadores de archivos con Exchange 2013 pueden producirse los siguientes problemas:

  - Los analizadores de archivos podrían analizar un archivo mientras se está usando o con un intervalo programado, lo que podría provocar que los analizadores bloquearan o pusieran en cuarentena un registro de Exchange o un archivo de base de datos mientras Exchange 2013 intenta usarlo. Este comportamiento podría causar un error grave en Exchange 2013, además de errores -1018 de registro de eventos.

  - Los analizadores de archivos no proporcionan protección contra virus de correo electrónico, como el virus Storm Worm. Storm Worm era un programa caballo de Troya de puerta trasera que se propagó automáticamente a través de mensajes de correo electrónico. El gusano unió el equipo infectado a una botnet por el que el equipo se utilizó para enviar mensajes de correo electrónico no deseado en ráfagas periódicas.

## Recomendaciones para el uso de análisis de nivel de archivo con Exchange 2013

Si va a implementar analizadores de archivos en servidores de Exchange 2013, asegúrese de realizar las exclusiones apropiadas para los directorios, procesos y extensiones de nombres de archivo tanto en los análisis residentes en memoria como en el nivel de archivo. Esta sección describe las exclusiones recomendadas de directorio, de procesos y de extensión de nombre de archivo.

**Contenido**

Exclusiones de directorios

Exclusiones de procesos

Exclusiones de extensiones de nombres de archivo

## Exclusiones de directorios

Debe excluir directorios específicos para cada servidor de Exchange en el cual ejecute un analizador antivirus de nivel de archivos. Esta sección describe los directorios que debe excluir del análisis de nivel de archivo.

  - **servidores de buzones de correo**
    
      - **Bases de datos de buzones de correo**
        
          - Archivos de bases de datos, de punto de control y de registro de Exchange. De manera predeterminada, están ubicados en subcarpetas, dentro de la carpeta %ExchangeInstallPath%Mailbox. Para determinar la ubicación de una base de datos de buzones de correo, de un registro de transacción y de un archivo de punto de control, ejecute el siguiente comando: `Get-MailboxDatabase -Server <servername>| Format-List *path*`
        
          - Índices de contenido de bases de datos. De forma predeterminada, éstos se encuentran en la misma carpeta que el archivo de la base de datos.
        
          - Archivos de Métricas de grupo. De manera predeterminada, estos archivos están ubicados en la carpeta %ExchangeInstallPath%GroupMetrics.
        
          - Archivos de registro generales, como los archivos de registro de seguimiento de mensajes y de reparación de calendario. De manera predeterminada, estos archivos están ubicados en subcarpetas dentro de la carpeta %ExchangeInstallPath%TransportRoles\\Logs y %ExchangeInstallPath%Logging. Para determinar las rutas de registro que se van a usar, ejecute este comando en el Shell de administración de Exchange: `Get-MailboxServer <servername> | Format-List *path*`
        
          - Archivos de la libreta de direcciones sin conexión. De forma predeterminada, están ubicados en subcarpetas dentro de la carpeta %ExchangeInstallPath%ClientAccess\\OAB.
        
          - Archivos del sistema IIS en la carpeta %SystemRoot%\\System32\\Inetsrv.
        
          - La carpeta temporal de la base de datos de buzones de correo: %ExchangeInstallPath%Mailbox\\MDBTEMP
    
      - **Miembros de grupos de disponibilidad de base de datos**
        
          - Todos los elementos que aparecen en la lista **Bases de datos de buzones de correo** y la base de datos de quórum de clúster que existe en %Windir%\\Cluster.
        
          - Los archivos del directorio testigo. Estos archivos están ubicados en otro servidor del entorno, normalmente un servidor de acceso de cliente que no está instalado en el mismo equipo que el servidor de buzones de correo. De forma predeterminada, el directorio testigo está ubicado en la ruta de acceso %SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\>.
    
      - **Servicio de transporte**
        
          - Archivos de registro, por ejemplo, registros de conectividad y seguimiento de mensajes. De manera predeterminada, estos archivos están ubicados en subcarpetas dentro de la carpeta %ExchangeInstallPath%TransportRoles\\Logs. Para determinar las rutas de registro que se van a usar, ejecute este comando en el Shell de administración de Exchange: `Get-TransportService <servername> | Format-List *logpath*,*tracingpath*`
        
          - Carpetas de directorio de mensajes Recogida y Reproducción. De manera predeterminada, estas carpetas están ubicadas dentro de la carpeta %ExchangeInstallPath%TransportRoles. Para determinar las rutas que se van a usar, ejecute este comando en el Shell de administración de Exchange: `Get-TransportService <servername>| Format-List *dir*path*`
        
          - Las bases de datos de cola, los puntos de control y los archivos de registro. De manera predeterminada, están ubicados en la carpeta %ExchangeInstallPath%TransportRoles\\Data\\Queue.
        
          - La base de datos de reputación de remitente, el punto de control y los archivos de registro. De manera predeterminada, están ubicados en la carpeta %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation.
        
          - Las carpetas temporales usadas para realizar las conversiones:
            
              - de forma predeterminada, las conversiones de contenido se realizan en la carpeta %TMP% del servidor de Exchange.
            
              - De manera predeterminada, la conversión de formato de texto enriquecido (RTF) a MIME/HTML se realiza en la carpeta %ExchangeInstallPath%\\Working\\OleConverter.
        
          - El agente Malware y la prevención de pérdida de datos (DLP) utilizan el componente de análisis de contenido. De forma predeterminada, estos archivos se encuentran en la carpeta %ExchangeInstallPath%FIP-FS.
    
      - **Servicio de transporte de buzón de correo**
        
          - Archivos de registro, por ejemplo, registros de conectividad. De manera predeterminada, estos archivos están ubicados en subcarpetas en la carpeta %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox. Para determinar las rutas de registro que se van a usar, ejecute este comando en el Shell de administración de Exchange: `Get-MailboxTransportService <servername> | Format-List *logpath*`
    
      - **Mensajería unificada**
        
          - Los archivos de gramática de las distintas configuraciones regionales, por ejemplo, en-EN o es-ES. De manera predeterminada, están almacenados en subcarpetas de la carpeta %ExchangeInstallPath%UnifiedMessaging\\grammars.
        
          - Los archivos de mensajes de asistencia por voz, de saludos y de mensajes informativos. De manera predeterminada, están almacenados en subcarpetas de la carpeta %ExchangeInstallPath%UnifiedMessaging\\Prompts
        
          - Los archivos de correo de voz se almacenan temporalmente en la carpeta %ExchangeInstallPath%UnifiedMessaging\\voicemail.
        
          - Los archivos temporales que genera Mensajería unificada. De manera predeterminada, se almacenan en la carpeta %ExchangeInstallPath%UnifiedMessaging\\temp.
    
      - **Instalación**
        
          - Archivos temporales de instalación de Exchange Server. Normalmente, estos archivos se encuentran en % SystemRoot%\\Temp\\ExchangeSetup.
    
      - **Servicio Exchange Search**
        
          - Archivos temporales utilizados por el servicio Exchange Search y Microsoft Filter Pack para realizar la conversión de archivos en un entorno de espacio aislado. Estos archivos se encuentran en %SystemRoot%\\Temp\\OICE\_*\<GUID\>*\\.

<!-- end list -->

  - **servidores Acceso de cliente**
    
      - **Componentes web**
        
          - Para los servidores que usan Internet Information Services (IIS) 7.0, la carpeta de compresión que se usa con Microsoft Outlook Web App. De forma predeterminada, la carpeta de compresión de IIS 7.0 está ubicada en %SystemDrive%\\inetpub\\temp\\IIS Temporary Compressed Files.
        
          - Archivos del sistema IIS en la carpeta %SystemRoot%\\System32\\Inetsrv
        
          - Inetpub\\logs\\logfiles\\w3svc
        
          - Subcarpetas de los archivos %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary ASP.NET
    
      - **Registro de protocolos POP3 y IMAP4**
        
          - Carpeta POP3: %ExchangeInstallPath%Logging\\POP3
        
          - Carpeta IMAP4: %ExchangeInstallPath%Logging\\IMAP4
    
      - **Servicio de transporte de front-end**
        
          - Archivos de registro, por ejemplo, registros de conectividad y registros de protocolo. De manera predeterminada, estos archivos se ubican en subcarpetas de la carpeta %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd. Para determinar las rutas de registro que se van a usar, ejecute este comando en el Shell de administración de Exchange: `Get-FrontEndTransportService <servername> | Format-List *logpath*`
    
      - **Programa de instalación**
        
          - Archivos temporales del programa de instalación de Exchange Server. Normalmente, estos archivos se encuentran en %SystemRoot%\\Temp\\ExchangeSetup.

Recomendaciones para el uso de análisis de nivel de archivo con Exchange 2013

## Exclusiones de procesos

Muchos analizadores de archivo ahora admiten el análisis de procesos, que puede producir un efecto negativo en Microsoft Exchange si se analizan los procesos incorrectos. Por lo tanto, debe excluir los siguientes procesos de los analizadores de archivos.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Proceso</th>
<th>Ruta de acceso</th>
<th>Comentarios</th>
<th>Servidores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dsamain.exe</p></td>
<td><p>%SystemRoot%\System32</p></td>
<td><p>Active Directory Lightweight Directory Services (AD LDS) en servidores de transporte perimetral suscritos.</p></td>
<td><p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Proceso de trabajo del servicio de transporte de Microsoft Exchange</p></td>
<td><p>servidores de buzones de correo</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>fms.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente de exploración de contenido que usan el agente de malware y DLP.</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>hostcontrollerservice.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\HostController</p></td>
<td><p>Servicio de controlador de host de búsqueda de Microsoft Exchange (HostControllerService)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>inetinfo.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.AntispamUpdateSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de actualización contra correo electrónico no deseado de Microsoft Exchange (MSExchangeAntispamUpdate)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.ContentFilter.Wrapper.exe</p></td>
<td><p>%ExchangeInstallPath%TransportRoles\agents\Hygiene</p></td>
<td><p>Agente de filtro de contenido</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Diagnostics.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de diagnósticos de Microsoft Exchange (MSExchangeDiagnostics)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Directory.TopologyService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de topología de Microsoft Exchange Active Directory (MSExchangeADTopology)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.EdgeCredentialSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de credenciales de Microsoft Exchange (MSExchangeEdgeCredential)</p></td>
<td><p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.EdgeSyncSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio EdgeSync de Microsoft Exchange (MSExchangeEdgeSync)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Imap4.exe</p></td>
<td><p>ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Servicio IMAP4 de Microsoft Exchange (MSExchangeImap4)</p></td>
<td><p>Servidores de acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Imap4service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Servicio de IMAP4 Backend de Microsoft Exchange (MSExchangeIMAP4BE)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Pop3.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Servicio POP3 de Microsoft Exchange (MSExchangePop3)</p></td>
<td><p>Servidores de acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Pop3service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Servicio POP3 Backend de Microsoft Exchange (MSExchangePOP3BE)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.ProtectedServiceHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de host de servicios de Microsoft Exchange (MSExchangeServiceHost)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.RPCClientAccess.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de acceso de cliente de RPC de Microsoft Exchange (MSExchangeRPC)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Search.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de búsqueda de Microsoft Exchange (MSExchangeFastSearch)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Servicehost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de host de servicios de Microsoft Exchange (MSExchangeServiceHost)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Store.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio Almacén de información de Microsoft Exchange (MSExchangeIS)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Store.Worker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Proceso de trabajo del servicio Almacén de información de Microsoft Exchange</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.UM.CallRouter.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\CallRouter</p></td>
<td><p>Servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange (MSExchangeUMCR)</p></td>
<td><p>Servidores de acceso de cliente</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeDagMgmt.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de administración de Microsoft Exchange DAG (MSExchangeDagMgmt)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeDelivery.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de entrega de transporte de buzones de Microsoft Exchange (MSExchangeDelivery)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeFrontendTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de transporte front-end de Microsoft Exchange (MSExchangeFrontEndTransport)</p></td>
<td><p>Servidores de acceso de cliente</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeHMHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio Administrador de estado de Microsoft Exchange (MSExchangeHM)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeHMWorker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Proceso de trabajo del servicio Administrador de estado de Microsoft Exchange</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio Asistentes de buzón de Microsoft Exchange (MSExchangeMailboxAssistants)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxReplication.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de replicación de buzones de Microsoft Exchange (MSExchangeMailboxReplication)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMigrationWorkflow.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de flujo de trabajo de migración de Microsoft Exchange (MSExchangeMigrationWorkflow)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeRepl.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de replicación de Microsoft Exchange (MSExchangeRepl)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeSubmission.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de envío de transporte de buzones de Microsoft Exchange (MSExchangeSubmission)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de transporte de Microsoft Exchange (MSExchangeTransport)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeTransportLogSearch.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de búsqueda de registros de transporte de Microsoft Exchange (MSExchangeTransportLogSearch)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeThrottling.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de limitación de peticiones de Microsoft Exchange (MSExchangeThrottling)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>Noderunner.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0</p></td>
<td><p>Servicio de búsqueda de Microsoft Exchange (MSExchangeFastSearch)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>OleConverter.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Convierte los mensajes de formato de texto enriquecido (RTF) a MIME/HTML para los destinatarios externos.</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>ParserServer.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\ParserServer</p></td>
<td><p>Servicio de búsqueda de Microsoft Exchange (MSExchangeFastSearch)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>Powershell.exe</p></td>
<td><p>C:\Windows\System32\WindowsPowerShell\v1.0</p></td>
<td><p>Shell de administración de Exchange</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p>
<p>Servidores de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>ScanEngineTest.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente de exploración de contenido que usan el agente de malware y DLP.</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>ScanningProcess.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente de exploración de contenido que usan el agente de malware y DLP.</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>TranscodingService.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing</p></td>
<td><p>Visualización de documentos WebReady en Outlook Web App.</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>UmService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Servicio de mensajería unificada de Microsoft Exchange (MSExchangeUM)</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>UmWorkerProcess.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Proceso de trabajo del servicio de mensajería unificada de Microsoft Exchange</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="odd">
<td><p>UpdateService.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente de exploración de contenido que usan el agente de malware y DLP.</p></td>
<td><p>Servidores de buzones de correo</p></td>
</tr>
<tr class="even">
<td><p>W3wp.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>Servidores de buzones de correo</p>
<p>Servidores de acceso de cliente</p></td>
</tr>
</tbody>
</table>


Recomendaciones para el uso de análisis de nivel de archivo con Exchange 2013

## Exclusiones de extensiones de nombres de archivo

Además de excluir directorios y procesos específicos, debe excluir las siguientes extensiones de nombres de archivo específicos de Exchange en caso de que se produzcan errores en las exclusiones de directorios o que se muevan archivos de sus ubicaciones predeterminadas.

  - Extensiones relacionadas con la aplicación:
    
      - .config
    
      - .dia
    
      - .wsb

<!-- end list -->

  - Extensiones relacionadas con bases de datos:
    
      - .chk
    
      - .edb
    
      - .jrs
    
      - .jsl
    
      - .log
    
      - .que

<!-- end list -->

  - Extensiones relacionadas con la libreta de direcciones sin conexión:
    
      - .lzx

<!-- end list -->

  - Extensiones relacionadas con el índice de contenido:
    
      - .ci
    
      - .dir
    
      - .wid
    
      - .000
    
      - .001
    
      - .002

<!-- end list -->

  - Extensiones relacionadas con Mensajería unificada:
    
      - .cfg
    
      - .grxml

<!-- end list -->

  - Extensiones relacionadas con las métricas de grupo:
    
      - .dsc
    
      - .txt

Recomendaciones para el uso de análisis de nivel de archivo con Exchange 2013

