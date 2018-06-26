---
title: 'Asesor de telefonía para Exchange 2013: Exchange 2013 Help'
TOCTitle: Asesor de telefonía para Exchange 2013
ms:assetid: e9f760f2-5901-4ed2-95a5-724555cc700e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee364753(v=EXCHG.150)
ms:contentKeyID: 50556901
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Asesor de telefonía para Exchange 2013

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2017-07-25_

La mensajería unificada (UM) requiere que se integre Microsoft Exchange con el sistema telefónico que haya en su organización. Una implementación correcta requiere un análisis cuidadoso de la infraestructura telefónica existente y la realización de los pasos de planificación adecuados para implementar la mensajería unificada.

La fase de planeación puede ser un reto importante para los administradores de Exchange con poca o ninguna experiencia con una red telefónica. Para obtener ayuda para enfrentarse a este reto, vea Resources to Help with Your UM Deployment más adelante en este tema.

Para ver las puertas de enlace VoIP admitidas para la mensajería unificada, determinar si su PBX admite el uso de un modelo o fabricante de puertas de enlace VoIP específicas, si se admite el IP PBX con una conexión SIP directa o bien conocer cuáles son los controladores de borde de sesión admitidos (SBC) para la mensajería unificada de Exchange Online, haga clic en uno de los vínculos siguientes:

  - Supported VoIP gateways

  - Supported PBXs when using an AudioCodes VoIP gateway

  - Supported PBXs when using a dialogic VoIP gateway
    
      - PBXs supported when using a DMG1000 series Media Gateway
    
      - PBXs supported when using a DMG 2000 series Media Gateway
    
      - PBXs supported when using a DMG3000 series Media Gateway

  - Supported IP PBXs

  - Supported IP PBXs when using SIP media gateways

  - Exchange Unified Messaging, Office Communications Server 2007 R2, and Microsoft Lync Server

## Recursos que ayudan con la implementación de mensajería unificada

