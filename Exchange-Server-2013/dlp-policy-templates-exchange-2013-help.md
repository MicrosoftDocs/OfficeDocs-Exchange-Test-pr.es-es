---
title: 'Plantillas de directiva de DLP: Exchange 2013 Help'
TOCTitle: Plantillas de directiva de DLP
ms:assetid: c7b1a8e4-30d9-4409-85c5-f85ae023737d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657730(v=EXCHG.150)
ms:contentKeyID: 49895902
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Plantillas de directiva de DLP

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-01-14_

Puede utilizar las plantillas de la directiva de Prevención contra la pérdida de datos (DLP) para comenzar con la solución DLP en Microsoft Exchange 2013. Una plantilla de la directiva de DLP es un modelo para una directiva. Puede seleccionar una plantilla para comenzar el proceso de creación de su directiva de DLP personalizada. En la directiva de DLP, puede personalizar las reglas para asegurarse de que cumplen con las necesidades comerciales para la prevención contra la pérdida de datos. Microsoft proporciona varias plantillas de directivas, pero no son la única forma de implementar la solución de prevención contra la pérdida de datos en Exchange.

¿Está buscando tareas de administración relacionadas con las plantillas de directivas de DLP? Consulte [Procedimientos de DLP](dlp-procedures-exchange-2013-help.md).

**Contenido**

Incorporación de plantillas y tipos de información para satisfacer sus necesidades

Creación de su propia plantilla de la directiva de DLP o sus propios tipos de información confidencial en un paquete de reglas de clasificación

Incluye la funcionalidad DLP con las reglas de transporte vigentes

Uso de directivas de DLP creadas por Microsoft

Más información

## Incorporación de plantillas y tipos de información para satisfacer sus necesidades

Puede incorporar definiciones de contenido confidencial y plantillas de directivas de Microsoft Partner o de archivos que usted mismo desarrolla, como una plantilla de la directiva de DLP, tipos de información y reglas ya proporcionadas en Exchange 2013. A continuación le presentamos varias formas de agregar su contenido DLP único y ampliar la funcionalidad de DLP. Las plantillas que Microsoft proporciona son un método convencional para comenzar con una solución de DLP. Para ampliar las características de DLP con sus archivos únicos de plantilla de la directiva de DLP, debe comprender los requisitos del esquema de XML para las plantillas de la directiva creadas independientemente de Exchange. Para obtener más información acerca de los cmdlet del Shell de administración de Exchange asociados con las plantillas de la directiva de DLP, consulte los cmdlet relacionados con `Get-DlpPolicyTemplate` en [Cmdlets de directiva y conformidad](https://technet.microsoft.com/es-es/library/dd298082\(v=exchg.150\)). Además, puede definir sus propios tipos de contenido confidencial una vez que comprenda el formato y procedimiento para incorporarlos. Para obtener más información acerca de los cmdlet del Shell de administración de Exchange asociados con las plantillas de la directiva de DLP, consulte los cmdlet relacionados con `Get-ClassificationRuleCollection` en [Cmdlets de directiva y conformidad](https://technet.microsoft.com/es-es/library/dd298082\(v=exchg.150\)).


> [!WARNING]
> Debe activar sus directivas de DLP en modo de prueba antes de ejecutarlas en su entorno de producción. Durante dichas pruebas, se recomienda que configure buzones de usuarios de ejemplo y envíe mensajes de prueba que invoquen las directivas de prueba para confirmar los resultados.



## Creación de su propia plantilla de la directiva de DLP o sus propios tipos de información confidencial en un paquete de reglas de clasificación

Puede crear un archivo con la plantilla de la directiva de DLP independiente de Exchange que coincida con la definición del esquema de XML específico proporcionado por Microsoft y luego importar el archivo a su sistema para que pueda crear directivas de DLP a partir de él. Al crear sus propios archivos de plantilla, puede definir su propio modelo de directivas de DLP que Microsoft aun no ha proporcionado. Esto no es lo mismo que crear una directiva de DLP usando el Centro de Administración de Exchange, que usualmente se da luego de que están disponibles las plantillas de la directiva. Si crea una plantilla de directiva independiente de Exchange, deberá importarla antes de poder usarla para examinar mensajes. También puede crear sus propias definiciones de información confidencial independientes de las definidas por Microsoft en Exchange. Hay una definición del esquema de XML separada para los archivos de plantilla de la directiva de DLP y para los paquetes de reglas de clasificación. Para empezar, consulte la siguiente información:

  -  [Definir sus propios tipos de información y plantillas de DLP](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

  -  [Importar una plantilla de directiva DLP personalizada desde un archivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

## Incluye la funcionalidad DLP con las reglas de transporte vigentes

Puede incorporar capacidades de detección de DLP con reglas de transporte tradicionales sin crear una nueva directiva de DLP. Si usted ha creado un juego complejo de reglas en una versión anterior de Exchange y desea duplicarlas o agregar la detección de información confidencial en Exchange 2013, puede usar el editor de reglas de transporte en el Centro de Administración de Exchange o el Shell de administración de Exchange para incorporar estas características. Para empezar, consulte la siguiente información:

  -  [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

  -  [Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)) (Exchange Online)

  -  [Administrar reglas de flujo de correo](manage-mail-flow-rules-exchange-2013-help.md)
    
  -  [Cmdlets de directiva y conformidad](https://technet.microsoft.com/es-es/library/dd298082\(v=exchg.150\))

## Uso de directivas de DLP creadas por Microsoft

Microsoft proporciona numerosas directivas de DLP. Esta es la forma más sencilla de comenzar con una solución de DLP flexible y simple de implementar. Puede utilizar las directivas proporcionadas en cualquier momento como punto de partida y personalizarlas para que cumplan sus requisitos. Para empezar, consulte la siguiente información:

  - [Plantillas de directivas de DLP suministradas en Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)

  - [Crear una directiva DLP a partir de una plantilla](how-to-new-dlp-data-loss-prevention-policy-template.md)

## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

