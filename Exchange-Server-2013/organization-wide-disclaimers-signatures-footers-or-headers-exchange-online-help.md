---
title: 'Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización: Exchange 2013 Help'
TOCTitle: Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización
ms:assetid: e45e33c9-e53b-427c-ada5-70901bc399b8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn600437(v=EXCHG.150)
ms:contentKeyID: 61061230
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Puede agregar un aviso de declinación de responsabilidades de correo electrónico, un aviso de declinación de responsabilidades legales, firmas u otro tipo de información en la parte superior o inferior de los mensajes de correo electrónico que ingresan a su organización o salen de ella. Esto puede resultar necesario por requisitos empresariales, legales o normativos, para identificar mensajes de correo electrónico potencialmente no seguros o por otros motivos exclusivos de su organización.

Para configurar un aviso de declinación de responsabilidades, debe crear una regla de transporte que incluya las condiciones, por ejemplo, cuando el remitente pertenezca a un grupo específico o cuando el mensaje incluya determinados patrones de texto, y el texto que desea agregar. Para aplicar varios avisos de declinación de responsabilidades a un solo mensaje de correo electrónico, puede usar varias reglas de transporte.


> [!IMPORTANT]
> <UL>
> <LI>
> <P>Si desea que la información se agregue solo a los mensajes salientes, debe agregar una condición como los destinatarios ubicados fuera de la organización. De forma predeterminada, las reglas de transporte se aplican tanto a los mensajes entrantes como a los salientes.</P></LI></UL>



**Contenido**

Ejemplos

Ámbito del aviso de declinación de responsabilidades

Formato del aviso de declinación de responsabilidades

Opciones de reserva si no se puede agregar el aviso de declinación de responsabilidades

Más información

