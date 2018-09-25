---
title: 'Supervisión de grupos de disponibilidad de base de datos: Exchange 2013 Help'
TOCTitle: Supervisión de grupos de disponibilidad de base de datos
ms:assetid: f5bdfd6e-e93c-4d96-8bc2-548750d51930
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351258(v=EXCHG.150)
ms:contentKeyID: 48268879
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supervisión de grupos de disponibilidad de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Puede usar la información detallada de este tema para supervisar el mantenimiento y el estado de las copias de la base de datos de buzones de correo para los grupos de disponibilidad de base de datos (DAG), para recopilar información de diagnóstico y configurar el umbral de supervisión de espacio insuficiente en disco.

## Cmdlet Get-MailboxDatabaseCopyStatus

Puede usar el cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/es-es/library/dd298044\(v=exchg.150\)) para ver información de estado de las copias de bases de datos de buzones de correo. Este cmdlet permite ver información sobre todas las copias de una base de datos determinada, información sobre una copia específica de una base de datos en un servidor determinado o información sobre todas las copias de bases de datos de un servidor. La tabla siguiente describe los posibles valores del estado de una copia de base de datos de buzones de correo.

### Estado de copia de base de datos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Estado de copia de base de datos</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Failed</p></td>
<td><p>La copia de una base de datos de buzones de correo muestra el estado Failed (Error) porque no está suspendida, ni puede copiar o reproducir archivos de registro. Mientras su estado sea Failed y no esté suspendida, el sistema comprobará periódicamente si se ha resuelto el problema que hizo que el estado de la copia cambiara a Failed. Una vez que el sistema ha detectado que el problema se ha resuelto, y ha descartado otros problemas, el estado de la copia cambiará automáticamente a Healthy (Correcta).</p></td>
</tr>
<tr class="even">
<td><p>Inicialización</p></td>
<td><p>La copia de base de datos se está propagando, el índice de contenido de la copia de base de datos de buzones de correo se está propagando o ambos elementos se están propagando. Una vez completada correctamente la propagación, el estado de copia cambiará a Initializing (Inicializando).</p></td>
</tr>
<tr class="odd">
<td><p>SeedingSource</p></td>
<td><p>La copia de base de datos de buzones de correo se está usando como origen de una operación de inicialización de copia de base de datos.</p></td>
</tr>
<tr class="even">
<td><p>Suspended</p></td>
<td><p>La copia de base de datos de buzones de correo está en estado Suspended (Suspendida) porque un administrador ha suspendido de forma manual la copia de base de datos mediante la ejecución del cmdlet <strong>Suspend-MailboxDatabaseCopy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Healthy</p></td>
<td><p>La copia de base de datos de buzones de correo está copiando y reproduciendo archivos de registro correctamente, o bien ha conseguido copiar y reproducir todos los archivos de registro disponibles.</p></td>
</tr>
<tr class="even">
<td><p>ServiceDown</p></td>
<td><p>El servicio de replicación de Microsoft Exchange no está disponible o se está ejecutando en el servidor que hospeda la copia de base de datos de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>Initializing</p></td>
<td><p>La copia de base de datos de buzones de correo está en estado de inicialización cuando se cree una copia de base de datos, cuando el servicio de replicación de Microsoft Exchange se esté iniciando o acabe de ser iniciado y durante las transiciones de los estados Suspended, ServiceDown, Failed, Seeding o SinglePageRestore a otro estado. Mientras permanece en este estado, el sistema verifica que la base de datos y la secuencia de registro sean coherentes. En la mayoría de los casos, el estado de la copia permanecerá en el estado Initializing durante unos 15 segundos, pero en general, no debería permanecer en dicho estado por más de 30 segundos.</p></td>
</tr>
<tr class="even">
<td><p>Resynchronizing</p></td>
<td><p>La copia de base de datos de buzones de correo y los archivos de registro correspondientes se están comparando con la copia activa de la base de datos para comprobar si existen divergencias entre las dos copias. El estado de la copia permanecerá así hasta que se detecte y resuelvan las divergencias.</p></td>
</tr>
<tr class="odd">
<td><p>Mounted</p></td>
<td><p>La copia activa está en línea y acepta conexiones de clientes. Solo la copia activa de la copia de base de datos de buzones de correo puede tener el estado Mounted (montada).</p></td>
</tr>
<tr class="even">
<td><p>Dismounted</p></td>
<td><p>La copia activa está sin conexión y no acepta conexiones de clientes. Solo la copia activa de la copia de base de datos de buzones de correo puede tener el estado Dismounted (desmontada).</p></td>
</tr>
<tr class="odd">
<td><p>Mounting</p></td>
<td><p>La copia activa se está conectando y aún no acepta conexiones de clientes. Solo la copia activa de la copia de base de datos de buzones de correo puede tener el estado Mounting (montando).</p></td>
</tr>
<tr class="even">
<td><p>Dismounting</p></td>
<td><p>La copia activa se está desconectando y está cerrando las conexiones de clientes. Solo la copia activa de la copia de base de datos de buzones de correo puede tener el estado Dismounting (desmontando).</p></td>
</tr>
<tr class="odd">
<td><p>DisconnectedAndHealthy</p></td>
<td><p>La copia de base de datos de buzones de correo ya no está conectada a la copia de base de datos activa, y tenía el estado Healthy (correcta) cuando se perdió la conexión. Este estado define cómo está la copia de base de datos con respecto a la conectividad con su copia de origen. Puede notificarse durante los errores de red de DAG entre la copia de origen y la copia de base de datos de destino.</p></td>
</tr>
<tr class="even">
<td><p>DisconnectedAndResynchronizing</p></td>
<td><p>La copia de base de datos de buzones de correo ya no está conectada a la copia de base de datos activa, y tenía el estado Resynchronizing (volviendo a sincronizar) cuando se perdió la conexión. Este estado define cómo está la copia de base de datos con respecto a la conectividad con su copia de origen. Puede notificarse durante los errores de red de DAG entre la copia de origen y la copia de base de datos de destino.</p></td>
</tr>
<tr class="odd">
<td><p>FailedAndSuspended</p></td>
<td><p>El sistema establece los estados Failed (error) y Suspended (suspendida) simultáneamente porque se ha detectado un error y porque la resolución del error requiere la intervención expresa de un administrador. Un ejemplo sería cuando el sistema detecta divergencias irrecuperables entre la base de datos de buzones de correo activa y la copia de base de datos. A diferencia del estado Failed (error), el sistema no comprobará periódicamente si se ha resuelto el problema para recuperarse de forma automática. En su lugar, debe intervenir un administrador para resolver la causa subyacente del error antes de que la copia de base de datos pueda pasar al estado Healthy (correcta).</p></td>
</tr>
<tr class="even">
<td><p>SinglePageRestore</p></td>
<td><p>Este estado indica que se está llevando a cabo una operación de restauración de página única en la copia de base de datos de buzones de correo.</p></td>
</tr>
</tbody>
</table>


