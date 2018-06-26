---
title: 'Redundancia de instantánea: Exchange 2013 Help'
TOCTitle: Redundancia de instantánea
ms:assetid: a40dbe61-2a18-48a8-b2e0-4e81a6678d11
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351027(v=EXCHG.150)
ms:contentKeyID: 49895810
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Redundancia de instantánea

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

La redundancia de la instantánea fue introducida en Microsoft Exchange Server 2010 para proporcionar copias redundantes de mensajes antes de que se entreguen a los buzones de correo. En Exchange 2010, la redundancia de la instantánea retrasaba la eliminación de un mensaje desde la base de datos de transporte de un servidor de transporte hasta que el servidor había comprobado si el siguiente salto de la ruta de entrega del mensaje había completado la entrega. Si el salto siguiente dada error antes de notificar al servidor de transporte que había realizado satisfactoriamente la entrega, este reenviaba el mensaje al siguiente salto. Los servidores Exchange 2010 usaban el verbo XSHADOW para anunciar su soporte de redundancia de la instantánea. Si un servidor SMTP no admitía la redundancia de la instantánea, Exchange 2010 usaba el reconocimiento retrasado basándose en un intervalo de tiempo configurado en el conector de recepción para realizar una copia redundante del mensaje.

La principal mejora en la redundancia de la instantánea en Microsoft Exchange Server 2013 es que el servidor de transporte ahora realiza una copia redundante de cualquier mensaje que recibe antes de notificar la recepción satisfactoria del mismo al servidor de envío. No tiene transcendencia si el servidor de envío admite o no la redundancia de la instantánea. Esto ayuda a garantizar que todos los mensajes de la canalización de transporte de Exchange 2013 son redundantes mientras se encuentran en tránsito. Si Exchange 2013 establece que el mensaje original se ha perdido en tránsito, se entrega la copia redundante del mensaje.

**Contenido**

Componentes de la redundancia de instantánea

Requisitos para la redundancia de instantánea

Redundancia de instantánea está activado por defecto

¿Cómo se crean mensajes de instantánea?

Tiempos de espera de SMTP

¿Cómo se mantienen los mensajes de instantánea?

Procesamiento de mensajes después de una interrupción

## Componentes de la redundancia de instantánea

La tabla siguiente describe los componentes de redundancia de la instantánea. A lo largo de este tema se emplean los términos que se describen a continuación.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Término</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidor de transporte</p></td>
<td><p>Servidor de Exchange que tiene colas de mensajes y se encarga de enrutar mensajes. En Exchange 2013, un servidor de transporte es un servidor de buzón de correo (servicio de transporte del servidor de buzón de correo).</p></td>
</tr>
<tr class="even">
<td><p>Base de datos de transporte</p></td>
<td><p>La base de datos de cola de mensajes en un servidor de transporte Exchange 2013. Las colas de instantánea y la red de seguridad también se almacenan en la base de datos de transporte.</p></td>
</tr>
<tr class="odd">
<td><p>Límite de alta disponibilidad de transporte</p></td>
<td><p>Grupo de disponibilidad de bases de datos (DAG) en entornos DAG, o un sitio de Active Directory en entornos que no sean parte de un DAG. Cuando un mensaje llega en un servidor de transporte del límite de alta disponibilidad de transporte, Exchange intenta conservar 2 copias redundantes del mensaje en servidores de transporte dentro del límite. Cuando un mensaje abandona el límite de alta disponibilidad de transporte, Exchange deja de conservar copias del mensaje.</p></td>
</tr>
<tr class="even">
<td><p>Mensaje principal</p></td>
<td><p>El mensaje enviado en la canalización de transporte para la entrega.</p></td>
</tr>
<tr class="odd">
<td><p>Mensaje de instantánea</p></td>
<td><p>La copia redundante del mensaje que el servidor de instantáneas conserva hasta que confirma que el mensaje principal ha sido procesado con éxito por el servidor principal.</p></td>
</tr>
<tr class="even">
<td><p>Servidor principal</p></td>
<td><p>Servidor de transporte que actualmente procesa el mensaje principal.</p></td>
</tr>
<tr class="odd">
<td><p>Servidor de instantánea</p></td>
<td><p>El servidor de transporte que contiene el mensaje de instantánea para el servidor principal. Un servidor de transporte puede ser el servidor principal de algunos mensajes y el servidor de instantánea de otros mensajes de manera simultánea.</p></td>
</tr>
<tr class="even">
<td><p>Cola de instantáneas</p></td>
<td><p>La cola de entrega donde el servidor de instantánea almacena mensajes de instantánea. En mensajes con múltiples destinatarios, cada salto del mensaje principal necesita colas de instantáneas independientes.</p></td>
</tr>
<tr class="odd">
<td><p>Estado de descarte</p></td>
<td><p>La información que conserva un servidor de transporte para mensajes de instantánea que indican que el mensaje principal ha sido procesado con éxito.</p></td>
</tr>
<tr class="even">
<td><p>Notificación de descarte</p></td>
<td><p>Respuesta que un servidor de instantáneas recibe de un servidor principal y que indica que un mensaje de instantánea se puede descartar.</p></td>
</tr>
<tr class="odd">
<td><p>Red de seguridad</p></td>
<td><p>La versión mejorada del contenedor de transporte en Exchange 2013. Los mensajes que se procesan o se entregan satisfactoriamente a un destinatario de buzón de correo por parte del servicio de transporte en un servidor de buzón de correo se mueven a la red de seguridad. Para obtener más información, consulte <a href="safety-net-exchange-2013-help.md">Red de seguridad</a>.</p></td>
</tr>
<tr class="even">
<td><p>Administrador de redundancia de instantánea</p></td>
<td><p>Componente de transporte que administra la redundancia de instantánea.</p></td>
</tr>
<tr class="odd">
<td><p>Latido</p></td>
<td><p>Proceso por el cual los servidores principales y los servidores de instantáneas comprueban su disponibilidad entre sí.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Requisitos para la redundancia de instantánea

