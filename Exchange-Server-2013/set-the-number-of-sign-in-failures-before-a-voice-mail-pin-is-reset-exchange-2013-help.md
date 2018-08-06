---
title: 'Establecer n.º error inicio sesión antes de restablecer NIP de correo de voz | Microsoft Docs'
TOCTitle: Establecer el número de errores de inicio de sesión antes de un restablecimiento del NIP de correo de voz
ms:assetid: 4de38499-0a6f-4f00-8697-eeff805d7266
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997939(v=EXCHG.150)
ms:contentKeyID: 50556797
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer el número de errores de inicio de sesión antes de un restablecimiento del NIP de correo de voz

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede configurar el número de errores de inicio de sesión permitidos antes de restablecer el PIN para un usuario de Outlook Voice Access en un valor de 1 a 998. El valor predeterminado es 5. Este número está configurado en una directiva de buzón de mensajería unificada (MU) y se aplica a todos los usuarios de Outlook Voice Access asociados con la directiva de buzón de MU.


> [!NOTE]
> Puede aumentar la seguridad al configurar la opción <STRONG>Número de errores de inicio de sesión permitidos antes de restablecer el PIN</STRONG> en un número inferior a 5. Reducirá la seguridad si la configura en un número superior a 5.



Para tareas adicionales relacionadas con la seguridad del PIN de Outlook Voice Access, consulte [Procedimientos de seguridad PIN](pin-security-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para configurar el número de errores de inicio de sesión antes de restablecer el PIN

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de MU**, en **Directivas de buzón de MU**, seleccione la directiva de buzón de MU que desee cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  Haga clic en **Directivas de PIN** y, luego, en **Número de errores de inicio de sesión permitidos antes de restablecer el PIN**, especifique un valor entre 0 y 999.

5.  Haga clic en **Guardar**.

## Uso del Shell para configurar el número de errores de inicio de sesión antes de restablecer el PIN

En este ejemplo, se establece el número de errores de inicio de sesión antes de restablecer el PIN del usuario en 3 para usuarios habilitados para MU asociados con una directiva de buzón de MU denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3

En este ejemplo, se establece el número de errores de inicio de sesión antes de que el PIN del usuario se restablezca en 3, el número máximo de intentos de inicio de sesión en 5 y una longitud mínima del PIN en 9 para usuarios habilitados para MU que están asociados con una directiva de buzón de MU denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MaxLogonAttempts 5 -MinPINLength 9