El cmdlet **Get-MailboxDatabaseCopyStatus** también devuelve detalles sobre las redes de replicación en uso, incluido *IncomingLogCopyingNetwork*, que se devuelve para copias pasivas de bases de datos, y *OutgoingConnections*, que se devuelve para bases de datos activas con más de una copia, así como cualquier copia de base de datos usada como fuente para una operación de inicialización de una base de datos. La información de conexión saliente se proporciona para las copias de bases de datos en replicación de modo de archivos. La información de conexión saliente no se proporciona para las copias de bases de datos en replicación de modo de bloque.

## Ejemplos de Get-MailboxDatabaseCopyStatus

Los ejemplos siguientes usan el cmdlet **Get-MailboxDatabaseCopyStatus**. Cada ejemplo envía los resultados al cmdlet **Format-List** para que los muestre en formato de lista.

En este ejemplo se devuelve información de estado para todas las copias de la base de datos DB2.

```powershell
Get-MailboxDatabaseCopyStatus -Identity DB2 | Format-List
```

En este ejemplo se devuelve el estado de todas las copias de base de datos del servidor de buzones de correo MBX2.

```powershell
Get-MailboxDatabaseCopyStatus -Server MBX2 | Format-List
```

En este ejemplo se devuelve el estado de todas las copias de base de datos del servidor de buzones de correo local.

```powershell
Get-MailboxDatabaseCopyStatus -Local | Format-List
```

