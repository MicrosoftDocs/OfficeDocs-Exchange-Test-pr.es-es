---
title: 'Habilitar o deshabilitar reproducción multimedia de mensajes de voz protegido'
TOCTitle: Habilitar o deshabilitar la reproducción multimedia de los mensajes de voz protegido
ms:assetid: 3c33370c-4262-42b1-8d83-d61fc7c426cd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423543(v=EXCHG.150)
ms:contentKeyID: 52061817
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o deshabilitar la reproducción multimedia de los mensajes de voz protegido

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede hacer que los usuarios que reciben mensajes de correo de voz protegidos utilicen la característica "Reproducir en teléfono" para escucharlos. O bien si el software cliente no admite la administración de derechos, los usuarios deben usar Outlook Voice Access para poder escucharlos.

Para escuchar los mensajes de voz, los usuarios con mensajería unificada habilitada pueden usar la característica "Reproducir en teléfono" o software multimedia en un equipo o dispositivo móvil. La reproducción multimedia permite que un usuario con mensajería unificada habilitada utilice un reproductor de medios a través de los altavoces del equipo o bien utilice un reproductor del dispositivo móvil para escuchar los mensajes de voz.


> [!NOTE]
> El correo de voz protegido únicamente está disponible para clientes que utilicen luna versión de Outlook que admita la administración de derechos. Si el software cliente no admite la administración de derechos, los usuarios deben usar Outlook Voice Access para poder escuchar sus llamadas.



De forma predeterminada, el valor de la propiedad **RequireProtectedPlayOnPhone** en una directiva de buzón de MU se configura como falso. Esto significa que los usuarios con mensajería unificada habilitada que estén asociados a una directiva de buzones de mensajería unificada pueden escuchar los mensajes de voz protegidos de los siguientes modos:

  - Mediante Outlook Voice Access.

  - Con el reproductor de medios integrado o el botón "Reproducir en teléfono" de Outlook 2010 o versiones posteriores.

  - Con el reproductor de medios integrado o el botón "Reproducir en teléfono" de Outlook Web App.

Si este valor está configurado como verdadero, no se permite la reproducción multimedia del correo de voz protegido. Los usuarios con mensajería unificada habilitada que estén asociados a una directiva de buzones de mensajería unificada en las que este valor esté definido como "true" únicamente podrán escuchar los mensajes de voz protegidos de los siguientes modos:

  - Mediante Outlook Voice Access.

  - Mediante el botón "Reproducir en teléfono" de Outlook 2010 o una versión posterior.

  - Con el botón "Reproducir en teléfono" de Outlook Web App.

Esta configuración resulta especialmente útil cuando los usuarios habilitados para mensajería unificada usan equipos públicos, equipos portátiles en lugares públicos o el reproductor multimedia de sus dispositivos móviles para escuchar correo de voz protegido que puede contener información privada.

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

## Utilizar el EAC para habilitar o deshabilitar la reproducción multimedia de mensajes de voz protegidos

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzones de mensajería unificada que desea administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzones de mensajería unificada** \> **Correo de voz protegido**, active la casilla al lado de **Requerir Reproducir en teléfono para mensajes de voz protegidos** para habilitar esta configuración. Desactive la casilla para deshabilitar esta configuración.

4.  Haga clic en **Guardar**.

## Usar el Shell para habilitar o deshabilitar la reproducción multimedia de los mensajes de voz protegidos

En este ejemplo se permite a los usuarios asociados a la directiva de buzones de mensajería unificada denominada `MyUMMailboxPolicy` que reproduzcan los mensajes de voz protegidos a través de un reproductor de medios.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $false

En este ejemplo se impide que los usuarios asociados a la directiva de buzones de mensajería unificada denominada `MyUMMailboxPolicy` reproduzcan los mensajes de voz protegidos a través de un reproductor de medios.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $true

