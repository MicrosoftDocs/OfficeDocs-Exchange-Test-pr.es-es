---
title: 'Establecer límites de conexión para POP3: Exchange 2013 Help'
TOCTitle: Establecer límites de conexión para POP3
ms:assetid: 512d61c2-2a34-4813-92a9-875339d3388b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997988(v=EXCHG.150)
ms:contentKeyID: 50556805
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Establecer límites de conexión para POP3

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-28_

Puede usar el Centro de Administración de Exchange o el Shell para administrar los límites de conexión POP3 para su organización.

Si desea especificar límites de la conexión para POP3, puede seleccionar límites para el servidor, una dirección IP o un usuario específico.

Para obtener más información acerca de POP3, consulte [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración POP3" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar la EMC para establecer los límites de conexión POP3 para un servidor, una dirección IP o un usuario

1.  En la consola EAC, desplácese hasta **Servidores** **\>** **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **POP3**.

4.  Desplácese hacia abajo y haga clic en **Más opciones**.

5.  En **Límites de conexión**, use la siguiente configuración:
    
      - **Conexiones máxima**   Especifica el número total de conexiones que aceptará el servidor especificado. Se incluyen en este número tanto las conexiones autenticadas como las que no lo están. El valor predeterminado es 2.147.483.647. Se admiten los valores de 1 a 2.147.483.647.
    
      - **Núm. máximo de conexiones desde una sola dirección IP**   Especifica la cantidad de conexiones que el servidor aceptará de una misma dirección IP. El valor predeterminado es 2.147.483.647. Se admiten los valores de 1 a 2.147.483.647.
    
      - **Núm. máximo de conexiones desde un solo usuario**   Especifica la cantidad de conexiones que el servidor aceptará de un usuario particular. El valor predeterminado es 16. Se admiten los valores de 1 a 2.147.483.647.
    
      - **Tamaño máximo del comando (bytes)**   Especifica el tamaño máximo de un único comando. El tamaño predeterminado es 512. Se admiten los valores de 40 a 1,024.

6.  Haga clic en **Aplicar** y, a continuación, haga clic en **Aceptar** para guardar los cambios.

Una vez que haya establecido los límites de la conexión, debe reiniciar los servicios POP3. Para obtener más información acerca de cómo reiniciar los servicios POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Usar el Shell para establecer los límites de conexión POP3 para un servidor, una dirección IP o un usuario

En este ejemplo, se define el límite de conexión para un servidor.

```powershell
Set-PopSettings -Identity CAS01 -MaxConnections Value
```

En este ejemplo, se define el límite de conexión para una dirección IP.

```powershell
Set-PopSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value
```

En este ejemplo, se define el límite de conexión para un usuario.

```powershell
Set-PopSettings -MaxConnectionsPerUser Value 
```

En este ejemplo, se establece el tamaño máximo de comando.

```powershell
Set-PopSettings -MaxCommandSize Value
```

Una vez que haya establecido los límites de la conexión, debe reiniciar los servicios POP3. Para obtener más información acerca de cómo reiniciar los servicios POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Set-POPSettings](https://technet.microsoft.com/es-es/library/aa997154\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si estableció los límites de conexión correctamente, siga uno de estos procedimientos:

1.  En la consola EAC, desplácese hasta **Servidores** **\>** **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **POP3**.

4.  Desplácese hacia abajo y haga clic en **Más opciones**.

5.  En **Límites de conexión**, compruebe que la configuración de la conexión sea correcta.

O bien

1.  Ejecute el siguiente comando en el Shell.
    
    ```powershell
    Get-PopSettings | format-list
    ```

2.  Compruebe que la configuración de la conexión sea correcta.

## Más información

Después de establecer los límites de conexión POP3 para un servidor, una dirección IP o un usuario, es posible que también desee realizar las siguientes tareas:

[Habilitar POP3 en Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[Establecer límites de tiempo de espera de conexión para POP3](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

