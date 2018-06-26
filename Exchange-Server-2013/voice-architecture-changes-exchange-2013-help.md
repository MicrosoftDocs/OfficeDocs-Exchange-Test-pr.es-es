---
title: 'Cambios en la arquitectura de voz: Exchange 2013 Help'
TOCTitle: Cambios en la arquitectura de voz
ms:assetid: 55d5ca4a-b0cd-45f1-9f47-e745ef208698
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150516(v=EXCHG.150)
ms:contentKeyID: 48268136
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cambios en la arquitectura de voz

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2015-03-09_

La arquitectura de Microsoft Exchange Server 2013 es diferente a la de Exchange Server 2007 y Exchange Server 2010. En Exchange 2007 y en Exchange 2010, los tipos de servidor se dividían en varios roles de servidor: acceso de clientes, buzones, transporte de concentradores y mensajería unificada. En Exchange 2013, todos los roles de servidor se combinan para formar dos tipos de servidor, y todos los componentes o servicios de dichos roles de servidor se ejecutan en el mismo servidor físico o en dos servidores separados denominados acceso de clientes y buzones de correo. En el nuevo modelo, el servidor de acceso de clientes que ejecuta el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange redirige el tráfico del protocolo de inicio de sesión (SIP) que se genera de una llamada entrante a un servidor de buzones. A continuación, se establece un canal de medios (protocolo de transporte en tiempo real (RTP) o RTP seguro (SRTP)) desde la puerta de enlace VoIP o la central de conmutación (PBX) IP hasta el servidor de buzones que hospeda el buzón del usuario. En Exchange 2013, el servidor de buzones tiene los mismos procesos que el rol de servidor Mensajería unificada en Exchange 2007 y en Exchange 2010. El servidor de buzones ejecuta el servicio de mensajería unificada de Microsoft Exchange y los procesos de trabajo de mensajería unificada. El servidor de acceso de clientes ejecuta el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange, que recibe una llamada entrante y la reenvía al servidor de buzones.

**Contenido**

Soporte para la nueva arquitectura de Exchange

Puertos de mensajería unificada

Planes de marcado de mensajería unificada

Contadores de rendimiento del enrutador de llamadas de mensajería unificada

## Soporte para la nueva arquitectura de Exchange

En Exchange 2013, el servidor de acceso de clientes es responsable de la detección automática, la capa de sockets seguros (SSL), la autenticación, la redirección y el proxy. El servidor de acceso de clientes representa el punto de entrada para las llamadas entrantes o solicitudes SIP para la mensajería unificada (UM). La lógica de enrutamiento y SIP REDIRECT se implementan como un servicio que se incluye de forma automática en un servidor de acceso de clientes. Este servicio se conoce como Enrutador de llamadas de mensajería unificada de Microsoft Exchange. Se instala y se ejecuta en todos los servidores de acceso de clientes de la organización. Cuando un servidor de acceso de clientes recibe un SIP INVITE para una llamada entrante, el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange redirige la llamada entrante al servidor de buzones. Después, se crea un canal de medios (RTP o SRTP) entre la puerta de enlace VoIP, la PBX IP o el controlador de borde de sesión (SBC) y el servidor de buzones. Aunque el servidor de acceso de clientes actúa como un redirector SIP, solo administra las solicitudes SIP de puertas de enlace VoIP, PBX IP o SBC. No recibe tráfico de medios. El tráfico de medios que usa RTP o SRTP solo se pasa entre el servidor de buzones y los sistemas SIP del mismo nivel, como puertas de enlace VoIP, PBX IP o SBC, y no al servidor de acceso de clientes. Al implementar Exchange 2013 y la mensajería unificada, es necesario configurar las puertas de enlace VoIP, la PBX IP o los SBC para que apunten a los servidores de acceso de clientes que instaló a fin de que las llamadas entrantes se enruten correctamente para la mensajería unificada.

En algunos casos, es necesario implementar varios servidores de acceso de clientes, que se deben implementar de manera independiente en hardware físico diferente de los servidores de buzones. Los servidores de acceso de clientes pueden agruparse en una matriz al usar un equilibrador de carga de software o hardware L4 o L5. Sin embargo, no hay ninguna matriz de servidores de acceso de clientes basada en objetos de Active Directory Exchange. En implementaciones grandes de Exchange se puede usar un equilibrador de carga de hardware o software con servidores de acceso de clientes.