Para obtener más información acerca del cmdlet **Get-MailboxDatabaseCopyStatus**, vea [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/es-es/library/dd298044\(v=exchg.150\)).

## Cmdlet Test-ReplicationHealth

Puede usar el cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/es-es/library/bb691314\(v=exchg.150\)) para ver información de estado de la replicación continua de copias de bases de datos de buzones de correo. Use el cmdlet para comprobar todos los aspectos del estado de replicación y reproducción con el fin de proporcionar una descripción general completa de un servidor de buzones de correo concreto de un grupo de disponibilidad de base de datos (DAG).

El cmdlet **Test-ReplicationHealth** está diseñado para realizar una supervisión proactiva de la replicación continua y de la canalización de replicación continua, la disponibilidad de Active Manager, el estado y el mantenimiento del servicio de clúster subyacente, así como de los componentes de quórum y de red. Se puede ejecutar de forma local o remota en cualquier servidor de buzones de correo de un grupo de disponibilidad de base de datos. El cmdlet **Test-ReplicationHealth** realiza las pruebas que se enumeran en la tabla siguiente.

### Pruebas del cmdlet Test-ReplicationHealth

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de la prueba</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ClusterService</p></td>
<td><p>Verifica que el servicio de clúster se está ejecutando y está accesible en el miembro DAG especificado; y, si no se ha especificado ningún miembro DAG, en el servidor local.</p></td>
</tr>
<tr class="even">
<td><p>ReplayService</p></td>
<td><p>Verifica que el servicio de replicación de Microsoft Exchange se está ejecutando y está accesible en el miembro DAG especificado; y, si no se ha especificado ningún miembro DAG, en el servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>ActiveManager</p></td>
<td><p>Comprueba que la instancia de Active Manager que se está ejecutando en el miembro DAG especificado, y si no se ha especificado ningún miembro DAG, en el servidor local, tiene asignado un rol válido (principal, secundario o independiente).</p></td>
</tr>
<tr class="even">
<td><p>TasksRpcListener</p></td>
<td><p>Verifica que el servidor de llamada a procedimiento remoto (RPC) para tareas se está ejecutando y está accesible en el miembro DAG especificado; y, si no se ha especificado ningún miembro DAG, en el servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>TcpListener</p></td>
<td><p>Verifica que el proceso de escucha de copias de registros TCP se está ejecutando y está accesible en el miembro DAG especificado; y, si no se ha especificado ningún miembro DAG, en el servidor local.</p></td>
</tr>
<tr class="even">
<td><p>ServerLocatorService</p></td>
<td><p>Comprueba los procesos de cliente/servidor de Active Manager en miembros del DAG y en el servidor de acceso de cliente que realizan búsquedas en Active Directory y Active Manager para determinar dónde está activa una base de datos de buzones de correo de un usuario.</p></td>
</tr>
<tr class="odd">
<td><p>DagMembersUp</p></td>
<td><p>Verifica que todos los miembros DAG están disponibles, ejecutándose y accesibles.</p></td>
</tr>
<tr class="even">
<td><p>ClusterNetwork</p></td>
<td><p>Comprueba que todas las redes administradas por clúster del miembro DAG especificado, y si no se ha especificado ninguno, del servidor local, están disponibles.</p></td>
</tr>
<tr class="odd">
<td><p>QuorumGroup</p></td>
<td><p>Verifica que el grupo de clústeres (grupo de quórum) predeterminado está en buen estado y conectado.</p></td>
</tr>
<tr class="even">
<td><p>FileShareQuorum</p></td>
<td><p>Verifica que el servidor testigo, el directorio testigo y el recurso compartido configurados para el grupo de disponibilidad de base de datos (DAG) están accesibles.</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseRedundancy</p></td>
<td><p>Comprueba que hay al menos una copia correcta disponible de las bases de datos en el miembro del DAG especificado, o si no hay ningún miembro del DAG especificado, en el servidor local.</p></td>
</tr>
<tr class="even">
<td><p>DatabaseAvailability</p></td>
<td><p>Comprueba que las bases de datos tienen suficiente disponibilidad en el miembro DAG especificado; y, si no se ha especificado ningún miembro DAG, en el servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>DBCopySuspended</p></td>
<td><p>Comprueba si hay alguna copia de base de datos de buzones de correo en el estado Suspended (suspendida) en el miembro DAG especificado; y, si no se ha especificado ningún miembro DAG, en el servidor local.</p></td>
</tr>
<tr class="even">
<td><p>DBCopyFailed</p></td>
<td><p>Comprueba si hay alguna copia de base de datos de buzones de correo en el estado Failed (error) en el miembro DAG especificado; y, si no se ha especificado ningún miembro DAG, en el servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>DBInitializing</p></td>
<td><p>Comprueba si hay alguna copia de base de datos de buzones de correo en el estado Initializing (inicializando) en el miembro DAG especificado; y, si no se ha especificado ningún miembro DAG, en el servidor local.</p></td>
</tr>
<tr class="even">
<td><p>DBDisconnected</p></td>
<td><p>Comprueba si hay alguna copia de base de datos de buzones de correo en el estado Disconnected (desconectada) en el miembro DAG especificado; y, si no se ha especificado ningún miembro DAG, en el servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>DBLogCopyKeepingUp</p></td>
<td><p>Comprueba que el proceso de copia de registros e inspección de las copias pasivas de base de datos en el miembro DAG especificado, y si no se ha especificado ninguno, en el servidor local, consigue mantener la actividad de generación de registros en la copia activa.</p></td>
</tr>
<tr class="even">
<td><p>DBLogReplayKeepingUp</p></td>
<td><p>Comprueba que la actividad de reproducción de las copias pasivas de base de datos en el miembro DAG especificado, y si no se ha especificado ninguno, en el servidor local, consigue mantener la actividad de copia de registros y de inspección.</p></td>
</tr>
</tbody>
</table>


