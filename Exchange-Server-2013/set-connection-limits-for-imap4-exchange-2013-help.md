---
title: 'Establecer los límites de conexión para IMAP4: Exchange 2013 Help'
TOCTitle: Establecer los límites de conexión para IMAP4
ms:assetid: 8e3aa366-e77c-4c70-b78d-ddbb178cb521
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123712(v=EXCHG.150)
ms:contentKeyID: 50556851
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Establecer los límites de conexión para IMAP4

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-28_

Puede usar el EAC o el Shell para administrar los límites de conexión IMAP4 de su organización.

Al especificar límites de conexión para IMAP4, puede seleccionar límites de conexión para el servidor, una dirección IP o un usuario específico.

Para obtener más información acerca de IMAP4, consulte [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de IMAP4" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para establecer los límites de conexión IMAP4 para un servidor, una dirección IP o un usuario

1.  En la consola EAC, desplácese hasta **Servidores** **\>** **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **IMAP4**.

4.  Desplácese hacia abajo y haga clic en **Más opciones**.

5.  En **Límites de conexión**, especifique lo siguiente:
    
      - **Número máximo de conexiones**   Especifica el número total de conexiones que aceptará el servidor especificado. Se incluyen en este número tanto las conexiones autenticadas como las que no lo están. El valor predeterminado es 2.147.483.647. Se admiten los valores de 1 a 2.147.483.647.
    
      - **Núm. máximo de conexiones desde una sola dirección IP**   Especifica el número de conexiones que el servidor aceptará de una misma dirección IP. El valor predeterminado es 2.147.483.647. Se admiten los valores de 1 a 2.147.483.647.
    
      - **Núm. máximo de conexiones desde un solo usuario**   Especifica el número de conexiones que el servidor aceptará de un usuario concreto. El valor predeterminado es 16. Se admiten los valores de 1 a 2.147.483.647.
    
      - **Tamaño máximo del comando (bytes)**   Especifica el tamaño máximo de un único comando. El tamaño predeterminado es 10.240. Se admiten los valores de 1.024 a 16.384.

6.  Haga clic en **Aplicar** y, a continuación, haga clic en **Aceptar** para guardar los cambios.

Una vez que haya establecido los límites de conexión, debe reiniciar los servicios IMAP4. Para obtener más información acerca de cómo reiniciar los servicios IMAP4, consulte [Iniciar y detener los servicios IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Usar el Shell para establecer los límites de conexión IMAP4 para un servidor, una dirección IP o un usuario

En este ejemplo, se define el límite de conexión para un servidor.

```powershell
Set-ImapSettings -Identity CAS01 -MaxConnections Value
```

En este ejemplo, se define el límite de conexión para una dirección IP.

```powershell
Set-ImapSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value
```

En este ejemplo, se define el límite de conexión para un usuario.

```powershell
Set-ImapSettings -MaxConnectionsPerUser Value
```

Este ejemplo establece el tamaño máximo de comando.

```powershell
Set-ImapSettings -MaxCommandSize Value
```

Una vez que haya establecido los límites de conexión, debe reiniciar los servicios IMAP4. Para obtener más información acerca de cómo reiniciar los servicios IMAP4, consulte [Iniciar y detener los servicios IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Set-ImapSettings](https://technet.microsoft.com/es-es/library/aa998252\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si estableció límites de conexión correctamente, siga uno de estos procedimientos:

1.  En la consola EAC, desplácese hasta **Servidores** **\>** **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **IMAP4**.

4.  Desplácese hacia abajo y haga clic en **Más opciones**.

5.  En **Límites de conexión**, compruebe que la configuración de conexión sea correcta.

O bien

1.  Ejecute el siguiente comando en el Shell.
    
    ```powershell
    Get-ImapSettings | format-list
    ```

2.  Compruebe que la configuración de la conexión sea correcta.

## Más información

Después de establecer los límites de conexión IMAP4 para un servidor, una dirección IP o un usuario, es posible que también desee realizar las siguientes tareas:

[Habilitar IMAP4 en Exchange 2016](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Establecer límites de tiempo de espera de conexión para IMAP4](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

