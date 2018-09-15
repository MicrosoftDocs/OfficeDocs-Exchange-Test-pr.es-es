---
title: 'Permitir el Indicador de mensaje en espera: Exchange 2013 Help'
TOCTitle: Permitir el Indicador de mensaje en espera
ms:assetid: 57fb439e-8208-499f-a20b-814677843a8c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298001(v=EXCHG.150)
ms:contentKeyID: 54652437
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permitir el Indicador de mensaje en espera

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-03-09_

El Indicador de mensaje en espera (MWI) es una función incluida en la mayoría de los sistemas de correo de voz heredados. Permite a los usuarios saber si tienen mensajes de correo de voz nuevos o sin escuchar. En su formato más común, esta característica enciende una luz en el teléfono del usuario para indicar la presencia de un mensaje de correo de voz nuevo o no escuchado.

**Contenido**

Información general

El rol del servidor de buzón en MWI

Mensajes de notificación SIP MWI

Resistencia de MWI

Administración de MWI

Notificaciones de mensaje de texto (SMS) para mensajes de correo de voz y llamadas perdidas

## Información general

Las notificaciones MWI pueden incluir cualquier mecanismo que indique la existencia de un mensaje de correo de voz nuevo o no escuchado. El mensaje puede estar en un nuevo mensaje de correo electrónico o uno que está marcado como sin leer. La notificación MWI podría tomar cualquiera de las siguientes formas:

  - Un nuevo mensaje de voz visto desde Microsoft Outlook o desde Outlook Web App.

  - Un mensaje de texto o servicio de mensajes cortos (SMS) enviado a un teléfono móvil configurado para recibir mensajes de texto.

  - Una llamada saliente realizada desde la mensajería unificada de Exchange.

  - Una luz en un teléfono.

  - Un tono de marcado especial.

  - Iconos o botones en la pantalla del teléfono.

  - Una notificación resaltada dentro de una aplicación de software.

En la mensajería unificada, el correo de voz del usuario se almacena en su buzón. Se puede obtener acceso desde un teléfono usando Outlook Voice Access, desde un equipo de escritorio o un equipo portátil usando Outlook o Outlook Web App, y desde clientes de teléfono móvil. Cuando un usuario recibe un nuevo mensaje de voz, el mensaje aparece en la carpeta de búsqueda de correo de voz. Si se obtiene acceso al mensaje de voz usando Outlook o Outlook Web App, se incluirá un mensaje de correo electrónico con el mensaje de voz.

Cuando se implementaban versiones anteriores de la mensajería unificada en una organización, MWI era compatible en un entorno de puerta de enlace VoIP tradicional o un entorno IP-PBX mediante una aplicación o solución de otros fabricantes, o se incluía como parte de la mensajería unificada de Exchange. En Exchange 2010 o posterior, también se admite MWI cuando se implementa la mensajería unificada con Microsoft Lync Server. El mecanismo de notificación MWI utilizado por Lync Server depende del tipo de teléfono basado en VoIP que el usuario habilitado para mensajería unificada y Telefonía IP empresarial utiliza, y puede estar ubicado en cualquiera de los siguientes lugares:

  - Un teléfono

  - Una pantalla de teléfono

  - Un botón de marcado

De manera predeterminada, MWI está activado para todos los usuarios que están habilitados para mensajería unificada. Se controla mediante opciones de configuración en una directiva de buzón de mensajería unificada o en las puertas de enlace IP de mensajería unificada que fueron creadas y vinculadas a un plan de marcado de mensajería unificada. MWI también funciona con mensajes de voz protegidos.

Para implementar MWI en un entorno de telefonía tradicional con puertas de enlace VoIP, IP-PBX, o PBX con SIP habilitado, un servidor de buzón que ejecuta al servicio de mensajería unificada de Microsoft Exchange envía un mensaje de notificación de protocolo de inicio de sesión (SIP) MWI a un *interlocutor SIP*, que es una IP-PBX, una puerta de enlace VoIP utilizada con una PBX heredada, una PBX habilitada para SIP o, si ha implementado Lync Server, los servidores de Lync también se consideran interlocutores SIP. La IP-PBX o PBX enciende la luz en el teléfono de escritorio para notificar al usuario sobre un mensaje de voz nuevo o sin escuchar.

