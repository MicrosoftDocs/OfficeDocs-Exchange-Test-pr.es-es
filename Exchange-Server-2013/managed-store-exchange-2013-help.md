---
title: 'Almacén administrado: Exchange 2013 Help'
TOCTitle: Almacén administrado
ms:assetid: efdaf80b-335c-491c-8eb5-1fafd297e8a2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn792020(v=EXCHG.150)
ms:contentKeyID: 62607055
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Almacén administrado

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-07-14_

Todas las versiones previas de Exchange Server, desde Exchange Server 4.0 hasta Exchange Server 2010, han admitido la ejecución de una sola instancia del proceso de almacén de información (Store.exe) en el rol de servidor Buzón de correo. Esta única instancia del almacén hospeda todas las bases de datos en el servidor: activas, pasivas, retrasadas y de recuperación. En las arquitecturas anteriores de Exchange, hay poco aislamiento, si lo hay, entre las distintas bases de datos hospedadas en un servidor de buzones. El problema que existe con una base de datos de un solo buzón es que puede afectar potencialmente de forma negativa a todas las demás bases de datos. Las interrupciones que surgen a raíz del daño del buzón pueden afectar el servicio para todos los usuarios cuyas bases de datos están hospedadas en dicho servidor.

Otro desafío que presenta una única instancia de almacén en las versiones anteriores de Exchange es que el Motor de almacenamiento extensible (ESE) escala bien a 8-12 núcleos del procesador, pero si se supera esta cantidad, los problemas de sincronización en la memoria caché y la comunicación entre los procesadores generan una escala negativa. En la actualidad se usan servidores mucho más grandes por lo que hay disponibles sistemas con más de 16 núcleos. Esto supondría el desafío administrativo de administrar la afinidad de 8-12 núcleos para ESE y usar los demás núcleos para procesos no relacionados con el almacén (por ejemplo, Asistentes, Search Foundation, Disponibilidad administrada, etc.). Además, la arquitectura anterior restringía el escalado para el proceso de almacén.

El proceso Store.exe ha evolucionado considerablemente con el transcurso de los años al igual que Exchange Server, pero como único proceso, su escalabilidad está limitada y representa un único punto de error. Debido a estos límites, Store.exe ya no está disponible en Exchange 2013 y se lo reemplazó por el almacén administrado.

## Almacén administrado

Almacén administrado es el nombre de los procesos del almacén de información (también conocido como el almacén) en Exchange Server 2013. El almacén administrado usa un modelo de proceso de controlador/trabajo que proporciona aislamiento del proceso de almacenamiento y conmutación por error de la base de datos más rápida. El almacén administrado también incluye un nuevo mecanismo de almacenamiento en caché de la base de datos estático que reemplaza el algoritmo de búfer dinámico de las versiones anteriores de Exchange Server. En el modelo de múltiples procesos que usa el almacén administrado, hay un único proceso de controlador de servicio del almacén (en este caso, Microsoft.Exchange.Store.Service.exe también conocido como MSExchangeIS) y un proceso de trabajo (en este caso, Microsoft.Exchange.Store.Worker.exe) para cada base de datos montada. Al montar una base de datos, se crea una instancia de un nuevo proceso de trabajo que da servicio a esa base de datos. Cuando se desmonta una base de datos, se termina el proceso de trabajo para dicha base de datos.

Por ejemplo, si tiene 40 bases de datos montadas en un servidor, habrá 41 procesos en ejecución para el almacén administrado, uno para cada base de datos y otro para el controlador de procesos de servicio del almacén.

