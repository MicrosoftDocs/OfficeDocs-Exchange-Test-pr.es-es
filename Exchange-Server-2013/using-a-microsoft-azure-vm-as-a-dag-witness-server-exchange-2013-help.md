---
title: 'Usar VM Microsoft Azure como servidor testigo DAG Exchange 2013 Help'
TOCTitle: Usar una máquina virtual de Microsoft Azure como un servidor testigo del DAG
ms:assetid: 03d1e215-518b-4b48-bfcd-8d187ff8f5ef
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn903504(v=EXCHG.150)
ms:contentKeyID: 63892248
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Usar una máquina virtual de Microsoft Azure como un servidor testigo del DAG

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Exchange Server 2013 permite configurar las bases de datos de buzones de correo en un grupo de disponibilidad de base de datos (DAG) para conmutación por error automática del centro de datos. Esta configuración requiere tres ubicaciones físicas independientes: dos centros de datos para servidores de buzones y una tercera ubicación para colocar el servidor testigo para el DAG. Las organizaciones con solo dos ubicaciones físicas ahora también pueden aprovechar las ventajas de la conmutación por error automática del centro de datos usando una máquina virtual de servidor de archivos de Microsoft Azure para que actúe como servidor testigo del DAG.

Este artículo se centra en la ubicación del testigo del DAG en Microsoft Azure y asume que está familiarizado con los conceptos de resistencia de sitios y que ya tiene una infraestructura de DAG totalmente funcional que incluye dos centros de datos. Si aún no tiene la infraestructura de DAG configurada, le recomendamos que consulte primero los siguientes artículos:

[Alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-exchange-2013-help.md)

