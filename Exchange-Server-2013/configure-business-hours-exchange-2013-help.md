---
title: 'Configurar el horario de oficina: Exchange 2013 Help'
TOCTitle: Configurar el horario de oficina
ms:assetid: 96b4be99-af94-4fa4-959a-48413387a044
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232133(v=EXCHG.150)
ms:contentKeyID: 49895792
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el horario de oficina

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-19_

Al configurar el horario comercial en un operador automático de mensajería unificada (UM), se definen las horas del día durante las cuales la organización permanece abierta y los saludos y mensajes de menú en horario comercial que oirán las personas que llamen a una extensión configurada en el operador automático. Si alguien llama al operador automático fuera del horario comercial definido, oirá los mensajes y los saludos definidos para el horario no comercial.

En el EAC, hay varias opciones de programación predeterminadas disponibles. Por ejemplo, la mayoría de las empresas están abiertas de 8:00 a 17:00, de lunes a viernes. En ocasiones, las opciones predeterminadas no satisfacen sus necesidades, y usted desea personalizar la programación. Si el horario comercial de su organización es distinto del de las programaciones definidas por el sistema, puede definir una programación personalizada para el operador automático.

Por defecto, el operador automático de mensajería unificada reproducirá los mensajes y saludos del horario comercial con independencia de la hora del día en la que se llame al operador automático.


> [!NOTE]
> Al establecer la programación del horario comercial y no comercial en un operador automático de mensajería unificada, asegúrese de que la zona horaria esté configurada correctamente.



Para otras tareas de administración relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para especificar el horario comercial para un operador automático de UM

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada para el que desea ajustar el horario comercial, y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada** \> **Horario comercial**, en **Horario comercial**, haga clic en **Configurar horario comercial**.

4.  En la página **Configurar horario comercial**, seleccione las horas que desee usar como horario comercial para cada día de la semana.

5.  Haga clic en **Aceptar**y, a continuación, haga clic en **Guardar**.

## Usar el Shell para especificar el horario comercial para un operador automático de MU

En este ejemplo, se establece el horario comercial de un operador automático de MU llamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30