## Ejemplo de Test-ReplicationHealth

En este ejemplo se usa el cmdlet **Test-ReplicationHealth** para comprobar el mantenimiento de replicación del servidor de buzones de correo MBX1.

```powershell
Test-ReplicationHealth -Identity MBX1
```

## Registro de eventos de canal Crimson

Windows incluye dos categorías de registros de eventos: Registros de Windows y registros de aplicaciones y servicios. La categoría de registros de Windows incluye los registros de eventos disponibles en versiones anteriores de Windows: Registros de eventos de aplicaciones, seguridad y sistema. También incluye dos nuevos registros: Setup y ForwardedEvents. Los registros de Windows tienen como objetivo almacenar eventos de aplicaciones heredadas y eventos que se aplican a todo el sistema.

Los registros de aplicaciones y servicios son una nueva categoría de registros de eventos. Estos registros almacenan eventos de una única aplicación o de un único componente, en lugar de eventos que pueden tener incidencia en todo el sistema. A esta nueva categoría de registros de eventos se alude como a un canal Crimson de aplicaciones.

La categoría de los registros de aplicaciones y servicios incluye cuatro subtipos: Registros administrativos, operativos, analíticos y de depuración. Los eventos de los registros administrativos son especialmente interesantes si el motivo por el que lleva un registro de eventos es para solucionar problemas. Los eventos en el registro administrativo deben proporcionar ayuda sobre cómo responder a los eventos. Los eventos del registro operativo también son útiles, pero quizá sea necesario un conocimiento más profundo. Los registros administrativos y de depuración no son especialmente sencillos para el usuario. Los registros analíticos (que aparecen ocultos o deshabilitados de manera predeterminada) almacenan eventos que hacen un seguimiento de un problema, y suele haber un número elevado de eventos registrado. Los registros de depuración son utilizados por los desarrolladores para depurar aplicaciones.

Exchange 2013 registra eventos en los canales Crimson del área de registros de aplicaciones y servicios. Puede ver estos canales si sigue los pasos que se detallan a continuación:

1.  Abra el Visor de eventos.

2.  En el árbol de la consola, vaya a **Registros de aplicaciones y servicios**\>**Microsoft**\>**Exchange**.

3.  En **Exchange**, seleccione un canal crimson, como **HighAvailability** o **MailboxDatabaseFailureItems** para ver el DAG y eventos relacionados con la copia de la base de datos, o **ActiveMontoring** o **ManagedAvailability** para ver eventos relacionados con la disponibilidad administrada.

