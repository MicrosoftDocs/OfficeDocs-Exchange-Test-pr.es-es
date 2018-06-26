---
title: 'Iniciar el servicio de mensajería unificada de Microsoft Exchange: Exchange 2013 Help'
TOCTitle: Iniciar el servicio de mensajería unificada de Microsoft Exchange
ms:assetid: b54008e6-172e-4435-8516-57cff740e89c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124330(v=EXCHG.150)
ms:contentKeyID: 50556869
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Iniciar el servicio de mensajería unificada de Microsoft Exchange

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-16_

Puede utilizar el complemento Servicios de Microsoft Management Console (MMC) o cmd.exe en un símbolo del sistema para iniciar el servicio de mensajería unificada de Microsoft Exchange en un servidor de buzones. De manera predeterminada, el servicio de mensajería unificada de Microsoft Exchange se inicia después de instalar un servidor de buzones. No obstante, puede haber ocasiones en las que deba reiniciar el servicio de mensajería unificada de Microsoft Exchange manualmente como, por ejemplo, cuando haya desconectado el servidor de buzones y tenga que conectarlo de nuevo.

Cuando el servicio de mensajería unificada de Microsoft Exchange se inicia en un servidor de buzones, este está disponible para responder y procesar llamadas entrantes de mensajería unificada.

Para otras tareas de administración relacionadas con los servidores de buzones, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Para ejecutar los siguientes procedimientos, debe iniciar sesión en el servidor de buzones mediante una cuenta que sea miembro del grupo de administradores locales.

  - Compruebe que el servidor de buzones está instalado, ya sea en el mismo equipo que el servidor de acceso de clientes o en otro distinto.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del complemento Servicios de MMC para iniciar el servicio de mensajería unificada de Microsoft Exchange

1.  Haga clic en **Inicio** y, a continuación, en **Panel de control**.

2.  En el Panel de control, haga doble clic en **Herramientas administrativas**.

3.  En **Herramientas administrativas**, haga doble clic en **Servicios**.

4.  En el panel de detalles de **Servicios**, haga clic con el botón secundario en **Mensajería unificada de Microsoft Exchange** y, a continuación, haga clic en **Iniciar**.

## Uso de un símbolo del sistema para iniciar el servicio de mensajería unificada de Microsoft Exchange

1.  Haga clic en **Inicio** y, a continuación, haga clic en **Ejecutar**.

2.  En el cuadro **Abrir**, escriba el siguiente comando y, a continuación, presione Entrar.
    
        net start MSExchangeUM