Aunque pueda parecer obvio, la redundancia de la instantánea requiere múltiples servidores de buzón de correo en Exchange 2013. El servidor de buzón de correo puede ser un servidor independiente, o servidores de buzón de correo y de acceso de clientes instalados en el mismo equipo.

  - Si el servidor del buzón de correo no es miembro de un DAG, los demás servidores de buzón de correo deben encontrarse en el sitio de Active Directory.

  - Si el servidor del buzón de correo es miembro de un DAG, los demás servidores del buzón de correo deben pertenecer al mismo DAG. El resto de servidores de buzón de correo que pertenecen al DAG pueden estar en el sitio local de Active Directory o en un sitio remoto de Active Directory. Si el DAG se extiende en varios sitios de Active Directory, la redundancia de la instantánea prefiere crear una copia redundante del mensaje en un sitio remoto de Active Directory para la resistencia del sitio.

Estas son las situaciones donde la redundancia de la instantánea no puede proteger mensajes en tránsito:

  - En entornos de servidor de Exchange solo.

  - En DAG infra aprovisionados.

  - Durante el error simultáneo de dos o más servidores de transporte que participan en la redundancia de la instantánea de un mensaje.

Volver al principio

## Redundancia de instantánea está activado por defecto

Por defecto, redundancia de instantánea está activado de manera global en el servicio de transporte de todos los buzones de correo usando el parámetro *ShadowRedundancyEnabled* en el cmdlet **Set-TransportConfig**. Por defecto, si el servicio de transporte de un servidor de buzón de correo no puede crear una copia redundante de un mensaje, el mensaje no se rechaza. No obstante, puede configurar Exchange 2013 para rechazar un mensaje si no se ha creado una copia redundante del mismo usando el parámetro *RejectMessageOnShadowFailure* en el cmdlet **Set-TransportConfig**. El mensaje se rechaza con un error transitorio, pero el servidor de envío puede volver a transmitir el mensaje. El código de respuesta SMTP es `451 4.4.0 Message failed to be made redundant.` Debe configurar Exchange 2013 para rechazar mensajes que no pueden ser redundantes solo cuando su organización tenga múltiples servidores de buzón de correo Exchange 2013 disponibles.

La tabla siguiente describe los parámetros que permiten redundancia de instantánea.