El canal HighAvailability contiene eventos relacionados con el inicio y apagado del servicio de replicación de Microsoft Exchange, y los diferentes componentes que se ejecutan en el servicio de replicación de Microsoft Exchange, como Active Manager, una API de replicación sincrónica de otros fabricantes, el servidor RPC de tareas, el proceso de escucha TCP y el escritor del servicio de instantáneas de volumen (VSS). El canal HighAvailability también es utilizado por Active Manager para registrar eventos relacionados con la supervisión de funciones de Active Manager y eventos de acción de base de datos, como la operación de montaje de base de datos y el truncado de registros, y también para registrar eventos relacionados con el clúster subyacente del grupo de disponibilidad de bases de datos.

El canal MailboxDatabaseFailureItems se usa para registrar eventos asociados con errores que afectan a una base de datos de buzones de correo replicada.

El canal ActiveMonitoring contiene eventos de definición y resultados de monitores, respondedores y sondeos de disponibilidad administrada.

El canal ManagedAvailability contiene los registros y los resultados de la acción de recuperación, y eventos relacionados.

## Monitor de espacio insuficiente en disco

La disponibilidad administrada de Exchange 2013 supervisa cientos de componentes y métricas del sistema cada minuto, incluida la cantidad de espacio libre en disco en los volúmenes que usa el rol de servidor Buzón de correo. En las versiones anteriores a Exchange 2013 Service Pack 1 (SP1), Exchange supervisa el espacio disponible en todos los volúmenes locales, incluidos los volúmenes que no contienen ninguna base de datos o archivo de registro. En SP1 y versiones posteriores, solo se supervisan los volúmenes que contienen archivos de registro y bases de datos de Exchange. En SP1, el umbral predeterminado para el monitor de espacio de bajo volumen es de 200 GB. En la actualización acumulativa 6 de Exchange 2013 y en las versiones posteriores, el umbral predeterminado es 180 GB. En SP1 y versiones posteriores, puede configurar el umbral al agregar el siguiente valor del Registro DWORD (en MB) en cada servidor de buzones de correo que desea personalizar:

Ruta de acceso: **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters**

Valor: *SpaceMonitorLowSpaceThresholdInMB*

Por ejemplo, para configurar el umbral en 100 GB, deberá configurar el siguiente valor del Registro:

**REG\_DWORD 186a0 (100000)**

Después de configurar o modificar el valor del registro anterior, debe reiniciar el servicio de administración de Microsoft Exchange DAG para que el cambio surta efecto.

## Script CollectOverMetrics.ps1

Exchange 2013 incluye un script denominado CollectOverMetrics.ps1, que puede encontrar en la carpeta Scripts. CollectOverMetrics.ps1 lee los registros de eventos de los miembros del DAG para recopilar información sobre las operaciones de base de datos (como montajes, movimientos y conmutación por error de bases de datos) durante un período de tiempo específico. Para cada operación, el script registra la información siguiente:

  - Identidad de la base de datos

  - La hora a la que ha comenzado y finalizado la operación

  - Los servidores en los que se había montado la base de datos al inicio y al final de la operación

  - La razón de la operación

  - Si la operación se completó correctamente o no y, en caso de error, se incluyen los detalles del error

Este script escriba la información en archivos .csv con una operación por fila. Escribe un archivo .csv por separado para cada DAG.

El script admite parámetros que permiten personalizar el comportamiento y los resultados del mismo. Por ejemplo, los resultados se pueden restringir a un subconjunto especificado mediante el parámetro *Database* o *ReportFilter*. Solamente se incluirán en el informe HTML de resumen las operaciones que coincidan con estos filtros. En la tabla siguiente se muestran los parámetros disponibles.

