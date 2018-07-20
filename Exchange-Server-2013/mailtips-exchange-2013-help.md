---
title: 'MailTips: Exchange 2013 Help'
TOCTitle: MailTips
ms:assetid: 9c989167-cc0c-40a6-82ba-383f573bd2d5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ649091(v=EXCHG.150)
ms:contentKeyID: 49895801
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# MailTips

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2017-04-28_

Las sugerencias de correo electrónico son mensajes informativos que se muestran a los usuarios mientras escriben un mensaje. Microsoft Exchange Server 2013 analiza el mensaje, incluida la lista de destinatarios a la que debe enviarse. Si se detecta un posible problema, notifica a los usuarios mediante sugerencias de correo electrónico antes de enviar el mensaje. Con la ayuda de la información brindada por las sugerencias de correo electrónico, los remitentes pueden ajustar el mensaje que están redactando para evitar situaciones no deseadas o informes de no entrega (NDR).

## ¿Cómo funcionan las sugerencias de correo electrónico?

Las sugerencias de correo electrónico se implementan como un servicio web en Exchange 2013. Cuando un remitente redacta un mensaje, el software de cliente realiza una llamada de servicio web de Exchange al servidor de acceso de cliente para obtener la lista de sugerencias de correo electrónico. El servidor responde con la lista de sugerencias de correo electrónico que se aplican al mensaje y el cliente de software muestra la sugerencia de correo electrónico.

Las siguientes situaciones de mensajería innecesaria son comunes en cualquier entorno de mensajería:

  - Los NDR que surgen como consecuencia del envío de mensajes que infringen las restricciones configuradas en una organización, como las restricciones de tamaño de mensaje o el número máximo de destinatarios por mensaje.

  - Los NDR que surgen como consecuencia del envío de mensajes a destinatarios inexistentes, destinatarios restringidos o usuarios con buzones llenos.

  - Envío de mensajes a usuarios con la función de respuestas automáticas configurada.

Todos estos casos incluyen al usuario que envía un mensaje y que espera que este sea entregado, en lugar de recibir una respuesta que indique que el mensaje no ha sido entregado. Incluso, en el mejor de los casos, como la respuesta automática, estos eventos provocan pérdidas de productividad. En el caso de un NDR, esta situación podría resultar en una llamada costosa al Departamento de soporte técnico.

Existen también varios casos en los que el envío de un mensaje no producirá un error, pero podrá causar consecuencias indeseadas, incluso incómodas:

  - Mensajes enviados a grupos de distribución extremadamente grandes.

  - Mensajes enviados a grupos de distribución inapropiados.

  - Mensajes enviados por accidente a destinatarios fuera de la organización.

  - Al seleccionar **Responder a todos** para un mensaje recibido como destinatario en copia oculta (CCO).

Todas estas situaciones problemáticas se pueden mitigar si se les informa a los usuarios sobre las posibles consecuencias de enviar el mensaje mientras se redacta. Por ejemplo, si los remitentes son conscientes de que el tamaño del mensaje que tratan de enviar supera las directivas corporativas, no intentarán enviar ese mensaje. Del mismo modo, si se notifica a los remitentes que el mensaje que envían será entregado a personas fuera de la organización, es más probable que se aseguren de que el contenido y el tono del mensaje sean apropiados.

Los siguientes clientes de mensajería admiten sugerencias de correo electrónico:

  - Outlook Web App

  - Microsoft Outlook 2010 o posterior

## Sugerencias de correo electrónico de Exchange

