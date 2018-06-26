---
title: 'Uso de elementos web de Outlook Web App: Exchange 2013 Help'
TOCTitle: Uso de elementos web de Outlook Web App
ms:assetid: 7272e3ab-430c-4d6c-8621-9535236ce463
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt574711(v=EXCHG.150)
ms:contentKeyID: 70312146
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Uso de elementos web de Outlook Web App

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-07-31_

Puede usar elementos web de MicrosoftOfficeOutlook Web App para especificar el buzón que se abrirá, la carpeta del buzón que se abrirá y la vista de contenido que se usará.

Los elementos web de Outlook Web App le permiten tener acceso al contenido de Outlook Web App directamente desde una URL. La URL puede especificarse en un explorador web o incrustarse en una aplicación. En general, los elementos web no se crean manualmente, sino que se crean de manera programada a partir de selecciones realizadas en una interfaz de usuario (IU), o bien se insertan directamente en una aplicación, como una página de SharePoint Server. El código subyacente en la interfaz de usuario crea la URL. Un uso de los elementos web de Outlook Web App es mostrar la Bandeja de entrada o el calendario de un usuario en una página de SharePoint.


> [!NOTE]
> Para usar los elementos web de Outlook Web App, tanto el buzón de correo del usuario como el buzón que se abre mediante un elemento web deben encontrarse en el mismo bosque de Active Directory.



## Permisos para usar los elementos web de Outlook Web Access

Para usar los elementos web de Outlook Web App, como mínimo, deberá tener delegado el acceso de "Revisor" al contenido que esté abriendo. Si ha insertado un elemento web de Outlook Web App que necesite autenticarse en una aplicación, debe pasar información de autenticación junto con la solicitud del elemento web. Una manera de hacerlo es configurar el directorio virtual de Outlook Web App para usar la autenticación integrada de Windows. La autenticación integrada de Windows permite a los usuarios que ya se hayan registrado a través de su cuenta de Active Directory usar Outlook Web App sin tener que escribir de nuevo sus credenciales.

## Sintaxis de los elementos web de Outlook Web App

Outlook Web App en Exchange 2013 tiene un nuevo formato de URL que se usa para solicitudes al directorio virtual /owa. Estas solicitudes pueden realizarse si se escribe directamente una dirección URL en un explorador web o al insertar la dirección URL en una aplicación web, por ejemplo, una página de SharePoint Server.

Los elementos web de Outlook Web App se pueden usar para crear direcciones URL de diferente complejidad. Una URL de un elemento web sencillo se puede usar para abrir la Bandeja de entrada de cualquier buzón. Una URL de un elemento web más complejo se podría usar para especificar el buzón que se abrirá, la carpeta del buzón que se abrirá y la vista de contenido que se usará.

En función de las medidas de seguridad que se hayan aplicado a la red, puede que tenga que configurar la codificación para la URL de los elementos web. Tras configurar la codificación, el código de la interfaz de usuario creará la URL con los parámetros codificados en la URL. Los parámetros codificados en la URL usan %20 en lugar de espacios y %2f en lugar del delimitador de ruta de acceso "/". Todos los ejemplos de este tema usan parámetros codificados.

En la tabla siguiente se indican los parámetros de un elemento web y algunos ejemplos de cómo usarlos.

