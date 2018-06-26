---
title: 'Dominios aceptados: Exchange 2013 Help'
TOCTitle: Dominios aceptados
ms:assetid: c1839a5b-49f9-4c53-b247-f4e5d78efc45
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124423(v=EXCHG.150)
ms:contentKeyID: 49895890
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dominios aceptados

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-06-16_

Un dominio aceptado es cualquier espacio de nombres SMTP para el que la organización de Microsoft Exchange Server 2013 envía o recibe mensajes de correo electrónico. Los dominios aceptados incluyen aquellos dominios para los cuales está autorizada la organización de Exchange. Una organización de Exchange está autorizada cuando administra la entrega de correo de los destinatarios en el dominio aceptado. Los dominios aceptados también incluyen dominios para los que la organización de Exchange recibe correo y, a continuación, lo retransmite a un servidor de correo electrónico que se encuentra fuera de la organización para que lo envíe al destinatario.

**Contenido**

Configuring accepted domains

Authoritative domains

Relay domains

Internal relay domain

External relay domain

Accepted domains and email address policies

## Configuración de dominios aceptados

Los dominios aceptados están configurados como configuración global de la organización de Exchange. Es preciso configurar cada uno de los dominios para los que la organización de Exchange retransmite o envía mensajes como un dominio aceptado en su organización.

Hay tres tipos de dominios aceptados: autorizado, de retransmisión de Internet y de retransmisión de borde. Estos tipos de dominios aceptados se describen en las siguientes secciones.


> [!NOTE]
> Si tiene un servidor Transporte perimetral con suscripción en la red perimetral, puede configurar dominios aceptados en un servidor de buzones de la organización de Exchange. La configuración de los dominios aceptados se replica al servidor Transporte perimetral durante la sincronización de EdgeSync. Para obtener más información, consulte <A href="edge-subscriptions-exchange-2013-help.md">Suscripciones perimetrales</A>.



## Dominios autorizados

Una organización puede tener más de un dominio SMTP. El conjunto de dominios de correo electrónico para una organización incluye dominios autorizados. En Exchange 2013, un dominio aceptado se considera autorizado si la organización de Exchange hospeda buzones para los destinatarios de este dominio SMTP.

De forma predeterminada, al instalar el primer servidor Buzón de correo Exchange 2013, se configura un dominio aceptado como autorizado para la organización de Exchange. El dominio aceptado predeterminado es el nombre de dominio completo (FQDN) del dominio raíz del bosque. Con frecuencia, el nombre del dominio interno es distinto del nombre de dominio externo. Por ejemplo, el nombre de dominio interno puede ser contoso.local, aunque el nombre de dominio externo sea contoso.com. El registro de agente de intercambio de correo (MX) de DNS para la organización hace referencia a contoso.com, que es el espacio de nombres SMTP que se asigna a los usuarios al crear una directiva de direcciones de correo electrónico. Debe crear un dominio aceptado que coincida con el nombre de dominio externo.

Para más información, consulte:

  - [Configurar un dominio aceptado dentro de su organización de Exchange como autoritativo](configure-an-accepted-domain-within-your-exchange-organization-as-authoritative-exchange-2013-help.md)

  - [Configurar Exchange para aceptar correo de varios dominios autoritativos](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)

## Dominios de retransmisión

Por lo general, la mayoría de los servidores de mensajería conectados a Internet están configurados para no aceptar otros dominios que retransmiten a través de ellos. No obstante, existen situaciones donde es posible que desee permitir a los asociados o filiales retransmitir mensajes a través de sus servidores Exchange. En Exchange 2013, puede configurar dominios aceptados como dominios de retransmisión. La organización recibe los mensajes de correo electrónico y, a continuación, los retransmite a otro servidor de correo electrónico.

Puede configurar un dominio de retransmisión como un dominio de retransmisión de Internet o como un dominio de retransmisión de borde. Estos dos tipos de dominios de retransmisión se describen en las siguientes secciones.

## Dominio de retransmisión interna

Al configurar un dominio de retransmisión interna, algunos o todos los destinatarios de este dominio no tienen buzones de correo en esta organización de Exchange. El correo que proviene de Internet se retransmite para este dominio a través de servidores de transporte en esta organización de Exchange. Esta configuración se utiliza en los escenarios que se describen en esta sección.

Es posible que una organización tenga que compartir el mismo espacio de direcciones SMTP entre dos o más sistemas de correo electrónico diferente. Puede, por ejemplo, que tenga que compartir el espacio de direcciones SMTP entre Exchange y un sistema de mensajería de terceros o entre entornos de Exchange que están configurados en diferentes bosques de Active Directory. En estos escenarios, los usuarios de cada sistema de correo electrónico tienen el mismo sufijo de dominio como parte de sus direcciones de correo electrónico.

Para admitir estos escenarios deberá crear un dominio aceptado que esté configurado como un dominio de retransmisión interna. También deberá agregar un conector de envío con origen en un servidor Buzón de correo y configurado para enviar correo electrónico al espacio de direcciones compartido. Si un dominio aceptado está configurado como autoritativo y no se encuentra un destinatario en Active Directory, se devuelve un informe de no entrega (NDR) al remitente. El dominio aceptado que está configurado como un dominio de retransmisión interna primero intenta realizar la entrega a un destinatario de la organización de Exchange. Si no se encuentra el destinatario, el mensaje se enruta al conector de envío que tenga el espacio de direcciones más cercano.

Si la organización contiene más de un bosque y ha configurado la sincronización de la lista global de direcciones (GAL), el dominio SMTP para un bosque se puede configurar como un dominio de retransmisión interna en un segundo bosque. Los mensajes que provienen de Internet que están destinados a destinatarios en los dominios de retransmisión interna se retransmiten a los servidores de buzones en la misma organización. Después, los servidores Buzón de correo enrutan los mensajes a los servidores Buzón de correo en el bosque destinatario. El dominio SMTP se configura como un dominio de retransmisión interna para asegurarse de que el correo electrónico que va dirigido a dicho dominio es aceptado por la organización de Exchange. La configuración del conector de la organización determina cómo se enrutan los mensajes.

Para más información, consulte [Configurar un dominio aceptado para una unidad de negocio con buzones de correo fuera de la organización de Exchange](configure-an-accepted-domain-for-a-business-unit-with-mailboxes-outside-your-exchange-organization-exchange-2013-help.md).

## Dominio de retransmisión externa

Al configurar un dominio de retransmisión externa, los mensajes se retransmiten a un servidor de correo electrónico que se encuentra fuera de la organización de Exchange y fuera del perímetro de la red de la organización.

Para más información, consulte [Configure un dominio aceptado para una unidad de negocio independiente](configure-an-accepted-domain-for-an-independent-business-unit-exchange-2013-help.md).

## Dominios aceptados y directivas de la dirección de correo electrónico

Debe configurar un dominio aceptado para poder usar el espacio de direcciones SMTP en una directiva de direcciones de correo. Al crear un dominio aceptado, puede usar un carácter comodín (\*) en el espacio de direcciones para indicar que la organización de Exchange también acepta todos los subdominios del espacio de direcciones SMTP. Por ejemplo, para configurar contoso.com y todos sus subdominios como dominios aceptados, escriba **\*.contoso.com** como espacio de direcciones SMTP. Las entradas de dominios aceptados están disponibles automáticamente para su uso en una directiva de direcciones de correo.

Si elimina un dominio aceptado que se usa en una directiva de direcciones de correo electrónico, dicha directiva deja de ser válida y los destinatarios con direcciones de correo electrónico en el dominio SMTP no pueden enviar ni recibir correo electrónico.

