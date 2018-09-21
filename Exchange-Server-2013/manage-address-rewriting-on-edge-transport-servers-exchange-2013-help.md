---
title: 'Gestión reconfigura dirección servidor transporte perimetra Exchange 2013 Help'
TOCTitle: Administrar la reconfiguración de direcciones en servidores de transporte perimetral
ms:assetid: 323a0b55-f921-425d-b1b0-18ad0fac315c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997185(v=EXCHG.150)
ms:contentKeyID: 61061233
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar la reconfiguración de direcciones en servidores de transporte perimetral

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

El Shell de administración de Exchange se usa en un servidor de transporte perimetral para todas las tareas de administración relativas a la reconfiguración de direcciones y a los agentes de reconfiguración de direcciones. Para obtener más información acerca de la reconfiguración de direcciones, consulte [Reconfiguración de direcciones en los servidores de transporte perimetral](address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

Puede crear entradas de reconfiguración de direcciones que se apliquen a un único destinatario, a todos los destinatarios de un dominio o subdominio específico, o a todos los destinatarios de varios subdominios. La reconfiguración de direcciones puede ser de solo salida, o de entrada y salida (bidireccional). Al crear entradas de reconfiguración de direcciones, recuerde lo siguiente:

  - Compruebe que las direcciones de correo electrónico resultantes sean únicas en su organización.

  - Only literal strings are supported in the email address values.

  - El carácter comodín (\*) solo se admite en las direcciones internas (las direcciones que quiere cambiar). La sintaxis válida para usar el carácter comodín es **\*.contoso.com**. Los valores **\*contoso.com** o **sales.\*.com** no se permiten.

  - Cuando use el carácter comodín, debe configurar la reconfiguración de direcciones como de solo salida (debe establecer el parámetro *OutboundOnly* en el valor `$true`).

  - Cuando configure la reconfiguración de direcciones como de solo salida (estableciendo el parámetro *OutboundOnly* en el valor `$true`), debe configurar las direcciones proxy en los destinatarios afectados. Esto permite que el correo que se envía a la dirección reconfigurada se entregue correctamente.

  - De forma predeterminada, la reconfiguración de direcciones es bidireccional para destinatarios únicos o para todos los destinatarios de un dominio o subdominio específico (el valor predeterminado del parámetro *OutboundOnly* es `$false`).

## ¿Qué necesita saber antes de comenzar?

  - Estimated time to complete each procedure: 10 minutes.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Servidores de transporte perimetral" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Tenga cuidado al configurar la reconfiguración de direcciones. Cualquier cambio que haga se aplicará inmediatamente al ejecutar el comando. Considere la posibilidad de ejecutar el comando con el parámetro *WhatIf*. Para obtener más información acerca del parámetro *WhatIf*, consulte [Modificadores WhatIf, Confirm y ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para habilitar o deshabilitar la reconfiguración de direcciones

Para habilitar o deshabilitar por completo la reconfiguración de direcciones, habilite o deshabilite los agentes de reconfiguración de direcciones. De forma predeterminada, los agentes de reconfiguración de direcciones de un servidor de transporte perimetral están habilitados.

Para deshabilitar la reconfiguración de direcciones, ejecute los siguientes comandos:

    Disable-TransportAgent "Address Rewriting Inbound Agent"
    Disable-TransportAgent "Address Rewriting Outbound Agent"

Para habilitar la reconfiguración de direcciones, ejecute los siguientes comandos:

    Enable-TransportAgent "Address Rewriting Inbound Agent"
    Enable-TransportAgent "Address Rewriting Outbound Agent"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la reconfiguración de direcciones se habilitó o deshabilitó correctamente, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
    ```powershell
Get-TransportAgent
```

2.  Compruebe que los valores de la propiedad **Enabled** del agente de reconfiguración de direcciones de entrada y del agente de reconfiguración de direcciones de salida son los valores que ha configurado.

## Usar el Shell para ver las entradas de reconfiguración de direcciones

Para ver una lista de resumen de todas las entradas de reconfiguración de direcciones, ejecute el siguiente comando.

```powershell
Get-AddressRewriteEntry
```

To view details of an address rewrite entry, use the following syntax.

```powershell
Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List
```

El ejemplo siguiente muestra los detalles de la entrada de reconfiguración de direcciones llamada Rewrite Contoso.com to Northwindtraders.com:

```powershell
Get-AddressRewriteEntry "Rewrite Contoso.com to Northwindtraders.com" | Format-List
```

## Usar el Shell para crear entradas de reconfiguración de direcciones

## Reconfigurar las direcciones de correo electrónico de destinatarios únicos

Para reconfigurar la dirección de correo electrónico de un único destinatario, use la siguiente sintaxis:

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> [-OutboundOnly <$true | $false>]

El ejemplo siguiente reconfigura la dirección de correo electrónico de todos los mensajes que entran y salen de la organización para el destinatario joe@contoso.com. Los mensajes de salida se reconfiguran para que parezca que proceden de support@nortwindtraders.com. Los mensajes de entrada que se envían a support@northwindtraders.com se reconfiguran como joe@contoso.com para entregarlos al destinatario (el parámetro *OutboundOnly* es `$false` de forma predeterminada).

    New-AddressRewriteEntry -Name "joe@contoso.com to support@northwindtraders.com" -InternalAddress joe@contoso.com -ExternalAddress support@northwindtraders.com

## Reconfigurar las direcciones de correo electrónico para los destinatarios de un único dominio o subdominio

Para reconfigurar las direcciones de correo electrónico para los destinatarios de un único dominio o subdominio, use la siguiente sintaxis:

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> [-OutboundOnly <$true | $false>]

El ejemplo siguiente reconfigura las direcciones de correo electrónico de todos los mensajes que entran y salen de la organización de Exchange para los destinatarios en el dominio contoso.com. Los mensajes de salida se reconfiguran para que parezca que proceden del dominio fabrikam.com. Los mensajes de entrada enviados a direcciones de correo electrónico de fabrikam.com se reconfiguran para contoso.com para entregarlos a los destinatarios (el parámetro *OutboundOnly* es `$false` de forma predeterminada).

    New-AddressRewriteEntry -Name "Contoso to Fabrikam" -InternalAddress contoso.com -ExternalAddress fabrikam.com

El ejemplo siguiente reconfigura las direcciones de correo electrónico de todos los mensajes que salen de la organización de Exchange y que son enviados por destinatarios del subdominio sales.contoso.com. Los mensajes de salida se reconfiguran para que parezca que proceden del dominio contoso.com. Los mensajes de entrada enviados a direcciones de correo electrónico de contoso.com no se reconfiguran.

    New-AddressRewriteEntry -Name "sales.contoso.com to contoso.com" -InternalAddress sales.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

## Reconfigurar direcciones de correo electrónico para destinatarios en varios subdominios

Para reconfigurar las direcciones de correo electrónico para los destinatarios de un dominio y todos los subdominios, use la siguiente sintaxis.

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -OutboundOnly $true [-ExceptionList <domain1,domain2...>]

El ejemplo siguiente reconfigura las direcciones de correo electrónico de todos los mensajes que salen de la organización de Exchange y que son enviados por destinatarios del dominio contoso.com y todos los subdominios. Los mensajes de salida se reconfiguran para que parezca que proceden del dominio contoso.com. Los mensajes de entrada enviados a destinatarios de contoso.com no se pueden reconfigurar porque se usa un carácter comodín en el parámetro *InternalAddress*.

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

El siguiente ejemplo es igual al anterior, excepto que ahora los mensajes enviados por destinatarios en los subdominios legal.contoso.com y corp.contoso.com no se reconfiguran nunca:

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains except legal.contoso.com and corp.contoso.com" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true -ExceptionList legal.contoso.com,corp.contoso.com

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha creado correctamente las entradas de reconfiguración de direcciones, realice lo siguiente:

1.  Ejecute el comando `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` y confirme que la configuración que aparece es la que ha establecido.

2.  Envíe un mensaje de prueba a un buzón exterior desde un buzón que se haya visto afectado por una entrada de reconfiguración de direcciones. Compruebe que el mensaje de prueba parece provenir de la dirección de correo electrónico reconfigurada.

3.  Responda al mensaje de prueba desde el buzón externo. Compruebe que el buzón original recibe la respuesta.

## Usar el Shell para modificar entradas de reconfiguración de direcciones

Las opciones de configuración que están disponibles cuando se modifica una entrada de reconfiguración de direcciones existente son idénticas que las opciones de configuración para crear una nueva entrada de reconfiguración de direcciones.

## Modificar entradas de reconfiguración de direcciones para destinatarios únicos

Para modificar una entrada de reconfiguración de direcciones que reconfigura la dirección de correo electrónico de un único destinatario, use la sintaxis siguiente:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> -OutboundOnly <$true | $false>

Este ejemplo modifica las siguientes propiedades de la entrada de reconfiguración de direcciones de destinatario único llamada "joe@contoso.com to support@nortwindtraders.com":

  - Cambia la dirección externa a support@northwindtraders.net.

  - Changes the name of the address rewrite entry to "joe@contoso.com to support@northwindtraders.net".

  - Cambia el valor de *OutboundOnly* a `$true`. Tenga en cuenta que este cambio requiere que configure support@northwindtraders.net como dirección proxy en el buzón de Joe.

<!-- end list -->

    Set-AddressRewriteEntry "joe@contoso.com to support@nortwindtraders.com" -Name "joe@contoso.com to support@northwindtraders.net" -ExternalAddress support@northwindtraders.net -OutboundOnly $true

## Modificar las entradas de reconfiguración de direcciones para destinatarios en dominios o subdominios únicos

Para modificar una entrada de reconfiguración de direcciones que reconfigura las direcciones de correo electrónico de los destinatarios en un dominio o subdominio único, use la sintaxis siguiente.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> -OutboundOnly <$true | $false>

El ejemplo siguiente cambia el valor de la dirección interna de la entrada de reconfiguración de direcciones de dominio único llamada "Northwind Traders to Contoso".

```powershell
Set-AddressRewriteEntry "Northwindtraders to Contoso" -InternalAddress northwindtraders.net
```

## Modificar entradas de reconfiguración de direcciones para destinatarios en varios subdominios

Para modificar una entrada de reconfiguración de direcciones que reconfigura la dirección de correo electrónico de destinatarios en un dominio y todos los subdominios, use la sintaxis siguiente.

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -ExceptionList <list of domains>

Para reemplazar los valores de la lista de excepciones existente de una entrada de reconfiguración de direcciones de varios subdominios, use la siguiente sintaxis:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList <domain1,domain2,...>

El ejemplo siguiente reemplaza la lista de excepciones existente para la entrada de reconfiguración de direcciones de varios subdominios llamada Contoso to Northwind Traders por los valores marketing.contoso.com y legal.contoso.com:

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList sales.contoso.com,legal.contoso.com

Para agregar o quitar selectivamente valores de lista de excepciones de una entrada de reconfiguración de direcciones de varios subdominios sin modificar los valores de la lista de excepciones existente, use la siguiente sintaxis:

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

El ejemplo siguiente agrega finanace.contoso.com y quita marketing.contoso.com de la lista de excepciones de la entrada de reconfiguración de direcciones de varios subdominios llamada Contoso to Northwind Traders:

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList @{Add="finanace.contoso.com"; Remove="marketing.contoso.com"}

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha modificado correctamente una entrada de reconfiguración de direcciones, realice lo siguiente:

1.  Ejecute el comando `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` y confirme que la configuración que aparece es la que ha establecido.

2.  Envíe un mensaje de prueba a un buzón exterior desde un buzón que se haya visto afectado por una entrada de reconfiguración de direcciones. Compruebe que el mensaje de prueba parece provenir de la dirección de correo electrónico reconfigurada.

3.  Responda al mensaje de prueba desde el buzón externo. Compruebe que el buzón original recibe la respuesta.

## Usar el Shell para quitar entradas de reconfiguración de direcciones

Para quitar una única entrada de reconfiguración de direcciones, use la siguiente sintaxis:

```powershell
Remove-AddressRewriteEntry <AddressRewriteEntryIdentity>
```

El ejemplo siguiente quita la entrada de reconfiguración de direcciones llamada "Contoso.com to Northwindtraders.com":

```powershell
Remove-AddressRewriteEntry "Contoso.com to Northwindtraders.com"
```

Para quitar varias entradas de reconfiguración de direcciones, use la siguiente sintaxis:

    Get-AddressRewriteEntry [<search criteria>] | Remove-AddressRewriteEntry [-WhatIf]

El ejemplo siguiente quita todas las entradas de reconfiguración de direcciones:

```powershell
Get-AddressRewriteEntry | Remove-AddressRewriteEntry
```

El ejemplo siguiente simula la eliminación de las entradas de reconfiguración de direcciones que contienen el texto "to contoso.com" en el nombre. El modificador *WhatIf* permite ver previamente el resultado sin confirmar los cambios.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry -WhatIf

Si está satisfecho con el resultado, ejecute el comando de nuevo sin el modificador *WhatIf* para quitar las entradas de reconfiguración de direcciones.

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry

## ¿Cómo saber si el proceso se ha completado correctamente?

To verify that you have successfully removed an address rewrite entry, do the following:

1.  Ejecute el comando `Get-AddressRewriteEntry` y compruebe que las entradas de reconfiguración de direcciones que ha quitado no están en la lista.

2.  Envíe un mensaje de prueba a un buzón exterior desde un buzón que se haya visto afectado por una entrada de reconfiguración de direcciones. Compruebe que el mensaje de prueba ya no resulta afectado por la entrada de reconfiguración de direcciones eliminada.

3.  Responda al mensaje de prueba desde el buzón externo. Compruebe que el buzón original recibe la respuesta y que el mensaje no se ve afectado por la entrada de reconfiguración de direcciones eliminada.

