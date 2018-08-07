---
title: 'Notas de configuración de puertas de enlace de VoIP, IP PBX y PBX admitidas'
TOCTitle: Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles
ms:assetid: 1583674f-5a57-45fd-8125-087d1624e686
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee681657(v=EXCHG.150)
ms:contentKeyID: 50556745
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

En esta página, se ofrecen vínculos a notas de configuración creadas y probadas por Microsoft o por un asociado de puertas de enlace VoIP. Cuando Microsoft o un asociado implementa la mensajería unificada con una puerta de enlace VoIP y una configuración de PBX o IP PBX nuevas, se registran los requisitos previos y las opciones de configuración. Esta información se usa para crear una nota de configuración.

Cada nota de configuración PBX contiene información acerca de cómo implementar la mensajería unificada con una configuración de telefonía específica e incluye el fabricante, el modelo y la versión de firmware de las puertas de enlace VoIP, IP PBX o PBX. Además, cada nota de configuración de PBX incluye otra información, como la siguiente:

  - Colaboradores en la creación de la nota de configuración.

  - Requisitos previos detallados que incluyen lo siguiente:
    
      - Características que se han habilitado o deshabilitado en la PBX.
    
      - Hardware especializado que debe instalarse.
    
      - Si es necesaria una puerta de enlace VoIP.
    
      - Características que deben estar presentes en la puerta de enlace VoIP en caso de que se necesite una.
    
      - Requisitos específicos de cableado entre una puerta de enlace IP y una PBX.
    
      - Una lista de las características de mensajería unificada que posiblemente no estén disponibles en una configuración telefónica determinada.

