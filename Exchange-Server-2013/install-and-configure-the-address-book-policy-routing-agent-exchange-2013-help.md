---
title: 'Instalar y configurar agente enrutamiento directivas libretas direcciones'
TOCTitle: Instalar y configurar al agente de enrutamiento de directivas de libretas de direcciones
ms:assetid: 20e8a43d-4508-4388-a2c9-aa3073593cc2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ907308(v=EXCHG.150)
ms:contentKeyID: 51406485
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Instalar y configurar al agente de enrutamiento de directivas de libretas de direcciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-01-09_

El agente de enrutamiento de directivas de libretas de direcciones es un agente de transporte que se ejecuta en el servidor de buzones que controla cómo se resuelven los destinatarios en la organización. Cuando el agente de enrutamiento de ABP se instala y configura, los usuarios asignados a diferentes GAL aparecen como destinatarios externos que no pueden ver las tarjetas de contacto de los destinatarios externos.

Para otras tareas de administración relacionadas con las directivas de libretas de direcciones (ABP), consulte [Procedimientos de directivas de la libreta de direcciones](address-book-policy-procedures-exchange-2013-help.md).

¿Busca la versión de Exchange Online de este tema? Vea [Activar el enrutamiento de directivas de la libreta de direcciones](https://technet.microsoft.com/es-es/library/jj891095\(v=exchg.150\)).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea:  15 minutos.

  - Tras instalar y configurar el agente de enrutamiento de ABP, este puede tardar hasta 30 minutos en evaluar el correo de la organización.

  - No puede usar la EAC para realizar este proceso. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Instalar el agente de enrutamiento de ABP

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Agentes de transporte" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

Instale el agente de enrutamiento de ABP ejecutando el siguiente comando. Este es el comando y la sintaxis exactos que tiene que usar.

    Install-TransportAgent -Name "ABP Routing Agent" -TransportAgentFactory "Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.AddressBookPolicyRoutingAgentFactory" -AssemblyPath $env:ExchangeInstallPath\TransportRoles\agents\AddressBookPolicyRoutingAgent\Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.dll

Recibirá una advertencia de que el servicio de transporte debe reiniciarse para que los cambios se apliquen, pero primero debe realizar el paso 2 para reiniciar el servicio solo una vez.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Install-TransportAgent](https://technet.microsoft.com/es-es/library/aa997998\(v=exchg.150\)).

## Paso 2: Habilitar el agente de enrutamiento de transporte

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Agentes de transporte" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

Tras instalar el agente de enrutamiento de ABP, tiene que habilitarlo ejecutando el comando siguiente:

    Enable-TransportAgent "ABP Routing Agent"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Enable-TransportAgent](https://technet.microsoft.com/es-es/library/bb124921\(v=exchg.150\)).

## Paso 3: Reiniciar el servicio de transporte y comprobar que el agente de enrutamiento de ABP está instalado y habilitado

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Agentes de transporte" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

1.  Reinicie el servicio de transporte ejecutando el siguiente comando.
    
        Restart-Service MSExchangeTransport

2.  Después de reiniciar el servicio, compruebe que el agente de enrutamiento de ABP esté instalado y habilitado ejecutando el cmdlet siguiente.
    
        Get-TransportAgent
    
    Si aparece el agente de enrutamiento de ABP, quiere decir que se ha instalado correctamente.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-TransportAgent](https://technet.microsoft.com/es-es/library/bb123536\(v=exchg.150\)).

## Paso 4: Habilitar el agente de enrutamiento de ABP

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de transporte" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

El último paso de este proceso es habilitar el enrutamiento de ABP en la organización. Ejecute el siguiente comando.

    Set-TransportConfig -AddressBookPolicyRoutingEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-TransportConfig](https://technet.microsoft.com/es-es/library/bb124151\(v=exchg.150\)).

