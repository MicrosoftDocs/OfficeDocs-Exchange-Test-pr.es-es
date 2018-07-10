---
title: 'Configurar un conector de envío entre bosques: Exchange 2013 Help'
TOCTitle: Configurar un conector de envío entre bosques
ms:assetid: 7840d172-071e-4f13-9379-2fe1eee1a7cc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ945053(v=EXCHG.150)
ms:contentKeyID: 52062033
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar un conector de envío entre bosques

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-21_

En Active Directory, el *bosque* representa los límites externos del servicio de directorio. Puede crear conectores de envío para permitir la comunicación entre los bosques. En este ejemplo, los conectores utilizan la autenticación básica.

Para otras tareas de administración relacionadas con la configuración de conectores, consulte [Conectores](connectors-exchange-2013-help.md).

¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Implementar Exchange 2013 en una topología entre bosques](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 20 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas "Conectores de envío" y "Conectores de recepción" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si está comenzando su instalación. Después de la instalación puede utilizar los pasos en este tema para crear conectores para configurar una topología entre bosques.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear una cuenta de usuario en cada bosque

Debe crear una cuenta de usuario en cada bosque para usar autenticación básica. Cree una cuenta en cada bosque y añada cada una de ellas al grupo de seguridad universal del servidor Exchange que se utiliza para la comunicación. El conector de envío usa esta cuenta para autenticarse con el servidor que recibe el correo en el otro bosque. Por ejemplo, cree una cuenta de usuario que tenga el nombre principal de usuario (UPN) FourthCoffee@Contoso.com como las credenciales que debe utilizar para la autenticación el servidor Exchange en el dominio Fourth Coffee cuando se envía correo al servidor Exchange del dominio Contoso.

## Usar el EAC para crear un conector de envío para enrutar el correo a otro bosque de Exchange 2013

Establezca un flujo de correo entre bosques mediante autenticación básica.

1.  En el EAC, vaya a **Flujo de correo** \> **Conectores de envío**. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el Asistente para **nuevo conector de envío**, especifique un nombre para el conector de envío y, a continuación, elija **Interno** para el **Tipo**. Haga clic en **siguiente**.

3.  Seleccione **Enrutar correo mediante hosts inteligentes** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Añadir host inteligente**, especifique la dirección IP del servidor de destino en el bosque secundario, como 64.4.6.100. Haga clic en **Guardar** y, a continuación, haga clic en **Siguiente**.
    
    Para la **Autenticación de host inteligente**, elija **Autenticación básica** y escriba el nombre de usuario y la contraseña. Aquí puede elegir **Ofrecer autenticación básica sólo después de iniciar TLS** para comunicaciones seguras por TLS.
    

    > [!NOTE]
    > Si usa autenticación básica por TLS, el servidor de destino debe estar configurado para usar un certificado X.509.



4.  En **Espacio de direcciones**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Agregar dominio**, asegúrese de que se muestre SMTP como **Tipo**. Para **Nombres de dominios completos (FQDN)**, escriba el dominio de recepción, como fourthcoffee.com. Haga clic en **Guardar** y, a continuación, **Siguiente**.

5.  En **Servidor de origen**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Seleccionar un servidor**, elija el servidor que quiere usar y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Haga clic en **Aceptar**.

6.  Haga clic en **Finalizar**. El conector aparece en la lista de conectores de envío.

Después de crear el conector de envío, cree un conector de envío en el bosque secundario que envía correo al bosque original. En este caso, el nombre de dominio completo (FQDN) que especifique será el nombre de dominio en el primer bosque. Por ejemplo, contoso.com.

## Usar el Shell para establecer permisos en el conector de envío

En este ejemplo se usa la secuencia de comandos Enable-CrossForestConnector.ps1 en el Shell para establecer permisos en el conector de envío que se utilizará en una topología entre bosques.

    .\Enable-CrossForestConnector.ps1 -Connector "Cross-Forest" -user "ANONYMOUS LOGON"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que los conectores de envío para enrutar el correo electrónico a un bosque secundario se crearon correctamente, envíe un mensaje de un usuario de su organización (puede usar Outlook Web App) al dominio especificado para el **Espacio de direcciones**. Si el destinatario recibe el mensaje, habrá configurado el conector de envío correctamente.

## Más información

[Crear un conector de envío para correo electrónico enviado a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Conectores de envío](send-connectors-exchange-2013-help.md)

