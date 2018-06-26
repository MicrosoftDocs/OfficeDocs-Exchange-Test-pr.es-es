---
title: 'Idiomas, mensajes y saludos de mensajería unificada: Exchange 2013 Help'
TOCTitle: Idiomas, mensajes y saludos de mensajería unificada
ms:assetid: d48df962-9669-420b-838f-44bfe1012e2f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124728(v=EXCHG.150)
ms:contentKeyID: 49895938
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Idiomas, mensajes y saludos de mensajería unificada

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Es posible instalar y configurar paquetes de idioma para que se admitan varios idiomas en entornos de mensajería unificada (MU).

Los paquetes de idioma de mensajería unificada permiten a las personas que llaman y a los usuarios de Outlook Voice Access interactuar con el sistema de correo de voz en varios idiomas. Tras instalar un idioma adicional en un servidor de buzones de correo, las personas que llaman y los usuarios de Outlook Voice Access podrán escuchar mensajes de correo electrónico e interactuar con el sistema de correo de voz en dicho idioma.

Existen varios componentes fundamentales que usan los paquetes de idioma de mensajería unificada para permitir que los usuarios y las personas que llaman interactúen con eficacia con la mensajería unificada en varios idiomas. Todos los paquetes de idioma de mensajería unificada contienen un motor de conversión de texto a voz (TTS) y los mensajes de asistencia por voz grabados previamente, además de admitir el reconocimiento automático de voz (ASR) y la vista previa de correo de voz para un idioma determinado. En este tema, se proporciona información acerca de los paquetes de idioma de mensajería unificada, los componentes de mensajería unificada que usan dichos paquetes y cómo se usan una vez hayan sido instalados para configurar los planes de marcado de mensajería unificada y los operadores automáticos de mensajería unificada para usar otros idiomas.

Los paquetes de idioma de Mensajería unificada de Exchange son específicos para cada versión y para cada plataforma. Desde Exchange Server 2007, se han efectuado diversos lanzamientos de versiones de paquetes de idioma de mensajería unificada, incluida la versión RTM de Exchange 2007, Exchange 2007 SP1, SP2 y SP3, la versión RTM de Exchange Server 2010, Exchange 2010 SP1 y SP2, y Exchange 2013. Para algunas versiones, se encuentran disponibles las descargas tanto de 32 como de 64 bits; mientras que, para otras versiones, se encuentra disponible solamente la descarga de 64 bits.

Es muy importante que instale la versión y la plataforma correctas de los paquetes de idioma de mensajería unificada en un servidor de buzones de correo. No instale paquetes de idioma de mensajería unificada en un servidor de buzones de correo que ejecute una versión anterior de Exchange o que esté diseñado para una plataforma de 32 bits.

**Contenido**

Información general sobre los paquetes de idioma de mensajería unificada

Componentes y características de idiomas de mensajería unificada

Vista previa del correo de voz

Idiomas de mensajería unificada

Paquetes de idioma de mensajería unificada

Idiomas del plan de marcado de mensajería unificada

Idiomas del operador automático de mensajería unificada

Proceso de selección de idioma del cliente

## Información general sobre los paquetes de idioma de mensajería unificada

Los paquetes de idioma de mensajería unificada permiten a los servidores de buzones de correo hablar en otros idiomas cuando reciben llamadas y reconocer otros idiomas cuando las personas que llaman usan el reconocimiento automático de voz o cuando se transcriben los mensajes de voz. Los paquetes de idioma de UM cuentan con:

  - Mensajes de asistencia por voz grabados previamente en el idioma del paquete de idioma de UM. Por ejemplo: "Después el tono, deje su mensaje. Cuando termine de grabarlo, cuelgue el teléfono o pulse la tecla \# para obtener más opciones."

  - Archivos de gramática en el idioma del paquete de idioma de mensajería unificada que usa un servidor de buzones de correo para buscar los nombres de determinados usuarios en el directorio.

  - Conversión de texto a voz (TTS) para que las personas que llamen puedan leer el contenido (correo electrónico, calendario, información de contacto, etc.) en el idioma del paquete de idioma de la mensajería unificada.

  - Compatibilidad con el reconocimiento automático de voz, que permite a las personas que llaman interactuar con el servicio de mensajería unificada mediante la interfaz de usuario de voz (VUI) en el idioma correspondiente al paquete de idioma de mensajería unificada.

  - Compatibilidad con la vista previa de correo de voz, que permite a los usuarios leer la transcripción de los mensajes de correo de voz en un idioma determinado desde un cliente de correo electrónico admitido, como Outlook o Outlook Web App.

