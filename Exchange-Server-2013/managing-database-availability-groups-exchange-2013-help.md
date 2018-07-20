---
title: 'Administrar grupos de disponibilidad de base de datos: Exchange 2013 Help'
TOCTitle: Administrar grupos de disponibilidad de base de datos
ms:assetid: 74be3f97-ec0f-4d2a-b5d8-7770cc489919
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298065(v=EXCHG.150)
ms:contentKeyID: 48268288
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar grupos de disponibilidad de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-10-04_

Un grupo de disponibilidad de base de datos (DAG) es un conjunto de hasta 16 servidores de buzones de correo de Microsoft Exchange Server 2013 que ofrece recuperación automática en el nivel de base de datos ante un error de base de datos, servidor o red. Los DAG usan replicación continua y un subconjunto de tecnologías de clústeres de conmutación por error de Windows para ofrecer alta disponibilidad y resistencia en los sitios. Los servidores de buzones de correo de un DAG se supervisan mutuamente para detectar errores. Cuando se agrega un servidor de buzones de correo a un DAG, éste trabaja con los demás servidores del DAG para ofrecer recuperación automática de base de datos a partir de errores de base de datos.

Cuando crea un DAG por primera vez, al principio está vacío. Al agregar el primer servidor a un DAG, se crea automáticamente un clúster de conmutación por error para el DAG. Además, se inicia la infraestructura que supervisa los servidores en busca de errores en la red o el servidor. El mecanismo de latidos del clúster de conmutación por error y la base de datos del clúster se usan para administrar la información sobre el DAG que puede cambiar rápidamente (como el estado de montaje de la base de datos, el estado de replicación y la última ubicación de montaje) y para realizar un seguimiento de dicha información.

**Contenido**

Creating DAGs

DAG membership

Configuring DAG properties

DAG networks

Configuring DAG members

Performing maintenance on DAG members

Shutting down DAG members

Installing updates on DAG members

## Cómo crear grupos de disponibilidad de base de datos

Se puede crear un DAG con el Asistente para nuevos grupos de disponibilidad de base de datos en el Centro de administración de Exchange (EAC) o mediante la ejecución del cmdlet **New-DatabaseAvailabilityGroup** en el Shell de administración de Exchange. Cuando cree un DAG, proporcione un nombre para el DAG y establezca una configuración adicional para el servidor y el directorio testigo. Además, puede asignar una o varias direcciones IP al DAG, ya sea usando direcciones IP estáticas o permitiendo que se asignen direcciones IP de forma automática al DAG mediante el Protocolo de configuración dinámica de host (DHCP). Puede asignar direcciones IP de forma manual al DAG mediante el parámetro *DatabaseAvailabilityGroupIpAddresses*. Si omite este parámetro, el DAG intenta obtener una dirección IP usando el servidor DHCP en la red.

Si va a crear un DAG que contendrá servidores de buzones de correo que ejecutan Windows Server 2012 R2, también tiene la opción de crear un DAG sin un punto de acceso administrativo al clúster. En ese caso, el clúster no tendrá un objeto de nombre de clúster (CNO) en Active Directory, y el grupo de recursos principal del clúster no contendrá un recurso de nombre de red o un recurso de dirección IP.

Para obtener instrucciones detalladas acerca de cómo crear un grupo de disponibilidad de base de datos, vea [Crear un grupo de disponibilidad de base de datos](create-a-database-availability-group-exchange-2013-help.md).

Al crear un DAG, en Active Directory se crean un objeto vacío que representa al DAG con el nombre especificado y una clase de objeto **msExchMDBAvailabilityGroup**.

Los DAG utilizan un subconjunto de tecnologías de clústeres de conmutación por error de Windows, como el latido de clúster, las redes de clústeres y la base de datos de clústeres (para almacenar datos que cambian o pueden cambiar rápidamente, por ejemplo, el estado de la base de datos que cambia de activa a pasiva, y viceversa, o de montada a desmontada, y viceversa). Dado que los DAG dependen del clúster de conmutación por error de Windows, solo pueden crearse en los servidores de buzones de correo de Exchange 2013 que ejecutan el sistema operativo Windows Server 2008 R2 Enterprise o Datacenter, o bien los sistemas operativos Windows Server 2012 Enterprise o Datacenter, o Windows Server 2012 R2 Standard o Datacenter.


> [!NOTE]
> El error en el clúster creado y utilizado por el DAG debe ser dedicado a DAG. El clúster no se puede usar para ninguna otra solución de alta disponibilidad ni para cualquier otro fin. Por ejemplo, el error en el clúster no se puede usar para organizar por clústeres otras aplicaciones o servicios. No es compatible el uso de un error en el clúster subyacente de DAG para fines que no son el DAG.



## Servidor testigo de DAG y directorio testigo

Al crear un DAG, se debe especificar un nombre que no supere los 15 caracteres y que sea único dentro del bosque de Active Directory. Además, cada DAG se configura con un servidor testigo y un directorio testigo. El servidor testigo y su directorio se usan solo cuando la cantidad de miembros del DAG es par y con fines de quórum exclusivamente. No es necesario crear un directorio testigo por adelantado. Exchange crea automáticamente y protege el directorio en el servidor testigo. El directorio no debe usarse para ningún fin que no sea para el servidor testigo del DAG.

Los requisitos para el servidor testigo son los siguientes:

  - El servidor testigo no puede ser miembro del DAG.

  - El servidor testigo debe estar en el mismo bosque de Active Directory que el DAG.

  - El servidor testigo debe estar ejecutando una versión compatible de Windows Server. Para obtener más información, consulte [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Un servidor simple puede servir de testigo para varios DAG. Sin embargo, cada DAG requiere su propio directorio testigo.

Independientemente de qué servidor se use como servidor testigo, si Windows Firewall se habilita en el servidor testigo deseado, debe habilitar la excepción de Windows Firewall para Compartir impresoras y archivos.


> [!IMPORTANT]
> Si el servidor testigo especificado no es un servidor Exchange&nbsp;2013 o Exchange 2010, debe agregar el grupo de seguridad universal (USG) del subsistema de confianza de Exchange al grupo de administradores locales en el servidor testigo antes de crear el DAG. Estos permisos de seguridad son necesarios para asegurar que Exchange&nbsp;pueda crear un directorio y compartirlo en el servidor testigo, según sea preciso.<BR>El servidor testigo utiliza el puerto 445 de SMB.



Ni el servidor testigo ni el directorio testigo necesitan ser tolerantes a errores ni usar ningún tipo de redundancia o alta disponibilidad. No es necesario usar un servidor de archivos en clúster para el servidor testigo, ni emplear ninguna otra forma de resistencia para el servidor testigo. Existen varias razones para ello. Con DAG más grandes (por ejemplo, de seis miembros o más) deben producirse varios errores antes de que sea necesario un servidor testigo. Debido a que un DAG de seis miembros puede tolerar hasta dos errores de votante sin perder quórum, se tendrían que producir errores en tres votantes antes de que se necesite un servidor testigo para mantener el quórum. Además, si se produce un error que afecta el servidor testigo actual (por ejemplo, se pierde el servidor testigo debido a un error de hardware), se puede usar el cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)) para configurar un servidor testigo y un directorio testigo nuevos (en caso de tener quórum).


