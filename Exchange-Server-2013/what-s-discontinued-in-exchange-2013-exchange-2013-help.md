---
title: 'Qué se ha discontinuado en Exchange 2013: Exchange 2013 Help'
TOCTitle: Qué se ha discontinuado en Exchange 2013
ms:assetid: 0ac0001c-b314-4108-b895-d9c0e271b489
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ619283(v=EXCHG.150)
ms:contentKeyID: 49116027
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Qué se ha discontinuado en Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

En este tema se tratan los componentes, las características o las funcionalidades que se han quitado, dejado de utilizar o sustituido en Microsoft Exchange Server 2013.


> [!NOTE]
> También le pueden interesar los siguientes temas: 
> <UL>
> <LI>
> <P><A href="what-s-new-in-exchange-2013-exchange-2013-help.md">Novedades en Exchange 2013</A>&nbsp;&nbsp;&nbsp;Información acerca de nuevas características y funcionalidades en Exchange Server 2013.</P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=267479">Hoja de ruta para el desarrollador de Exchange 2013</A> &nbsp;&nbsp;&nbsp;&nbsp;Vea la sección “Tecnologías de desarrollo quitadas de Exchange” para obtener más información acerca de las características de API y desarrollo suspendidas en Exchange&nbsp;2013.</P></LI></UL>



## Características discontinuadas de Exchange 2010 a Exchange 2013

Esta sección incluye las características de Exchange Server 2010 que ya no están disponibles en Exchange 2013.

## Arquitectura


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Rol del servidor Transporte de concentradores</p></td>
<td><p>El rol de servidor Transporte de concentradores ha sido reemplazado por los servicios de transporte que se ejecutan en los roles de servidor Buzón de correo y Acceso de cliente. El rol de servidor Buzón de correo incluye los servicios Transporte de Microsoft Exchange, Entrega de transporte de buzones de Microsoft Exchange y Envío de transporte de buzones de Microsoft Exchange. El rol de servidor Acceso de cliente incluye el servicio Transporte front-end de Microsoft Exchange. Para obtener más información, vea <a href="mail-flow-exchange-2013-help.md">Flujo de correo</a>.</p></td>
</tr>
<tr class="even">
<td><p>Rol del servidor Mensajería unificada</p></td>
<td><p>El rol de servidor Mensajería unificada ha sido reemplazado por los servicios de mensajería unificada que se ejecutan en los roles de servidor Buzón de correo y Acceso de cliente. El rol de servidor Buzón de correo incluye el servicio de mensajería unificada de Microsoft Exchange y el rol de servidor Acceso de cliente incluye el servicio Enrutador de llamadas de mensajería unificada de Microsoft Exchange. Para obtener más información, vea <a href="voice-architecture-changes-exchange-2013-help.md">Cambios en la arquitectura de voz</a>.</p></td>
</tr>
</tbody>
</table>


## Interfaces de administración


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Consola de administración de Exchange y Panel de control de Exchange</p></td>
<td><p>El Centro de administración de Exchange (EAC) ha sustituido a la Consola de administración de Exchange y al Panel de control de Exchange. EAC usa el mismo directorio virtual (/ecp) que el Panel de control de Exchange. Para obtener más información, vea <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Centro de administración de Exchange en Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