### Parámetros del script CollectOverMetrics.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DatabaseAvailabilityGroup</em></p></td>
<td><p>Especifica el nombre del grupo de disponibilidad de base de datos (DAG) de la que se va a recopilar la métrica. Si se omite este parámetro, se usará el DAG del que es miembro el servidor local. Se pueden usar caracteres comodín para recopilar información y notificar sobre varios DAG.</p></td>
</tr>
<tr class="even">
<td><p><em>Database</em></p></td>
<td><p>Proporciona una lista de bases de datos para las que debe generarse el informe. Se admiten caracteres comodín, por ejemplo, <code>-Database:&quot;DB1&quot;,&quot;DB2&quot;</code> o <code>-Database:&quot;DB*&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>Especifica la duración del período de tiempo sobre el que se debe realizar el informe. El script solamente recopila los eventos registrados durante dicho período. Por consiguiente, es posible que el script recopile registros de operaciones parciales (por ejemplo, solamente el final de una operación al inicio del período, o viceversa). Si no se especifica ningún valor para <em>StartTime</em> ni <em>EndTime</em>, el script registrará de forma predeterminada las últimas 24 horas. Si solamente se especifica un parámetro, el período será de 24 horas y empezará o finalizará a la hora especificada.</p></td>
</tr>
<tr class="even">
<td><p><em>EndTime</em></p></td>
<td><p>Especifica la duración del período de tiempo sobre el que se debe realizar el informe. El script solamente recopila los eventos registrados durante dicho período. Por consiguiente, es posible que el script recopile registros de operaciones parciales (por ejemplo, solamente el final de una operación al inicio del período, o viceversa). Si no se especifica ningún valor para <em>StartTime</em> ni <em>EndTime</em>, el script registrará de forma predeterminada las últimas 24 horas. Si solamente se especifica un parámetro, el período será de 24 horas y empezará o finalizará a la hora especificada.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>Especifica la carpeta usada para almacenar los resultados de procesamiento de eventos. Si se omite este parámetro, se usará la carpeta Scripts. Si se especifica, el script selecciona una lista de archivos .csv generada mediante el script y los usa como datos de origen para generar un informe HTML de resumen. El informe es el mismo que se genera con la opción -GenerateHtmlReport. Los archivos pueden generarse en varios DAG a distintas horas, o incluso con horas que se solapen, y el script unificará todos los datos.</p></td>
</tr>
<tr class="even">
<td><p><em>GenerateHtmlReport</em></p></td>
<td><p>Especifica que el script recopile toda la información que ha registrado, agrupe los datos por tipo de operación y genere un archivo HTML que incluye estadísticas para cada uno de los grupos. El informe incluye el número total de operaciones de cada grupo, el número de operaciones que han dado error y estadísticas sobre el tiempo que se ha tardado en cada grupo. Asimismo, contiene un desglose de los distintos tipos de errores devueltos en las operaciones erróneas.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowHtmlReport</em></p></td>
<td><p>Especifica que el informe generado en HTML debe mostrarse en un explorador web una vez generado.</p></td>
</tr>
<tr class="even">
<td><p><em>SummariseCsvFiles</em></p></td>
<td><p>Especifica que el script lea los datos de los archivos .csv existentes que se hayan generado anteriormente mediante el script. A continuación, estos datos se usan para generar un informen de resumen similar al informe que genera el parámetro <em>GenerateHtmlReport</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ActionType</em></p></td>
<td><p>Especifica el tipo de acciones operativas que el script debe recopilar. Los valores de este parámetro son <code>Move</code>, <code>Mount</code>, <code>Dismount</code> y <code>Remount</code>. El valor <code>Move</code> hace referencia a cada vez que la base de datos cambia su servidor activo, ya sea mediante movimientos controlados o mediante conmutaciones por error. Los valores <code>Mount</code>, <code>Dismount</code> y <code>Remount</code> hacen referencia a las ocasiones en que la base de datos cambia su estado de montaje sin moverse a otro equipo.</p></td>
</tr>
<tr class="even">
<td><p><em>ActionTrigger</em></p></td>
<td><p>Especifica las operaciones administrativas que debe recopilar el script. Los valores de este parámetro son <code>Admin</code> o <code>Automatic</code>. Las acciones automáticas son aquéllas que realiza el sistema automáticamente (por ejemplo, una conmutación por error cuando un servidor se desconecta). Las acciones de administración son las acciones realizadas por un administrador mediante el Shell de administración de Exchange o el Centro de administración de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><em>RawOutput</em></p></td>
<td><p>Especifica que el script debe escribir los resultados que deberían haberse escrito en los archivos .csv directamente en el flujo de salida, como sucedería con write-output. A continuación, esta información puede transferirse a otros comandos.</p></td>
</tr>
<tr class="even">
<td><p><em>IncludedExtendedEvents</em></p></td>
<td><p>Especifica que el script debe recopilar los eventos que proporcionan datos de diagnóstico del tiempo tardado en montar las bases de datos. Esta fase puede llevar tiempo si el registro de eventos de la aplicación en los servidores es grande.</p></td>
</tr>
<tr class="odd">
<td><p><em>MergeCSVFiles</em></p></td>
<td><p>Especifica que el script debe tomar todos los archivos .csv que contengan datos sobre cada operación y unificarlos en un solo archivo .csv.</p></td>
</tr>
<tr class="even">
<td><p><em>ReportFilter</em></p></td>
<td><p>Especifica que se debe aplicar un filtro a las operaciones usando los campos tal y como aparecen en los archivos .csv. Este parámetro usa el mismo formato que una operación <code>Where</code>, con cada elemento definido en <code>$_</code> y que devuelve un valor booleano. Por ejemplo: <code>{$_DatabaseName -notlike &quot;Mailbox Database*&quot;}</code> puede usarse para excluir las bases de datos predeterminadas del informe.</p></td>
</tr>
</tbody>
</table>


