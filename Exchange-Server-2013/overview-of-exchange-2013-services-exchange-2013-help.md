---
title: 'Visión general de los servicios de Exchange de 2013: Exchange 2013 Help'
TOCTitle: Visión general de los servicios de Exchange de 2013
ms:assetid: 2ed45d18-2ff3-4099-b841-050eb16a416b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423542(v=EXCHG.150)
ms:contentKeyID: 74479254
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visión general de los servicios de Exchange de 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-10-20_

Durante la instalación de Exchange Server 2013, el programa de instalación ejecuta en un conjunto de tareas que instale nuevos servicios en Microsoft Windows. Un servicio es un proceso en segundo plano que puede ser lanzado durante el inicio del servidor Windows Service Control Manager. Servicios están diseñados para funcionar de forma independiente y sin intervención administrativa de archivos ejecutables. Un servicio puede ejecutarse mediante un modo de interfaz gráfica de usuario o un modo de consola.

Todas las versiones anteriores de Exchange incluyen componentes que se implementan como servicios. Cada función de servidor de Exchange incluye servicios que forman parte de (o pueden ser necesaria en) la función de servidor para realizar sus funciones. Tenga en cuenta que algunos servicios sólo activarán cuando se utilizan características específicas.

Las secciones en este tema describen los distintos servicios que se instalan de Exchange 2013 en los servidores de buzón de correo, servidores de acceso de cliente y servidores de transporte perimetral. Para los servicios que se etiquetan como opcional, puede deshabilitar el servicio si determina que su organización no necesita la funcionalidad proporcionada por el servicio.

## Servicios de Exchange en los servidores de buzones de Exchange 2013

La tabla siguiente describe los servicios de Exchange que se instalan en servidores de buzones.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del servicio</th>
<th>Nombre corto del servicio</th>
<th>Descripción y dependencias</th>
<th>Tipo de inicio predeterminado</th>
<th>Contexto de seguridad</th>
<th>Dependencias</th>
<th>Obligatorio u opcional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Proporciona información de topología de Active Directory a Exchange servicios. Si se detiene este servicio, no se puede iniciar la mayoría de los servicios de Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Servicio de uso compartido de puertos Net.TCP</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Actualización contra correo electrónico no deseado de Microsoft Exchange</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Proporciona actualizaciones de definición de correo basura de SmartScreen de Exchange.</p>

> [!NOTE]
> El 1 de noviembre de 2016 Microsoft detuvo las actualizaciones de definiciones de correo no deseado para los filtros de SmartScreen en Exchange y Outlook. Las definiciones existentes de correo no deseado de SmartScreen permanecerán en su lugar, pero es probable que su eficacia se degrade con el tiempo. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange</A> (Fin del soporte de SmartScreen en Outlook y Exchange).


