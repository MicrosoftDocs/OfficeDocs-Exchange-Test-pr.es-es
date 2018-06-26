---
title: 'Habilitar un mensaje del menú de horario comercial personalizada: Exchange 2013 Help'
TOCTitle: Habilitar un mensaje del menú de horario comercial personalizada
ms:assetid: 89053e84-3490-4dc6-ade3-9b6c5dbf4020
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232116(v=EXCHG.150)
ms:contentKeyID: 50556846
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar un mensaje del menú de horario comercial personalizada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-19_

Puede personalizar el mensaje de menú que debe utilizar un operador automático de mensajería unificada en horario comercial. Después de crear un operador automático de mensajería unificada, se usa un aviso del sistema predeterminado (\&quot;Bienvenido a la mensajería unificada\&quot;) como mensaje del menú que los llamantes escuchan después de que se reproduzca la bienvenida personalizada en horario comercial. Aunque no se debe sustituir ni cambiar el aviso del sistema, puede personalizar los saludos y avisos del menú utilizados con los operadores automáticos de mensajería unificada. Después de crear un archivo de audio de mensaje del menú de horario comercial personalizado, debe habilitar las entradas de navegación del menú en el operador automático de mensajería unificada.

Si solo desea incluir el nombre de la empresa o la organización como parte del aviso del sistema predeterminado, escriba el nombre en el cuadro **Nombre de la empresa** en el operador automático de mensajería unificada. Para obtener información más detallada, consulte [Escriba un nombre de empresa](enter-a-business-name-exchange-2013-help.md).


> [!IMPORTANT]
> Debe configurar el horario comercial en el operador automático. Para obtener información más detallada, consulte <A href="configure-business-hours-exchange-2013-help.md">Configurar el horario de oficina</A>.



Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Cree un archivo .wav o .wma para usarlo para el mensaje del menú.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar un mensaje del menú de horario comercial personalizado

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada para el que desee habilitar un mensaje del menú de horario comercial personalizado, y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada**, \> **Navegación de menús**, en la sección **Navegación de menús en horario comercial**, haga clic en **Cambiar** y, a continuación, haga clic en **Examinar** para ubicar el archivo del menú de horario comercial personalizado.
    

    > [!IMPORTANT]
    > El archivo que use para el mensaje del menú debe ser un archivo .wav o .wma.



4.  Después de encontrar el archivo, haga clic en **Abrir** y, a continuación, en **Guardar**.

## Usar el Shell para habilitar un mensaje del menú de horario comercial personalizado

En este ejemplo se habilita un mensaje del menú principal de horario comercial personalizado y un mensaje personalizado denominado `businesshoursprompts.wav` en el operador automático de mensajería unificada `MyUMAutoAttendant`.

    Command Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursMainMenuCustomPromptEnabled $true -BusinessHoursMainMenuCustomPromptFilename BusinessHoursPrompts.wav

En este ejemplo, se configura un operador automático de MU denominado `MyUMAutoAttendant` cuyo horario comercial es de 10:45 a 13:15 (domingo), de 09:00 a 17:00 (lunes) y de 09:00 a 16:30 (sábado), y cuyas vacaciones y saludos asociados son "`New Year`" el 02.01.13 y "`Building Closed for Construction`" desde el 24.04.13 hasta el 28.04.13.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

En este ejemplo se configura un operador automático de mensajería unificada denominado `MyAutoAttendant` y se habilitan los menús de navegación en horario comercial de modo que, cuando la persona que llama presione 1, se le reenvía a otro operador automático de mensajería unificada denominado `SalesAutoAttendant`. Cuando la persona presione 2, se le reenvía al número de extensión 12345 para `Support` y cuando presione 3, se le envía a otro operador automático que reproduce un archivo de audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

