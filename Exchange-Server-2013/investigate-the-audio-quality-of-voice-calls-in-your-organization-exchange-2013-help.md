---
title: 'Investigar la calidad de audio de las llamadas de voz en su organización'
TOCTitle: Investigar la calidad de audio de las llamadas de voz en su organización
ms:assetid: 8a87694b-1678-4a01-859f-5ad3b2c73db5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659069(v=EXCHG.150)
ms:contentKeyID: 50556850
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Investigar la calidad de audio de las llamadas de voz en su organización

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-21_

Si su organización tiene problemas con la calidad de audio de las llamadas de mensajería unificada y los mensajes de correo de voz, use el informe de estadísticas de llamadas como ayuda para conocer lo que provoca los problemas.


> [!NOTE]
> La calidad de audio de una llamada se puede ver afectada por factores que no se tratan en los informes. Por ejemplo, si los servidores Exchange tienen una carga de memoria o de CPU intensa, los usuarios pueden notificar que hay una calidad de audio deficiente, aunque en los informes se indique una calidad de audio excelente.



Para ver tareas adicionales relacionadas con las estadísticas de llamadas consulte [Procedimientos de informes de mensajería unificada](um-reports-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Cmdlets de informes de resumen y datos de llamada de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el EAC para obtener estadísticas de calidad de audio para su organización

1.  En el EAC, vaya a **Mensajería unificada **\> **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") \> **Estadísticas de llamadas**.

2.  Elija las estadísticas de llamada que se incluirán en el informe. El informe se actualiza automáticamente al seleccionar cualquiera de las siguientes opciones:
    
      - **Mostrar **  Elija el tipo de estadísticas de llamada que se mostrará:
        
          - **Diariamente (90 días) **  Seleccione Diariamente para ver los detalles de todas las llamadas de los últimos 90 días.
        
          - **Mensualmente (12 meses)**   Seleccione Mensualmente para ver un resumen de las llamadas por mes de los últimos 12 meses.
        
          - **Todo**   Seleccione Todo para ver las estadísticas combinadas de todas las llamadas recibidas desde que la mensajería unificada empezó a administrar las llamadas.
    
      - **Plan de marcado de mensajería unificada**   Si desea limitar los datos del informe únicamente a las llamadas de un determinado plan de marcado de mensajería unificada, seleccione dicho plan.
    
      - **Puerta de enlace IP de mensajería unificada**   Si desea limitar los datos del informe únicamente a las llamadas de una determinada puerta de enlace IP de mensajería unificada, seleccione dicha puerta de enlace IP de mensajería unificada. Si primero selecciona un plan de marcado de mensajería unificada, en la lista solo estarán disponibles las puertas de enlace IP de MU asociadas al plan de marcado de MU seleccionado.

3.  Para obtener más detalles acerca de la calidad de audio de una fila del informe, seleccione la fila y haga clic en **Detalles de la calidad de audio**. La siguiente información está disponible:
    
      - **FECHA Y HORA**   Fecha y hora UTC a las que se capturaron las estadísticas de llamadas.
    
      - **PLAN DE MARCADO DE MENSAJERÍA UNIFICADA**   Plan de marcado de las llamadas incluidas en las estadísticas.
    
      - **PUERTA DE ENLACE IP DE MENSAJERÍA UNIFICADA**   Puerta de enlace IP de mensajería unificada que aceptó las llamadas incluidas en las estadísticas.
    
      - **NMOS**La opinión media de red (NMOS) para la llamada. NMOS indica la calidad de audio de la llamada como un número en una escala de 1 a 5, donde 5 es excelente.
        

        > [!NOTE]
        > La NMOS máxima posible para una llamada depende del códec de audio que se use. Puede que la NMOS no esté disponible para las llamadas breves de menos de 10&nbsp;segundos.

    
      - **DETERIORO NMOS:**    Cantidad de degradación de audio de la NMOS a partir del máximo valor posible para el códec de audio que se está usando. Por ejemplo, si el valor de degradación NMOS para una llamada fuera 1.2 y la NMOS notificada para la llamada fuera 3.3, la máxima puntuación NMOS para esa llamada sería 4.5 (1.2 + 3.3).
    
      - **VIBRACIÓN**   Variación promedio en la llegada de paquetes de datos para la llamada.
    
      - **PÉRDIDA DE PAQUETES**   Porcentaje promedio de pérdida de paquete de datos de la llamada seleccionada. La pérdida de paquetes es un indicativo de la fiabilidad de la conexión.
    
      - **IDA Y VUELTA**   La puntuación promedio de ida y vuelta, en milisegundos, para el audio en la llamada seleccionada. La puntuación de ida y vuelta mide la latencia en la conexión.
    
      - **DURACIÓN DE PÉRDIDA DE RÁFAGAS**   La duración promedio de la pérdida de paquetes durante las ráfagas de pérdidas para la llamada seleccionada.
    
      - **NÚMERO DE MUESTRAS**   Número de llamadas que se muestrearon para calcular los promedios.

4.  Para las métricas de la calidad de audio detalladas de determinadas llamadas, consulte [Investigación de la calidad de audio de llamadas de voz para un usuario](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md).