</td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Administración de DAG</p></td>
<td><p>MSExchangeDagMgmt</p></td>
<td><p>Proporciona administración de diseño de almacenamiento de información y base de datos para servidores de buzones en grupos de disponibilidad de base de datos (DAGs).</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p>
<p>Servicio de uso compartido de puertos Net.TCP</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnósticos</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Proporciona a un agente que supervisa el estado del servidor Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Ninguno</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange EdgeSync</p></td>
<td><p>MSExchangeEdgeSync</p></td>
<td><p>Replica datos de destinatario y configuración entre el servidor de buzón y UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) en servidores de transporte perimetral suscritos a través de un canal seguro de LDAP.</p>
<p>Si no tiene los servidores de transporte perimetral suscritos, puede deshabilitar este servicio.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Administrador de salud</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Parte de disponibilidad administrada que supervisa el estado de los componentes clave en el servidor Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Windows Registro de eventos</p>
<p>Windows Instrumental de administración de</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Back-end de IMAP4</p></td>
<td><p>MSExchangeIMAP4BE</p></td>
<td><p>Recibe conexiones de clientes procesadas desde el desde el servicio IMAP4 en servidores acceso de cliente. De forma predeterminada, este servicio no se está ejecutando, por lo que los clientes IMAP4 no pueden conectar con el servidor de Exchange hasta que se inicie este servicio.</p>
<p>Si no dispone de ningún cliente de IMAP4, puede deshabilitar este servicio.</p></td>
<td><p>Manual</p></td>
<td><p>Servicio de red</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="even">
<td><p>Almacén de información de Microsoft Exchange</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>Administra las bases de datos de buzón en el servidor. Si se detiene este servicio, no están disponibles las bases de datos de buzón en el servidor.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p>
<p>Llamada a procedimiento remoto (RPC)</p>
<p>Servidor</p>
<p>Windows Registro de eventos</p>
<p>Estación de trabajo</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Asistentes de buzón de Microsoft Exchange</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Realiza el procesamiento en segundo plano de los buzones en bases de datos de buzones en el servidor.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Replicación de buzones</p></td>
<td><p>MSExchangeMailboxReplication</p></td>
<td><p>Buzón de procesos se mueve y las solicitudes de movimiento.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p>
<p>Servicio de uso compartido de puertos Net.TCP</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Entrega de transporte de buzón</p></td>
<td><p>MSExchangeDelivery</p></td>
<td><p>Recibe mensajes SMTP de Microsoft Exchange servicio de transporte (en los servidores de buzón locales o remotos) y los entrega a una base de datos de buzón local mediante RPC.</p></td>
<td><p>Automático</p></td>
<td><p>Servicio de red</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Envío de transporte de buzón</p></td>
<td><p>MSExchangeSubmission</p></td>
<td><p>Recibe mensajes RPC desde una base de datos de buzón de correo local y envía a través de SMTP para el servicio de transporte (en los servidores de buzón locales o remotos) Microsoft Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Back-end de POP3</p></td>
<td><p>MSExchangePOP3BE</p></td>
<td><p>Recibe conexiones de cliente procesadas por el proxy desde el servicio POP3 en los servidores acceso de cliente. De forma predeterminada, este servicio no se está ejecutando, por lo que los clientes POP3 no pueden conectar con el servidor de Exchange hasta que se inicie este servicio.</p></td>
<td><p>Manual</p></td>
<td><p>Servicio de red</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="even">
<td><p>Servicio de replicación de Microsoft Exchange</p></td>
<td><p>MSExchangeRepl</p></td>
<td><p>Proporciona funcionalidad de replicación de bases de datos de buzones en una base de datos de grupos de disponibilidad (DAGs).</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Acceso de cliente RPC de Microsoft Exchange</p></td>
<td><p>MSExchangeRPC</p></td>
<td><p>Administra las conexiones RPC de cliente para Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Servicio de red</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Búsqueda</p></td>
<td><p>MSExchangeFastSearch</p></td>
<td><p>Proporciona indización del contenido del buzón, lo que mejora el rendimiento de la búsqueda de contenido.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Controladora de Host de búsqueda</p></td>
<td><p>HostControllerService</p></td>
<td><p>Proporciona servicios de implementación y administración de aplicaciones en el servidor local Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Servicio HTTP</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Extensión de Microsoft Exchange Server para Copias de seguridad de Windows Server</p></td>
<td><p>WSBExchange</p></td>
<td><p>Permite Windows Server copia de seguridad de copia y restauración de datos de servidor Exchange.</p></td>
<td><p>Manual</p></td>
<td><p>Sistema local</p></td>
<td><p>Ninguno</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Host de servicio de Microsoft Exchange</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Proporciona un servicio de host para los componentes de Exchange que no dispone de sus propios servicios.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Limitación de peticiones de Microsoft Exchange</p></td>
<td><p>MSExchangeThrottling</p></td>
<td><p>Proporciona administración de carga de trabajo del usuario que limita la tasa de las operaciones de usuario (conocido como límite de usuario).</p></td>
<td><p>Automático</p></td>
<td><p>Servicio de red</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Transporte de Microsoft Exchange</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Proporciona servidor SMTP y la pila de transporte.</p></td>
<td><p>Automático</p></td>
<td><p>Servicio de red</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p>
<p>Microsoft Servicio de administración de filtrado</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Búsqueda de registro de transporte Microsoft Exchange</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Proporciona capacidades de búsqueda remota de archivos de registro de transporte (por ejemplo, seguimiento de mensajes).</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Mensajería unificada de Microsoft Exchange</p></td>
<td><p>MSExchangeUM</p></td>
<td><p>Proporciona funciones de mensajería unificada (UM): permite que los mensajes de voz y de fax se almacenen en Exchange y ofrece a los usuarios acceso telefónico a correo electrónico, correo de voz, calendario, contactos o un operador automático. Si se detiene este servicio, mensajería unificada no estará disponible.</p>
<p>Si no utiliza la mensajería unificada, puede deshabilitar este servicio.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Aislamiento de claves CNG</p>
<p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
</tbody>
</table>


## Servicios de Exchange en los servidores acceso de cliente de Exchange 2013

