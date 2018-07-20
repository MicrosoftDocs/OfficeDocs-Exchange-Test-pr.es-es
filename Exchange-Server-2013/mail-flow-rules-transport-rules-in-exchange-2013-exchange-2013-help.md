---
title: 'Reglas de transporte o de flujo de correo: Exchange 2013 Help'
TOCTitle: Reglas de flujo de correo (reglas de transporte)
ms:assetid: c3d2031c-fb7b-4866-8ae1-32928d0138ef
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351127(v=EXCHG.150)
ms:contentKeyID: 49895896
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Reglas de transporte o de flujo de correo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-04-28_

Puede usar las reglas de flujo de correo (también denominadas reglas de transporte) para identificar mensajes del flujo de correo de su organización de Exchange 2013 y realizar acciones en ellos. Las reglas de flujo de correo son similares a las reglas de la Bandeja de entrada que hay disponibles en Outlook y en Outlook Web App. La diferencia principal radica en que las reglas de flujo de correo actúan en los mensajes mientras se encuentran en tránsito y no después de que se entreguen al buzón de correo. Contienen un conjunto más amplio de condiciones, excepciones y acciones, lo que le proporciona la flexibilidad de implementar muchos tipos de directivas de mensajería.

En este artículo se explican los componentes de las reglas de flujo de correo y su funcionamiento.

