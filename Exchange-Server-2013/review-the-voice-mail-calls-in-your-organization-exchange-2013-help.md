---
title: 'Revisar las llamadas de correo de voz en su organización: Exchange 2013 Help'
TOCTitle: Revisar las llamadas de correo de voz en su organización
ms:assetid: f6fdbe17-d1d2-442a-aa13-06b908d9c33a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659073(v=EXCHG.150)
ms:contentKeyID: 50556912
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Revisar las llamadas de correo de voz en su organización

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Puede usar el informe de estadísticas de llamadas para ver información acerca del tipo y del estado de las llamadas entrantes administradas por los servidores Exchange de la organización. El informe proporciona información acerca de las llamadas desviadas o realizadas por la mensajería unificada (UM) para la organización. Esta información le permite realizar un seguimiento del uso a fin de planificar la capacidad, supervisar y solucionar problemas en la disponibilidad y calidad de audio de la mensajería unificada, así como solucionar problemas en las llamadas erróneas.

En este tema se tratan las siguientes preguntas:

  - How do I get call statistics for UM?

  - How do I interpret UM call statistics?

Para tareas adicionales relacionadas con informes de mensajería unificada, consulte [Procedimientos de informes de mensajería unificada](um-reports-procedures-exchange-2013-help.md).

## ¿Cómo obtengo las estadísticas de llamadas para mensajería unificada?

1.  En el Centro de administración de Exchange (EAC), haga clic en **Mensajería unificada** \> **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") \> **Estadísticas de llamadas**.

2.  Elija la información que desee incluir en el informe. El informe se actualiza automáticamente al seleccionar cualquiera de las siguientes opciones:
    
      - **Mostrar **  Elija el tipo de estadísticas de llamada que se mostrará:
        
          - **Diariamente (90 días) **  Seleccione Diariamente para ver los detalles de todas las llamadas de los últimos 90 días.
        
          - **Mensualmente (12 meses)**   Seleccione Mensualmente para ver un resumen de las llamadas por mes de los últimos 12 meses.
        
          - **Todo**   Seleccione Todo para ver las estadísticas combinadas de todas las llamadas recibidas desde que la mensajería unificada empezó a administrar las llamadas.
    
      - **Plan de marcado de mensajería unificada**   Si desea limitar los datos del informe únicamente a las llamadas de un determinado plan de marcado de mensajería unificada, seleccione dicho plan.
    
      - **Puerta de enlace IP de mensajería unificada**   Si desea limitar los datos del informe únicamente a las llamadas de una determinada puerta de enlace IP de mensajería unificada, seleccione dicha puerta de enlace. Si primero selecciona un plan de marcado de mensajería unificada, en la lista solo estarán disponibles las puertas de enlace IP de MU asociadas al plan de marcado de MU seleccionado.

3.  Para obtener más detalles acerca de la calidad de audio de una fila del informe, seleccione la fila y haga clic en **Detalles de la calidad de audio**. Para obtener más información acerca cómo interpretar la calidad de audio, vea [Investigar la calidad de audio de las llamadas de voz en su organización](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md).

4.  Para copiar el informe en el Portapapeles, haga clic en **Copiar**.

5.  En el caso de los informes diarios, puede exportar los detalles de un determinado día a un archivo .csv.
    
    1.  Seleccione el día y haga clic en **Exportar día**.
    
    2.  En el cuadro de confirmación **Descarga de archivos**, haga clic en **Abrir** o **Guardar**.
    
    El archivo exportado se denominará um\_cdr\_*AAAA-MM-DD*.csv, donde *AAAA-MM-DD* es el año, el mes y el día en que se ejecutó el informe. Para obtener más información, consulte [Interpretar los registros de llamadas de correo de voz](interpret-voice-mail-call-records-exchange-2013-help.md).
    

    > [!NOTE]
    > En la página del informe, puede descargar una plantilla de Microsoft Excel que puede usar para importar el archivo .csv correspondiente a un día concreto.



Volver al principio

## ¿Cómo interpreto las estadísticas de llamadas de mensajería unificada?

Las estadísticas de llamadas de mensajería unificada incluyen la siguiente información:

  - **FECHA**   La fecha UTC de los datos de llamada. El formato de fecha depende del tipo de informe elegido y de su configuración regional. Se puede elegir entre las opciones siguientes:
    
      - **--- **  Se muestran todas las llamadas.
    
      - **MMM/AA**   El mes de las llamadas. Por ejemplo, Ene/13.
    
      - **DD/MM/AA**   El día de las llamadas. Por ejemplo, 23/06/2013.

  - **TOTAL**   El número total de llamadas del plan de marcado de mensajería unificada o la puerta de enlace IP de mensajería unificada seleccionado para dicha fecha.

  - **MENSAJE DE VOZ**   El porcentaje de llamadas entrantes a las que mensajería unificada respondió en nombre de los usuarios en las que los autores de llamadas dejaron un mensaje de voz.

  - **PERDIDAS**   El porcentaje de llamadas entrantes a las que mensajería unificada respondió en nombre de los usuarios en las que los autores de llamadas no dejaron un mensaje de voz, lo que dio lugar a una notificación de llamada perdida.

  - **OUTLOOK VOICE ACCESS**   Porcentaje de llamadas entrantes en las que los usuarios iniciaron sesión en la mensajería unificada (y se autenticaron) para obtener acceso a sus correos electrónicos, calendarios y mensajes de voz.

  - **SALIENTE**   El porcentaje de llamadas realizadas o transferidas por mensajería unificada en nombre de los usuarios autenticados o sin autenticar. Esta estadística incluye los tipos de llamada: Buscarme, Reproducir en teléfono y Saludos de Reproducir en teléfono.

  - **OPERADOR AUTOMÁTICO**   El porcentaje de llamadas entrantes respondidas por operadores automáticos de mensajería unificada.

  - **FAX**   El porcentaje de llamadas entrantes que se redirigieron a un socio de fax.

  - **OTRAS**   Porcentaje de cualquier otra llamada entrante o realizada que no pertenece a ninguna de las categorías anteriores. Estas llamadas incluyen las realizadas a los números de Outlook Voice Access en las que los usuarios no iniciaron sesión y no se autenticaron.

  - **CON ERROR O RECHAZADO**   El porcentaje de llamadas con error o rechazadas por mensajería unificada. Tenga en cuenta que las llamadas con error no se cuentan dos veces. Por ejemplo, si se produce un error en una llamada a Outlook Voice Access, solo se cuenta como una llamada con error y no como una llamada de Outlook Voice Access.

  - **CALIDAD DE AUDIO**   Representación gráfica de la calidad de audio general para el periodo de tiempo seleccionado para la organización.

Volver al principio

## Más información

[Investigar la calidad de audio de las llamadas de voz en su organización](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md)

[Interpretar los registros de llamadas de correo de voz](interpret-voice-mail-call-records-exchange-2013-help.md)

