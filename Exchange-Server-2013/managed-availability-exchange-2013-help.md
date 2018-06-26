---
title: 'Disponibilidad administrada: Exchange 2013 Help'
TOCTitle: Disponibilidad administrada
ms:assetid: ceb99e6f-6dca-446d-abfb-3e6fc6a72704
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn482056(v=EXCHG.150)
ms:contentKeyID: 59890416
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disponibilidad administrada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013 SP1_

_**Última modificación del tema:**2017-03-29_

Garantizar que los usuarios tengan una buena experiencia de correo electrónico siempre ha sido el objetivo principal de los administradores del sistema de mensajería. Para ayudar a garantizar la disponibilidad y confiabilidad de la organización de Microsoft Exchange Server 2013, todos los aspectos del sistema deben supervisarse activamente y los problemas detectados deben resolverse rápidamente. En las versiones anteriores de Exchange, la supervisión de componentes críticos del sistema normalmente implicaba el uso de una aplicación externa como Microsoft System Center 2012 Operations Manager para recopilar datos y proporcionar acciones de recuperación para los problemas detectados como resultado del análisis de los datos recopilados. Exchange 2010 y las versiones anteriores incluían manifiestos de mantenimiento y motores de correlación en forma de módulos de administración. Estos componentes habilitaban Operations Manager para determinar si un componente concreto estaba en buen estado o en mal estado. Además, Operations Manager también usaba la infraestructura de cmdlet de diagnóstico integrada en Exchange 2010 para ejecutar transacciones sintéticas en diversos aspectos del sistema.

Exchange 2013 adopta un nuevo enfoque para supervisar y preservar la experiencia del usuario final de forma nativa mediante una característica denominada *Disponibilidad administrada* que proporciona acciones de recuperación y supervisión integradas.

## Disponibilidad administrada

La disponibilidad administrada, también conocida como *supervisión activa* o *supervisión activa local*, es la integración de acciones de recuperación y supervisión integradas con la plataforma de alta disponibilidad de Exchange. Está diseñada para detectar y solucionar problemas a medida que surgen y que el sistema los detecta. A diferencia de las técnicas y soluciones de supervisión externas para Exchange, la disponibilidad administrada no intenta identificar ni comunicar la causa principal de un problema. En cambio, está enfocada en los aspectos de recuperación que abordan tres áreas clave de la experiencia del usuario:

  - **Disponibilidad**   ¿Pueden los usuarios tener acceso al servicio?

  - **Latencia**   ¿Cómo es la experiencia para los usuarios?

  - **Errores**   ¿Los usuarios son capaces de lograr sus objetivos?

La consolidación de rol de servidor y otros cambios arquitectónicos en Exchange 2013 requieren un nuevo enfoque para las metodologías de supervisión y el modelo de mantenimiento usado en las versiones anteriores de Exchange. La disponibilidad administrada está diseñada para tratar estos cambios proporcionando una solución de recuperación y supervisión de mantenimiento nativo. Se aleja de la supervisión de segmentos independientes individuales del sistema para supervisar la experiencia integral del usuario y protege la experiencia del usuario final mediante acciones orientadas a la recuperación.

La disponibilidad administrada es un proceso interno que se ejecuta en cada servidor de Exchange 2013. Sondea y analiza cientos de métricas de mantenimiento cada segundo. Si se encuentra que algo está mal, la mayor parte del tiempo se solucionará automáticamente. Pero siempre habrá problemas que la disponibilidad administrada no podrá solucionar por sí sola. En esos casos, la disponibilidad administrada remitirá el problema a un administrador por medio del registro de eventos.

La disponibilidad administrada implementada mediante dos servicios:

  - **Servicio de administración de mantenimiento de Exchange (MSExchangeHMHost.exe):** es un proceso de controlador que se usa para administrar procesos de trabajo. Se usa para crear, ejecutar, iniciar y detener procesos de trabajo, según sea necesario. También se usa para recuperar procesos de trabajo en caso de que generen errores, para evitar que los procesos de trabajo sean un punto único de error.

  - **Proceso de trabajo de administración de mantenimiento de Exchange (MSExchangeHMWorker.exe)**   Es el proceso de trabajo responsable de realizar las tareas de tiempo de ejecución dentro del marco de disponibilidad administrada.

