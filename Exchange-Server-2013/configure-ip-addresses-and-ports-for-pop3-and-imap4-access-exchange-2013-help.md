---
title: 'Configurar direcciones IP y puertos de acceso a POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Configurar direcciones IP y puertos de acceso a POP3 e IMAP4
ms:assetid: 8292747b-6626-4d7f-ba73-1e17f5d99fa4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123530(v=EXCHG.150)
ms:contentKeyID: 50556837
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar direcciones IP y puertos de acceso a POP3 e IMAP4

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-28_

Puede usar el EAC y el Shell para configurar los servicios Microsoft Exchange POP3 y IMAP4 para que usen direcciones IP y puertos diferentes de la configuración predeterminada.


> [!NOTE]
> Especifique direcciones IP e intervalos de direcciones IP en el formato de Protocolo de Internet versión 4 (IPv4), Protocolo de Internet versión 6 (IPv6) o en ambos. Una instalación predeterminada de Windows Server 2008 permite la compatibilidad para IPv4 e IPv6.



Para obtener más información acerca de POP3 e IMAP4, vea [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas "Configuración de POP3" y “Configuración de IMAP4” en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Configurar direcciones IP y puertos para POP3

## Usar el EAC para configurar direcciones IP y puertos para POP3

1.  En la consola EAC, desplácese hasta **Servidores** **\>** **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **POP3**.

4.  En **TLS o conexiones sin cifrar**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

5.  En la página **Agregar dirección IP**, en **Dirección IP**, elija una de las siguientes opciones:
    
      - **Todas las direcciones IPv4 disponibles**   Use todas las direcciones IPv4 disponibles para un servidor.
    
      - **Todas las direcciones IPv6 disponibles**    Use todas las direcciones IPv6 disponibles para un servidor.
    
      - **Especificar una dirección IP**   Use una dirección IP específica.

6.  En **Puerto**, escriba un número de puerto o acepte el puerto predeterminado.

7.  Haga clic en **Guardar** para guardar los cambios.

Una vez definida la configuración de la dirección IP y del puerto para POP3, debe reiniciar el servicio POP3 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar el servicio POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Usar el Shell para configurar direcciones IP y puertos para POP3

En este ejemplo, se establece la dirección IP y el puerto de comunicación con Exchange mediante POP3 con Capa de sockets seguros (SSL).

    Set-PopSettings -SSLBindings: IPaddress:Port

En este ejemplo, se establece la dirección IP y el puerto de comunicación con Exchange mediante POP3 sin cifrado ni cifrado Seguridad de la capa de transporte (TLS).

    Set-PopSettings -UnencryptedOrTLSBindings IPaddress:Port

Una vez definida la configuración de la dirección IP y del puerto para POP3, debe reiniciar el servicio POP3 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar el servicio POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obtener más información sobre sintaxis y parámetros, consulte [Set-POPSettings](https://technet.microsoft.com/es-es/library/aa997154\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Haga lo siguiente para comprobar que ha cambiado la configuración de la dirección POP3 IP y del puerto en un servidor.

1.  Ejecute el siguiente comando en el Shell.
    
        Get-PopSettings | format-list

2.  Verifique que la configuración de *UnencryptedOrTLSBindings* y *SSLBindings* sea correcta.

## Configurar direcciones IP y puertos para IMAP4

## Usar el EAC para configurar direcciones IP y puertos para IMAP4

1.  En la consola EAC, desplácese hasta **Servidores** **\>** **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **IMAP4**.

4.  Si desea establecer una configuración de conexiones sin cifrar o TLS, en **TLS o conexiones sin cifrar**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Si desea cambiar la configuración de la conexión capa de sockets seguros (SSL), en **Conexiones de nivel de sockets seguros (SSL)**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

5.  En la página **Agregar dirección IP**, en **Dirección IP**, elija una de las siguientes opciones:
    
      - **Todas las direcciones IPv4 disponibles**   Use todas las direcciones IPv4 disponibles para un servidor.
    
      - **Todas las direcciones IPv6 disponibles**    Use todas las direcciones IPv6 disponibles para un servidor.
    
      - **Especificar una dirección IP**   Use una dirección IP específica.

6.  En **Puerto**, escriba un número de puerto o acepte el puerto predeterminado.

7.  Haga clic en **Guardar** para guardar los cambios.

Una vez definida la configuración de la dirección IP y del puerto para IMAP4, debe reiniciar los servicios IMAP4 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar los servicios IMAP4, consulte [Iniciar y detener los servicios IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Uso del Shell para configurar direcciones IP y puertos para IMAP4

En este ejemplo, se establece la dirección IP y el puerto de comunicación con Exchange mediante IMAP4.

    Set-ImapSettings -SSLBindings: IPaddress:Port

En este ejemplo, se establece la dirección IP y el puerto de comunicación con Exchange mediante IMAP4 sin cifrado ni cifrado TLS.

    Set-ImapSettings -UnencryptedOrTLSBindings IPaddress:Port 

Una vez definida la configuración de la dirección IP y del puerto para IMAP4, debe reiniciar el servicio IMAP4 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar el servicio IMAP4, consulte [Iniciar y detener los servicios IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Para obtener más información sobre sintaxis y parámetros, consulte [Set-ImapSettings](https://technet.microsoft.com/es-es/library/aa998252\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Haga lo siguiente para comprobar que ha cambiado la configuración de la dirección IMAP4 IP y del puerto en un servidor.

1.  Ejecute el siguiente comando en el Shell.
    
        Get-ImapSettings | format-list

2.  Verifique que la configuración de *UnencryptedOrTLSBindings* y *SSLBindings* sea correcta.

## Más información

Después de configurar direcciones IP y puertos para POP3 e IMAP4, es posible que también desee:

[Habilitar IMAP4 en Exchange 2016](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Habilitar POP3 en Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

