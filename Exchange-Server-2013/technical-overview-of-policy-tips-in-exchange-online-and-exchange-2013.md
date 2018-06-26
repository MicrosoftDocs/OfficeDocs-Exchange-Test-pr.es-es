---
title: Introducción técnica a las sugerencias de directiva en Exchange Online y Exchange 2013
TOCTitle: Sugerencias de directiva
ms:assetid: 4266b83c-dd8a-4b3d-99ff-402e68fc810c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150512(v=EXCHG.150)
ms:contentKeyID: 48267641
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Sugerencias de directiva

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2015-07-22_

Para ayudar a evitar que los usuarios de correo electrónico de Microsoft Outlook Outlook Web App (OWA) y OWA para dispositivos de su organización envíen información confidencial de forma inapropiada, puede crear directivas de prevención de pérdida de datos (DLP) que incluyan mensajes de notificación *Sugerencias de directivas*. Al igual que las sugerencias de correo electrónico incluidas en Microsoft Exchange Server 2010, las sugerencias de directivas son mensajes de notificación que se muestran a los usuarios en Outlook mientras crean un mensaje de correo electrónico. Los mensajes de notificación de sugerencias de directivas sólo aparecen si el mensaje de correo electrónico del remitente parece infringir de alguna manera una directiva de DLP que implementó y dicha directiva incluye una regla para notificar al remitente cuando se cumplen las condiciones que usted estableció. Para obtener más información general acerca de la prevención de pérdida de datos, vea [Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md).

Para mostrar sugerencias de directivas a sus remitentes de correo electrónico, sus reglas deben incluir la acción **Notificar al remitente con una sugerencia de directiva** . Puede agregar este editor de reglas desde el Centro de administración de Exchange. Para obtener más información, vea [Administrar las sugerencias de las directivas](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).

El agente de reglas de transporte que aplica las directivas de DLP no diferencia entre datos adjuntos del mensaje, cuerpo del texto o líneas de asunto al evaluar los mensajes y las condiciones dentro de las directivas. Por ejemplo, si un usuario crea un mensaje de correo electrónico que incluye un número de tarjeta de crédito en el cuerpo del mensaje y luego intenta enviar el mensaje a un destinatario fuera de su organización, se puede mostrar al usuario en Outlook o Outlook Web App un mensaje de notificación de sugerencias de directiva recordándole acerca de las expectativas de la empresa en relación con dicha información. Sin embargo, este tipo de notificación sólo se mostrará si ha configurado una directiva de DLP que restrinja las acciones del ejemplo como se describen; en este caso agregar un alias externo al encabezado de un mensaje con datos de una tarjeta de crédito. Existen una gran variedad de condiciones, acciones y excepciones que puede elegir mientras crea directivas de DLP. Esta variedad le permite personalizar sus esfuerzos de prevención de pérdida de datos de forma que se adapten a las necesidades específicas de su organización.

Cada vez que utilice la acción de notificar al emisor o de sobrescribir en una regla, se recomienda que también incluya la condición de que el mensaje se haya enviado desde su organización. Puede hacerlo si utiliza el editor de reglas de directivas para agregar la condición siguiente: **El remitente se encuentra…**\>**dentro de la organización**. Obtenga más información acerca de cómo cambiar las directivas de DLP existentes en [Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md). Es un procedimiento recomendado porque la acción de notificar al emisor se aplica como parte de la experiencia de creación de mensajes de su empresa. Los emisores a los que hace referencia la acción son los autores de los mensajes de su empresa. Los usuarios no pueden actuar sobre la interacción de usuario que presentan las Sugerencias de directivas para los mensajes entrantes y se omitirá cuando el emisor se encuentre fuera de la organización. Puede aplicar directivas de DLP para explorar los mensajes entrantes y realizar varias acciones. No obstante, al hacerlo, no agregará la acción de notificar al remitente.

Si los remitentes de correo electrónico de su organización que están escribiendo un mensaje son conscientes de sus expectativas de organización y de los estándares en tiempo real a través de las notificaciones de Sugerencias de directivas, es menos probable que infrinjan los estándares que su organización desee aplicar.


> [!NOTE]
> <UL>
> <LI>
> <P>Exchange Online: DLP es una característica premium que requiere una suscripción al plan 2 de Exchange Online. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Licencias de Exchange Online</A>.</P>
> <LI>
> <P>Exchange&nbsp;2013: La prevención de pérdida de datos (DLP) es una característica especial que requiere una licencia de acceso de cliente de empresa (CAL) de Exchange. Para obtener más información sobre las CAL y la emisión de licencias del servidor, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licencias de Exchange Server</A>.</P>
> <LI>
> <P>Si su organización usa Exchange&nbsp;2013 SP1 o Exchange Online, hay disponibles sugerencias de directiva para las personas que envían correo desde Outlook 2013, Outlook Web App o OWA para dispositivos. Sin embargo, si su organización está usando Exchange&nbsp;2013, las sugerencias de directiva solo están disponibles para las personas que envían correo electrónico desde Outlook 2013.</P></LI></UL>



## Texto predeterminado para las sugerencias de directivas y opciones de reglas

