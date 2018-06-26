---
title: 'Administrar las sugerencias de las directivas: Exchange 2013 Help'
TOCTitle: Administrar las sugerencias de las directivas
ms:assetid: cec50a35-1d00-47b3-b72f-ac1bb0fd630e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ619307(v=EXCHG.150)
ms:contentKeyID: 49116554
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar las sugerencias de las directivas

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Las sugerencias de directiva son avisos informativos que se muestran a los remitentes de correo electrónico mientras crean un mensaje. El propósito de la sugerencia de directiva es indicar a los usuarios que pueden estar infringiendo las directivas o prácticas empresariales que se exigen con las directivas de prevención de pérdida de datos (DLP) establecidas. Los siguientes procedimientos lo ayudarán a comenzar a usar las sugerencias de directiva. Vea este vídeo para obtener más información.

> [!VIDEO https://www.microsoft.com/es-es/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 30 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Prevención de pérdida de datos (DLP)" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Las sugerencias de directivas solo se mostrarán para remitentes de correo electrónico si se cumplen las siguientes condiciones:
    
    1.  El programa cliente de mensajes del remitente es Microsoft Outlook 2013. Si su organización implementó Exchange 2013 SP1 o usa Exchange Online, las sugerencias de directivas también se muestran en Outlook Web App y OWA para dispositivos.
    
    2.  Existe una regla de transporte que invoca las notificaciones de la sugerencia de directiva. Puede crear dicha regla de transporte al configurar la directiva de DLP que incluya la acción de **Notificar al remitente con una sugerencia de directiva**.
    
    3.  El contenido del encabezado de un mensaje, el cuerpo del mensaje o los archivos adjuntos del mensaje que examina el agente de transporte cumplen con las condiciones establecidas en las reglas o directivas de DLP, que también incluyen las reglas de notificación de la sugerencia de directiva. En otras palabras, la sugerencia de directiva solo se muestra para usuarios finales si realizan alguna acción que hace que se aplique la regla asociada.

  - El texto de notificación predeterminado de la sugerencia de directiva que se genera en el sistema se mostrará si no usa la característica de configuración de la sugerencia de directiva para personalizar el texto de dicha sugerencia. Para obtener más información acerca del texto predeterminado, consulte [Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear o modificar una sugerencia de directiva solo de notificación

Mediante este procedimiento se muestra una sugerencia de directiva informativa a un remitente de correo electrónico si se cumplen las condiciones de una regla específica. En Microsoft Outlook, el remitente puede evitar que se muestre esta sugerencia al usar el cuadro de diálogo de opciones de sugerencias de directiva. Para configurar el texto de la sugerencia de directiva personalizado, consulte Crear texto de notificación de la sugerencia de directiva.

## Usar el EAC para configurar sugerencias de directiva solo de notificación

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención de la pérdida de datos**.

2.  Haga doble clic en una de las directivas que aparecen en la lista de directivas o resalte un elemento y seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Editar directiva de DLP**, seleccione **Reglas**.

4.  Para agregar sugerencias de directiva a una regla existente, resalte la regla y seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    Para agregar una nueva regla en blanco que puede personalizar totalmente, seleccione **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y luego **Crear una nueva regla**.

5.  En **Aplicar esta regla si**, seleccione **El mensaje contiene información confidencial**. Esta condición es necesaria.

6.  Seleccione ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"), elija los tipos de información confidencial y seleccione **Agregar**, **Aceptar** y de nuevo **Aceptar**.

7.  En el cuadro **Realizar lo siguiente**, seleccione **Notificar al remitente con una sugerencia de directiva** y elija una opción de la lista desplegable **Elegir si el mensaje se bloquea o puede enviarse** y luego seleccione **Aceptar**.

8.  Si desea agregar otras condiciones o acciones, en la parte inferior de la ventana, seleccione **Más opciones**.
    

    > [!NOTE]
    > Solo se pueden usar las siguientes condiciones: 
    > <UL>
    > <LI>
    > <P><STRONG>SentTo (El destinatario es)</STRONG></P>
    > <LI>
    > <P><STRONG>SentToScope (El destinatario está ubicado)</STRONG></P>
    > <LI>
    > <P><STRONG>From (El remitente es)</STRONG></P>
    > <LI>
    > <P><STRONG>FromMemberOf (El remitente es un miembro de)</STRONG></P>
    > <LI>
    > <P><STRONG>FromScope (El remitente está ubicado)</STRONG></P></LI></UL>No se pueden usar las siguientes acciones: 
    > <UL>
    > <LI>
    > <P><STRONG>RejectMessageReasonText (Rechazar el mensaje e incluir una explicación)</STRONG></P>
    > <LI>
    > <P><STRONG>RejectMessageEnhancedStatusCode (Rechazar el mensaje con el código de estado mejorado de)</STRONG></P>
    > <LI>
    > <P><STRONG>DeletedMessage (Eliminar el mensaje sin notificarlo a nadie)</STRONG></P></LI></UL>



9.  En la lista **Elegir un modo para esta regla**, seleccione si quiere que la regla se exija. Se recomienda probar primero la regla.

10. Seleccione **Guardar** para terminar de modificar la regla y guardar los cambios.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que creó correctamente una sugerencia de directiva que solo notificará a un remitente, siga estos pasos:

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención de la pérdida de datos**.

2.  Seleccione la directiva que espera que contenga un mensaje de notificación.

3.  Seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") y luego **Reglas**.

4.  Seleccione la regla específica que espera que contenga un mensaje de notificación.

5.  Confirme que la acción **Notificar al remitente** aparece en la parte inferior del resumen de reglas.

## Crear o modificar una sugerencia de directiva de bloqueo de mensajes

Mediante este procedimiento se muestra una sugerencia de directiva a un remitente de correo electrónico que indica que un mensaje fue rechazado y que no se entregará hasta que la condición problemática se haya resuelto. Se proporciona al remitente una opción para indicar si el mensaje de correo electrónico no incluye la condición problemática. Esto también se conoce como anulación de falso positivo. Si el remitente indica esto, el mensaje puede salir de la bandeja de salida y se debe auditar el informe del usuario. Sin embargo, Exchange bloqueará el mensaje y no podrá enviarse. Para configurar el texto de la sugerencia de directiva personalizado, consulte Crear texto de notificación de la sugerencia de directiva.

## Usar el EAC para configurar sugerencias de directiva de bloqueo de mensajes

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención de la pérdida de datos**.

2.  Haga doble clic en una de las directivas que aparecen en la lista de directivas o resalte un elemento y seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Editar directiva de DLP**, seleccione **Reglas**.

4.  Para agregar sugerencias de directiva a una regla existente, resalte la regla y seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

5.  Para agregar una nueva regla en blanco que puede personalizar totalmente, seleccione **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

6.  Para agregar una acción que revele una sugerencia de directiva, seleccione **Más opciones…** y luego el botón **Agregar acción**.

7.  Desde la lista desplegable, seleccione **Notificar al remitente con una sugerencia de directiva** y luego, **Bloquear el mensaje**.

8.  Seleccione **Aceptar** y luego **Guardar** para terminar de modificar la regla y guardar los cambios.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó correctamente una sugerencia de directiva de rechazo de mensajes, haga lo siguiente:

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención de la pérdida de datos**.

2.  Seleccione una vez para resaltar la directiva que espera que contenga un mensaje de notificación.

3.  Seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") y luego **Reglas**.

4.  Seleccione una vez para resaltar la regla concreta que espera que contenga un mensaje de notificación.

5.  Confirme que la acción **Notificar al remitente que no se puede enviar el mensaje** aparece en la parte inferior del resumen de reglas.

## Crear o modificar una sugerencia de directiva de bloqueo salvo anulación

Hay cuatro opciones para las sugerencias de directiva que pueden rechazar mensajes o evitar que los mensajes salgan de la bandeja de salida del remitente. Para obtener más información sobre estas opciones, consulte [Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Usar el EAC para configurar sugerencias de directiva de bloqueo salvo anulación

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención de la pérdida de datos**.

2.  Haga doble clic en una de las directivas que aparecen en la lista de directivas o resalte un elemento y seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Editar directiva de DLP**, seleccione **Reglas**.

4.  Para agregar sugerencias de directiva a una regla existente, resalte la regla y seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    Para agregar una nueva regla en blanco que puede personalizar totalmente, seleccione **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y luego **Más opciones…**.

5.  Para agregar la acción que revelará una sugerencia de directiva, seleccione el botón **Agregar acción**.

6.  Desde la lista desplegable, seleccione **Notificar al remitente con una sugerencia de directiva** y luego, **Bloquear el mensaje, pero permitir al remitente invalidarlo y enviarlo**.

7.  Seleccione **Aceptar** y luego **Guardar** para terminar de modificar la regla y guardar los cambios.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó correctamente una sugerencia de directiva de rechazo salvo anulación, haga lo siguiente:

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención de la pérdida de datos**.

2.  Seleccione una vez para resaltar la directiva que espera que contenga un mensaje de notificación.

3.  Seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") y luego **Reglas**.

4.  Seleccione una vez para resaltar la regla concreta que espera que contenga un mensaje de notificación.

5.  Confirme que la acción **Bloquear el mensaje, pero permitir al remitente invalidarlo y enviarlo** aparece en la parte inferior del resumen de reglas.

## Crear texto de notificación de la sugerencia de directiva

Este procedimiento opcional lo ayudará a personalizar el texto de notificación de la sugerencia de directiva que los remitentes de correo electrónico ven en el programa de correo electrónico. Si sigue este procedimiento, el texto de notificación de la sugerencia de directiva no aparecerá a menos que también configure una regla de directiva de DLP con una acción que hará que se muestre la notificación. Tenga en cuenta que el sistema incluye notificaciones de sugerencias de directiva predeterminadas que pueden aparecer si no personaliza el texto de notificación de la sugerencia de directiva. Para obtener más información acerca del texto predeterminado, consulte [Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Usar el EAC para crear y administrar el texto de notificación de la sugerencia de directiva personalizado

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención de la pérdida de datos**.

2.  Seleccione **Configuración de sugerencias de directivas**![Configuración de sugerencia de directiva](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Configuración de sugerencia de directiva").

3.  Para agregar una nueva sugerencia de directiva con un mensaje personalizado, seleccione **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para obtener más información sobre las opciones de acción disponibles, consulte [Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).
    
    Para modificar una sugerencia de directiva existente, resáltela y seleccione **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    Para eliminar una sugerencia de directiva existente, resáltela y seleccione **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono") y luego confirme la acción.

4.  Seleccione **Guardar** para terminar de modificar la sugerencia de directiva y guardar los cambios.

5.  Seleccione **Cerrar** para terminar de administrar las sugerencias de directiva y guardar los cambios.

## Usar el Shell para crear el texto de notificación de la sugerencia de directiva personalizado

En el siguiente ejemplo se crea una nueva sugerencia de directiva en inglés que bloqueará un mensaje para que no salga. El texto de esta sugerencia de directiva personalizada se cambia al valor siguiente: "Este mensaje parece incluir contenido restringido y no será entregado."

    New-PolicyTipConfig -Name en\Reject -Value "This message appears to contain restricted content and will not be delivered."

Para obtener más información acerca de los cmdlets DLP, consulte [Cmdlets de directiva y conformidad](https://technet.microsoft.com/es-es/library/dd298082\(v=exchg.150\)).

## Usar el Shell para modificar el texto de notificación de la sugerencia de directiva personalizado

En el siguiente ejemplo se modifica una sugerencia de directiva existente en inglés solo de notificación. El texto de esta Sugerencia de directiva personalizada se cambió a "No se recomienda enviar números de cuentas bancarias por correo electrónico".

    Set-PolicyTipConfig en\NotifyOnly "Sending bank account numbers in email is not recommended."

Para obtener más información acerca de los cmdlets DLP, consulte [Cmdlets de directiva y conformidad](https://technet.microsoft.com/es-es/library/dd298082\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó correctamente el texto de la sugerencia de directiva personalizado, haga lo siguiente:

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención de la pérdida de datos**.

2.  Seleccione **Configuración de sugerencias de directivas**![Configuración de sugerencia de directiva](images/JJ619307.54d1813d-3289-4765-a9a3-a7303a5ab3c7(EXCHG.150).gif "Configuración de sugerencia de directiva").

3.  Seleccione **Actualizar**![Icono Actualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icono Actualizar").

4.  Confirme que la acción, la configuración regional y el texto para esa configuración regional aparecen en la lista.

## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Sugerencias de directiva](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange 2013

[Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\))Exchange Online

[Sugerencias de correo electrónico de Exchange 2010](https://go.microsoft.com/fwlink/?linkid=265179)

