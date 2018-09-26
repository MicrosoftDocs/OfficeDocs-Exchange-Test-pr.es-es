---
title: 'Administrar el buzón de sitio políticas de provisioning: Exchange 2013 Help'
TOCTitle: Administrar el buzón de sitio políticas de provisioning
ms:assetid: 2f160d1a-a031-461f-8d29-c9cd49ca1645
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ710340(v=EXCHG.150)
ms:contentKeyID: 49895544
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar el buzón de sitio políticas de provisioning

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-21_

Las directivas de aprovisionamiento del buzón del sitio sólo se aplican al correo electrónico que se envía a y desde el buzón del sitio y el tamaño del buzón del sitio en el servidor Exchange.

Para obtener más información acerca de los buzones del sitio, consulte [Buzones de correo del sitio](site-mailboxes-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Buzones de correo de sitio" en el tema [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Aunque puede crear varias directivas de aprovisionamiento de buzones del sitio, sólo se aplicará la política de aprovisionamiento predeterminada a todos los buzones del sitio. No se pueden aplicar varias directivas en la organización.

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear una directiva de aprovisionamiento del buzón del sitio

En este ejemplo se crea la directiva de aprovisionamiento predeterminada SM\_ProvisioningPolicy con la siguiente configuración:

  - La cuota de advertencia para los buzones de sitio es de 9 GB.

  - No se puede recibir mensajes en los buzones de sitio cuando el tamaño del buzón alcanza 10 GB.

  - El tamaño máximo de los mensajes de correo electrónico que se pueden enviar a los buzones de sitio es de 50 MB.

<!-- end list -->
```powershell
    New-SiteMailboxProvisioningPolicy -Name SM_ProvisioningPolicy -IsDefault -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB -MaxReceiveSize 50MB
```

## Ver la configuración de una directiva de aprovisionamiento de buzón del sitio

En este ejemplo se devuelve la información detallada sobre todas las directivas de aprovisionamiento de buzón de la organización.

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List
```

En este ejemplo se devuelven todas las directivas de la organización, pero solamente se muestra la información `IsDefault` para identificar la directiva predeterminada.

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List IsDefault
```

## Realizar cambios en una directiva de aprovisionamiento de buzón del sitio existente

Este ejemplo cambia la directiva de aprovisionamiento de buzón de sitio denominada Default a fin de permitir que el tamaño máximo de mensajes de correo electrónico que el buzón de sitio puede recibir sea de 25 MB. (Cuando instala Exchange, se crea una directiva de aprovisionamiento con el nombre **Predeterminado**.)

```powershell
Set-SiteMailboxProvisioningPolicy -Identity Default -MaxReceiveSize 25MB
```

Este ejemplo cambia la cuota de advertencia a 9,5 GB y la cuota de prohibir envío y de prohibir recepción a 10 GB.

```powershell
    Set-SiteMailboxProvisioningPolicy -Identity Default -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB
```

## Configurar un prefijo de nombre en el buzón del sitio

Al crear un nuevo buzón del sitio, la dirección de correo predeterminada tendrá un prefijo. Con el prefijo de la dirección de correo puede buscar y consultar fácilmente los buzones de los sitios, y también ayuda a los usuarios a reconocerlos. Si quiere, puede deshabilitar el prefijo, o bien modificarlo para su inquilino de Office 365 o para un bosque concreto de una implementación local. Con el comportamiento del prefijo predeterminado, si se crea el buzón del sitio en Office 365, el prefijo predeterminado es **SMO-**. Si, en cambio, el buzón del sitio se crea en la implementación local, el prefijo es **SM-**. El comportamiento predeterminado es diferente según la implementación, de forma que los clientes híbridos no experimenten ningún conflicto si los buzones de los sitios se crean en ambas ubicaciones y luego se sincronizan entre locales.

En este ejemplo se deshabilita la nomenclatura del prefijo configurando el parámetro *DefaultAliasPrefixEnabled* en $false.

```powershell
    Set-SiteMailboxProvisioningPolicy -Identity Default -DefaultAliasPrefixEnabled $false -AliasPrefix $null
```

En este otro ejemplo se modifica la directiva de aprovisionamiento predeterminado y se define el *AliasPrefix* en FOREST01.


> [!NOTE]
> Para las implementaciones con varios bosques, se recomienda usar un prefijo diferente en cada bosque para evitar conflictos cuando los objetos se sincronicen entre los bosques en caso de que los buzones de sitios se hayan creado con el mismo nombre en dos o más bosques.


```powershell
    Set-SiteMailboxProvisioningPolicy -Identity Default -AliasPrefix FOREST01 -DefaultAliasPrefixEnabled $false
```


> [!NOTE]
> En el caso de una implementación híbrida en la que tenga Exchange local y en Office 365, todos los buzones de sitios basados en la nube se crearán con el prefijo <STRONG>SMO-</STRONG>. Los prefijos son diferentes en Office 365 y en la organización local de Exchange para que los clientes no experimenten ningún conflicto si los buzones de sitios se crean en ambas ubicaciones y luego se sincronizan entre locales. El parámetro AliasPrefix tiene preferencia sobre el parámetro DefaultAliasPrefixEnabled. Por lo tanto, si se define el parámetro <EM>AliasPrefix</EM> en una cadena válida que no sea nula, cada nuevo buzón del sitio tendrá una cadena agregada al alias.



## Eliminar una directiva de aprovisionamiento del buzón del sitio

Este ejemplo elimina la directiva del buzón del sitio predeterminada que se creó durante la instalación de Exchange.

```powershell
Remove-SiteMailboxProvisioningPolicy -Identity Default
```


> [!IMPORTANT]
> Primero debe crear y designar otra directiva predeterminada para poder quitar la directiva denominada <STRONG>Predeterminado</STRONG>.



## Más información

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

[New-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/es-es/library/jj218647\(v=exchg.150\))

[Get-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/es-es/library/jj218617\(v=exchg.150\))

[Set-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/es-es/library/jj218624\(v=exchg.150\))

[Remove-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/es-es/library/jj218672\(v=exchg.150\))

