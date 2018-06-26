---
title: 'Virtualización de Exchange 2013: Exchange 2013 Help'
TOCTitle: Virtualización de Exchange 2013
ms:assetid: 36184b2f-4cd9-48f8-b100-867fe4c6b579
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ619301(v=EXCHG.150)
ms:contentKeyID: 49116143
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Virtualización de Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2017-08-08_

Puede implementar Microsoft Exchange Server 2013 en un entorno virtualizado. En este tema se proporciona información general sobre los escenarios compatibles con la implementación de Exchange 2013 en software de virtualización de hardware.

**Contenido**

Requirements for hardware virtualization

Host machine storage requirements

Exchange storage requirements

Exchange memory requirements and recommendations

Host-based failover clustering and migration for Exchange

Los siguientes términos se utilizan en la descripción de la virtualización de Exchange:

  - **Arranque en frío** Cuando un sistema pasa de estar de un estado de apagado a un inicio correcto del sistema operativo, la acción se denomina *arranque en frío*. En este caso, no se conserva ningún estado de sistema operativo.

  - **Estado guardado**   Cuando se apaga una máquina virtual, los hipervisores generalmente tienen la capacidad de guardar el estado de la máquina virtual, por lo que cuando ésta se enciende de nuevo, vuelve al *estado guardado* en lugar de iniciarse mediante un arranque en frío.

  - **Migración planificada**   Cuando un administrador de sistema inicia el movimiento de una máquina virtual de un host de hipervisor a otro, esta acción se denomina *migración planificada*. Puede tratarse de una migración única, o bien un administrador de sistema puede configurar la automatización para mover la máquina virtual de manera programada. Una migración planificada también puede ser el resultado de otro evento que ocurra en el sistema, que no sea un error de hardware o software. El punto clave es que la máquina virtual de Exchange funciona correctamente y se debe reubicar por algún motivo. Esta reubicación puede hacerse a través de tecnologías como Migración en vivo o vMotion. No obstante, si la máquina virtual de Exchange o el host del hipervisor donde se encuentra la máquina virtual experimenta algún tipo de condición de error, el resultado no se considerará una migración planificada.

## Requisitos para la virtualización de hardware

