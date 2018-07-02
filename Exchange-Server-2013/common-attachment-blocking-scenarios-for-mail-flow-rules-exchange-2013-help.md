---
title: 'Escenarios comunes de bloqueo de datos adjuntos: Exchange 2013 Help'
TOCTitle: Escenarios comunes de bloqueo de datos adjuntos
ms:assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn950026(v=EXCHG.150)
ms:contentKeyID: 65207674
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Escenarios comunes de bloqueo de datos adjuntos

 

_**Se aplica a:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Última modificación del tema:** 2017-02-23_

Es posible que su organización necesite bloquear o rechazar determinados tipos de mensajes con el fin de cumplir requisitos legales o de cumplimiento normativo, o bien para satisfacer necesidades empresariales específicas. Aquí se incluyen algunos ejemplos de escenarios comunes para el bloqueo de todos los datos adjuntos que puede configurar mediante reglas de transporte en Exchange:

  -  
    Example 1: Block messages with attachments, and notify the sender

  -  
    Example 2: Notify intended recipients when an inbound message is blocked

  -  
    Example 3: Modify the subject line for notifications

  -  
    Example 4: Apply a rule with a time limit

Para obtener más ejemplos de cómo bloquear datos adjuntos concretos, consulte:

  - [Usar reglas de transporte para inspeccionar datos adjuntos de mensajes](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013)

  - [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/es-es/library/jj919236\(v=exchg.150\)) (Exchange Online, Exchange Online Protection)

