---
title: 'Habilitar un aviso de menú personalizado para el horario no comercial: Exchange 2013 Help'
TOCTitle: Habilitar un aviso de menú personalizado para el horario no comercial
ms:assetid: 094c50b2-072b-4929-aaf8-f7db5b19e9b6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb266919(v=EXCHG.150)
ms:contentKeyID: 50556737
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar un aviso de menú personalizado para el horario no comercial

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-03-22_

Puede personalizar el mensaje de menú que usará el operador automático de mensajería unificada fuera del horario comercial. Después de crear un operador automático de mensajería unificada, se usa un mensaje del sistema predeterminado (\&quot;Bienvenido a la mensajería unificada\&quot;) como mensaje de menú que los llamadores oyen después de reproducirse el saludo de bienvenida del horario no comercial. Si bien no se debe sustituir ni cambiar el mensaje del sistema, puede personalizar los saludos y los mensajes del menú que se usa con los operadores automáticos de UM. Después de crear un archivo de audio de mensaje del menú personalizado para el horario no comercial, debe habilitar las entradas de navegación del menú en el operador automático de UM para el horario no comercial.

Si solo quiere incluir el nombre de la empresa o la organización como parte del mensaje del sistema predeterminado, puede escribir el nombre en el cuadro **Nombre de la empresa** en el operador automático de mensajería unificada. Para obtener información más detallada, consulte [Escriba un nombre de empresa](enter-a-business-name-exchange-2013-help.md).


> [!IMPORTANT]
> Debe configurar el horario comercial en el operador automático. Al configurar el horario comercial, el horario no comercial se establece automáticamente. Para obtener información más detallada, consulte <A href="configure-business-hours-exchange-2013-help.md">Configurar el horario de oficina</A>.



Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Cree el archivo .wav o .wma que se usará para el mensaje de menú.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar un mensaje de menú para el horario no comercial personalizado

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de UM que quiere cambiar y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada para el que quiere habilitar un mensaje de menú personalizado para el horario no comercial y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada**, \> **Navegación del menú**, en **Navegación del menú en horario no comercial**, haga clic en **Modificar** y luego en **Examinar** para buscar el archivo de mensaje del menú personalizado para el horario no comercial.
    

    > [!IMPORTANT]
    > El archivo que use para el mensaje del menú debe ser un archivo .wav o .wma.



4.  Cuando encuentre el archivo, haga clic en **Abrir** y luego en **Guardar**.

## Usar el Shell para habilitar un mensaje de menú para el horario no comercial personalizado

En este ejemplo, se habilita un operador automático de UM denominado `MyUMAutoAttendant` cuyo horario comercial es de 10:45 a 13:15 (domingo), de 09:00 a 17:00 (lunes) y de 09:00 a 16:30 (sábado), y cuyas vacaciones y saludos asociados son "`New Year`" el 1 de enero de 2013 y "`Building Closed for Construction`" desde el 24 de abril de 2013 hasta el 28 de abril de 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

En este ejemplo, se configura un operador automático de UM denominado `MyAutoAttendant` y se habilitan los menús de navegación en horario no comercial de modo que, cuando el llamador presiona 1, la llamada se desvía a otro operador automático de UM llamado `SalesAutoAttendant`. Cuando presiona 2, la llamada se desvía al número de extensión 12345 para `Support` y cuando presiona 3, la llamada se desvía a otro operador automático de UM que reproduce un archivo de audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - 
    AfterHoursKeyMappingEnabled $true -
    AfterHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

