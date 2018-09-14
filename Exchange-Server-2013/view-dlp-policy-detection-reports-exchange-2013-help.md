---
title: 'Ver informes de detección de directivas de DLP: Exchange 2013 Help'
TOCTitle: Ver informes de detección de directivas de DLP
ms:assetid: 5c3f1cf6-d8c7-4d83-bb24-641ea9d50cbc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150520(v=EXCHG.150)
ms:contentKeyID: 48267663
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ver informes de detección de directivas de DLP

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-16_

La administración de detección de directivas de prevención de pérdida de datos (DLP) define, en términos generales, las actividades que una organización lleva a cabo para identificar, investigar y solucionar las infracciones de directivas de DLP. Para administrar incidentes, debe acceder a la información que identifica lo que han detectado las directivas de DLP. Esta información de detección está integrada con los formatos de registros y datos de Microsoft Exchange Server 2013, de manera que puede utilizar un sistema con datos ya existentes para administrar los incidentes del flujo de correo.

Para obtener información sobre la creación de informes de incidentes con un evento de detección de directiva única, vea [Crear informes de incidentes para detecciones de directivas de DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md). Para obtener más información acerca de los registros de mensajes, vea [Seguimiento de mensajes con informes de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).


> [!NOTE]
> Exchange&nbsp;2013: La prevención de pérdida de datos (DLP) es una característica especial que requiere una licencia de acceso de cliente de empresa (CAL) de Exchange. Para obtener más información sobre las CAL y la emisión de licencias del servidor, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licencias de Exchange Server</A>.



## Información de auditoría

Los datos relacionados con la administración de detección de DLP en Exchange se integran en los registros de seguimiento de mensajes, también conocidos como informes de entrega. Las funciones vuelven a usar en gran medida el marco de registro existente que está disponible en el sistema. Para obtener información general, incluida una explicación de la estructura de los archivos de registro de seguimiento de mensajes, consulte el contenido existente de [Descripción del seguimiento de mensajes](message-tracking-exchange-2013-help.md) o [Seguimiento de mensajes con informes de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).

Un informe de entrega es un registro detallado de toda la actividad de mensajes a medida que estos se transfieren de un equipo en el que se ejecuta el servicio de transporte a un servidor de buzones de correo. Se puede tener acceso al registro de seguimiento de mensajes a través del Shell de administración de Exchange mediante el cmdlet **Get-MessageTrackingLog**. Los datos de DLP se incluyen en el informe de entrega según las convenciones y los formatos de datos existentes.

## Formato de registro de datos

Los registros de seguimiento de mensajes incluyen datos de los agentes que participan en el procesamiento del contenido de flujo de correo. En el caso de DLP, se usa el agente de regla de transporte (TRA) para invocar el análisis profundo del contenido de los mensajes y para aplicar las directivas que se definieron como parte de ETR. Se utiliza el evento AgentInfo existente para agregar entradas relacionadas con DLP en el registro de seguimiento de mensajes.

El nombre del agente será **TRA** o **Agente de regla de transporte** en el evento AgentInfo. Se registrará solo un evento AgentInfo por mensaje, el cual describe el procesamiento de DLP aplicado al mensaje. Los datos de DLP que registre el agente de regla de transporte aparecerán en el campo **CustomData** del campo de entrada del registro de seguimiento de mensajes. Este campo puede contener varias entradas: una línea de clasificación de datos e información del cliente para cada clasificación de datos que se encuentra en el mensaje, una línea de regla para cada regla que se aplica al mensaje y una línea de supervisión de estado para cada regla que supera el umbral de carga o tiempo de ejecución.

Aquí se muestra un ejemplo de la entrada de registro de DLP. Se formateó el resultado a fin de mostrar las cadenas en líneas separadas con nuevas líneas entre medio.

Origen: AGENT

EventId: AGENTINFO

CustomData: S:TRA=DC|dcid=41BFDBC6C9D811E0816A3CD34824019B|count=10|conf=77;

