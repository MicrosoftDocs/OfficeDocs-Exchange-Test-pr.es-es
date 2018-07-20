---
title: 'Planes de marcado de mensajería unificada: Exchange 2013 Help'
TOCTitle: Planes de marcado de mensajería unificada
ms:assetid: ed7afc03-94af-4b23-8745-6a61f203c149
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125151(v=EXCHG.150)
ms:contentKeyID: 49895999
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planes de marcado de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-21_

Los planes de marcado de mensajería unificada (MU) son el componente principal de la mensajería unificada y son necesarios para implementar correctamente el correo de voz de mensajería unificada en la red. En las siguientes secciones, se describen los planes de marcado de mensajería unificada y cómo se usan en una implementación de mensajería unificada.

## Introducción a los planes de marcado de mensajería unificada

Un plan de marcado de mensajería unificada representa un conjunto de centrales de conmutación (PBX) o IP PBX que comparten números de extensión de usuarios comunes. Todas las extensiones de usuarios hospedadas en PBX o IP PBX en un plan de marcado contienen la misma cantidad de dígitos. Los usuarios pueden marcar otra extensión de teléfono sin anexar un número especial a la extensión o sin marcar un número de teléfono completo.

Un plan de marcado de mensajería unificada refleja un plan de marcado de telefonía. Un plan de marcado de telefonía se configura en centrales de conmutación o IP PBX.

En la mensajería unificada, pueden existir las siguientes topologías de planes de marcado:

  - Un plan de marcado único que representa un subconjunto de extensiones o todas las extensiones de una organización que tiene una central de conmutación o una IP PBX.

  - Un plan de marcado único que representa un subconjunto de extensiones o todas las extensiones de una organización que tiene varias centrales de conmutación o IP PBX conectadas en red.

  - Varios planes de marcado que representan un subconjunto de extensiones o todas las extensiones de una organización que tiene una central de conmutación o una IP PBX.

  - Varios planes de marcado que representan un subconjunto de extensiones o todas las extensiones de una organización que tiene varias centrales de conmutación o varias IP PBX.

Los usuarios que pertenecen al mismo plan de marcado tienen las siguientes características:

  - Un número de extensión que identifica únicamente el buzón del usuario en el plan de marcado.

  - La capacidad de llamar o enviar mensajes de voz a otros miembros del plan de marcado usando sólo el número de extensión.

Para obtener más información acerca de cómo habilitar a un usuario para la mensajería unificada, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

Los planes de marcado de mensajería unificada se usan en la mensajería unificada para garantizar que las extensiones telefónicas de los usuarios son únicas. En algunas redes de telefonía, pueden existir varias PBX o IP PBX. En estas redes de telefonía, pueden existir dos usuarios que tengan el mismo número de extensión telefónica. Los planes de marcado de mensajería unificada resuelven esta situación. Al poner a dos usuarios en dos planes de marcado de mensajería unificada separados, las extensiones son únicas.

## Cómo funcionan los planes de marcado

Al integrar una red de telefonía con la mensajería unificada, deben existir uno o varios dispositivos de hardware llamados puerta de enlace de voz sobre IP (VoIP) o IP PBX que conecten la red de telefonía con la red de conmutación de paquetes basada en IP. Las puertas de enlace de VoIP convierten los protocolos de conmutación de circuitos de una PBX que se encuentran en una red de telefonía en un protocolo de conmutación de datos, como IP. Las IP PBX también convierten protocolos de conmutación de circuitos en un protocolo de conmutación de datos. Los controladores de borde de sesión (SBC) permiten conectar dos redes basadas en IP a través de una WAN pública o privada, y se encuentran en implementaciones de mensajería unificada híbridas o en línea. Cada puerta de enlace VoIP, IP PBX o controlador de borde de sesión (SBC) de la organización están representados por una puerta de enlace IP de MU. Para obtener más información acerca de las puertas de enlace IP de mensajería unificada, vea [Puertas de enlace IP de mensajería unificada](um-ip-gateways-exchange-2013-help.md) .

