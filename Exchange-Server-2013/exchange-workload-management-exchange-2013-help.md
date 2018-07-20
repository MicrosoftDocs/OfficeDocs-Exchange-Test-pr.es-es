---
title: 'Administración de carga de trabajo de Exchange: Exchange 2013 Help'
TOCTitle: Administración de carga de trabajo de Exchange
ms:assetid: 276740c4-bdb7-49f1-9470-ae6f2bfd65aa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150503(v=EXCHG.150)
ms:contentKeyID: 48267911
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administración de carga de trabajo de Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-11-16_

Una carga de trabajo de Exchange es una característica de un servidor, un protocolo o un servicio de Exchange que se definió de manera explícita para fines de administración de recursos del sistema de Exchange. Cada carga de trabajo de Exchange consume recursos del sistema como CPU, operaciones de la base de datos de buzones de correo o solicitudes de Active Directory, para ejecutar solicitudes del usuario o trabajos en segundo plano. Ejemplos de las cargas de trabajo de Exchange incluyen Outlook Web App, Exchange ActiveSync, migración de buzones de correo y el Asistentes para buzones de correo.

Las cargas de trabajo de Exchange se administran controlando la forma en que los usuarios individuales consumen los recursos (lo que a veces se conoce como limitación de peticiones de usuarios en Exchange 2010). El control de la forma en que los usuarios individuales consumían los recursos del sistema de Exchange era posible en Exchange Server 2010, y esta capacidad se ha ampliado para Exchange Server 2013.


> [!NOTE]
> La administración de cargas de trabajo mediante la supervisión del mantenimiento de los recursos del sistema en los servidores de Exchange de la organización solo debe realizarse bajo la dirección del servicio de soporte y atención al cliente de Microsoft.



## Administrar cargas de trabajo mediante el control de cómo los usuarios individuales consumen los recursos

La funcionalidad de limitación se mejora en Exchange 2013. La funcionalidad de limitación le ayuda a garantizar que el consumo excesivo de recursos por parte de usuarios individuales no afecta negativamente el rendimiento del servidor ni la experiencia de usuario.

De forma predeterminada, la limitación de usuarios en Exchange 2013 permite a los usuarios incrementar el consumo de recursos durante breves períodos sin experimentar ninguna reducción en el ancho de banda. Además, el bloqueo completo de los usuarios que usan una gran cantidad de recursos será infrecuente o no se producirá nunca. En lugar de bloquear por completo la realización de operaciones de un usuario, se lleva a cabo la limitación y se demoran los procesos durante breves periodos de tiempo (piense en estos como "microdemoras") que se producen antes de que causen un impacto significativo en un servidor.

**Puntos destacados de la función**

A continuación tiene unos elementos destacados de la forma en que Exchange controla cómo los usuarios individuales consumen los recursos en Exchange 2013:

  - **Concesiones de ráfaga**   Las concesiones de ráfaga permiten a los usuarios realizar breves periodos de un mayor consumo de recursos sin experimentar limitaciones.

  - **Velocidad de recarga**   La velocidad de recarga administra el consumo de los recursos de los usuarios usando un sistema de presupuestos del sistema. Puede establecer la velocidad de recarga de los presupuestos de recursos de los usuarios. Por ejemplo, un valor de 600.000 (en milisegundos) implica que los presupuestos de los usuarios se recargaran a una velocidad de diez minutos del uso por hora.

  - **Moldeador de tráfico**   Cuando el uso del recurso de un usuario alcanza un límite configurado durante un período de tiempo, se demora al usuario durante períodos de tiempo muy cortos antes de que provoque un impacto significativo en un servidor. Los usuarios generalmente no notan estos "micro retrasos". Este proceso permite a Exchange 2013 moldear el tráfico de forma eficiente sin bloquear a usuarios y evitar que sean productivos. El moldeador de tráfico tiene un impacto menor en los usuarios que el bloqueo temprano, y reduce significativamente las posibilidades de que se produzca un bloqueo.

  - **Uso máximo**   En raras circunstancias, un usuario puede consumir una cantidad muy elevada de recursos durante un período de tiempo corto. Como precaución, a un usuario que alcance un umbral de uso máximo puede que se le bloqueen temporalmente sus recursos. Los usuarios a los cuales se les bloquee temporalmente el uso de los recursos se desbloquean tan pronto se recargan sus presupuestos de uso.

Para obtener una lista de cmdlets que pueda usar para controlar la forma en que los usuarios individuales consumen los recursos, vea “Cmdlets para controlar cómo los usuarios individuales usan los recursos” más adelante en este tema.

**Funcionalidad de limitación y consideraciones de la implementación de Exchange 2013**

