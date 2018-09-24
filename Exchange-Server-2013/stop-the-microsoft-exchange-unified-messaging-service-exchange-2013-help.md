---
title: 'Interrumpir el servicio de UM Microsoft Exchange: Exchange 2013 Help'
TOCTitle: Interrumpir el servicio de mensajería unificada de Microsoft Exchange
ms:assetid: 64fa5535-8150-45c6-82e6-d2346892a031
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998595(v=EXCHG.150)
ms:contentKeyID: 50556798
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Interrumpir el servicio de mensajería unificada de Microsoft Exchange

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-16_

Puede usar el complemento Servicios de Microsoft Management Console (MMC) o cmd.exe en un símbolo del sistema para detener el servicio de mensajería unificada de Microsoft Exchange en el servidor de buzones. Es posible que, en ciertas ocasiones, deba detener este servicio, por ejemplo, cuando sea necesario desconectar el servidor de buzones. Cuando detenga el servicio de mensajería unificada de Microsoft Exchange, el servidor de buzones no podrá aceptar ni procesar llamadas entrantes.

Para otras tareas de administración relacionadas con los servidores de buzones, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Para ejecutar los siguientes procedimientos, debe iniciar sesión en el servidor de buzones usando una cuenta que sea miembro del grupo local de administradores.

  - Compruebe que el servidor de buzones está instalado, bien en el mismo equipo que el servidor de acceso de clientes o en otro distinto.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el complemento Servicios de MMC para detener el servicio de mensajería unificada de Microsoft Exchange

1.  Haga clic en **Inicio** y, a continuación, en **Panel de control**.

2.  En el Panel de control, haga doble clic en **Herramientas administrativas**.

3.  En **Herramientas administrativas**, haga doble clic en **Servicios**.

4.  En el panel de detalles de **Servicios**, haga clic con el botón secundario en **Mensajería unificada de Microsoft Exchange** y, a continuación, haga clic en **Detener**.

## Usar un símbolo del sistema para detener el servicio de mensajería unificada de Microsoft Exchange

1.  Haga clic en **Inicio** y, a continuación, haga clic en **Ejecutar**.

2.  En el cuadro **Abrir**, escriba el siguiente comando y, a continuación, presione Entrar.
    
    ```powershell
    net stop MSExchangeUM
    ```

