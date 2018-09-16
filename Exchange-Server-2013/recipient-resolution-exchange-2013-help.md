---
title: 'Resolución de destinatarios: Exchange 2013 Help'
TOCTitle: Resolución de destinatarios
ms:assetid: 09deda5a-d405-45b1-a3ff-fefd3d76cdea
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb430743(v=EXCHG.150)
ms:contentKeyID: 52062001
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Resolución de destinatarios

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-03-17_

La *resolución de destinatarios* es el proceso de expandir la lista de destinatarios y resolver todos los destinatarios de un mensaje. La acción de resolver destinatarios hace coincidir un destinatario con el objeto de Active Directory correspondiente de la organización de Microsoft Exchange. La acción de expandir destinatarios expande todos los grupos de distribución en una lista de destinatarios individuales. La resolución de destinatarios permite que se apliquen correctamente límites de mensajes y destinatarios alternativos a cada destinatario.

En una organización de Microsoft Exchange Server 2013, la resolución de destinatarios la hace el categorizador del servicio de transporte de los servidores de buzones de correo. La categorización se produce en los mensajes cuando se coloca un mensaje recién llegado en la cola de envío. La resolución de mensajes, además del enrutamiento y la conversión de contenido, se lleva a cabo en el mensaje antes de colocarlo en una cola de entrega. El categorizador realiza la resolución de destinatarios antes del enrutamiento. El componente del categorizador responsable de la resolución de destinatarios se suele denominar *resolución*.

**Contenido**

Resolución de alto nivel

Expansión

Bifurcación y control de la expansión de destinatarios

Diagnóstico de resolución de destinatarios

## Resolución de alto nivel

La *resolución de alto nivel* es la primera etapa de la resolución de destinatarios. La resolución de alto nivel asocia cada destinatario de un mensaje entrante con un objeto de destinatario coincidente en Active Directory. Durante la resolución de alto nivel, el categorizador crea una lista que contiene las direcciones de correo del remitente y del destinatario inicial sin expandir que se encuentran en el mensaje. Luego el categorizador usa esa lista de direcciones de correo para consultar a Active Directory y buscar los objetos habilitados para correo que tengan atributos de dirección de correo coincidentes. Cuando se encuentra una coincidencia, las propiedades de los objetos de Active Directory que coinciden se almacenan en la caché para su uso posterior. También se aplican las restricciones de mensajes del remitente.

## Direcciones de correo de destinatarios

La resolución de alto nivel empieza con un mensaje y la lista de destinatarios inicial sin expandir del *sobre del mensaje*. El sobre del mensaje contiene los comandos que se usan para transmitir mensajes entre servidores de mensajería SMTP. La dirección de correo del remitente se incluye en el comando **MAIL FROM:**  diferente. La dirección de correo de cada destinatario se incluye en un comando **RCPT TO:**  independiente diferente. El remitente y los destinatarios del sobre se crean, normalmente, a partir del remitente y los destinatarios de los campos de encabezado `To:`, `From:`, `Cc:` y `Bcc:` del encabezado del mensaje. No obstante, esto no siempre es así. Los campos de encabezado `To:`, `From:`, `Cc:` y `Bcc:` de un mensaje se pueden manipular con facilidad y es posible que no coincidan con las direcciones de correo del remitente o de los destinatarios originales que se usaron para transmitir el mensaje.

## Direcciones de correo encapsuladas

Las direcciones de correo SMTP estándar siguen las especificaciones de RFC 2821 y RFC 2822, como, por ejemplo, chris@contoso.com. Sin embargo, una dirección de correo también puede ser una dirección de correo no SMTP que está encapsulada dentro de una dirección SMTP válida. Exchange admite direcciones encapsuladas que usan el método de encapsulación Internet Mail Connector Encapsulated Address (IMCEA).

Este método de encapsulación requiere la codificación de los caracteres que no sean válidos en las direcciones de correo SMTP. Los caracteres alfanuméricos, el signo igual (=) y el guión (-) no requieren codificación. Otros caracteres usan la siguiente sintaxis de codificación:

  - La barra diagonal (/) se sustituye por un guión bajo (\_).

  - Otros caracteres US-ASCII se sustituyen por un signo más (+) y los dos dígitos del valor ASCII se escriben en formato hexadecimal. Por ejemplo, el carácter de espacio tiene el valor codificado `+20`.

