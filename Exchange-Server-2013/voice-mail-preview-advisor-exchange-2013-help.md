---
title: 'Asesor de vista previa de correo de voz: Exchange 2013 Help'
TOCTitle: Asesor de vista previa de correo de voz
ms:assetid: 0957dd54-df6d-4b50-9db5-4757f548b899
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee364730(v=EXCHG.150)
ms:contentKeyID: 51406472
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Asesor de vista previa de correo de voz

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

La mensajería unificada (UM) de Exchange Microsoft incluye una característica denominada Vista previa de correo de voz, que usa el reconocimiento de voz automático (ASR) para agregar una versión en texto del archivo de audio del correo de voz a los mensajes de correo de voz. ASR no es totalmente preciso, sobre todo cuando se usa para grabar audio que incluye voces o ruidos desconocidos con un teléfono. Algunas organizaciones requieren transcripciones sin errores (o casi sin errores) de los mensajes de voz. El programa de asociado de Vista previa de correo de voz puede ayudar a estas organizaciones a cumplir con esos requisitos.

Vista previa de correo de voz usa las [tecnologías de voz de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=187348) para ofrecer una versión de texto de las grabaciones de audio. El texto del correo de voz aparece en los mensajes de correo de MicrosoftOutlook Web App, Outlook 2010 o versiones posteriores, así como en otros programas de correo.

De forma predeterminada, cuando habilita a un usuario para la mensajería unificada en una implementación local o híbrida, las vistas previas del correo de voz se envían si hay instalado un paquete de idioma de UM compatible. Al habilitar a un usuario para la UM en Exchange Online, se instalan todos los paquetes de idioma de este servicio. No obstante, Vista previa de correo de voz no admite todos los idiomas instalados.

Algunos asociados de Vista previa de correo de voz ofrecen soporte y servicios de transcripción mejorados para esta característica. Estos socios cuentan con empleados que corrigen las transcripciones de correo de voz creadas con el reconocimiento de voz automático (ASR). Cada asociado de Vista previa de correo de voz debe cumplir un conjunto de requisitos para obtener la certificación que le permite interaccionar con la mensajería unificada de Exchange.

Si determina que las vistas previas de correo de voz envían a sus usuarios no son suficientemente precisos, usted puede ponerse en contacto con uno de los asociados de negocios certificados de vista previa del correo de voz enumerados en [Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=281966) y signo de consigo un costo adicional.

**Contenido**

Información general

Exchange Unified Messaging Voice Mail Partner program

Voice Mail Preview partners certified for Exchange Unified Messaging

Configuring Voice Mail Preview partners

VoIP or media gateways and IP PBX support

## Información general

Cuando la mensajería unificada registra el audio de un mensaje de correo de voz, usa el ASR para crear texto de vista previa de correo de voz a partir del archivo de audio y luego envía el mensaje de voz completo para que se entregue al usuario. Para todos los mensajes de voz creados, la mensajería unificada determina el nivel de confianza de la vista previa de correo de voz incluida en el mensaje. Calcula la calidad de la coincidencia entre los sonidos y las palabras, números y frases del mensaje. Si el sistema encuentra coincidencias con facilidad, el nivel de confianza es alto. Un mayor nivel de confianza está generalmente asociado con una precisión superior.

La precisión del texto de vista previa de correo de voz depende de varios factores y, a veces, no es posible controlarlos. Sin embargo, es probable que el texto sea más preciso cuando:

  - El autor de la llamada deja un mensaje de voz sencillo y no utiliza argots, jergas técnicas ni palabras o frases poco comunes.

  - La persona que llama usa un idioma que el sistema de correo de voz reconoce y traduce fácilmente. En general, los mensajes de voz que dejan las personas que llaman que no hablan demasiado rápido ni demasiado lento, y que no tienen acentos marcados, producirán oraciones y frases más precisas.

  - El mensaje de voz no tiene ruidos ni ecos de fondo y el audio no se corta.

La mayoría de los clientes que usan la mensajería unificada opinan que las vistas previas de correo de voz son lo suficientemente precisas para sus usuarios. Sin embargo, cuando se aplica ASR a las grabaciones que se realizan por teléfono con voces desconocidas y ruido de fondo, el texto de vista previa de correo de voz, en general, no es absolutamente preciso. Si el nivel de confianza es bajo normalmente o las vistas previas de correo de voz que se reciben no son muy precisas, puede aumentar la precisión de las vistas previas de correo de voz que reciben los usuarios de la siguiente manera:

  - Suscríbase para recibir un servicio de transcripción de voz de un asociado de Vista previa de correo de voz.

  - Después de suscribirse a un asociado de Vista previa de correo de voz, configure el asociado para que funcione con la mensajería unificada. Para más información sobre cómo configurar UM para un asociado de Vista previa de correo de voz, consulte [Configurar servicios de socios de vista previa del correo de voz para los usuarios](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md).