> [!NOTE]
> También se puede usar el cmdlet <STRONG>Set-DatabaseAvailabilityGroup</STRONG> para configurar el servidor testigo y el directorio testigo en la ubicación original si el servidor testigo perdió su almacenamiento o si alguien cambió el directorio testigo o los permisos de los recursos compartidos.



## Consideraciones de ubicación de servidores testigo

La colocación de un servidor testigo de DAG dependerá de los requisitos de su empresa y de las opciones disponibles para su organización. Exchange 2013 admite las nuevas opciones de configuración de DAG que no están recomendadas o que no son posibles en versiones anteriores de Exchange. Estas opciones incluyen el uso de una tercera ubicación, como un tercer centro de datos, una sucursal o una red virtual de Microsoft Azure.

La siguiente tabla muestra recomendaciones generales de colocación de servidores testigo para distintos escenarios de implementación.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Escenario de implementación</th>
<th>Recomendaciones</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Un solo DAG implementado en un solo centro de datos</p></td>
<td><p>Ubicar el servidor testigo en el mismo centro de datos que los miembros de DAG.</p></td>
</tr>
<tr class="even">
<td><p>Un solo DAG implementado en dos centros de datos; no hay ubicaciones adicionales disponibles</p></td>
<td><p>Ubicar el servidor testigo en una red virtual de Microsoft Azure para habilitar la conmutación por error automática del centro de datos. O bien,</p>
<p>Ubicar el servidor testigo en el centro de datos principal.</p></td>
</tr>
<tr class="odd">
<td><p>Varios DAG implementados en un solo centro de datos</p></td>
<td><p>Ubicar el servidor testigo en el mismo centro de datos que los miembros de DAG. Entre las opciones adicionales se incluyen:</p>
<ul>
<li><p>Uso del mismo servidor testigo para varios DAG</p></li>
<li><p>Uso de un miembro de DAG para que actúe como servidor testigo para un DAG testigo</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>Varios DAG implementados en dos centros de datos</p></td>
<td><p>Ubicar el servidor testigo en una red virtual de Microsoft Azure para habilitar la conmutación por error automática del centro de datos. O bien,</p>
<p>Ubicar el servidor testigo en el centro de datos considerado principal para cada DAG. Entre las opciones adicionales se incluyen:</p>
<ul>
<li><p>Uso del mismo servidor testigo para varios DAG</p></li>
<li><p>Uso de un miembro de DAG para que actúe como servidor testigo para un DAG testigo</p>
<p></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Uno o varios DAG implementados en más de dos centros de datos</p></td>
<td><p>En esta configuración, el servidor testigo debe localizarse en el centro de datos donde desee que se encuentre la mayoría de votos por quórum.</p></td>
</tr>
</tbody>
</table>


Si un DAG se ha implementado en dos centros de datos, una nueva opción de configuración en Exchange 2013 debe usar una tercera ubicación para hospedar el servidor testigo. Si su organización tiene una tercera ubicación con una infraestructura de red aislada de fallos de red que afectan a los dos centros de datos en los que ha implementado su DAG, puede implementar el servidor testigo de DAG en esa tercera ubicación, configurando por tanto su DAG con la capacidad de conmutar por error automáticamente las bases de datos en el otro centro de datos en respuesta al evento de error en el centro de datos. Si su organización solo tiene dos ubicaciones físicas, puede utilizar una red virtual de Microsoft Azure como una tercera ubicación para colocar el servidor testigo.

## Especificación de un servidor testigo y un directorio testigo durante la creación de los DAG

Al crear un DAG, debe proporcionar un nombre para el DAG. Además, puede especificar un servidor testigo y un directorio testigo.

Al crear un DAG, estarán disponibles las siguientes combinaciones de opciones y comportamientos:

  - Puede solamente especificar un nombre para el DAG y dejar en blanco los campos **Servidor testigo** y **Directorio testigo**. En este escenario, el asistente busca el sitio local de Active Directory para un servidor de acceso de cliente que no tenga el servidor de buzones de correo instalado, y crea automáticamente el directorio predeterminado (%SystemDrive%:\\DAGFileShareWitnesses\\\<*DAGFQDN*\>) y el recurso compartido predeterminado (\<*DAGFQDN*\>) en ese servidor. Además, usa el servidor de acceso de cliente como servidor testigo. Por ejemplo, piense en un servidor testigo CAS3 en cuya unidad C se ha instalado el sistema operativo en la unidad C. Un DAG denominado DAG1 en el dominio contoso.com usaría el directorio testigo predeterminado C:\\DAGFileShareWitnesses\\DAG1.contoso.com, que se compartiría como \\\\CAS3\\DAG1.contoso.com.

  - Puede especificar un nombre para el DAG, el servidor testigo que desea usar y el directorio que va a crear y compartir en el servidor testigo.

  - Puede especificar un nombre para el DAG y el servidor testigo que desea usar, y dejar en blanco el campo **Directorio testigo**. En este caso, el asistente creará el directorio predeterminado en el servidor testigo especificado.

  - Puede especificar un nombre para el DAG, dejar en blanco el campo **Servidor testigo** y especificar el directorio que va a crear y compartir en el servidor testigo. En este escenario, el asistente busca un servidor de acceso de cliente que no tenga instalado el servidor de buzones de correo y crea automáticamente el DAG especificado en dicho servidor, comparte el directorio y usa ese servidor de acceso de cliente como servidor testigo.

