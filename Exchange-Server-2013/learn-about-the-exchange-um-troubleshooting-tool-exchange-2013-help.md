---
title: 'Información herramienta solucionar problemas UM Exchange: Exchange 2013 Help'
TOCTitle: Información sobre herramienta para la solución de problemas de mensajería unificada de Exchange
ms:assetid: cc11bf5e-2c87-4495-b2ad-3e9a6bc81dbc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg584301(v=EXCHG.150)
ms:contentKeyID: 56271505
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Información sobre herramienta para la solución de problemas de mensajería unificada de Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La herramienta de solución de problemas de MU de Microsoft Exchange 2010 es un cmdlet del Shell de administración de Exchange denominado **Test-ExchangeUMCallFlow**. Esta herramienta es válida para efectuar una serie de pruebas de diagnóstico de mensajería unificada en la organización. Si alguna de las pruebas no se supera, la herramienta informa del motivo y presenta las posibles soluciones. La herramienta para la solución de problemas de Mensajería unificada solo se puede usar en los servidores Exchange 2010 o posteriores.

La herramienta de solución de problemas de mensajería unificada se usa para comprobar si el correo de voz funciona correctamente en las implementaciones locales y las implementaciones entre entornos. Esta herramienta se puede usar en las implementaciones de Mensajería unificada que incluyen Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server 2010 o posterior, o en las implementaciones de Mensajería unificada que incluyen puertas de enlace IP, centrales de conmutación IP (PBX IP) o controladores de borde de sesión (SBC).


> [!NOTE]
> La herramienta de solución de problemas de mensajería unificada se usa para realizar pruebas y solucionar problemas. Por otro lado, el cmdlet <STRONG>Test-UMConnectivity</STRONG> debe usarse para supervisión. El cmdlet <STRONG>Test-UMConnectivity</STRONG> se usa con los módulos de administración de System Center Operations Manager (SCOM) que se usan para supervisar los servidores de Mensajería unificada de Exchange 2010 o los servidores de buzones de correo y acceso de cliente de Exchange 2013 y los componentes de telefonía. El cmdlet <STRONG>Test-UMConnectivity</STRONG> efectúa pruebas de SIP locales y de inicio de sesión locales en buzones de correo; asimismo, puede ejecutarse como tarea de SCOM.