### Parámetros que permiten redundancia de instantánea

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowRedundancyEnabled</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> habilita la redundancia de instantáneas en todos los servidores de transporte de la organización.</p></li>
<li><p><code>$false</code> deshabilita la redundancia de instantáneas en todos los servidores de transporte de la organización.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RejectMessageOnShadowFailure</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$false</code></p></td>
<td><ul>
<li><p><code>$false</code>   Cuando no puede crearse una instantánea, los servidores de transporte de la organización aceptan el mensaje principal de todas maneras. Esos mensajes de forma redundante no persistieron mientras están en tránsito.</p></li>
<li><p><code>$true</code>   Los servidores de transporte de la organización no aceptan o notifican mensajes hasta que se cree una instantánea del mensaje de manera satisfactoria. En caso de no poder crear una instantánea del mensaje, el mensaje principal se rechaza con un error transitorio. Todos los mensajes de la organización se conservan de forma redundante mientras están en tránsito.</p>
<p>Debe cambiar este valor a <code>$true</code> solo si tiene varios servidores de buzón de correo Exchange 2013 en un DAG o sitio de Active Directory en el que pueda crearse una instantánea del mensaje.</p></li>
</ul>
<p>Este parámetro sólo tiene sentido cuando <em>ShadowRedundancyEnabled</em>es <code>$true</code>.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## ¿Cómo se crean mensajes de instantánea?

El objetivo principal de la redundancia de instantánea es disponer siempre de dos copias de un mensaje en el límite de alta disponibilidad de transporte mientras el mensaje se encuentra en tránsito. Cuándo y dónde se crea la copia redundante del mensaje depende de la procedencia y el destino del mensaje. Hay tres factores determinantes principales:

  - Mensajes recibidos desde fuera de un límite de alta disponibilidad de transporte.

  - Mensajes enviados fuera de un límite de alta disponibilidad de transporte.

  - Mensajes recibidos desde el servicio de envío de transporte de buzón de correo desde un servidor de correo en el límite de alta disponibilidad de transporte.

El *límite de alta disponibilidad de transporte* es uno de los siguientes:

  - Un DAG, para servidores de correo que son miembros de un DAG. Esto incluye un DAG que abarca múltiples sitios de Active Directory.

  - Un sitio de Active Directory, para servidores de buzón de correo que no pertenecen a un DAG.

Redundancia de instantánea nunca rastrea mensajes de instantánea a través de un límite de alta disponibilidad de transporte. Cuando un mensaje cruza el límite de alta disponibilidad de transporte, la redundancia de instantánea comienza o se reinicia. Esto reduce el tráfico de mantenimiento de mensajes de instantánea y evitar que se reenvíen mensajes de instantánea en los límites de alta disponibilidad de tráfico. Los servidores de transporte de concentradores de Exchange 2010 son un caso especial del que se hablará más adelante en este mismo tema.

## Mensajes recibidos desde fuera de un límite de alta disponibilidad de transporte

Cuando el servicio de transporte de un servidor de buzón de correo de Exchange 2013 recibe un mensaje externo al límite de alta disponibilidad de transporte, al servidor de buzón de correo no le interesa la compatibilidad o falta de compatibilidad de redundancia de instantánea en el servidor emisor. En la medida en que se habilite la redundancia de instantánea, el servidor de buzón de correo que recibe el mensaje realiza una instantánea del mensaje en otro servidor de buzón de correo en el límite de alta disponibilidad de tráfico antes de acusar recibo del mensaje al servidor emisor. Este es un ejemplo de cómo funciona el proceso:

![Creación del mensaje de instantánea](images/Dd351027.a97d383b-6ae4-458d-af3a-1ac0a41cd52b(EXCHG.150).gif "Creación del mensaje de instantánea")

1.  Un servidor SMTP transmite un mensaje al servicio de transporte de un servidor de buzón de correo. El servidor del buzón de correo es el servidor principal y el mensaje es el mensaje principal.

