---
title: 'Active Manager: Exchange 2013 Help'
TOCTitle: Active Manager
ms:assetid: f4be27b7-1d7c-47b4-87ac-bfdfcc046f00
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd776123(v=EXCHG.150)
ms:contentKeyID: 48268874
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Manager

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Microsoft Exchange Server 2013 incluye un componente denominado *Active Manager* que administra la plataforma de alta disponibilidad e incluye el grupo de disponibilidad de base de datos (DAG) y copias de la base de datos de buzones de correo. Active Manager se ejecuta dentro del servicio de replicación de Microsoft Exchange (MSExchangeRepl.exe) en todos los servidores de buzones de correo. En los servidores de buzones de correo que no son miembros de un DAG, existe un único rol de Active Manager: *Active Manager independiente*. En los servidores que son miembros de un DAG, existen dos roles de Active Manager: *Primary Active Manager* (PAM) y *Standby Active Manager* (SAM). PAM es el rol de Active Manager de un DAG que decide qué copias serán activas y qué copias serán pasivas. PAM se encarga de recibir las notificaciones de cambio de topología y de reaccionar a los errores de servidor. El miembro de DAG que posee el rol de PAM siempre es aquél que actualmente posee el recurso de quórum de clúster (grupo de clústeres predeterminado). Si el servidor que posee el recurso de quórum de clúster experimenta un error, el rol de PAM pasa automáticamente a un servidor subsistente que se apropia del recurso de quórum de clúster. Además, si necesita desconectar el servidor que hospeda el recurso de quórum de clúster para realizar tareas de mantenimiento o una actualización, primero deberá mover el PAM a otro servidor del DAG. El PAM controla el movimiento de las designaciones activas entre las copias de una base de datos. (Solo puede haber una copia activa en un momento dado, que se puede montar o desmontar.) El PAM también realiza las funciones del rol de SAM en el sistema local (detección de errores en bases de datos locales y almacenes de información locales).

SAM proporciona información acerca del servidor que hospeda la copia activa de una base de datos de buzones de correo para otros componentes de Exchange que ejecutan un componente de cliente de Active Manager (por ejemplo, servicios de acceso de cliente o de transporte). El SAM detecta los errores de bases de datos locales y el almacén de información local. Reacciona a los errores solicitando al PAM que inicie un proceso de conmutación por error (si se ha replicado la base de datos). Un SAM no determina el destino de una conmutación por error ni actualiza el estado de ubicación de una base de datos en el PAM. Obtendrá acceso al estado de ubicación de la copia de base de datos activa para responder a las consultas que recibe sobre la copia activa de la base de datos.


> [!NOTE]
> Exchange&nbsp;2013 no es una aplicación agrupada en clúster. En lugar de ello, utiliza las funciones de la biblioteca de clústeres implementadas en clusapi.dll para clústeres, grupos, redes de clústeres (latentes), administración de nodos, registro de clústeres y varias funciones de códigos de control. Además, Active Manager almacena la información actual de la base de datos de buzones de correo (por ejemplo, datos activos y pasivos, y datos montados) en la base de datos de clúster (también conocida como registro de clústeres). Aunque la información se almacena directamente en la base de datos de clúster, ningún otro componente tiene acceso directo a ésta.



En Exchange 2013, el servicio de replicación de Microsoft Exchange supervisa periódicamente el mantenimiento de todas las bases de datos montadas. También supervisa el Motor de almacenamiento extensible (ESE) para detectar errores o problemas de E/S. Cuando el servicio detecta un error, lo notifica a Active Manager. A continuación, Active Manager determina qué copia de base de datos se debe montar y qué se requiere para hacerlo. Además, realiza un seguimiento de la copia activa de una base de datos de buzones de correo (basada en la última copia montada de la base de datos) y proporciona información sobre los resultados del seguimiento al servidor de acceso de cliente al cual está conectado el cliente.

## Mejor selección de copia

Cuando se produce un error que impide el acceso a la copia activa de una base de datos de buzones de correo replicada, Active Manager sigue varios pasos para recuperarse del error y selecciona la mejor copia pasiva posible de la base de datos afectada para activar. Este proceso era conocido como mejor selección de copia (BCS) en Exchange 2010 y ahora se conoce como mejor selección de copia y servidor (BCSS) en Exchange 2013. El proceso general tiene lugar en el siguiente orden:

1.  La función de disponibilidad administrada o Active Manager detecta un error, o bien un administrador inicia un cambio sin destino.