Independientemente de si realiza una instalación limpia de Exchange 2013 o instala Exchange 2013 en un entorno de coexistencia que incluya equipos con Exchange 2010, todos los usuarios con buzones de correo en equipos que ejecuten Exchange 2013 se limitan mediante la nueva funcionalidad de limitación de Exchange 2013. Sin embargo, los buzones de Exchange 2010 continuarán limitados por la funcionalidad de limitación de Exchange 2010 al acceder a sus buzones mediante los servidores de acceso de clientes de Exchange 2010.

Cuando se instala Exchange 2013 en un entorno de coexistencia, el proceso de instalación de Exchange 2013 puede intentar continuar con algunas de las configuraciones de limitación de usuarios que ya había definido en la configuración de Exchange 2010. Sin embargo, la funcionalidad de limitación de Exchange 2013 es tan diferente que el impacto de cualquier configuración de limitación de usuarios anterior generalmente no afectará al funcionamiento de la limitación en Exchange 2013.

**Administración de directivas de limitación mediante ámbitos**

Similar a Exchange 2010, hay una única directiva de limitación predeterminada en Exchange 2013. En Exchange 2013, la directiva de limitación predeterminada se denomina **GlobalThrottlingPolicy**. Esta directiva tiene un ámbito **Global**. Los otros ámbitos de limitación de usuarios disponibles son **Organization** y **Regular**. Debido a la presentación de la asignación del ámbito de las directivas de limitación de usuarios de Exchange 2013, administra las directivas de limitación de forma diferente a la de Exchange 2010. El **GlobalThrottlingPolicy** define la configuración de limitación predeterminada de línea base para cada usuario nuevo y existente en la organización a no ser que tenga directivas de limitaciones personalizadas en la organización. En muchos casos de implementación típicos de Exchange, el **GlobalThrottlingPolicy** será adecuado para administrar a sus usuarios.

Le recomendamos encarecidamente que no personalice la configuración de limitaciones modificando **GlobalThrottlingPolicy**. En su lugar, debería crear directivas de limitación adicionales. La creación de directivas de limitación adicionales le ayudará a administrar mejor sus cargas de trabajo. También evitará que las modificaciones de la configuración de directivas de limitación se ignoren con actualizaciones futuras de Exchange 2013.

Para personalizar la configuración de limitaciones que se aplican a todos los usuarios de la organización, cree una nueva directiva de limitación con la asignación del ámbito **Organization**. En las nuevas directivas de ámbito de organización, sólo debería establecer configuraciones de limitaciones diferentes a las de **GlobalThrottlingPolicy**. Para personalizar la configuración de limitaciones que se aplican sólo a usuarios concretos de la organización, cree una nueva directiva de limitación con la asignación del ámbito **Regular**. En las nuevas directivas de ámbito regular, sólo debería establecer configuraciones de limitaciones diferentes a las de **GlobalThrottlingPolicy** y otras directivas de organización. Esto le ayudará a heredar el resto de configuraciones de directivas de **GlobalThrottlingPolicy** y le permitirá beneficiarse de actualizaciones de las directivas de limitaciones que se agreguen a actualizaciones futuras de Exchange.

## Administrar la configuración de la limitación de carga de trabajo

Administra la configuración de la limitación de la carga de trabajo de Exchange con el Shell de administración de Exchange.

**Cmdlets para controlar cómo los usuarios individuales utilizan los recursos**

Administra la configuración de limitaciones con los siguientes cmdlets, que se presentaron en Exchange 2010:

Administrar directivas de limitación

  - [Get-ThrottlingPolicy](https://technet.microsoft.com/es-es/library/dd351264\(v=exchg.150\))

  - [New-ThrottlingPolicy](https://technet.microsoft.com/es-es/library/dd351045\(v=exchg.150\))

  - [Remove-ThrottlingPolicy](https://technet.microsoft.com/es-es/library/dd351178\(v=exchg.150\))

  - [Set-ThrottlingPolicy](https://technet.microsoft.com/es-es/library/dd298094\(v=exchg.150\))

Asignar directivas de limitación

  - [Get-ThrottlingPolicyAssociation](https://technet.microsoft.com/es-es/library/ff459241\(v=exchg.150\))

  - [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/es-es/library/ff459231\(v=exchg.150\))


> [!NOTE]
> Los cmdlets de administración de carga de trabajo del sistema <STRONG>*-ResourcePolicy</STRONG>, <STRONG>*-WorkloadManagementPolicy</STRONG> y <STRONG>*-WorkloadPolicy</STRONG> han quedado obsoletos. Las opciones de administración de carga de trabajo del sistema se deben personalizar solo bajo la dirección del servicio de soporte y atención al cliente de Microsoft.