Cuando se instala un servidor Acceso cliente, se ejecuta el servicio Enrutador de llamada de mensajería unificada de Microsoft Exchange. El servicio hace lo siguiente:

  - Cuando se inicializa, lee un archivo de configuración local llamado msexchangeumcallrouter.config.

  - Se realiza la generación de las gramáticas de voz mediante un buzón de arbitraje para una organización.

  - Admite conexiones del Protocolo de control de transmisión (TCP) o de Seguridad de la capa de transporte (TLS). Este valor se puede configurar.

  - Solo se detendrá si existe un error de configuración o si no se pueden registrar los puertos requeridos.

En Exchange 2013, el servidor de buzones no es el responsable de responder a las solicitudes SIP de las llamadas entrantes. Solo se encarga de recibir el tráfico SIP de un servidor de acceso de clientes y, a continuación, de establecer una conexión RTP o SRTP a la puerta de enlace VoIP, PBX IP o SBC.

Después de que un servidor de acceso de clientes redirija una llamada entrante a un servidor de buzones, se establece un canal de medios entre la puerta de enlace VoIP, la PBX IP o el SBC y el servidor de buzones. Una vez establecido el canal de medios, el servicio de mensajería unificada de Microsoft Exchange del servidor de buzones reproduce el saludo del correo de voz del usuario, se procesan las reglas de contestador automático para el usuario y se invita al autor de la llamada a dejar un mensaje de voz. Después, el servidor de buzones registra el mensaje de voz, crea una transcripción de este y lo deposita en el buzón de correo del usuario. No obstante, si va a integrar Exchange con Office Communications Server 2007 R2 o Lync Server, los servidores Lync y el servidor de buzones administran tanto el SIP como los canales de medios RTP y SRTP para las llamadas entrantes. En un entorno integrado con Lync no hay puertas de enlace VoIP, PBX IP ni SBC. Para Lync, el servidor de buzones que se ejecuta en el servicio de mensajería unificada de Microsoft Exchange actúa como un servidor de mensajería unificada de Exchange 2010. El servidor de buzones y el servidor de acceso de clientes que ejecutan el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange se consideran sistemas del mismo nivel de confianza porque ambos servidores se deben agregar a un plan de marcado SIP. Lync enruta la llamada entrante mediante el componente de enrutamiento de entrada, que usa SIP para comunicarse con el servidor de acceso de clientes y, a continuación, enruta la llamada a un servidor de buzones.

Los administradores de mensajería unificada de Exchange 2010 pueden configurar un conjunto de propiedades para mensajería unificada en cada servidor de mensajería unificada. En Exchange 2013, los componentes y los valores de configuración de mensajería unificada se encuentran en los servidores de buzones y de acceso de clientes. Los valores de configuración que se aplican a un solo equipo que ejecute el rol de servidor Mensajería unificada en Exchange 2010 aún estarán disponibles. No obstante, algunos de esos valores de propiedades y de configuración se establecen en un servidor de acceso de clientes que ejecute el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange, y otros estarán disponibles en un servidor de buzones que ejecute el servicio de mensajería unificada de Microsoft Exchange. En algunos casos, la misma configuración está disponible en ambos. En la siguiente lista, se muestran los cmdlets y los parámetros que están disponibles en los servidores de acceso de cliente y de buzones y donde se hicieron cambios a un cmdlet para admitir escenarios de implementación con versiones anteriores de mensajería unificada.

  - **Set-UMService -DialPlans \<MultiValuedProperty\>**    Disponible en servidores de buzones de Exchange 2013. También funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMCallRouterSettings -DialPlans \<MultiValuedProperty\>**    Disponible en servidores de acceso de cliente de Exchange 2013, pero no disponible para los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMService -MaxCallsAllowed \<Int32\>**    Disponible en servidores de buzones de Exchange 2013. También funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMCallRouterSettings -MaxCallsAllowed \<Int32\>**   No disponible en servidores de acceso de cliente de Exchange 2013 ni para los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMService -SipTcpListeningPort \<Int32\>**    No se puede configurar en servidores de buzones de Exchange 2013, pero funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMService -SipTlsListeningPort \<Int32\>**   No se puede configurar en servidores de buzones de Exchange 2013, pero funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMCallRouterSettings -SipTcpListeningPort \<Int32\>**    Disponible en servidores de acceso de cliente de Exchange 2013, pero no funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMCallRouterSettings -SipTlsListeningPort \<Int32\>**   Disponible en servidores de acceso de cliente de Exchange 2013, pero no funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMService - Status \<Enabled | Disabled | NoNewCalls\>**   No disponible en servidores de buzones de Exchange 2013, pero funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMCallRouterSettings - Status \<Enabled | Disabled | NoNewCalls\>**    No disponible en servidores de cliente de acceso de Exchange 2013, y no funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMService -UMStartupMode \<TCP | TLS | Dual\>**   Disponible en servidores de buzones de Exchange 2013, funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Set-UMCallRouterSettings - UMStartupMode \<TCP | TLS | Dual\>**    Disponible en servidores de acceso de cliente de Exchange 2013, pero no funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Enable-UMService**    No disponible en servidores de buzones de Exchange 2013, pero funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

  - **Disable-UMService**    No disponible en servidores de buzones de Exchange 2013, pero funciona en los servidores de mensajería unificada de Exchange 2007 y Exchange 2010.