Microsoft admite Exchange 2013 en producción en software de virtualización de hardware únicamente si se cumplen las siguientes condiciones:

  - El software de virtualización de hardware está ejecutando uno de los componentes siguientes:
    
      - Cualquier versión de Windows Server con tecnología Hyper-V o Microsoft Hyper-V Server
    
      - Cualquier hipervisor de terceros que se haya validado según el [Programa de validación de virtualización de Windows Server](https://go.microsoft.com/fwlink/p/?linkid=125375).
    

    > [!NOTE]
    > Se admite la implementación de Exchange 2013 en los proveedores de infraestructura como servicio (IaaS) si se cumplen todos los requisitos de compatibilidad. En el caso de los proveedores que aprovisionan máquinas virtuales, estos requisitos incluyen asegurarse de que el hipervisor que se usa para las máquinas virtuales de Exchange sea totalmente compatible y que la infraestructura que usará Exchange cumpla los requisitos de rendimiento que se determinaron durante el proceso de tamaño. Si todos los volúmenes de almacenamiento que se utilizan para las bases de datos de Exchange y los registros de transacciones de base de datos (incluidas las bases de datos de transporte) están configurados para el almacenamiento premium de Azure, se admite una implementación de máquinas virtuales de Microsoft Azure.



  - La máquina virtual invitada de Exchange tiene las siguientes condiciones:
    
      - Está ejecutando Exchange 2013.
    
      - Se implementa en Windows Server 2008 R2 SP1 (o versiones posteriores), en Windows Server 2012 o en Windows Server 2012 R2.

Para implementaciones de Exchange 2013:

  - Todos los roles de servidor Exchange 2013 son compatibles con una máquina virtual.

  - Las máquinas virtuales del servidor Exchange (incluidas las máquinas virtuales de buzones de correo de Exchange que forman parte de un grupo de disponibilidad de base de datos o DAG), pueden combinarse con la tecnología de migración y agrupación en clústeres de conmutación por error basada en host, siempre que las máquinas virtuales estén configuradas de tal modo que no guarden ni restauren el estado del disco si se mueven o desconectan. Toda la actividad de conmutación por error que se produzca a nivel hipervisor debe dar lugar a un arranque frío cuando la máquina virtual está activada en el nodo de destino. Todas las migraciones planeadas deben dar lugar al apagado y arranque frío, o bien a una migración en línea que use alguna tecnología como la migración en vivo de Hyper-V. El proveedor del hipervisor admite la migración del hipervisor de máquinas virtuales; por lo tanto, debe asegurarse de que el proveedor del hipervisor haya probado y admita la migración de máquinas virtuales de Exchange. Microsoft admite la migración en vivo de Hyper-V de estas máquinas virtuales.

  - En la máquina host física solamente se puede implementar software de administración (por ejemplo, software antivirus, software de copia de seguridad o software de administración de máquinas virtuales). No se puede instalar ninguna otra aplicación basada en servidor (por ejemplo, Exchange, SQL Server, Active Directory, o SAP) en la máquina host. La máquina host se debe destinar a la ejecución de máquinas virtuales invitadas.

  - Algunos hipervisores no incluyen características para la creación de instantáneas de máquinas virtuales. Las instantáneas de máquinas virtuales capturan el estado de una máquina virtual durante su ejecución. Esta característica permite tomar varias instantáneas de una máquina virtual y, a continuación, revertir la máquina virtual a cualquiera de sus estados anteriores aplicándole una instantánea. Sin embargo, las instantáneas de máquinas virtuales no son para aplicaciones, y usarlas puede tener consecuencias no intencionadas e inesperadas para la aplicación de un servidor que mantiene datos de estado, como Exchange. Por consiguiente, no se admite la creación de instantáneas de una máquina virtual invitada de Exchange.

  - Muchos productos de virtualización de hardware le permiten especificar el número de procesadores virtuales que deben ser asignados a cada máquina virtual de invitado. Los procesadores virtuales que se encuentra en la máquina virtual invitada comparten un número fijo de núcleos de procesador físicos en el sistema físico. Exchange es compatible con una proporción de núcleo de procesador a procesador físico virtual no superior a 2:1, aunque se recomienda una proporción de 1:1. Por ejemplo, un sistema de procesador dual con procesadores de núcleo cuádruple contiene un total de 8 núcleos de procesador físico en el sistema host. En un sistema con esta configuración, no asignar más de un total de 16 procesadores virtuales a todas las máquinas virtuales de invitado combinados.

  - Al calcular el número total de procesadores virtuales que necesita la máquina host, también se deben tener en cuenta los requisitos de E/S y del sistema operativo. En la mayoría de los casos, el equivalente al número de procesadores virtuales necesarios en el sistema operativo host para un sistema que hospeda máquinas virtuales de Exchange es 2. Este valor se debe usar como línea base para el procesador virtual del sistema operativo host al calcular la proporción general entre núcleos físicos y procesadores virtuales. Si la supervisión del rendimiento del sistema operativo host indica que se está consumiendo más capacidad de procesador que la equivalente a dos procesadores, el número de procesadores virtuales asignados a las máquinas virtuales invitadas se debe reducir en consecuencia y se debe comprobar que la proporción global entre procesadores virtuales y núcleos físicos no sea superior a 2:1.

  - El sistema operativo de una máquina invitada de Exchange debe usar un disco con un tamaño mínimo de 15 gigabytes (GB) más el tamaño de la memoria virtual asignada a la máquina invitada. Este requisito es necesario para hacer frente a los requisitos de disco del sistema operativo y del archivo de paginación. Por ejemplo, si la máquina invitada tiene asignados 16 GB de memoria, el espacio de disco mínimo necesario para el disco del sistema operativo es de 31 GB.
    
    Además, es posible que las máquinas virtuales invitadas no se puedan comunicar directamente con el canal de fibra o los adaptadores de bus host SCSI (HBA) instalados en la máquina host. En este caso, se deben configurar los adaptadores del sistema operativo de la máquina host y presentar los números de la unidad lógica (LUN) a máquinas virtuales invitadas como un disco virtual o un disco de acceso directo.

  - La única forma admitida de enviar mensajes de correo a dominios externos desde recursos de procesos de Azure es a través de la retransmisión SMTP (también conocida como host inteligente SMTP). El recurso de procesos de Azure envía el correo electrónico a la retransmisión SMTP y después el proveedor de la retransmisión SMTP entrega el correo al dominio externo. Microsoft Exchange Online Protection es un proveedor de retransmisión SMTP, pero también existen otros proveedores de terceros. Para más información, consulte la publicación del blog del equipo de soporte técnico de Microsoft Azure [Enviar correo desde recursos de procesos de Azure a dominios externos](https://go.microsoft.com/fwlink/p/?linkid=799723).

Volver al principio

## Requisitos de almacenamiento de las máquinas host

Los requisitos de espacio mínimo en disco para las máquinas host son los siguientes:

  - Las máquinas host de algunas aplicaciones de virtualización de hardware pueden necesitar espacio de almacenamiento para un sistema operativo y sus componentes. Por ejemplo, al ejecutar Windows Server 2008 R2 con Hyper-V, necesitará un mínimo de 10 GB para cumplir los requisitos para Windows Server 2008. Para obtener más detalles, vea [Requisitos de sistema de Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=125378). También se requiere espacio de almacenamiento adicional para admitir el archivo de paginación del sistema operativo, el software de administración y los archivos de recuperación tras bloqueo (volcado).

  - Algunos hipervisores mantienen archivos en la máquina host que son exclusivos de cada máquina virtual invitada. Por ejemplo, en un entorno Hyper-V, se crea y se mantiene un archivo de almacenamiento de memoria temporal (archivo BIN) para cada máquina invitada. El tamaño de cada archivo BIN es igual a la cantidad de memoria asignada a la máquina invitada. Además, se pueden haber creado y mantenido otros archivos en la máquina host para cada máquina invitada.

  - Si su equipo host ejecuta Windows Server 2012 Hyper-V o Hyper-V 2012, y está configurando un clúster de conmutación por error basado en host que hospedará servidores de buzones de correo de Exchange en un grupo de disponibilidad de bases de datos, recomendamos seguir las instrucciones documentadas en el artículo de Microsoft Knowledge Base [2872325, sobre la posibilidad de que no se puedan crear o unir los nodos de clústeres invitados en Hyper-V](https://support.microsoft.com/kb/2872325).

Volver al principio

## Requisitos de almacenamiento de Exchange

Los requisitos de almacenamiento para un servidor Exchange virtualizado son los siguientes:

  - Cada máquina virtual de Exchange debe tener asignado suficiente espacio de almacenamiento en la máquina host para el disco fijo que contiene el sistema operativo invitado, para los archivos de almacenamiento de memoria temporal que estén en uso y para los archivos de máquinas virtuales relacionados hospedados en la máquina host. Además, para cada máquina invitada de Exchange, debe tener suficiente espacio para las colas de mensajes así como para el almacenamiento suficiente para las bases de datos y los archivos de registro de los servidores de buzones de correo.

  - El almacenamiento usado por el equipo invitado de Exchange para el almacenamiento de datos de Exchange (por ejemplo, colas de transporte y bases de datos de buzones de correo) puede ser un almacenamiento virtual de un tamaño fijo (por ejemplo, discos duros virtuales fijos \[VHD o VHDX\] en un entorno Hyper-V), almacenamiento virtual dinámico cuando se usan archivos VHDX con Hyper-V, almacenamiento a través de SCSI o almacenamiento SCSI en Internet (iSCSI). El almacenamiento de acceso directo es un tipo de almacenamiento configurado en el host y destinado a una máquina invitada. Todo el almacenamiento que use una máquina invitada de Exchange para el almacenamiento de datos de Exchange deberá ser almacenamiento a nivel de bloque, ya que Exchange 2013 no es compatible con el uso de volúmenes de almacenamiento conectado a la red (NAS) que no sean en el escenario SMB 3.0 que se indica más adelante en este tema. Además, no se admite el almacenamiento NAS presentado al invitado como almacenamiento a nivel de bloque mediante hipervisor.

  - Los discos virtuales dinámicos o fijos se pueden almacenar en archivos de SMB 3.0 aquí con el soporte del almacenamiento a nivel de bloque si la máquina invitada se ejecuta en un Windows Server 2012 Hyper-V (o una versión posterior de Hyper-V). El único uso compatible de los recursos compartidos del archivo SMB 3.0 es para el almacenamiento de discos virtuales dinámicos o fijos. Estas comparticiones de discos no se pueden usar para el almacenamiento directo de los datos de Exchange. Al usar los recursos compartidos de archivos SMB 3.0 para almacenar discos virtuales dinámicos o fijos, el almacenamiento que proporciona compatibilidad al archivo se debería configurar para una alta disponibilidad, a fin de garantizar la mejor disponibilidad posible del servicio de Exchange.

  - El almacenamiento usado por Exchange se debe hospedar en ejes de disco independientes del almacenamiento que hospeda el sistema operativo de la máquina virtual.

  - Se admite la configuración de almacenamiento iSCSI para usar un iniciador iSCSI en una máquina virtual invitada de Exchange. Sin embargo, el rendimiento será inferior en esta configuración si la pila de red dentro de la máquina virtual no tiene todas las características (por ejemplo, no todas las pilas de red virtuales admiten tramas gigantes).

Volver al principio

## Requisitos y recomendaciones de memoria para Exchange

Algunos hipervisores tienen la capacidad de suscribir en exceso o ajustar de forma dinámica la cantidad de memoria disponible para una máquina invitada específica en función del uso de memoria percibido en la máquina invitada en comparación con las necesidades de otras máquinas invitadas administradas por el mismo hipervisor. Esta tecnología es útil para cargas de trabajo en las que se necesita la memoria por períodos cortos de tiempo y que luego se puede liberar para otros usuarios. Sin embargo, no es útil para cargas de trabajo que están diseñadas para usar la memoria de forma regular y constante. Exchange, como muchas aplicaciones de servidor con optimizaciones para rendimiento que conllevan el almacenamiento de datos en la memoria caché, es susceptible a un rendimiento bajo del sistema y a una experiencia del cliente inaceptable si no tiene control completo sobre la memoria asignada a la máquina física o virtual en la que se está ejecutando. Como resultado, el uso de características de memoria dinámica en Exchange no es compatible.

Volver al principio

## Migración y agrupación en clústeres de conmutación por error basada en host para Exchange

A continuación, se responden las preguntas más frecuentes sobre la tecnología de agrupación en clústeres de conmutación por error basada en host con DAG de Exchange 2013:

  - **¿Admite Microsoft una tecnología de migración de terceros?**
    
    Microsoft no puede realizar afirmaciones respecto de la compatibilidad con la integración de hipervisores de terceros mediante el uso de estas tecnologías con Exchange, ya que no forman parte del Programa de validación de virtualización del servidor (SVVP). El programa SVVP abarca otros aspectos de la compatibilidad de Microsoft con hipervisores de terceros. Asegúrese de que su proveedor de hipervisores admite la combinación de su tecnología de agrupación en clústeres y migración con Exchange. Si su proveedor de hipervisores admite su tecnología de migración con Exchange, Microsoft admitirá Exchange con la tecnología de migración del proveedor.

  - **¿Cómo define Microsoft la agrupación en clústeres de conmutación por error basada en host?**
    
    La agrupación en clústeres de conmutación por error basada en host se refiere a cualquier tecnología que proporcione una capacidad automática para reaccionar a los errores a nivel de host e iniciar las máquinas virtuales afectadas en servidores alternativos. Se admite el uso de esta tecnología siempre que, en un escenario de error, la máquina virtual se inicie a partir de un arranque en frío en el host alternativo. Con esta tecnología, se garantiza que la máquina virtual no se active nunca desde un estado guardado que persista en el disco porque será un relativo obsoleto para el resto de miembros del grupo de disponibilidad de base de datos.

  - **¿Qué entiende Microsoft por soporte de migración?**
    
    Por tecnología de migración se entiende cualquier tecnología que permita un movimiento planificado de una máquina virtual de un equipo host a otro. Este movimiento también podría ser un movimiento automático que ocurre como parte del equilibrio de carga de recursos, aunque no está relacionado con un error en el sistema. Las migraciones se admiten siempre que las máquinas virtuales no se inicien a partir de un estado guardado que persista en el disco. Esto significa que con Exchange se admite la tecnología que mueve una máquina virtual mediante el transporte del estado y de la memoria de la máquina virtual por la red sin tiempo de inactividad perceptible. Un proveedor de hipervisores de terceros debe ofrecer compatibilidad con la tecnología de migración, a la vez que Microsoft ofrece compatibilidad con Exchange cuando se use en esta configuración.

Volver al principio