## Ejemplos de CollectOverMetrics.ps1

En el ejemplo siguiente se recopila la métrica de todas las bases de datos que coinciden con DB\* (la búsqueda incluye un carácter comodín) en el grupo de disponibilidad de base de datos DAG1. Una vez recopilada la métrica, se genera y muestra un informe HTML.

```powershell
CollectOverMetrics.ps1 -DatabaseAvailabilityGroup DAG1 -Database:"DB*" -GenerateHTMLReport -ShowHTMLReport
```

En los ejemplos siguientes se describen distintos métodos para filtrar el informe HTML de resumen. En el primero se usa el parámetro *Database* que toma una lista de nombres de bases de datos. El informe de resumen solamente contiene datos sobre estas bases de datos. En los dos ejemplos siguientes se usa la opción *ReportFilter*. En el último ejemplo se filtran todas las bases de datos predeterminadas.

```powershell
CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -Database MailboxDatabase123,MailboxDatabase456
CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { $_.DatabaseName -notlike "Mailbox Database*" }
CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { ($_.ActiveOnStart -like "ServerXYZ*") -and ($_.ActiveOnEnd -notlike "ServerXYZ*") }
```

## Script de CollectReplicationMetrics.ps1

CollectReplicationMetrics.ps1 es otro script de métrica de estado incluido en Exchange 2013. Este script es un método activo de supervisión, porque recopila la métrica en tiempo real, mientras se ejecuta el script. CollectReplicationMetrics.ps1 recopila datos de contadores de rendimiento relacionados con la replicación de base de datos. El script reúne datos de varios servidores de buzones de correo, escribe los datos de cada servidor en un archivo .csv y, a continuación, realiza un informe con varias estadísticas sobre todos los datos (por ejemplo, la cantidad de tiempo durante el cual cada copia estuvo en estado de error o suspendida, la longitud media de cola de copia o de reproducción, o la cantidad de tiempo durante el cual las copias no han cumplido los criterios de conmutación por error).

Puede especificar los servidores individualmente o bien especificar DAG enteros. Puede ejecutar el script para primero recopilar los datos y, a continuación, generar el informe, o bien ejecutarlo para solo reunir los datos o solo generar el informe sobre los datos que ya se hayan recopilado. Puede especificar la frecuencia a la que debe realizarse el muestreo de los datos y la duración total para reunir los datos.

Los datos recopilados de cada servidor se escriben en un archivo llamado **CounterData.\<ServerName\>.\<TimeStamp\>.csv**. El informe de resumen se escribirá en un archivo denominado **HaReplPerfReport.\<DAGName\>.\<TimeStamp\>.csv** o **HaReplPerfReport.\<TimeStamp\>.csv** si no ejecutó el script con el parámetro *DagName*.

El script inicia trabajos de Windows PowerShell para recopilar los datos de cada servidor. Estos trabajos se ejecutan durante todo el período en que se recopilan los datos. Si especifica una gran cantidad de servidores, puede que este proceso use una cantidad de memoria considerable. La fase final del proceso, cuando los datos se procesan en un informe de resumen, también puede llevar bastante tiempo si se trata de grandes cantidades de datos. Es posible ejecutar la fase de recopilación en un equipo y, a continuación, copiar los datos en otro lugar para su procesamiento.

