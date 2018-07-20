---
title: 'DSN y NDR en Exchange 2013: Exchange 2013 Help'
TOCTitle: DSN y NDR en Exchange 2013
ms:assetid: 8e91de84-76fa-49b2-898c-c5eface76560
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232118(v=EXCHG.150)
ms:contentKeyID: 49895769
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DSN y NDR en Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_


> [!NOTE]
> Si necesita ayuda con NDR en Office 365 o Exchange Online, vea <A href="https://go.microsoft.com/fwlink/p/?linkid=524931">Informes de no entrega de correo electrónico en Office 365</A>.



Cuando hay un problema al entregar un mensaje, Exchange Server 2013 enviará una notificación de estado de entrada (DSN) al remitente del mensaje. Estos mensajes generados por el sistema también se conocen como mensajes de devolución y contienen un código de error, detalles técnicos sobre el problema y, a veces, pasos para que el remitente del mensaje solucione el problema. Los mensajes de informe de no entrega (NDR) son un tipo común de notificación de estado. En este tema para los administradores de correo electrónico se describen las posibles causas y soluciones de muchos de los códigos de estado de NDR. También se indica cómo leer e interpretar los mensajes de NDR.

**Contenido**

Códigos de estado mejorados habituales

Secciones del NDR

Ejemplos

## Códigos de estado mejorados habituales