## Acceso de cliente


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2003 no es compatible</p></td>
<td><p>Para conectar Microsoft Outlook a Exchange 2013, es necesario el uso del servicio de detección automática. Sin embargo, Microsoft Outlook 2003 no es compatible con el uso del servicio de detección automática.</p></td>
</tr>
<tr class="even">
<td><p>Acceso RPC/TCP para clientes de Outlook</p></td>
<td><p>En Exchange 2013, los clientes de Microsoft Outlook pueden conectarse utilizando Outlook en cualquier lugar (RPC/HTTP) o MAPI sobre HTTP en Exchange 2013 Service Pack 1 y Outlook 2013 Service Pack 1 y versiones posteriores. Si tiene clientes de Outlook en su organización, es necesario utilizar Outlook en cualquier lugar o MAPI sobre HTTP. Para más información, vea <a href="outlook-anywhere-exchange-2013-help.md">Outlook en cualquier lugar</a> y <a href="mapi-over-http-exchange-2013-help.md">MAPI sobre HTTP</a>.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App y Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Corrector ortográfico</p></td>
<td><p>Outlook Web App ya no incluye servicios de revisión ortográfica integrada. En su lugar, usa las características de revisión ortográfica de los exploradores web.</p></td>
</tr>
<tr class="even">
<td><p>Filtros personalizables</p></td>
<td><p>Outlook Web App ya no tiene vistas filtradas personalizables ni permite guardar vistas filtradas en Favoritos. Los filtros personalizables se han cambiado por filtros fijos que se pueden usar para ver todos los mensajes: los no leídos, los enviados al usuarios y los marcados.</p></td>
</tr>
<tr class="odd">
<td><p>Marcadores de mensaje</p></td>
<td><p>En Outlook Web App no existe la posibilidad de establecer una fecha personalizada en un indicador de mensaje. Puede usar Outlook para establecer fechas personalizadas.</p></td>
</tr>
<tr class="even">
<td><p>Lista de contactos de chat</p>
<p></p></td>
<td><p>La lista de contactos de chat que aparecía en la lista de carpetas en Outlook Web App para Exchange 2010 ya no está disponible.</p></td>
</tr>
<tr class="odd">
<td><p>Carpetas de búsqueda</p></td>
<td><p>La capacidad de los usuarios para usar carpetas de búsqueda no se encuentra disponible actualmente en Outlook Web App.</p></td>
</tr>
</tbody>
</table>


## Flujo de correo


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Conectores vinculados</p></td>
<td><p>Se ha quitado la capacidad de vincular un conector de envío a un conector de recepción. Específicamente, el parámetro <em>LinkedReceiveConnector</em> se ha quitado de <a href="https://technet.microsoft.com/es-es/library/aa998936(v=exchg.150)">New-SendConnector</a> y <a href="https://technet.microsoft.com/es-es/library/aa998294(v=exchg.150)">Set-SendConnector</a>.</p></td>
</tr>
</tbody>
</table>


## Antimalware y contra el correo no deseado


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración del agente contra correo electrónico no deseado en el EMC</p></td>
<td><p>En Exchange 2010, cuando habilita los agentes contra correo electrónico no deseado en un servidor de transporte de concentradores, podría administrar los agentes contra el correo electrónico no deseado en la Consola de administración de Exchange (EMC). En Exchange 2013, cuando habilita los agentes contra correo no deseado en un servidor de buzones de correo, no puede administrar los agentes con EAC. Solo puede usar el Shell. Para obtener información acerca de cómo habilitar los agentes contra correo electrónico no deseado en un servidor de buzones de correo, vea <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo</a>.</p></td>
</tr>
<tr class="even">
<td><p>Agente de filtrado de conexión en los servidores de transporte de concentradores</p></td>
<td><p>En Exchange 2010, cuando habilitaba los agentes contra correo electrónico no deseado en un servidor de transporte de concentradores, el agente de filtro de datos adjuntos era el único agente contra correo electrónico no deseado que no estaba disponible. En Exchange 2013, cuando habilita los agentes contra correo electrónico no deseado en un servidor de buzones de correo, el agente de filtrado de datos adjuntos y el agente de filtrado de conexión no están disponibles. El agente de filtrado de conexión proporciona capacidades de lista de direcciones IP permitidas y de lista de direcciones IP bloqueadas. Para obtener información acerca de cómo habilitar los agentes contra correo electrónico no deseado en un servidor de buzones de correo, vea <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo</a>.</p>

> [!NOTE]
> Los agentes contra correo no deseado no se pueden habilitar en un servidor de acceso de cliente de Exchange&nbsp;2013. Por lo tanto, la única forma de acceder al agente de filtrado de conexiones es instalar un servidor de transporte perimetral en la red perimetral. Para obtener más información, vea <A href="edge-transport-servers-exchange-2013-help.md">Servidores de transporte perimetral</A>.


</td>
</tr>
</tbody>
</table>


## Directiva de mensajería y conformidad


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carpetas administradas</p></td>
<td><p>En Exchange 2010, utilice las carpetas administradas para la administración de la retención de mensajería (MRM). En Exchange 2013, las carpetas administradas no son compatibles. Debe utilizar las directivas de retención para MRM.</p>

