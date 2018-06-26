---
title: 'Interpretar los registros de llamadas de correo de voz: Exchange 2013 Help'
TOCTitle: Interpretar los registros de llamadas de correo de voz
ms:assetid: 368d9c58-61a2-43d5-8189-d3469a9e2a8d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659061(v=EXCHG.150)
ms:contentKeyID: 50556771
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Interpretar los registros de llamadas de correo de voz

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Para ver información detallada sobre las llamadas que administran los servidores de Exchange un día concreto, exporte los datos de llamadas correspondientes a ese día desde el informe Estadísticas de llamadas. Los datos de llamadas diarios, disponibles para los últimos 90 días, pueden servir para diagnosticar problemas relacionados con la calidad de audio o las llamadas rechazadas, y dan información para las auditorías o los informes en los servidores de Exchange de la organización.

Para tareas adicionales relacionadas con informes de mensajería unificada, consulte [Procedimientos de informes de mensajería unificada](um-reports-procedures-exchange-2013-help.md).

## Uso del EAC para exportar registros de llamadas diarias de MU

1.  En el EAC, vaya a **Mensajería unificada** \> **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") \> **Estadísticas de llamadas**.

2.  En **Mostrar**, haga clic en **Diariamente (90 días)** y, luego, seleccione el plan de marcado de MU o la puerta de enlace IP de MU, o ambos, si lo desea. El informe se actualiza automáticamente mientras elige las opciones.

3.  Seleccione el día cuyos registros de llamadas desea exportar y, luego, haga clic en **Exportar día**.

4.  En el cuadro de confirmación **Descarga de archivos**, haga clic en **Abrir** o **Guardar**.
    
    El archivo exportado se denominará um\_cdr\_*AAAA-MM-DD*.csv, donde *AAAA-MM-DD* es el año, el mes y el día en que se ejecutó el informe.
    

    > [!NOTE]
    > En la página del informe, puede descargar una plantilla de Microsoft Excel que puede usar para importar el archivo .csv correspondiente a un día concreto.



5.  Utilice una aplicación como Excel para procesar el archivo .csv y generar sus propios informes personalizados.

## Interpretación de los datos de llamada de MU

Los datos de llamadas de mensajería unificada exportados incluyen la siguiente información detallada sobre cada una de las llamadas que la mensajería unificada ha controlado a lo largo del día.


