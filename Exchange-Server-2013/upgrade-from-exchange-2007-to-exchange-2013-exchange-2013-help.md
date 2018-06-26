---
title: 'Actualizar de Exchange 2007 a Exchange 2013: Exchange 2013 Help'
TOCTitle: Actualizar de Exchange 2007 a Exchange 2013
ms:assetid: a604b96d-2a51-480f-937f-45ad753c2cad
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ898581(v=EXCHG.150)
ms:contentKeyID: 51406536
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Actualizar de Exchange 2007 a Exchange 2013

 

_**Se aplica a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Microsoft Exchange Server 2010 y Exchange Server 2007 tienen múltiples roles de servidor: acceso de cliente, buzón de correo, transporte de concentradores, mensajería unificada y transporte perimetral. Con Exchange Server 2013, el número de roles de servidor se reduce de cinco a tres: acceso de cliente, buzón de correo y transporte perimetral. Ahora, la mensajería unificada se considera un componente o subfunción de las características relacionadas con la voz que se ofrecen en Exchange 2013. (Para obtener más información acerca de los cambios, vea "Arquitectura de Exchange 2013" en [Novedades en Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)).

Cuando actualiza su organización existente de Exchange 2007 a Exchange 2013, existe un período en el que coexisten los servidores de Exchange 2007 y de Exchange 2013 dentro de su organización. Puede mantener este modo durante un período de tiempo indefinido o completar inmediatamente la actualización a Exchange 2013 moviendo todos los recursos de Exchange 2007 a Exchange 2013 y, a continuación, retirando los servidores de Exchange 2007. Se da una situación de coexistencia si se cumplen las siguientes condiciones:

  - Exchange 2013 se implementa en una organización existente de Exchange.

  - Existe más de una versión de Microsoft Exchange que proporciona servicios de mensajería a la organización.

No puede actualizar una organización de Exchange 2003 existente directamente a Exchange 2013. Primero debe actualizar la organización de Exchange 2003 a una organización de Exchange 2007 o Exchange 2010, y luego puede actualizar la organización de Exchange 2007 o Exchange 2010 a Exchange 2013. Le recomendamos que actualice su organización de Exchange 2003 a Exchange 2010, y luego actualice de Exchange 2010 a Exchange 2013.


> [!WARNING]
> Debe eliminar todas las instancias de Exchange 2003 de su organización antes de poder actualizar a Exchange 2013.