2.  Aunque la sesión SMTP original con el servidor SMTP sigue estando activa, el servicio de transporte del servidor principal abre una nueva sesión SMTP simultánea con el servicio de transporte en un servidor de buzón de correo diferente de la organización para crear la copia redundante del mensaje.
    
      - Si el servidor principal es miembro de un DAG, este se conecta con un servidor de buzón de correo diferente en el mismo DAG. Si el DAG se expande en varios sitios de Active Directory, se prefiere un servidor de buzón de correo en un sitio de Active Directory de manera predeterminada. Esta configuración se controla mediante el parámetro *ShadowMessagePreference* del cmdlet **Set-TransportService**. El valor por defecto es `PreferRemote`, pero se puede cambiar a `RemoteOnly` o `LocalOnly`.
    
      - Si el servidor principal no es miembro de un DAG, este se conecta a un servidor de buzón de correo diferente en el mismo sitio de Active Directory, con independencia del valor del parámetro *ShadowMessagePreference*.

3.  El servidor principal transmite una copia del mensaje al servicio de transporte del servidor de buzón de correo, y el servicio de transporte del otro servidor de buzón de correo notifica que la copia del mensaje se ha creado satisfactoriamente. La copia del mensaje es un mensaje de instantánea, y el servidor del buzón de correo que contiene el mensaje es el servidor de instantánea del servidor principal. El mensaje existe en una cola de instantánea en el servidor de instantánea.

4.  Cuando el servidor principal recibe una notificación del servidor de instantánea, el servidor principal acusa recibo del mensaje principal al servidor SMTP original en la sesión SMTP original, y la sesión SMTP se cierra.

## Mensajes enviados fuera de un límite de alta disponibilidad de transporte

Cuando un servidor de transporte Exchange 2013 transmite un mensaje fuera del límite de alta disponibilidad de tráfico y el servidor SMTP en el otro lado acusa recibo del mensaje, el servidor de transporte mueve el mensaje a la red de seguridad. No puede volver a enviarse el mensajes desde la red de seguridad una vez que el mensaje principal ha sido transmitido satisfactoriamente a través del límite de alta disponibilidad de transporte. Para obtener más información acerca de la red de seguridad, consulte [Red de seguridad](safety-net-exchange-2013-help.md).

## Mensajes transmitidos dentro de un límite de alta disponibilidad de transporte

El enrutado de mensajes está optimizado en Exchange 2013 de manera que cuando el destino último es un sitio DAG o de Active Directory, no suelen ser necesarios múltiples saltos entre el servicio de transporte en servidores de buzón de correo en dicho sitio DAG o Active Directory. Una vez que el mensaje es aceptado por el servicio de transporte en un servidor de buzón de correo en el sitio DAG o Active Directory que mantiene el último destino del mensaje, el siguiente salto del mensaje suele ser el propio destino último. El objetivo de la redundancia de instantánea de mantener dos copias de un mensaje en tránsito se cumple cuando una instantánea del mensaje existe en cualquier lugar de un sitio DAG o Active Directory. Normalmente, solo las situaciones de fallo en un DAG que exija que el cmdlet **Redirect-Message** purgue las colas activas en un servidor de buzón de correo requieren múltiples saltos en el mismo límite de alta disponibilidad de tráfico.

## La redundancia de instantánea con servidores de transporte de concentradores Exchange 2010 en el mismo sitio de Active Directory

Cuando un servidor de transporte de concentradores de Exchange 2010 transmite un mensaje a un servidor de buzón de correo Exchange 2013 en el mismo sitio de Active Directory, el servidor de transporte de concentradores de Exchange 2010 anuncia la compatibilidad de la redundancia de instantánea usando el comando XSHADOW, pero el servidor de buzón de correo no anuncia la compatibilidad de la redundancia de instantánea. Esto impide que el servidor de transporte de concentradores de Exchange 2010 cree una instantánea del mensaje en un servidor de buzón de correo de Exchange 2013.

Cuando un servicio de transporte en un servidor de buzón de correo Exchange 2013 transmite un mensaje a un transporte de concentradores Exchange 2010 del mismo sitio de Active Directory, el servidor de buzón de correo Exchange 2013 crea una instantánea del mensaje para el servidor de transporte de concentradores Exchange 2010. Una vez que el servidor de buzón de correo Exchange 2013 recibe notificación del servidor de transporte de concentradores Exchange 2010 de que el mensaje ha sido recibido satisfactoriamente, el servidor de buzón de correo Exchange 2013 mueve el mensaje procesado satisfactoriamente en la red de seguridad. Sin embargo, el mensaje procesado satisfactoriamente y almacenado en la red de seguridad por el buzón de correo Exchange 2013 no se vuelve a reenviar a los servidores de transporte de concentradores de Exchange 2010.

