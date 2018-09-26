---
title: 'Marcas de correo no deseado: Exchange 2013 Help'
TOCTitle: Marcas de correo no deseado
ms:assetid: 28d3a5c2-8509-4b25-9876-763536e77c27
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996878(v=EXCHG.150)
ms:contentKeyID: 49895531
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Marcas de correo no deseado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Las marcas de correo electrónico no deseado le ayudan a diagnosticar los problemas relacionados con el correo no deseado mediante la aplicación de metadatos de diagnóstico, o marcas, como información específica del remitente, resultados de la validación del puzzle y resultados del filtrado de contenido, a los mensajes, mientras pasan a través de las características contra correo electrónico no deseado que filtran los mensajes entrantes de Internet.  Hay tres marcas contra correo electrónico no deseado: la marca de nivel de confianza contra suplantación de identidad (phishing), la marca de nivel de confianza contra correo no deseado y la marca de Id. de remitente.

Puede usar marcas de correo electrónico no deseado como herramientas de diagnóstico para determinar las acciones que se deben realizar con los falsos positivos y los mensajes que se sospecha que son correo electrónico no deseado que reciben las personas en los buzones.

## Visualización de marcas de correo electrónico no deseado

Las marcas de correo electrónico no deseado se pueden ver mediante Microsoft Outlook. Para obtener más información, consulte [Ver marcas de correo electrónico no deseado en Outlook](view-anti-spam-stamps-in-outlook-exchange-2013-help.md).

## Descripción del informe contra correo electrónico no deseado

Es un informe resumido de los resultados del filtro contra correo electrónico que se han aplicado a un mensaje de correo. El agente de filtrado de contenido aplica esta marca al sobre del mensaje en forma de encabezado X, del modo siguiente.

```PowerShell
X-MS-Exchange-Organization-Antispam-Report: DV:<DATVersion>;CW:CustomList;PCL:PhishingVerdict <verdict>;P100:PhishingBlock;PP:Presolve;SID:SenderIDStatus <status>;TIME:<SendReceiveDelta>;MIME:MimeCompliance
``` 

En la tabla siguiente se describe la información de filtro que puede aparecer en un informe de correo electrónico no deseado.


> [!NOTE]  
> El informe de correo electrónico no deseado solo muestra información de los filtros que se han aplicado a un mensaje específico. Por lo general, un informe de correo electrónico no deseado no contiene toda la información que se muestra en la tabla siguiente. Por ejemplo, puede recibir el siguiente informe de correo electrónico no deseado: <CODE>DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures</CODE>.



### Información de filtro en un informe de correo electrónico no deseado

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Marca</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SID</p></td>
<td><p>La marca de Id. del remitente (SID) se basa en la estructura de directivas del remitente (SPF) que autoriza el uso de dominios en el correo electrónico. La SPF aparece en el sobre del mensaje como <code>Received-SPF</code>. El proceso de evaluación de Id. del remitente genera un estado de Id. del remitente para el mensaje. Este estado se puede devolver con uno de los valores siguientes:</p>
<ul>
<li><p><strong>Pass   </strong>La dirección IP y la Dirección responsable pretendida (PRA) han superado la comprobación del Id. de remitente.</p></li>
<li><p><strong>Neutral   </strong>Los datos del Id. de remitente publicados no son explícitamente concluyentes.</p></li>
<li><p><strong>Soft fail</strong>   Es posible que la dirección IP de la PRA no esté en el conjunto permitido.</p></li>
<li><p><strong>Fail   </strong>La dirección IP no está permitida; no se encontró ninguna PRA en el correo entrante o no existe el dominio remitente.</p></li>
<li><p><strong>None   </strong>No hay datos publicados de la SPF en el DNS del remitente.</p></li>
<li><p><strong>TempError   </strong>Ha ocurrido un error temporal de DNS como, por ejemplo, un servidor DNS no disponible.</p></li>
<li><p><strong>PermError   </strong>El registro DNS no es válido; por ejemplo, existe un error en el formato de registro.</p></li>
</ul>
<p>La marca de Id. del remitente aparece como una cabecera X en el sobre del mensaje, tal y como se indica a continuación:</p>

