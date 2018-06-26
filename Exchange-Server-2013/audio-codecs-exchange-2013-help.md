---
title: 'Códecs de audio: Exchange 2013 Help'
TOCTitle: Códecs de audio
ms:assetid: 6c39d65c-c2d3-4128-aae9-8596602819c3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998670(v=EXCHG.150)
ms:contentKeyID: 54652435
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Códecs de audio

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

En la mensajería unificada (UM), se usa un códec de audio para almacenar los mensajes de correo de voz. Se usa otro códec entre una puerta de enlace VoIP o central de conmutación (PBX) IP y el servidor de buzones de correo que ejecuta el servicio de mensajería unificada de Microsoft Exchange o el servidor de acceso de cliente que ejecuta el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange. La mensajería unificada puede usar cualquiera de los cuatro códecs de audio siguientes para crear y almacenar mensajes de voz:

  - MP3 (predeterminado)

  - Windows Media Audio (WMA)

  - Group System Mobile (GSM) 06.10

  - Modulación por impulsos codificados (PCM) lineal G.711


> [!WARNING]
> Los códecs G.711 (PCMA y PCMU) y G.723.1 son códecs VoIP que se usan entre una puerta de enlace VoIP y los servidores de acceso de cliente y se buzones.



Parte del planeamiento del sistema de mensajería unificada consiste en elegir el códec de audio según las necesidades y los requisitos de su organización. En este tema, se analizan los códecs de audio que la mensajería unificada puede usar, y puede utilizarlo para ayudar a planear la implementación de mensajería unificada.

## Códecs

El término *códec* es una combinación de las palabras "codificación" y "descodificación", y se usa con datos de audio digitales. Un códec es un software informático que transforma los datos digitales en un formato de archivo de audio o de secuencias de audio. Los códecs se usan para convertir una señal de voz analógica en una versión digital de la señal de voz. Los códecs pueden variar en calidad de sonido, ancho de banda necesario para usarlos y requisitos del sistema necesarios para hacer la codificación.

En mensajería unificada, se usan dos tipos de códecs:

  - El códec utilizado entre una puerta de enlace VoIP, IP-PBX, o PBX habilitada para SIP y los servidores de acceso de cliente y de buzones o entre una PBX o una puerta de enlace VoIP.

  - El códec utilizado para codificar y almacenar mensajes de voz para los usuarios.

Al usar un teléfono normal en la red telefónica pública conmutada (PSTN), la voz se transporta en formato analógico en la línea telefónica. Pero con el protocolo de voz sobre Internet (VoIP), la voz debe convertirse en señales digitales. Este proceso de conversión se conoce como codificación. Un códec realiza la codificación. Después de que la voz digitalizada haya alcanzado su destino, debe decodificarse a su formato analógico original para que la persona que recibe la llamada pueda oír y entender a quien la inició.

## Códec VoIP

En la mensajería unificada (UM), se pueden usar tres tipos de códecs entre puertas de enlace VoIP o IP-PBX y los servidores de acceso de cliente y buzón:

  - G.711 µ-law

  - G.711 A-law

  - G.723.1

G.711 es un estándar que se desarrolló para usarlo con códecs de audio. Existen dos algoritmos principales definidos en el estándar para G.711: el algoritmo µ-law que se usa en los Estados Unidos y el algoritmo A-law que se usa en Europa y en otros países. El códec de audio G.723.1 se usa mayoritariamente en aplicaciones VoIP y necesita una licencia para poder usarse. G.723.1 es un tipo de códec de alta calidad y de compresión elevada.

Un servidor de acceso de cliente o de buzones y una puerta de enlace IP o IP-PBX compatibles pueden ofrecer el códec G.711 y G.723.1. De manera predeterminada, el primer códec que se usa es G.723.1. Si desea usar un códec que no sea G.723.1 entre los servidores de acceso de cliente y de buzones y la puerta de enlace IP o IP-PBX, se recomienda modificar la configuración en la puerta de enlace IP o IP-PBX. En la tabla siguiente se resumen algunos de los códecs VoIP comunes.

