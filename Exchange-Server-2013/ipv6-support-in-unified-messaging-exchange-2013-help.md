---
title: 'Compatibilidad con IPv6 en mensajería unificada: Exchange 2013 Help'
TOCTitle: Compatibilidad con IPv6 en mensajería unificada
ms:assetid: 91242c85-ce4e-422a-954e-ab623d3d6939
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150536(v=EXCHG.150)
ms:contentKeyID: 48268419
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Compatibilidad con IPv6 en mensajería unificada

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2015-04-07_

El Protocolo de Internet versión 6 (IPv6) es la versión del Protocolo de Internet (IP) más reciente. IPv6 está diseñado para corregir muchas de las deficiencias de IPv4, que era la versión anterior de IP. En Microsoft Exchange Server 2010, IPv6 solo se admite cuando también se usa IPv4. No se admite un entorno IPv6 Exchange puro. Solo se admite el uso de direcciones IPv6 e intervalos de direcciones IP si las versiones IPv6 e IPv4 están habilitadas en el equipo que ejecuta Exchange 2010 y la red admite ambas versiones de dirección IP. Sin embargo, dado que IPv4 e IPv6 son protocolos completamente diferentes, una red IPv4 no se puede comunicar directamente con una red IPv6, y viceversa. Para gestionar este defecto, los administradores de la red deben implementar dispositivos, como los routers, que puedan guiar la información entre las redes IPv4 e IPv6. Si Exchange 2010 está implementado con IPv4 e IPv6, todos los roles del servidor (excepto la mensajería unificada (MU)) podrán enviar y recibir datos de dispositivos, servidores y clientes que usen direcciones IPv6. Con Exchange 2013, la mensajería unificada ya no es un rol de servidor por separado como los roles del servidor de transporte, el de acceso de cliente y de buzones de correo en Exchange 2007 y Exchange 2010. Los componentes relacionados con la MU y con los servicios de voz únicamente funcionan con servidores de acceso de cliente y de buzones de correo.

En Exchange 2013, debido a que la arquitectura de MU ha cambiado y ahora requiere la API administrada de comunicaciones unificadas (UCMA) v4.0 para admitir tanto IPv4 como IPv6 (así como también otras características de Exchange), tanto los servidores de acceso de cliente como los de buzones de correo que tienen componentes y servicios de mensajería unificada serán completamente compatibles con redes IPv6.

## Soporte de IPv6

Empezando por Exchange 2010 Service Pack 1 (SP1), el rol de servidor de mensajería unificada confiaba en UCMA 2.0 para procesar la señal y la voz de su protocolo de inicio de sesión subyacente (SIP). UCMA 2.0 es el componente principal para las características de voz en MU. UCMA 2.0 contiene una pila SIP, una pila de medios y motores de voz para reconocimiento automático de voz (ASR), así como sintetización de voz generada por conversión de texto a voz (TTS).

En Exchange 2010, era necesario que todos los roles de servidor ejecutaran una doble pila (IPv4 e IPv6), exceptuando el de MU (dado que requería UCMA 2.0 pero únicamente era compatible con IPv4 y no con IPv6). En Exchange 2013, la MU utiliza UCMA 4.0, que se necesita para instalar Exchange 2013 en servidores de acceso de cliente y de buzones de correo. UCMA 4.0 es necesario para admitir las nuevas características y para que sea compatible con IPv6.

A continuación aparecen algunos de los motivos por los cuales MU ahora utiliza UCMA 4.0 para admitir las nuevas características de Exchange 2013, incluido IPv6:

  - Algunas autoridades gubernamentales requieren compatibilidad con IPv6 para los productos que utilizan.

  - La MU ahora requiere una compatibilidad con dispositivos hardware como routers, puertas de enlace IP, IP PBX y controladores de borde de sesión (SBC) que guían tanto una doble pila (IPv4 e IPv6) como solo IPv6.

  - En Exchange 2013, el servicio de mensajería unificada de Microsoft se ejecuta en un servidor de buzones de correo, mientras que el servicio enrutador de llamadas de la mensajería unificada de Microsoft se ejecuta en un servidor de acceso de cliente. Los roles de servidor de buzones de correo y de acceso de cliente de Exchange 2013 requieren tanto IPv4 como IPv6.

  - Los servicios en línea permiten que los clientes se puedan conectar a su servicio tanto si es a través de IPv4 como IPv6.

  - Se está agotando el espacio de direcciones IPv4 públicas. Para Exchange Server 2013 Enterprise, esto no es realmente un problema de mensajería unificada dado que MU se comunica permanentemente con pares SIP internos que pueden implementarse con un espacio de direcciones IPv4 privadas. Sin embargo, para la mensajería unificada hospedada de Exchange, el equipo del cliente debe admitir la MU hospedada mediante IPv4 o IPv6.

