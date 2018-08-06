---
title: 'Reconfigurar direcciones servidores transporte perimetral: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Reconfiguración de direcciones en los servidores de transporte perimetral
ms:assetid: 23f1eaf6-247a-4671-ad72-aae19d9b511d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996806(v=EXCHG.150)
ms:contentKeyID: 61061232
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Reconfiguración de direcciones en los servidores de transporte perimetral

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

La reconfiguración de direcciones modifica las direcciones de correo electrónico de los remitentes y destinatarios en los mensajes que entran o salen de la organización a través de un servidor Transporte perimetral. Dos agentes de transporte en el servidor Transporte perimetral proporcionan la funcionalidad de reconfiguración: el agente de reconfiguración de direcciones en entrada y agente de reconfiguración de direcciones en salida. El objetivo principal de la reconfiguración de direcciones en mensajes salientes es presentar un dominio de correo electrónico único y coherente a los destinatarios externos. El objetivo principal de la reconfiguración de direcciones en mensajes entrantes es entregar los mensajes al destinatario correcto.

La *entrada de reescritura de direcciones*, que se crea, especifica las direcciones internas (las direcciones de correo electrónico que desea cambiar) y las direcciones externas (las direcciones de correo electrónico finales que desea). Puede especificar si las direcciones de correo electrónico se vuelve a escribir en los mensajes entrantes y salientes, o bien solamente en los mensajes salientes. Puede crear entradas de reescritura de direcciones para un solo usuario (chris@contoso.com a support@contoso.com), todos los usuarios en un solo dominio (contoso.com a fabrikam.com) o para los usuarios en varios subdominios con excepciones (\*.fabrikam.com a contoso.com, excepto legal.fabrikam.com).


> [!IMPORTANT]
> Independientemente de cómo piensa usar la reconfiguración de direcciones, necesita comprobar que las direcciones de correo electrónico resultantes sean únicas en la organización para terminar con duplicados. Esto se debe a que la reconfiguración de direcciones no comprueba la unicidad de una dirección de correo electrónico reconfigurada.



**Contenido**

Escenarios para la reconfiguración de direcciones

Propiedades de mensajes modificadas mediante la reconfiguración de direcciones

Lo que no cambia la reconfiguración de direcciones

Consideraciones sobre la reconfiguración de direcciones solo salientes

Consideraciones sobre la reconfiguración de direcciones entrantes y salientes

Consideraciones sobre la reconfiguración de direcciones de correo electrónico en varios dominios

Prioridad de las entrada de reescritura de direcciones

Mensajes firmados digitalmente, cifrados y protegidos por derechos

## Escenarios para la reconfiguración de direcciones

Los siguientes escenarios son ejemplos de cómo se puede usar la reconfiguración de direcciones:

  - **Consolidación de grupos**   Algunas organizaciones segmentan sus negocios internos en dominios independientes basados en requisitos técnicos o de negocio. Esta configuración puede hacer que los mensajes de correo electrónico aparezcan como si procedieran de grupos diferentes o incluso de organizaciones diferentes.
    
    En el siguiente ejemplo se muestra cómo una organización, Contoso, Ltd., puede ocultar sus subdominios internos de los destinatarios externos:
    
      - Los mensajes salientes de los dominios northamerica.contoso.com, europe.contoso.com y asia.contoso.com se vuelven a escribir para que parezca como si procedieran de un único dominio contoso.com. Todos los mensajes se vuelven a escribir como si pasaran por servidores de transporte perimetral que proporcionan conectividad SMTP entre toda la organización e Internet.
    
      - El servidor Transporte perimetral retransmite a un servidor de buzones de correo los mensajes entrantes para los destinatarios de contoso.com. El mensaje se entrega al destinatario correcto según la dirección de proxy que está configurada en el buzón del destinatario.

  - **Fusiones y adquisiciones**   Una empresa adquirida puede seguir funcionando como una empresa independiente, pero se puede usar la reconfiguración de direcciones para hacer que las dos organizaciones parezcan una sola organización integrada.
    
    En el siguiente ejemplo se muestra cómo Contoso, Ltd. puede ocultar el dominio de correo electrónico de la empresa Fourth Coffee recientemente adquirida:
    
      - Contoso, Ltd. desea que parezca que todos los mensajes salientes de la organización de Exchange de Fourth Coffee se hubieran originado desde contoso.com. Todos los mensajes de ambas organizaciones se envían a través de los servidores de transporte perimetral de Contoso, Ltd., donde se vuelven a escribir los mensajes de correo electrónico de *usuario*@fourthcoffee.com a *usuario*@contoso.com.
    
      - Los mensajes entrantes para *usuario*@contoso.com se vuelven a escribir y se enrutan a los buzones de *usuario*@fourthcoffee.com. Los mensajes entrantes que se envían a *usuario*@fourthcoffee.com se enrutan directamente a los servidores de correo electrónico de Fourth Coffee.

  - **Socios**   Muchas organizaciones usan socios externos para proporcionar servicios a sus clientes, otras organizaciones o a la misma organización. Para evitar la confusión, la organización puede reemplazar el dominio de correo electrónico de la organización del socio con su propio dominio de correo electrónico.
    
    En el siguiente ejemplo se muestra cómo Contoso, Ltd. puede ocultar un dominio de correo electrónico del socio:
    
      - Contoso, Ltd. proporciona soporte técnico a una organización mayor, la Wingtip Toys. Wingtip Toys desea una experiencia de correo electrónico unificada para sus clientes y necesita que parezca que todos los mensajes del personal de soporte técnico de Contoso, Ltd. se hubieran enviado desde Wingtip Toys. Todos los mensajes salientes relacionados con Wingtip Toys se envían mediante sus servidores de transporte perimetral y todas las direcciones de correo electrónico de contoso.com se vuelven a escribir para que parezcan direcciones de wingtiptoys.com.
    
      - Los servidores de transporte perimetral de Wingtip Toys aceptan los mensajes entrantes de soporte@wingtiptoys.com, estos se vuelven a escribir y, a continuación, se enrutan a la dirección de correo electrónico soporte@contoso.com.