> [!NOTE]
> En el informe de estadísticas de llamadas, los días están en hora UTC.



  - **Hora de inicio de la llamada   **La fecha y hora en que la mensajería unificada controló la llamada, en hora UTC. La fecha y hora UTC se representan en el siguiente formato: *AAAA-MM-DD hh:mm:SSZ*, donde *AAAA* = año, *MM* = mes, *DD* = día, *hh* = hora, en formato de 24 horas, *mm* = minutos, ss = segundos. Z significa Zulu, que es una forma de denotar UTC (como +*hh*:*mm* o -*hh*:*mm*, que proporciona la hora UTC). Dado que todas las horas de llamada del informe están en hora UTC, aquí siempre se usará una Z.
    
    Por ejemplo, en el caso de una llamada realizada el 23.06.13 a las 2:23 p.m, la hora de inicio de la llamada se muestra como 23/06/2013 14:23:11Z.

  - **Tipo de llamada   **El tipo de llamada:
    
      - **Mensaje de voz de contestador automático**  La llamada no se ha atendido y se ha desviado a los servidores de Exchange; el autor de la llamada ha dejado un mensaje de voz.
    
      - **Llamada perdida de contestador automático**  La llamada no se ha atendido y se ha desviado a los servidores de Exchange; el autor de la llamada no ha dejado un mensaje de voz.
    
      - **Acceso de suscriptor**   Se realizó una llamada al número de acceso del suscriptor. El autor de la llamada inició sesión y fue autenticado en la MU con su extensión y su contraseña para obtener acceso a mensajes de correo electrónico, calendarios y mensajes de voz en el teléfono.
    
      - **Operador automático** Un operador automático de mensajería unificada ha atendido la llamada. Estas llamadas son las típicas llamadas en las que el autor de la llamada marca el número de teléfono principal de la organización.
    
      - **Fax**   Se recibió una llamada en la que se detectó un tono de fax. Si ha configurado asociados de fax, esta llamada se envió al asociado de fax.
    
      - **Reproducir en teléfono** La mensajería unificada realizó una llamada porque el usuario hizo clic en el botón Reproducir en teléfono en un mensaje de voz en Microsoft Outlook Web App o Outlook.
    
      - **Buscarme**   La mensajería unificada realizó una llamada saliente como resultado de la existencia de una regla Buscarme en una regla de respuesta a llamada.
    
      - **Número piloto no autenticado**   Se realizó una llamada al número de Outlook Voice Access. El autor de la llamada no inició sesión ni fue autenticado.
    
      - **Grabado del saludo**   La mensajería unificada realizó una llamada para registrar los saludos personales de un usuario.
    
      - **Ninguno** Se realizó una llamada pero el tipo no se ha definido.

  - **Identidad de la llamada** La identidad de la llamada SIP, tal como la suministra la puerta de enlace IP de MU.

  - **Identidad de la llamada principal** La identidad de la sesión SIP que originó la llamada. Este cuadro se usa cuando se usa la característica Buscarme de las reglas de respuesta a llamada o la transferencia de llamadas, incluidas las transferencias entre operadores automáticos de MU.

  - **Nombre del servidor de MU** El nombre del servidor de buzones que controla la llamada, si lo hubiere. Solo se proporciona esta información si se dispone de un servidor de buzones local.

  - **Nombre del plan de marcado** El plan de marcado de MU que controla la llamada.

  - **Duración de la llamada** La duración total de la llamada.

  - **Dirección de la puerta de enlace IP** El nombre de dominio completo (FQDN) de la puerta de enlace IP que controló la llamada.

  - **Número de teléfono marcado** El número de teléfono o la dirección SIP del destinatario de la llamada (para los usuarios de los planes de marcado de SIP, como los usuarios de Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server).

  - **Número de teléfono del autor de la llamada** El número de teléfono o la dirección SIP del autor de la llamada.

  - **Resultado de la oferta** El estado de la llamada:
    
      - **Respuesta**   La mensajería unificada ha respondido o ha realizado una llamada correctamente. La llamada no se ha transferido ni se ha redirigido. Estas llamadas incluyen las llamadas a Outlook Voice Access, Reproducir en teléfono u operadores automáticos de mensajería unificada que se han completado, y las llamadas que tuvo que controlar la mensajería unificada porque la extensión a la que se llamó no atendió el teléfono.
    
      - **Error**   La mensajería unificada ha aceptado o ha realizado una llamada, pero esta ha generado un error. Estas llamadas incluyen las llamadas cuya dirección o número marcado está ocupado, no contesta o no existe; las llamadas en las que el autor de la llamada cuelga antes de que se haya establecido la conexión; las llamadas en las que el plan de marcado de MU o la configuración de directiva de buzón de correo de MU impide la llamada; o las llamadas en las que no se puede llegar a la puerta de enlace VoIP o IP PBX en su sistema telefónico.
    
      - **Rechazada**   La mensajería unificada ha rechazado la llamada, normalmente debido a un error de configuración. Estas llamadas incluyen las llamadas en las que la puerta de enlace IP de UM no está asociada a un plan de marcado de UM o en las que existen problemas de incompatibilidad.
    
      - **Redirigida**   La MU aceptó la llamada, pero la redirigió a otro servidor de buzones. Estas llamadas incluyen las llamadas en las que el autor usó el menú de la MU para llamar a un contacto en el directorio o los contactos personales, o en las que el autor llamó a un número de Outlook Voice Access con un número telefónico que no está asociado con el buzón de correo del usuario. En estos casos, la UM transfiere la llamada al servidor de Exchange asociado con esa cuenta de usuario.
    
      - **Ninguno**   El estado de la llamada es desconocido.

  - **Motivo de desconexión de la llamada** La razón por la que se ha desconectado la llamada, siempre y cuando la MU haya podido determinar dicha razón. Por ejemplo, si el autor de la llamada colgó, se muestra Graceful Hangup.

  - **Motivo de la llamada** Cómo se conectó la llamada:
    
      - **Directo**   El autor de la llamada ha marcado el número directamente.
    
      - **Desvío**   El autor de la llamada ha marcado un número, pero la persona a la que ha llamado ha redirigido la llamada al correo de voz de mensajería unificada.
    
      - **Desvío ocupado **  El autor de la llamada ha marcado un número, pero la persona estaba ocupada, por lo que la llamada se ha redirigido al correo de voz de MU.
    
      - **Desvío sin respuesta **  El autor de la llamada ha marcado un número, pero la persona no ha respondido, por lo que la llamada se ha redirigido al correo de voz de mensajería unificada.
    
      - **Saliente**   La MU realizó la llamada, por ejemplo, para reproducir un mensaje de voz usando Reproducir en teléfono.
    
      - **Ninguno**   No se ha dado ninguna razón para la llamada.

  - **Cadena marcada** La dirección o el número de teléfono de la persona a la que se ha redirigido o transferido esta llamada. Este valor también hace referencia a la dirección o el número de teléfono marcado en las llamadas Reproducir en teléfono.

  - **Alias del buzón del autor de la llamada** El alias de buzón de correo (la parte de la dirección de correo electrónico que precede al símbolo @) del autor de la llamada. Este valor solo está disponible si el autor de la llamada inició sesión en Outlook Voice Access.

  - **Alias del buzón del autor de la llamada** El alias de buzón de correo del destinatario de la llamada, si dicho destinatario es un usuario habilitado para la MU.

  - **Nombre del operador automático** El nombre del operador automático relacionado con esta llamada.

  - **Puntuación de NMOS** La puntuación de opinión media de red (NMOS) para la llamada. La NMOS indica la calidad de audio de la llamada como un número en una escala de 1 a 5, donde 5 es excelente.
    

    > [!NOTE]
    > <STRONG>Nota</STRONG>&nbsp;&nbsp;&nbsp;El valor máximo de la NMOS para la llamada depende del códec de audio usado. Es posible que la NMOS no esté disponible para llamadas muy cortas de menos de 10 segundos de duración.



  - **Degradación NMOS** La cantidad de degradación de audio de la puntuación NMOS a partir del máximo valor posible para el códec de audio que se está usando. Por ejemplo, si el valor de degradación NMOS para una llamada fuera 1.2 y la puntuación NMOS notificada para la llamada fuera 3.3, la máxima NMOS para esa llamada sería 4.5 (1.2 + 3.3).

  - **Vibración de la degradación NMOS** La degradación NMOS total por la vibración.

  - **Pérdida de paquetes de la degradación NMOS** La degradación NMOS total por la pérdida de paquetes.

  - **Vibración   **La variación promedio en la llegada de paquetes de datos para la llamada.

  - **Pérdida de paquetes    **El porcentaje promedio de pérdida de paquetes de datos para la llamada seleccionada. La pérdida de paquetes es un indicativo de la fiabilidad de la conexión.

  - **Ida y vuelta** El tiempo promedio de ida y vuelta, en milisegundos, para el audio en la llamada seleccionada. La puntuación de ida y vuelta mide la latencia en la conexión.

  - **Densidad de ráfagas   **El porcentaje de paquetes perdidos y descartados durante un período de pérdida de ráfagas (tasa de pérdida elevada).

  - **Duración del intervalo de ráfagas   **La duración promedio de la pérdida de paquetes durante la pérdida de ráfagas para la llamada seleccionada.

  - **Códec de audio   **El códec de audio utilizado durante la llamada.