```PowerShell
X-MS-Exchange-Organization-SenderIdResult:&lt;status&gt;
```

<p>Para obtener más información acerca del Id. del remitente, consulte <a href="sender-id-exchange-2013-help.md">Id. del remitente</a> .</p></td>
</tr>
<tr class="even">
<td><p>DV</p></td>
<td><p>La marca de versión del DAT (DV) indica la versión del archivo de definición de correo electrónico no deseado que se ha usado al examinar el mensaje.</p></td>
</tr>
<tr class="odd">
<td><p>SA</p></td>
<td><p>La marca de acción de firma (SA) indica que el mensaje se ha recuperado o se ha eliminado porque se ha encontrado una firma en el mensaje.</p></td>
</tr>
<tr class="even">
<td><p>SV</p></td>
<td><p>La marca de versión del DAT de firma (SV) indica la versión del archivo de firma que se utilizó al examinar el mensaje.</p></td>
</tr>
<tr class="odd">
<td><p>PCL</p></td>
<td><p>La marca de nivel de confianza de suplantación de identidad (phishing) (PCL) muestra la calificación del mensaje en función de su contenido y se aplica cuando el agente de filtrado de contenido procesa el mensaje. Este estado se puede devolver con uno de los valores siguientes:</p>
<ul>
<li><p><strong>Neutral   </strong>No es probable que el contenido del mensaje sea suplantación de identidad (phishing).</p></li>
<li><p><strong>Suspicious   </strong>Es probable que el contenido del mensaje sea phishing.</p></li>
</ul>
<p>El valor de PCL varía de 1 a 8. Una calificación de PCL de 1 a 3 devuelve el estado de <code>Neutral</code>. Esto significa que no es probable que el contenido del mensaje sea suplantación de identidad (phishing). Una calificación de PCL de 4 a 8 devuelve un estado de <code>Suspicious</code>. Esto significa que es probable que el mensaje sea &quot;phishing&quot;.</p>
<p>Los valores se utilizan para determinar qué medidas toma Outlook con los mensajes. Outlook usa la marca PCK para bloquear el contenido de los mensajes sospechosos.</p>
<p>La marca PCL aparece como una cabecera X en el sobre del mensaje, tal y como se indica a continuación:</p>


```PowerShell
X-MS-Exchange-Organization-PCL:&lt;status&gt;
```

</td>
</tr>
<tr class="even">
<td><p>SCL</p></td>
<td><p>La marca del nivel de confianza de correo no deseado (SCL) del mensaje muestra la calificación del mensaje en función de su contenido. El agente de filtrado de contenido usa la tecnología SmartScreen de Microsoft para evaluar el contenido de un mensaje y asignar una clasificación de confianza de correo no deseado para cada mensaje. El valor de SCL se encuentra de 0 a 9, donde 0 indica que es poco probable que sea correo electrónico no deseado y 9 indica que es más probable que sea correo electrónico no deseado. Las acciones que Exchange y Outlook realizan dependen de la configuración de los umbrales de SCL.</p>
<p>La marca SCL aparece como una cabecera X en el sobre del mensaje, tal y como se indica a continuación:</p>


```PowerShell
X-MS-Exchange-Organization-SCL:&lt;status&gt;
```