La disponibilidad administrada usa el almacenamiento persistente para realizar sus funciones:

  - Los archivos XML en la carpeta \\bin\\Monitoring\\config se utilizan para almacenar valores de configuración para algunos de los elementos de trabajo de sondeo y supervisión.

  - Active Directory se utiliza para almacenar reemplazos globales.

  - El Registro de Windows se utiliza para almacenar datos de tiempo de ejecución, como marcadores y reemplazos locales (específicos del servidor).

  - La infraestructura de registro de eventos de canal Crimson de Windows se utiliza para almacenar los resultados de los elementos de trabajo.

  - Los buzones de mantenimiento se utilizan para la actividad de sondeo. Se crearán varios buzones de mantenimiento en cada base de datos de buzones de correo que existe en el servidor.

Como se ilustra en el siguiente diagrama, la disponibilidad administrada incluye tres componentes principales asincrónicos que están funcionando constantemente.

**Componentes de disponibilidad administrada**

![Disponibilidad administrada en Exchange Server 2013](images/Dn482056.7a54dcb5-1e28-4bd4-87e6-0d496b4ab796(EXCHG.150).gif "Disponibilidad administrada en Exchange Server 2013")

El primer componente se denomina *sondeo*. Los sondeos son responsables de tomar medidas en el servidor y recopilar datos. Los resultados de estas medidas se reflejan en el segundo componente, el *monitor*. El monitor contiene la lógica empresarial que usa el sistema en función de lo que se considere como un estado correcto en los datos recopilados. De manera similar a un motor de reconocimiento de patrones, el monitor busca los diferentes patrones en todas las medidas recopiladas y, luego, decide si algo es correcto o no. Por último, están los *respondedores*, que son responsables de las acciones de recuperación y escalación. Cuando hay algo incorrecto, la primera acción es intentar recuperar dicho componente. Esto puede incluir acciones de recuperación de varias etapas; por ejemplo, el primer intento puede ser reiniciar el grupo de aplicaciones; el segundo, reiniciar el servicio; el tercero, reiniciar el servidor y, el próximo, desconectar el servidor de modo que ya no acepte tráfico. Si las acciones de recuperación fracasan, el sistema remite el problema a la persona a través de las notificaciones de registro de eventos.

Hay tres categorías principales de sondeos: sondeos recurrentes, notificaciones y comprobaciones. Los sondeos recurrentes son transacciones sintéticas realizadas por el sistema para probar la experiencia integral del usuario. Las comprobaciones son la infraestructura que recopila los datos de rendimiento, como el tráfico de usuario, y mide los datos recopilados según umbrales definidos para determinar puntas en los errores de usuario. Esto permite que la infraestructura de comprobaciones sepa cuándo tienen problemas los usuarios. Por último, la lógica de notificación permite que el sistema actúe inmediatamente según un evento crítico, sin tener que esperar los resultados de los datos recopilados mediante un sondeo. Por lo general, estas son excepciones o condiciones que se pueden detectar y reconocer sin un conjunto grande de muestras.

Los sondeos recurrentes se ejecutan cada pocos minutos y comprueban algún aspecto del mantenimiento del servicio. Estos sondeos pueden transmitir un correo electrónico mediante Exchange ActiveSync al buzón de supervisión, pueden conectarse a un extremo de RPC o pueden comprobar la conectividad del acceso de cliente al buzón de correo.

Todos los sondeos se definen en el inicio del servicio del administrador de mantenimiento en el canal crimson Microsoft.Exchange.ActiveMonitoring\\ProbeDefinition. Cada definición de sondeo cuenta con muchas propiedades, pero las propiedades más relevantes son:

  - **Name** El nombre del sondeo, que comienza con una *SampleMask* del monitor del sondeo.

  - **TypeName** El tipo de objeto de código del sondeo que contiene la lógica del sondeo.

  - **ServiceName** El nombre del conjunto de mantenimiento que contiene el sondeo.

  - **TargetResource** El objeto que está validando el sondeo. Esto se anexa al nombre del sondeo cuando se ejecuta para convertirse en un resultado del sondeo *ResultName*

  - **RecurrenceIntervalSeconds** La frecuencia de ejecución del sondeo.

  - **TimeoutSeconds** El tiempo que esperará el sondeo antes de presentar un error.