El controlador de procesos de servicio del almacén es muy fino y confiable, pero si deja de funcionar o se termina, todos sus procesos de trabajo también dejan de existir (detectarán que el proceso del controlador de servicio se ha ido y se cierran). El controlador de procesos de almacén supervisa el mantenimiento de todos los procesos de trabajo del almacén en el servidor. Una terminación inesperada o forzada de Microsoft.Exchange.Store.Service.exe provoca una conmutación por error inmediata de todas las copias de bases de datos activas. El almacén administrado también está estrechamente integrado con el servicio de replicación de Microsoft Exchange (MSExchangeRepl.exe) y Active Manager. El proceso de controlador, los procesos de trabajo y servicio de replicación trabajan en conjunto para proporcionar mayor disponibilidad y confiabilidad:

  - Proceso del servicio de replicación de Microsoft Exchange (MSExchangeRepl.exe)
    
      - Responsable de la emisión de montar y desmontar las operaciones de la tienda
    
      - Inicia la acción de recuperación en los errores de almacenamiento o base de datos informados por los respondedores del almacén, el Motor de almacenamiento extensible (ESE) y la disponibilidad administrada.
    
      - Detecta errores inesperados en la base de datos.
    
      - Proporciona la interfaz administrativa para las tareas de administración.

  - Controlador/proceso del servicio de almacén (Microsoft.Exchange.Store.Service.exe)
    
      - Administra cada duración del proceso de trabajo en función de las operaciones de montaje y desmontaje recibidas desde el servicio de replicación.
    
      - Controla las solicitudes entrantes desde el Administrador de control de servicios de Windows.
    
      - Registra elementos de error cuando se detectan problemas del proceso de trabajo del almacén (por ejemplo, bloqueo o salida inesperada).
    
      - Termina los procesos de trabajo del almacén en evento de conmutación por error de respuesta.

  - Proceso de trabajo de almacén (Microsoft.Exchange.Store.Worker.exe)
    
      - Responsable de ejecutar las operaciones RPC para buzones de correo en una base de datos
    
      - La instancia de extremo RPC dentro del proceso de trabajo es el GUID de la base de datos.
    
      - Proporciona la memoria caché de base de datos para una base de datos.

## Algoritmo de almacenamiento en caché de base de datos estático

El algoritmo de almacenamiento en caché de bases de datos conocido como asignación dinámica de búfer que se introdujo en Exchange Server 5.5 y que se usó en el almacén de información en Exchange 2000 Server, Exchange Server 2003, Exchange Server 2007 y Exchange Server 2010, ya no está disponible en Exchange 2013. Exchange 2013 emplea un algoritmo muy simple y directo para determinar la memoria caché de la base de datos. El almacén administrado ya no reasigna dinámicamente la memoria caché entre las bases de datos cuando se produce una conmutación por error, lo que simplifica enormemente la administración interna de la caché. En su lugar, la memoria asignada para cada caché de base de datos (por ej., cada proceso de trabajo del almacén) se basa en un número de copias de bases de datos locales y en el valor de *MaximumActiveDatabases*, si está configurado. Si el valor de *MaximumActiveDatabases* es mayor que el número de copias de bases de datos actual, el cálculo de la memoria caché se basa en el número de copias de bases de datos.

El algoritmo estático que usa Exchange 2013 asigna memoria para cada memoria caché del ESE del proceso de trabajo del trabajo en función de la memoria RAM física. Esto se conoce como un *destino máximo de memoria caché* de la base de datos. El 25 % de la memoria total del servidor se asigna a la caché del ESE. Esto se conoce como el *destino de tamaño de caché de servidor*.


> [!NOTE]
> El destino de tamaño de la caché del servidor y, por ende, la cantidad de memoria asignada al almacén para la memoria caché del ESE, se pueden reemplazar mediante el atributo <EM>msExchESEParamCacheSizeMax</EM> del objeto <EM>InformationStore</EM> en Active Directory (el valor configurado es el número de páginas de 32 KB que se asignarán en todos los procesos del almacén).



Se asigna una cantidad estática de esta memoria caché a las copias activas y pasivas. El proceso de trabajo de almacén se asignará al destino máximo de memoria caché solo cuando se brinda servicio a una copia de la base de datos activa. A las copias de bases de datos pasivas se les asigna el 20 % del destino máximo de memoria caché. El almacén reserva el resto y lo asigna al proceso de trabajo si la base de datos pasa de pasivo a activo.