Para descargar la herramienta para la solución de problemas de Mensajería unificada, vea [Herramienta para la solución de problemas de Mensajería unificada](https://go.microsoft.com/fwlink/p/?linkid=182625).

**Contenido**

Introducción

Arquitectura de solución de problemas de Mensajería unificada

Implementaciones de puerta de enlace VoIP y PBX IP

Implementaciones de Office Communications Server 2007 R2 y Microsoft Lync Server

Instalación de la herramienta de solución de problemas de mensajería unificada

Parámetros del cmdlet

## Introducción

La herramienta de solución de problemas de mensajería unificada simplifica la realización de pruebas y la solución de problemas en las implementaciones de mensajería unificada. Cuando se ejecuta dicha herramienta, genera automáticamente una serie de archivos de seguimiento que se almacenan en la carpeta C:\\Users\\%UserProfile%\\AppData\\Roaming\\Microsoft Exchange 2010 UM Troubleshooting. La herramienta genera estos archivos de seguimiento:

  - **UMTool\_Collaboration**   Incluye seguimientos de pilas de comunicación en tiempo real.

  - **UMTool\_DiagnosticLog**   Muestra todas las pruebas realizadas y sus resultados.

  - **UMTool\_S4**   Incluye los seguimientos de pilas de señalización de S4.

  - **UMTool\_SIPMessageLogs**   Incluye todos los seguimientos de SIP para la llamada de prueba que se realiza.

La herramienta para la solución de problemas de Mensajería unificada se conecta directamente a un controlador de borde de sesión (SBC) local, si lo hay, o bien se conecta a un SBC de un centro de datos y emula una llamada entrante como si procediera de una PBX a través de una puerta de enlace VoIP o una PBX IP. La herramienta de solución de problemas de mensajería unificada es válida para diagnosticar los casos siguientes:

  - Configuración incorrecta de implementaciones de Mensajería unificada locales o entre locales que tengan implementado Office Communications Server 2007 R2 o Microsoft Lync Server.

  - Configuración incorrecta de equipos de telefonía locales o entre locales que incluyan puertas de enlace VoIP y PBX o PBX IP.

  - Problemas con el sistema de nombres de dominio (DNS).

  - Problemas de certificados al usar planes de marcado de mensajería unificada protegidos o protegidos por SIP.

  - Problemas de medios y señalización para DTMF (o marcación por tonos) y audio.

Si la herramienta de solución de problemas de mensajería unificada detecta un error en la configuración, informa sobre el motivo del error y las soluciones posibles. A continuación se muestran los errores de los que puede informar la herramienta de solución de problemas de mensajería unificada en una implementación local:

  - Se ha llegado al límite máximo de llamadas.

  - El usuario no está habilitado para mensajería unificada.

  - No se puede encontrar información sobre la puerta de enlace IP de mensajería unificada, el plan de marcado o el grupo de extensiones.

  - El tipo de seguridad no coincide con el plan de marcado de mensajería unificada.

  - No hay procesos de trabajo disponibles para procesar la llamada.

  - El servicio de Mensajería unificada o los servicios de enrutador de llamada de Mensajería unificada se detienen.

  - No se puede encontrar el bosque de Active Directory.

  - No se dispone de espacio en disco.

  - En la solicitud se han usado encabezados de SIP no válidos.

  - Se ha realizado una llamada a un servidor de Office Communications Server 2007 R2 o de Lync Server.

  - La puerta de enlace IP de mensajería unificada está deshabilitada.

  - El URI del usuario al que se llama no es válido.

Si la herramienta de solución de problemas de mensajería unificada se ejecuta en una implementación entre entornos, puede informar de los errores siguientes:

  - El usuario no está habilitado para mensajería unificada.

  - La puerta de enlace IP de mensajería unificada está deshabilitada.

  - El URI del usuario no es válido.

  - El tipo de seguridad no coincide con el plan de marcado de mensajería unificada.

  - En la solicitud se han usado encabezados de SIP no válidos.

  - No se puede encontrar información sobre la puerta de enlace IP de mensajería unificada, el plan de marcado o el grupo de extensiones.

La herramienta para la solución de problemas de Mensajería unificada envía un archivo .wav de muestra de 15 segundos. Después de enviar y reproducir el archivo de audio y la secuencia de audio RTP, la herramienta informa de la métrica de calidad de audio general para diagnosticar problemas de calidad de audio relacionados con la conectividad de red como, por ejemplo, vibración y pérdida de paquetes promedio. Estos informes incluyen la calidad de la secuencia de medios procedente de y destinada a un servidor de mensajería unificada, y contienen lo siguiente:

  - Clasificación de NMOS

  - Códec

  - Latencia en milisegundos

  - Vibración en milisegundos

  - % de pérdida de paquetes

  - A continuación se indican la clasificación de NMOS y la que se usará para determinar la calidad del audio:
    
      - NMOS menor que 2 = deficiente
    
      - NMOS mayor que 2 pero menor que 3 = promedio
    
      - NMOS mayor que 3 pero menor que 4 = buena
    
      - NMOS mayor que 4 pero menor que 5 = excelente

La herramienta de solución de problemas de mensajería unificada admite los planes de marcado de mensajería unificada que usan llamadas de los tipos Protegida, SIP protegida y No protegida. Si opta por Protegida o SIP protegida, la huella digital del certificado que se usa se comprueba para determinar si el certificado está en vigor y el tipo de certificado que se usa para comunicaciones de Seguridad de la capa de transporte. El certificado se usa para identificar de manera correcta y garantizar la identidad del equipo remoto. Si se selecciona el modo Protegida o SIP protegida, la herramienta de solución de problemas de mensajería unificada comprueba si se cumple lo siguiente:

  - El certificado local se ubica en el almacén de equipos locales.

  - El certificado que se utiliza es de confianza.

  - El nombre de destino especificado en el certificado es válido.

  - El certificado ha expirado.

  - El equipo remoto confía en el certificado.

  - El certificado se ha revocado.

  - El certificado carece del uso mejorado de clave requerido.

La herramienta para la solución de problemas de Mensajería unificada se puede ejecutar en modo de puerta de enlace o de SIPClient, según si está implementado Office Communications Server 2007 R2 o Lync Server, o según si se usan puertas de enlace VoIP y PBX o PBX IP con los servidores de Mensajería unificada. En modo de puerta de enlace o de SIPClient, la herramienta de solución de problemas de mensajería unificada permite realizar llamadas en los formatos siguientes. El formato que se usa depende del tipo de URI del plan de marcado de mensajería unificada:

  - Extensión telefónica   425-555-1010

  - Números de teléfono de E.164   +1 (425) 555-1010

  - Direcciones SIP   tonysmith@contoso.com

Si se usa el modo SIPClient, la herramienta de solución de problemas de mensajería unificada realiza una llamada de voz. Es una llamada que no llama a un teléfono ni a un extremo de comunicaciones unificadas, sino que envía directamente la llamada al buzón de voz. Si la herramienta de solución de problemas de mensajería unificada se ejecuta en modo de SIPClient, determinará:

  - El usuario de destino al que se llama.

  - Si la llamada SIP se ha establecido correctamente.

  - Si un servidor de Mensajería unificada de Exchange 2010 o un servidor de buzones de correo de Exchange 2013 aceptó la llamada SIP.

  - Si se ha recibido la secuencia de DTMF correcta.

  - Si un servidor de Mensajería unificada de Exchange 2010 o un servidor de buzones de correo de Exchange 2013 envió y recibió el archivo .wav de diagnóstico.

  - La métrica que se usó cuando se recibió la secuencia de medios o de calidad de audio.

La herramienta de solución de problemas de mensajería unificada emula llamadas entrantes y ejecuta una serie de pruebas de diagnóstico con las cuales los administradores locales y de arrendatario verifican el flujo de llamadas para detectar las llamadas de contestador automático e identificar errores de configuración. Aunque la herramienta de solución de problemas de mensajería unificada puede usarse en diferentes opciones de contestador automático, es válida para probar los tipos de llamadas siguientes:

  - Llamadas de Outlook Voice Access, incluidas las llamadas que acceden al correo de voz, el correo electrónico, el calendario, el directorio, los contactos personales o las opciones personales

  - Operadores automáticos de mensajería unificada

  - Reproducir en teléfono

  - Reglas de contestador automático

  - Faxes

  - Aprovisionamiento de mensajes

Introducción

## Arquitectura de solución de problemas de Mensajería unificada

La herramienta para la solución de problemas de Mensajería unificada ayuda a solucionar, diagnosticar y reparar problemas de configuración en implementaciones entre locales, y también se puede usar en implementaciones de Mensajería unificada locales. En las implementaciones entre locales, la herramienta valida también las configuraciones de SBC del sitio. El administrador puede probar todos los componentes de mensajería unificada usados por la mensajería unificada, incluidos los controladores de borde de sesión.

## Implementaciones de puerta de enlace VoIP y PBX IP

En el siguiente ejemplo, se usa el modo de puerta de enlace para probar el flujo de llamadas en un entorno que no incluye Office Communications Server 2007 R2 ni Lync Server. En este ejemplo, se prueban el equipo de telefonía, incluidas las puertas de enlace VoIP, PBX y PBX IP, y los componentes de Mensajería unificada. En este ejemplo, se configura el modo de seguridad de VoIP en No protegida, se usa la dirección IP 10.1.1.1 como el siguiente salto e incluye un número de extensión en la información de desvío.

```powershell
Test-ExchangeUMCallFlow -Mode Gateway -VoIPSecurity Unsecured -NextHop 10.1.1.1 -Diversion 12345
```

Introducción

## Implementaciones de Office Communications Server 2007 R2 y Microsoft Lync Server

La herramienta para la solución de problemas de Mensajería unificada se puede usar en las implementaciones locales o entre locales que incluyan Office Communications Server 2007 R2 o Microsoft Lync Server cuando se establece el modo SIPClient. En el siguiente ejemplo, se usa el modo SIPClient y se prueba el flujo de llamadas con un plan de marcado de Mensajería unificada con protección en un entorno que contiene servidores Office Communications Server 2007 R2 o Lync Server. De forma predeterminada, cuando se ejecuta la herramienta de solución de problemas de mensajería unificada, usa las credenciales del usuario que ha iniciado sesión en el equipo. Cuando ejecute el ejemplo siguiente, se le solicitará que proporcione las credenciales que desea usar para ejecutar la herramienta de solución de problemas de mensajería unificada. Para obtener más información, vea [Establecer las credenciales para usar con la herramienta para la solución de problemas de Mensajería unificada de Exchange](set-the-credentials-to-use-with-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).

    Test-ExchangeUMCallFlow -Mode SIPClient -VoIPSecurity Secured -CallingParty tony@contoso.com -CalledParty david@contoso.com -Credential $get

## Instalación de la herramienta de solución de problemas de mensajería unificada

La herramienta de solución de problemas de mensajería unificada se puede instalar en un servidor local de mensajería unificada o en otro equipo de 64 bits que ejecute:

  - Los sistemas operativos Windows 7 o Windows 8.

  - Los sistemas operativos Windows Server 2008 o Windows Server 2008 R2.

  - Los sistemas operativos Windows Server 2012 o Windows Server 2012 R2.

Si usa la herramienta para la solución de problemas de Mensajería unificada en una versión de 64 bits de Windows 7, Windows 8 o la edición de 64 bits de Windows Server 2008, los siguientes componentes deben estar instalados antes de poder instalar la herramienta para la solución de problemas de Mensajería unificada:

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1).   Vea [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/?linkid=152380).
    

    > [!NOTE]
    > Si la herramienta se ejecutará en un PC con Windows Vista o Windows Server 2008, vea <A href="https://go.microsoft.com/fwlink/?linkid=178998">Microsoft .NET Framework 3.5 Family Update para Windows Vista x64 y Windows Server 2008 x64</A>.



  - Administración remota de Windows (WinRM) 2.0 y Windows PowerShell V2 (Windows6.0-KB968930.msu)   Vea el artículo 968930 de Microsoft Knowledge Base, sobre el [paquete de Windows Management Framework Core (Windows PowerShell 2.0 y WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - API 2.0 administrada de comunicaciones unificadas de Microsoft, Core Runtime (UcmaRuntimeWebDownloadX64.msi)   Vea [API 2.0 administrada de comunicaciones unificadas, Core Runtime (64 bits)](https://go.microsoft.com/fwlink/?linkid=198175).

La herramienta para la solución de problemas de Mensajería unificada (cmdlet **Test-ExchangeUMCallFlow**) no se incluye en el DVD de Exchange 2010 SP1, en la descarga que solo incluye Exchange 2010 ni en los medios de instalación de Exchange 2013. Sin embargo, puede descargar la herramienta para la solución de problemas de Mensajería unificada desde el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625).

Para obtener más información, vea [Instalación de la herramienta para la solución de problemas de Mensajería unificada de Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).

Introducción

## Parámetros del cmdlet

En la siguiente tabla figuran los parámetros, junto con sus descripciones, que se pueden usar con el cmdlet **Test-ExchangeUMCallFlow**. También puede usar el comando del Shell `Get-help Test-ExchangeUMCallFlow -detailed` para buscar información detallada sobre los parámetros que pueden usarse con el cmdlet **Test-ExchangeUMCallFlow**, así como ejemplos prácticos.

### Parámetros

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>CalledParty</em></p></td>
<td><p>El parámetro <em>CalledParty</em> especifica el URI del SIP del usuario de Office Communications Server 2007 R2 o Lync Server que se ha habilitado para la Telefonía IP empresarial. Es el usuario al que el cmdlet <strong>Test-ExchangeUMCallFlow</strong> hará la llamada de voz, por ejemplo: <code>-CalledParty tonysmith@contoso.com</code>. Use este parámetro si está ejecutando la herramienta en modo SIPClient.</p></td>
</tr>
<tr class="even">
<td><p><em>CallingParty</em></p></td>
<td><p>El parámetro <em>CallingParty</em> especifica el URI del SIP del usuario de Office Communications Server 2007 R2 o Lync Server que se ha habilitado para la Telefonía IP empresarial. Es el usuario que efectúa la llamada entrante, por ejemplo: <code>-CallingParty tonysmith@contoso.com</code>. Use este parámetro si está ejecutando la herramienta en modo SIPClient.</p></td>
</tr>
<tr class="odd">
<td><p><em>Diversion</em></p></td>
<td><p>El parámetro <em>Diversion</em> especifica la cadena que se debe enviar como información de desvío de la llamada entrante. Puede ser en forma de desvío o encabezado de información de historial. La información de desvío que se incluye en la llamada entrante puede ser un número de extensión o proporcionar información de desvío adicional.</p>
<p>Al proporcionar información de desvío en el encabezado de información de historial, compruebe lo siguiente:</p>
<ul>
<li><p>Hay al menos dos entradas diferentes con distintas partes de usuario.</p></li>
<li><p>La última entrada contiene el número piloto del plan de marcado de Mensajería unificada asociado al usuario.</p></li>
<li><p>La penúltima entrada incluye un número de extensión del usuario habilitado para mensajería unificada. Esta entrada también debe incluir el texto de motivo adecuado. Este texto se debe escapar correctamente según las reglas de escape del parámetro URL estándar.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>El parámetro <em>Mode</em> especifica si se usará el modo de puerta de enlace VoIP, PBX IP o Office Communications Server 2007 R2 o Lync Server. Puede especificar el modo de puerta de enlace si la implementación de Mensajería unificada incluye puertas de enlace VoIP o PBX IP, o bien el modo SIPClient si la implementación de Mensajería unificada incluye Office Communications Server 2007 R2 o Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>NextHop</em></p></td>
<td><p>El parámetro <em>NextHop</em> especifica la dirección IP o el nombre de dominio completo (FQDN) del siguiente salto, y puede incluir también el puerto TCP del siguiente salto al que se debe conectar el cmdlet <strong>Test-ExchangeUMCallFlow</strong> mientras emula la puerta de enlace VoIP o PBX IP. Cuando incluya el puerto TCP, deberá incluir el puerto 5060 en modo No protegida o el puerto 5061 en modo Protegida o SIP protegida. Por ejemplo: <code>gateway.contoso.com:5061</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateThumbprint</em></p></td>
<td><p>El parámetro <em>CertificateThumbprint</em> especifica la huella digital del certificado usado para la Seguridad de la capa de transporte (TLS). Es necesario si en el plan de marcado de mensajería unificada se ha configurado en modo Protegida o SIP protegida. Esta huella digital de certificado es el certificado que se exportó a partir de la puerta de enlace VoIP, la PBX IP o el SBC. Además, el equipo que tiene instalada la herramienta de solución de problemas de mensajería unificada y se usa para probar el flujo de llamadas debe confiar en el certificado de autoridad del siguiente salto.</p></td>
</tr>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p>El parámetro <em>Credential</em> especifica las credenciales que se usarán para ejecutar el cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>HuntGroup</em></p></td>
<td><p>El parámetro <em>HuntGroup</em> especifica el grupo de extensiones de Mensajería unificada asociadas a la puerta de enlace VoIP que se emula. Por lo general, es un número de extensión. Use este parámetro si se está ejecutando la herramienta en modo de puerta de enlace.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoIPSecurity</em></p></td>
<td><p>El parámetro <em>VoIPSecurity</em> especifica el modo de seguridad al usar el cmdlet en modo de puerta de enlace. Puede usar uno de los valores modos de seguridad VoIP siguientes:</p>
<ul>
<li><p>Protegida (TLS/SRTP)</p></li>
<li><p>No protegida (TCP/RTP) (predeterminado)</p></li>
<li><p>SIP protegida (TLS/RTP)</p></li>
</ul></td>
</tr>
</tbody>
</table>


Introducción