En la tabla siguiente se proporciona una lista de los códigos de estado mejorados que se devuelven en los NDR para los errores de entrega de mensajes más habituales.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Código de estado mejorado</th>
<th>Descripción</th>
<th>Posible causa</th>
<th>Información adicional</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>4.3.1</p></td>
<td><p><code>Insufficient system resources</code></p></td>
<td><p>Error de memoria insuficiente. La causa puede ser un problema de recursos, como un disco lleno.</p>
<p>En lugar de obtener un error de disco lleno, puede que obtenga un error de memoria insuficiente.</p></td>
<td><p>Asegúrese de que el servidor de Exchange cuenta con suficiente almacenamiento en disco.</p></td>
</tr>
<tr class="even">
<td><p>4.3.2</p></td>
<td><p><code>System not accepting network messages</code></p></td>
<td><p>Este NDR (informe de no entrega) se genera cuando se ha inmovilizado una cola.</p></td>
<td><p>Puede resolver este problema desbloqueando la cola.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.1</p></td>
<td><p><code>Connection timed out</code></p></td>
<td><p>El servidor de destino no responde. Este error podría estar provocado por condiciones transitorias de la red. El servidor de Exchange intenta volver a conectarse automáticamente al servidor y entregar el correo. Si tras varios intentos la entrega no se produce correctamente, se genera un NDR con un código de error permanente.</p></td>
<td><p>Supervise la situación. Puede tratarse de un problema transitorio que se solucione por sí solo.</p></td>
</tr>
<tr class="even">
<td><p>4.4.2</p></td>
<td><p><code>Connection dropped</code></p></td>
<td><p>Se ha interrumpido una conexión entre servidores. Este error podría estar provocado por condiciones transitorias de la red o porque un servidor está teniendo problemas. El servidor de envío volverá a intentar entregar el mensaje durante un período determinado de tiempo y, después, generará informes de estado.</p></td>
<td><p>Observe la situación cuando el servidor vuelva a intentar realizar la entrega. Puede tratarse de un problema transitorio que se solucione por sí solo.</p>
<p>Esta situación se puede producir también cuando se alcanza el límite de tamaño de un mensaje para la conexión, o si se ha superado el límite configurado de frecuencia de envío de mensajes para la dirección IP del cliente.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.7</p></td>
<td><p><code>Message expired</code></p></td>
<td><p>El mensaje de la cola ha expirado. El servidor de envío intentó retransmitir o entregar el mensaje, pero no se completó la acción antes de producirse el tiempo de expiración del mensaje. Este mensaje también podría indicar que se ha alcanzado el límite de encabezados de mensaje en un servidor remoto, o bien que se produjo cualquier otro tiempo de espera agotado de protocolo durante la comunicación con el servidor remoto.</p></td>
<td><p>Este mensaje suele indicar un problema en el servidor de recepción. Compruebe la validez de la dirección del destinatario y que el servidor de recepción está configurado para recibir mensajes correctamente.</p>
<p>Es posible que tenga que reducir el número de destinatarios en el encabezado del mensaje del host del que está recibiendo este error. Si vuelve a enviar el mensaje, se coloca en la cola otra vez. Si está disponible el servidor de recepción, el mensaje se entrega.</p></td>
</tr>
<tr class="even">
<td><p>5.0.0</p></td>
<td><p><code>HELO / EHLO requires domain address</code></p></td>
<td><p>Esta es una situación de error permanente. Entre las posibles causas se incluyen:</p>
<ul>
<li><p>No hay ruta para el espacio de direcciones especificado. Por ejemplo, hay configurado un conector SMTP, pero esta dirección no coincide.</p></li>
<li><p>DNS ha devuelto un host autorizado que no se encuentra en el dominio.</p></li>
<li><p>Se ha producido un error SMTP.</p></li>
</ul></td>
<td><p>Entre las posibles soluciones se incluyen:</p>
<ul>
<li><p>En uno o más conectores SMTP, agregue un valor asterisco (<strong>*</strong>) como espacio de direcciones SMTP.</p></li>
<li><p>Compruebe que DNS funciona.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>5.1.0</p></td>
<td><p><code>Sender denied</code></p></td>
<td><p>Este NDR se debe a un error general (error de dirección incorrecta). Puede que una dirección de correo electrónico u otro atributo no se encuentren en los Servicios de dominio de Active Directory. Este problema podría producirse si las entradas de contactos no tienen establecido el atributo <strong>targetAddress</strong>. Otra posible causa podría ser que el atributo <strong>homeMDB</strong> de un usuario no se haya podido determinar. El atributo <strong>homeMDB</strong> corresponde al servidor de Exchange donde reside el buzón del usuario.</p>
<p>Otra causa habitual de este NDR se da cuando se usa Microsoft Outlook para guardar un mensaje de correo electrónico como un archivo y, a continuación, otra persona lo abre sin conexión y responde al mensaje. La propiedad del mensaje solo preserva el atributo <strong>legacyExchangeDN</strong> cuando Outlook entrega el mensaje y, por consiguiente, se podría producir un error en la búsqueda.</p></td>
<td><p>O bien la dirección del destinatario tiene un formato incorrecto o el destinatario no se ha podido resolver correctamente. El primer paso para solucionar este error es comprobar la dirección del destinatario y volver a enviar el mensaje.</p></td>
</tr>
<tr class="even">
<td><p>5.1.1</p></td>
<td><p><code>Bad destination mailbox address</code></p></td>
<td><p>Este error podría deberse a las siguientes condiciones:</p>
<ul>
<li><p>El remitente escribió incorrectamente la dirección de correo electrónico del destinatario.</p></li>
<li><p>El destinatario no existe en el sistema de correo electrónico de destino.</p></li>
<li><p>El buzón del destinatario se ha movido y la memoria caché del destinatario de Outlook no se ha actualizado en el equipo del remitente.</p></li>
<li><p>El nombre de dominio (DN) heredado del buzón del destinatario de Servicios de dominio de Active Directory no es válido.</p></li>
</ul></td>
<td><p>Normalmente, este error se produce cuando el remitente del mensaje escribe incorrectamente la dirección de correo electrónico del destinatario. El remitente debe comprobar la dirección de correo electrónico del destinatario y enviarlo de nuevo. Este error también se produce si la dirección de correo electrónico del destinatario era correcta pero cambió o se quitó del sistema de correo electrónico de destino.</p>
<p>Si el remitente del mensaje está en la misma organización de Exchange que el destinatario y el buzón del destinatario aún existe, determine si se ha reubicado en otro servidor de correo electrónico. En este caso, es posible que Outlook no haya actualizado la memoria caché del destinatario correctamente. Indique al remitente que quite la dirección del destinatario de la memoria caché de destinatarios de Outlook del remitente y que, después, cree un mensaje nuevo. Si se vuelve a enviar el mensaje original, se producirá el mismo error.</p>
<p>Este error puede deberse a otras causas, como un nombre completo (DN) heredado no válido en los Servicios de dominio de Active Directory. Examine y corrija el nombre completo anterior del buzón del destinatario. Después, indique al remitente que quite la dirección del destinatario de la memoria caché de destinatarios de Outlook del remitente y que, después, cree un mensaje nuevo. Si se vuelve a enviar el mensaje original, se producirá el mismo error.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.2</p></td>
<td><p><code>Invalid X.400 address</code></p></td>
<td><p>El destinatario tiene una dirección que no es SMTP y que no coincide con un destino. La dirección no parece ser local y no hay conectores configurados con espacios de direcciones que contengan la dirección del destinatario.</p></td>
<td><p>Compruebe que la dirección del destinatario se ha escrito correctamente. Si la dirección del destinatario está en un sistema de correo electrónico que no es SMTP y al que usted desea específicamente entregar correo, debe agregar el tipo de conector adecuado a su topología y configurarlo para que ofrezca servicio al sistema de correo electrónico del destinatario.</p></td>
</tr>
<tr class="even">
<td><p>5.1.3</p></td>
<td><p><code>Invalid recipient address</code></p></td>
<td><p>Este mensaje indica que la dirección del destinatario aparece de forma incorrecta en el mensaje.</p></td>
<td><p>O bien la dirección del destinatario tiene un formato incorrecto o la dirección del destinatario no se ha podido resolver correctamente. El primer paso para solucionar este error es comprobar la dirección del destinatario y volver a enviar el mensaje.</p>
<p>También, examine la directiva de destinatario SMTP y asegúrese de que cada dominio de correo para el que desea aceptar correo aparece correctamente.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.4</p></td>
<td><p><code>Destination mailbox address ambiguous</code></p></td>
<td><p>Dos o más destinatarios de la organización de Exchange tienen la misma dirección.</p></td>
<td><p>Normalmente, este error se produce debido a una configuración incorrecta de los Servicios de dominio de Active Directory. Posiblemente por problemas de replicación, dos objetos de destinatario de los Servicios de dominio de Active Directory tienen la misma dirección SMTP o dirección de Exchange Server (EX).</p></td>
</tr>
<tr class="even">
<td><p>5.1.7</p></td>
<td><p><code>Invalid address</code></p></td>
<td><p>La dirección SMTP del remitente falta o tiene un formato incorrecto, el atributo <strong>mail</strong> del servicio de directorio. El elemento de correo no se puede entregar sin un atributo <strong>mail</strong> válido.</p></td>
<td><p>Compruebe la estructura de directorios del remitente y vea si existe el atributo <strong>mail</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.1</p></td>
<td><p><code>Mailbox cannot be accessed</code></p></td>
<td><p>No se puede obtener acceso al buzón de correo. Puede que el buzón esté sin conexión, deshabilitado o que una regla haya puesto en cuarentena al mensaje.</p></td>
<td><p>Compruebe si la base de datos del destinatario está conectada, si el buzón del mismo está deshabilitado o si el mensaje se ha puesto en cuarentena.</p></td>
</tr>
<tr class="even">
<td><p>5.2.2</p></td>
<td><p><code>Mailbox full</code></p></td>
<td><p>El buzón del destinatario ha superado su cuota de almacenamiento y ya no puede aceptar mensajes nuevos.</p></td>
<td><p>Este error se produce cuando el buzón del destinatario ha superado su cuota de almacenamiento. El destinatario debe reducir el tamaño del buzón o el administrador debe aumentar la cuota de almacenamiento para que la entrega sea correcta.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.3</p></td>
<td><p><code>Message too large</code></p></td>
<td><p>Este mensaje es demasiado grande y se ha superado la cuota local. Por ejemplo, un usuario remoto de Exchange puede tener una restricción sobre el tamaño máximo de un mensaje entrante.</p></td>
<td><p>Envíe nuevamente el mensaje sin datos adjuntos, o bien establezca el límite en el servidor o en el cliente para que permita un tamaño de mensaje mayor.</p></td>
</tr>
<tr class="even">
<td><p>5.2.4</p></td>
<td><p><code>Mailing list expansion problem</code></p></td>
<td><p>El destinatario es una lista de distribución dinámica mal configurada. O la cadena de filtrado no es válida o lo es el DN base de la lista de distribución dinámica.</p></td>
<td><p>Establezca el nivel de registro de evento categorizador como mínimo en su nivel inferior y envíe otro mensaje a la lista de distribución dinámica. Compruebe en el registro de eventos de la aplicación si no se ha producido un evento 6025 o 6026 que indica cuál es el atributo mal configurado en el objeto de lista de distribución dinámica.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.3</p></td>
<td><p><code>Unrecognized command</code></p></td>
<td><p>Cuando el servidor remoto de Exchange llega a su capacidad de almacenamiento en disco para contener correo, puede responder con este NDR. Este error se produce normalmente cuando el servidor de envío envía correo con un comando ESMTP BDAT. Este error indica igualmente un posible error de protocolo SMTP.</p></td>
<td><p>Asegúrese de que el servidor remoto cuenta con la suficiente capacidad de almacenamiento para hospedar correo. Compruebe el registro SMTP.</p></td>
</tr>
<tr class="even">
<td><p>5.3.4</p></td>
<td><p><code>Message too big for system</code></p></td>
<td><p>El mensaje supera el límite de tamaño configurado en un transporte o en una base de datos de buzones de correo y no se puede aceptar. Este error puede ser generado por el sistema de correo electrónico de envío o de recepción.</p></td>
<td><p>Este error se produce cuando el tamaño del mensaje enviado por el remitente supera el tamaño de mensaje máximo permitido cuando pasa a través de un componente de transporte o una base de datos de buzones de correo. El remitente debe reducir el tamaño del mensaje para poder entregarlo correctamente. Para obtener más información acerca de cómo configurar límites de tamaño de mensajes, vea <a href="message-size-limits-exchange-2013-help.md">Límites de tamaño de mensaje</a>.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.5</p></td>
<td><p><code>System incorrectly configured</code></p></td>
<td><p>Se ha detectado una situación de bucle de correo, lo que significa que el servidor está configurado para que se generen bucles de correo electrónico en el propio servidor.</p></td>
<td><p>Compruebe la configuración de los conectores del servidor para ver si hay bucles y asegúrese de que cada conector está definido por un único puerto entrante. Si hay varios servidores virtuales, asegúrese de que ninguno de ellos está establecido como &quot;Ninguna asignada&quot;.</p></td>
</tr>
<tr class="even">
<td><p>5.4.4</p></td>
<td><p><code>Invalid arguments</code></p></td>
<td><p>Este NDR se produce si no hay una ruta para la entrega de mensajes o si el categorizador no puede determinar el destino del siguiente salto.</p></td>
<td><p>Compruebe que el nombre de dominio especificado es válido y que existe un registro de intercambio de correo (MX).</p></td>
</tr>
<tr class="odd">
<td><p>5.4.6</p></td>
<td><p><code>Routing loop detected</code></p></td>
<td><p>Un error de configuración ha provocado un bucle de correo electrónico. De forma predeterminada, después de 20 iteraciones de un bucle de correo electrónico, Exchange interrumpe el bucle y genera un NDR para el remitente del mensaje.</p></td>
<td><p>Este error se produce cuando la entrega de un mensaje genera un mensaje en respuesta. A su vez, dicho mensaje genera un tercer mensaje y el proceso se repite, creando un bucle. Para ayudar a protegerse contra recursos que agotan el sistema, Exchange interrumpe el bucle de correo después de 20 iteraciones. Normalmente, los bucles de correo se crean debido a un error de configuración en el servidor de correo de envío, en el servidor de correo de recepción o en ambos. Compruebe la configuración de las reglas del buzón del destinatario y del remitente para determinar si está habilitado el reenvío automático de mensajes.</p></td>
</tr>
<tr class="even">
<td><p>5.5.2</p></td>
<td><p><code>Send hello first</code></p></td>
<td><p>Se produce un error SMTP genérico cuando los comandos SMTP se envían fuera de la secuencia. Por ejemplo, un servidor intenta enviar un comando AUTH (autorización) antes de identificarse a sí mismo con un comando EHLO.</p>
<p>Este error también puede producirse cuando el disco del sistema está lleno.</p></td>
<td><p>Vea el registro SMTP o una traza Netmon, y asegúrese de que cuenta con el almacenamiento en disco adecuado y de que dispone de memoria virtual.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.3</p></td>
<td><p><code>Too many recipients</code></p></td>
<td><p>El número total combinado de destinatarios en las líneas Para, CC y CCO del mensaje supera el número total de destinatarios permitidos en un único mensaje.</p></td>
<td><p>Este error se produce cuando el remitente ha incluido demasiados destinatarios en el mensaje. El remitente debe reducir el número de direcciones de destinatarios del mensaje o debe aumentar el número máximo de destinatarios para que el mensaje se pueda entregar correctamente.</p></td>
</tr>
<tr class="even">
<td><p>5.5.4</p></td>
<td><p><code>Invalid domain name</code></p></td>
<td><p>El mensaje contiene o bien un remitente que no es válido o un formato incorrecto de dirección de destinatario.</p>
<p>Un posible causa sería que el formato de la dirección del destinatario contiene caracteres que no cumplen los estándares de Internet.</p></td>
<td><p>Compruebe si hay caracteres no estándar en la dirección del destinatario.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.6</p></td>
<td><p><code>Invalid message content</code></p></td>
<td><p>Este mensaje indica un posible error de protocolo.</p></td>
<td><p>Compruebe los posibles errores en el registro de eventos.</p></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Delivery not authorized</code></p></td>
<td><p>No se permite que el remitente envíe mensajes al destinatario.</p></td>
<td><p>Este error se produce cuando el remitente intenta enviar un mensaje a un destinatario pero no está autorizado a hacerlo. Esto suele ocurrir cuando un remitente intenta enviar mensajes a un grupo de distribución que se ha configurado para aceptar mensajes sólo de los miembros de ese grupo de distribución o de otros remitentes autorizados. El remitente debe solicitar permiso para enviar mensajes al destinatario.</p>
<p>Este error también se puede producir si una regla de transporte de Exchange rechaza un mensaje porque cumplía las condiciones configuradas en la regla de transporte.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.1</p></td>
<td><p><code>Unable to relay</code></p></td>
<td><p>No se permite al sistema de correo electrónico de envío enviar un mensaje a un sistema de correo electrónico en el que ese sistema de correo electrónico no sea el destino final del mensaje.</p></td>
<td><p>Este error se produce cuando el sistema de correo electrónico de envío intenta enviar un mensaje anónimo a un sistema de correo electrónico de recepción y éste no acepta mensajes para el dominio o dominios especificados en uno o varios de los destinatarios. Los motivos más habituales de este error son los siguientes:</p>
<ul>
<li><p>Un tercero intenta usar un sistema de correo electrónico de recepción para enviar correo no deseado y este sistema rechaza el intento. Debido a la naturaleza del correo no deseado, es posible que la dirección de correo electrónico del remitente se haya falsificado y el NDR resultante se haya enviado a la dirección de correo electrónico del remitente no sospechoso. Es difícil evitar esta situación.</p></li>
<li><p>Un registro de MX de un dominio apunta a un sistema a de correo electrónico de recepción en el que el dominio no se acepta. El administrador responsable del nombre de dominio específico debe corregir el registro de MX o configurar el sistema de correo electrónico de recepción para que acepte los mensajes enviados a ese dominio, o ambos.</p></li>
<li><p>El sistema de correo electrónico de envío o el cliente que debe usar el sistema de correo electrónico de recepción para retransmitir los mensajes no tienen los permisos correctos para hacerlo.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Client was not authenticated</code></p></td>
<td><p>El sistema de correo electrónico de envío no se autenticó en el sistema de correo electrónico de recepción. El sistema de correo electrónico de recepción requiere autenticación antes de enviar el mensaje.</p></td>
<td><p>Este error se produce cuando el servidor de recepción debe autenticarse antes del envío de mensajes y el sistema de correo electrónico de envío no se ha autenticado en el sistema de correo electrónico de recepción. El administrador del sistema de correo electrónico de envío debe configurar el sistema para que se autentique en el sistema de correo electrónico de recepción con el fin de que la entrega sea correcta. Este error también se puede producir si intenta aceptar mensajes anónimos de Internet con un servidor de buzones de correo que no esté configurado para hacerlo.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.3</p></td>
<td><p><code>Not Authorized</code></p></td>
<td><p>El remitente prohibió la reasignación al destinatario alternativo.</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