[Grupos de disponibilidad de base de datos (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[Planificación de alta disponibilidad y resistencia de sitios](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)

## Cambios en Microsoft Azure

Esta configuración requiere una VPN de varios sitios. Siempre ha sido posible conectar la red de su organización con Microsoft Azure usando una conexión VPN de sitio a sitio. Sin embargo, en el pasado, Azure solo admitía una VPN de sitio a sitio. Dado que configurar un DAG y su testigo en tres centros de datos requería varias VPN de sitio a sitio, inicialmente no era posible colocar el testigo del DAG en una máquina virtual de Azure.

En junio de 2014, Microsoft Azure incorporó compatibilidad para VPN de varios sitios, que permite a las organizaciones conectar varios centros de datos a la misma red virtual de Azure. Este cambio también ha hecho posible que las organizaciones con dos centros de datos aprovechen Microsoft Azure como una tercera ubicación donde colocar los servidores testigo del DAG. Para obtener más información acerca de la característica de VPN de varios sitios en Azure, consulte [Configurar una VPN de varios sitios](http://go.microsoft.com/fwlink/?linkid=522621).


> [!NOTE]
> Esta configuración utiliza una VPN de varios sitios y máquinas virtuales de Azure para implementar el servidor testigo, y no utiliza el testigo de nube de Azure.



## Testigo de servidor de archivos de Microsoft Azure

El siguiente diagrama ofrece una visión general de cómo usar una máquina virtual de servidor de archivos de Microsoft Azure como testigo del DAG. Necesita una red virtual de Azure, una VPN de varios sitios que conecte los centros de datos con la red virtual de Azure, y un controlador de dominio y un servidor de archivos implementados en máquinas virtuales de Azure.


> [!NOTE]
> Es técnicamente posible usar una única máquina virtual de Azure para este propósito y colocar el testigo del recurso compartido de archivos en el controlador de dominio. Sin embargo, esto provocará una elevación de privilegios innecesaria. Por lo tanto, no se recomienda esta configuración.



**Servidor testigo del DAG en Microsoft Azure**

![Testigo de Exchange DAG en información general de Azure](images/Dn903504.7cbda882-bbae-4be7-b0ea-60947b8aa4ef(EXCHG.150).png "Testigo de Exchange DAG en información general de Azure")

Lo primero que debe hacer para poder usar una máquina virtual de Microsoft Azure para su testigo del DAG es obtener una suscripción. Consulte en [Instrucciones para contratar Azure](http://go.microsoft.com/fwlink/?linkid=398989) la mejor manera de adquirir una suscripción de Azure.

Cuando tenga su suscripción de Azure, debe hacer lo siguiente en orden:

1.  Preparar la red virtual de Microsoft Azure

2.  Configurar una VPN de varios sitios

3.  Configurar las máquinas virtuales

4.  Configurar el testigo del DAG


> [!NOTE]
> Una parte importante de las instrucciones de este artículo están relacionadas con la configuración de Microsoft Azure. Por lo tanto, se usarán vínculos a la documentación de Azure siempre que proceda.



## Requisitos previos

  - Dos centros de datos con capacidad para una implementación de Exchange con resistencia de sitios y alta disponibilidad. Consulte [Planificación de alta disponibilidad y resistencia de sitios](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) para obtener más información

  - Una dirección IP pública que no esté detrás de NAT para las puertas de enlace VPN en cada sitio

  - Un dispositivo VPN en cada sitio que sea compatible con Microsoft Azure. Consulte [Acerca de los dispositivos VPN de la red virtual](http://go.microsoft.com/fwlink/?linkid=522619) para obtener más información acerca de los dispositivos compatibles

  - Estar familiarizado con conceptos y administración de DAG

  - Estar familiarizado con Windows PowerShell

## Fase 1: Preparar la red virtual de Microsoft Azure

La configuración de la red de Microsoft Azure es la parte más importante del proceso de implementación. Al final de esta fase, tendrá una red virtual Azure totalmente funcional conectada a los dos centros de datos a través de una VPN de varios sitios.

## Registrar los servidores DNS

Como esta configuración requiere la resolución de nombres entre los servidores locales y las máquinas virtuales de Azure, tendrá que configurar Azure para utilizar sus propios servidores DNS. El tema [Resolución de nombres (DNS)](http://msdn.microsoft.com/es-es/library/azure/jj156088.aspx) ofrece una descripción general de la resolución de nombres en Azure.

Haga lo siguiente para registrar los servidores DNS:

1.  En el portal de Azure, vaya a **redes** y, después, haga clic en **NUEVO**.

2.  Haga clic en **SERVICIOS DE RED** \> **RED VIRTUAL** \> **REGISTRAR SERVIDOR DNS**.

3.  Escriba el nombre y la dirección IP del servidor DNS. El nombre especificado aquí es un nombre lógico que se usa en el portal de administración y no tiene que coincidir con el nombre real del servidor DNS.

4.  Repita los pasos 1 a 3 para cualquier otro servidor DNS que quiera agregar.
    

    > [!NOTE]
    > Los servidores DNS que se registre no se utilizan en modo por turnos. Las máquinas virtuales de Azure usarán el primer servidor DNS que aparezca y solo usará otros servidores si el primero de ellos no está disponible.



5.  Repita los pasos 1 a 3 para agregar la dirección IP que se va a utilizar para el controlador de dominio que implementará en Microsoft Azure.

## Crear objetos de red locales en Azure

A continuación, haga lo siguiente para crear objetos de red lógicos que representan los centros de datos en Microsoft Azure:

1.  En el portal de Azure, vaya a **redes** y haga clic en **NUEVO**.

2.  Haga clic en **SERVICIOS DE RED** \> **RED VIRTUAL** \> **AGREGAR RED LOCAL**.

3.  Escriba el nombre del sitio del primer centro de datos y la dirección IP del dispositivo VPN en ese sitio. Esta dirección IP debe ser una dirección IP pública estática que no esté detrás de NAT.

4.  En la siguiente pantalla, especifique las subredes IP para el primer sitio.

5.  Repita los pasos 1 a 4 para el segundo sitio.

## Crear la red virtual de Azure

Ahora, haga lo siguiente para crear la red virtual de Azure que las máquinas virtuales usarán:

1.  En el portal de Azure, vaya a **redes** y, después, haga clic en **NUEVO**.

2.  Haga clic en **SERVICIOS DE RED** \> **RED VIRTUAL** \> **CREACIÓN PERSONALIZADA**.

3.  En la página **Detalles de la red Virtual** , especifique un nombre para la red virtual y seleccione la ubicación geográfica de la red.

4.  En la página **Servidores DNS y conectividad VPN**, compruebe que los servidores DNS registrados anteriormente aparecen como servidores DNS.

5.  Active la casilla **Configurar una VPN de sitio a sitio** en **CONECTIVIDAD DE SITIO A SITIO**.
    

    > [!IMPORTANT]
    > No seleccione <STRONG>Usar ExpressRoute</STRONG> porque esto evitará los cambios de configuración necesarios para configurar una VPN de varios sitios.



6.  En **RED LOCAL**, seleccione una de las dos redes locales configuradas.

7.  En la página **Espacios de direcciones de la red virtual**, especifique el intervalo de direcciones IP que se usará para la red virtual de Azure.

## Punto de control: revisar la configuración de la red

En este momento, cuando vaya a **redes**, debería ver la red virtual configurada en **REDES VIRTUALES**, los sitios locales en **REDES LOCALES** y los servidores DNS registrados en **SERVIDORES DNS**.

## Fase 2: Configurar una VPN de varios sitios

El siguiente paso es establecer las puertas de enlace VPN a los sitios locales. Para ello, deberá:

1.  Establecer una puerta de enlace VPN a uno de los sitios mediante el portal de Azure.

2.  Exportar las opciones de configuración de la red virtual.

3.  Modificar el archivo de configuración de la VPN de varios sitios.

4.  Importar la configuración de red de Azure actualizada.

5.  Registrar la dirección IP de la puerta de enlace de Azure y las claves previamente compartidas.

6.  Configurar los dispositivos VPN locales.

Para obtener más información acerca de cómo configurar una VPN de varios sitios, consulte [Configurar una VPN de varios sitios](http://go.microsoft.com/fwlink/?linkid=522621).

## Establecer una puerta de enlace VPN para el primer sitio

Al crear la puerta de enlace virtual, tenga en cuenta que ya ha especificado que se conectará al primer sitio local. Cuando entre en el panel de la red virtual, verá que la puerta de enlace no se ha creado.

Para establecer la puerta de enlace VPN en el lado de Azure, siga las instrucciones de la sección [Iniciar la puerta de enlace de la red virtual](http://msdn.microsoft.com/es-es/library/azure/jj156210.aspx#bkmk+_startgateway) en el tema [Configurar una puerta de enlace de red virtual en el Portal de administración](http://msdn.microsoft.com/es-es/library/azure/jj156210.aspx).


> [!IMPORTANT]
> Realice solo los pasos de la sección "Iniciar la puerta de enlace de la red virtual" y no continúe en las secciones posteriores.



## Exportar las opciones de configuración de la red virtual

El portal de administración de Azure actualmente no permite configurar una VPN de varios sitios. Para esta configuración, deberá exportar las opciones de configuración de la red virtual a un archivo XML y, después, modificar el archivo. Siga las instrucciones de [Exportar la configuración de red virtual a un archivo de configuración de red](http://msdn.microsoft.com/es-es/library/azure/dn133804.aspx) para exportar la configuración.

## Modificar la configuración de red de la VPN de varios sitios

Abra el archivo exportado en cualquier editor de XML. Las conexiones de puerta de enlace a los sitios locales figuran en la sección "ConnectionsToLocalNetwork". Busque ese término en el archivo XML para encontrar la sección. Esta sección del archivo de configuración será similar a esta (suponiendo que el nombre que creó para el sitio local sea "Site A").

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

Para configurar el segundo sitio, agregue otra sección "LocalNetworkSiteRef" en la sección "ConnectionsToLocalNetwork". La sección del archivo de configuración actualizado será similar a la siguiente (suponiendo que el nombre del segundo sitio local sea "Site B").

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
        <LocalNetworkSiteRef name="Site B">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

Guarde el archivo de configuración actualizado.

## Importar las opciones de configuración de la red virtual

La segunda referencia de sitio que se ha agregado al archivo de configuración activará Microsoft Azure para crear un túnel nuevo. Importe el archivo actualizado siguiendo las instrucciones de [Importar un archivo de configuración de red](http://msdn.microsoft.com/es-es/library/azure/jj156213.aspx). Después de completar la importación, el panel de la red virtual le mostrará las conexiones de puerta de enlace a ambos sitios locales.

## Registrar la dirección IP de puerta de enlace de Azure y las claves previamente compartidas

Después de importar la nueva configuración de red, el panel de la red virtual mostrará la dirección IP de la puerta de enlace de Azure. Se trata de la dirección IP a la que se conectarán los dispositivos VPN en ambos sitios. Registre esta dirección IP como referencia.

También tendrá que obtener las claves de IPsec/IKE previamente compartidas para cada uno de los túneles que se creó. Para configurar los dispositivos VPN locales se usan estas claves junto con la dirección IP de la puerta de enlace de Azure.

Deberá usar PowerShell para obtener las claves previamente compartidas. Si no está familiarizado con el uso de PowerShell para administrar Azure, consulte [Azure PowerShell](http://msdn.microsoft.com/es-es/library/azure/jj156055.aspx).

Use el cmdlet [Get-AzureVNetGatewayKey](http://msdn.microsoft.com/es-es/library/azure/dn495198.aspx) para extraer las claves previamente compartidas. Ejecute este cmdlet una vez para cada túnel. El siguiente ejemplo muestra los comandos que debe ejecutar para extraer las claves de los túneles entre la red virtual "Azure Site" y los sitios "Site A" y "Site B". En este ejemplo, los resultados se guardan en archivos diferentes. También puede canalizar estas claves para otros cmdlets de PowerShell o usarlas en un script.

    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site A" > C:\Keys\KeysForTunnelToSiteA.txt 
    
    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site B" > C:\Keys\KeysForTunnelToSiteB.txt

## Configurar los dispositivos VPN locales

Microsoft Azure proporciona scripts de configuración de dispositivo VPN para los dispositivos VPN compatibles. En el panel de red virtual, haga clic en el vínculo **Descargar script de dispositivo VPN** del script correspondiente a sus dispositivos VPN.

El script que descargue tendrá la configuración del primer sitio que configuró al instalar la red virtual, y puede utilizarlo tal cual para configurar el dispositivo VPN para ese sitio. Por ejemplo, si ha especificado Site A como **RED LOCAL** al crear la red virtual, puede usar el script del dispositivo VPN para Site A. Sin embargo, tendrá que modificarlo para configurar el dispositivo VPN de Site B. En concreto, debe actualizar la clave compartida previamente para que coincida con la clave del segundo sitio.

Por ejemplo, si utiliza un dispositivo VPN del Servicio de Enrutamiento y acceso remoto (RRAS) para sus sitios, necesitará hacer lo siguiente:

1.  Abra el script de configuración en cualquier editor de texto.

2.  Busque la sección `#Add S2S VPN interface`.

3.  Busque el comando **Add-VpnS2SInterface** en esta sección. Compruebe que el valor del parámetro *SharedSecret* coincide con la clave previamente compartida del sitio para el que va a configurar el dispositivo VPN.

Otros dispositivos pueden necesitar otras comprobaciones. Por ejemplo, los scripts de configuración de los dispositivos Cisco establecen reglas ACL usando intervalos de direcciones IP locales. Debe revisar y comprobar todas las referencias al sitio local en el script de configuración antes de utilizarlo. Consulte los temas siguientes para obtener más información:

[Plantillas del Servicio de Enrutamiento y acceso remoto (RRAS)](http://msdn.microsoft.com/es-es/library/azure/dn133801.aspx)

[Plantillas de Cisco ASR](http://msdn.microsoft.com/es-es/library/azure/dn133802.aspx)

[Plantillas de Cisco ISR](http://msdn.microsoft.com/es-es/library/azure/dn133800.aspx)

[Plantillas de Juniper SRX](http://msdn.microsoft.com/es-es/library/azure/dn133794.aspx)

[Plantillas de Juniper serie J](http://msdn.microsoft.com/es-es/library/azure/dn133799.aspx)

[Plantillas de Juniper ISG](http://msdn.microsoft.com/es-es/library/azure/dn133797.aspx)

[Plantillas de Juniper SSG](http://msdn.microsoft.com/es-es/library/azure/dn133796.aspx)

## Punto de control: Revisar el estado de la VPN

En este punto, sus dos sitios están conectados a la red virtual de Azure a través de las puertas de enlace VPN. Para validar el estado de la VPN de varios sitios, ejecute el comando siguiente en PowerShell.

    Get-AzureVnetConnection -VNetName "Azure Site" | Format-Table LocalNetworkSiteName, ConnectivityState

Si ambos túneles están en funcionamiento, el resultado de este comando será similar al siguiente.

    LocalNetworkSiteName    ConnectivityState
    
    --------------------    -----------------
    
    Site A                  Connected
    
    Site B                  Connected

También puede comprobar la conectividad en el panel de la red virtual, en el portal de administración de Azure. La columna **ESTADO** de ambos sitios se mostrará como **Conectado**.


> [!NOTE]
> Una vez establecida la conexión correctamente, el cambio de estado puede tardar varios minutos en aparecer en el portal de administración de Azure.



## Fase 3: Configurar las máquinas virtuales

Debe crear un mínimo de dos máquinas virtuales en Microsoft Azure para esta implementación: un controlador de dominio y un servidor de archivos que actuará como testigo del DAG.

1.  Cree las máquinas virtuales para el controlador de dominio y para el servidor de archivos siguiendo las instrucciones de [Creación de una máquina virtual que ejecuta Windows](http://azure.microsoft.com/es-es/documentation/articles/virtual-machines-windows-tutorial/). Asegúrese de seleccionar la red virtual que creó para **REGIÓN/GRUPO DE AFINIDAD/RED VIRTUAL** cuando especifique la configuración de las máquinas virtuales.

2.  Especificar las direcciones IP preferidas tanto para el controlador de dominio como para el servidor de archivos usando Azure PowerShell. Cuando se especifica una dirección IP preferida para una máquina virtual, es necesario actualizarla, lo que requiere reiniciar la máquina virtual. El ejemplo siguiente establece las direcciones IP para Azure-DC y Azure-FSW en 10.0.0.10 y 10.0.0.11, respectivamente.
    
        Get-AzureVM Azure-DC | Set-AzureStaticVNetIP -IPAddress 10.0.0.10 | Update-AzureVM
        
        Get-AzureVM Azure-FSW | Set-AzureStaticVNetIP -IPAddress 10.0.0.11 | Update-AzureVM
    

    > [!NOTE]
    > Una máquina virtual con una dirección IP preferida intentará usar esa dirección. Sin embargo, si esa dirección se ha asignado a una máquina virtual diferente, no se iniciará la máquina virtual con la configuración de dirección IP preferida. Para evitar esta situación, asegúrese de que la dirección IP que utilice no está asignada a otra máquina virtual. Consulte <A href="https://msdn.microsoft.com/es-es/library/azure/dn630228.aspx">Configurar una dirección IP interna estática para una máquina virtual</A> para obtener más información.



3.  Aprovisione la máquina virtual del controlador de dominio en Azure según los estándares de la organización.

4.  Prepare el servidor de archivos con los requisitos previos para un testigo del DAG de Exchange:
    
    1.  Agregue el rol de servidor de archivos con el Asistente para agregar roles y características o el cmdlet [Add-WindowsFeature](http://technet.microsoft.com/es-es/library/ee662309.aspx).
    
    2.  Agregue el grupo de seguridad universal de Subsistemas de confianza de Exchange al grupo de administradores locales.

## Punto de control: Revisar el estado de la máquina virtual

En este momento, las máquinas virtuales debe estar en funcionamiento y debe ser capaces de comunicarse con los servidores de ambos centros de datos locales:

  - Compruebe que el controlador de dominio en Azure se está replicando con los controladores de dominio locales.

  - Compruebe que puede comunicarse con el servidor de archivos en Azure por nombre y establecer una conexión SMB desde los servidores de Exchange.

  - Compruebe que puede comunicarse con los servidores de Exchange por nombre desde el servidor de archivos en Azure.

## Fase 4: Configurar el testigo del DAG

Por último, deberá configurar el DAG para usar el nuevo servidor testigo. De forma predeterminada, Exchange utiliza C:\\DAGFileShareWitnesses como ruta de acceso del testigo del recurso compartido de archivos en el servidor testigo. Si utiliza una ruta de acceso de archivo personalizado, también debe actualizar el directorio del testigo para el recurso compartido específico.

1.  Conéctese a Shell de administración de Exchange

2.  Ejecute el siguiente comando para configurar el servidor testigo para sus DAG.
    
        Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessServer Azure-FSW

Consulte los temas siguientes para obtener más información:

[Configurar las propiedades del grupo de disponibilidad de base de datos](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](http://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\).aspx)

## Punto de control: Validar el testigo del recurso compartido de archivos del DAG

En este punto, ha configurado el DAG para usar el servidor de archivos en Azure como testigo del DAG. Haga lo siguiente para validar la configuración:

1.  Valide la configuración del DAG ejecutando el siguiente comando.
    
        Get-DatabaseAvailabilityGroup -Identity DAG1 -Status | Format-List Name, WitnessServer, WitnessDirectory, WitnessShareInUse
    
    Compruebe que el parámetro *WitnessServer* está establecido en el servidor de archivos en Azure, el parámetro *WitnessDirectory* está establecido en la ruta de acceso correcta y el parámetro *WitnessShareInUse* muestra **Primary**.

2.  Si el DAG tiene un número par de nodos, se configurará el testigo del recurso compartido de archivos. Ejecute el siguiente comando para validar la configuración del testigo del recurso compartido de archivos en las propiedades del clúster. El valor del parámetro *SharePath* debe apuntar al servidor de archivos y mostrar la ruta de acceso correcta.
    
        Get-ClusterResource -Cluster MBX1 | Get-ClusterParameter | Format-List

3.  A continuación, ejecute el siguiente comando para comprobar el estado del recurso de clúster "Testigo del recurso compartido de archivos". El *State* del recurso de clúster debe mostrar **Online**.
    
        Get-ClusterResource -Cluster MBX1

4.  Por último, revise la carpeta en el Explorador de archivos y los recursos compartidos en el Administrador del servidor para comprobar que el recurso compartido se ha creado correctamente en el servidor de archivos.

## Vea también


[Planificación de alta disponibilidad y resistencia de sitios](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
[Cambios y conmutaciones por error](switchovers-and-failovers-exchange-2013-help.md)  
[Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md)

