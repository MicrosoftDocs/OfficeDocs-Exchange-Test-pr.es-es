---
title: 'Investigación de la calidad de audio de llamadas de voz para un usuario: Exchange 2013 Help'
TOCTitle: Investigación de la calidad de audio de llamadas de voz para un usuario
ms:assetid: 0c945886-3cfa-423e-9b46-0d6b1584a145
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659059(v=EXCHG.150)
ms:contentKeyID: 50556739
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Investigación de la calidad de audio de llamadas de voz para un usuario

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-21_

Si un usuario informa un problema con la calidad de audio de sus llamadas de mensajería unificada (MU), use el informe Registros de llamadas de usuario como ayuda para conocer qué provoca los problemas.


> [!NOTE]
> La calidad de audio de una llamada se puede ver afectada por factores que no se tratan en los informes. Por ejemplo, si los servidores de Exchange tienen una carga de memoria o de CPU intensa, los usuarios pueden informar de que la calidad del audio es deficiente aunque en los informes ponga que es excelente.



Para tareas adicionales relacionadas con informes de mensajería unificada, consulte [Procedimientos de informes de mensajería unificada](um-reports-procedures-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Cmdlets de informe de resumen y datos de llamadas de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Centro de Administración de Exchange para obtener los registros de llamadas para un usuario habilitado para MU

1.  En el Centro de Administración de Exchange, navegue a **Mensajería unificada** \> **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") \> **Registros de llamadas de usuarios**.

2.  Haga clic en **Seleccionar un usuario** y, a continuación, seleccione al usuario del que desea los datos.

3.  Para obtener más detalles acerca de la calidad de audio de una fila del informe, seleccione la fila y haga clic en **Detalles de la calidad de audio**. La siguiente información está disponible:
    
      - **FECHA Y HORA**   La fecha y la hora de la llamada, en la zona horaria que el usuario seleccionado ha establecido en Outlook Web App.
    
      - **USUARIO** El usuario seleccionado.
    
      - **PLAN DE MARCADO DE MU** El plan de marcado para la llamada.
    
      - **PUERTA DE ENLACE IP DE MU** La puerta de enlace de MU que se usó para la llamada.
    
      - **CÓDEC DE AUDIO** El códec de audio que se usó durante la llamada.
    
      - **NMOS**   La puntuación de opinión media de red (NMOS) para la llamada. La NMOS indica la calidad de audio de la llamada como un número en una escala de 1 a 5, donde 5 es excelente.
        

        > [!NOTE]
        > El valor máximo de la NMOS para la llamada depende del códec de audio usado. Es posible que la NMOS no esté disponible para llamadas muy cortas de menos de 10 segundos de duración.

    
      - **DETERIORO NMOS** La cantidad de degradación de audio de la NMOS a partir del máximo valor posible para el códec de audio que se está usando. Por ejemplo, si el valor de degradación NMOS para una llamada fuera 1.2 y la puntuación NMOS notificada para la llamada fuera 3.3, la máxima NMOS para esa llamada sería 4.5 (1.2 + 3.3).
    
      - **VIBRACIÓN** La variación promedio en la llegada de paquetes de datos para la llamada.
    
      - **PÉRDIDA DE PAQUETES** El porcentaje promedio de pérdida de paquete de datos de la llamada seleccionada. La pérdida de paquetes es un indicativo de la fiabilidad de la conexión.
    
      - **IDA Y VUELTA** La puntuación promedio de ida y vuelta, en milisegundos, para el audio en la llamada seleccionada. La puntuación de ida y vuelta mide la latencia en la conexión.
    
      - **DURACIÓN DE PÉRDIDA DE RÁFAGAS** La duración promedio de la pérdida de paquetes durante las ráfagas de pérdidas para la llamada seleccionada.