Volver al principio

## Secciones del NDR

En Exchange 2013, los NDR están diseñados para que leerlos y comprenderlos sea una tarea sencilla tanto para los usuarios finales como para los administradores. La información que se muestra en los NDR se distribuye en las siguientes dos secciones:

  - Una sección de información del usuario

  - Una sección de información del administrador

La información de cada sección está destinada a los lectores de dicha sección. La sección de información del usuario aparece primero y contiene comentarios que ayudarán al usuario a comprender, en términos no técnicos, por qué se produjo un error de entrega del mensaje. La sección **Información de diagnóstico para administradores** proporciona información técnica con mayor detalle, como los encabezados del mensaje original, que ayuda a los administradores a solucionar los problemas de entrega. En la figura siguiente se muestra la sección de información del usuario y la sección **Información de diagnóstico para administradores** de un NDR.

**Secciones del NDR**

![NDR que muestra información de diagnóstico de administrador y usuario](images/Bb232118.96245455-5fb9-4669-a931-5563ddd3ab35(EXCHG.150).png "NDR que muestra información de diagnóstico de administrador y usuario")

## Sección de información del usuario

La sección de información del usuario de un NDR generado por Exchange contiene la información que se quiere comunicar a un usuario final que ha enviado un mensaje que, más tarde, se devolvió con un NDR. El texto que aparece en esta sección lo ha insertado el servidor de Exchange que generó el NDR.

