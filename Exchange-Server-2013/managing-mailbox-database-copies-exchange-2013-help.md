---
title: 'Administración de copias de bases de datos de buzones de correo: Exchange 2013 Help'
TOCTitle: Administración de copias de bases de datos de buzones de correo
ms:assetid: 28cedf1d-365a-4e36-b2ba-6bf81af8684f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335158(v=EXCHG.150)
ms:contentKeyID: 48267922
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administración de copias de bases de datos de buzones de correo

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-08-26_

Una vez que un grupo de disponibilidad de base de datos (DAG) se ha creado, configurado y completado con miembros del servidor de buzones de correo, puede usar el Centro de administración de Exchange (EAC) o el Shell de administración de Exchange para agregar copias de la base de datos de buzones de correo de manera flexible y granular.

## Administración de copias de bases de datos

Después de que se crean varias copias de una base de datos, puede usar el EAC y el Shell para supervisar el estado de cada copia y para realizar otras tareas de administración asociadas con las copias de bases de datos. Algunas de las tareas de administración que puede necesitar realizar incluyen la suspensión o reanudación de una copia de base de datos, la inicialización de una copia de base de datos, la supervisión de copias de base de datos, la configuración de copias de base de datos y la eliminación de una copia de base de datos.

## Suspensión y reanudación de las copias de base de datos

Por diversos motivos, como la realización de un mantenimiento planeado, puede ser necesario suspender y reanudar la actividad de replicación continua de una copia de base de datos. Además, algunas tareas de administración, como la inicialización, requieren que, primero, se suspenda la copia de base de datos. Recomendamos la suspensión de toda actividad de replicación cuando se cambia la ruta para la base de datos o los archivos de registro. Puede suspender y reanudar la actividad de una copia de base de datos mediante el uso del EAC o mediante la ejecución de los cmdlets **Suspend-MailboxDatabaseCopy** y **Resume-MailboxDatabaseCopy** en el Shell. Para obtener instrucciones detalladas acerca de cómo suspender o reanudar la actividad de replicación continua de una copia de base de datos, vea [Suspensión o reanudación de una copia de base de datos de buzones](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md).

## Inicialización de una copia de base de datos

La *inicialización*, también conocida como *actualización*, es el proceso en el que una base de datos, ya sea una base de datos en blanco o una copia de la base de datos de producción, se agrega a la ubicación de la copia de destino en otro servidor de buzones de correo en el mismo DAG que la base de datos activa. Ésta se convierte en la base de datos de base para la copia mantenida por ese servidor.

En función de la situación, la inicialización puede ser un proceso automático o manual que debe iniciar el usuario. Cuando se agrega una copia de base de datos, la copia se inicializa automáticamente, siempre que el servidor de destino y su almacenamiento estén configurados correctamente. Si desea inicializar una copia de base de datos de forma manual y no desea que la inicialización se produzca automáticamente al crear la copia, puede usar el parámetro *SeedingPostponed* al ejecutar el cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298105\(v=exchg.150\)).

Prácticamente no es necesario reinicializar las copias de base de datos después de que se ha producido la inicialización inicial. Pero si es necesario reinicializar o si desea inicializar manualmente una copia de base de datos en lugar de que el sistema inicialice la copia automáticamente, estas tareas se pueden realizar con el Asistente de la copia de base de datos de buzones de correo en el EAC o con el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)) del Shell. Antes de inicializar una copia de base de datos, primero, debe suspender la copia de base de datos de buzones de correo. Para obtener instrucciones detalladas acerca de cómo reinicializar una copia de la base de datos, vea [Actualización de una copia de la base de datos de buzones](update-a-mailbox-database-copy-exchange-2013-help.md).

Después de que finaliza una operación de inicialización manual, la replicación de la copia de base de datos de buzones de correo inicializada se reanuda automáticamente. Si no desea que la replicación se reanude automáticamente, puede usar el parámetro *ManualResume* al ejecutar el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)).

## Selección de elementos para inicializar

Al realizar una operación de inicialización, puede elegir inicializar la copia de base de datos de buzones de correo, el catálogo del índice de contenido para la copia de base de datos de buzones de correo o la copia de base de datos y la copia del catálogo del índice de contenido.

El comportamiento predeterminado del Asistente para actualizar copias de bases de datos de buzones de correo y el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)) es inicializar la copia de base de datos de buzones de correo y la copia del catálogo del índice de contenido. Para inicializar solamente la copia de base de datos de buzones de correo sin inicializar el catálogo del índice de contenido, use el parámetro *DatabaseOnly* al ejecutar el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)). Para inicializar solamente la copia del catálogo del índice de contenido, use el parámetro *CatalogOnly* al ejecutar el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)).

## Selección del origen de inicialización

Cualquier copia de base de datos en buen estado puede usarse como origen de inicialización para una copia adicional de esa base de datos. Esto es especialmente útil cuando tiene un DAG que se ha extendido en varias ubicaciones físicas. Por ejemplo, considere una implementación de DAG de cuatro miembros, en donde dos miembros (MBX1 y MBX2) están ubicados en Portland, Oregón, y dos miembros (MBX3 y MBX4) están en Nueva York, Nueva York. Una base de datos de buzones de correo denominada DB1 está activa en MBX1, y hay copias pasivas de DB1 en MBX2 y MBX3. Al agregar una copia de DB1 a MBX4, tiene la opción de usar una copia en MBX3 como origen de inicialización. Al hacerlo, evita inicializar sobre un vínculo de Red de área extensa (WAN) entre Portland y Nueva York.

Para usar una copia específica como origen de inicialización al agregar una nueva copia de base de datos, haga lo siguiente:

  - Use el parámetro *SeedingPostponed* al ejecutar el cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298105\(v=exchg.150\)) para agregar la copia de base de datos. Si no se usa el parámetro *SeedingPostponed*, la copia de base de datos se inicializará explícitamente usando la copia activa de la base de datos como origen.

  - Puede especificar el servidor de origen que desea usar como parte de la actualización del Asistente de la copia de la base de datos de buzones de correo en el EAC o puede usar el parámetro *SourceServer* al ejecutar el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)) para especificar el servidor de origen de inicialización deseado. En el ejemplo anterior, se especificaría MBX3 como el servidor de origen. Si no se usa el parámetro *SourceServer*, la copia de base de datos se inicializará explícitamente desde la copia activa de la base de datos.

## Inicialización y redes