El filtro de malware incluye un filtro de tipos comunes de datos adjuntos. En Centro de administración de Exchange (CEF), vaya a **Protección** y, después, haga clic en **Nuevo** (![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")) para agregar filtros. En el portal de Exchange Online, vaya a **Protección** y, después, seleccione **Filtro de malware**.

Para empezar a implementar cualquiera de estos escenarios para bloquear determinados tipos de mensajes:

1.  Inicie sesión en Centro de administración de Exchange.

2.  Vaya a **Flujo de correo** \>**Reglas**.

3.  Seleccione **Nuevo** (![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")) y seleccione **Crear una nueva regla**.

4.  En el cuadro **Nombre**, especifique un nombre para la regla y después haga clic en **Más opciones**.

5.  Seleccione las condiciones y las acciones que desee.

**Nota:**  En CEF, 1 kilobyte es el tamaño de archivo más pequeño que se puede adjuntar. Por lo tanto, debería detectar la mayoría de los datos adjuntos. Sin embargo, si desea que se detecten todos los posibles datos adjuntos de cualquier tamaño, deberá usar PowerShell para ajustar el tamaño de los datos adjuntos a 1 byte tras crear la regla en CEF. Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)).Para obtener información sobre cómo usar Windows PowerShell para conectarse a Exchange Online, vea [Conexión a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).Para obtener información sobre cómo usar Windows PowerShell para conectarse a Protección de Exchange Online, vea [Conexión a PowerShell de Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=627290).

Reemplace *\<Rule Name\>* por el nombre de la regla existente y ejecute el comando siguiente para establecer el tamaño de los datos adjuntos en 1 byte:

    Set-TransportRule -Identity "<Rule Name>" -AttachmentSizeOver 1B

Después de ajustar el tamaño de los datos adjuntos a 1 byte, el valor que se muestra para la regla en CEF es **0,00 KB**.

## Ejemplo 1: Bloquear mensajes con datos adjuntos y notificar al remitente

Si no desea que las personas de su organización envíen o reciban datos adjuntos, configure una regla de transporte para bloquear todos los mensajes que incluyan datos adjuntos.

En este ejemplo se bloquean todos los mensajes con datos adjuntos enviados o recibidos por la organización.

![Regla que bloquea todos los datos adjuntos](images/Dn950026.38094183-166f-4ba5-a9cf-242e7d0f4e04(EXCHG.150).png "Regla que bloquea todos los datos adjuntos")

Si solo desea bloquear el mensaje, quizá le interese detener el procesamiento de reglas una vez que la regla coincida. Desplácese hacia abajo por el cuadro de diálogo de la regla y seleccione la casilla **Detener el procesamiento de más reglas**.

## Ejemplo 2: Notificar a los destinatarios cuando se bloquea un mensaje entrante

Si desea rechazar un mensaje e informar al destinatario de lo ocurrido, use la acción **Notificar al destinatario con un mensaje**.

Puede utilizar marcadores de posición en el mensaje de notificación para que incluya información sobre el mensaje original. Los marcadores de posición deben encerrarse entre dos signos de porcentaje (%). Cuando se envía el mensaje de notificación, los marcadores de posición se reemplazan con la información del mensaje original. En el mensaje también puede usar HTML básico como \<br\>, \<b\>, \<i\> e \<img\>.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Tipo de información</strong></p></td>
<td><p><strong>Marcador de posición</strong></p></td>
</tr>
<tr class="even">
<td><p>Remitente del mensaje.</p></td>
<td><p>%%From%%</p></td>
</tr>
<tr class="odd">
<td><p>Destinatarios que aparecen en la línea &amp;quot;Para&amp;quot;.</p></td>
<td><p>%%To%%</p></td>
</tr>
<tr class="even">
<td><p>Destinatarios que aparecen en la línea &amp;quot;Cc&amp;quot;.</p></td>
<td><p>%%Cc%%</p></td>
</tr>
<tr class="odd">
<td><p>Asunto del mensaje original.</p></td>
<td><p>%%Subject%%</p></td>
</tr>
<tr class="even">
<td><p>Encabezados del mensaje original. Esto es similar a la lista de encabezados en una notificación de estado de entrega (DSN) que se genera para el mensaje original.</p></td>
<td><p>%%Headers%%</p></td>
</tr>
<tr class="odd">
<td><p>Fecha en que se envió el mensaje original.</p></td>
<td><p>%%MessageDate%%</p></td>
</tr>
</tbody>
</table>


En este ejemplo, se bloquean todos los mensajes que contienen datos adjuntos y se envían a personas de su organización. Además, el destinatario recibe una notificación.

![Regla que notifica a los destinatarios que se ha bloqueado un mensaje entrante](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Regla que notifica a los destinatarios que se ha bloqueado un mensaje entrante")

## Ejemplo 3: Modificar la línea de asunto para las notificaciones

Cuando se envía una notificación al destinatario, la línea de asunto es el asunto del mensaje original. Si desea modificar al asunto para que le resulte más claro al destinatario, debe usar dos reglas de transporte:

  - La primera regla agrega la palabra \&quot;undeliverable\&quot; (no se puede entregar) al principio del asunto de los mensajes con datos adjuntos.

  - La segunda regla bloquea el mensaje y envía un mensaje de notificación al remitente con el nuevo asunto del mensaje original.


> [!IMPORTANT]
> Las dos reglas deben tener condiciones idénticas. Las reglas se procesan por orden, por lo que la primera regla agrega la palabra &amp;quot;undeliverable&amp;quot; y la segunda regla bloquea el mensaje y notifica al destinatario.



Así sería la primera regla si deseara agregar \&quot;undeliverable\&quot; en el asunto:

![Regla que antepone "No se puede entregar" a los mensajes con datos adjuntos](images/Dn950026.2552b0bd-c69d-48b4-9e69-267fcaf20e70(EXCHG.150).png "Regla que antepone \"No se puede entregar\" a los mensajes con datos adjuntos")

Y la segunda regla realiza el bloqueo y la notificación (la misma regla del ejemplo 2):

![Regla que notifica a los destinatarios que se ha bloqueado un mensaje entrante](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Regla que notifica a los destinatarios que se ha bloqueado un mensaje entrante")

## Ejemplo 4: Aplicar una regla con un límite de tiempo

Si experimenta un ataque de malware, quizá desee aplicar una regla con un límite de tiempo para bloquear temporalmente los datos adjuntos. Por ejemplo, la siguiente regla tiene un día y una hora de inicio y finalización:

![Regla que muestra un límite de tiempo](images/Dn950026.bdc8c4d8-72fa-4c5b-97f2-5fe76d50e643(EXCHG.150).png "Regla que muestra un límite de tiempo")

## Vea también


[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)  


[Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\))  
[Reglas de flujo de correo (reglas de transporte) en Exchange Online Protection](https://technet.microsoft.com/es-es/library/dn271424\(v=exchg.150\))

