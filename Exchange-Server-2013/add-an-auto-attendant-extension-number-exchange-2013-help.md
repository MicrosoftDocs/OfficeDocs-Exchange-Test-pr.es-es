---
title: 'Agregar un número de extensión de operador automático: Exchange 2013 Help'
TOCTitle: Agregar un número de extensión de operador automático
ms:assetid: f2bd62ba-1e01-4cb7-862c-c750752e20e0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232200(v=EXCHG.150)
ms:contentKeyID: 49896010
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agregar un número de extensión de operador automático

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

Puede configurar uno o varios números de extensión en un operador automático de mensajería unificada (MU). Cuando agrega un número de extensión a un operador automático de mensajería unificada, ese número puede ser utilizado por las personas que llaman para conectarse con el operador automático. Asimismo, quizá deba agregar números de extensión porque las personas que llaman pueden usar más de un número de extensión para obtener acceso a un operador automático. De forma predeterminada, no se configura ningún número de extensión al crear un operador automático.

Se puede crear un operador automático sin configurar un número de extensión para dicho operador. También puede asociarse más de un número de teléfono o de extensión con un único operador automático. Puede agregarse los números de extensión al crear el operador automático de mensajería unificada o tras configurar el operador automático. El número de dígitos del número de extensión que configure en el operador automático de mensajería unificada debe coincidir con el número de dígitos de un número de extensión configurado en el plan de marcado de mensajería unificada asociado al operador automático de mensajería unificada.


> [!NOTE]
> También puede agregar una dirección de protocolo de inicio de sesión (SIP) en lugar de agregar un número de extensión. Una dirección SIP puede ser utilizada por algunas centrales de conmutación (PBX) IP y Office Communications Server 2007 R2 o Microsoft Lync Server.



Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para agregar números de teléfono o extensión para un operador automático de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea editar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada para el que desea agregar números de teléfono o extensión.

3.  En la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  En la página **Operador automático de mensajería unificada** \> **General**, en el cuadro de texto de **Números de acceso**, escriba el número de teléfono o extensión que desea usar y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

5.  Haga clic en **Guardar** para agregar el número.

## Uso del Shell para configurar un número de extensión en un operador automático de mensajería unificada

En este ejemplo, se configura un operador automático de mensajería unificada denominado `MyUMAutoAttendant` con varios números de extensión.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -PilotIdentifierList "12345, 72000, 75000"