Cuando se forma un DAG, éste inicialmente usará el modelo de quórum Mayoría de nodo. Cuando se agrega el segundo servidor de buzones de correo al DAG, el quórum cambia automáticamente a un modelo de quórum Mayoría de recurso compartido de archivos y nodo. Al producirse este cambio, el clúster del DAG comienza a usar el servidor testigo para mantener el quórum. Si el directorio testigo no existe, Exchange lo crea y lo comparte de forma automática, y lo aprovisiona con permisos de control total para la cuenta del equipo de CNO para el DAG.


> [!NOTE]
> No se admite el uso de un recurso compartido de archivos que forme parte de un espacio de nombres del Sistema de archivos distribuido (DFS).



Si Firewall de Windows está habilitado en el servidor testigo antes de crear el DAG, es posible que bloquee la creación. Exchange usa Instrumental de administración de Windows (WMI) para crear el directorio y el recurso compartido de archivos en el servidor testigo. Si Firewall de Windows está habilitado en el servidor testigo y no hay excepciones de firewall configuradas para WMI, el cmdlet **New-DatabaseAvailabilityGroup** se cierra con un error. Si especifica un servidor testigo y no especifica un directorio testigo, obtiene el siguiente mensaje de error.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>La tarea no pudo crear el directorio testigo predeterminado en el servidor &lt;<em>Nombre del servidor</em>&gt;. Especifique un directorio testigo manualmente.</p></td>
</tr>
</tbody>
</table>


Si especifica un servidor testigo y un directorio testigo, obtiene el siguiente mensaje de advertencia.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>No se puede obtener acceso a los recursos compartidos de archivos en el servidor testigo '<em>nombre de servidor</em>'. Es posible que el grupo de disponibilidad de base de datos sea más vulnerable a errores hasta que se corrija este problema. Puede usar el cmdlet Set DatabaseAvailabilityGroup para intentar la operación de nuevo. Error: No se ha encontrado la ruta de acceso de la red.</p></td>
</tr>
</tbody>
</table>


Si Firewall de Windows está habilitado en el servidor testigo después de crear el DAG pero antes de agregar los servidores, es posible que bloquee las acciones de agregar o quitar miembros del DAG. Si Firewall de Windows está habilitado en el servidor testigo y no hay excepciones de firewall configuradas para WMI, el cmdlet **Add-DatabaseAvailabilityGroupServer** muestra el siguiente mensaje de advertencia.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>No se pudo crear el directorio testigo de recurso compartido de archivos 'C:\DAGFileShareWitnesses\DAG_FQDN' en el servidor testigo <em>nombre de servidor</em>. Es posible que el grupo de disponibilidad de base de datos sea más vulnerable a errores hasta que se corrija este problema. Puede usar el cmdlet Set DatabaseAvailabilityGroup para intentar la operación de nuevo. Error: Se produjo la excepción WMI en el servidor <em>nombre de servidor</em>: el servidor RPC no está disponible. (Excepción de HRESULT: 0x800706BA)</p></td>
</tr>
</tbody>
</table>


Para solucionar el error y las advertencias precedentes, realice una de las siguientes acciones:

  - Cree manualmente el directorio testigo y el recurso compartido en el servidor testigo, y asigne el CNO para el control completo de DAG para el directorio y el recurso compartido.

  - Habilite la excepción de WMI en Firewall de Windows.

  - Deshabilite Firewall de Windows.

Volver al principio

## Pertenencia de DAG

Después de crear un DAG, es posible agregarle o quitarle servidores mediante el Asistente para administrar grupos de disponibilidad de bases de datos en el EAC, o mediante los cmdlets **Add-DatabaseAvailabilityGroupServer** o **Remove-DatabaseAvailabilityGroupServer** en el Shell. Para obtener instrucciones detalladas sobre cómo administrar la pertenencia a un DAG, vea [Administración de la pertenencia a grupos de disponibilidad de base de datos](manage-database-availability-group-membership-exchange-2013-help.md).


> [!NOTE]
> Cada servidor de buzones de correo que pertenezca a un DAG también es un nodo en el clúster subyacente usado por el DAG. Como consecuencia, en cualquier momento, un servidor de buzones de correo puede pertenecer a un solo DAG.



Si el servidor de buzones de correo que se agrega al DAG no tiene instalado un componente de clúster de conmutación por error, el método usado para agregar el servidor (por ejemplo, el cmdlet **Add-DatabaseAvailabilityGroupServer** o el Asistente para administrar grupos de disponibilidad de base de datos) instala la característica de clúster de conmutación por error.

Cuando se agrega el primer servidor de buzones de correo a un DAG, ocurre lo siguiente:

  - Se instala el componente de clúster de conmutación por error de Windows, si aún no se había instalado.

  - Se crea un clúster de conmutación por error usando el nombre del DAG. Este error en el clúster es usado exclusivamente por el DAG, y el clúster debe estar dedicado al DAG. No se admite el uso del clúster para cualquier otro fin.

  - Un CNO se crea en el contenedor de equipos predeterminado.

  - El nombre y la dirección IP del DAG se registran como Host (A) en Sistema de nombres de dominio (DNS).

  - El servidor se agrega al objeto del DAG en Active Directory.

  - La base de datos del clúster se actualiza con información sobre las bases de datos montadas en el servidor agregado.

En un entorno grande o de varios sitios, en especial en los que el DAG se extiende a varios sitios de Active Directory, debe esperar hasta que se complete la replicación de Active Directory en el objeto DAG que contiene el primer miembro del DAG. Si este objeto de Active Directory no se replica en todo el entorno, el agregado del segundo servidor puede ocasionar la creación de un clúster nuevo (y un CNO nuevo) en el DAG. Esto sucede porque el objeto DAG parece estar vacío desde la perspectiva del segundo miembro que se agrega y, por lo tanto, producirá que el cmdlet **Add-DatabaseAvailabilityGroupServer** cree un clúster y un CNO para el DAG, a pesar de que estos objetos ya existen. Para comprobar que el objeto DAG que contiene el primer servidor DAG se haya replicado, use el cmdlet **Get-DatabaseAvailabilityGroup** en el segundo servidor que se agrega a fin de comprobar si el primer servidor que se agregó figura como miembro del DAG.