### Parámetros de elementos web y cómo se usan

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro URL</th>
<th>Descripción</th>
<th>Valores y ejemplos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nombre del servidor y directorio (obligatorio)</p></td>
<td><p>La URL del directorio virtual de Outlook Web App.</p></td>
<td><p>Esta puede ser la misma URL que usan los usuarios para iniciar sesión en Outlook Web App, por ejemplo:</p>
<p>https://&lt;<em>server name</em>&gt;/owa</p></td>
</tr>
<tr class="even">
<td><p>Identificación explícita del buzón para el inicio de sesión de Exchange 2013 (opcional)</p></td>
<td><p>Cualquier dirección SMTP asociada con el buzón que se va a abrir.</p>
<p>Si falta esta sección de la URL, se abre el buzón predeterminado del usuario autenticado.</p>
<p>Si no se especifican parámetros adicionales, el comportamiento predeterminado consiste en abrir la Bandeja de entrada.</p></td>
<td><p>Para abrir el buzón con la dirección SMTP tsmith@fourthcoffee.com, use la URL siguiente:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/tsmith@fourthcoffee.com</p></td>
</tr>
<tr class="odd">
<td><p>cmd (se requiere en el caso de no especificar ningún parámetro diferente a la identificación explícita del buzón para el inicio de sesión)</p></td>
<td><p>?cmd=contents muestra el elemento web de Outlook Web App que especifican los parámetros en lugar de la interfaz de usuario completa de Outlook Web App.</p></td>
<td><p>Si no se especifica ningún buzón de correo, el parámetro cmd aparecerá después de la dirección de inicio de sesión, como se indica a continuación:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents</p>
<p>Si se especifica un buzón de correo, el parámetro cmd aparecerá después de la identificación explícita del buzón, como se indica a continuación:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/&lt;<em>SMTP address</em>&gt;/?cmd=contents</p>
<p>Si no se especifican parámetros adicionales, el comportamiento predeterminado consiste en abrir la Bandeja de entrada.</p></td>
</tr>
<tr class="even">
<td><p>exsvurl</p></td>
<td><p>Este parámetro debe incluirse al usar la autenticación de LiveID</p>
<p>Se descartarán todos los parámetros durante la autenticación de LiveID si &quot;exsvurl=1&quot; no está presente. Este parámetro solo es para los buzones de Office 365.</p></td>
<td><p>https://&lt;nombre del servidor&gt;/owa/?cmd=contents&amp;exsvurl=1</p></td>
</tr>
<tr class="odd">
<td><p>fpath (opcional)</p></td>
<td><p>Esta parte de la dirección URL puede haberse escrito mediante el uso de la codificación URL para que pueda atravesar los firewalls.</p>
<p>Cuando se usa la codificación URL, un espacio se convierte en %20 y un delimitador de ruta de acceso (/) en %2f.</p>
<p>La jerarquía de carpeta comenzará en la raíz del buzón.</p>
<p>Esta ruta de carpeta puede apuntar a carpetas ordinarias o carpetas de búsqueda.</p></td>
<td><p>Para abrir la subcarpeta Proyectos en la Bandeja de entrada, use la URL siguiente:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;fpath= inbox%2fprojects</p></td>
</tr>
<tr class="even">
<td><p>module (opcional)</p></td>
<td><p>Este parámetro se puede usar para especificar cualquiera de las carpetas predeterminadas sin conocer el nombre localizado.</p></td>
<td><p>Los valores del parámetro module no distinguen entre mayúsculas y minúsculas e incluyen lo siguiente:</p>
<ul>
<li><p>Bandeja de entrada</p></li>
<li><p>Calendario</p></li>
<li><p>Buzón de equipo</p></li>
</ul>
<p>Para abrir el calendario de un buzón independientemente de su localización, use la URL siguiente:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;module=calendar</p></td>
</tr>
<tr class="odd">
<td><p>view (opcional)</p></td>
<td><p>Este parámetro especifica la vista que se va a mostrar en la carpeta.</p>
<p>Las vistas predeterminadas cuando este parámetro no está presente son las siguientes:</p>
<ul>
<li><p>Calendario   Diaria</p></li>
<li><p>Mensajes   Mensajes</p></li>
</ul>

> [!NOTE]
> Las cadenas para las vistas predeterminadas se codifican automáticamente con URL.


