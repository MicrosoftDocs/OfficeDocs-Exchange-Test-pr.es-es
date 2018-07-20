---
title: 'Recomendaciones de configuración y dimensionamiento de Exchange 2013: Exchange 2013 Help'
TOCTitle: Recomendaciones de configuración y dimensionamiento de Exchange 2013
ms:assetid: 4c4ba2fc-014a-46fb-949a-2dabba92c4a5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn879075(v=EXCHG.150)
ms:contentKeyID: 63892249
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recomendaciones de configuración y dimensionamiento de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-03-27_

Exchange 2013 consume más recursos del sistema que otras versiones anteriores de Exchange. Para establecer las bases de una implementación de rendimiento óptimo, debe dimensionar correctamente la infraestructura de Exchange 2013 y, después, aplicar algunas configuraciones recomendadas a los componentes relacionados con Exchange dentro de esa infraestructura.

## Dimensionamiento de Exchange 2013

Dimensionar correctamente el tamaño de Exchange 2013 es una de las maneras más eficaces de evitar problemas de rendimiento. La calculadora de requisitos del rol de servidor de Exchange 2013 está [disponible aquí](https://go.microsoft.com/fwlink/p/?linkid=523844). La versión más reciente es la 6.6, pero le recomendamos que compruebe periódicamente si hay actualizaciones. Para usar esta calculadora correctamente, consulte las entradas de blog sobre la [calculadora de requisitos del rol de servidor de Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=386677) y sobre cómo [dimensionar las implementaciones de Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=301990).

Es importante empezar con la calculadora antes de adquirir e implementar el hardware; en primer lugar, debe determinar los requisitos generales de recursos según los resultados de la calculadora. Puede usar la calculadora para indicar las demandas de su organización y utilizar los resultados para obtener instrucciones sobre cómo escalar el hardware. La calculadora no le indica cuántos servidores debe usar, pero le permitirá calcular el impacto de una carga de trabajo de Exchange en un determinado conjunto de servidores. Debe probar con distintas configuraciones para ver cómo afecta al rendimiento y poder satisfacer las necesidades de hardware y de empresa específicas de su entorno.

Para simplificar las implementaciones y obtener el mejor uso del hardware, el grupo de productos Exchange recomienda servidores de varios roles. El uso de servidores de varios roles proporciona mejor disponibilidad en el nivel del servidor de acceso de cliente (CAS) porque hay disponibles más servidores de acceso de cliente para administrar las solicitudes durante un escenario de error. Un aspecto clave del diseño de Exchange 2013 es utilizar servidores "más pequeños" (de escalado horizontal en lugar de escalado vertical). El diseño y las pruebas se realizaron con dos equipos de socket que contienen hasta veinte núcleos de procesador, con hasta 96 gigabytes (GB) de RAM. Si su hardware es mayor, debe tener en cuenta otras opciones, por ejemplo, usar ese hardware para otras necesidades y comprar servidores más pequeños para su entorno de Exchange 2013, o virtualizar.

Es preferible crear más servidores (escalado horizontal) que agregar recursos a los servidores existentes más grandes (escalado vertical). El escalado horizontal permite que su entorno aproveche las características de alta disponibilidad integradas en Exchange 2013. Para comprender por qué se recomienda esta configuración, revise en detalle las publicaciones sobre [la arquitectura preferida](https://go.microsoft.com/fwlink/p/?linkid=523782) y el [impacto de la resistencia de sitios en la disponibilidad](https://go.microsoft.com/fwlink/p/?linkid=523845).

La calculadora no tiene en cuenta productos de terceros que se ejecutan en los servidores Exchange, ni productos que interactúan con Exchange (incluidas las aplicaciones desarrolladas internamente), lo que significa que debe asegurarse de tenerlos en cuenta durante el dimensionamiento. Por ejemplo, Lync Server, las aplicaciones de servicios web de Exchange (EWS) de terceros y los dispositivos ActiveSync pueden aumentar significativamente los requisitos de CPU por usuario. Puede hacer referencia a la documentación del producto de terceros para obtener información sobre cómo afectará a Exchange. Se recomienda establecer los valores de referencia de rendimiento de Exchange antes de implementar soluciones de terceros.

## Configuraciones de rendimiento recomendadas

Se recomiendan las siguientes optimizaciones de rendimiento para su entorno de Exchange 2013.

## Alimentación

Configure el BIOS para que el sistema operativo (SO) administre la energía.

En el sistema operativo, active el plan de energía de alto rendimiento.

## Proceso

Desactive la característica hyper-threading en los servidores físicos de Exchange. Si está virtualizando, puede habilitarse hyper-threading en el servidor físico, pero solo se debe asignar el número necesario de CPU virtuales a cada servidor virtual (no asignar las CPU virtuales en exceso) y utilizar solo el número de núcleos de procesador físicos para los cálculos de dimensionamiento.

En Exchange Server 2013 Service Pack 1 o posteriores, puede habilitar la descarga de SSL para ayudar a reducir el consumo de CPU en los servidores de acceso de cliente, pero quizás la complejidad de la configuración de la descarga de SSL no compense los beneficios.

## .NET Framework


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Versión de Exchange</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU16</p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU15</p></td>
<td><p> X</p></td>
<td><p>X1,2 </p></td>
<td><p> X</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2013 CU13 y CU14</p></td>
<td> </td>
<td><p>X1,2 </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


1 .NET Framework 4.6.1 requiere revisiones posteriores al lanzamiento si quiere instalarlo en un servidor que ejecute Exchange 2013 CU13. Para obtener más información, vea [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2Si está actualizando a Exchange 2013 CU13, CU14 o CU15 desde Exchange 2013 CU12 o versiones anteriores, se recomienda encarecidamente que instale Exchange 2013 CU13 antes de .NET Framework 4.6.1 y sus revisiones posteriores al lanzamiento.

Si no puede instalar .NET 4.5.2, consulte el artículo 2995145 de Microsoft Knowlege Base "[Problemas de rendimiento o retrasos al conectarse a Exchange Server 2013 que se ejecuta en Windows Server](https://go.microsoft.com/fwlink/p/?linkid=524159)". Las revisiones que aparecen en el artículo se elaboraron a partir de las conclusiones internas sobre el uso de memoria del proceso de trabajo de almacén. Al aplicar estas revisiones, se reduce el consumo de memoria total para todos los procesos administrados (incluido el proceso de trabajo de almacén) y se reducirá el tiempo total de CPU que se dedica a la recolección de elementos no usados de .NET.

## Correcciones

El equipo de rendimiento de Exchange recomienda instalar todas las correcciones siguientes relacionadas con el rendimiento.

  - [Hay disponible una actualización que mejora la resistencia del clúster en Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=524088)

  - [Revisiones y actualizaciones recomendadas para clústeres de conmutación por error basados en Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=524089)

  - [Revisiones y actualizaciones recomendadas para clústeres de conmutación por error basados en Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?linkid=524090)

  - [Asignación incorrecta de procesador RSS en un equipo con Windows 8 o Windows Server 2012 con procesadores de varios núcleos](https://go.microsoft.com/fwlink/p/?linkid=324140)

  - [Problemas de rendimiento o retrasos al conectarse a Exchange Server 2013 que se ejecuta en Windows Server](https://go.microsoft.com/fwlink/p/?linkid=312962)

  - [Problema de conectividad de Outlook si SSLOffloading es "True" en Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=524091)

  - [Conexión del servidor prolongada para Outlook tras una conmutación por error de base de datos en Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=524092)

  - [Rendimiento lento de Outlook Web App cuando Lync se integra con Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=524093)

  - [EMS tarda mucho tiempo en ejecutar el primer comando en un entorno de Exchange Server 2013 con actualización acumulativa 5](https://go.microsoft.com/fwlink/p/?linkid=524094)

  - [Latencia de enrutamiento de mensajes si IPv6 está habilitado en Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=524095)

  - [Uso de CPU elevado por parte de una aplicación que depende de un cliente de LDAP de Microsoft en Windows Server 2008 R2 SP1](https://go.microsoft.com/fwlink/p/?linkid=530287)

  - [El uso de CPU es alto cuando usa RPC mediante el protocolo HTTP en Windows 8.1 o Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?linkid=619127)

## Redes

Con Exchange 2013, se recomienda un único adaptador de red porque ya no es necesario dividir MAPI y las redes de replicación. Vea [Network requirements](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) para más información.

Utilice la configuración predeterminada de descarga de SNP cuando esté disponible y asegúrese de que RSS está habilitado (configuración predeterminada en Windows Server 2012 y versiones posteriores). RSS le ayudará a escalar el uso de la CPU, especialmente en 10GbE.

Compruebe que el sistema operativo no ha desactivado la tarjeta de red para ahorrar energía.

Mantenga actualizados los controladores NIC. Vea mensualmente con su proveedor si hay actualizaciones para los controladores pertinentes.

## Internet Information Services (IIS)

Durante la instalación, Exchange modifica algunos límites de conexión para IIS. Se recomienda no realizar más ajustes en IIS.

Evite las personalizaciones siempre que sea posible. Las actualizaciones de Windows o las actualizaciones acumulativas de Exchange pueden sobrescribir los cambios realizados en web.config o en las claves del Registro.

## Almacenamiento

Las directrices para el almacenamiento de Exchange 2013 están disponibles en [Opciones de configuración de almacenamiento de Exchange 2013](exchange-2013-storage-configuration-options-exchange-2013-help.md).

## Virtualización

Vea [Requirements for hardware virtualization](exchange-2013-virtualization-exchange-2013-help.md). Tenga en cuenta también que Exchange no reconoce el acceso de memoria no uniforme (NUMA). Por lo tanto, se recomienda usar la configuración de NUMA predeterminada del fabricante de hardware.

## Active Directory

Supervise el rendimiento del servidor de directorio, porque las consultas de Active Directory tienen un impacto directo en la implementación de Exchange.

El tiempo de búsqueda de LDAP es un contador fundamental para medir el estado de Active Directory. Supervise la CPU en los controladores de dominio. Los problemas de la CPU en los controladores de dominio se representarán como problema de rendimiento en los servidores de Exchange.

Ejecute el "Diagnóstico de Active Directory" integrado en el controlador de dominio, en el Monitor de rendimiento situado en "Conjunto de recopiladores de datos", para ayudar a aislar a la causa de los problemas de rendimiento del controlador de dominio.

Planee suficiente memoria RAM en los controladores de dominio para poder almacenar en caché el archivo de base de datos completo de AD.

Se recomienda implementar 1 núcleo de catálogo global de Active Directory para cada núcleos de 8 buzones que se encargan de la carga activa (basándose en núcleos de catálogo global de 64 bits).

## Equilibrio de carga

Todos los servidores de acceso de cliente deben recibir aproximadamente el mismo número de conexiones entrantes.

Para todos los protocolos, Exchange 2013 no requiere afinidad de sesión entre un servidor de acceso de cliente determinado y el equilibrador de carga.

Debe usarse un equilibrador de carga de hardware o de software para administrar todo el tráfico entrante a los servidores de acceso de cliente. La selección del servidor de destino se puede determinar con varios métodos, como “round robin”, donde cada conexión entrante pasa al siguiente servidor de destino en una lista circular, o “menor número de conexiones”, donde el equilibrador de carga envía cada nueva conexión al servidor con menos conexiones establecidas en ese momento. Estos métodos se detallan en [Equilibrio de carga](load-balancing-exchange-2013-help.md). También debe considerar lo siguiente:

  - El método "round robin" tiene el problema de una convergencia lenta con conexiones de larga duración (como RPC/HTTP). A medida que haya más equipos nuevos en línea, las conexiones atendidas en los equipos de destino tardarán mucho tiempo en converger.

  - Con el método de "menor número de conexiones", tenga en cuenta que es posible que un servidor de acceso de cliente se sobrecargue y deje de responder durante una interrupción del servidor de acceso de cliente o durante un mantenimiento para aplicación de revisiones. En el contexto del rendimiento de Exchange, la autenticación es una operación costosa.

Debido a una serie de limitaciones con Equilibrio de carga de red (NLB) de Windows en un entorno de Exchange 2013, detalladas en [Equilibrio de carga](load-balancing-exchange-2013-help.md), no se recomienda usar Windows NLB.

## Distribución de la base de datos y de usuarios

Mantenga una distribución equilibrada de usuarios por base de datos y de bases de datos activas por servidor. Distribuya uniformemente el consumo de espacio de disco de base de datos y equilibre los usuarios intensos en todas las bases de datos.

Debe crear el perfil de su base de usuarios para saber cómo interactúan con Exchange (dispositivos, Outlook y OWA) y el impacto que esas interacciones tendrán desde la perspectiva del rendimiento. Para obtener más información sobre cómo crear un perfil del uso de Exchange por usuario, vea los blogs de calculadora de la sección 2.

Configure la preferencia de activación de copia de base de datos y la configuración de "MaximumPreferredActiveDatabases" (por servidor) para mantener el equilibrio durante una conmutación por error o un cambio.

El script RedistributeActiveDatabases.ps1 equilibrará las bases de datos activas entre los nodos del DAG.

Considere la posibilidad de aplicar límites estrictos de número de elementos que coincidan con los de Office 365. Para ello, use el cmdlet Set-Mailbox y la información proporcionada en [Límites de la carpeta de buzón de correo](https://go.microsoft.com/fwlink/p/?linkid=398779).

## Archivo de paginación

Establezca un tamaño máximo para el archivo de paginación de 32778 MB si usa más de 32 GB de RAM.

El archivo de paginación no debería hospedarse en la misma unidad que los archivos de base de datos de Exchange o que los archivos de registro de la base de datos.

Es esencial que utilice un archivo de paginación de tamaño fijo y no permita que Windows administre el tamaño. El crecimiento del archivo de paginación puede ser una tarea que afecta mucho al rendimiento y puede producir problemas cuando Exchange está sobrecargado.

Si necesita obtener un volcado completo del núcleo, use el artículo 969028 de Microsoft Knowledge Base, [Cómo generar un núcleo o un archivo de volcado de memoria completo en Windows Server 2008 y Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=524044) para ver un archivo de volcado específico.

## Modo de Outlook

Se recomienda el modo en caché. Para comprender las ventajas de usar el modo en caché, consulte [Elegir entre los modos caché de Exchange y en línea para Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=524045).

Es importante tener en cuenta que el rendimiento puede verse afectado por los complementos de servidor y por los complementos de terceros de Outlook. Cuando se utiliza el modo en línea, los clientes pueden esperar que haya problemas de rendimiento de los complementos de terceros, recuentos de elementos elevados, vistas restringidas o número de usuarios que acceden al buzón de correo, entre otros factores. Los clientes antiguos pueden experimentar más impacto por los recuentos de elementos elevados y el rendimiento que Outlook 2013.

Si la razón principal para que una organización tenga configurado en modo en línea de Outlook es la seguridad, considere la posibilidad de usar BitLocker en su lugar.

Outlook 2013 ofrece una nueva característica, "Control deslizante de sincronización", para reducir al mínimo el tiempo de descarga y el tamaño del archivo OST. Consulte [Configurar el modo caché de Exchange en Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=390456) para obtener más información.

Compruebe mensualmente si hay actualizaciones de los clientes de Outlook compatibles con su entorno.

## Software de terceros

Como procedimiento recomendado, desinstale o deshabilite el software de terceros mientras soluciona problemas de rendimiento de Exchange. La siguiente lista contiene los tipos de software de terceros que el soporte técnico de Microsoft ha observado con más frecuencia que afectan al rendimiento de Exchange 2013.

  - Soluciones antivirus

  - Software de prevención de intrusiones

  - Software de copia de seguridad

  - Software auditar software, tanto usuarios como archivos

  - Soluciones de archivado