La mensajería unificada requiere que al menos cree un plan de marcado de mensajería unificada. Independientemente de que cree uno o más planes de marcado, todos los servidores Exchange de la organización responderán las llamadas entrantes. También debe haber una o varias puertas de enlace IP de mensajería unificada asociadas con el plan de marcado. En implementaciones híbridas y locales, después de instalar servidores Exchange y asociar una puerta de enlace IP de mensajería unificada, todos los servidores Exchange responderán las llamadas entrantes de todos los planes de marcado. Sin embargo, para las implementaciones híbridas o locales, al integrar Exchange y Lync Server, debe crear planes de marcado de URI de SIP.


> [!IMPORTANT]
> Cada vez que se crea un plan de marcado de mensajería unificada, también se crea una directiva de buzón de correo de mensajería unificada predeterminada. La directiva de buzón de correo de mensajería unificada se denomina directiva predeterminada &lt;<EM>Dial Plan Name</EM>&gt;. Esta directiva de buzón de correo de mensajería unificada se puede eliminar o configurar de forma diferente.



Cuando se crea la primera puerta de enlace IP de mensajería unificada y al mismo tiempo se especifica un plan de marcado, también se crea un grupo de extensiones de mensajería unificada predeterminado. La creación de estos componentes permite que los servidores Exchange reciban llamadas de una puerta de enlace VoIP, IP PBX o SBC y, a continuación, procesen esas llamadas entrantes para usuarios asociados con el plan de marcado de mensajería unificada. En las implementaciones locales o híbridas, cuando ingresa una llamada a la puerta de enlace VoIP, a IP PBX o a SBC, esta se reenvía a un servidor de acceso de cliente. A continuación, el servidor de acceso de cliente reenvía la llamada a un servidor de buzones de correo y este último intenta relacionar el número de extensión del usuario con el plan de marcado de mensajería unificada asociado.

## Tipos de planes de marcado

Un identificador uniforme de recursos (URI) es una cadena de caracteres (numéricos o alfabéticos) que se utiliza para identificar un nombre o un recurso. En la mensajería unificada, el principal objetivo de un URI es habilitar dispositivos VoIP para que se comuniquen con otros dispositivos mediante protocolos específicos. Un URI define el formato o esquema de nombres y numeración que se utiliza para la información de la persona que hace la llamada y del destinatario de la misma, y que está contenida en un encabezado de Protocolo de inicio de sesión (SIP) para una llamada entrante o saliente.

Los tipos de planes de marcado de mensajería unificada que puede crear con la mensajería unificada dependerán de los tipos de URI compatibles con las puertas de enlace VoIP o IP PBX de su organización. El tipo de URI es el tipo de cadena que se envía desde la PBX o IP PBX. Cuando cree un plan de marcado, debe conocer los tipos de URI específicos compatibles con sus PBX o IP PBX. Hay tres formatos o tipos de URI que se pueden configurar en los planes de marcado de mensajería unificada:

  - Extensión telefónica (TeleExtn)

  - URI de SIP

  - E.164

De manera predeterminada, cada vez que se crea un plan de marcado en la mensajería unificada, este plan usará el tipo de URI de extensión telefónica. Después de crear un plan de marcado, no podrá cambiar el tipo de URI. Debe eliminar el plan de marcado existente y crear otro con el tipo de URI correcto.

## Tipo de URI de extensión telefónica

El tipo de URI de extensión telefónica es el tipo de plan de marcado de mensajería unificada más común y se utiliza con IP PBX y PBX. Cuando configura un plan de marcado de extensión telefónica (TelExtn), las puertas de enlace VoIP, PBX e IP PBX que use deberán ser compatibles con el tipo de URI de TelExtn. Hoy en día, la mayoría de las PBX e IP PBX admiten este tipo de URI.

Cuando la PBX recibe una llamada y el usuario habilitado para mensajería unificada no está disponible para responder, la PBX reenvía la llamada a la puerta de enlace VoIP. La puerta de enlace VoIP, o la IP PBX si se usa una, convertirán la llamada de un protocolo basado en circuitos a un protocolo basado en IP. En el encabezado del paquete SIP recibido desde la puerta de enlace VolP o IP PBX, la información de la persona que llama y del receptor aparecerá con uno de los siguientes formatos:

  - Tel:512345

  - 512345@\<*Dirección IP*\>

El formato de extensión telefónica (TelExtn) que se usa se basa en la configuración de la puerta de enlace VoIP o IP PBX.

## Tipo de URI de SIP

