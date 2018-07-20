---
title: 'Opciones de la codificación de mensajes: Exchange 2013 Help'
TOCTitle: Opciones de la codificación de mensajes
ms:assetid: c1d9edbb-d87c-41e5-881b-cd612d83d7e4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb310794(v=EXCHG.150)
ms:contentKeyID: 49895891
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Opciones de la codificación de mensajes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Las opciones de codificación de mensajes disponibles en Exchange especifican las características del mensaje, como los juegos de caracteres MIME y no MIME, la codificación binaria y los formatos de adjuntos. Puede especificar las opciones de codificación de mensajes en las siguientes ubicaciones:

  - Configuración del dominio remoto

  - Configuración del usuario de correo y el contacto de correo

  - Configuración de Microsoft Outlook
    
      - Formato del mensaje
    
      - Formato de los mensajes de Internet
    
      - Formato de los mensajes de destinatario de Internet
    
      - Opciones de codificación del conjunto de caracteres del mensaje

**Contenido**

Opciones de codificación de mensajes para los mensajes enviados a dominios remotos

Opciones de codificación de mensajes para usuarios y contactos de correo

Opciones de codificación de mensajes disponibles en Outlook

Opciones de codificación de mensajes disponibles en Outlook Web App

Orden de prioridad para las opciones de codificación de mensaje

Más información

## Opciones de codificación de mensajes para los mensajes enviados a dominios remotos

Cuando configure las opciones de codificación de mensajes que se envían a dominios remotos, la configuración específica se aplicará a todos los mensajes que se envíen a ese dominio. Para los dominios remotos de su organización, tendrá las siguientes opciones de configuración de codificación de mensajes.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Configuración</strong></p></td>
<td><p><strong>Disponible en EAC en Exchange Online dedicado</strong></p></td>
<td><p><strong>Disponible en el Shell</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Juego de caracteres MIME</strong>   El juego de caracteres especificado se usará solamente para los mensajes MIME que no tengan su propio juego de caracteres especificado. Si se establece este parámetro, no se sobrescribirán los juegos de caracteres que ya se hayan especificado en el correo de salida.</p>
<p><strong>Juego de caracteres no MIME</strong>   Esta configuración se usa si se da alguna de las siguientes condiciones:</p>
<ul>
<li><p>Mensajes entrantes de un dominio remoto sin el valor del parámetro <em>charset=</em> en el tipo de contenido MIME: .</p></li>
<li><p>A los mensajes salientes hacia un dominio remoto les falta el valor del juego de caracteres MIME.</p></li>
</ul>
<p></p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo de contenido</strong>   Puede especificar el tipo de contenido de los mensajes MIME que se envían a los destinatarios en el dominio remoto. Puede usar los siguientes valores:</p>
<ul>
<li><p><strong>MimeHtmlText</strong>   Convierte todos los mensajes a mensajes MIME con formato HTML, excepto cuando el mensaje original es un mensaje de texto. Si el mensaje original es un mensaje de texto, el mensaje saliente será un mensaje MIME con formato de texto. Esta es la configuración predeterminada.</p></li>
<li><p><strong>MimeText</strong>   Convierte todos los mensajes a mensajes MIME con formato de texto.</p></li>
<li><p><strong>MimeHtml</strong>   Convierte todos los mensajes a mensajes MIME con formato HTML.</p></li>
</ul></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p><strong>Tamaño de ajuste de línea</strong>   Este parámetro especifica el número máximo de caracteres que se pueden incluir en una sola línea de texto del cuerpo del mensaje de correo electrónico. Las aplicaciones cliente de correo electrónico más antiguas prefieren 78 caracteres por línea. Esta opción solo está disponible mediante el Shell.</p>
<p></p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Opciones de codificación de mensajes para usuarios y contactos de correo

Cuando configure las opciones de codificación de mensajes para un contacto o usuario de correo, esas opciones se aplicarán a todos los mensajes que se envíen a ese destinatario específico. Para los contactos o usuarios de correo de su organización, tendrá las siguientes opciones de configuración de codificación de mensajes:

  - **UsePreferMessageFormat**   Este parámetro especifica si los valores del formato del mensaje configurados para el contacto de correo invalidan los valores globales configurados para el dominio remoto. Si deshabilita esta configuración, Exchange ignora otras opciones de codificación de mensajes para este destinatario y la codificación del mensaje queda determinada por la configuración del dominio remoto o por la opción configurada por el remitente del mensaje.

  - **MessageFormat**   Este parámetro especifica el formato del mensaje. Puede especificar Texto o MIME como formato del mensaje. El valor de esta configuración depende del parámetro *MessageBodyFormat*. Si el formato del cuerpo del mensaje es Html o TextAndHtml, debe establecer este parámetro en Mime.

  - **MessageBodyFormat**   Este parámetro especifica el formato del cuerpo del mensaje. Puede especificar Texto, Html o TextAndHtml. El valor de esta configuración depende del parámetro *MessageFormat*. Si el formato del mensaje es Texto, también debe establecer este parámetro en Texto.

  - **MacAttachmentFormat**   Este parámetro especifica el formato de archivos adjuntos del sistema operativo Apple Macintosh para los mensajes. Puede especificar BinHex, UuEncode, AppleSingle o AppleDouble. El valor de esta configuración depende del parámetro *MessageFormat*. Si el formato del mensaje tiene el valor Texto, debe establecer este parámetro en BinHex o UuEncode. Si el formato del mensaje tiene el valor Mime, debe establecer este parámetro en BinHex, AppleSingle o AppleDouble.

