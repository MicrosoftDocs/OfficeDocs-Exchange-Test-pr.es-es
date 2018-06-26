---
title: 'Conversión de contenido: Exchange 2013 Help'
TOCTitle: Conversión de contenido
ms:assetid: bc367eb3-0306-4da9-9a84-4341caef77af
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232174(v=EXCHG.150)
ms:contentKeyID: 49895874
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conversión de contenido

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

*Conversión de contenido* es el proceso de formatear correctamente un mensaje para cada destinatario. La decisión de llevar a cabo la conversión de contenido de un mensaje depende del destinatario y del formato del mensaje que se está procesando. En Microsoft Exchange Server 2013, existen dos tipos de conversión de contenido diferentes:

  - **Conversión de mensajes para destinatarios externos**   Este tipo de conversión de contenido incluye las opciones de conversión de Formato de encapsulamiento neutro para el transporte (TNEF) y las opciones de codificación de mensajes para los destinatarios externos. No es necesario convertir el tipo de contenido de los mensajes enviados a destinatarios dentro de la organización de Exchange. El categorizador administra la conversión de este tipo de contenido en el servicio de transporte en el servidor Buzón de correo. La categorización se produce en los mensajes cuando se coloca un mensaje recién llegado en la cola de envío. Además de la resolución de destinatario y de enrutamiento, la conversión de contenido se realiza en el mensaje antes de que se ponga en la cola de envío. Si un único mensaje contiene varios destinatarios, el categorizador determina la codificación adecuada para cada destinatario del mensaje. El seguimiento de conversión de contenido no detecta los errores en la conversión de contenido con los que se encuentra el categorizador cuando convierte los mensajes que se envían a los destinatarios externos.

  - **Conversión de MAPI para destinatarios internos**   El servicio de transporte de buzones administra este tipo de conversión de contenido. El servicio de transporte de buzones existe en los servidores Buzón de correo para transmitir los mensajes entre las bases de datos de buzones de correo en el servidor local y el servicio de transporte en los servidores Buzón de correo. Específicamente, el servicio de envío de transporte de buzones transmite mensajes desde la bandeja de salida del remitente hasta el servicio de transporte en un servidor Buzón de correo. El servicio de entrega de transporte de buzones transmite mensajes desde el servicio de transporte en un servidor Buzón de correo hasta la bandeja de entrada del destinatario. El servicio de envío de transporte de buzones convierte todos los mensajes salientes de MAPI y el servicio de entrega de transporte de buzones convierte todos los mensajes entrantes a MAPI. El seguimiento de la conversión de contenido detecta estos errores de conversión de MAPI. Para obtener más información, vea [Seguimiento de conversión de contenido](content-conversion-tracing-exchange-2013-help.md).

Este tema explica las opciones de conversión de mensajes para destinatarios externos.

**Contenido**

Formatos de mensajes de Exchange y Outlook

Opciones de conversión de contenido para destinatarios externos

Información sobre la estructura de los mensajes de correo electrónico

## Formatos de mensajes de Exchange y Outlook

