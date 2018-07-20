---
title: 'Coexistencia con Office Communications Server 2007 R2 y Lync Server: Exchange 2013 Help'
TOCTitle: Coexistencia con Office Communications Server 2007 R2 y Lync Server
ms:assetid: f12d65c7-0b2c-46a1-a14a-802a76296fa1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ851069(v=EXCHG.150)
ms:contentKeyID: 50556908
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Coexistencia con Office Communications Server 2007 R2 y Lync Server

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-03-09_

Communications Server 2007 R2 y Lync Server ofrecen muchas características para el usuario final, como la mensajería instantánea (MI), presencia o MI entre varias entidades. Además, la funcionalidad de correo de voz se puede integrar en la mensajería unificada (UM) de Exchange. En las implementaciones que integran Lync Server 2010 o 2013, los usuarios se pueden habilitar para Enterprise Voice, lo que permite a aquellos usuarios que estén habilitados para el acceso a correo de voz que tengan acceso a dicho correo a través de los componentes de Lync Server.

Cuando se integra la mensajería unificada en versiones anteriores de Office Communications Server o Lync Server, no están disponibles todas las características. Para que los usuarios aprovechen al máximo las nuevas y mejoradas características para el usuario final, como las fotografías en alta resolución, el almacén de contactos unificado y la integración de archivo de Lync, deben tener cuentas de usuario en Lync Server 2013 y en Exchange Server 2013 y usar la última versión del software de cliente de Lync 2013. Por ejemplo, el almacén de contactos unificado no está disponible para los usuarios que se hayan habilitado para Enterprise Voice en Lync Server 2010. Asimismo, las fotografías en alta resolución no se pueden mostrar en Lync 2010.

Al integrar la mensajería unificada de Exchange en Office Communications Server 2007 R2 o Lync Server 2010, puede que tenga que instalar revisiones adicionales, paquetes o actualizaciones acumulativas y service packs en los servidores de Office Communications Server 2007 R2 o Lync 2010 que se hayan implementado en la organización. Los componentes que deba instalar dependerán de la topología de la implementación y de las versiones de producto que vaya a integrar con la mensajería unificada de Exchange.

## Revisiones, paquetes y actualizaciones acumulativas y service packs necesarios

En la siguiente tabla se muestran las revisiones que se requieren para las versiones de los productos a fin de integrarlos con la mensajería unificada.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Actualización acumulativa 10 de Office Communications Server 2007 R2 o posterior.</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>Actualización acumulativa 3 de Lync Server 2010 o posterior.</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>No se necesitan actualizaciones.</p></td>
</tr>
</tbody>
</table>