Con la excepción de la MU y una pequeña parte del servidor de transporte, Exchange 2013 puede conectarse a los servidores de Exchange 2010 de una organización cuando un servidor de acceso de cliente o de buzones de correo se ejecute en modo de doble pila con IPv4 e IPv6 habilitados. Esto significa que los clientes pueden instalar Exchange 2013 en equipos que ejecutan direcciones de pila IPv4 e IPv6 configuradas. Esto permite que los clientes IPv6 y otros servidores de Exchange, incluido Exchange Server 2010, se conecten directamente a Exchange 2013.

La MU funciona en servidores de Windows que se ejecutan en modo de doble pila. Esto se debe a que los protocolos como HTTP ignoran el tipo de transporte y la mensajería unificada usa protocolos de voz por IP (VoIP), incluidos SIP/RTP/STUN/TURN/ICE), que son independientes entre ellos. Esto incluye negociación de medios (RTP/SRTP) en la cual la mensajería unificada anuncia y comunica una lista de direcciones IP a pares SIP, como puertas de enlace IP, IP PBX o SBC.

## ¿Qué significa compatibilidad con IPv6 para mensajería unificada?

Para habilitar la compatibilidad de la mensajería unificada de Exchange 2013 con IPv6, los administradores de mensajería unificada en línea y empresariales deben poder aprovechar IPv6 al conectar la mensajería unificada a dispositivos compatibles con IPv6, incluidos los dispositivos tales como routers, puertas de enlace IP, IP PBX y servidores de Office Communications Server 2007 R2 y Microsoft Lync. Sin embargo, si IPv6 no está disponible para la interoperabilidad y compatibilidad con versiones anteriores de Exchange, los administradores no necesitarán realizar cambios de configuración adicionales y en su lugar podrán usar IPv4.

Para Exchange 2013 Enterprise, la mensajería unificada debe comunicarse directamente con los pares SIP (puertas de enlace IP, IP PBX y SBC) que pueden no admitir IPv6 en su software o firmware. Por lo tanto, la mensajería unificada debe poder comunicarse directamente con los pares SIP que admiten IPv4 y, lo que es más importante, con IPv6. Para Exchange 2013 hospedado, la MU se comunica con el equipo de cliente a través de SBC, Lync Server 2010 o Lync Server 15. En entornos Exchange 2013 hospedados, los clientes con SIP IPv6 (como los servidores SBC y Lync), pueden implementarse y, por tanto, gestionar el proceso de conversión IPv6-a-IPv4.

## Compatibilidad de dispositivos de mensajería unificada para IPv6

Dado que los servidores de acceso de cliente y de buzones de correo de Exchange 2013 que ejecutan componentes y servicios de MU admiten IPv6, puerta de enlace IP, IP PBX y SBC, los proveedores también deben admitir IPv6. Hay varias cuestiones que afectan a la compatibilidad con dispositivos para IPv6:

  - Hay varias puertas de enlace IP y SBC que pueden admitir IPv6 pero aún no se han probado con IPv6 ni mensajería unificada. Esta compatibilidad puede añadirse en el futuro, pero depende del proveedor de hardware.

  - Algunas puertas de enlace IP actualmente no admiten IPv6.

  - Algunos SBC tienen funcionalidad IPv4-IPv6 pero actualmente no funcionan con mensajería unificada ya que no admiten SRTP/SDES (Protocolo de transporte en tiempo real seguro / Seguridad de protocolo de descripción de sesión).

  - Hay hardware IP PBX sin compatibilidad con pila dual e IPv6 puro; sin embargo, no se ha probado si estos dispositivos funcionan con Exchange 2013.

Actualmente, UCMA 4.0 tiene IPv6 habilitada. Esto significa que puede aceptar conexiones IPv6, pero que IPv4 también puede aceptarse al funcionar en modo dual o al realizar conexiones salientes. La ejecución en modo dual permite la realización de conexiones IPv4 cuando es necesaria la conexión con versiones anteriores de mensajería unificada de Exchange. Para las instalaciones de Lync, esto se realiza mediante Lync Server, que obtiene la información de versión desde Active Directory para la última versión de Exchange Server. Para que los dispositivos de telefonía tradicional (incluidos la puerta de enlace IP, IP PBX y SBC) admitan las conexiones IPv6 junto con IPv4, estos deben escuchar ambos tipos de conexiones. Esto se debe a que cada par SIP debe poder aceptar ambos tipos de conexiones para ser compatibles con versiones anteriores de mensajería unificada de Exchange. Esto es también es necesario para la compatibilidad con llamadas externas para ambos tipos de conexiones.

## Configuración de mensajería unificada para admisión de IPv6

