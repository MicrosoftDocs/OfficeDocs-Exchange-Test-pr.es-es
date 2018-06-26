---
title: 'Red de seguridad: Exchange 2013 Help'
TOCTitle: Red de seguridad
ms:assetid: d0abb807-3b12-4c7d-bc7e-769b87c84ccb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657495(v=EXCHG.150)
ms:contentKeyID: 49895928
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Red de seguridad

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

En Microsoft Exchange Server 2013, el mecanismo principal de alta disponibilidad del buzón de correo es el grupo de disponibilidad de base de datos (DAG). Para obtener más información acerca de los DAG, consulte [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md). El *contenedor de transporte* fue presentado por primera vez en Exchange 2007 y, para la versión Exchange 2010, se implementaron mejoras para proporcionar copias redundantes de mensajes después de su correcta entrega en los buzones de correo en DAG. En Exchange 2010, el contenedor de transporte ayudó a proteger contra la pérdida de datos ya que mantuvo una cola de mensajes entregados correctamente que no se habían replicado en las copias de base de datos de buzones de correo en el DAG. Cuando un error de servidor o base de datos de buzones de correo requirió la promoción de una copia desactualizada de la base de datos de buzones de correo, los mensajes en el contenedor de transporte se reenviaron automáticamente a la nueva copia activa de la base de datos de buzones de correo.

Se ha mejorado el contenedor de transporte en Exchange 2013 y ahora se llama *Red de seguridad*.

Vea de qué manera la red de seguridad es similar al contenedor de transporte en Exchange 2010:

  - La red de seguridad es una cola asociada con el servicio de transporte en un servidor de buzones de correo. Esta cola almacena copias de mensajes correctamente procesados por el servidor.

  - Puede especificar durante cuánto tiempo la red de seguridad almacenará las copias de los mensajes correctamente procesados antes de que caduquen y se eliminen automáticamente. El valor predeterminado es 2 días.

Vea de qué manera la red de seguridad es diferente en Exchange 2013:

  - La red de seguridad no requiere DAG. Para los servidores de buzones de correo que no pertenecen a un DAG, la red de seguridad almacena las copias de los mensajes entregados en otros servidores de buzones de correo en el sitio de Active Directory local.

  - La red de seguridad en sí ahora es redundante y deja de ser un único punto de error. Esto introduce el concepto de la *Red de seguridad principal* y la *Red de seguridad de instantáneas*. Si la red de seguridad principal no está disponible durante más de 12 horas, las solicitudes de reenvío se convierten en solicitudes de reenvío de instantáneas, y los mensajes se vuelven a entregar desde la red de seguridad de instantáneas.

  - La red de seguridad tiene algo de responsabilidad de la redundancia de instantáneas en entornos de DAG. La redundancia de instantáneas no necesita mantener otra copia del mensaje entregado en una cola de instantáneas mientras espera que el mensaje entregado se replique en las copias pasivas de la base de datos de buzones de correo en los otros servidores de buzones de correo en el DAG. La copia del mensaje entregado ya está almacenada en la red de seguridad, así que el mensaje se puede reenviar desde la red de seguridad, si es necesario.

  - En Exchange 2013, la alta disponibilidad del transporte es más que solo el mejor esfuerzo para la redundancia de mensajes. Exchange 2013 intenta garantizar la redundancia de mensajes. Debido a esto, no se puede especificar un límite máximo de tamaño para la red de seguridad. Solo se puede especificar durante cuánto tiempo la red de seguridad almacenará los mensajes antes de que se eliminen automáticamente.

**Contenido**

Cómo funciona la red de seguridad

Reenvío de mensajes desde la red de seguridad

Reenvío de mensajes desde la red de seguridad de instantáneas

## Cómo funciona la red de seguridad

La redundancia de instantáneas mantiene una copia redundante del mensaje mientras este está en tránsito. La red de seguridad mantiene una copia redundante del mensaje luego de que dicho mensaje es correctamente procesado. Por lo tanto, la red de seguridad comienza donde termina la redundancia de instantáneas. Para la red de seguridad, también se aplican los mismos conceptos de redundancia de instantáneas, incluidos el límite de alta disponibilidad del transporte, los mensajes principales, los servidores principales, los mensajes de instantáneas y los servidores de instantáneas. Para obtener más información, consulte [Redundancia de instantánea](shadow-redundancy-exchange-2013-help.md).

