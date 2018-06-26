---
title: 'Plantillas de directivas de DLP suministradas en Exchange: Exchange 2013 Help'
TOCTitle: Plantillas de directivas de DLP suministradas en Exchange
ms:assetid: 7e1917ab-1920-4a52-97d1-7dfe2add6198
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150530(v=EXCHG.150)
ms:contentKeyID: 48267679
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Plantillas de directivas de DLP suministradas en Exchange

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

En Microsoft Exchange Server 2013 y Exchange Online, puede usar las plantillas de directivas de prevención de pérdida de datos (DLP) como punto de inicio para crear directivas de DLP que le ayudarán a satisfacer las necesidades normativas y de cumplimiento específicas. Puede modificar las plantillas para satisfacer las necesidades específicas de su organización.


> [!WARNING]
> Debe habilitar sus directivas de DLP en modo de prueba antes de ejecutarlo en su entorno de producción. Durante dichas pruebas, se recomienda que configure buzones de usuarios de ejemplo y envíe mensajes de prueba que invoquen las directivas de prueba para confirmar los resultados.<BR>El uso de estas directivas no garantiza la conformidad con ninguna regulación. Después de finalizar la prueba, realice los cambios de configuración necesarios en Exchange, de modo que la transmisión de información cumpla con las directivas de su organización. Por ejemplo, es posible que deba configurar TLS con socios comerciales conocidos o bien añadir más acciones de reglas de transporte restrictivas, como por ejemplo añadir la protección de derechos en los mensajes que contengan cierto tipo de información.



## Plantillas disponibles para DLP

