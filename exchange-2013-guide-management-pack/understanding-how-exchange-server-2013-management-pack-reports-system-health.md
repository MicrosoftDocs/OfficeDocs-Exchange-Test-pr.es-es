---
title: Módulo de administración de Exchange Server 2013 y estado del sistema
TOCTitle: Descripción de cómo el módulo de administración de Exchange Server 2013 informa el estado del sistema
ms:assetid: 6ca8847f-93fe-458d-bd43-7afad7fdd2f4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn195910(v=EXCHG.150)
ms:contentKeyID: 53181938
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de cómo el módulo de administración de Exchange Server 2013 informa el estado del sistema

 

_**Última modificación del tema:**   2015-03-09_

En este tema, se proporciona información sobre cómo el módulo de administración de Exchange Server 2013 supervisa e informa el estado del sistema de Exchange. En el módulo de administración de Exchange 2013, la información sobre el estado se muestra de una forma simple. En el momento en que un conjunto de mantenimiento aparece en estado incorrecto y se activa el respondedor de transferencia, se registra el siguiente evento en el registro de eventos de Windows:

## Disponibilidad administrada

En Exchange Server 2013, se realizaron varias modificaciones de arquitectura. Una de las modificaciones clave es la característica *Disponibilidad administrada*, en la que todos los componentes de Exchange 2013 tienen monitores integrados que detectan problemas e intentan recuperar la disponibilidad del servicio. El módulo de administración de Exchange 2013 utiliza esta característica. Cualquier problema que no se pueda resolver automáticamente se transfiere al módulo de administración de Exchange 2013 en forma de alerta. Cada componente en Exchange 2013 se autosupervisa mediante tres componentes básicos llamados sondeos, monitores y respondedores.

![Disponibilidad administrada](images/Dn195910.dd5febae-d05e-4089-a3f5-1691b2d9a3d7(EXCHG.150).png "Disponibilidad administrada")

  - **Sondeos** Son conjuntos de recopiladores de datos que miden varios componentes. Hay tres tipos definidos de sondeos:
    
      - Las transacciones sintéticas que miden las operaciones sintéticas de usuarios de un extremo a otro y comprobaciones que miden el tráfico real.
    
      - Comprobaciones que miden el tráfico real de clientes.
    
      - Notificaciones que permiten a Exchange realizar acciones de forma inmediata. Un buen ejemplo de esto es la notificación que se dispara cuando un certificado caduca.

  - **Monitores**   Los datos recopilados por los sondeos se transfieren a monitores que los analizan en busca de condiciones específicas y, según esas condiciones, determinan si el componente particular está en estado correcto o no.

  - **Respondedores**   Si un monitor determina que un componente no está en estado correcto, se activará un respondedor. Si se puede recuperar el problema, el respondedor intentará recuperar el componente con una lógica integrada. Existen varios respondedores disponibles para cada componente, pero el relevante para el módulo de administración de Exchange 2013 es el *Respondedor de transferencia*. Al activarse el Respondedor de transferencia, se genera un evento reconocido por el módulo de administración de Exchange 2013, el cual aporta la información necesaria sobre dicha alerta, lo que proporciona a los administradores la información necesaria para resolver el problema.

Cada componente de Exchange 2013 usa un conjunto específico de sondeos, monitores y respondedores para autosupervisarse. Estas colecciones de sondeos y monitores se denominan *conjuntos de mantenimiento*. Por ejemplo, existe una cantidad de sondeos que recopilan datos sobre varios aspectos del servicio ActiveSync. Estos datos son procesados por un sistema designado de monitores que desencadenan los respondedores correspondientes para corregir cualquier problema que detecten en el servicio ActiveSync. Todos juntos, estos componentes conforman el conjunto de mantenimiento ActiveSync.

Los conjuntos de mantenimiento en Exchange se organizan en las siguientes cuatro categorías que corresponden al panel del módulo de administración:

  - Puntos táctiles del cliente

  - Componentes del servicio

  - Recursos del servidor

  - Dependencias clave