El texto de la sección de información del usuario está diseñado para ayudar a los usuarios finales a determinar por qué se rechazó el mensaje y cómo reenviarlo correctamente si es necesario. Si corresponde, en la sección de información del usuario se incluye el nombre de dominio completo del servidor que rechazó el mensaje. Si se produce un error en la entrega a más de un destinatario, se muestra la dirección de correo electrónico de cada destinatario y se incluye el motivo del error en el espacio situado debajo de la dirección de correo electrónico del destinatario.

El texto de la sección de información del usuario se puede modificar con el cmdlet **New-SystemMessage**. Al crear un mensaje personalizado, podrá proporcionar información específica a los usuarios finales, como un número de teléfono para que se pongan en contacto con el departamento de soporte técnico o un hipervínculo para obtener soporte de servicio autónomo.

Volver al principio

## Información de diagnóstico para administradores

La sección **Información de diagnóstico para administradores** contiene información más detallada acerca del error específico producido durante la entrega del mensaje, el servidor que generó el NDR y el servidor que rechazó el mensaje. En la mayoría de los NDR se encuentran los siguientes campos, que se pueden ver en la figura "Secciones del NDR" más arriba en este tema:

  - **Servidor de generación** El servidor de generación es el servidor SMTP que creó el NDR. El servidor de generación toma el código de estado mejorado que se explica más adelante en este tema. Este código crea un NDR fácil de leer. Si no se muestra ningún servidor remoto debajo de la dirección de correo electrónico del remitente en la sección **Información de diagnóstico para administradores**, el servidor de generación también será el servidor que rechazó el mensaje de correo electrónico original. Si el error en la entrega del mensaje se produce cuando este se envía a otro destinatario de la misma organización de Exchange, normalmente el mismo servidor rechaza el mensaje original y genera el NDR.

  - **Destinatario rechazado**   El destinatario rechazado es la dirección de correo electrónico del destinatario donde se produjo el error de entrega del mensaje original. Si se produce un error de entrega a más de un destinatario, aparecen las direcciones de correo electrónico de todos los destinatarios. El campo de destinatario rechazado también contiene los siguientes subcampos para cada una de las direcciones de correo electrónico mostrada:
    
      - **Servidor remoto**   El campo de servidor remoto contiene el FQDN del servidor que rechaza la entrega del mensaje durante la conversación del SMTP. El campo de servidor remoto sólo se llena cuando se ha intentado la entrega a un servidor remoto y ese intento se ha rechazado antes de que el servidor de recepción confirme correctamente el mensaje una vez enviado el cuerpo del mismo. Si el servidor de recepción confirma correctamente el mensaje original y después se rechaza debido a restricciones de contenido, por ejemplo, el campo de servidor remoto no se llena.
    
      - **Código de estado mejorado** El código de estado mejorado es el código que devuelve el servidor que rechazó el mensaje original. Este código de estado mejorado indica el motivo por el que se rechazó el mensaje original. Exchange no vuelve a escribir el código de estado mejorado, pero se usa para determinar qué texto se mostrará en la sección de información del usuario. Los códigos de estado mejorados que encontrará con más frecuencia se enumeran en "Códigos de estado mejorados habituales" más adelante en este tema. Para ver una lista detallada de los códigos de estado mejorados, vea RFC 3463.
    
      - **Respuesta SMTP** La respuesta SMTP es el texto legible para la máquina que devuelve el servidor que rechazó el mensaje original. Normalmente, la respuesta SMTP contiene una cadena corta que proporciona una explicación del código de estado mejorado que también se devuelve. Exchange no vuelve a escribir la respuesta del SMTP. Además, esta respuesta siempre se presenta en formato US-ASCII.

  - **Encabezados del mensaje original**   La sección de encabezados del mensaje original contiene los encabezados del mensaje rechazado. Estos encabezados pueden proporcionar información útil para el diagnóstico; por ejemplo, para determinar la ruta que siguió el mensaje antes de ser rechazado o si el campo **Para** coincide con la dirección de correo electrónico especificada en el campo de destinatario rechazado.

