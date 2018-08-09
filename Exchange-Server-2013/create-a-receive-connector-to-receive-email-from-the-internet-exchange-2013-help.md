---
title: 'Crear un conector de recepción para recibir correo electrónico de Internet'
TOCTitle: Creación de un conector de recepción para recibir correo electrónico de Internet
ms:assetid: 534bbd32-a0db-4d50-9579-4933b156d7b3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657447(v=EXCHG.150)
ms:contentKeyID: 49895628
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creación de un conector de recepción para recibir correo electrónico de Internet

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-15_

En este procedimiento se muestra cómo configurar un conector de recepción para recibir correo electrónico de Internet.


> [!NOTE]
> En la mayoría de los casos, no es necesario configurar ningún conector de recepción de forma explícita para recibir correo de Internet, porque al instalar Exchange se crea un conector de recepción de manera implícita para aceptar correo de Internet. Vea <A href="receive-connectors-exchange-2013-help.md">Conectores de recepción</A> para obtener más información.



¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Configurar el flujo de correo y el acceso de cliente](configure-mail-flow-and-client-access-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Conectores de recepción" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Vea [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si va a comenzar con la instalación. Después de la instalación puede utilizar los pasos en este tema para crear el conector de recepción.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el EAC para crear un conector de recepción para recibir mensajes de Internet

1.  En el EAC, vaya a **Flujo de correo** \> **Conectores de recepción**. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para crear un conector de recepción.

2.  En el asistente para **nuevo conector de recepción**, especifique un nombre para el conector de recepción y, a continuación, elija **Transporte front-end** para el **Rol**. Como en este caso va a recibir correo de Internet, se recomienda que enrute el correo desde el principio al servidor o servidores front-end para simplificar y consolidar el flujo de trabajo.

3.  Elija **Internet** para el tipo. El conector de recepción recibirá correo de remitentes de Internet.

4.  Para los **Enlaces de adaptador de red**, observe si aparece **Todas las direcciones IPV4 disponibles** en la lista de **Direcciones IP** y el **Puerto** es 25. (El Protocolo simple de transferencia de correo (SMTP) usa el puerto 25.) Esto indica que el conector está preparado para las conexiones en todas las direcciones IP asignadas a los adaptadores de red en el servidor local.
    

    > [!NOTE]
    > Si tiene varios adaptadores de red, en esta página puede agregar una dirección IP que esté asignada a un adaptador de red específico en el servidor local, aunque esto no es necesario.



5.  Haga clic en el botón **Finalizar** para crear el conector.

Una vez que haya creado el conector de recepción, éste aparece en la lista de conectores de recepción. Si desea consultar un ejemplo sobre cómo crear un conector de recepción con un cmdlet, vea [New-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125139\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que creó correctamente el conector de recepción para recibir mensajes de Internet, intente enviar correo desde un origen externo y ver si uno de los usuarios lo recibe. Si puede recibir correo, significa que la configuración se estableció correctamente.

## Más información

[Crear un conector de recepción seguro para recibir correos electrónicos de un socio](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

[Creación de un conector de recepción para recibir correo electrónico de un sistema que no tenga instalado Exchange](create-a-receive-connector-to-receive-email-from-a-system-not-running-exchange-exchange-2013-help.md)

