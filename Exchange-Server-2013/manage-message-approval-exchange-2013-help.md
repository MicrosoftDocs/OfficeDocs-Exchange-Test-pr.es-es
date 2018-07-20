---
title: 'Administrar la aprobación de mensajes: Exchange 2013 Help'
TOCTitle: Administrar la aprobación de mensajes
ms:assetid: 43a89f71-8002-4cb0-b3c8-1c2b2597f227
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd297936(v=EXCHG.150)
ms:contentKeyID: 49895597
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar la aprobación de mensajes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-05-04_

A veces es conveniente echar un segundo vistazo a un mensaje antes de entregarlo. Como administrador de Exchange, puede configurar esto. Este proceso se denomina *moderación* y el aprobador se llama *moderador*. Según qué mensajes necesiten aprobación, puede usar uno de estos dos enfoques:

  - Cambiar las propiedades del grupo de distribución

  - Crear una regla de flujo de correo

En este artículo se explica:

  - Cómo decidir qué método de aprobación usar

  - Cómo funciona el proceso de aprobación

Para obtener información sobre cómo implementar escenarios comunes, vea [Escenarios comunes de aprobación de mensajes](common-message-approval-scenarios-exchange-2013-help.md).

## Cómo decidir qué método de aprobación usar

Esta es una comparación de los dos enfoques para la aprobación de mensajes.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>¿Qué quiere hacer?</th>
<th>Enfoque</th>
<th>Primer paso</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Crear un grupo de distribución moderado donde se deben aprobar todos los mensajes al grupo.</p></td>
<td><p>Configurar la aprobación de mensajes para el grupo de distribución.</p></td>
<td><p>Vaya al Centro de administración de Exchange (EAC) &gt; <strong>Destinatarios</strong>  &gt; <strong> Grupos</strong>, edite el grupo de distribución y seleccione <strong>Aprobación de mensajes</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Requerir la aprobación de los mensajes que cumplan determinados criterios o que se envíen a una persona específica.</p></td>
<td><p>Crear una regla de transporte usando la acción <strong>Reenviar el mensaje para aprobación</strong>.</p>
<p>Puede especificar los criterios de mensaje, incluidos los patrones de texto, remitentes y destinatarios. Los criterios también pueden contener excepciones.</p></td>
<td><p>Vaya a EAC &gt;<strong>Flujo de correo</strong>&gt;<strong>Reglas</strong>.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Cómo funciona el proceso de aprobación

Cuando alguien envía un mensaje a una persona o grupo que requiere aprobación, si están usando Outlook Web Access, se les notificará que su mensaje podría retrasarse.

![Mensaje que muestra la notificación de aprobación de mensaje](images/Dd297936.80e2e5f1-0a1e-4c37-9076-794581155405(EXCHG.150).png "Mensaje que muestra la notificación de aprobación de mensaje")

El moderador recibe un correo electrónico con una solicitud para aprobar o rechazar el mensaje. El texto del mensaje incluye botones para aprobar o rechazar el mensaje y los datos adjuntos incluyen el mensaje original para revisar.

![Mensaje de solicitud de aprobación, incluidos datos adjuntos](images/Dd297936.bf517f5a-b10e-40df-a48a-403b395b5962(EXCHG.150).png "Mensaje de solicitud de aprobación, incluidos datos adjuntos")

El moderador puede realizar una de tres acciones:

![Flujo de trabajo que muestra las opciones de aprobación de un mensaje](images/Dd297936.dc7a6ca9-c67d-487a-8713-4d628e07f4b3(EXCHG.150).png "Flujo de trabajo que muestra las opciones de aprobación de un mensaje")

1.  Si se aprueba, el mensaje va a los destinatarios originales previstos. No se informa al remitente original.

2.  Si se rechaza, se envía un mensaje de rechazo al remitente. El moderador puede agregar una explicación:
    
    ![Aviso de rechazo con comentarios del moderador](images/Dd297936.a663d36a-c67d-4155-b8f6-4b5dc8e105d9(EXCHG.150).png "Aviso de rechazo con comentarios del moderador")  