Cuando se agrega el segundo servidor y los servidores siguientes a un DAG, ocurre lo siguiente:

  - El servidor se une al clúster de conmutación por error de Windows del DAG.

  - El modelo de quórum se ajusta automáticamente:
    
      - El modelo de quórum Mayoría de nodos se usa para los DAG que tienen una cantidad impar de miembros.
    
      - El modelo de quórum Mayoría de recurso compartido de archivos y nodo se usa para los DAG que tienen una cantidad par de miembros.

  - De ser necesario, Exchange crea automáticamente el directorio testigo y el recurso compartido.

  - El servidor se agrega al objeto del DAG en Active Directory.

  - La base de datos del clúster se actualiza con información acerca de las bases de datos montadas.


> [!NOTE]
> El cambio de modelo de quórum debe producirse automáticamente. Sin embargo, si el modelo de quórum no cambia automáticamente al modelo adecuado, puede ejecutar el cmdlet <STRONG>Set-DatabaseAvailabilityGroup</STRONG> solo con el parámetro <EM>Identity</EM> para corregir la configuración de quórum del DAG.



## Preconfiguración del objeto de nombre de clúster para un grupo de disponibilidad de base de datos

El CNO es una cuenta de equipo que se crea en Active Directory y se asocia con el recurso Nombre del clúster. El recurso Nombre del clúster está asociado al CNO, que es un objeto habilitado para Kerberos que actúa como la identidad del clúster y proporciona el contexto de seguridad del clúster. La formación del clúster subyacente del DAG y del CNO de ese clúster se realiza cuando se agrega el primer miembro al DAG. PowerShell remoto se comunica con el servicio de replicación de Microsoft Exchange en el servidor de buzones de correo que se agrega cuando se agrega el primer servidor al DAG. El servicio de replicación de Microsoft Exchange instala la característica de clúster de conmutación por error (si aún no está instalada) y comienza el proceso de creación del clúster. El servicio de replicación de Microsoft Exchange se ejecuta bajo el contexto de seguridad LOCAL SYSTEM y es en este contexto de seguridad donde se realiza la creación del clúster.


> [!WARNING]
> Si sus miembros de DAG se ejecutan en Windows Server 2012, debe ensayar previamente el CNO antes de agregar el primer serviros al DAG. Si los miembros del DAG ejecutan Windows Server 2012 R2 y crea un DAG sin un punto de acceso administrativo al clúster, no se creará ningún CNO y no necesitará crear un CNO para el DAG.



Se puede preconfigurar y aprovisionar el CNO en entornos en los que la creación de la cuenta de equipo está restringida o en los que las cuentas de equipo se crean en un contenedor distinto del contenedor de equipos predeterminado. Se crea una cuenta de equipo para el CNO, se la deshabilita y, a continuación, hay dos alternativas:

  - Asignar el control total de la cuenta de equipo a la cuenta de equipo del primer servidor del buzón de correo que se agrega al DAG.

  - Asignar el control total sobre la cuenta de equipo al grupo de seguridad universal del subsistema de confianza de Exchange.

La asignación del control total sobre la cuenta de equipo a la cuenta de equipo del primer servidor de buzones de correo que agrega al DAG garantiza que el contexto de seguridad LOCAL SYSTEM podrá administrar la cuenta de equipo preconfigurada. Como alternativa, se puede usar la asignación de control total sobre la cuenta de equipo al grupo de seguridad del subsistema de confianza de Exchange porque el grupo del subsistema de confianza de Exchange contiene las cuentas de equipo de todos los servidores de Exchange del dominio.

