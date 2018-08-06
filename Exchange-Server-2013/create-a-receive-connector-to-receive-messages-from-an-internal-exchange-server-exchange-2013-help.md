---
title: 'Crear conector de recepción para recibir mensajes de servidor Exchange interno | Microsoft Docs'
TOCTitle: Creación de un conector de recepción para recibir mensajes de un servidor Exchange interno
ms:assetid: 546cead9-7a2d-4332-a5f6-35343d56c619
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657448(v=EXCHG.150)
ms:contentKeyID: 49895632
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creación de un conector de recepción para recibir mensajes de un servidor Exchange interno

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Los conectores de recepción de tipo **Interno** se crean cuando desea recibir correo de un servidor Exchange. Utilice este tipo de conector para controlar el enrutamiento de correo dentro de su organización: por ejemplo, cuando desee enrutar correo del servicio de transporte de un servidor de buzones a un servidor de transporte perimetral específico o de un servidor de buzones a otro.

¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Configurar el flujo de correo y el acceso de cliente](configure-mail-flow-and-client-access-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Conectores de recepción" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Vea [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si va a comenzar con la instalación. Después de la instalación puede utilizar los pasos en este tema para crear el conector de recepción.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Creación de un conector de recepción para recibir mensajes de un servidor Exchange interno

1.  En el EAC, vaya a **Flujo de correo** \> **Conectores de recepción**. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para crear un conector de recepción nuevo.

2.  En el asistente para **nuevo conector de recepción**, especifique un nombre para el conector de recepción y, a continuación, elija **Transporte de concentradores** para el **Rol**. En este caso, se asume que desea enrutar el correo dentro de su red, y no dentro o fuera de la organización.

3.  Elija **Interno** para el tipo. El conector se configura con la autenticación de servidor Exchange.

4.  Si en la página de configuración de red remota aparece 0.0.0.0-255.255.255.255, que significa que el conector de recepción recibe conexiones de todas las direcciones IP, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") para eliminarla. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"), agregue la dirección IP para el servidor del que desea recibir, como 192.168.1.1, y haga clic en **Guardar**.

5.  Haga clic en **Finalizar** para crear el conector.

Una vez que haya creado el conector de recepción, éste aparece en la lista de conectores de recepción. Si desea consultar un ejemplo sobre cómo crear un conector de recepción con un cmdlet, vea [New-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125139\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que creó correctamente un conector de recepción para recibir mensajes de un servidor interno, intente probar si los mensajes del servidor de envío se transfieren correctamente al servidor del destinatario. Para ello, use el Shell de administración de Exchange para establecer el parámetro *ProtocolLoggingLevel* para el conector de recepción que creó en `Verbose`, mediante el cmdlet [Set-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125140\(v=exchg.150\)), y compruebe los registros para asegurar que el mensaje se entregó correctamente.

## Más información

[Creación de un conector de recepción para recibir correo electrónico de Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

[Crear un conector de recepción seguro para recibir correos electrónicos de un socio](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