Además de seleccionar un servidor de origen específico para inicializar una copia de base de datos de buzones de correo, también puede usar el Shell para especificar qué redes del DAG usar y, opcionalmente, puede anular la configuración de cifrado y compresión de la red del DAG durante la operación de inicialización.


> [!NOTE]
> La propagación del catálogo de índice de contenido solo es posible a través de una red MAPI. Esto ocurre aunque use el parámetro <CODE>-Network</CODE> en el cmdlet Update-MailboxDatabaseCopy.



Para especificar las redes que desea usar para la inicialización, use el parámetro *Network* al ejecutar el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)) y especifique las redes del DAG que desea usar. Si no usa el parámetro *Network*, el sistema usa el siguiente comportamiento predeterminado para seleccionar una red que usará en la operación de inicialización:

  - Si el servidor de origen y el servidor de destino están en la misma subred, y se ha configurado una red de replicación que incluye una subred, se usa la red de replicación.

  - Si el servidor de origen y el servidor de destino están en distintas subredes, incluso si se ha configurado una red de replicación que contiene esas subredes, se usa la red de cliente (MAPI) para la inicialización.

  - Si el servidor de origen y el servidor de destino están en distintos centros de datos, se usa la red de cliente (MAPI) para inicialización.

En el DAG, las redes del DAG están configuradas para cifrado y compresión. La configuración predeterminada establece el uso de cifrado y compresión solamente para comunicaciones en diferentes subredes. Si el servidor de origen y el servidor de destino están en distintas subredes, y el DAG está configurado con los valores predeterminados para *NetworkCompression* y *NetworkEncryption*, puede anular estos valores con los parámetros *NetworkCompressionOverride* y *NetworkEncryptionOverride*, respectivamente, al ejecutar el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)).

## Proceso de inicialización

Cuando inicia un proceso de inicialización con los cmdlets [Add-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298105\(v=exchg.150\)) o [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)), se realizan las siguientes tareas:

1.  Las propiedades de base de datos de Active Directory se leen para validar las bases de datos y los servidores especificados, y para comprobar que los servidores de origen y de destino estén ejecutando Exchange 2013, que ambos sean miembros del mismo DAG y que la base de datos especificada no sea una base de datos de recuperación. Las rutas de acceso al archivo de base de datos también se leen.

2.  Los preparativos para las comprobaciones de reinicialización ocurren desde el servicio de replicación de Microsoft Exchange en el servidor de destino.

3.  El servicio de replicación de Microsoft Exchange en el servidor de destino comprueba la presencia de archivos de base de datos y de registro de transacciones en los directorios de archivos leídos por las comprobaciones de Active Directory en el paso 1.

4.  El servicio de replicación de Microsoft Exchange devuelve la información de estado del servidor de destino a la interfaz administrativa desde donde se ejecutó el cmdlet.

5.  Si todas las comprobaciones preliminares se han realizado, se le pide que confirme la operación antes de continuar. Si confirma la operación, el proceso continúa. Si se detecta un error durante las comprobaciones preliminares, el error se informa y la operación falla.

6.  La operación de inicialización se inicia desde el servicio de replicación de Microsoft Exchange en el servidor de destino.

7.  El servicio de replicación de Microsoft Exchange suspende la replicación de la base de datos para la copia activa de la base de datos.

8.  El servicio de replicación de Microsoft Exchange actualiza la información de estado de la base de datos para reflejar el estado de la inicialización.

9.  Si el servidor de destino aún no tiene los directorios para los archivos de registro y de la base de datos de destino, se crean.

10. Una solicitud para inicializar la base de datos se transmite del servicio de replicación de Microsoft Exchange en el servidor de destino al servicio de replicación de Microsoft Exchange en el servidor de origen mediante el TCP. Esta solicitud y las comunicaciones posteriores para inicializar la base de datos se producen en una red del DAG que ha sido configurada como una red de replicación.

11. El servicio de replicación de Microsoft Exchange en el servidor de origen inicia una copia de seguridad por secuencias del Motor de almacenamiento extensible (ESE) a través de la interfaz del servicio Almacén de información de Microsoft Exchange.

12. El servicio Almacén de información de Microsoft Exchange transmite los datos de la base de datos al servicio de replicación de Microsoft Exchange.

13. Los datos de la base de datos se mueven del servicio de replicación de Microsoft Exchange del servidor de origen al servicio de replicación de Microsoft Exchange del servidor de destino.

14. El servicio de replicación de Microsoft Exchange en el servidor de destino escribe la copia de la base de datos en un directorio temporal ubicado en el directorio de la base de datos principal denominado *temp-seeding*.

15. La operación de copia de seguridad por secuencias en el servidor de origen termina cuando se llega al final de la base de datos.

16. Se completa la operación de escritura en el servidor de destino y se mueve la base de datos del directorio temp-seeding a la ubicación final. Se elimina el directorio temp-seeding.

17. En el servidor de destino, el servicio de replicación de Microsoft Exchange envía mediante el proxy una solicitud al servicio de búsqueda de Microsoft Exchange para montar el catálogo del índice de contenido para la copia de la base datos, si existe. Si hay archivos de catálogo existentes no actualizados de una instancia previa de la copia de la base de datos, la operación de montaje falla y genera la necesidad de replicar el catálogo del servidor de origen. Del mismo modo, si el catálogo no existe en una nueva instancia de la copia de la base de datos en el servidor de destino, se requiere una copia del catálogo. El servicio de replicación de Microsoft Exchange indica al servicio de búsqueda de Microsoft Exchange que suspenda la indización de la copia de la base de datos mientras se copia un nuevo catálogo del servidor de origen.

18. El servicio de replicación de Microsoft Exchange en el servidor de destino envía una solicitud de catálogo de inicialización al servicio de replicación de Microsoft Exchange en el servidor de origen.

19. En el servidor de origen, el servicio de replicación de Microsoft Exchange solicita la información del directorio del servicio de búsqueda de Microsoft Exchange y solicita que se suspenda la indización.

20. El servicio de búsqueda de Microsoft Exchange en el servidor de origen devuelve la información del directorio del catálogo de búsqueda al servicio de replicación de Microsoft Exchange.

21. El servicio de replicación de Microsoft Exchange en el servidor de origen lee los archivos de catálogo del directorio.

22. El servicio de replicación de Microsoft Exchange en el servidor de origen mueve los datos del catálogo al servicio de replicación de Microsoft Exchange en el servidor de destino mediante una conexión en la red de replicación. Después de que finaliza la lectura, el servicio de replicación de Microsoft Exchange envía una solicitud al servicio de búsqueda de Microsoft Exchange para reanudar la indización de la base de datos del servidor de origen.