Para ver una lista completa de los conjuntos de mantenimiento de Exchange, consulte [Appendix A: Exchange health sets](appendix-a-exchange-health-sets.md).

Para obtener más información acerca de la función de disponibilidad administrada, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Información sobre el estado

En este tema, se proporciona información sobre cómo el módulo de administración de Exchange Server 2013 supervisa e informa el estado del sistema de Exchange. En el módulo de administración de Exchange 2013, la información sobre el estado se muestra de una forma simple. En el momento en que un conjunto de mantenimiento aparece en estado incorrecto y se activa el respondedor de transferencia, se registra el siguiente evento en el registro de eventos de Windows:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Nombre de registro</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>Origen</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>Fecha</p></td>
<td><p>&lt;<em>fecha y hora del evento</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Id. de evento</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>Categoría de la tarea</p></td>
<td><p>Supervisión</p></td>
</tr>
<tr class="even">
<td><p>Nivel</p></td>
<td><p>Error</p></td>
</tr>
<tr class="odd">
<td><p>Palabras clave</p></td>
<td><p>&lt;<em>ninguno</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Usuario</p></td>
<td><p>SISTEMA</p></td>
</tr>
<tr class="odd">
<td><p>Equipo</p></td>
<td><p>&lt;<em>FQDN del servidor de Exchange</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Descripción</p></td>
<td><p>&lt;<em>generado dinámicamente por el respondedor de transferencia</em>&gt;</p></td>
</tr>
</tbody>
</table>


El agente del módulo de administración detecta y procesa este evento. Con este evento, la disponibilidad administrada puede generar alertas en SCOM. Cuando se resuelve el problema correspondiente y el conjunto de mantenimiento regresa al estado correcto, se registra el siguiente evento en el registro de eventos de Windows:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Nombre de registro</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>Origen</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>Fecha</p></td>
<td><p>&lt;<em>fecha y hora del evento</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Id. de evento</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>Categoría de la tarea</p></td>
<td><p>Supervisión</p></td>
</tr>
<tr class="even">
<td><p>Nivel</p></td>
<td><p>Información</p></td>
</tr>
<tr class="odd">
<td><p>Palabras clave</p></td>
<td><p>&lt;<em>ninguno</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Usuario</p></td>
<td><p>SISTEMA</p></td>
</tr>
<tr class="odd">
<td><p>Equipo</p></td>
<td><p>&lt;<em>FQDN del servidor de Exchange</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Descripción</p></td>
<td><p>&lt;<em>generado dinámicamente por el respondedor de transferencia</em>&gt;</p></td>
</tr>
</tbody>
</table>


Los módulos de administración que supervisaban versiones anteriores de Exchange estaban completamente centralizados. Los agentes de cada servidor de Exchange recopilaban datos y el motor de correlación central comparaba y evaluaba todos los datos que le enviaban los agentes para determinar el estado general del servicio. En los entornos de gran escala, este proceso provocaba correlaciones complejas, generando retrasos en la generación de alertas. Sin embargo, en Exchange 2013 ya no se utiliza la correlación de alertas. En su lugar, cada servidor realiza su propia supervisión y alerta a SCOM en caso de ser necesario, permitiendo una arquitectura altamente escalable.

Según el impacto del evento y el conjunto de mantenimiento que lo activa, el problema se muestra en una categoría diferente de la consola SCOM. Si el evento causa un impacto sobre el usuario, el indicador de puntos táctiles del cliente se muestra como incorrecto. Si ocasiona que un componente entero como OWA no quede disponible, el indicador de componente de servicio se muestra como incorrecto. Si se trata de un problema con un servidor particular, el indicador de estado del servidor correspondiente se muestra como incorrecto. Finalmente, si el problema está relacionado con un recurso del cual Exchange depende, el indicador de dependencias clave se muestra como incorrecto. Para obtener más información acerca de estas categorías, consulte [Introducción al módulo de administración de Exchange Server 2013](getting-started-with-exchange-server-2013-management-pack.md).