Los paquetes de idioma de mensajería unificada incluyen mensajes de asistencia por voz grabados previamente, admiten conversión de texto a voz (TTS) para un idioma específico y, en ciertos casos, el reconocimiento automático de voz. En entornos con diversos idiomas, puede ser necesario instalar paquetes de idioma de mensajería unificada adicionales, dado que algunas de las personas que llaman prefieren ser atendidos en otro idioma o porque reciben correo electrónico en más de un idioma. Debe instalar varios paquetes de idioma de mensajería unificada para que el servidor de buzones de correo pueda leer un correo electrónico que contenga más de un idioma, puesto que es necesario indicar al sistema de conversión TTS el idioma que debe seleccionar según el texto del mensaje que se va a leer. Si no se ha instalado el paquete de idioma de mensajería unificado, el mensaje de correo electrónico no tendrá lógica y será incoherente cuando lo lea el usuario. Si instala el paquete de idioma adecuado, el motor de conversión de texto a voz podrá leer el correo electrónico y los elementos de calendario al usuario de Outlook Voice Access utilizando el idioma correcto, además de proporcionar mensajes de asistencia por voz grabados previamente en un idioma concreto para la mensajería unificada. En ciertos casos, también podrán admitir el reconocimiento automático de voz.


> [!NOTE]
> El motor de conversión de texto a voz convierte el texto en voz, pero no la voz en texto. Un usuario habilitado para mensajería unificada puede enviar a otro usuario un mensaje de correo electrónico que contenga un archivo de voz adjunto. No obstante, no pueden crear ni enviar mensajes de correo electrónico basados en texto a otro usuario.



Al instalar un paquete de idioma, el programa de instalación realiza los siguiente:

1.  Copia los mensajes de asistencia por voz del idioma que se van a usar para configurar los planes de marcado y los operadores automáticos de mensajería unificada.

2.  Permite al motor TTS leer mensajes cuando un usuario de Outlook Voice Access tiene acceso a su Bandeja de entrada.

3.  Habilita el reconocimiento automático de voz para los planes de marcado y los operadores automáticos de mensajería unificada habilitados para voz para el idioma instalado.

4.  Habilita la vista previa de correo de voz para clientes en otros idiomas.

Puede agregar paquetes de idioma de mensajería unificada mediante el comando **Setup.exe** o la ejecución del programa de instalación *\<UMLanguagePack\>*.exe después de haber descargado el paquete de idioma de mensajería unificada de los [paquetes de idioma de mensajería unificada para Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=266542). Sin embargo, debe usar el comando Setup.exe para quitar un paquete de idioma de mensajería unificada. No existe ningún cmdlet del Shell de administración de Exchange para agregar o quitar idiomas de un servidor de buzones de correo. Para obtener más información acerca de cómo instalar un paquete de idioma de UM, vea [Instalar un paquete de idioma de mensajería unificada](install-a-um-language-pack-exchange-2013-help.md). Para obtener más información acerca de cómo quitar un paquete de idioma de mensajería unificada, vea [Quitar un paquete de idioma de mensajería unificada](remove-a-um-language-pack-exchange-2013-help.md).


> [!NOTE]
> De manera predeterminada, al instalar un servidor de buzones de correo, se instala el paquete de idioma inglés de los Estados Unidos (en-US). No se puede eliminar a no ser que elimine el servidor Buzón de correo del equipo.



Volver al principio

