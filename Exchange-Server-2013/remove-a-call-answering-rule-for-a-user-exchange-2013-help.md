---
title: 'Quitar una regla de respuesta a llamadas para un usuario: Exchange 2013 Help'
TOCTitle: Quitar una regla de respuesta a llamadas para un usuario
ms:assetid: 1da3c5bc-7227-4b37-96f6-67ceefc084d5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ898497(v=EXCHG.150)
ms:contentKeyID: 51406483
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar una regla de respuesta a llamadas para un usuario

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-04-08_

Puede usar el Shell para quitar una o varias reglas de contestador automático para un usuario. También puede usar el cmdlet **Remove-UMCallAnsweringRule** en un script del Shell de administración de Exchange para quitar una o varias reglas del mismo tipo en varios usuarios.

El modo en que se aplican las reglas de contestador automático a las llamadas entrantes es parecido al modo en que se aplican las reglas de bandeja de entrada a los mensajes de correo entrantes. De manera predeterminada, cuando un usuario se habilita para Mensajería unificada (UM), no se configuran reglas de contestador automático. Aun así, el sistema de correo contesta a las llamadas entrantes e invita a los llamadores a que dejen un mensaje de voz.


> [!NOTE]
> Los usuarios habilitados para UM pueden iniciar sesión en Outlook Web App para crear, administrar y quitar reglas de contestador automático.



Para otras tareas de administración relacionadas con las reglas del contestador automático, vea [Reenvío de llamadas a procedimientos](forwarding-calls-procedures-exchange-2013-help.md).

## ¿Qué necesito saber antes de empezar?

  - Tiempo estimado para finalizar: menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Reglas del contestador automático de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo esta tarea, confirme que se haya creado un plan de marcado de UM. Puede ver los pasos detallados en [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo esta tarea, confirme que se haya creado una directiva de buzón de UM. Puede ver los pasos detallados en [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo esta tarea, confirme que el buzón del usuario esté habilitado para UM. Puede ver los pasos detallados en [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento. Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)). Para obtener información sobre cómo usar Windows PowerShell para conectarse a Exchange Online, vea [Conexión a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para quitar una regla de contestador automático

En este ejemplo se quita la regla de contestador automático `MyUMCallAnsweringRule` del buzón de un usuario. El buzón de usuario es el buzón que ejecuta el cmdlet.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

En este ejemplo se deshabilita la regla de contestador automático `MyUMCallAnsweringRule` en el buzón de Tony Smith.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