Existen dos maneras para que los autores de llamadas dejen mensajes de voz: mediante contestador automático y Outlook Voice Access. Con el contestador automático, un servidor de buzón contesta una llamada entrante y permite que el autor de la llamada deje un mensaje de voz para un usuario. Con Outlook Voice Access, cuando una persona llama al número de Outlook Voice Access, puede usar el sistema del menú para dejar un mensaje de voz para un usuario habilitado para mensajería unificada.

Información general

## El rol del servidor de buzón en MWI

Cuando una persona llama a un usuario habilitado para mensajería unificada y el usuario no contesta el teléfono, el servicio de mensajería unificada de Microsoft Exchange en un servidor de buzón recibe una información de cambio de estado MWI y usa un mensaje de notificación SIP para enviar la solicitud de un cambio de notificación a una puerta de enlace VoIP, IP-PBX, o PBX habilitada para SIP. El cambio de notificación incluye la siguiente información:

  - Indicador de mensajes en espera habilitado (Sí o No).

  - Cantidad de mensajes de voz nuevos o mensajes de voz marcados como sin escuchar.

  - Cantidad de mensajes de voz viejos o mensajes de voz marcados como escuchados.

  - Cantidad de nuevos mensajes de voz urgentes o mensajes de voz urgentes marcados como sin escuchar.

  - Cantidad de viejos mensajes de voz urgentes o mensajes de voz urgentes marcados como escuchados.

  - El número de extensión primario en el plan de marcado de mensajería unificada primario.

  - La dirección IP o el nombre de dominio completo (FQDN) del interlocutor SIP que se va a usar para los mensajes de notificación SIP.

  - El tipo de seguridad del plan de marcado de mensajería unificada (no protegido, protegido con SIP o protegido). Esta información se utilizará para determinar si la conexión a la puerta de enlace VoIP o IP-PBX debe ser SIP en TCP o SIP en TLS. Se admite la Seguridad de la capa de transporte (TLS) para notificación SIP MWI.

El servidor de buzón usa la información de desvío en el encabezado de la llamada entrante para determinar el número de extensión o número de teléfono del usuario habilitado para mensajería unificada. Cuando se determina el número de teléfono o extensión, el servidor de buzón envía la solicitud al interlocutor SIP. El interlocutor SIP luego cambia el estado MWI y activa la notificación en el teléfono del usuario.


> [!NOTE]
> Aunque son raros los problemas de falta de disponibilidad de PBX, la mensajería unificada actualiza automáticamente el estado MWI para cada buzón al menos una vez cada 12&nbsp;horas. No existe manera de forzar una actualización, pero si la PBX o IP-PBX está apagada y todas las luces MWI se apagan, deben restaurarse todas las luces al estado correcto dentro de las seis horas.



Información general

## Mensajes de notificación SIP MWI

Las notificaciones MWI usan los mensajes de notificación SIP para comunicarse con interlocutores SIP. La información de cambio de estado MWI se incluye en el mensaje de notificación SIP e indica si las notificaciones MWI se enviarán a los usuarios. Cada vez que hay un cambio en el estado MWI, el asistente de buzones envía esta información al servicio de mensajería unificada de Microsoft Exchange que se ejecuta en un servidor de buzón. Después de que el servicio de mensajería unificada recibe esta información, analiza el mensaje para obtener el interlocutor SIP de destino y la información de cambio de estado MWI. Luego forma un mensaje de notificación SIP con la información de cambio de estado MWI en el cuerpo del mensaje y envía esta información al interlocutor SIP.