En la tabla siguiente aparece una lista de los paquetes de idioma de mensajería unificada que hay disponibles. Asimismo, se indica el nombre del archivo de instalación de cada uno de ellos y el Id. de referencia cultural del idioma de UM.

### Id. de referencia cultural y nombres de archivos de instalación de paquetes de idioma de UM

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Idioma</th>
<th>País o región</th>
<th>Id. de referencia cultural</th>
<th>Nombre de archivo de instalación</th>
<th>Disponibilidad</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Catalán</p></td>
<td><p>España</p></td>
<td><p>ca-ES</p></td>
<td><p>UMLanguagePack. ca-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Chino (Hong Kong)</p></td>
<td><p>China</p></td>
<td><p>zh-HK</p></td>
<td><p>UMLanguagePack. zh-HK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Chino (simplificado)</p></td>
<td><p>China</p></td>
<td><p>zh-CHS</p></td>
<td><p>UMLanguagePack.zh-CN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Chino (tradicional)</p></td>
<td><p>Taiwán</p></td>
<td><p>zh-TW</p></td>
<td><p>UMLanguagePack.zh-TW</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Danés</p></td>
<td><p>Dinamarca</p></td>
<td><p>da-DK</p></td>
<td><p>UMLanguagePack.da-DK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Holandés</p></td>
<td><p>Países Bajos</p></td>
<td><p>nl-NL</p></td>
<td><p>UMLanguagePack.nl-NL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Inglés</p></td>
<td><p>Australia</p></td>
<td><p>en-AU</p></td>
<td><p>UMLanguagePack.en-AU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Inglés</p></td>
<td><p>Canadá</p></td>
<td><p>en-CA</p></td>
<td><p>UMLanguagePack. en-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Inglés</p></td>
<td><p>India</p></td>
<td><p>en-IN</p></td>
<td><p>UMLanguagePack. en-IN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Inglés</p></td>
<td><p>Reino Unido</p></td>
<td><p>en-GB</p></td>
<td><p>UMLanguagePack.en-GB</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Inglés</p></td>
<td><p>Estados Unidos</p></td>
<td><p>en-US</p></td>
<td><p>Incluido con la instalación de un servidor de buzones de correo</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Finlandés</p></td>
<td><p>Finlandia</p></td>
<td><p>fi-Fl</p></td>
<td><p>UMLanguagePack.fi-Fl</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Francés</p></td>
<td><p>Canadá</p></td>
<td><p>fr-CA</p></td>
<td><p>UMLanguagePack.fr-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Francés</p></td>
<td><p>Francia</p></td>
<td><p>fr-FR</p></td>
<td><p>UMLanguagePack.fr-FR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Alemán</p></td>
<td><p>Alemania</p></td>
<td><p>de-DE</p></td>
<td><p>UMLanguagePack.de-DE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Italiano</p></td>
<td><p>Italia</p></td>
<td><p>it-IT</p></td>
<td><p>UMLanguagePack.it-IT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Japonés</p></td>
<td><p>Japón</p></td>
<td><p>ja-JP</p></td>
<td><p>UMLanguagePack.ja-JP</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Corea</p></td>
<td><p>Coreano</p></td>
<td><p>ko-KR</p></td>
<td><p>UMLanguagePack.ko-KR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Noruego (Bokmal)</p></td>
<td><p>Noruega</p></td>
<td><p>nb-NO</p></td>
<td><p>UMLanguagePack.nb-NO</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Polaco</p></td>
<td><p>Polonia</p></td>
<td><p>pl-PL</p></td>
<td><p>UMLanguagePack.pl-PL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Portugués</p></td>
<td><p>Brasil</p></td>
<td><p>pt-BR</p></td>
<td><p>UMLanguagePack.pt-BR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Portugués</p></td>
<td><p>Portugal</p></td>
<td><p>pt-PT</p></td>
<td><p>UMLanguagePack.pt-PT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Ruso</p></td>
<td><p>Rusia</p></td>
<td><p>ru-RU</p></td>
<td><p>UMLanguagePack. ru-RU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Español</p></td>
<td><p>España</p></td>
<td><p>es-ES</p></td>
<td><p>UMLanguagePack.es-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="odd">
<td><p>Español</p></td>
<td><p>México</p></td>
<td><p>es-MX</p></td>
<td><p>UMLanguagePack.es-MX</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
<tr class="even">
<td><p>Sueco</p></td>
<td><p>Suecia</p></td>
<td><p>sv-SE</p></td>
<td><p>UMLanguagePack.sv-SE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Descarga disponible</a></p></td>
</tr>
</tbody>
</table>