En los servidores de buzones, se usan los cmdlets **Set/Get/Enable/Disable-UMService** para ver o configurar las propiedades de MU del servicio de mensajería unificada de Microsoft Exchange en los servidores de buzones de Exchange 2013 o en los servidores de mensajería unificada de Exchange 2010 o Exchange 2007. Para ver y configurar las propiedades del servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange en un servidor de acceso de clientes se usa un conjunto distinto de cmdlets, como **Set/Get-UMCallRouterSettings**. Esto garantiza que los cmdlets **Get-UMServer**, **Set-UMServer**, **Enable-UMServer** y **Disable-UMServer** existentes de Exchange 2007 y de Exchange 2010 funcionen en una implementación de coexistencia con los servidores de buzones de Exchange 2013. Asimismo, se garantiza que los cmdlets funcionen cuando los servidores de buzones y de acceso de clientes se instalen en el mismo servidor o en servidores distintos.

Soporte para la nueva arquitectura de Exchange

## Puertos de mensajería unificada

El servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange de un servidor de acceso de clientes usa SIP sobre el Protocolo de control de transmisión (TCP) o la Seguridad de la capa de transporte mutua (Mutual TLS) para comunicarse con servidores de buzones que ejecuten el servicio de mensajería unificada de Microsoft Exchange. Para evitar conflictos entre puertos TCP o del Protocolo de datagramas de usuario (UDP), el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange y el servicio de mensajería unificada de Microsoft Exchange usan distintos puertos TCP de manera predeterminada y escuchan en ellos. Aceptan conexiones seguras y no seguras, en función de si se usa Mutual TLS con el tráfico RTP y SIP. De forma predeterminada, un servidor de acceso de clientes escucha las solicitudes SIP en el puerto TCP 5060 en modo no seguro y en el puerto TCP 5061 en modo seguro SIP cuando se usa Mutual TLS. Estos puertos se pueden configurar mediante el cmdlet **Set-UMCallRouterSettings**. El servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange en el servidor de acceso de clientes no administra el tráfico de medios (RTP o SRTP), por lo tanto se usan solamente los puertos TCP y no se usan los puertos UDP. De forma predeterminada, un servidor de buzones escucha las solicitudes SIP en el puerto TCP 5062 en modo no seguro y en el puerto TCP 5063 en modo seguro SIP cuando se usa Mutual TLS. Estos puertos no se pueden configurar mediante los cmdlets del Shell de administración de Exchange. En el servidor de buzones que ejecuta el servicio de mensajería unificada de Microsoft Exchange, los puertos TCP no se pueden configurar en el servidor Exchange mediante el Shell ni mediante la configuración de los valores en el registro. El servicio de mensajería unificada de Microsoft Exchange en el servidor de buzones acepta conexiones de un servidor de acceso de clientes en los puertos SIP 5062 y 5063. Una vez que el servidor de acceso de clientes redirige la solicitud SIP a un servidor de buzones, se crea un canal de medios RTP o SRTP mediante una puerta de enlace VoIP, PBX IP o SBC, y el proceso de trabajo de mensajería unificada de Microsoft Exchange en el servidor de buzones.