3.  Si el aprobador elimina o pasa por alto el mensaje de aprobación, se envía un mensaje de expiración al remitente. Esto sucede después de dos días en Exchange Online y después de cinco días en Exchange Server 2013. (En Exchange Server 2013, este período de tiempo se puede cambiar).

El mensaje que está esperando la aprobación se almacena temporalmente en un buzón del sistema llamado *buzón de arbitraje*. Hasta que el moderador decida aprobar o rechazar el mensaje, elimina el mensaje de aprobación o deja que el mensaje de aprobación expire, el mensaje original se conserva en el buzón de arbitraje.

Volver al principio

## Preguntas y respuestas

**¿Cuál es la diferencia entre el aprobador y el propietario de un grupo de distribución?**

El propietario de un grupo de distribución es responsable de administrar la pertenencia al grupo de distribución, pero es posible que no pueda moderar los mensajes que recibe. Por ejemplo, una persona de TI puede ser el propietario de un grupo de distribución llamado Todos los empleados, pero solo el administrador de Recursos humanos puede estar configurado como moderador.

**¿Qué sucede cuando el moderador o el aprobador envían un mensaje al grupo de distribución?**

El mensaje va directamente al grupo, pasando por alto el proceso de aprobación.

**¿Qué ocurre cuando solo un subconjunto de destinatarios necesita aprobación?**

Puede enviar un mensaje a un grupo de destinatarios y que solo un subconjunto de ellos necesite aprobación. Considere un mensaje que se envía a 12 destinatarios, uno de los cuales es un grupo de distribución moderado. El mensaje se divide automáticamente en dos copias. Un mensaje se entrega inmediatamente a los 11 destinatarios que no necesitan aprobación, y el segundo mensaje se envía al proceso de aprobación para el grupo de distribución moderado. Si un mensaje está dirigido a más de un destinatario moderado, se crea automáticamente una copia diferente del mensaje para cada destinatario moderado y cada copia pasa por el proceso de aprobación correspondiente.

**¿Qué sucede si mi grupo de distribución contiene destinatarios moderados que requieren aprobación?**

Un grupo de distribución puede incluir destinatarios moderados que también necesitan aprobación. En este caso, después de que el mensaje del grupo de distribución es aprobado, se produce un proceso de aprobación independiente para cada destinatario moderado que es miembro del grupo de distribución. Sin embargo, también puede habilitar la aprobación automática de los miembros del grupo de distribución después de que se aprueba el mensaje para el grupo de distribución moderado. Para hacerlo, use el parámetro *BypassNestedModerationEnabled* en el cmdlet [Set-DistributionGroup](https://technet.microsoft.com/es-es/library/bb124955\(v=exchg.150\)).

**¿Este proceso es diferente si tenemos nuestros propios servidores de Exchange?**

De forma predeterminada, se usa un buzón de arbitraje para cada organización de Exchange. Si tiene sus propios servidores de Exchange y necesita más buzones de arbitraje para equilibrar la carga, siga las instrucciones para agregar buzones de arbitraje en [Administrar y solucionar problemas de aprobación de mensajes](manage-and-troubleshoot-message-approval-exchange-2013-help.md). Los buzones de arbitraje son buzones del sistema y no necesitan una licencia de Exchange.


> [!NOTE]
> <STRONG>Si tiene Exchange 2007:</STRONG> Microsoft Exchange Server 2007 no es compatible con los destinatarios moderados. Si un mensaje enviado a un grupo de distribución moderado se amplía en un servidor de transporte de concentradores de Exchange 2007, el mensaje omitirá la moderación y se entregará a todos los miembros del grupo de distribución. Si tiene servidores de transporte de concentradores de Exchange 2007 en su organización de Exchange, deberá designar un servidor de buzones de correo de Exchange Server 2013 como servidor de ampliación para los grupos de distribución moderados. Esto garantiza que todos los mensajes enviados al grupo de distribución sean moderados.



Volver al principio

## ¿Necesita más información?

[Administrar reglas de flujo de correo](manage-mail-flow-rules-exchange-2013-help.md)

[Guía de referencia rápida del Shell de administración de Exchange para Exchange 2013](exchange-management-shell-quick-reference-for-exchange-2013-exchange-2013-help.md)

[Exchange Online PowerShell](https://technet.microsoft.com/es-es/library/jj200677\(v=exchg.150\))

