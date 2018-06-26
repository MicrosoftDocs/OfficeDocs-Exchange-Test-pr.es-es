---
title: 'Escenarios de espacios de nombres distintos: Exchange 2013 Help'
TOCTitle: Escenarios de espacios de nombres distintos
ms:assetid: 90101d49-6f45-44be-8a93-eeb2c8283e3b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb676377(v=EXCHG.150)
ms:contentKeyID: 49895776
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Escenarios de espacios de nombres distintos

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

En este tema, se proporciona información acerca del concepto de espacios de nombres distintos y los escenarios en los que se admite la implementación de Microsoft Exchange 2013 en un dominio con un espacio de nombres distinto.

**Contenido**

Nombres de dominios DNS y NetBIOS

Espacios de nombres distintos

Exchange 2013 y espacios de nombres distintos

Permitir a los servidores de Exchange 2013 tener acceso a los controladores de dominio que son distintos

Ver la información relacionada con los nombres de DNS y NetBIOS de un equipo que ejecuta Windows Server 2008

## Nombres de dominios DNS y NetBIOS

En primer lugar, se brindan algunos antecedentes. Cada equipo con conexión a Internet tiene un nombre de Sistema de nombres de dominio (DNS). También se conoce como *nombre del equipo* o *nombre de host*. Todos los equipos que ejecutan el sistema operativo Windows con funcionalidades de red también tienen un nombre NetBIOS.

Un equipo que ejecuta Windows en un dominio de Active Directory tiene un nombre de dominio DNS y un nombre de dominio NetBIOS tal como sigue:

  - **Nombre de dominio DNS** El nombre de dominio consta de uno o más subdominios separados por un punto (**.**) y termina en un nombre de dominio de nivel superior. Por ejemplo, en el nombre de dominio DNS corp.contoso.com, los subdominios son corp y contoso, y el nombre de dominio de nivel superior es com.

  - **Nombre de dominio NetBIOS**   Normalmente, el nombre de dominio NetBIOS es el subdominio del nombre de dominio DNS. Por ejemplo, si el nombre de dominio es contoso.com, el nombre de dominio NetBIOS es contoso. Si el nombre de dominio DNS es corp.contoso.com, el nombre de dominio NetBIOS es corp.


> [!NOTE]
> Para obtener información acerca de DNS y NetBIOS para equipos que ejecutan Windows Server 2008, consulte Ver la información relacionada con los nombres de DNS y NetBIOS de un equipo que ejecuta Windows Server 2008.



Un equipo de un dominio Active Directory también tiene un sufijo DNS principal y puede tener sufijos DNS adicionales. De forma predeterminada, el sufijo DNS principal es igual al nombre de dominio DNS. Para obtener información detallada acerca de cómo cambiar el sufijo DNS principal, consulte los procedimientos mencionados más adelante en este tema.

