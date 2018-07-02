---
title: 'Requisitos del sistema para Exchange 2013: Exchange 2013 Help'
TOCTitle: Requisitos del sistema para Exchange 2013
ms:assetid: 1e80857c-b870-4a6d-a0f4-ff7b3a7be037
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996719(v=EXCHG.150)
ms:contentKeyID: 48267875
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Requisitos del sistema para Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Obtenga información sobre los requisitos de Exchange 2013 que debe conocer antes de instalar Exchange de 2013. Por ejemplo, podrá conocer los requisitos de hardware, red y sistema operativo.

Antes de instalar Microsoft Exchange Server 2013, se recomienda consultar este tema para garantizar que la red, el hardware, el software, los clientes y los demás elementos cumplan los requisitos de Exchange 2013. Además, asegúrese de comprender los escenarios de coexistencia admitidos para Exchange 2013 y versiones anteriores de Exchange.

## Escenarios de coexistencia compatibles

En la siguiente tabla, se enumeran los casos en los que se admite la coexistencia de Exchange 2013 y versiones anteriores de Exchange.

### Coexistencia de Exchange 2013 y versiones anteriores de Exchange Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versión de Exchange</th>
<th>Coexistencia de organización de Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 y versiones anteriores</p></td>
<td><p>No se admite</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>Compatible con las siguientes versiones mínimas de Exchange:</p>
<ul>
<li><p>1Paquete acumulativo de actualizaciones 10 para Exchange 2007 Service Pack 3 (SP3) en todos los servidores Exchange 2007 de la organización, incluidos los servidores de transporte perimetral.</p></li>
<li><p>Actualización acumulativa 2 (CU2) de Exchange 2013 o posterior en todos los servidores Exchange 2013 de la organización.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Compatible con las siguientes versiones mínimas de Exchange:</p>
<ul>
<li><p>2 Exchange 2010 SP3 en todos los servidores Exchange 2010 de la organización, incluidos los servidores de transporte perimetral.</p></li>
<li><p>CU2 de Exchange 2013 o posterior en todos los servidores Exchange 2013 de la organización.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Organización mixta de Exchange 2010 y Exchange 2007</p></td>
<td><p>Compatible con las siguientes versiones mínimas de Exchange:</p>
<ul>
<li><p>1Paquete acumulativo de actualizaciones 10 para Exchange 2007 SP3 en todos los servidores Exchange 2007 de la organización, incluidos los servidores de transporte perimetral.</p></li>
<li><p>2 Exchange 2010 SP3 en todos los servidores Exchange 2010 de la organización, incluidos los servidores de transporte perimetral.</p></li>
<li><p>CU2 de Exchange 2013 o posterior en todos los servidores Exchange 2013 de la organización.</p></li>
</ul></td>
</tr>
</tbody>
</table>


1 Si quiere crear una suscripción de EdgeSync entre un servidor de transporte de concentradores de Exchange 2007 y un servidor de transporte perimetral de Exchange 2013 SP1, deberá instalar el paquete acumulativo de actualizaciones 13 de Exchange 2007 SP3 o posterior en el servidor de transporte de concentradores de Exchange 2007.

2 Si quiere crear una suscripción de EdgeSync entre un servidor de transporte de concentradores de Exchange 2010 y un servidor de transporte perimetral de Exchange 2013 SP1, deberá instalar el paquete acumulativo de actualizaciones 5 de Exchange 2010 SP3 o posterior en el servidor de transporte de concentradores de Exchange 2010.

## Escenarios de implementación híbrida compatibles

