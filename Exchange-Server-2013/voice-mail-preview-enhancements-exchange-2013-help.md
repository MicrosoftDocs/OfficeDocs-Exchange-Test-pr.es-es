---
title: 'Mejoras de vista previa del correo de voz: Exchange 2013 Help'
TOCTitle: Mejoras de vista previa del correo de voz
ms:assetid: 1fcccec1-4edc-40b8-948c-111647d7d770
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150501(v=EXCHG.150)
ms:contentKeyID: 48267880
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mejoras de vista previa del correo de voz

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-07-05_

La vista previa del correo de voz es una característica disponible para los usuarios que reciben mensajes de voz con Microsoft Exchange Server 2010 o la mensajería unificada (MU) de Exchange Server 2013. La vista previa del correo de voz mejora la funcionalidad de correo de voz de mensajería unificada proporcionando una versión de texto de las grabaciones sonoras. El texto del correo de voz se muestra en un mensaje de correo electrónico de Microsoft Office Outlook Web App, Outlook 2010 y otros programas de correo electrónico.

## Mejoras de la Vista previa de correo de voz

En Exchange 2013, la mensajería unificada incluye mejoras a la interfaz de usuario de los clientes de Outlook Web App y Outlook y mejoras para incrementar la confianza y la precisión de la vista previa del correo. Además, se ofrecen algunas ventajas a los servicios relacionados con la voz a través de Microsoft Speech Platform (Versión 11.0) y API administrado de comunicaciones unificadas de Microsoft (UCMA) 4.0 para mejorar la generación de gramática y la compatibilidad de idioma.

La mensajería unificada introdujo la característica Vista previa de correo de voz en Exchange 2010. Vista previa de correo de voz usa el reconocimiento de voz automático (ASR) para agregar una versión de texto de un archivo de audio de correo de voz a un mensaje de voz. ASR no es totalmente preciso, sobre todo cuando se usa para grabar audio que incluye voces o ruidos desconocidos con un teléfono.

Algunas organizaciones requieren transcripciones libres de errores, o prácticamente libres de errores, de los mensajes de voz para algunos, o todos, sus usuarios. El programa asociado de vista previa del buzón de voz ayuda a estas organizaciones a cumplir con esos requisitos. En el caso de Exchange 2010, el programa asociado de vista previa del buzón de voz fue diseñado para mejorar los resultados de la Vista previa de correo de voz. Sin embargo, los clientes de Exchange 2010 no lo usaban debido a los gastos generales y los costos del servicio. Para solventar estos problemas, Exchange 2013 incluye las siguientes mejoras para la Vista previa de correo de voz:

  - **Normalización de audio mejorada**   La normalización de audio es el proceso de aumentar (o disminuir) uniformemente la amplitud de una señal de audio completa, de manera que la amplitud máxima resultante coincida con el objetivo o la norma deseada. La mensajería instantánea normaliza la grabación de audio antes de comprimirla y enviarla al usuario.

  - **Reconocimiento de voz mejorado**   Con la recopilación de mensajes de correo de voz (sólo si el cliente de Exchange elije compartir esta información), los resultados de las vistas previas del correo de voz se pueden usar para agregar palabras y frases al motor de voz. Esto se hace configurando el parámetro *VoiceMailAnalysisEnabled* a `$true` usando el cmdlet **Set-UMMailbox** o estableciendo el parámetro *AllowVoiceMailAnalysis* a `$true` en el cmdlet **Set-UMMailboxPolicy**. Además, la mensajería unificada de Exchange 2013 usa de una manera más eficiente la información de subprocesos de correo electrónico que un usuario crea mediante Outlook Voice Access. Esto incluye información sobre el participante (Active Directory o contactos personales), otra información (país, ciudad, compañía) y el número de teléfono del usuario de Outlook Voice Access.

  - **Confianza de vista previa de correo de voz**   La puntuación de confianza es el número que asigna la mensajería unificada directamente relacionado con la precisión general de la transcripción. Los cálculos de confianza que usa la mensajería unificada se han ajustado para que sean más precisos y representen la precisión real del mensaje transcrito.

  - **Filtrado**   La palabras ofensivas se detectan y se filtran y los resultados se almacenan en la caché y en el buzón de correo del usuario.

  - **Ocultar la vista previa del texto**   Si el puntaje de confianza de una vista previa de correo de voz está por debajo de un umbral determinado, se ocultará el texto de la Vista previa de correo de voz. Si el texto está oculto, el mensaje de correo de voz incluirá un texto que indicará que la confianza del correo de voz fue demasiado baja para que se mostraran los resultados.

  - **Rendimiento de la transcripción**   La vista previa de correo de voz es una operación de gran consumo de CPU que requiere prácticamente el doble del tiempo para procesar un archivo de audio. Si se tarda demasiado a generar la vista previa de correo de voz, la limitación de la CPU detiene el procesamiento de la vista previa. En Exchange 2010, la mensajería unificada no transcribe ningún mensaje de voz que supere los 75 segundos. En Exchange 2013, se transcribe todo el mensaje de voz, pero el texto del mensaje no se incluye si dura más de 75 segundos.

  - **Esquemas de color**   Debido a la confusión con los colores que se usaban para distinguir entre confianza baja, media y alta de una vista previa de correo de voz, el esquema de color se ha eliminado en Exchange 2013 para Outlook Web App y Outlook.