El Protocolo de inicio de sesión (SIP) es un protocolo estándar para iniciar sesiones de usuario interactivas con elementos multimedia como vídeo, voz, chat y juegos. SIP es un protocolo con estructura de solicitud-respuesta que resuelve las solicitudes de clientes y las respuestas de los servidores. Los clientes se identifican mediante los URI de SIP. Las solicitudes se pueden enviar mediante cualquier protocolo de transporte, como UDP o TCP. SIP determina el extremo que se utilizará en la sesión; para ello, selecciona el medio de comunicación y los parámetros del medio.

Al crear un nuevo plan de marcado, tiene la opción de crear un plan de marcado de URI de SIP si el entorno tiene implementado Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. También puede crear un plan de marcado de URI de SIP si la organización tiene IP PBX o PBX habilitadas para SIP. En el último caso, la organización también debe admitir URI de SIP y enrutamiento SIP.

Una URI de SIP es el número de teléfono SIP de un usuario. El URI de SIP es similar a una dirección de correo electrónico y se escribe con el siguiente formato: sip*:\<nombre de usuario\>@\<dominio o dirección IP\>*:*puerto*. Cuando se usa PBX o IP PBX habilitadas para SIP para enviar una llamada a los servidores Exchange, el dispositivo enviará el URI de SIP de la persona que llama y del receptor en el encabezado SIP y no incluirá los números de extensión.

## Tipo de URI E.164

E.164 es un formato de numeración estándar que define el plan de numeración de telecomunicaciones públicas internacionales utilizado en la Red telefónica conmutada (RTC) y algunas redes de datos. E.164 define el formato de los números de teléfono. Los números E.164 pueden tener un máximo de 15 dígitos y normalmente se escriben con un signo más (+) delante de los dígitos del número de teléfono. Para marcar un número de teléfono con formato E.164 desde un teléfono se debe incluir el prefijo de llamada internacional adecuado en el número que se marca. En un plan de numeración E.164 para sistemas de teléfonos públicos, cada número asignado contiene un código de país (CC), un código de destino nacional (NDC) y un número de suscriptor (SN).

Al crear un nuevo plan de marcado, tiene la opción de crear un plan de marcado E.164. Sin embargo, si crea y configura un plan de marcado E.164, las PBX e IP PBX deben ser compatibles con el enrutamiento E.164. El encabezado SIP recibido desde una puerta de enlace VoIP asociada con un plan de marcado E.164 incluirá el número de teléfono con formato E.164 y la información de la persona que llama y del receptor, y se escribirá con el siguiente formato: Tel.: +14255550123. Para las implementaciones de Exchange Online con mensajería unificada de Exchange y Lync Server, debe usar los números E.164 con el formato correcto para los números de Outlook Voice Access y del operador automático.

## seguridad de VoIP

Los servidores Exchange se pueden comunicar con puertas de enlace VolP, IP PBX y otros equipos que ejecutan Exchange en modo no protegido, protegido con SIP o en modo protegido, en función de cómo se haya configurado el plan de marcado de mensajería unificada. En implementaciones híbridas y locales, los servidores de acceso de cliente y de buzones pueden funcionar en cualquier modo configurado en un plan de marcado porque escuchan en el puerto TCP 5060 las solicitudes no protegidas y, en el puerto TCP 5061, las solicitudes protegidas al mismo tiempo si están configurados para iniciarse en modo dual. Los servidores de acceso de cliente y de buzones de correo responden todas las llamadas entrantes para todos los planes de marcado de mensajería unificada, pero esos planes de marcado pueden tener una configuración de seguridad de VoIP distinta.

En implementaciones híbridas y locales, de manera predeterminada, al crear un plan de marcado de mensajería unificada, este se comunicará en modo no protegido, y los servidores de acceso de cliente y de buzones enviarán y recibirán los datos desde puertas de enlace VoIP, IP PBX y SBC sin usar el cifrado. En modo no protegido, no se cifra ni el canal de medios del protocolo de transporte en tiempo real (RTP) ni la información de señalización de SIP. Puede usar el cmdlet **Get-UMDialPlan** en el Shell para determinar la configuración de seguridad para un plan de marcado de mensajería unificada específico.