Hay cientos de sondeos recurrentes. Muchos de estos sondeos se realizan según la base de datos, por lo tanto, a medida que aumenta el número de bases de datos, aumenta la cantidad de sondeos. La mayoría de los sondeos se definen en código y, por ende, no se pueden detectar directamente.

Los conceptos básicos de un sondeo recurrente son los siguientes: se inicia cada *RecurrenceIntervalSeconds* y comprueba (o sondea) algún aspecto del mantenimiento. Si el componente está en buen estado, el sondeo pasa y escribe un evento informativo en el canal Microsoft.Exchange.ActiveMonitoring\\ProbeResult con un *ResultType* de 3. Si la comprobación no se realiza correctamente o se agota el tiempo de espera, el sondeo presenta un error y escribe un evento de error en el mismo canal. Un *ResultType* de 4 significa que la comprobación no se realizó correctamente y un *ResultType* de 1 significa que se agotó el tiempo de espera. Muchos sondeos se volverán a ejecutar si se agotó el tiempo de espera, hasta el valor de la propiedad *MaxRetryAttempts*.


> [!NOTE]
> <STRONG>Nota</STRONG> El canal crimson ProbeResult puede estar muy ocupado con cientos de sondeos en ejecución cada minutos y el registro de eventos, por lo que puede generar un verdadero impacto en el rendimiento del servidor Exchange si intenta realizar consultas costosas con los registros de eventos en un entorno de producción.



Las notificaciones son sondeos que no ejecutan el marco del administrador de mantenimiento, sino otro servicio del servidor. Estos servicios ejecutan su propia supervisión y suministran sus datos al marco de disponibilidad administrada al escribir directamente los resultados de los sondeos. No podrá ver estos sondeos en el canal ProbeDefinition, ya que en este canal solo se describen los sondeos que ejecuta el marco de disponibilidad administrada. Por ejemplo, el monitor ServerOneCopyMonitor se desencadena por los resultados de los sondeos escritos por el servicio MSExchangeDAGMgmt. Este servicio lleva a cabo su propia supervisión, determina si hay un problema y registra un resultado de sondeo. La mayoría de los sondeos de notificación tienen la capacidad de registrar tanto un evento rojo que indica que el monitor presenta errores y un evento en verde que representa que el monitor está nuevamente en mantenimiento.

Las comprobaciones son sondeos que solo registran eventos cuando un contador de rendimiento está por encima o por debajo de un umbral definido. Se trata de un caso realmente especial de sondeos de notificación, ya que hay un servicio que supervisa los contadores de rendimiento en el servidor y registra los eventos del canal ProbeResult cuando se alcanza el umbral configurado.

Para encontrar el contador y el umbral que se considera incorrecto, puede buscar en el monitor esta comprobación. Los monitores del tipo *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueAboveThresholdMonitor* o *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueBelowThresholdMonitor* significan que el sondeo que observan es un sondeo de comprobación.

Los monitores consultan los datos recopilados mediante sondeos para determinar si es necesario realizar alguna acción según un conjunto de reglas predefinido. Según la regla o la naturaleza del problema, un monitor puede iniciar un respondedor o remitir el problema a una persona mediante una entrada del registro de eventos. Además, los monitores definen cuánto tiempo transcurrirá después de un error hasta que se ejecute un respondedor, además del flujo de trabajo de la acción de recuperación. Los monitores tienen diversos estados. Desde una perspectiva de estado del sistema, los monitores tienen dos estados:

  - **Correcto** El monitor está funcionando adecuadamente y todas las métricas recopiladas están dentro de los parámetros de funcionamiento normales

  - **Incorrecto**   El monitor no es correcto e inició una recuperación mediante un respondedor o notificó a un administrador mediante la escalación.

