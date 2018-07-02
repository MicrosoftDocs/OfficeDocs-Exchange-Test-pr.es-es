---
title: 'Seguimiento de mensajes con informes de entrega: Exchange 2013 Help'
TOCTitle: Seguimiento de mensajes con informes de entrega
ms:assetid: a14e4e62-08ca-4a7b-92e1-d39fe3e0a9e5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150554(v=EXCHG.150)
ms:contentKeyID: 48268499
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Seguimiento de mensajes con informes de entrega

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-13_

Informes de entrega es una herramienta de seguimiento de mensajes del Centro de administración de Exchange (EAC) que puede utilizar para buscar el estado de la entrega en los mensajes de correo electrónico con respecto a su envío o recepción por parte de los usuarios en la libreta de direcciones de la organización, con un asunto determinado. Puede realizar el seguimiento de la información de entrega de los mensajes enviados desde un buzón de correo específico de la organización o recibidos desde dicho buzón. En un informe de entrega no se recupera el contenido del cuerpo del mensaje, pero la línea de asunto se muestra en los resultados. Puede realizar el seguimiento de los mensajes hasta 14 días después del envío o de la recepción.


> [!NOTE]
> Informes de entrega realiza el seguimiento de los mensajes enviados por los usuarios mediante los clientes de correo electrónico de Microsoft Outlook u Outlook Web App. No realiza el seguimiento de los mensajes enviados desde clientes de correo POP o IMAP, como Windows Mail, Outlook Express o Mozilla Thunderbird.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: El tiempo para completar variará según el alcance de la búsqueda.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Seguimiento de mensajes" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## ¿Qué desea hacer?

Utilice el EAC para seguimiento de los mensajes

Utilice el EAC para revisar un informe de entrega

## Utilice el EAC para seguimiento de los mensajes

1.  En el EAC, navegue a **Flujo de correo** \> **Informes de entrega**.

2.  Escriba la información siguiente:
    
      - **\* Buzón para buscar:**  Haga clic en **Examinar** para seleccionar el buzón en la libreta de direcciones y luego haga clic en **Aceptar**. Es preciso seleccionar el buzón de correo donde se va a buscar.
    
      - Seleccione una de las siguientes opciones:
        
          - **Buscar mensajes enviados a**Use esta opción para buscar los mensajes enviados a usuarios específicos. Haga clic en **Seleccionar usuarios** y, a continuación, elija los usuarios en la libreta de direcciones seleccionando a un usuario en la lista y haciendo clic en **Agregar**. Aquí puede seleccionar a más de un usuario. Cuando haya terminado de seleccionar a los usuarios, haga clic en **Aceptar** para volver a la página **Informes de entrega**. Si selecciona esta opción, también puede dejar el campo vacío para buscar mensajes enviados a cualquier usuario.
        
          - **Buscar mensajes recibidos de** Utilice esta opción para buscar los mensajes que se hayan recibido de un usuario determinado. Nuevamente, seleccione solo el usuario de la libreta de direcciones y haga clic en **Aceptar** para volver a la página **Informes de entrega**. Si selecciona esta opción, tiene que especificar un remitente.
    
      - **Buscar estas palabras en la línea de asunto**Escriba aquí la información de la línea de asunto o déjelo en blanco para ampliar la búsqueda.

3.  Cuando haya terminado, haga clic en **Buscar**. Si desea volver a empezar, haga clic en **Borrar**.

## Utilice el EAC para revisar un informe de entrega

Para visualizar la información sobre la entrega, seleccione un mensaje en el panel **Resultados de la búsqueda** y haga clic en **Detalles**.

En el informe de entrega se indica el estado de la entrega y se incluye información detallada sobre la entrega del mensaje seleccionado en el panel **Resultados de la búsqueda**. En la parte superior del informe, aparecen los campos siguientes:

  - **Asunto   **La línea de asunto del mensaje aparece como encabezado del informe.

  - **De   **Alias, nombre para mostrar o dirección de correo electrónico de la persona que envió el mensaje.

  - **Para**   Alias, nombre para mostrar o dirección de correo electrónico del destinatario del mensaje.

  - **Enviado el   **Fecha y hora en que se envió el mensaje.

## Sección Resumen hasta la fecha

Esta sección aparece en el informe de entrega cuando un mensaje se envió a varias personas o destinatarios. En la parte superior de esta sección se indica el número total de destinatarios a los que se envió el mensaje y aparece una breve descripción de la entrega a cada destinatario.

  - **Resumen hasta la fecha   **Aquí se indica el número total de destinatarios y si los mensajes tienen el estado Pendiente, Entregado o Incorrecto. Haga clic en los hipervínculos para ordenar la información en función del estado.

  - **Cuadro de búsqueda**   El cuadro de búsqueda resulta útil cuando el mensaje se envía a un grupo formado por más de 30 destinatarios. En el cuadro de búsqueda, escriba la dirección de correo electrónico cuya información sobre la entrega desee consultar y haga clic en el icono de lupa.

  - **Para   **Muestra la dirección de correo electrónico del destinatario.

  - **Estado   **En esta columna, se muestra el estado del mensaje de cada destinatario.

## Información detallada del informe

Esta sección contiene información detallada sobre la entrega del mensaje enviado al destinatario que seleccionó en la sección Resumen hasta la fecha.

  - **Informe de entrega para**   Aquí aparece la dirección de correo electrónico del destinatario seleccionado.

  - **Enviado**   Fecha y hora en que el sistema envió el mensaje para su entrega.

En función del estado de entrega del mensaje, pueden verse una variedad de estados, entre ellos:

  - **Entregado   **Indica que la entrega se realizó correctamente.

  - **Aplazado   **Indica que el mensaje se retrasó.

  - **Pendiente   **Si la entrega del mensaje está pendiente porque el mensaje satisface los criterios de una regla o directiva que se aplica a toda la organización o porque está sujeto a la aprobación de mensajes, el mensaje de estado indica la acción que está realizando una regla o que el mensaje debe ser aprobado por un moderador antes de su entrega.

  - **Moderador**   El estado indica si el moderador aprobó o rechazó el mensaje.

  - **Grupo expandido   **Si se envió un mensaje a un grupo, cada uno de los usuarios aparece en la sección **Resumen hasta la fecha** a fin de que pueda ver el estado de entrega para cada destinatario. Si necesita quitar un usuario de un grupo o agregarlo mientras examina el informe de entrega, haga clic en **Editar grupos** para poder modificar los grupos.

  - **Error**   Muestra la fecha, la hora y el motivo de un error de entrega de un mensaje. Por ejemplo, puede haber una regla que afecte a toda la organización que impida la entrega del mensaje o puede que el mensaje no pudiera entregarse.

Cuando termine de revisar el informe, haga clic en **Cerrar**. Los informes de entrega no se guardan, pero pueden ejecutarse de nuevo en cualquier momento. Recuerde que hay una ventana de búsqueda de dos semanas.

## ¿Cómo saber si el proceso se ha completado correctamente?

Si la búsqueda se ha realizado con éxito, los mensajes que cumplen los criterios de búsqueda aparecen en el panel **Resultados de la búsqueda**. Para ver la información de la entrega para el mensaje específico, seleccione un elemento y haga clic en **Detalles**. Si no se muestra ningún mensaje en el panel **Resultados de la búsqueda**, cambie los criterios de búsqueda y vuelva a realizar la búsqueda.