En la siguiente lista se describen los formatos básicos de mensajes que hay disponibles en Exchange y Microsoft Outlook:

  - **Texto sin formato**   Un mensaje de texto sin formato usa solamente texto US-ASCII tal y como se describe en RFC 2822. El mensaje no puede contener diferentes fuentes o formato de texto. Los dos siguientes formatos se pueden usar para un mensaje de texto sin formato:
    
      - Los encabezados de mensaje y el cuerpo del mensaje están compuestos por texto US-ASCII. Los adjuntos tendrían que codificarse mediante *Uuencode*. Uuencode representa una codificación de Unix a Unix y define un algoritmo de codificación para almacenar documentos adjuntos binarios en el cuerpo de un mensaje de correo electrónico mediante el uso de caracteres de texto US-ASCII.
    
      - El mensaje está codificado con MIME con un valor de tipo de contenido de texto/sin formato, y un valor de codificación de transferencia de contenido de 7 bits para las partes de texto de un mensaje de varias partes. Cualquier dato adjunto del mensaje se codifica con el método de entrecomillado imprimible o Base64. De manera predeterminada, cuando escribe y envía un mensaje de texto sin formato en Outlook, el mensaje se codifica en MIME con un valor de tipo de contenido de texto/sin formato.

  - **HTML**   Un mensaje HTML es compatible con el formato del texto, imágenes de fondo, tablas, viñetas y otros elementos gráficos. Por definición, un mensaje con formato HTML tiene que estar codificado en MIME para conservar estos elementos de formato.

  - **Formato de texto enriquecido (RTF)**    RTF es compatible con formato de texto y otros elementos gráficos. RTF es sinónimo de TNEF. TNEF y RTF se pueden usar de manera intercambiable. El formato del mensaje de texto enriquecido es totalmente diferente al formato de documento de texto enriquecido disponible en Microsoft Word.
    
    Solo Outlook y algunos clientes de correo electrónico MAPI comprenden los mensajes RTF.

  - **TNEF**   El formato de encapsulamiento neutro en el transporte es un formato específico de Microsoft para encapsular las propiedades de los mensajes MAPI. Un mensaje codificado mediante TNEF contiene una versión del mensaje en texto sin formato y datos adjuntos que empaquetan la versión original del mensaje con formato. Normalmente, estos datos adjuntos se denominan Winmail.dat e incluyen la siguiente información:
    
      - La versión del mensaje original con formato, incluidos, entre otros, las fuentes, tamaños y colores del texto
    
      - Los objetos OLE, por ejemplo imágenes incrustadas o documentos insertados de Microsoft Office
    
      - Características especiales de Outlook, como formularios personalizados, botones de voto o convocatorias de reunión
    
      - Datos adjuntos normales de mensaje que estaban en el mensaje original
    
    El mensaje de texto sin formato resultante se puede representar en los siguientes formatos:
    
      - Un mensaje compatible con RFC 2822 que se componga solamente de texto EE. UU.-ASCII con datos adjuntos Winmail.dat codificados en UUencode
    
      - Un mensaje de varias partes codificado en MIME que tenga un archivo Winmail.dat como datos adjuntos
    
    Un cliente de correo electrónico compatible con MAPI que entiende perfectamente TNEF, como Outlook, procesa los datos adjuntos Winmail.dat y muestra el contenido del mensaje original sin mostrar nunca los datos adjuntos Winmail.dat. Un cliente de correo electrónico que no entiende TNEF puede presentar un mensaje en TNEF de varias maneras:
    
      - La versión sin formato del mensaje se visualiza, y el mensaje contiene unos datos adjuntos llamados Winmail.dat, o algún otro nombre genérico como Att*nnnnn*.dat o Att*nnnnn*.eml, en los que el marcador de posición *nnnnn* representa un número aleatorio.
    
      - La versión de texto sin formato del mensaje se visualiza. Los datos adjuntos en TNEF se ignoran o se quitan. El resultado es un mensaje de texto sin formato.
    
      - Los servidores de mensajería que entienden el formato TNEF se pueden configurar para quitar los datos adjuntos TNEF de los mensajes entrantes. El resultado es un mensaje de texto sin formato. También hay algunos clientes de correo electrónico, como Microsoft Outlook Express, que podrían no entender TNEF pero sí reconocer y omitir los documentos adjuntos TNEF. El resultado es un mensaje de texto sin formato.
    
    Hay utilidades de terceros que pueden ayudar a convertir los datos adjuntos Winmail.dat.
    
    TNEF es entendido por todas las versiones de Exchange desde Exchange Server, versión 5.5.

  - **Formato de encapsulamiento neutro para el transporte de resumen (STNEF)**   STNEF es equivalente a TNEF. Sin embargo, los mensajes STNEF están codificados de manera diferente a los mensajes TNEF. En concreto, los mensajes STNEF siempre están codificados en MIME y siempre tienen un valor de codificación de la transferencia de contenido de binario. Por consiguiente, el mensaje no se representa en texto sin formato y no aparecen datos adjuntos Winmail.dat en el cuerpo del mensaje. El mensaje entero se representa sólo mediante datos binarios. Los mensajes que contienen un valor binario de codificación de la transferencia de contenido solamente se pueden transferir entre servidores de mensajería SMTP que admiten y que anuncian las extensiones BINARYMIME y CHUNKING SMTP, tal y como se define en RFC 3030. Los mensajes siempre se transfieren entre los servidores de mensajería SMTP mediante el comando BDAT, en vez del comando estándar DATA.
    
    STNEF es entendido por todas las versiones de Exchange desde Exchange 2000. STNEF se usa automáticamente para todos los mensajes que se transfieren entre los servidores Exchange en la organización desde el modo nativo Exchange Server 2003.
    
    Exchange nunca manda mensajes con formato STNEF a destinatarios externos. Solamente se pueden enviar mensajes TNEF a destinatarios fuera de la organización de Exchange.