Exchange 2013 admite implementaciones híbridas con inquilinos de Office 365 que se actualizaron a la última versión de Office 365. Para más información sobre implementaciones híbridas específicas, vea [Requisitos previos de implementación híbrida](https://technet.microsoft.com/es-es/library/hh534377\(v=exchg.150\)).

## Servidores de directorios y redes

A continuación, se indican los requisitos de red y los servidores de directorio para su organización de Exchange 2013.

**Requisitos de servidor de red y directorio para Exchange 2013**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Maestro de esquema</p></td>
<td><p>De forma predeterminada, el maestro de esquema se ejecuta en el primer controlador de dominio de Active Directory instalado en un bosque. El maestro de esquema debe ejecutar uno de los siguientes componentes:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard o Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard o Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM o posterior</p></li>
<li><p>Windows Server 2008 Standard o Enterprise (32 bits o 64 bits)</p></li>
<li><p>Windows Server 2008 Datacenter RTM o posterior</p></li>
<li><p>Windows Server 2003 Standard Edition con Service Pack 2 (SP2) o posterior (32 bits o 64 bits)</p></li>
<li><p>Windows Server 2003 Enterprise Edition con SP2 o posterior (32 bits o 64 bits)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Servidor de catálogo global</p></td>
<td><p>En cada sitio de Active Directory donde tiene pensado instalar Exchange 2013, debe tener por lo menos un servidor de catálogo global en ejecución en uno de los siguientes sistemas:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard o Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard o Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM o posterior</p></li>
<li><p>Windows Server 2008 Standard o Enterprise (32 bits o 64 bits)</p></li>
<li><p>Windows Server 2008 Datacenter RTM o posterior</p></li>
<li><p>Windows Server 2003 Standard Edition con Service Pack 2 (SP2) o posterior (32 bits o 64 bits)</p></li>
<li><p>Windows Server 2003 Enterprise Edition con SP2 o posterior (32 bits o 64 bits)</p></li>
</ul>
<p>Para más información sobre los servidores de catálogo global, vea <a href="http://go.microsoft.com/fwlink/p/?linkid=178996">¿qué es el catálogo global?</a></p></td>
</tr>
<tr class="odd">
<td><p>Controlador de dominio</p></td>
<td><p>En cada sitio de Active Directory donde tiene pensado instalar Exchange 2013, debe tener por lo menos un controlador de dominio grabable en ejecución en uno de los siguientes sistemas:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard o Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard o Enterprise SP1 o posterior</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM o posterior</p></li>
<li><p>Windows Server 2008 Standard o Enterprise SP1 o posterior (32 bits o 64 bits)</p></li>
<li><p>Windows Server 2008 Datacenter RTM o posterior</p></li>
<li><p>Windows Server 2003 Standard Edition con Service Pack 2 (SP2) o posterior (32 bits o 64 bits)</p></li>
<li><p>Windows Server 2003 Enterprise Edition con SP2 o posterior (32 bits o 64 bits)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Bosque de Active Directory</p></td>
<td><p>Active Directory debe estar en modo de funcionalidad de bosque de Windows Server 2003 o posterior2.</p></td>
</tr>
<tr class="odd">
<td><p>Compatibilidad del espacio de nombres de DNS</p></td>
<td><p>Exchange 2013 es compatible con los siguientes espacios de nombres de sistema de nombre de dominio (DNS):</p>
<ul>
<li><p>Contiguos</p></li>
<li><p>No contiguos</p></li>
<li><p>Dominios de etiqueta única</p></li>
<li><p>Separados</p></li>
</ul>
<p>Para más información sobre los espacios de nombre de DNS compatibles con Exchange, vea el artículo de Microsoft Knowledge Base 2269838, <a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2269838">Compatibilidad de Microsoft Exchange con dominios de etiqueta única, espacios de nombres disjuntos y espacios de nombres no contiguos</a>.</p></td>
</tr>
<tr class="even">
<td><p>Compatibilidad con IPv6</p></td>
<td><p>En Exchange 2013, IPv6 solo se admite cuando también está instalado y habilitado IPv4. Si Exchange 2013 está implementado en esta configuración y la red admite IPv4 e IPv6, todos los servidores Exchange pueden enviar y recibir datos de dispositivos, servidores y clientes que usen direcciones IPv6. Para obtener más información, vea <a href="ipv6-support-in-exchange-2013-exchange-2013-help.md">Compatibilidad con IPv6 en Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


1Windows Server 2012R2 es compatible solo con Exchange 2013 SP1 o posterior.

2Windows Server 2012El modo de funcionalidad de bosque de R2 es compatible solo con Exchange 2013 SP1 o posterior.

## Arquitectura de servidor de directorios

El uso de controladores de dominio Active Directory de 64 bits aumenta el rendimiento del servicio del directorio de Exchange 2013.


> [!NOTE]
> En entornos multidominio, en controladores de dominio de Windows Server 2008 que tienen la configuración regional del idioma Active Directory establecida en japonés, es posible que sus servidores no reciban ciertos atributos almacenados en un objeto durante una replicación entrante. Para obtener más información, vea el artículo 949189 de Microsoft Knowledge Base, <A href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=949189">Es posible que un controlador de dominio de Windows Server 2008 cuya configuración regional de idioma está establecida en japonés no aplique las actualizaciones a los atributos de un objeto durante una replicación entrante</A>.



## Instalación de Exchange 2013 en servidores de directorios

Por motivos de seguridad y rendimiento, se recomienda instalar Exchange 2013 solamente en servidores miembro y no en servidores de directorio de Active Directory. Sin embargo, no puede ejecutar DCPromo en un equipo con Exchange 2013. Una vez instalado Exchange 2013, no se permite cambiar su rol de servidor miembro a servidor de directorio o viceversa.

## Hardware

Los requisitos de hardware recomendados para servidores de Exchange 2013 varían en función de diferentes factores, incluidos los roles de servidor instalados y la carga prevista de los servidores.

Para obtener información detallada sobre cómo ajustar el tamaño y configurar correctamente la implementación, vea [Recomendaciones de configuración y dimensionamiento de Exchange 2013](exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md).

Para más información sobre cómo implementar Exchange en un entorno virtualizado, vea [Virtualización de Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md).

**Requisitos de hardware para Exchange 2013**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Requisito</th>
<th>Notas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Procesador</p></td>
<td><ul>
<li><p>Equipo basado en arquitectura x64 con procesador Intel compatible con la arquitectura Intel 64 (anteriormente denominada Intel EM64T)</p></li>
<li><p>Procesador AMD compatible con la plataforma AMD64</p></li>
<li><p>Los procesadores Intel Itanium IA64 no son compatibles</p></li>
</ul></td>
<td><p>Vea la sección &quot;Sistema operativo&quot; más adelante en este artículo para conocer los sistemas operativos compatibles.</p></td>
</tr>
<tr class="even">
<td><p>Memoria</p></td>
<td><p>Varía según los roles de Exchange instalados:</p>
<ul>
<li><p><strong>Buzón de correo</strong>   8 GB como mínimo</p></li>
<li><p><strong>Acceso de clientes</strong>   4 GB como mínimo</p></li>
<li><p><strong>Buzones de correo y acceso de clientes combinados</strong>   8 GB como mínimo</p></li>
<li><p><strong>Transporte perimetral</strong>   4 GB como mínimo</p></li>
</ul></td>
<td><p>Ninguno.</p></td>
</tr>
<tr class="odd">
<td><p>Tamaño del archivo de paginación</p></td>
<td><p>El tamaño mínimo y máximo del archivo de paginación se debe establecer en la memoria RAM física más 10 MB, hasta un tamaño máximo de 32778 MB si se usan más de 32 GB de RAM.</p></td>
<td><p>Para obtener recomendaciones detalladas del archivo de paginación, vea la sección &quot;Archivo de paginación&quot; en <a href="exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md">Recomendaciones de configuración y dimensionamiento de Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Espacio en disco</p></td>
<td><ul>
<li><p>Al menos 30 GB en la unidad en la que se va a instalar Exchange</p></li>
<li><p>500 MB adicionales de espacio de disco disponible para cada paquete de idiomas de mensajería unificada (UM) que desee instalar</p></li>
<li><p>200 MB de espacio de disco disponible en la unidad de sistema</p></li>
<li><p>Un disco duro que almacene la base de datos de colas de mensajes activa con al menos 500 MB de espacio libre.</p></li>
</ul></td>
<td><p>Para obtener información detallada sobre las recomendaciones de almacenamiento, vea <a href="exchange-2013-storage-configuration-options-exchange-2013-help.md">Opciones de configuración de almacenamiento de Exchange 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Unidad</p></td>
<td><p>Unidad de DVD-ROM, accesible de forma local o a través de la red</p></td>
<td><p>Ninguno.</p></td>
</tr>
<tr class="even">
<td><p>Resolución de pantalla</p></td>
<td><p>1024 x 768 píxeles o superior</p></td>
<td><p>Ninguno.</p></td>
</tr>
<tr class="odd">
<td><p>Formato de archivos</p></td>
<td><p>Particiones de disco formateadas como sistemas de archivos NTFS, lo que se aplica a las siguientes particiones:</p>
<ul>
<li><p>Partición del sistema</p></li>
<li><p>Particiones que almacenan archivos binarios de Exchange o archivos generados por el registro de diagnóstico de Exchange</p></li>
</ul>
<p>Las particiones de disco que contienen los siguientes tipos de archivos se pueden formatear como ReFS:</p>
<ul>
<li><p>Particiones que contienen los archivos de registro de transacciones</p></li>
<li><p>Particiones que contienen archivos de base de datos</p></li>
<li><p>Particiones que contienen archivos de indización de contenido</p></li>
</ul></td>
<td><p>Ninguno.</p></td>
</tr>
</tbody>
</table>


## Sistema operativo

En la siguiente tabla se enumeran los sistemas operativos compatibles para Exchange 2013.


> [!IMPORTANT]
> No se admite la instalación de Exchange&nbsp;2013 en un equipo que se ejecute en modo Windows Server Core. El equipo debe ejecutar la instalación completa de Windows Server. Si desea instalar Exchange&nbsp;2013 en un equipo que se ejecute en modo Windows Server Core, debe convertir el servidor a una instalación completa de Windows Server mediante una de las opciones siguientes: 
> <UL>
> <LI>
> <P><STRONG>Windows Server 2008 R2</STRONG>&nbsp;&nbsp;&nbsp;Reinstale Windows Server y seleccione la opción <STRONG>Instalación completa</STRONG>.</P>
> <LI>
> <P><STRONG>Windows Server 2012 R2</STRONG> o <STRONG>Windows Server 2012</STRONG>&nbsp;&nbsp;&nbsp;Convierta su servidor en modo Windows Server Core en una instalación completa al ejecutar el siguiente comando.</P><PRE><CODE>Install-WindowsFeature Server-Gui-Mgmt-Infra, Server-Gui-Shell -Restart</CODE></PRE></LI></UL>



**Sistemas operativos compatibles para Exchange 2013**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox, Client Access, and Edge Transport server roles</p></td>
<td><p>One of the following:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard or Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard with Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Enterprise with Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM or later</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Management tools</p></td>
<td><p>One of the following:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard o Datacenter1</p></li>
<li><p>Windows Server 2012 Standard or Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard with SP1</p></li>
<li><p>Windows Server 2008 R2 Enterprise with SP1</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM or later</p></li>
<li><p>Edición de 64 bits de Windows 8.12</p></li>
<li><p>64-bit edition of Windows 8</p></li>
<li><p>64-bit edition of Windows 7 with Service Pack 1</p></li>
</ul></td>
</tr>
</tbody>
</table>


1 Windows Server 2012 R2 solo es compatible con Exchange 2013 SP1 o posterior.

2 Windows 8.1 solo es compatible con Exchange 2013 SP1 o posterior.

**Versiones de Windows Management Framework compatibles con Exchange 2013**

Exchange 2013 solo admite la versión de Windows Management Framework que está integrado en la versión de Windows en la que está instalando Exchange. No instale versiones de Windows Management Framework que están disponibles como descargas independientes en servidores que ejecutan Exchange.

## .NET Framework

Se recomienda encarecidamente usar la versión más reciente de .NET Framework que es compatible con la versión de Exchange que está instalando.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Versión de Exchange</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU16</p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU15</p></td>
<td><p> X</p></td>
<td><p>X1,2 </p></td>
<td><p> X</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2013 CU13 y CU14</p></td>
<td> </td>
<td><p>X1,2 </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


1 .NET Framework 4.6.1 requiere revisiones posteriores al lanzamiento si quiere instalarlo en un servidor que ejecute Exchange 2013 CU13. Para obtener más información, vea [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2Si está actualizando a Exchange 2013 CU13, CU14 o CU15 desde Exchange 2013 CU12 o versiones anteriores, se recomienda encarecidamente que instale Exchange 2013 CU13 antes de .NET Framework 4.6.1 y sus revisiones posteriores al lanzamiento.

## Clientes compatibles

Exchange 2013 admite las siguientes versiones de Outlook y Entourage para Mac:

  - Outlook 2016

  - Outlook 2013

  - Outlook 2010

  - Outlook 2007

  - Entourage 2008 para Mac, Web Services Edition

  - Outlook para Mac para Office 365

  - Outlook para Mac 2011

Para ver una lista de versiones de Outlook compatibles con Exchange, consulte [Actualizaciones de Outlook](https://go.microsoft.com/fwlink/p/?linkid=513459).


> [!IMPORTANT]
> Le recomendamos encarecidamente que instale los últimos Service Pack y actualizaciones disponibles para que los usuarios reciban la mejor experiencia posible al conectarse a Exchange.



No se admiten los clientes de Outlook con versiones anteriores a Outlook 2007. Los clientes de correo electrónico en sistemas operativos Mac que requieren DAV, como Entourage 2008 para Mac RTM y Entourage 2004, no son compatibles.

Outlook Web App es compatible con varios exploradores en una variedad de sistemas operativos y dispositivos. Para obtener información, consulte [Novedades de Outlook Web App en Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md).

