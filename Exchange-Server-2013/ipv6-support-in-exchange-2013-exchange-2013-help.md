---
title: 'Compatibilidad con IPv6 en Exchange 2013: Exchange 2013 Help'
TOCTitle: Compatibilidad con IPv6 en Exchange 2013
ms:assetid: 33543023-eb9a-4102-b990-84a818a52814
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg144561(v=EXCHG.150)
ms:contentKeyID: 48267969
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Compatibilidad con IPv6 en Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

El Protocolo de Internet versión 6 (IPv6) es la versión del Protocolo de Internet (IP) más reciente. IPv6 está diseñado para corregir muchas de las deficiencias de IPv4, que era la versión anterior de IP.

En Microsoft Exchange Server 2013, IPv6 solo se admite cuando también está instalado y habilitado IPv4. Si Exchange 2013 está implementado en esta configuración y la red admite IPv4 e IPv6, todos los servidores de Exchange pueden enviar y recibir datos de dispositivos, servidores y clientes que usen direcciones IPv6.

En este tema, se trata el direccionamiento IPv6 en Exchange 2013. Para obtener información adicional sobre IPv6, consulte [IPv6](https://go.microsoft.com/fwlink/p/?linkid=92582) .

**Contenido**

Compatibilidad con IPv6 en componentes de Exchange 2013

Habilitar o deshabilitar protocolos en el sistema operativo

Conceptos básicos de dirección IPv6

## Compatibilidad con IPv6 en componentes de Exchange 2013

En la siguiente tabla, se describen los componentes de Exchange 2013 que se ven afectados por IPv6.

### Características de Exchange 2013 e IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>IPv6 admitido</th>
<th>Comments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lista de direcciones IP permitidas y lista de direcciones IP bloqueadas en el agente de filtrado de conexión</p></td>
<td><p>Sí</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Proveedores de listas de direcciones IP permitidas y proveedores de listas de direcciones IP bloqueadas en el agente de filtrado de conexión.</p></td>
<td><p>No</p></td>
<td><p>Actualmente, no existe ningún protocolo estándar aceptado globalmente por el sector para buscar direcciones IPv6. La mayoría de los proveedores de la lista de direcciones IP bloqueadas no admiten direcciones IPv6. Si permite conexiones anónimas de direcciones IPv6 desconocidas en un conector de recepción, incrementará el riesgo de que los emisores de correo no deseado omitan los proveedores de la lista de direcciones IP bloqueadas y consigan entregar correo no deseado a su organización.</p></td>
</tr>
<tr class="odd">
<td><p>Reputación del remitente en el agente de análisis de protocolos</p></td>
<td><p>No</p></td>
<td><p>El agente de análisis de protocolo no computa el nivel de reputación del remitente (SRL) de los mensajes que se originan de remitentes IPv6. Para obtener más información acerca de la reputación de remitente, consulte <a href="sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md">Reputación del remitente y agente de análisis de protocolo</a>.</p></td>
</tr>
<tr class="even">
<td><p>Id. del remitente</p></td>
<td><p>Sí</p></td>
<td><p>Para obtener más información, consulte <a href="sender-id-exchange-2013-help.md">Id. del remitente</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Conectores de recepción</p></td>
<td><p>Sí</p></td>
<td><p>Las direcciones IPv6 se aceptan para los siguientes componentes:</p>
<ul>
<li><p>Enlaces de dirección IP local</p></li>
<li><p>Direcciones IP remotas</p></li>
<li><p>Intervalos de direcciones IP</p></li>
</ul>
<p>Le recomendamos que no configure conectores de recepción para que acepten conexiones anónimas de direcciones IPv6 desconocidas. Si su organización debe recibir correo de remitentes que usan direcciones IPv6, cree un conector de recepción especial que restrinja las direcciones IP remotas a las direcciones IPv6 específicas que usan dichos remitentes.</p>
<p>Para obtener más información, consulte <a href="receive-connectors-exchange-2013-help.md">Conectores de recepción</a>.</p></td>
</tr>
<tr class="even">
<td><p>Conectores de envío</p></td>
<td><p>Sí</p></td>
<td><p>Las direcciones IPv6 se aceptan para los siguientes componentes:</p>
<ul>
<li><p>Direcciones IP de host inteligente</p></li>
<li><p>El parámetro <em>SourceIPAddress</em> para conectores de envío configurados en servidores de transporte perimetral</p></li>
</ul>

> [!NOTE]
> Si desea especificar una dirección IPv6 para el parámetro <EM>SourceIPAddress</EM>, asegúrese de que los registros DNS AAAA y Mail eXchange (MX) estén configurados correctamente. Esto ayuda a garantizar la entrega de mensajes si un servidor de mensajería remoto intenta cualquier prueba de búsqueda inversa en la dirección IPv6 especificada.


<p>Para obtener más información, consulte <a href="send-connectors-exchange-2013-help.md">Conectores de envío</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Límites de velocidad de mensajes entrantes</p></td>
<td><p>Parcial</p></td>
<td><p>Los límites de velocidad de mensajes entrantes que pueden establecerse en un conector de recepción, como el parámetro <em>MaxInboundConnectionPercentagePerSource</em>, el parámetro <em>MaxInboundConnectionPerSource</em> y el parámetro <em>TarpitInterval</em>, sólo son válidos para una dirección IPv6 global. Las direcciones IPv6 locales de vínculo y las direcciones IPv6 locales de sitio no están afectadas por los límites de velocidad de mensaje entrante que se especifiquen.</p></td>
</tr>
<tr class="even">
<td><p>Mensajería unificada</p></td>
<td><p>Sí</p></td>
<td><p>Para obtener más información, consulte <a href="ipv6-support-in-unified-messaging-exchange-2013-help.md">Compatibilidad con IPv6 en mensajería unificada</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Miembro de un grupo de disponibilidad de base de datos (DAG)</p></td>
<td><p>Sí</p></td>
<td><p>Windows Server y el servicio de clúster admiten las direcciones IPv6 estáticas. Sin embargo, el uso de direcciones IPv6 estáticas va en contra de los procedimientos recomendados. Exchange 2013 no admite la configuración de direcciones IPv6 estáticas durante la instalación.</p>
<p>Los clústeres de conmutación por error admiten el Intra-site Automatic Tunneling Addressing Protocol (ISATAP). Sólo admiten direcciones IPv6 que permitan el registro dinámico en DNS. Las direcciones locales de vínculo no pueden usarse en un clúster.</p>
<p>Para más información sobre los requisitos de red de los DAG, vea la sección &quot;Requisitos de red&quot; de <a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">Planificación de alta disponibilidad y resistencia de sitios</a>.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Habilitar o deshabilitar protocolos en el sistema operativo

Los servidores de Exchange 2013 son totalmente compatibles con redes IPv6. Por lo tanto, aunque no use IPv6, no tiene que deshabilitar IPv6 en los servidores de Exchange.

La compatibilidad de IPv6 en Exchange 2013 exige que IPv4 esté instalado y habilitado en todos los servidores de Exchange 2013. El IPv4 no se puede desinstalar desde los servidores de Exchange 2013.

Para obtener más información sobre la compatibilidad de IPv6 en Microsoft Windows, consulte [IPv6 para Microsoft Windows: Preguntas más frecuentes](https://go.microsoft.com/fwlink/p/?linkid=147465) .

Volver al principio

## Conceptos básicos de dirección IPv6

Una dirección IPv6 tiene una longitud de 128 bits. La dirección se describe por medio de notación hexadecimal con dos puntos. La notación hexadecimal con dos puntos describe la dirección de 128 bits mediante el uso de ocho números hexadecimales de 16 bits y 4 dígitos que están separados por el carácter de los dos puntos (:). Un ejemplo de una dirección IPv6 en notación hexadecimal con dos puntos es 2001:0DB8:0000:0000:02AA:00FF:C0A8:640A.

Una dirección IPv6 se puede expresar con los siguientes métodos:

  - **Suprimir ceros iniciales**   Se pueden omitir los ceros iniciales de cualquier número hexadecimal de 4 dígitos de una dirección IPv6.

  - **Compresión de dos caracteres de dos puntos**   Se pueden usar dos caracteres de dos puntos (::) para representar dígitos hexadecimales contiguos de 16 bits que sólo contienen ceros. Estos dígitos de todo ceros pueden encontrarse al principio, en mitad o al final de la dirección IPv6. Sólo se puede usar la compresión de dos caracteres de dos puntos una vez en cada dirección IPv6.

  - **Notación decimal con puntos al final**   Puede expresar los últimos 32 bits del final de una dirección IPv6 en notación decimal con puntos separando los dígitos de 8 bits con un punto (.). La notación decimal con puntos al final se usa con frecuencia en direcciones compatibles con IPv4.

En la siguiente tabla, se proporcionan ejemplos de la notación de dirección IPv6 y la sintaxis de la dirección IPv6 equivalente.

### Notación y sintaxis de la dirección IPv6

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Notación de dirección IPv6</th>
<th>Sintaxis de la dirección IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dirección IPv6 completa</p></td>
<td><p>2001:0DB8:0000:0000:02AA:00FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Dirección IPv6 que usa supresión de ceros iniciales</p></td>
<td><p>2001:DB8:0:0:2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="odd">
<td><p>Dirección IPv6 que usa compresión de dos caracteres de dos puntos</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Dirección IPv6 que usa compresión decimal con puntos al final</p></td>
<td><p>2001:DB8::2AA:FF:192.168.100.10</p></td>
</tr>
</tbody>
</table>


Las direcciones IPv6 se clasifican en los siguientes tipos:

  - **Dirección de unidifusión**   Se envía un paquete a una interfaz.

  - **Dirección de multidifusión**   Se envía un paquete a múltiples interfaces.

  - **Dirección de difusión por proximidad (anycast)**   Se envía un paquete a la más próxima de un conjunto de múltiples interfaces. La distancia entre interfaces se define por el costo de enrutamiento.

Las direcciones de unidifusión IPv6 tienen los siguientes alcances posibles:

  - **Local de vínculo**   El alcance de la dirección IPv6 es la subred local. Las direcciones IPv6 locales de vínculo pueden compararse con las direcciones IPv4 locales de vínculo que se usan en Direccionamiento automático de IP privada (APIPA).

  - **Local de sitio**   El alcance de la dirección IPv6 es la organización local. Las direcciones locales de sitio fueron desaprobadas por la RFC 3879 y sustituidas por direcciones locales únicas según la definición de RFC 4193. Las direcciones IPv6 locales únicas son comparables a las direcciones IP privadas de IPv4.

  - **Global**   El alcance de la dirección IPv6 es todo el mundo. Las direcciones IPv6 globales son comparables a las direcciones IP públicas de IPv4.

En la tabla siguiente se ofrece una comparación de los elementos de IPv4 y los elementos de IPv6.

### Comparación de los elementos de IPv4 e IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>IPv4</th>
<th>IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dirección IP privada</p></td>
<td><p>10.0.0.0/8</p>
<p>172.16.0.0/12</p>
<p>192.168.0.0/16</p></td>
<td><p>FD00::/8</p></td>
</tr>
<tr class="even">
<td><p>Dirección local de vínculo</p></td>
<td><p>169.254.0.0/16</p></td>
<td><p>FE80::/64</p></td>
</tr>
<tr class="odd">
<td><p>Dirección de bucle invertido</p></td>
<td><p>127.0.0.1</p></td>
<td><p>::1</p></td>
</tr>
<tr class="even">
<td><p>Dirección sin especificar</p></td>
<td><p>0.0.0.0</p></td>
<td><p>::</p></td>
</tr>
<tr class="odd">
<td><p>Resolución de dirección</p></td>
<td><p>Protocolo de resolución de dirección (ARP)</p></td>
<td><p>Detección de vecinos (ND)</p></td>
</tr>
<tr class="even">
<td><p>Resolución de nombre de host del Sistema de nombre de dominio (DNS)</p></td>
<td><p>Registro de dirección (registro A)</p></td>
<td><p>Registro AAAA o registro A6</p></td>
</tr>
</tbody>
</table>


Para obtener más información sobre el direccionamiento de IPv6, consulte [Tipos de dirección IPv6](https://go.microsoft.com/fwlink/p/?linkid=98357) .

## Formatos de entrada de la dirección IPv6 admitidos

Los siguientes tipos de formatos de entrada de dirección IPv6 se admiten en Exchange 2013:

  - Una única dirección IPv6

  - Un intervalo de direcciones IPv6

  - Una dirección IPv6 junto con una máscara de subred

  - Una dirección IPv6 junto con una máscara de subred que usa notación de Enrutamiento de interdominios sin clases (CIDR)

En la siguiente tabla, se ven ejemplos de los formatos de entrada de dirección IPv6 aceptables en Exchange 2013.

### Ejemplos de dirección IPv6

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo</th>
<th>Ejemplo de una dirección IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dirección única</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>Intervalo de direcciones</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A-2001:DB8::2AA:FF:C0A8:6414</p></td>
</tr>
<tr class="odd">
<td><p>Dirección junto con máscara de subred</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A(FFFF:FFFF:FFFF:FFFF::)</p></td>
</tr>
<tr class="even">
<td><p>Dirección junto con máscara de subred que usa notación CIDR</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A/64</p></td>
</tr>
</tbody>
</table>


En Exchange 2013, se admiten los siguientes formatos de entrada:

  - Supresión de ceros iniciales

  - Compresión de dos caracteres de dos puntos

  - Notación decimal con punto al final

Volver al principio