El nombre de dominio DNS y el nombre de dominio NetBIOS de un dominio Active Directory se definen al configurar el primer controlador del dominio. Para obtener más información acerca de cómo configurar los controladores de dominio, consulte [Roles del controlador de dominio](https://go.microsoft.com/fwlink/p/?linkid=268367) e [Información general de Servicios de dominio de Active Directory](https://go.microsoft.com/fwlink/p/?linkid=268366).

## Espacios de nombres distintos

En la mayoría de las topologías de dominio, el sufijo DNS principal de los equipos del dominio es el mismo que el nombre de dominio DNS.

En algunos casos, puede que necesite que estos espacios de nombres sean diferentes. Esto se denomina un *espacio de nombres distinto*. Por ejemplo, una fusión o adquisición puede ocasionar que tenga una topología con un espacio de nombres distinto. Además, si la administración de DNS de la empresa está dividida entre administradores de Active Directory y administradores de redes, puede que necesite una topología con un espacio de nombres distintos.

Un escenario de espacio de nombres distinto es aquél en que el sufijo DNS principal de un equipo no coincide con el sufijo del nombre de dominio DNS donde reside el equipo. Al equipo cuyo sufijo DNS principal no coincide se le denomina *distinto*. Otro escenario de espacio de nombres distinto se da cuando el nombre de dominio NetBIOS de un controlador de dominios no coincide con el nombre de dominio DNS.

## Exchange 2013 y espacios de nombres distintos

Exchange 2013 admite los tres casos siguientes para implementar Exchange en un dominio con un espacio de nombre distinto:

  - **El sufijo DNS principal y el nombre de dominio DNS son diferentes**   El sufijo DNS principal del controlador del dominio no es el mismo que el nombre del dominio DNS. Los equipos miembros del dominio pueden ser distintos o no distintos.

  - **El equipo miembro es diferente**   Un equipo miembro de un dominio de Active Directory es distinto, aunque el controlador del dominio no lo sea.

  - **El nombre de NetBIOS del controlador del dominio es diferente del subdominio del nombre de dominio de su DNS**   El nombre de dominio NetBIOS del controlador del dominio no es el mismo que el subdominio del nombre de dominio DNS del mismo controlador.

Estos escenarios se detallan en las secciones siguientes.


> [!NOTE]
> Es compatible con la ejecución de Exchange&nbsp;2013&nbsp;en los casos de espacio de nombres distintos descritos en este tema. No obstante, si conoce algún caso de espacio de nombres distinto que no se ajuste a ninguno de los casos descritos en este tema, deberá trabajar con los Servicios de Microsoft para implementar Exchange&nbsp;2013. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=94845">Servicios de Microsoft</A>.



## Caso: El sufijo DNS principal y el nombre de dominio DNS son diferentes

En este escenario, el sufijo DNS principal del controlador de dominio no es el mismo que el nombre de dominio DNS. El controlador del dominio es distinto. Los equipos miembros del dominio, incluidos los servidores Exchange y los equipos cliente de Microsoft Outlook, pueden tener un sufijo DNS principal que coincida con el sufijo DNS principal del controlador de dominio o con el nombre de dominio DNS.

## Caso: El equipo miembro es distinto

En este escenario, el sufijo DNS principal de un equipo miembro en el que está instalado Exchange 2013 no es el mismo que el nombre de dominio DNS, aunque el sufijo DNS principal del controlador de dominio sea el mismo que el nombre de dominio DNS. En este escenario, se cuenta con un controlador de dominio que no es distinto y un equipo miembro que sí lo es. Los equipos miembros que ejecutan Outlook pueden tener un sufijo DNS principal que coincida con el sufijo DNS principal del servidor de Exchange distinto o con el nombre de dominio DNS.

## Caso: El nombre NetBIOS del controlador del dominio es diferente al subdominio del nombre de dominio DNS

En este escenario, el nombre de dominio NetBIOS del controlador de dominio no es el mismo que el nombre de dominio DNS de dicho controlador de dominio.

**El nombre de dominio NetBIOS no coincide con el nombre de dominio DNS**

![El nombre de dominio NetBIOS no coincide con el nombre de dominio DNS](images/Bb676377.1ee18cb6-0296-4875-b572-0ddf33f65f7c(EXCHG.150).gif "El nombre de dominio NetBIOS no coincide con el nombre de dominio DNS")

## Permitir a los servidores de Exchange 2013 tener acceso a los controladores de dominio que son distintos

Para permitir que los servidores de Exchange 2013 tengan acceso a controladores de dominio que son distintos, debe modificar el atributo **msDS-AllowedDNSSuffixes**Active Directory en el contenedor del objeto de dominio. Debe agregar los dos sufijos DNS al atributo. Para obtener instrucciones detalladas acerca de cómo modificar el atributo, consulte [El sufijo principal DNS del equipo no coincide con el FQDN del dominio donde reside](https://go.microsoft.com/fwlink/p/?linkid=98848).

Además, para asegurarse de que la lista de búsqueda de sufijos DNS contiene todos los espacios de nombres DNS implementados en la organización, debe configurarla para cada equipo del dominio que sea distinto. La lista de espacios de nombres no debe incluir únicamente el sufijo DNS principal del controlador de dominio y el nombre de dominio DNS, sino también cualquier espacio de nombres adicional de otros servidores con los que Exchange pueda interoperar (como servidores de supervisión o servidores de aplicaciones de terceros). Esto se puede hacer mediante la configuración de una directiva de grupo para el dominio. Para obtener más información acerca de la directiva de grupo, consulte los siguientes temas:

  - [Preguntas más frecuentes sobre directivas de grupos](https://go.microsoft.com/fwlink/p/?linkid=100128)

  - [Nuevas directivas de grupos para DNS en Windows Server 2003](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=294785)

  - [Directiva de grupo](https://go.microsoft.com/fwlink/p/?linkid=268043)

Para obtener instrucciones detalladas acerca de cómo configurar la directiva de grupo de la lista de búsqueda de sufijos DNS, consulte [Configurar la lista de búsqueda de sufijos DNS para un espacio de nombres distintos](configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md).

## Ver la información relacionada con los nombres de DNS y NetBIOS de un equipo que ejecuta Windows Server 2008

1.  Haga clic en **Inicio** y, a continuación, haga clic con el botón secundario en **Equipo** y elija **Propiedades**.

2.  En **Sistema**, el nombre de host DNS y el sufijo DNS principal se muestran en **Configuración de nombre, dominio y grupo de trabajo del equipo**, junto a **Nombre completo de equipo**. El nombre de dominio DNS se muestra junto a **Dominio**.

3.  Haga clic en **Cambiar configuración**.

4.  En **Propiedades del sistema**, en la ficha **Nombre de equipo**, haga clic en **Cambiar**.

5.  En **Cambios en el dominio o en el nombre del equipo**, haga clic en **Más**. El sufijo DNS principal se muestra en **Sufijo DNS principal de este equipo**. El nombre NetBIOS del equipo se muestra en **Nombre NetBIOS del equipo**.
    
    Para cambiar el sufijo DNS principal, escriba el nuevo sufijo DNS principal en **Sufijo DNS principal de este equipo** y, a continuación, haga clic en **Aceptar**.

6.  Desde una ventana del símbolo del sistema, escriba **set**. La variable USERDNSDOMAIN muestra el nombre de dominio DNS. La variable USERDOMAIN muestra el nombre de dominio NetBIOS.