En implementaciones híbridas y locales, puede configurar un servidor de acceso de cliente y de buzones para que usen la Seguridad de la capa de transporte mutua (TLS mutua) a fin de cifrar el tráfico SIP y RTP enviado y recibido en otros dispositivos y servidores. Al configurar el plan de marcado para usar el modo SIP protegida, únicamente se cifrará el tráfico de señalización de SIP, mientras que los canales de medios RTP seguirán utilizando TCP, que no está cifrado. No obstante, al configurar el plan de marcado para usar el modo Protegida, tanto el tráfico de señalización de SIP como los canales de medios RTP están cifrados. Un canal de medios de señalización cifrado que usa el Protocolo de transporte en tiempo real seguro (SRTP) también usa la TLS mutua para cifrar los datos de VoIP.

Puede configurar el modo de seguridad de VoIP al crear un nuevo plan de marcado o después de crearlo mediante el EAC o el cmdlet **Set-UMDialPlan** en el Shell. Al configurar el plan de marcado de mensajería unificada para que use el modo SIP protegida o Protegida, los servidores de acceso de cliente y de buzones de correo cifrarán el tráfico de señalización de SIP o los canales de medios RTP, o ambos. No obstante, para poder enviar datos cifrados a servidores Exchange, o desde estos, debe configurar correctamente el plan de marcado de mensajería unificada, y los dispositivos VoIP, como puertas de enlace VoIP, IP PBX y SBC, deben admitir la TLS mutua.

## Outlook Voice Access

Hay dos tipos de personas que llaman que tienen acceso al sistema de correo de voz usando el número de Outlook Voice Access configurado en un plan de marcado de mensajería unificada: personas que llaman no autenticadas y personas que llaman autenticadas. Cuando las personas que llaman marcan el número de Outlook Voice Access configurado en un plan de marcado, se las considera anónimas o no autenticadas hasta que proporcionen información, como la extensión de correo de voz y el PIN. La única opción que está disponible para las llamadas anónimas o no autenticadas es la característica de búsqueda de directorio. Después de que las personas que llaman proporcionan la extensión de correo de voz y el PIN, se las autenticará y se les brindará acceso al buzón de correo. Una vez que acceden al sistema de correo de voz, utilizan la característica Outlook Voice Access.

Outlook Voice Access es una serie de solicitudes de voz que permiten que la persona que llama tenga acceso al correo electrónico, el correo de voz, el calendario y otra información. Outlook Voice Access permite a las personas que llaman, una vez autenticadas, consultar la información personal de su buzón, realizar llamadas o buscar otros usuarios mediante el tono de marcado de frecuencia múltiple (DTMF), también llamado marcación por tonos o entradas de voz.

## Números de Outlook Voice Access

Una vez creado el plan de marcado de mensajería unificada, es necesario agregar al menos un número de Outlook Voice Access. Los números de Outlook Voice Access también se denominan números piloto del plan de marcado. Este número es usado por los usuarios de Outlook Voice Access para tener acceso a sus buzones, y les permite buscar en el directorio.

De manera predeterminada, cuando se crea un plan de marcado de mensajería unificada, no se configura ningún número de Outlook Voice Access. Para permitir que los usuarios usen la característica Outlook Voice Access, debe configurar al menos un número de teléfono o extensión. El número de caracteres alfanuméricos del número de Outlook Voice Access no puede superar los 20. Después de configurarlo en el plan de marcado, este número aparecerá en las opciones de correo de voz de Microsoft Outlook y en Outlook Web App.

Puede usar el cuadro **Números de Outlook Voice Access** en el plan de marcado de mensajería unificada para agregar un número de teléfono o extensión al que un usuario llamará para acceder al sistema de correo de voz usando Outlook Voice Access. En la mayoría de los casos habrá que introducir un número de extensión o un número de teléfono externo. No obstante, dado que este campo acepta caracteres alfanuméricos, se puede usar un URI de SIP si está utilizando IP PBX, PBX habilitada para SIP, Office Communications Server 2007 R2 o Microsoft Lync Server.

Según las necesidades de su organización, posiblemente desee configurar uno o varios números de Outlook Voice Access. Puede tener un único número de Outlook Voice Access configurado en un solo plan de marcado de mensajería unificada o puede tener varios números de Outlook Voice Access en un solo plan de marcado de mensajería unificada, pero no puede tener un único número de Outlook Voice Access para varios planes de marcado de mensajería unificada.

