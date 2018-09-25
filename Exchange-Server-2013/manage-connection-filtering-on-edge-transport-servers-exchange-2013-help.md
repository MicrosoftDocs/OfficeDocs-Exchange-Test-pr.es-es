---
title: 'Administrar el filtrado de conexiones en servidores de transporte perimetral: Exchange 2013 Help'
TOCTitle: Administrar el filtrado de conexiones en servidores de transporte perimetral
ms:assetid: baebc865-ec3e-48ca-ac48-7aac8b34c003
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124376(v=EXCHG.150)
ms:contentKeyID: 60830019
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar el filtrado de conexiones en servidores de transporte perimetral

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

El filtrado de conexiones es una característica contra correo no deseado proporcionada por el agente de filtrado de conexiones, que está disponible solamente en los servidores de transporte perimetral de Microsoft Exchange 2013. El filtrado de conexiones habilita las siguientes características:

  - listas de direcciones IP bloqueadas

  - proveedores de listas de direcciones IP bloqueadas

  - listas de direcciones IP admitidas

  - proveedores de lista de IP permitidas

Cada una de estas características se puede habilitar o deshabilitar por separado.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Características contra el correo no deseado" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para habilitar o deshabilitar el filtrado de conexión

Para habilitar o deshabilitar por completo el filtrado de conexiones, habilite o deshabilite el agente de filtrado de conexiones. El cambio surte efecto después de que se reinicia el servicio de transporte de Microsoft Exchange. Al reiniciar este servicio en un servidor Transporte perimetral, el flujo de correo del servidor se interrumpe temporalmente.

Para deshabilitar el filtrado de conexiones, ejecute el comando siguiente:

```powershell
Disable-TransportAgent "Connection Filtering Agent"
```

Para habilitar el filtrado de conexiones, ejecute el siguiente comando:

```powershell
Enable-TransportAgent "Connection Filtering Agent"
```

Para que el cambio surta efecto, reinicie el servicio de transporte de Microsoft Exchange ejecutando el siguiente comando:

```powershell
Restart-Service MSExchangeTransport
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya habilitado o deshabilitado correctamente el filtrado de conexiones, ejecute el siguiente comando y compruebe que el valor mostrado sea el valor que haya configurado.

```powershell
Get-TransportAgent "Connection Filtering Agent" | Format-List Enabled
```

## Procedimientos de listas de direcciones IP bloqueadas

Estos procedimientos se aplican a la lista de direcciones IP bloqueadas que se configura de forma manual. No se aplican a los proveedores de listas de IP bloqueadas.

Use los cmdlets **IPBlockListConfig** para ver y configurar la forma en que el filtrado de conexiones usa la lista de direcciones IP bloqueadas. Use los cmdlets **IPBlockListEntry** para ver y configurar las direcciones IP bloqueadas en la lista de direcciones IP bloqueadas.

## Uso del Shell para ver la configuración de la lista de direcciones IP bloqueadas

Para ver la configuración de la lista de direcciones IP bloqueadas, ejecute el siguiente comando:

```powershell
Get-IPBlockListConfig | Format-List *Enabled,*Response
```

## Uso del Shell para habilitar o deshabilitar la lista de direcciones IP bloqueadas

Para deshabilitar la lista de direcciones IP bloqueadas, ejecute el siguiente comando:

```powershell
Set-IPBlockListConfig -Enabled $false
```


Para habilitar la lista de direcciones IP bloqueadas, ejecute el siguiente comando:

```powershell
Set-IPBlockListConfig -Enabled $true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya habilitado o deshabilitado correctamente la lista de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que el valor mostrado sea el valor que haya configurado.

```powershell
Get-IPBlockListConfig | Format-List Enabled
```

## Uso del Shell para configurar la lista de direcciones IP bloqueadas

Para configurar la lista de direcciones IP bloqueadas, use la siguiente sintaxis:

```powershell
Set-IPBlockListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false> -MachineEntryRejectionResponse "<Custom response text>"] [-StaticEntryRejectionResponse "<Custom response text>"]
```