Volver al principio

## Tiempos de espera de SMTP

Durante el intento de realizar una copia redundante del mensaje, la conexión SMTP entre el servidor SMTP de envío y el servidor principal, o la sesión SMTP entre el servidor principal y el servidor de instantánea podría agotar el tiempo de espera. Los conectores de recepción y de envío tienen un parámetro *ConnectionInactivityTimeOut* para cuando los datos se transmiten en el conector. Los conectores de recepción también tienen un parámetro absoluto *ConnectionTimeOut*.

Cuando alguna de las sesiones SMTP agotan el tiempo de espera antes de que la instantánea del mensaje se cree y notifique satisfactoriamente, el resultado es controlado por el parámetro *RejectMessageOnShadowFailure* en el cmdlet **Set-TransportConfig**. Por defecto, el valor de este parámetro es `$false`, lo que significa que se acepta el mensaje principal sin crear una instantánea. Si el valor de este parámetro es `$true` el mensaje principal es rechazado con el error transitorio `451 4.4.0`.

Si la instantánea de un mensaje se crea satisfactoriamente, pero la sesión SMTP entre el servidor SMTP de envío y el servidor principal agota el tiempo de espera, el servidor principal acepta y procesa el mensaje principal. El servidor SMTP de envío reenviará el mensaje no confirmado, pero la detección de mensajes duplicados evitará que los usuarios de Exchange vean mensajes duplicados. Cuando el servidor SMTP de envío reenvía el mensaje, el servidor principal creará otra instantánea del mensaje. No existe relación entre las instantáneas creadas durante el reenvío de mensajes por parte del servidor SMTP de envío.

La siguiente tabla describe los parámetros que controlan la creación de instantáneas

