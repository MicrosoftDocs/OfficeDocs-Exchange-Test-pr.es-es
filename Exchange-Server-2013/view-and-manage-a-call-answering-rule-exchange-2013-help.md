---
title: 'Ver y administrar una regla de respuesta a llamada: Exchange 2013 Help'
TOCTitle: Ver y administrar una regla de respuesta a llamada
ms:assetid: de6d9fa1-7878-49a9-bddb-e3317d94f4d8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn140251(v=EXCHG.150)
ms:contentKeyID: 54652418
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver y administrar una regla de respuesta a llamada

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2015-04-08_

Puede usar el Shell para ver o configurar una o varias reglas de respuesta a llamada para un usuario. También puede usar los cmdlets **Get-UMCallAnsweringRule** o **Set-UMCallAnsweringRule** en un script del Shell de administración de Exchange para ver o administrar reglas de respuesta a llamada para varios usuarios.

El modo en que se aplican las reglas de respuesta a llamada a las llamadas entrantes es similar al modo en que se aplican las reglas de bandeja de entrada a los mensajes de correo electrónico entrantes. De manera predeterminada, cuando un usuario está habilitado para la mensajería unificada (UM), no se configuran reglas de respuesta a llamada. A pesar de ello, el sistema de correo responde las llamadas entrantes y les pide a los autores de la llamada que dejen un mensaje de voz.


> [!IMPORTANT]
> Los usuarios que tienen la mensajería unificada habilitada pueden iniciar sesión en Outlook Web App para crear, administrar y quitar reglas de respuesta a llamada.



Para otras tareas de administración relacionadas con reglas de respuesta a llamada, vea [Reenvío de llamadas a procedimientos](forwarding-calls-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de empezar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Reglas de respuesta a llamada de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de mensajería unificada. Para conocer los pasos detallados, vea [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo este procedimiento, confirme que se haya creado una directiva para los buzones de mensajería unificada. Para conocer los pasos detallados, vea [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo este procedimiento, confirme que el buzón del usuario esté habilitado para mensajería unificada. Para conocer los pasos detallados, vea [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento. Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)). Para obtener información sobre cómo usar Windows PowerShell para conectarse a Exchange Online, vea [Conexión a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué quiere hacer?

## Usar el Shell para ver una regla de respuesta a llamada

Puede recuperar las propiedades de una sola regla de respuesta a llamada o una lista de reglas de respuesta a llamada en un buzón de correo de usuario habilitado para mensajería unificada.

En este ejemplo se muestra una lista con formato de las reglas de respuesta a llamada en un buzón de correo habilitado para mensajería unificada.

    Get-UMCallAnsweringRule-Mailbox tonysmith | Format-List

En este ejemplo se muestran las propiedades de la regla de respuesta a llamada `MyUMCallAnsweringRule`.

    Get-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

## Usar el Shell para configurar una regla de respuesta a llamada

Puede configurar o cambiar una regla de respuesta a llamada que está almacenada en el buzón del usuario. Puede especificar las siguientes condiciones:

  - Persona que realiza la llamada

  - Hora del día

  - Estado de disponibilidad del calendario

  - Si las respuestas automáticas están activadas para el correo electrónico

También puede especificar las siguientes acciones:

  - Encontrarme

  - Transferir la llamada a otra persona

  - Dejar un mensaje de voz

En este ejemplo se establece la prioridad en 2 para la regla de respuesta a llamada `MyCallAnsweringRule` que existe en el buzón de correo para Tony Smith.

    Set-UMCallAnsweringRule -Mailbox tonysmith -Name MyCallAnsweringRule -Priority 2

En este ejemplo se realizan las siguientes acciones en la regla de respuesta a llamada `MyCallAnsweringRule` en el buzón de correo para Tony Smith:

  - Establece la regla de respuesta a llamada en dos identificadores de llamada.

  - Establece la prioridad de la regla de respuesta a llamada en 2.

  - Establece la regla de respuesta a llamada que permite a los autores de la llamada interrumpir el saludo.

<!-- end list -->

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

En este ejemplo se cambia el estado de la disponibilidad a "Fuera de la oficina" en la regla de respuesta a llamada `MyCallAnsweringRule` en el buzón de correo para Tony Smith y se establece la prioridad en 2.

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith@contoso.com -ScheduleStatus 0x8

