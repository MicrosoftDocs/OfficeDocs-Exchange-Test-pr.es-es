---
title: 'Establecer la duración PIN de correo de voz: Exchange 2013 Help'
TOCTitle: Establecer la duración PIN de correo de voz
ms:assetid: d17f0bf6-0ad6-40a4-bdd5-f7098f39250d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124712(v=EXCHG.150)
ms:contentKeyID: 50556891
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer la duración PIN de correo de voz

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Puede configurar la vigencia del PIN de los usuarios que estén habilitados para mensajería unificada. La vigencia del PIN es el tiempo máximo que un PIN de Outlook Voice Access es válido para los destinatarios habilitados para mensajería unificada. La opción de vigencia del PIN se configura en una directiva de buzón de mensajería unificada y se aplica a todos los usuarios con mensajería unificada habilitada que estén asociados a dicha directiva.

En una directiva de buzón de mensajería unificada pueden configurarse varias opciones relacionadas con el PIN. La opción de vigencia del PIN controla el intervalo de tiempo, en días, desde la última fecha en la que un usuario de Outlook Voice Access cambió su PIN hasta la fecha en la que debe volver a cambiarlo. El intervalo es de 0 a 999, siendo el valor predeterminado 60 días. Si se especifica 0, el PIN del usuario no caducará. Se recomienda no configurar este valor en 0, porque al hacerlo se disminuye enormemente la seguridad de la red.


> [!IMPORTANT]
> La mensajería unificada no avisa a los usuarios cuando su PIN está a punto de caducar.



Para tareas adicionales relacionadas con la seguridad del PIN de Outlook Voice Access, vea [Procedimientos de seguridad PIN](pin-security-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para configurar la vigencia del PIN

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de **plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzones de mensajería unificada que desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  Haga clic en **Directivas de PIN** y, al lado de **Aplicar vigencia de PIN (días)**, escriba un valor entre 0 y 999.

5.  Haga clic en **Guardar**.

## Uso del Shell para configurar la vigencia de PIN

En este ejemplo se define en 30 el número de días durante los cuales se puede usar un PIN para los usuarios de Outlook Voice Access que estén asociados a una directiva de buzones de mensajería unificada denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINLifetime 30

En este ejemplo se establece la configuración de PIN de los usuarios de Outlook Voice Access que estén asociados a una directiva de buzones de mensajería unificada denominada `MyUMMailboxPolicy`:

  - Define el número de errores de inicio de sesión antes de que el PIN del usuario se restablezca en 3.

  - El número máximo de intentos de inicio de sesión se establece en 5.

  - Establece la longitud mínima de PIN en 9 dígitos.

  - Establece que el PIN caducará en 40 días.

<!-- end list -->

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9 -PINLifetime 40