### Códecs VoIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Códec VoIP</th>
<th>Ancho de banda (Kbps)</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>64</p></td>
<td><p>Este códec requiere un procesamiento muy lento. Necesita un mínimo de 128 Kb por segundo (Kbps) para una comunicación bidireccional.</p></td>
</tr>
<tr class="even">
<td><p>G.723.1</p></td>
<td><p>5,3/6,3</p></td>
<td><p>Este códec ofrece una compresión alta con audio de alta calidad. Necesita más procesamiento que el códec G.711. El códec G.723.1 usa un ancho de banda reducido pero ofrece una calidad de audio más pobre.</p></td>
</tr>
</tbody>
</table>


## Códec de almacenamiento de mensajes de voz de mensajería unificada

Los planes de conmutación de llamadas de mensajería unificada constituyen una parte integral del funcionamiento de la mensajería unificada. De manera predeterminada, al crear un plan de marcado de mensajería unificada, este usa el códec de audio MP3 para crear y almacenar mensajes de voz. Sin embargo, después de crear el plan de marcado de mensajería unificada, puede configurarlo de forma que utilice los códecs de audio WMA, GSM 06.10 o G.711 PCM lineal.

Cada códec de audio presenta ventajas y desventajas. El códec de audio MP3 se eligió como códec de audio predeterminado debido a su calidad de sonido y propiedades de compresión. Los códecs de audio GSM 06.10 y G.711 PCM Linear se incluyeron como opciones disponibles por su capacidad para admitir otros tipos de sistemas de mensajería.

Cuando planifique la mensajería unificada, debe considerar el tamaño y la calidad relativa del archivo de audio que se creará para los mensajes de correo de voz. Normalmente, cuanto mayor sea la velocidad de bits de un archivo de audio, mayor será su calidad. También debe tener en cuenta si el archivo de audio se va a comprimir. En la siguiente tabla, se muestran la velocidad de muestreo (bits/seg.) y las propiedades de compresión para cada códec de audio usado en la mensajería unificada.

### Códecs de almacenamiento de mensajes de voz de MU predeterminados

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Códec de almacenamiento de mensajes de voz</th>
<th>Bits</th>
<th>¿Archivo comprimido?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>16 bits</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>16 bits</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>G.711 PCM</p></td>
<td><p>16 bits</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>GSM 06.10</p></td>
<td><p>8 bits</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


En la mensajería unificada, el tipo de archivo que se crea para un mensaje de voz depende del códec de audio usado para crear el archivo de audio de mensaje de voz. El códec de audio MP3 crea archivos de audio .mp3, el códec de audio WMA crea archivos de audio .wma y los códecs de audio GSM 06.10 y G.711 PCM lineal crean archivos de audio .wav. Todos estos tipos de archivos de audio se envían junto con un mensaje de correo electrónico al destinatario del mensaje de voz.

Generalmente, pero no siempre, la codificación y descodificación de los datos digitales también implican compresión y descompresión. La compresión de audio es una forma de compresión de datos que reduce el tamaño de los archivos de datos de audio. El algoritmo de compresión de audio que utiliza el códec de audio comprime los archivos de audio .wma o .wav. En la mensajería unificada, el tipo de algoritmo de compresión de audio que se usa se basa en el tipo de códec de audio elegido en las propiedades del plan de mensajería unificada. Después de crear y comprimir el archivo de audio, éste se adjunta al mensaje de voz.

A veces, la información de los datos digitales se pierde durante la compresión y descompresión. Cuanta más alta sea la compresión usada para comprimir el archivo de audio, mayor será la pérdida de información durante la conversión. Sin embargo, se usa menor espacio de disco debido a que se reduce el tamaño del archivo de audio. En cambio, cuanto menor sea la compresión, menor será la pérdida de información. Sin embargo, se usará más espacio de disco debido a que el tamaño del archivo de audio aumenta.

El ancho de banda RTAudio o audio de alta fidelidad para grabar mensajes de voz también está disponible como códec de audio. Sin embargo, el audio de alta fidelidad con RTAudio está disponible solo después de integrar correctamente la mensajería unificada con [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=202010). Para habilitar RTAudio como códec de transferencia, ya sea de banda ancha o estrecha, el plan de marcado de mensajería unificada debe estar configurado como plan de marcado de tipo de URI del Protocolo de inicio de sesión (SIP) y el usuario debe establecer el códec de contestador automático en el plan de marcado como MP3 o WMA para habilitar el audio de banda ancha (16 Khz).


