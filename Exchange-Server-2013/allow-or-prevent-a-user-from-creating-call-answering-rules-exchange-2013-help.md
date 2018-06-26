---
title: 'Permitir o impedir la creación de reglas de respuesta de llamada de un usuario: Exchange 2013 Help'
TOCTitle: Permitir o impedir la creación de reglas de respuesta de llamada de un usuario
ms:assetid: 81863440-8b21-4523-bdab-6a2311889a0d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298097(v=EXCHG.150)
ms:contentKeyID: 50556835
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir o impedir la creación de reglas de respuesta de llamada de un usuario

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Puede especificar si desea que los usuarios individuales puedan crear y administrar sus propias reglas de contestador automático mediante la configuración de las propiedades de su buzón. De forma predeterminada, puede crear reglas de contestador automático.

Puede habilitar o deshabilitar reglas de contestador automático para varios usuarios con mensajería unificada habilitada configurando reglas de contestador automático en un plan de marcado de mensajería unificada o una directiva de buzones de mensajería unificada.


> [!NOTE]
> No puede usar el EAC para configurar esta característica. Debe usar el Shell para habilitar o deshabilitar reglas de contestador automático para un usuario de correo de voz.



Para otras tareas de administración relacionadas con autorizar usuarios a desviar llamadas, consulte [Reenvío de llamadas a procedimientos](forwarding-calls-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva para los buzones de MU. Para obtener instrucciones detalladas, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el buzón del usuario esté habilitado para MU. Para obtener instrucciones detalladas, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para habilitar o deshabilitar reglas de contestador automático para un usuario habilitado para MU

Este ejemplo habilita reglas de contestador automático para el usuario tony@contoso.com.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $true

En este ejemplo, se deshabilitan las reglas de contestador automático para el usuario antonio@contoso.com.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $false