La tabla siguiente muestra las plantillas de directivas de DLP en Exchange. Para obtener más información acerca de cómo personalizar estas plantillas para crear directivas de DLP, consulte [Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Plantilla</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Datos financieros de Australia</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente datos financieros en Australia, incluidos los números de tarjetas de crédito y códigos SWIFT.</p></td>
</tr>
<tr class="even">
<td><p>Ley de registros de salud de Australia (Ley HRIP)</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente sujetos a la Ley de privacidad de información y registros de salud (HRIP) en Australia, como por ejemplo el número de expediente médico y el número de archivo fiscal.</p></td>
</tr>
<tr class="odd">
<td><p>Datos de identificación personal (PII) de Australia</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente como información de identificación personal (PII) en Australia, como el número de archivo fiscal y de la licencia de conducir.</p></td>
</tr>
<tr class="even">
<td><p>Ley de privacidad de Australia</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente sujetos a la Ley de privacidad de Australia, como el número de licencia de conducir y de pasaporte.</p></td>
</tr>
<tr class="odd">
<td><p>Datos financieros de Canadá</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente datos financieros en Canadá, incluidos los números de cuentas bancarias y tarjetas de crédito.</p></td>
</tr>
<tr class="even">
<td><p>Ley de información sobre salud (HIA) de Canadá</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a la Ley de información sobre salud (HIA) de Alberta, incluidos datos como los números de pasaporte e información de salud.</p></td>
</tr>
<tr class="odd">
<td><p>Ley sobre salud personal de Canadá (PHIPA) - Ontario</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a la Ley de protección de información sobre salud personal de Canadá (PHIPA) para Ontario, incluidos datos como los números de pasaporte e información de salud.</p></td>
</tr>
<tr class="even">
<td><p>Ley de información sobre salud personal de Canadá (PHIA) - Manitoba</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a la Ley de información sobre salud personal de Canadá (PHIA) para Manitoba, incluidos datos como información de salud.</p></td>
</tr>
<tr class="odd">
<td><p>Ley de protección de información personal de Canadá (PIPA)</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a la Ley de protección de información personal de Canadá (PIPA) para British Columbia, incluidos datos como los números de pasaporte e información de salud.</p></td>
</tr>
<tr class="even">
<td><p>Ley de protección de información personal de Canadá (PIPEDA)</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a la Ley de protección de información personal y documentos electrónicos de Canadá (PIPEDA), incluidos datos como los números de pasaporte e información de salud.</p></td>
</tr>
<tr class="odd">
<td><p>Datos de identificación personal de Canadá (PII)</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente como información de identificación personal (PII) en Canadá, como el número de identificación médica y el número de la Seguridad Social.</p></td>
</tr>
<tr class="even">
<td><p>Ley de protección de datos de Francia</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente sujetos a la Ley de protección de datos personales de Francia, como el número de la tarjeta del seguro médico.</p></td>
</tr>
<tr class="odd">
<td><p>Datos financieros de Francia</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente como información financiera en Francia, incluidos los datos de tarjetas de crédito, información de la cuenta y los números de tarjetas de débito.</p></td>
</tr>
<tr class="even">
<td><p>Información de identificación personal (PII) de Francia</p></td>
<td><p>Ayuda a detectar la presencia de datos que comúnmente se consideran información de identificación personal (PII) en Francia, incluidos datos como los números de pasaporte.</p></td>
</tr>
<tr class="odd">
<td><p>Datos financieros de Alemania</p></td>
<td><p>Ayuda a detectar la presencia de datos comúnmente considerados datos financieros en Alemania, como los números de las tarjetas de débito europeas.</p></td>
</tr>
<tr class="even">
<td><p>Información de identificación personal (PII) de Alemania</p></td>
<td><p>Ayuda a detectar la presencia de datos que comúnmente se consideran información de identificación personal (PII) en Alemania, incluidos datos como la licencia de conducir y los números de pasaporte.</p></td>
</tr>
<tr class="odd">
<td><p>Datos financieros de Israel</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente datos financieros en Israel, incluidos los números de cuentas bancarias y códigos SWIFT.</p></td>
</tr>
<tr class="even">
<td><p>Información de identificación personal (PII) de Israel</p></td>
<td><p>Ayuda a detectar la presencia de datos que comúnmente se consideran información de identificación personal (PII) en Israel, incluidos datos como el número de identificación nacional.</p></td>
</tr>
<tr class="odd">
<td><p>Protección de privacidad en Israel</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente sujetos a la ley de protección de privacidad de Israel, incluidos los datos como números de cuentas bancarias o de identificación nacional.</p></td>
</tr>
<tr class="even">
<td><p>Datos financieros de Japón</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente como información financiera en Japón, incluidos los datos de tarjetas de crédito, información de la cuenta y los números de tarjetas de débito.</p></td>
</tr>
<tr class="odd">
<td><p>Datos de identificación personal (PII) de Japón</p></td>
<td><p>Ayuda a detectar la presencia de datos que comúnmente se consideran información de identificación personal (PII) en Japón, incluidos datos como la licencia de conducir y los números de pasaporte.</p></td>
</tr>
<tr class="even">
<td><p>Protección de información personal de Japón</p></td>
<td><p>Ayuda a detectar la presencia de información sujeta a la ley de protección de información personal de Japón, incluidos los datos como los números de registro de residente.</p></td>
</tr>
<tr class="odd">
<td><p>Estándar de seguridad de datos PCI (PCI DSS)</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos al Estándar de seguridad de datos PCI (PCI DSS), incluidos los datos como los números de tarjetas de crédito o de débito.</p></td>
</tr>
<tr class="even">
<td><p>Ley contra el crimen cibernético de Arabia Saudí</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente sujetos a la Ley contra el crimen cibernético de Arabia Saudí, incluidos los datos como los números de cuentas bancarias internacionales y códigos SWIFT.</p></td>
</tr>
<tr class="odd">
<td><p>Datos financieros de Arabia Saudí</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente datos financieros en Arabia Saudí, incluidos los números de cuentas bancarias internacionales y códigos SWIFT.</p></td>
</tr>
<tr class="even">
<td><p>Información de identificación personal (PII) de Arabia Saudí</p></td>
<td><p>Ayuda a detectar la presencia de datos que comúnmente se consideran información de identificación personal (PII) en Arabia Saudí, incluidos datos como el número de identificación nacional.</p></td>
</tr>
<tr class="odd">
<td><p>Ley de acceso a informes médicos del Reino Unidos</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a la Ley de acceso a informes médicos del Reino Unido, incluidos los datos como los números del Servicio de salud nacional.</p></td>
</tr>
<tr class="even">
<td><p>Ley de protección de datos del Reino Unido</p></td>
<td><p>Ayuda a detectar la presencia de información sujeta a la ley de protección de datos del Reino Unido, incluidos los datos como los números del seguro nacional.</p></td>
</tr>
<tr class="odd">
<td><p>Datos financieros del Reino Unido</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente como información financiera en el Reino Unido, incluidos los datos de tarjetas de crédito, información de la cuenta y los números de tarjetas de débito.</p></td>
</tr>
<tr class="even">
<td><p>Código de prácticas en línea de información personal (PIOCP) del Reino Unido</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos al Código de prácticas en línea de información personal del Reino Unido, incluidos datos como información de salud.</p></td>
</tr>
<tr class="odd">
<td><p>Información de identificación personal (PII) del Reino Unido</p></td>
<td><p>Ayuda a detectar la presencia de datos que comúnmente se consideran información de identificación personal (PII) en el Reino Unido, incluidos datos como la licencia de conducir y los números de pasaporte.</p></td>
</tr>
<tr class="even">
<td><p>Normas de comunicaciones electrónicas y privacidad del Reino Unido</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a las Normas de comunicaciones electrónicas y privacidad del Reino Unido, incluidos los datos como la información financiera.</p></td>
</tr>
<tr class="odd">
<td><p>Normas del consumidor de la Comisión Federal de Comercio de los EE.UU.</p></td>
<td><p>Ayuda a detectar la presencia de información sujeta a las Normas del consumidor de la Comisión Federal de Comercio de los EE.UU., incluyendo datos como números de tarjeta de crédito.</p></td>
</tr>
<tr class="even">
<td><p>Datos financieros de EE.UU.</p></td>
<td><p>Ayuda a detectar la presencia de datos considerados comúnmente como información financiera en los Estados Unidos, incluidos los datos de tarjetas de crédito, información de la cuenta y los números de tarjetas de débito.</p></td>
</tr>
<tr class="odd">
<td><p>Ley Gramm-Leach-Bliley (GLBA) de EE.UU.</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a la Ley Gramm-Leach.Bliley (GLBA), incluidos los datos como números de Seguridad Social o de las tarjetas de crédito.</p></td>
</tr>
<tr class="even">
<td><p>Ley de seguros de salud (HIPAA) de los EE. UU.</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a la Ley de transferencia y responsabilidad de seguros de salud (HIPAA) de los Estados Unidos, incluidos datos como los números de la Seguridad Social e información de salud.</p></td>
</tr>
<tr class="odd">
<td><p>Ley Patriota de los EE.UU.</p></td>
<td><p>Ayuda a detectar la presencia de datos comúnmente sujetos a la Ley Patriota de los EE.UU., incluyendo datos como los números de tarjetas de crédito o números de identificación fiscal.</p></td>
</tr>
<tr class="even">
<td><p>Información de identificación personal (PII) de Estados Unidos</p></td>
<td><p>Ayuda a detectar la presencia de datos que comúnmente se consideran información de identificación personal (PII) en los Estados Unidos, incluidos datos como los números de la Seguridad Social o de las licencias de conducir.</p></td>
</tr>
<tr class="odd">
<td><p>Leyes de notificación de incumplimiento estatal de EE.UU.</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a las leyes de notificación de incumplimiento estatal de EE.UU., incluidos datos como los números de la Seguridad Social y de las tarjetas de crédito.</p></td>
</tr>
<tr class="even">
<td><p>Leyes de confidencialidad sobre el número de Seguridad Social de EE.UU.</p></td>
<td><p>Ayuda a detectar la presencia de datos sujetos a las leyes de confidencialidad sobre el número de Seguridad Social en EE.UU., incluidos datos como los números de la Seguridad Social.</p></td>
</tr>
</tbody>
</table>


## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Crear una directiva DLP a partir de una plantilla](how-to-new-dlp-data-loss-prevention-policy-template.md)

[Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

