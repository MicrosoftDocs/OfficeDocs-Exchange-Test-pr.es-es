---
title: 'Saludos de correo de voz, anuncios, menús y mensajes: Exchange 2013 Help'
TOCTitle: Saludos de correo de voz, anuncios, menús y mensajes
ms:assetid: df61105d-c9d8-452c-b028-50cbda47aecf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124902(v=EXCHG.150)
ms:contentKeyID: 54652457
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Saludos de correo de voz, anuncios, menús y mensajes

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2015-03-09_

Al instalar la mensajería unificada (UM), también se instala un conjunto común de archivos de audio predeterminados que se usa para el sistema de correo de voz y para los mensajes del menú, saludos y anuncios informativos. Si bien puede crear un operador automático de mensajería unificada o un plan de marcado que use solo los indicativos de audio predeterminados, estos indicativos son muy genéricos para que sirvan como una interfaz pública aceptable para muchas empresas. En este tema se tratan los mensajes del menú y del sistema, saludos y anuncios informativos usados por los planes de marcado y operadores automáticos de mensajería unificada, y cómo se usan cuando las personas que llaman tienen acceso al sistema de correo de voz.

**Contenido**

Introducción a los indicativos de audio y saludos

Mensajes del sistema

Anuncios y saludos de los planes de marcado de mensajería unificada

Saludos, anuncios y mensajes del menú del operador automático de mensajería unificada

Personalización de saludos, anuncios, mensajes del menú y menús de navegación

## Introducción a los indicativos de audio y saludos

Después de que se instala la mensajería unificada, los archivos de audio de los planes de marcado y operadores automáticos de mensajería unificada se copian en el servidor de buzones de correo. De modo predeterminado, el programa de instalación copia los archivos de audio en la carpeta Archivos de programa\\Microsoft\\Exchange Server\\V15\\Unified Messaging\\Prompts*\\\<idioma\>*. Si tiene instalada la versión en inglés de Estados Unidos, se creará una carpeta denominada \\en durante la instalación para almacenar las versiones en inglés de Estados Unidos de los mensajes del sistema. El servidor de buzones de correo reproduce estos mensajes del sistema para que las personas que llaman puedan escuchar saludos, mensajes del menú y anuncios informativos y para que puedan navegar por los menús de mensajería unificada.

Estos indicativos o archivos de audio del sistema no deben reemplazarse nunca. Sin embargo, la mensajería unificada permite personalizar los mensajes de bienvenida, los mensajes del menú principal y los anuncios informativos de los planes de marcado y operadores automáticos de mensajería unificada.

En la tabla siguiente se resumen los mensajes y saludos usados en los planes de marcado de mensajería unificada.

### Indicativos de audio para planes de marcado de mensajería unificada

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Mensajes y saludos</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mensajes del sistema</p></td>
<td><p>No deben modificarse.</p></td>
</tr>
<tr class="even">
<td><p>Saludo de bienvenida</p></td>
<td><p>El saludo de bienvenida predeterminado es un mensaje del sistema que se reproduce de manera predeterminada. Sin embargo, es posible usar un archivo de saludo personalizado que usted mismo cree.</p></td>
</tr>
<tr class="odd">
<td><p>Anuncio informativo</p></td>
<td><p>De manera predeterminada, los anuncios informativos están deshabilitados. Si habilita un anuncio informativo, debe especificar un archivo de saludo personalizado.</p></td>
</tr>
</tbody>
</table>


En la tabla siguiente se resumen los mensajes y los saludos que se usan con los operadores automáticos de mensajería unificada.

