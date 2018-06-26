---
title: 'Configurar el modo de inicio en un servidor de acceso de cliente: Exchange 2013 Help'
TOCTitle: Configurar el modo de inicio en un servidor de acceso de cliente
ms:assetid: 71cc9061-9e3c-4b4a-8dbe-f590ca5bcee8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673533(v=EXCHG.150)
ms:contentKeyID: 50556814
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el modo de inicio en un servidor de acceso de cliente

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-15_

Es posible especificar el modo de inicio del servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange en un servidor de acceso de cliente. De forma predeterminada, el servidor de acceso de cliente se iniciará en el modo TCP, pero si utiliza Seguridad de la capa de transporte (TLS) para cifrar el tráfico de voz sobre IP (VoIP), debe configurar el servidor de acceso de cliente para que utilice el modo Dual o TLS. Le recomendamos configurar los servidores de acceso de cliente para que usen el modo Dual como modo de inicio. Esto se debe a que los servidores de acceso de cliente y de buzones de correo pueden responder a todas las llamadas entrantes para todos los planes de marcado de mensajería unificada, y esos planes de marcado pueden tener una configuración de seguridad de distinta. Si cambia el modo de inicio, debe reiniciar el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange para que el cambio se aplique.


> [!IMPORTANT]
> De forma predeterminada, los servidores de acceso de cliente están disponibles para contestar las llamadas entrantes. No tiene que añadir un plan servidor de acceso de cliente a un plan de marcado de mensajería unificada para procesar llamadas de mensajería unificada a no ser que integre la mensajería unificada y el Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server.



Para consultar otras tareas de administración relacionadas con la mensajería unificada y los servidores de acceso de clientes, vea [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servidor de acceso de cliente (servicio de enrutamiento de llamadas de mensajería unificada)" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que el servidor de acceso de cliente esté instalado, en el mismo ordenador que el servidor de buzones de correo o en otro equipo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar el modo de inicio en un servidor de acceso de clientes

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor Exchange que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración de enrutador de llamadas de mensajería unificada** \> **Modo de inicio de mensajería unificada**, seleccione una de las siguientes opciones de la lista desplegable:
    
      - **TCP** Utilice esta opción si no utiliza mTLS y utiliza únicamente planes de marcado no seguros.
    
      - **TLS** Utilice esta opción si utiliza mTLS y utiliza únicamente planes de marcado SIP protegidos o planes de marcado seguros.
    
      - **DUAL** Utilice esta opción si utiliza mTLS y utiliza planes de marcado no seguros, planes de marcado SIP protegidos y planes de marcado seguros.

5.  Después de seleccionar el modo de inicio de mensajería unificada, haga clic en **Guardar**.

## Usar el Shell para configurar el modo de inicio en un servidor de acceso de cliente

En este ejemplo, se establece el modo de inicio para un servidor de acceso de clientes denominado `UMCallRouter1` en modo dual.

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode Dual

En este ejemplo, se establece el modo de inicio para un servidor de acceso de clientes denominado `UMCallRouter1` en modo TLS.

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode TLS

