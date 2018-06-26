---
title: 'Filtrado de remitentes: Exchange 2013 Help'
TOCTitle: Filtrado de remitentes
ms:assetid: b833f864-ff10-46a0-a653-28fb9ba30896
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124354(v=EXCHG.150)
ms:contentKeyID: 49895861
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtrado de remitentes

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-12_

El filtrado de remitentes se basa en el encabezado MAIL FROM: El encabezado SMTP determina qué acción, si la hay, se debería realizar en un mensaje de correo electrónico de entrada. El Agente de filtrado de remitentes proporciona el filtrado del remitente.

El agente de filtro de remitentes actúa sobre los mensajes de remitentes específicos ajenos a la organización. Los administradores mantienen una lista de remitentes que se bloquean para que no envíen mensajes a la organización. Como administrador, puede bloquear a remitentes individuales (como kim@contoso.com), dominios enteros (contoso.com) o dominios y todos sus subdominios (\*.contoso.com). También se puede configurar qué acción realizará el agente de filtro de remitentes cuando se encuentra un mensaje de un remitente bloqueado. Se pueden configurar las siguientes acciones:

  - El agente de filtro de remitentes rechaza la solicitud de SMTP con un error de sesión SMTP `554 5.1.0 Sender Denied` y cierra la conexión.

  - El agente de filtro de remitentes acepta el mensaje y lo actualiza para indicar que proviene de un remitente bloqueado. Dado que el mensaje proviene de un remitente bloqueado y está marcado como tal, el agente de filtro de contenido usará esta información cuando calcule el nivel de confianza de correo no deseado (SCL).

Puede designar remitentes bloqueados y definir cómo debe actuar el agente de filtro de remitentes con los mensajes de los remitentes bloqueados. Para obtener más información acerca de cómo configurar el agente de filtro de remitentes, consulte [Administrar el filtrado de remitentes](manage-sender-filtering-exchange-2013-help.md) .


> [!IMPORTANT]
> Los encabezados MAIL FROM: SMTP se pueden suplantar. Por tanto, no debería basarse sólo en el agente de filtro de remitentes. Utilice el agente de filtro de remitentes y el agente de Id. de remitentes juntos. El agente Id. del remitente usa la dirección IP de origen del servidor de envío para verificar que el dominio en el MAIL FROM: El encabezado SMTP coincide con el dominio registrado. Para obtener más información acerca del agente de Id. de remitentes, consulte <A href="sender-id-exchange-2013-help.md">Id. del remitente</A> .



## Uso del agente de filtro de remitentes para bloquear mensajes

Cuando el agente de filtro de remitentes está habilitado en un servidor de Exchange, el filtrado de remitentes bloquea los mensajes entrantes que provienen de Internet pero que no están autenticados. Estos mensajes se consideran mensajes externos. Puede deshabilitar al agente de filtro de remitentes en las configuraciones de equipo individual. Para obtener más información, consulte [Administrar el filtrado de remitentes](manage-sender-filtering-exchange-2013-help.md).

Cuando habilita el agente de filtro de remitentes en un servidor de Exchange, éste filtra todos los mensajes que llegan a cualquiera de los conectores de recepción de ese equipo. Como ya se ha mencionado antes en este mismo tema, sólo se filtran los mensajes provenientes de orígenes externos. Los *Orígenes externos* se definen como orígenes no autenticados. Se consideran orígenes de Internet anónimos.

Es recomendable no filtrar los mensajes de correo electrónico de socios de confianza o de su propia organización. Cuando se ejecutan filtros contra correo no deseado, siempre existe la posibilidad de que los filtros identifiquen falsos positivos. Debería configurar los agentes contra correo no deseado para que se ejecuten únicamente en aquellos mensajes que tengan origen desconocido y potencialmente no sean de confianza. Esto reducirá la posibilidad de que los filtros contra correo deseado gestionen de forma incorrecta los mensajes legítimos. Se puede habilitar y deshabilitar el agente de filtro de remitentes para que se ejecute en mensajes de cualquier origen. Para obtener más información, consulte [Administrar el filtrado de remitentes](manage-sender-filtering-exchange-2013-help.md).

El agente de filtro de remitentes se puede configurar para que bloquee los mensajes entrantes que no especifiquen remitente y dominio en el encabezado MAIL FROM: Encabezado SMTP. Puede utilizar esta característica para evitar los ataques de informe de no entrega (NDR) en el servidor de Exchange. La mayor parte de los mensajes SMTP legítimos provienen de servidores SMTP que proporcionan un remitente y un dominio en MAIL FROM: SMTP.

## Especificar la acción de bloqueo

Tras especificar los remitentes y dominios bloqueados, deberá establecer cómo desea que actúe el agente de filtro de remitentes con los mensajes de los remitentes y dominios bloqueados. Se recomienda rechazar los mensajes. Cuando se utiliza el agente de filtro de remitentes para bloquear las direcciones de correo electrónico y dominios que vienen especificados por el administrador de Exchange, la posibilidad de falsos positivos es relativamente menor que cuando se utilizan otros agentes contra correo no deseado. Por ejemplo, el agente de filtro de contenido es un agente contra correo no deseado que se basa en muchas variables diferentes para determinar si un mensaje es correo no deseado.

Sólo hay dos situaciones en las que el agente de filtro de remitentes puede rechazar mensajes legítimos:

  - Si se escribe mal una dirección de correo electrónico o un nombre de dominio, se puede bloquear el remitente erróneo.

  - Si un nombre de dominio se vuelve a registrar en una empresa legítima después de que el dominio se agregue a la lista de remitentes bloqueados, se bloquearán involuntariamente mensajes legítimos.

En cualquiera de estos casos, sigue siendo recomendable rechazar los mensajes.