### Indicativos de audio para operadores automáticos de mensajería unificada

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Mensajes y saludos</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mensajes del sistema</p></td>
<td><p>No deben modificarse.</p></td>
</tr>
<tr class="even">
<td><p>Mensajes del menú de horario comercial</p></td>
<td><p>De manera predeterminada, los mensajes del menú de horario comercial están habilitados y se reproduce un mensaje del sistema. Sin embargo, es posible usar un archivo de saludo personalizado que usted mismo cree.</p></td>
</tr>
<tr class="odd">
<td><p>Mensajes del menú de horario no comercial</p></td>
<td><p>De manera predeterminada, los mensajes del menú de horario no comercial están habilitados y se reproduce un mensaje del sistema. Sin embargo, es posible usar un archivo de saludo personalizado que usted mismo cree.</p></td>
</tr>
<tr class="even">
<td><p>Saludo para horario comercial</p></td>
<td><p>De manera predeterminada, el saludo para horario comercial está habilitado y se reproduce un mensaje del sistema. Sin embargo, es posible usar un archivo de saludo personalizado que usted mismo cree. También se lo conoce como saludo de bienvenida.</p></td>
</tr>
<tr class="odd">
<td><p>Saludo para horario no comercial</p></td>
<td><p>De manera predeterminada, hay un saludo para horario no comercial habilitado y se reproduce un mensaje del sistema. Sin embargo, es posible usar un archivo de saludo personalizado que usted mismo cree. También se lo conoce como saludo de bienvenida.</p></td>
</tr>
<tr class="even">
<td><p>Anuncio informativo</p></td>
<td><p>De manera predeterminada, los anuncios informativos están deshabilitados. Si habilita un anuncio informativo, debe especificar un archivo de saludo personalizado.</p></td>
</tr>
</tbody>
</table>



> [!WARNING]
> No se permite la modificación de los avisos del sistema instalados.



Introducción a los indicativos de audio y saludos

## Mensajes del sistema

La mensajería unificada se instala con un conjunto de indicativos de audio predeterminados que se usan con Outlook Voice Access, planes de marcado y operadores automáticos. Se instalan cientos de mensajes del sistema para cada idioma en el servidor de buzones de correo. El servidor de buzones de correo reproduce los archivos de audio para estos mensajes del sistema en los autores de la llamada cuando obtienen acceso al sistema de correo de voz. Aquí te mostramos algunos ejemplos de estos mensajes del sistema:

  - "Escriba su PIN".

  - "Para acceder a su buzón, introduzca su extensión".

  - "Para contactar con alguien, presione almohadilla".

  - "Deletree el nombre de la persona a quien llama, primero el apellido".

  - "Para contactar con una persona en concreto, simplemente diga su nombre".


> [!WARNING]
> No se permite la modificación de los avisos del sistema instalados.




> [!NOTE]
> Cuando se inicie el servicio de mensajería unificada en el servidor de buzones de correo, comprobará que todos los mensajes del sistema estén disponibles. Si no se encuentra un mensaje del sistema, la mensajería unificada devolverá un error. Para solucionar el error devuelto, busque el evento con el Visor de eventos y copie el archivo mostrado en la ventana <STRONG>Propiedades del evento</STRONG> del DVD de instalación en la carpeta adecuada del servidor de buzones de correo.



## Anuncios y saludos de los planes de marcado de mensajería unificada

Después de instalar el servidor de buzones de correo y crear un plan de marcado de mensajería unificada, tiene la opción de usar los archivos de audio para los mensajes del sistema predeterminados que se crean durante la instalación o para crear archivos de audio que se pueden usar con los planes de marcado de mensajería unificada.

Los planes de marcado de mensajería unificada tienen un saludo de bienvenida y un anuncio informativo opcional que se puede modificar. El saludo de bienvenida se usa cuando un usuario de Outlook Voice Access u otra persona llama al número de acceso de suscriptor. Las personas que llaman escuchan un saludo de bienvenida predeterminado que dice: "Bienvenido, está conectado a Microsoft Exchange". Es posible que quiera cambiar este saludo por un saludo de bienvenida alternativo específico de su empresa, como "Bienvenido a Outlook Voice Access para Woodgrove Bank". Si personaliza este saludo, puede grabar el saludo personalizado y guardarlo como archivo .wav y luego configurar el plan de marcado para que use el saludo personalizado.

La mensajería unificada permite reproducir un anuncio informativo tras el mensaje de bienvenida. De forma predeterminada, no se configura ningún anuncio informativo. Sin embargo, es posible que quiera incluir uno para quienes llaman. Es posible usar el anuncio informativo para anuncios generales que cambian más frecuentemente que los saludos de bienvenida o para anuncios requeridos por las directivas de conformidad corporativas. Cuando es importante que se escuche todo el anuncio informativo, se puede configurar para que no se pueda interrumpir su reproducción. Esto impide que quien llame presione una tecla o pronuncie un comando para interrumpir y detener el anuncio informativo.