Volver al principio

## Propiedades de mensajes modificadas mediante la reconfiguración de direcciones

Un mensaje de correo electrónico SMTP estándar está compuesto por el *sobre del mensaje* y el contenido del mensaje. El sobre del mensaje contiene información necesaria para la transmisión y la entrega del mensaje entre los servidores de correo SMTP. El contenido del mensaje contiene el cuerpo del mensaje y campos de encabezado de mensaje, que se denominan de forma colectiva *encabezado del mensaje*. El sobre del mensaje se describe en RFC 2821 y el encabezado del mensaje se describe en RFC 2822.

Cuando un emisor redacta un mensaje de correo electrónico y lo envía para su entrega, el mensaje contiene la información básica necesaria para el cumplimiento de los estándares SMTP, como el remitente, un destinatario, la fecha y la hora de redacción del mensaje, una línea de asunto opcional y un cuerpo del mensaje también opcional. Esta información está contenida en el propio mensaje y, por definición, en el encabezado del mensaje.

El servidor de correo del remitente genera un sobre del mensaje para el mensaje con la información del remitente y el destinatario que se encuentra en el encabezado del mensaje. Después transmite el mensaje a Internet para su entrega al servidor de correo del destinatario. Los destinatarios nunca ven el sobre del mensaje porque lo genera el proceso de transmisión del mensaje y no forma parte del mensaje.

La reconfiguración de direcciones cambia una dirección de correo electrónico volviendo a escribir campos específicos en el encabezado del mensaje o el sobre del mensaje. La reconfiguración de direcciones cambia varios campos en los mensajes salientes, pero solo un campo en los mensajes de correo electrónico entrantes. En la tabla siguiente se muestran los campos con encabezado SMTP que se vuelven a escribir en los mensajes entrantes y salientes.

### Campos de mensaje reconfigurados en los mensajes entrantes y salientes

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del campo</th>
<th>Ubicación</th>
<th>Mensajes salientes</th>
<th>Mensajes entrantes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MAIL FROM</strong></p></td>
<td><p>Sobre del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
<tr class="even">
<td><p><strong>RCPT TO</strong></p></td>
<td><p>Sobre del mensaje</p></td>
<td><p>No reescrito</p></td>
<td><p>Reescrito</p></td>
</tr>
<tr class="odd">
<td><p><strong>To</strong></p></td>
<td><p>Encabezado del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
<tr class="even">
<td><p><strong>CC</strong></p></td>
<td><p>Encabezado del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
<tr class="odd">
<td><p><strong>From</strong></p></td>
<td><p>Encabezado del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
<tr class="even">
<td><p><strong>Sender</strong></p></td>
<td><p>Encabezado del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reply-To</strong></p></td>
<td><p>Encabezado del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
<tr class="even">
<td><p><strong>Return-Receipt-To</strong></p></td>
<td><p>Encabezado del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
<tr class="odd">
<td><p><strong>Disposition-Notification-To</strong></p></td>
<td><p>Encabezado del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
<tr class="even">
<td><p><strong>Resent-From</strong></p></td>
<td><p>Encabezado del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
<tr class="odd">
<td><p><strong>Resent-Sender</strong></p></td>
<td><p>Encabezado del mensaje</p></td>
<td><p>Reescrito</p></td>
<td><p>No reescrito</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Lo que no cambia la reconfiguración de direcciones

