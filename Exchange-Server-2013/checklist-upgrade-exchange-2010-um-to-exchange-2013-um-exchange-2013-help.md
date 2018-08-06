---
title: 'Lista comprobación Actualizar UM Exchange 2007 a UM de 2013 Exchange 2013 Help | Microsoft Docs'
TOCTitle: 'Lista de comprobación: Actualizar la mensajería unificada (UM) de Exchange 2010 a la mensajería unificada (UM) de Exchange 2013'
ms:assetid: 799bd1b1-a918-4bd8-911e-e6ca08bd7b52
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn169228(v=EXCHG.150)
ms:contentKeyID: 54652443
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de comprobación: Actualizar la mensajería unificada (UM) de Exchange 2010 a la mensajería unificada (UM) de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Use esta lista de comprobación para actualizar mensajería unificada (UM) de Exchange 2010 a mensajería unificada (UM) de Exchange 2013. Asegúrese de consultar esta información cuando actualiza su organización de Exchange 2010 y su implementación de mensajería unificada (UM) a Exchange 2013. Para obtener instrucciones paso a paso para la actualización a mensajería unificada (UM) de Exchange 2013, vea [Actualizar la mensajería unificada (UM) de Exchange 2010 a la mensajería unificada de Exchange 2013](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md).

Antes de empezar con la lista de comprobación, debe estar familiarizado con los conceptos que se explican en:

  - [Diseño de mensajería unificada](planning-for-unified-messaging-exchange-2013-help.md)

  - [Integración del sistema telefónico con mensajería unificada](telephone-system-integration-with-um-exchange-2013-help.md)

  - [Conecte su sistema de correo de voz a la red de teléfono](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md)

Para obtener indicaciones paso a paso sobre cómo actualizar de la mensajería unificada (UM) de Exchange 2007 a la mensajería unificada (UM) de Exchange 2013, vea [Actualizar la mensajería UNIFICADA de Exchange 2007 para la mensajería UNIFICADA de Exchange de 2013](upgrade-exchange-2007-um-to-exchange-2013-um-exchange-2013-help.md).

## Lista de comprobación para actualización de mensajería unificada (UM) de Exchange 2010 a mensajería unificada (UM) de Exchange 2013


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
<th>Tema</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Implemente y configure los componentes de telefonía.</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">Conectar la mensajería unificada para su sistema telefónico</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Revise los requisitos del sistema antes de instalar Exchange 2013.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos del sistema para Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verifique que cumple con los requisitos previos para la instalación.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Instale los servidores de acceso de cliente y de buzones requeridos.</p>

> [!WARNING]
> Debe implementar al menos un servidor de buzones de correo de Exchange 2013 en su organización antes de configurar las puertas de enlace VoIP o las centrales de conmutación (PBX) de IP para enviar protocolos de inicio de sesión (SIP) de UM y tráfico RTP a los servidores de acceso de cliente de Exchange 2013.


</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar Exchange 2013 utilizando el asistente de configuración</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verifique la instalación y compruebe los registros de configuración del servidor.</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Comprobar una instalación de Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Si es necesario, instale los paquetes de idioma requeridos para la Mensajería unificada.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Instalar un paquete de idioma de mensajería unificada</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Mover a Exchange 2013 el buzón del sistema de Exchange 2010 utilizado para mensajes personalizados de mensajería unificada (UM).</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimientos de buzones de Exchange 2013</a></p>

> [!NOTE]
> Si ya se ha movido el buzón del sistema, puede importar o exportar manualmente los mensajes personalizados desde Exchange 2010 usando <A href="import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md">Importar y exportar saludos personalizados, anuncios, menús y avisos</A>.


</td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exportar e importar certificados.</p></td>
<td><p><a href="deploying-certificates-for-um-exchange-2013-help.md">Implementación de certificados para mensajería unificada</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurar el modo de inicio de mensajería unificada en todos los servidores de acceso de cliente de Exchange 2013.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurar el modo de inicio en un servidor de acceso de cliente</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurar el modo de inicio de mensajería unificada en todos los servidores de buzones de correo de Exchange 2013.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configurar el modo de inicio en un servidor de buzones</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Crear o configurar planes de marcado de mensajería unificada existentes.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">Crear un plan de marcado de mensajería unificada</a></p>
<p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Administrar un plan de marcado de mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Crear o configurar puertas de enlace IP existentes de mensajería unificada.</p></td>
<td><p><a href="create-a-um-ip-gateway-exchange-2013-help.md">Cree una puerta de enlace IP de mensajería unificada</a></p>
<p><a href="manage-a-um-ip-gateway-exchange-2013-help.md">Administrar una puerta de enlace IP de mensajería unificada</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Crear un grupo de extensiones de mensajería unificada.</p></td>
<td><p><a href="create-a-um-hunt-group-exchange-2013-help.md">Crear un grupo de extensiones de mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Crear o configurar operadores automáticos de mensajería unificada.</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">Crear un operador automático de mensajería unificada</a></p>
<p><a href="manage-a-um-auto-attendant-exchange-2013-help.md">Administrar a un operador automático de mensajería unificada</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Crear o configurar directivas de buzón de mensajería unificada.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Crear una directiva de buzón de mensajería unificada</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">Administrar una directiva de buzones de correo de mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Mover buzones de correo existentes habilitados para mensajería unificada a Exchange 2013.</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimientos de buzones de Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Habilitar nuevos usuarios para mensajería unificada o configurar las opciones para un usuario existente habilitado para mensajería unificada.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">Habilitar a un usuario para el correo de voz</a></p>
<p><a href="manage-voice-mail-settings-for-a-user-exchange-2013-help.md">Administrar la configuración de correo de voz para un usuario</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurar las puertas de enlace VoIP, IP-PBX y PBX habilitadas para SIP para enviar todas las llamadas entrantes a los servidores de acceso de cliente de Exchange 2013.</p></td>
<td><p><a href="configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md">Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles</a> <a href="connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md">Conectar una puerta de enlace VoIP, IP PBX o un controlador de borde de sesión a mensajería unificada</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Deshabilitar el contestador automático en los servidores de mensajería unificada de Exchange 2010.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296335">Deshabilitar mensajería unificada en Exchange 2010</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Eliminar un servidor de mensajería unificada de Exchange 2010 de un plan de marcado.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296336">Quitar un servidor de mensajería UNIFICADA de un Plan de marcado</a></p></td>
</tr>
</tbody>
</table>