Para obtener información acerca de las reglas de flujo de correo en Exchange Online, consulte [Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)). Para obtener información acerca de las reglas de flujo de correo en Protección de Exchange Online, consulte [Reglas de flujo de correo (reglas de transporte) en Exchange Online Protection](https://technet.microsoft.com/es-es/library/dn271424\(v=exchg.150\))

Puede usar el Centro de administración de Exchange (EAC) o el Shell de administración de Exchange para administrar las reglas de flujo de correo. Para obtener instrucciones sobre cómo administrar las reglas de transporte, consulte [Administrar reglas de flujo de correo](manage-mail-flow-rules-exchange-2013-help.md).

Para cada regla, tiene la posibilidad de aplicarla, probarla o probarla y notificar al remitente. Para obtener más información sobre las opciones de prueba, consulte [Probar una regla de flujo de correo](test-a-mail-flow-rule-exchange-2013-help.md) y [Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

Para implementar directivas de mensajería específicas mediante el uso de reglas de flujo de correo, vea estos temas:

  - [Usar reglas de transporte para inspeccionar datos adjuntos de mensajes](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [Escenarios comunes de bloqueo de datos adjuntos](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)

  - [Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [Usar reglas de flujo de correo para que los mensajes puedan evitar Otros correos](use-mail-flow-rules-so-messages-can-bypass-clutter-exchange-2013-help.md)

  - [Usar reglas de flujo de correo para enrutar el correo electrónico en función de una lista de palabras, expresiones o patrones](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)

  - [Escenarios comunes de aprobación de mensajes](common-message-approval-scenarios-exchange-2013-help.md)

## Componentes de las reglas de flujo de correo

Una regla de flujo de correo está formada por las condiciones, acciones y excepciones propiedades:

  - **Condiciones**   Identifican los mensajes a los que quiere aplicar las acciones. Algunas condiciones examinan campos de encabezado del mensaje (por ejemplo, los campos Para, De o CC). Otras examinan propiedades del mensaje (por ejemplo, el asunto, el cuerpo, los datos adjuntos, el tamaño del mensaje o la clasificación del mensaje). La mayoría de las condiciones exigen que se especifique un operador de comparación (por ejemplo, es igual a, no es igual a o contiene) y un valor de coincidencia. En caso de que no haya condiciones o excepciones, la regla se aplica a todos los mensajes.
    
    Para obtener más información acerca de las condiciones de regla de flujo de correo en Exchange 2013, consulte [Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

  - **Excepciones**   Identifican de forma opcional los mensajes a los que no deben aplicarse las acciones. Los mismos identificadores de mensaje que están disponibles en las condiciones están también disponibles en las excepciones. Las excepciones invalidan las condiciones e impiden que se apliquen las acciones de regla a un mensaje, aunque este cumpla todas las condiciones configuradas.

  - **Acciones**   Especifican lo que hay que hacer en los mensajes que cumplen las condiciones de la regla y no cumplen ninguna de las excepciones. Existen numerosas acciones disponibles, como, por ejemplo, rechazar, eliminar o redirigir mensajes; agregar más destinatarios; agregar prefijos al asunto del mensaje; o insertar avisos de declinación de responsabilidades en el cuerpo del mensaje.
    
    Para obtener más información acerca de las acciones de regla de flujo de correo en Exchange 2013, consulte [Acciones de regla de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md).

  - **Propiedades**: especifican otras configuraciones de las reglas diferentes a las condiciones, excepciones y acciones. Por ejemplo, especifican cuándo debe aplicarse la regla, si se va a aplicar o a probar y el periodo de tiempo en el que está activa.
    
    Para obtener más información, consulte la sección de Propiedades de regla de flujo de correo en este tema.

## Múltiples condiciones, excepciones y acciones

En la siguiente tabla se muestra cómo se controlan múltiples condiciones, valores de condición, excepciones y acciones en una regla.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Lógica</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Múltiples condiciones</p></td>
<td><p>Y</p></td>
<td><p>Un mensaje debe cumplir todas las condiciones de la regla. Si tiene que cumplir una condición u otra, use reglas independientes para cada condición. Por ejemplo, si desea agregar el mismo aviso de declinación de responsabilidades a los mensajes con archivos adjuntos y a los mensajes que contienen un texto específico, cree una regla para cada condición. En el EAC, puede copiar fácilmente una regla.</p></td>
</tr>
<tr class="even">
<td><p>Una condición con múltiples valores</p></td>
<td><p>O</p></td>
<td><p>Determinadas condiciones permiten especificar más de un valor. El mensaje debe coincidir con alguno de los valores especificados (no todos). Por ejemplo, si un mensaje de correo tiene el asunto <strong>Información del precio en bolsa</strong> y la condición <strong>El asunto incluye cualquiera de estas palabras</strong> está establecida para coincidir con las palabras <strong>Contoso</strong> o <strong>bolsa</strong>, la condición se cumple ya que el asunto contiene al menos uno de los valores de la condición.</p></td>
</tr>
<tr class="odd">
<td><p>Múltiples excepciones</p></td>
<td><p>O</p></td>
<td><p>Si un mensaje coincide con alguna de las excepciones, las acciones no se aplican al mensaje. El mensaje no tiene que coincidir con todas las excepciones.</p></td>
</tr>
<tr class="even">
<td><p>Múltiples acciones</p></td>
<td><p>Y</p></td>
<td><p>Mensajes que coinciden con las condiciones de una regla obtienen todas las acciones que se especifican en la regla. Por ejemplo, si se seleccionan las acciones <strong>Anteponer al asunto del mensaje</strong> y <strong>Agregar destinatarios en el cuadro CCO</strong>, ambas acciones se aplican al mensaje.</p>
<p>Tenga en cuenta que algunas acciones, por ejemplo, <strong>Borrar el mensaje sin notificar a nadie</strong>, evitan que se apliquen las reglas siguientes a un mensaje. Otras acciones como <strong>Reenviar el mensaje</strong> no permiten acciones adicionales.</p>
<p>También puede establecer una acción en una regla de modo que cuando se aplique la regla, no se apliquen las reglas posteriores al mensaje.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Propiedades de las reglas de flujo de correo

En la tabla siguiente se describen las propiedades de regla que están disponibles en las reglas de flujo de correo.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de la propiedad en el EAC</th>
<th>Nombre del parámetro en PowerShell</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Prioridad</strong></p></td>
<td><p><em>Priority</em></p></td>
<td><p>Indica el orden en el que se aplican las reglas a los mensajes. La prioridad predeterminada se establece en función del momento en el que se creó la regla (las reglas más antiguas tienen más prioridad que las más recientes y las reglas con una prioridad superior se procesan antes que las que tienen una prioridad inferior).</p>
<p>La prioridad de la regla en el EAC se cambia moviendo la regla hacia arriba o hacia abajo en la lista de reglas. En el PowerShell, establezca el número de prioridad (0 es la prioridad más alta).</p>
<p>Por ejemplo, si dispone de una regla para rechazar mensajes que incluyan un número de tarjeta de crédito y otra que exija su probación, deseará que se aplique primero la regla de rechazo y que dejen de aplicarse las demás.</p>
<p>Para obtener más información, consulte <a href="manage-mail-flow-rules-exchange-2013-help.md">Set the priority of a mail flow rule</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Modo</strong></p></td>
<td><p><em>Mode</em></p></td>
<td><p>Puede especificar si quiere que la regla inicie el procesamiento de mensajes inmediatamente o si quiere probar las reglas sin afectar a la entrega del mensaje (con o sin sugerencias de directiva de prevención de pérdida de datos o DLP).</p>
<p>Mediante las sugerencias de directiva, se muestra una nota breve en Outlook o en Outlook en la web que ofrece información sobre posibles infracciones de la directiva al usuario que crea el mensaje. Para obtener más información, consulte <a href="technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md">Sugerencias de directiva</a>.</p>
<p>Para obtener más información acerca de los modos, consulte <a href="test-a-mail-flow-rule-exchange-2013-help.md">Probar una regla de flujo de correo</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Activar esta regla en la siguiente fecha</strong></p>
<p><strong>Desactivar esta regla en la siguiente fecha</strong></p></td>
<td><p><em>ActivationDate</em></p>
<p><em>ExpiryDate</em></p></td>
<td><p>Especifica el intervalo de fechas en que la regla está activa.</p></td>
</tr>
<tr class="even">
<td><p>Casilla <strong>Activado</strong> seleccionada o no</p></td>
<td><p>Nuevas reglas: parámetro <em>Enabled</em> en el cmdlet <strong>New-TransportRule</strong>.</p>
<p>Reglas existentes: Usar los cmdlets <strong>Enable-TransportRule</strong> o <strong>Disable-TransportRule</strong>.</p>
<p>El valor se muestra en la propiedad <strong>State</strong> de la regla.</p></td>
<td><p>Puede crear una regla deshabilitada y habilitarla cuando desee probarla. O bien, puede deshabilitar una regla sin eliminarla para conservar la configuración.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Aplazar el mensaje si no se completa el procesamiento de la regla</strong></p></td>
<td><p><em>RuleErrorAction</em></p></td>
<td><p>Puede especificar cómo debe tratarse el mensaje si el procesamiento de la regla no se puede completar. La regla se omitirá de forma predeterminada, pero el mensaje se puede volver a enviar para su procesamiento.</p></td>
</tr>
<tr class="even">
<td><p><strong>La dirección del remitente debe coincidir con el siguiente elemento del mensaje</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>Si la regla usa condiciones o excepciones que examinan la dirección de correo electrónico del remitente, puede buscar el valor en el encabezado del mensaje, en el sobre del mensaje o en ambos.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Detener el procesamiento de más reglas</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>Se trata de una acción para la regla, pero parece una propiedad en el EAC. Puede dejar de aplicar reglas adicionales a un mensaje después de que esta regla procese un mensaje.</p></td>
</tr>
<tr class="even">
<td><p><strong>Comentarios</strong></p></td>
<td><p><em>Comments</em></p></td>
<td><p>Puede escribir comentarios descriptivos sobre la regla.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Cómo se aplican las reglas de flujo de correo a los mensajes

Todo el flujo de mensajes de su organización se evalúa mediante las reglas de flujo de correo habilitadas en esta. Las reglas se procesan en el orden que se especifica en la página **Flujo de correo** \> **Reglas** del Centro de administración de Exchange o en función del valor del parámetro *Priority* correspondiente de PowerShell.

Cada regla también ofrece la opción de detener el procesamiento de reglas adicionales si se encuentra una coincidencia con la regla en cuestión. Esta configuración es importante para los mensajes que coinciden con las condiciones de varias reglas de flujo de correo (¿qué regla desea que se aplique al mensaje? ¿Todas? ¿Solo una?).

## Diferencias en el procesamiento según el tipo de mensaje

Hay varios tipos de mensajes que pasan a través de una organización. En la tabla siguiente, se muestran los tipos de mensajes que se pueden procesar mediante reglas de flujo de correo.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de mensaje</th>
<th>¿Se puede aplicar una regla?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Mensajes normales</strong>   Mensajes que contienen un único formato de texto enriquecido (RTF) o HTML, un cuerpo de mensaje de texto sin formato o un conjunto alternativo o de varias partes de cuerpos de mensaje.</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p><strong>Cifrado de mensajes de Office 365 :</strong> mensajes que cifra Cifrado de mensajes de Office 365 en Office 365. Para obtener más información, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=392525">Cifrado de mensajes de Office 365</a>.</p></td>
<td><p>Las reglas siempre pueden acceder a los encabezados de sobre y procesar los mensajes según las condiciones que se inspeccionan en los encabezados.</p>
<p>Para que una regla inspeccione o modifique el contenido de un mensaje cifrado, deberá comprobar que el descifrado de transporte está habilitado (como obligatorio u opcional; el valor predeterminado es Opcional). Para obtener más información, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">Habilitar o deshabilitar el descifrado de transporte</a>.</p>
<p>También puede crear una regla que descifre automáticamente los mensajes cifrados. Para obtener más información, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=402846">Definir reglas para cifrar o descifrar mensajes de correo electrónico</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mensajes cifrados S/MIME</strong></p></td>
<td><p>Las reglas solo pueden acceder a los encabezados de sobre y procesar los mensajes según las condiciones que se inspeccionan en los encabezados.</p>
<p>No se pueden procesar reglas con condiciones que requieran la inspección del contenido del mensaje ni acciones que pueden modificar dicho contenido.</p></td>
</tr>
<tr class="even">
<td><p><strong>Mensajes protegidos por RMS:</strong> mensajes a los que se ha aplicado una directiva de Active Directory Rights Management Services (AD RMS) o Azure Rights Management (RMS).</p></td>
<td><p>Las reglas siempre pueden acceder a los encabezados de sobre y procesar los mensajes según las condiciones que se inspeccionan en los encabezados.</p>
<p>Para que una regla inspeccione o modifique el contenido de un mensaje protegido por RMS, deberá comprobar que el descifrado de transporte está habilitado (como obligatorio u opcional; el valor predeterminado es Opcional). Para obtener más información, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">Habilitar o deshabilitar el descifrado de transporte</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mensajes con firma transparente</strong>: mensajes que se han firmado pero no cifrado.</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p><strong>Mensajes de mensajería unificada (UM)</strong>   Mensajes creados o procesados por el servicio de mensajería unificada, como correo de voz, fax, notificaciones de llamadas perdidas y mensajes creados o reenviados con Microsoft Outlook Voice Access.</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mensajes anónimos</strong>: mensajes que han enviado remitentes anónimos.</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p><strong>Informes de lectura:</strong> informes que se generan en respuesta a las solicitudes de confirmación de lectura que realizan los remitentes. Los informes de lectura se clasifican en las clases de mensaje siguientes: <code>IPM.Note*.MdnRead</code> o <code>IPM.Note*.MdnNotRead</code>.</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


## Reglas de transporte y pertenencia a grupos

Cuando se define una regla de transporte mediante una condición que amplía la pertenencia a un grupo de distribución, el servicio de transporte del servidor del buzón de correo que aplica la regla guarda en caché la lista de destinatarios resultante. A eso se le llama *Caché de grupos expandida*; también la utiliza el agente de registro en diario con el fin de evaluar la pertenencia al grupo para las reglas del diario. De forma predeterminada, la caché de grupos expandida almacena la pertenencia a grupos durante cuatro horas. También se almacenan los destinatarios que devuelve el filtro de destinatarios de un grupo de distribución dinámico. La caché de grupos expandida hace que sean innecesarios los retornos repetidos a Active Directory y el tráfico de red resultante de resolver las pertenencias a grupos.

En Exchange 2013, este intervalo y otros parámetros relacionados con la caché de grupos expandida se pueden configurar. Es posible reducir el intervalo de expiración de caché o desactivar por completo el almacenamiento en caché, con el fin de garantizar que las pertenencias a grupos se actualizarán con mayor frecuencia. Es necesario planear el correspondiente aumento de la carga de los controladores de dominio de Active Directory para las consultas de expansión de grupos de distribución. También es posible borrar la caché de un servidor Buzón de correo reiniciando el servicio de transporte de Microsoft Exchange en ese servidor. Es necesario hacerlo en cada servidor Buzón de correo en el que se desea borrar la caché. Al crear y probar reglas de transporte que utilizan condiciones basadas en pertenencia a grupos de distribución, así como al solucionar problemas en esas reglas de transporte, también hay que tener en cuenta el impacto de la caché de grupos expandida.

## Almacenamiento y replicación de reglas

Las reglas de flujo de correo que se crean y configuran en servidores de buzones se almacenan en Active Directory y el servicio de transporte las lee y aplica en todos los servidores de buzones de la organización. Cuando se crea, modifica o elimina una regla de flujo de correo, el cambio se replica entre los controladores de dominio de la organización. Esto permite a Exchange proporcionar un conjunto de reglas de flujo de correo coherente en toda la organización.

**Notas**:

  - La replicación entre controladores de dominio depende de factores que no están controlados por Exchange (por ejemplo, el número de sitios de Active Directory y la velocidad de los vínculos de red). Por lo tanto, debe tener en cuenta que se pueden producir retrasos en la replicación cuando implemente reglas de flujo de correo en la organización. Para obtener más información sobre la replicación de Active Directory, consulte [Administración de la replicación y la topología de Active Directory con Windows PowerShell](https://go.microsoft.com/fwlink/p/?linkid=274904).

  - Cada servidor de buzones almacena en caché grupos de distribución expandidos para evitar consultas de Active Directory repetidas con el fin de determinar la pertenencia a un grupo. De forma predeterminada, las entradas en la memoria caché de grupos expandidos expiran cada cuatro horas. Por lo tanto, las reglas de flujo de correo no pueden detectar los cambios en la pertenencia al grupo hasta que se actualice la caché de grupos expandidos. Para forzar una actualización inmediata de la caché en un servidor de buzones, reinicie el servicio de transporte de Microsoft Exchange. Debe reiniciar el servicio en cada servidor de buzones en el que quiera actualizar de forma forzada la caché.

Las reglas de flujo de correo que se crean y configuran en servidores de transporte perimetral se almacenan en la instancia local de AD LDS en el servidor. No se produce ninguna replicación automática de reglas de flujo de correo en los servidores de transporte perimetral. Las reglas creadas en el servidor de transporte perimetral solo se aplican a los mensajes que pasan por el servidor local. Si tiene que aplicar el mismo conjunto de reglas de flujo de correo en varios servidores de transporte perimetral, puede clonar la configuración del servidor de transporte perimetral o exportar e importar las reglas de flujo de correo. Para obtener más información, consulte [Configuración clonada del servidor de transporte perimetral](edge-transport-server-cloned-configuration-exchange-2013-help.md) e [Import or export a mail flow rule collection](manage-mail-flow-rules-exchange-2013-help.md).

Siempre que el servicio de transporte en un servidor de buzones o un servidor de transporte perimetral detecta una regla de flujo de correo modificada, se registra un evento en el registro de aplicación en el Visor de eventos (identificador de evento 4002 en servidores de buzones e identificador de evento 16028 en servidores de transporte perimetral).

## Replicación de reglas y almacenamiento en entornos mixtos

Existen dos escenarios de entorno mixto que son comunes en Exchange 2013:

  - **Implementaciones híbridas en las que parte de la organización reside en UNRESOLVED\_TOKEN\_VAL(Office365)**
    
    En un entorno híbrido, no hay replicación de reglas entre la organización local de Exchange y UNRESOLVED\_TOKEN\_VAL(Office365). Por lo tanto, cuando cree una regla en Exchange, tendrá que crear una regla coincidente en UNRESOLVED\_TOKEN\_VAL(Office365). Las reglas que cree en UNRESOLVED\_TOKEN\_VAL(Office365) se almacenan en la nube, mientras que las reglas que cree en la organización local se almacenan de forma local en Active Directory. Si administra reglas en un entorno híbrido, debe asegurarse de mantener sincronizados los dos conjuntos de reglas. Para ello, realice el cambio en ambos sitios, o bien, realícelo en un entorno y después exporte las reglas e impórtelas en el otro entorno.
    

    > [!IMPORTANT]
    > Aunque hay una superposición sustancial entre las condiciones y acciones disponibles en UNRESOLVED_TOKEN_VAL(Office365) y en Exchange Server, hay diferencias. Si piensa crear la misma regla en ambas ubicaciones, asegúrese de que todas las condiciones y acciones que piensa usar estén disponibles. Para ver la lista de condiciones y acciones disponibles en UNRESOLVED_TOKEN_VAL(Office365), consulte los siguientes temas:<BR><A href="https://technet.microsoft.com/es-es/library/jj919235(v=exchg.150)">Excepciones (predicados) y las condiciones de la regla de flujo de correo en Exchange Online</A><BR><A href="https://technet.microsoft.com/es-es/library/jj919237(v=exchg.150)">Enviar por correo las acciones de regla de flujo de Exchange Online</A>



  - **Coexistencia con Exchange 2010 o Exchange 2007**
    
    Cuando coexisten con Exchange 2010 o Exchange 2007, todas las reglas de flujo de correo se almacenan en Active Directory y se replican en toda la organización, independientemente de la versión de Exchange Server que se utiliza para crear las reglas. Sin embargo, todas las reglas de flujo de correo están asociadas a la versión Exchange Server del servidor que se utilizó para crearlas y se almacena en un contenedor específico de la versión de Active Directory. Primera vez que se implementa Exchange 2013 en su organización, las reglas existentes se importan a Exchange 2013 como parte del proceso de instalación. Sin embargo, los cambios posteriormente tendría que hacerse con ambas versiones. Por ejemplo, si cambia una regla existente en Exchange 2013 (Shell de administración de Exchange o EAF), necesitará realizar el mismo cambio en Exchange 2010 (Shell de administración de Exchange o la UNRESOLVED\_TOKEN\_VAL(exEMC) ). O bien, puede exportar las reglas de Exchange 2013 e importarlos en Exchange 2010.
    
    Exchange 2010 no puede procesar reglas que tengan el valor de **versión** o **RuleVersion** 15.*n*.*n*.*n*. Para estar seguro de que todas las reglas pueden procesarse, use únicamente reglas que tengan el valor 14.*n*.*n*.*n*.

## Más información

[Administrar reglas de flujo de correo](manage-mail-flow-rules-exchange-2013-help.md)

[Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Acciones de regla de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Agentes de transporte](transport-agents-exchange-2013-help.md)