Volver al principio

## Ejemplos de mensajes de NDR

En las siguientes secciones se ofrecen ejemplos de las dos maneras en que se pueden generar mensajes NDR:

  - Por el mismo servidor

  - Por servidores diferentes

## El mismo servidor generó el NDR y rechazó el mensaje original

En el siguiente ejemplo se muestra lo que sucede cuando una organización de correo electrónico remota acepta la entrega de un mensaje de correo electrónico a través de un servidor de transporte perimetral y, después, rechaza el mensaje debido a una directiva de restricción del buzón de correo del destinatario. En este caso, no se permite que el remitente envíe mensajes al destinatario. Los servidores de transporte perimetral no realizan una validación del tamaño del mensaje por lo que, en este ejemplo, el servidor de transporte perimetral acepta el mensaje porque tiene una dirección de destinatario válida y el mensaje no incumple otras restricciones de contenido. Debido a que la organización de correo electrónico remota acepta todo el mensaje, incluido el contenido del mismo, es la responsable de rechazar el mensaje y generar el NDR que se enviará al remitente.

**El mismo servidor generó el NDR y rechazó el mensaje**

![NDR que muestra el mismo servidor de generación y rechazo](images/Bb232118.c9a7cd2d-f35f-4d77-8225-c29585fa3ccd(EXCHG.150).gif "NDR que muestra el mismo servidor de generación y rechazo")

