---
title: 'Autorizar llamadas mediante reglas de marcado: Exchange 2013 Help'
TOCTitle: Autorizar llamadas mediante reglas de marcado
ms:assetid: 4c18bc07-f55c-42b7-81c1-729878aa93aa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ898499(v=EXCHG.150)
ms:contentKeyID: 51406507
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizar llamadas mediante reglas de marcado

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-03-09_

De manera predeterminada, los usuarios no pueden realizar llamadas salientes. Para especificar los tipos de llamadas que los usuarios realizan, debe crear primero reglas de marcado y, a continuación, autorizar a los grupos de dichas reglas de marcado en planes de marcado de mensajería unificada, directivas de buzón de correo de mensajería unificada u operadores automáticos de mensajería unificada. Antes de autorizar los grupos de reglas de marcado, primero tiene que definir las reglas de marcado para el plan de marcado de mensajería unificada. Para obtener información detallada, consulte [Crear reglas de marcado para usuarios](create-dialing-rules-for-users-exchange-2013-help.md).

Cada regla de marcado que cree contendrá los tipos de llamadas o patrones de números a los que quiera proporcionar acceso a los usuarios. Puede autorizar a diferentes tipos de usuarios para que realicen diferentes tipos de llamadas. Las llamadas que autorice pueden ser dentro de un país o región, o pueden ser internacionales.

Para autorizar o restringir el marcado, deben configurarse correctamente los siguientes ajustes:

  - **Reglas de marcado**   Las reglas de marcado definen el número que marcan los usuarios con mensajería unificada así como el número que se enviará desde la mensajería unificada y que marcará la central de conmutación (PBX) o la IP PBX. Puede crear un grupo de reglas de marcado añadiendo una regla de marcado. Después de crear un grupo de reglas de marcado, debe añadirlo a la lista de llamadas autorizadas para un grupo de reglas de marcado nacional/regional o internacional.

  - **Grupos de reglas de marcado**   Los grupos de reglas de marcado determinan el tipo de llamadas que pueden realizar los usuarios de un grupo de marcado.

  - **Autorizaciones de marcado**   Las autorizaciones de marcado determinan las restricciones que se aplicarán para evitar que los usuarios generen gastos innecesarios de teléfono o realicen llamadas a larga distancia.

## ¿Cómo autorizo un grupo de reglas de marcado?

Se autorizan los grupos de reglas de marcado en función del tipo de autores de llamada que quiere autorizar para realizar llamadas. Por ejemplo, si quiere que sólo los usuarios de Outlook Voice Access puedan realizar llamadas, deber crear las reglas de marcado y, a continuación, autorizar dichos grupos de reglas de marcado en la directiva de buzón de correo de mensajería unificada a la que los usuarios de Outlook Voice Access estén vinculados. La siguiente tabla muestra cómo autorizar llamadas para diferentes tipos de autores de llamada.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de autor de llamada</th>
<th>Autorizar grupos de reglas de marcado aquí</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autores de llamada no autenticados que llamen a un número de Outlook Voice Access y no escriban un PIN</p></td>
<td><p>Plan de marcado de MU. Para obtener información detallada, consulte <a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Autorizar llamadas a los usuarios en un plan de marcado</a>.</p></td>
</tr>
<tr class="even">
<td><p>Autores de llamada autenticados que llamen a un número de Outlook Voice Access y escriban un PIN</p></td>
<td><p>Directiva de buzón de correo de mensajería unificada para el autor de llamada. Para obtener información detallada, consulte <a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">¿Autorizar llamadas para un grupo de usuarios</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Autores de llamada no autenticados que llamen a un número de teléfono que está configurado en un operador automático de mensajería unificada</p></td>
<td><p>Operador automático de mensajería unificada. Para obtener información detallada, consulte <a href="authorize-calls-for-auto-attendant-callers-exchange-2013-help.md">¿Autorizar llamadas de llamadores de operador automático</a>.</p></td>
</tr>
</tbody>
</table>


En función de qué usuarios ha autorizado para realizar llamadas salientes, deberá utilizar la página **Autorización de marcado** en el Centro de administración de Exchange (EAC) para el plan de marcado, el operador automático y la directiva de buzones de correo de mensajería unificada.

