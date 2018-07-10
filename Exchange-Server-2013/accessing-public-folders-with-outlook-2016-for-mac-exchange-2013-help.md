---
title: 'Acceso a las carpetas públicas con Outlook 2016 para Mac: Exchange 2013 Help'
TOCTitle: Acceso a las carpetas públicas con Outlook 2016 para Mac
ms:assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt788631(v=EXCHG.150)
ms:contentKeyID: 74115368
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Acceso a las carpetas públicas con Outlook 2016 para Mac

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016, Office 365_

_**Última modificación del tema:** 2017-05-19_

**Resumen:**  Las últimas topologías de Exchange admitidas que permiten a los usuarios acceder a las carpetas públicas con Outlook 2016 para Mac.

Con las versiones de la [actualización de abril de 2016](https://go.microsoft.com/fwlink/?linkid=829202) de 2016 de Outlook para los clientes de Mac, [14 de actualización acumulativa (CU14)](https://go.microsoft.com/fwlink/p/?linkid=849432) para 2013 de intercambio y [actualización acumulativa 2 (2 CU)](https://go.microsoft.com/fwlink/p/?linkid=849793) de 2016, Exchange, los usuarios de Outlook de 2016 para Mac pueden ahora acceso a carpetas públicas en más tipos de topologías de que podían antes.

## Limitaciones de Outlook para Mac

Todas las versiones de Outlook para Mac pueden acceder a las carpetas públicas de Exchange, pero hasta hace poco estos clientes no podían acceder a las carpetas públicas en los siguientes escenarios de implementación:

  - **Coexistencia con carpetas públicas heredadas.** Cuando está en el buzón de un usuario en un servidor Exchange de 2013 o 2016 de Exchange, el usuario no podría utilizar Outlook para Mac para tener acceso a carpetas públicas implementadas en servidores que ejecutan Exchange 2010 Service Pack 3 o posteriores. Otros clientes pueden tener acceso a estas carpetas públicas heredadas en este escenario.

  - **Topologías híbridas.** Usuarios locales con un buzón basado en Exchange en línea no podrían utilizar Outlook para Mac para tener acceso a las carpetas públicas moderno local. De igual forma, los usuarios que tengan un 2013 de Exchange o Exchange 2016 buzón local no podrían utilizar Outlook para Mac acceso a las carpetas públicas en Exchange había implementado en línea.

## Outlook 2016 para Mac

Con la actualización de abril de 2016 de 2016 de Outlook para Mac, así como CU14 para Exchange 2013 y CU2 para Exchange 2016, los escenarios anteriores ahora funcionará para 2016 de Outlook para los clientes de Mac.

En la siguiente tabla se resumen las topologías admitidas para los usuarios con clientes de Outlook 2016 para Mac que intentan acceder a carpetas públicas en Exchange 2013, Exchange 2016 y Exchange Online.


> [!NOTE]
> Los escenarios que se muestran en la siguiente tabla presuponen que la actualización de abril de 2016 para Outlook 2016 para Mac se ha aplicado en todos los clientes.




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
<th>Las carpetas públicas se implementan en...</th>
<th>El buzón de usuario está en Exchange 2010 SP3 o posterior</th>
<th>El buzón de usuario está en Exchange 2013 CU13 o posterior</th>
<th>El buzón de usuario está en Exchange 2016 CU2 o posterior</th>
<th>El buzón de usuario está en Office 365/Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2010 SP3 o posterior</p></td>
<td><p>Admitido</p></td>
<td><p>Admitido</p></td>
<td><p>Se admite</p></td>
<td><p>No admitido</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2013 CU13 o posterior</p></td>
<td><p>No se admite</p></td>
<td><p>Compatible</p></td>
<td><p>Admitido</p></td>
<td><p>Admitido</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2016 CU2 o posterior</p></td>
<td><p>No se admite</p></td>
<td><p>Compatible</p></td>
<td><p>Admitido</p></td>
<td><p>Admitido</p></td>
</tr>
<tr class="even">
<td><p>Office 365 / Exchange Online</p></td>
<td><p>No se admite</p></td>
<td><p>Compatible</p></td>
<td><p>Admitido</p></td>
<td><p>Admitido</p></td>
</tr>
</tbody>
</table>


En los siguientes artículos se describe cómo implementar carpetas públicas en su organización de Exchange en una topología híbrida o de coexistencia. Siempre que sus clientes de Outlook 2016 para Mac hayan instalado la actualización de abril de 2016, podrán acceder a carpetas públicas en las configuraciones que se detallan en estos artículos:

  - [Configurar las carpetas públicas heredadas en las que se encuentran los buzones de usuario en los servidores de Exchange 2013](configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help.md)

  - [Configuración de las carpetas públicas de Exchange 2013 para una implementación híbrida](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

  - [Configurar las carpetas públicas de Exchange Online para una implementación híbrida](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