El método de encapsulación IMCEA usa la sintaxis siguiente: `IMCEA<Type>-<address>@<domain>`

El marcador de posición \<*Type*\> identifica el tipo de dirección no SMTP, por ejemplo, `EX`, `X400` o `FAX`.


> [!NOTE]
> Pese a que, teóricamente, <CODE>SMTP</CODE> y <CODE>X500</CODE> son valores válidos para &lt;<EM>Type</EM>&gt;, la resolución de destinatarios de Exchange&nbsp;rechaza todas las direcciones codificadas con IMCEA que usan alguno de estos tipos.



El marcador de posición \<*address*\> es la dirección original codificada. El marcador de posición \<*domain*\> representa al dominio SMTP que se usa para encapsular la dirección no SMTP, por ejemplo, contoso.com

Con el método de encapsulación IMCEA, las direcciones solo se desencapsulan cuando el dominio coincide con el dominio autoritativo predeterminado de la organización de Exchange. Para obtener más información acerca de los dominios aceptados, vea [Dominios aceptados](accepted-domains-exchange-2013-help.md).

La longitud máxima para una dirección de correo SMTP en Exchange es de 571 caracteres. Este límite incluye lo siguiente:

  - 315 caracteres para el nombre de la dirección

  - 255 caracteres para el nombre de dominio

  - El carácter arroba (@) que separa el nombre de la dirección del nombre de dominio

Recuerde que Exchange no admite mensajes codificados con el método de encapsulado IMCEA cuando la parte del nombre de la dirección supera los 315 caracteres aunque la dirección completa tenga menos de 571 caracteres.

## Resolución de dirección

En cada mensaje, las direcciones de correo del remitente y los destinatarios se agregan a una lista que se usa para consultar a Active Directory. Antes de agregarlas a la lista de direcciones de correo, las direcciones encapsuladas se desencapsulan. La consulta de Active Directory se realiza en un máximo de 20 direcciones a la vez. Si la consulta de Active Directory encuentra algún error temporal, el mensaje se devuelve a la cola de envío y se aplaza durante el tiempo especificado por la clave *ResolverRetryInterval* del archivo de configuración de la aplicación XML `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` asociado al servicio de transporte de Microsoft Exchange. El valor predeterminado es de 30 minutos.

En la tabla siguiente se describen los objetos de destinatario que se encuentran en Active Directory. Para más información sobre los tipos de destinatario de Exchange, vea [Destinatarios](recipients-exchange-2013-help.md).

### Objetos de destinatario en Active Directory

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de destinatario de Active Directory</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DistributionGroup</p></td>
<td><p>Cualquier objeto de grupo habilitado para correo. Los tipos de objeto de grupo de distribución son:</p>
<ul>
<li><p><strong>MailUniversalDistributionGroup</strong>    un objeto de grupo de distribución universal</p></li>
<li><p><strong>MailUniversalSecurityGroup</strong>   Un objeto de grupo de seguridad universal (USG) que tiene una dirección de correo</p></li>
<li><p><strong>MailNonUniversalGroup</strong>   Un objeto de grupo de seguridad local o un objeto de grupo de seguridad global que tiene una dirección de correo</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DynamicDistributionGroup</p></td>
<td><p>Un objeto que tiene la clase <strong>msExchDynamicDistributionList</strong> de Active Directory. Para obtener más información, vea <a href="https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/add-an-auto-attendant-extension-number">Administrar grupos de distribución dinámica</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p>Un objeto de usuario que tiene una dirección de correo y un parámetro <em>Database</em> definido</p></td>
</tr>
<tr class="even">
<td><p>MailUser</p></td>
<td><p>Un objeto de usuario que tiene una dirección de correo sin un parámetro <em>Database</em> definido. Para obtener más información, vea <a href="https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-mail-users">Administrar usuarios de correo</a>.</p></td>
</tr>
<tr class="odd">
<td><p>MailContact</p></td>
<td><p>Un objeto de contacto que tiene una dirección de correo. Por lo general, los contactos de correo se usan para destinatarios que no pertenecen a la organización de Exchange. Los contactos de correo también se usan en entornos entre bosques de Exchange. Para obtener más información, vea <a href="https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-mail-contacts">Administrar contactos de correo</a>.</p></td>
</tr>
<tr class="even">
<td><p>MailPublicFolder</p></td>
<td><p>Un objeto de carpeta pública que tiene una dirección de correo.</p></td>
</tr>
<tr class="odd">
<td><p>MicrosoftExchangeRecipient</p></td>
<td><p>Un objeto que tiene la clase <strong>msExchExchangeServerRecipient</strong> de Active Directory. Para más información sobre el objeto de destinatario de Microsoft Exchange, vea <a href="recipients-exchange-2013-help.md">Destinatarios</a>.</p></td>
</tr>
<tr class="even">
<td><p>SystemAttendantMailbox</p></td>
<td><p>Un objeto que tiene la clase <strong>exchangeAdminService</strong> de Active Directory. La organización de Exchange solo debe tener un buzón de operador de sistema.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox</p></td>
<td><p>Un objeto de usuario que tiene una dirección de correo y que se encuentra en el contenedor Objetos de sistema de Microsoft Exchange. La organización de Exchange solo debe tener un buzón de sistema para cada base de datos de buzones de correo.</p></td>
</tr>
</tbody>
</table>


