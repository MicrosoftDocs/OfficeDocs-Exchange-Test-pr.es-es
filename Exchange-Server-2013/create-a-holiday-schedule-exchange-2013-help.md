---
title: 'Crear una programación de vacaciones: Exchange 2013 Help'
TOCTitle: Crear una programación de vacaciones
ms:assetid: 0c5c51e4-5b51-451b-ab93-2cebf644dc96
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb266921(v=EXCHG.150)
ms:contentKeyID: 49895455
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear una programación de vacaciones

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-19_

Puede definir las fechas y las horas durante las que la organización estará cerrada por vacaciones y otros motivos. En el intervalo entre la fecha de inicio y fin que especifique, las personas que llamen al operador automático de mensajería unificada (MU) escucharán el saludo de vacaciones que haya especificado al configurar la programación de vacaciones. Después del saludo de vacaciones especificado, se escucharán los saludos correspondientes de fuera del horario comercial y las instrucciones del menú.

También puede crear una programación de vacaciones dentro de otra que ya existe. Cuando crea varias programaciones de vacaciones, la mensajería unificada permite superponer los períodos de vacaciones programados. Por ejemplo, puede crear una programación de vacaciones desde el 15 de diciembre hasta el 31 de diciembre, mientras su organización permanezca cerrada por obras y puede definir otra programación de vacaciones desde el 24 al 26 de diciembre. Las personas que llamen al operador automático desde el 15 de diciembre al 23 de diciembre y desde el 27 de diciembre al 31 de diciembre, escucharán el saludo de vacaciones especificado para esas fechas determinadas. Por ejemplo, "En estos momentos, nuestra empresa permanece cerrada por obras." Cuando las personas llamen al operador automático entre el 24 de diciembre y el 26 de diciembre, escucharán otro saludo de vacaciones, como, por ejemplo, "Durante estas fiestas familiares, nuestra empresa se encuentra cerrada."

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, vea [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para especificar una programación de vacaciones de un operador automático de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que quiera modificar y luego, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada para el que quiera establecer la programación de vacaciones. En la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operadores automáticos de mensajería unificada** \> **Horario comercial**, en **Programación de vacaciones**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En la página **Nuevo día festivo**, configure lo siguiente:
    
      - **Nombre**: escriba el nombre de la programación de vacaciones.
    
      - **Saludo en días festivos**: desplácese hasta el archivo .wav que quiera usar como saludo. Es un campo obligatorio.
    
      - **Fecha de inicio**: use esta lista para seleccionar la fecha en la que quiere que empiecen las vacaciones. La programación de vacaciones comenzará a la medianoche de la fecha especificada en esta lista.
    
      - **Fecha de finalización:** use esta lista para seleccionar la fecha en la que quiere que terminen las vacaciones. La programación de vacaciones finalizará a las 11:59 p. m. de la fecha especificada en esta lista.

5.  Una vez configurada la programación de vacaciones, haga clic en **Aceptar** y luego en **Guardar**.

## Usar el Shell para especificar una programación de vacaciones de un operador automático de mensajería unificada

En este ejemplo, se configura un operador automático de mensajería unificada denominado `MyUMAutoAttendant` cuyo horario comercial es de 10:45 a 13:15 (domingo), de 09:00 a 17:00 (lunes) y de 09:00 a 16:30 (sábado), y cuyas vacaciones y saludos asociados son "Año nuevo" el 2 de enero de 2013 y "Edificio cerrado por obras" desde el 24 de abril de 2013 hasta el 28 de abril de 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