> [!NOTE]
> Los Cmdlets relacionados con carpetas administradas están todavía disponibles. Se pueden crear carpetas administradas, configuraciones de administración de contenido, directivas para las carpetas administradas del buzón de correo, y aplicar una directiva para las carpetas administradas del buzón para un usuario, pero el asistente de MRM saltea el procesamiento de los buzones a los que se les aplicó una directiva para las carpetas administradas del buzón.


</td>
</tr>
<tr class="even">
<td><p>Asistente para trasladar carpetas administradas</p></td>
<td><p>En Exchange 2010, usa el Asistente para trasladar carpetas administradas para crear etiquetas de retención basadas en la carpeta administrada y en la configuración de contenido gestionado. En Exchange 2013, el Centro de administración de Exchange no incluye esta función. Puede usar el cmdlet <strong>New-RetentionPolicyTag</strong> con el parámetro <em>ManagedFolderToUpgrade</em> para crear una etiqueta de retención basada en una carpeta administrada.</p></td>
</tr>
</tbody>
</table>


## Mensajería unificada y correo de voz


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Búsquedas en directorios con el Reconocimiento de voz automático (ASR)</p></td>
<td><p>En Exchange 2010, los usuarios de Outlook Voice Access pueden usar entradas de voz a través del Reconocimiento de voz automático (ASR) para buscar usuarios que estén en el directorio. Las entradas de voz también pueden usarse en Outlook Voice Access para desplazarse por menús, mensajes y otras opciones. No obstante, incluso si un usuario de Outlook Voice Access puede usar entradas de voz, tienen que usar el teclado numérico del teléfono para especificar su PIN y navegar por las opciones personales.</p>
<p>En Exchange 2013, los usuarios de Outlook Voice Access autenticados y sin autenticar no pueden buscar usuarios en el directorio con entradas de voz o ASR en ningún idioma. No obstante, las personas que realizan llamadas a un operador automático pueden usar entradas de voz en varios idiomas para desplazarse por los menús de operadores automáticos en el directorio.</p></td>
</tr>
</tbody>
</table>


## Herramientas


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practice Analyzer</p></td>
<td><p>En Exchange 2010, Exchange Best Practice Analyzer examinó su implementación de Exchange y determinó si la configuración estaba en línea con las prácticas recomendadas de Microsoft. En Exchange 2013, Exchange Best Practice Analyzer se reemplazó por <a href="https://go.microsoft.com/fwlink/p/?linkid=391077">Office 365 Best Practices Analyzer para Exchange Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Solucionador de problemas del flujo de correo</p></td>
<td><p>En Exchange 2010, el solucionador de problemas del flujo de correo le asistía en la solución de problemas del flujo de correo más habituales. En Exchange 2013, el solucionador de problemas de flujo de correo se ha retirado. Ahora puede usar la característica de seguimiento de mensajes en EAC en Exchange 2013. Para obtener más información, vea <a href="track-messages-with-delivery-reports-exchange-2013-help.md">Seguimiento de mensajes con informes de entrega</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Monitor de rendimiento</p></td>
<td><p>En Exchange 2010, el monitor de rendimiento se incluyo en el cuadro de herramientas de Exchange para permitirle recopilar información acerca del rendimiento del sistema de mensajería. El monitor de rendimiento se usa normalmente para visualizar los parámetros clave mientras se solucionan problemas de rendimiento. En Exchange 2013, el monitor de rendimiento se ha retirado del cuadro de herramientas. Todavía puede encontrar el monitor de rendimiento en <strong>Herramientas administrativas</strong> en Windows Server 2008.</p></td>
</tr>
<tr class="even">
<td><p>Solucionador de problemas de rendimiento</p></td>
<td><p>En Exchange 2013, el solucionador de problemas de rendimiento se ha retirado.</p></td>
</tr>
<tr class="odd">
<td><p>Visor de registro de enrutamiento</p></td>
<td><p>En Exchange 2013, el Visor de registro de enrutamiento se ha retirado.</p></td>
</tr>
</tbody>
</table>


## Copias de bases de datos de buzones


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Update-MailboxDatabaseCopy</p></li>
<li><p>Asistente de actualización de copia de base de datos de buzones</p></li>
</ul></td>
<td><p>Ya no es posible la propagación del catálogo de índice de contenido a través de la red de replicación. Solo puede hacerse a través de una red MAPI. Esto ocurre aunque use el parámetro <code>-Network</code> en el cmdlet Update-MailboxDatabaseCopy.</p></td>
</tr>
</tbody>
</table>


