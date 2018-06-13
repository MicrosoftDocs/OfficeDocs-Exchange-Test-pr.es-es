---
title: 'Factores de rendimiento y procedimientos recomendados para migraciones híbridas: Exchange 2013 Help'
TOCTitle: Factores de rendimiento y procedimientos recomendados para migraciones híbridas
ms:assetid: 120a7832-d2d3-47d7-b305-918360c2ef66
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt483789(v=EXCHG.150)
ms:contentKeyID: 70118020
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Factores de rendimiento y procedimientos recomendados para migraciones híbridas

 

_**Se aplica a:**Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Existen varias rutas para migrar datos de una organización de correo electrónico local a Office 365. Al planificar una migración a Office 365, suelen surgir dudas sobre cómo mejorar el rendimiento de la migración de datos y optimizar la velocidad de migración. Este artículo describe el rendimiento de la migración para implementaciones híbridas de Exchange. Para obtener información de rendimiento sobre otros métodos de migración, consulte [Prácticas recomendadas y rendimiento de la migración de Office 365](http://go.microsoft.com/fwlink/p/?linkid=623651).

## Factores de rendimiento y procedimientos recomendados para migraciones híbridas

La migración de implementaciones híbridas permite una migración sin problemas entre servidores de Exchange locales y Exchange Online en Office 365.

La migración de implementaciones híbridas es, con diferencia, el método más rápido para migrar datos de buzones de correo a Office 365. Se observó una capacidad de proceso de hasta 100 GB/hora durante implementaciones de clientes reales. La siguiente tabla incluye una lista de factores que influyen en los escenarios de migración híbrida nativos de Office 365.

Si su entorno local contiene varios sitios en ubicaciones geográficamente dispersas, puede crear extremos de migración geográficamente próximos para mejorar el rendimiento de la migración. En estos casos, la migración usa la red de Microsoft en lugar de un extremo de migración centralizado que usa su red local.

## Factor 1: Origen de datos (Exchange Server)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Lista de comprobación</th>
<th>Descripción</th>
<th>Procedimientos recomendados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Rendimiento del sistema</p></td>
<td><p>La extracción de datos es una tarea intensiva. El sistema de origen debe disponer de los recursos suficientes, como memoria y tiempo de CPU, para proporcionar el mejor rendimiento de migración. En el momento de la migración, el sistema de origen suele estar casi al máximo de capacidad para atender la carga de trabajo normal del usuario final; la carga adicional de la migración a veces desactiva el acceso del usuario final por la falta de recursos del sistema.</p></td>
<td><p>Supervise el rendimiento del sistema durante una prueba piloto de migración. Si el sistema está ocupado, le recomendamos evitar una programación de migraciones agresiva para el sistema determinado porque es posible que la migración se vea ralentizada y haya problemas con la disponibilidad del servicio. De ser posible, mejore el rendimiento del sistema de origen agregando recursos de hardware y reduciendo la carga del sistema trasladando tareas y usuarios a otros servidores que no participen en la migración.</p>
<p>Para obtener más información, vea:</p>
<ul>
<li><p><a href="http://go.microsoft.com/fwlink/?linkid=723566">Ask the Perf Guy: Sizing Exchange 2016 Deployments (Ajustar el tamaño de las implementaciones de Exchange 2016)</a></p></li>
<li><p><a href="https://technet.microsoft.com/es-es/library/jj150551(v=exchg.150)">Rendimiento y mantenimiento del servidor</a></p></li>
<li><p><a href="http://technet.microsoft.com/es-es/library/dd351192.aspx">Descripción del rendimiento de Exchange 2010</a></p></li>
</ul>
<p>Cuando se realice una migración desde una organización de Exchange local donde hay múltiples servidores de buzones de correo y múltiples bases de datos, recomendamos crear una lista de usuarios de migración que se distribuya uniformemente entre los múltiples servidores de buzones de correo. Basándose en el rendimiento de cada servidor, la lista puede optimizarse aún más para maximizar la capacidad de proceso.</p>
<p>Por ejemplo, si el servidor A tiene un 50% más de disponibilidad de recursos que el servidor B, es comprensible que haya un 50% más de usuarios del servidor A en el mismo lote de migración. Se pueden aplicar procedimientos similares a otros sistemas de origen.</p>
<p>Realice las migraciones cuando los servidores tengan la mayor disponibilidad de recursos posible, como puede ser después del horario laboral o en fines de semana y durante días festivos.</p></td>
</tr>
<tr class="even">
<td><p>Tareas de back-end</p></td>
<td><p>Otras tareas de back-end que se ejecutan durante el proceso de migración. Debido a que realizar las migraciones después del horario laboral es un procedimiento recomendado, también es típico que las migraciones entren en conflicto con otras tareas de mantenimiento que se están ejecutando en los servidores locales, como las copias de seguridad de datos.</p></td>
<td><p>Revise las otras tareas del sistema que pueden estar ejecutándose durante la migración. Recomendamos que las migraciones se lleven a cabo cuando no se estén ejecutando otras tareas de uso intensivo de recursos.</p>
<p><strong>Nota</strong> Para los clientes que usen Microsoft Exchange local, las tareas de back-end comunes son soluciones de copia de seguridad y el <a href="http://technet.microsoft.com/es-es/library/aa996226(exchg.65).aspx">Mantenimiento del almacén de Exchange</a>.</p></td>
</tr>
</tbody>
</table>


## Factor 2: Servidor de migración

La migración de implementaciones híbridas es un método de migración de extracción e inserción de datos iniciado en la nube, y un servidor híbrido de Exchange actúa como el servidor de migración. A menudo esto no se tiene en cuenta y los clientes usan una máquina virtual de baja escala como servidor híbrido. Esto empobrece el rendimiento de la migración.

**Procedimiento recomendado**

Además de aplicar los procedimientos recomendados descritos anteriormente, probamos los siguientes procedimientos recomendados que mejoraron el rendimiento de la migración en migraciones de clientes reales:

  - Use máquinas físicas de tipo servidor potentes en lugar de máquinas virtuales para los servidores híbridos de Exchange.

  - Use múltiples servidores híbridos que estén detrás del equilibrador de carga de la red del cliente.

Por ejemplo, en migraciones de clientes reales, se logró una capacidad de proceso constante de 30 GB/hora con la configuración siguiente:

  - **Red** Canalización saliente de 500 MB a Internet. La red interna es de 1 GB, con una red troncal de fibra óptica de 10 GB.

  - **Hardware** Las especificaciones para los dos servidores de acceso de cliente/concentrador (físicos) son las siguientes:
    
      - CPU: Intel® Xeon® CPU E5520 de 2,27 GHz 2,26 GHz (2 procesadores).
    
      - RAM: 24 GB.
    
      - Discos: Ocho de 146 GB por disco. Configuración de volumen RAID-5 = 960 GB de espacio total no asignado.

  - **MRSProxy** Está configurado con una simultaneidad de 100.

## Factor 3: Motor de migración

La migración de implementaciones híbridas usa herramientas nativas de Office 365. Está sujeta a la limitación del servicio de migración de Office 365.

**Exchange 2003 frente a las versiones posteriores de Exchange**

Existe una diferencia clave en la experiencia del usuario final cuando se realiza la migración desde Exchange 2003. A diferencia de las versiones posteriores de Exchange, los usuarios finales de Exchange 2003 no pueden acceder a los buzones de correo cuando se están migrando los datos. Por lo tanto, para los clientes de Exchange 2003 suele ser más importante cuándo programar las migraciones y el tiempo que tardan en llevarse a cabo, especialmente cuando el rendimiento de la migración es bajo porque el tamaño del buzón de correo es muy grande o porque la red es muy lenta.

Asimismo, la migración de Exchange 2003 es muy susceptible a interrupciones. Por ejemplo, en migraciones de clientes reales, durante la migración de un buzón de correo de 10 GB ocurrió un incidente del servicio cuando se había completado el 50 % del proceso. Fue necesario reiniciar el servidor de acceso de cliente de Office 365 que procesaba la migración de datos para resolver el problema. En este caso, fue necesario reiniciar la migración de dicho buzón de correo, lo que implicó que el cliente tuvo que volver a migrar los 10 GB de datos. No fue posible reanudar la migración desde el punto en el que se detuvo. Sin embargo, Exchange 2010 y las versiones posteriores de Exchange tienen la capacidad de reanudar las migraciones después de sufrir interrupciones.

**Procedimiento recomendado**

Algunos clientes prefieren hacer migraciones de dos saltos para buzones de Exchange 2003 más grandes y sensibles:

  - **Primer salto** Migración de buzones de correo de Exchange 2003 a un servidor de Exchange 2010 o posterior, que suele ser el servidor híbrido. El primer salto es un movimiento sin conexión, pero suele ser una migración muy rápida a través de una red local.

  - **Segundo salto**. Migración de buzones de correo de Exchange 2010 o posterior a Office 365.

El segundo salto es un movimiento en línea, lo que proporciona una mejor experiencia del usuario y tolerancia a errores. Este enfoque de dos saltos necesita una licencia de Exchange para el buzón de correo local temporal del usuario.

**Proxy del servicio de replicación de buzones (MRSProxy)**

El proxy MRS es la característica de migración local que colabora con el servicio de replicación de buzones de correo del lado de Office 365. Para obtener más información, vea la [Descripción de solicitudes de movimiento](http://technet.microsoft.com/es-es/library/dd298174.aspx)

**Procedimiento recomendado**

Se puede configurar el número máximo de conexiones de MRSProxy para el servidor híbrido de Exchange local. Ejecute el siguiente comando de Windows PowerShell.

    Set-WebServicesVirtualDirectory -Identity "EWS (Default Web Site)" -MRSMaxConnections <number between 0 and unlimited; default is 100>


> [!NOTE]
> En la mayor parte de las migraciones de cliente no es necesario cambiar el valor predeterminado de MRSMaxConnections. Si necesita proteger el servidor de origen para que no se colapse con la carga de la migración, puede reducir el número de conexiones. Esta configuración se realiza en cada servidor MRSProxy. Si el cliente tiene dos servidores MRSProxy, cada uno con 10&nbsp;conexiones, el número de conexiones MRSProxy que recibirán será de 20 (2x10). Para obtener más información sobre cómo configurar el servicio MRSProxy en la organización Exchange 2010 local, vea <A href="http://technet.microsoft.com/es-es/library/ee732395.aspx">Iniciar el servicio MRSProxy en un servidor de acceso de cliente remoto</A>.



## Factor 4: Red

**Pruebas de comprobación**

Los clientes que utilizan Exchange 2010 o versiones posteriores pueden probar el rendimiento de la red en las migraciones híbridas realizando múltiples migraciones de buzones de prueba. Si no, también se pueden migrar buzones de usuarios reales con la opción “-SuspendWhenReadyToComplete” para obtener una indicación del rendimiento de la migración. Cuando finalice la prueba, elimine la solicitud de movimiento para que no influya en los usuarios finales.

Para obtener más información acerca de las solicitudes de traslado, consulte [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

## Factor 5: Servicio de Office 365

La limitación basada en el estado de los recursos de Office 365 influye en las migraciones que usan migraciones de implementaciones híbridas de Office 365. Vea la sección Limitación basada en el estado de los recursos de Office 365 para obtener más información.

