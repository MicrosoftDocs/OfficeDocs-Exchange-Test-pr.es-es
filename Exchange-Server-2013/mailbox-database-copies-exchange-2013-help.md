---
title: 'Copias de bases de datos de buzones: Exchange 2013 Help'
TOCTitle: Copias de bases de datos de buzones
ms:assetid: ce748bca-3e24-493b-b9e6-153157bffd6a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd979802(v=EXCHG.150)
ms:contentKeyID: 48268678
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Copias de bases de datos de buzones

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Microsoft Exchange Server 2013 emplea el concepto de movilidad de base de datos, que es la conmutación por error en el nivel de la base de datos administrada por Exchange. La movilidad de base de datos desconecta las bases de datos de los servidores, agrega soporte para hasta 16 copias de una sola base de datos y ofrece una experiencia nativa para agregar copias de bases de datos a una base de datos.

## Características claves

Las características claves de las copias de base de datos de buzones de correo son las siguientes:

  - Se pueden crear hasta 16 copias de una base de datos de buzones de correo de Exchange 2013 en varios servidores de buzones de correo, siempre y cuando los servidores se encuentren agrupados en un grupo de disponibilidad de base de datos (DAG), que es un límite para la replicación continua. Las bases de datos de buzones de correo de Exchange 2013 sólo se pueden replicar en otros servidores de buzones de correo de Exchange 2013 dentro de un DAG. No es posible replicar una base de datos fuera de un DAG ni replicar una base de datos de buzones de correo de Exchange 2013 en un servidor que ejecute Exchange 2010 o versiones anteriores. Para obtener información detallada sobre los DAGS, consulte [Grupos de disponibilidad de base de datos (DAG)](database-availability-groups-dags-exchange-2013-help.md) .

  - Todos los servidores de buzones de correo de un DAG deben estar en el mismo dominio de Active Directory.

  - Las copias de bases de datos de buzones admiten los conceptos de tiempo de retardo de reproducción y tiempo de retardo de truncamiento. Se debe realizar una planificación adecuada antes de habilitar estas funciones.

  - Se puede realizar una copia de seguridad de todas las copias de base de datos mediante una aplicación de copia de seguridad basada en el Servicio de instantáneas de volumen (VSS) y admitida por Exchange.

  - Las copias de bases de datos sólo se pueden crear en servidores de buzones de correo que no hospeden la copia activa de una base de datos. No se pueden crear dos copias de la misma base de datos en el mismo servidor.

  - Todas las copias de una base de datos utilizan la misma ruta en cada servidor que contiene una copia. Las rutas de base de datos y archivo de registros de una copia de base de datos en cada servidor de buzones de correo no deben entrar en conflicto con otras rutas de bases de datos.

  - Se pueden crear copias de bases de datos en el mismo sitio de Active Directory u otro distinto, y en la misma subred de red u otra distinta.

  - No se admiten copias de bases de datos entre servidores de buzones de correo con una latencia de red de ida y vuelta superior a 500 milisegundos (ms).

## Copias de bases de datos de buzones

Se puede crear una copia de base de datos de buzones de correo en cualquier momento. Las copias de bases de datos de buzones de correo se pueden distribuir en todos los servidores de buzones de correo de forma flexible y pormenorizada.

Se puede crear una copia de base de datos de buzones mediante el Asistente **para agregar copias de bases de datos de buzones** en el Centro de Administración de Exchange o mediante el cmdlet **Add-MailboxDatabaseCopy** en el Shell de administración de Exchange.

Al crear una copia de base de datos de buzones de correo, especifique los parámetros siguientes:

  - *Identity*   Este parámetro especifica el nombre de la base de datos de buzones que se está copiando. Los nombres de las base de datos deben ser únicos dentro de la organización de Exchange.

  - *MailboxServer*   Este parámetro especifica el nombre del servidor Buzón de correo que admitirá la copia de la base de datos. Dicho servidor debe pertenecer al mismo DAG y no hospedar ya una copia de la base de datos.

También puede especificar:

  - *ActivationPreference*    Este parámetro especifica el número de preferencia de activación, que se usa como parte del proceso de selección de la mejor copia de Active Manager. También se emplea para redistribuir bases de datos de buzones activas en todo el DAG cuando se usa el script RedistributeActiveDatabases.ps1. El valor para la preferencia de activación es un número igual o superior a 1, donde 1 está al principio de la orden de preferencia. El número de posición no puede ser mayor que el número de copias de la base de datos de buzones.

  - *ReplayLagTime *  Este parámetro especifica la cantidad de tiempo que el servicio de replicación de Microsoft Exchange debe esperar antes de reproducir los archivos de registro que se copiaron en la copia de la base de datos. El formato de este parámetro es (días.horas:minutos:segundos). El ajuste predeterminado para este valor es 0 segundos. El ajuste máximo permitido para este valor es 14 días. El valor mínimo permitido es 0 segundos. Si se establece el valor del tiempo de retardo de reproducción en 0, el retraso de reproducción del registro queda desactivado.

  - *TruncationLagTime*    Este parámetro especifica la cantidad de tiempo que el servicio de replicación de Microsoft Exchange debe esperar antes de truncar los archivos de registro que se han reproducido en una copia de la base de datos. El intervalo de tiempo empieza una vez que el registro se ha reproducido correctamente en la copia de la base de datos. El formato de este parámetro es (días.horas:minutos:segundos). El ajuste predeterminado para este valor es 0 segundos. El ajuste máximo permitido para este valor es 14 días. El valor mínimo permitido es 0 segundos. Si se establece el valor del tiempo de retardo de truncamiento en 0, el retraso de truncamiento del registro queda desactivado.

  - *SeedingPostponed*    Este parámetro especifica que la tarea no debería inicializar la copia de la base de datos en el servidor Buzón de correo indicado. Esta opción suele usarse al intentar inicializar una nueva copia de la base de datos a partir de una copia pasiva de dicha base de datos (por ejemplo, agregando una segunda copia de una determinada base de datos a una ubicación remota). Al usar este parámetro, la copia de la base de datos debe inicializarse manualmente mediante el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)).

Para obtener más información sobre la creación, el uso y la administración de copias de bases de datos de buzones de correo, consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

