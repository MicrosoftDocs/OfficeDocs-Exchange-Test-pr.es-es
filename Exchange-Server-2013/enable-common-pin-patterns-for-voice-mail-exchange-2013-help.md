---
title: 'Permitir patrones comunes de PIN de correo de voz: Exchange 2013 Help'
TOCTitle: Permitir patrones comunes de PIN de correo de voz
ms:assetid: 9940a8c2-f576-4089-ab96-8b318ad3da0f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673546(v=EXCHG.150)
ms:contentKeyID: 50556819
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir patrones comunes de PIN de correo de voz

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Puede habilitar o deshabilitar los patrones de PIN de mensajería unificada comunes para los usuarios de Outlook Voice Access. Si habilita o deshabilita los patrones de PIN comunes mediante la configuración de una directiva de buzones de mensajería unificada, la configuración se aplicará a todos los usuarios habilitados para mensajería unificada asociados con la directiva de buzones de mensajería unificada. De modo predeterminado, los usuarios habilitados para mensajería unificada no pueden usar patrones comunes cuando crean un PIN.

Puede configurar varias opciones relacionadas con el PIN en una directiva de buzones de mensajería unificada. La opción **Permitir patrones comunes de NIP** se utiliza para permitir o impedir el uso de patrones numéricos comunes cuando los usuarios crean un PIN. De forma predeterminada, esta opción está deshabilitada, lo cual impide que los usuarios utilicen los siguientes patrones numéricos:

  - **Números secuenciales**   Son valores del PIN que sólo incluyen números consecutivos. Ejemplos de números consecutivos para un PIN son 1234 y 65432.

  - **Números repetidos**   Hay valores del PIN que sólo incluyen números repetidos. Ejemplos de números repetidos son 11111 y 22222.

  - **Sufijo de la extensión de buzón**   Son valores del PIN que incluyen el sufijo del buzón de un usuario. Por ejemplo, si la extensión del buzón de un usuario es 36697, el PIN de un usuario no puede ser 3669712.


> [!NOTE]
> Si la opción <STRONG>Permitir patrones comunes de NIP</STRONG> está habilitada, sólo se rechazará el sufijo de la extensión de buzón.



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

## Usar el EAC para activar patrones comunes de PIN

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de la lista, seleccione el plan de marcado de mensajería unificada que quiere modificar y luego, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de mensajería unificada**, seleccione la directiva de buzones de correo de mensajería unificada que desee administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de correo de mensajería unificada**, en **Directivas de PIN** active la casilla de verificación al lado de **Permitir patrones comunes de NIP**.

4.  Haga clic en **Guardar**.

## Usar el Shell para activar patrones comunes de PIN

Este ejemplo permite a los usuarios asociados con la directiva de buzones de mensajería unificada denominada `MyUMMailboxPolicy` usar los PIN que contienen patrones comunes.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowCommonPatterns $true