2.  PAM ejecuta el algoritmo interno BCSS.

3.  Se lleva a cabo un proceso llamado *intentar copia de los últimos registros* (ACLL), que intenta copiar los archivos de registro faltantes del servidor que hospedaba la copia de la base de datos activa antes de que se produjera el error o el cambio.

4.  Una vez que se completa el proceso ACLL, el valor de *AutoDatabaseMountDial* para los servidores de buzones de correo que hospedan las copias de la base de datos se compara con la longitud de cola de copia de la base de datos que se activa. Llegados a este punto, existen dos posibilidades:
    
      - El número de archivos de registro que faltan es menor o igual que el valor de *AutoDatabaseMountDial*, en cuyo caso se realiza el paso 5.
    
      - El número de archivos de registro que faltan es mayor que el valor de *AutoDatabaseMountDial*, en cuyo caso Active Manager tratará de activar la mejor copia siguiente disponible, si existe.

5.  PAM emite una solicitud de montaje para el Almacén de información de Microsoft Exchange mediante una llamada de procedimiento remoto (RPC). Llegados a este punto, existen dos posibilidades:
    
      - Se monta la base de datos y pasa a estar disponible para los clientes.
    
      - No se monta la base de datos y el PAM realiza los pasos 3 y 4 en la siguiente mejor copia (si hay alguna disponible).

En Exchange 2010, el proceso BCS evalúa varios aspectos de cada copia de base de datos para determinar la mejor copia para activar. Estos incluían:

  - Copiar longitud de cola

  - Repetir longitud de cola

  - Estado de la base de datos

  - Estado del índice de contenido

En Exchange 2013, Active Manager realiza las mismas fases y comprobaciones de BCS, pero ahora también incluye el uso de una restricción del orden descendente de los estados. De manera específica, BCSS incluye varias comprobaciones nuevas de mantenimiento que forman parte de los componentes de supervisión de disponibilidad administrada integrados en Exchange 2013. Existen cuatro nuevas comprobaciones adicionales que realiza Active Manager (se indican por orden de realización):

1.  **Todo correcto**   Comprueba que un servidor que hospede una copia de la base de datos afectada tenga todos los componentes de supervisión en estado correcto.

2.  **Hasta correcto normal**   Comprueba que un servidor que hospede una copia de la base de datos afectada tenga todos los componentes de supervisión con prioridad Normal en estado correcto.

3.  **Todo mejor que el origen**   Comprueba que un servidor que hospede una copia de la base de datos afectada tenga los componentes de supervisión en un estado que sea mejor que el servidor actual que hospeda la copia afectada.

4.  **Igual que el origen**   Comprueba que un servidor que hospede una copia de la base de datos afectada tenga los componentes de supervisión en un estado que sea igual que el servidor actual que hospeda la copia afectada.

Si se invoca a BCSS como resultado de una conmutación por error desencadenada por un componente de supervisión (p. ej., mediante un respondedor de conmutación por error), se aplica una restricción obligatoria adicional allí donde el estado del componente del servidor de destino deba ser mejor que el servidor en el que se produjo la conmutación por error. Por ejemplo, si un error de Microsoft Office Outlook Web App desencadena una conmutación por error mediante un respondedor de conmutación por error, BCSS debe seleccionar un servidor que hospede una copia de la base de datos afectada en la que Outlook Web App sea correcto.

## Proceso de mejor selección de copia

Con respecto a los errores de base de datos (no errores de protocolo), Active Manager realiza las mismas comprobaciones en Exchange 2013 que en Exchange 2010. Active Manager inicia el proceso de selección de la mejor copia creando una lista de copias de base de datos que son posibles candidatas para la activación. Las copias de bases de datos que sean inalcanzables o que estén bloqueadas administrativamente para la activación se ignoran y no se usarán durante el proceso de selección. El orden de la lista depende del valor de *AutoDatabaseMountDial*:

  - Si el parámetro *AutoDatabaseMountDial* se configura con cualquier valor que no sea `Lossless` en todos los servidores que hospeden una copia de la base de datos, Active Manager ordena la lista resultante tomando la longitud de cola de copia como clave principal. El cálculo se basa en LastLogInspected (desde el punto de vista de la copia), por lo que la lista de posibles copias se ordenará por el valor más alto para LastLogInspected (que será la copia con la longitud de copia de cola más baja). Si es necesario, Active Manager ordena la lista una segunda vez y usa el valor de preferencias de activación como clave secundaria para romper cualquier condición de unión en la que dos o más copias pasivas tengan la misma longitud de cola de copia. La copia con el valor de preferencia de activación más bajo tiene la máxima prioridad en la lista.

  - Si el parámetro *AutoDatabaseMountDial* se configura con un valor `Lossless` en cualquier servidor que hospede una copia de la base de datos, Active Manager ordena la lista resultante en orden ascendente tomando el valor de preferencia de activación como clave principal. Además, cuando un administrador ejecuta un servidor sin pérdida o un cambio de base de datos sin especificar un destino, Active Manager también ordena la lista resultante en orden ascendente tomando el valor de referencia de activación como clave principal.

