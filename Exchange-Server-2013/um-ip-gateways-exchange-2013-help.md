---
title: 'Puertas de enlace IP de mensajería unificada: Exchange 2013 Help'
TOCTitle: Puertas de enlace IP de mensajería unificada
ms:assetid: 991d77e0-3995-44ab-bedf-52ff7a0301ab
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123890(v=EXCHG.150)
ms:contentKeyID: 49895797
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Puertas de enlace IP de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2014-06-24_

La puerta de enlace IP de mensajería unificada representa un dispositivo de hardware con puerta de enlace física de voz sobre IP (VoIP), central de conmutación IP (PBX), o controlador de borde de sesión (SBC). Antes de usar una puerta de enlace VoIP, IP PBX, o SBC para responder a llamadas entrantes y enviar llamadas salientes a usuarios de correo de voz, debe crearse una puerta de enlace IP de MU en el servicio de directorio.

**Contenido**

Introducción a las puertas de enlace IP de MU

Puertas de enlace IP de mensajería unificada

Soporte IPv6 para puertas de enlace IP de mensajería unificada

Habilitar y deshabilitar puertas de enlace IP de mensajería unificada

## Introducción a las puertas de enlace IP de MU

Normalmente el término *puerta de enlace* describe un dispositivo físico que conecta dos redes no compatibles. Con mensajería unificada de Exchange y otras soluciones de mensajería unificada, la puerta de enlace de VoIP se usa para traducir entre la red telefónica pública conmutada (PSTN)/multiplexión por división de tiempos (TDM) o una red telefónica basada en conmutación de circuitos y un IP o una red de datos de conmutación de paquetes. Las PBX IP también traducen entre la red PSTN y una red de conmutación de paquetes, de manera que cuando se utiliza una PBX IP, no es necesario utilizar una puerta de enlace VoIP. Las puertas de enlace VoIP solo son necesarias si conecta un dispositivo de hardware PBX heredado a una implementación de MU.


> [!NOTE]
> Las redes de conmutación de paquetes son redes en las que los paquetes (mensajes o fragmentos de mensajes) se enrutan de manera individual entre dispositivos como enrutadores, conmutadores, puertas de enlace VoIP, PBX IP y SBC. Este tipo de red contrasta con la red de conmutación de circuitos que establece una conexión dedicada entre los dos nodos para su uso exclusivo durante la duración de la comunicación.



La mensajería unificada de Exchange depende de la capacidad de la puerta de enlace VoIP para traducir TDM o protocolos de telefonía basados en conmutación de circuitos, como la Red digital de servicios integrados (ISDN o RDSI) o QSIG, desde una PBX a los protocolos basados en VoIP o IP, como el protocolo de inicio de sesión (SIP), el protocolo de transporte en tiempo real (RTP) o T.38 para el transporte de facsímil en tiempo real.

Las PBX IP también se utilizan al conectar una red de telefonía de conmutación de circuitos a una red de datos o de conmutación de paquetes. También se utilizan para traducir protocolos de conmutación de circuitos a protocolos basados en VoIP o IP, tales como SIP, RTP y Secure RTPC (SRTP).

Los Controladores de borde de sesión (SBC) son un tanto distintos de las puertas de enlace VoIP y las PBX IP. En lugar de conectar una red de conmutación de circuitos a una red de conmutación de paquetes, se utilizan para conectar dos redes de datos en una red pública como Internet o en una conexión WAN privada. En mensajería unificada, los SBC se utilizan en una implementación híbrida de MU en la que la mensajería unificada usa algunos componentes que están ubicados localmente y otros, como los buzones de correo, que se ubican en la nube.

## Configuraciones de dispositivos de VoIP

Aunque hay diversos tipos y fabricantes de PBX, puertas de enlace VoIP y PBX IP, existen básicamente tres tipos de configuraciones de dispositivos VoIP:

  - **PBX IP**   Un único dispositivo que traduce entre la PSTN/TDM o una red telefónica basada en conmutación de circuitos y un IP o una red de datos de conmutación de paquetes

  - **PBX (heredada) y puerta de enlace VoIP**   Dos componentes separados que traducen juntos entre PSTN/TDM o red telefónica basada en conmutación de circuitos y un IP o una red de datos de conmutación de paquetes

  - **SBC**   Uno o varios dispositivos que conectan dos tipos de redes basadas en IP como una LAN y un centro de datos.