Volver al principio

## Componentes y características de idiomas de mensajería unificada

Existen diversos componentes y características fundamentales en la mensajería unificada que permiten a los usuarios y a las personas que llaman interactuar con un sistema de correo de voz en varios idiomas. Para que estas características y componentes funcionen correctamente y permitan a las personas que llaman interactuar con el sistema en varios idiomas, los paquetes de idioma de mensajería unificada deben instalarse correctamente en un servidor de buzones de correo.

## Mensajes de asistencia por voz grabados previamente

El rol del servidor de buzones de correo se instala con un conjunto de archivos de mensajes de audio predeterminados. Estos archivos de audio contienen las grabaciones de los menús de Outlook Voice Access, saludos de correo de voz y números que se usa la mensajería unificada de Exchange. Las personas que realizan llamadas entrantes internas y externas escucharán estos archivos de audio reproducidos por un servidor de buzones de correo. Muchos de los archivos de audio son mensajes predeterminados que proporcionan a los usuarios de la interfaz de usuario de telefonía (TUI) y de Outlook Voice Access la información que necesitan para desplazarse por la interfaz de usuario de telefonía y por la interfaz de usuario de voz (VUI). Los mensajes de asistencia por voz se encuentran en \<*Archivos de programa*\>\\Microsoft\\Exchange Server\\V15\\UnifiedMessaging\\Prompts\\\<idioma\>. Los mensajes que usa el servidor de buzones de correo para que las personas que llaman puedan desplazarse por los menús no se deben sustituir ni modificar.

Cuando se instala otro paquete de idioma de UM, los mensajes de asistencia por voz previamente grabados de ese idioma también se instalarán. Cuando se instale un paquete de idioma de UM, los planes de marcado y los operadores automáticos de UM podrán usar los mensajes de asistencia por voz previamente grabados de ese idioma.

## Idiomas de TTS

La mensajería unificada se basa en un motor de conversión de texto a voz (TTS). El servicio de Servidor de voz de Microsoft proporciona las funciones de TTS. El motor de TTS lee y convierte texto escrito en formato audible que la persona que llama puede oír. El motor de TTS lee y convierte los elementos siguientes en el buzón de un usuario:

  - Nombres, asuntos y cuerpos de mensajes de correo de voz y electrónico

  - Nombres, ubicaciones, asuntos y cuerpos de elementos de calendario

  - Nombres de contacto personales

  - Saludos de correo de voz predeterminados del usuario


> [!NOTE]
> Cuando un usuario grabe saludos de correo de voz personalizados, la versión de TTS de sus saludos de correo de voz no se volverá a usar.



## Reconocimiento automático de voz

Además de TTS, incluye compatibilidad de ASR en la mensajería unificada. El servicio de servidor de voz de Microsoft proporciona la funcionalidad de ASR. Mediante ASR, las personas que llaman pueden usar comandos de voz desplazarse por los menús e interactuar con elementos desde sus buzones individuales, entre los que se incluyen mensajes, contactos personales y el calendario. Todos los paquetes de idioma admiten el ASR.

Volver al principio

## Vista previa del correo de voz

Además, los paquetes de idioma de mensajería unificada admiten la vista previa de correo de voz, que permite a los usuarios evaluar rápidamente los errores de los mensajes de voz al leer las transcripciones desde un cliente de correo electrónico admitido, como Outlook o Outlook Web App.

