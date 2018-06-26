---
title: 'Administrar reglas de flujo de correo: Exchange 2013 Help'
TOCTitle: Administrar reglas de flujo de correo
ms:assetid: e7a81372-b6d7-4d1f-bc9e-a845a7facac2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657505(v=EXCHG.150)
ms:contentKeyID: 49895985
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar reglas de flujo de correo

 

_**Se aplica a:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Las reglas de flujo de correo, también denominadas reglas de transporte, se pueden usar para buscar condiciones específicas en mensajes que pasan a través de su organización y para realizar distintas acciones. En este tema se muestra cómo crear, copiar, ajustar el orden, habilitar o deshabilitar, eliminar, importar o exportar reglas, y cómo supervisar su uso.


> [!TIP]
> Para asegurarse de que las reglas funcionan de la forma esperada, asegúrese de probar cuidadosamente cada regla y las interacciones entre las reglas.



¿Le interesa ver escenarios donde se utilizan estos procedimientos? Vea los siguientes temas:

  - [Avisos de declinación de responsabilidades, firmas, pies de página o encabezados en toda la organización](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [Usar reglas de transporte para inspeccionar datos adjuntos de mensajes](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [Escenarios comunes de bloqueo de datos adjuntos](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)

  - [Usar reglas de flujo de correo para enrutar el correo electrónico en función de una lista de palabras, expresiones o patrones](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)

  - [Escenarios comunes de aprobación de mensajes](common-message-approval-scenarios-exchange-2013-help.md)

  - [Usar reglas de flujo de correo para que los mensajes puedan evitar Otros correos](use-mail-flow-rules-so-messages-can-bypass-clutter-exchange-2013-help.md)

  - [Procedimientos recomendados para configurar las reglas de flujo de correo](best-practices-for-configuring-mail-flow-rules-exchange-2013-help.md)

  - [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/es-es/library/jj919236\(v=exchg.150\))

  - [Utilice las reglas de transporte para configurar el filtrado de correo electrónico masivo](https://technet.microsoft.com/es-es/library/dn720438\(v=exchg.150\))

  - [Definir reglas para cifrar o descifrar mensajes de correo electrónico](https://go.microsoft.com/fwlink/p/?linkid=402846)

  - [Crear un remitente seguro en toda la organización o listas de remitentes bloqueados en Office 365](https://technet.microsoft.com/es-es/library/dn198251\(v=exchg.150\))

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Reglas de transporte" en [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md) (Exchange Server), o en [Permisos de características de Exchange Online](https://technet.microsoft.com/es-es/library/jj200673\(v=exchg.150\)).

  - Si una regla aparece como **versión 14**, significa que está basada en un formato de regla de flujo de correo de Exchange Server 2010. Todas las opciones están disponibles para estas reglas.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear una regla de flujo de correo

Para crear una regla de flujo de correo, puede configurar una directiva de prevención de pérdida de datos (DLP), crear una nueva regla o copiar una regla. Use el Centro de administración de Exchange (EAC) o el Shell de administración de Exchange.


> [!NOTE]
> Después de crear o modificar una regla de flujo de correo, esta puede tardar hasta 30 minutos en aplicarse al correo electrónico.



## Usar una directiva DLP para crear reglas de flujo de correo

Cada directiva DLP es una colección de reglas de flujo de correo. Después de crear la directiva DLP, puede ajustar las reglas mediante los procedimientos que se indican a continuación.

1.  Cree una directiva de DLP. Para obtener instrucciones, vea:
    
      - [Procedimientos de DLP de Exchange Server 2013](dlp-procedures-exchange-2013-help.md)
    
      - [Procedimientos de DLP de Exchange Online](dlp-procedures-exchange-2013-help.md)

2.  Modifique las reglas de flujo de correo creadas por la directiva DLP. Consulte Ver o modificar una regla de flujo de correo.

## Usar el EAC para crear una regla de flujo de correo

El EAC le permite crear reglas de flujo de correo desde cero, a partir de una plantilla o copiando una regla existente.

1.  Vaya a **Flujo de correo** \> **Reglas**.

2.  Cree la regla usando una de las siguientes opciones:
    
      - Para crear una regla a partir de una plantilla, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y seleccione una plantilla.
    
      - Para copiar una regla, seleccione la regla y después seleccione **Copiar**![Copiar icono](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "Copiar icono").
    
      - Para crear una nueva regla desde el principio, elija **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y después seleccione **Crear una nueva regla**.

3.  En el cuadro de diálogo **Nueva regla**, asigne un nombre a la regla y seleccione las condiciones y acciones para ella:
    
    1.  En **Aplicar esta regla si...**, seleccione la condición que quiera en la lista de condiciones disponibles.
        
          - Algunas condiciones requieren valores específicos. Por ejemplo, si selecciona la condición **El remitente es…**, debe especificar una dirección de remitente. Si va a agregar una palabra o frase, tenga en cuenta que no se permiten espacios finales.
        
          - Si la condición que desea no aparece o si necesita agregar excepciones, seleccione **Más opciones**. Se mostrarán las excepciones y condiciones adicionales.
        
          - Si no desea especificar una condición y desea que esta regla se aplique a todos los mensajes de su organización, seleccione la condición **\[Aplicar esta regla a todos los mensajes\]**.
    
    2.  En **Hacer lo siguiente...**, en la lista de acciones disponibles, seleccione la acción que quiera que la regla realice en los mensajes que cumplan los criterios.
        
          - Algunas de las acciones requieren la especificación de valores. Por ejemplo, si selecciona la condición **Reenviar el mensaje para su aprobación...**, deberá seleccionar un destinatario en la organización.
        
          - Si la condición que quiere no aparece en la lista, seleccione **Más opciones**. Se mostrarán condiciones adicionales.
    
    3.  Especifique cómo se mostrarán los datos que coinciden con la regla en los [informes de Prevención de pérdida de datos (DLP)](https://go.microsoft.com/fwlink/p/?linkid=402768) y en los [informes de reglas de transporte](https://go.microsoft.com/fwlink/p/?linkid=402769).
        
          - En **Auditar esta regla con nivel de gravedad**, seleccione el nivel de gravedad de la regla. En los informes de actividad de Office 365, las reglas de flujo de correo se agrupan por nivel de gravedad. El nivel de gravedad es simplemente un filtro que facilita el uso de los informes y que no afecta a la prioridad con la que se procesan las reglas.
            

            > [!NOTE]
            > Si desactiva la casilla <STRONG>Auditar esta regla con nivel de gravedad</STRONG>, las coincidencias con la regla no se mostrarán en los informes de regla.

    
    4.  Establecer el modo de la regla. Puede usar uno de los dos modos de prueba para probar la regla sin que afecte al flujo de correo. En ambos modos de prueba, cuando se cumplen las condiciones, se agrega una entrada al seguimiento de mensajes.
        
          - **Exigir**   Esta opción activa la regla e inicia el procesamiento de los mensajes inmediatamente. Se realizarán todas las acciones de la regla.
        
          - **Probar con sugerencias de directivas**   Activa la regla y se enviarán las acciones las sugerencias de directivas (**Notificar al remitente con una Sugerencia de directivas**) pero no se realizarán acciones relativas a la entrega de mensajes. Para usar este modo se necesita Prevención de pérdida de datos (DLP). Para obtener más información, vea [Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).
        
          - **Probar sin sugerencias de directivas**   Solo se aplicará la acción de generar informe de incidente. No se realizan acciones relacionadas con la entrega de mensajes.

4.  Si está conforme con la regla, vaya al paso 5. Si desea agregar más condiciones o acciones, o si desea especificar determinadas excepciones o establecer propiedades adicionales, haga clic en **Más opciones**. Después de hacer clic en **Más opciones**, complete los siguientes campos para crear la regla:
    
    1.  Para agregar más condiciones, haga clic en **Agregar condición**. Si tiene más de una condición, puede hacer clic en **Quitar X** junto a cada una de ellas para quitarlas. Tenga en cuenta que, cuando hace clic en **Más opciones**, hay una mayor variedad de condiciones disponibles.
    
    2.  Para agregar más acciones, haga clic en **Agregar acción**. Si tiene más de una acción, puede hacer clic en **Quitar X** junto a cada una de ellas para quitarlas. Tenga en cuenta que, cuando hace clic en **Más opciones**, hay una mayor variedad de acciones disponibles.
    
    3.  Para especificar excepciones, haga clic en **Agregar excepción** y luego seleccione excepciones en la lista desplegable **Excepto si...**. Para quitar cualquier excepción de la regla, puede hacer clic en **Quitar X** junto a cada una de ellas.
    
    4.  Si desea que esta regla entre en vigor después de una fecha determinada, haga clic en **Activar esta regla en la siguiente fecha:** y especifique una fecha. Tenga en cuenta que esta regla aún estará habilitada antes de esa fecha, pero no se procesará.
        
        De manera similar, puede detener el procesamiento de la regla en una fecha determinada. Para ello, haga clic en **Desactivar esta regla en la siguiente fecha:** y especifique una fecha. Tenga en cuenta que la regla permanecerá habilitada, pero no se procesará.
    
    5.  Puede elegir evitar aplicar reglas adicionales una vez que esta regla procesa un mensaje. Para ello, haga clic en **Detener el procesamiento de más reglas**. Si selecciona esto, y esta regla procesa un mensaje, no se procesan reglas posteriores para ese mensaje.
    
    6.  Puede especificar como se debería tratar el mensaje si no se puede completar el procesamiento de las reglas. De manera predeterminada, la regla se pasará por alto y el mensaje se procesará de forma regular, pero puede optar por volver a enviar el mensaje para su procesamiento. Para hacerlo, active la casilla **Aplazar el mensaje si no se completa el procesamiento de la regla**.
    
    7.  Si la regla analiza la dirección del remitente, solo examina los encabezados del mensaje de manera predeterminada. Sin embargo, puede configurar su regla para que también examine el sobre del mensaje SMTP. Para especificar lo que se examina, haga clic en uno de los siguientes valores de **Coincidir con la dirección del remitente en el mensaje**:
        
          - **Encabezado**   Solo se examinarán los encabezados de los mensajes.
        
          - **Sobre**   Solo se examinará el sobre del mensaje SMTP.
        
          - **Encabezado o sobre**   Se examinarán los encabezados del mensaje y el sobre del mensaje SMTP.
    
    8.  Puede agregar comentarios a esta regla en el cuadro **Comentarios**.

5.  Haga clic en **Guardar** para completar la creación de la regla.

## Usar el Shell de administración de Exchange para crear una regla de flujo de correo

En este ejemplo, se usa el cmdlet [New-TransportRule](https://technet.microsoft.com/es-es/library/bb125138\(v=exchg.150\)) para crear una nueva regla de flujo de correo que antepone "`External message to Sales DG:`" a los mensajes que se envían desde fuera de la organización al grupo de distribución del departamento de ventas.

    New-TransportRule -Name "Mark messages from the Internet to Sales DG" -FromScope NotInOrganization -SentTo "Sales Department" -PrependSubject "External message to Sales DG:"

Los parámetros de la regla y la acción que se usan en el procedimiento anterior son solamente a modo de ejemplo. Revise todas las acciones y las condiciones de la regla de flujo de correo disponibles para determinar cuáles se ajustan a sus requisitos.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la nueva regla de flujo de correo se creó correctamente, realice lo siguiente:

  - En el EAC, compruebe que la nueva regla de flujo de correo aparezca en la lista **Reglas**.

  - En el Shell de administración de Exchange, ejecute el siguiente comando para comprobar que la nueva regla de transporte se creó correctamente (en el ejemplo siguiente, se comprueba la regla creada en el ejemplo de Shell de administración de Exchange anterior):
    
        Get-TransportRule "Mark messages from the Internet to Sales DG"

## Ver o modificar una regla de flujo de correo


> [!NOTE]
> Después de crear o modificar una regla de flujo de correo, esta puede tardar hasta 30 minutos en aplicarse al correo electrónico.



## Usar el EAC para ver o modificar una regla de flujo de correo

1.  En el EAC, vaya a **Flujo de correo** \> **Reglas**.

2.  Cuando selecciona una regla de la lista, las condiciones, las acciones, las excepciones y las propiedades de selección de esa regla se muestran en el panel de detalles. Para ver todas las propiedades de una regla específica, haga doble clic en ella. Se abrirá la ventana del editor de reglas, donde puede realizar cambios a la regla. Para obtener más información sobre las propiedades de regla, vea la sección Usar el EAC para crear una regla de flujo de correo más arriba en este tema.

## Usar el Shell de administración de Exchange para ver o modificar una regla de flujo de correo

En el ejemplo siguiente, se muestra una lista de todas las reglas configuradas en su organización:

    Get-TransportRule

Para ver las propiedades de una regla de flujo de correo específica, proporcione el nombre de esa regla o su GUID. Generalmente, es útil enviar la salida al cmdlet **Format-List** para dar formato a las propiedades. En el ejemplo siguiente, se devuelven todas las propiedades de la regla de flujo de correo llamada **Sender is a member of Marketing**:

    Get-TransportRule "Sender is a member of marketing" | Format-List

Para modificar las propiedades de una regla existente, use el cmdlet [Set-TransportRule](https://technet.microsoft.com/es-es/library/bb123534\(v=exchg.150\)). Este cmdlet permite cambiar cualquier propiedad, condición, acción o excepción asociadas con una regla. En el ejemplo siguiente, se agrega una excepción a la regla "Sender is a member of marketing", de modo que no se aplicará a los mensajes enviados por el usuario Kelly Rollin:

    Set-TransportRule "Sender is a member of marketing" -ExceptIfFrom "Kelly Rollin"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la regla de flujo de correo se modificó correctamente, haga lo siguiente:

  - En la lista de reglas del EAC, haga clic en la regla que modificó en la lista **Reglas** y vea el panel de detalles.

  - En el Shell de administración de Exchange, ejecute el siguiente comando, que enumerará las propiedades modificadas junto con el nombre de la regla, para comprobar que modificó correctamente la regla de flujo de correo (en el ejemplo siguiente, se comprueba la regla modificada en el ejemplo de Shell de administración de Exchange anterior):
    
        Get-TransportRule "Sender is a member of marketing" | Format-List Name,ExceptIfFrom

## Propiedades de las reglas de flujo de correo

También puede usar el cmdlet Set-TransportRule para modificar reglas de transporte existentes en la organización. A continuación encontrará una lista de propiedades que no están disponibles en el EAC y que puede modificar. Para obtener más información sobre el uso del cmdlet Set-TransportRule para realizar estos cambios, consulte [Set-TransportRule](https://technet.microsoft.com/es-es/library/bb123534\(v=exchg.150\))


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de condición en el EAC</th>
<th>Nombre de condición en Shell de administración de Exchange</th>
<th>Propiedades</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Detener las reglas de procesamiento</strong></p></td>
<td><p><code>StopRuleProcessing </code></p></td>
<td><p><code> Not applicable</code></p></td>
<td><p>Le permite detener el procesamiento de reglas adicionales.</p></td>
</tr>
<tr class="even">
<td><p><strong>Coincidencia de encabezado y sobre</strong></p></td>
<td><p><code>SenderAddressLocation </code></p></td>
<td><p>No aplicable</p></td>
<td><p>Le permite examinar el sobre del mensaje SMTP para garantizar que la cabecera y el sobre coincidan.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><strong>Gravedad de auditoría</strong></p></td>
<td><p><code>SetAuditSeverity </code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>Permite seleccionar un nivel de gravedad de la auditoría.</p></td>
</tr>
<tr class="even">
<td><p><strong>Modos de regla</strong></p></td>
<td><p><code>Mode</code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>Le permite definir el modo para la regla.</p></td>
</tr>
</tbody>
</table>


## Establecer la prioridad de una regla de flujo de correo

La regla que está en la parte superior de la lista se procesa en primer lugar. Esta regla tiene una **Prioridad** de 0.

## Usar el EAC para establecer la prioridad de una regla

1.  En el EAC, vaya a **Flujo de correo** \> **Reglas**. Las reglas se muestran en el orden con el que se procesan.

2.  Seleccione una regla y use las flechas para subir o bajar la regla en la lista.

## Usar el Shell de administración de Exchange para establecer la prioridad de una regla

En el ejemplo siguiente se establece la prioridad de "Sender is a member of marketing" en 2:

    Set-TransportRule "Sender is a member of marketing" priority "2"

## ¿Cómo puedo saber si el proceso se ha completado correctamente?

Para comprobar que la regla de flujo de correo se modificó correctamente, haga lo siguiente:

  - En la lista de reglas en el EAC, examine el orden de las reglas.

  - En el Shell de administración de Exchange, compruebe la prioridad de las reglas (en el ejemplo siguiente se comprueba la regla modificada en el ejemplo anterior del Shell de administración de Exchange):
    
        Get-TransportRule * | Format-List Name,Priority

## Habilitar o deshabilitar una regla de flujo de correo

Las reglas de flujo de correo se habilitan en el momento de crearlas, pero puede deshabilitarlas.

## Usar el EAC para habilitar o deshabilitar una regla de flujo de correo

1.  En el EAC, vaya a **Flujo de correo** \> **Reglas**.

2.  Para deshabilitar una regla, desactive la casilla junto a su nombre.

3.  Para habilitar una regla deshabilitada, active la casilla de verificación junto a su nombre.

## Usar el Shell de administración de Exchange para habilitar o deshabilitar una regla de flujo de correo

En el ejemplo siguiente, se deshabilita la regla de flujo de correo “Sender is a member of marketing”:

    Disable-TransportRule "Sender is a member of marketing"

En el ejemplo siguiente, se habilita la regla de flujo de correo “Sender is a member of marketing”:

    Enable-TransportRule "Sender is a member of marketing"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la regla de flujo de correo se habilitó o deshabilitó correctamente, haga lo siguiente:

  - En el EAC, vea la lista de reglas en la lista **Reglas** y compruebe el estado de la casilla en la columna **ACTIVADO**.

  - En el Shell de administración de Exchange, ejecute el siguiente comando para obtener una lista de todas las reglas de la organización junto con su estado:
    
        Get-TransportRule | Format-Table Name,State

## Quitar una regla de flujo de correo

## Usar el EAC para quitar una regla de flujo de correo

1.  En el EAC, vaya a **Flujo de correo** \> **Reglas**.

2.  Seleccione la regla que desea quitar y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

## Usar el Shell de administración de Exchange para quitar una regla de flujo de correo

En el ejemplo siguiente, se quita la regla de flujo de correo “Sender is a member of marketing”:

    Remove-TransportRule "Sender is a member of marketing"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la regla de flujo de correo se quitó correctamente, haga lo siguiente:

  - En el EAC, vea las reglas en la lista **Reglas** y compruebe que la regla que quitó ya no aparece.

  - En el Shell de administración de Exchange, ejecute el siguiente comando y compruebe que la regla que quitó ya no esté enumerada:
    
        Get-TransportRule

## Supervisar el uso de las reglas

Si está usando Exchange Online o Exchange Online Protection, use un informe de regla para comprobar el número de veces que cada regla coincide. Para que se incluyan en los informes, una regla debe tener activada la casilla **Auditar esta regla con el nivel de gravedad**. Puede ver un informe en línea o descargar una versión de Excel de todos los informes de protección de correo.


> [!NOTE]
> Aunque la mayoría de los datos del informe son de las últimas 24 horas, algunos datos pueden tardar hasta 5 días en aparecer.



## Usar el Centro de administración de Office 365 para generar un informe de regla

1.  En el centro de administración de Office 365, seleccione **Informes**.

2.  En la sección **Reglas**, seleccione **coincidencias con las principales reglas para correo** o **coincidencias de regla para correo**.

Para obtener más información, vea [Ver informes de protección de correo](https://go.microsoft.com/fwlink/p/?linkid=402958).

## Descargar una versión de Excel de los informes

1.  En la página Informes del centro de administración de Office 365, seleccione **Informe de protección de correo electrónico (Excel)**.

2.  Si es la primera vez que usa los informes de protección de correo de Excel, se abre una pestaña con la página de descarga.
    
    1.  Seleccione **Descargar** para descargar el complemento Excel de Microsoft Office 365 para informes de Exchange Online.
    
    2.  Abra la descarga.
    
    3.  En el cuadro de diálogo **Instalación de Informes de protección de correo electrónico para Office 365**, seleccione **Siguiente**, acepte los términos del contrato de licencia y, después, seleccione **Siguiente**.
    
    4.  Seleccione el servicio que está usando y, después, seleccione **Siguiente**.
    
    5.  Compruebe los requisitos previos y, después, seleccione **Siguiente**.
    
    6.  Seleccione **Instalar**. En el escritorio se muestra un acceso directo a los informes.

3.  En el escritorio, seleccione **Informes de protección de correo electrónico de Office 365**.

4.  En el informe, seleccione la pestaña **Reglas**.

## Importar o exportar una colección de reglas de flujo de correo

Use el [Export-TransportRuleCollection](https://technet.microsoft.com/es-es/library/bb124410\(v=exchg.150\)) para importar o exportar una colección de reglas de flujo de correo. Para obtener información sobre cómo importar una colección de reglas de flujo de correo desde un archivo XML, vea Shell de administración de Exchange. Para obtener información sobre cómo exportar una colección de reglas de flujo de correo a un archivo XML, vea [Import-TransportRuleCollection](https://technet.microsoft.com/es-es/library/bb123582\(v=exchg.150\)).

## ¿Necesita más ayuda?

Recursos para Exchange Online:

[Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\))

[Excepciones (predicados) y las condiciones de la regla de flujo de correo en Exchange Online](https://technet.microsoft.com/es-es/library/jj919235\(v=exchg.150\))

[Enviar por correo las acciones de regla de flujo de Exchange Online](https://technet.microsoft.com/es-es/library/jj919237\(v=exchg.150\))

[Límites de las reglas de Bandeja de entrada y Transporte](https://go.microsoft.com/fwlink/p/?linkid=324584)

Recursos para Exchange Online Protection:

[Reglas de flujo de correo (reglas de transporte) en Exchange Online Protection](https://technet.microsoft.com/es-es/library/dn271424\(v=exchg.150\))

[Mail excepciones (predicados) y las condiciones de la regla de flujo de Exchange Online Protection](https://technet.microsoft.com/es-es/library/jj919234\(v=exchg.150\))

[Mail acciones de regla de flujo de Exchange Online Protection](https://technet.microsoft.com/es-es/library/jj920117\(v=exchg.150\))

[Límites de las reglas de Bandeja de entrada y Transporte](https://go.microsoft.com/fwlink/p/?linkid=324584)

Recursos para Exchange Server 2013:

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Acciones de regla de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