MWI se basa en RFC 3842. RFC 3842 indica que las notificaciones de evento SIP se deben usar para las notificaciones de mensaje en espera. MWI se basa en el modelo SIP y lo controlan los extremos encontrados en un sistema de mensajería unificada. Los extremos SIP, también denominados interlocutores SIP, que obtienen información de MWI deben enviar un mensaje de suscripción SIP al servicio de mensajería unificada. El servicio responde con un mensaje de notificación que indica que la suscripción fue aceptada. Toda la información de cambio de estado MWI será transmitida desde el sistema de mensajería unificada a un extremo SIP usando los mensajes de notificación incrustados dentro de la suscripción que se creó previamente. La sintaxis exacta del mensaje de notificación SIP que se enviará al interlocutor SIP está basada en el formato que se describe en RFC 3842.

Cuando el servicio de mensajería unificada en un servidor de buzón envía un mensaje de notificación MWI al interlocutor SIP, el encabezado del evento se establece en "resumen del mensaje", lo que indica que este es un mensaje de notificación relacionado con MWI. El campo de encabezado Para indica el extremo SIP para el cual se debe proporcionar el servicio MWI. El encabezado del estado de suscripción se debe establecer en "terminado" en lugar de "activo". Las siguientes acciones tienen lugar en respuesta al mensaje de notificación SIP:

1.  El interlocutor SIP transmite esta información a PBX usando un protocolo de conmutación de circuitos, como SMDI.

2.  PBX envía un mensaje de operación correcta por el protocolo de conmutación de circuitos.

3.  El interlocutor SIP puede responder con cualquiera de los siguientes mensajes: 200 OK (Correcto) o 480 (Temporalmente no disponible). Un servidor de buzón puede encargarse tanto de estas respuestas como de respuestas de error adicionales.

## MWI en un entorno de telefonía tradicional

En un entorno de telefonía tradicional, una llamada entrante es recibida por la PBX y luego enviada a la puerta de enlace VoIP, o es recibida por la IP-PBX o PBX habilitada para SIP. El servidor de buzón y el asistente del buzón se usan para determinar el estado MWI para el usuario habilitado para mensajería unificada. Se encargan de entregar la notificación SIP otra vez a la puerta de enlace VoIP y PBX heredada, IP-PBX o PBX habilitada para SIP.

En un entorno de telefonía tradicional, el flujo de llamadas y la notificación MWI se realizan de la siguiente manera:

1.  La llamada entrante es recibida por la PBX heredada, reenviada a la puerta de enlace VoIP o a una IP-PBX o PBX habilitada para SIP y, luego, reenviada al número de extensión del usuario habilitado para mensajería unificada. El usuario no responde y a la persona que llama se le pide que deje un mensaje de voz.

2.  La puerta de enlace VoIP o IP-PBX envía la llamada al servidor de buzón que ejecuta el servicio de mensajería unificada de Microsoft Exchange.

3.  El servidor de buzón realiza una consulta LDAP para ubicar la información del usuario habilitado para mensajería unificada, como el número de extensión y los saludos personales del usuario. Se reproducen los saludos para el usuario habilitado para mensajería unificada.

4.  El mensaje de voz creado por el servicio de mensajería unificada se envía al servicio de transporte de Microsoft Exchange en el mismo servidor de buzón.

5.  El servicio de transporte en el servidor de buzón envía el mensaje de voz al servidor de buzón que contiene el buzón del usuario. El asistente del buzón recibe un evento MAPI para un nuevo mensaje de voz.

6.  El asistente del buzón lee el plan de marcado de mensajería unificada y la directiva de buzón de mensajería unificada para determinar si las notificaciones de MWI se deben enviar al usuario habilitado para mensajería unificada. El asistente del buzón consulta por todos los servidores de buzón que están asociados con el plan de marcado de mensajería unificada del usuario habilitado para mensajería unificada. El asistente del buzón intenta enviar el evento RPC al primer servidor de buzón que se devolvió. Si se produce un error, intenta con el siguiente. Continuará reintentando por cinco minutos o hasta que se hayan intentado todos los servidores de buzón. Si se produce un error en la llamada de RPC, el asistente del buzón registra el error en el Visor de eventos. El servidor de buzón consulta por todas las puertas de enlace IP de mensajería unificada que están asociadas con el plan de marcado de mensajería unificada del buzón del usuario habilitado para mensajería unificada.

