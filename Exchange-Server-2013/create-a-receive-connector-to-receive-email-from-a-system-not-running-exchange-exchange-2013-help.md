---
title: 'Crear conector recepción recibir correo de sistema no tenga Exchange'
TOCTitle: Creación de un conector de recepción para recibir correo electrónico de un sistema que no tenga instalado Exchange
ms:assetid: 85f0864a-6502-49db-8804-16755a7292b4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657467(v=EXCHG.150)
ms:contentKeyID: 49895751
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creación de un conector de recepción para recibir correo electrónico de un sistema que no tenga instalado Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Es posible que tenga problemas cuando quiera recibir mensajes de un sistema que no ejecuta Exchange. Por ejemplo, si tiene un dispositivo de red que realiza comprobaciones de directrices y más adelante redirige mensajes a su servidor de Exchange. En este caso, suponemos que el dispositivo utiliza SMTP. En caso contrario, deberá usar un conector externo o un conector de agente de entrega.

¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Configurar el flujo de correo y el acceso de cliente](configure-mail-flow-and-client-access-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Conectores de recepción" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si está comenzando la instalación. Después de la instalación puede utilizar los pasos en este tema para crear el conector de recepción.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el EAC para crear un conector de recepción para recibir mensajes desde un dispositivo de mensajería

1.  En el EAC, vaya a **Flujo de correo** \> **Conectores de recepción**. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para crear un conector de recepción.

2.  En la página **Nuevo conector de recepción**, especifique un nombre para el conector de recepción y, a continuación, seleccione **Transporte de concentradores** para la **Regla**. En este caso, desea que el servidor de buzones de correo ejecute el servicio de transporte para recibir mensajes del dispositivo.

3.  Seleccione **Personalizado** para el tipo, dado que el conector de recepción recibirá correo de un dispositivo que no ejecuta Microsoft Exchange Server 2013.

4.  Para los **Enlaces de adaptador de red**, observe que **Todas las IPV4 disponibles** aparece en la lista **Direcciones IP**. Haga clic en **Siguiente**.

5.  Para **Configuración de red remota**, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") para quitar **0.0.0.0-255.255.255.255** de la lista de **Direcciones IP**, dado que desea especificar que el conector acepte correo de un dispositivo específico. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para añadir una dirección IP nueva y, en la ventana **Agregar dirección IP**, agregue la dirección IP del dispositivo. Haga clic en **Guardar**.

6.  Haga clic en el botón **Finalizar** para crear el conector.

Una vez que haya creado el conector de recepción, éste aparece en la lista de conectores de recepción. Si desea ver un ejemplo de cómo crear un conector de recepción con un cmdlet, consulte [New-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125139\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha creado correctamente un conector de recepción para recibir mensajes de un dispositivo de mensajería, haga una prueba de que puede recibir correo del dispositivo. Si puede recibir correo, significa que la configuración se estableció correctamente.

## Más información

[Creación de un conector de recepción para recibir correo electrónico de Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

