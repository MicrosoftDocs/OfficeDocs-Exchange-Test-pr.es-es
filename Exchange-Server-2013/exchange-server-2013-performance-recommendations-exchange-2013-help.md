---
title: 'Recomendaciones de rendimiento para Exchange Server 2013: Exchange 2013 Help'
TOCTitle: Recomendaciones de rendimiento para Exchange Server 2013
ms:assetid: 6d0aea68-10d5-4a18-b632-a814ce3daa43
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn879084(v=EXCHG.150)
ms:contentKeyID: 63895112
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recomendaciones de rendimiento para Exchange Server 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

El ajuste del rendimiento y la solución de problemas de Exchange Server 2013 es más eficaz cuando el entorno ha sido correctamente dimensionado y planeado. Aunque Exchange 2013 se ha diseñado para simplificar la infraestructura subyacente de recursos, aún puede consumir una gran cantidad de recursos del sistema, tales como memoria, capacidad de almacenamiento y capacidad de la CPU.

Los artículos de esta sección han sido redactados por el equipo de rendimiento de Exchange. Contienen los conocimientos del grupo de productos de Exchange, así como los procedimientos recomendados aprendidos a partir de los casos de soporte de clientes. El objetivo de estos artículos es ayudar a comprender el impacto de los cambios incorporados en Exchange 2013 y la importancia de dimensionar correctamente la infraestructura de Exchange 2013. Hemos incluido también las optimizaciones recomendadas y una guía para identificar problemas de rendimiento.

## Cambios en la arquitectura en Exchange 2013 y otros recursos

Los cambios en la arquitectura en Exchange 2013 ya están documentados en TechNet y en el [Blog del equipo de Exchange](https://go.microsoft.com/fwlink/p/?linkid=35786). Primero nos detendremos en algunos cambios generales que debe tener en cuenta para comprender mejor el costo para el rendimiento y el dimensionamiento. Después hemos incluido una lista de referencias recomendadas que ofrecen más contexto e información sobre estas áreas importantes.


> [!NOTE]
> Consulte <A href="exchange-2013-virtualization-exchange-2013-help.md">Virtualización de Exchange 2013</A> para obtener una guía de optimización del rendimiento al implementar Exchange Server 2013 en un entorno virtualizado.



En Exchange 2013, el rol de servidor Acceso de cliente es un servidor proxy sin estado. Ahora, la principal responsabilidad del rol de servidor Acceso de cliente es autenticar las solicitudes entrantes y, después, derivar cada solicitud al servidor de buzones apropiado, el que hospede la copia activa del buzón del usuario. Esto significa que ya no es necesario configurar la afinidad entre el servidor de acceso de cliente y el equilibrador de carga para protocolos específicos.

Otro cambio destacable en Exchange 2013 es el almacén de información. Ahora, el almacén de información se compone de dos tipos de procesos: host y trabajo. Cada instancia de base de datos está asociada a su propio proceso Microsoft.Exchange.Store.Worker.exe. Esto permite aislar mejor los problemas de las bases de datos problemáticas y puede reducir el impacto sobre el rendimiento de un problema de base de datos a solo la instancia de trabajo de esa base de datos.

El servicio de replicación de Microsoft Exchange es responsable de todos los servicios de alta disponibilidad relacionados con el rol de servidor de buzones de correo. Este servicio de replicación hospeda el componente Active Manager, que es responsable de supervisar los errores y realizar acciones correctivas.

En [Arquitectura de los roles de servidor de Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=523735) encontrará una excelente publicación sobre los cambios de arquitectura, incluido el impacto del redimensionamiento de un entorno de Exchange 2013 desde versiones anteriores.

En los siguientes artículos encontrará más información acerca de los cambios de arquitectura de Exchange 2013, así como información sobre otras áreas pertinentes:

[Arquitectura de Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523769)

[Planear correctamente: escenarios de dimensionamiento de Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523773)

[Supervisar y ajustar el rendimiento de Microsoft Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523774)

[Implementar Exchange Server 2013: (01) Actualizar e implementar Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523775)

[Implementar Exchange Server 2013: (02) Planear correctamente: dimensionamiento de Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523776)

[Implementar Exchange Server 2013: (03) Procedimientos recomendados para la virtualización de Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523777)

[Implementar Exchange Server 2013: (04) Arquitectura de Exchange: alta disponibilidad y resistencia de sitios](https://go.microsoft.com/fwlink/p/?linkid=523779)

[Implementar Exchange Server 2013: (05) Conectividad de Outlook](https://go.microsoft.com/fwlink/p/?linkid=523781)

[La arquitectura preferida](https://go.microsoft.com/fwlink/p/?linkid=523782)

[Rol de servidor Acceso de cliente de Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=386373)

[Procedimientos recomendados para la virtualización de Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523783)

[Equilibrio de carga](load-balancing-exchange-2013-help.md)

[Actualizaciones de Exchange Server: números de compilación y fechas de lanzamiento](https://technet.microsoft.com/es-es/library/hh135098\(v=exchg.150\))

[Notas de la versión de Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md)

[Actualizaciones para Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)

[Uso de subprocesos de ASP.NET en IIS 7.5, IIS 7.0 e IIS 6.0](https://go.microsoft.com/fwlink/p/?linkid=169626)

