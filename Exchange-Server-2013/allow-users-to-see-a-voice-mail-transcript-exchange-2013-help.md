---
title: 'Permitir a los usuarios ver una transcripción de correo de voz: Exchange 2013 Help'
TOCTitle: Permitir a los usuarios ver una transcripción de correo de voz
ms:assetid: c5192e05-905c-440f-beec-1f697edc15b3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff629381(v=EXCHG.150)
ms:contentKeyID: 51406551
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir a los usuarios ver una transcripción de correo de voz

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

La vista previa del correo de voz es una característica disponible para los usuarios que reciben mensajes de voz de la mensajería unificada. La vista previa del correo de voz mejora la funcionalidad de correo de voz de MU existente proporcionando una versión de texto de las grabaciones sonoras. El texto del correo de voz se muestra en mensajes de correo electrónico de Microsoft Outlook Web App, Outlook 2010 y versiones posteriores y otros programas de correo electrónico. Para obtener más información, consulte [Tecnología de voz de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=187348).

## ¿Hay que usar un programa de correo electrónico específico?

No. La vista previa del correo de voz se incluye en el cuerpo del mensaje de cualquier programa de correo electrónico, incluidos los programas para móviles. Aunque los usuarios pueden utilizar otros programas de correo electrónico para recibir mensajes de voz, Outlook y Outlook Web App proporcionan una mejor experiencia. Por ejemplo, en Outlook 2010 y en versiones posteriores, al hacer clic en una palabra de la vista previa del correo de voz, la reproducción de audio del mensaje de voz empezará a reproducirse desde esa palabra. Es muy útil para oír una parte concreta de un mensaje de voz.

## ¿Los usuarios pueden buscar mensajes de correo de voz específicos?

Sí. Las palabras y frases de la vista previa del correo de voz se indizan automáticamente de modo que los mensajes de voz aparecen en los resultados de búsqueda. En Outlook 2010 y versiones posteriores y en Outlook Web App, los usuarios pueden usar la casilla **Notas de audio** para agregar texto acerca de un mensaje de voz. Estas notas también se incluyen en las búsquedas para que sea más fácil localizar un mensaje.

## ¿Por qué esta característica se denomina "vista previa del correo de voz"?

Es importante que las expectativas de los usuarios sean las correctas. La vista previa del correo de voz no siempre produce un texto idéntico al de los mensajes de voz. De hecho, suele incluir algunas imprecisiones. El uso del término "transcripción" implicaría que el resultado obtenido es más perfecto. "Vista previa" implica que el lector puede entender la idea general del contenido del mensaje, lo que se aproxima más a los resultados reales de la característica.

## ¿Qué hace que el texto de la vista previa del correo de voz sea más o menos preciso?

La precisión de la vista previa del correo de voz depende de muchos factores, algunos de los cuales no se pueden controlar. Sin embargo, es probable que el texto de la vista previa del correo de voz sea más preciso cuando:

  - El autor de la llamada deja un mensaje de voz sencillo sin términos de jerga, vocabulario técnico ni palabras o frases extrañas.

  - El autor de la llamada utiliza un idioma que el sistema de correo de voz puede reconocer y traducir fácilmente. Generalmente, los mensajes de voz de personas que no hablan muy rápido ni muy bajo y que no tienen acentos muy marcados producen frases más precisas.

  - El mensaje de voz no tiene ruidos ni ecos de fondo y el audio no se corta.

## ¿Qué idiomas se pueden usar con la vista previa del correo de voz?

La vista previa del correo de voz está disponible en los siguientes idiomas:

  - Inglés (EE. UU.) (en-US)

  - Inglés (Canadá) (en-CA)

  - Francés (Francia) (fr-FR)

  - Italiano (it-IT)

  - Polaco (pl-PL)

  - Portugués (Portugal) (pt-PT)

  - Español (España) (es-es)

Si tienes un local o híbrido implementación de mensajería UNIFICADA, puede descargar los paquetes de idioma de mensajería UNIFICADA desde el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=266542).

Si tiene una implementación híbrida o local, después de instalar el paquete de idioma de mensajería unificada, los planes de marcado y los operadores automáticos se pueden configurar para usar el idioma elegido. En cuanto a los clientes en línea, no tiene que instalar ningún paquete de idioma de mensajería unificada. Muchas compañías tienen un único plan de marcado de mensajería unificada. La mensajería unificada intentará crear una vista previa del correo de voz en el idioma predeterminado del plan de marcado, pero solo se realizará correctamente si el idioma predeterminado es compatible con la vista previa del correo de voz. El plan de marcado de mensajería unificada solo puede configurarse para crear vistas previas de correo de voz en un idioma cada vez.

Si desea configurar la mensajería unificada para que ofrezca vistas previas de correo de voz en un idioma que no sea en-US, siga estos pasos:

1.  Compruebe que la vista previa del correo de voz incluye el idioma que desea usar.

2.  Si tiene una implementación local o híbrida, descargue e instale el paquete de idioma de mensajería unificada adecuado. El idioma predefinido del plan de marcado no se configura al descargar e instalar el paquete de idioma.

3.  Configure el plan de marcado con el idioma que se usará en la vista previa del correo de voz. Para obtener más información, consulte [Establecer el idioma predeterminado en un plan de marcado](set-the-default-language-on-a-dial-plan-exchange-2013-help.md).

