---
title: Introducción a la creación de huella digital de documento en Exchange
TOCTitle: Creación de huella digital de documento
ms:assetid: 1e0c579c-26e0-462a-a1b0-d7506dfe05fa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn635176(v=EXCHG.150)
ms:contentKeyID: 61204104
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creación de huella digital de documento

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-09-11_

Los trabajadores de la información en su organización tratan con diversos tipos de información confidencial durante un día normal. La *creación de huella digital de documento* facilita la protección de esta información al identificar los formularios estándar que se usan en toda la organización. En este tema se describen los conceptos detrás de la creación de huella digital de documento. Si quiere aprender a crear una huella digital de documento, consulte [Proteger los datos de formulario con huellas digitales de documentos](protect-form-data-with-document-fingerprinting-exchange-2013-help.md).

## Escenario básico para la creación de huella digital de documento

La creación de huella digital de documento es una característica de prevención de pérdida de datos (DLP) que convierte un formulario estándar en un tipo de información confidencial, que puede usar para definir reglas de transporte y directivas DLP. Por ejemplo, puede crear una huella digital de documento con base en una plantilla de patente en blanco y después crear una directiva DLP que detecte y bloquee todas las plantillas de patente salientes que incluyan contenido confidencial. Opcionalmente, puede configurar [Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md) para notificar a los remitentes que podrían estar enviando información confidencial, y que el remitente deba comprobar que los destinatarios están calificados para recibir las patentes. Este proceso funciona con cualquier formulario basado en texto que se use en la organización. Algunos ejemplos adicionales de formularios que puede cargar son:

  - Formularios de gobierno

  - Formularios de cumplimiento de Health Insurance Portability and Accountability Act (HIPAA)

  - Formularios de información sobre empleados para los departamentos de recursos humanos

  - Formularios personalizados creados específicamente para la organización

Idealmente, la organización ya tiene una práctica de negocios establecida sobre el uso de determinados formularios para transmitir información confidencial. Tras cargar un formulario vacío para que se convierta en una huella digital de documento y se configure una directiva correspondiente, el agente de DLP detectará cualquier documento en el correo saliente que coincida con esa huella digital.

## Funcionamiento de la creación de huella digital de documento

Probablemente ya adivinó que los documentos no tienen huellas digitales reales, pero el nombre ayuda a explicar la característica. Del mismo modo que las huellas digitales de una persona tienen patrones únicos, los documentos tienen patrones de palabras únicos. Cuando carga un archivo, el agente de DLP identifica el patrón de palabras único del documento, crea una huella digital de documento con base en dicho patrón y la usa para detectar documentos salientes que contenga el mismo patrón. Por ello, la carga de un formulario o plantilla crea el tipo más efectivo de huella digital de documento. Todas las personas que rellenan un formulario usan el mismo conjunto de palabras original y después agregan sus propias palabras al documento. Siempre y cuando el documento saliente no esté protegido por contraseña y tenga todo el texto del formulario original, el agente de DLP puede determinar si el documento coincide con la huella digital de documento.

El siguiente ejemplo muestra qué sucede si crea una huella digital de documento con base en una plantilla de patente, pero puede usar cualquier formulario como base para crear una huella digital de documento.

**Ejemplo de documento de patente que coincide con una huella digital de documento de una plantilla de patente**

![Un documento de patente que coincide con una huella digital de documento.](images/Dn635176.9c952770-2cd4-4f62-9735-6d073344be7f(EXCHG.150).png "Un documento de patente que coincide con una huella digital de documento.")

La plantilla de patente contiene los campos en blanco "Título de patente", "Inventores" y "Descripción", así como descripciones para cada uno de esos campos. Ese es el patrón de palabras. Cuando carga la plantilla de patente original, es uno de los tipos de archivo admitidos y con texto sin formato. El agente de DLP usa un algoritmo para convertir este patrón de palabras en una huella digital de documento, que es un pequeño archivo XML Unicode con un valor hash único que representa el texto original. La huella digital se guarda como una clasificación de datos en Active Directory. (Como medida de seguridad, el propio documento original no se almacena en el servicio; solo se almacena el valor hash y el documento original no se puede reconstruir a partir del valor hash). A continuación, la huella digital de patente se convierte en un tipo de información confidencial que puede asociar con una directiva DLP. Tras asociar la huella digital con una directiva DLP, el agente de DLP detecta cualquier correo electrónico saliente con documentos que coincidan con la huella digital de patente y se ocupa de estos según las directivas de la organización. Por ejemplo, tal vez quiera configurar una directiva DLP que impida que los empleados regulares envíen mensajes salientes que contengan patentes. El agente de DLP usará la huella digital de patente para detectar patentes y bloquear dichos mensajes de correo electrónico. Por otro lado, tal vez quiera permitir que el departamento jurídico tenga la capacidad de enviar patentes a otras organizaciones porque tiene una necesidad empresarial de hacerlo. Puede permitir que determinados departamentos envíen información confidencial creando excepciones para dichos departamentos en su directiva DLP, o bien puede permitirles que invaliden una sugerencia de directiva con una justificación empresarial. Para obtener información más detallada sobre la creación de reglas y excepciones de directivas DLP, consulte [Procedimientos de DLP](https://technet.microsoft.com/es-es/library/jj938003\(v=exchg.150\)). Y para obtener más información sobre la configuración de sugerencias de directivas que los usuarios pueden invalidar, consulte [Administrar las sugerencias de las directivas](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).

## Tipos de archivo admitidos

Creación de huella digital de documento admite los mismos tipos de archivo que se admiten en las reglas de transporte. Para obtener una lista de los tipos admitidos, consulte [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/es-es/library/jj919236\(v=exchg.150\)). Nota rápida sobre los tipos de archivo: ni las reglas de transporte ni la creación de huella digital de documento admiten el tipo de archivo .dotx, lo cual puede resultar confuso porque es un archivo de plantilla de Word. Cuando ve la palabra "plantilla" en este y otros temas de creación de huella digital de documento, se refiere a un documento que se ha establecido como formulario estándar, no al tipo de archivo de plantilla.

## Limitaciones de la creación de huella digital de documento

El agente de DLP de la creación de huella digital de documento no detectará información confidencial en los siguientes casos:

  - Archivos protegidos por contraseña

  - Archivos que solo contienen imágenes

  - Documentos que no contienen todo el texto del formulario original utilizado para crear la huella digital de documento

## Más información

[Proteger los datos de formulario con huellas digitales de documentos](protect-form-data-with-document-fingerprinting-exchange-2013-help.md)

[Integración de las reglas de información confidencial con las reglas de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[Procedimientos de DLP](https://technet.microsoft.com/es-es/library/jj938003\(v=exchg.150\))