En la tabla siguiente se describen los anuncios informativos y saludos de los planes de marcado de mensajería unificada.

### Anuncios informativos y saludos de los planes de marcado de mensajería unificada

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Saludo</th>
<th>Ejemplo predeterminado</th>
<th>Ejemplo personalizado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Saludo de bienvenida</p></td>
<td><p>&quot;Bienvenido, está conectado a Microsoft Exchange&quot;.</p></td>
<td><p>&quot;Bienvenido a Outlook Voice Access para Woodgrove Bank&quot;.</p></td>
</tr>
<tr class="even">
<td><p>Anuncio informativo</p></td>
<td><p>De forma predefinida, no se configura ningún mensaje informativo.</p></td>
<td><p>&quot;Al usar este sistema, acepta cumplir todas las directivas corporativas cuando tenga acceso a este sistema&quot;.</p></td>
</tr>
</tbody>
</table>


Al personalizar y configurar saludos y anuncios, asegúrese de que la configuración de idioma establecida en el plan de marcado de mensajería unificada sea la misma que el idioma de los mensajes personalizados que cree. De lo contrario, es posible que las personas que llaman escuchen un mensaje o un saludo en un idioma y otro mensaje o saludo en otro idioma distinto.

Introducción a los indicativos de audio y saludos

## Saludos, anuncios y mensajes del menú del operador automático de mensajería unificada

Al igual que los planes de marcado de mensajería unificada, los operadores automáticos de mensajería unificada tienen un saludo de bienvenida, un anuncio informativo opcional y un mensaje de menú personalizado opcional. Existen diferentes versiones del saludo de bienvenida y de los mensajes del menú que puede configurar para horario comercial y no comercial. Puede modificarlas todas.

El saludo de bienvenida es lo primero que escucha la persona que llama cuando el operador automático de mensajería unificada responde a la llamada. De manera predeterminada, este saludo dice: "Bienvenido al operador automático de Microsoft Exchange". El archivo de audio que se reproduce para la llamada es el mensaje del sistema predeterminado para el operador automático de mensajería unificada. Sin embargo, puede crear un saludo alternativo específico para su compañía, por ejemplo "Gracias por llamar a Woodgrove Bank". Si personaliza este saludo de bienvenida, grabe el saludo personalizado y guárdelo como archivo .wav y, luego, configure el operador automático para que use el saludo personalizado. También es posible personalizar los mensajes del menú, al igual que se hace con los saludos de bienvenida.

La mensajería unificada permite reproducir un anuncio informativo tras un saludo de horario comercial o no comercial. De manera predeterminada, no hay ningún anuncio informativo configurado, pero es posible establecer uno para las personas que llaman. El anuncio informativo puede anunciar el horario comercial de su empresa, por ejemplo: "El horario de nuestra empresa es de 8:00 a. m. a 5:00 p. m., de lunes a viernes, y de 8:30 a. m. a 1:00 p. m. el sábado". El anuncio informativo también puede proporcionar información necesaria para el cumplimiento de las directivas de la empresa, por ejemplo, “Se pueden controlar las llamadas con fines de formación”. Cuando es importante que se escuche todo el anuncio informativo, se puede configurar para que no se pueda interrumpir su reproducción. Esto impide que quien llame presione una tecla o pronuncie un comando para interrumpir y detener el anuncio informativo.

En la tabla siguiente se describen los anuncios informativos y los saludos de los operadores automáticos de mensajería unificada.

