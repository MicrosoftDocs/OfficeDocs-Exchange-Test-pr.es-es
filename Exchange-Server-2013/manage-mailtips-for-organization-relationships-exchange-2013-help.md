---
title: 'Administrar sugerencias de correo electrónico para las relaciones de la organización: Exchange 2013 Help'
TOCTitle: Administrar sugerencias de correo electrónico para las relaciones de la organización
ms:assetid: 6e6b48ef-c41c-47ad-8063-66901765c2a5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ649324(v=EXCHG.150)
ms:contentKeyID: 49895699
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar sugerencias de correo electrónico para las relaciones de la organización

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

El Shell de administración de Exchange permite configurar valores personalizados para Sugerencias de correo electrónico entre varias organizaciones.

Al establecer una relación organizativa, puede mejorar la experiencia de usuario de ambas organizaciones al compartir datos de disponibilidad, configurar un flujo de mensajes seguros y habilitar el seguimiento de mensajes. Para obtener más información acerca de relaciones organizativas, consulte [Sugerencias de correo electrónico sobre las relaciones de la organización](mailtips-over-organization-relationships-exchange-2013-help.md).

Puede utilizar diversas configuraciones para controlar cómo se utilizará la información sobre correo entre dos organizaciones que han establecido una relación organizativa. Los procedimientos descritos en esta sección ilustran estos diversos controles. En todos los ejemplos, la organización local es contoso.com, la organización remota es online.contoso.com y la relación organizativa se denomina Contoso Online.

Para configurar estas opciones, se usa el cmdlet **Set-OrganizationRelationship**.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Información sobre correo" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Use el Shell para habilitar o deshabilitar la información sobre correo entre dos organizaciones

En este ejemplo, se configura la relación organizativa de modo que la información sobre correo se devuelva a los remitentes de la organización remota al componer mensajes a destinatarios de su organización.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $true

En este ejemplo, se configura la relación organizativa a fin de evitar que la información sobre correo se devuelva a los remitentes de la organización remota al componer mensajes a destinatarios de su organización.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $false

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OrganizationRelationship](https://technet.microsoft.com/es-es/library/ee332326\(v=exchg.150\)).

## Utilice el Shell para configurar la información sobre correo que es devuelta a la organización remota

Para cada relación organizativa, puede determinar qué conjunto de información sobre correo se devuelve a los remitentes de la otra organización. En este ejemplo, se configura la relación organizativa de modo que se devuelva toda la información sobre correo.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel All

En este ejemplo, se configura la relación organizativa de modo que solo se devuelvan las respuestas automáticas, los mensajes sobredimensionados, los destinatarios restringidos y la información sobre correo del buzón de correo lleno.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel Limited

En este ejemplo, se configura la relación organizativa de modo que no se devuelva información sobre correo.


> [!NOTE]
> No utilice este método para deshabilitar la información sobre correo de esta relación. Para deshabilitar la información sobre correo, establezca el parámetro <EM>MailTipsAccessEnabled</EM> en <CODE>$false</CODE>.



    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel None

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OrganizationRelationship](https://technet.microsoft.com/es-es/library/ee332326\(v=exchg.150\)).

## Utilice el Shell para configurar un grupo específico de usuarios a quien se devuelve la información sobre correo específica de los destinatarios

Puede restringir la devolución de información sobre correo específica de los destinatarios para un grupo específico de usuarios. De manera predeterminada, cuando habilite la información sobre correo para una relación organizativa, se devolverá la siguiente información sobre correo específica de los destinatarios para todos los usuarios:

  - Respuestas automáticas

  - Buzón de correo lleno

  - información sobre correo personalizada

Puede especificar un grupo de acceso de información sobre correo en la relación organizativa. Después de especificar un grupo, la información sobre correo se devuelve solo para los buzones de correo, contactos de correo y usuarios de correo que son miembros de ese grupo. Este ejemplo configura la relación organizativa para devolver la información sobre correo específica del destinatario solo a los miembros del grupo ShareMailTips@contoso.com.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessScope ShareMailTips@contoso.com

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OrganizationRelationship](https://technet.microsoft.com/es-es/library/ee332326\(v=exchg.150\)).