La consulta de Active Directory clasifica como objetos no válidos los objetos que contienen propiedades esenciales incorrectas o que carecen de ellas. Por ejemplo, un objeto de grupo de distribución dinámica sin una dirección de correo no se considera válido. Los mensajes que se envían a destinatarios clasificados como objetos no válidos generan un informe de no entrega (NDR).

Para cada dirección de correo, se hace una única consulta inicial de todas las propiedades de destinatario posibles, como los identificadores de destinatario, el tipo de destinatario, los límites de mensaje, las direcciones de correo y los destinatarios alternativos. Las propiedades aplicables al destinatario se almacenan en la memoria caché para su uso en el futuro. La resolución de destinatarios clasifica a los destinatarios en función de las similitudes a la hora de resolver los destinatarios y la similitud de las propiedades de destinatario aplicables.

El filtro LDAP que se usa para la resolución de direcciones se describe a continuación:

  - En el caso del tipo de dirección de correo **EX**, el filtro LDAP se basa en el atributo de destinatario de Active Directory **legacyExchangeDN** o en el atributo de destinatario de Active Directory **proxyAddresses**. El atributo **legacyExchangeDN** de Active Directory tiene prioridad.

  - En los demás tipos de direcciones de correo, se usa el atributo de destinatario de Active Directory **proxyAddresses** como filtro LDAP.

Si la dirección de correo usada en el mensaje no coincide con la dirección principal SMTP del objeto correspondiente de Active Directory, el categorizador reescribe la dirección en el mensaje para que coincida con la dirección principal SMTP. La dirección original se guarda en la entrada `ORCPT=` en el comando **RCPT TO:**  en el sobre del mensaje.

## Restricciones de mensajes del remitente

El tamaño que se usa para la restricción de tamaño de los mensajes del remitente es el valor del campo de encabezado **X-MS-Exchange-Organization-OriginalSize:**  el campo de encabezado del encabezado del mensaje. Exchange usa este campo de encabezado para registrar el tamaño original que tenía el mensaje al entrar en la organización de Exchange. Siempre que se comprueban los límites de los mensajes indicados con respecto al mensaje, se usa el valor más bajo del tamaño del mensaje actual o el encabezado del tamaño del mensaje original. El tamaño del mensaje puede cambiar debido a la conversión del contenido, la codificación y el procesamiento de agentes. Si este campo de encabezado no existe, se crea mediante el valor de tamaño del mensaje actual. Si el mensaje es demasiado grande, se genera un NDR y se detiene el procesamiento adicional del mensaje.

El límite de destinatarios del remitente solo se aplica en el servicio de transporte del primer servidor de buzones de correo que procesa el mensaje. El recuento original de destinatarios en el sobre del mensaje sin expandir se compara con el límite de destinatarios del remitente. El recuento original de destinatarios en el sobre del mensaje sin expandir se usa para evitar los problemas de entrega parcial de mensajes que se producen en Microsoft Exchange Server 2003 cuando las listas de distribución anidadas usan servidores de expansión remotos.

El remitente del mensaje y todos los destinatarios se marcan como resueltos con un sellado de propiedad extendida en el mensaje. Esta propiedad extendida permite que el mensaje omita la resolución de nivel superior en caso de que deba volver a pasar por la resolución de destinatarios. Es posible que un mensaje deba volver a pasar por la resolución de destinatarios si se reinicia el servicio de transporte de Microsoft Exchange.