Crear directrices para la implementación de redes de telefonía es todo un reto. Puede haber muchas diferencias entre ellas porque pueden incluir puertas de enlace VoIP, IP PBX y PBX con diferentes configuraciones, firmware y requisitos. Sin embargo, existen varios recursos que ayudan a implementar correctamente la mensajería unificada:

  - **Especialistas en mensajería unificada   **Los especialistas en mensajería unificada son integradores de sistemas que han recibido un aprendizaje técnico sobre mensajería unificada de Exchange impartido por el equipo de ingeniería de Exchange. Para ayudar a garantizar una transición sin problemas a la mensajería unificada a partir de sistemas de correo de voz heredados, Microsoft recomienda que todos los clientes contraten un especialista en mensajería unificada. Para ver la información de contacto, visite [Especialistas en mensajería unificada (UM) de Microsoft Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=262708) o [Microsoft Pinpoint para mensajería unificada](https://go.microsoft.com/fwlink/p/?linkid=261951).

  - **Notas de configuración para puertas de enlace VoIP, IP PBX y PBX admitidos**   En estas notas de configuración se incluye la configuración y otra información muy útil para configurar puertas de enlace VoIP, IP PBX y PBX para comunicarse con los servidores de mensajería unificada de su red. Para obtener más información, vea [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md).

  - **Notas de configuración para los controladores de borde de sesión admitidos**   Estas notas de configuración contienen parámetros y otra información muy útil al configurar los controladores de borde de sesión (SBC) para comunicarse con los servidores de Mensajería unificada en implementaciones híbridas y de mensajería unificada (UM) de Exchange Online. Para obtener más información, vea [Notas de configuración de los controladores de borde de sesión admitidos](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md).
    

    > [!NOTE]
    > En línea MU compatibilidad con sistemas PBX de terceros a través de conexiones directas desde cliente operado SBCs terminará en julio de 2018. Consulte el blog del equipo de Exchange <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">mensajería unificada de descontinuación de la compatibilidad con controladores de límite de sesión de Exchange Online</A> para obtener más información.



Antes de contratar un especialista de mensajería unificada, deberá ser capaz de responder a las preguntas clave que le hará. Tener la respuesta a las siguientes preguntas le ayudará a que la conversación con el especialista de MU sea productiva:

  - ¿Cuántos usuarios de teléfono o de correo de voz, o ambos, hay en su organización?

  - ¿A cuántos usuarios quiere proporcionar mensajería unificada?

  - ¿Qué PBX tiene pensado usar para la integración con la mensajería unificada?

  - ¿Cuántas PBX tiene su organización? Especifique los proveedores, tipos (basados en circuito o en IP), modelos y versiones de firmware.

  - ¿Están las PBX conectadas en red y están centralizadas o se encuentran en varias ubicaciones?

  - ¿Qué sistema o sistemas de correo de voz usa actualmente su organización? Especifique los proveedores, tipos, modelos y versiones de firmware.

  - ¿Cómo están integrados los sistemas de correo de voz en sus PBX (analógico, T1/E1, PRI, emulación de equipo digital, VoIP, otro)?

  - ¿Usa actualmente redes de voz?

  - ¿Qué tipo de sistema o sistemas de fax usa su organización y admiten dichos sistemas el enrutamiento del fax entrante para Exchange?

  - ¿Usa su organización operadores automáticos?

  - ¿Solo necesita asistencia para usuarios de teléfono, es decir, para los usuarios que no tendrán acceso al correo electrónico?

## Puertas de enlace VoIP admitidas

La integración de mensajería unificada con PBX requiere que se usen una o varias puertas de enlace VoIP para traducir los protocolos de conmutación de circuitos usados por PBX basadas en TDM en protocolos de conmutación de paquetes basados en IP que utiliza la mensajería unificada. Se han probado proveedores de puertas de enlace VoIP con varios modelos de puertas de enlace VoIP y de medios y son compatibles con la mensajería unificada.

La prueba de interoperabilidad de la Mensajería unificada con puertas de enlace VoIP, IP PBX y SBC se integra ahora en el Programa de Comunicaciones Unificadas e Interoperabilidad Abierta de Microsoft Microsoft. Para obtener más información, vea el [Programa de Comunicaciones Unificadas e Interoperabilidad Abierta de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=140722).

El programa de certificación [Programa de Comunicaciones Unificadas e Interoperabilidad Abierta de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=140722) para puertas de enlace VoIP, IP PBX y puertas de enlace VoIP avanzadas garantiza que los clientes tengan una experiencia de instalación y compatibilidad sin problemas cuando utilicen puertas de enlace de telefonía VoIP e IP PBX certificados con el software de comunicaciones unificadas de Microsoft. Solo reciben la certificación los productos que cumplen rigurosos y exhaustivos requisitos de prueba, así como las especificaciones y planes de prueba.

Para obtener más información acerca de la configuración de puertas de enlace VoIP, IP PBX, PBX y SBC compatibles, vea uno de los siguientes recursos:

  - [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Notas de configuración de los controladores de borde de sesión admitidos](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

Se comprobó la interoperabilidad de los siguientes proveedores de puertas de enlace VoIP:

  - AudioCodes

  - Dialogic

  - En la tabla siguiente se muestra el proveedor de puertas de enlace VoIP, el modelo y los protocolos que admite cada modelo.

### Puertas de enlace VoIP admitidas para mensajería unificada

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Proveedor</th>
<th>Modelo</th>
<th>Protocolos admitidos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>MediaPack 114/8 FXO</p></td>
<td><ul>
<li><p>Analógico con DTMF interno</p></li>
<li><p>Analógica con SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><ul>
<li><p>Analógico con DTMF interno</p></li>
<li><p>Analógico con SMDI</p></li>
<li><p>BRI Q.SIG</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><ul>
<li><p>T1/E1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG1000PBXDNIW</p></td>
<td><p>Emulación de equipo digital</p></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG1000LSW</p></td>
<td><ul>
<li><p>Analógico con DTMF interno</p></li>
<li><p>Analógico con SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG2000</p></td>
<td><ul>
<li><p>T1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><ul>
<li><p>BRI Q.SIG</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NET</p></td>
<td><p>VX1200</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Sonus</p></td>
<td><p>SBC 1000/2000 2.2.1 o posterior</p></td>
<td><ul>
<li><p>Señalización de TDM (ISDN o RDSI): AT&amp;T 4ESS/5ESS, Nortel DMS- 100, Euro ISDN (ETSI 300-102), QSIG, NTT InsNet (Japón), ANSI National ISDN-2 (NI-2)</p></li>
<li><p>Señalización de TDM (CAS): T1 CAS (E&amp;M, inicio de bucle); E1 CAS (R2)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Quintum</p></td>
<td><p>Tenor DX Series</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
</tbody>
</table>


## PBX admitidas al usar una puerta de enlace VoIP de AudioCodes

En la tabla siguiente se muestran las PBX compatibles con puertas de enlace VoIP de AudioCodes incluidas MediaPack-114 FXO, MediaPack-118 FXO y Mediant 2000.

### PBX compatibles con una puerta de enlace VoIP de AudioCodes

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante de PBX</th>
<th>Modelo/tipo de PBX</th>
<th>AudioCodes modelo &amp;quot;x&amp;quot; - sustituir con 4 u 8, según necesidad &amp;quot;y&amp;quot; - sustituir con 1, 2, 4, 8 o 16, según necesidad</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>OmniPCX 4400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Aastra</p></td>
<td><p>M1000, M2000</p></td>
<td><ul>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Magix/Merlin</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8300</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>S8700</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>IP Office</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>CallManager 4.x</p></td>
<td><ul>
<li><p>Mediant1000/IP-to-IP</p></li>
<li><p>Mediant2000/IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>Electra Elite</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>NEAX2400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP/RS232</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NeXspan</p></td>
<td><p>S</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Communication Server-1000M, 1000S, 1000E</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 11c, 51c, 61c, 81c</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Panasonic</p></td>
<td><p>KX-TES824, KX-TEA308</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Panasonic</p></td>
<td><p>KX-TDA30, KX-TDA100, KX-TDA200, KX-TDA600</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Shortel</p></td>
<td><p>Sistema de telefonía IP</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 150E</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 3550</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tadiran Telecom</p></td>
<td><p>Coral Flexicom, Coral IPX</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
</tbody>
</table>


## PBX admitidas al usar una puerta de enlace VoIP de Dialogic

Cada modelo de puerta de enlace VoIP de Dialogic admite diferentes PBX. En las tablas siguientes se muestran los fabricantes de PBX, el modelo y la puerta de enlace VoIP de Dialogic que se puede usar. Cada puerta de enlace VoIP usa diferentes métodos de señalización, densidades y protocolos.

## PBX admitidas al usar una puerta de enlace de medios de la serie DMG1000

En la siguiente tabla se muestran las PBX compatibles con la puerta de enlace de Dialogic Media de baja densidad (DMG1000). Sin embargo, al usar una DMG1000 analógica, se necesita una señalización suplementaria (RS232 SMDI, MD110, protocolos MCI o señalización Inband DTMF).

### PBX admitidas al usar una puerta de enlace VoIP serie DMG1000 de Dialogic de baja densidad

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante de PBX</th>
<th>Modelo/tipo de PBX</th>
<th>Modelo de DMG e indicaciones adicionales</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>Aastra MD110 (antes Ericsson MD110)</p></td>
<td><p>DMG1008LSW</p>
<p>Conectividad analógica mediante el protocolo MD110 RS232</p></td>
</tr>
<tr class="even">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3 S8100, S8300, S8700 y S8710 (Communications Mgr SW V2.0 o versiones posteriores)</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p>DMG1008LSW</p>
<p>Conectividad analógica usando el protocolo serial SMDI</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>SX-200D, SX-200 Light, SX-2000 Light, SX-2000 S, SX-2000 VS, SX-200 ICP</p></td>
<td><p>DMG1008MTLDNIW</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2000, 2400, 2400 IPX</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 1 - Opción 11, 21, 21A, 51, 61, 71 y 81</p>
<p>Meridian SL1 - Generic X11, versión 15 o posteriores</p>
<p>Nortel Communication Server - 1000M, 1000S, 1000E con V3.0 o versiones posteriores</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>SL 100</p></td>
<td><p>DMG1008LSW</p>
<p>Conectividad analógica usando el protocolo serie SMDI</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E (Europeo)</p></td>
<td><p>DMG1008LSW</p>
<p>Conectividad analógica mediante señalación Inband DTMF</p></td>
</tr>
<tr class="odd">
<td><p>Siemens/ROLM</p></td>
<td><p>8000 (versión de software 80003 o posterior)<br />
9000 (todas las versiones)</p>
<p>9751 (todas las versiones de software versión 9005)</p>
<p>9751 (versión de software 9006.4 o posterior)</p></td>
<td><p>DMG1008RLMDNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Toshiba</p></td>
<td><p>CTX (versión de software AR1ME021.00)</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="even">
<td><p>Otros</p></td>
<td><p>Varios</p></td>
<td><p>DMG1008LSW</p>
<p>Conectividad analógica mediante Inband DTMF o SMDI</p></td>
</tr>
</tbody>
</table>


## PBX admitidas al usar una puerta de enlace de medios de la serie DMG 2000

En la tabla siguiente se muestran las PBX compatibles con la puerta de enlace de Dialogic Media T1/E1 (DMG2000). La puerta de enlace DMG2000, que se suministra con densidades de span único (DMG2030DTIQ), span dual (DMG2060DTIQ) o span cuádruple (DMG2120DTIQ), admite los siguientes protocolos:

  - T1 CAS

  - T1 Q.SIG

  - E1 Q.SIG

  - T1 NI-2

  - T1 5ESS

  - T1 DMS100

Si usa una señalización asociada al canal (CAS), se necesita una señalización suplementaria (RS232 SMDI, MD110, protocolos MCI o señalización Inband DTMF). Si usa una señalización Q.SIG, la PBX debe admitir los servicios complementarios asociados con la información del autor y del destinatario de la llamada y las capacidades de transferencia de llamadas que precisa la mensajería unificada.

### PBX compatibles con la puerta de enlace DMG2000 Media Gateway

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante de PBX</th>
<th>Modelo/tipo de PBX</th>
<th>Versión de software necesaria</th>
<th>Protocolo e indicaciones adicionales</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>Versión 3.2.712.5</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><p>Versión 3 o posterior</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8500</p></td>
<td><p>Manager SW V2.0 o versiones posteriores</p></td>
<td><p>T1 CAS</p>
<p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Ericsson</p></td>
<td><p>MD110</p></td>
<td><p>Versión MX1 TSW R2A (BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>CAS (con protocolo serie SMDI)</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2400 IMX</p></td>
<td><p>Versión 5200 Dic. 92 1b o versiones posteriores</p></td>
<td><p>CAS (con protocolo serie MCI)</p></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>2400 IPX</p></td>
<td><p>R17 versión 03.46.001</p></td>
<td><p>T1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Meridian 1- Opción 11</p></td>
<td><p>Versión 15 o posterior; son necesarias las opciones 19 y 46.</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Communication Server 1000</p></td>
<td><p>Versión 2121, versión 4</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>Versión 9006.4 o posterior (nota: solo carga de software de Norteamérica)</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>V2 SMR 9 SMPO</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Mitel</p></td>
<td><p>SX-2000 S, SX-2000 VS</p></td>
<td><p>LW 34</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>3300</p></td>
<td><p>Versión 5.1.4.8</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
</tbody>
</table>


## PBX admitidas al usar una puerta de enlace de medios de la serie DMG4008BRI

La puerta de enlace DMG4000 Series Media incluye varias opciones de interfaz TDM. La puerta de enlace DMG4008BRI admite densidades de 4 puertos/8 canales y admite los protocolos siguientes:

  - ISDN BRI Q.SIG

  - ETSI-DSS1 (Euro ISDN)

  - NET 3 (Bélgica)

  - VN3 (Francia)

  - 1TR6 (Alemania)

  - INS-64 (Japón)

  - 5ESS personalizado (Norteamérica - AT\&T)

  - ISDN nacional (NI1 - Norteamérica)

En la tabla siguiente se muestran las PBX compatibles con una serie de puertas de enlace Dialogic 4000 Media (DMG4008).

### PBX compatibles con una puerta de enlace DMG4008BRI Media

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante de PBX</th>
<th>Modelo/tipo de PBX</th>
<th>Versión de software necesaria</th>
<th>Protocolo e indicaciones adicionales</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>S.0 B4400</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
</tbody>
</table>


## IP-PBX admitidos

La mensajería unificada también admite IP PBX. En la tabla siguiente se muestran las IP PBX compatibles con la conexión SIP directa para Mensajería unificada.

### IP PBX admitidas al usar una conexión SIP directa

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante de PBX</th>
<th>Modelo/tipo de PBX</th>
<th>Versión de software necesaria</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>MX-ONE</p></td>
<td><p>4.0</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Aura</p></td>
<td><p>5.2.1 con Service Pack 5 (SP5)</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Communication Server 2100</p></td>
<td><p>CS2100 SE13</p></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>Call Manager, Unified Communications Manager</p></td>
<td><p>5.1, 6.x, 7.0 and8.0</p></td>
</tr>
</tbody>
</table>


## IP PBX admitidas al usar puertas de enlace de medios SIP

La mensajería unificada también admite IP PBX con puertas de enlace de medios SIP. En la tabla siguiente se muestran las IP PBX compatibles con el uso de capacidades IP en IP de puertas de enlace de medios SIP para conectarse a la mensajería unificada.

### IP PBX admitidas al usar una puerta de enlace de medios SIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante de PBX</th>
<th>Modelo/tipo de PBX</th>
<th>Modelo de puerta de enlace SIP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco</p></td>
<td><p>Call Manager 4.x</p></td>
<td><p>AudioCodes Mediant 1000/2000 (habilitada para IP en IP)</p></td>
</tr>
</tbody>
</table>


## Mensajería unificada de Exchange, Office Communications Server 2007 R2 y Microsoft Lync Server

Para las implementaciones locales e híbridas, la Mensajería unificada de Exchange se puede implementar junto con Microsoft Office Communications Server 2007 R2, Microsoft Lync Server 2010 o Lync Server 2013 para ofrecer mensajería de voz, mensajería instantánea, presencia de usuario mejorada, conferencias de audio y vídeo, así como una experiencia de mensajería y de correo electrónico integrada para los usuarios de la organización. Para obtener más información, vea:

  - [Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=202010)

Para obtener más información acerca del Programa de Comunicaciones Unificadas e Interoperabilidad Abierta de Microsoft para infraestructuras de telefonía empresariales, incluida la búsqueda de puertas de enlace PSTN SIP e IP PBX certificadas, así como sobre el proceso por el que los proveedores de infraestructura de telefonía se unen y participan en el programa, vea el [Programa de Comunicaciones Unificadas e Interoperabilidad Abierta de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=132071).

