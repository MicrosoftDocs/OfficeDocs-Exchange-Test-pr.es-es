---
title: 'Agregar servidores de acceso de cliente y buzón a un plan de marcado de URI de SIP: Exchange 2013 Help'
TOCTitle: Agregar servidores de acceso de cliente y buzón a un plan de marcado de URI de SIP
ms:assetid: 17fed308-ff0d-4e61-b9f9-e6680b6eccaa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996399(v=EXCHG.150)
ms:contentKeyID: 52062006
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agregar servidores de acceso de cliente y buzón a un plan de marcado de URI de SIP

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-16_

Puede agregar servidores de acceso de cliente y de buzones a los planes de marcado URI de SIP. Los servidores de acceso de cliente y de buzones no se pueden asociar con planes de marcado de extensión telefónica ni E.164, pero responderán a todas las llamadas entrantes.

Si va a implementar Microsoft Lync Server, para que las llamadas salientes funcionen correctamente, debe agregar manualmente todos los servidores de acceso de cliente y de buzones a los planes de marcado URI de SIP que haya creado para Lync Server.

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estas tareas, confirme que se haya creado un plan de marcado URI de SIP. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](https://technet.microsoft.com/es-es/library/bb123819(v=exchg.150)).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para agregar un servidor de buzones a un plan de marcado URI de SIP

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor de buzones que quiere modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración del servicio de mensajería unificada** \> **Planes de marcado asociados**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

5.  En la ventana **Seleccionar un plan de marcado de mensajería unificada**, seleccione el plan de marcado URI de SIP, haga clic en **Agregar**, en **Aceptar** y, por último, en **Guardar**.

## Usar el Shell para agregar un servidor de buzones a un plan de marcado URI de SIP

En este ejemplo se añade el servidor de buzones `MyMailboxServer` a un plan de marcado URI de SIP denominado `MySIPDialPlan` y se impide que acepte nuevas llamadas. Además, establece el modo de inicio en Dual, que permite que el servidor de buzones acepte solicitudes TCP y TLS.

```powershell
Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan -Status Disabled -UMStartupMode Dual
```

En este ejemplo se agrega el servidor de buzones `MyMailboxServer` a dos planes de marcado SIP denominados `MySIPDialPlan` y `MySIPDialPlan2`, y se define lo siguiente:

  - Permite direcciones IPv4 e IPv6.

  - Establece el número máximo de llamadas entrantes en 50.

  - Configura el Servicio de acceso SIP para Lync Server.

<!-- end list -->

```powershell
Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -MaxCallsAllowed 50 -SipAccessService northamerica.lyncpoolna.contoso.com
```

## Usar el EAC para agregar un servidor de acceso de cliente a un plan de marcado URI de SIP

1.  En el EAC, vaya a **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor de acceso de cliente que quiere modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración del enrutador de llamadas de mensajería unificada** \> **Planes de marcado asociados**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

5.  En la ventana **Seleccionar un plan de marcado de mensajería unificada**, seleccione el plan de marcado URI de SIP, haga clic en **Agregar**, en **Aceptar** y, por último, en **Guardar**.

## Usar el Shell para agregar un servidor de acceso de cliente a un plan de marcado URI de SIP

En este ejemplo se agrega el servidor de acceso de cliente llamado `MyClientAccessServer` a un plan de marcado URI de SIP denominado `MySIPDialPlan`. También se establece el modo de inicio en Dual, que permite que el servidor de acceso de cliente acepte solicitudes TCP y TLS.

```powershell
Set-UMCallRouterSettings -DialPlans MySIPDialPlan -Server MyClientAccessServer -UMStartupMode Dual
```

En este ejemplo se agrega el servidor de acceso de cliente llamado `MyClientAccessServer` a dos planes de marcado SIP (`MySIPDialPlan` y `MySIPDialPlan2`) y se permite al servidor usar las direcciones IPv4 e IPv6.

```powershell
Set-UMCallRouterSettings -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -Server MyClientAccessServer
```