S:TRA=DC|dcid=C7ECCBA0CA0011E0B6C00B124924019B|count=3|conf=81;

S:TRA=CI|sndOverride=or|just=Business Reason;

S:TRA=CI|sndOverride=fp;

S:TRA=ETR|ruleId=FC2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=PrependSubject|action=Encrypt|sev=2|mode=audit|dcid=41BFDBC6C9D811E0816A3CD34824019B|sndOverride=or;

S:TRA=ETR|ruleId=AB2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=Encrypt|sev=1|mode=enabled|dcid=C7ECCBA0CA0011E0B6C00B124924019B|sndOverride=fp;

S:TRA=ETRP|ruleId=C27D21EECA0311E0BCB896154924019B|LoadW=200|LoadC=100|ExecW=5500|ExecC=200;

El Agente de regla de transporte requiere la agrupación del Id. de regla, el Id. de directiva de DLP (opcional), la fecha de última modificación, la acción, la gravedad, el modo, la clasificación de datos detectados (opcional) y la invalidación de remitente (opcional) en función del ID de regla (indicado por “TRA=ETR” en la línea de registro). También requiere que se agrupe el Id de clasificación de datos, el recuento y el nivel de confianza de las clasificaciones según el nombre de clasificación (indicado por “TRA=DC” en la línea de registro).

Las agrupaciones adicionales incluyen el Id. de clasificación de datos, la invalidación de remitente (opcional) y la justificación de invalidación (opcional) en función del Id. de clasificación de datos para todas las clasificaciones que se detectaron en el cliente (indicado por “TRA=CI” en la línea de registro). El Agente de regla de transporte también requiere que se agrupe el Id. de regla, el reloj de carga (opcional), el reloj de carga de CPU (opcional), el reloj de ejecución (opcional) y el reloj de ejecución de CPU (opcional) según el Id. de regla para todas las reglas que superan los umbrales de reloj o reloj de CPU de carga o ejecución (indicado por “TRA=ETRP” en la línea de registro).