### Parámetros de creación del mensaje de instantánea

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origen</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowMessagePreferenceSetting</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p><code>PreferRemote</code></p></td>
<td><ul>
<li><p><code>PreferRemote</code>   Intente hacer una instantánea del mensaje en un servidor de buzón de correo de un sitio Active Directory diferente. Si la operación falla, intente hacer una instantánea del mensaje en un servidor del sitio local de Active Directory.</p></li>
<li><p><code>LocalOnly</code>   Solo debe hacerse una instantánea del mensaje en un servidor de transporte del sitio local de Active Directory.</p></li>
<li><p><code>RemoteOnly</code>: Solo debe hacerse una instantánea del mensaje en un servidor de transporte de un sitio local diferente de Active Directory.</p></li>
</ul>
<p>Este parámetro solo es útil cuando el servidor principal que intenta realizar una instantánea del mensaje es un servidor de buzón de correo que es miembro de un DAG que se extiende en múltiples sitios de Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxRetriesForRemoteSiteShadow</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p>4</p></td>
<td><p>Este parámetro se emplea cuando el servidor de buzón de correo es miembro de un DAG que se extiende en múltiples sitios de Active Directory.</p>
<ul>
<li><p>Si <em>ShadowMessagePreferenceSetting</em> se configura en <code>PreferRemote</code>, el servidor de buzón de correo intenta primero crear una instantánea del mensaje en otro servidor de buzón de correo de un sitio remoto de Active Directory el número de veces especificadas en <em>MaxRetriesForRemoteSiteShadow</em>. Si esto falla, el servidor de buzón de correo intenta crear una instantánea del mensaje en un servidor diferente de buzón de correo del sitio local de Active Directory el número de veces especificadas en <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>Si <em>ShadowMessagePreferenceSetting</em> se configura en <code>RemoteOnly</code>, el servidor de buzón de correo solo intenta crear una instantánea del mensaje en otro servidor de buzón de correo de un sitio remoto de Active Directory el número de veces especificadas en <em>MaxRetriesForRemoteSiteShadow</em>.</p></li>
<li><p>El</p></li>
</ul>
<p>Cuando no se puede crear una instantánea del mensaje correctamente:</p>
<ul>
<li><p>Si <em>RejectMessageOnShadowFailure</em> es <code>$true</code>, el mensaje principal se rechaza con un error transitorio.</p></li>
<li><p>Si <em>RejectMessageOnShadowFailure</em> es <code>$false</code>, el mensaje principal se acepta de todas formas, pero no persiste de forma redundante.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MaxRetriesForLocalSiteShadow</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p>2</p></td>
<td><p>Este proceso se usa en las siguientes circunstancias:</p>
<ul>
<li><p>Si el servidor de buzón de correo es miembro de un DAG que se extiende en múltiples sitios de Active Directory.</p>
<ol>
<li><p>Si <em>ShadowMessagePreferenceSetting</em> se configura en <code>PreferRemote</code>, el servidor de buzón de correo intenta primero crear una instantánea del mensaje en otro servidor de buzón de correo de un sitio remoto de Active Directory el número de veces especificadas en <em>MaxRetriesForRemoteSiteShadow</em>. Si esto falla, el servidor de buzón de correo intenta crear una instantánea del mensaje en un servidor diferente de buzón de correo del sitio local de Active Directory el número de veces especificadas en <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>Si <em>ShadowMessagePreferenceSetting</em> se configura en <code>LocalOnly</code>, el servidor de buzón de correo solo intenta crear una instantánea del mensaje en un servidor de buzón de correo de un sitio remoto de Active Directory el número de veces especificadas en <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ol></li>
<li><p>Si el servidor de buzón de correo no es miembro de una DAG, o si el servidor de buzón de correo es miembro de una DAG que se encuentra en un sitio de Active Directory, el servidor de buzón de correo solo intenta crear una instantánea del mensaje en un servidor de buzón de correo distinto en el sitio local de Active Directory el número de veces especificadas en <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ul>
<p>Cuando no se puede crear una instantánea del mensaje correctamente:</p>
<ul>
<li><p>Si <em>RejectMessageOnShadowFailure</em> es <code>$true</code>, el mensaje principal se rechaza con un error transitorio.</p></li>
<li><p>Si <em>RejectMessageOnShadowFailure</em> es <code>$false</code>, el mensaje principal se acepta de todas formas, pero no persiste de forma redundante.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeout</em> en <strong>Set-ReceiveConnector</strong></p></td>
<td><p>5 minutos en el servicio de transporte en los servidores de buzón de correo</p>
<p>5 minutos en el servicio de transporte front-end en los servidores de acceso de cliente.</p>
<p>1 minuto en los servidores de transporte perimetral.</p></td>
<td><p>Este parámetro especifica el tiempo máximo que puede permanecer inactiva una conexión SMTP abierta con un servidor de mensajería de origen antes de que se cierre la conexión. El valor de este parámetro debe ser menor que el valor especificado por el parámetro <em>ConnectionTimeout</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ConnectionTimeout</em> en <strong>Set-ReceiveConnector</strong></p></td>
<td><p>10 minutos en el servicio de transporte en los servidores de buzón de correo</p>
<p>10 minutos en el servicio de transporte front-end en los servidores de acceso de cliente.</p>
<p>5 minutos en los servidores de transporte perimetral.</p></td>
<td><p>Este parámetro especifica el tiempo máximo que puede permanecer abierta una conexión SMTP con un servidor de mensajería de origen, incluso aunque el servidor de mensajería de origen esté transmitiendo datos. El valor de este parámetro debe ser mayor que el valor especificado por el parámetro <em>ConnectionInactivityTimeout</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeOut</em> en <strong>Set-SendConnector</strong></p></td>
<td><p>10 minutos</p></td>
<td><p>Este parámetro especifica el tiempo máximo que puede permanecer inactiva una conexión SMTP con un servidor de mensajería de destino antes de que se cierre la conexión.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## ¿Cómo se mantienen los mensajes de instantánea?

Una vez creado un mensaje de instantánea, el trabajo de la redundancia de instantánea no ha hecho más que empezar. El servidor principal y el servidor de instantánea necesitan estar en contacto entre sí para rastrear el progreso del mensaje.

Cuando el servidor principal transmite con éxito el mensaje al siguiente salto, y este acusa recibo del mensaje, el servidor principal actualiza el *estado de descarte* del mensaje como entrega completa. El estado de descarte consiste básicamente en un mensaje que contiene una lista de mensajes que se están supervisando. Los mensajes que se envían con éxito no necesitan mantenerse en una cola de instantánea, de manera que cuando el servidor de instantánea sabe que el servidor principal ha transmitido con éxito el mensaje al siguiente salto, el servidor de instantánea mueve el mensaje de la cola de instantánea a la red de seguridad.

