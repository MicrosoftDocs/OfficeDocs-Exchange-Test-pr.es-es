---
title: 'Cambiar el plan de marcado de mensajería unificada: Exchange 2013 Help'
TOCTitle: Cambiar el plan de marcado de mensajería unificada
ms:assetid: 4a6b6b6f-c61c-44e8-91dd-c5d28835f441
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633465(v=EXCHG.150)
ms:contentKeyID: 49895612
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambiar el plan de marcado de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-05_

Puede que sea necesario mover un usuario habilitado para mensajería unificada (MU) a un plan de marcado de MU diferente o cambiar el plan de marcado asociado al usuario. Por ejemplo, puede que desee mover un usuario habilitado para mensajería unificada de un plan de marcado de extensión telefónica a un plan de marcado URI de SIP.

Para cambiar el plan de marcado de mensajería unificada, deberá deshabilitar el usuario para mensajería unificada y volver a habilitarlo en el nuevo plan de marcado de mensajería unificada. Esto sucede porque los distintos planes de marcado pueden tener configuraciones y requisitos diferentes, como longitudes de extensión distintas o tipos de URI diferentes. Por ejemplo, los planes de marcado URI de SIP necesitan un identificador de recurso SIP para que se puedan asignar a los buzones habilitados para MU, pero los planes de marcado de extensión telefónica no lo necesitan. Además, cada buzón de MU contiene referencias tanto del plan de marcado de MU como de la directiva de buzón de MU. A su vez, la directiva de buzón de MU también contiene referencias del plan de marcado de MU. Si cambia la dirección de proxy principal de un usuario habilitado para MU para que apunte a un plan de marcado distinto, el estado del buzón de MU será incoherente.

Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva para los buzones de MU. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que el destinatario Exchange existente tenga habilitada la mensajería unificada. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Cómo realiza esto?

## Paso 1: Crear el nuevo plan de marcado de mensajería unificada


> [!IMPORTANT]
> Si va a migrar usuarios habilitados para mensajería unificada a Microsoft Office Communications Server 2007 R2 o a Microsoft Lync Server, debe crear primero un plan de marcado URI de SIP.



Para obtener instrucciones detalladas, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

## Paso 2: Deshabilitar al usuario para mensajería unificada

Para obtener instrucciones detalladas, consulte [Deshabilitar el correo de voz para un usuario](disable-voice-mail-for-a-user-exchange-2013-help.md).

## Paso 3: Habilitar al usuario para mensajería unificada en el nuevo plan de marcado de mensajería unificada


> [!IMPORTANT]
> Si mueve usuarios a un entorno con Office Communications Server 2007 R2 o Lync Server, también debe incluir un identificador de recursos SIP para el usuario cuando lo habilite para mensajería unificada. También debe seleccionar la directiva de buzón de MU asociada con el plan de marcado SIP.



Para obtener instrucciones detalladas, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

