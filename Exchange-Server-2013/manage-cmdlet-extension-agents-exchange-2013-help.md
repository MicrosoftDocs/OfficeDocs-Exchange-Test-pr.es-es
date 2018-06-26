---
title: 'Administrar los agentes de extensión de cmdlet: Exchange 2013 Help'
TOCTitle: Administrar los agentes de extensión de cmdlet
ms:assetid: 9141b3cb-ad13-4415-be2f-aa89f91445f5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298143(v=EXCHG.150)
ms:contentKeyID: 50556859
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar los agentes de extensión de cmdlet

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-11-19_

Este tema le muestra cómo habilitar, deshabilitar, ver y cambiar la prioridad de los agentes de extensiones cmdlet en Microsoft Exchange Server 2013. Para obtener más información acerca de los agentes de extensión del cmdlet Exchange 2013, consulte [Agentes de extensión de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: menos de 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Agentes de extensión de cmdlet" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Antes de habilitar `Scripting Agent`, debe comprobar que está configurado correctamente. Para obtener más información acerca de `Scripting Agent`, consulte [Agentes de extensión de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Habilitar un agente de extensión de cmdlet

Cuando habilita un agente de extensión de cmdlet en Exchange 2013, el agente se ejecuta en cada servidor que ejecuta Exchange 2013 en la organización. Cuando se habilita un agente, queda disponible para cmdlets que, a continuación, pueden usar al agente para realizar operaciones adicionales.


> [!WARNING]
> Antes de habilitar un agentes, asegúrese de saber cómo funciona el agente y qué impacto tendrá en su organización.



En este ejemplo, se habilita a un agente de extensión de cmdlet mediante el cmdlet **Enable-CmdletExtensionAgent**. Debe especificar el nombre del agente que desea habilitar al ejecutar el cmdlet. Antes de habilitar `Scripting Agent`, debe asegurarse de haber implementado el archivo de configuración `ScriptingAgentConfig.xml` en todos los servidores de la organización. Si no implementa primero el archivo de configuración y habilita `Scripting``Agent`, todos los cmdlets no **Get** fallarán cuando se ejecuten. En este ejemplo, se habilita `Scripting Agent`.

    Enable-CmdletExtensionAgent "Scripting Agent"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Enable-CmdletExtensionAgent](https://technet.microsoft.com/es-es/library/dd335192\(v=exchg.150\)).

## Deshabilitar un agente de extensión de cmdlet

Si se deshabilita un agente de extensión de cmdlet en Exchange 2013, el agente se deshabilita en cada servidor de la organización que ejecute Exchange 2013. Cuando un agente está deshabilitado, no está disponible para los cmdlets. Los cmdlets ya no pueden usar al agente para realizar operaciones adicionales.


> [!WARNING]
> Antes de deshabilitar un agente, asegúrese de saber cómo funciona el agente y las repercusiones que deshabilitarlo tendrá en su organización.



Para deshabilitar un agente de extensión de cmdlet , use el cmdlet **Disable-CmdletExtensionAgent** cmdlet. Indique el nombre del agente que desea deshabilitar al ejecutar el cmdlet. En este ejemplo, se deshabilita `Scripting Agent`.

    Disable-CmdletExtensionAgent "Scripting Agent"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Disable-CmdletExtensionAgent](https://technet.microsoft.com/es-es/library/dd298132\(v=exchg.150\)).

## Ver agentes de extensión de cmdlet existentes

Ver agentes de extensión de cmdlet le permite ver los agentes que se ejecutan primero en una organización de Exchange 2013. Para obtener más información acerca de la canalización y del cmdlet **Format-Table**, consulte los temas siguientes:

  - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))

  - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

En este ejemplo, se obtienen los detalles de un agente de extensión de cmdlet específico al usar el cmdlet **Get-CmdletExtensionAgent**. En este ejemplo, se devuelven los detalles de `Mailbox Permissions Agent`.

    Get-CmdletExtensionAgent "Mailbox Permissions Agent"

En este ejemplo, se obtienen agentes de extensión de cmdlet múltiples al usar el cmdlet **Get-CmdletExtensionAgent** y, a continuación, se canaliza la salida al cmdlet **Format-Table**. En este ejemplo, se muestra una lista de todos los agentes de extensión de cmdlet en la organización y, al usar el cmdlet **Format-Table**, las propiedades **Name**, **Enabled** y **Priority** de cada agente se muestran en una tabla.

    Get-CmdletExtensionAgent | Format-Table Name, Enabled, Priority

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-CmdletExtensionAgent](https://technet.microsoft.com/es-es/library/dd297946\(v=exchg.150\)).

## Cambiar la prioridad de un agente de extensión de cmdlet

La capacidad de cambiar la prioridad de un agente de extensión de cmdlet en Exchange 2013 es útil cuando desea que un cmdlet llame a un agente determinado antes que otro. Esto es útil en especial si crea un script personalizado que se ejecuta en el `Scripting Agent` y desea que ese script tenga prioridad con respecto a un agente integrado. Para obtener más información acerca de `Scripting Agent`, consulte [Agentes de extensión de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).


> [!WARNING]
> Cambiar la prioridad o reemplazar la funcionalidad de un agente integrado es una operación avanzada. Asegúrese de comprender por completo los cambios que realiza.



Los agentes se ordenan de cero al número máximo de agentes. Cuando más cercano a cero esté el agente, mayor será su prioridad. Se llama primero a los agentes con mayor prioridad. Para obtener más información acerca de las prioridades de los agentes, consulte [Agentes de extensión de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

En este ejemplo, se cambia la prioridad de un agente de extensión de cmdlet por medio del cmdlet **Set-CmdletExtensionAgent**. En este ejemplo, la prioridad del `Scripting Agent` se cambia a 3.

    Set-CmdletExtensionAgent "Scripting Agent" -Priority 3

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-CmdletExtensionAgent](https://technet.microsoft.com/es-es/library/dd335175\(v=exchg.150\)).