El servidor de instantánea decide el estado de descarte de los mensajes de instantánea en las colas de instantáneas consultando al servidor principal. Si el servidor de instantánea abre una sesión SMTP con el servidor principal por cualquier motivo, incluida la transmisión de otros mensajes sin relación, el servidor de instantánea emite el comando **XQDISCARD** para decidir el estado de descarte de los mensajes principales. Si el servidor de instantánea no ha abierto una sesión SMTP con el servidor principal después de un intervalo de tiempo preconfigurado, el servidor de instantánea abrirá una sesión SMTP con el servidor principal y emitirá el comando **XQDISCARD**. El intervalo de tiempo lo controla el parámetro *ShadowHeartbeatFrequentcy* del cmdlet **Set-TransportConfig**. El valor predeterminado es de 2 minutos. Una vez que el servidor de instantánea abre una sesión SMTP con el servidor principal, este responde con las *notificaciones de descarte* para los mensajes se aplican al servidor de instantánea que realiza la consulta. En Exchange 2013, las notificaciones de descarte se almacenan en el disco, no en la memoria. Por lo tanto, si el servicio de transporte de Microsoft Exchange se reinicia las notificaciones de descarte persisten. Una vez iniciado el servicio, el servidor principal sigue conocimiento los mensajes que ha procesado satisfactoriamente, y la información está disponible para el servidor de instantánea.

La comunicación SMTP entre el servidor de instantánea y el servidor principal se emplea como el*latido* que determina la disponibilidad de los servidores. Si el servidor de instantánea no puede abrir una sesión SMTP con el servidor principal después de un intervalo de tiempo preconfigurado, o si la base de datos de transporte del servidor principal tiene un Id. distinto de base de datos, el servidor de instantánea se promueve como el servidor principal, promueve los mensajes de instantánea como mensajes principales y los transmite al siguiente salto. El intervalo de tiempo lo controla el parámetro *ShadowResubmitTimeSpan* del cmdlet **Set-TransportConfig**. El valor predeterminado es 3 horas.

El *administrador de redundancia de instantánea* es el componente central de un servidor de transporte de Exchange 2013 responsable de administrar la redundancia de instantánea. El administrador de redundancia de instantánea se encarga de mantener los datos enumerados a continuación de todos los mensajes principales que un servidor procesa actualmente:

  - El servidor de instantánea de cada mensaje principal que se está procesando.

  - El estado de descarte que se va a enviar a los servidores de instantánea.

El administrador de redundancia de instantánea se ocupa de las siguientes tareas relativas a todos los mensajes de instantánea que un servidor de instantáneas tiene en sus colas de instantáneas:

  - Mantener la lista de servidores principales de cada mensaje de instantánea.

  - Comparar el Id. original y el Id. actual de la base de datos de la base de datos de cola en el que se almacena la copia principal del mensaje.

  - Comprobar la disponibilidad de cada servidor principal para el que hay un mensaje de instantánea en cola.

  - Procesar las notificaciones de descarte de los servidores principales.

  - Eliminar los mensajes de instantánea de las colas de instantánea una vez que se han recibido todas las notificaciones de descarte previstas.

  - Decidir el momento en el que un servidor de instantánea debe hacerse con la propiedad de los mensajes de instantánea y, de este modo, convertirse en un servidor principal.

  - Rastrear las bifurcaciones de mensajes y otros efectos secundarios de mensajes como notificaciones de estado de entrega (DSN) e informes de diario para comprobar que la copia redundante del mensaje no se lanza hasta que se han procesado íntegramente todas las bifurcaciones del mensaje.