23. Si hay archivos de catálogo en el servidor de destino, en el directorio, el servicio de replicación de Microsoft Exchange en el servidor de destino los elimina.

24. El servicio de replicación de Microsoft Exchange en el servidor de destino escribe los datos del catálogo en un directorio temporal denominado *CiSeed.Temp* hasta que los datos se transfieran completamente.

25. El servicio de replicación de Microsoft Exchange mueve todos los datos del catálogo a la ubicación final.

26. El servicio de replicación de Microsoft Exchange en el servidor de destino reanuda la indización de búsqueda en la base de datos de destino.

27. El servicio de replicación de Microsoft Exchange en el servidor de destino devuelve un estado de finalización.

28. El resultado final de esta operación se transmite a la interfaz administrativa desde donde se llamó el cmdlet.

## Configuración de las copias de bases de datos

Después de que se cree una copia de base de datos, podrá ver y modificar la configuración cuando sea necesario. Puede ver la información de la configuración si examina la página **Propiedades** de una copia de base de datos en el EAC. También puede usar los cmdlets [Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\)) y [Set-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298104\(v=exchg.150\)) en el Shell para ver y establecer la configuración de copias de bases de datos, como el tiempo de retardo de reproducción, el tiempo de retardo de truncamiento y el orden de preferencia de activación. Para obtener instrucciones detalladas acerca de cómo ver y establecer la configuración de copias de bases de datos, vea [Configuración de las propiedades de una copia de base de datos de buzones](configure-mailbox-database-copy-properties-exchange-2013-help.md).

## Usar las opciones de tiempo de retardo de reproducción y tiempo de retardo de truncamiento

Las copias de bases de datos de buzones de correo admiten el uso de un *tiempo de retardo de reproducción* y un *tiempo de retardo de truncamiento*, ambos configurados en minutos. La configuración de un tiempo de retardo de reproducción le permite volver a llevar una copia de base de datos a un momento específico. La configuración de un tiempo de retardo de truncamiento le permite usar los registros en una copia de base de datos pasiva para recuperarse de la pérdida de archivos de registro en una copia de base de datos activa. Dado que estas dos características provocarán la acumulación temporaria de archivos de registro, usar cualquiera de ellas afectará su diseño de almacenamiento.

## Tiempo de retardo de reproducción

El tiempo de retardo de reproducción es una propiedad de una copia de base de datos de buzones de correo que especifica la cantidad de tiempo, en minutos, de retardo de reproducción del registro de la copia de base de datos. El temporizador de retardo de reproducción se inicia cuando un archivo de registro ha sido replicado en la copia pasiva y ha pasado correctamente la inspección. Mediante el retardo de la reproducción de archivos de la copia de base de datos, usted tiene la posibilidad de recuperar la base de datos en un momento específico anterior. Una copia de base de datos de buzones de correo configurada con un valor de tiempo de retardo de reproducción mayor que 0 se denomina *copia de base de datos de buzones de correo atrasada* o simplemente *copia atrasada*.

Una estrategia que usa las funciones de espera de litigio y de copias de base de datos de Exchange 2013 puede proporcionar protección contra diversos errores que, normalmente, podrían generar la pérdida de datos. Sin embargo, estas funciones no pueden brindar protección contra la pérdida de datos en caso de daños de lógica, que si bien no son muy comunes, pueden generar la pérdida de datos. Las copias retrasadas están diseñadas para prevenir la pérdida de datos en caso de daños de lógica. Generalmente, hay dos tipos de daños de lógica:

  - **Daños de lógica de una base de datos**   La suma de comprobación de las páginas de base de datos coincide, pero los datos de las páginas son lógicamente incorrectos. Esto se puede producir cuando ESE intenta escribir una página de la base de datos y, aunque el sistema operativo muestra un mensaje de operación correcta, los datos nunca se escribieron en el disco o se escribieron en el lugar incorrecto. Esto se conoce como *vaciado perdido*. Para impedir que los vaciados perdidos pierdan datos, ESE incluye un mecanismo de detección de vaciados perdidos en la base de datos junto con una función de revisión de páginas (restauración de página única).

  - **Daños de lógica del almacén**   Se agregan, eliminan o manipulan datos de una manera en la que el usuario no espera. Normalmente, estos casos son causados por aplicaciones de otros fabricantes. Solo se considera un daño, por lo general, porque el usuario lo ve como un daño. El almacén de Exchange considera que la transacción que produce los daños de lógica es una serie de operaciones MAPI válidas. La función Retención por juicio en Exchange 2013 brinda protección contra la corrupción lógica del almacenamiento (ya que evita que el contenido sea eliminado de manera permanente por un usuario o una aplicación). Sin embargo, pueden darse varias situaciones en las que un buzón de correo se corrompa de tal manera que sería más fácil restaurar la base de datos a un punto en el tiempo anterior al momento de la corrupción y luego exportar el buzón de datos del usuario para recuperar los datos que no se corrompieron.

La combinación de copias de bases de datos, directiva de retención y restauración de página única ESE solo deja lugar para el caso, poco común pero catastrófico, de daños de lógica del almacén. Su decisión acerca de usar una copia de base de datos con un retraso de reproducción (una copia retrasada) dependerá de las aplicaciones de otros fabricantes que use y del historial de daños de lógica del almacén de su organización.

Las copias retrasadas se pueden administrar a sí mismas en Exchange 2013 mediante la invocación de la reproducción automática del registro para que reproduzca los archivos de registro en ciertos escenarios:

  - Cuando se alcance un umbral de espacio en disco insuficiente

  - Cuando la copia retrasada tiene un daño físico y se debe revisar por páginas

  - Cuando hay menos de tres copias correctas disponibles (activas o pasivas; las copias de bases de datos retrasadas no cuentan) durante más de 24 horas

La aplicación de revisión de páginas está disponible para las copias retrasadas a través de esta característica de reproducción automática. Si el sistema detecta que la aplicación de revisiones de páginas es necesaria para una copia retrasada, los registros se vuelven a reproducir automáticamente en la copia retrasada al realizar la aplicación de revisión de páginas. Las copias retrasadas también invocan esta característica de reproducción automática cuando se alcanza un umbral de espacio de disco bajo y cuando la copia retrasada se detecta como la única copia disponible durante un período específico.