## Características discontinuadas de Exchange 2010 a Exchange 2007

Esta sección incluye las características de Exchange Server 2007 que ya no están disponibles en Exchange 2013.

## Las API y el desarrollo


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WebDAV de Exchange</p></td>
<td><p>Use <a href="https://go.microsoft.com/fwlink/p/?linkid=167197">Servicios web de Exchange</a> o <a href="https://go.microsoft.com/fwlink/p/?linkid=157179">API administrada por EWS</a>. También puede mantener un servidor Exchange 2007 para los buzones de correo administrados por aplicaciones que usan WebDAV. Para obtener más información, vea <a href="https://go.microsoft.com/fwlink/p/?linkid=169474">Migración desde WebDAV</a>.</p></td>
</tr>
</tbody>
</table>


## Arquitectura


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Grupos de almacenamiento</p></td>
<td><p>Exchange 2013 ya no usa la construcción de grupos de almacenamiento y, en su lugar, simplemente se administran bases de datos de buzones de correo. Para obtener más información, vea <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Administrar bases de datos de buzones en Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>API de copia de seguridad de transmisión por secuencias de motor de almacenamiento extensible (ESE)</p></td>
<td><p>Exchange 2013 solo admite copias de seguridad basadas en el Servicio de instantáneas de volumen (VSS) con Exchange. Exchange 2013 incluye un complemento para Copias de seguridad de Windows Server, que permite realizar copias de seguridad de los datos y restaurarlos. Para obtener información, vea <a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">Copia de seguridad, restauración y recuperación ante desastres</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Notificaciones del protocolo de datagramas de usuario (UDP)</p></td>
<td><p>La compatibilidad para notificaciones del Protocolo de datagramas de usuario (UDP) se ha quitado de Exchange 2013. Esto afecta a la experiencia de usuario cuando los clientes de Outlook 2003 se conectan a sus buzones en un servidor de Exchange 2013. Para más información, vea el artículo de Microsoft Knowledge Base 2009942, <a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2009942">Las carpetas tardan mucho en actualizarse cuando un usuario de Exchange Server 2010 utiliza Outlook 2003 en modo en línea</a>.</p></td>
</tr>
</tbody>
</table>


## Alta disponibilidad


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Replicación continua en clúster (CCR)</p></td>
<td><p>Exchange 2013 usa los grupos de disponibilidad de base de datos (DAGs) y copias de base de datos de buzones de correo. Para obtener información, vea <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidad y resistencia de sitios</a>.</p></td>
</tr>
<tr class="even">
<td><p>Replicación continua local (LCR)</p></td>
<td><p>Exchange 2013 usa DAGs y copias de base de datos de buzones de correo. Para obtener información, vea <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidad y resistencia de sitios</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Réplica continua en espera (SCR)</p></td>
<td><p>Exchange 2013 usa DAGs y copias de base de datos de buzones de correo. Para obtener información, vea <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidad y resistencia de sitios</a>.</p></td>
</tr>
<tr class="even">
<td><p>Clúster de copia única (SCC)</p></td>
<td><p>Exchange 2013 usa DAGs y copias de base de datos de buzones de correo. Para obtener información, vea <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidad y resistencia de sitios</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Setup /recoverCMS</p></td>
<td><p>Exchange 2013 usa Setup /m:recoverServer. Para obtener información, vea <a href="recover-an-exchange-server-exchange-2013-help.md">Recuperar un servidor de Exchange</a>.</p></td>
</tr>
<tr class="even">
<td><p>Servidor de buzones de correo en clústeres</p></td>
<td><p>Exchange 2013 usa DAGs y copias de base de datos de buzones de correo. Para obtener información, vea <a href="high-availability-and-site-resilience-exchange-2013-help.md">Alta disponibilidad y resistencia de sitios</a>.</p></td>
</tr>
</tbody>
</table>