7.  La mensajería unificada envía un mensaje de notificación SIP a la primera puerta de enlace VoIP o IP-PBX que se devolvió desde la consulta. Si se produce un error, el servidor de buzón elegirá la siguiente puerta de enlace VoIP o IP-PBX. El servidor de buzón continuará intentando con una puerta de enlace VoIP o IP-PBX por cinco minutos. Si se producen errores en todos los intentos de encontrar una puerta de enlace VoIP o IP-PBX, el servidor de buzón registrará un error. Si una puerta de enlace VoIP o IP-PBX se ubica correctamente, la puerta de enlace VoIP enviará la notificación a la PBX, y esta, a su vez, enviará una notificación del evento MWI al teléfono del usuario para que se encienda la luz del teléfono. Si se usa una IP-PBX, esta procesará la notificación MWI y luego encenderá la luz del teléfono del usuario. En la sección Introducción, se enumeran otros mecanismos de notificación MWI. El tipo de notificación depende del proveedor de hardware de IP-PBX o PBX y de si se está usando Lync Server. También depende del tipo de teléfono (analógico, digital o VoIP) que se está usando.

Información general

## MWI en un entorno de Lync Server

En entornos de telefonía que incluyen Lync Server, una llamada entrante se puede enviar desde un teléfono externo al servidor de mediación, enviado desde un cliente Lync o desde un teléfono basado en comunicaciones unificadas (UC) o basado en VoIP. Después de que se recibe la llamada, esta se envía al grupo de servidores front-end de Lync Server. El servidor de buzón y el asistente del buzón se usan para determinar el estado MWI para el usuario habilitado para mensajería unificada y para enviar esta notificación al cliente Lync, o teléfono analógico o digital, basado en UC o en VoIP.

En un entorno de telefonía con Lync Server, el flujo de llamadas y la notificación MWI se realizan de la siguiente manera:

1.  La llamada es enviada desde uno de los siguientes puntos:
    
      - Un teléfono externo a la organización (enviado a un servidor de mediación)
    
      - Un cliente basado en Lync
    
      - Un teléfono basado en UC o VoIP

2.  La llamada entrante es recibida por el grupo de servidores front-end de Lync Server y enviada al teléfono o extremo SIP del usuario habilitado para mensajería unificada. El usuario no responde y a la persona que llama se le pide que deje un mensaje de voz.

3.  El grupo de servidores front-end de Lync Server envía la llamada al servidor de buzón dentro de la red local y se encuentra el buzón del usuario.

4.  El servidor de buzón realiza una consulta LDAP para ubicar la información del usuario habilitado para mensajería unificada, como el número de extensión y los saludos. Se reproducen los saludos y a la persona que llama se le pide que deje un mensaje de voz.

5.  El mensaje de voz creado por el servicio de mensajería unificada se envía al servicio de transporte en el mismo servidor de buzón dentro del mismo sitio.

6.  El servicio de transporte envía el mensaje de voz al servidor de buzón que contiene el buzón del usuario. El asistente del buzón recibe un evento MAPI para el nuevo mensaje de voz.

7.  El asistente del buzón lee el plan de marcado de mensajería unificada y la directiva de buzón de mensajería unificada para decidir si las notificaciones de MWI se deben enviar al usuario. El asistente del buzón consulta por todos los servidores de buzón que están asociados con el plan de marcado de mensajería unificada del usuario. El asistente del buzón intenta enviar el evento RPC al primer servidor de buzón que se devolvió. Si se produce un error en el intento, el asistente del buzón intenta con el próximo. Seguirá intentando buscar un servidor de buzón durante cinco minutos o hasta que se hayan probado todos los servidores. Si se produce un error en la llamada de RPC, el asistente del buzón registrará un error en el Visor de eventos. El servidor de buzón consulta en Active Directory por todas las puertas de enlace IP de mensajería unificada que están asociadas con el plan de marcado de mensajería unificada del usuario habilitado para mensajería unificada.

