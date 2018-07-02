---
title: 'Lista de comprobación: instalación nueva de Exchange 2013: Exchange 2013 Help'
TOCTitle: 'Lista de comprobación: instalación nueva de Exchange 2013'
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 49116630
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Lista de comprobación: instalación nueva de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Use esta lista de comprobación para implementar Microsoft Exchange Server 2013. Antes de empezar con la lista de comprobación, debe estar familiarizado con los conceptos que se explican en:

  - [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Lista de comprobación de seguridad de la implementación](deployment-security-checklist-exchange-2013-help.md)

Esta lista de comprobación es genérica en el sentido de proporcionar instrucciones para un escenario típico.


> [!NOTE]
> El Asistente de implementación de Exchange Server proporciona indicaciones personalizadas paso a paso acerca de cómo implementar Exchange Server. El Asistente de implementación le puede ayudar a implementar una nueva instalación de Exchange Server 2013, actualizar una versión anterior a Exchange 2013 o configurar una implementación híbrida de Exchange 2013 y Exchange Online. Para obtener más información, consulte <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Asistente para la implementación de Exchange Server</A>.



## Lista de comprobación para una instalación nueva de Exchange 2013


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
<td><p>Tema</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Leer las notas de la versión.</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de la versión de Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. Comprobar los requisitos del sistema.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos del sistema para Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. Confirmar la realización de los pasos de requisitos previos.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. Configurar el espacio de nombres separado.</p>

> [!NOTE]
> Este paso es opcional. Solamente es necesario si la organización ejecuta un espacio de nombres separado.


</td>
<td><p><a href="disjoint-namespace-scenarios-exchange-2013-help.md">Escenarios de espacios de nombres distintos</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>5. Instalar el rol de servidor Buzón de correo.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar Exchange 2013 utilizando el asistente de configuración</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>6. Instalar el rol de servidor Acceso de clientes.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar Exchange 2013 utilizando el asistente de configuración</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Instalar el rol del servidor Transporte perimetral.</p>

> [!NOTE]
> Este paso es opcional. Solo es necesario si quiere instalar un servidor de transporte perimetral. Para más información, vea <A href="edge-transport-servers-exchange-2013-help.md">Servidores de transporte perimetral</A>.


</td>
<td><p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Instalar el rol de transporte perimetral de Exchange 2013 mediante el asistente de instalación</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Crear un archivo de suscripción EdgeSync.</p>
<p>Este paso es opcional. Solo es necesario si ha instalado un servidor de transporte perimetral y quiere configurar una suscripción EdgeSync entre dicho servidor y un servidor de transporte de concentradores. Para más información, vea <a href="edge-subscriptions-exchange-2013-help.md">Suscripciones perimetrales</a>.</p></td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configure Internet mail flow through a subscribed Edge Transport server</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Configurar el transporte.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 1: Create a Send connector</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. Agregar dominios aceptados adicionales.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 2: Add additional accepted domains</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurar directivas de direcciones de correo electrónico.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 3: Configure the default email address policy</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>12. Configurar valores en directorios virtuales, como la libreta de direcciones sin conexión, los servicios Web Exchange, el Centro de administración de Exchange (EAC), Outlook Web App y los directorios virtuales de Exchange ActiveSync.</p>

> [!NOTE]
> Este paso es necesario si va a usar los servicios web de Exchange, Outlook en cualquier lugar o la libreta de direcciones sin conexión. También puede ser necesario para cambiar cualquiera de los valores predeterminados del EAC, Outlook Web App o Exchange ActiveSync.


</td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 4: Configure external URLs</a></p>
<p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 5: Configure internal URLs</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. Agregar certificados digitales al servidor de acceso de cliente.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 6: Configure an SSL certificate</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>14. Configurar la mensajería unificada.</p>

> [!NOTE]
> Este paso es opcional. Solamente es necesario si desea usar la mensajería unificada en la organización.


</td>
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Implementación del correo de voz y mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Establecer configuraciones adicionales de mensajería unificada y Lync Server.</p>

> [!NOTE]
> Este paso es opcional. Solo es necesario si ha configurado la mensajería unificada en su organización y desea integrarla con Lync Server.


</td>
<td><p><a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>16. Tareas posteriores a la instalación.</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Tareas posteriores a la instalación de Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

