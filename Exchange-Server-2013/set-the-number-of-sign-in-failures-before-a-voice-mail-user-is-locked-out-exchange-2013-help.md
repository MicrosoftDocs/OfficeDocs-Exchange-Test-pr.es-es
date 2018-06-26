---
title: 'Establecer el número de errores de inicio de sesión antes de bloquea un usuario de correo de voz: Exchange 2013 Help'
TOCTitle: Establecer el número de errores de inicio de sesión antes de bloquea un usuario de correo de voz
ms:assetid: 855e1980-2868-4983-b097-0b5f63f202b8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123544(v=EXCHG.150)
ms:contentKeyID: 50556842
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer el número de errores de inicio de sesión antes de bloquea un usuario de correo de voz

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Puede configurar el número de errores de inicio de sesión permitidos antes de que al usuario de Outlook Voice Access se le bloquee el uso de su buzón de correo. El número de errores de inicio de sesión permitidos antes de que un usuario de correo de voz quede bloqueado se configura en una directiva de buzones de mensajería unificada y se aplica a todos los usuarios habilitados para mensajería unificada que estén asociados a dicha directiva. De forma predeterminada, está establecida en 15.

Para aumentar la seguridad, disminuya el número máximo de intentos incorrectos. Recuerde que si disminuye este valor a un número muy inferior al valor predeterminado, puede ocasionar el bloqueo innecesario de los usuarios. La mensajería unificada generará eventos de advertencia que podrán ser visualizados mediante el Visor de eventos si la autenticación de NIP presenta errores a un usuario habilitado para mensajería unificada o si el usuario no logra iniciar sesión en el sistema. Esta configuración debe ser más grande que la configuración del número de errores de inicio de sesión antes de que se establezca el PIN.

Para otras tareas relacionadas con la seguridad del PIN de Outlook Voice Access, consulte [Procedimientos de seguridad PIN](pin-security-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar el número de errores de inicio de sesión antes de que se bloquee un usuario de correo de voz

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de mensajería unificada**, seleccione la directiva de buzones de correo de mensajería unificada que desee cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  Haga clic en **Directivas de PIN**, y al lado de **Número de errores de inicio de sesión antes de bloquearlo**, escriba un valor entre 1 y 999.

5.  Haga clic en **Guardar**.

## Usar el Shell para configurar el número de errores de inicio de sesión antes de que se bloquee un usuario de correo de voz

En este ejemplo, se establece en 10 el número máximo de intentos de inicio de sesión para usuarios habilitados para MU que estén asociados a una directiva de buzones de MU denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MaxLogonAttempts 10

En este ejemplo, se establece el número de errores de inicio de sesión antes de que el PIN del usuario de Outlook Voice Access se restablezca en 3, el número máximo de intentos de inicio de sesión en 5 y una longitud mínima del NIP en 9 para usuarios habilitados para mensajería unificada que están asociados con una directiva de buzón de mensajería unificada denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9