### Saludos, anuncios informativos y mensajes del menú del operador automático de mensajería unificada

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Saludo</th>
<th>Ejemplo predeterminado</th>
<th>Ejemplo personalizado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Saludo para horario comercial</p></td>
<td><p>&quot;Bienvenido al operador automático de Microsoft Exchange&quot;.</p></td>
<td><p>&quot;Gracias por llamar a Woodgrove Bank&quot;.</p></td>
</tr>
<tr class="even">
<td><p>Saludo para horario no comercial</p></td>
<td><p>No se reproduce ningún saludo para horario no comercial predeterminado hasta que configure el horario comercial para el operador automático. Sin embargo, el saludo de horario comercial se reproduce cuando alguien llama a cualquier hora del día.</p></td>
<td><p>&quot;Ha llamado a Woodgrove Bank fuera del horario comercial. El horario comercial es de 8:00 a. m. a 5:00 p. m., de lunes a viernes&quot;.</p></td>
</tr>
<tr class="odd">
<td><p>Anuncio informativo</p></td>
<td><p>De manera predeterminada, no hay anuncios informativos configurados.</p></td>
<td><p>&quot;Se pueden controlar las llamadas con fines de formación&quot;.</p></td>
</tr>
<tr class="even">
<td><p>Mensaje del menú principal para horario comercial</p></td>
<td><p>No se reproducirá ningún mensaje del menú principal para horario comercial predeterminado hasta que configure las asignaciones de teclas en el operador automático.</p></td>
<td><p>&quot;Para asistencia técnica, presione o diga 1. Para oficinas corporativas y administración, presione o diga 2. Para el departamento comercial, presione o diga 3&quot;.</p></td>
</tr>
<tr class="odd">
<td><p>Mensaje del menú principal para horario no comercial</p></td>
<td><p>No se reproducirá ningún mensaje del menú principal para horario no comercial predeterminado hasta que configure las asignaciones de teclas y el horario comercial en el operador automático.</p></td>
<td><p>&quot;Su llamada es muy importante para nosotros. Sin embargo, ha llamado a Woodgrove Bank fuera del horario comercial. Si desea dejar un mensaje, presione o diga 1 y lo llamaremos lo antes posible&quot;.</p></td>
</tr>
</tbody>
</table>


Al igual que con los planes de marcado de mensajería unificada, asegúrese de que la configuración de idioma establecida en el operador automático de mensajería unificada sea la misma que el idioma de los saludos personalizados que cree y de que tenga configurado el mismo idioma que el plan de marcado de mensajería unificada. De lo contrario, es posible que las personas que llaman escuchen un mensaje o un saludo en un idioma y otro mensaje o saludo en otro idioma distinto.

Introducción a los indicativos de audio y saludos

## Personalización de saludos, anuncios, mensajes del menú y menús de navegación

Aunque no se deben reemplazar ni cambiar los mensajes del sistema, es probable que quiera personalizar los saludos, los anuncios informativos, los mensajes del menú y los menús de navegación usados con los planes de marcado y los operadores automáticos de mensajería unificada. Después de la instalación, puede configurar los planes de marcado de mensajería unificada y los operadores automáticos para usar archivos de audio personalizados (.wav o .wma). Es necesario completar los pasos siguientes antes de habilitar los mensajes de voz personalizados para las personas que llaman:

1.  Grabe los saludos, los anuncios y los mensajes personalizados y guárdelos como archivos .wav. Se debe usar el códec de audio PCM lineal (16 bit/muestra), 8 kilohercios (kHz) para codificar los archivos .wav. Si no se usa este formato específico para los archivos .wav, se generará un error que indica que no se admite el formato del archivo de origen. Aunque se genere un error, el error no aparecerá en el Visor de eventos.

2.  Configure el operador automático o el plan de marcado de mensajería unificada para que use los saludos, los anuncios y los mensajes personalizados.

De forma predeterminada, al crear un operador automático de MU, los saludos o avisos en horario comercial o no comercial no están configurados y no se define ninguna asignación de claves para los mensajes del menú principal, tanto en horario comercial como en horario no comercial. Para configurar correctamente los saludos y los mensajes personalizados para un operador automático, debe:

  - Configurar el horario comercial y no comercial en la página **Horario comercial**.

  - Crear los archivos de audio de saludos (.wav o .wma) que se usarán para los saludos de bienvenida en horario comercial y no comercial.

  - Configurar los saludos de bienvenida para horario comercial y no comercial en la página **Saludos**.

  - Crear los archivos de saludos que se usarán para los saludos del mensaje del menú principal en horario comercial y no comercial.

  - Configurar los saludos de mensaje del menú principal para el horario comercial y no comercial en la página **Saludos**.

  - Habilitar y configurar la navegación de menús en horarios comerciales y no comerciales en la página **Navegación de menús**.

Introducción a los indicativos de audio y saludos