Volver al principio

## Expansión

La expansión se realiza después de la resolución de nivel superior. La expansión expande totalmente los niveles anidados de destinatarios en destinatarios individuales. La expansión puede requerir varios recorridos por el proceso de expansión para expandir todos los destinatarios. No es necesario expandir todos los destinatarios. No obstante, todos los destinatarios deben pasar por el proceso de expansión. El proceso de expansión también aplica restricciones de mensajes de destinatarios para todos los tipos de destinatarios.

En la lista siguiente se describen los tipos de destinatarios que requieren expansión:

  - **Grupos de distribución y grupos de distribución dinámica**   Los grupos de distribución se expanden de acuerdo con la propiedad **memberOf** de Active Directory. Los grupos de distribución dinámica se expanden usando la definición de la consulta de Active Directory. Si el parámetro *ExpansionServer* está establecido en el grupo, el servidor actual no expande el grupo. El grupo de distribución se enruta hacia el servidor especificado para la expansión.
    

    > [!NOTE]
    > Si selecciona un servidor de transporte concreto de la organización como servidor de expansión, el uso del grupo de distribución dependerá de la disponibilidad del servidor de expansión. Si el servidor de expansión no está disponible, no podrá entregarse ningún mensaje que se envíe al grupo de distribución. Si tiene pensado usar servidores de expansión específicos para sus grupos de distribución, de manera que se reduzca el riesgo de interrupción del servicio, deberá tener en cuenta la implementación de soluciones de alta disponibilidad para dichos servidores.



  - **Destinatarios alternativos**   El parámetro *ForwardingAddress* se puede establecer en buzones y en carpetas públicas habilitadas para correo. El parámetro *ForwardingAddress* redirige todos los mensajes al destinatario alternativo especificado. Este destinatario se conoce como *destinatario reenviado*. Cuando se especifica una dirección de entrega alternativa en el parámetro *ForwardingAddress* y el parámetro *DeliverToMailboxAndForward* está establecido en `$true`, el mensaje se entrega al destinatario original y al destinatario alternativo. Este destinatario se conoce como *destinatario entregado y reenviado*.

  - **Cadenas de contacto**   Una *cadena de contacto* es un usuario o contacto de correo que tiene el parámetro *ExternalEmailAddress* establecido en la dirección de correo de otro destinatario de la organización de Exchange.

## Detección de bucles de destinatarios

Cuando los grupos de distribución, los destinatarios alternativos y las cadenas de contactos se expanden, el categorizador busca *bucles de destinatarios*. Un bucle de destinatarios es un problema de configuración de destinatarios que provoca la entrega de un mensaje a los mismos destinatarios en un círculo infinito. En la lista siguiente se describen los diferentes tipos de bucles de destinatarios:

  - **Bucle de destinatarios inofensivo**   Un bucle de destinatarios inofensivo deriva en la correcta entrega de los mensajes. En la lista siguiente se describen dos situaciones en las que se producen bucles de destinatarios inofensivos.
    
      - Cuando dos grupos de distribución se contienen el uno al otro como miembros.
    
      - Cuando los buzones o carpetas públicas habilitadas para correo están establecidos para entregar y reenviar mensajes entre sí. Esto sucede cuando el parámetro *DeliverToMailboxAndForward* de ambos destinatarios se establece en `$true` y el parámetro *ForwardingAddress* se establece en uno a otro.
    
    Cuando se detecta un bucle de destinatarios inofensivo, el mensaje se entrega al destinatario, pero no se vuelve a intentar la entrega del mensaje al mismo destinatario.

  - **Bucle de destinatarios roto**   Un bucle de destinatarios roto no entrega los mensajes correctamente. Un ejemplo de un bucle de destinatarios roto se produce cuando los buzones o las carpetas públicas habilitadas para correo tienen el parámetro *ForwardingAddress* establecido en uno a otro. Cuando el categorizador detecta un bucle de destinatario roto, la actividad de expansión del destinatario actual se detiene y se genera un NDR para el destinatario.

La detección de bucles de destinatarios no evita la entrega de mensajes duplicados. Por ejemplo, el grupo de distribución C sufrirá la entrega de mensajes duplicados si se cumplen las siguientes condiciones:

  - Los grupos de distribución B y C son miembros del grupo de distribución A.

  - El grupo de distribución C también es miembro del grupo de distribución B.