El comportamiento de reproducción de copias retrasadas está deshabilitado de manera predeterminada, pero se puede habilitar mediante la ejecución del siguiente comando.

    Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true

Después de su habilitación, la reproducción ocurre cuando hay menos de tres copias. Puede cambiar el valor predeterminado de 3 modificando el siguiente valor DWORD del Registro.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

Para habilitar la reproducción cuando el espacio en disco insuficiente, debe configurar la siguiente entrada del Registro.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

Después de configurar cualquiera de estas opciones del Registro, reinicie el servicio de administración de Microsoft Exchange DAG para que los cambios surtan efecto.

Como ejemplo, considere un entorno donde una base de datos tiene 4 copias (3 copias de alta disponibilidad y 1 copia retrasada) y se utiliza el valor predeterminado de ReplayLagManagerNumAvailableCopies. Si una copia no retrasada está fuera de servicio por cualquier motivo (por ejemplo, se ha suspendido), la copia retrasada reproducirá automáticamente sus archivos de registro en 24 horas.

Si decide usar copias retrasadas sin habilitar el parámetro `ReplayLagManagerEnabled`, debe tener en cuenta las siguientes repercusiones:

  - El tiempo de retardo de reproducción es un valor configurado por el administrador y, de manera predeterminada, está deshabilitado.

  - La configuración de tiempo de retardo de reproducción tiene una configuración predeterminada de 0 días y una configuración máxima de 14 días.

  - Las copias retrasadas no se consideran copias de alta disponibilidad. En cambio, están diseñadas para la recuperación ante desastres, con el fin de brindar protección contra los daños de lógica del almacén.

  - Cuanto mayor sea el tiempo de retardo de reproducción, más largo será el proceso de recuperación de base de datos. La cantidad de horas que llevará recuperar una base de datos dependerá de la cantidad de archivos de registro que es necesario reproducir durante la recuperación y la velocidad en la que el hardware puede reproducirlos.

  - Le recomendamos que determine si las copias retrasadas son cruciales para su estrategia general de recuperación ante desastres. Si su uso es crucial para la estrategia, le recomendamos usar varias copias retrasadas o una matriz redundante de discos independientes (RAID) para proteger una sola copia retrasada, si no tiene varias copias retrasadas. Si pierde un disco o si se producen daños, no pierde su copia retrasada tal como estaba en un momento específico anterior al momento en que se produjeron los daños.

  - Las copias retrasadas no se pueden revisar con la función de restauración de página única ESE. Si una copia retrasada detecta daños en las páginas de la base de datos (por ejemplo, un error -1018), tendrá que reinicializarse (que perderá el aspecto retrasado de la copia).

Activar y recuperar una copia de la base de datos de buzones de correo retrasada es un proceso sencillo si desea que la base de datos reproduzca todos los archivos de registro y actualice la copia de la base de datos. Si desea reproducir los archivos de registro hasta un momento dado, la operación es un poco más difícil porque debe manipular los archivos de registro de forma manual y ejecutar la utilidad de base de datos de Exchange Server (Eseutil.exe) .

Para obtener más información sobre cómo activar una copia de base de datos de buzones de correo retrasada, vea [Activación de una copia de base de datos de buzones atrasada](activate-a-lagged-mailbox-database-copy-exchange-2013-help.md).

## Tiempo de retardo de truncamiento

El tiempo de retardo de truncamiento es una propiedad de una copia de base de datos de buzones de correo que especifica la cantidad de tiempo, en minutos, que se demora la eliminación del registro para la copia de base de datos después de que el archivo de registro se ha reproducido en la copia de base de datos. El temporizador de retardo de truncamiento se inicia cuando un archivo de registro se ha replicado en la copia pasiva, ha pasado correctamente la inspección y se ha reproducido correctamente en la copia de la base de datos. Mediante el retardo del truncamiento de los archivos de registro de la copia de base de datos, usted tiene la posibilidad de recuperarse de errores que afectan los archivos de registro para la copia activa de la base de datos.

## Copias de base de datos y truncamiento de registros

El truncamiento de registros funciona en Exchange 2013 de la misma manera que lo hizo en Exchange 2010. El comportamiento de truncamiento está determinado por la configuración del tiempo de retardo de reproducción y del tiempo de retardo de truncamiento para la copia.

Para que un archivo de registro de una copia de base de datos se trunque cuando la configuración de retardo se deja en los valores predeterminados de 0 (deshabilitado), es necesario que se cumplan los siguientes criterios:

  - Es necesario que se haya realizado correctamente una copia de seguridad del archivo de registro o que esté habilitado el registro circular.

  - El archivo de registro debe estar por debajo del punto de control (el archivo de registro mínimo necesario para la recuperación) para la base de datos.

  - Todas las otras copias retrasadas deben haber inspeccionado el archivo de registro.

  - Todas las otras copias (copias no retrasadas) deben haber reproducido el archivo de registro.

Para que se produzca el truncamiento de una copia retrasada de base de datos es necesario que se cumplan los siguientes criterios:

  - El archivo de registro debe estar por debajo del punto de control para la base de datos.

  - El archivo de registro debe ser anterior a ReplayLagTime + TruncationLagTime.

  - El archivo de registro se debe haber truncado en la copia activa.

En Exchange 2013, el truncamiento del registro no se produce en una copia de base de datos de buzones de correo activa cuando se suspenden una o más copias pasivas. Si las actividades de mantenimiento planeado llevarán un período prolongado (por ejemplo, varios días), puede ser que tenga una gran acumulación de archivos de registro. Para evitar que la unidad del registro se llene con registros de transacciones, puede quitar la copia de base de datos pasiva afectada en lugar de suspenderla. Cuando finaliza el mantenimiento planeado, puede volver a agregar la copia de base de datos pasiva.

Exchange 2013 Service Pack 1 (SP1) presenta una nueva característica denominada *truncamiento suelto*, que está deshabilitada de manera predeterminada. Durante las operaciones normales, cada copia de la base de datos mantiene los registros que deben enviarse a otras copias de la base de datos hasta que todas las copias de una base de datos confirmen que han reproducido (copias pasivas) o recibido (copias retrasadas) los archivos de registro. Se trata del comportamiento de truncamiento de registro predeterminado. Si una copia de la base de datos se desconecta por algún motivo, los archivos de registro comienzan a acumularse en los discos usados por las otras copias de la base de datos. Si la copia de la base de datos permanece sin conexión durante un período prolongado, esto puede causar que las otras copias de la base de datos se queden sin espacio en disco.