La red de seguridad principal existe en el servidor de buzones de correo que retuvo el mensaje principal antes de que el servicio de transporte procesara correctamente dicho mensaje. Esto podría significar que el mensaje fue entregado al servicio de transporte de buzones en el servidor de buzones de correo de destino. Otra alternativa es que el mensaje podría haber sido retransmitido mediante el servidor de buzones de correo en un sitio de Active Directory designado como sitio de concentradores en el camino hacia el DAG de destino o al sitio de Active Directory. Después de que el servidor principal procesa el mensaje principal, el mensaje se mueve de la cola activa a la red de seguridad principal en el mismo servidor.

La red de seguridad de instantáneas existe en el servidor de buzones de correo que retuvo el mensaje de instantáneas. Después de que el servidor de instantáneas determina que el servidor principal procesó correctamente el mensaje principal, el servidor de instantáneas mueve el mensaje de instantáneas de la cola de instantáneas a la red de seguridad de instantáneas en el mismo servidor. Si bien puede parecer obvio, la existencia de la red de seguridad de instantáneas requiere que la redundancia de instantáneas esté habilitada, y esta está habilitada de manera predeterminada en Exchange 2013.

Los parámetros utilizados por la red de seguridad se describen en la tabla siguiente.


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
<td><p><em>SafetyNetHoldTime</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p>2 días</p></td>
<td><p>El tiempo que los mensajes principales correctamente procesados se almacenan en la red de seguridad principal y que los mensajes de instantáneas reconocidos se almacenan en la red de seguridad de instantáneas.</p>
<p>También puede especificar este valor en el centro de administración de Exchange (EAC) en <strong>Flujo de correo</strong> &gt; <strong>Conectores de recepción</strong> &gt; <strong>Más opciones</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icono Más opciones" alt="Icono Más opciones" /> &gt; <strong>Configuración de transporte de la organización</strong> &gt; <strong>Red de seguridad</strong> &gt; <strong>Tiempo de retención de red de seguridad</strong>.</p>
<p>Los mensajes de instantáneas no reconocidos finalmente caducan en la red de seguridad de instantáneas después de la suma de <em>SafetyNetHoldTime</em> y de <em>MessageExpirationTimeout</em> en <strong>Set-TransportService</strong>.</p>
<p>Para evitar la pérdida de datos durante los reenvíos de la red de seguridad, el valor de <em>SafetyNetHoldTime</em> debe ser superior o igual al valor de <em>ReplayLagTime</em> en <strong>Set-MailboxDatabaseCopy</strong> para la copia retrasada de la base de datos de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplayLagTime</em> en <strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>No configurado</p></td>
<td><p>La cantidad de tiempo que el servicio de replicación de Microsoft Exchange debe esperar antes de reproducir los archivos de registro que se copiaron en la copia de la base de datos pasiva. Si se establece este parámetro en un valor mayor que 0, se crea una copia retrasada de la base de datos de buzones de correo. El valor máximo es 14 días.</p>
<p>Para evitar la pérdida de datos durante los reenvíos de la red de seguridad, el valor de <em>ReplayLagTime</em> debe ser inferior o igual al valor de <em>SafetyNetHoldTime</em> en <strong>Set-TransportConfig</strong> para la copia retrasada de la base de datos de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> en <strong>Set-TransportService</strong></p></td>
<td><p>2 días</p></td>
<td><p>Tiempo que un mensaje puede permanecer en una cola antes de que caduque.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowRedundancyEnabled</em> en <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> habilita la redundancia de instantáneas en todos los servidores de transporte de la organización.</p></li>
<li><p><code>$false</code> deshabilita la redundancia de instantáneas en todos los servidores de transporte de la organización.</p></li>
</ul>
<p>Una red de seguridad redundante requiere redundancia de instantáneas para su habilitación.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Reenvío de mensajes desde la red de seguridad

Los reenvíos de mensajes desde la red de seguridad se inician con el componente Active Manager del servicio de replicación de Microsoft Exchange que administra copias de la base de datos de buzones de correo y DAG. No se requiere ninguna acción manual para reenviar mensajes desde la red de seguridad. Para obtener más información acerca de Active Manager, consulte [Active Manager](active-manager-exchange-2013-help.md).

Hay dos situaciones básicas de reenvío de mensajes de la red de seguridad:

  - Después de la conmutación por error automática o manual de una base de datos de buzones de correo en un DAG.

  - Después de activar una copia retrasada de una base de datos de buzones de correo.