## Redirección de informes de entrega para grupos de distribución

Cuando se expande un grupo de distribución, se comprueba el tipo de mensaje para determinar si se trata de un mensaje de informe de entrega. Si se trata de un informe de entrega, se comprueba la configuración de redirección del grupo de distribución para determinar si es necesario redireccionar el informe de entrega. Es recomendable eliminar los informes de entrega, pues pueden revelar información no deseada acerca del grupo de distribución y sus miembros.

En la lista siguiente se describen las configuraciones de redirección del informe de entrega disponibles para los grupos de distribución y los grupos de distribución dinámica:

  - **ReportToManagerEnabled**   Este parámetro habilita los informes de entrega para enviarlos al administrador del grupo de distribución. Los valores válidos son `$true` o `$false`. El valor predeterminado es `$false`. Para un grupo de distribución, el administrador se controla mediante el parámetro *ManagedBy* del cmdlet **Set-Group**. Para un grupo de distribución dinámico, el administrador se controla mediante el parámetro *ManagedBy* del cmdlet **Set-DynamicDistributionGroup**.

  - **ReportToOriginatorEnabled**   Este parámetro permite que los informes de entrega se envíen al remitente de los mensajes de correo que se envían a este grupo de distribución. Los valores válidos son `$true` o `$false`. El valor predeterminado es `$true`.
    

    > [!NOTE]
    > El valor del parámetro <EM>ReportToManagerEnabled</EM> y el valor del parámetro <EM>ReportToOriginatorEnabled</EM> no pueden ser <CODE>$true</CODE>. Si un parámetro está establecido como <CODE>$true</CODE>, el otro deberá estar establecido como <CODE>$false</CODE>. Los valores de ambos parámetros pueden ser <CODE>$false</CODE>. De esta manera, se elimina la redirección de todos los mensajes de informes de entrega.