Para ser compatibles con la mensajería unificada, se usan uno o ambos tipos de configuración de dispositivos IP/VoIP al conectar una infraestructura de red de telefonía a una infraestructura de red de datos o conectar una implantación local con una implementación de mensajería unificada en la nube.

## Puertas de enlace IP de mensajería unificada

La puerta de enlace IP de mensajería unificada contiene uno o varios grupos de extensiones de MU y opciones de configuración. Los grupos de extensión de MU se usan para enlazar una puerta de enlace IP de MU con un plan de marcado MU. La combinación de la puerta de enlace IP de MU y un grupo de extensiones de MU establece un vínculo entre una puerta de enlace VoIP, IP PBX o SBC y un plan de marcado de MU. Mediante la creación de varios grupos de extensiones de mensajería unificada, puede asociar una única puerta de enlace IP a varios planes de marcado de mensajería unificada.

Una vez creada una puerta de enlace IP de mensajería unificada, los servidores de Exchange enlazados con la puerta de enlace IP de mensajería unificada enviarán una solicitud de OPCIONES de SIP a la puerta de enlace VoIP, PBX IP o SBC para asegurarse de que el dispositivo responde. En el caso de que la puerta de enlace VoIP, PBX IP, o SBC no responda a la solicitud, el servidor Exchange registrará un evento con el Id. 1400 en el que se informará de que la solicitud ha fallado. Si esto ocurre, asegúrese de que la puerta de enlace VoIP,PBX IP, o SBC esté disponible y en línea, y de que la configuración de mensajería unificada sea correcta.

Los servidores de buzón de correo se comunican solo con puertas de enlace VoIP, PBX IP, o SBC que aparecen como interlocutores SIP de confianza. En algunos casos, si dos puertas de enlace VoIP, PBX IP, o SBCsIP están configuradas para usar la misma dirección IP, se registrará un evento con el Id. 1175. La mensajería unificada protege de las solicitudes no autorizadas mediante la recuperación de la URL interna del directorio virtual de servicios web de mensajería unificada y, a continuación, usa dicha URL para crear una lista de FQDN para los interlocutores SIP de confianza. Cuando dos FQDN se resuelven con la misma dirección IP, este evento se registra.

## Soporte IPv6 para puertas de enlace IP de mensajería unificada

El Protocolo de Internet versión 6 (IPv6) es la versión del Protocolo de Internet (IP) más reciente. IPv6 está diseñado para corregir muchas de las deficiencias de IPv4, que era la versión anterior de IP. En Microsoft Exchange Server 2010, en implementaciones locales e híbridas, IPv6 solo se admitía cuando también se usaba IPv4.

En Exchange 2013 en implementaciones locales e híbridas, los componentes relacionados con la mensajería unificada y los servicios de voz se ejecutan solo en servidores de acceso de cliente y buzón de correo. Dado que la arquitectura de la mensajería unificada ha cambiado y ahora necesita API administrada de comunicaciones unificadas (UCMA) v4.0 para admitir IPv4 y IPv6 así como otras características de Exchange, los servidores de acceso de cliente y buzón de correo que cuentan con componentes y servicios de mensajería unificada son totalmente compatibles con redes IPv6 y no necesitan IPv4.

En implementaciones locales, híbridas y de Exchange Online los administradores de mensajería unificada empresarial y de mensajería unificada Exchange Online pueden usar IPv6 cuando conectan la mensajería unificada con dispositivos habilitados para IPv6, incluidos dispositivos como enrutadores, puertas de enlace IP, IP PBX y Microsoft Office Communications Server 2007 R2 y servidores de Microsoft Lync. Sin embargo, para la interpolaridad y la compatibilidad hacia atrás, se puede usar IPv4 sin cambios de configuración adicionales si el parámetro *IPAddressFamily* se establece a `Any` en las puertas de enlace IP de mensajería unificada.