En este ejemplo se configura la lista de direcciones IP bloqueadas de la siguiente forma:

  - La lista de direcciones IP bloqueadas filtra las conexiones entrantes de los servidores de correo internos y externos. De manera predeterminada, las conexiones se filtran desde servidores de correo externos únicamente (*ExternalMailEnabled* se establece en `$true` y *InternalMailEnabled* se establece en `$false`). Las conexiones no autenticadas y las conexiones autenticadas de socios externos se consideran externas.

  - El texto de respuesta personalizado para las conexiones filtradas por direcciones IP que se agregaron automáticamente a la lista de direcciones IP bloqueadas mediante la característica de reputación del remitente del agente de análisis de protocolo se establece en el valor "La reputación del remitente rechazó la conexión de la dirección IP {0}".

  - El texto de respuesta personalizado para las conexiones filtradas por las direcciones IP que se agregaron de forma manual a la lista de direcciones IP bloqueadas se establece en el valor "El filtrado de conexiones rechazó la conexión de la dirección IP {0}".

<!-- end list -->

```powershell
Set-IPBlockListConfig -InternalMailEnabled $true -MachineEntryRejectionResponse "Connection from IP address {0} was rejected by sender reputation." -StaticEntryRejectionResponse "Connection from IP address {0} was rejected by connection filtering."
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya configurado correctamente la lista de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que los valores mostrados sean los valores que haya configurado.

```powershell
Get-IPBlockListConfig | Format-List *MailEnabled,*Response
```

## Uso del Shell para ver entradas de la lista de direcciones IP bloqueadas

Para ver todas las entradas de la lista de direcciones IP bloqueadas, ejecute el siguiente comando:

```powershell
Get-IPBlockListEntry
```

Tenga en cuenta que cada entrada de la lista de direcciones IP bloqueadas se identifica mediante un valor entero. El entero de identidad se asigna en orden ascendente cuando se agregan entradas a la lista de direcciones IP bloqueadas y la lista de direcciones IP permitidas.

Para ver una entrada de la lista de direcciones IP bloqueadas, use la siguiente sintaxis:

```powershell
Get-IPBlockListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

Por ejemplo, para ver la entrada de la lista de direcciones IP bloqueadas que contiene la dirección IP 192.168.1.13, ejecute el siguiente comando:

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.13
```


> [!NOTE]
> Al usar el parámetro <EM>IPAddress</EM>, la entrada de la lista de direcciones IP bloqueadas resultante puede ser una dirección IP individual, un intervalo de direcciones IP o una dirección IP del Enrutamiento de interdominios sin clases (CIDR). Para usar el parámetro <EM>Identity</EM>, especifique el valor entero que se asigna a la entrada de la lista de direcciones IP bloqueadas.



## Uso del Shell para agregar entradas de la lista de direcciones IP bloqueadas

Para agregar entradas de la lista de direcciones IP bloqueadas, use la siguiente sintaxis:

```powershell
Add-IPBlockListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-comment "<Descriptive Comment>"]
```

En el siguiente ejemplo se agrega la entrada de la lista de direcciones IP bloqueadas para el intervalo de direcciones IP de 192.168.1.10 a 192.168.1.15, y se configura la entrada de la lista de direcciones IP bloqueadas para que expire el 14 de julio de 2014 a las 15:00.

```powershell
Add-IPBlockListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya agregado correctamente una entrada de la lista de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que aparezca la nueva entrada de la lista de direcciones IP bloqueadas.

```powershell
Get-IPBlockListEntry
```

## Uso del Shell para quitar entradas de la lista de direcciones IP bloqueadas

Para quitar entradas de la lista de direcciones IP bloqueadas, use la siguiente sintaxis:

```powershell
Remove-IPBlockListEntry <IdentityInteger>
```

En el siguiente ejemplo se quita la entrada de la lista de direcciones IP bloqueadas que tiene el valor 3 *Identity*.

```powershell
Remove-IPBlockListEntry 3
```

En el siguiente ejemplo se quita la entrada de la lista de direcciones IP bloqueadas que contiene la dirección IP 192.168.1.12 sin usar el valor entero *Identity*. Tenga en cuenta que la entrada de la lista de direcciones IP bloqueadas puede ser una dirección IP individual o un intervalo de direcciones IP.

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.12 | Remove-IPBlockListEntry
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya quitado correctamente una entrada de la lista de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que haya desaparecido la entrada de la lista de direcciones IP bloqueadas que quitó.

```powershell
Get-IPBlockListEntry
```

## Procedimientos de proveedores de listas de direcciones IP bloqueadas