En la siguiente tabla se resumen los puertos y protocolos de Exchange 2013, y si dichos puertos se pueden cambiar.

### Puertos de escucha de mensajería unificada

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocolo</th>
<th>Puerto TCP</th>
<th>Puerto UDP</th>
<th>¿Se pueden cambiar los puertos?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP (servidor Acceso de cliente; servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange)</p></td>
<td><p>5060 (no protegido), 5061 (protegido). El servicio escucha en ambos puertos.</p></td>
<td><p>No aplicable</p></td>
<td><p>Si, mediante el cmdlet <strong>Set-UMCallRouterSettings</strong>.</p></td>
</tr>
<tr class="even">
<td><p>SIP (servidor Buzón de correo; servicio de mensajería unificada de Microsoft Exchange)</p></td>
<td><p>5062 (no protegido), 5063 (protegido). El servicio escucha en ambos puertos.</p></td>
<td><p>No aplicable</p></td>
<td><p>No se pueden cambiar los puertos.</p></td>
</tr>
<tr class="odd">
<td><p>SIP (servidor Buzón de correo; proceso de trabajador de MU)</p></td>
<td><p>5065 y 5067 para TCP (no protegidos). 5066 y 5068 para TLS mutua (protegidos). Esto sucede cuando <em>UMStartupMode</em> se establece en <em>Dual</em>. Si <em>UMStartUpMode</em> se establece en <em>TCP</em> o <em>TLS</em>, se usan los puertos 5065 y 5066. El valor predeterminado de <em>UMStartupMode</em> es <em>TCP</em>.</p></td>
<td><p>No aplicable</p></td>
<td><p>No se pueden cambiar los puertos.</p></td>
</tr>
<tr class="even">
<td><p>RTP (servidor Buzón de correo; proceso de trabajador de MU)</p></td>
<td><p>No aplicable</p></td>
<td><p>Puertos entre 1024 y 65535.</p></td>
<td><p>El intervalo de puertos puede cambiarse mediante el registro; sin embargo, no es una configuración admitida:</p>
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMinPort</p>
<p>HKLM\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMaxPort</p></td>
</tr>
</tbody>
</table>


Soporte para la nueva arquitectura de Exchange

## Planes de marcado de mensajería unificada

No es necesario asignar ni asociar planes de marcado de mensajería unificada a servidores de mensajería unificada en Exchange 2013 del modo en que se requería en Exchange 2007 o en Exchange 2010. Los servidores de buzones y de acceso de clientes que ejecutan servicios de mensajería unificada no se tienen que vincular a ningún plan de marcado porque se espera que reciban las llamadas entrantes de las puertas de enlace VoIP, PBX IP o SBC. La excepción es que si los planes de marcado SIP se usan con Lync 2013, Lync Server 2010 y Office Communications Server 2007 R2 se deben asociar a servidores de buzones y de acceso de clientes que haya implementado. Ambos tipos de servidores de Exchange se deben agregar a cada plan de marcado SIP para incluirse como sistemas del mismo nivel de confianza desde Communications Server 2007 R2 o Lync Server. De lo contrario, Communications Server 2007 R2 y Lync Server rechazarán las llamadas salientes de los usuarios.

En la siguiente tabla se resume la relación entre los servidores de buzones y de acceso de clientes y los planes de marcado de mensajería unificada.

