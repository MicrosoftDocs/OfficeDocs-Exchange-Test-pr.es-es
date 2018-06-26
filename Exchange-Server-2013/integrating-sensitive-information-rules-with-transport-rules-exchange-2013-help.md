---
title: 'Integración de las reglas de información confidencial con las reglas de transporte: Exchange 2013 Help'
TOCTitle: Integración de las reglas de información confidencial con las reglas de transporte
ms:assetid: feb014a7-89dd-4f2d-a06d-52806ce435d4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150583(v=EXCHG.150)
ms:contentKeyID: 48267739
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Integración de las reglas de información confidencial con las reglas de transporte

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2015-01-14_

En Microsoft Exchange, puede crear directivas de DLP que contengan reglas no solo para clasificaciones tradicionales de mensajes y reglas de transporte existentes sino también combinarlas con reglas para información confidencial encontrada en los mensajes. El marco de reglas de transporte existente ofrece completas funcionalidades para definir directivas de mensajería, que abarcan toda la variedad de controles parciales o completos. Algunos ejemplos son:

  - Limitar la interacción entre los remitentes y los destinatarios, incluidas las interacciones entre los grupos departamentales de una organización.

  - Aplicar directivas independientes para las comunicaciones dentro y fuera de una organización.

  - Evitar que contenido inapropiado entre y salga de la organización.

  - Filtrar información confidencial.

  - Efectuar el seguimiento de los mensajes que envían o reciben ciertas personas, o archivarlos.

  - Redireccionar los mensajes entrantes y salientes para inspeccionarlos antes de entregarlos.

  - Aplicar avisos de declinación de responsabilidades a los mensajes conforme pasan por la organización.

Las reglas de transporte permiten aplicar directivas de mensajería a los mensajes de correo electrónico que fluyen por la canalización de transporte del servicio Transporte en servidores de buzones y de transporte perimetral. Estas reglas permiten a los administradores de sistemas aplicar directivas de mensajería, preservar la seguridad de los mensajes, proteger los sistemas de seguridad y evitar pérdidas accidentales de información. Para obtener más información acerca de las reglas de transporte, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013) o [Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)) (Exchange Online).

## Reglas de información confidencial en el marco de la regla de transporte

Las reglas de información confidencial se integran con el marco de reglas de transporte mediante la introducción de una condición que se puede personalizar: **Si el mensaje contiene...Información confidencial**. Esta condición se puede configurar con uno o más tipos de información confidencial que contienen los mensajes. Cuando varias directivas o reglas de DLP en una directiva están configuradas con esta condición, la directiva o regla se cumple cuando coincide alguna de las condiciones. Las reglas de directivas de Exchange examinan el asunto, el cuerpo y los archivos adjuntos de un mensaje. Si la regla coincide con alguno de estos componentes del mensaje, se aplicarán las acciones de la regla.

La condición de información confidencial se puede combinar con las reglas de transporte existentes para definir las directivas de mensajería. Al combinarse, la condición actúa junto con otras reglas y proporciona la semántica AND. Por ejemplo, dos condiciones diferentes se agregan junto con una instrucción AND, de manera que ambas deban coincidir para que la acción se aplique. Todas las acciones de reglas de transporte se pueden configurar como resultado de las reglas coinciden con el tipo de información confidencial. El agente de reglas de transporte, que analiza los mensajes para aplicar las reglas de transporte, puede analizar muchos tipos diferentes de archivos. Para obtener más información acerca de los tipos de archivos admitidos, consulte [Usar reglas de transporte para inspeccionar datos adjuntos de mensajes](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013) o [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/es-es/library/jj919236\(v=exchg.150\)) (Exchange Online).

Las reglas también se pueden usar en la parte de excepción de una definición de regla. El uso en la definición de la excepción es independiente del uso como condición en la regla. Esto proporciona la flexibilidad de definir reglas que tengan la condición que especifica varios tipos de información que se aplicarán como parte de la condición y también tipos diferentes de información en la condición. Esto permitirá directivas como la coincidencia con reglas específicas tradicionales de clasificación de mensajes, pero no la coincidencia con otros tipos de información confidencial antes de realizar acciones que se definen en una directiva.

## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange Server 2013

[Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\))Exchange Online

[Crear una nueva directiva de DLP personalizada](create-a-custom-dlp-policy-exchange-2013-help.md)