Tiene una variedad de opciones posibles al agregar las reglas de notificación del remitente a las directivas de DLP. Cuando agregue una regla para notificar al remitente mediante la acción **Notificar al remitente con una sugerencia de directiva** en una directiva de DLP, puede elegir su grado de restricción. Las opciones de notificación de la siguiente tabla están disponibles. Para obtener información general acerca de las directivas de edición, vea [Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md). Para obtener información más concreta acerca de la creación de sugerencias de directivas, vea [Administrar las sugerencias de las directivas](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Regla de notificación</th>
<th>Significado</th>
<th>Mensaje de notificación de sugerencias de directivas predeterminado que verán los usuarios de Outlook</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Solo notificar</strong></p></td>
<td><p>Al igual que las sugerencias de correo electrónico, esto genera un mensaje de notificación de sugerencias de directivas sobre una infracción de la directiva. Un remitente puede evitar que se muestre este tipo de sugerencia al usar un cuadro de diálogo de opciones de sugerencias de directiva al que se puede acceder en Outlook.</p></td>
<td><p>Este mensaje puede incluir contenido confidencial. Todos los destinatarios deben estar autorizados para recibir este contenido.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rechazar mensaje</strong></p></td>
<td><p>El mensaje no se entregará hasta que la condición haya desaparecido. Se proporciona al remitente una opción para indicar si su mensaje de correo electrónico no incluye contenido confidencial. Esto también se conoce como anulación de falso positivo. Si el remitente indica esto, Outlook permitirá que el mensaje salga de la bandeja de salida de modo que el informe del usuario pueda ser auditado, pero Exchange bloqueará el envío del mensaje.</p></td>
<td><p>Este mensaje puede incluir contenido confidencial. Su organización no permitirá que se envíe este mensaje hasta que se haya quitado el contenido.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rechazar a menos que se anule el falso positivo</strong></p></td>
<td><p>El resultado de esta regla de notificación es similar a la regla de notificación de <strong>Rechazar mensaje</strong>. Sin embargo, si selecciona esto, Exchange permitirá el envío del mensaje al destinatario previsto en lugar de bloquear el mensaje.</p></td>
<td><p><strong>Antes de que el remitente seleccione una opción para anular:</strong> Este mensaje puede incluir contenido confidencial. Su organización no permitirá que se envíe este mensaje hasta que se haya quitado el contenido.</p>
<p><strong>Después de que el remitente selecciona la anulación de una opción:</strong> Se enviarán sus comentarios al administrador cuando se haya enviado el mensaje.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rechazar a menos que se realice la anulación en silencio</strong></p></td>
<td><p>El mensaje no se entregará hasta que la condición haya desaparecido o el remitente indique una anulación. Se suministra al remitente una opción para indicar si desea anular la directiva.</p></td>
<td><p><strong>Antes de que el remitente seleccione una opción para invalidar:</strong> Este mensaje puede incluir contenido confidencial. Su organización no permitirá que se envíe este mensaje hasta que se haya quitado el contenido.</p>
<p><strong>Después de que el remitente selecciona la invalidación de una opción:</strong> Ha invalidado la directiva de la organización por contenido confidencial en este mensaje. Su acción será auditada por la organización.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rechazar a menos que se realice anulación explícita</strong></p></td>
<td><p>El resultado de esta regla de notificación es similar a la regla de notificación <strong>Rechazar a menos que se realice la anulación en silencio</strong>, excepto que en este caso cuando el remitente intenta invalidar la directiva, se le pide que indique el motivo.</p></td>
<td><p><strong>Antes de que el remitente seleccione una opción para invalidar:</strong> Este mensaje puede incluir contenido confidencial. Su organización no permitirá que se envíe este mensaje hasta que se haya quitado el contenido.</p>
<p><strong>Después de que el remitente selecciona la invalidación de una opción:</strong> Ha invalidado la directiva de la organización por contenido confidencial en este mensaje. Su acción será auditada por la organización.</p></td>
</tr>
</tbody>
</table>


## Personalizar los mensajes de notificación de sugerencia de directiva

Para personalizar el texto de una notificación de sugerencia de directiva que ven los remitentes en su programa de correo electrónico, seleccione **Administrar sugerencias de directivas** en la página Prevención de pérdida de datos. Para que cualquier texto personalizado aparezca, una regla de directiva DLP debe incluir la acción **Notificar al remitente con una sugerencia de directiva**. Agregar la acción a una regla mediante el editor de reglas de DLP.

Para procedimientos para explicar cómo crear sus propias sugerencias de directivas, vea [Administrar las sugerencias de las directivas](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md). El texto personalizado que cree puede sustituir el texto predeterminado que se muestra en la tabla anterior.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración y acciones de las notificaciones de sugerencia de directiva</th>
<th>Significado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Notificar al remitente</strong></p></td>
<td><p>El texto solo aparece cuando se inicia una acción <strong>Notificar al remitente, pero permitirle enviar</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Permitir al remitente invalidar</strong></p></td>
<td><p>El texto solo aparece cuando se inician las siguientes acciones: <strong>Bloquear el mensaje a menos que sea un falso positivo</strong>, <strong>Bloquear el mensaje, pero permitir al remitente invalidar y enviar</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Bloquear el mensaje</strong></p></td>
<td><p>El texto solo aparece cuando se inicia una acción <strong>Bloquear el mensaje</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Vincular a una dirección URL de cumplimiento</strong></p></td>
<td><p>La dirección URL de cumplimiento es un vínculo a una página web donde puede explicar su cumplimiento e invalidar las directivas. Este vínculo se muestra en la sugerencia de directiva cuando un usuario hace clic en el vínculo <strong>Más detalles</strong>.</p></td>
</tr>
</tbody>
</table>


## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md)

[Administrar las sugerencias de las directivas](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)

