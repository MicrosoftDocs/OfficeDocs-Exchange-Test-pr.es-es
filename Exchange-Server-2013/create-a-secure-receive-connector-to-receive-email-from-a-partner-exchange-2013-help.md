---
title: 'Crear un conector de recepción seguro para recibir correos electrónicos de un socio: Exchange 2013 Help'
TOCTitle: Cree un conector de recepción seguro para recibir correos electrónicos de un socio
ms:assetid: 06aa692c-7940-4a14-a722-058c47440f85
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673037(v=EXCHG.150)
ms:contentKeyID: 49895450
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear un conector de recepción seguro para recibir correos electrónicos de un socio

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Este procedimiento le muestra cómo configurar un conector de recepción para recibir correo electrónico seguro de un asociado. Use este procedimiento cuando se le requiera que cifre las comunicaciones entre usted y un asociado de confianza. El conector está configurado para aceptar conexiones sólo de servidores que se autentiquen con Seguridad de la capa de transporte (TLS).

¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Configurar el flujo de correo y el acceso de cliente](configure-mail-flow-and-client-access-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Conectores de recepción" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) si está comenzando su instalación. Después de la instalación puede utilizar los pasos en este tema para crear el conector de recepción.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use el EAC para crear un conector de recepción para recibir mensajes seguros de un asociado

1.  En el EAC, vaya a **Flujo de correo** \> **Conectores de recepción**. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para crear un nuevo conector de recepción.

2.  En la página **Nuevo conector de recepción**, especifique un nombre para el conector de recepción y, a continuación, seleccione **Transporte Frontend** para el **Rol**. Como recibe correo de un asociado en este caso, le recomendamos que inicialmente enrute correo a su servidor front-end para simplificar y consolidad su flujo de correo.

3.  Elija **Asociado** para el tipo. El conector de recepción recibirá correo de un tercero de confianza.

4.  Para los **Enlaces de adaptador de red**, observe que **Todas las direcciones IPv4 disponibles** aparece en la lista **Direcciones IP** y el **Puerto** sea 25. (El Protocolo simple de transferencia de correo usa el puerto 25.) Esto indica que el conector está preparado para las conexiones en todas las direcciones IP asignadas a los adaptadores de red en el servidor local. Haga clic en **Siguiente**.

5.  Si en la página Configuración de red remota aparece 0.0.0.0-255.255.255.255, que significa que el conector de recepción recibe conexiones de todas las direcciones IP, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") para quitarlo. Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"), agregue la dirección IP del servidor de su asociado y haga clic en **Guardar**.
    

    > [!NOTE]
    > También puede especificar un intervalo de direcciones IP con notación CIDR, como 64.4.6.100/24.



6.  Haga clic en **Finalizar** para crear el conector.

Una vez que haya creado el conector de recepción, éste aparece en la lista de conectores de recepción. Si desea ver un ejemplo de cómo crear un conector de recepción con un cmdlet, consulte [New-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125139\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya creado correctamente un conector de recepción para recibir mensajes de un asociado, compruebe si el asociado puede enviar correo a uno de los usuarios y que el usuario lo reciba correctamente. Si puede recibir correo cifrado (puede comprobar que se usa TLS comprobando el encabezado del mensaje), sabrá que la configuración funciona bien.

## Más información

[Conectores de recepción](receive-connectors-exchange-2013-help.md)