8.  La mensajería unificada envía un mensaje de notificación SIP a la primera puerta de enlace VoIP o IP-PBX que se devolvió desde la consulta. Si se produce un error, el servidor de buzón elegirá la siguiente puerta de enlace VoIP o IP-PBX. El servidor de buzón continuará intentando encontrar una puerta de enlace VoIP o IP-PBX por cinco minutos. Si se producen errores en todos los intentos de comunicarse con la puerta de enlace VoIP o IP-PBX, el servidor de buzón registrará un error. Si se logra, la puerta de enlace VoIP o la IP-PBX enviará la notificación al grupo de servidores front-end de Lync Server, el cual, a su vez, enviará una notificación del evento MWI a un evento de SIP utilizado por el usuario, al teléfono del usuario o a un cliente Lync.

Información general

## Resistencia de MWI

Cuando está implementando servidores de buzón y acceso de cliente, los planes de marcado de mensajería unificada y las puertas de enlace IP de mensajería unificada, y está usando MWI para usuarios habilitados para mensajería unificada, lo mejor es implementar varios servidores de buzón y acceso de cliente al igual que varias puertas de enlace VoIP e IP-PBX para crear tolerancia a errores y resistencia. Esta acción también crea resistencia MWI porque proporciona varias maneras de enviar notificaciones MWI, como se describe en la sección anterior.

Para habilitar la tolerancia a la falla para MWI en la mensajería unificada, debe crear y configurar uno o más de los siguientes elementos:

  - Un plan de marcado de mensajería unificada vinculado con el usuario habilitado para mensajería unificada que recibirá las notificaciones MWI.

  - Una directiva de buzón de mensajería unificada vinculada con el usuario habilitado para mensajería unificada que recibirá las notificaciones MWI.

  - Una puerta de enlace IP de mensajería unificada vinculada con el plan de marcado de mensajería unificada asociado con el usuario habilitado para mensajería unificada que recibirá las notificaciones MWI.

  - Si se usa Lync Server, todos los servidores de acceso de cliente y de buzón deben agregarse al plan de marcado de URI de SIP de mensajería unificada vinculado con el usuario habilitado para mensajería unificada que recibirá las notificaciones MWI.

## Administración de MWI

MWI se puede administrar al realizar las configuraciones en dos componentes de mensajería unificada: Directivas del buzón de mensajería unificada y puertas de enlace IP de mensajería unificada. Para ambos componentes de mensajería unificada, puede habilitar o deshabilitar notificaciones MWI con el cmdlet **Set-UMMailboxPolicy** o el cmdlet **Set-UMIPgateway** en el Shell de administración de Exchange. También puede configurar las opciones mediante el Centro de administración de Exchange (EAC). Puede ver el estado de las notificaciones MWI usando el cmdlet **Get-UMMailboxPolicy** y el cmdlet **Get-UMIPgateway** en el Shell, o viendo las configuraciones en el EAC.

## Directivas de buzón de mensajería unificada y MWI

Puede crear una directiva de buzón de mensajería unificada para aplicar un conjunto común de configuraciones de directivas de mensajería unificada a una serie de buzones de usuarios habilitados para mensajería unificada. Por ejemplo, puede usar una directiva de buzón de mensajería unificada para aplicar las configuraciones de la directiva PIN, limitaciones de marcado y configuraciones de notificaciones MWI. Si habilita o deshabilita MWI en una directiva de buzón de mensajería unificada, se habilitará o deshabilitará para todos los usuarios habilitados para mensajería unificada vinculados con esa directiva de buzón de mensajería unificada. La configuración de MWI también se puede aplicar a un subconjunto de usuarios vinculados con un plan de marcado de mensajería unificada. Para obtener más información sobre las directivas de buzón de mensajería unificada, incluyendo cómo habilitar o deshabilitar el MWI para un grupo de usuarios habilitados para mensajería unificada, vea [Procedimientos de políticas de buzón de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policy-procedures).

Puede usar el EAC o el cmdlet **Set-UMMailboxPolicy** en el Shell para configurar las opciones de MWI, como se muestra en la siguiente tabla.

