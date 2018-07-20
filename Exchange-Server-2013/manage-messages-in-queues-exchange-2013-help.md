---
title: 'Administrar mensajes en colas: Exchange 2013 Help'
TOCTitle: Administrar mensajes en colas
ms:assetid: 83358884-6036-4e91-87a8-35200541874d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123535(v=EXCHG.150)
ms:contentKeyID: 51406521
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar mensajes en colas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-05-07_

En Microsoft Exchange Server 2013, puede usar el Visor de cola del Cuadro de herramientas de Exchange o el Shell de administración de Exchange para administrar los mensajes en cola. Para obtener más información acerca del uso de los cmdlets de administración de mensajes en el Shell de administración de Exchange, consulte [Uso del Shell de administración de Exchange para administrar colas](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada «Colas» en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Quitar mensajes de las colas

Un mensaje que se está enviando a varios destinatarios puede estar ubicado en más de una cola. Para quitar un mensaje de más de una cola en una única operación, debe usar un filtro. Puede seleccionar si enviar un informe de no entrega (NDR) cuando quita mensajes de una cola. No puede quitar un mensaje de la cola Envío.

## Usar el Visor de cola del Cuadro de herramientas de Exchange para quitar mensajes

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **herramientas de flujo de correo**, haga doble clic en **Visor de cola** para abrir la herramienta en una ventana nueva.

3.  En el Visor de cola, haga clic en la ficha **Mensajes**. Se muestra una lista de todos los mensajes del servidor al que está conectado. Para ajustar la acción a una cola única, haga clic en la ficha **Colas**, haga doble clic en el nombre de la cola y, a continuación, haga clic en la ficha *Servidor\\Cola* que aparece.

4.  Seleccione uno o más mensajes de la lista, haga clic con el botón secundario y, a continuación, seleccione **Quitar mensajes (con NDR)** o **Quitar mensajes (sin NDR)**. Aparece un cuadro de diálogo que confirma la acción seleccionada y pregunta, **¿Desea continuar?** Haga clic en **Sí**.

5.  Para quitar todos los mensajes de una cola en concreto, haga clic en la ficha **Colas**. Seleccione una cola, haga clic con el botón secundario y seleccione **Quitar mensajes (con NDR)** o **Quitar mensajes (sin NDR)**. Aparece un cuadro de diálogo que confirma la acción seleccionada y pregunta, **¿Desea continuar?** Haga clic en **Sí**.
    

    > [!NOTE]
    > Si usa una lista diferente, la página mostrada puede no incluir todos los elementos en el filtro. En este caso, aparece un mensaje que muestra: <STRONG>Esta acción afectará a todos los elementos de esta página. Para expandir el ámbito de esta acción y que incluya todos los elementos en este filtro, seleccione la siguiente casilla antes de hacer clic en Aceptar.</STRONG>



## Usar el Shell para quitar mensajes

Para quitar mensajes de las colas, utilice la sintaxis siguiente.

    Remove-Message <-Identity MessageIdentity | -Filter {MessageFilter}> -WithNDR <$true | $false>

En este ejemplo, los mensajes se quitan de las colas que tienen un asunto "Win Big" sin enviar un NDR.

    Remove-Message -Filter {Subject -eq "Win Big"} -WithNDR $false

En este ejemplo se quita el mensaje con el identificador de mensaje 3 de la cola inaccesible del servidor denominado Mailbox01 y se envía un NDR.

    Remove-Message -Identity Mailbox01\Unreachable\3 -WithNDR $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que los mensajes se quitaron correctamente de las colas, siga uno de estos pasos:

  - En el Visor de cola, seleccione la cola o cree un filtro para comprobar que el mensaje ya no existe.

  - Use el cmdlet **Get-Message** con los parámetros *Queue* o *Filter* para comprobar que los mensajes ya no existen. Para obtener más información, consulte [Get-Message](https://technet.microsoft.com/es-es/library/bb124738\(v=exchg.150\)).

## Reanudar mensajes en cola

Es posible reanudar cualquier mensaje que esté en estado Suspendido. Al reanudar un mensaje, se habilita su entrega. Si reanuda un mensaje que está ubicado en la cola de mensajes dudosos, el mensaje se enviará al categorizador para su procesamiento. Un mensaje que se envía a varios destinatarios puede estar ubicado en diferentes colas. Para restaurar un mensaje en más de una cola en una sola operación, debe usar un filtro.

## Usar el Visor de cola del Cuadro de herramientas de Exchange para reanudar mensajes

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **herramientas de flujo de correo**, haga doble clic en **Visor de cola** para abrir la herramienta en una ventana nueva.

3.  En el Visor de cola, haga clic en la ficha **Mensajes**. Se muestra una lista de todos los mensajes del servidor al que está conectado. Para ajustar la acción de modo que se centre en una única cola, haga clic en la ficha **Colas**, haga doble clic en el nombre de la cola y, a continuación, haga clic en la ficha *Servidor\\Cola* que se muestra.

4.  Haga clic en **Crear filtro** y especifique la expresión de filtro de la siguiente forma:
    
    1.  Seleccione **Estado** en la lista desplegable de propiedades del mensaje.
    
    2.  Seleccione **Es igual a** en la lista desplegable del operador de comparación.
    
    3.  Seleccione **Suspendido** en la lista desplegable de valores.

5.  Haga clic en **Aplicar filtro**. Se muestran todos los mensajes que tengan el estado Suspendido.

6.  Seleccione uno o más mensajes de la lista, haga clic con el botón secundario y, a continuación, seleccione **Reanudar**.

## Usar el Shell para reanudar mensajes

Para reanudar mensajes, use la sintaxis siguiente:

    Resume-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

En este ejemplo, se reanudan todos los mensajes enviados por cualquier remitente en el dominio Contoso.com.

    Resume-Message -Filter {FromAddress -eq "*contoso.com"}

En este ejemplo, se reanuda el mensaje con el identificador de mensaje 3 en la cola inalcanzable en el servidor Hub01.

    Resume-Message -Identity Hub01\Unreachable\3

Para reenviar mensajes de la cola de mensajes dudosos, siga los pasos siguientes:

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que los mensajes se han reanudado correctamente en las colas, siga uno de estos pasos:

  - En el Visor de cola, seleccione la cola o cree un filtro para comprobar que los mensajes ya no están suspendidos.

  - Use el cmdlet **Get-Message** con los parámetros *Queue* o *Filter* para comprobar que los mensajes ya no están suspendidos. Para obtener más información, consulte [Get-Message](https://technet.microsoft.com/es-es/library/bb124738\(v=exchg.150\)).

Tenga en cuenta que si no puede encontrar el mensaje en ninguna cola del servidor es probable que el mensaje se haya entregado correctamente al próximo salto.

## Suspender mensajes en colas

Cuando suspende un mensaje impide que éste se entregue. No se suspenderá un mensaje que aparece en la cola y que ya fue entregado. La entrega continuará y el estado del mensaje será **PendingSuspend**. Si la entrega no se puede realizar, el mensaje volverá a la cola y, a continuación, se suspenderá. Los mensajes que están en las colas de envío o de mensajes dudosos no se pueden suspender.

Un mensaje que se envía a varios destinatarios puede estar ubicado en diferentes colas. Para suspender un mensaje en más de una cola en una única operación, debe usar un filtro.

## Usar el Visor de cola del Cuadro de herramientas de Exchange para suspender mensajes

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **herramientas de flujo de correo**, haga doble clic en **Visor de cola** para abrir la herramienta en una ventana nueva.

3.  En el Visor de cola, haga clic en la ficha **Mensajes**. Se muestra una lista de todos los mensajes del servidor al que está conectado. Para limitar la vista a una sola cola, haga clic en la ficha **Colas**, haga doble clic en el nombre de la cola y, a continuación, haga clic en la ficha *Servidor\\Cola* que aparece.

4.  Seleccione uno o más mensajes, haga clic con el botón secundario en ellos y, a continuación, seleccione **Suspender**.

## Usar Shell para suspender los mensajes

Para suspender mensajes, use la sintaxis siguiente:

    Suspend-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

En este ejemplo se suspenden todos los mensajes en las colas de cualquier remitente del dominio contoso.com.

    Suspend-Message -Filter {FromAddress -eq "*contoso.com"}

En este ejemplo se suspende el mensaje con el identificador de mensaje 3 en la cola inaccesible del servidor denominado Mailbox01:

    Suspend-Message -Identity Mailbox01\Unreachable\3

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que los mensajes se han suspendido correctamente en las colas, siga uno de estos pasos:

  - En el Visor de cola, seleccione la cola o cree un filtro para comprobar que los mensajes se han suspendido.

  - Use el cmdlet **Get-Message** con los parámetros *Queue* o *Filter* para comprobar que los mensajes están suspendidos. Para obtener más información, consulte [Get-Message](https://technet.microsoft.com/es-es/library/bb124738\(v=exchg.150\)).