## Acceso de cliente


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autenticación de cliente mediante autenticación integrada de Windows (NTLM) para los usuarios de POP3 e IMAP4</p></td>
<td><p>NTLM no es compatible con la conectividad de cliente POP3 ni IMAP4 en Exchange 2013. Se producirá un error en las conexiones de programas cliente POP3 o IMAP4 mediante NTLM. Si ejecuta la versión RTM de Exchange 2013, la alternativa recomendada a NTLM es usar Autenticación de texto sin formato con SSL.</p>
<p>Si usa Exchange 2013, para usar NTLM, debe conservar un servidor de Exchange 2007 en la organización de Exchange 2013.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App y Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acceso a documentos</p></td>
<td><p>Outlook Web App no se puede usar para acceder a las bibliotecas de documentos Microsoft SharePoint y al uso compartido de archivos de Windows.</p></td>
</tr>
<tr class="even">
<td><p>Marcadores de mensaje</p></td>
<td><p>La capacidad de establecer una fecha personalizada en un indicador de mensaje no está disponible en Outlook Web App 2013. Puede usar Outlook para establecer fechas personalizadas.</p></td>
</tr>
<tr class="odd">
<td><p>Corrector ortográfico</p></td>
<td><p>Outlook Web App usa las características de revisión ortográfica del explorador web.</p></td>
</tr>
<tr class="even">
<td><p>Carpetas de búsqueda</p></td>
<td><p>La capacidad de los usuarios para usar carpetas de búsqueda no se encuentra disponible actualmente en Outlook Web App.</p></td>
</tr>
<tr class="odd">
<td><p>Vistas máximas en caché</p></td>
<td><p>Exchange 2007 admitía modificar el número máximo del parámetro (msExchMaxCachedViews) de vistas almacenadas en caché por base de datos para los clientes de Outlook. Exchange 2013 ya no usa este parámetro.</p></td>
</tr>
</tbody>
</table>


## Características relacionadas con los destinatarios


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cmdlets <strong>Export-Mailbox</strong> y <strong>Import-Mailbox</strong></p></td>
<td><p>En Exchange 2013, use las solicitudes de exportación o importación. Para obtener más información, vea <a href="mailbox-import-and-export-requests-exchange-2013-help.md">Solicitudes de importación y exportación de buzones</a>.</p></td>
</tr>
<tr class="even">
<td><p>Conjunto de cmdlets <strong>Move-Mailbox</strong></p></td>
<td><p>En Exchange 2013, use solicitudes de movimiento para mover buzones de correo. Para obtener información, vea <a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimientos de buzones de Exchange 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>ISInteg</p></td>
<td><p>En Exchange 2013, use <a href="https://technet.microsoft.com/es-es/library/ff625226(v=exchg.150)">New-MailboxRepairRequest</a>.</p></td>
</tr>
</tbody>
</table>


## Directiva de mensajería y conformidad


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carpetas administradas</p></td>
<td><p>En Exchange 2007, utilice las carpetas administradas para la administración de la retención de mensajería (MRM). En Exchange 2013, las carpetas administradas no son compatibles. Debe utilizar las directivas de retención para MRM.</p>

> [!NOTE]
> Los Cmdlets relacionados con carpetas administradas están todavía disponibles. Se pueden crear carpetas administradas, configuraciones de administración de contenido, directivas para las carpetas administradas del buzón de correo, y aplicar una directiva para las carpetas administradas del buzón para un usuario, pero el asistente de MRM saltea el procesamiento de los buzones a los que se les aplicó una directiva para las carpetas administradas del buzón.


</td>
</tr>
</tbody>
</table>


## Mensajería unificada y correo de voz


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Comentarios y mitigación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Búsquedas en directorios con el Reconocimiento de voz automático (ASR) para Outlook Voice Access</p></td>
<td><p>En Exchange 2007, los usuarios de Outlook Voice Access pueden usar entradas de voz a través del Reconocimiento de voz automático (ASR) en inglés de Estados Unidos (en-US) para buscar usuarios que estén en el directorio. Las entradas de voz también pueden usarse en Outlook Voice Access para desplazarse por menús, mensajes y otras opciones. No obstante, incluso si un usuario de Outlook Voice Access puede usar entradas de voz, tienen que usar el teclado numérico del teléfono para especificar su PIN y navegar por las opciones personales.</p>
<p>En Exchange 2013, los usuarios de Outlook Voice Access autenticados y sin autenticar no pueden buscar usuarios en el directorio con entradas de voz o ASR en ningún idioma. No obstante, las personas que realizan llamadas a un operador automático pueden usar entradas de voz en varios idiomas para desplazarse por los menús de operadores automáticos en el directorio.</p></td>
</tr>
</tbody>
</table>