### Configuración del indicador de mensajes en espera en una directiva de buzón de mensajería unificada

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro del Shell</th>
<th>¿La configuración está disponible en el EAC?</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowMessageWaitingIndicator</em></p></td>
<td><p>Sí</p></td>
<td><p>El parámetro <em>AllowMessageWaitingIndicator</em> especifica si los usuarios que están vinculados con la directiva de buzones de mensajería unificada pueden recibir notificaciones MWI cuando reciben un nuevo mensaje de voz. El valor predeterminado es <code>$true</code>.</p>
<p>Cuando esta configuración está habilitada, las notificaciones MWI se envían a los usuarios vinculados con una sola directiva de buzón de mensajería unificada para llamadas tomadas por una puerta de enlace IP de mensajería unificada. Esta opción permite a la puerta de enlace IP de mensajería unificada recibir y enviar mensajes de notificación SIP a los teléfonos de los usuarios habilitados para la mensajería unificada o los extremos SIP.</p>
<p></p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de cómo administrar las configuraciones de MWI en una directiva de buzón de mensajería unificada, consulte los siguientes temas:

  - [Administrar una directiva de buzones de correo de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy)

  - [Habilitar el indicador de espera de mensaje (MWI) para los usuarios](https://docs.microsoft.com/es-es/exchange/collaboration-exo/public-folders/set-up-exo-hybrid-public-folders)

  - [Deshabilitar el indicador de espera de mensaje (MWI) para los usuarios](https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/manage-dynamic-distribution-groups)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/es-es/library/bb124903\(v=exchg.150\))

## Puertas de enlace IP de mensajería unificada y MWI

Si deshabilita el MWI en una puerta de enlace IP de mensajería unificada, deshabilitará las notificaciones MWI para todos los usuarios que se conectan a la puerta de enlace VoIP o IP-PBX que está representada por la puerta de enlace IP de mensajería unificada. Al deshabilitar MWI en una sola puerta de enlace IP de mensajería unificada vinculada con un plan de marcado de mensajería unificada, se pueden deshabilitar las notificaciones MWI para todos los usuarios habilitados para mensajería unificada con uno o varios planes de marcado de mensajería unificada o con una o varias directivas de buzón de mensajería unificada. Para obtener más información sobre las directivas de buzón de mensajería unificada, incluyendo cómo habilitar o deshabilitar el MWI para un grupo de usuarios habilitados para mensajería unificada, vea [Administrar una directiva de buzones de correo de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy).

Puede usar el EAC o el cmdlet **Set-UMMailboxPolicy** en el Shell para configurar las opciones de MWI, como se muestra en la siguiente tabla.

