---
title: 'Filtrado de contenido: Exchange 2013 Help'
TOCTitle: Filtrado de contenido
ms:assetid: d660ffbf-de05-46c2-940b-5200eca94e0a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124739(v=EXCHG.150)
ms:contentKeyID: 49895942
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtrado de contenido

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_


> [!NOTE]
> El 1 de noviembre de 2016 Microsoft detuvo las actualizaciones de definiciones de correo no deseado para los filtros de SmartScreen en Exchange y Outlook. Las definiciones existentes de correo no deseado de SmartScreen permanecerán en su lugar, pero es probable que su eficacia se degrade con el tiempo. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange</A> (Fin del soporte de SmartScreen en Outlook y Exchange).



El agente de filtro de contenido evalúa los mensajes de correo entrantes y evalúa la probabilidad de que un mensaje entrante sea legítimo o spam. A diferencia de otras muchas tecnologías filtrados, el agente de filtro de contenido utiliza las características de una muestra estadísticamente significativa de mensajes de correo electrónico. La inclusión de mensajes legítimos en esta muestra reduce la posibilidad de errores. Debido a que el agente de filtro de contenido reconoce las características de los mensajes legítimos como spam, se aumenta su precisión. Actualizaciones para el agente de filtro de contenido están disponibles periódicamente a través de [Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836).

**Contenido**

Usar el agente de filtro de contenido

Configuración del agente de filtro de contenido

## Usar el agente de filtro de contenido

El agente de filtro de contenido es uno de los muchos agentes contra correo electrónico no deseado en Exchange. Cuando se configuran agentes contra correo electrónico no deseado en un servidor Exchange, los agentes actúan en los mensajes de forma acumulativa con el fin de reducir la cantidad de correo no deseado que entra en la organización. Para obtener más información sobre cómo planear e implementar los agentes contra correo electrónico no deseado, consulte [Protección contra correo no deseado](anti-spam-protection-exchange-2013-help.md).

El agente de filtro de contenido asigna una clasificación de confianza de correo no deseado (SCL) a cada mensaje. La clasificación SCL es un número entre 0 y 9. Una clasificación SCL alta indica que el mensaje tiene más posibilidades de ser correo no deseado.

Puede configurar el agente de filtro de contenido para implantar las siguientes acciones en los mensajes de acuerdo con la clasificación de confianza de correo no deseado (SCL):

  - Eliminar mensaje

  - Rechazar mensaje

  - Poner mensaje en cuarentena

Por ejemplo, puede determinar que los mensajes que tienen una clasificación de confianza de correo no deseado (SCL) de 7 o superior se eliminen, que los que tengan una clasificación de confianza de correo no deseado (SCL) de 6 se rechacen y que los que tengan un SCL de 5 se pongan en cuarentena.

Para ajustar el comportamiento del umbral SCL, asigne diferentes clasificaciones SCL a cada una de estas acciones. Para obtener más información sobre cómo ajustar el umbral SCL de modo que se adapte a las necesidades de su organización y sobre los umbrales SCL por destinatario, consulte [Umbral de nivel de confianza de correo no deseado](spam-confidence-level-threshold-exchange-2013-help.md).


> [!NOTE]
> El filtro inteligente de mensajes no analiza los mensajes que superan los 11&nbsp;MB. En su lugar, pasan a través del filtro de contenido sin que se examinen.



## Permitir expresiones y expresiones no autorizadas

Puede personalizar cómo asigna el agente de filtro de contenido valores de la clasificación de confianza de correo no deseado (SCL) configurando palabras personalizadas. Las palabras personalizadas son palabras individuales o frases que usa el agente de filtro del contenido para aplicar el procesamiento del filtro apropiado. Configure palabras aprobadas o expresiones con Expresiones permitidas y palabras no aprobadas o expresiones con Expresiones no autorizadas. Cuando el agente de filtro de contenido detecta una expresión permitida preconfigurada en un mensaje entrante, dicho agente asigna automáticamente un valor SCL de 0 al mensaje. Por otro lado, cuando detecta una expresión no autorizada configurada en un mensaje entrante, asigna una clasificación SCL de 9.

Puede escribir palabras o expresiones personalizadas empleando cualquier combinación de letras en mayúscula y minúscula. Sin embargo, cuando el agente de filtro de contenido evalúa el contenido del mensaje, pasa por alto lo de las mayúsculas y minúsculas. El número máximo de palabras o expresiones personalizadas que se pueden crear es de 800.

## Validación del certificado electrónico Outlook

El agente de filtro de contenido también incluye validación del certificado electrónico Microsoft Office Outlook, una prueba computacional que Outlook aplica a los mensajes salientes para ayudar a los sistemas de mensajería de los destinatarios a distinguir el correo electrónico legítimo del no deseado. Esta característica ayuda a reducir la posibilidad de falsos positivos. En el contexto de un filtrado de correo no deseado, existe un *falso positivo* cuando el filtro de correo no deseado identifica de forma incorrecta un mensaje de un remitente legítimo como correo electrónico no deseado. Cuando la validación de certificado electrónico Outlook está habilitada, el agente de filtro de contenido analiza el mensaje entrante en busca de un encabezamiento de certificado computacional. La presencia de un encabezamiento de certificado computacional válido y resuelto en el mensaje indica que el equipo del cliente que generó el mensaje resolvió dicho certificado.

Los equipos no necesitan invertir demasiado tiempo en el procesamiento para resolver certificados computacionales individuales. Sin embargo, los certificados de procesamiento de muchos mensajes pueden ser prohibitivos para un remitente dañino. No es probable que la persona que envía millones de mensajes de correo electrónico no deseado invierta la capacidad de procesamiento necesaria para resolver certificados de todos los correos electrónicos no deseados salientes. Si el correo electrónico de un remitente contiene un certificado computacional válido y resuelto, no es probable que el remitente sea un remitente malintencionado. En este caso, el agente de filtrado de contenido bajaría la clasificación SCL. Si la característica de validación de certificados está habilitada y un mensaje entrante no contiene un encabezamiento de certificado computacional, o dicho encabezamiento no es válido, el agente de filtro de contenido no variará la clasificación SCL.

## Omitir el destinatario, el remitente y el dominio del remitente

En algunas organizaciones, se deben aceptar todos los correos electrónicos de ciertos alias. Esta situación puede conllevar problemas si su organización pertenece a un sector que gestiona grandes volúmenes de correo electrónico no deseado.

Por ejemplo, una compañía llamada Woodgrove Bank tiene el alias customerloans@woodgrovebank.com, que proporciona soporte de correo electrónico a clientes de préstamo externos. Los administradores de Exchange configuran el agente de filtro de contenido para establecer expresiones de bloqueo, que filtran las palabras o expresiones que se usan normalmente en los correos electrónicos no deseados enviados por agencias de préstamo sin escrúpulos. Para prevenir que se rechacen mensajes potencialmente legítimos, los administradores establecen excepciones al filtrado de contenido. Para ello, introducen una lista de direcciones de destinatarios de correo electrónico SMTP en la configuración del agente de filtro de contenido.

También puede especificar remitentes y dominios de remitentes que no desea que bloquee el agente de filtro del contenido.

## Agregación de listas seguras

En Exchange 2013, el agente de filtro de contenido usa las listas de remitentes seguros, de remitentes bloqueados, de destinatarios seguros y de contactos de confianza de Outlook para optimizar el filtrado de correo no deseado. *Agregación de lista segura* es un conjunto de funcionalidades contra correo no deseado que se comparten entre Outlook y Exchange. Tal como su nombre sugiere, esta funcionalidad recopila datos de las listas seguras contra correo electrónico no deseado que configuran los usuarios de Outlook y los pone a disposición de los agentes contra correo electrónico no deseado en el servidor Exchange. El agente de filtro de contenido identifica como seguros los mensajes de correo electrónico que los usuarios de Outlook reciben de los contactos en que han confiado o que han agregado a las listas de destinatarios seguros o de remitentes seguros de Outlook. El agente de filtro de remitentes también realiza un filtrado de remitentes por destinatario mediante el uso de la lista de remitentes bloqueados que configuran los usuarios. Para obtener más información, consulte [Agregación de lista segura](safelist-aggregation-exchange-2013-help.md).

## Configuración del agente de filtro de contenido

El agente de filtro de contenido se configura con el Shell de administración de Exchange.


> [!IMPORTANT]
> Los cambios de configuración que hace en el agente de filtro de contenido en el Shell de administración de Exchange solo se realizan en el equipo local. Si tiene el agente de filtro de contenido en ejecución en varios servidores Exchange de su organización, debe hacer cambios en la configuración del filtro de contenido en todos los equipos.



El agente del filtro de contenido depende de las actualizaciones para determinar si un mensaje se puede enviar con la confianza de que no es un correo no deseado. Las actualizaciones contienen datos sobre sitios web de phishing, heurística de correo no deseado de Microsoft SmartScreen y otras actualizaciones de filtro inteligente de mensajes. Las actualizaciones de filtro de contenido suelen contener unos 6 MB de datos útiles durante períodos de tiempo más largos que otros datos de actualización contra correo no deseado.

Las actualizaciones de filtro de contenido están disponibles en [Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836). Cada dos semanas hay datos de actualización del filtro de contenido actualizados y listos para ser descargados.

Para obtener más información sobre cómo configurar el filtrado de contenido, consulte [Administrar el filtrado de contenido](manage-content-filtering-exchange-2013-help.md).