Cuando una persona que llama deja un mensaje de voz para un usuario habilitado para mensajería unificada, el archivo del mensaje de voz y una transcripción de este se agregan al cuerpo del mensaje de correo de voz que se enviará al buzón del usuario.

Todos los paquetes de idioma de mensajería unificada son archivos únicos que pueden descargarse. Estos paquetes de idioma incluyen mensajes grabados previamente, archivos de gramática, conversión de texto a voz (TTS) y reconocimiento de voz automático (ASR). Sin embargo, solamente algunos paquetes de idioma de mensajería unificada admiten la vista previa de correo de voz.

Los siguientes paquetes de idioma de mensajería unificada admiten todos los componentes y características, incluida la vista previa de correo de voz:

  - Inglés (EE. UU.) (en-US)

  - Inglés (Canadá) (en-CA)

  - Francés (Francia) (fr-FR)

  - Italiano (it-IT)

  - Polaco (pl-PL)

  - Portugués (Portugal) (pt-PT)

  - Español (España) (es-ES)

De manera predeterminada, cuando instale el servidor de buzones de correo, el servidor enviará vistas previas de correo de voz a usuarios habilitados para mensajería unificada si tienen instalado un paquete de idioma de mensajería unificada compatible.

Algunos socios de vista previa de correo de voz de mensajería unificada ofrecen compatibilidad de transcripción mejorada para la característica de vista previa de correo de voz. Estos socios cuentan con empleados que corrigen las transcripciones de correo de voz creadas con el reconocimiento de voz automático (ASR). Cada socio de Vista previa de correo de voz debe cumplir un conjunto de requisitos para obtener la certificación que le permite interaccionar con la mensajería unificada.

