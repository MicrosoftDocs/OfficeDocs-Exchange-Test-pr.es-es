---
title: 'Habilitar un saludo de horario comercial personalizada: Exchange 2013 Help'
TOCTitle: Habilitar un saludo de horario comercial personalizada
ms:assetid: a2272b7d-de88-4d3f-81e6-ad81f0ee6c5e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232152(v=EXCHG.150)
ms:contentKeyID: 50556830
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar un saludo de horario comercial personalizada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-19_

Puede habilitar un saludo de horario comercial de un operador automático de mensajería unificada de Microsoft. El saludo de horario comercial es lo primero que escucha la persona que llama cuando el operador automático de mensajería unificada responde a la llamada durante el horario comercial. Probablemente deseará personalizar el saludo.

La mensajería unificada incluye un mensaje del sistema predeterminado para usarlo durante el horario comercial. A pesar de que el mensaje predeterminado del sistema no debe sustituirse ni cambiarse, puede proporcionar un saludo personalizado. Puede crear un saludo personalizado en formato de archivo .wav o .wma que puede ser utilizado cuando alguien llama a un operador automático de mensajería unificada durante el horario comercial. Por ejemplo, "Ha llamado al Banco Woodgrove."

Si desea incluir el nombre de su organización o empresa como parte del saludo personalizado, puede especificar el nombre en el cuadro **Nombre de la empresa** o en el operador automático de mensajería unificada. Para obtener información detallada, consulte [Escriba un nombre de empresa](enter-a-business-name-exchange-2013-help.md).

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Cree un archivo .wav o .wma para utilizarlo para el saludo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar un saludo personalizado en horario comercial

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada para el que desee habilitar un saludo de horario comercial personalizado, y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada**, \> **Saludos**, en **Saludo en horario comercial**, haga clic en **Cambiar** y, a continuación, haga clic en **Examinar** para ubicar el archivo del saludo personalizado en horario comercial que creó antes de iniciar este procedimiento.
    

    > [!IMPORTANT]
    > El archivo que use para el saludo debe ser .wav o .wma.



4.  Después de encontrar el archivo, haga clic en **Abrir** y, a continuación, en **Guardar**.

## Usar el Shell para habilitar un saludo personalizado en horario comercial

En este ejemplo, se habilita el saludo de horario comercial que usa un mensaje personalizado denominado `GreetingFile.wav` en el operador automático de mensajería unificada `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursWelcomeGreetingEnabled $true -BusinessHoursWelcomeGreetingFilename GreetingFile.wav

En este ejemplo, se configura un operador automático de mensajería unificada denominado `MyUMAutoAttendant` cuyo horario comercial es de 10:45 a 13:15 (domingo), de 09:00 a 17:00 (lunes) y de 09:00 a 16:30 (sábado), y cuyas vacaciones y saludos asociados son "`New Year`" el 02.01.13 y "`Building Closed for Construction`" desde el 24.04.13 hasta el 28.04.13.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

En este ejemplo, se configura un operador automático de mensajería unificada denominado `MyAutoAttendant` y se habilitan las asignaciones de tecla en horario comercial de modo que, cuando la persona que llama presiona 1, se la reenvía a otro operador automático de mensajería unificada denominado `SalesAutoAttendant`. Cuando la persona presione 2, se le reenvía al número de extensión 12345 para `Support` y cuando presione 3, se le envía a otro operador automático que reproduce un archivo de audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