La tabla siguiente describe los servicios de Exchange que están instalados en los servidores acceso de cliente.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del servicio</th>
<th>Nombre corto del servicio</th>
<th>Descripción y dependencias</th>
<th>Tipo de inicio predeterminado</th>
<th>Contexto de seguridad</th>
<th>Dependencias</th>
<th>Obligatorio u opcional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Proporciona información de topología de Active Directory a Exchange servicios. Si se detiene este servicio, no se puede iniciar la mayoría de los servicios de Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Servicio de uso compartido de puertos Net.TCP</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnósticos</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Proporciona a un agente que supervisa el estado del servidor Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Ninguno</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Transporte de front-end</p></td>
<td><p>MSExchangeFrontEndTransport</p></td>
<td><p>Conexiones de proxy SMTP desde hosts externos a la Microsoft Exchange el servicio de transporte en los servidores de buzones.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Administrador de salud</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Parte de disponibilidad administrada que supervisa el estado de los componentes clave en el servidor Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Windows Registro de eventos</p>
<p>Windows Instrumental de administración de</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4</p></td>
<td><p>MSExchangeIMAP4</p></td>
<td><p>Conexiones de cliente de IMAP4 de servidores proxy para el servicio IMAP4 en servidores de buzones. De forma predeterminada, este servicio no se está ejecutando, por lo que los clientes IMAP4 no pueden conectar con el servidor de Exchange hasta que se inicie este servicio.</p>
<p>Si no dispone de ningún cliente de IMAP4, puede deshabilitar este servicio.</p></td>
<td><p>Manual</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange POP3</p></td>
<td><p>MSExchangePOP3</p></td>
<td><p>Conexiones de cliente de POP3 de servidores proxy para el servicio IMAP4 en servidores de buzones. De forma predeterminada, este servicio no se está ejecutando, por lo que los clientes POP3 no pueden conectar con el servidor de Exchange hasta que se inicie este servicio.</p></td>
<td><p>Manual</p></td>
<td><p>Servicio de red</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Controladora de Host de búsqueda</p></td>
<td><p>HostControllerService</p></td>
<td><p>Proporciona servicios de implementación y administración de aplicaciones en el servidor local Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Servicio HTTP</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Host de servicio de Microsoft Exchange</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Proporciona un servicio de host para los componentes de Exchange que no dispone de sus propios servicios.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange El enrutador de llamada de mensajería unificada</p></td>
<td><p>MSExchangeUMCR</p></td>
<td><p>Redirige las conexiones de cliente de mensajería unificada para el servicio de mensajería unificada en servidores de buzones.</p>
<p>Si no utiliza la mensajería unificada, puede deshabilitar este servicio.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Aislamiento de claves CNG</p>
<p>Microsoft Exchange Topología de Active Directory</p></td>
<td><p>Opcional</p></td>
</tr>
</tbody>
</table>


## Servicios de Exchange en los servidores de transporte perimetral Exchange 2013

La tabla siguiente describe los servicios de Exchange que se instalan en servidores de transporte perimetral.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del servicio</th>
<th>Nombre corto del servicio</th>
<th>Descripción</th>
<th>Tipo de inicio predeterminado</th>
<th>Contexto de seguridad</th>
<th>Dependencias</th>
<th>Obligatorio u opcional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ADAM de Microsoft Exchange</p></td>
<td><p>ADAM_MSExchange</p></td>
<td><p>Almacena datos de configuración y destinatarios en el servidor de transporte perimetral. Este servicio representa la instancia con nombre de la UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) que Exchange el programa de instalación crea automáticamente.</p></td>
<td><p>Automático</p></td>
<td><p>Servicio de red</p></td>
<td><p>Sistema de sucesos COM +</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Actualización contra correo electrónico no deseado de Microsoft Exchange</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Proporciona actualizaciones de definición de correo basura de SmartScreen de Exchange.</p>

> [!NOTE]
> El 1 de noviembre de 2016 Microsoft detuvo las actualizaciones de definiciones de correo no deseado para los filtros de SmartScreen en Exchange y Outlook. Las definiciones existentes de correo no deseado de SmartScreen permanecerán en su lugar, pero es probable que su eficacia se degrade con el tiempo. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange</A> (Fin del soporte de SmartScreen en Outlook y Exchange).


</td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>ADAM de Microsoft Exchange</p></td>
<td><p>Opcional</p></td>
</tr>
<tr class="odd">
<td><p>Servicio de credenciales de Microsoft Exchange</p></td>
<td><p>MSExchangeEdgeCredential</p></td>
<td><p>Supervisa los cambios de credencial en UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) e instala los cambios en el servidor de transporte perimetral.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>ADAM de Microsoft Exchange</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Diagnósticos</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Proporciona a un agente que supervisa el estado del servidor Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Ninguno</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Administrador de salud</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Parte de disponibilidad administrada que supervisa el estado de los componentes clave en el servidor Exchange.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>Registro de eventos de Windows</p>
<p>Windows Management Instrumentation</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Host de servicio de Microsoft Exchange</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>Proporciona un servicio de host para los componentes de Exchange que no dispone de sus propios servicios.</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>ADAM de Microsoft Exchange</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="odd">
<td><p>Transporte de Microsoft Exchange</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>Proporciona servidor SMTP y la pila de transporte.</p></td>
<td><p>Automático</p></td>
<td><p>Servicio de red</p></td>
<td><p>ADAM de Microsoft Exchange</p></td>
<td><p>Obligatorio</p></td>
</tr>
<tr class="even">
<td><p>Búsqueda de registro de transporte Microsoft Exchange</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>Proporciona capacidades de búsqueda remota de archivos de registro de transporte (por ejemplo, seguimiento de mensajes).</p></td>
<td><p>Automático</p></td>
<td><p>Sistema local</p></td>
<td><p>ADAM de Microsoft Exchange</p></td>
<td><p>Opcional</p></td>
</tr>
</tbody>
</table>