<p>El orden predeterminado de una vista es la forma en la que la carpeta se ordenaría si se abriera en el cliente de Outlook Web App.</p>
<p>Las cadenas que identifican las vistas no están localizadas y no distinguen entre mayúsculas y minúsculas.</p></td>
<td><p>Las vistas disponibles varían en función del tipo de carpeta.</p>
<p>Vistas de calendario:</p>
<ul>
<li><p>Diaria   La vista de calendario diaria</p></li>
<li><p>Semanal   La vista de calendario semanal</p></li>
<li><p>Mensual   La vista de calendario mensual</p></li>
</ul>
<p>Vistas de mensajes:</p>
<ul>
<li><p>Mensajes   La vista de mensajes, con orden predeterminado</p></li>
<li><p>By%20Sender   Vista de mensajes ordenados por De con los nombres de los remitentes que comienzan por &quot;a&quot; en la parte superior</p></li>
<li><p>By%20Subject   Vista de mensajes ordenados por Asunto con los asuntos que comienzan por &quot;a&quot; en la parte superior</p></li>
<li><p>By%20Conversation%20Topic   Vista de conversación, no disponible en la versión ligera de Outlook Web App</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>d, m, y (opcional)</p></td>
<td><p>Especifica la fecha por la que debe mostrarse el calendario. Estos parámetros pueden especificarse en cualquier orden y usarse por separado o de manera conjunta.</p>
<p>Si no se especifica ninguno de estos parámetros, los valores predeterminados son los valores del día, mes y año actuales. Por ejemplo, si hoy es 3 de mayo de 2016 y especifica un valor de mes de &quot;9&quot; para septiembre, la fecha mostrada será el 3 de septiembre de 2016.</p></td>
<td><p>Los valores válidos para los parámetros de fecha son los siguientes:</p>
<p>d=[1-31]</p>
<p>m=[1-12]</p>
<p>y=[año de cuatro dígitos]</p>
<p>Para abrir un calendario en la fecha 3 de mayo de 2016, usará la siguiente URL: https://&lt;<em>server name</em>&gt;/owa/?cmd=content&amp;fpath=calendar&amp;view=daily&amp;d=3&amp;m=5&amp;y=2016</p></td>
</tr>
<tr class="odd">
<td><p>part (opcional)</p></td>
<td><p>Especifica que Outlook Web App deberá mostrar un elemento web más pequeño.</p></td>
<td><p>Cuando use elementos web para tener acceso al contenido de Outlook Web App, la interfaz de usuario que se muestra será más pequeña que la interfaz de usuario completa de Outlook Web App. El parámetro part reduce aún más la interfaz de usuario. En la siguiente URL de ejemplo se muestra la lista de tareas en el formato de elemento web más pequeño:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;part=1</p>
<p>El parámetro part no se aplica al módulo de calendario.</p></td>
</tr>
<tr class="even">
<td><p>FolderList</p></td>
<td><p>Este parámetro part incluye el control de lista de carpetas para que los usuarios cambien entre las subcarpetas. Esto solo se aplica a las carpetas de correo electrónico.</p></td>
<td><p>https://&lt;nombre del servidor&gt;/owa/?cmd=contents&amp;folderlist=1</p></td>
</tr>
</tbody>
</table>


## Especificar elementos web de Outlook Web App manualmente

Los elementos web de Outlook Web App pueden especificarse también manualmente en un explorador web. Por ejemplo, un usuario puede usar una URL de un elemento web de Outlook Web App para abrir el calendario de otro usuario.

En los ejemplos siguientes se muestra cómo acceder directamente a las vistas comunes de Outlook Web App:

  - **Bandeja de entrada:** https://*\<server name\>*/owa/?cmd=contents\&module=inbox

  - **Calendario (hoy):**https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&exsvurl=1

  - **Calendario (semanal):** https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&view=weekly\&exsvurl=1

  - **Calendario (mensual):** https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&view=monthly\&exsvurl=1

## Para obtener más información

  - [Personalizar las páginas de inicio de sesión, selección de idioma y error de Outlook Web App](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)

  - [Crear un tema para Outlook Web App](create-a-theme-for-outlook-web-app-exchange-2013-help.md)