La siguiente tabla enumera las sugerencias de correo electrónico disponibles en Exchange 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sugerencia de correo electrónico</th>
<th>Disponibilidad</th>
<th>Situación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Destinatario interno no válido</p></td>
<td><p>Outlook</p></td>
<td><p>Se mostrará la sugerencia de correo electrónico Destinatario interno no válido si el remitente agrega un destinatario que aparece como interno a la organización pero que no existe.</p>
<p>Esto podría suceder si el remitente le envía un mensaje a un usuario que ya no es parte de la compañía, pero cuya dirección se resuelve debido a la memoria caché de resolución de nombres o a una entrada en la carpeta Contactos del remitente. También, esto puede suceder si el remitente escribe una dirección SMTP con un dominio para el que Exchange esté autorizado y si la dirección no resuelve para un remitente existente.</p>
<p>La sugerencia de correo electrónico indica el destinatario no válido y brinda al remitente la opción de eliminar el destinatario del mensaje.</p></td>
</tr>
<tr class="even">
<td><p>Buzón de correo lleno</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>La sugerencia de correo electrónico Buzón de correo lleno se muestra si el remitente agrega un destinatario cuyo buzón está lleno y la organización ha implementado una restricción que prohíbe la recepción de mensajes para buzones que hayan sobrepasado un tamaño especificado.</p>
<p>La sugerencia de correo electrónico indica el destinatario cuyo buzón de correo está lleno y brinda al remitente la opción de eliminar el destinatario del mensaje.</p>
<p>La sugerencia de correo electrónico es precisa en el momento de la muestra. Si el mensaje no se envía inmediatamente, la sugerencia de correo electrónico se actualizará cada dos horas. Esta acción también se aplica a los mensajes que fueron guardados en la carpeta Borradores y que se volvieron a abrir después de dos horas.</p></td>
</tr>
<tr class="odd">
<td><p>Respuestas automáticas</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>La sugerencia de correo electrónico de Respuestas automáticas se muestra si el remitente agrega un destinatario que ha activado la función de respuestas automáticas.</p>
<p>La sugerencia de correo electrónico indica que el destinatario tiene activada la respuesta automática y también muestra los primeros 175 caracteres de la respuesta automática configurada por el destinatario.</p>
<p>La sugerencia de correo electrónico es precisa en el momento de la muestra. Si el mensaje no se envía inmediatamente, la sugerencia de correo electrónico se actualizará cada dos horas. Esta acción también se aplica a los mensajes que fueron guardados en la carpeta Borradores y que se volvieron a abrir después de dos horas.</p>
<p>Si una parte de los buzones de correo de usuarios se hospedan en Exchange en línea y coexiste con un escenario Exchange en línea, la configuración en el objeto de dominio remoto que representa la parte remota de su organización tendrá un efecto directo sobre la manera en la que se procesa la sugerencia de correo.</p>
<p>En Exchange 2013, los usuarios pueden configurar respuestas automáticas distintas para los remitentes internos y para los externos. Si el dominio remoto está configurado como un dominio interno (mediante la configuración del parámetro <em>IsInternal</em> en el objeto de dominio remoto hacia <code>$true</code>), la respuesta automática interna se devolverá a todos los usuarios de la organización independientemente de donde resida su buzón de correo. Sin embargo, si el dominio remoto no está configurado como dominio interno, se devolverá una respuesta automática interna a todos los usuarios cuyos buzones de correo se encuentran en el dominio local y se devolverá una respuesta automática externa a los usuarios cuyos buzones de correo se encuentran en el dominio remoto.</p></td>
</tr>
<tr class="even">
<td><p>Personalizado</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>Una sugerencia de correo electrónico personalizada se muestra si el remitente agrega un destinatario para el que se configura una sugerencia de correo electrónico personalizada.</p>
<p>Una sugerencia de correo electrónico personalizada puede ser útil para proporcionar información específica sobre el destinatario. Por ejemplo, es posible crear una sugerencia de correo electrónico personalizada para un grupo de distribución que explique la intención de reducir su mal uso. Para obtener más información, vea <a href="configure-custom-mailtips-for-recipients-exchange-2013-help.md">Configurar las sugerencias de correo electrónico personalizadas para los destinatarios</a>.</p>
<p>De forma predeterminada, las sugerencias de correo electrónico personalizadas no se muestran si el remitente no se encuentra habilitado para enviar un correo electrónico a ese destinatario. En tal caso, se muestra la sugerencia de correo electrónico Destinatario restringido. No obstante, se puede cambiar esta configuración y mostrar la sugerencia de correo electrónico personalizada.</p></td>
</tr>
<tr class="odd">
<td><p>Destinatario restringido</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>La sugerencia de correo electrónico Destinatario restringido se muestra si el remitente agrega un destinatario para el que se configuran restricciones de entrega que prohíben al remitente enviar mensajes.</p>
<p>La sugerencia de correo electrónico señala a aquel destinatario al que el remitente no está habilitado para enviar mensajes y le brinda al remitente la opción de eliminar al destinatario del mensaje. También, informa claramente al remitente de que el mensaje no será entregado si se envía.</p>
<p>Si el destinatario restringido es un destinatario externo o si se encuentra en un grupo de distribución que contiene destinatarios externos, esta información también se le proporcionará al remitente. Sin embargo, se suprimirán las siguientes sugerencias de correo electrónico si corresponde:</p>
<ul>
<li><p>Respuestas automáticas</p></li>
<li><p>Buzón de correo lleno</p></li>
<li><p>Sugerencia de correo personalizada</p></li>
<li><p>Destinatario moderado</p></li>
<li><p>Mensaje sobredimensionado</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Destinatarios externos</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>La sugerencia de correo electrónico Destinatarios externos se muestra si el remitente agrega un destinatario externo o agrega un grupo de distribución que contenga destinatarios externos.</p>
<p>Esta sugerencia de correo electrónico informa a los remitentes si el mensaje que redactan saldrá de la organización. De esta manera, se tomarán decisiones correctas acerca del uso de vocabulario, el tono y el contenido del mensaje.</p>
<p>Esta sugerencia de correo electrónico está desactivada de manera predeterminada. Puede activar esta sugerencia mediante el cmdlet de <strong>Set-OrganizationConfig</strong>. Para obtener información más detallada, vea <a href="mailtips-over-organization-relationships-exchange-2013-help.md">Sugerencias de correo electrónico sobre las relaciones de la organización</a>.</p>
<p>Si una parte de los buzones de correo de usuarios se hospedan en Exchange en línea y coexiste con una situación en línea de Exchange, la configuración en el objeto de dominio remoto que representa la parte remota de su organización tendrá un efecto directo sobre la manera en la que se procesa la sugerencia de correo.</p>
<p>Si el dominio remoto está configurado como un dominio interno (mediante la configuración del parámetro <em>IsInternal</em> en el objeto de dominio remoto hacia <code>$true</code>), los destinatarios de este dominio remoto serán considerados internos y, por lo tanto, no se mostrará la sugerencia de correo Destinatarios externos. Sin embargo, si el dominio remoto no está configurado como dominio interno, los destinatarios de ese dominio serán considerados externos y no se mostrará esta sugerencia de correo cuando se redacte un mensaje a esos destinatarios.</p>