Volver al principio

## Opciones de conversión de contenido para destinatarios externos

Las opciones de conversión de contenido que puede establecer en una organización Exchange para destinatarios externos se pueden describir en las siguientes categorías:

  - **Opciones de conversión TNEF**   Estas opciones de conversión especifican si se ha de quitar o conservar el formato TNEF en los mensajes que salen de la organización de Exchange.

  - **Opciones de codificación de mensaje**   Estas opciones especifican las opciones de codificación de mensaje, como los conjuntos de caracteres MIME y no MIME, codificación de mensaje y formatos de datos adjuntos.

Estas opciones de conversión y codificación son independientes las unas de las otras. Por ejemplo, el hecho de que los mensajes TNEF puedan salir de la organización de Exchange no tiene nada que ver con las opciones de configuración de la codificación MIME o la configuración de codificación de texto sin formato de esos mensajes.

Puede especificar la conversión del contenido a diferentes niveles de la organización de Exchange tal y como se describe en la siguiente lista:

  - **Configuración de dominio remoto**   Los dominios remotos definen la configuración de las transferencias de mensajes salientes entre la organización de Exchange y los dominios externos. Incluso si no crea entradas de dominio remoto para dominios específicos, hay un dominio remoto predeterminado llamado Predeterminado que se aplica a todos los espacios de direcciones remotos (\*).

  - **Configuración de usuario de correo y de contacto de correo**   Los usuarios de correo y contactos de correo son similares ya que ambos tienen direcciones de correo electrónico externas y contienen información acerca de personas fuera de la organización de Exchange. La diferencia principal es que los usuarios de correo tienen cuentas que se pueden usar para iniciar sesión en el dominio de Active Directory y obtener acceso a recursos en la organización.

  - **Configuración de Outlook**   En Outlook, puede establecer las opciones de formato y codificación de mensajes descritas en la siguiente lista:
    
      - **Formato de mensaje**   Puede fijar el formato de mensaje predeterminado para todos los mensajes. Puede invalidar el formato de mensaje predeterminado al tiempo que escribe un mensaje específico.
    
      - **Formato de mensaje interno**   Puede controlar si los mensajes TNEF se envían a destinatarios remotos o si primero se convierten a un formato más compatible. También puede especificar diferentes opciones de codificación para mensajes que se envían a destinatarios remotos. Esta configuración no se aplica a los mensajes enviados a destinatarios de la organización de Exchange.
    
      - **Formato de mensaje de destinatario de Internet**   Puede controlar si los mensajes TNEF se envían a destinatarios específicos o si primero se convierten a un formato más compatible. Puede establecer las opciones de conversión para contactos específicos en su carpeta de contactos, y puede invalidar las opciones de conversión para un destinatario específico en los campos Para, CC o CCO, a medida que redacta un mensaje. Estas opciones de conversión no están disponibles para destinatarios de la organización de Exchange.
    
      - **Opciones de codificación de mensajes para destinatarios de Internet**   Puede controlar las opciones de codificación de MIME o de texto sin formato para contactos específicos de su carpeta de contactos y puede invalidar las opciones de conversión para un destinatario específico en los campos Para, CC o CCO, a medida que redacta un mensaje. Estas opciones de conversión no están disponibles para destinatarios de la organización de Exchange.
    
      - **Opciones internacionales**   Puede controlar los conjuntos de caracteres que se usan en los mensajes.