Una *copia retrasada de la base de datos de buzones de correo* o *copia retrasada* es una copia pasiva de una base de datos de buzones de correo donde las actualizaciones en la base de datos se demoran intencionalmente para proteger contra el daño lógico de la base de datos de buzones de correo. Para obtener más información, consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

La única diferencia significativa entre las dos situaciones es qué tan lejos en el tiempo ir para reenviar mensajes desde la red de seguridad. Generalmente, para la conmutación por error en un DAG, la nueva copia activa de la base de datos de buzones de correo es anterior, de varios minutos a varias horas, a la copia activa más antigua. Una copia retrasada de una base de datos de buzones de correo es, por lo general, varios días anterior a la copia activa más antigua.

El principal requisito para un reenvío correcto desde la red de seguridad de una copia retrasada es que la cantidad de tiempo que los mensajes se almacenan en la red de seguridad sea mayor que el tiempo de retraso de la copia retrasada de la base de datos de buzones de correo o igual a él. En otras palabras, el valor de *SafetyNetHoldTime* en **Set-TransportConfig** debe ser superior o igual al valor de *ReplayLagTime* en **Set-MailboxDatabaseCopy** para la copia retrasada.

Volver al principio

## Reenvío de mensajes desde la red de seguridad de instantáneas

Al igual que el reenvío de mensajes desde la red de seguridad principal, los reenvíos de mensajes desde la red de seguridad de instantáneas son totalmente automatizados y no requieren ningún tipo de intervención manual.

Cuando Active Manager solicita el reenvío de mensajes desde la red de seguridad durante un período específico, la solicitud se dirige al servicio de transporte en los servidores de buzones de correo donde la red de seguridad principal retiene las copias de mensajes durante el período solicitado. En las grandes organizaciones de Exchange, es probable que los mensajes solicitados existan en la red de seguridad en varios servidores de buzones de correo, sobre todo si el período solicitado es prolongado.

Sin la optimización, el reenvío de mensajes desde la red de seguridad daría como resultado cantidades potencialmente elevadas de entregas duplicadas. Las entregas duplicadas en la organización de Exchange no son un problema porque la detección de mensajes duplicados evita que los usuarios de buzones vean copias duplicadas de un mensaje. Pero la entrega de mensajes duplicados a destinatarios fuera de la organización de Exchange dará como resultado copias duplicadas de mensajes. Afortunadamente, el reenvío de mensajes desde la red de seguridad ha sido optimizada en Exchange 2013 para que reduzca la entrega de mensajes duplicados.

Si inicialmente la red de seguridad principal no responde o deja de responder durante un reenvío de mensajes, Active Manager continúa intentando contactarla durante 12 horas antes de abandonar los intentos. Después de 12 horas, se envía una difusión al servicio de transporte en todos los servidores de buzones en el enlace de alta disponibilidad del transporte que solicita el reenvío del mensaje desde la red de seguridad por el intervalo de tiempo requerido para la base de datos de buzones de correo requerida. Cuando una red de seguridad de instantáneas responde, reenvía los mensajes únicamente para la base de datos de buzones de correo requerida durante el intervalo de tiempo requerido.

Hay algunas consideraciones importantes para los mensajes de instantáneas almacenadas en la red de seguridad de instantáneas:

  - La red de seguridad de instantáneas no sabe a dónde el servidor principal transmitió el mensaje principal.

  - Los mensajes de instantáneas en la red de seguridad de instantáneas únicamente contienen los destinatarios de sobre de mensaje original, no los destinatarios reales a los que se entregó el mensaje principal. Por ejemplo, el destinatario de sobre de mensaje puede ser un grupo de distribución que requiere expansión.

  - Los mensajes en la red de seguridad de instantáneas no tienen ninguna de las actualizaciones de mensaje que se produjeron después de que el servidor principal procesara el mensaje. Por ejemplo, codificación del mensaje o conversión de contenido.

El mensaje de instantáneas reenviado desde la red de seguridad de instantáneas requiere categorización y procesamiento completos mediante el servicio de transporte en el servidor de buzones de correo. El reenvío de grandes cantidades de mensajes de instantáneas desde la red de seguridad de instantáneas puede ser costoso en términos de recursos del servidor de buzones de correo. Afortunadamente, el reenvío de mensajes de instantáneas desde la red de seguridad de instantáneas también ha sido optimizado, de modo que únicamente se reenvían los mensajes en la red de seguridad de instantáneas por el intervalo de tiempo requerido y para la base de datos de buzones de correo requerida.