Puede migrar todos los buzones de Exchange 2003 a Exchange Online. Para obtener más información sobre este enfoque, consulte [Formas de migrar varias cuentas de correo electrónico a Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

En la siguiente tabla, se enumeran los casos en los que se admite la coexistencia de Exchange 2013 y versiones anteriores de Exchange.

### Coexistencia de Exchange 2013 y versiones anteriores de Exchange Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versión de Exchange</th>
<th>Coexistencia de organización de Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 y versiones anteriores</p></td>
<td><p>No se admite</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>Compatible con las siguientes versiones mínimas de Exchange:</p>
<ul>
<li><p>1Paquete acumulativo de actualizaciones 10 para Exchange 2007 Service Pack 3 (SP3) en todos los servidores Exchange 2007 de la organización, incluidos los servidores de transporte perimetral.</p></li>
<li><p>Actualización acumulativa 2 (CU2) de Exchange 2013 o posterior en todos los servidores Exchange 2013 de la organización.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Compatible con las siguientes versiones mínimas de Exchange:</p>
<ul>
<li><p>2 Exchange 2010 SP3 en todos los servidores Exchange 2010 de la organización, incluidos los servidores de transporte perimetral.</p></li>
<li><p>CU2 de Exchange 2013 o posterior en todos los servidores Exchange 2013 de la organización.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Organización mixta de Exchange 2010 y Exchange 2007</p></td>
<td><p>Compatible con las siguientes versiones mínimas de Exchange:</p>
<ul>
<li><p>1Paquete acumulativo de actualizaciones 10 para Exchange 2007 SP3 en todos los servidores Exchange 2007 de la organización, incluidos los servidores de transporte perimetral.</p></li>
<li><p>2 Exchange 2010 SP3 en todos los servidores Exchange 2010 de la organización, incluidos los servidores de transporte perimetral.</p></li>
<li><p>CU2 de Exchange 2013 o posterior en todos los servidores Exchange 2013 de la organización.</p></li>
</ul></td>
</tr>
</tbody>
</table>


1 Si quiere crear una suscripción de EdgeSync entre un servidor de transporte de concentradores de Exchange 2007 y un servidor de transporte perimetral de Exchange 2013 SP1, deberá instalar el paquete acumulativo de actualizaciones 13 de Exchange 2007 SP3 o posterior en el servidor de transporte de concentradores de Exchange 2007.

2 Si quiere crear una suscripción de EdgeSync entre un servidor de transporte de concentradores de Exchange 2010 y un servidor de transporte perimetral de Exchange 2013 SP1, deberá instalar el paquete acumulativo de actualizaciones 5 de Exchange 2010 SP3 o posterior en el servidor de transporte de concentradores de Exchange 2010.

## Coexistencia del modo mixto de Exchange 2013 y Exchange 2007 con Exchange 2010

Si cuenta con sitios de Active Directory que tienen instalado Exchange 2010y Exchange 2007, siga las instrucciones de actualización de Exchange 2010 y Exchange 2007, y complete los pasos de actualización necesarios para ambos sistemas.

## Introducción al proceso de actualización

Para ayudarle a obtener información general del proceso de actualización de Exchange 2007 a Exchange 2013, hemos recopilado recursos relacionados con cada una de las tareas principales en la siguiente tabla. Para obtener una guía específica paso a paso, vea [Lista de comprobación: Actualización desde Exchange 2007](checklist-upgrade-from-exchange-2007-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tarea</th>
<th>Tema</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Obtenga más información acerca de los roles y componentes de Exchange 2013</p></td>
<td><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Novedades en Exchange 2013</a></p>
<p><a href="client-access-server-exchange-2013-help.md">Servidor de acceso de cliente</a></p>
<p><a href="mailbox-server-exchange-2013-help.md">Servidor de buzones de correo</a></p>
<p><a href="mail-flow-exchange-2013-help.md">Flujo de correo</a></p>
<p><a href="unified-messaging-exchange-2013-help.md">Mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p>Instalar Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar Exchange 2013 utilizando el asistente de configuración</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Instalar el rol de transporte perimetral de Exchange 2013 mediante el asistente de instalación</a> (opcional)</p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Comprobar una instalación de Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Agregar certificados digitales al servidor de acceso de cliente</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuración del servidor de acceso de cliente de Exchange 2013</a></p>
<p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificados digitales y SSL</a></p>
<p><a href="create-a-digital-certificate-request-exchange-2013-help.md">Crear una solicitud de certificado digital</a></p></td>
</tr>
<tr class="even">
<td><p>Configurar los directorios virtuales relacionados con Exchange</p></td>
<td><p><a href="default-settings-for-exchange-virtual-directories-exchange-2013-help.md">Configuración predeterminada para directorios virtuales de Exchange</a></p></td>
</tr>
<tr class="odd">
<td><p>Mover buzones deExchange 2010</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimientos de buzones de Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurar componentes de transporte</p></td>
<td><p><a href="edge-subscriptions-exchange-2013-help.md">Suscripciones perimetrales</a> (necesario únicamente si ha instalado un servidor de transporte perimetral)</p>
<p><a href="mail-routing-exchange-2013-help.md">Enrutamiento de correo</a></p>
<p><a href="shadow-redundancy-exchange-2013-help.md">Redundancia de instantánea</a></p>
<p><a href="delivery-reports-for-administrators-exchange-2013-help.md">Informes de entrega para administradores</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurar e implementar la mensajería unificada</p></td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Diseño de mensajería unificada</a></p>
<p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Implementación del correo de voz y mensajería unificada</a></p></td>
</tr>
</tbody>
</table>

