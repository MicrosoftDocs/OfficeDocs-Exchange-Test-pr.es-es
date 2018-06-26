---
title: 'Establecer directivas de NIP de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Establecer directivas de NIP de Outlook Voice Access
ms:assetid: 5b2800b7-bfa6-4282-975c-0706ae25ad64
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998285(v=EXCHG.150)
ms:contentKeyID: 50556781
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer directivas de NIP de Outlook Voice Access

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Puede establecer directivas de NIP en una directiva de buzón de mensajería unificada (MU). Las directivas de buzón de MU pueden configurarse para aumentar el nivel de seguridad de los usuarios habilitados para la MU que usan Outlook Voice Access al solicitar que los usuarios cumplan con las directivas de PIN predefinidas para su organización.

Para establecer directivas de PIN para usuarios de Outlook Voice Access, puede crear una directiva nueva de buzón de MU o modificar una existente. Después de crear una nueva directiva de buzón de MU, es posible configurarla mediante los siguientes parámetros de NIP:

  - `MinPasswordLength`

  - `PINLifetime`

  - `LogonFailuresBeforePINReset`

  - `MaxLogonAttempts`

  - `AllowCommonPatterns`

  - `PINHistoryCount`

La práctica de seguridad recomendada es implementar requisitos seguros de NIP para los usuarios de MU. Esto se puede lograr creando directivas de NIP de mensajería unificada que requieran NIP de 6 o más dígitos y aumenten el nivel de seguridad de la red.

Cuando cambia la directiva de NIP, la nueva configuración de NIP se aplica a los usuarios que están actualmente a la directiva de buzón de MU. Por ejemplo, si modifica la directiva de buzón de MU y cambia la longitud mínima del NIP de 7 a 10 dígitos, la próxima vez que los usuarios inicien la sesión estarán obligados a cambiar su NIP para cumplir con el nuevo requisito de NIP.

Para tareas adicionales relacionadas con la seguridad del PIN de Outlook Voice Access, consulte [Procedimientos de seguridad PIN](pin-security-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para establecer directivas de PIN para usuarios de Outlook Voice Access

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, haga clic en el plan de marcado de MU que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de MU**, en **Directivas de buzón de MU**, seleccione la directiva de buzón de MU que desee editar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  Haga clic en **Propiedades**.

4.  En la página **Directiva de buzón de MU**, haga clic en la ficha **Directivas de PIN**.

5.  En la página **Directivas de PIN**, configure los ajustes de PIN para los usuarios de Outlook Voice Access asociados con esta directiva de buzón de MU y, luego, haga clic en **Guardar**.

## Uso del Shell para establecer directivas de PIN para usuarios de Outlook Voice Access

En este ejemplo, se establece la configuración de NIP para los usuarios asociados con la directiva de buzón de MU `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