¿Busca procedimientos? Vea [Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización en Office 365](https://technet.microsoft.com/es-es/library/dn600323\(v=exchg.150\)).

## Ejemplos

Aquí le presentamos algunas ideas sobre cómo usar avisos de declinación de responsabilidades.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo</th>
<th>Texto de muestra agregado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Legal: mensajes salientes</p></td>
<td><p>Este correo electrónico y los archivos transmitidos con él son confidenciales y tienen como fin exclusivo el uso por parte del individuo o la entidad a quienes están dirigidos. Si ha recibido este correo electrónico por error, notifíqueselo al administrador del sistema.</p></td>
</tr>
<tr class="even">
<td><p>Legal: mensajes entrantes</p></td>
<td><p>Se les exige expresamente a los empleados que no realicen declaraciones difamatorias, no infrinjan ni autoricen ninguna infracción de las leyes de propiedad intelectual o cualquier otro derecho legal mediante comunicaciones por correo electrónico. Los empleados que reciban un correo electrónico de este tipo deben notificar a su supervisor de inmediato.</p></td>
</tr>
<tr class="odd">
<td><p>Observe que el mensaje se envió a un alias</p></td>
<td><p>Este mensaje se envió al grupo de discusión de ventas.</p></td>
</tr>
<tr class="even">
<td><p>Firma: recopila datos para cada empleado</p></td>
<td><p>Kathleen Mayer<br />
Departamento de Ventas<br />
Contoso<br />
www.contoso.com<br />
kathleen@contoso.com<br />
teléfono móvil: 111-222-1234</p></td>
</tr>
<tr class="odd">
<td><p>Publicidad</p></td>
<td><p>Haga clic aquí para ver los especiales de marzo.</p></td>
</tr>
</tbody>
</table>


Los ejemplos proporcionados en este artículo no están diseñados para utilizarse tal como se muestran. Modifíquelos según sus necesidades.

## Ámbito del aviso de declinación de responsabilidades

A medida que trabaja en los avisos de declinación de responsabilidades, considere a qué tipo de mensajes desea aplicarlos. Por ejemplo, quizás quiera especificar unos avisos de declinación de responsabilidades para mensajes internos y otros para mensajes externos, o para los mensajes que envían los usuarios de un departamento determinado. A fin de asegurarse de que solo el primer mensaje de una conversación incluya un aviso de declinación de responsabilidades, agregue una excepción que busque texto exclusivo de su aviso.

Aquí le presentamos algunos ejemplos de las condiciones y excepciones que puede usar.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Descripción</th>
<th>Condiciones y excepciones en el EAC</th>
<th>Condiciones y excepciones en el Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Fuera de la organización, si el mensaje original no incluye texto del aviso de declinación de responsabilidad, como &quot;CONTOSO LEGAL NOTICE&quot;.</p></td>
<td><p>Condición: <strong>El destinatario se encuentra</strong>&gt;<strong>fuera de la organización</strong>.</p>
<p>Excepción: <strong>El asunto o el cuerpo</strong>&gt;<strong>El asunto o el cuerpo coincide con estos patrones de texto</strong>&gt;<strong>CONTOSO LEGAL NOTICE</strong></p></td>
<td>

```powershell
-FromScope NotInOrganization -ExceptIf -SubjectOrBodyMatches "CONTOSO LEGAL NOTICE"
```
</td>
</tr>
<tr class="even">
<td><p>Mensajes entrantes con datos adjuntos ejecutables</p></td>
<td><p>Condición 1: <strong>El remitente se encuentra</strong>&gt;<strong>fuera de la organización</strong>.</p>
<p>Condición 2: <strong>Los datos adjuntos</strong>&gt;<strong>tienen contenido ejecutable</strong></p></td>
<td>

```powershell
-FromScope NotInOrganization -AttachmentHasExecutableContent
```
</td>
</tr>
<tr class="odd">
<td><p>El remitente está en el departamento de marketing</p></td>
<td><p>Condición: <strong>El remitente</strong>&gt;<strong>es miembro de este grupo</strong>&gt;<strong>group name</strong></p></td>
<td>

```powershell
-FromMemberOf "Marketing Team"
```
</td>
</tr>
<tr class="even">
<td><p>Cada mensaje que proviene de un remitente externo al grupo de discusión de ventas</p></td>
<td><p>Condición 1: <strong>El remitente se encuentra</strong>&gt;<strong>fuera de la organización</strong>.</p>
<p>Condición 2: <strong>El mensaje</strong>&gt;<strong>El cuadro Para o CC contiene esta persona</strong>&gt;<strong>group name</strong></p></td>
<td>

```powershell
-FromScope NotInOrganization -SentTo "Sales Discussion Group" -PrependSubject "Sent to Sales Discussion Group: "
```

</td>
</tr>
<tr class="odd">
<td><p>Agregue un anuncio a los mensajes salientes durante un mes</p></td>
<td><p>Condición 1: <strong>El destinatario se encuentra</strong>&gt;<strong>fuera de la organización</strong>.</p>
<p>Especifique las fechas en la parte inferior del cuadro de diálogo <strong>Nueva regla</strong>.</p></td>
<td><p>-ApplyHtmlDisclaimerLocation 'Prepend' -SentToScope 'NotInOrganization' –ActivationDate ‘03/1/2014’ –ExpiryDate ‘03/31/2014’</p></td>
</tr>
</tbody>
</table>


Para obtener una lista completa de las condiciones de la regla de transporte que puede usar para el aviso de declinación de responsabilidades, vea uno de los siguientes temas:

  - [Excepciones (predicados) y las condiciones de la regla de flujo de correo en Exchange Online](https://technet.microsoft.com/es-es/library/jj919235\(v=exchg.150\)) (Exchange Online)

  - [Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)

  - [Excepciones (predicados) y las condiciones de la regla de flujo de correo en Exchange Online](https://technet.microsoft.com/es-es/library/jj919235\(v=exchg.150\)) (Exchange Online Protection)

## Formato del aviso de declinación de responsabilidades

Puede darle el formato que sea necesario al aviso de declinación de responsabilidades. Aquí se muestra qué se puede incluir en el texto del aviso de declinación de responsabilidades.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de información</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Texto</p></td>
<td><p>La longitud máxima es de 5000 caracteres, incluidas las etiquetas HTML y las hojas de estilos en cascada (CSS) en línea.</p></td>
</tr>
<tr class="even">
<td><p>HTML y CSS en línea</p></td>
<td><p>Puede usar los estilos CSS en línea y HTML para darle formato al texto. Por ejemplo, use la etiqueta <code>&lt;HR&gt;</code> para agregar una línea antes del aviso de declinación de responsabilidades.</p>
<p>Se ignora el formato HTML de un aviso de declinación de responsabilidades si el aviso se agrega a un mensaje de texto sin formato.</p></td>
</tr>
<tr class="odd">
<td><p>Agregar imágenes</p></td>
<td><p>Use la etiqueta <code>&lt;IMG&gt;</code> para apuntar a una imagen disponible en Internet. Por ejemplo, <code>&lt;IMG src=&quot;http://contoso.com/images/companylogo.gif&quot; alt=&quot;Contoso logo&quot;&gt;</code></p>
<p>Tenga en cuenta que Outlook Web App y Outlook bloquean de forma predeterminada el contenido web externo, incluso imágenes. Es posible que los usuarios tengan que realizar una determinada acción, si desean ver el contenido externo bloqueado. Esto significa que puede que las imágenes agregadas mediante la etiqueta <code>IMG</code> no estén visibles de forma predeterminada. Recomendamos que pruebe los avisos de declinación de responsabilidades que contengan etiquetas <code>IMG</code> en los clientes de correo electrónico que sus destinatarios probablemente utilizarán; así se asegurará de que se muestran correctamente.</p></td>
</tr>
<tr class="even">
<td><p>Agregar información para firmas personalizadas</p></td>
<td><p>Si quiere que todos tengan el mismo formato de firma con la misma información, puede agregar información exclusiva para cada empleado, por ejemplo, <code>DisplayName</code>, <code>FirstName</code>, <code>LastName</code>, <code>PhoneNumber</code>, <code>Email</code>, <code>FaxNumber</code> y <code>Department</code>. La información debe estar entre dos signos de porcentaje (%%). Por ejemplo, para usar <code>DisplayName</code>, debe usar <strong>%%DisplayName%%</strong> en el aviso de declinación de responsabilidades.</p>
<p>Cuando se desencadena una regla de aviso de declinación de responsabilidades, se insertan los valores correspondientes al usuario. Los datos provienen de la cuenta de usuario de Active Directory del remitente (para un servidor Exchange local) o de la cuenta de Office 365 del remitente para Exchange Online.</p>
<p>Para obtener una lista completa de los atributos que se pueden usar en los avisos de declinación de responsabilidades y las firmas personalizadas, vea la descripción de la propiedad <code>ADAttribute</code> en <a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">Condiciones de las reglas de transporte (predicados)</a> (Exchange Server), <a href="https://technet.microsoft.com/es-es/library/jj919235(v=exchg.150)">Excepciones (predicados) y las condiciones de la regla de flujo de correo en Exchange Online</a> (Exchange Online) o <a href="https://technet.microsoft.com/es-es/library/jj919234(v=exchg.150)">Mail excepciones (predicados) y las condiciones de la regla de flujo de Exchange Online Protection</a> (Exchange Online Protection).</p></td>
</tr>
</tbody>
</table>


Por ejemplo, aquí hay un aviso de declinación de responsabilidades en HTML que incluye una firma, una etiqueta `IMG` y CSS incrustada.

```html
<div style="font-size:9pt;  font-family: 'Calibri',sans-serif;">
%%displayname%%</br>
%%title%%</br>
%%company%%</br>
%%street%%</br>
%%city%%, %%state%% %%zipcode%%</div>
&nbsp;</br>
<div style="background-color:#D5EAFF; border:1px dotted #003333; padding:.8em; ">
<div><img alt="Fabrikam"  src="http://fabrikam.com/images/fabrikamlogo.png"></div>
<span style="font-size:12pt;  font-family: 'Cambria','times new roman','garamond',serif; color:#ff0000;">HTML Disclaimer Title</span></br>
<p style="font-size:8pt; line-height:10pt; font-family: 'Cambria','times roman',serif;">This message contains confidential information and is intended only for the individual(s) addressed in the message. If you are not the named addressee, you should not disseminate, distribute, or copy this e-mail. If you are not the intended recipient, you are notified that disclosing, distributing, or copying this e-mail is strictly prohibited.  </p>
<span style="padding-top:10px; font-weight:bold; color:#CC0000; font-size:10pt; font-family: 'Calibri',Arial,sans-serif; "><a href="http://www.fabrikam.com">Fabrikam, Inc. </a></span></br></br>
</div>
```

## Opciones de reserva si no se puede agregar el aviso de declinación de responsabilidades

Algunos mensajes, como los mensajes cifrados, impiden que Exchange modifique el contenido del mensaje original. Puede controlar la forma en que su organización administra estos mensajes. Puede optar entre encapsular un mensaje que no se puede modificar dentro de un sobre de mensaje que contenga el aviso de declinación de responsabilidades, rechazar el mensaje si no se le puede agregar el aviso, o ignorar la acción del aviso y entregar el mensaje sin el aviso.

En la siguiente lista se describe cada una de las alternativas:

  - **Encapsular**   Si no se puede insertar el aviso de declinación de responsabilidades en el mensaje original, Exchange encierra, o "encapsula", el mensaje original en un sobre de mensaje nuevo. A continuación, el aviso de declinación de responsabilidades se inserta en el nuevo mensaje. El mensaje original no se entrega si no se puede encapsular en un nuevo sobre de mensaje. El remitente del mensaje recibe un informe de no entrega (NDR) que explica por qué el mensaje no se ha entregado.
    

    > [!IMPORTANT]
    > Si un mensaje original se encapsula en un nuevo sobre de mensaje, las posteriores reglas de transporte se aplican al nuevo sobre de mensaje, no al mensaje original. Por tanto, debe configurar las reglas de transporte con acciones de avisos de declinación de responsabilidades que encapsulen los mensajes originales en un nuevo cuerpo del mensaje después de configurar otras reglas de transporte.



  - **Rechazar**   Si el aviso de declinación de responsabilidades no se puede insertar en el mensaje original, Exchange no entrega el mensaje. El remitente del mensaje recibe un NDR que explica por qué el mensaje no se entregó.

  - **Ignorar**   Si no se puede insertar el aviso de declinación de responsabilidades en el mensaje original, Exchange permite que el mensaje original se entregue sin modificar. No se agrega ningún aviso de declinación de responsabilidades.

## Más información

[Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización en Office 365](https://technet.microsoft.com/es-es/library/dn600323\(v=exchg.150\))

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

[Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Reglas de flujo de correo (reglas de transporte) en Exchange Online Protection](https://technet.microsoft.com/es-es/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

