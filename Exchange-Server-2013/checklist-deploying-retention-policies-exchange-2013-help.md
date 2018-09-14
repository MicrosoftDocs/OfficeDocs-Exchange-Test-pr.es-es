---
title: 'Lista de comprobación: implementación directivas retención: Exchange 2013 Help'
TOCTitle: 'Lista de comprobación: implementación de directivas de retención'
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 49895645
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Lista de comprobación: implementación de directivas de retención

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Esta lista de comprobación se puede usar para implementar directivas de retención en su organización de Microsoft Exchange Server 2013. Antes de comenzar a trabajar con esta lista de comprobación, asegúrese de estar familiarizado con los conceptos en los temas siguientes:

  - [Administración de registros de mensajes](https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/messaging-records-management)

  - [Etiquetas de retención y directivas de retención](https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/retention-tags-and-policies)

## Lista de comprobación para la implementación de directivas de retención


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>¿Listo?</th>
<th>Tareas</th>
<th>Recursos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p> </p></td>
<td><p>Evaluar los requisitos de Administración de registros de mensajería (MRM) para distintos conjuntos de usuarios.</p></td>
<td><p><a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/messaging-records-management">Administración de registros de mensajes</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Determinar qué de versiones del cliente Microsoft Outlook están en uso.</p></td>
<td><p>Analizar los archivos de registro del acceso de clientes RPC que están ubicados en <code>%ExchangeInstallPath%Logging\RPC Client Access</code>.</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Crear etiquetas de retención.</p></td>
<td><p><a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">Crear directivas de retención</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Crear directivas de retención.</p></td>
<td><p><a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">Crear directivas de retención</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Agregar etiquetas de retención a las directivas de retención.</p></td>
<td><p><a href="add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md">Agregar etiquetas de retención o quitar etiquetas de retención de una directiva de retención</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Colocar buzones en la suspensión de la retención.</p></td>
<td><p><a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">Poner un buzón en retención</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Aplicar una directiva de retención a un único buzón para realizar pruebas.</p></td>
<td><p><a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/apply-retention-policy">Aplicar una directiva de retención a los buzones</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Opcional: Implementar un bloqueo de clientes para bloquear clientes heredados de Outlook.</p></td>
<td><p><a href="configure-outlook-client-blocking-exchange-2013-help.md">Configurar el bloqueo de clientes de Outlook para la administración de registros de mensajería</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Comenzar la comunicación de usuario y las actividades de entrenamiento. Incluir una fecha límite cuando se procesen directivas de retención y los elementos movidos o eliminados.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Aplicar una directiva de retención a buzones adicionales.</p></td>
<td><p><a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/apply-retention-policy">Aplicar una directiva de retención a los buzones</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Con unos días de anticipación, recuerde a los usuarios acerca de la fecha límite.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>En la fecha límite, quitar la suspensión de la retención de los buzones.</p></td>
<td><p><a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">Poner un buzón en retención</a></p></td>
</tr>
</tbody>
</table>