> [!NOTE]
> Esta sugerencia de correo no se evaluará cuando se redacte un mensaje a un grupo de distribución en el dominio remoto.


</td>
</tr>
<tr class="odd">
<td><p>Gran audiencia</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>La sugerencia de correo electrónico Gran audiencia se muestra si el remitente agrega un grupo de distribución que tiene un tamaño mayor al de la gran audiencia configurada en la organización. De forma predeterminada, Exchange muestra esta sugerencia de correo electrónico para mensajes a grupos de distribución que cuentan con más de 25 miembros. Para obtener información detallada, vea <a href="configure-the-large-audience-size-for-your-organization-exchange-2013-help.md">Configurar el tamaño de gran audiencia para su organización</a>.</p>
<p>El tamaño de los grupos de distribución no se calcula todas las veces. En su lugar, se lee la información del grupo de distribución de los datos de métricas de grupo.</p></td>
</tr>
<tr class="even">
<td><p>Destinatario moderado</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>La sugerencia de correo electrónico Destinatario moderado se muestra si el remitente agrega un destinatario que es moderado.</p>
<p>La sugerencia de correo electrónico señala al destinatario moderado e informa al remitente que esta situación puede causar un retraso en la entrega del mensaje.</p>
<p>Si el remitente también es el moderador, no se muestra esta sugerencia de correo electrónico. Tampoco se muestra si el remitente ha sido explícitamente habilitado para enviar mensajes al destinatario (si se agrega el nombre del remitente a la lista Aceptar mensajes solamente de para el destinatario).</p>
<p>Para obtener más información sobre cómo configurar los destinatarios moderados en Exchange 2013, vea <a href="common-message-approval-scenarios-exchange-2013-help.md">Escenarios comunes de aprobación de mensajes</a>.</p>
<p>Para obtener más información sobre cómo configurar los destinatarios moderados en Exchange Online, vea <a href="https://technet.microsoft.com/es-es/library/jj983442(v=exchg.150)">Configurar un destinatario moderado en Exchange Online</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Responder a todos en CCO</p></td>
<td><p>Outlook Web App</p></td>
<td><p>La sugerencia de correo electrónico Responder a todos en CCO se muestra si el remitente recibe una copia oculta de un mensaje y selecciona <strong>Responder a todos</strong>.</p>
<p>Cuando un usuario selecciona <strong>Responder a todos</strong> a un mensaje de esas características, el hecho de que el usuario recibió una copia oculta de ese mensaje se revela al resto de la audiencia a que se le envió el mensaje. En la mayoría de los casos, esta situación en indeseada, y esta sugerencia de correo electrónico informa al usuario sobre esta condición.</p></td>
</tr>
<tr class="even">
<td><p>Mensaje sobredimensionado</p></td>
<td><p>Outlook</p></td>
<td><p>La sugerencia de correo Mensaje sobredimensionado se muestra si el mensaje que el remitente redacta es más grande que los límites de tamaño de mensajes configurados en la organización.</p>
<p>La sugerencia de correo electrónico se muestra si el tamaño del mensaje infringe una de las siguientes restricciones de tamaño:</p>
<ul>
<li><p>Configuración de tamaño máximo de envío en el buzón de correo del remitente</p></li>
<li><p>Configuración de tamaño máximo de recepción en el buzón de correo del destinatario</p></li>
<li><p>Restricción de tamaño máximo de mensaje para la organización</p></li>
</ul>

