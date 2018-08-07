---
title: 'Lista comprobar Integrar UM Exchange 2013 con Lync Server Exchange 2013 Help'
TOCTitle: 'Lista de comprobación: Integrar mensajería unificada de Exchange 2013 con Lync Server'
ms:assetid: 3b82e86f-9f30-4445-96ad-744082abeaeb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638120(v=EXCHG.150)
ms:contentKeyID: 52062018
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Lista de comprobación: Integrar mensajería unificada de Exchange 2013 con Lync Server

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Utilice esta lista de verificación para instalar e implementar la mensajería unificada y Microsoft Lync Server 2013. En este tema, "Lync Server" también se refiere a Lync Server 2010. No obstante, también se puede implementar Microsoft Office Communications Server 2007 R2 junto con la mensajería unificada.

> [!NOTE]  


Antes de empezar con la lista de comprobación, debe estar familiarizado con los conceptos que se explican en:

  - [Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Coexistencia con Office Communications Server 2007 R2 y Lync Server](coexistence-with-office-communications-server-2007-r2-and-lync-server-exchange-2013-help.md)

Para obtener más información sobre cómo realizar las tareas que deben completarse para Lync Server, consulte [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=265752).

## Lista de verificación para implementar Microsoft Lync Server y la mensajería unificada


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
<td><p>Revise los requisitos del sistema antes de instalar Exchange Server 2013.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos del sistema para Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Verifique que cumple con los requisitos previos para la instalación.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Compruebe los requisitos previos para integrar Microsoft Lync Server 2013 y Microsoft Exchange Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282082">Requisitos previos para integrar Microsoft Lync Server 2013 y Microsoft Exchange Server 2013</a></p>

> [!TIP]
> Se requiere la API administrada de comunicaciones unificadas (UCMA) 4.0 Runtime para Exchange 2013 y Lync Server 2010 y 2013, y se instala durante la instalación. Para descargar y revisar la información sobre UCMA 4.0, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=258269">API administrada de comunicaciones unificadas 4.0 Runtime</A>


</td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Instale los servidores de acceso de cliente y de buzones requeridos.</p></td>
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
<td><p>Cree el número de planes de marcado URI de SIP necesarios para la organización.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">Crear un plan de marcado de mensajería unificada</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure los parámetros de seguridad del plan de marcado.</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">Establecer la configuración de seguridad de VoIP</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configure el número de llamadas simultáneas en los servidores de buzones de correo.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">Configurar el número de llamadas entrantes en un servidor de buzones</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure los números y otros parámetros de Outlook Voice Access.</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Administrar un plan de marcado de mensajería unificada</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Añada todos los servidores de acceso de cliente y de buzones de correo para cada plan de marcado URI de SIP.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Agregar servidores de acceso de cliente y buzón a un plan de marcado de URI de SIP</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure el marcado saliente para la mensajería unificada. Permita todas las llamadas en los planes de marcado URI de SIP y directivas de buzones de mensajería unificada que estén vinculados a dichos planes de marcado.</p></td>
<td><p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Autorizar llamadas a los usuarios en un plan de marcado</a></p>
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
<td><p> </p></td>
<td><p>Cree, importe y habilite un nuevo certificado de Exchange para la mensajería unificada, o bien habilite un certificado de terceros con confianza mutua.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Agregar servidores de acceso de cliente y buzón a un plan de marcado de URI de SIP</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Configure el modo de inicio de la mensajería unificada en Dual o TLS para cada servidor de acceso de cliente y de buzones.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configurar el modo de inicio en un servidor de buzones</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurar el modo de inicio en un servidor de acceso de cliente</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Reinicie el servicio de Mensajería unificada de Microsoft Exchange y el servicio de enrutamiento de llamadas de mensajería unificada en todos los servidores de Exchange para que se carguen los certificados necesarios.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Interrumpir el servicio de mensajería unificada de Microsoft Exchange</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Iniciar el servicio de mensajería unificada de Microsoft Exchange</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Detenga el servicio Microsoft Exchange Unified Messaging llame al Router</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Iniciar el servicio Microsoft Exchange Unified Messaging llame al Router</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Cree una directiva de buzón de mensajería unificada o configure una directiva de buzón de mensajería unificada predeterminada.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Crear una directiva de buzón de mensajería unificada</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">Administrar una directiva de buzones de correo de mensajería unificada</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Habilite la mensajería unificada para los usuarios con dirección SIP y vincúlelos a un plan de marcado URI de SIP.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">Habilitar a un usuario para el correo de voz</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Consulte la documentación de planeación de Lync Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282081">Planeación</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Instale e implemente Lync Server 2013.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282051">Implementar Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Importe el certificado de terceros o PKI interno de confianza mutua que se importará en los servidores de mensajería unificada de Exchange.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281863">Configurar certificados para servidores</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281865">Configurar certificados en el servidor que ejecuta la mensajería unificada de Microsoft Exchange Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Si es necesario, inicie los servicios de Lync en los servidores para que se carguen los certificados.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282084">Iniciar servicios en servidores</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Abra el Shell de administración de Exchange y ejecute el script exchucutil.ps1 ubicado en la carpeta %Archivos de programa%\Microsoft\Exchange Server\V15\Scripts.</p>
<p></p></td>
<td><p><a href="configure-um-to-work-with-lync-server-exchange-2013-help.md">Configurar la mensajería unificada para que funcione con Lync Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Consulte los requisitos para Telefonía IP empresarial.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281876">Requisitos previos de software para Telefonía IP empresarial</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281875">Requisitos previos de seguridad y configuración para Telefonía IP empresarial</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Implemente y configure puertas de enlace de medios o servidores de mediación y defina a los interlocutores.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281872">Implementar servidores de mediación y definir servidores del mismo nivel</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configure un tronco entre un servidor de mediación y uno o más interlocutores para proporcionar conectividad de red telefónica pública conmutada (PSTN).</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281868">Configuración de troncos</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Cree y configure un plan de marcado de Lync. Seguidamente, cree, defina y asocie reglas de normalización.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281867">Configurar planes de marcado</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configure directivas de voz y defina el uso del teléfono y las rutas de llamadas salientes.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281869">Configurar directivas de voz, registros de uso de RTC y rutas de voz</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Ejecute la utilidad de integración de Exchange (ocsumutil.exe), lo que crea objetos de contacto para Outlook Voice Access y para los operadores automáticos.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281866">Configurar Lync Server 2013 para que funcione con la mensajería unificada en Microsoft Exchange Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Defina, implemente y configure todas las características avanzadas de Telefonía IP empresarial que sean necesarias.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281871">Implementar características avanzadas de Telefonía IP empresarial</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Habilite a los usuarios para Telefonía IP empresarial. Escriba un URI de línea y asigne una directiva de voz y un plan de marcado de Lync.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281873">Habilitar a los usuarios para la telefonía IP empresarial</a></p></td>
</tr>
</tbody>
</table>

