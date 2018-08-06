---
title: 'Ver las propiedades de mensajes en cola en Visor de cola: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Ver las propiedades de mensajes en cola en el Visor de cola
ms:assetid: 9d15d8b8-e061-4288-9354-df58e282fb6b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123934(v=EXCHG.150)
ms:contentKeyID: 49895802
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.Edge.SystemManager.MessagePropertyPage
ms.translationtype: MT
---

# Ver las propiedades de mensajes en cola en el Visor de cola

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-01-17_

El Visor de cola se utiliza en el cuadro de herramientas de Exchange para ver las propiedades de un mensaje que está en cola para la entrega.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Colas" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - También puede usar el cmdlet Get-Message en el Shell de administración de Exchange para ver propiedades del mensaje adicionales que no son visibles en el Visor de cola. Para obtener más información, consulte [Filtros de mensajes](message-filters-exchange-2013-help.md) y [Uso del Shell de administración de Exchange para administrar colas](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Visor de cola del cuadro de herramientas de Exchange para ver las propiedades de un mensaje

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **herramientas de flujo de correo**, haga doble clic en **Visor de cola** para abrir la herramienta en una ventana nueva.

3.  En Visor de cola, seleccione la pestaña **Mensajes** para ver la lista de mensajes que están actualmente en cola para la entrega en la organización.

4.  Haga clic con el botón secundario del mouse en las propiedades que desea ver y, a continuación, seleccione **Propiedades**.

5.  La ficha **General** muestra la siguiente información detallada acerca del mensaje:
    
      - **Identidad**   Este campo muestra el entero que representa un mensaje en particular. La base de datos de cola asigna la identidad del mensaje cuando éste se recibe para su procesamiento. Puede incluir una identidad de servidor y de cola opcionales para identificar una copia única del mensaje.
    
      - **Asunto**   Este campo muestra el asunto de un mensaje y se expresa como una cadena de texto. Este valor se obtiene del campo de encabezado `Subject:`.
    
      - **Id. de mensaje de Internet**   Este campo muestra el valor del campo del encabezado `MessageID:`. El valor de esta propiedad se expresa como un GUID seguido por la dirección SMTP del servidor de envío, como en este ejemplo: 67D754D6103DC4FB3BA6BC7205DACABA61231@exchange.contoso.com
    
      - **Dirección remitente**   Este campo muestra la dirección SMTP del remitente del mensaje. Este valor se toma de MAIL FROM: en el sobre del mensaje.
    
      - **Estado**   Este campo muestra el estado actual de los mensajes. Un mensaje puede tener uno de los siguientes estados:
        
          - **Activo** Si el mensaje está en una cola de entrega, se entregará a su destino. Si el mensaje está en la cola de envío, el categorizador lo está procesando.
        
          - **Eliminar pendientes**   El administrador eliminó el mensaje, pero ya se estaba entregando. Si la entrega acaba con un error que provoca que el mensaje vuelva a entrar en la cola, este se eliminará. De lo contrario, se proseguirá con la entrega.
        
          - **Suspender pendientes**   El administrador suspendió el mensaje, pero ya se estaba entregando. Si la entrega acaba con un error que provoca que el mensaje vuelva a entrar en la cola, este se suspenderá. De lo contrario, se proseguirá con la entrega.
        
          - **Ready**   El mensaje está aguardando en la cola y está listo para su procesamiento.
        
          - **Retry**   Error del último intento de conexión en la cola en la que está ubicado este mensaje. El mensaje está esperando el siguiente reintento de cola.
        
          - **Suspendido**   El administrador ha suspendido el mensaje.
    
      - **Tamaño (KB)**   Este campo muestra el tamaño del mensaje redondeando al kilobyte más cercano (KB).
    
      - **Nombre de origen del mensaje**   Este campo muestra el nombre del componente que ha enviado este mensaje a la cola.
    
      - **IP de origen**   Este campo muestra la dirección IP del servidor externo que ha enviado el mensaje a la organización de Exchange.
    
      - **SCL**   Este campo muestra la clasificación de confianza de correo no deseado (SCL) del mensaje. Las entradas SCL válidas son enteros del 0 al 9. o -1. Una entrada SCL vacía indica que el agente de filtrado de contenido no ha procesado el mensaje.
    
      - **Fecha de recepción**   Este campo muestra la fecha y hora en la que el mensaje se ha recibido en el servidor que contiene la cola en la que está ubicado dicho mensaje.
    
      - **Fecha de expiración**   Este campo muestra la fecha y la hora en que expira el mensaje y se eliminará de la cola en caso de que no se pueda entregar.
    
      - **Último error**   Este campo muestra el último error registrado para un mensaje.
    
      - **Id. de cola**   Este campo muestra la identidad de la cola que almacena el mensaje. La identidad de la cola se expresa con el formato *Servidor/destino*, donde *destino* es un nombre de dominio remoto, servidor de buzones o cola persistente, o el identificador de la base de datos de cola. El identificador de la base de datos de cola se representa como un entero y se puede determinar mediante la visualización de las propiedades de los mensajes.
    
      - **Destinatarios**   Este campo muestra la lista de destinatarios a los cuales está dirigido el mensaje.
    
      - **Número de reintentos**   Este campo muestra el número de veces que se ha intentado entregar un mensaje a un destino.

6.  La ficha **Información de los destinatarios** muestra la siguiente información acerca de los destinatarios del mensaje:
    
      - **Dirección**   Este campo muestra la dirección SMTP del destinatario del mensaje. Este valor se obtiene de `RCPT TO:` en el sobre del mensaje.
    
      - **Estado**   Este campo muestra el estado actual de los mensajes. Un mensaje puede tener uno de los siguientes estados:
        
          - **Activo** Si el mensaje está en una cola de entrega, se entregará a su destino. Si el mensaje está en la cola de envío, el categorizador lo está procesando.
        
          - **Eliminar pendientes**   El administrador ha eliminado el mensaje, pero ya se estaba entregando. Si la entrega acaba con un error que provoca que el mensaje vuelva a entrar en la cola, este se eliminará. De lo contrario, se proseguirá con la entrega.
        
          - **Suspender pendientes**   El administrador ha suspendido el mensaje, pero ya se estaba entregando. Si la entrega acaba con un error que provoca que el mensaje vuelva a entrar en la cola, este se suspenderá. De lo contrario, se proseguirá con la entrega.
        
          - **Ready**   El mensaje está aguardando en la cola y está listo para su procesamiento.
        
          - **Retry**   Error del último intento de conexión en la cola en la que está ubicado este mensaje. El mensaje está esperando el siguiente reintento de cola.
        
          - **Suspendido**   El administrador ha suspendido el mensaje.
    
      - **Último error**   Este campo muestra el último error registrado para un mensaje.

## Usar el Shell para ver las propiedades de un mensaje

Puede usar el cmdlet **Get-Message** para ver las propiedades de un mensaje que actualmente está en cola para la entrega. En el siguiente ejemplo se tabula información de la dirección del remitente, los destinatarios, el asunto y la fecha de recepción para todos los mensajes que actualmente están en estado de reintento:

    Get-Message -IncludeRecipientInfo -Filter {Status -eq "Retry"} | Format-Table FromAddress,Recipients,Subject,DateReceived

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-Message](https://technet.microsoft.com/es-es/library/bb124738\(v=exchg.150\)).

