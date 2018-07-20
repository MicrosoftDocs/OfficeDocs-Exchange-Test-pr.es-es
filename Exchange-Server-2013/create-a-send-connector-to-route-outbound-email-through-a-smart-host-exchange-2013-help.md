---
title: 'Crear un conector de envío para enrutar el correo saliente a través de un Host inteligente: Exchange 2013 Help'
TOCTitle: Crear un conector de envío para enrutar el correo saliente a través de un Host inteligente
ms:assetid: 4a9ef08e-bd62-4c6b-8790-d24fb0f8f24b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673059(v=EXCHG.150)
ms:contentKeyID: 49895614
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear un conector de envío para enrutar el correo saliente a través de un Host inteligente

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-07_

En algunos casos, puede que desee enrutar el correo electrónico mediante un host inteligente de terceros, por ejemplo, si tiene una aplicación de red para la que desea realizar comprobaciones de directiva en los mensajes salientes.


> [!NOTE]
> El host inteligente de terceros debe usar SMTP para el transporte. Si no lo hace, debe usar un conector externo o un conector de agente de entrega.



¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Configurar el flujo de correo y el acceso de cliente](configure-mail-flow-and-client-access-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Conectores de envío" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Vea [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si va a comenzar con la instalación. Después de la instalación puede utilizar los pasos en este tema para crear el conector de salida.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el EAC para crear un conector de envío para enrutar el correo electrónico saliente a través de un host inteligente

1.  En el Centro de administración de Exchange (EAC), vaya a **Flujo de correo** \> **Conectores de envío** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el asistente para **nuevo conector de envío**, especifique un nombre para el conector de envío y, a continuación, elija **Personalizado** para el **Tipo**. Generalmente, se elige esta configuración cuando se desea enrutar mensajes a equipos que no tengan instalado Microsoft Exchange Server 2013. Haga clic en **Siguiente**.

3.  Seleccione **Enrutar correo mediante hosts inteligentes** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Agregar host inteligente**, especifique una dirección IP, como 192.168.100.1, o un nombre de dominio completo (FQDN), como contoso.com. Haga clic en **Guardar**.
    
    En **Autenticación de host inteligente**, elija el tipo de autenticación que requiere el host inteligente. Si elige **Autenticación básica**, debe proporcionar un nombre de usuario y una contraseña.
    

    > [!NOTE]
    > Si elige la autenticación básica, se recomienda usar una conexión cifrada porque el nombre de usuario y la contraseña se envían como texto no cifrado.



4.  En **Espacio de direcciones**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Agregar dominio**, asegúrese de que aparece SMTP en la lista de **Tipo**. En **Nombre de dominio completo (FQDN)**, escriba \* para indicar que este conector de envío se aplica a los mensajes enviados a cualquier dominio. Haga clic en **Guardar**.

5.  En **Servidor de origen**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Seleccionar un servidor**, elija un servidor de buzones que se usará para enviar correo a Internet a través del servidor de acceso de clientes y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Cuando haya seleccionado el servidor, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Haga clic en **Aceptar**.

6.  Haga clic en **Finalizar**.

Una vez que haya creado el conector de envío, éste aparece en la lista de conectores de envío.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el conector de envío para enrutar el correo electrónico saliente a través de un host inteligente se creó correctamente, envíe un mensaje a un usuario de su organización (puede usar Outlook Web App) al dominio especificado para el **Espacio de direcciones**. Si el destinatario recibe el mensaje, habrá configurado el conector de envío correctamente.

## Más información

[Crear un conector de envío para correo electrónico enviado a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Conectores de envío](send-connectors-exchange-2013-help.md)