Para obtener instrucciones detalladas acerca de cómo preconfigurar y aprovisionar el CNO para un DAG, vea [Preconfiguración del objeto de nombre de clúster para un grupo de disponibilidad de base de datos](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

## Cómo eliminar servidores de un DAG

Se pueden quitar servidores de buzones de correo de un DAG mediante el Asistente para administrar grupos de disponibilidad de base de datos en el EAC o el cmdlet **Remove-DatabaseAvailabilityGroupServer** en el Shell. Antes de que sea posible quitar el servidor de buzones de correo de un DAG, se deben quitar del servidor todas las bases de datos de buzones de correo replicadas. Si intenta quitar de un DAG un servidor de buzones de correo con bases de datos de buzones de correo replicadas, se produce un error en la tarea.

Existen escenarios en los que, antes de realizar determinadas operaciones, se debe quitar un servidor de buzones de correo de un DAG. Entre estos escenarios se incluyen lo siguientes:

  - **Ejecución de una operación de recuperación de servidores**   Si un servidor de buzones de correo que es miembro de un grupo de disponibilidad de base de datos se pierde o presenta algún error y debe ser reemplazado porque no es posible recuperarlo, puede ejecutar una operación de recuperación del servidor mediante el conmutador **Setup /m:RecoverServer**. Sin embargo, antes de realizar la operación de recuperación, primero, deberá quitar el servidor del DAG mediante el cmdlet [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/es-es/library/dd297956\(v=exchg.150\)) con el parámetro *ConfigurationOnly*.

  - **Eliminación de un grupo de disponibilidad de base de datos**   Pueden existir situaciones en las que se debe quitar un DAG (por ejemplo, al deshabilitar el modo de replicación de terceros). Si necesita eliminar un DAG, primero, deberá quitar todos los servidores del DAG. Si intenta quitar un DAG que contiene algún miembro, se produce un error en la tarea.

Volver al principio

## Cómo configurar las propiedades del DAG

Una vez que los servidores se han agregado al DAG, puede usar el EAC o el Shell para configurar las propiedades de un DAG, incluidos el servidor testigo y el directorio testigo que usa el DAG, y las direcciones IP asignadas al DAG.

Las propiedades configurables incluyen las siguientes:

  - **Servidor testigo**   El nombre del servidor en el que desea hospedar el recurso compartido de archivos para el recurso compartido de archivos testigo. Se recomienda especificar un servidor de acceso de cliente como servidor testigo. Esto permite al sistema configurar, proteger y usar automáticamente el recurso compartido, según sea necesario, y permite al administrador de mensajería conocer la disponibilidad del servidor testigo.

  - **Directorio testigo**   El nombre de un directorio que se usará para almacenar datos del testigo del recurso compartido de archivos. El sistema creará automáticamente este directorio en el servidor testigo especificado.

  - **Direcciones IP del grupo de disponibilidad de base de datos**   Deben asignarse una o varias direcciones IP al DAG, a menos que los miembros del DAG ejecuten Windows Server 2012 R2 y vaya a crear un DAG sin una dirección IP. De lo contrario, las direcciones IP del DAG se pueden configurar mediante direcciones IP estáticas asignadas de forma manual o se pueden asignar al DAG de forma automática mediante un servidor DHCP de la organización.

El Shell le permite configurar propiedades del DAG que no están disponibles en el EAC, como direcciones IP del DAG, opciones de cifrado y compresión de redes, detección de redes, el puerto TCP usado para la replicación y opciones alternativas para el servidor testigo y el directorio testigo. Además, le permite habilitar el modo de coordinación de la activación del centro de datos.

Para obtener instrucciones detalladas sobre cómo configurar las propiedades de un DAG, vea [Configurar las propiedades del grupo de disponibilidad de base de datos](configure-database-availability-group-properties-exchange-2013-help.md).

## Cifrado de red de DAG

Los DAG admiten el uso de cifrado mediante el aprovechamiento de las capacidades de cifrado del sistema operativo de Windows Server. Los DAG utilizan la autenticación Kerberos entre servidores de Exchange. Las API EncryptMessage y DecryptMessage del proveedor de compatibilidad para seguridad (SSP) Microsoft Kerberos manejan el cifrado del tráfico de red del DAG. El SSP de Microsoft Kerberos admite varios algoritmos de cifrado. (Para conocer la lista completa, vea la sección 3.1.5.2, "Tipos de cifrado" de [Extensiones del protocolo Kerberos](https://go.microsoft.com/fwlink/p/?linkid=179131)). El protocolo de enlace de la autenticación de Kerberos selecciona el protocolo de cifrado más alto de la lista: en general, el Estándar de cifrado avanzado (AES) de 256 bits, posiblemente con un HMAC (código de autenticación de mensajes basado en hash) SHA para mantener la integridad de los datos. Para obtener información detallada, vea [HMAC](https://en.wikipedia.org/wiki/hmac).

El cifrado de red es una propiedad del DAG, y no una red del DAG. Puede configurar el cifrado de red del DAG mediante el uso del cmdlet **Set-DatabaseAvailabilityGroup** en el Shell. En la siguiente tabla, se muestran las opciones disponibles de cifrado de las comunicaciones de red del DAG.

### Opciones de cifrado de las comunicaciones de red del DAG

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Deshabilitado</p></td>
<td><p>No se usa cifrado de red.</p></td>
</tr>
<tr class="even">
<td><p>Habilitado</p></td>
<td><p>El cifrado de red se usa en todas las redes del DAG para replicación y propagación.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>El cifrado de red se usa en las redes del DAG al replicar en diferentes subredes. Esta es la configuración predeterminada.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>El cifrado de red se usa en todas las redes del DAG solo para la propagación.</p></td>
</tr>
</tbody>
</table>


## Compresión de red de DAG

Los DAG admiten compresión integrada. Cuando se habilita la compresión, la comunicación de redes del DAG usa XPRESS, que es la implementación del algoritmo LZ77 por parte de Microsoft. Para obtener información detallada, vea la [introducción al algoritmo deflate](http://www.zlib.net/feldspar.html) y la sección 3.1.4.11.1.2.1 sobre el algoritmo de compresión LZ77 de la [especificación de Wire Format Protocol](https://go.microsoft.com/fwlink/p/?linkid=179133). Se trata del mismo tipo de compresión usado en muchos protocolos de Microsoft, en especial, la compresión RPC de MAPI entre Microsoft Outlook y Exchange.

Como sucede con el cifrado de red, la compresión de red es una propiedad del DAG, y no una red del DAG. Para configurar la compresión de red del DAG debe usar el cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)) en el Shell. En la siguiente tabla, se muestran las opciones disponibles de compresión de las comunicaciones de red del DAG.

### Opciones de compresión de las comunicaciones de red del DAG

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Deshabilitado</p></td>
<td><p>No se usa compresión de red.</p></td>
</tr>
<tr class="even">
<td><p>Habilitado</p></td>
<td><p>La compresión de red se usa en todas las redes del DAG para replicación y propagación.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>La compresión de red se usa en las redes del DAG al replicar en diferentes subredes. Esta es la configuración predeterminada.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>La compresión de red se usa en todas las redes del DAG solo para la propagación.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Redes de DAG

Una red del DAG es un conjunto de una o más subredes usadas para el tráfico de replicación o el tráfico MAPI. Cada DAG contiene un máximo de una red MAPI y cero más redes de replicación.

## Configuración de adaptador de red simple

En una configuración de adaptador de red simple se usa la misma red para el tráfico de replicación y MAPI. Para reducir la complejidad, la configuración recomendada para los servidores Exchange es un adaptador de red simple, por lo que es aceptable tener tanto tráfico de replicación como MAPI en la misma red.

## Configuración de adaptador de red dual

Normalmente, solo tiene que usar adaptadores de red dual donde el tráfico de red tiene el potencial para saturar un adaptador de red simple.

En un adaptador de red dual, una red se dedica generalmente al tráfico de replicación y la otra se usa principalmente para el tráfico MAPI. También puede agregar adaptadores de red a cada miembro DAG y configurar redes DAG adicionales como redes de replicación.


> [!NOTE]
> Cuando se usan varias redes de replicación, no hay forma de especificar una orden de precedencia para el uso de las redes. Exchange selecciona aleatoriamente una red de replicación del grupo de redes de replicación para usarla en el trasvase de registros.



En Exchange 2010, la configuración manual de las redes del DAG era necesaria en muchos escenario. De forma predeterminada, en Exchange 2013, es el sistema el que configura automáticamente las redes del DAG. Antes de crear o modificar las redes del DAG, primero deberá habilitar el control manual de la red del DAG ejecutando el siguiente comando:

    Set-DatabaseAvailabilityGroup <DAGName> -ManualDagNetworkConfiguration $true

Una vez haya habilitado la configuración de red del DAG manual, podrá usar el cmdlet **New-DatabaseAvailabilityGroupNetwork** en el Shell para crear una red del DAG. Para obtener instrucciones detalladas acerca de cómo crear una red de grupo de disponibilidad de base de datos, vea [Creación de una red de grupos de disponibilidad de base de datos](create-a-database-availability-group-network-exchange-2013-help.md).

Puede configurar las propiedades de la red de DAG utilizando el cmdlet **Set-DatabaseAvailabilityGroupNetwork** en el Shell. Para obtener instrucciones detalladas sobre cómo configurar las propiedades de una red de DAG, vea [Configuración de propiedades de red de grupos de disponibilidad de base de datos](configure-database-availability-group-network-properties-exchange-2013-help.md). Cada red del DAG tiene parámetros obligatorios y opcionales para configurar:

  - **Nombre de red**   Nombre exclusivo para la red del DAG de 128 caracteres como máximo.

  - **Descripción de red**   Descripción opcional de la red del DAG de 256 caracteres como máximo.

  - **Subredes de red**   Una o más subredes a las que se obtiene acceso mediante un formato de *dirección IP o máscara de bits* (por ejemplo, 192.168.1.0/24 para subredes del protocolo de Internet versión 4 IPv4; 2001:DB8:0:C000::/64 para subredes del protocolo de Internet 6 IPv6).

  - **Habilitar replicación**   En el EAC, seleccione la casilla que permite dedicar la red del DAG al tráfico de replicación y bloquee el tráfico MAPI. Desactive la casilla para impedir que la replicación use la red del DAG y para habilitar el tráfico MAPI. En el Shell, use el parámetro *ReplicationEnabled* del cmdlet [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd298008\(v=exchg.150\)) para habilitar y deshabilitar la replicación.


> [!NOTE]
> La deshabilitación de la replicación en la red MAPI no garantiza que el sistema no usará esa red MAPI para replicación. Cuando todas las redes configuradas para replicación se encuentran sin conexión, presentan errores o no se encuentran disponibles y solo existe una red MAPI (que no está configurada como habilitada para la replicación) el sistema usa esa red MAPI para la replicación.



Las redes de DAG iniciales (por ejemplo, MapiDagNetwork y ReplicationDagNetwork01) creadas por el sistema se basan en las subredes enumeradas por el Servicio de clúster. Cada miembro DAG debe tener la misma cantidad de adaptadores de redes y cada adaptador de red debe tener una dirección IPv4 (y opcionalmente, también una dirección IPv6) en una subred única. Varios miembros de DAG pueden tener direcciones IPv4 en la misma subred, pero cada adaptador de red y par de dirección de IP en un miembro DAG específico deben estar en una subred única. Además, solamente el adaptador usado para la red MAPI se debe configurar con la puerta de enlace predeterminada. Las redes de replicación no se deben configurar con una puerta de enlace predeterminada.

Por ejemplo, considere DAG1, un DAG de dos miembros donde cada miembro tiene dos adaptadores de red (uno dedicado para la red MAPI y el otro para la red de replicación). Las configuraciones de dirección IP de ejemplo se muestran en la siguiente tabla.

### Configuraciones del adaptador de red de ejemplo

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Adaptador de red del servidor</th>
<th>Dirección IP/máscara de subred</th>
<th>Puerta de enlace predeterminada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.1.15/24</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>Replicación de EX1</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.16</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>Replicación de EX2</p></td>
<td><p>10.0.0.16</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


En la siguiente configuración, hay dos subredes configuradas en el DAG: 192.168.1.0 y 10.0.0.0. Cuando se agregan EX1 y EX2 al DAG, se enumerarán dos subredes y se crearán dos redes de DAG: MapiDagNetwork (192.168.1.0) y ReplicationDagNetwork01 (10.0.0.0). Estas redes se configurarán como se muestra en la siguiente tabla.

### Configuraciones de red DAG enumeradas para un DAG de subred simple

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre</th>
<th>Subredes</th>
<th>Interfaces</th>
<th>Acceso a MAPI habilitado</th>
<th>Replicación habilitada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.1.15)</p>
<p>EX2 (192.168.1.16)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.0.16)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