A continuación se muestra una lista completa de los campos de datos. Todos los datos en el MTL son del tipo cadena. La columna de formato describe cómo reconocer cada campo en el registro de seguimiento de mensajes. La columna Campo opcional especifica los campos que pueden no registrarse cuando coincide una regla. La columna Específico de DLP muestra qué campos son específicos para la función DLP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Nombre del campo</strong></p></td>
<td><p><strong>Descripción</strong></p></td>
<td><p><strong>Formato</strong></p></td>
<td><p><strong>Campo opcional</strong></p></td>
<td><p><strong>Específico de DLP</strong></p></td>
</tr>
<tr class="even">
<td><p>TRA</p></td>
<td><p>Agente de regla de transporte; tipo AgentName</p></td>
<td><p>TRA=DC, ETR, CI o ETRP</p></td>
<td><p>Obligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>DC</p></td>
<td><p>Clasificación de datos; tipo groupName</p></td>
<td><p>TRA=DC</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>ETR</p></td>
<td><p>Regla de transporte de Exchange; tipo groupName</p></td>
<td><p>TRA=ETR</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>CI</p></td>
<td><p>Información del cliente, tipo groupName</p></td>
<td><p>TRA=CI</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>ETRP</p></td>
<td><p>Rendimiento de regla de transporte de Exchange; tipo groupName</p></td>
<td><p>TRA=ETRP</p></td>
<td><p>Opcional</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>dcid</p></td>
<td><p>Id. de la clasificación de datos</p></td>
<td><p>dcid=GUID</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>count</p></td>
<td><p>Recuento de la clasificación de datos</p></td>
<td><p>count=Entero</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>conf</p></td>
<td><p>Nivel de confianza de la clasificación de datos</p></td>
<td><p>conf=Entero (porcentaje)</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>sndOverride</p></td>
<td><p>Invalidación de remitente; el campo es opcional.</p>
<p>En la línea TRA=CI, cuando el campo se establece en “or”, significa que se invalidó la clasificación de datos. Si el campo se establece en “fp”, significa que la clasificación de datos se notificó como un falso positivo.</p>
<p>En la línea TRA=ETR, cuando el campo se establece en “or”, significa que se invalidó la regla o parte de ella. Si el campo se establece en “fp”, significa que la regla, o parte de la regla, se notificó como un falso positivo.</p></td>
<td><p>sndOverride=or o fp</p>
<p>Donde &quot;or&quot; representa la invalidación y &quot;fp&quot; significa falso positivo. El campo sndOverride está presente cuando un usuario final informó que se invalidó una regla o que es un falso positivo.</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>just</p></td>
<td><p>Justificación; el campo es opcional y solo está disponible cuando el campo de invalidación de remitente es igual a “or” en la línea TRA=CI. Texto de justificación proporcionado por el usuario final como el motivo por el cual se debe invalidar la clasificación de datos.</p></td>
<td><p>just=cadena de justificación de entrada de IW</p>
<p>El campo de justificación solo se registra cuando el usuario final informa una invalidación.</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>ruleId</p></td>
<td><p>ID de una regla</p></td>
<td><p>ruleId=GUID</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>dlpId</p></td>
<td><p>Id. de una directiva de DLP. El campo es opcional; si no hay dlpId la regla no pertenece a una directiva de DLP.</p></td>
<td><p>dlpId=GUID</p></td>
<td><p>Opcional</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>st</p></td>
<td><p>Fecha de última modificación de una regla</p></td>
<td><p>st=fecha y hora UTC</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>action</p></td>
<td><p>Medidas adoptadas por una regla; pueden haber varias acciones por regla</p></td>
<td><p>action=acción única</p>
<p>Si hay varias acciones que se aplican para una regla, habrán varios campos de acción.</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>sev</p></td>
<td><p>Gravedad de auditoría de la regla</p></td>
<td><p>sev=1, 2 o 3</p>
<p>Donde 1 representa baja, 2 mediana y 3 alta.</p></td>
<td><p>Opcional</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>mode</p></td>
<td><p>Estado cuando se obtuvo acceso a la regla (aplicación, auditoría o auditandnotify).</p></td>
<td><p>mode=auditoría, auditandnotify o aplicación</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>loadW</p></td>
<td><p>Reloj de carga; el campo es opcional</p></td>
<td><p>loadW=tiempo en ms</p></td>
<td><p>Opcional</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>loadC</p></td>
<td><p>Reloj de carga de CPU; el campo es opcional</p></td>
<td><p>loadC=tiempo en ms</p></td>
<td><p>Opcional</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>execW</p></td>
<td><p>Reloj de ejecución; el campo es opcional</p></td>
<td><p>execW=tiempo en ms</p></td>
<td><p>Opcional</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>execC</p></td>
<td><p>Reloj de ejecución de CPU; el campo es opcional</p></td>
<td><p>execC=tiempo en ms</p></td>
<td><p>Opcional</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>message-id</p></td>
<td><p>Id. del mensaje</p></td>
<td><p>message-id=Id. del mensaje</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>fecha-hora</p></td>
<td><p>Fecha y hora en que se envió el mensaje en tiempo universal</p></td>
<td><p>date-time=Fecha y hora UTC</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>sender-address</p></td>
<td><p>Dirección de correo electrónico especificada en el campo de remitente</p></td>
<td><p>sender-address=Dirección de correo electrónico</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>dirección de destinatario</p></td>
<td><p>Direcciones de correo electrónico de los destinatarios del mensaje</p></td>
<td><p>recipient-address=Dirección de correo electrónico</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>message-subject</p></td>
<td><p>Datos que se encontraron en el campo de asunto del mensaje</p></td>
<td><p>message-subject=cadena de asunto de entrada del usuario final</p></td>
<td><p>Obligatoria</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Más información

[Prevención de pérdida de datos](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Crear informes de incidentes para detecciones de directivas de DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)

[Seguimiento de mensajes con informes de entrega](track-messages-with-delivery-reports-exchange-2013-help.md)