Después de instalar los servidores de acceso de cliente y de buzones de correo, debe crear planes de marcado de mensajería unificada, operadores automáticos, puertas de enlace IP y grupos de extensiones. Para permitir que la mensajería unificada admita IPv6, debe:

  - Crear una nueva puerta de enlace IP de mensajería unificada o configurar una existente con una dirección IPv6 para cada una de las puertas de enlace IP, IP PBX o SBC en su red. Al crear y configurar las puertas de enlace IP de mensajería unificada necesarias, debe agregar la dirección IPv6 o el nombre de dominio completo (FGDN) de la puerta de enlace IP de mensajería unificada. Al agregar el FQDN a la puerta de enlace IP de mensajería unificada, debe haber creado los registros DNS correctos para resolver el FQDN de la puerta de enlace IP de mensajería unificada en la dirección IPv6. Si ya tiene una puerta de enlace IP de mensajería unificada, puede usar el cmdlet **Set-UMIPgateway** para configurar la dirección IPv6 o FQDN. Después de crear o configurar las puertas de enlace IP de mensajería unificada, puede usar el cmdlet **Get-UMIPgateway** para ver las propiedades de la puerta de enlace IP de mensajería unificada a fin de comprobar que la configuración de IPv6 sea correcta.

  - Configurar el parámetro *IPAddressFamily* en cada puerta de enlace IP de mensajería unificada. Para permitir que la puerta de enlace IP acepte paquetes IPv6, debe establecer la puerta de enlace IP de mensajería unificada para que acepte las conexiones tanto IPv4 como IPv6, bien para que acepte o solo las conexiones IPv6 mediante el uso del cmdlet **Set-UMIPgateway**. A continuación, configure el parámetro *IPAddressFamily* en una de las siguientes opciones:
    
      - *IPv4*: esta es la opción predeterminada y se usa si no hay otro valor configurado.
    
      - *IPv6*: esto habilita IPv6 como dirección de uso. Sin embargo, no se utiliza IPv4.
    
      - *Any*: esto permitirá el uso de IPv6 pero, si el dispositivo no admite IPv6, se usará IPv4 en su lugar.

  - Después de configurar puertas de enlace IP de mensajería unificada, también debe configurar puertas de enlace IP, IP PBX o SBC en su red para admitir IPv6. Para obtener detalles, consulte con su proveedor de hardware para obtener una lista de dispositivos que admitan IPv6 y conocer cómo configurarlos correctamente.

  - Alternativamente, puede establecer los servidores de acceso de cliente y buzones de correo para que acepten el tráfico IPv6 si alguno de los servidores está establecido únicamente para recibir tráfico IPv4. No obstante, la configuración predeterminada, tanto para servidores de acceso de clientes que ejecutan el servicio de enrutamiento de llamadas de mensajería unificada de Microsoft Exchange como para servidores de buzones de correo que ejecutan el servicio de mensajería unificada de Microsoft Exchange, es aceptar tráfico IPv4 e IPv6. Para obtener información acerca de cómo configurar los valores de IPv6 en servidores de acceso de cliente y de buzones de correo, consulte [Set-UMCallRouterSettings](https://technet.microsoft.com/es-es/library/jj215758\(v=exchg.150\)) y [Set-UMService](https://technet.microsoft.com/es-es/library/jj552412\(v=exchg.150\)).
    
    Hay dos parámetros que posiblemente deban configurarse en los servidores de acceso de cliente y de buzones de correo para que admitan IPv6: *IPAddressFamily* y *IPAddressFamilyConfigurable*. Para habilitar un servidor de acceso de cliente o de buzones de correo para que acepten paquetes IPv6, debe establecer dichos servidores para que acepten tanto conexiones IPv4 como IPv6, o bien para que acepten únicamente conexiones IPv6. Para configurar el parámetro *IPAddressFamily*, el parámetro *IPAddressFamilyConfigurable* debe estar establecido en `$true`.

## Lógica de direccionamiento IP de mensajería unificada

La lógica que respalda la compatibilidad de IPv6 con la mensajería unificada de Exchange 2013 es la siguiente:

  - Los servidores de acceso de cliente y de buzones de correo escuchan las interfaces IPv4 e IPv6 cuando la doble pila está habilitada cuando dichos servidores están establecidos como *IPv6* o *Any*. De lo contrario, se usa IPv4.

  - Para las llamadas salientes, la mensajería unificada utiliza el modo dual si el parámetro *IPAddressFamily*para las puertas de enlace IP de la MU, los servidores de acceso de cliente y los de buzones de correo están establecidos como *IPv6* o *Any*. De lo contrario, se usa IPv4.

Al realizar llamadas salientes en modo dual, si el parámetro *IPAddressFamily* está establecido en *IPv6* o *Any*:

  - UCMA obtendrá una lista de direcciones en el FQDN para un par SIP que intenta obtener.

  - UCMA probará todas las direcciones IPv6, si hay alguna.

  - Si UCMA determina que una dirección no está disponible, incluirá la dirección en una lista y no volverá a probarla nuevamente en base a un intervalo configurado. Esto evita que la MU reintente innecesariamente direcciones incorrectas conocidas.

  - Si no hay direcciones IPv6 disponibles, UCMA regresará a las direcciones IPv4 de la lista de direcciones de pares SIP.

