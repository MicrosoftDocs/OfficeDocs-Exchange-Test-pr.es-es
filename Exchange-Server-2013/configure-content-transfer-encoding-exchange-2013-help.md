---
title: 'Configurar la codificación de transferencia de contenido: Exchange 2013 Help'
TOCTitle: Configurar la codificación de transferencia de contenido
ms:assetid: c4922362-18d4-42f7-9189-9076720eb1d8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg144562(v=EXCHG.150)
ms:contentKeyID: 49895897
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar la codificación de transferencia de contenido

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

*Codificación de transferencia de contenido* define los métodos de codificación para transformar los datos de mensajes de correo electrónico binarios en formato de texto sin formato US-ASCII. La transformación permite al mensaje explorar servidores de mensajería SMTP antiguos que sólo admiten mensajes en texto US-ASCII. La codificación de transferencia de contenido se define en RFC 2045. El método de codificación de transferencia en el campo de encabezado **Codificación-Transferencia-Contenido** en el mensaje. En Microsoft Exchange Server 2013, los siguientes métodos de codificación de transferencia de contenido están disponibles:

  - **7 bits**   Este valor indica que los datos del cuerpo del mensaje ya se encuentran el texto sin formato US ASCII y no se ha realizado ninguna codificación al mensaje.

  - **Entrecomillado imprimible (QP)**   Este método de codificación usa caracteres US-ASCII imprimibles para codificar los datos del cuerpo del mensaje. Si el texto del mensaje original está en su mayor parte en US-ASCII, la codificación de entrecomillado imprimible produce resultados compactos y más o menos legibles. De forma predeterminada, Exchange 2013 utiliza QP para codificar datos de mensajes binarios.

  - **Base64**   Este método de codificación está basado principalmente en el estándar Correo de privacidad mejorada (PEM) definido en RFC 1421. La codificación Base64 usa el método de codificación del alfabeto de 64 caracteres, así como caracteres de relleno de salida que están definidos en PEM para codificar los datos del cuerpo del mensaje. La codificación con Base64 crea un incremento predecible en el tamaño del mensaje y es óptimo para los datos binarios y texto que no sea US-ASCII.

El método de codificación de transferencia se codifica utilizando el parámetro *ByteEncoderTypeFor7BitCharsets* en los cmdlets **Set-OrganizationConfig** y **Set-RemoteDomain**. La configuración de codificación de transferencia de contenido que estableció con **Set-OrganizationConfig** se aplican a todos los mensajes de la organización de Exchange. La configuración de codificación de transferencia de contenido que estableció con **Set-RemoteDomain** se aplica solamente a mensajes que se envían a destinatarios externos en el dominio remoto.

En la tabla siguiente figuran los valores que puede usar para cambiar el método de codificación de transferencia.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro en <strong>Set-OrganizationConfig</strong></th>
<th>Parámetro en <strong>Set-RemoteDomain</strong></th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p><code>Use7Bit</code></p></td>
<td><p>Use siempre la codificación de 7 bits para HTML y texto sin formato. Es el valor predeterminado.</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p><code>UseQP</code></p></td>
<td><p>Use siempre la codificación de entrecomillado imprimible para HTML y texto sin formato.</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p><code>UseBase64</code></p></td>
<td><p>Use siempre la codificación Base64 para HTML y texto sin formato.</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p><code>UseQPHtmlDetectTextPlain</code></p></td>
<td><p>Use la codificación de entrecomillado imprimible para HTML y para texto sin formato a menos que en este segundo caso esté habilitada la línea de ajuste. Si está habilitada la línea de ajuste, use la codificación de 7 bits para texto sin formato.</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p><code>UseBase64HtmlDetectTextPlain</code></p></td>
<td><p>Use la codificación Base64 para HTML y para texto sin formato a menos que en este segundo caso esté habilitada la línea de ajuste. Si está habilitada la línea de ajuste en texto sin formato, use la codificación Base64 para HTML y la de 7 bits para texto sin formato.</p></td>
</tr>
<tr class="even">
<td><p>13</p></td>
<td><p><code>UseQPHtml7BitTextPlain</code></p></td>
<td><p>Use siempre la codificación de entrecomillado imprimible para HTML. Use siempre la codificación de 7 bits para texto sin formato.</p></td>
</tr>
<tr class="odd">
<td><p>14</p></td>
<td><p><code>UseBase64Html7BitTextPlain</code></p></td>
<td><p>Use siempre la codificación Base64 para HTML. Use siempre la codificación de 7 bits para texto sin formato.</p></td>
</tr>
</tbody>
</table>


Para obtener más información sobre el campo de encabezado **Codificación-Transferencia-Contenido**, vea la sección "Comprender la estructura de mensajes de correo electrónico" en [Conversión de contenido](content-conversion-exchange-2013-help.md).

Para obtener más información acerca de los dominios remotos, vea [Dominios remotos](remote-domains-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Estimated time to complete: 15 minutes

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Transport service" entry in the [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md) topic.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para configurar el método de codificación de transferencia de contenido para la organización

Para configurar el método de codificación de transferencia de contenido para la organización, ejecute el siguiente comando:

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets <Integer>

Por ejemplo, para establecer el método de codificación de transferencia de contenidos para una Base64, ejecute el siguiente comando:

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets 2

## Uso del Shell para configurar el método de codificación de transferencia de contenido para un dominio remoto

Para configurar el método de codificación de transferencia de contenido para todos los destinatarios de un dominio remoto, ejecute el siguiente comando:

    Set-RemoteDomain -ByteEncoderTypeFor7BitCharsets <Value>

Por ejemplo, para establecer el método de codificación de transferencia de contenidos para una Base64, ejecute el siguiente comando:

    Set- RemoteDomain -ByteEncoderTypeFor7BitCharsets UseBase64

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha configurado correctamente el método para la codificación de transferencia de contenido, realice lo siguiente:

1.  Envíe un mensaje de prueba que contenga una mezcla de texto US-ASCII y datos binarios o un texto no US-ASCII a una cuenta de prueba interna o externa. Use una cuenta interna para probar la configuración de la organización y una cuenta externa en un domino remoto para probar la configuración del dominio remoto.

2.  En un cliente de correo electrónico, verifique el campo de encabezado **Content-Transfer-Encoding** en el mensaje y verifique el método de codificación de transferencia de contenido que se utilizó en el mensaje que coincide con el método que configuró.

