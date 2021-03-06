﻿---
title: 'Detenga el servicio Microsoft Exchange Unified Messaging llame al Router: Exchange 2013 Help'
TOCTitle: Detenga el servicio Microsoft Exchange Unified Messaging llame al Router
ms:assetid: 79935528-1a8c-4f22-826c-8f9a60f4f6f4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673535(v=EXCHG.150)
ms:contentKeyID: 50556823
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Detenga el servicio Microsoft Exchange Unified Messaging llame al Router

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-16_

Puede utilizar el complemento Servicios de Microsoft Management Console (MMC) o cmd.exe en un símbolo del sistema para detener el servicio de enrutador de llamadas de mensajería unificada de MicrosoftExchange en un servidor de acceso de cliente. Es posible que, en ciertas ocasiones, deba detener este servicio, por ejemplo, cuando sea necesario desconectar el servidor de acceso de cliente. Cuando detenga el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange, el servidor de acceso de cliente no podrá aceptar ni procesar llamadas entrantes.

Para conocer tareas de administración adicionales relacionadas con servidores de acceso de cliente, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Para ejecutar los siguientes procedimientos, debe iniciar sesión en el servidor de acceso de cliente usando una cuenta que sea miembro del grupo local de administradores.

  - Compruebe que el servidor de acceso de cliente esté instalado, en el mismo ordenador que el servidor de buzones de correo o en otro equipo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del complemento Servicios de MMC para detener el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange

1.  Haga clic en **Inicio** y, a continuación, en **Panel de control**.

2.  En el Panel de control, haga doble clic en **Herramientas administrativas**.

3.  En **Herramientas administrativas**, haga doble clic en **Servicios**.

4.  En el panel de detalles **Servicios**, haga clic con el botón secundario en **Enrutador de llamadas de mensajería unificada de Microsoft Exchange** y, a continuación, haga clic en **Detener**.

## Uso de un símbolo del sistema para detener el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange

1.  Haga clic en **Inicio** y, a continuación, haga clic en **Ejecutar**.

2.  En el cuadro **Abrir**, escriba el siguiente comando y, a continuación, presione Entrar.
    
  ```powershell
  net stop MSExchangeUMCR
  ```

