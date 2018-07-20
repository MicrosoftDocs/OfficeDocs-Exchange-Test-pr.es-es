---
title: 'Sugerencias de correo electrónico sobre las relaciones de la organización: Exchange 2013 Help'
TOCTitle: Sugerencias de correo electrónico sobre las relaciones de la organización
ms:assetid: 1784256f-abe1-4503-b8c4-26d544b73452
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ670165(v=EXCHG.150)
ms:contentKeyID: 49895493
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sugerencias de correo electrónico sobre las relaciones de la organización

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Microsoft Exchange Server 2013 le permite configurar relaciones de organización con Microsoft Exchange Online u otras organizaciones de Exchange. El establecimiento de una relación de organización le permite mejorar la experiencia de usuario al tratar con la otra organización. Por ejemplo, puede compartir datos disponibles u ocupados, configurar el flujo de mensajes seguros y habilitar el seguimiento de mensajes en ambas organizaciones.

## Control del nivel de acceso de sugerencias de correo electrónico

Es posible que desee restringir ciertos tipos de sugerencias de correo electrónico. Puede permitir que se devuelvan todas las sugerencias de correo electrónico o permitir sólo un conjunto limitado que evitaría informes de no entrega (NDR). Puede fijar esta configuración con el parámetro *MailTipsAccessLevel* en el cmdlet **Set-OrganizationRelationship**. La siguiente tabla muestra la información sobre correo que se devuelve en la relación de la organización.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Información sobre correo</th>
<th>¿Las sugerencias de correo electrónico están disponibles cuando el nivel de acceso se establece a &quot;Todo&quot;?</th>
<th>¿Las sugerencias de correo electrónico están disponibles cuando el nivel de acceso se establece a &quot;Limitado&quot;?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gran audiencia</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Respuestas automáticas</p></td>
<td><p>Sí</p>
<p>Si el dominio remoto del destinatario se especifica como interno, se mostrará la respuesta automática interna. De lo contrario, se muestra la respuesta automática externa.</p></td>
<td><p>Sí</p>
<p>Se muestra la respuesta automática externa.</p></td>
</tr>
<tr class="odd">
<td><p>Destinatario moderado</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Mensaje sobredimensionado</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Destinatario restringido</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Buzón de correo lleno</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Sugerencias de correo electrónico personalizadas</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Destinatarios externos</p></td>
<td><p>Sí</p>
<p>Si el dominio remoto del destinatario se especifica como interno, se suprimirá esta información sobre correo. De lo contrario, se devuelve la información sobre correo externa.</p></td>
<td><p>Sí</p>
<p>Si el dominio remoto del destinatario se especifica como interno, se suprimirá esta información sobre correo. De lo contrario, se devuelve la información sobre correo externa.</p></td>
</tr>
</tbody>
</table>


Para conocer los pasos detallados acerca de cómo configurar niveles de acceso de información sobre correo, consulte [Administrar sugerencias de correo electrónico para las relaciones de la organización](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

## Control del ámbito de acceso de sugerencias de correo electrónico

Cuando habilita la información sobre correo en una relación de organización y configura el nivel de acceso en `All`, la información sobre correo específica del destinatario, el buzón lleno, las respuestas automáticas y la información sobre correo personalizada se devolverán a todos los usuarios. Sin embargo, es posible que solo desee permitir esta información sobre correo a un grupo de usuarios específico. Por ejemplo, si configura una relación de organización con un asociado, es posible que desee permitir esta información sobre correo solo para los usuarios que trabajan con ese asociado.

Para lograrlo, primero necesita crear un grupo y agregar a todos los usuarios para los que desee compartir información sobre correo específica de ese destinatario con ese grupo. A continuación, se puede especificar ese grupo en la relación de la organización.

Después de implementar esta restricción, sus servidores de Acceso de cliente primero comprobarán si el destinatario para el que ha recibido la consulta de información sobre correo forma parte de este grupo. Si el destinatario es miembro de este grupo, los servidores de Acceso de cliente le enviará toda la información sobre correo, incluida la información sobre correo específica del destinatario. En caso contrario, no incluirán la información sobre correo específica del destinatario en su respuesta.

Para conocer los pasos detallados acerca de cómo configurar niveles de acceso de información sobre correo, consulte [Administrar sugerencias de correo electrónico para las relaciones de la organización](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

