---
title: 'Crear un conector de envío para enviar correo electrónico a un colaborador con Seguridad de la capa de transporte (TLS) aplicada: Exchange 2013 Help'
TOCTitle: Creación de un conector de envío para enviar correo electrónico a un colaborador con seguridad de capa de transporte (TLS) aplicada
ms:assetid: ff2abefc-dd3e-4431-b947-df942fbf82d9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657514(v=EXCHG.150)
ms:contentKeyID: 49896042
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear un conector de envío para enviar correo electrónico a un colaborador con Seguridad de la capa de transporte (TLS) aplicada

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-15_

Si desea garantizar la comunicación segura, cifrada con un asociado, puede crear un conector de envío que se configura para aplicar Seguridad de la capa de transporte (TLS) para mensajes que se envían a un dominio asociado. TLS proporciona comunicación segura mediante Internet.

¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Configurar el flujo de correo y el acceso de cliente](configure-mail-flow-and-client-access-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Conectores de envío" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si está comenzando su instalación. Después de la instalación puede utilizar los pasos en este tema para crear el conector de salida.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el EAC para crear un conector de envío para enviar correo electrónico a un asociado, con TLS aplicada

Para crear un conector de envío para este escenario, inicie sesión en el EAC y realice los siguientes pasos:

1.  En el EAC, desplácese hasta **Flujo de correo** \> **Conectores de envío** y, luego, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el asistente de **Nuevo conector de envío**, especifique un nombre para el conector de envío y, luego, seleccione **Socio** para **Tipo**. Cuando selecciona **Socio**, el conector se configura para permitir conexiones solo con servidores que se autentican con certificados TLS. Haga clic en **Siguiente**.

3.  Compruebe que **Registro MX asociado con el dominio del destinatario** esté seleccionado, que especifica que el conector usa el sistema de nombres de dominio (DNS) para enrutar el correo. Haga clic en **Siguiente**.

4.  En **Espacio de direcciones**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Agregar dominio** asegúrese de que se muestre SMTP como **Tipo**. En **Nombre de dominio completo (FQDN)** escriba el nombre del dominio asociado. Haga clic en **Guardar**.

5.  En **Servidor de origen**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Seleccionar un servidor** seleccione un servidor de buzones que se usará para enviar el correo a Internet mediante el servidor de acceso de cliente y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Después de seleccionar el servidor, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Haga clic en **Aceptar**.

6.  Haga clic en **Finalizar**.

Una vez que haya creado el conector de envío, éste aparece en la lista de conectores de envío.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que creó correctamente un conector de envío para enviar correo electrónico a un asociado, con TLS aplicada, envíe un mensaje desde un usuario de la organización a un destinatario de la organización asociada. Si el destinatario recibe el mensaje, el conector se creó correctamente.

## Más información

[Crear un conector de envío para correo electrónico enviado a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Crear un conector de envío para enrutar el correo saliente a través de un Host inteligente](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

