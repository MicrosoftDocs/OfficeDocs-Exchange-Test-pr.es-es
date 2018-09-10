---
title: 'Novedades de las reglas de transporte: Exchange 2013 Help'
TOCTitle: Novedades de las reglas de transporte
ms:assetid: 0c2fc0b5-3cd2-4d79-aa2b-0c7622ae15a8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150483(v=EXCHG.150)
ms:contentKeyID: 48267615
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Novedades de las reglas de transporte

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-10-03_

En Microsoft Exchange Server 2013, se han realizado varias mejoras en las reglas de transporte. Este tema proporciona una introducción breve de alguno de los cambios y mejoras principales. Para obtener más información acerca de las reglas de transporte, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

## Compatibilidad con las directivas de prevención de pérdida de datos

Las características de prevención de pérdida de datos (DLP) de Exchange 2013 pueden ayudar a las organizaciones a reducir la divulgación inintencionada de información confidencial. Se han actualizado las reglas de transporte para admitir la creación de reglas que acompañan y aplican directivas de DLP. Para obtener más información acerca de la compatibilidad con DLP, consulte los siguientes temas:

[Integración de las reglas de información confidencial con las reglas de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[Prevención de pérdida de datos](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

## Acciones y predicados nuevos

La funcionalidad de las reglas de transporte se ha ampliado mediante la adición de acciones y predicados. Todos los predicados que se indican a continuación se pueden usar como condición o excepción al crear reglas de transporte.

Para obtener información detallada acerca del uso de estas acciones y predicados nuevos, consulte [Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) y [Acciones de regla de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md).

## Nuevos predicados

  -  **AttachmentExtensionMatchesWords**   Usado para detectar mensajes que contengan archivos adjuntos con extensiones concretas.

  -  **AttachmentHasExecutableContent**   Usado para detectar mensajes que contengan archivos adjuntos con contenido ejecutable.

  -  **HasSenderOverride** Usado para detectar mensajes donde el remitente ha elegido ignorar una restricción de directiva de DLP.

  -  **MessageContainsDataClassifications**   Usado para detectar información confidencial en el cuerpo del mensaje y en alguno de los archivos adjuntos. Para consultar una lista de las clasificaciones de datos disponibles, vea [Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

  -  **MessageSizeOver**   Usado para detectar mensajes cuyo tamaño general sea superior o igual al límite especificado.

  -  **SenderIPRanges**   Usado para detectar mensajes enviados desde un conjunto concreto de intervalos de direcciones IP.

## Nuevas acciones

  -  **GenerateIncidentReport**   Genera un informe de incidentes que se envía a una dirección SMTP especificada. La acción también tiene un parámetro llamado *IncidentReportOriginalMail* que acepta uno de dos valores: IncludeOriginalMail o DoNotIncludeOriginalMail.

  -  **NotifySender**   Controla el modo en que se notifica al remitente de un mensaje que infringe una directiva DLP. Puede elegir simplemente informar al remitente y enrutar el mensaje con normalidad o puede elegir rechazar el mensaje y notificar al remitente.

  -  **StopRuleProcessing**   Detiene el procesamiento de todas las reglas posteriores del mensaje.

  -  **ReportSeverityLevel**   Establece el nivel de gravedad especificada en el informe de incidentes. Los valores de la acción son: informativo, bajo, medio, alto y desactivado.

  -  **RouteMessageOutboundRequireTLS**   Requiere cifrado de Seguridad de la capa de transporte (TLS) cuando se enruta este mensaje fuera de su organización. Si no se admite el cifrado TLS, se rechaza el mensaje y no se entrega.

## Otros cambios en las reglas de transporte

  - **Soporte para sintaxis de expresión regular ampliada**   Las reglas de transporte en Exchange 2013 se basan en la función de expresión regular de .NET Framework (regex) y ahora admiten la sintaxis de expresión regular ampliada.

  - **Invocación del agente de reglas de transporte**   El cambio arquitectónico principal en Exchange 2013 para las reglas de transporte es que el agente de reglas de transporte se invoca en onResolvedMessage. En versiones anteriores de Exchange, el agente de reglas se invocaba en onRoutedMessage. Este cambio nos permitió añadir nuevas acciones, como la necesidad de TLS, que puede cambiar la forma en que el mensaje se enruta. Para obtener más información acerca de la arquitectura de reglas de transporte en Exchange 2013, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

  - **Información de regla de transporte detallada en registros de seguimiento de mensajes**   Ahora se incluye información detallada acerca de las reglas de transporte en registros de seguimientos de mensajes. La información incluye las reglas que se desencadenaron para un mensaje específico y las acciones tomadas como consecuencia del procesamiento de dichas reglas.

  - **Nueva función de supervisión de reglas**Exchange 2013 supervisa las reglas de transporte configuradas y mide el costo de ejecución de dichas reglas cuando crea la regla y durante el funcionamiento regular. Exchange puede detectar y generar alertas para las reglas que causan demoras en la entrega de correo.

