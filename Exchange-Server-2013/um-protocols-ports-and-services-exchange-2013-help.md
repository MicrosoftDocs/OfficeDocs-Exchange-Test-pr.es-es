---
title: 'Protocolos, puertos y servicios de mensajería unificada (UM): Exchange 2013 Help'
TOCTitle: Protocolos, puertos y servicios de mensajería unificada (UM)
ms:assetid: 5997ce29-1755-48bb-8ff4-b08da549482a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998265(v=EXCHG.150)
ms:contentKeyID: 54652438
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Protocolos, puertos y servicios de mensajería unificada (UM)

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2015-03-09_

Microsoft La mensajería unificada (MU) de Exchange 2013 requiere que se usen varios puertos TCP y Protocolos de datagramas de usuario (UDP) para establecer la comunicación entre servidores que ejecutan Exchange 2013 y otros dispositivos. Al permitir el acceso a través de estos puertos IP, se habilitará la mensajería unificada para que funcione correctamente. En este tema, se describen los puertos TCP y UDP que se usan en la mensajería unificada de Exchange 2013.

## Protocolos y servicios de mensajería unificada

Exchange 2013 Las características y los servicios de mensajería unificada dependen de puertos TCP y UDP estáticos y dinámicos para garantizar la correcta operación de los servidores de acceso de cliente que ejecutan el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange y los servidores de buzones de correo que ejecutan el servicio de mensajería unificada de Microsoft Exchange.Cuando se instala Exchange 2013, se agregan reglas del firewall de Windows estáticas entrantes para Exchange. Si cambia los puertos TCP utilizados por los servidores de buzones de correo y de acceso de cliente, también es posible que deba volver a configurar las reglas de firewall de Windows para permitir el correcto funcionamiento de la mensajería unificada.


> [!IMPORTANT]
> En los servidores de buzones de correo y de acceso de cliente de Exchange&nbsp;2013 que ejecutan componentes y servicios de mensajería unificada (UM), la configuración de Exchange crea reglas de firewall entrantes que permiten la comunicación entrante sin restricciones de puertos TCP. Se agregan las siguientes reglas entrantes para servicios de mensajería unificada (UM):



1.  **SESWorker (GFW) (TCP-In)**

2.  **UMCallRouter (GFW) (TCP-In)**

3.  **UMCallRouter (TCP-In)**

4.  **UMService (GFW) (TCP-In)**

5.  **UMService (TCP-In)**

6.  **UMWorkerProcess – RPC (TCP-In)**

7.  **UMWorkerProcess (GFW) (TCP-In)**

8.  **UMWorkerProcess (TCP-In)**

## Protocolo de inicio de sesión

El protocolo de inicio de sesión (SIP) es un protocolo que se usa para iniciar, modificar y finalizar una sesión interactiva de usuario que comprende elementos multimedia como vídeo, voz, mensajería instantánea, juegos en línea y realidad virtual. Es uno de los principales protocolos de señalización para Voz sobre IP (VoIP), junto con H.323. La mayoría de soluciones VoIP basadas en estándares usan H.323 o SIP. Sin embargo, también existen varios diseños y protocolos propietarios. Los protocolos VoIP admiten normalmente funciones como llamada en espera, llamada en conferencia y transferencia de llamada.

Los clientes SIP, como puertas de enlace VoIP y centrales de conmutación (PBX) IP, pueden usar el puerto 5060 UDP y TCP para conectarse a servidores SIP, incluidos servidores de acceso de cliente que ejecutan el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange. SIP es el único protocolo usado para configurar y anular llamadas de voz y vídeo. Todas las comunicaciones de voz y vídeo tienen lugar en el Protocolo de transporte en tiempo real (RTP).

## Protocolo de transporte en tiempo real

El RTP define un formato de paquetes estándar para enviar audio y vídeo sobre una red específica, como Internet. RTP solamente transporta datos de voz/vídeo en la red. SIP es el que suele realizar la configuración y la anulación de llamadas.

El RTP no requiere un puerto TCP o UDP estándar o estático con el que comunicarse. Las comunicaciones RTP tienen lugar en un puerto UDP par y el siguiente puerto impar superior se usa para las comunicaciones TCP. Aunque no existen asignaciones de intervalos de puertos estándar, RTP generalmente se configura para usar puertos entre 1024 y 65535, y los servidores de buzones de correo que ejecutan el servicio de mensajería unificada de Microsoft Exchange siguen esta convención. Es difícil para RTP atravesar firewalls porque usa un rango de puertos dinámico.

## Servicios web de mensajería unificada

Los servicios web de mensajería unificada instalados en servidores de buzones de correo usan IP para la comunicación en red entre un cliente, el servidor de buzones de correo y equipos que ejecutan otros roles de servidor de Exchange 2013. Varias características de cliente de Exchange 2013Outlook Web App y Outlook 2013 dependen de los servicios web de mensajería unificada para funcionar correctamente.

Las siguientes características de cliente de mensajería unificada dependen de los servicios web de mensajería unificada:

  - Las opciones de correo de voz que están disponibles con Exchange 2013Outlook Web App, incluso la función Reproducir en teléfono y la capacidad de restablecer un PIN.

  - La característica Reproducir en teléfono que se encuentra en un cliente de Outlook.

## Puertos de mensajería unificada

El servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange de un servidor de acceso de clientes usa SIP sobre el Protocolo de control de transmisión (TCP) o la Seguridad de la capa de transporte mutua (TLS mutua) para comunicarse con servidores de buzones de correo que ejecuten el servicio de mensajería unificada de Microsoft Exchange. Para evitar conflictos entre puertos TCP o del Protocolo de datagramas de usuario (UDP), el servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange y el servicio de mensajería unificada de Microsoft Exchange usan distintos puertos TCP de manera predeterminada y escuchan en ellos. Aceptan conexiones seguras y no seguras, en función de si se usa TLS mutua con el tráfico RTP y SIP. De forma predeterminada, un servidor de acceso de clientes escucha las solicitudes SIP en el puerto TCP 5060 en modo no seguro y en el puerto TCP 5061 en modo seguro SIP cuando se usa TLS mutua. Estos puertos se pueden configurar mediante el cmdlet **Set-UMCallRouterSettings**. El servicio del enrutador de llamadas de mensajería unificada de Microsoft Exchange en el servidor de acceso de clientes no administra el tráfico de medios (RTP o SRTP), por lo tanto se usan solamente los puertos TCP y no se usan los puertos UDP. De forma predeterminada, un servidor de buzones de correo escucha las solicitudes SIP en el puerto TCP 5062 en modo no seguro y en el puerto TCP 5063 en modo seguro SIP cuando se usa TLS mutua. Estos puertos no se pueden configurar mediante los cmdlets del Shell de administración de Exchange. El servicio de mensajería unificada de Microsoft Exchange en el servidor de buzones de correo acepta conexiones de un servidor de acceso de clientes en los puertos SIP 5062 y 5063. Una vez que el servidor de acceso de clientes redirige la solicitud SIP a un servidor de buzones de correo, se crea un canal de medios RTP o SRTP mediante una puerta de enlace VoIP, PBX IP o SBC, y el proceso de trabajo de mensajería unificada de Microsoft Exchange en el servidor de buzones de correo.

En la siguiente tabla se resumen los puertos y protocolos de Exchange 2013, y si dichos puertos se pueden cambiar.

### Puertos de escucha de mensajería unificada

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocolo</th>
<th>Puerto TCP</th>
<th>Puerto UDP</th>
<th>¿Se pueden cambiar los puertos?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP (servidor de acceso de cliente; servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange)</p></td>
<td><p>5060 (no protegido), 5061 (protegido). El servicio escucha en ambos puertos.</p></td>
<td><p>No aplicable</p></td>
<td><p>Sí, mediante el cmdlet <strong>Set-UMCallRouterSettings</strong>.</p></td>
</tr>
<tr class="even">
<td><p>SIP (servidor de buzones de correo; servicio de mensajería unificada de Microsoft Exchange)</p></td>
<td><p>5062 (no protegido), 5063 (protegido). El servicio escucha en ambos puertos.</p></td>
<td><p>No aplicable</p></td>
<td><p>No se pueden cambiar los puertos.</p></td>
</tr>
<tr class="odd">
<td><p>SIP (servidor de buzones de correo; proceso de trabajo de MU)</p></td>
<td><p>5065 y 5067 para TCP (no protegidos). 5065 y 5067 para TLS mutua (protegidos). Si se configura en modo Dual, también se usan 5066 y 5068.</p></td>
<td><p>No aplicable</p></td>
<td><p>No se pueden cambiar los puertos.</p></td>
</tr>
<tr class="even">
<td><p>RTP (servidor de buzones de correo; proceso de trabajo de MU)</p></td>
<td><p>No aplicable</p></td>
<td><p>Puertos entre 1024 y 65535.</p></td>
<td><p>Los puertos se pueden modificar en el archivo de configuración msexchangeum.config. El archivo msexchangeum.config se encuentra en la carpeta \Archivos de programa\Microsoft\Exchange\V15\bin en un servidor de mensajería unificada de Exchange 2013.</p></td>
</tr>
</tbody>
</table>


## Puertos de mensajería unificada (UM) y Lync Server

Mensajería unificada de Exchange 2013 admite la traducción de direcciones de red (NAT) transversal y permite que los medios RTP se envíen a un servidor de buzones de correo por un túnel a través de un firewall NAT. Sin embargo, para que esto funcione, también debe tener Microsoft Office Communications Server 2007 R2 y Microsoft Lync Server 2010 o Microsoft Lync 2013 implementados en el entorno. Si implementa Exchange 2013 y Communications Server 2007 R2 o Microsoft Lync Server 2010 o Lync 2013 en la red, esta implementación habilitará los servidores de buzones de correo que ejecutan el servicio de mensajería unificada de Microsoft Exchange para comunicarse con extremos fuera de un firewall NAT. El servidor de buzones de correo está asociado con un grupo de Communications Server 2007 R2, Microsoft Lync Server 2010 o Lync 2013 y obtiene los tokens de autenticación adecuados del servicio de autenticación A/V en un equipo que sirve ese grupo particular de Communications Server 2007 o Lync Server.

El servicio de autenticación A/V se usa para permitir el cruce de los medios de voz RTP por dispositivos y firewalls NAT. Esto resulta útil dado que las puertas de enlace de medios solo manejan señales y no pueden transportar la voz de forma segura a través de un dispositivo o firewall NAT. Cuando se configura un servidor de mediación en Communications Server 2007 R2, Lync Server 2010 o Lync 2013, se debe especificar el servidor perimetral A/V en el que se esté ejecutando el servicio de autenticación A/V de forma que el servidor de mediación pueda saber dónde debe enviar los paquetes de medios entrantes.

Para obtener más información sobre cómo implementar Communications Server 2007 R2 o Lync Server 2010 o 2013 y mensajería unificada de Exchange 2013, vea lo siguiente:

  - [Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Lista de comprobación: Integrar mensajería unificada de Exchange 2013 con Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)

