---
title: 'Filtrado de destinatarios en servidores de transporte perimetral: Exchange 2013 Help'
TOCTitle: Filtrado de destinatarios en servidores de transporte perimetral
ms:assetid: 994eefd9-3903-41e6-a882-1e333d6d2d18
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123891(v=EXCHG.150)
ms:contentKeyID: 49895798
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtrado de destinatarios en servidores de transporte perimetral

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-05-07_

El filtrado de destinatarios es una característica de Microsoft Exchange Server 2013 contra el correo no deseado que usa el encabezado RCPT TO SMTP para determinar qué acción, en caso de que sea necesario, se realizará en un mensaje de correo electrónico entrante. El filtrado de destinatarios lo realiza el agente de filtrado de destinatarios.

El agente de filtro de destinatarios bloquea los mensajes en función de las características del destinatario de la organización. El agente de filtro de destinatarios puede ayudarle a impedir la aceptación de mensajes en los siguientes escenarios:

  - **Destinatarios no existentes**   Puede impedir la entrega a destinatarios que no estén en la libreta de direcciones de la organización. Por ejemplo, puede detener la entrega a nombres de cuentas que normalmente no se usan correctamente, como administrador@contoso.com o soporte@contoso.com.

  - **Listas de distribución restringidas**   Puede impedir la entrega de correo de Internet a listas de distribución que solo deben usar los usuarios internos.

  - **Buzones de correo que no deben recibir mensajes de Internet**   Puede impedir la entrega de correo de Internet a un buzón o alias específico que se suela usar dentro de la organización, como el departamento de soporte técnico.

El agente de filtro de destinatarios actúa en los destinatarios almacenados en una o las dos fuentes de datos siguientes:

  - **Lista de destinatarios bloqueados**   Una lista definida por un administrador de los destinatarios que no deben recibir nunca mensajes de Internet.

  - **Búsqueda de destinatarios**   Consultas en Active Directory para comprobar si el destinatario existe en la organización. En un servidor de transporte perimetral, la Búsqueda de destinatarios requiere el acceso a información de Active Directory proporcionada por EdgeSync a la instancia local de Active Directory Lightweight Directory Services (AD LDS).

Si se habilita el agente de filtro de destinatarios, se realiza una de las acciones siguientes en los mensajes entrantes según las características de los destinatarios. Dichos destinatarios los indica el encabezado RCPT TO.

  - Si el mensaje entrante contiene un destinatario que está en la lista de destinatarios bloqueados, el servidor Exchange envía un error de sesión SMTP `550 5.1.1 User unknown` al servidor remitente.

  - Si el mensaje entrante contiene un destinatario que no coincide con ninguno de los de la búsqueda de destinatarios, el servidor Exchange envía un error de sesión SMTP `550 5.1.1 User unknown` al servidor remitente.

  - Si el destinatario no está en la lista de destinatarios bloqueados, pero sí aparece en la búsqueda de destinatarios, el servidor Exchange envía una respuesta SMTP `250 2.1.5 Recipient OK` al servidor remitente y el siguiente agente contra correo electrónico no deseado de la cadena procesa el mensaje.

**Contenido**

Configuring recipient lookup

Tarpitting functionality

Multiple namespaces

## Configuración de búsqueda de destinatarios

Una de las maneras más eficaces de reducir el correo electrónico no deseado es validar a los destinatarios antes de aceptar mensajes entrantes de Internet. Para habilitar el bloqueo de mensajes enviados a destinatarios que no existen en la organización Exchange y el bloqueo de destinatarios específicos se usa el cmdlet **Set-RecipientFilterConfig** en el Shell de administración de Exchange. Para más información, vea [Administrar el filtrado de destinatarios en servidores de transporte perimetral](manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).

Si ha instalado el servidor de transporte perimetral en su red perimetral, es conveniente configurar la instancia AD LDS que se ejecuta en el servidor de transporte perimetral para que sincronice con Active Directory. De manera predeterminada, AD LDS está instalado y configurado en el servidor de transporte perimetral. Sin embargo, debe configurar AD LDS para comunicarse con un servidor de catálogo global Active Directory unido a un dominio mediante la suscripción del servidor de transporte perimetral en su organización. Para más información, vea [Usar un servidor de transporte perimetral de Exchange 2010 o 2007 en Exchange 2013](use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md).

Volver al principio

## Funcionalidad del retraso del tráfico de red (tarpitting)