### Configuración del indicador de mensajes en espera en una puerta de enlace IP de mensajería unificada

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro del Shell</th>
<th>¿La configuración está disponible en el EAC?</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>MessageWaitingIndicatorAllowed</em></p></td>
<td><p>Sí</p></td>
<td><p>El parámetro <em>MessageWaitingIndicatorAllowed</em> especifica si se habilita la puerta de enlace IP de mensajería unificada para permitir que se envíen mensajes de notificación SIP a los usuarios asociados a un plan de marcado de mensajería unificada. El valor predeterminado es <code>$true</code>.</p>
<p>Cuando se habilita esta configuración, se pueden enviar notificaciones de correo de voz a los usuarios para las llamadas que son recibidas por la puerta de enlace IP de mensajería unificada. Esta opción permite a la puerta de enlace IP de mensajería unificada enviar notificaciones de mensaje en espera a los usuarios habilitados para mensajería unificada.</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de cómo administrar las configuraciones de MWI, consulte los siguientes temas:

  - [Administrar una puerta de enlace IP de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/manage-um-ip-gateway)

  - [Permitir el Indicador de mensajes en espera (MWI) en una puerta de enlace IP de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-mwi-on-um-ip-gateway)

  - [Evitar que el indicador de espera de mensaje (MWI) en una puerta de enlace IP de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/prevent-mwi-on-um-ip-gateway)

  - [Set-UMIPGateway](https://technet.microsoft.com/es-es/library/aa996577\(v=exchg.150\))

Información general

## Notificaciones de mensaje de texto (SMS) para mensajes de correo de voz y llamadas perdidas

Como se mencionó antes, una notificación MWI es cualquier mecanismo que indica la existencia de un nuevo mensaje de correo de voz. Además de los mecanismos ya discutidos, los usuarios pueden recibir notificaciones de que tienen un mensaje de voz en espera mediante un mensaje de texto, también conocido como mensaje SMS (servicio de mensajes cortos). Este es un tipo de notificación MWI diferente de la luz tradicional u otros mecanismos para nuevos mensajes de voz.

Se envía un mensaje de texto al teléfono móvil de un usuario cuando el autor de la llamada deja un nuevo mensaje de voz. Los usuarios también pueden recibir un mensaje de texto que los notifica cuando no contestan una llamada telefónica y no se deja un mensaje de voz. El mensaje de texto de notificación de llamada perdida puede enviarse al usuario junto con la notificación de nuevo correo de voz.


> [!NOTE]
> El mensaje de texto que se envía a un usuario incluye una vista previa del correo de voz.



Las notificaciones de mensajes de texto usan una configuración diferente de la configuración MWI en la puerta de enlace IP de mensajería unificada o la directiva de buzón de mensajería unificada. Las notificaciones de mensajes de texto para nuevo correo de voz y llamadas perdidas se configuran en las directivas de buzón de mensajería unificada y en los buzones de mensajería unificada. Puede habilitar o deshabilitar las notificaciones de mensajes de texto mediante el cmdlet **Set-UMMailboxPolicy** y el cmdlet **Set-UMMailbox** en el Shell. Puede ver el estado de las notificaciones de mensajes de texto usando el cmdlet **Get-UMMailboxPolicy** y el cmdlet **Get-UMMailbox**. No es posible configurar notificaciones de mensajes de texto en el EAC.

En la siguiente tabla, se muestra el parámetro en un buzón de mensajería unificada que debe configurarse para que un usuario reciba mensajes de texto para notificaciones de llamadas perdidas y correo de voz.

### Configuración de notificaciones de mensajes de texto en el buzón de un usuario

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>UMSMSNotificationOption</em></p></td>
<td><p>No</p></td>
<td><p>El parámetro <em>UMSMSNotificationOption</em> especifica si un usuario habilitado para mensajería unificada puede recibir notificaciones de mensajes de texto para correo de voz solamente, para correo de voz y llamadas perdidas, o si no va a recibir ningún tipo de notificación. Los valores para este parámetro son <code>VoiceMail</code>, <code>VoiceMailAndMissedCalls</code> y <code>None</code>. El valor predeterminado es <code>None</code>.</p>
<p></p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de cómo administrar las configuraciones de notificación mediante mensajes de texto en el buzón de un usuario, consulte los siguientes temas:

  - [Administrar la configuración de correo de voz para un usuario](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-voice-mail-settings)

  - [Set-UMMailbox](https://technet.microsoft.com/es-es/library/bb124893\(v=exchg.150\))

En la siguiente tabla, se muestra el parámetro en una directiva de buzón de mensajería unificada que debe configurarse para que un usuario reciba mensajes de texto para notificaciones de llamadas perdidas y correo de voz.

### Configuración de notificaciones de mensajes de texto y llamadas perdidas en una directiva de buzón de mensajería unificada

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro del Shell</th>
<th>¿La configuración está disponible en el EAC?</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowSMSNotification</em></p></td>
<td><p>No</p></td>
<td><p>El parámetro <em>AllowSMSNotification</em> especifica si los usuarios habilitados para mensajería unificada cuyos buzones están asociados con la directiva de buzón de mensajería unificada pueden recibir notificaciones de mensajes de texto en sus teléfonos móviles. Si este parámetro se establece como <code>$true</code>, también debe usar el cmdlet <strong>Set-UMMailbox</strong> y establecer el parámetro <em>UMSMSNotificationOption</em> para el usuario habilitado para mensajería unificada en <code>voicemail</code> o <code>VoiceMailAndMissedCalls</code>. El valor predeterminado es <code>$true</code>.</p>
<p></p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de cómo administrar las configuraciones de notificación de mensaje de texto, consulte los siguientes temas:

  - [Administrar una directiva de buzones de correo de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/es-es/library/bb124903\(v=exchg.150\))

Para el correcto funcionamiento de las notificaciones de mensajes de texto para correo de voz y llamadas perdidas, se deben realizar las siguientes tareas:

1.  Use el EAC o el Shell para habilitar el usuario para mensajería unificada y vincularlo a la directiva de buzón de mensajería unificada correcta.

2.  En la directiva de buzón de mensajería unificada vinculada con el usuario, compruebe que el parámetro *AllowSMSNotification* esté establecido como `$true`. Para establecer el parámetro como `$true`, ejecute el siguiente comando: `Set-UMMailboxPolicy -id MyUMMailboxPolicy - AllowSMSNotification $true`.

3.  En el buzón del usuario, habilite las notificaciones de mensajes de texto al establecer el parámetro *UMSMSNotificationOption* en `VoiceMailAndMissedCalls` o `VoiceMail`.

4.  Dado que la configuración predeterminada es `None`, debe ejecutar el siguiente comando del Shell y establecer la opción de notificación de mensaje de texto como `VoiceMailAndMissedCalls` o `VoiceMail`. Por ejemplo: `Set-UMMailbox- -id MyUMMailbox -UMSMSNotificationOption VoiceMailAndMissedCalls`.
    

    > [!IMPORTANT]
    > El parámetro <EM>AllowSMSNotification</EM> en la directiva de buzón de mensajería unificada y el parámetro <EM>UMSMSNotificationOption</EM> en el buzón del usuario deben establecerse como <CODE>$true</CODE> para que funcionen las notificaciones de mensajes de texto.



Además de configurar la directiva de buzón de mensajería unificada y el buzón del usuario para habilitar notificaciones de texto para nuevo correo de voz y llamadas perdidas, el usuario debe habilitar y configurar las notificaciones de mensajes de texto cuando inicia sesión en Outlook Web App. Para establecer y configurar notificaciones de mensajes de texto, haga lo siguiente:

1.  Inicie sesión en Outlook Web App y vaya a **Opciones** \> **Teléfono** \> **Correo de voz**.

2.  En la página **Correo de voz**, dentro de **Notificaciones**, haga clic en **Configurar notificaciones**.

3.  En la página **Mensajería de texto**, haga clic en **Activar notificaciones**.
    

    > [!WARNING]
    > No haga clic en <STRONG>Notificaciones de correo de voz</STRONG> porque, si lo hace, regresará a la página <STRONG>Correo de voz</STRONG>.



4.  En la página **Mensajería de texto**, dentro de **Configuración local**, use la lista desplegable para seleccionar la configuración regional o ubicación del operador de telefonía móvil para mensajería de texto.

5.  En la página **Mensajería de texto**, dentro de **Operador de telefonía móvil**, use la lista desplegable para seleccionar el operador de telefonía móvil para mensajería de texto y, a continuación, haga clic en **Siguiente**.

6.  En la página **Mensajería de texto**, en el cuadro **Escriba el número de teléfono y haga clic en Siguiente**, escriba el número de teléfono móvil utilizado para notificaciones de mensajes de texto y haga clic en **Siguiente**. Se enviará un código de acceso de seis dígitos al teléfono móvil. Si no recibió un código de acceso, haga clic en **No recibí un código de acceso y necesito que me lo reenvíen**.

7.  Escriba el código de acceso en el cuadro **Código de acceso** y luego haga clic en **Finalizar**.

8.  Una vez habilitadas las notificaciones de mensajes de texto, puede hacer clic en **Configurar notificaciones de correo de voz** en la página **Mensajería de texto**. Regresará a la página de correo de voz, donde puede desplazarse hacia abajo hasta la sección **Notificaciones** y configurar las opciones de notificación de mensaje de texto para llamadas perdidas y correo de voz.

Información general

