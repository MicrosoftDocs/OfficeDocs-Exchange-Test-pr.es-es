---
title: 'Configurar correo de voz protegido de llamadores autenticados: Exchange 2013 Help'
TOCTitle: Configurar correo de voz protegido de llamadores autenticados
ms:assetid: f69e94a7-9768-4445-9ded-e78d732bd623
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423560(v=EXCHG.150)
ms:contentKeyID: 52061907
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar correo de voz protegido de llamadores autenticados

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede configurar la mensajería unificada para que responda a una llamada entrante y, a continuación, determinar si aplicará protección a los mensajes de correo de voz usando el cifrado. Cuando un mensaje de voz está protegido:

  - El mensaje se marca como privado en Microsoft Outlook y Outlook Web App.

  - El mensaje de voz solo lo puede abrir su destinatario deseado.

  - El destinatario puede responder al mensaje de voz, pero no puede reenviárselo a alguien que no esté incluido en el mensaje de voz original.

Esta configuración se aplica a los mensajes de voz enviados a los usuarios habilitados para mensajería unificada cuando éstos no responden el teléfono. Este parámetro también se aplica cuando las personas que llaman inician sesión en su buzón mediante Outlook Voice Access, y desde ahí crean y envían un mensaje de voz.

Para otras tareas de administración relacionadas con los procedimientos de correo de voz protegido, consulte [Procedimientos de correo de voz protegidos](protected-voice-mail-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar el correo de voz protegido de los autores de llamadas autenticados

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzón de mensajería unificada que desee administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de mensajería unificada** \> **Correo de voz protegido**, en **Proteger mensajes de voz de personas que llaman autenticadas**, seleccione una de las siguientes opciones:
    
      - **Ninguno**   Use esta configuración cuando no desee que se aplique protección a los mensajes de voz enviados a los usuarios habilitados para mensajería unificada.
    
      - **Privado**   Use esta configuración si desea que la mensajería unificada aplique la protección únicamente a los mensajes de voz marcados como privados por el autor de la llamada.
    
      - **Todos**   Use esta configuración si desea que la mensajería unificada aplique la protección a todos los mensajes de voz, incluidos aquellos no marcados como privados.

4.  Haga clic en **Guardar**.

## Usar el Shell para configurar el correo de voz protegido de personas autenticadas que llaman

En este ejemplo se protegen los mensajes de voz de todas las personas autenticadas que llaman en la directiva de buzón de mensajería unificada de `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy ProtectAuthenticatedVoiceMail -All

