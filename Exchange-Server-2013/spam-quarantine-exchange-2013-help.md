---
title: 'Cuarentena de correo electrónico no deseado: Exchange 2013 Help'
TOCTitle: Cuarentena de correo electrónico no deseado
ms:assetid: 4535496f-de6a-43df-8e53-c9a97f65cccc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997692(v=EXCHG.150)
ms:contentKeyID: 49895601
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cuarentena de correo electrónico no deseado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-12_

Muchas organizaciones están obligadas por leyes o normativas a conservar o hacer entrega de todos los mensajes de correo electrónico legítimos. En Microsoft Exchange Server 2013, la cuarentena de correo no deseado es una característica del agente de filtro de contenido que reduce el riesgo de perder mensajes legítimos. La cuarentena de correo no deseado proporciona una ubicación de almacenamiento temporal para aquellos mensajes identificados como correo no deseado que no deben ser entregados a un buzón de usuario dentro de la organización.

Los mensajes identificados por el agente de filtro de contenido como correo no deseado se envuelven en un informe de no entrega (NDR) y se entregan a un buzón de cuarentena de correo no deseado dentro de la organización. Puede administrar los mensajes entregados al buzón de cuarentena de correo no deseado y tomar las medidas pertinentes. Por ejemplo, puede eliminar mensajes o dejar que los mensajes marcados como falsos positivos en el filtrado contra correo no deseado se enruten hacia los destinatarios a los que iban dirigidos. Además, puede configurar el buzón de cuarentena de correo no deseado de forma que los mensajes se eliminen automáticamente después de un periodo determinado de tiempo.

**Contenido**

Spam confidence level

Spam quarantine

## Nivel de confianza de correo no deseado

Cuando un usuario externo envía mensajes de correo electrónico a un servidor de Exchange en el que se ejecutan las características contra correo no deseado, éstas evalúan las características de los mensajes de manera acumulativa y actúan como sigue:

  - Se filtran los mensajes sospechosos de ser correo no deseado.

  - Se asigna una puntuación a los mensajes en base a la probabilidad de que sean correo no deseado. Esta clasificación se almacena con el propio mensaje como una propiedad del mensaje llamada clasificación de nivel de confianza de correo no deseado (SCL).

La cuarentena de correo no deseado utiliza la clasificación de SCL para determinar si el correo tiene una probabilidad alta de ser correo no deseado. La clasificación de SCL es un valor numérico entre 0 y 9; el 0 significa que es poco probable que sea correo no deseado y el 9, que es altamente probable que lo sea.

Puede configurar el correo con una clasificación de SCL determinada para que se elimine, se rechace o se ponga en cuarentena. La clasificación que inicia cualquiera de estas acciones es lo que se conoce como el *umbral de cuarentena de SCL*. Con el filtrado de contenido se puede configurar el agente de filtro de contenido de modo que actúe en función del umbral de cuarentena de SCL. Por ejemplo, puede establecer las siguientes condiciones:

  - El umbral de SCL para eliminar se ha definido en 8.

  - El umbral de SCL para rechazar se ha definido en 7.

  - El umbral de SCL para poner en cuarentena se ha definido en 6.

  - El umbral de SCL de la carpeta Correo no deseado se ha definido en 5.

Basándose en los anteriores umbrales de SCL, todo el correo electrónico con un SCL de 6 se entregará en el buzón de cuarentena de correo no deseado.

Para obtener más información, consulte [Administrar el filtrado de contenido](manage-content-filtering-exchange-2013-help.md).

Volver al principio

## Cuarentena de correo electrónico no deseado

Cuando el servidor Exchange que ejecuta todos los agentes contra correo electrónico no deseado predeterminados recibe mensajes, el filtro de contenido se aplica como se indica a continuación:

  - Si la clasificación de SCL es mayor o igual que el umbral de SCL de cuarentena, pero menor que el umbral de SCL para eliminar o rechazar, el mensaje irá a parar al buzón de cuarentena de correo no deseado.

  - Si la clasificación de SCL es menor que el umbral de cuarentena de correo no deseado, el mensaje se entregará en la Bandeja de entrada del destinatario.

El administrador de mensajes utiliza Microsoft Outlook para supervisar el buzón de cuarentena de correo no deseado y detectar los posibles falsos positivos. Si se detecta un falso positivo, el administrador puede enviar el mensaje al buzón del destinatario.

El administrador de mensajes puede revistar los sellos contra correo no deseado si se cumple cualquiera de estas condiciones:

  - Se han filtrado demasiados falsos positivos al buzón de cuarentena de correo no deseado.

  - No se está rechazando o eliminando suficiente correo no deseado.

Para obtener más información, consulte [Marcas de correo no deseado](anti-spam-stamps-exchange-2013-help.md).

También puede ajustar las clasificaciones de SCL para filtrar con mayor precisión el correo no deseado que llega a la organización. Para obtener más información, consulte [Umbral de nivel de confianza de correo no deseado](spam-confidence-level-threshold-exchange-2013-help.md).

Para utilizar la cuarentena contra correo no deseado, es necesario seguir estos pasos:

1.  Comprobar que el filtrado de contenido está habilitado.

2.  Crear un buzón de correo dedicado para la cuarentena de correo electrónico no deseado.

3.  Especificar el buzón de cuarentena de correo no deseado.

4.  Configurar el umbral de cuarentena del nivel de confianza contra correo no deseado.

5.  Administrar el buzón de cuarentena de correo no deseado.

6.  Ajustar el umbral de cuarentena del nivel de confianza contra correo no deseado si es necesario.

Para obtener instrucciones detalladas, consulte [Configurar un buzón de cuarentena de correo no deseado](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

Volver al principio

