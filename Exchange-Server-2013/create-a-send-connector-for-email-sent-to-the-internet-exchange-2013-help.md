---
title: 'Crear un conector de envío para correo electrónico enviado a Internet: Exchange 2013 Help'
TOCTitle: Crear un conector de envío para correo electrónico enviado a Internet
ms:assetid: 6deaefa8-1152-40d9-b1ba-9c19bdf8a928
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657457(v=EXCHG.150)
ms:contentKeyID: 49895697
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear un conector de envío para correo electrónico enviado a Internet

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-01-23_

De forma predeterminada, Microsoft Exchange Server 2013 no permite enviar correo fuera del dominio. Para enviar correo fuera del dominio, debe crear un conector de envío. El gráfico siguiente ilustra el flujo de correo al crear un conector de envío para enviar correo a Internet.

![connector\_send\_onprem\_internet](images/JJ657457.e8963e4f-7dce-461f-bbcf-660278cefa35(EXCHG.150).gif "connector_send_onprem_internet")

¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Configurar el flujo de correo y el acceso de cliente](configure-mail-flow-and-client-access-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Conectores de envío" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Vea [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si va a comenzar con la instalación. Después de la instalación puede utilizar los pasos en este tema para crear el conector de salida.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para crear un conector de envío para el correo electrónico enviado a Internet

1.  En el Centro de administración de Exchange (EAC), vaya a **Flujo de correo** \> **Conectores de envío** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el asistente para **nuevo conector de envío**, especifique un nombre para el conector de envío y, a continuación, elija **Internet** para el **Tipo**. Haga clic en **Siguiente**.

3.  Compruebe que **Registro MX asociado con el dominio del destinatario** esté seleccionado, lo cual especifica que el conector utiliza el sistema de nombres de dominio (DNS) para enrutar el correo. Haga clic en **Siguiente**.

4.  En **Espacio de direcciones**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Agregar dominio**, asegúrese de que aparece SMTP en la lista de **Tipo**. En **Nombre de dominio completo (FQDN)**, escriba \*, que indica que este conector de envío se dirige a los mensajes enviados a cualquier dominio. Haga clic en **Guardar**.

5.  Asegúrese de que la casilla **Conector de envío en el ámbito** está desactivada y, a continuación, haga clic en **Siguiente** .

6.  En **Servidor de origen**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Seleccionar un servidor**, elija un servidor de buzones que se usará para enviar correo a Internet a través del servidor de acceso de clientes y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Cuando haya seleccionado el servidor, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Haga clic en **Aceptar**.

7.  Haga clic en **Finalizar**.

Una vez que haya creado el conector de envío, éste aparece en la lista de conectores de envío.

## Usar el Shell para enrutar correo a través del servidor de acceso de clientes

En Exchange 2013, puede usar el parámetro *FrontendProxyEnabled* del cmdlet **Set-SendConnector** para enrutar mensajes salientes a través del servidor de acceso de clientes. Este parámetro no está establecido en `$true` de forma predeterminada, aunque en muchos casos ayuda a consolidar y a simplificar el correo electrónico, especialmente si trabaja en un entorno con un gran número de servidores de mensajería.

En este ejemplo se establece el parámetro *FrontendProxyEnabled* en `$true` en un conector de envío.

    Set-SendConnector "Contoso.com Send Connector" -FrontendProxyEnabled $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el conector de envío para correo electrónico enviado a Internet se creó correctamente, envíe un correo desde uno de sus usuarios a un destinatario externo y compruebe que el mensaje llega correctamente.

## Más información

[Conectores de envío](send-connectors-exchange-2013-help.md)

[Crear un conector de envío para enrutar el correo saliente a través de un Host inteligente](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