Para completar la configuración de ReplicationDagNetwork01 como la red de replicación dedicada, deshabilite la replicación para MapiDagNetwork ejecutando el siguiente comando.

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG1\MapiDagNetwork -ReplicationEnabled:$false

Después de deshabilitar la replicación para MapiDagNetwork, el servicio de replicación de Microsoft Exchange usa ReplicationDagNetwork01 para la replicación continua. Si se produce un error en ReplicationDagNetwork01, el servicio de replicación de Microsoft Exchange vuelve a usar MapiDagNetwork para la replicación continua. Esto lo hace intencionalmente el sistema para mantener la disponibilidad alta.

## Implementaciones de varias subredes y redes de DAG

En el ejemplo anterior, aunque hay dos redes diferentes usadas por el DAG (192.168.1.0 y 10.0.0.0), el DAG se considera un DAG de subred simple ya que cada miembro utiliza la misma subred para formar la red MAPI. Cuando los miembros de DAG usan diferentes subredes para la red MAPI, el DAG es referido como un *DAG de subredes múltiples*. En un DAG de varias subredes, cada red de DAG tiene asociada automáticamente la subred adecuada.

Por ejemplo, considere DAG2, un DAG de dos miembros donde cada miembro tiene dos adaptadores de red (uno dedicado para la red MAPI y otro para una red de replicación) y cada miembro de DAG está ubicado en un sitio de Active Directory separado, con su red MAPI en una subred diferente. Las configuraciones de dirección IP de ejemplo se muestran en la siguiente tabla.

### Configuraciones del adaptador de red del ejemplo para un DAG en una subred múltiple

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Adaptador de red del servidor</th>
<th>Dirección IP/máscara de subred</th>
<th>Puerta de enlace predeterminada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.0.15/24</p></td>
<td><p>192.168.0.1</p></td>
</tr>
<tr class="even">
<td><p>Replicación de EX1</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.15</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>Replicación de EX2</p></td>
<td><p>10.0.1.15</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


En la siguiente configuración, hay cuatro subredes configuradas en el DAG: 192.168.0.0, 192.168.1.0, 10.0.0.0, y 10.0.1.0. Cuando se agregan EX1 y EX2 al DAG, se enumerarán cuatro subredes pero solo se crearán dos redes de DAG: MapiDagNetwork (192.168.0.0, 192.168.1.0) y ReplicationDagNetwork01 (10.0.0.0, 10.0.1.0). Estas redes se configurarán como se muestra en la siguiente tabla.

