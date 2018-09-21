---
title: 'Administración de colas: Exchange 2013 Help'
TOCTitle: Administración de colas
ms:assetid: 37f11378-a884-4aff-ab55-689f40a46321
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997263(v=EXCHG.150)
ms:contentKeyID: 51406490
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administración de colas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-01-31_

En Microsoft Exchange Server 2013, puede usar el Visor de cola del cuadro de herramientas de Exchange o el Shell de administración de Exchange para administrar las colas. Para más información sobre cómo usar los cmdlets de administración de colas en el Shell de administración de Exchange, consulte [Uso del Shell de administración de Exchange para administrar colas](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada «Colas» en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Ver colas

## Usar el Visor de cola del cuadro de herramientas de Exchange para ver las colas

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **herramientas de flujo de correo**, haga doble clic en **Visor de cola** para abrir la herramienta en una ventana nueva.

3.  En el Visor de cola, haga clic en la ficha **Colas**. Se muestra una lista de todas las colas del servidor al que está conectado.

4.  Se puede utilizar el vínculo **Exportar lista**en el panel de acciones para exportar la lista de colas. Para obtener más información, consulte [Exportar listas del visor de cola](export-lists-from-queue-viewer-exchange-2013-help.md)

## Usar el Shell para ver las colas

Para ver colas, use la sintaxis siguiente.

    Get-Queue [-Filter <Filter> -Server <ServerIdentity> -Include <Internal | External | Empty | DeliveryType> -Exclude <Internal | External | Empty | DeliveryType>]

En este ejemplo aparece la información básica sobre todas las colas no vacías en el servidor de buzones de Exchange 2013 denominado Mailbox01.

```powershell
Get-Queue -Server Mailbox01 -Exclude Empty
```

En este ejemplo se muestra información detallada de todas las colas que contienen más de 100 mensajes en el servidor de buzones en el que se ejecuta el comando.

```powershell
Get-Queue -Filter {MessageCount -gt 100} | Format-List
```

## Usar el Shell para ver la información de resumen de cola en varios servidores de Exchange

El cmdlet **Get-QueueDigest** proporciona una vista agregada de alto nivel del estado de las colas en todos los servidores dentro de un ámbito concreto, por ejemplo, un DAG, un sitio de Active Directory, una lista de servidores o todo un bosque de Active Directory. Observe que las colas de un servidor de transporte perimetral suscrito en una red perimetral no aparecen entre los resultados. De igual modo, **Get-QueueDigest** está disponible en un servidor de transporte perimetral, pero los resultados se acotan a las colas en el servidor de transporte perimetral.


> [!NOTE]
> De forma predeterminada, el cmdlet <STRONG>Get-QueueDigest</STRONG> muestra las colas de entrega que contienen diez o más mensajes y los resultados que tienen entre uno y dos minutos de antigüedad. Si quiere ver las instrucciones para cambiar estos valores predeterminados, consulte <A href="configure-get-queuedigest-exchange-2013-help.md">Configurar Get-QueueDigest</A>.



Para ver la información de resumen de colas en varios servidores de Exchange, ejecute el comando siguiente:

    Get-QueueDigest <-Server <ServerIdentity1,ServerIdentity2,..> | -Dag <DagIdentity1,DagIdentity2...> | -Site <ADSiteIdentity1,ADSiteIdentity2...> | -Forest> [-Filter <Filter>]

En este ejemplo aparece la información de resumen sobre las colas de todos los servidores de buzones de Exchange 2013 del sitio de Active Directory denominado FirstSite en el que el recuento de mensajes es superior a 100.

```powershell
Get-QueueDigest -Site FirstSite -Filter {MessageCount -gt 100}
```

En este ejemplo aparece la información de resumen de las colas de todos los servidores de buzones de Exchange 2013 del grupo de disponibilidad de base de datos (DAG) denominado DAG01 en el que el estado de cola tiene el valor **Retry**.

```powershell
Get-QueueDigest -Dag DAG01 -Filter {Status -eq "Retry"}
```

## Reanudar colas

Al reanudar una cola, se reinician las actividades salientes en una cola cuyo estado es Suspendido. La cola debe tener el estado Suspendido para que esta acción tenga efecto. Cuando reanuda una cola, el estado de los mensajes en la cola no cambia. Los mensajes cuyo estado es Suspendido permanecen suspendidos y no dejan la cola.

## Usar el Visor de cola del cuadro de herramientas de Exchange para reanudar colas

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **herramientas de flujo de correo**, haga doble clic en **Visor de cola** para abrir la herramienta en una ventana nueva.

3.  En el Visor de cola, haga clic en la ficha **Colas**. Se muestra una lista de todas las colas del servidor al que está conectado.

4.  Haga clic en **Crear filtro** y especifique la expresión de filtro de la siguiente forma:
    
    1.  Seleccione **Estado** en la lista desplegable de propiedades de la cola.
    
    2.  Seleccione **Es igual a** en la lista desplegable del operador de comparación.
    
    3.  Seleccione **Suspendido** en la lista desplegable de valores.

5.  Haga clic en **Aplicar filtro**. Se muestran todas las colas actualmente suspendidas en el servidor.

6.  Seleccione una o más colas de la lista, haga clic con el botón secundario y, a continuación, seleccione **Reanudar**.

## Usar el Shell para reanudar colas

Para reanudar colas, utilice la sintaxis siguiente.

    Resume-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

En este ejemplo, se reanudan todas las colas del servidor local que tienen el estado Suspendido.

```powershell
Resume-Queue -Filter {Status -eq "Suspended"}
```

En este ejemplo se reanuda la cola de entrega suspendida contoso.com en el servidor llamado Mailbox01.

```powershell
Resume-Queue -Identity Mailbox01\contoso.com
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha reanudado una cola correctamente, siga estos pasos:

1.  Use el Visor de cola o el cmdlet **Get-Queue** para encontrar la cola que quiere reanudar.

2.  Compruebe que la propiedad **Status** de la cola no tenga el valor `Suspended`.

## Reintentar colas

Cuando un servidor de transporte no puede conectar con el siguiente salto, la cola de entrega pasa al estado de reintento. Cuando se reintenta una cola de entrega mediante el uso del Visor de colas o el Shell, se fuerza un intento inmediato de conexión y se reemplaza la siguiente hora de reintento programada. Si no se logra establecer la conexión, se restablece el temporizador de intervalos de reintento. La cola debe estar en estado de reintento para que esta acción tenga efecto.

## Usar el Visor de cola del cuadro de herramientas de Exchange para reintentar colas

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **herramientas de flujo de correo**, haga doble clic en **Visor de cola** para abrir la herramienta en una ventana nueva.

3.  En el Visor de cola, haga clic en la ficha **Colas**. Se muestra una lista de todas las colas del servidor al que está conectado.

4.  Haga clic en **Crear filtro** y especifique la expresión de filtro de la siguiente forma:
    
    1.  Seleccione **Estado** en la lista desplegable de propiedades de la cola.
    
    2.  Seleccione **Es igual a** en la lista desplegable del operador de comparación.
    
    3.  Seleccione **Reintentar** en la lista desplegable de valores.

5.  Haga clic en **Aplicar filtro**. Se mostrarán todas las colas que tengan en ese momento el estado **Reintentar**.

6.  Seleccione una o más colas de la lista. Haga clic con el botón secundario y seleccione **Reintentar colar**. Si se establece la conexión, el estado de la cola cambia a **Activo**. Si no se establece la conexión, la cola permanece en estado **Reintentar** y se actualiza la siguiente hora de reintento.

## Uso del Shell para reintentar una cola

Para reintentar colas, utilice la sintaxis siguiente.

    Retry-Queue <-Identity QueueIdentity | -Filter QueueFilter [-Server ServerIdentity]>

En este ejemplo se reintentan todas las colas del servidor local con el estado Reintentar.

```powershell
Retry-Queue -Filter {status -eq "retry"}
```

En este ejemplo se reintenta la cola denominada contoso.com con estado `Retry` en el servidor denominado Mailbox01.

```powershell
Retry-Queue -Identity Mailbox01\contoso.com
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha reintentado una cola correctamente, siga estos pasos:

1.  Use el Visor de cola o el cmdlet **Get-Queue** para encontrar la cola que quiere reintentar.

2.  Compruebe que la propiedad de cola **LastRetryTime** coincide con la hora en la que trató de reintentar la cola.

## Volver a enviar mensajes en colas

La acción de volver a enviar una cola es similar a reintentarla, excepto que los mensajes se vuelven a enviar a la cola de envío para que los reprocese el categorizador. Puede reenviar los mensajes que tengan los siguientes estados:

  - Colas de entrega con estado «Reintentar». Los mensajes de las colas no pueden estar en estado Suspendido.

  - Mensajes de la cola inaccesible que no estén en estado suspendido.

  - Los mensajes de la cola de mensajes con daños.

## Usar el Shell para reenviar los mensajes

Para reenviar mensajes, utilice la sintaxis siguiente.

    Retry-Queue <-Identity QueueIdentity | -Filter {Status -eq "Retry"} -Server ServerIdentity> -Resubmit $true

En este ejemplo, se vuelven a enviar todos los mensajes ubicados en las colas de entrega con el estado de Reintentar en el servidor denominado Mailbox01.

```powershell
Retry-Queue -Filter {Status -eq "Retry"} -Server Mailbox01 -Resubmit $true
```

En este ejemplo se reenvían todos los mensajes de la cola inalcanzable del servidor Mailbox01.

```powershell
Retry-Queue -Identity Mailbox01\Unreachable -Resubmit $true
```

## Volver a enviar los mensajes en la cola de mensajes dudosos

Podrá reenviar los mensajes de la cola de mensajes dudosos reanudando el mensaje. Puede usar el Visor de cola o el Shell para reenviar los mensajes de la cola de mensajes dudosos. Recuerde que la cola de mensajes dudosos solamente es visible en el Visor de cola cuando hay mensajes en la cola de mensajes dudosos.


> [!NOTE]
> La cola de mensajes dudosos contiene mensajes que pueden dañar el sistema de Exchange tras un error del servidor. Los mensajes pueden ser genuinamente dañinos en su contenido o formato.También pueden ser víctimas de un agente mal escrito que haya bloqueado el servidor de Exchange mientras estaba procesando los mensajes supuestamente incorrectos. Si no está seguro de la seguridad de los mensajes en la cola de mensajes dudosos, exporte los mensajes a archivos para poder examinarlos. Para obtener más información, consulte <A href="export-messages-from-queues-exchange-2013-help.md">Exportar mensajes de las colas</A>.



## Usar el Visor de cola del cuadro de herramientas de Exchange para reenviar los mensajes de la cola de mensajes dudosos

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **herramientas de flujo de correo**, haga doble clic en **Visor de cola** para abrir la herramienta en una ventana nueva.

3.  En el Visor de cola, haga clic en la ficha **Colas**. Se muestra una lista de todas las colas del servidor al que está conectado.

4.  Haga clic en la cola de mensajes dañados. En el panel de acciones, seleccione **Ver mensajes**.

5.  Seleccione uno o más mensajes de la lista, haga clic con el botón secundario y, a continuación, seleccione **Reanudar**.

## Usar el Shell para reenviar los mensajes en la cola de mensajes dudosos

Para reenviar un mensaje de la cola de mensajes dudosos, siga estos pasos.

1.  Busque la identidad del mensaje ejecutando el comando siguiente.
    
    ```powershell
Get-Message -Queue Poison | Format-Table Identity
```

2.  Use la identidad del mensaje del paso anterior en el siguiente comando.
    
    ```powershell
Resume-Message <PoisonMessageIdentity>
```
    
    En este ejemplo, se reanuda un mensaje de la cola de mensajes dudosos que tiene un valor de identidad de mensaje de 222.
    
    ```powershell
Resume-Message 222
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha reenviado un mensaje correctamente desde la cola de mensajes dudosos, siga estos pasos:

1.  Use el Visor de cola o el cmdlet **Get-Queue** para ver la cola de mensajes dudosos de donde quiere reenviar el mensaje.

2.  Compruebe que el mensaje ya no está en la cola de mensajes dudosos. Recuerde que una cola de mensajes dudosos vacía no aparecerá en el Visor de cola ni en el cmdlet **Get-Queue**. Por tanto, si el mensaje que reenvió era el único mensaje que estaba en la cola de mensajes dudosos y la cola ya no está visible, esto también es una señal de que el reenvío del mensaje se ha realizado correctamente.

## Suspender colas

Al suspender una cola, se impide que los mensajes salgan de la misma, pero no se cambia el estado de sus mensajes. Los mensajes que se están entregando mediante SMTP finalizarán las operaciones.Se puede suspender una cola para detener el flujo de correo y, posteriormente, suspender uno o más mensajes de la cola. Cuando se restaura la cola, los mensajes suspendidos no abandonarán la cola.

Se pueden suspender las colas que tengan el estado Activo o Reintentar, así como las colas con el estado Inaccesible y Envío.

Si se suspende la cola Inaccesible, los elementos, hasta que se restaure la cola, no se reenviarán al categorizador cuando el servidor de transporte reciba actualizaciones de configuración. Si se suspende la cola Envío, el categorizador no recibirá mensajes hasta que se restaure la cola.

## Usar el Visor de cola del cuadro de herramientas de Exchange para suspender una cola

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange 2013** \> **Cuadro de herramientas de Exchange**.

2.  En la sección **herramientas de flujo de correo**, haga doble clic en **Visor de cola** para abrir la herramienta en una ventana nueva.

3.  En el Visor de cola, haga clic en la ficha **Colas**. Se muestra una lista de todas las colas del servidor al que está conectado. Se puede crear un filtro para mostrar solo las colas que cumplen unos criterios específicos.

4.  Seleccione una o más colas, haga clic con el botón secundario en ellas y, a continuación, seleccione **Suspender**.

## Uso del Shell para suspender una cola

Para suspender una cola, utilice la sintaxis siguiente.

    Suspend-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

En este ejemplo se suspenden todas las colas del servidor local que tienen un recuento de mensajes igual o superior a 1.000 y el estado Reintentar.

```powershell
Suspend-Queue -Filter {MessageCount -ge 1000 -and Status -eq "Retry"}
```

En este ejemplo se suspende la cola denominada contoso.com en el servidor denominado Mailbox01.

```powershell
Suspend-Queue -Identity Mailbox01\contoso.com
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha suspendido una cola correctamente, siga estos pasos:

1.  Use el Visor de cola o el cmdlet **Get-Queue** para encontrar la cola que quiere suspender.

2.  Compruebe que la propiedad **Status** de la cola tiene el valor `Suspended`.