Desde una perspectiva administrativa, los monitores tienen estados adicionales que aparecen en el Shell:

  - **Degradado**   Cuando un monitor tiene un estado incorrecto entre 0 y 60 segundos, se considera degradado. Si un monitor tiene un estado incorrecto durante más de 60 segundos, se considera incorrecto.

  - **Deshabilitado** El monitor ha sido explícitamente deshabilitado por un administrador.

  - **No disponible** El servicio de estado de Microsoft Exchange consulta periódicamente el estado de cada monitor. Si no obtiene una respuesta a la consulta, el estado del monitor es no disponible.

  - **Reparando**   Un administrador establece el estado "reparando" para indicar al sistema que hay una persona realizando una acción correctiva, lo cual permite que el sistema y las personas diferencien, entre otros errores que pueden ocurrir al mismo tiempo, la acción correctiva que se está llevando a cabo (como una operación de reinicialización de copia de la base de datos).

Cada monitor tiene una propiedad *SampleMask* en su definición. Cuando el monitor se ejecuta, busca eventos en el canal ProbeResult que tiene un *ResultName* que coincide con la *SampleMask* del monitor. Estos eventos pueden provenir de sondeos recurrentes, notificaciones o comprobaciones. Si se alcanzan los umbrales del monitor, es incorrecto. Desde la perspectiva del monitor, los tres tipos de sondeos son iguales ya que cada uno registra resultados en el canal ProbeResult.

Cabe mencionar que un solo sondeo incorrecto no indica necesariamente que hay algo mal en el servidor. El diseño de los monitores es el que identifica correctamente cuando hay un problema real que debe corregirse. Esta es la razón por la que muchos monitores tienen umbrales incorrectos de varios sondeos antes de presentar errores. Incluso los respondedores pueden corregir automáticamente muchos de estos problemas, por lo que el mejor sitio en el que debe buscar problemas que requieren intervención manual es en el canal crimson Microsoft.Exchange.ManagedAvailability\\Monitoring. Incluirá el error de sondeo más reciente.

Como su nombre sugiere, los respondedores ejecutan algún tipo de respuesta a una alerta generada por un monitor. Los respondedores llevan a cabo diversas acciones de recuperación, como el restablecimiento de un grupo de trabajo de aplicaciones para reiniciar un servidor. Hay varios tipos de respondedores:

  - **Respondedor de reinicio :** termina y reinicia un servicio

  - **Respondedor de restablecimiento de grupo de aplicaciones:** detiene y reinicia un grupo de aplicaciones en Internet Information Services (IIS)

  - **Respondedor de conmutación por error:** inicia una conmutación por error de servidor o base de datos

  - **Respondedor de comprobación de errores:** inicia una comprobación de errores en el servidor, lo que provoca un reinicio del servidor

  - **Respondedor sin conexión:** toma un protocolo en un servidor fuera de servicio (rechaza solicitudes del cliente)

  - **Respondedor en línea:** vuelve a colocar un protocolo en un servidor en producción (acepta solicitudes del cliente)

  - **Respondedor de remisión:** remite el problema a un administrador mediante el registro de eventos

Además de los respondedores enumerados anteriormente, algunos componentes también tienen respondedores especializados que son exclusivos de su componente.

Todos los respondedores incluyen el comportamiento de limitación, que proporciona un mecanismo integrado de secuencias para controlar las acciones de respuesta. El comportamiento de limitación está diseñado para garantizar que el sistema no está en peligro o haya empeorado como resultado de las acciones de recuperación del respondedor. Todos los respondedores están limitados de alguna manera. Cuando se produce la limitación, es posible que se omita o retrase la acción de recuperación del respondedor, según la acción de respuesta. Por ejemplo, cuando se limita el respondedor de comprobación de errores, su acción se omite y no se retrasa.

## Conjunto de mantenimiento