Cuando está habilitado el truncamiento suelto, el comportamiento del truncamiento es diferente. Cada copia de la base de datos realiza un seguimiento de su propio espacio libre en disco y aplica el comportamiento de truncamiento suelto si queda poco espacio libre. Para la copia activa, se pasa por alto la copia atrasada más antigua (la copia pasiva de base de datos que se encuentra más atrás en la reproducción del registro) y el truncamiento respeta las copias pasivas más antiguas restantes. La copia de base de datos activa es donde se calcula el truncamiento global. Las copias pasivas intentarán respetar la decisión de truncamiento tomada en la copia activa. A pesar de la implicación del nombre, MinCopiesToProtect, Exchange solo pasará por alto la copia atrasada más antigua conocida en el momento en que se ejecuta el truncamiento. En el caso de una copia pasiva, si el espacio se empieza a agotar, truncará sus archivos de registro de forma independiente usando los parámetros configurados que se describen a continuación.

Cuando la base de datos sin conexión vuelve a estar en línea, le faltarán archivos de registro que se habían eliminado de las otras copias en buen estado, y el estado de la copia de la base de datos será FailedAndSuspended. En este caso, si se ha configurado Reinicialización automática, la copia afectada se reiniciará automáticamente. Si no se ha configurado Reinicialización automática, un administrador deberá reiniciar manualmente la copia de la base de datos.

El número necesario de copias en buen estado, el umbral de espacio disponible en disco y el número de registros que se mantienen son parámetros que se pueden configurar. De forma predeterminada, el umbral de espacio libre en disco es de 204.800 MB (200 GB), y el número de registros para guardar es de 100.000 (100 GB) para las copias pasivas, y de 10.000 (10 GB) para las copias activas.

Para habilitar el truncamiento suelto y configurar sus parámetros, es necesario editar el Registro de Windows en cada miembro del DAG. Hay tres valores del Registro que se pueden configurar y que se almacenan en HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\BackupInformation. Los siguientes valores DWORD de la clave BackupInformation no existen de forma predeterminada y deben crearse manualmente. Los valores DWORD del Registro en BackupInformation se describen en la tabla siguiente:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor de Registro</th>
<th>Descripción</th>
<th>Valor predeterminado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LooseTruncation_MinCopiesToProtect</p></td>
<td><p>Esta clave se utiliza para habilitar el truncamiento suelto. Representa el número de copias pasivas para proteger del truncamiento suelto en la copia activa de una base de datos. Si establece el valor de esta clave en 0, se deshabilita el truncamiento suelto.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p>LooseTruncation_MinDiskFreeSpaceThresholdInMB</p></td>
<td><p>Umbral de espacio disponible en disco (en MB) para la activación del truncamiento suelto. Si el espacio disponible en disco cae por debajo de este valor, se activa el truncamiento suelto.</p></td>
<td><p>Si este valor del Registro no está configurado, el valor predeterminado que usa el truncamiento suelto es 200 GB.</p></td>
</tr>
<tr class="odd">
<td><p>LooseTruncation_MinLogsToProtect</p></td>
<td><p>El número mínimo de archivos de registro que se conservarán en las copias en buen estado cuyos registros se van a truncar. Si este valor del Registro está configurado, se aplican los valores configurados tanto a las copias activas como pasivas.</p></td>
<td><p>Si este valor del Registro no está configurado, se usan los valores predeterminados de 100.000 para las copias pasivas de base de datos y 10.000 para las copias activas de base de datos.</p></td>
</tr>
</tbody>
</table>


Cuando se usa el valor del Registro LooseTruncation\_MinLogsToProtect, tenga en cuenta que el comportamiento es diferente para las copias de base de datos activas y pasivas. En la copia activa de base de datos, este es el número de los registros adicionales que se conservan anteriores a los que las copias pasivas protegidas necesitan y al intervalo de copia activa requerido. En una copia pasiva de base de datos, es el número de registros que se mantiene a partir del último registro disponible. Una décima parte de este número también se usa para mantener los registros anteriores al intervalo requerido de esta copia pasiva. Los dos límites se usan para garantizar que copias de base de datos atrasadas no ocupen demasiado espacio, porque su intervalo suele ser muy grande.

## Directiva de activación de base de datos

Existen situaciones en las que es probable que desee crear una copia de base de datos de buzones de correo e impedir que el sistema active automáticamente esa copia en caso de error, por ejemplo:

  - Si implementa una o más copias de la base de datos del buzón de correo en un centro de datos en espera o alternativo.

  - Si configura una copia retrasada de la base de datos para propósitos de recuperación.

  - Si realiza el mantenimiento o la actualización de un servidor.