El destino máximo de memoria caché se calcula solo en el inicio del almacén. Por lo tanto, si agrega o quita las bases de datos o las copias de la base de datos, debe reiniciar el servicio del controlador de almacén (MSExchangeIS) para que la memoria caché se pueda ajustar en consecuencia. Si el servicio no se reinicia, entonces las bases de datos recientemente creadas tendrán un destino de tamaño de memoria caché más pequeño que las bases de datos creadas antes del inicio del servicio. En este caso, la suma de los destinos de tamaño de la memoria caché de bases de datos probablemente superará el destino de tamaño de la memoria caché de servidor hasta que se reinicie MSExchangeIS.

## Cálculos de memoria caché de bases de datos de ejemplo

A continuación se proporcionan cálculos de memorias caché de bases de datos que se basan en la configuración de memoria y base de datos de un servidor de buzones.

**Ejemplo 1**

En este ejemplo, el servidor de buzón tiene 48 GB de memoria y hospeda dos bases de datos activas y dos bases de datos pasivas. Además, el parámetro *MaximumActiveDatabases* no está configurado. En esta configuración, la cantidad de caché de base de datos es de 3 GB para cada proceso de trabajo de copia de base de datos activa y 0,6 GB para cada proceso de trabajo de copia pasiva de la base de datos. Aquí le mostramos cómo se obtuvieron estos valores.

Para obtener el destino de tamaño de la memoria caché de servidor, multiplique la cantidad de memoria en un 25 %:

48 GB X 25 % = 12 GB

Para obtener el destino máximo de memoria caché de la base de datos, divida el destino de tamaño dela memoria caché de servidor por el número total de bases de datos activas y pasivas:

12 GB / 4 bases de datos = 3 GB

Para determinar la cantidad de memoria utilizada para las copias pasivas de la base de datos, multiplique el destino máximo de memoria caché de base de datos en un 20 %:

3 GB X 20 % = 0,6 GB

Fuera de los 12 GB de memoria asignada al destino de tamaño de memoria caché del servidor, los procesos de trabajo de la base de datos usarán 7,2 GB y el almacén de información reservará 4,8 GB para las dos copias de bases de datos pasivas en caso de que se conviertan en copias activas. En ese caso, usarán su destino máximo de memoria caché de 3 GB.

**Ejemplo 2**

En este ejemplo, el servidor de buzón de correo cuenta también con 48 GB de memoria y hospeda dos bases de datos activas y dos bases de datos pasivas; no obstante, el parámetro *MaximumActiveDatabases* está configurado con un valor de 2. En esta configuración, la cantidad de memoria caché de la base de datos es 5 GB para cada proceso de trabajo de copia de base de datos activa y 0,2 GB para cada proceso de trabajo de copia de base de datos pasiva. Aquí le mostramos cómo se obtuvieron estos valores.

Para obtener el destino de tamaño de la memoria caché de servidor, multiplique la cantidad de memoria en un 25 %:

48 GB X 25 % = 12 GB

Para obtener el destino máximo de memoria caché de la base de datos, divida el destino de tamaño de la memoria caché del servidor por el número total de bases de datos activas sumado al número total de bases de datos pasivas multiplicado por 20 %:

12 GB / (2A + (2P X 20 %)) = 5 GB

Para determinar la cantidad de memoria utilizada para las copias pasivas de la base de datos, multiplique el destino máximo de memoria caché de base de datos en un 20 %:

5 GB X 20% = 1 GB

Fuera de los 12 GB de memoria asignada al destino de tamaño de memoria caché del servidor, los procesos de trabajo de la base de datos usarán 12 GB y el almacén de información no reservará memoria para las dos copias de bases de datos pasivas porque no pueden convertirse en copias activas en esta configuración (debido a que el parámetro *MaximumActiveDatabases* está configurado con un valor de 2 y ya hay dos copias de bases de datos activas en el servidor).