<p>Para obtener más información acerca de los umbrales de SCL y las acciones, consulte <a href="spam-confidence-level-threshold-exchange-2013-help.md">Umbral de nivel de confianza de correo no deseado</a> .</p></td>
</tr>
<tr class="odd">
<td><p>CW</p></td>
<td><p>La marca de ponderación personalizada (CW) de un mensaje indica que el mensaje contiene una palabra o una frase no aprobada y que el valor de SCL, o ponderación, esa palabra o frase no aprobada se ha aplicado a la calificación final de SCL:</p>
<ul>
<li><p>Las frases no aprobadas, o frases no admitidas, tienen una ponderación máxima y cambian la calificación de SCL a 9.</p></li>
<li><p>Las palabras o frases aprobadas, o frases admitidas, tienen una ponderación mínima y cambian la calificación de SCL a 0.</p></li>
</ul>
<p>Para obtener más información acerca del modo de agregar palabras o frases aprobadas y no aprobadas al agente de filtrado de contenido, consulte <a href="manage-content-filtering-exchange-2013-help.md">Administrar el filtrado de contenido</a>.</p></td>
</tr>
<tr class="even">
<td><p>PP</p></td>
<td><p>La marca de puzzle resuelto previamente (PP) indica que si un mensaje del remitente contiene un certificado electrónico válido y resuelto, basado en la funcionalidad de validación del certificado electrónico de Outlook, no es probable que se trate de un remitente malintencionado. En este caso, el agente Filtro de contenido reduciría la calificación de SCL.</p>
<p>El agente de filtrado de contenido no cambia la calificación de SCL si la característica de validación de certificado electrónico está habilitada y si se cumple alguna de las siguientes condiciones:</p>
<ul>
<li><p>Un mensaje entrante no contiene un encabezado de certificado electrónico.</p></li>
<li><p>El encabezado del certificado electrónico no es válido.</p></li>
</ul>
<p>Para obtener más información acerca de la característica de validación del matasellos, consulte <a href="content-filtering-exchange-2013-help.md">Filtrado de contenido</a>.</p></td>
</tr>
<tr class="odd">
<td><p>TIME:TimeBasedFeatures</p></td>
<td><p>La marca TIME indica que hay un tiempo de retraso importante entre la hora a la que se envió el mensaje y la hora a la que se recibió. La marca TIME se usa para determinar la calificación SCL final del mensaje.</p></td>
</tr>
<tr class="even">
<td><p>MIME:MIMECompliance</p></td>
<td><p>La marca MIME indica que el mensaje de correo electrónico no es compatible con MIME.</p></td>
</tr>
<tr class="odd">
<td><p>P100:PhishingBlock</p></td>
<td><p>La marca P100 indica que el mensaje contiene una dirección URL que está presente en un archivo de definición de suplantación de identidad (phishing).</p></td>
</tr>
<tr class="even">
<td><p>IPOnAllowList</p></td>
<td><p>La marca IPOnAllowList indica que la dirección IP del remitente se encuentra en la lista de IP permitidas. Para obtener más información acerca de la lista de direcciones IP permitidas, consulte <a href="http://go.microsoft.com/fwlink/?linkid=268732">Descripción del filtrado de conexión</a> .</p></td>
</tr>
<tr class="odd">
<td><p>MessageSecurityAntispamBypass</p></td>
<td><p>La marca MessageSecurityAntispamBypass indica que no se ha filtrado el contenido del mensaje y que se ha concedido al remitente permiso para eludir los filtros contra correo electrónico no deseado.</p></td>
</tr>
<tr class="even">
<td><p>SenderBypassed</p></td>
<td><p>La marca SenderBypassed indica que el agente de filtrado de contenido no procesa el filtrado de contenido de los mensajes recibidos de este remitente. Para obtener más información, consulte <a href="manage-content-filtering-exchange-2013-help.md">Administrar el filtrado de contenido</a>.</p></td>
</tr>
<tr class="odd">
<td><p>AllRecipientsBypassed</p></td>
<td><p>La marca AllRecipientsBypassed indica que se ha cumplido una de las condiciones siguientes para todos los destinatarios incluidos en el mensaje:</p>
<ul>
<li><p>El parámetro <em>AntispamBypassedEnabled</em> del buzón de correo del destinatario está establecido en <code>$true</code>. Es una configuración para destinatarios que sólo puede establecer un administrador que use el cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p>El remitente del mensaje se encuentra en la lista de remitentes seguros de Outlook del destinatario. Para obtener más información acerca de la lista de remitentes seguros, consulte <a href="manage-safelist-aggregation-exchange-2013-help.md">Administrar agregación de lista segura</a> .</p></li>
<li><p>El agente de filtrado de contenido no procesa ningún filtrado de contenido para los mensajes que se envían a este destinatario. Para obtener más información acerca de las excepciones de destinatarios, consulte <a href="manage-content-filtering-exchange-2013-help.md">Administrar el filtrado de contenido</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>

