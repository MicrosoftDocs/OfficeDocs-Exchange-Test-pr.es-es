---
title: 'Establecer número correo voz anterior pines para reciclaje: Exchange 2013 Help'
TOCTitle: Establecer el número de correo de voz anterior pines para reciclaje
ms:assetid: b094e68e-c493-4576-a6b1-4c780e635405
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124254(v=EXCHG.150)
ms:contentKeyID: 50556860
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer el número de correo de voz anterior pines para reciclaje

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Cuando los usuarios de Outlook Voice Access llaman a un número de Outlook Voice Access, se les indica que introduzcan su PIN, para que el sistema de correo de voz pueda autenticarlos. Tras autenticarlos, pueden obtener acceso al correo de voz, al correo electrónico, a los calendarios y a la información de contacto personal de su buzón desde cualquier teléfono.

En una directiva de buzón de mensajería unificada (UM) se pueden configurar varias opciones relacionadas con el PIN. El valor del **Número de reciclajes de PIN** especifica el número de PIN únicos que los usuarios pueden utilizar para que puedan volver a usar un PIN antiguo. Se puede configurar el valor de esta opción entre 1 y 20. En la mayoría de las organizaciones, este valor debe configurarse en 5 PIN, que es el valor predeterminado. Establecer un valor demasiado alto puede resultar poco práctico para los usuarios, ya que crear y memorizar muchos PIN puede resultar una actividad bastante ardua. Si es demasiado bajo, puede suponer una amenaza para la seguridad de la red.


> [!IMPORTANT]
> No se puede deshabilitar el recuento de reciclajes de PIN.



Para conocer otras tareas relacionadas con la seguridad del PIN de Outlook Voice Access, consulte [Procedimientos de seguridad PIN](pin-security-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para cambiar el número de reciclajes de PIN

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de **plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzones de mensajería unificada que desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  Haga clic en **Directivas de NIP** y, al lado de **Número de reciclajes de PIN**, escriba un valor entre 1 y 20.

5.  Haga clic en **Guardar**.

## Usar el Shell para cambiar el número de reciclajes de PIN

En este ejemplo, se establece el número de reciclajes de PIN en la directiva de buzón de mensajería unificada `MyUMMailboxPolicy` en 10.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINHistoryCount 10