El modo en que la vista previa del correo de voz muestra el texto en los idiomas admitidos depende del tipo de mensaje de voz. Existen dos tipos:

  - **Mensajes de voz grabados cuando un usuario no responde al teléfono**
    
    En estos mensajes, el idioma utilizado en la vista previa del correo de voz depende del idioma que habla el autor de la llamada y de si dicho idioma se admite. Por ejemplo, si una persona deja un mensaje de voz en italiano, el texto de la Vista previa del correo de voz aparecerá en italiano si se ha configurado ese idioma en el plan de marcado. Sin embargo, si lo deja en japonés, no se incluirá texto de vista previa del correo de voz porque ese idioma no está incluido.

  - **Mensajes de voz que se envían a un usuario de Outlook Voice Access**
    
    En los mensajes enviados por un usuario de Outlook Voice Access, el administrador de correo de voz controla el idioma usado para la vista previa de correo de voz. Por lo tanto, el texto de vista previa del correo de voz estará en el mismo idioma que el sistema de correo de voz. Si una persona que habla un idioma incompatible con la Vista previa del correo de voz utiliza Outlook Voice Access para dejar un mensaje, no se incluirá la vista previa del correo de voz. Para obtener más información acerca de Outlook Voice Access, consulte [Configuración de Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md).

## ¿La mensajería unificada detecta si la vista previa de correo de voz es inexacta?

El nivel de confianza se determina para cada vista previa de correo de voz incluida con un mensaje de voz. El sistema de correo de voz mide el nivel de coincidencia de los sonidos de la grabación con las palabras, los números y las frases. Si se encuentran coincidencias fácilmente, el nivel de confianza es alto. Un mayor nivel de confianza suele ir asociado con una mayor precisión.

Si se determina que el nivel de confianza es menor que un valor determinado, la frase **Vista previa de correo de voz (baja confianza)** se incluye encima del texto de la vista previa del correo de voz. Si el nivel de confianza es bajo, es probable que la vista previa del correo de voz sea imprecisa.

La mensajería unificada usa Reconocimiento de voz automático (ASR) para calcular la confianza en la vista previa, pero no puede determinar qué palabras están mal y cuáles son correctas.

Sin embargo, la mensajería unificada intenta aprender para mejorar la precisión de las vistas previas de correo de voz. Así, intenta hacer coincidir el número de teléfono de autor de la llamada (si se proporciona) con los contactos personales del usuario y la libreta de direcciones de su organización o contactos de sus redes sociales. Si la mensajería unificada encuentra una coincidencia, incluirá el nombre del autor de la llamada con sus listas estándar de nombres y palabras, al aplicar el ASR sobre la grabación de voz.

## ¿Se puede usar la vista previa del correo de voz si no es completamente precisa?

La experiencia de uso de la vista previa del correo de voz será mejor si no intenta leer el texto palabra por palabra. Lo recomendable es buscar nombres, números de teléfonos y frases como "Llámeme" o "Tenemos que hablar", que darán pistas sobre el objetivo de la llamada.

La vista previa de correo de voz no está pensada para transcribir mensajes sino para ayudar a responder preguntas como las siguientes:

  - ¿Se trata de un mensaje de voz relacionado con mi trabajo?

  - ¿Es un mensaje de voz importante para mí?

  - ¿Han dejado un número de teléfono? ¿Es diferente de los números que pueda tener para el autor de la llamada?

  - ¿El autor de la llamada considera que el mensaje es urgente?

  - ¿Debería salir de una reunión para llamar a esa persona?

  - Esperaba una llamada para confirmar una solicitud. ¿Se trata de la llamada de confirmación?

## ¿Se puede activar o desactivar la vista previa del correo de voz?

Sí. Si ha habilitado la vista previa del correo de voz, los usuarios pueden activarla o desactivarla con Outlook 2010 o versión posterior o Outlook Web App. Sin embargo, el idioma del plan de marcado debe ser compatible con la vista previa del correo de voz y el paquete de idioma correspondiente para la MU debe estar instalado.

Aunque la configuración de la vista previa del correo de voz es la misma con Outlook 2010 o una versión posterior o con Outlook Web App, el modo de acceso es diferente:

**Outlook Web App**

Para tener acceso a la configuración de la vista previa de correo de voz en Outlook Web App, los usuarios hacen clic en **Configuración** \> **teléfono** \> **Correo de voz**. En la página **Correo de voz**, la configuración está disponible en **vista previa de correo de voz**.

Ambas opciones de vista previa del correo de voz están disponibles de manera predeterminada cuando un usuario tiene habilitada la mensajería unificada. Si el plan de marcado de mensajería unificada está configurado para usar un paquete de idioma compatible con la vista previa del correo de voz, un servidor de mensajería unificada creará vistas previas de correo de voz para los usuarios cuando:

  - Alguien deje un mensaje de voz porque el usuario no responde al teléfono.

  - Un usuario con mensajería unificada inicie sesión en Outlook Voice Access y grabe un mensaje de voz para uno o más destinatarios.

Cuando un usuario deja un mensaje de voz y está seleccionada la opción **Incluir vista previa con los mensajes de voz recibidos**, la mensajería unificada creará una vista previa de correo de voz en el mensaje de correo electrónico, adjuntará el archivo de audio y lo enviará al buzón de correo del destinatario. Tal vez desee desactivar esta opción si el idioma configurado en el plan de marcado no es compatible con la vista previa de correo de voz y no desea incluir vistas previas de correo de voz en los mensajes de correo de voz.

Cuando los usuarios inician sesión en Outlook Voice Access y envían un mensaje de voz a otro usuario, puede que quieran desactivar la casilla **Incluir texto de vista previa con los mensajes de voz que envíe mediante Outlook Voice Access**. Por ejemplo, puede que deseen hacerlo si envían mensajes de voz en un idioma no compatible con la vista previa de correo de voz, o si no desean incluir la vista previa de correo de voz con el mensaje de voz porque es demasiado largo.