Una vez que se ha suscrito a un asociado de Vista previa de correo de voz, los servidores de Exchange de la organización redirigen los mensajes de voz con el archivo de audio adjunto al asociado de Vista previa de correo de voz en lugar de generar texto de vista previa de correo de voz para los mensajes de voz y enviar estos mensajes al buzón del usuario. Luego, el mensaje de correo con el texto de vista previa de correo de voz que produce el asociado de Vista previa de correo de voz se envía a los servidores de Exchange de la organización para entregarlo al buzón del destinatario.


> [!IMPORTANT]
> Se recomienda que todos los clientes que planean implementar mensajería unificada obtención la asistencia de un especialista en mensajería UNIFICADA. Un especialista en mensajería UNIFICADA le ayuda a asegurarse de que hay una transición sin problemas a la mensajería UNIFICADA de un sistema de correo de voz heredado. Realizar una nueva implementación o actualización de un sistema de correo de voz heredado requiere conocimientos importantes sobre las puertas de enlace VoIP, IP PBX, PBX, controladores de borde de sesión (SBCs) y la mensajería unificada. Para obtener más información acerca de cómo ponerse en contacto con un especialista de mensajería UNIFICADA, consulte el <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 (UM) especialistas en mensajería unificada</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft Pinpoint para mensajería unificada</A>.



Volver al principio

## Programa de asociados de correo de voz de mensajería unificada de Exchange

Para convertirse en un asociado de correo de voz certificado e interoperar con la UM de Exchange, el asociado debe implementar los requisitos incluidos en la especificación de interoperabilidad de asociados de Vista previa de correo de voz y un proveedor de certificación independiente debe certificar la solución del asociado. Si está interesado en certificar su servicio de transcripción para que funcione con la mensajería unificada de Exchange, envíe una solicitud a [Asociados de Vista previa de correo de voz para mensajería unificada](mailto:vmppp@microsoft.com).

## Asociados de Vista previa de correo de voz certificados para la mensajería unificada de Exchange

Si ya ha implementado la mensajería unificada en su organización y está buscando un asociado certificado de vista previa del correo de voz para proporcionar servicios de soporte técnico de transcripción, consulte [Microsoft PinPoint](https://go.microsoft.com/fwlink/p/?linkid=281966). Estos proveedores de software han sido certificados como interoperables con mensajería UNIFICADA de Exchange.

## Configurar asociados de Vista previa de correo de voz

Tras configurar la mensajería unificada, este servicio reenvía los mensajes de voz con el audio a un asociado de Vista previa de correo de voz dedicado, que a partir del archivo de audio crea el texto de vista previa de correo de voz. Sin embargo, para permitir que los usuarios reciban la vista previa de correo de voz con sus mensajes de voz en el buzón, debe configurar una directiva de buzones de correo de UM, asociar los usuarios a la directiva y hacer que estos comprueben si pueden recibir vistas previas de correo de voz en los mensajes de voz en Outlook 2010 (u otra versión posterior) o en Outlook Web App. Para más información sobre cómo configurar UM para un asociado de Vista previa de correo de voz, consulte [Configurar servicios de socios de vista previa del correo de voz para los usuarios](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md).

## Compatibilidad con puertas de enlace VoIP o de medios y con IP PBX

Configurar puertas de enlace VoIP e IP PBX para la organización es una tarea de implementación difícil que se debe completar satisfactoriamente para implementar de forma correcta la mensajería unificada con un asociado de Vista previa de correo de voz. Si quiere información de ayuda para configurar las puertas de enlace VoIP y las IP PBX, e información actualizada para configurarlas, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md) o [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md).

Interoperabilidad de prueba de mensajería UNIFICADA de Exchange con puertas de enlace VoIP se ha integrado con el programa de interoperabilidad de Unified Communications Open Microsoft. Para obtener más información, vea [Microsoft Unified Communications interoperabilidad programa abierto](https://go.microsoft.com/fwlink/p/?linkid=132071).

Volver al principio

