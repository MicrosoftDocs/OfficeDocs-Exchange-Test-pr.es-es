---
title: 'Configurar el correo de voz protegido de los llamadores no autenticados: Exchange 2013 Help'
TOCTitle: Configurar el correo de voz protegido de los llamadores no autenticados
ms:assetid: 106bfa0a-a0fa-4a1b-bd59-4b6df1d0d61d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335098(v=EXCHG.150)
ms:contentKeyID: 52061787
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el correo de voz protegido de los llamadores no autenticados

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Puede configurar Mensajería unificada para que responda una llamada entrante y luego determinar si aplicará protección a los mensajes de correo de voz con cifrado. Cuando un mensaje de correo de voz está protegido:

  - El mensaje está marcado como Privado en Microsoft Outlook y Outlook Web App.

  - El mensaje de voz únicamente lo puede abrir el destinatario del mensaje de voz.

  - El destinatario puede contestar el mensaje de voz, pero no lo puede reenviar a una persona que no esté incluida en el mensaje de voz original.

Esta configuración se aplica a los mensajes de voz enviados a usuarios habilitados para MU cuando éstos no responden el teléfono. Esta opción también se aplica a los mensajes de voz enviados directamente a los usuarios habilitados para MU cuando la persona que llama usa un operador automático de MU.

Para otras tareas de administración relacionadas con los procedimientos del correo de voz protegido, consulte [Procedimientos de correo de voz protegidos](protected-voice-mail-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar el correo de voz protegido de llamadores no autenticados

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de mensajería unificada**, seleccione la directiva de buzón de UM que quiera administrar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzones de mensajería unificada** \> **Correo de voz protegido**, en **Proteger mensajes de voz de autores de llamadas no autenticados**, seleccione una de las opciones siguientes:
    
      - **Ninguno** Use esta configuración cuando no quiera que se aplique protección a ninguno de los mensajes de voz enviados a los usuarios habilitados para mensajería unificada.
    
      - **Privado** Use esta configuración si quiere que la mensajería unificada aplique la protección solo a los mensajes de voz marcados como privados por el autor de la llamada.
    
      - **Todos** Use esta configuración si quiere que la mensajería unificada aplique la protección a todos los mensajes de voz, incluidos aquellos no marcados como privados.

4.  Haga clic en **Guardar**.

## Usar el Shell para configurar el correo de voz protegido de personas que llaman sin autenticación

En este ejemplo, se protegen todos los mensajes de voz de todas las personas que llaman sin autenticación en la directiva de buzón de MU `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectUnauthenticatedVoiceMail -All

