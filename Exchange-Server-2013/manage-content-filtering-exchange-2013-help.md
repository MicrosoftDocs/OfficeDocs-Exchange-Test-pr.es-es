---
title: 'Administrar el filtrado de contenido: Exchange 2013 Help'
TOCTitle: Administrar el filtrado de contenido
ms:assetid: 05bd9d39-81dc-4514-8b75-7be386d5bcad
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa995953(v=EXCHG.150)
ms:contentKeyID: 49895447
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar el filtrado de contenido

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

El agente de filtrado de contenido proporciona el filtrado de contenido. El agente de filtrado de contenido filtra todos los mensajes que llegan a los conectores de recepción en el servidor Exchange. Tan solo se filtran los mensajes procedentes de orígenes sin autenticación.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada «Característica contra el correo no deseado» en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - De manera predeterminada, las características contra correo no deseado no están habilitadas en el Servicio de transporte en un servidor de buzones. Por lo general, solo se habilitan las características contra correo no deseado si la organización de Exchange no realiza un filtrado previo contra correo no deseado antes de aceptar mensajes entrantes. Para obtener más información, consulte [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para habilitar o deshabilitar el filtrado de contenido

Para deshabilitar el filtro de contenido, ejecute el comando siguiente:

    Set-ContentFilterConfig -Enabled $false

Para habilitar el filtrado de contenido, ejecute el siguiente comando:

    Set-ContentFilterConfig -Enabled $true


> [!NOTE]
> Al deshabilitar el filtrado de contenido, el agente de filtrado de contenido subyacente todavía está habilitado. Para deshabilitar el agente de filtrado de contenido, ejecute el comando: <CODE>Disable-TransportAgent "Content Filter Agent"</CODE>.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya habilitado o deshabilitado el filtrado de contenido, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-ContentFilterConfig | Format-List Enabled

2.  Compruebe el valor de la propiedad *Enabled* que se muestra.

## Use el Shell para habilitar o deshabilitar el filtrado de contenido de mensajes externos

De forma predeterminada, la función de filtro de contenido está habilitada para los mensajes externos.

Para deshabilitar el filtrado de contenido para mensajes externos, ejecute el comando siguiente:

    Set-ContentFilterConfig -ExternalMailEnabled $false

Para habilitar el filtro de contenido para mensajes externos, ejecute el comando siguiente:

    Set-ContentFilterConfig -ExternalMailEnabled $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya habilitado o deshabilitado el filtrado de contenido de los mensajes externos, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-ContentFilterConfig | Format-List ExternalMailEnabled

2.  Compruebe el valor de la propiedad *ExternalMailEnabled* que se muestra.

## Use el Shell para habilitar o deshabilitar el filtrado de contenido de mensajes internos

Es recomendable no filtrar los mensajes de socios de confianza o de su propia organización. Cuando se ejecutan filtros contra correo electrónico no deseado, siempre existe la posibilidad de que los filtros identifiquen falsos positivos. Para reducir la posibilidad de que los filtros traten de forma errónea mensajes legítimos de correo electrónico, los agentes contra correo electrónico no deseado sólo se deben ejecutar con mensajes provenientes de orígenes que no sean de confianza o sean desconocidos.

Para habilitar el filtrado de contenido para mensajes internos, ejecute el comando siguiente:

    Set-ContentFilterConfig -InternalMailEnabled $true

Para deshabilitar el filtrado de contenido para mensajes internos, ejecute el comando siguiente:

    Set-ContentFilterConfig -InternalMailEnabled $false

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya habilitado o deshabilitado el filtrado de contenido de los mensajes internos, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-ContentFilterConfig | Format-List InternalMailEnabled

2.  Compruebe el valor de la propiedad *InternalMailEnabled* que se muestra.

## Uso del Shell para configurar las excepciones de destinatarios y remitentes

Para reemplazar los valores existentes, ejecute el siguiente comando:

    Set-ContentFilterConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenders <sender1,sender2...> -BypassedSenderDomains <domain1,domain2...>

Este ejemplo configura las siguientes excepciones en filtrado de contenido:

  - El filtrado de contenido no comprueba los destinatarios laura@contoso.com y julia@contoso.com.

  - El filtrado de contenido no comprueba los destinatarios steve@fabrikam.com y cindy@fabrikam.com.

  - El filtrado de contenido no comprueba todos los remitentes en el dominio nwtraders.com y todos los subdominios.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients laura@contoso.com,julia@contoso.com -BypassedSenders steve@fabrikam.com,cindy@fabrikam.com -BypassedSenderDomains *.nwtraders.com

Para agregar o quitar entradas sin modificar valores existentes, ejecute el siguiente comando:

    Set-ContentFilterConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Este ejemplo configura las siguientes excepciones en el filtrado de contenido:

  - Agregue tiffany@contoso.com y chris@contoso.com a la lista de los destinatarios existentes que el filtrado de contenido no ha comprobado.

  - Agregue joe@fabrikam.com y michelle@fabrikam.com a la lista de remitentes existentes que el filtrado de contenido no ha comprobado.

  - Agregue blueyonderairlines.com a la lista de dominios existentes cuyos remitentes no son comprobados por el filtrado de contenido.

  - Elimine el dominio woodgrovebank.com y todos los subdominios de la lista de dominios existentes cuyos remitentes no son comprobados por el filtrado de contenido.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients @{Add="tiffany@contoso.com","chris@contoso.com"} -BypassedSenders @{Add="joe@fabrikam.com","michelle@fabrikam.com"} -BypassedSenderDomains @{Add="blueyonderairlines.com"; Remove="*.woodgrovebank.com"}

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha configurado las excepciones de remitente o destinatario, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-ContentFilterConfig | Format-List Bypassed*

2.  Compruebe que los valores mostrados coinciden con los ajustes que especificó.

## Uso del Shell para configurar las frases o palabras permitidas y bloqueadas

Para agregar frases y palabras permitidas y bloqueadas, ejecute el siguiente comando:

    Add-ContentFilterPhrase -Influence GoodWord -Phrase <Phrase> -Influence BadWord -Phrase <Phrase>

Este ejemplo permite todos los mensajes que contengan la frase "comentarios del cliente".

    Add-ContentFilterPhrase -Influence GoodWord -Phrase "customer feedback"

Este ejemplo bloquea todos los mensajes que contengan la frase "consejos sobre negocios".

    Add-ContentFilterPhrase -Influence BadWord -Phrase "stock tip"

Para eliminar frases permitidas o bloqueadas, ejecute el siguiente comando:

    Remove-ContentFilterPhrase -Phrase <Phrase>

Este ejemplo elimina la frase "consejos sobre negocios":

    Remove-ContentFilterPhrase -Phrase "stock tip"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha configurado correctamente las frases permitidas y las bloqueadas, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-ContentFilterPhrase | Format-List Influence,Phrase

2.  Compruebe que los valores mostrados coinciden con los ajustes que especificó.

## Uso del Shell para configurar los umbrales de SCL

Para configurar los umbrales y las acciones del nivel de confianza contra correo no deseado (SCL), ejecute el siguiente comando:

    Set-ContentFilterConfig -SCLDeleteEnabled <$true | $false> -SCLDeleteThreshold <Value> -SCLRejectEnabled <$true | $false> -SCLRejectThreshold <Value> -SCLQuarantineEnabled <$true | $false> -SCLQuarantineThreshold <Value>


> [!NOTE]
> La acción Eliminar tiene preferencia sobre la acción Rechazar y la acción Rechazar tiene preferencia sobre la acción Cuarentena. Por lo tanto, el umbral de SCL para la acción «Eliminar» debe ser mayor que el umbral de SCL para la acción «Rechazar», que a su vez debe ser mayor que el umbral SCL para la acción «Cuarentena». Sólo la acción «Rechazar» está habilitada de forma predeterminada, y tiene un valor de umbral SCL de 7.



Este ejemplo configura los siguientes valores para los umbrales SCL:

  - La acción "Eliminar" está habilitada y el umbral SCL correspondiente está establecido en 9.

  - La acción "Rechazar" está habilitada y el umbral SCL correspondiente está establecido en 8.

  - La acción "Cuarentena" está habilitada y el umbral SCL correspondiente está establecido en 7.

<!-- end list -->

    Set-ContentFilterConfig -SCLDeleteEnabled $true -SCLDeleteThreshold 9 -SCLRejectEnabled $true -SCLRejectThreshold 8 -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya configurado correctamente los umbrales SCL, siga estos pasos:

1.  Ejecute el siguiente comando:
    
        Get-ContentFilterConfig | Format-List SCL*

2.  Compruebe que los valores mostrados coinciden con los ajustes que especificó.

## Uso del Shell para configurar la respuesta de rechazo

Cuando la acción «Rechazar» está habilitada, puede personalizar la respuesta de rechazo que se envía al remitente del mensaje. La respuesta de rechazo no puede superar los 240 caracteres.

Para configurar una respuesta de rechazo personalizada, ejecute el siguiente comando:

    Set-ContentFilterConfig -RejectionResponse "<Custom Text>"

Este ejemplo configura el agente de filtrado de contenido para enviar una respuesta de rechazo personalizada.

    Set-ContentFilterConfig -RejectionResponse "Your message was rejected because it appears to be SPAM."

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya configurado correctamente la respuesta de rechazo, siga estos pasos:

1.  Ejecute el siguiente comando:
    
        Get-ContentFilterConfig | Format-List *Reject*

2.  Compruebe que los valores mostrados coinciden con los ajustes que especificó.

## Uso del Shell para habilitar o deshabilitar la certificación electrónica de correo electrónico de Outlook

La validación de *certificación electrónica de correo electrónico de Outlook* es una prueba computacional que Microsoft Office aplica a los mensajes salientes para ayudar a los sistemas de mensajería del destinatario a distinguir entre el correo electrónico legítimo y el correo no deseado. La certificación electrónica está disponible en Outlook 2007 y en las versiones posteriores. La certificación electrónica ayuda a reducir los falsos positivos. La certificación electrónica de correo electrónico de Outlook está habilitada de forma predeterminada.

Para deshabilitar la certificación electrónica de correo electrónico de Outlook, ejecute el comando siguiente:

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $false

Para habilitar la certificación electrónica de correo electrónico de Outlook, ejecute el comando siguiente:

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya configurado correctamente certificación electrónica de correo electrónico de Outlook, siga estos pasos:

1.  Ejecute el siguiente comando:
    
        Get-ContentFilterConfig | Format-List OutlookEmailPostmarkValidationEnabled

2.  Compruebe que el valor mostrado coincida con el ajuste que especificó.

