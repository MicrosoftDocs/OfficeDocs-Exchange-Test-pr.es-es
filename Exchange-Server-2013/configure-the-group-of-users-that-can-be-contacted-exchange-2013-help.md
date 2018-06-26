---
title: 'Configurar el grupo de usuarios a los que se puede contactar: Exchange 2013 Help'
TOCTitle: Configurar el grupo de usuarios a los que se puede contactar
ms:assetid: 45d9d6d5-c9d6-4b73-8aa2-a23599a4381c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423545(v=EXCHG.150)
ms:contentKeyID: 52061820
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el grupo de usuarios a los que se puede contactar

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-12-09_

Puede especificar el grupo de usuarios con quienes los autores de llamadas se pueden comunicar cuando llaman a un operador automático de mensajería unificada. De manera predeterminada, las personas que llaman pueden comunicarse con los usuarios del mismo plan de marcado asociado con el operador automático de MU. Sin embargo, puede cambiar las agrupaciones de usuarios para permitir a los autores de llamadas transferir llamadas o enviar mensajes de voz a los usuarios de la lista de direcciones de la organización o a un conjunto concreto de usuarios.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Administrar a un operador automático de mensajería unificada](manage-a-um-auto-attendant-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar el grupo de usuarios con quienes los autores de llamadas se pueden comunicar

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, bajo **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada que desee configurar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada** \> **Libreta de direcciones y acceso de operador**, bajo **Opciones para las búsquedas en la libreta de direcciones**, elija las opciones siguientes:
    
      - **En este plan de marcado únicamente** Seleccione esta opción para permitir a las personas que llaman que se conectan con el operador automático de mensajería unificada ubicar usuarios del plan de marcado asociado al operador automático de mensajería unificada y ponerse en contacto con ellos.
    
      - **En toda la organización** Seleccione esta opción para permitir que los autores de llamadas que se conecten al operador automático de mensajería unificada puedan localizar a cualquier persona que aparezca en la lista de direcciones de la organización y ponerse en contacto con ellos. Se incluyen todos los usuarios que tengan el buzón habilitado.

4.  Haga clic en **Guardar**.

## Usar el Shell para configurar el grupo de usuarios con quienes los autores de llamadas se pueden comunicar

En este ejemplo se establece el ámbito de usuarios con quienes los autores de llamadas se pueden comunicar en todos los usuarios de la libreta de direcciones de la organización de un operador automático de mensajería unificada denominado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -ContactScope GlobalAddressList