En cada una de las situaciones anteriores, usted tiene copias de base de datos que no desea que el sistema active automáticamente. Para impedir que el sistema active automáticamente una copia de base de datos de buzones de correo, puede configurar la copia para que quede bloqueada (suspendida) para activarse. Esto permite al sistema mantener la vigencia de la base de datos mediante el envío y la reproducción de registros, pero impide que el sistema se active automáticamente y use la copia. Un administrador debe activar manualmente las copias bloqueadas para la activación. Puede configurar la directiva de activación de la base de datos para un servidor entero con el cmdlet [Set-MailboxServer](https://technet.microsoft.com/es-es/library/aa998651\(v=exchg.150\)) o para una base de datos individual con el cmdlet [Set-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298104\(v=exchg.150\)) a fin de configurar el parámetro *DatabaseCopyAutoActivationPolicy* en Bloqueado.

Para obtener más información acerca de cómo configurar la directiva de activación de base de datos, vea [Configurar la directiva de activación para una copia de base de datos de buzones](configure-activation-policy-for-a-mailbox-database-copy-exchange-2013-help.md).

## Efecto de movimientos del buzón de correo sobre la replicación continua

En una base de datos de buzones de correo muy ocupada, con un índice de generación de registros muy alto, hay más probabilidades de pérdida de datos si la replicación en las copias pasivas de la base de datos no puede mantener el nivel de la generación de registros. Una situación que puede provocar un índice de generación de registros muy alto es el movimiento del buzón de correo. Exchange 2013 incluye la API de garantía de datos que es usada por servicios como el Servicio de replicación de buzones (MRS) de Microsoft Exchange para verificar el estado de la arquitectura de la copia de la base de datos según el valor de un parámetro *DataMoveReplicationConstraint* que envió el sistema o un administrador. Específicamente, la API de garantía de datos puede utilizarse para:

  - **Verificar el estado de la replicación**   Confirma que está disponible la cantidad de copias de la base de datos que era un requisito previo.

  - **Verificar el vaciado de la replicación**   Confirma que los archivos de registro requeridos se han reproducido contra la cantidad de copias de la base de datos que era un requisito previo.

Al ejecutarla, la API regresa la siguiente información de estado a la aplicación de llamada:

  - **Reintentar**   Significa que existen errores transitorios que evitan que se coteje la condición con la base de datos.

  - **Cumplido**   Significa que la base de datos cumple las condiciones requeridas o que la base de datos no ha sido replicada.

  - **No cumplido** Significa que la base de datos no cumple las condiciones requeridas. Además, se brinda información a la aplicación de llamada con respecto al motivo por el cual se suministró la respuesta **No cumplido**.

El valor del parámetro *DataMoveReplicationConstraint* para la base de datos del buzón de correo determina cuántas copias de la base de datos deben evaluarse como parte de la solicitud. El parámetro *DataMoveReplicationConstraint* tiene los siguientes valores posibles:

  - `None`   Cuando usted crea una base de datos del buzón de correo, este valor se configura de manera predeterminada. Cuando se configura este valor, se omiten las condiciones de la API de garantía de datos. Esta opción debe usarse sólo para bases de datos de buzones de correo que no se replican.

  - `SecondCopy`   Este es el valor predeterminado cuando agrega una segunda copia de la base de datos del buzón de correo. Cuando se configura este valor, al menos una copia pasiva de la base de datos debe cumplir las condiciones de la API de garantía de datos.

  - `SecondDatacenter`   Cuando se configura este valor, al menos una copia pasiva de la base de datos en otro sitio de Active Directory debe cumplir las condiciones de la API de garantía de datos.

  - `AllDatacenters`   Cuando se configura este valor, al menos una copia pasiva de la base de datos en cada sitio de Active Directory debe cumplir las condiciones de la API de garantía de datos.

  - `AllCopies`   Cuando se configura este valor, todas las copias de la base de datos deben cumplir las condiciones de la API de garantía de datos.

**Verificar el estado de la replicación**

Cuando la API de garantía de datos se ejecuta para evaluar el estado de la infraestructura de la copia de la base de datos, se evalúan varios elementos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Si el parámetro <em>DataMoveReplicationConstraint</em> está establecido en...</th>
<th>Entonces, para una base de datos determinada…</th>
<th>Condiciones</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SecondCopy</code></p></td>
<td><p>Al menos una copia pasiva de la base de datos para un base de datos replicada debe cumplir las condiciones de la siguiente columna.</p></td>
<td><p>La copia pasiva de la base de datos deberá:</p>
<ul>
<li><p>Funcionar correctamente.</p></li>
<li><p>Tener una cola de reproducción antes de que transcurran 10 minutos del tiempo de retardo de reproducción.</p></li>
<li><p>Tener una longitud de la cola de copia de menos de 10 registros.</p></li>
<li><p>Tener una longitud de cola de copia promedio de menos de 10 registros. La longitud de cola de copia promedio se computa según la cantidad de veces que la aplicación haya consultado el estado de la base de datos.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SecondDatacenter</code></p></td>
<td><p>Al menos una copia pasiva de la base de datos en otro sitio de Active Directory debe cumplir las condiciones de la siguiente columna.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>AllDatacenters</code></p></td>
<td><p>La copia activa debe estar montada y una copia pasiva de cada sitio de Active Directory debe cumplir las condiciones de la siguiente columna.</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>AllCopies</code></p></td>
<td><p>La copia activa debe estar montada y todas las copias pasivas de la base de datos deben cumplir las condiciones de la siguiente columna.</p></td>
<td></td>
</tr>
</tbody>
</table>


**Verificar el vaciado de la replicación**

La API de garantía de datos también puede utilizarse para validar que la cantidad de copias de la base de datos que era un requisito previo haya reproducido los registros de transacciones requeridos. Esto se verifica mediante la comparación de la marca de tiempo del último registro reproducido con la marca de tiempo comprometida del servicio de llamadas (en la mayoría de los casos, es la marca de tiempo del último archivo de registro que contiene los datos requeridos), más cinco segundos adicionales (para solucionar la desviación o el sesgo del reloj del sistema). Si la marca de tiempo de reproducción es superior a la marca de tiempo comprometida, el parámetro *DataMoveReplicationConstraint* se cumple. Si la marca de tiempo de reproducción es inferior a la marca de tiempo comprometida, el parámetro *DataMoveReplicationConstraint* no se cumple.

Antes de mover grandes cantidades de buzones de correo desde bases de datos de replicación o hacia ellas dentro de un DAG, le recomendamos que configure el parámetro *DataMoveReplicationConstraint* en cada base de datos del buzón de correo según lo siguiente:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Si está implementando…</th>
<th>Configure DataMoveReplicationConstraint en…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bases de datos de buzones de correo que no tienen ninguna copia de la base de datos</p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p>Un DAG dentro de un único sitio de Active Directory</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="odd">
<td><p>Un DAG en múltiples centros de datos que utilizan un sitio de Active Directory extendido</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="even">
<td><p>Un DAG que abarca dos sitios de Active Directory, y usted tendrá copias disponibles de la base de datos en cada sitio</p></td>
<td><p><code>SecondDatacenter</code></p></td>
</tr>
<tr class="odd">
<td><p>Un DAG que abarca dos sitios de Active Directory, y usted tendrá copias retrasadas de la base de datos en el segundo sitio</p></td>
<td><p><code>SecondCopy</code></p>
<p>Esto sucede porque la API de garantía de datos no garantizará los datos que se comprometan hasta que se reproduzca el archivo de registro en la copia de la base de datos y, debido a la naturaleza de la copia retrasada de la base de datos, esta limitación reprobará la solicitud de movimiento a menos que el valor de la copia retrasada de la base de datos ReplayLagTime sea inferior a 30 minutos.</p></td>
</tr>
<tr class="even">
<td><p>Un DAG que abarca tres o más sitios de Active Directory, y cada sitio contendrá copias disponibles de la base de datos</p></td>
<td><p><code>AllDatacenters</code></p></td>
</tr>
</tbody>
</table>


## Equilibrio de las copias de bases de datos

Debido a la naturaleza inherente de los DAG, como resultado de los cambios de base de datos y las conmutaciones por error, las copias de bases de datos de buzones de correo cambian de host varias veces durante la vida de un DAG. Como resultado, los DAG pueden quedar desequilibrados en cuanto a la distribución de las copias de bases de datos de buzones de correo activas. En la tabla siguiente se muestra el ejemplo de un DAG que tiene cuatro bases de datos con cuatro copias para cada base de datos (formando un total de 16 bases de datos en cada servidor) que presenta una distribución desigual de copias de bases de datos activas.

### DAG con distribución desequilibrada de copias activas

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Cantidad de bases de datos activas</th>
<th>Cantidad de bases de datos pasivas</th>
<th>Cantidad de bases de datos montadas</th>
<th>Cantidad de bases de datos desmontadas</th>
<th>Lista de conteo de preferencia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>5</p></td>
<td><p>11</p></td>
<td><p>5</p></td>
<td><p>0</p></td>
<td><p>4, 4, 3, 5</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 8, 6, 1</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>0</p></td>
<td><p>13, 2, 1, 0</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 1, 5, 9</p></td>
</tr>
</tbody>
</table>


En el ejemplo anterior, hay cuatro copias de cada base de datos y, por lo tanto, sólo cuatro valores posibles de preferencia de activación (1, 2, 3 ó 4). La columna **Lista de conteo de preferencia** muestra el conteo de la cantidad de bases de datos con cada uno de esos valores. Por ejemplo, en EX3 hay 13 copias de bases de datos con una preferencia de activación de 1, dos copias con una preferencia de activación de 2, una copia con una preferencia de activación de 3 y ninguna copia con una preferencia de activación de 4.

Como puede ver, este DAG no está equilibrado en cuanto a la cantidad de bases de datos activas alojadas por cada miembro del DAG, a la cantidad de bases de datos pasivas alojadas por cada miembro del DAG ni al conteo de preferencia de activación de las bases de datos alojadas.

Puede usar el script RedistributeActiveDatabases.ps1 para almacenar las copias activas de las bases de datos del buzón en todo el DAG. Este script traslada las bases de datos entre sus copias, intentando obtener una cantidad igual de bases de datos montadas en cada servidor del DAG. Si es necesario, el script también intenta equilibrar las bases de datos activas entre sitios.

El script proporciona dos opciones para equilibrar copias de bases de datos activas dentro de un DAG:

  - **BalanceDbsByActivationPreference**   Cuando se indica esta opción, el script intenta trasladar las bases de datos a su copia preferida (según la preferencia de activación) sin tener en cuenta el sitio de Active Directory.

  - **BalanceDbsBySiteAndActivationPreference**   Cuando se indica esta opción, el script intenta trasladar las bases de datos activas a su copia preferida y al mismo tiempo intenta equilibrar las bases de datos activas dentro de cada sitio de Active Directory.

Después de ejecutar el script con la primera opción, el DAG que estaba desequilibrado se equilibra, tal como se muestra en la tabla siguiente.

### DAG con distribución equilibrada de copias activas

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Cantidad de bases de datos activas</th>
<th>Cantidad de bases de datos pasivas</th>
<th>Cantidad de bases de datos montadas</th>
<th>Cantidad de bases de datos desmontadas</th>
<th>Lista de conteo de preferencia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
</tbody>
</table>


Como se muestra en la tabla anterior, este DAG está equilibrado en cuanto a la cantidad de bases de datos activas y pasivas que hay en cada servidor y en la preferencia de activación de todos los servidores.

La siguiente tabla muestra los parámetros disponibles para el script RedistributeActiveDatabases.ps1.

### Parámetros del script RedistributeActiveDatabases.ps1

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
<td><p>Especifica el nombre del DAG que desea volver a equilibrar. Si se omite este parámetro, se usa el DAG del que es miembro el servidor local.</p></td>
</tr>
<tr class="even">
<td><p><em>BalanceDbsByActivationPreference</em></p></td>
<td><p>Especifica que el script debe trasladar las bases de datos a su copia preferida sin tener en cuenta el sitio de Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><em>BalanceDbsBySiteAndActivationPreference</em></p></td>
<td><p>Especifica que el script debe intentar trasladar las bases de datos activas a su copia preferida y al mismo tiempo intentar equilibrar las bases de datos activas dentro de cada sitio de Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowFinalDatabaseDistribution</em></p></td>
<td><p>Indica que se muestre un informe la distribución actual de bases de datos, una vez que la redistribución se haya completado.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowedDeviationFromMeanPercentage</em></p></td>
<td><p>Especifica la variación entre sitios permitida para las bases de datos activas, expresada en un porcentaje. El valor predeterminado es 20%. Por ejemplo, si hubiera 99 bases de datos distribuidas en tres sitios, la distribución ideal sería de 33 bases de datos en cada uno. Si la variación permitida es del 20%, el script intentará equilibrar las bases de datos de manera que cada sitio tenga hasta un 10% más o menos que dicho número. El 10% de 33 es 3,3 lo cual se redondea en 4. Por lo tanto, el script intentará colocar entre 29 y 37 bases de datos en cada sitio.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowDatabaseCurrentActives</em></p></td>
<td><p>Indica al script que produzca un informe de cada base de datos, detallando de qué manera se trasladó dicha base de datos y si ahora se encuentra activa en su copia preferida.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowDatabaseDistributionByServer</em></p></td>
<td><p>Indica al script que produzca un informe de cada servidor, mostrando su distribución de bases de datos.</p></td>
</tr>
<tr class="even">
<td><p><em>RunOnlyOnPAM</em></p></td>
<td><p>Indica al script que sólo se ejecute en el miembro del DAG que posee el rol de PAM. El script verifica que se esté ejecutando desde el PAM. Si no se está ejecutando desde el PAM, el script sale.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogEvents</em></p></td>
<td><p>Indica al script registrar un evento (MsExchangeRepl evento 4115) que contenga un resumen de las acciones.</p></td>
</tr>
<tr class="even">
<td><p><em>IncludeNonReplicatedDatabases</em></p></td>
<td><p>Indica al script que incluya las bases de datos no replicadas (bases de datos sin copias) al determinar la manera de redistribuir las bases de datos activas. Si bien las bases de datos no replicadas no pueden trasladarse, pueden afectar la distribución de las bases de datos replicadas.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>El modificador Confirmar se puede usar para suprimir la pregunta de confirmación que aparece de forma predeterminada cuando se ejecuta este script. Para quitar la pregunta de confirmación, use la sintaxis -Confirm:$False. Debe incluir dos puntos ( : ) en la sintaxis.</p></td>
</tr>
</tbody>
</table>


## Ejemplos con RedistributeActiveDatabases.ps1

En este ejemplo se muestra la distribución actual de las bases de datos de un DAG, incluida la lista de conteo de preferencia.

    RedistributeActiveDatabases.ps1 -DagName DAG1 -ShowDatabaseDistributionByServer | Format-Table

En este ejemplo se redistribuyen y equilibran las copias activas de las bases de datos del buzón de correo de un DAG mediante el uso de la preferencia de activación sin solicitar entrada.

    RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -Confirm:$False

En este ejemplo se redistribuyen y equilibran las copias de las bases de datos de buzones de correo activas de un DAG, mediante la preferencia de activación, y se genera un resumen de la distribución.

    RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -ShowFinalDatabaseDistribution

## Supervisión de copias de base de datos

Una copia de base de datos es su primer defensa si se produce un error que afecta la copia activa de una base de datos. Por lo tanto, es crítico supervisar el estado de las copias de las bases de datos para garantizar que estarán disponibles cuando sea necesario. Puede ver una variedad de información, incluida la longitud de la cola de copia, la longitud de la cola de reproducción, la información sobre la categoría y el estado del índice de contenido examinando los detalles de una copia de base de datos en el EAC. También puede usar el cmdlet **Get-MailboxDatabaseCopyStatus** en el Shell para ver cierta información de estado de una copia de base de datos.

Para obtener más información acerca de cómo supervisar copias de base de datos, vea [Supervisión de grupos de disponibilidad de base de datos](monitoring-database-availability-groups-exchange-2013-help.md).

## Eliminación de una copia de base de datos

Puede eliminar en cualquier momento una copia de base de datos con la EMC o con el cmdlet **Remove-MailboxDatabaseCopy** en el Shell. Después de quitar una copia de base de datos, debe eliminar del servidor del cual se está quitando la copia cualquier archivo de base de datos y archivo de registro de forma manual. Para obtener instrucciones detalladas acerca de cómo eliminar la copia de una base de datos, vea [Eliminación de una copia de base de datos de buzones](remove-a-mailbox-database-copy-exchange-2013-help.md).

## Cambios de base de datos

El servidor de buzones de correo que hospeda la copia activa de una base de datos se conoce como el patrón de base de datos de buzones de correo. El proceso de activación de una copia de base de datos pasiva cambia el patrón de base de datos de buzones de correo de la base de datos y convierte a la copia pasiva en la nueva copia activa. Este proceso se denomina cambio de base de datos. En un cambio de base de datos, la copia activa de una base de datos se desmonta en un servidor de buzones de correo, y una copia pasiva de esa base de datos se monta como la nueva base de datos de buzones de correo activa en otro servidor de buzones de correo. Cuando se realiza un cambio, tiene la opción de anular la configuración del marcado de montaje de base de datos en el nuevo patrón de base de datos de buzones de correo.

Si revisa la columna de la derecha de la ficha **Copia de la base de datos** en la EAC, puede identificar rápidamente qué servidor de buzones de correo es el patrón de la base de datos de buzones de correo actual. Para realizar un cambio, use el vínculo **Activar** en la EMC o use el cmdlet **Move-ActiveMailboxDatabase** en el Shell.

Existen varias comprobaciones internas que se realizarán antes de activar una copia pasiva:

  - Se comprueba el estado de la copia de base de datos. Si la copia de base de datos está en estado de error, se bloquea el cambio. Puede anular este comportamiento y omitir la comprobación de estado usando el parámetro *SkipHealthChecks* del cmdlet **Move-ActiveMailboxDatabase**. Este parámetro le permite mover la copia activa a una copia de base de datos en estado de error.

  - La copia activa de la base de datos se verifica para comprobar si es actualmente un origen de inicialización para copias pasivas de la base de datos. Si la copia activa actualmente se está usando como origen de inicialización, el cambio se bloquea. Puede anular este comportamiento y omitir la verificación del origen de inicialización usando el parámetro *SkipActiveCopyChecks* del cmdlet **Move-ActiveMailboxDatabase**. Este parámetro le permite mover la copia activa que se está usando como origen de inicialización. Si utiliza este parámetro se cancelará la operación de inicialización y se considerará un error.

  - Las longitudes de la cola de copia y de la cola de reproducción de la copia de base de datos se comprueban para garantizar que sus valores estén dentro de los criterios configurados. Además, la copia de base de datos se comprueba para garantizar que no esté en uso en ese momento como origen de inicialización. Si los valores para las longitudes de cola están fuera de los criterios configurados, o si la base de datos está en uso como origen de inicialización, se bloquea el cambio. Puede anular este comportamiento y omitir estas comprobaciones usando el parámetro *SkipLagChecks* del cmdlet **Move-ActiveMailboxDatabase**. Este parámetro permite que se active una copia que tiene las colas de reproducción y copia fuera de los criterios configurados.

  - Se comprueba el estado del catálogo de búsqueda (índice de contenido) de la copia de base de datos. Si el catálogo de búsqueda no está actualizado, se encuentra en un estado incorrecto o está dañado, se bloquea el cambio. Puede anular este comportamiento y omitir la comprobación del catálogo de búsqueda usando el parámetro *SkipClientExperienceChecks* del cmdlet **Move-ActiveMailboxDatabase**. Este parámetro hace que esta búsqueda omita la comprobación del estado del catálogo. Si el catálogo de búsqueda de la copia de base de datos que está activando se encuentra en un estado incorrecto o inutilizable, y usted usa este parámetro para omitir la comprobación del estado del catálogo y activar la copia de base de datos, tendrá que rastrear o inicializar el catálogo de búsqueda nuevamente.

Al realizar un cambio de base de datos, también tiene la opción de anular la configuración del marcado de montaje para el servidor que hospeda la copia pasiva de la base de datos que se está activando. Al usar el parámetro *MountDialOverride* del cmdlet **Move-ActiveMailboxDatabase**, se le indica al servidor de destino que anule su propia configuración del marcado de montaje y use la que especifica el parámetro *MountDialOverride*.

Para obtener instrucciones detalladas acerca de cómo realizar un cambio de una copia de base de datos, vea [Activación de una copia de base de datos de buzones](activate-a-mailbox-database-copy-exchange-2013-help.md).