Desde una perspectiva de creación de informes, la disponibilidad administrada tiene dos vistas de mantenimiento: una interna y otra externa. La vista interna usa *conjuntos de mantenimiento*. La disponibilidad administrada supervisa cada componente en Exchange 2013 (por ejemplo, Outlook Web App, Exchange ActiveSync, el servicio Almacén de información, la indización de contenido, los servicios de transporte, etc.) mediante sondeos, monitores y respondedores. Un grupo de sondeos, monitores y respondedores de un componente dado se denomina *conjunto de mantenimiento*. Un conjunto de mantenimiento es un grupo de sondeos, monitores y respondedores que determinan si el componente está en buen estado. El estado actual de un conjunto de mantenimiento (por ejemplo, si está en buen estado o no) se determina mediante el estado de los monitores del conjunto de mantenimiento. Si todos los monitores del conjunto de mantenimiento están en buen estado, el conjunto de mantenimiento está en buen estado. Si un monitor no está en buen estado, el estado del conjunto de mantenimiento se determinará por su monitor menos correcto.

Para los pasos detallados para ver el estado de los conjuntos de mantenimiento o el mantenimiento del servidor, vea [Administrar conjuntos de salud y el estado del servidor](manage-health-sets-and-server-health-exchange-2013-help.md).

## Grupos de mantenimiento

La vista externa de disponibilidad administrada consta de *grupos de mantenimiento*. Los grupos de mantenimiento están expuestos a System Center Operations Manager 2007 R2 y System Center Operations Manager 2012.

Hay cuatro grupos de mantenimiento principales:

  - **Puntos de contacto del cliente:** componentes que afectan a las interacciones del usuario en tiempo real, como los protocolos o el Almacén de información

  - **Componentes del servicio:** componentes sin interacciones directas del usuario en tiempo real, como el servicio de replicación de buzón de Microsoft Exchange o el proceso de generación de las listas de direcciones sin conexión (OABGen)

  - **Componentes de servidor:** los recursos físicos del servidor, tales como el espacio en disco, la memoria y las redes

  - **Disponibilidad de dependencia:** la capacidad del servidor para acceder a dependencias necesarias, como Active Directory, DNS, etc.

Cuando se instala el paquete de administración de Exchange, System Center Operations Manager (SCOM) actúa como un portal de salud para ver información relacionada con el entorno de Exchange. El tablero de mandos SCOM incluye tres vistas Exchange estado del servidor:

  - **Alertas activas:** los respondedores de remisión escriben eventos en el registro de eventos de Windows que usa el monitor en SCOM. Estas aparecen como alertas en la vista de alertas activas.

  - **Mantenimiento de la organización:** un resumen acumulativo del mantenimiento global del mantenimiento de la organización de Exchange se muestra en esta vista. Estos paquetes acumulativos incluyen la visualización de mantenimiento para grupos de disponibilidad de bases de datos individuales y mantenimiento dentro de sitios específicos de Active Directory.

  - **Mantenimiento del servidor:** los conjuntos de mantenimiento relacionados se combinan en grupos de mantenimiento y se resumen en esta vista.

## Reemplazos

Los reemplazos proporcionan a un administrador la capacidad para configurar algunos aspectos de los sondeos, monitores y respondedores de disponibilidad administrada. Los reemplazos se pueden usar para ajustar algunos de los umbrales utilizados por la disponibilidad administrada. También se pueden usar para habilitar acciones de emergencia para eventos inesperados que pueden requerir parámetros de configuración distintos de los valores predeterminados de fábrica.

Los reemplazos se pueden crear y aplicar a un servidor único (lo que se conoce como *reemplazo de servidor*) o se pueden aplicar a un grupo de servidores (lo que se conoce como *reemplazo global*). Los datos de configuración de reemplazo del servidor se almacenan en el Registro de Windows en el servidor en el que se aplica el reemplazo. Los datos de configuración de reemplazo global se almacenan en Active Directory.

Los reemplazos se pueden configurar para que duren indefinidamente o se pueden configurar para una duración determinada. Además, los reemplazos globales se pueden aplicar a todos los servidores o solo a los servidores que ejecutan una versión específica de Exchange.

