---
title: 'Crear una regla de respuesta a llamadas: Exchange 2013 Help'
TOCTitle: Crear una regla de respuesta a llamadas
ms:assetid: 0976f8f2-3449-44f1-b0d1-20c91622e827
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ898495(v=EXCHG.150)
ms:contentKeyID: 51406473
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear una regla de respuesta a llamadas

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-04-08_

Para crear una o varias reglas de contestador automático para un usuario, se puede usar el Shell. También se puede usar el cmdlet **New-UMCallAnsweringRule** en un script del Shell de administración de Exchange para crear reglas de contestador automático para varios usuarios.

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



## Usar el Shell para crear una regla de contestador automático

En este ejemplo se crea la regla de contestador automático `MyCallAnsweringRule` en el buzón de correo de Tony Smith con la prioridad 2.

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith

En este ejemplo se crea la regla de contestador automático `MyCallAnsweringRule` en el buzón de correo de Tony Smith y se realizan las siguientes acciones:

  - Se establece la regla de contestador automático en dos identificadores de llamadores.

  - Se establece la prioridad de la regla de contestador automático en 2.

  - Se establece la regla de contestador automático que permite a los autores de la llamada interrumpir el saludo.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

En este ejemplo se crea la regla de contestador automático `MyCallAnsweringRule` en el buzón de correo de Tony Smith y se realizan las siguientes acciones:

  -  
    Se establece la prioridad de la regla de contestador automático en 2.

  -  
    Se crean asignaciones de teclas para la regla de contestador automático.

  -  
    Si el autor de la llamada conecta con el buzón de voz del usuario y el estado de este es "ocupado", el autor de la llamada puede:
    
      - Pulsar la tecla 1 para que se le transfiera a la recepcionista en la extensión 45678.
    
      - Pulsar la tecla 2 para que se use la función Buscarme para asuntos urgentes, llamar primero a la extensión 23456 y luego a la 45671.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith -ScheduleStatus 0x4 - -KeyMappings "1,1,Receptionist,,,,,45678,","5,2,Urgent Issues,23456,23,45671,50,,"