La interacción de la red de seguridad principal y la red de seguridad de instantáneas durante el reenvío de mensajes de describe en la siguiente situación.

1.  Active Manager solicita el reenvío de mensajes desde la red de seguridad para una base de datos de buzones de correo por el intervalo de tiempo de 5:00:00 a 9:00. Sin embargo, el servidor de buzones de correo que retiene la red de seguridad principal se bloqueó debido a un error de hardware. Active Manager intenta repetidas veces contactarse con la red de seguridad principal durante 12 horas.

2.  Después de 12 horas, Active Manager envía un mensaje de difusión al servicio de transporte en todos los servidores de buzones en el límite de alta disponibilidad del transporte en busca de otras redes de seguridad que contengan mensajes para la base de datos de buzones de destino del intervalo de tiempo de 5:00 a 9:00. La red de seguridad de instantáneas responde con mensajes de reenvío para la base de datos de buzones del intervalo de tiempo de 5:00 a 9:00.

Se produce una interacción interesante si la red de seguridad principal estaba sin conexión durante parte del intervalo de reenvío requerido, según se describe en la siguiente situación.

1.  La base de datos de colas en el servidor de buzones de correo que retiene la red de seguridad principal está dañada, y a las 7:00 se crea una nueva base de datos de colas. Se pierden todos los mensajes principales almacenados en la red de seguridad principal de 1:00 a 7:00, pero el servidor puede almacenar copias de mensajes correctamente entregados en la red de seguridad a partir de las 7:00.

2.  Active Manager solicita el reenvío de mensajes desde la red de seguridad para una base de datos de buzones de correo por el intervalo de tiempo de 1:00 a 9:00.

3.  La red de seguridad principal reenvía mensajes por el intervalo de tiempo de 7:00 a 9:00.

4.  La red de seguridad principal envía un mensaje de difusión al servicio de transporte en todos los servidores de buzones en el límite de alta disponibilidad del transporte en busca de otras redes de seguridad que contengan mensajes para la base de datos de buzones de correo de destino por el intervalo de tiempo de 1:00 a 7:00 para el cual la red de seguridad principal no tiene mensaje. La red de seguridad de instantáneas genera una segunda solicitud de reenvío en nombre de la red de seguridad principal para reenviar los mensajes de instantáneas para la base de datos de buzones de correo de destino por el intervalo de tiempo de 1:00 a 7:00.

Hay otros problemas que se deben considerar cuando se reenvían mensajes desde la red de seguridad.

1.  Todas las notificaciones de estado de entrega (DSN) y los informes de no entrega (NDR) se suprimen para los reenvíos de la red de seguridad. Por ejemplo, si el mensaje principal resultó ser un NDR, el NDR para el informe reenvío no se entregará.

2.  Los usuarios eliminados de un grupo de distribución pueden no recibir un mensaje reenviado cuando la red de seguridad de instantáneas reenvía el mensaje. Por ejemplo, se envía un mensaje a un grupo que contiene el usuario A y el usuario B, y ambos destinatarios reciben el mensaje. El usuario B se quita posteriormente del grupo. Más tarde, se realiza una solicitud de reenvío desde la red de seguridad principal para la base de datos de buzones de correo que retiene el buzón del usuario B. Sin embargo, la red de seguridad principal no está disponible durante más de 12 horas, así que el servidor de la red de seguridad de instantáneas responde y reenvía el mensaje afectado. Durante un reenvío cuando el grupo de distribución se expande, el usuario B no es miembro del grupo y no recibirá una copia del mensaje reenviado.

3.  Los usuarios nuevos agregados a un grupo de distribución pueden recibir un mensaje reenviado anterior cuando la red de seguridad de instantáneas reenvía el mensaje. Por ejemplo, se envía un mensaje a un grupo que contiene el usuario A y el usuario B, y ambos destinatarios reciben el mensaje. El usuario C posteriormente se agrega al grupo. Más tarde, se realiza una solicitud de reenvío desde la red de seguridad principal para la base de datos de buzones de correo que retiene el buzón del usuario C. Sin embargo, el servidor de la red de seguridad principal no está disponible durante más de 12 horas, así que el servidor de la red de seguridad de instantáneas responde y reenvía los mensajes afectados. Durante un reenvío cuando el grupo de distribución se expande, el usuario C es miembro del grupo y recibirá una copia del mensaje reenviado.

Volver al principio

