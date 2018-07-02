---
title: 'Habilitar el extremo del proxy MRS para movimientos remotos: Exchange 2013 Help'
TOCTitle: Habilitar el extremo del proxy MRS para movimientos remotos
ms:assetid: 9840f712-127e-4c2d-bfe5-1b35cdb2a31b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn155787(v=EXCHG.150)
ms:contentKeyID: 54652446
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar el extremo del proxy MRS para movimientos remotos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-07-02_

El proxy de servicio de replicación de buzón de correo (proxy MRS) facilita los movimientos de buzón de correo entre bosques y las migraciones de movimiento remoto entre su organización Exchange local y Exchange Online. En Exchange 2013, el proxy MRS está incluido en el rol de servidor Buzón de correo (también llamado el *servidor de buzones de correo*). Durante las migraciones de movimiento remoto y entre bosques, un servidor de acceso de cliente actúa como un proxy para las solicitudes de movimiento entrantes para el servidor de buzones de correo. La capacidad de un servidor de acceso de cliente para aceptar estas solicitudes está deshabilitada de forma predeterminada. Para permitir que el servidor de acceso de cliente pueda aceptar solicitudes de movimiento entrantes, tiene que habilitar el extremo del proxy MRS.

El servidor de acceso de cliente en el que se habilitará el extremo de proxy MRS depende del tipo de movimiento de buzón de correo y su dirección.

  - **Movimientos de empresa entre bosques**   Para movimientos entre bosques que se inician en el entorno de destino (conocidos como un tipo de movimiento de *extracción*), tiene que habilitar el extremo de proxy MRS en los servidores de acceso de cliente del entorno de origen. Para movimientos entre bosques que se inician en el entorno de origen (conocido como un tipo de movimiento de *introducción*), tiene que habilitar el extremo de proxy MRS en los servidores de acceso de cliente del entorno de destino.

  - **Migraciones de movimiento remoto entre una organización de Exchange local y Exchange Online**   Tanto en las migraciones de movimiento remoto de incorporación como en las de exteriorización, debe habilitar el extremo de proxy MRS en los servidores de acceso de cliente de su organización local.


> [!NOTE]
> Si utiliza el EAC para mover buzones de correo, los movimientos entre bosques y las migraciones de movimiento remoto de incorporación son tipos de movimiento de extracción, puesto que la solicitud se inicia en el entorno de destino. Las migraciones de movimiento remoto de exteriorización son un tipo de movimiento de introducción, puesto que la solicitud se inicia en el entorno de origen.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 minutos por servidor.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Permisos de servicios Web Exchange" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Si ha implementado más de un servidor de acceso de cliente en su organización de Exchange, debería habilitar el extremo de proxy MRS en cada uno de ellos. Si agrega otros servidores de acceso de cliente, asegúrese de habilitar el extremo de proxy MRS en los servidores nuevos. De lo contrario, si el extremo de proxy MRS no está habilitado en todos los servidores de acceso de cliente, se pueden producir errores en los movimientos entre bosques y las migraciones de movimiento remoto.

  - Si no realiza movimientos entre bosques o migraciones de movimiento remoto, mantenga los extremos de proxy MRS deshabilitados para reducir la superficie de ataque de su organización.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar el extremo de proxy MRS

1.  En el EAC, vaya a **Destinatarios**  \> **Grupos** \> **Directorios virtuales**.

2.  En la lista desplegable **Seleccionar servidor**, seleccione el nombre del servidor de acceso de cliente en el que desea habilitar el extremo de proxy MRS. O seleccione **Todos los servidores** para mostrar los directorios virtuales de todos los servidores de acceso de cliente de su organización.

3.  En la lista desplegable **Seleccionar tipo**, seleccione **EWS** para mostrar el directorio virtual de servicios web de Exchange (EWS) para el servidor seleccionado.

4.  En la lista de directorios virtuales, haga clic en **EWS (sitio web predeterminado)** para el servidor de acceso de cliente que desee configurar y, después, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

5.  En la página de propiedades **EWS (sitio web predeterminado)**, seleccione la casilla de verificación **MRS Proxy habilitado** y, a continuación, haga clic en **Guardar**.

## Usar el Shell para habilitar el extremo de proxy MRS

Con el siguiente comando se habilita el extremo de proxy MRS en un servidor de acceso de cliente llamado EXCH-SRV-01.

    Set-WebServicesVirtualDirectory -Identity "EXCH-SRV-01\EWS (Default Web Site)" -MRSProxyEnabled $true

Con el siguiente comando se habilita el extremo de proxy MRS en todos los servidores de acceso de cliente de su organización de Exchange.

    Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -MRSProxyEnabled $true


> [!IMPORTANT]
> Como se ha indicado anteriormente, todos los servidores de acceso de cliente de su organización deben tener habilitado el extremo de proxy MRS. Ejecute el comando anterior después de agregar un nuevo servidor de acceso de cliente en su organización.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha habilitado el extremo de proxy MRS correctamente, siga uno de estos procedimientos:

1.  En el EAC, vaya a **Destinatarios**  \> **Servidores** \> **Directorios virtuales**.

2.  En la lista de directorios virtuales, haga clic en **EWS (sitio web predeterminado)** y compruebe en el panel de detalles que el extremo de proxy MRS esté habilitado.
    
    Si no, puede hacer clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para ver la página de propiedades de **EWS (sitio web predeterminado)** y comprobar que la casilla **MRS Proxy habilitado** esté seleccionada.

O bien

Ejecute el siguiente comando en el Shell:

    Get-WebServicesVirtualDirectory | FL Identity,MRSProxyEnabled

Compruebe que el parámetro *MRSProxyEnabled* esté establecido en `True`.

Otra forma de comprobar que el extremo de proxy MRS está habilitado consiste en utilizar el cmdlet **Test-MigrationServerAvailability** para probar la capacidad de comunicación con el servidor remoto que hospeda los buzones de correo que desea mover o, en el caso de exteriorizar buzones de correo de Exchange Online a su organización local, un servidor de su organización local. Para obtener más información, consulte [Test-MigrationServerAvailability](https://technet.microsoft.com/es-es/library/jj219169\(v=exchg.150\)).

En el siguiente ejemplo se muestra la conexión a un servidor en el bosque corp.contoso.com.

    $Credentials = Get-Credential

    Test-MigrationServerAvailability -ExchangeRemoteMove -Autodiscover -EmailAddress administrator@corp.contoso.com -Credentials $Credentials

Para ejecutar este comando correctamente, el extremo de proxy MRS debe estar habilitado.