### Configuraciones de red DAG enumeradas para un DAG de subred múltiple

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre</th>
<th>Subredes</th>
<th>Interfaces</th>
<th>Acceso a MAPI habilitado</th>
<th>Replicación habilitada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.0.0/24</p>
<p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.0.15)</p>
<p>EX2 (192.168.1.15)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p>
<p>10.0.1.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.1.15)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


## Redes del DAG y redes iSCSI

De forma predeterminada, los DAG encuentran todas las redes detectadas y configuradas para ser usadas según su clúster subyacente. Esto incluye todas las redes Internet SCSI (iSCSI) que se usan como resultado del uso del almacenamiento iSCSI para uno o más miembros del DAG. Se recomienda que el almacenamiento iSCSI use redes y adaptadores de red dedicados. Estas redes no deben ser administradas por el DAG ni por su clúster, ni deben usarse como redes del DAG (MAPI o replicación). En lugar de ello, estas redes deben ser manualmente deshabilitadas para que el DAG no las use, de modo que puedan dedicarse al tráfico de almacenamiento iSCSI. Para deshabilitar la detección de las redes iSCSI y su uso como redes de DAG, configure el DAG para que omita cualquier red iSCSI actualmente detectada usando el cmdlet [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/es-es/library/dd298008\(v=exchg.150\)), como se muestra en el ejemplo siguiente:

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG2\DAGNetwork02 -ReplicationEnabled:$false -IgnoreNetwork:$true

Este comando también deshabilitará el uso de la red por parte del clúster. Si bien las redes iSCSI continuarán apareciendo como redes de DAG, no se usarán para tráfico de replicación o MAPI después de la ejecución del comando anterior.

Volver al principio

## Cómo configurar los miembros de DAG

Los servidores del buzón de correo que son los miembros de un DAG tienen propiedades específicas para alta disponibilidad que se pueden configurar como se describe en las siguientes secciones:

  - Automatic database mount dial

  - Database copy automatic activation policy

  - Maximum active databases

## Marcación automática de montaje de base de datos