La mensajería unificada de Exchange debe comunicarse directamente con los pares SIP (puertas de enlace VoIP, IP PBX y SBC) que pueden no admitir IPv6 en su software o firmware. Si no admiten IPv6, la mensajería unificada debe ser capaz de comunicarse directamente con interlocutores SIP que utilicen IPv4. Para el correo de voz alojado, la mensajería unificada se comunica con el equipo del cliente a través de SBC, Lync Server 2010, o Lync Server 2013. En entornos alojados, es posible implementar clientes IPv6 con SIP como SBC y servidores Lync para controlar el proceso de conversión de IPv6 a IPv4.

Para las implementaciones locales e híbridas después de instalar sus servidores de acceso de cliente y de buzones de voz, y para las implementaciones de mensajería unificada de Exchange Online, debe crear puertas de enlace IP de mensajería unificada. Si necesita sus puertas de enlace IP de mensajería unificada compatibles con IPv6, también debe:

1.  Crear una nueva puerta de enlace IP de mensajería unificada o configurar una existente con una dirección IPv6 para cada una de las puertas de enlace IP, IP PBX o SBC en su red. Al crear y configurar las puertas de enlace IP de mensajería unificada necesarias, debe agregar la dirección IPv6 o el nombre de dominio completo (FGDN) de la puerta de enlace IP de mensajería unificada. Al agregar el FQDN a la puerta de enlace IP de mensajería unificada, debe haber creado los registros DNS correctos para resolver el FQDN de la puerta de enlace IP de mensajería unificada en la dirección IPv6. Si ya tiene una puerta de enlace IP de mensajería unificada, puede usar el cmdlet **Set-UMIPgateway** para configurar la dirección IPv6 o FQDN.

2.  Configure el parámetro *IPAddressFamily* en cada puerta de enlace IP de mensajería unificada. Para permitir que la puerta de enlace VoIP acepte paquetes IPv6, deberá configurar la puerta de enlace IP de MU para que acepte conexiones IPv4 e IPv6, o para que acepte solo conexiones IPv6, usando el cmdlet **Set-UMIPgateway**.

3.  Después de configurar puertas de enlace IP de mensajería unificada, también debe configurar puertas de enlace IP, IP PBX o SBC en su red para admitir IPv6. Para obtener detalles, consulte con su proveedor de hardware para obtener una lista de dispositivos que admitan IPv6 y conocer cómo configurarlos correctamente.


> [!NOTE]
> El número máximo de puertas de enlace IP de mensajería unificada por plan de marcado es 200. Si crea más de 200 no se iniciará el servicio de mensajería unificada.



## Habilitar y deshabilitar puertas de enlace IP de mensajería unificada

De manera predeterminada, las puertas de enlace IP de MU permanecen habilitadas tras su creación. No obstante, es posible habilitar y deshabilitar la puerta de enlace IP de mensajería unificada. Si deshabilita una puerta de enlace IP de mensajería unificada, puede ajustarla para que fuerce a todos los servidores Exchange a colgar las llamadas existentes. De manera alternativa, puede configurarla para que fuerce a todos los servidores Exchange asociados con la puerta de enlace IP de mensajería unificada a dejar de controlar todas las llamadas nuevas que se presenten en la puerta de enlace VoIP, IP PBX, o SBC.

Si está integrando mensajería unificada con Office Communications Server R2 o Microsoft Lync Server, deberá permitir que una única puerta de enlace IP de MU realice llamadas salientes para los usuarios, y deshabilitar las llamadas salientes y demás puertas de enlace IP de MU asociadas con sus planes de marcado URI de SIP. Utilizar el Shell o el EAC para desactivar la llamada saliente.

Al seleccionar la puerta de enlace IP de mensajería unificada con la que realizar llamadas salientes para las implementaciones locales e híbridas, elija aquella que pueda admitir más tráfico. No permita el tráfico saliente a través de una puerta de enlace IP de MU que se conecta con un grupo de Lync Server Directors. Esto es necesario para garantizar que las llamadas salientes a usuarios externos que realiza un servidor de buzón de correo que ejecuta el servicio de mensajería unificada de Microsoft Exchange (por ejemplo, en situaciones de Reproducción en teléfono) recorren de forma fiable el firewall corporativo.