Para encontrar más información acerca del programa Microsoft Unified Communications Open Interoperability Program para infraestructuras de telefonía empresarial, incluida la búsqueda de puertas de enlace SIP/RTC e IP PBX certificadas, así como sobre el proceso que deben seguir lo proveedores de infraestructura de telefonía para unirse y participar en el programa, vea [Microsoft Unified Communications Open Interoperability Program](https://go.microsoft.com/fwlink/p/?linkid=132071).

## Notas de configuración sobre puertas de enlace VoIP, IP PBX y PBX

Microsoft está trabajando con asociados de puertas de enlace VoIP, AudioCodes y Dialogic para ampliar la lista de PBX probadas. Como actualmente estamos probando muchas combinaciones de componentes telefónicos, este tema se actualiza con frecuencia. Vuelva a comprobar si no puede localizar la nota de configuración para su implementación.

Están disponibles las siguientes notas de configuración:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Aastra</p></li>
<li><p>Alcatel</p></li>
<li><p>Avaya</p></li>
<li><p>Cisco</p></li>
<li><p>Inter-Tel</p></li>
<li><p>Intecom</p></li>
<li><p>Mitel</p></li>
<li><p>NEC</p></li>
</ul></td>
<td><ul>
<li><p>NeXspan</p></li>
<li><p>Nortel</p></li>
<li><p>Panasonic</p></li>
<li><p>Rolm</p></li>
<li><p>ShoreTel</p></li>
<li><p>Siemens</p></li>
<li><p>Sonus</p></li>
<li><p>Tadiran</p></li>
<li><p>Toshiba</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Aastra


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra MD110 (antes Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (también llamado BC13)</p></td>
<td><p>Analógico: serie MD110</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Aastra MD110 (antes Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (también llamado BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Aastra MX-ONE</p></td>
<td><p>4,0</p></td>
<td><p>Conexión SIP directa</p></td>
<td><p>N.D.</p></td>
<td><p>N.D.</p></td>
<td><p>Aastra</p></td>
<td><p><a href="http://www.aastra.com/cps/rde/aareddownload?file_id=4384-14746-_p06_xml%26dsproject=aastra%26mtype=pdf">Descarga</a></p></td>
</tr>
</tbody>
</table>


## Alcatel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OmniPCX 4400</p></td>
<td><p>R4.2-d2.304-4-h-il-c6s2</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Avaya


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aura</p></td>
<td><p>Gerente de comunicación 5.2.1 con SP 5</p>
<p>Administrador de sesión 5.2.</p></td>
<td><p>Conexión SIP directa</p></td>
<td><p>N.D.</p></td>
<td><p>N.D.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/downloads/">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>CS 2100</p></td>
<td><p>CS 2100 SE13</p></td>
<td><p>Conexión SIP directa</p></td>
<td><p>N.D.</p></td>
<td><p>N.D.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/css/p8/documents/100149819">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R009i.05.122.4</p></td>
<td><p>Emulación de equipo digital (DNI7434)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 CAS: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Merlin Magix</p></td>
<td><p>Versión 1.5 v.6.0</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>G3xV11 Communication Manager 1.3</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>T1 CAS: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Communication Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>S8500</p></td>
<td><p>Communication Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 CAS: DTMF en banda</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Communication Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>S8700</p></td>
<td><p>R011x.02.0.110.4</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Cisco


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco Call Manager 4.x</p></td>
<td><p>4.x</p></td>
<td><p>IP-to-IP</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco Call Manager 5.1</p></td>
<td><p>5.1.0.9921-12</p></td>
<td><p>Conexión SIP directa</p></td>
<td><p>N.D.</p></td>
<td><p>N.D.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 6.0 y 6.1</p></td>
<td><p>6.x</p></td>
<td><p>Conexión SIP directa</p></td>
<td><p>N.D.</p></td>
<td><p>N.D.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco Unified Communications Manager 7,0</p></td>
<td><p>7.0.2.20000-5</p></td>
<td><p>Conexión SIP directa</p></td>
<td><p>N.D.</p></td>
<td><p>N.D.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=196361">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 8.0</p></td>
<td><p>8.0.3.20000-5</p></td>
<td><p>Conexión SIP directa</p></td>
<td><p>N.D.</p></td>
<td><p>N.D.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=213007">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Inter-Tel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5000</p></td>
<td><p>Inter-Tel 5000 v2.1</p></td>
<td><p>T1 CAS: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Axxess</p></td>
<td><p>Axxess V9.0</p></td>
<td><p>T1 CAS: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Intecom


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PointSpan M6880</p></td>
<td><p>40PS3.5.K.2</p></td>
<td><p>T1 CAS: SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Mitel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>SX2000</p></td>
<td><p>5.0.24</p></td>
<td><p>Emulación de equipo digital (DNISS430)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008MTLDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
</tbody>
</table>


## NEC


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Electra Elite 192</p></td>
<td><p>SP034V4.5</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IMX</p></td>
<td><p>versión 7400</p></td>
<td><p>T1 CAS: serie MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IMX &amp; IPX</p></td>
<td><p>versión 7400</p></td>
<td><p>Emulación de equipo digital (DNIDtermIII)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver. R18.06.24.000</p></td>
<td><p>T1 CAS: serie MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver. R18.06.24.000</p></td>
<td><p>Analógico: serie MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver.17 Rel.03.46.001</p></td>
<td><p>T1 Q.SIG: serie MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
</tbody>
</table>


## NeXspan


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Los</p></td>
<td><p>RMS1 versión R1.3 E1TA</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Nortel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CS1000</p></td>
<td><p>3.0 y 4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Meridian 81C</p></td>
<td><p>4,5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Meridian 81C</p></td>
<td><p>4,5</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>Versión 25</p></td>
<td><p>Emulación de equipo digital (DNI2616)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Option11c</p></td>
<td><p>Versión 25</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>Versión 25</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>CS-1000M (sucesión)</p></td>
<td><p>Versión 25.40</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Panasonic


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KX-TDA200</p></td>
<td><p>001-001</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>KX-TDA200</p></td>
<td><p>3</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>KX-TES824</p></td>
<td><p>2.0.2</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Rolm


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9751</p></td>
<td><p>9005</p></td>
<td><p>Emulación de equipo digital (DNIRP400)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008RLMDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
</tbody>
</table>


## ShoreTel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sistema de telefonía IP</p></td>
<td><p>6.1</p></td>
<td><p>Analógico: SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Sistema de telefonía IP</p></td>
<td><p>7.5</p></td>
<td><p>Analógico: SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Siemens


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HiCom 150E</p></td>
<td><p>Ver. 2.2</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>Emulación de equipo digital (DNIOptiset)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>T1 CAS: DTMF en banda</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 3550</p></td>
<td><p>Ver. 3</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Ver 3.0 SMR5 SMP4</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Ver 3.0 SMR5 SMP4</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>Versión 2.0 SMR9 SMP0</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Versión 2.0 SMR9 SMP0</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Sonus


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de puerta de enlace VoIP</th>
<th>Versión de software de puerta de enlace VoIP</th>
<th>Protocolos admitidos</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SBC 1000/2000</p></td>
<td><p>2.2.1 o posterior</p></td>
<td><ul>
<li><p>Señalización de TDM (ISDN o RDSI): AT&amp;T 4ESS/5ESS, Nortel DMS- 100, Euro ISDN (ETSI 300-102), QSIG, NTT InsNet (Japón), ANSI National ISDN-2 (NI-2)</p></li>
<li><p>Señalización de TDM (CAS): T1 CAS (E&amp;M, inicio de bucle); E1 CAS (R2)</p></li>
</ul></td>
<td><p>Sonus</p></td>
<td><p><a href="http://www.sonus.net/sites/default/files/sonussbc1k2kconfigo365.pdf">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Tadiran


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS: DTMF en banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Descargar</a></p></td>
</tr>
</tbody>
</table>


## Toshiba


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versión de software de la PBX</th>
<th>Protocolo</th>
<th>Proveedor de puerta de enlace</th>
<th>Modelo de puerta de enlace</th>
<th>Autor de la configuración</th>
<th>Descarga del archivo de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>Analógico: SMDI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
<tr class="even">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>Analógico: DTMF en banda</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Descargar</a></p></td>
</tr>
</tbody>
</table>