El parámetro *AutoDatabaseMountDial* especifica el montaje de la base de datos automático después de la falla de la base de datos. Puede usar el cmdlet [Set-MailboxServer](https://technet.microsoft.com/es-es/library/aa998651\(v=exchg.150\)) para configurar el parámetro *AutoDatabaseMountDial* con cualquiera de los siguientes valores:

  - `BestAvailability`   Si especifica este valor, la base de datos monta automáticamente tras un error si la longitud de la cola de copia es inferior o igual a 12. La longitud de la cola de copia es el número de registros reconocidos por la copia pasiva que debe replicarse. Si la longitud de la cola de copia es superior a 12, las bases de datos no se montan automáticamente. Cuando la longitud de la cola de copia es inferior o igual a doce, Exchange intentará replicar los registros restantes en la copia pasiva y montará la base de datos.

  - `GoodAvailability`   Si especifica este valor, las bases de datos se montarán de forma automática inmediatamente tras un error si la longitud de la cola de copia es inferior o igual a 6. La longitud de la cola de copia es el número de registros que la copia pasiva reconoce que deben replicarse. Si la longitud de la cola de copia es superior a seis, la base de datos no se monta automáticamente. Cuando la longitud de la cola de copia es inferior o igual a 6, Exchange intentará replicar los registros restantes en la copia pasiva y montará la base de datos.

  - `Lossless`   Si especifica este valor, la base de datos no se montará automáticamente hasta que todos los registros de la copia activa se hayan copiado en la copia pasiva. Esta configuración también causa el algoritmo de selección de copia del administrador activo para ordenar candidatos posibles para la activación basada en el valor de preferencia de activación de la copia de la base de datos y no en la longitud de la cola de la copia.

El valor predeterminado es `GoodAvailability`. Si especifica entre `BestAvailability` o `GoodAvailability`, y ninguno de los registros de la copia activa se pueden copiar en la copia pasiva, es posible que pierda parte de los datos del buzón. No obstante, la característica red de seguridad (habilitada de manera predeterminada) contribuye a proteger contra la pérdida de datos, al volver a enviar los mensajes en la cola de la red de seguridad.

## Ejemplo: configuración de la marcación automática de montaje de base de datos

El siguiente ejemplo configura un servidor de buzones de correo con una configuración *AutoDatabaseMountDial* de `GoodAvailability`.

    Set-MailboxServer -Identity EX1 -AutoDatabaseMountDial GoodAvailability

## Directiva de activación automática de la copia de la base de datos

El parámetro *DatabaseCopyAutoActivationPolicy* especifica el tipo de activación automática disponible para copias de bases de datos de buzones de correo en los servidores de buzones de correo seleccionados. Puede usar el cmdlet [Set-MailboxServer](https://technet.microsoft.com/es-es/library/aa998651\(v=exchg.150\)) para configurar el parámetro *DatabaseCopyAutoActivationPolicy* con cualquiera de los siguientes valores:

  - `Blocked`   Si especifica este valor, las bases de datos no pueden ser activadas automáticamente en los servidores de buzones de correo seleccionados.

  - `IntrasiteOnly`   Si especifica este valor, la copia de la base de datos puede activarse en servidores en el mismo sitio de Active Directory. Esto impide activación o errores entre sitios. Esta propiedad es para ingresar copias de bases de datos del buzón (por ejemplo: una copia pasiva se transforma en una copia activa). Las bases de datos no pueden activarse en este servidor de buzones de correo para copias de bases de datos que están activas en otro sitio de Active Directory.

  - `Unrestricted`   Si especifica este valor, no existen restricciones especiales de activación para copias de bases de datos de buzones de correo de los servidores de buzones de correo seleccionados.

## Ejemplo: configuración de la directiva de activación automática de la copia de base de datos

El siguiente ejemplo configura un servidor de buzones de correo con una configuración *DatabaseCopyAutoActivationPolicy* de `Blocked`.

    Set-MailboxServer -Identity EX1 -DatabaseCopyAutoActivationPolicy Blocked

## Bases de datos activas máximas

El parámetro *MaximumActiveDatabases* (también usado con el cmdlet [Set-MailboxServer](https://technet.microsoft.com/es-es/library/aa998651\(v=exchg.150\))) especifica el número de bases de datos que se puede montar en este servidor de buzones de correo. Puede configurar los servidores del buzón de correo para cumplir con los requisitos de implementación al asegurar que un servidor de correo de voz individual no se sobrecargue.

El parámetro *MaximumActiveDatabases* está configurado con un valor numérico de número entero. Cuando se alcanza el número máximo, las copias de la base de datos en el servidor no se activarán si se produce un error o cambio. Si las copias ya están activas en un servidor, este no permite montar bases de datos.

## Ejemplo: configuración de las bases de datos activas máximas

El siguiente ejemplo configura un servidor de buzones de correo para que admita un máximo de 20 bases de datos activas.

    Set-MailboxServer -Identity EX1 -MaximumActiveDatabases 20

Volver al principio

## Cómo realizar el mantenimiento en los miembros de DAG

Antes de realizar cualquier mantenimiento de software o hardware en un miembro de DAG, primero debe colocar el miembro de DAG en modo de mantenimiento. Esto implica mover todas las bases de datos activas del servidor y bloquear las bases de datos activas para que no se muevan del servidor. Esto también asegura que toda la funcionalidad de compatibilidad de DAG crítico que pueda haber en el servidor (por ejemplo, el rol del administrador activo primario (PAM)) se mueva a otro servidor y se bloquee para que no vuelva al servidor. En concreto, debe realizar las siguientes tareas:

1.  Para comenzar el proceso de drenar las colas de transporte, ejecute `Set-ServerComponentState <ServerName> -Component HubTransport -State Draining -Requester Maintenance`.

2.  Para comenzar el proceso de drenar las colas de transporte, ejecute `Restart-Service MSExchangeTransport`.

3.  Para comenzar el proceso de drenar todas las llamadas de mensajería unificada, ejecute `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Draining -Requester Maintenance`.

4.  Para redirigir los mensajes con entrega pendiente en las colas locales al servidor de buzones de correo especificado por el parámetro de destino, ejecute `Redirect-Message -Server <ServerName> -Target <MailboxServerFQDN>`.

5.  Para detener el nodo del clúster, que impide que el nodo sea y se convierta en el PAM, ejecute `Suspend-ClusterNode <ServerName>`.

6.  Para mover todas las bases de datos activas alojadas actualmente en el miembro de DAG a otros miembros de DAG, ejecute `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $True`.

7.  Para impedir que el servidor hospede copias de bases de datos activas, ejecute `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Blocked`.

8.  Para colocar el servidor en modo de mantenimiento, ejecute `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Inactive -Requester Maintenance`.

Para comprobar que un servidor está listo para mantenimiento, realice las siguientes tareas:

1.  Para comprobar que el servidor se ha colocado en modo de mantenimiento, ejecute `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`.

2.  Para comprobar que el servidor no hospeda ninguna copia de bases de datos activas, ejecute `Get-MailboxServer <ServerName> | ft DatabaseCopy* -Autosize`.

3.  Para comprobar que el nodo está pausado, ejecute `Get-ClusterNode <ServerName> | fl`.

4.  Para comprobar que todas las colas de transporte se han drenado, ejecute `Get-Queue`.

Una vez completado el mantenimiento y listo el miembro de DAG para volver al servicio, puede sacar al miembro de DAG del modo de mantenimiento y volverlo a poner en la producción realizando las siguientes tareas:

  - Para designar que el servidor está fuera de modo de mantenimiento, ejecute `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Maintenance`.

  - Para permitir que el servidor acepte las llamadas de mensajería unificada, ejecute `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Active -Requester Maintenance`.

  - Para reanudar el nodo en el clúster y habilitar la funcionalidad completa del clúster para el servidor, ejecute `Resume-ClusterNode <ServerName>`.

  - Para permitir que las bases de datos estén activas en el servidor, ejecute `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $False`.

  - Para eliminar los bloques de activación automática, ejecute `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Unrestricted`.

  - Para habilitar las colas de transporte y permitir que el servidor acepte y procese mensajes, ejecute `Set-ServerComponentState <ServerName> -Component HubTransport -State Active -Requester Maintenance`.

  - Para reanudar la actividad de transporte, ejecute `Restart-Service MSExchangeTransport`.

Para comprobar que un servidor está listo para su uso en producción, realice las siguientes tareas:

1.  Para comprobar que el servidor no se encuentra en modo de mantenimiento, ejecute `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`.

Si va a instalar una actualización de Exchange y se produce un error en el proceso de actualización, puede que algunos componentes de servidor se encuentren en estado inactivo. Esto se indicará en el resultado del cmdlet Get-ServerComponentState anterior. Para resolverlo, ejecute los siguientes comandos:

  - `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component Monitoring -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component RecoveryActionsEnabled -State Active -Requester Functional`

Volver al principio

## Cómo apagar los miembros de DAG

La solución de alta disponibilidad de Exchange 2013 está integrada con el proceso de apagado de Windows. Si un administrador o una aplicación inician el apagado de un servidor de Windows en un DAG con una base de datos montada que se replica en uno o más miembros del DAG, el sistema intentará activar otra copia de la base de datos montada antes de permitir que se complete el proceso de apagado.

Sin embargo, este nuevo comportamiento no garantiza que todas las bases de datos del servidor que se apaguen experimenten una activación `lossless`. Por lo tanto, el procedimiento recomendado es realizar una conmutación de servidor antes de apagar un servidor miembro de un grupo de disponibilidad de base de datos.

Volver al principio

## Instalación de actualizaciones en miembros DAG

La instalación de actualizaciones de Microsoft Exchange Server 2013 en un servidor que es miembro de un DAG es un proceso relativamente directo. Al instalar una actualización en un servidor que es miembro de un DAG, se detienen varios servicios durante la instalación, incluidos todos los servicios de Exchange y el servicio de clúster. El proceso general para aplicar actualizaciones a un DAG es el siguiente:

1.  Siga los pasos descritos arriba para poner el miembro de DAG en modo de mantenimiento.

2.  Instale el paquete.

3.  Use los pasos descritos arriba para sacar al miembro de DAG del modo de mantenimiento y volver a ponerlo en la producción.

4.  De forma opcional, use la secuencia RedistributeActiveDatabases.ps1 para volver a equilibrar las copias de la base de datos en el DAG.

Puede descargar la actualización más reciente para Exchange 2013 en el [Centro de descarga de Microsoft](http://www.microsoft.com/downloads/).

Volver al principio