Estos procedimientos se aplican a los proveedores de listas de direcciones IP bloqueadas. No se aplican a la lista de direcciones IP bloqueadas.

Use los cmdlets **IPBlockListProvidersConfig** para ver y configurar la forma en que el filtrado de conexiones usa todos los proveedores de listas de direcciones IP bloqueadas. Use los cmdlets **IPBlockListProvider** para ver, configurar y probar los proveedores de listas de direcciones IP bloqueadas.

## Uso del Shell para ver la configuración de todos los proveedores de listas de direcciones IP bloqueadas

Para ver cómo el filtrado de conexiones usa todos los proveedores de listas de direcciones IP bloqueadas, ejecute el siguiente comando:

```powershell
Get-IPBlockListProvidersConfig | Format-List *Enabled,Bypassed*
```

## Uso del Shell para habilitar o deshabilitar todos los proveedores de listas de direcciones IP bloqueadas

Para deshabilitar todos los proveedores de listas de direcciones IP bloqueadas, ejecute el siguiente comando:

```powershell
Set-IPBlockListProvidersConfig -Enabled $false
```

Para habilitar todos los proveedores de listas de direcciones IP bloqueadas, ejecute el siguiente comando:

```powershell
Set-IPBlockListProvidersConfig -Enabled $true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se hayan habilitado o deshabilitado correctamente todos los proveedores de listas de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que el valor mostrado sea el valor que haya configurado.

```powershell
Get-IPBlockListProvidersConfig | Format-List Enabled
```

## Uso del Shell para configurar todos los proveedores de listas de direcciones IP bloqueadas

Para configurar la forma en que el filtrado de conexiones usa todos los proveedores de listas de direcciones IP bloqueadas, use la siguiente sintaxis:

```powershell
Set-IPBlockListProvidersConfig [-BypassedRecipients <recipient1,recipient2...>] [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]
```

En el siguiente ejemplo se configuran todos los proveedores de listas de direcciones IP bloqueadas con las siguientes opciones:

  - Los proveedores de listas de direcciones IP bloqueadas filtran las conexiones entrantes de los servidores de correo internos y externos. De manera predeterminada, las conexiones se filtran desde servidores de correo externos únicamente (*ExternalMailEnabled* se establece en `$true` y *InternalMailEnabled* se establece en `$false`). Las conexiones no autenticadas y las conexiones autenticadas de socios externos se consideran externas.

  - Los mensajes enviados a los destinatarios internos chris@fabrikam.com y michelle@fabrikam.com se excluyen del filtrado por parte de los proveedores de listas de direcciones IP bloqueadas. Tenga en cuenta que si quiere agregar destinatarios a la lista sin afectar a los destinatarios existentes, debe usar la sintaxis `@{Add="<recipient1>","<recipient2>"...}`.

<!-- end list -->

```powershell
Set-IPBlockListProvidersConfig -BypassedRecipients chris@fabrikam.com,michelle@fabrikam.com -InternalMailEnabled $true
```

Para más información, vea [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/es-es/library/aa998543\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se hayan configurado correctamente todos los proveedores de listas de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que los valores mostrados sean los valores que haya configurado.

```powershell
Get-IPBlockListProvidersConfig | Format-List *MailEnabled,Bypassed*
```

## Uso del Shell para ver proveedores de listas de direcciones IP bloqueadas

Para ver la lista de resumen de todos los proveedores de listas de direcciones IP bloqueadas, ejecute el siguiente comando:

```powershell
Get-IPBlockListProvider
```

Para ver los detalles de un proveedor específico, use la siguiente sintaxis:

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity>
```

En el siguiente ejemplo se muestran los detalles del proveedor llamado Proveedor de listas de direcciones IP bloqueadas de Contoso.

```powershell
Get-IPBlockListProvider "Contoso IP Block List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match,*Response
```

## Uso del Shell para agregar un proveedor de listas de direcciones IP bloqueadas

Para agregar un proveedor de listas de direcciones IP bloqueadas, use la siguiente sintaxis:

```powershell
Add-IPBlockListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]
```

En este ejemplo se crea un proveedor de listas de direcciones IP bloqueadas llamado "Proveedor de listas de direcciones IP bloqueadas de Contoso" con las siguientes opciones:

  - **FQDN para usar el proveedor** rbl.contoso.com

  - **Código de máscara de bits que se va a usar del proveedor** 127.0.0.1