### Vinculación de planes de marcado de mensajería unificada

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topología</th>
<th>Plan de marcado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de buzones o de acceso de clientes en el mismo servidor (sin planes de marcado no habilitados para SIP de Communications Server 2007 R2 o Lync Server 2010)</p></td>
<td><p>Para asociarse con un servidor Acceso de cliente o Buzón de correo ya no se requieren planes de marcado. No podrá agregar servidores de buzones o de acceso de clientes a un plan de marcado. Si ejecuta el cmdlet <strong>Set-UMService</strong>, se generará un error si trata de asociar un servidor de buzones a un plan de marcado no habilitado para SIP.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de buzones o de acceso de clientes en servidores diferentes (sin planes de marcado no habilitados para SIP de Communications Server 2007 R2 o Lync Server 2010)</p></td>
<td><p>Para asociarse a un servidor de acceso de clientes o de buzones ya no se requieren planes de marcado. No podrá agregar servidores de buzones ni de acceso de clientes a un plan de marcado. Si ejecuta el cmdlet <strong>Set-UMService</strong>, se generará un error si trata de asociar un servidor de buzones a un plan de marcado no habilitado para SIP.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de buzones o de acceso de clientes en el mismo servidor físico (con Communications Server 2007 R2 o Lync Server 2010 con planes de marcado SIP)</p></td>
<td><p>Para un plan de marcado SIP individual, agregue todos los servidores de acceso de cliente y de buzones al plan de marcado SIP. Para varios planes de marcado SIP, agregue todos los servidores de acceso de cliente y de buzones a cada plan de marcado SIP. Esto hará que ambos servidores sean un par de confianza de Office Communications Server 2007 R2 o Lync Server. Debe usar el mismo certificado en la implementación de Office Communications Server 2007 R2 o Lync Server que en los servidores de buzones o de acceso de clientes.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de buzones o de acceso de clientes en servidores físicos distintos (con Communications Server 2007 R2 o Lync Server 2010 con planes de marcado SIP)</p></td>
<td><p>Para un plan de marcado SIP individual, agregue todos los servidores de acceso de cliente y de buzones al plan de marcado SIP. Para varios planes de marcado SIP, agregue todos los servidores de acceso de cliente y de buzones a cada plan de marcado SIP. Esto hará que ambos servidores sean un par de confianza de Office Communications Server 2007 R2 o Lync Server. Si los certificados que se usan en los servidores de buzones o de acceso de clientes son distintos, debe usar el mismo certificado en la implementación de Office Communications Server 2007 R2 o Lync Server que en los servidores de buzones o de acceso de clientes de la organización.</p></td>
</tr>
</tbody>
</table>


Soporte para la nueva arquitectura de Exchange

## Contadores de rendimiento del enrutador de llamadas de mensajería unificada

Las versiones anteriores de Exchange incluían el rol de servidor Mensajería unificada, que ejecutaba el servicio de mensajería unificada de Microsoft Exchange. Debido a los cambios en la arquitectura de Exchange 2013, el servidor de acceso de cliente ejecuta el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange y el servidor de buzones ejecuta el servicio de mensajería unificada de Microsoft Exchange. Los administradores pueden utilizar los mismos contadores de rendimiento para el servicio de mensajería unificada de Microsoft Exchange que en versiones anteriores de la mensajería unificada de Exchange. No obstante, también existen algunos contadores de rendimiento adicionales que puede usar en el servidor de acceso de cliente para comprobar el estado del servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange y para solucionar problemas.

Ahora están disponibles los siguientes contadores de rendimiento para admitir el nuevo servicio del enrutador de llamadas de mensajería unificada de acceso de clientes en Exchange 2013.

### Contadores de rendimiento

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Categoría de contador de rendimiento</th>
<th>Nombre del contador</th>
<th>Descripción</th>
<th>Umbral</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Porcentaje de llamadas entrantes rechazadas por el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange durante la última hora</p></td>
<td><p>Muestra el porcentaje de llamadas entrantes rechazadas por el servicio de mensajería unificada de Microsoft Exchange durante la última hora.</p></td>
<td><p>Siempre debe ser inferior al 5 por ciento, aunque debería ser 0 en todo momento.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Llamadas desconectadas en un error interno irrecuperable para el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange</p></td>
<td><p>Muestra el número de llamadas desconectado después de que se produjo un error interno del sistema.</p></td>
<td><p>Debe ser 0 en todo momento.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Total de llamadas entrantes rechazadas por el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange</p></td>
<td><p>Muestra el número total de llamadas entrantes rechazadas por el servicio Enrutador de llamada de mensajería unificada de Microsoft Exchange desde que se inició el servicio.</p></td>
<td><p>Debe ser 0 en todo momento.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Total de llamadas recibidas por el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange</p></td>
<td><p>Muestra el número total de llamadas entrantes recibidas por el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange desde que se inició el servicio.</p></td>
<td><p>Debe tener el valor de 0 o superior.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Porcentaje de llamadas entrantes rechazadas por el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange durante la última hora</p></td>
<td><p>Muestra el porcentaje de llamadas entrantes rechazadas por el servicio de mensajería unificada de Microsoft Exchange durante la última hora.</p></td>
<td><p>Debe ser inferior al 5 por ciento.</p></td>
</tr>
</tbody>
</table>


Soporte para la nueva arquitectura de Exchange

