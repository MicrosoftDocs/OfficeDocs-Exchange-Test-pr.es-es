---
title: 'Quitar servidores de buzón y acceso de cliente de plan marcado de URI de SIP'
TOCTitle: Quitar servidores de buzón y acceso de cliente de un plan de marcado de URI de SIP
ms:assetid: 367441e1-1a0f-42c8-9fa8-8abe80b3d015
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997238(v=EXCHG.150)
ms:contentKeyID: 54652431
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar servidores de buzón y acceso de cliente de un plan de marcado de URI de SIP

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-16_

Puede quitar servidores de acceso de cliente y de buzones de los planes de marcado URI de SIP. Cuando va a implementar Microsoft Lync Server, para que las llamadas salientes funcionen correctamente, debe agregar manualmente todos los servidores de acceso de cliente y de buzones a los planes de marcado URI de SIP que haya creado para Lync Server. Sin embargo, puede que tenga que quitar un servidor de acceso de cliente o de buzones de la implementación de Lync, por ejemplo, si está haciendo tareas de mantenimiento o va a desconectar el servidor.

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesito saber antes de empezar?

  - Tiempo estimado para finalizar: menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estas tareas, confirme que se haya creado un plan de marcado URI de SIP. Puede ver los pasos detallados en [Crear un plan de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué quiere hacer?

## Usar el EAC para quitar un servidor de buzones de un plan de marcado URI de SIP

1.  En el EAC, vaya a **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor de buzones que quiere modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración del servicio de mensajería unificada** \> **Planes de marcado asociados**, busque el plan de marcado URI de SIP que quiere quitar y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") y en **Guardar**. Si quiere quitar más de un plan de marcado URI de SIP, mantenga presionada la tecla CTRL, seleccione los planes de marcado que quiere quitar y luego haga clic en **Guardar**.

## Usar el Shell para quitar un servidor de buzones de un plan de marcado URI de SIP

En este ejemplo se quita el servidor de buzones `MyMailboxServer` de un plan de marcado URI de SIP denominado `MySIPDialPlan`.

```powershell
$dp= Get-UMDialPlan "MySIPDialPlan"
$s=Get-UMService MyMailboxServer
$s.dialplans-=$dp.identity
Set-UMService -id MyMailboxServer -dialplans:$s.dialplans
```

En este ejemplo, hay tres planes de marcado URI de SIP: SipDP1, SipDP2 y SipDP3. En este ejemplo se quita el servidor de buzones `MyMailboxServer` del plan de marcado SipDP3.

```powershell
Set-UMService -id MyMailboxServer -DialPlans SipDP1,SipDP2
```

En este ejemplo, hay dos planes de marcado URI de SIP: SipDP1 y SipDP2. En este ejemplo se quita el servidor de buzones `MyMailboxServer` del plan de marcado SipDP2.

```powershell
Set-UMService -id MyMailboxServer -DialPlans SipDP1
```

En este ejemplo se quita el servidor de buzones `MyMailboxServer` de todos los planes de marcado de SIP.

```powershell
Set-UMService -id MyUMServer -DialPlans $null
```

## Usar el EAC para quitar un servidor de acceso de cliente de un plan de marcado URI de SIP

1.  En el EAC, vaya a **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor de acceso de cliente que quiere modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración del enrutador de llamadas de mensajería unificada** \> **Planes de marcado asociados**, busque el plan de marcado URI de SIP que quiere quitar y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") y en **Guardar**. Si quiere quitar más de un plan de marcado URI de SIP, mantenga presionada la tecla CTRL, seleccione los planes de marcado que quiere quitar y luego haga clic en **Guardar**.

## Usar el Shell para quitar un servidor de acceso de cliente de un plan de marcado URI de SIP

En este ejemplo se quita el servidor de acceso de cliente `MyClientAccessServer` de un plan de marcado URI de SIP denominado `MySIPDialPlan`.

```powershell
$dp= Get-UMDialPlan "MySIPDialPlan"
$s=Get-UMCallRouterSettings MyClientAccessServer
$s.dialplans-=$dp.identity
Set-UMCallRouterSettings -id MyClientAccessServer -dialplans:$s.dialplans
```

En este ejemplo, hay tres planes de marcado URI de SIP: SipDP1, SipDP2 y SipDP3. En este ejemplo se quita el servidor de acceso de cliente `MyClientAccessServer` del plan de marcado SipDP3.

```powershell
Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1,SipDP2
```

En este ejemplo, hay dos planes de marcado URI de SIP: SipDP1 y SipDP2. En este ejemplo se quita el servidor de acceso de cliente `MyClientAccessServer` del plan de marcado SipDP2.

```powershell
Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1
```

En este ejemplo se quita el servidor de acceso de cliente `MyClientAccessServer` de todos los planes de marcado de SIP.

```powershell
Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans $null
```