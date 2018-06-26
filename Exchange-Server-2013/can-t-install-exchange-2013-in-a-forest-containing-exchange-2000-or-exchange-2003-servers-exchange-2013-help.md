---
title: 'No es posible instalar Exchange 2013 en un bosque que contenga servidores de Exchange 2000 o Exchange 2003.: Exchange 2013 Help'
TOCTitle: No es posible instalar Exchange 2013 en un bosque que contenga servidores de Exchange 2000 o Exchange 2003.
ms:assetid: a115b182-cbd2-4d31-aa0e-375240939301
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.exchange2000or2003presentinorg(v=EXCHG.150)
ms:contentKeyID: 49116421
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No es posible instalar Exchange 2013 en un bosque que contenga servidores de Exchange 2000 o Exchange 2003.

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2016-12-09_

Microsoft Exchange Server 2013 no puede continuar porque se encontraron uno o varios equipos que ejecutan Exchange 2000 Server o Exchange Server 2003 en el bosque de Active Directory. Antes de que pueda instalar Exchange 2013, hay que eliminar todos los servidores de Exchange 2000 y Exchange 2003 del bosque. Los buzones de correo, las carpetas públicas y todos los objetos o componentes de Exchange tienen que actualizarse a Exchange Server 2007 o Exchange Server 2010. No puede actualizar desde Exchange 2000 o Exchange 2003 directamente a Exchange 2013.

La ruta que debe seguir para instalar Exchange 2013 en su organización depende de la versión de Exchange que tenga instalada actualmente en su bosque. Consulte la tabla siguiente para obtener más información.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Si tiene lo siguiente instalado en su organización</th>
<th>Debe tomar esta ruta para actualizar a Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2000</p></td>
<td><ol>
<li><p>Instalar Exchange 2007 en su organización de Exchange 2000.</p></li>
<li><p>Configurar la coexistencia de Exchange 2007 y Exchange 2000.</p></li>
<li><p>Migrar los buzones de correo, las carpetas públicas y el resto de componentes de Exchange 2000 a Exchange 2007.</p></li>
<li><p>Decomisar y quitar todos los servidores de Exchange 2000.</p></li>
<li><p>Instalar Exchange 2013 en su organización de Exchange 2007.</p></li>
<li><p>Configurar la coexistencia de Exchange 2013 y Exchange 2007.</p></li>
<li><p>Migrar los buzones de correo, las carpetas públicas y el resto de componentes de Exchange 2007 a Exchange 2013.</p></li>
<li><p>Decomisar y quitar todos los servidores de Exchange 2007.</p></li>
</ol>
<p>Para obtener más información, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=103281">Actualización a Exchange 2007</a> y <a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Actualizar de Exchange 2007 a Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2003</p></td>
<td><ol>
<li><p>Instalar Exchange 2010 en su organización de Exchange 2003.</p></li>
<li><p>Configurar la coexistencia de Exchange 2010 y Exchange 2003.</p></li>
<li><p>Migrar los buzones de correo, las carpetas públicas y el resto de componentes de Exchange 2003 a Exchange 2010.</p></li>
<li><p>Decomisar y quitar todos los servidores de Exchange 2003.</p></li>
<li><p>Instalar Exchange 2013 en su organización de Exchange 2010.</p></li>
<li><p>Configurar la coexistencia de Exchange 2013 y Exchange 2010.</p></li>
<li><p>Migrar los buzones de correo, las carpetas públicas y el resto de componentes de Exchange 2010 a Exchange 2013.</p></li>
<li><p>Decomisar y quitar todos los servidores de Exchange 2010.</p></li>
</ol>
<p>Para obtener más información, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=268414">Exchange 2003 - Guía de planeamiento para la actualización y coexistencia</a> y <a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Actualizar de Exchange 2010 a Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


Cuando actualice a Exchange 2010 o Exchange 2013, puede usar el Asistente para la implementación de Exchange para ayudarle a completar su implementación. Para obtener más información, consulte los siguientes vínculos:

  - [Asistente de implementación de Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=171086)

  - [Asistente de implementación de Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=277105)

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

