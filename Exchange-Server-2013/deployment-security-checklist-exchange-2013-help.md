---
title: 'Lista de comprobación de seguridad de la implementación: Exchange 2013 Help'
TOCTitle: Lista de comprobación de seguridad de la implementación
ms:assetid: 0cbfad59-f503-48a0-8184-6ca999d89e61
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996026(v=EXCHG.150)
ms:contentKeyID: 49116021
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Lista de comprobación de seguridad de la implementación

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Las funciones de Microsoft Exchange Server 2013 están diseñadas para mejorar la seguridad de su entorno de mensajería. En general, para Exchange 2013, se cumplen las siguientes condiciones:

  - Las cuentas que usa Exchange 2013 tienen los derechos mínimos necesarios para realizar los conjuntos de tareas determinados.

  - De forma predeterminada, los servicios se inician solamente cuando se necesitan.

  - Los derechos de una lista de control de acceso (ACL) para objetos de Exchange se minimizan.

  - Los permisos administrativos se establecen de acuerdo con el ámbito de cambio del objeto que requiere una modificación determinada.

  - De forma predeterminada, todas las rutas de mensajes predeterminados internos están cifradas.

Este tema muestra una lista de los pasos que se recomiendan seguir para proteger el entorno de mensajería antes de instalar Microsoft Exchange. Es aconsejable consultar esta lista de comprobación cada vez que instale una nueva función del servidor Exchange.

Antes de instalar Exchange 2013, realice los siguientes procedimientos.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Procedimiento</th>
<th>¿Listo?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ejecute <a href="https://go.microsoft.com/fwlink/p/?linkid=54836">Microsoft Update</a>.</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Ejecute la Herramienta de la eliminación de software malintencionado de Microsoft Windows. La Herramienta de eliminación de software malintencionado se incluye con una Actualización de Microsoft. Para obtener más información, consulte <a href="http://go.microsoft.com/fwlink/p/?linkid=73452">Herramienta para la eliminación de software malintencionado</a> .</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Ejecute <a href="https://go.microsoft.com/fwlink/p/?linkid=16526">Microsoft Baseline Security Analyzer</a>.</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

