---
title: 'Configurar el modo de inicio en un servidor de buzones: Exchange 2013 Help'
TOCTitle: Configurar el modo de inicio en un servidor de buzones
ms:assetid: 4457d6a0-52bd-4269-8cb5-d34d7fe9bfc3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423544(v=EXCHG.150)
ms:contentKeyID: 50556778
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el modo de inicio en un servidor de buzones

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-15_

Es posible especificar el modo de inicio del servicio de mensajería unificada de Microsoft Exchange en un servidor de buzones. De manera predeterminada, el servidor de buzones se iniciará en el modo TCP, pero si usa Seguridad de la capa de transporte (TLS) para cifrar el tráfico de voz sobre IP (VoIP), debe configurar el servidor de buzones para que use el modo Dual o TLS. Recomendamos configurar los servidores de buzones para usar Dual como modo de inicio. Esto es porque todos los servidores de acceso de cliente y de buzones pueden responder las llamadas entrantes para todos los planes de marcado de MU, y esos planes de marcado pueden tener una configuración de seguridad distinta (No protegida, SIP protegida o Protegida). Si cambia el modo de inicio, debe reiniciar el servicio de mensajería unificada de Microsoft Exchange para que el cambio se aplique.


> [!IMPORTANT]
> De manera predeterminada, los servidores de buzones están disponibles para contestar las llamadas entrantes. No es necesario que agregue un servidor de buzones a un plan de marcado de MU para procesar llamadas de mensajería unificada, a menos que integre la MU y Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server.



Para tareas de administración adicionales relacionadas con servidores de buzones y mensajería unificada, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servidor de buzones de correo (servicio de mensajería unificada)" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que el servidor de buzones está instalado, bien en el mismo equipo que el servidor de acceso de clientes o en otro distinto.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para configurar el modo de inicio en un servidor de buzones

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor Exchange que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración del servicio de mensajería unificada** \> **Modo de inicio de mensajería unificada**, seleccione una de las siguientes opciones de la lista desplegable:
    
      - **TCP** Utilice esta opción si no utiliza mTLS y utiliza únicamente planes de marcado no seguros.
    
      - **TLS** Utilice esta opción si utiliza mTLS y utiliza únicamente planes de marcado SIP protegidos o planes de marcado seguros.
    
      - **DUAL** Utilice esta opción si utiliza mTLS y utiliza planes de marcado no seguros, planes de marcado SIP protegidos y planes de marcado seguros.

5.  Después de seleccionar el modo de inicio de mensajería unificada, haga clic en **Guardar**.

## Uso del Shell para configurar el modo de inicio en un servidor de buzones

En este ejemplo se establece el modo de inicio para un servidor de buzones denominado `MyUMServer1` en modo Dual.

```powershell
Set-UMService -Identity MyUMServer1 -UMStartUpMode Dual
```

En este ejemplo se establece el modo de inicio para un servidor de buzones denominado `MyUMServer1` en modo TLS.

```powershell
Set-UMService -Identity MyUMServer1 -UMStartUpMode TLS
```

