---
title: 'Definir sus propios tipos de información y plantillas DLP: Exchange 2013 Help'
TOCTitle: Definir sus propios tipos de información y plantillas de DLP
ms:assetid: f4622dba-3347-4758-b4a2-f01b043c908c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ674310(v=EXCHG.150)
ms:contentKeyID: 49896014
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Definir sus propios tipos de información y plantillas de DLP

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-01-14_

Puede desarrollar plantillas de directiva de prevención de pérdida de datos (DLP) como archivos XML independientes de Microsoft Exchange Server 2013 y, a continuación, importarlas mediante el Centro de administración de Exchange o el Shell de administración de Exchange. En esta sección, se describen el proceso y los detalles sobre la creación y el ajuste de archivos XML DLP para usar con una solución DLP. No es necesario que desarrolle sus propios archivos XML DLP, ya que el Centro de administración de Exchange ofrece una manera de comenzar rápidamente con plantillas de directiva DLP y reglas de transporte existentes a fin de analizar mensajes.

¿Está buscando tareas de administración relacionadas con las plantillas de directivas de DLP? Consulte [Procedimientos de DLP](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) o [Procedimientos de DLP](https://technet.microsoft.com/es-es/library/jj938003\(v=exchg.150\)) (Exchange Online).


> [!NOTE]
> Exchange&nbsp;2013: La prevención de pérdida de datos (DLP) es una característica especial que requiere una licencia de acceso de cliente de empresa (CAL) de Exchange. Para obtener más información sobre las CAL y la emisión de licencias del servidor, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licencias de Exchange Server</A>.<BR>Exchange Online: DLP es una característica premium que requiere una suscripción al plan 2 de Exchange Online. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Licencias de Exchange Online</A>.




> [!IMPORTANT]
> En este documento, no se recomienda un modelo de negocios ni información sobre el empaquetado de archivos o las instrucciones de implementación para las reglas de información confidencial ni se analizan cómo se distribuirán esas reglas. Además, este documento no analiza mecanismos de protección, como cifrado, para las reglas personalizadas, ni analiza cómo se implementará ese mecanismo.



## Amplíe los tipos de información para satisfacer sus necesidades

En las siguientes secciones, se describen conceptos y la definición de esquema XML que debe comprender para comenzar a crear sus propios archivos XML para plantillas de directiva DLP y paquetes de reglas de información confidencial que se pueden importar en Exchange 2013 y usarse como directivas DLP.

DLP en Microsoft Exchange ayuda a aplicar una directiva específica de la organización para la información confidencial. Un factor clave de la solidez de una solución DLP es la capacidad de identificar correctamente información confidencial propia de la organización, las necesidades normativas, la geografía y otros aspectos del negocio. Aunque, con el producto, Microsoft proporciona tipos de información confidencial y plantillas de directiva para poder comenzar, las necesidades específicas de su negocio pueden requerir una solución de prevención de pérdida de datos personalizada. Por este motivo, Microsoft ofrece una manera de crear e importar sus propias plantillas de directiva DLP o sus propias definiciones de información confidencial dentro de paquetes de reglas de clasificación. Una solución DLP se basa en la configuración del conjunto adecuado de reglas para el motor de detección de información confidencial que proporcionan un nivel alto de protección y minimizan los falsos positivos y negativos.

## Desarrolle sus propias plantillas de directiva DLP

Puede escribir su propio archivo XML de plantillas de directiva DLP e importarlo. Este enfoque de ampliar la solución DLP ofrecida en Exchange le permitirá crear directivas DLP que se ajusten estrechamente a sus necesidades de DLP.

Administrar plantillas personalizadas y sus correspondientes directivas resulta similar a administrar las directivas de DLP que pueden crearse a partir de las plantillas que proporciona Microsoft. En un ciclo de vida típico de directiva de DLP, debería hacer lo siguiente:

1.  Crear su propia plantilla de directiva de DLP (un archivo XML personalizado). Para más información, vea [Desarrollo de archivos de plantilla de directivas de DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

2.  Importar la plantilla personalizada. Para más información, vea [Importar una plantilla de directiva DLP personalizada desde un archivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

3.  Crear una directiva de DLP basada en la plantilla personalizada. Para más información, vea [Crear una directiva DLP a partir de una plantilla](how-to-new-dlp-data-loss-prevention-policy-template.md).

4.  Repetir los pasos 1 y 2 para actualizar la plantilla personalizada.

5.  Quitar la plantilla personalizada. Para más información, vea [Remove-DlpPolicyTemplate](https://technet.microsoft.com/es-es/library/jj215739\(v=exchg.150\)).

Para obtener más información sobre la definición de esquema XML y los conceptos relacionados con el desarrollo de sus propias plantillas, consulte [Desarrollo de archivos de plantilla de directivas de DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

## Desarrolle sus propios tipos de información confidencial y lógica de coincidencia en paquetes de reglas de clasificación

Puede escribir sus propias definiciones de información confidencial en un paquete de reglas de clasificación, que es un archivo XML, e importarlo como parte de su solución DLP. El motor de detección de información confidencial proporciona las capacidades de análisis profundo de contenido para identificar información confidencial, como números de tarjetas de crédito, números de seguridad social y propiedad intelectual de la empresa. El motor es controlado por un conjunto configurable de instrucciones, o reglas, para analizar el contenido. Las reglas se combinan en un paquete de clasificación de reglas, un documento XML que cumple con una definición de esquema XML de paquete de reglas estandarizado. Y estos son los pasos para desarrollar sus propios tipos de información.

1.  Crear sus propios tipos de información confidencial (un archivo XML personalizado). Para más información, vea [Desarrollar paquetes de reglas de información confidencial](technical-description-of-xml-schema-for-dlp-rule-packages.md).

2.  Importar el tipo de información confidencial. Para más información, vea [New-ClassificationRuleCollection](https://technet.microsoft.com/es-es/library/jj218619\(v=exchg.150\)).

3.  Crear una plantilla personalizada basada en sus tipos de información. Para más información, vea [Desarrollar paquetes de reglas de información confidencial](technical-description-of-xml-schema-for-dlp-rule-packages.md).

4.  Repetir los pasos 1 y 2 para actualizar la plantilla personalizada.

5.  Quitar la plantilla personalizada. Para más información, vea [Remove-ClassificationRuleCollection](https://technet.microsoft.com/es-es/library/jj218670\(v=exchg.150\)).

Para obtener más información sobre los paquetes de reglas, consulte [Desarrollar paquetes de reglas de información confidencial](technical-description-of-xml-schema-for-dlp-rule-packages.md) y [Coincidencia de métodos y técnicas para paquetes de reglas](technical-description-of-xsd-rule-matching-for-dlp-rule-packages.md).

## Comprensión de los tipos de reglas en paquetes de regla

Las reglas de un paquete configuran el proceso para detectar características de contenido bien definidas, por ejemplo, reglas para encontrar un número de licencia de conducir. Hay dos tipos de reglas principales disponibles: Entidad y afinidad.

Las reglas de *entidad* se enfocan en identificadores bien definidos (a menudo, regulados), como números de seguridad social de los EE. UU. Una entidad está representada por una colección de patrones contables. Un patrón define una colección de coincidencias con un identificador de coincidencias principal explícito. Un ejemplo de entidad es una licencia de conducir.

Las reglas de *afinidad* se enfocan en un tipo determinado de documento, como un estado financiero corporativo. Una afinidad se representa como una colección de evidencias independientes. La evidencia es una agregación de coincidencias necesarias dentro de cierta proximidad. Un ejemplo de una afinidad es la ley Sarbanes-Oxley de los EE. UU.

## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Importar una plantilla de directiva DLP personalizada desde un archivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

[New-ClassificationRuleCollection](https://technet.microsoft.com/es-es/library/jj218619\(v=exchg.150\))

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange Server 2013

[Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\))Exchange Online

[Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