<!-- end list -->

```powershell
Add-IPBlockListProvider -Name "Contoso IP Block List Provider" -LookupDomain rbl.contoso.com -BitmaskMatch 127.0.0.1
```


> [!NOTE]
> Al agregar un nuevo proveedor de listas de direcciones IP bloqueadas, se habilita de manera predeterminada (el valor de <EM>Enabled</EM> es <CODE>$true</CODE>), y el valor de prioridad se incrementa (la primera entrada tiene el valor 1 <EM>Priority</EM>).



Para más información, vea [Add-IPBlockListProvider](https://technet.microsoft.com/es-es/library/bb124358\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya agregado correctamente un proveedor de listas de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que aparezca el nuevo proveedor de listas de direcciones IP bloqueadas.

```powershell
Get-IPBlockListProvider
```

## Uso del Shell para habilitar o deshabilitar un proveedor de listas de direcciones IP bloqueadas

Para habilitar o deshabilitar un proveedor específico de listas de direcciones IP bloqueadas, use la siguiente sintaxis:

```powershell
Set-IPBlockListProvider <IPBlockListProviderIdentity> -Enabled <$true | $false>
```

En el siguiente ejemplo se deshabilita el proveedor llamado Proveedor de listas de direcciones IP bloqueadas de Contoso.

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $false
```

En el siguiente ejemplo se habilita el proveedor llamado Proveedor de listas de direcciones IP bloqueadas de Contoso.

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya habilitado o deshabilitado correctamente un proveedor de listas de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que el valor mostrado sea el valor que haya configurado.

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List Enabled
```

## Uso del Shell para configurar un proveedor de listas de direcciones IP bloqueadas

Las opciones de configuración que están disponibles en el cmdlet **Set-IPBlockListProvider** son idénticas para las que están disponibles en el cmdlet **New-IPBlockListProvider**.

Para configurar un proveedor existente de listas de direcciones IP bloqueadas, use la siguiente sintaxis:

```powershell
Set-IPBlockListProvider <IPBlockListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]
```

Por ejemplo, para agregar el código de estado de dirección IP 127.0.0.1 a la lista de códigos de estado existentes para el proveedor llamado Proveedor de listas de direcciones IP bloqueadas de Contoso, ejecute el siguiente comando:


Set-IPBlockListProvider "Contoso IP Block List Provider" -IPAddressesMatch @{Add="127.0.0.1"}

Para más información, vea [Set-IPBlockListProvider](https://technet.microsoft.com/es-es/library/bb124979\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya configurado correctamente un proveedor de listas de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que los valores mostrados sean los valores que haya configurado.

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List
```

## Uso del Shell para probar un proveedor de listas de direcciones IP bloqueadas

Para probar un proveedor de listas de direcciones IP bloqueadas, use la siguiente sintaxis.

```powershell
Test-IPBlockListProvider <IPBlockListProviderIdentity> -IPAddress <IPAddressToTest>
```

En el siguiente ejemplo se prueba el proveedor llamado Proveedor de listas de direcciones IP bloqueadas de Contoso buscando la dirección IP 192.168.1.1.

```powershell
Test-IPBlockListProvider "Contoso IP Block List Provider" -IPAddress 192.168.1.1
```

## Uso del Shell para quitar un proveedor de listas de direcciones IP bloqueadas

Para quitar un proveedor de listas de direcciones IP bloqueadas, use la siguiente sintaxis:

```powershell
Remove-IPBlockListProvider <IPBlockListProviderIdentity>
```

En el siguiente ejemplo se quita un proveedor de listas de direcciones IP bloqueadas llamado Proveedor de listas de direcciones IP bloqueadas de Contoso.

```powershell
Remove-IPBlockListProvider "Contoso IP Block list Provider"
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya quitado correctamente un proveedor de listas de direcciones IP bloqueadas, ejecute el siguiente comando y compruebe que haya desaparecido el proveedor de listas de direcciones IP bloqueadas que quitó.

```powershell
Get-IPBlockListProvider
```

## Procedimientos de listas de direcciones IP permitidas

Estos procedimientos se aplican a la lista de direcciones IP permitidas que se configura de forma manual. No se aplican a los proveedores de listas de IP permitidas.

Use los cmdlets **IPAllowListConfig** para ver y configurar la forma en que el filtrado de conexiones usa la lista de direcciones IP permitidas. Use los cmdlets **IPAllowListEntry** para ver y configurar las direcciones IP en la lista de direcciones IP permitidas.

## Uso del Shell para ver la configuración de la lista de direcciones IP permitidas

Para ver la configuración de la lista de direcciones IP permitidas, ejecute el siguiente comando:

```powershell
Get-IPAllowListConfig | Format-List *Enabled
```

## Uso del Shell para habilitar o deshabilitar la lista de direcciones IP permitidas

Para deshabilitar la lista de direcciones IP permitidas, ejecute el siguiente comando:

```powershell
Set-IPAllowListConfig -Enabled $false
```

Para habilitar la lista de direcciones IP permitidas, ejecute el siguiente comando:

```powershell
Set-IPAllowListConfig -Enabled $true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya habilitado o deshabilitado correctamente la lista de direcciones IP permitidas, ejecute el siguiente comando y compruebe que el valor mostrado sea el valor que haya configurado.

```powershell
Get-IPAllowListConfig | Format-List Enabled
```

## Uso del Shell para configurar la lista de direcciones IP permitidas

Para configurar la lista de direcciones IP permitidas, use la siguiente sintaxis:

```powershell
Set-IPAllowListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>
```

En este ejemplo se configura la lista de direcciones IP permitidas para filtrar las conexiones entrantes de los servidores de correo internos y externos. De manera predeterminada, las conexiones se filtran desde servidores de correo externos únicamente (*ExternalMailEnabled* se establece en `$true` y *InternalMailEnabled* se establece en `$false`). Las conexiones no autenticadas y las conexiones autenticadas de socios externos se consideran externas.

```powershell
Set-IPAllowListConfig -InternalMailEnabled $true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya configurado correctamente la lista de direcciones IP permitidas, ejecute el siguiente comando y compruebe que los valores mostrados sean los valores que haya configurado.

```powershell
Get-IPAllowListConfig | Format-List *MailEnabled
```

## Uso del Shell para ver entradas de la lista de direcciones IP permitidas

Para ver todas las entradas de la lista de direcciones IP permitidas, ejecute el siguiente comando:

```powershell
Get-IPAllowListEntry
```

Tenga en cuenta que cada entrada de la lista de direcciones IP permitidas se identifica mediante un valor entero. El entero de identidad se asigna en orden ascendente cuando se agregan entradas a la lista de direcciones IP bloqueadas y la lista de direcciones IP permitidas.

Para ver una entrada de la lista de direcciones IP permitidas, use la siguiente sintaxis:

```powershell
Get-IPAllowListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

Por ejemplo, para ver la entrada de la lista de direcciones IP permitidas que contiene la dirección IP 192.168.1.13, ejecute el siguiente comando:

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.13
```


> [!NOTE]
> Al usar el parámetro <EM>IPAddress</EM>, la entrada de la lista de direcciones IP permitidas resultante puede ser una dirección IP individual, un intervalo de direcciones IP o una dirección IP del Enrutamiento de interdominios sin clases (CIDR). Para usar el parámetro <EM>Identity</EM>, especifique el valor entero que se asigna a la entrada de la lista de direcciones IP permitidas.



## Uso del Shell para agregar entradas de la lista de direcciones IP permitidas

Para agregar entradas de la lista de direcciones IP permitidas, use la siguiente sintaxis:

```powershell
Add-IPAllowListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-Comment "<Descriptive Comment>"]
```

En este ejemplo se agrega la entrada de la lista de direcciones IP permitidas para el intervalo de direcciones IP de 192.168.1.10 a 192.168.1.15, y se configura la entrada de la lista de direcciones IP permitidas para que expire el 14 de julio de 2014 a las 15:00.

```powershell
Add-IPAllowListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya agregado correctamente una entrada de la lista de direcciones IP permitidas, ejecute el siguiente comando y compruebe que aparezca la nueva entrada de la lista de direcciones IP permitidas.

```powershell
Get-IPAllowListEntry
```

## Uso del Shell para quitar entradas de la lista de direcciones IP permitidas

Para quitar entradas de la lista de direcciones IP permitidas, use la siguiente sintaxis:

```powershell
Remove-IPAllowListEntry <IdentityInteger>
```

En el siguiente ejemplo se quita la entrada de la lista de direcciones IP permitidas que tiene el valor 3 *Identity*.

```powershell
Remove-IPAllowListEntry 3
```

En el siguiente ejemplo se quita la entrada de la lista de direcciones IP permitidas que contiene la dirección IP 192.168.1.12 sin usar el valor entero *Identity*. Tenga en cuenta que la entrada de la lista de direcciones IP permitidas puede ser una dirección IP individual o un intervalo de direcciones IP.

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.12 | Remove-IPAllowListEntry
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya quitado correctamente una entrada de la lista de direcciones IP permitidas, ejecute el siguiente comando y compruebe que haya desaparecido la entrada de la lista de direcciones IP permitidas que quitó.

```powershell
Get-IPAllowListEntry
```

## Procedimientos de proveedores de listas de direcciones IP permitidas

Estos procedimientos se aplican a los proveedores de listas de direcciones IP permitidas. No se aplican a la lista de direcciones IP permitidas.

Use los cmdlets **IPAllowListProvidersConfig** para ver y configurar la forma en que el filtrado de conexiones usa todos los proveedores de listas de direcciones IP permitidas. Use los cmdlets **IPAllowListProvider** para ver, configurar y probar los proveedores de listas de direcciones IP permitidas.

## Uso del Shell para ver la configuración de todos los proveedores de listas de direcciones IP permitidas

Para ver cómo el filtrado de conexiones usa todos los proveedores de listas de direcciones IP permitidas, ejecute el siguiente comando:

```powershell
Get-IPAllowListProvidersConfig | Format-List *Enabled
```

## Uso del Shell para habilitar o deshabilitar todos los proveedores de listas de direcciones IP permitidas

Para deshabilitar todos los proveedores de listas de direcciones IP permitidas, ejecute el siguiente comando:

```powershell
Set-IPAllowListProvidersConfig -Enabled $false
```

Para habilitar todos los proveedores de listas de direcciones IP permitidas, ejecute el siguiente comando:

```powershell
Set-IPAllowListProvidersConfig -Enabled $true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se hayan habilitado o deshabilitado correctamente todos los proveedores de listas de direcciones IP permitidas, ejecute el siguiente comando y compruebe que el valor mostrado sea el valor que haya configurado.

```powershell
Get-IPAllowListProvidersConfig | Format-List Enabled
```

## Uso del Shell para configurar todos los proveedores de listas de direcciones IP permitidas

Para configurar la forma en que el filtrado de conexiones usa todos los proveedores de listas de direcciones IP permitidas, use la siguiente sintaxis:

```powershell
Set-IPAllowListProvidersConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]
```

En este ejemplo se configuran todos los proveedores de listas de direcciones IP permitidas para filtrar las conexiones entrantes de los servidores de correo internos y externos. De manera predeterminada, las conexiones se filtran desde servidores de correo externos únicamente (*ExternalMailEnabled* se establece en `$true` y *InternalMailEnabled* se establece en `$false`). Las conexiones no autenticadas y las conexiones autenticadas de socios externos se consideran externas.

```powershell
Set-IPAllowListProvidersConfig -InternalMailEnabled $true
```

Para más información, vea [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/es-es/library/aa998543\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se hayan configurado correctamente todos los proveedores de listas de direcciones IP permitidas, ejecute el siguiente comando y compruebe que los valores mostrados sean los valores que haya configurado.

```powershell
Get-IPAllowListProvidersConfig | Format-List *MailEnabled
```

## Uso del Shell para ver proveedores de listas de direcciones IP permitidas

Para ver la lista de resumen de todos los proveedores de listas de direcciones IP permitidas, ejecute el siguiente comando.

```powershell
Get-IPAllowListProvider
```

Para ver los detalles de un proveedor específico, use la siguiente sintaxis.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity>
```

En este ejemplo se muestran los detalles del proveedor llamado Proveedor de listas de direcciones IP permitidas de Contoso.

```powershell
Get-IPAllowListProvider "Contoso IP Allow List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match
```

## Uso del Shell para agregar un proveedor de listas de direcciones IP permitidas

Para agregar un proveedor de listas de direcciones IP permitidas, use la siguiente sintaxis:

```powershell
Add-IPAllowListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]
```

En este ejemplo se crea un proveedor de listas de direcciones IP permitidas llamado "Proveedor de listas de direcciones IP permitidas de Contoso" con las siguientes opciones:

  - **FQDN para usar el proveedor** allow.contoso.com

  - **Código de máscara de bits que se va a usar del proveedor** 127.0.0.1

<!-- end list -->

```powershell
Add-IPAllowListProvider -Name "Contoso IP Allow List Provider" -LookupDomain allow.contoso.com -BitmaskMatch 127.0.0.1
```


> [!NOTE]
> Al agregar un nuevo proveedor de listas de direcciones IP permitidas, se habilita de manera predeterminada (el valor de <EM>Enabled</EM> es <CODE>$true</CODE>), y el valor de prioridad se incrementa (la primera entrada tiene el valor 1 <EM>Priority</EM>).



Para más información, vea [Add-IPBlockListProvider](https://technet.microsoft.com/es-es/library/bb124358\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya agregado correctamente un proveedor de listas de direcciones IP permitidas, ejecute el siguiente comando y compruebe que aparezca el nuevo proveedor de listas de direcciones IP permitidas.

```powershell
Get-IPAllowListProvider
```

## Uso del Shell para habilitar o deshabilitar un proveedor de listas de direcciones IP permitidas

Para habilitar o deshabilitar un proveedor específico de listas de direcciones IP permitidas, use la siguiente sintaxis.

```powershell
Set-IPAllowListProvider <IPAllowListProviderIdentity> -Enabled <$true | $false>
```

En este ejemplo se deshabilita el proveedor llamado Proveedor de listas de direcciones IP permitidas de Contoso.

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $false
```

En este ejemplo se habilita el proveedor llamado Proveedor de listas de direcciones IP permitidas de Contoso.

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya habilitado o deshabilitado correctamente un proveedor de listas de direcciones IP permitidas, ejecute el siguiente comando y compruebe que el valor mostrado sea el valor que haya configurado.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List Enabled
```

## Uso del Shell para configurar un proveedor de listas de direcciones IP permitidas

Las opciones de configuración que están disponibles en el cmdlet **Set-IPAllowListProvider** son idénticas para las que están disponibles en el cmdlet **New-IPAllowListProvider**.

Para configurar un proveedor existente de listas de direcciones IP permitidas, use la siguiente sintaxis:

```powershell
Set-IPAllowListProvider <IPAllowListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]
```

Por ejemplo, para agregar el código de estado de dirección IP 127.0.0.1 a la lista de códigos de estado existentes para el proveedor llamado Proveedor de listas de direcciones IP permitidas de Contoso, ejecute el siguiente comando:

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddressesMatch @{Add="127.0.0.1"}
```

Para más información, vea [Set-IPBlockListProvider](https://technet.microsoft.com/es-es/library/bb124979\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya configurado correctamente un proveedor de listas de direcciones IP permitidas, ejecute el siguiente comando y compruebe que los valores mostrados sean los valores que haya configurado.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List
```

## Uso del Shell para probar un proveedor de listas de direcciones IP permitidas

Para probar un proveedor de listas de direcciones IP permitidas, use la siguiente sintaxis:

```powershell
Test-IPAllowListProvider <IPAllowListProviderIdentity> -IPAddress <IPAddressToTest>
```

En el siguiente ejemplo se prueba el proveedor llamado Proveedor de listas de direcciones IP permitidas de Contoso buscando la dirección IP 192.168.1.1.

```powershell
Test-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddress 192.168.1.1
```

## Uso del Shell para quitar un proveedor de listas de direcciones IP permitidas

Para quitar un proveedor de listas de direcciones IP permitidas, use la siguiente sintaxis:

```powershell
Remove-IPAllowListProvider <IPAllowListProviderIdentity>
```

En este ejemplo se quita el proveedor de listas de direcciones IP permitidas llamado Proveedor de listas de direcciones IP permitidas de Contoso.

```powershell
Remove-IPAllowListProvider "Contoso IP Allow List Provider"
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se haya quitado correctamente un proveedor de listas de direcciones IP permitidas, ejecute el siguiente comando y compruebe que haya desaparecido el proveedor de listas de direcciones IP permitidas que quitó.

```powershell
Get-IPAllowListProvider
```