## Opciones de conversión de TNEF

Puede establecer las opciones de conversión de TNEF en los siguientes niveles:

  - Configuración del dominio remoto

  - Configuración del usuario de correo y el contacto de correo

  - La configuración de Outlook, que incluye:
    
      - Formato del mensaje
    
      - Formato de los mensajes de Internet
    
      - Formato de los mensajes de destinatario de Internet

## Opciones de la codificación de mensajes

Puede establecer las opciones de codificación de mensajes en los siguientes niveles:

  - Configuración del dominio remoto

  - Configuración del usuario de correo y el contacto de correo

  - La configuración de Outlook, que incluye:
    
      - Formato del mensaje
    
      - Mensaje de Internet
    
      - Formato de los mensajes de destinatario de Internet
    
      - Opciones de codificación del conjunto de caracteres del mensaje

Para obtener información, vea [Opciones de la codificación de mensajes](message-encoding-options-exchange-2013-help.md).

Volver al principio

## Información sobre la estructura de los mensajes de correo electrónico

Para comprender mejor las opciones de conversión de contenido para los destinatarios externos, necesita comprender la estructura de los mensajes de correo electrónico. Un mensaje SMTP se basa en un texto US-ASCII de 7 bits sin formato para componer y enviar mensajes de correo electrónico. Un mensaje SMTP estándar consiste en los siguientes elementos:

  - **El sobre del mensaje**   El sobre del mensaje está definido en RFC 2821 y contiene información necesaria para transmitir y entregar el mensaje. Los destinatarios nunca ven el sobre del mensaje porque lo genera el proceso de transmisión y no forma parte del contenido del mensaje.

  - **El contenido del mensaje**   El contenido del mensaje está definido en RFC 2822 y se compone de los siguientes elementos:
    
      - **El encabezado del mensaje**   Se trata de una colección de campos de encabezado. Los campos de encabezado consisten en el nombre del campo, seguido de dos puntos (:), después el cuerpo del campo y por último una combinación de caracteres de retorno de carro y avance de línea (CR/LF).
        
        Un nombre de campo tiene que estar compuesto por caracteres de texto US-ASCII imprimibles, a excepción del carácter de los dos puntos (:). En concreto, se permiten los caracteres ASCII que tengan valores comprendidos entre 33 y 57 y entre 59 y 126.
        
        Un cuerpo de campo puede estar compuesto por cualquier carácter US-ASCII, excepto los caracteres de retorno de carro (CR) y de avance de línea (LF). Sin embargo, un cuerpo de campo puede contener una combinación de caracteres CR/LF cuando se usa en un *doblado de encabezado*. El doblado de encabezado es la separación de un único cuerpo de campo de encabezado en varias líneas, tal y como se describe en la sección 2.2.3 de RFC 2822. En las secciones 3 y 4 de RFC 2822 se describen otros requisitos de sintaxis de cuerpo de campo.
    
      - **El cuerpo del mensaje**   El cuerpo del mensaje es una colección de líneas de caracteres de texto US-ASCII que aparece después del encabezado del mensaje. El encabezado del mensaje y el cuerpo del mensaje están separados por una línea en blanco que termina con la combinación de caracteres CR/LF. El cuerpo de mensaje es opcional. Cualquier línea de texto en el cuerpo del mensaje tiene que tener menos de 998 caracteres. Los caracteres de retorno de carro y de avance de línea solamente aparecen juntos para indicar el final de una línea.

