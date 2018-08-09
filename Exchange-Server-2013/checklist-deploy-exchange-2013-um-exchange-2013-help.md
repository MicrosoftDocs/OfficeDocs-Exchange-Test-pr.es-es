---
title: 'Lista de comprobación: Implementar UM de Exchange 2013: Exchange 2013 Help'
TOCTitle: 'Lista de comprobación: Implementar mensajería unificada de Exchange 2013'
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 52062022
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de comprobación: Implementar mensajería unificada de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-03-09_

Use la siguiente lista de comprobación para instalar e implementar la mensajería unificada en su organización.

Antes de empezar con la lista de comprobación, debe estar familiarizado con los conceptos que se explican en:

  - [Mensajería unificada](unified-messaging-exchange-2013-help.md)

  - [Nuevas características de correo de voz](new-voice-mail-features-exchange-2013-help.md)

  - [Diseño de mensajería unificada](planning-for-unified-messaging-exchange-2013-help.md)

Para obtener una guía paso a paso sobre cómo implementar la mensajería unificada y Microsoft Lync Server, vea [Lista de comprobación: Integrar mensajería unificada de Exchange 2013 con Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).

## Lista de comprobación para implementar la mensajería unificada


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
<td><p> </p></td>
<td><p>Verifique que cumple con los requisitos previos para la instalación.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
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
<td><p> </p></td>
<td><p>Si es necesario, instale los paquetes de idioma requeridos para la Mensajería unificada.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Instalar un paquete de idioma de mensajería unificada</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Cree el número necesario de planes de marcado para la organización.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">Crear un plan de marcado de mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure los parámetros de seguridad del plan de marcado.</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">Establecer la configuración de seguridad de VoIP</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Configure el modo de inicio de mensajería unificada en cada servidor de acceso de cliente y de buzones.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configurar el modo de inicio en un servidor de buzones</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurar el modo de inicio en un servidor de acceso de cliente</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure el número de llamadas simultáneas en los servidores de buzones de correo.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">Configurar el número de llamadas entrantes en un servidor de buzones</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configure los números y otros parámetros de Outlook Voice Access.</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Administrar un plan de marcado de mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure el marcado saliente para la Mensajería unificada.</p></td>
<td><p><a href="authorize-calls-using-dialing-rules-exchange-2013-help.md">Autorizar llamadas mediante reglas de marcado</a></p>
<p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Autorizar llamadas a los usuarios en un plan de marcado</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">¿Autorizar llamadas para un grupo de usuarios</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Cree el número necesario de operadores automáticos.</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">Crear un operador automático de mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Instale y configure cada uno de los operadores automáticos de la mensajería unificada.</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">Configuración de un operador automático de mensajería unificada</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Cree, importe y habilite un nuevo certificado de Exchange para la mensajería unificada, o bien habilite un certificado de terceros con confianza mutua. Además, importe el certificado en todas las puertas de enlace VoIP, IP-PBX y SBC.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Agregar servidores de acceso de cliente y buzón a un plan de marcado de URI de SIP</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Reinicie el servicio de Mensajería unificada de Microsoft Exchange y el servicio de enrutamiento de llamadas de mensajería unificada en todos los servidores de Exchange para que se carguen los certificados necesarios.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Interrumpir el servicio de mensajería unificada de Microsoft Exchange</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Iniciar el servicio de mensajería unificada de Microsoft Exchange</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Detenga el servicio Microsoft Exchange Unified Messaging llame al Router</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Iniciar el servicio Microsoft Exchange Unified Messaging llame al Router</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Cree una directiva de buzón de mensajería unificada o configure una directiva de buzón de mensajería unificada predeterminada.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Crear una directiva de buzón de mensajería unificada</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">Administrar una directiva de buzones de correo de mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Habilite a los usuarios para la mensajería unificada con un número de extensión y un número E.164, si corresponde.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">Habilitar a un usuario para el correo de voz</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Habilite el servicio de fax entrante (opcional).</p></td>
<td><p><a href="enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md">Permitir que los usuarios de correo de voz reciban faxes</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure el correo de voz protegido (opcional).</p></td>
<td><p><a href="protect-voice-mail-exchange-2013-help.md">Protección del correo de voz</a></p></td>
</tr>
</tbody>
</table>


Volver al principio

