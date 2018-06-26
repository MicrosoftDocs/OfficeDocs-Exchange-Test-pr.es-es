---
title: 'Identidad de mensajes DSN: Exchange 2013 Help'
TOCTitle: Identidad de mensajes DSN
ms:assetid: 70ffba22-e4fd-4cd3-98f5-8bfca2df89e4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998835(v=EXCHG.150)
ms:contentKeyID: 49895702
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Identidad de mensajes DSN

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Puede identificar un mensaje personalizado de notificación de estado de entrega (DNS) según su sintaxis. La identidad es la GUID del mensaje DSN personalizado o una cadena que contenga los siguientes valores:

  - **Configuración regional**   Esta variable especifica la configuración regional del idioma en que se muestra el mensaje DSN. Para obtener una lista de códigos regionales que puede utilizar con el comando **New-SystemMessage**; vea [Idiomas admitidos para mensajes del sistema](supported-languages-for-system-messages-exchange-2013-help.md).

  - **Interna o externa**   Esta variable especifica si el mensaje DSN se envía solo a los destinatarios que forman parte de la organización interna de Microsoft Exchange Server 2013 o también a los que están fuera de la organización de Exchange. Puede usar la opción Interna cuando desee incluir una resolución o un contacto de correo electrónico específicos en los mensajes DSN que se envíen a remitentes internos, pero no desee mostrar dicha información a remitentes externos a la organización.

  - **Código DSN**   Esta variable especifica el código DSN del mensaje DSN personalizado.

La sintaxis de la identidad del mensaje DSN es `<Locale>\<Internal or External>\<DSN code>`.

Para cada código DSN, puede crear más de un mensaje DSN personalizado, que puede estar dirigido a remitentes internos o externos, y tener configuraciones regionales diferentes. Por ejemplo, la tabla siguiente muestra algunas de las configuraciones posibles para el código de DNS 5.1.2 y las identidades de mensaje de DNS correspondientes.

### Ejemplos de configuraciones de DSN e identidades

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración de DSN</th>
<th>Identidad DSN</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mostrar mensajes DSN a remitentes internos con configuración regional inglesa (en)</p></td>
<td><p>En\Interno\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Mostrar mensajes DSN a remitentes externos con configuración regional inglesa (en)</p></td>
<td><p>En\Externo\5.1.2</p></td>
</tr>
<tr class="odd">
<td><p>Mostrar mensajes DSN a remitentes internos con configuración regional japonesa (ja)</p></td>
<td><p>Ja\Interno\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Mostrar mensajes DSN a remitentes externos con configuración regional japonesa (ja)</p></td>
<td><p>Ja\Externo\5.1.2</p></td>
</tr>
</tbody>
</table>

