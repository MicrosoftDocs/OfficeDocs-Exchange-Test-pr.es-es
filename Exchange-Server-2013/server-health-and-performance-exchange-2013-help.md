---
title: 'Rendimiento y mantenimiento del servidor: Exchange 2013 Help'
TOCTitle: Rendimiento y mantenimiento del servidor
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 48268481
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Rendimiento y mantenimiento del servidor

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Entender el rendimiento y el estado del servidor es vital para diseñar y mantener una infraestructura de mensajería de alto rendimiento. Microsoft Exchange Server 2013 introduce mejoras en el rendimiento y la salud del servidor.

¿Busca una lista de todos los temas de salud y el rendimiento de servidor? Vea Documentación sobre rendimiento y estado del servidor.

## Disponibilidad administrada

Exchange 2013 introduce el concepto de *disponibilidad administrada*. Disponibilidad administrada se ejecuta en cada servidor Exchange 2013. Se compone de dos procesos: administración de carga de trabajo del sistema (MSExchangeHMHost.exe) y administración de carga de trabajo del usuario (MSExchangeHMWorker.exe), y contiene los siguientes componentes asincrónicos:

  - **Motor de la sonda** El *motor de la sonda* realiza mediciones en el servidor.

  - **Supervisión del motor de la sonda**   La *supervisión del motor de la sonda* almacena la lógica empresarial sobre aquello que constituye un estado correcto. Funciona como un motor de reconocimiento de patrones, que busca patrones y mediciones que difieren de un estado correcto para evaluar si un componente o característica presentan o no un mal estado.

  - **Motor de respuesta**   Cuando el *motor de respuesta* recibe una alerta sobre un componente en mal estado, la primera acción será intentar recuperar dicho componente. La disponibilidad administrada permite acciones de recuperación gradual. El primer intento consistirá en reiniciar el grupo de aplicaciones, el segundo en reiniciar el servicio correspondiente, y el tercer intento será reiniciar el servidor. El intento final consistirá en desconectar el servidor, de manera que deje de aceptar tráfico. En caso de que todo lo anterior falle, se enviará una alerta al servicio de asistencia.

Para obtener más información acerca de la disponibilidad administrada, vea [Disponibilidad administrada](managed-availability-exchange-2013-help.md).

## Administración de la carga de trabajo

Exchange 2013 la administración de la carga de trabajo incluye los siguientes componentes:

  - *La administración de la carga de trabajo del usuario* es el nuevo nombre de las características de limitación del usuario en Exchange Server 2010. Puede personalizar estas opciones según las necesidades de su entorno.

  - *La administración de carga de trabajo del sistema* es nueva en Exchange 2013 y se usa para limitar automáticamente cargas de trabajo específicas de Exchange supervisando el mantenimiento de los recursos clave del servidor. Estas opciones se deben personalizar solo con la dirección de Servicio de soporte y atención al cliente de Microsoft.

Para obtener más información, vea [Administración de carga de trabajo de Exchange](exchange-workload-management-exchange-2013-help.md).

## Documentación sobre rendimiento y estado del servidor

La siguiente tabla contiene enlace a temas que le ayudarán a aprender y administrar el rendimiento y estado del servidor en Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tema</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="exchange-workload-management-exchange-2013-help.md">Administración de carga de trabajo de Exchange</a></p></td>
<td><p>Obtenga información sobre cómo administrar cargas de trabajo de Exchange mediante el control de cómo los usuarios individuales consumen los recursos.</p></td>
</tr>
<tr class="even">
<td><p><a href="managed-availability-exchange-2013-help.md">Disponibilidad administrada</a></p></td>
<td><p>Obtenga información sobre las acciones de recuperación y supervisión de recursos integradas que están disponibles en Exchange 2013.</p></td>
</tr>
</tbody>
</table>