Cuando los mensajes SMTP contienen elementos que no son texto sin formato US-ASCII, el mensaje tiene que ir codificado para preservar esos elementos. El estándar MIME define un método de codificación de contenido de mensajes que no es de texto. MIME permite texto con otros conjuntos de caracteres, datos adjuntos sin texto, cuerpos de mensajes de varias partes y campos de encabezado en otros conjuntos de caracteres. MIME está definido en RFC 2045, RFC 2046, RFC 2047, RFC 2048 y RFC 2077. MIME define una colección de campos de encabezado que especifica atributos de mensaje adicionales. En la tabla siguiente se describen algunos campos de encabezado MIME importantes.

### Campos de encabezado MIME importantes

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de campo de encabezado</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Versión de MIME</p></td>
<td><p>1,0</p></td>
<td><p>Este campo de encabezado es el primer campo de encabezado MIME que aparece en un mensaje con formato MIME. Este campo de encabezado aparece después de los otros campos de encabezado estándar RFC 2822, pero antes que cualquier campo de encabezado MIME. Los clientes de correo electrónico para MIME usan este campo de encabezado para identificar un mensaje codificado con MIME. Cuando no existe este campo de encabezado, los clientes de correo electrónico para MIME identifican el mensaje como texto sin formato.</p></td>
</tr>
<tr class="even">
<td><p>Tipo de contenido</p></td>
<td><p>texto/sin formato</p></td>
<td><p>Este campo de encabezado identifica el tipo de medio del contenido del mensaje tal y como se describe en RFC 2046. Un tipo de medio consiste en un tipo, un subtipo y uno o varios parámetros opcionales, como el parámetro <em>charset=</em>, que define la codificación de caracteres MIME. Los tipos que comienzan con &quot;x-&quot; no son estándar. Los subtipos que comienzan con &quot;vnd.&quot; son específicos del proveedor. Internet Assigned Numbers Authority (IANA) tiene una lista de los tipos de medio registrados. Si desea obtener más información, vea <a href="https://www.iana.org/assignments/media-types/">Tipos de medios MIME</a>.</p>
<p>El tipo de medio <em>multiparte</em> permite varias partes de mensaje dentro del mismo mensaje mediante secciones definidas por diferentes tipos de medio. Algunos valores de campo del tipo de contenido incluyen texto/sin formato, texto/html, varias partes/mixto y varias partes/alternativo.</p></td>
</tr>
<tr class="odd">
<td><p>Codificación de la transferencia de contenido</p></td>
<td><p>7 bytes</p></td>
<td><p>Este campo de encabezado puede describir la siguiente información de un mensaje:</p>
<ul>
<li><p>El algoritmo de codificación que se usó para transformar cualquier texto no EE. UU.-ASCII o datos binarios que se hallan en el cuerpo del mensaje.</p></li>
<li><p>Un indicador que describe la condición actual del cuerpo del mensaje.</p></li>
</ul>
<p>Un mensaje MIME puede contener varios valores del campo de encabezado de la codificación de transferencia de contenido. Cuando el campo de encabezado de la codificación de transferencia de contenido aparece en el encabezado del mensaje, se aplica a todo el cuerpo del mensaje. Cuando el campo de encabezado de la codificación de transferencia de contenido aparece en una de las partes de un mensaje de varias partes, se aplica sólo a esa parte del mensaje.</p>
<p>Cuando se aplica un algoritmo de codificación a los datos del cuerpo de un mensaje, estos se transforman en texto US-ASCII sin formato. La transformación permite al mensaje explorar servidores de mensajería SMTP antiguos que sólo admiten mensajes en texto US-ASCII. Los valores del campo de encabezado de la codificación de transferencia de contenido que indican que se usó un algoritmo de codificación en el cuerpo del mensaje, son los siguientes:</p>
<ul>
<li><p><strong>Entrecomillado imprimible</strong>   Este algoritmo de codificación usa caracteres US-ASCII imprimibles para codificar los datos del cuerpo del mensaje. Si el texto del mensaje original está en su mayor parte en EE. UU.-ASCII, la codificación entrecomillada e imprimible produce resultados compactos y más o menos legibles. Todos los caracteres de texto EE. UU.-ASCII imprimibles, excepto el signo de igual ( = ), se pueden representar sin codificarse.</p></li>
<li><p><strong>Base64</strong>   Este algoritmo de codificación está basado principalmente en el estándar Correo de privacidad mejorada (PEM) definido en RFC 1421. La codificación Base64 usa el algoritmo de codificación del alfabeto de 64 caracteres, así como caracteres de relleno de salida que están definidos en PEM para codificar los datos del cuerpo del mensaje. Un mensaje codificado con Base64 suele ser un 33% mayor que el mensaje original. La codificación con Base64 crea un incremento predecible en el tamaño del mensaje y es óptimo para los datos binarios y texto que no sea US-ASCII.</p></li>
</ul>
<p>Por lo general, no se ven los diferentes algoritmos de codificación usados en el mismo mensaje.</p>
<p>Cuando no se ha usado ningún algoritmo de codificación en el cuerpo del mensaje, el campo de encabezado de codificación de transferencia de contenido simplemente identifica la condición actual de los datos del cuerpo del mensaje. Los siguientes valores del campo de encabezado de codificación de transferencia de contenido indican que no se usaron algoritmos de codificación en el cuerpo del mensaje:</p>
<ul>
<li><p><strong>7 bit</strong>    Este valor indica que los datos del cuerpo del mensaje ya tienen el formato RFC 2822. En concreto, significa que las siguientes condiciones deben ser verdaderas:</p>
<ul>
<li><p>Todas las líneas de texto han de contener menos de 998 caracteres.</p></li>
<li><p>Todos los caracteres deben estar en formato EE. UU.-ASCII y tener valores de carácter entre 1 y 127.</p></li>
<li><p>Los caracteres de retorno de carro y de avance de línea solamente pueden usarse juntos para indicar el final de una línea.</p></li>
</ul>
<p>El cuerpo entero del mensaje puede que sea de 7 bytes, o parte del cuerpo de un mensaje multiparte puede ser de 7bytes. Si el mensaje multiparte contiene otras partes que tienen datos binarios o texto no US-ASCII, esa parte del mensaje tiene que ser codificada con los algoritmos de codificación de entrecomillado imprimible o Base64.</p>
<p>Los mensajes que tengan cuerpos de 7bytes pueden explorar servidores de mensajería SMTP mediante el comando estándar DATA.</p></li>
<li><p><strong>8 bytes</strong>   Este valor indica que los datos del cuerpo del mensaje contienen caracteres que no son US-ASCII. En concreto, significa que las siguientes condiciones deben ser verdaderas:</p>
<ul>
<li><p>Todas las líneas de texto deben contener menos de 998 caracteres.</p></li>
<li><p>Uno o más de los caracteres en el cuerpo de mensaje tiene valores superiores a 127.</p></li>
<li><p>Los caracteres de retorno de carro y de avance de línea solamente pueden usarse juntos para indicar el final de una línea.</p></li>
</ul>
<p>El cuerpo entero del mensaje puede que sea de 8 bytes, o parte del cuerpo de un mensaje multiparte puede ser de 8 bytes. Si el mensaje multiparte contiene otras partes que tienen datos binarios, esa parte del mensaje tiene que ser codificada con los algoritmos de codificación de entrecomillado imprimible o Base64.</p>
<p>Los mensajes con cuerpos de 8 bits solamente pueden navegar entre servidores de mensajería SMTP que sean compatibles con la extensión 8BITMIME SMTP, tal y como se define en RFC 1652, como en los servidores que ejecutan Exchange 2000 Server o versiones posteriores. En concreto, significa que las siguientes condiciones deben ser verdaderas:</p>
<ul>
<li><p>La palabra clave 8BITMIME tiene que anunciarse en la respuesta del servidor EHLO.</p></li>
<li><p>Se siguen transmitiendo los mensajes mediante el comando estándar DATA de SMTP. Sin embargo, se tiene que agregar el parámetro BODY=8BITMIME al final del comando MAIL FROM.</p></li>
</ul></li>
<li><p><strong>Binario</strong>   Este valor indica que el cuerpo del mensaje contiene datos binarios o caracteres que no son US-ASCII. En concreto, significa que las siguientes condiciones son verdaderas:</p>
<ul>
<li><p>Se permite cualquier secuencia de caracteres.</p></li>
<li><p>No hay límite de longitud de línea.</p></li>
<li><p>Los elementos de mensaje binarios no necesitan codificación.</p></li>
</ul>
<p>Los mensajes con cuerpos binarios solamente pueden navegar entre servidores de mensajería SMTP que sean compatibles con la extensión BINARYMIME SMTP, tal y como se define en RFC 3030, como en los servidores que ejecutan Exchange 2000 Server o versiones posteriores. En concreto, significa que las siguientes condiciones deben ser verdaderas:</p>
<ul>
<li><p>La palabra clave BINARYMIME tiene que anunciarse en la respuesta del servidor EHLO.</p></li>
<li><p>La extensión BINARYMIME SMTP solamente se puede usar con la extensión CHUNKING SMTP. <em>Fragmentación</em> permite que se manden los cuerpos de mensaje grandes en varios y pequeños fragmentos. La fragmentación también se define en RFC 3030. La clave CHUNKING también tiene que anunciarse en la respuesta del servidor EHLO.</p></li>
<li><p>Los mensajes se transfieren mediante el comando BDAT, en vez del comando estándar DATA.</p></li>
<li><p>El parámetro <em>BODY=BINARYMIME</em> se tiene que agregar al final del comando MAIL FROM cuando el mensaje tiene cuerpo de mensaje.</p></li>
</ul></li>
</ul>
<p>Los valores 7 bytes, 8 bytes y binario nunca pueden existir al mismo tiempo en el mismo mensaje multiparte. Los valores son mutuamente excluyentes. Los valores de entrecomillado imprimible o Base64 pueden aparecer en un cuerpo de mensaje multiparte de 7 bytes u 8 bytes, pero nunca en un cuerpo de mensaje binario. Si el cuerpo de un mensaje de varias partes contiene diferentes partes con contenido de 7 y 8 bits, el mensaje entero se clasifica como de 8 bits. Si el cuerpo de un mensaje multiparte contiene diferentes partes compuestas por contenido de 7 bytes, 8 bytes y binario, el mensaje entero se clasifica como binario.</p></td>
</tr>
<tr class="even">
<td><p>Disposición del contenido</p></td>
<td><p>Datos adjuntos</p></td>
<td><p>Este campo de encabezado indica al cliente de correo electrónico con MIME cómo debería visualizar unos documentos adjuntos, tal y como se describe en RFC 2183. Los valores de este campo pueden ser en línea o datos adjuntos. Cuando el valor de este campo es en línea, los datos adjuntos se visualizan en el cuerpo del mensaje. Cuando el valor de este campo son datos adjuntos, el archivo adjunto aparece como datos adjuntos normales, separado del cuerpo del mensaje. Hay otros parámetros disponibles cuando el valor es datos adjuntos, como nombre de archivo, fecha de creación y tamaño.</p></td>
</tr>
</tbody>
</table>


Volver al principio