Para establecer las opciones de codificación de mensajes para usuarios y contactos de correo, deberá utilizar estos parámetros en el Shell de administración de Exchange. Para obtener más información, vea estos temas:

  - [Enable-MailContact](https://technet.microsoft.com/es-es/library/aa996001\(v=exchg.150\))

  - [New-MailContact](https://technet.microsoft.com/es-es/library/bb124519\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/es-es/library/aa995950\(v=exchg.150\))

  - [Enable-MailUser](https://technet.microsoft.com/es-es/library/aa996549\(v=exchg.150\))

  - [New-MailUser](https://technet.microsoft.com/es-es/library/aa996335\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/es-es/library/aa995971\(v=exchg.150\))

Volver al principio

## Opciones de codificación de mensajes disponibles en Outlook

Como remitente, puede especificar las opciones de codificación de mensajes en Outlook en cualquiera de las siguientes etapas:

  - Mediante la configuración del formato del mensaje predeterminado como texto sin formato o HTML.

  - En el momento de la redacción, mediante la configuración del formato del mensaje como texto sin formato o HTML usando el área **Formato** en la ficha **Opciones**.

  - Puede especificar las opciones de codificación de mensajes para los mensajes que se envían a todos los destinatarios fuera de la organización de Exchange. Estas opciones se denominan opciones *Formato de mensajes de Internet*. Las opciones solo se aplican a destinatarios remotos y no se aplican a los destinatarios en la organización de Exchange.

  - Puede especificar las opciones de codificación de mensajes para los mensajes que se envían a destinatarios específicos fuera de la organización de Exchange. Estas opciones se denominan opciones *Formato de los mensajes de destinatario de Internet*. Las opciones solo se aplican a destinatarios remotos en su carpeta de Contactos y no se aplican a los destinatarios en la organización de Exchange.

De manera predeterminada, Outlook utiliza la codificación automática para juego de caracteres de mensajes explorando el texto completo del mensaje saliente con el objeto de determinar la codificación apropiada para el mensaje. Esta configuración se aplica a los mensajes que envíe a destinatarios de Internet y a destinatarios en la organización de Exchange. Sin embargo, puede omitir este paso y especificar una codificación preferida para los mensajes salientes.

Volver al principio

## Opciones de codificación de mensajes disponibles en Outlook Web App

Como remitente, puede especificar las opciones de codificación de mensajes en Outlook Web App en cualquiera de las siguientes etapas:

  - Al configurar el formato del mensaje predeterminado para que sea texto sin formato o HTML en la sección **Formato del mensaje** de la página **Configuración**\>**Opciones**\>**Configuración**.

  - Al configurar el formato del mensaje mientras lo redacta ya sea en texto sin formato o en HTML mediante el menú **Más opciones** y seleccionando **Cambiar a texto sin formato** o **Cambiar a HTML**.

Volver al principio

## Orden de prioridad para las opciones de codificación de mensaje

Exchange utiliza el orden de prioridad como se describe en la siguiente lista para determinar las opciones de codificación para los mensajes salientes que se envían a destinatarios fuera de la organización de Exchange:

1.  Configuración del dominio remoto

2.  Configuración de Outlook o Outlook Web App

3.  Configuración del usuario de correo o el contacto de correo

La lista especifica el orden de prioridad de menor a mayor. Una configuración a un nivel más alto puede invalidar una configuración de un nivel inferior.

En la tabla siguiente, se describe el orden de prioridad de mayor a menor para las opciones de codificación del juego de caracteres del mensaje.

### Orden de prioridad de mayor a menor para las opciones de codificación del juego de caracteres del mensaje

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
<th>Valores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Opción de entrada de dominio remoto, mediante el EAC o <strong>Set-RemoteDomain</strong></p></td>
<td><p><em>CharacterSet</em></p></td>
<td><p>Especificado</p></td>
</tr>
<tr class="even">
<td><p>Opción de entrada de dominio remoto, mediante el EAC o <strong>Set-RemoteDomain</strong></p></td>
<td><p><em>NonMimeCharacterSet</em></p></td>
<td><p>Especificado</p></td>
</tr>
<tr class="odd">
<td><p>Configuración de Outlook</p></td>
<td><p>Codificación del conjunto de caracteres del mensaje</p></td>
<td><ul>
<li><p>Selección automática</p></li>
<li><p>Especificado</p></li>
</ul></td>
</tr>
</tbody>
</table>


Al establecer el juego de caracteres no MIME para un dominio remoto, el juego de caracteres se asigna a los siguientes tipos de mensajes:

  - Mensajes salientes hacia un dominio remoto configurado que no contienen un juego de caracteres especificado.

  - Mensajes entrantes de un dominio remoto configurado que no contienen un juego de caracteres especificado.

El valor de la página de código Windows ANSI para el servidor de transporte se utiliza para asignar un juego de caracteres a los siguientes tipos de mensajes:

  - Mensajes internos que no contienen un juego de caracteres especificado.

  - Mensajes internos que contienen un juego de caracteres especificado, pero que no contienen una determinada página de códigos del servidor.

Si un mensaje contiene un juego de caracteres especificado, pero no válido, el servidor de transporte intenta remplazar el juego de caracteres no válido por uno válido.

En la tabla siguiente, se describe el orden de prioridad de mayor a menor para las opciones de codificación de mensajes sin formato.

### Orden de prioridad de mayor a menor para las opciones de codificación de mensajes sin formato

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
<th>Valores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>LineWrapSize</em></p></td>
<td><ul>
<li><p>De 0 a 132</p></li>
<li><p>Ilimitado</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Configuración de Outlook</p></td>
<td><p>Formato del mensaje</p></td>
<td><p>Texto sin formato</p></td>
</tr>
<tr class="odd">
<td><p>Configuración de Outlook</p></td>
<td><p>Formato de los mensajes de Internet</p></td>
<td><p>Opciones de texto sin formato:</p>
<ul>
<li><p>Opción de codificación de datos adjuntos en formato UuEncode cuando se envíe un mensaje de texto sin formato</p></li>
<li><p>Opción de ajuste automático de texto en <em>nn</em> caracteres</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Configuración de Outlook</p></td>
<td><p>Formato de los mensajes de destinatario de Internet</p></td>
<td><p>Texto sin formato:</p>
<ul>
<li><p>Opción de codificación de datos adjuntos en formato UuEncode</p></li>
<li><p>Formato BinHex para datos adjuntos de Mac</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><ul>
<li><p><code>$true</code></p></li>
<li><p><code>$false</code></p></li>
</ul>
<p>Si el valor es <code>$false</code> o si el destinatario no se ha definido como usuario o contacto de correo en la organización de Exchange, se ignorará la configuración de usuario o de contacto de correo.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><p>Text</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><p>Text</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>UuEncode</p></li>
</ul></td>
</tr>
</tbody>
</table>


En la tabla siguiente, se describe el orden de prioridad de mayor a menor para las opciones de codificación de mensajes MIME.

### Orden de prioridad de mayor a menor para las opciones de codificación de mensajes MIME

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
<th>Valores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>ContentType</em></p></td>
<td><ul>
<li><p><code>MimeHtmlText</code></p></li>
<li><p><code>MimeText</code></p></li>
<li><p><code>MimeHtml</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Configuración de Outlook o Outlook Web App</p></td>
<td><p>Formato del mensaje</p></td>
<td><ul>
<li><p>Texto sin formato</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Configuración de Outlook</p></td>
<td><p>Formato de los mensajes de destinatario de Internet</p></td>
<td><p>Formato de mensaje MIME</p>
<ul>
<li><p>Texto sin formato</p></li>
<li><p>Incluir texto sin formato y HTML</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><p><code>$true</code></p>
<p><code>$false</code></p>
<p>Si el valor es <code>$false</code> o si el destinatario no se ha definido como usuario o contacto de correo en la organización de Exchange, se ignorará la configuración de usuario o de contacto de correo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><ul>
<li><p>Text</p></li>
<li><p>Mime</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><ul>
<li><p><code>Text</code></p></li>
<li><p><code>Html</code></p></li>
<li><p><code>TextAndHtml</code></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>AppleSingle</p></li>
<li><p>AppleDouble</p></li>
</ul></td>
</tr>
</tbody>
</table>


Volver al principio

## Más información

[Opciones de la codificación de mensajes](message-encoding-options-exchange-2013-help.md)

[Opciones de conversión de TNEF](tnef-conversion-options-exchange-2013-help.md)

[Dominios remotos](remote-domains-exchange-2013-help.md)

[Dominios remotos en Exchange Online](https://technet.microsoft.com/es-es/library/jj966211\(v=exchg.150\))

[Administrar usuarios de correo](manage-mail-users-exchange-2013-help.md)

[Administrar contactos de correo](manage-mail-contacts-exchange-2013-help.md)

[Cambiar el formato de mensaje en Outlook](https://go.microsoft.com/fwlink/p/?linkid=397890)