Además, los mensajes que se rechazan cuando se envían a destinatarios que forman parte de la misma organización de Exchange normalmente son rechazados por el mismo servidor de correo electrónico que genera el NDR. Los mensajes enviados a los destinatarios locales se pueden rechazar por varios motivos, entre otros, porque los buzones han superado su cuota, por falta de autorización para enviar mensajes a la dirección del destinatario o por errores de hardware que provocan una pérdida de conectividad con otros servidores de la organización.

En ambos casos, no se incluye ningún servidor remoto bajo la dirección de correo electrónico de los destinatarios listados en el mensaje NDR.

Volver al principio

## El servidor que generó el NDR y el servidor que rechazó el mensaje original son diferentes

En el siguiente ejemplo se muestra lo que sucede cuando una organización de correo electrónico remota rechaza la entrega de un mensaje de correo electrónico antes incluso de aceptar el mensaje. En este ejemplo, el servidor remoto rechaza el mensaje y devuelve un código de estado mejorado al servidor de envío local porque el destinatario especificado no existe. El rechazo se produce antes de que el servidor de recepción confirme el mensaje. Puesto que el servidor de recepción no confirma correctamente el mensaje, no es responsable del mismo. Por lo tanto, el servidor de envío local genera el NDR y lo envía al remitente del mensaje original.

**El servidor que generó el NDR y el servidor que rechazó el mensaje son diferentes**

![NDR que muestra diferentes servidores de generación/envío](images/Bb232118.adfb8d5a-9c1d-4cd9-8a71-ce14224434f8(EXCHG.150).gif "NDR que muestra diferentes servidores de generación/envío")

Volver al principio

## Vea también


[Qué son los NDR de Exchange en Exchange Online y Office 365](https://go.microsoft.com/fwlink/p/?linkid=524931)

