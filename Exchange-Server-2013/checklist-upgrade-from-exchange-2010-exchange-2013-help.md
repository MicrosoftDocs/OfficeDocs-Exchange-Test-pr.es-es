---
title: 'Lista de comprobación: Actualización desde Exchange 2010: Exchange 2013 Help'
TOCTitle: 'Lista de comprobación: Actualización desde Exchange 2010'
ms:assetid: 06c1045a-5fcf-4e24-a901-1a979302fb8d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee332309(v=EXCHG.150)
ms:contentKeyID: 51406471
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Lista de comprobación: Actualización desde Exchange 2010

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Utilice esta lista de comprobación para actualizarse de Microsoft Exchange 2010 a Exchange 2013. Antes de empezar con la lista de comprobación, debe estar familiarizado con los conceptos que se explican en:

  - [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Novedades en Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)

Esta lista de comprobación es genérica ya que brinda una guía para un escenario de actualización típico.


> [!NOTE]
> El Asistente de implementación de Exchange Server proporciona indicaciones personalizadas paso a paso acerca de cómo implementar Exchange Server. El Asistente de implementación le puede ayudar a implementar una nueva instalación de Exchange Server 2013, actualizar una versión anterior a Exchange 2013 o configurar una implementación híbrida de Exchange 2013 y Exchange Online. Para obtener más información, consulte <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Asistente para la implementación de Exchange Server</A>.



## Lista de comprobación para actualizar de Exchange 2010 a Exchange 2013


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>¿Listo?</p></td>
<td><p>Tarea</p></td>
<td><p>Tema(s)</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Leer las notas de versión.</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de la versión de Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>2. Comprobar los requisitos del sistema</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos del sistema para Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>3. Confirmar la realización de los pasos de requisitos previos</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">Lista de comprobación de seguridad de la implementación</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>4. Configurar el espacio de nombres separado</p>

> [!NOTE]
> Este paso es opcional. Solamente es necesario si la organización está ejecutando un espacio de nombres separado.


</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">Configurar la lista de búsqueda de sufijos DNS para un espacio de nombres distintos</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. Seleccionar una libreta de direcciones sin conexión para todas las bases de datos de buzones de correo de Exchange 2010</p></td>
<td><p><a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Set mailbox database properties</a> en <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Administrar bases de datos de buzones en Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. Instalar Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar Exchange 2013 utilizando el asistente de configuración</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Instalar el rol de transporte perimetral de Exchange 2013 mediante el asistente de instalación</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Comprobar una instalación de Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Crear un buzón de correo de Exchange 2013</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Crear buzones de usuario</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Configurar directorios virtuales relacionados con Exchange</p>

> [!NOTE]
> Este paso es necesario si desea usar los servicios web de Exchange, Outlook en cualquier lugar o la libreta de direcciones sin conexión. También puede ser necesario si quiere cambiar cualquier configuración predeterminada para el Panel de control de Exchange, Microsoft Office&nbsp;Outlook Web App, o Exchange ActiveSync.<BR>


</td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuración del servidor de acceso de cliente de Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Agregar certificados digitales al servidor de acceso de cliente</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificados digitales y SSL</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. Mover un buzón de correo de arbitraje</p></td>
<td><p><a href="move-the-exchange-2010-system-mailbox-to-exchange-2013-exchange-2013-help.md">Mover el buzón del sistema de Exchange 2010 a Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurar la mensajería unificada</p>

> [!NOTE]
> Este paso es opcional. Solamente es necesario si desea usar la Mensajería unificada en la organización.


</td>
<td><p><a href="upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md">Actualizar la mensajería unificada (UM) de Exchange 2010 a la mensajería unificada de Exchange 2013</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. Configurar el servidor Transporte perimetral</p>

> [!NOTE]
> Este paso es opcional. Solo es necesario si su organización usa un servidor Transporte perimetral.


</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configure Internet mail flow through a subscribed Edge Transport server</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>13. Habilitar y configurar Outlook en cualquier lugar</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook en cualquier lugar</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. Configurar el punto de conexión de servicio</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuración del servidor de acceso de cliente de Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configurar registros DNS</p></td>
<td><p><a href="https://technet.microsoft.com/es-es/library/dn307232(v=exchg.150)">Configurar registros DNS para la instalación de varios servidores de Exchange 2010</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. Mover buzones de Exchange 2010 a Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimientos de buzones de Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. Mover los datos de la carpeta pública de Exchange 2013 a Exchange 2013</p></td>
<td><p><a href="public-folders-exchange-2013-help.md">Carpetas públicas</a></p>
<p><a href="https://technet.microsoft.com/es-es/library/jj150486(v=exchg.150)">Usar la migración en serie para migrar carpetas públicas a Exchange 2013 desde versiones anteriores</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>18. Tareas posteriores a la instalación</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Tareas posteriores a la instalación de Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