La reconfiguración de direcciones no modifica ningún campo de encabezado de mensaje que podría provocar un mal funcionamiento de SMTP. Por ejemplo, modificar algunos campos de encabezado podría afectar a la detección de bucles de enrutamiento, invalidar la firma o hacer ilegible el mensaje protegido por derechos. Por lo tanto, la reconfiguración de direcciones no modifica los siguientes campos de encabezado.

  - **Return-Path**

  - **Received**

  - **Message-ID**

  - **X-MS-TNEF-Correlator**

  - **Content-Type Boundary=string**

  - Encabezados que se encuentran en las partes del cuerpo MIME

La reconfiguración de direcciones omite los dominios que no están controlados mediante la organización de Exchange. En otras palabras, la reconfiguración de direcciones no vuelve a escribir campos de encabezado que contienen dominios para los cuales la organización de Exchange no es autoritativa. La reconfiguración de dichos dominios podría causar una forma no controlable de retransmisión de mensajes.

La reconfiguración de direcciones tampoco modifica los campos de encabezado de los mensajes que están incrustados en otro mensaje. Los remitentes y los destinatarios esperan que los mensajes incrustados permanezcan intactos y se entreguen sin modificaciones, siempre que no desencadenen reglas de transporte que se implementen entre el remitente y el destinatario.

Volver al principio

## Consideraciones sobre la reconfiguración de direcciones solo salientes

La reconfiguración de direcciones solo salientes en un servidor Transporte perimetral modifica la dirección de correo electrónico del remitente cuando el mensaje sale de la organización de Exchange. Puede configurar la reconfiguración de direcciones solo salientes para un solo usuario (chris@contoso.com a support@contoso.com) o para todos los usuarios en un solo dominio (contoso.com a fabrikam.com). Es necesario configurar la reconfiguración de direcciones solo salientes para los usuarios en varios subdominios (\*.fabrikam.com a .contoso.com).

La dirección de correo electrónico reconfigurada debe configurarse como dirección proxy en los destinatarios afectados. Por ejemplo, si laura@sales.contoso.com se reconfigura como laura@contoso.com, la dirección proxy de laura@contoso.com debe configurarse en el buzón de Laura. Esto permite que las respuestas y los mensajes entrantes se entreguen correctamente.

Volver al principio

## Consideraciones sobre la reconfiguración de direcciones entrantes y salientes

La reconfiguración de direcciones entrantes y salientes, o *bidireccional* en un servidor Transporte perimetral modifica la dirección de correo electrónico del remitente en los mensajes que salen de la organización de Exchange, y modifica la dirección de correo electrónico del destinatario en los mensajes que entran a la organización de Exchange.

Puede configurar la reconfiguración de direcciones solo salientes para un solo usuario (chris@contoso.com a support@contoso.com) y todos los usuarios en un solo dominio (contoso.com a fabrikam.com). No puede configurar la reconfiguración de direcciones bidireccional para los usuarios en varios subdominios (\*.fabrikam.com a contoso.com).

Volver al principio

## Consideraciones sobre la reconfiguración de direcciones de correo electrónico en varios dominios

Al incluir varios dominios o subdominios internos en un solo dominio externo, necesita tener en cuenta los siguientes factores:

  - **Comprobar alias únicos**   Todos los alias de correo electrónico (la parte a la izquierda del signo @) deben ser únicos en todos los subdominios. Por ejemplo, si existe joe@sales.contoso.com, no puede existir joe@marketing.contoso.com porque la dirección de correo electrónico reconfigurada para ambos usuarios sería joe@contoso.com.

  - **Agregar direcciones proxy**   La dirección de correo electrónico reconfigurada debe configurarse como una dirección proxy para todos los remitentes afectados en los dominios afectados. Por ejemplo, si joe@sales.contoso.com se vuelve a escribir en joe@contoso.com, es necesario agregar la dirección proxy joe@contoso.com al buzón de Joe. Esto permite que las respuestas y los mensajes entrantes se entreguen correctamente.

  - **Contactos de correo para las organizaciones que no son de Exchange**   Si va a reconfigurar direcciones de correo electrónico en un sistema de correo electrónico que no es de Exchange, necesita crear contactos de correo electrónico en Exchange para representar a los usuarios en el sistema que no es de Exchange. Estos contactos de correo electrónico deben contener las direcciones de correo electrónico originales y las direcciones de correo electrónico reconfiguradas. Por ejemplo, si joe@unix.contoso.com se vuelve a escribir en joe@contoso.com, es necesario crear un contacto de correo con joe@unix.contoso.com como la dirección de correo electrónico externa y joe@contoso.com como dirección proxy.