La funcionalidad de búsqueda de destinatarios permite al servidor remitente determinar si las direcciones de correo electrónico son válidas o no. Como se ha mencionado anteriormente, cuando el destinatario de un mensaje entrante es un destinatario conocido, el servidor Exchange devuelve una respuesta SMTP `250 2.1.5 Recipient OK` al servidor remitente. Esta funcionalidad proporciona un entorno ideal para los ataques de robo de directorio (DHA).

Un *ataque por recolección de directorios* es un intento de recopilar direcciones de correo electrónico válidas de una organización concreta y agregarlas a una base de datos de correo electrónico no deseado. Dado que la finalidad de todo el correo electrónico no deseado es que la gente abra mensajes de correo electrónico, las direcciones que se saben que están activas suponen una ventaja por la que los usuarios malintencionados, o *spammers*, pagan. Como el protocolo SMTP proporciona información acerca de los remitentes conocidos y desconocidos, los spammers pueden escribir un programa automático que use nombres comunes o términos del diccionario para crear direcciones de correo electrónico en un dominio concreto. El programa recopila todas las direcciones de correo electrónico que devuelven una respuesta SMTP `250 2.1.5 Recipient OK` y descarta aquellas direcciones que devuelven un error de sesión SMTP `550 5.1.1 User unknown`. A continuación, el spammer puede vender las direcciones de correo electrónico válidas o usarlas como destinatarios para mensajes no solicitados.

Para combatir los ataques por recolección de directorios, Exchange 2013 incluye la funcionalidad de retraso del tráfico de red. El *retraso del tráfico de red* es la práctica de retrasar artificialmente las respuestas del servidor para ciertos patrones de comunicación de SMTP que indican volúmenes elevados de correo electrónico no deseado u otros mensajes no deseados. El propósito del retraso del tráfico de red (tarpitting) es ralentizar el proceso de comunicación del tráfico de correo electrónico, con el fin de que el coste del envío de correo electrónico no deseado aumente para la persona u organización que envía dicho correo. El retraso del tráfico de red hace que los ataques de robo de directorio sean demasiado costosos como para automatizarlos eficazmente.

Si el retraso del tráfico de red no está configurado, el servidor Exchange devuelve inmediatamente un error de sesión SMTP `550 5.1.1 User unknown` al remitente cuando un destinatario no se encuentre en la búsqueda de destinatarios. De manera alternativa, si el retraso del tráfico de red está configurado, SMTP espera un número de segundos determinado antes de devolver el error `550 5.1.1 User unknown`. Esta pausa en la sesión SMTP dificulta aún más el ataque de robo de directorio y hace que sea menos rentable al emisor de correo electrónico no deseado. De forma predeterminada, el retraso del tráfico de red no deseado está configurado para 5 segundos en conectores de recepción.

Para configurar el retraso antes de que SMTP devuelva el error `550 5.1.1 User unknown`, deberá configurar el intervalo de retraso del tráfico de red con el parámetro *TarpitInterval* en el cmdlet **Set-ReceiveConnector**. La sintaxis es:

    Set-ReceiveConnector <Receive Connector> -TarpitInterval <00:00:00 to 00:10:00>

El valor predeterminado es `00:00:05` o 5 segundos. El nombre del conector de recepción predeterminado en un servidor de transporte perimetral es `Default internal receive connector <server name>`.

Proceda con cuidado si decide cambiar este valor. Un intervalo demasiado largo podría interrumpir el flujo de correo ordinario, mientras que uno demasiado corto podría no ser tan eficaz a la hora de frustrar un ataque por recolección de directorios. Si cambia el intervalo de retraso del tráfico de red, hágalo en incrementos pequeños y compruebe los resultados. Por ejemplo, si 5 segundos no resulta eficiente, pruebe cambiar el intervalo a 10 segundos.

Volver al principio

## Varios espacios de nombres

El agente de filtrado de destinatarios realiza búsquedas de destinatarios solo para dominios con autoridad. Si su organización acepta y renvía mensajes en nombre de otro dominio que está configurado como dominio de retransmisión interna o de retransmisión externa, el agente de filtrado de destinatarios no realiza una búsqueda de destinatarios en dichos dominios. No obstante, si el destinatario aparece en la lista de destinatarios bloqueados, el agente de filtrado de destinatarios lo bloqueará.

Tenga en cuenta que también puede configurar dominios aceptados localmente en un servidor de transporte perimetral. Si el dominio está configurado como dominio de retransmisión interna o retransmisión externa, el agente de filtrado de destinatarios del servidor de transporte perimetral no realiza una búsqueda de destinatarios en dichos dominios.

Volver al principio