> [!IMPORTANT]
> RTAudio no está disponible en entornos en los que Lync Server no esté implementado. Esto se debe a que, en entornos que no integraron Lync Server, el plan de marcado estará establecido en la extensión del teléfono o E.164 y no en el URI del SIP.



Existen dos flujos de medios para cada llamada entrante: entrante a un servidor de acceso de cliente y saliente desde un servidor de buzones de correo. Cuando el tipo de plan de marcado está establecido en URI de SIP y el códec de respuesta de llamada del plan de marcado está establecido en MP3 o WMA, un servidor de acceso de cliente intenta seleccionar el códec VoIP RTAudio para el flujo de medios de entrada. Si la negociación es correcta, se usará el códec RTAudio para el flujo de entrada en las llamadas de respuesta o en las llamadas que se creen desde un cliente o servidor Lync.


> [!NOTE]
> Las llamadas establecidas para usar la característica Reproducir en teléfono no usarán el códec RTAudio. El flujo de entrada para las llamadas establecidas para usar Reproducir en teléfono utilizará el códec G.711 o G.723.1.



Cuando se usa el códec RTAudio, el mensaje de voz grabado se grabará en alta fidelidad y se almacenará como un archivo de audio con una extensión .mp3 o .wma., según la configuración del plan de marcado. Al reproducir el mensaje de voz de nuevo al usuario en Outlook o Outlook Web App, se escuchará el mensaje de voz en un audio de alta fidelidad. Si la negociación no es correcta, se usará tanto el códec G.711 como el G.723.1. Tanto el códec G.711 como el G.723.1 son códecs de banda estrecha. Al usarlos como el códec VoIP, el mensaje de voz se graba y almacena como un archivo de audio de banda estrecha con una extensión .mp3 o .wma.

El flujo de medio de salida siempre se negociará usando tanto el códec G.711 como el G.723.1. Esto significa que el autor de la llamada siempre escuchará audio de banda estrecha en el teléfono. Esto también se aplica a las situaciones en las que se realiza una llamada mediante Microsoft Lync Server 2010 o posterior.

El formato y el códec de audio que usan los servidores de buzones de correo para almacenar los mensajes de voz de audio no solamente dependen del códec de audio que esté configurado en el plan de marcado, sino también de la velocidad de bits del audio que la mensajería unificada negocia con un interlocutor SIP. Si el entorno incluye extremos SIP o Lync Server, un servidor de buzones de correo también negociará el códec de audio para usar con el interlocutor SIP. Por ejemplo, si se negocia RTAudio de banda ancha como códec de transferencia, el servidor de buzones de correo usará el formato MP3 de 32 Kbps o WMA 9.2 para crear mensajes de voz, en función de la configuración del plan de marcado. En la tabla siguiente se muestra la relación entre el códec de audio de almacenamiento de mensajes de voz y el códec de audio de transferencia o VoIP usado.

### Relación entre el códec de audio de almacenamiento y el códec de audio de transferencia o VoIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Códec de audio configurado en un plan de marcado de mensajería unificada</th>
<th>Códec de transferencia o VoIP (banda estrecha) - G.723, G.711 o RTAudio (8 KHz)</th>
<th>Códec de transferencia o VoIP (banda ancha) - RTAudio (16 KHz)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>G.711</p></td>
<td><p>No aplicable Un servidor de acceso de cliente o de buzones no negocia audio de banda ancha si el plan de marcado está definido en G.711.</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>WMA 9 Voice</p></td>
<td><p>WMA 9.2</p></td>
</tr>
<tr class="odd">
<td><p>GSM</p></td>
<td><p>GSM 6.10</p></td>
<td><p>No aplicable Un acceso de cliente o de buzones no negocia audio de banda ancha si el plan de marcado está definido en GSM.</p></td>
</tr>
<tr class="even">
<td><p>MP3</p></td>
<td><p>MP3 (16 Kbps)</p></td>
<td><p>MP3 (32 Kbps)</p></td>
</tr>
</tbody>
</table>


