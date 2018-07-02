---
title: 'Configuración de enrutamiento de correo de Exchange en Active Directory: Exchange 2013 Help'
TOCTitle: Configuración de enrutamiento de correo de Exchange en Active Directory
ms:assetid: d01f8545-c201-4a96-be39-ed4c7008afcf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ674705(v=EXCHG.150)
ms:contentKeyID: 49895925
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración de enrutamiento de correo de Exchange en Active Directory

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

De manera predeterminada, Microsoft Exchange Server 2013 hace referencia a los objetos de vínculo a sitios IP en Active Directory para ayudarlo a determinar la ruta de acceso menos costosa. Sin embargo, si determina que los costos de vínculo a sitios IP de Active Directory y los patrones de flujo de tráfico no son los mejores para el enrutamiento de correo en Exchange, puede establecer configuraciones en Active Directory que solo usen Exchange para optimizar el flujo de correo.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Sitio y administración del vínculo del sitio de Active Directory" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para configurar un costo específico de Exchange en un vínculo a sitios IP de Active Directory

Determine el nombre del vínculo a sitios IP de Active Directory para el que desea establecer un costo de Exchange. Un valor de costo más bajo indica una ruta preferida. Puede examinar el contenido de los registros de la tabla de enrutamiento y ver los datos en la sección del identificador **ADTopologyPath ID** para ver los detalles acerca de la ruta de acceso menos costosa calculada entre dos sitios de Active Directory.

Para establecer un costo específico de Exchange en un vínculo a sitios de Active Directory, ejecute el siguiente comando:

``` 
 Set-AdSiteLink <ADSiteLinkIdentity> -ExchangeCost <Integer | $null>
```

En este ejemplo, se establece un costo específico de Exchange de 10 para el vínculo al sitio IP denominado IPSiteLinkAB.

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost 10

En este ejemplo, se borra el costo específico de Exchange en el vínculo al sitio IP IPSiteLinkAB.

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost $null

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que estableció correctamente un costo de Exchange en un vínculo a sitios de Active Directory, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-AdSiteLink | Format-List Name,ExchangeCost

2.  Compruebe que el costo de Exchange está configurado en el vínculo a sitios de Active Directory.

## Uso del Shell para configurar un sitio de Active Directory como sitio de concentradores

Cuando existe un sitio de concentrador junto con la ruta de acceso menos costosa para un mensaje, el mensaje debe enrutarse a través del sitio del concentrador. Examine el contenido de los registros de la tabla de enrutamiento y vea los datos de la sección **ADTopologyPath ID** para comprobar si existe el sitio seleccionado en la ruta de acceso menos costosa entre dos sitios de Active Directory. Si no es el caso, debe asignar costos específicos de Exchange a los vínculos a sitios IP para que la ruta de acceso menos costosa pase por los sitios seleccionados.

Para configurar un sitio de Active Directory en un sitio del concentrador, ejecute el siguiente comando:

    Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true

En este ejemplo, el sitio de Active Directory denominado Sitio A se configura como un sitio del concentrador.

    Set-AdSite "Site A" -HubSiteEnabled $true

En este ejemplo se elimina el atributo de sitio del concentrador del sitio de Active Directory denominado Sitio B.

    Set-AdSite "Site B" -HubSiteEnabled $false

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que configuró correctamente un sitio de Active Directory como un sitio del concentrador, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-AdSite | Format-List Name,HubSiteEnabled

2.  Compruebe que el valor *HubSiteEnabled* es `True` para el sitio de Active Directory.