En la siguiente tabla se describen los parámetros que controlan cómo se mantiene un mensaje.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowHeartbeatFrequency</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p>2 minutos</p></td>
<td><p>La cantidad máxima de tiempo que espera un servidor de instantáneas antes de abrir una conexión SMTP en el servidor principal para comprobar el estado de descarte de los mensajes.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowResubmitTimeSpan</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p>3 horas</p></td>
<td><p>El tiempo de espera de un servidor antes de decidir que un servidor principal falla y asume la propiedad de las instantáneas de mensajes en la cola de instantáneas para el servidor principal que es inalcanzable.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShadowMessageAutoDiscardInterval</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p>2 días</p></td>
<td><p>Intervalo de tiempo en que un servidor conserva eventos de descarte para mensajes entregados correctamente. Un servidor principal pone en cola los eventos de descarte hasta que lo consulta el servidor de seguridad. Ahora bien, si el servidor de seguridad no consulta al servidor de seguridad respecto a la duración que se especifica en este parámetro, el servidor principal elimina los elementos descartados que están en cola.</p></td>
</tr>
<tr class="even">
<td><p><em>SafetyNetHoldTime</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p>2 días</p></td>
<td><p>Cuánto tiempo se conservan los mensajes procesados correctamente en la red de seguridad. Los mensajes de instantánea no confirmados terminan caducando en la red de seguridad al sumar <em>SafetyNetHoldTime</em> y <em>MessageExpirationTimeout</em> en <strong>Set-TransportService</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> en <strong>Set-TransportService</strong></p></td>
<td><p>2 días</p></td>
<td><p>Tiempo que un mensaje puede permanecer en una cola antes de que caduque.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Procesamiento de mensajes después de una interrupción

La redundancia de instantánea reduce el riesgo de que un mensaje se pierda a causa de una interrupción del servidor. Cuando un servidor de transporte vuelve a estar operativo tras una interrupción, pueden darse dos escenarios:

  - **El servidor vuelve a estar operativo con una nueva base de datos de transporte**   En este escenario, la base de datos de transporte no se puede recuperar debido a que los datos están dañados o a un error en el hardware. En tal caso, como el servidor de transporte tendrá un nuevo identificador de base de datos, el resto de servidores de transporte de la organización lo identificarán como una nueva ruta. Esto es igualmente aplicable a la situación en la que un servidor no se ha podido recuperar y, por lo tanto, se aprovisiona otro nuevo para sustituirlo.

  - **El servidor vuelve a conectarse con la misma base de datos de transporte**   En esta situación hipotética, no se ha producido ningún error en el servidor de transporte específico pero este ha estado desconectado durante un periodo de tiempo largo para que el servidor de instantánea asuma la propiedad de los mensajes y reenviarlos. Por ejemplo, a causa de un error en la tarjeta de red o un mantenimiento del servidor muy prolongado.

La siguiente tabla resume cómo redundancia de instantánea reacciona a estas dos situaciones. Para entenderlo mejor, supongamos que el servidor que ha sufrido una interrupción se llama Mailbox01.

### Procesamiento de mensajes en situaciones de recuperación

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Escenario de recuperación</th>
<th>Acciones realizadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox01 vuelve a estar conectado con una base de datos nueva.</p></td>
<td><p>Cuando Mailbox01 deja de estar disponible, todos los servidores que tienen mensajes de instantánea en cola para Mailbox01 asumirán la propiedad de dichos mensajes y los volverán a enviar. Los mensajes luego son entregados a sus destinos.</p>
<p>El retraso máximo de los mensajes es el valor del parámetro <em>ShadowHeartbeatFrequency</em> en el cmdlet <strong>Set-TransportConfig</strong>. El valor predeterminado es de 2 minutos.</p></td>
</tr>
<tr class="even">
<td><p>Mailbox01 vuelve a estar conectado con la misma base de datos.</p></td>
<td><p>Cuando Mailbox01 vuelve a estar en línea, entregará los mensajes en sus colas, que ya habrán sido entregadas por los servidores que mantienen instantáneas de los mensajes para Mailbox01. Como consecuencia, lo mensajes se entregarán por duplicado. Los usuarios del buzón de Exchange no verán mensajes duplicados gracias a la detección de mensajes duplicados. Sin embargo, los destinatarios en sistemas de mensajería ajenos a Exchange pueden recibir copias duplicadas de los mensajes.</p>
<p>El retraso máximo de los mensajes es el valor del parámetro <em>ShadowResubmitTimeSpan</em> en el cmdlet <strong>Set-TransportConfig</strong>. El valor predeterminado es 3 horas.</p></td>
</tr>
</tbody>
</table>


Volver al principio