> [!NOTE]
> Debido a la complejidad de la implementación, no se tienen en cuenta los límites de tamaño de mensajes en los conectores de la organización.


</td>
</tr>
</tbody>
</table>


## Restricciones de las sugerencias de correo electrónico

Las sugerencias de correo electrónico están sujetas a las siguientes restricciones:

  - Las sugerencias de correo electrónico no son compatibles cuando se trabaja en modo sin conexión con Outlook.

  - Cuando un mensaje está dirigido a un grupo de distribución, no se evalúan las sugerencias de correo electrónico para destinatarios individuales que son miembros de ese grupo de distribución. No obstante, si uno de los miembros es un destinatario externo, se muestra la sugerencia de correo electrónico Destinatarios externos. Esta sugerencia muestra al remitente el número de destinatarios externos en el grupo de distribución.

  - Si se envía el mensaje a más de 200 destinatarios, no se evalúan las sugerencias de correo electrónico para buzones individuales por motivos de rendimiento.

  - Las informaciones sobre correo personalizadas tienen un límite de 175 caracteres.

  - Mientras que Exchange 2010 rellenará Sugerencias de correo electrónico en su totalidad, Exchange 2013 solo mostrará hasta 1000 caracteres.

  - Si el remitente comienza a redactar un mensaje y lo deja abierto por un período de tiempo prolongado, se evaluará la sugerencia de correo, las Respuestas automáticas y el Buzón lleno cada dos horas.