Códecs

## Tamaño de los mensajes de mensajería unificada

Puede configurar la Mensajería unificada para utilizar uno de los cuatro códecs de audio siguientes para crear mensajes de voz: MP3, WMA, GSM 06.10 y G.711 PCM Linear. El formato MP3 está seleccionado de forma predeterminada.

El códec de audio WMA siempre se almacena en formato multimedia de Windows y los datos adjuntos son un archivo con extensión .wma. Los archivos de audio cifrados mediante los códecs de audio GSM o G.711 PCM Linear siempre se almacenan en formato RIFF/WAV y los datos adjuntos son un archivo con extensión .wav.

El tamaño de los mensajes de voz de mensajería unificada depende del tamaño de los datos adjuntos que contienen los datos de voz. Así, el tamaño de los datos adjuntos depende de los siguientes factores:

  - La duración de la grabación del correo de voz

  - El códec de audio usado

  - El formato de almacenamiento del archivo de audio

La siguiente figura muestra cómo el tamaño del archivo de audio depende de la duración de la grabación del correo de voz para los tres códecs de audio que se pueden usar en MU.


> [!NOTE]
> En esta figura, la longitud media de un mensaje de voz de llamada contestada es de unos 30 segundos.



**Tamaño del archivo de audio**

![UM\_Message\_Sizing](images/Aa998670.76ca4891-450f-4ffd-9493-aac8d0d23a5d(EXCHG.150).gif "UM_Message_Sizing")

## MP3

De forma predeterminada, se selecciona el formato MP3 y es el formato de archivo de audio predeterminado para los mensajes de correo de voz. El formato MP3 es un formato de archivo de audio habitual que se usa para reducir considerablemente el tamaño de los archivos de audio; se trata del formato de audio que usan la mayoría de dispositivos de audio personales y reproductores MP3. MP3 es un códec de audio multiplataforma que se usa para obtener compatibilidad con una amplia variedad de teléfonos móviles, dispositivos y sistemas operativos.

## WMA

WMA es el códec de audio con mayor índice de compresión de los tres tipos de códecs. Su índice de compresión es de unos 11.000 bytes por cada 10 segundos de audio. Sin embargo, el formato de archivo .wma tiene una sección de encabezado mucho más grande que un formato de archivo .wav. La sección de encabezado de un archivo .wma es aproximadamente de 7 kilobytes (KB), mientras que la sección de encabezado de un archivo .wav es de menos de 100 bytes. Aunque las grabaciones de audio WMA se graban durante más de 15 segundos, su tamaño queda más reducido que el de las grabaciones de audio GSM. Por lo tanto, para obtener archivos de audio más pequeños, pero de mayor calidad, utilice el códec de audio WMA.


> [!NOTE]
> Si usa notificaciones de inserción de su implementación local de OWA para dispositivos, no puede usar el formato WMA. OWA para dispositivos solo admite el formato de archivo MP3.



## G.711 PCM Linear

El códec de audio G.711 PCM Linear crea archivos de audio .wav que no se comprimen. Por eso, los archivos de audio G.711 PCM Linear .wav son los que ocupan más espacio, independientemente de su duración, en comparación con los códecs de audio GSM y WMA. Los archivos de audio G.711 PCM Linear .wav ocupan más de 160.000 bytes por cada 10 segundos de audio. Los archivos de audio G.711 PCM lineal .wav ofrecen la mejor calidad de audio de los tres códecs que utiliza la mensajería unificada. Sin embargo, la calidad de los archivos de audio comparables que se crean con los códecs de audio WMA y GSM es aceptable para la mayoría de los usuarios que escuchan mensajes de voz.

## GSM

El códec de audio GSM crea archivos de audio .wav que se comprimen. Los archivos de audio GSM .wav ocupan más de 16.000 bytes por cada 10 segundos de audio. Sin embargo, GSM crea archivos de audio más grandes que los creados por el códec de audio WMA. Por eso, si desea obtener un equilibrio entre la calidad y el tamaño de los mensajes de voz, puede que no se trate de la mejor elección.

Códecs