Al configurar un reemplazo, este no surte efecto inmediatamente. El servicio de administración del estado de Microsoft Exchange busca datos de configuración actualizados cada 10 minutos. Además, los reemplazos globales serán dependientes de la latencia de replicación de Active Directory.

Para los pasos detallados para ver o configurar reemplazos globales o de servidor, vea [Configurar invalidaciones de disponibilidad administrada](configure-managed-availability-overrides-exchange-2013-help.md).

## Cmdlets y tareas de administración

Existen tres tareas operativas principales que normalmente los administradores realizan con respecto a la disponibilidad administrada:

  - Extracción o visualización del mantenimiento del sistema

  - Visualización de conjuntos de mantenimiento y detalles sobre sondeos, monitores y respondedores

  - Administración de reemplazos

Las dos herramientas principales de administración para la disponibilidad administrada son el registro de eventos de Windows y el Shell. Los registros de disponibilidad administrada constituyen una gran cantidad de información en el registro de eventos de canal Crimson ActiveMonitoring y ManagedAvailability de Exchange.

  - Definiciones de sondeo, monitor y respondedor, que se registran en los respectivos registros de eventos de \*definición.

  - Resultados de sondeo, monitor y respondedor, que se registran en los respectivos registros de eventos de \*resultados.

  - Más información acerca de las acciones de recuperación del respondedor, incluso cuando se inicia la acción de recuperación y se considera completa (ya sea correcta o no), que se registran en el registro de eventos de RecoveryActionResults.

Se usan 12 cmdlets para la disponibilidad administrada, los cuales se describen en la tabla siguiente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218703(v=exchg.150)">Get-ServerHealth</a></p></td>
<td><p>Se usa para obtener información de mantenimiento del servidor sin procesar, como conjuntos de mantenimiento y su estado actual (correcto o incorrecto), monitores de conjunto de mantenimiento, componentes de servidor, recursos de destino para sondeos y marcas de tiempo relacionadas con horas de inicio y finalización de sondeos o monitores, así como horas de transición de estado.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218724(v=exchg.150)">Get-HealthReport</a></p></td>
<td><p>Se usa para obtener una vista de mantenimiento de resumen que incluye conjuntos de mantenimiento y su estado actual.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218668(v=exchg.150)">Get-MonitoringItemIdentity</a></p></td>
<td><p>Se usa para ver los sondeos, monitores y respondedores asociados a un conjunto de mantenimiento específico.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218642(v=exchg.150)">Get-MonitoringItemHelp</a></p></td>
<td><p>Se usa para ver descripciones sobre algunas de las propiedades de los sondeos, monitores y respondedores.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218628(v=exchg.150)">Add-ServerMonitoringOverride</a></p></td>
<td><p>Se usa para crear un reemplazo local, específico del servidor de un sondeo, monitor o respondedor.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218664(v=exchg.150)">Get-ServerMonitoringOverride</a></p></td>
<td><p>Se usa para ver una lista de reemplazos locales en el servidor especificado.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/dn482411(v=exchg.150)">Remove-ServerMonitoringOverride</a></p></td>
<td><p>Se usa para quitar un reemplazo local de un servidor específico.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218683(v=exchg.150)">Add-GlobalMonitoringOverride</a></p></td>
<td><p>Se usa para crear un reemplazo global para un grupo de servidores.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218627(v=exchg.150)">Get-GlobalMonitoringOverride</a></p></td>
<td><p>Se usa para ver una lista de los reemplazos globales configurados en la organización.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218675(v=exchg.150)">Remove-GlobalMonitoringOverride</a></p></td>
<td><p>Se usa para quitar un reemplazo global.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218699(v=exchg.150)">Set-ServerComponentState</a></p></td>
<td><p>Se usa para configurar el estado de uno o más componentes del servidor.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/es-es/library/jj218713(v=exchg.150)">Get-ServerComponentState</a></p></td>
<td><p>Se usa para ver el estado de uno o más componentes del servidor.</p></td>
</tr>
</tbody>
</table>

