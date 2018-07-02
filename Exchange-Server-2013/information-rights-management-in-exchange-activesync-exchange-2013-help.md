---
title: 'Information Rights Management en Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Information Rights Management en Exchange ActiveSync
ms:assetid: ebf04460-4d61-4b00-86b9-85ec1dbbd6a1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff657743(v=EXCHG.150)
ms:contentKeyID: 49895995
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Information Rights Management en Exchange ActiveSync

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Con frecuencia, los trabajadores de información usan el correo electrónico para intercambiar información confidencial. Para garantizar la seguridad de esta información, una organización puede usar Information Rights Management (IRM) para aplicar protección persistente al contenido de los mensajes. Debido a que los dispositivos móviles se usan cada vez más para obtener acceso al correo electrónico, es importante que los usuarios de dispositivos móviles puedan crear y consumir contenido protegido por IRM.

**Contenido**

Protección IRM móvil en Exchange 2013

Requisitos

Seguridad

Habilitación de IRM en Exchange ActiveSync

¿Está buscando tareas de administración relacionadas con IRM? Consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Protección IRM móvil en Exchange 2013

En Exchange 2013, IRM en Microsoft Exchange ActiveSync permite que los usuarios accedan a una amplia funcionalidad de IRM en cualquier dispositivo compatible con Exchange ActiveSync, sin que sea necesario configurar permisos AD RMS ni conectar el dispositivo a un equipo y activarlo para IRM. Tampoco es necesario que el dispositivo móvil ejecute Windows. Exchange ActiveSync tiene licencia de Microsoft para fabricantes de dispositivos móviles, fabricantes de equipos originales (OEM) y otros. Para ver una lista de las licencias de Exchange ActiveSync actuales, expanda la sección "Protocolo de Exchange ActiveSync" en la página de [Licencias de tecnología de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=198562).

Mediante el uso de IRM en Exchange ActiveSync, los usuarios de dispositivos móviles pueden:

  - Crear mensajes protegidos por IRM.

  - Leer mensajes protegidos por IRM.

  - Responder y reenviar mensajes protegidos por IRM.

Protección IRM móvil en Exchange 2013

## Requisitos

Se aplican los siguientes requisitos:

  - Los servidores de acceso de cliente de la organización deben ejecutar Exchange 2010 SP1 o posterior.

  - La organización debe implementar un servidor AD RMS.

  - Se debe habilitar IRM para los mensajes internos. Es un requisito previo para todas las características de IRM en Exchange 2010. Para obtener detalles, consulte [Habilitar o deshabilitar IRM para mensajes internos](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - IRM debe estar habilitado en la directiva de buzón de Exchange ActiveSync. Puede habilitar o deshabilitar IRM para diferentes grupos de usuarios mediante diferentes directivas de buzón de Exchange ActiveSync.

  - Los dispositivos compatibles con el protocolo de Exchange ActiveSync versión 14.1, incluidos los teléfonos con Windows, pueden admitir IRM en Exchange ActiveSync. La aplicación de correo electrónico móvil en un dispositivo debe ser compatible con la etiqueta RightsManagementInformation definida en el protocolo Exchange ActiveSync versión 14.1.

Protección IRM móvil en Exchange 2013

## Seguridad

Al habilitar IRM en Exchange ActiveSync, el servidor de Acceso de cliente descifra mensajes protegidos por IRM antes de ofrecer acceso al dispositivo móvil compatible. Al realizarse la sincronización, los mensajes protegidos por IRM residen en el dispositivo móvil en formato sin cifrar. La aplicación de cliente de correo electrónico compatibles con IRM aplican la protección con IRM en el dispositivo móvil.

IRM de Exchange ActiveSync no descifra los adjuntos protegidos por IRM en el servidor de Acceso de cliente. La aplicación usada para crear o ver el archivo permite el acceso a los archivos protegidos por IRM. Por ejemplo, en un teléfono Windows, la protección IRM para archivos de Microsoft Office es proporcionada por [Microsoft Office Mobile](https://go.microsoft.com/fwlink/p/?linkid=205121). Para obtener acceso a archivos de Office protegidos por IRM, los usuarios deben conectar el dispositivo a un equipo y activar Office Mobile con el servidor RMS.

Al habilitar IRM en Exchange ActiveSync, se recomienda usar la configuración de la directiva de Exchange ActiveSync que se muestra en la siguiente tabla como ayuda para proteger los dispositivos móviles.

### Configuración de directiva de Exchange ActiveSync

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Configuración con el Asistente para Nueva directiva de buzón de Exchange ActiveSync</th>
<th>Configuración con el cmdlet New-ActiveSyncMailboxPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Seleccione a los usuarios que escriban una contraseña para obtener acceso a la información del dispositivo móvil.</p></td>
<td><p>Active la casilla <strong>Solicitar contraseña</strong>.</p></td>
<td><p>Establezca el parámetro <em>DevicePasswordEnabled</em> en <code>$true</code>.</p></td>
</tr>
<tr class="even">
<td><p>Habilite la codificación en el dispositivo móvil.</p></td>
<td><p>Active la casilla <strong>Requerir contraseña</strong> y, luego, la casilla <strong>Requerir cifrado del dispositivo</strong>.</p></td>
<td><p>Establezca el parámetro <em>RequireDeviceEncryption</em> en <code>$true</code>.</p>

> [!IMPORTANT]
> Cuando establece el parámetro <EM>RequireDeviceEncryption</EM> en <CODE>$true</CODE>, los dispositivos móviles que no admiten el cifrado de dispositivos no podrán conectarse.


</td>
</tr>
<tr class="odd">
<td><p>No permita que los dispositivos móviles no aprovisionables se sincronicen con el servidor Exchange.</p></td>
<td><p>Desactive la casilla <strong>Permitir dispositivos no aprovisionables</strong>.</p></td>
<td><p>Establezca el parámetro <em>AllowNonProvisionableDevices</em> en <code>$false</code>.</p></td>
</tr>
</tbody>
</table>


Para obtener más información, consulte [Directivas de buzón de dispositivo móvil](mobile-device-mailbox-policies-exchange-2013-help.md).

Protección IRM móvil en Exchange 2013

## Habilitación de IRM en Exchange ActiveSync

Para habilitar IRM en Exchange ActiveSync, realice las siguientes tareas:

1.  Agregue el buzón de correo de federación (un buzón de correo del sistema creado por la configuración de Exchange 2013 y Exchange 2010) al grupo de superusuarios en AD RMS. Esto permite que los servidores Exchange 2013 y Exchange 2010 tengan acceso a mensajes protegidos por IRM. Para obtener detalles, consulte [Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

2.  Use el cmdelt [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)) en el Shell de administración de Exchange para habilitar IRM en el servidor Acceso de cliente. Esto habilita IRM en Exchange ActiveSync e IRM en Microsoft OfficeOutlook Web App para su organización. Para obtener detalles, consulte [Habilitar o deshabilitar el servicio Information Rights Management en los servidores de acceso de cliente](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md).

Protección IRM móvil en Exchange 2013