El script CollectReplicationMetrics.ps1 admite parámetros que permiten personalizar el comportamiento y los resultados del mismo. En la tabla siguiente se muestran los parámetros disponibles.

### Parámetros del script CollectReplicationMetrics.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>Especifica el nombre del grupo de disponibilidad de base de datos (DAG) de la que se va a recopilar la métrica. Si se omite este parámetro, se usará el DAG del que es miembro el servidor local.</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseNames</em></p></td>
<td><p>Proporciona una lista de bases de datos para las que debe generarse el informe. Se admiten caracteres comodín, por ejemplo, <code>-DatabaseNames:&quot;DB1&quot;,&quot;DB2&quot;</code> o <code>-DatabaseNames:&quot;DB*&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>Especifica la carpeta usada para almacenar los resultados de procesamiento de eventos. Si se omite este parámetro, se usará la carpeta Scripts.</p></td>
</tr>
<tr class="even">
<td><p><em>Duration</em></p></td>
<td><p>Especifica el tiempo que debe durar el proceso de recolección de datos. Los valores habituales son entre una y tres horas. Las duraciones más largas solamente deben usarse con intervalos largos entre cada ejemplo o una serie de trabajos más cortos realizados por tareas programadas.</p></td>
</tr>
<tr class="odd">
<td><p><em>Frequency</em></p></td>
<td><p>Especifica la frecuencia a la que debe recopilarse la métrica de datos. Los valores habituales son 30 segundos, un minuto o cinco minutos. Bajo circunstancias normales, los intervalos más breves no supondrán cambios significativos entre cada ejemplo.</p></td>
</tr>
<tr class="even">
<td><p><em>Servers</em></p></td>
<td><p>Especifica la identidad de los servidores de los que se deben recopilar estadísticas. Puede especificar cualquier valor, incluidos caracteres comodín o GUID.</p></td>
</tr>
<tr class="odd">
<td><p><em>SummariseFiles</em></p></td>
<td><p>Especifica una lista de archivos .csv para generar un informe de resumen. Estos archivos se llaman <strong>CounterData.&lt;CounterData&gt;*</strong> y se generan mediante el script CollectReplicationMetrics.ps1.</p></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>Especifica las fases de procesamiento que ejecuta el script. Puede usar los siguientes valores:</p>
<ul>
<li><p><code>CollectAndReport</code>   Éste es el valor predeterminado. Este valor significa que el script debe recopilar los datos de los servidores y, a continuación, procesarlos para generar el informa de resumen.</p></li>
<li><p><code>CollectOnly</code>   Este valor significa que el script solamente debe recopilar los datos, sin generar el informe.</p></li>
<li><p><code>ProcessOnly</code>   Este valor significa que el script debe importar los datos de un conjunto de archivos .csv y procesarlos para generar el informe de resumen. El parámetro <em>SummariseFiles</em> se usa para proporcionar al script una lista de archivos para procesar.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MoveFilestoArchive</em></p></td>
<td><p>Especifica que el script debe mover los archivos a una carpeta comprimida tras el procesamiento.</p></td>
</tr>
<tr class="even">
<td><p><em>LoadExchangeSnapin</em></p></td>
<td><p>Especifica que el script debe cargar los comandos del Shell. Este parámetro es útil cuando el script tiene que ejecutarse desde fuera del Shell, por ejemplo en una tarea programada.</p></td>
</tr>
</tbody>
</table>


## Ejemplo de CollectReplicationMetrics.ps1

En el ejemplo siguiente se reúnen los datos equivalentes a una hora de trabajo de todos los servidores que se encuentran en el DAG DAG1, con un muestreo basado en intervalos de un minuto y, a continuación, se genera un informe de resumen. Asimismo, se usa el parámetro *ReportPath*, que hace que el script coloque todos los archivos en el directorio actual.

```powershell
CollectReplicationMetrics.ps1 -DagName DAG1 -Duration "01:00:00" -Frequency "00:01:00" -ReportPath
```

En el ejemplo siguiente se leen los datos de todos los archivos que coincidan con CounterData\* y se genera un informe de resumen.

```powershell
CollectReplicationMetrics.ps1 -SummariseFiles (dir CounterData*) -Mode ProcessOnly -ReportPath
```