A continuación, Active Manager intenta localizar una copia de la base de datos de buzones en la lista cuyo estado sea Healthy, DisconnectedAndHealthy, DisconnectedAndResynchronizing o SeedingSource y evalúa el potencial de activación de cada una de las copias de la lista mediante un conjunto ordenado de diez criterios. Active Manager determina si alguno de las copias candidatas para la activación cumple el primer conjunto de criterios:

  - Tiene un índice de contenido con un estado Correcto.

  - Tiene una longitud de la cola de copia inferior a 10 archivos de registro.

  - Tiene una longitud de la cola de reproducción inferior a 50 archivos de registro.

Si ninguna de las copias de base de datos cumple el primer conjunto de criterios, Active Manager intenta localizar una copia de base de datos que cumpla el segundo conjunto de criterios:

  - Tiene un índice de contenido con un estado de rastreo.

  - Tiene una longitud de la cola de copia inferior a 10 archivos de registro.

  - Tiene una longitud de la cola de reproducción inferior a 50 archivos de registro.

Si ninguna de las copias de base de datos cumple el segundo conjunto de criterios, Active Manager intenta localizar una copia de base de datos que cumpla el tercer conjunto de criterios:

  - Tiene un índice de contenido con un estado Correcto.

  - Tiene una longitud de la cola de reproducción inferior a 50 archivos de registro.

Si ninguna de las copias de base de datos cumple el tercer conjunto de criterios, Active Manager intenta localizar una copia de base de datos que cumpla el cuarto conjunto de criterios:

  - Tiene un índice de contenido con un estado de rastreo.

  - Tiene una longitud de la cola de reproducción inferior a 50 archivos de registro.

Si ninguna de las copias de base de datos cumple el cuarto conjunto de criterios, Active Manager intenta localizar una copia de base de datos que cumpla el quinto conjunto de criterios:

  - Tiene una longitud de la cola de reproducción inferior a 50 archivos de registro.

Si ninguna de las copias de base de datos cumple el quinto conjunto de criterios, Active Manager intenta localizar una copia de base de datos que cumpla el sexto conjunto de criterios:

  - Tiene un índice de contenido con un estado Correcto.

  - Tiene una longitud de la cola de copia inferior a 10 archivos de registro.

Si ninguna de las copias de base de datos cumple el sexto conjunto de criterios, Active Manager intenta localizar una copia de base de datos que cumpla el séptimo conjunto de criterios:

  - Tiene un índice de contenido con un estado de rastreo.

  - Tiene una longitud de la cola de copia inferior a 10 archivos de registro.

Si ninguna de las copias de base de datos cumple el séptimo conjunto de criterios, Active Manager intenta localizar una copia de base de datos que cumpla el octavo conjunto de criterios:

  - Tiene un índice de contenido con un estado Correcto.

Si ninguna de las copias de base de datos cumple el octavo conjunto de criterios, Active Manager intenta localizar una copia de base de datos que cumpla el noveno conjunto de criterios:

  - Tiene un índice de contenido con un estado de rastreo.

Si ninguna de las copias de base de datos cumple el noveno conjunto de criterios, Active Manager intenta activar cualquier copia de base de datos que tenga el estado Healthy, DisconnectedAndHealthy, DisconnectedAndResynchronizing o SeedingSource (el décimo conjunto de criterios). Si no encuentra ninguna copia de base de datos que cumpla el décimo conjunto de criterios, no podrá activar automáticamente ninguna copia de base de datos.

Después de encontrar una o más copias que cumplan uno o más conjuntos de criterios, se ejecuta el proceso ACLL para copiar los archivos de registro de la copia original a la nueva posible copia activa. Después de completar el proceso ACLL, el PAM emite una solicitud de montaje y se monta la base de datos, que pasa a estar disponible para los clientes, o bien no se monta la base de datos y el PAM busca la siguiente mejor copia (si hay alguna disponible).