Si cree que las vistas previas del correo de voz que se envían a sus usuarios no son lo suficientemente precisas, puede ponerse en contacto con uno de los socios certificados de Vista previa de correo de voz que aparecen en la página [Microsoft Pinpoint para la mensajería unificada](https://go.microsoft.com/fwlink/p/?linkid=261951) y suscribirse con un costo adicional.

Puede descargar los paquetes de idioma de mensajería unificada del [Centro de descargas de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542). Para obtener información detallada, consulte [Instalar un paquete de idioma de mensajería unificada](install-a-um-language-pack-exchange-2013-help.md).

## Idiomas de mensajería unificada

Para que las personas que llaman puedan utilizar las características de diversos idiomas de la mensajería unificada, es necesario instalar primero un paquete de idioma de mensajería unificada. De este modo, podrá configurar otros componentes de UM.

  - Instale el paquete de idioma de mensajería unificada en los servidores de buzones de correo de su organización.

  - Si es necesario, configure el idioma predeterminado para un plan de marcado de UM determinado. De esta forma, los usuarios de Outlook Voice Access asociados con este plan de marcado de UM usarán el nuevo idioma cuando tengan acceso a su buzón. Sin embargo, los usuarios todavía pueden configurar las opciones de idioma en las opciones de Outlook Web App.

  - Si necesita habilitar varios idiomas en los operadores automáticos, configure la opción de idioma en un operador automático de mensajería unificada. De forma predeterminada, un operador automático de UM usa el idioma del plan de marcado de UM. Sin embargo, es posible cambiar esta configuración y permitir a las personas autenticadas que llaman conectarse a la organización y desplazarse por los menús del operador automático en el idioma que usted haya especificado en el operador automático de UM.

## Paquetes de idioma de mensajería unificada

Instale un paquete de idioma de mensajería unificada en el servidor de buzones de correo mediante Setup.exe. Tras instalar el nuevo paquete de idioma, el idioma asociado al paquete de idioma se agregará a la lista de idiomas disponibles que puede usar. Puede ver los idiomas instalados mediante el cmdlet [Get-UMService](https://technet.microsoft.com/es-es/library/jj552407\(v=exchg.150\)) en el Exchange Shell de administración.

Al instalar los paquetes de idioma de mensajería unificada, se copian los archivos que usan el motor de conversión de texto a voz y los mensajes de asistencia por voz previamente grabados para el idioma elegido, que estarán disponibles para los usuarios que se conecten al sistema de correo de voz. Puede descargar los paquetes de idioma de mensajería unificada del [Centro de descargas de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542). Para obtener información detallada, consulte [Instalar un paquete de idioma de mensajería unificada](install-a-um-language-pack-exchange-2013-help.md).

## Idiomas del plan de marcado de mensajería unificada

Cada plan de marcado de mensajería unificada creado contiene una configuración de idioma predeterminada. La configuración del idioma del plan de marcado de mensajería unificada se necesita porque es posible que la mensajería unificada tenga que utilizar la conversión de texto a voz o reproducir un mensaje de asistencia por voz de audio estándar para los usuarios de Outlook Voice Access cuando obtengan acceso a su buzón. No tiene que seleccionar un idioma de plan de marcado predeterminado.

Cuando se instala Exchange U.S. English por primera vez, el inglés de Estados Unidos es el idioma predeterminado y el único idioma disponible para el plan de marcado. Tras instalar un paquete de idioma de mensajería unificada en un servidor Buzón de correo, el idioma asociado al paquete de idioma también aparecerá como opción disponible al configurar el idioma predeterminado del plan de marcado.

El idioma predeterminado es importante para las personas que llaman. Cuando un usuario de Outlook Voice Access llama al sistema de correo de voz, el idioma que se usa depende de la configuración de idioma en Outlook Web App establecida cuando el usuario inició sesión por primera vez en su buzón de correo. La mensajería unificada compara el idioma establecido en Outlook Web App con la lista de idiomas disponibles del plan de marcado con la que está asociada el usuario. Si no hay una coincidencia adecuada, se utilizará el idioma de plan de marcado de mensajería unificada predeterminado. Por ejemplo, si tiene un plan de marcado que contiene únicamente usuarios de Francia, es posible que desee cambiar la configuración del idioma predeterminado del plan de marcado a Francia.

## Idiomas del operador automático de mensajería unificada

De manera predeterminada, dado que los operadores automáticos de mensajería unificada están asociados con un plan de marcado de mensajería unificada cuando se crean, usarán la configuración de idioma predeterminada del plan de marcado de mensajería unificada asociado. Sin embargo, es posible cambiar esta configuración después de crear el operador automático de mensajería unificada.

La configuración de idioma del operador automático de mensajería unificada es necesaria porque es posible que la mensajería unificada tenga que usar la conversión del motor TTS o reproducir mensajes de audio estándar a una persona que llame. La mensajería unificada no comprueba si el idioma de los mensajes personalizados del operador automático coincide con la configuración de idioma de dicho operador. Sin embargo, se recomienda que compruebe que la configuración de idioma del operador automático coincida con el idioma de los mensajes personalizados. De lo contrario, la persona que llama puede oír el cambio de sistema de un idioma a otro.

La posibilidad de cambiar la configuración de idioma del operador automático de mensajería unificada también es útil si necesita varios operadores automáticos específicos del idioma para las personas que llaman.

## Proceso de selección de idioma del cliente

Los paquetes de idioma de mensajería unificada permiten a las personas que llaman y a los usuarios de Outlook Voice Access interactuar con el sistema de mensajería unificada en varios idiomas. Tras instalar los paquetes de idioma adicionales en un servidor de buzones de correo, los autores de las llamadas y los usuarios de Outlook Voice Access podrán escuchar mensajes de correo electrónico e interactuar con el sistema de correo de voz, y los usuarios de Outlook Web App y los usuarios que usan Outlook 2010 o una versión posterior podrán ver la transcripción de un mensaje de voz mediante la vista previa de correo de voz en un idioma específico.

Para admitir un idioma concreto, debe haber instalado un paquete de idioma de cliente de mensajería unificada para dicho idioma en cada servidor de buzones de correo.

En algunos casos, si no se ha instalado un paquete de idioma de mensajería unificada para un determinado idioma y este no está disponible, se puede usar un idioma de reserva de cliente. Para algunos idiomas, hay disponibles idiomas de cliente de mensajería unificada de reserva, pero para otros idiomas, no hay ninguno disponible. Si no hay instalado un paquete de idioma de mensajería unificada para un idioma concreto, y tampoco hay disponible un idioma de reserva para dicho idioma, se usará el paquete de idioma en-US (inglés de EE. UU.).

En la tabla siguiente se incluye una lista de idiomas de cliente y los idiomas de reserva que se usan cuando no se ha instalado un paquete de idioma de mensajería unificada específico en un servidor de buzones de correo.

### Idiomas de reserva de cliente para mensajería unificada

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Idioma</th>
<th>País o región</th>
<th>Id. de referencia cultural</th>
<th>Primer idioma elegido, si está instalado</th>
<th>Segundo idioma elegid, si está instalado</th>
<th>Tercer idioma elegido, si está instalado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Catalán</p></td>
<td><p>España</p></td>
<td><p>ca-ES</p></td>
<td><p>ca-ES</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Chino (Hong Kong)</p></td>
<td><p>China</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="odd">
<td><p>Chino (simplificado)</p></td>
<td><p>China</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="even">
<td><p>Chino (tradicional)</p></td>
<td><p>Taiwán</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
</tr>
<tr class="odd">
<td><p>Danés</p></td>
<td><p>Dinamarca</p></td>
<td><p>da-DK</p></td>
<td><p>da-DK</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Holandés</p></td>
<td><p>Países Bajos</p></td>
<td><p>nl-NL</p></td>
<td><p>nl-NL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inglés</p></td>
<td><p>Australia</p></td>
<td><p>en-AU</p></td>
<td><p>en-AU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Inglés</p></td>
<td><p>Canadá</p></td>
<td><p>en-CA</p></td>
<td><p>en-CA</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inglés</p></td>
<td><p>India</p></td>
<td><p>en-IN</p></td>
<td><p>en-IN</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Inglés</p></td>
<td><p>Reino Unido</p></td>
<td><p>en-GB</p></td>
<td><p>en-GB</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inglés</p></td>
<td><p>Estados Unidos</p></td>
<td><p>en-US</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Finlandés</p></td>
<td><p>Finlandia</p></td>
<td><p>fi-FL</p></td>
<td><p>fi-FL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Francés</p></td>
<td><p>Canadá</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-FR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Francés</p></td>
<td><p>Francia</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-CA</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Alemán</p></td>
<td><p>Alemania</p></td>
<td><p>de-DE</p></td>
<td><p>de-DE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Italiano</p></td>
<td><p>Italia</p></td>
<td><p>it-IT</p></td>
<td><p>it-IT</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Japonés</p></td>
<td><p>Japón</p></td>
<td><p>ja-JP</p></td>
<td><p>ja-JP</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Coreano</p></td>
<td><p>Corea</p></td>
<td><p>ko-KR</p></td>
<td><p>ko-KR</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Noruego (Bokmal)</p></td>
<td><p>Noruega</p></td>
<td><p>nb-NO</p></td>
<td><p>nb-NO</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Polaco</p></td>
<td><p>Polonia</p></td>
<td><p>pl-PL</p></td>
<td><p>pl-PL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Portugués</p></td>
<td><p>Brasil</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-PT</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Portugués</p></td>
<td><p>Portugal</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-BR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Ruso</p></td>
<td><p>Rusia</p></td>
<td><p>ru-RU</p></td>
<td><p>ru-RU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Español</p></td>
<td><p>España</p></td>
<td><p>es-ES</p></td>
<td><p>es-ES</p></td>
<td><p>es-MX</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Español</p></td>
<td><p>México</p></td>
<td><p>es-MX</p></td>
<td><p>es-MX</p></td>
<td><p>es-ES</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Sueco</p></td>
<td><p>Suecia</p></td>
<td><p>sv-SE</p></td>
<td><p>sv-SE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


Volver al principio