## Comprobar alias únicos

Cuando reconfigura direcciones de correo electrónico en varios subdominios, necesita asegurarse de que todos los alias de correo electrónico son únicos en todos los subdominios. Por ejemplo, tenga en cuenta la siguiente configuración:

Los siguientes usuarios se encuentran en los subdominios sales.contoso.com, marketing.contoso.com y research.contoso.com:

  - nuria@ventas.contoso.com

  - maria@ventas.contoso.com

  - jaime@marketing.contoso.com

  - miguelangel@marketing.contoso.com

  - maria@investigacion.contoso.com

  - arturo@investigacion.contoso.com

Supongamos que quiere reconfigurar los subdominios sales.contoso.com, marketing.contoso.com y research.contoso.com en un solo dominio contoso.com.

Cuando las direcciones de correo electrónico en cada subdominio se reconfiguran, se produce un conflicto entre chris@sales.contoso.com y chris@research.contoso.com porque ambas direcciones se reconfiguran en chris@contoso.com. Para resolver esta situación, es necesario cambiar la dirección de correo electrónico de los destinatarios afectados. Por ejemplo, puede cambiar chris@research.contoso.com a christopher@research.contoso.com para que la dirección de correo electrónico se reconfigure como christopher@contoso.com.

Volver al principio

## Prioridad de las entrada de reescritura de direcciones

Si la dirección de correo electrónico de un usuario coincide con varias entradas de reescritura de direcciones, la dirección de correo electrónico solo se volverá a escribir una vez según la coincidencia más aproximada. En la siguiente lista se describe el orden de prioridad de las entradas de reescritura de direcciones, desde la prioridad de mayor nivel a la de menos nivel:

1.  **Direcciones de correo electrónico individuales**   Se configura una entrada de reescritura de direcciones para volver a escribir la dirección de john@contoso.com como support@contoso.com.

2.  **Asignación de dominios o subdominios**   Se configura una entrada de reescritura de direcciones para volver a escribir todas las direcciones de correo electrónico de contoso.com en northwindtraders.com o todas las direcciones de sales.contoso.com en contoso.com.

3.  **Simplificación de dominios**   Se configura una entrada de reescritura de direcciones para volver a escribir las direcciones de correo electrónico de \*.contoso.com en contoso.com.

Por ejemplo, supongamos un servidor Transporte perimetral en el que se configuren las siguientes entradas de reescritura de direcciones salientes:

  - Las direcciones de correo electrónico de \*.contoso.com se vuelven a escribir en contoso.com

  - Las direcciones de correo electrónico de japan.sales.contoso.com se vuelven a escribir en contoso.jp

Si masato@japan.sales.contoso.com envía un mensaje de correo electrónico, la dirección se vuelve a escribir en masato@contoso.jp, porque esa entrada es la que más se aproxima a la dirección de correo electrónico del remitente.

Volver al principio

## Mensajes firmados digitalmente, cifrados y protegidos por derechos

La reconfiguración de direcciones no tendría que afectar a la mayoría de los mensajes firmados, cifrados o protegidos por derechos. Si la reconfiguración de direcciones se llevara a cabo para invalidar o cambiar el estado de seguridad de estos tipos de mensajes en algún modo, la reconfiguración de direcciones no se aplica.

Los siguientes valores se pueden volver a escribir porque la información no forma parte de mensajes firmados, cifrados o protegidos por derechos:

  - Campos en el sobre del mensaje

  - Encabezados del cuerpo del mensaje de nivel superior

Los siguientes valores no se vuelven a escribir porque la información forma parte de mensajes firmados, cifrados o protegidos por derechos:

  - Los campos de encabezado que están ubicados dentro de las partes del cuerpo MIME se pueden firmar

  - El parámetro de cadena de límites del tipo de contenido MIME

Volver al principio