En la lista siguiente se describen los mensajes de informes de entrega disponibles:

  - **Confirmación de entrega (DR)**   Este informe confirma que un mensaje se ha entregado al destinatario previsto.

  - **Notificación de estado de entrega (DSN)**   Este informe describe el resultado de un intento de entrega de un mensaje. Para obtener más información acerca de los mensajes DSN, vea [DSN y NDR en Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

  - **Notificación de estado de mensaje (MDN)**   Este informe describe el estado de un mensaje después de su correcta entrega a un destinatario. Un mensaje MDN puede ser una notificación de lectura (RN) o una notificación de no lectura (NRN), por ejemplo. Los mensajes MDN se definen en RFC 2298 y los controla el campo de encabezado **Disposition-Notification-To:**  el campo de encabezado del encabezado del mensaje. La configuración de MDN que usa el campo de encabezado `Disposition-Notification-To:` es compatible con muchos servidores de mensajes diferentes. La configuración de MDN también se puede definir con propiedades MAPI en Microsoft Outlook y Exchange.

  - **Informe de no entrega (NDR)**   Este informe indica al remitente del mensaje que el mensaje no se ha podido entregar a los destinatarios especificados.

  - **Notificación de no lectura (NRN)**   Este informe indica que un mensaje se ha eliminado antes de leerlo.

  - **Fuera de la oficina (OOF)**   Este informe indica que el destinatario no responderá a mensajes de correo. El acrónimo OOF se remonta al sistema de mensajería original de Microsoft, donde la notificación correspondiente se llamaba "out of facility" (fuera de las instalaciones)

  - **Notificación de lectura (RN)**   Este informe indica que un mensaje se ha leído.

  - **Informe de recuperación**   Este informe indica el estado de una solicitud de recuperación para un destinatario determinado. Una solicitud de recuperación se produce cuando un remitente intenta recuperar un mensaje enviado con Outlook.

Cuando se envía un mensaje de informe de entrega a un grupo de distribución, las siguientes configuraciones provocan la eliminación del mensaje del informe:

  - La redirección del informe no está establecida, o la redirección del informe está establecida en el remitente del mensaje.

  - La redirección del informe se establece en el administrador del grupo de distribución y el mensaje de informe de entrega no es un NDR.

Cuando se envía un mensaje de informe de entrega a un grupo de distribución, el mensaje de informe de entrega se puede enviar al administrador del grupo de distribución. Esto sucede cuando la redirección del informe se establece para el administrador del grupo de distribución y el mensaje de informe es un NDR.

Cuando se envía un mensaje que no es un informe de entrega a un grupo de distribución, el mensaje se entrega a los miembros del grupo de distribución. En la lista siguiente se resume la configuración de la solicitud del informe:

  - Si la redirección del informe está establecida en el remitente del mensaje, la configuración de la solicitud del informe no se modifica.

  - Si la redirección del informe no está establecida, se elimina toda la configuración de la solicitud del informe. La entrada `NOTIFY=NEVER` se agrega a **RCPT TO:**  para todos los destinatarios del sobre del mensaje.

  - Si la redirección del informe está establecida en el administrador del grupo de distribución, se elimina toda la configuración de la solicitud del informe, excepto los mensajes NDR que se envían al administrador del grupo de distribución.

## Restricciones de mensajes de los destinatarios

El proceso de expansión también aplica las restricciones de mensajes que están configuradas para los destinatarios. Estas restricciones se pueden configurar individualmente para cada destinatario u organizativamente para todos los servidores de transporte de concentradores de la organización de Exchange. La tabla siguiente describe las restricciones de mensajes que se configuran para los destinatarios.

### Restricciones de mensajes de los destinatarios

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origen</th>
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-TransportConfig</strong></p></td>
<td><p><em>MaxReceiveSize</em></p></td>
<td><p>El parámetro <em>MaxReceiveSize</em> especifica que el tamaño que se usa para las restricciones del mensaje que se configuran para los destinatarios es el valor del campo de encabezado <strong>X-MS-Exchange-Organization-OriginalSize:</strong> el campo de encabezado del encabezado del mensaje. Exchange usa este campo de encabezado para registrar el tamaño original que tenía el mensaje al entrar en la organización de Exchange. Siempre que se comprueban los límites de tamaño de los mensajes indicado con respecto al mensaje, se usa el valor más bajo del tamaño del mensaje actual o el encabezado del tamaño del mensaje original. El tamaño del mensaje puede cambiar debido a la conversión del contenido, la codificación y el procesamiento de agentes. Si este campo de encabezado no existe, se crea mediante el valor de tamaño del mensaje actual. Si el mensaje es demasiado grande, se genera un NDR y se detiene el procesamiento adicional del mensaje.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em></p></td>
<td><p>El parámetro <em>RequireSenderAuthenticationEnabled</em> requiere que todos los mensajes que se envíen al destinatario provengan de remitentes autenticados. Si el valor del parámetro está establecido en <code>$true</code>, los mensajes de remitentes no autenticados se rechazan. Todos los remitentes que envíen mensajes a los buzones del sistema y del operador del sistema deben estar autenticados.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em></p>
<p><em>RejectMessagesFromSendersOrMembers</em></p></td>
<td><p>El parámetro <em>AcceptMessagesOnlyFromSendersOrMembers</em> especifica los grupos de remitentes o de distribución cuyos miembros están autorizados a enviar mensajes a este destinatario. Recuerde que este parámetro combina las funciones de los antiguos parámetros <em>AcceptMessagesOnlyFrom</em> y <em>AcceptMessagesOnlyFromDLMembers</em>.</p>
<p>El parámetro <em>RejectMessagesFromSendersOrMembers</em> especifica los remitentes o grupos de distribución cuyos miembros no están autorizados a enviar mensajes a este destinatario. Recuerde que este parámetro combina las funciones de los antiguos parámetros <em>RejectMessagesFrom</em> y <em>RejectMessagesFromDLMembers</em>.</p>
<p>El categorizador comprueba el permiso del destinatario en dos fases. La primera fase determina si el remitente se encuentra en el parámetro <em>AcceptOnlyMessagesFromSendersOrMembers</em> o <em>RejectMessagesFromSendersOrMembers</em>. Si el remitente no se encuentra en ninguno de los parámetros, los grupos de distribución de estos parámetros se expanden completamente. La expansión completa de los grupos de distribución puede tardar cierto tiempo. Es recomendable minimizar la profundidad de los grupos de distribución anidados en estos parámetros.</p></td>
</tr>
</tbody>
</table>


Algunos tipos de mensajes enviados por remitentes autenticados no están sujetos a estas restricciones. En la lista siguiente se describen los mensajes que no están sujetos a restricciones de destinatarios:

  - **Todos los mensajes que envía el destinatario de Microsoft Exchange** Estos mensajes son mensajes DSN, informes de diarios, mensajes de cuota y otros mensajes generados por el sistema que se envían a remitentes de mensajes internos. Para más información sobre el destinatario de Microsoft, vea [Destinatarios](recipients-exchange-2013-help.md).

  - **Todos los mensajes enviados desde la dirección del administrador de correo externo**   Estos mensajes son mensajes DSN y otros mensajes generados por el sistema que se envían a remitentes de mensajes externos. Para obtener más información acerca de la dirección del administrador de correo externo, vea [Configurar la dirección externa del postmaster](configure-the-external-postmaster-address-exchange-2013-help.md).

Algunos tipos de mensajes se bloquean cuando se envían desde la organización de Exchange a dominios externos. La configuración se controla mediante los parámetros siguientes del cmdlet **Set-RemoteDomain**:

  - *AllowedOOFType*

  - *AutoForwardEnabled*

  - *AutoReplyEnabled*

  - *DeliveryReportEnabled*

  - *NDREnabled*

Para obtener más información, vea [Dominios remotos](remote-domains-exchange-2013-help.md).

Volver al principio

## Bifurcación y control de la expansión de destinatarios

Debido a que la resolución de destinatarios resuelve y expande la lista completa de destinatarios del mensaje, a veces es necesario crear varias copias del mismo mensaje. Las siguientes situaciones ejemplifican estos casos:

  - **Cuando los destinatarios del mensaje requieren diferentes configuraciones de mensaje**   Es posible que las propiedades de los mensajes, como las confirmaciones de lectura, deban estar habilitadas para algunos destinatarios y bloqueadas para otros. La creación de una nueva versión del mensaje con propiedades ligeramente diferentes a las del mensaje original se llama *bifurcación*.

  - **Para limitar el número de destinatarios del sobre en un solo mensaje**   El proceso de expansión de destinatarios puede generar miles de destinatarios cuando se expanden grupos de distribución grandes. En Exchange, en vez de crear una sola copia del mensaje con miles de destinatarios del sobre, se crean varias copias del mismo mensaje con un número limitado de destinatarios del sobre.

## Bifurcación

La resolución de destinatarios bifurca un mensaje si se dan las siguientes condiciones:

  - Si el remitente del mensaje que aparece en **MAIL FROM:** , en el sobre del mensaje, está actualizado. Esto ocurre, por ejemplo, cuando el parámetro *ReportToManagerEnabled* de un grupo de distribución tiene el valor `$true`.

  - Si deben eliminarse los mensajes de respuesta automática, como los mensajes DSN, OOF y de informes de recuperación.

  - Si se expanden los destinatarios alternativos.

  - Cuando un campo de encabezado **Resent-From:**  debe agregarse al encabezado del mensaje. Los campos de encabezado de reenvío son de tipo informativo y se pueden usar para determinar si un usuario ha reenviado un mensaje. Los campos de encabezado de reenvío se usan para que el mensaje se muestre al destinatario como si el remitente original lo hubiese enviado directamente. El destinatario puede ver el encabezado del mensaje para saber quién ha reenviado el mensaje. Los campos de encabezado de reenvío se definen en la sección 3.6.6 de RFC 2822.

  - Si debe transmitirse el historial de expansiones del grupo de distribución.

## Control de la expansión de destinatarios

Si el número de destinatarios expandidos es demasiado grande, el categorizador divide el mensaje en varias copias. De esta manera, se reduce el uso de los recursos del sistema durante la expansión de mensajes. El número máximo de destinatarios del sobre de un mensaje se controla con la clave *ExpansionSizeLimit* del archivo de configuración de aplicación `%ExchangeInstallPath%Bin\EdgeTransport.exe.config`. El valor predeterminado es 1000.


> [!WARNING]
> No es recomendable modificar el valor de la clave <EM>ExpansionSizeLimit</EM> en un servidor de transporte de Exchange en un entorno de producción.



Volver al principio

## Diagnóstico de resolución de destinatarios

La información de diagnóstico y los informes de la resolución de destinatarios se proporcionan en los contadores de rendimiento y las entradas de registros de seguimiento de mensajes. Esta información puede ayudarle a identificar y diagnosticar los problemas de resolución de destinatarios.

## Contadores de rendimiento de resolución de destinatarios

En la tabla siguiente se describen los contadores de rendimiento que están disponibles para la resolución de destinatarios.

### Contadores de rendimiento de resolución de destinatarios

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del contador</th>
<th>Nombre para mostrar</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AmbiguousRecipientsTotal</p></td>
<td><p>Destinatarios ambiguos</p></td>
<td><p>Se trata del número total de destinatarios ambiguos que se detectaron durante la resolución de destinatarios. Los destinatarios ambiguos son diferentes destinatarios que tienen atributos coincidentes <strong>legacyExchangeDN</strong> de Active Directory o atributos coincidentes <strong>proxyAddresses</strong> de Active Directory.</p></td>
</tr>
<tr class="even">
<td><p>AmbiguousSendersTotal</p></td>
<td><p>Remitentes ambiguos</p></td>
<td><p>Se trata del número total de remitentes ambiguos que se detectaron durante la resolución de destinatarios. Los remitentes ambiguos son diferentes remitentes que tienen atributos coincidentes <strong>legacyExchangeDN</strong> de Active Directory o atributos coincidentes <strong>proxyAddresses</strong> de Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p>FailedRecipientsTotal</p></td>
<td><p>Destinatarios erróneos</p></td>
<td><p>Se trata del número total de destinatarios erróneos que se detectaron durante la resolución de destinatarios.</p></td>
</tr>
<tr class="even">
<td><p>LoopRecipientsTotal</p></td>
<td><p>Destinatarios de bucle</p></td>
<td><p>Se trata del número total de destinatarios que no superaron la resolución de destinatarios debido a bucles de destinatarios.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesChippedTotal</p></td>
<td><p>Mensajes procesados</p></td>
<td><p>Se trata del número total de copias del mismo mensaje que se crearon durante la resolución de destinatarios para controlar el número de destinatarios del sobre en un solo mensaje. En Exchange, este proceso se conoce como <em>división</em>.</p></td>
</tr>
<tr class="even">
<td><p>MessagesCreatedTotal</p></td>
<td><p>Mensajes creados</p></td>
<td><p>Se trata del número total de mensajes que se crearon durante la resolución de destinatarios.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesRetriedTotal</p></td>
<td><p>Mensajes reintentados</p></td>
<td><p>Se trata del número total de mensajes que estaban programados para su reintento durante la resolución de destinatarios.</p></td>
</tr>
<tr class="even">
<td><p>UnresolvedOrgRecipientsTotal</p></td>
<td><p>Destinatarios sin resolver de la organización</p></td>
<td><p>Se trata del número total de destinatarios sin resolver de un dominio autoritativo que se detectaron durante la resolución de destinatarios.</p></td>
</tr>
<tr class="odd">
<td><p>UnresolvedOrgSendersTotal</p></td>
<td><p>Remitentes sin resolver de la organización</p></td>
<td><p>Se trata del número total de remitentes sin resolver de un dominio autoritativo que se detectaron durante la resolución de destinatarios.</p></td>
</tr>
</tbody>
</table>


## Eventos de resolución de destinatarios en el registro de seguimiento de mensajes

En la tabla siguiente se describen los eventos de resolución de destinatarios que se escribieron en el registro de seguimiento de mensajes.

### Eventos de resolución de destinatarios en el registro de seguimiento de mensajes

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evento de seguimiento de mensajes</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EXPAND</p></td>
<td><p>Este evento indica que se ha expandido un grupo de distribución.</p></td>
</tr>
<tr class="even">
<td><p>REDIRECT</p></td>
<td><p>Este evento indica que un mensaje enviado al destinatario de un buzón de correo o al destinatario de una carpeta pública habilitada para correo se redirigió a un destinatario alternativo, tal como especificaba el parámetro <em>ForwardingAddress</em>.</p></td>
</tr>
<tr class="odd">
<td><p>RESOLVE</p></td>
<td><p>Este evento indica que se ha cambiado la dirección de correo de un destinatario por la dirección de correo SMTP principal del objeto de destinatario de Active Directory correspondiente.</p></td>
</tr>
<tr class="even">
<td><p>TRANSFER</p></td>
<td><p>Este evento indica que un mensaje se ha bifurcado o dividido.</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de seguimiento de mensajes, vea[Seguimiento de mensajes](message-tracking-exchange-2013-help.md).

