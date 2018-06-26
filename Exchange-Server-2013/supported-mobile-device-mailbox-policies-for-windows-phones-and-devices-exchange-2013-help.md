---
title: 'Directivas de buzones de correo para dispositivos móviles compatibles con teléfonos y dispositivos de Windows: Exchange 2013 Help'
TOCTitle: Directivas de buzones de correo para dispositivos móviles compatibles con teléfonos y dispositivos de Windows
ms:assetid: d76b1d4c-d1f6-4501-a7c9-854327aceda5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ983805(v=EXCHG.150)
ms:contentKeyID: 52062066
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Directivas de buzones de correo para dispositivos móviles compatibles con teléfonos y dispositivos de Windows

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Con el lanzamiento de Windows Phone 8, Windows 8 y Windows RT hay varios dispositivos que son compatibles con Exchange ActiveSync y directivas de buzones de correo de dispositivos móviles. Cada sistema operativo del dispositivo es compatible con un conjunto específico de configuraciones de directivas de buzones de correo de dispositivos móviles.

## Matriz de compatibilidad del cliente de Windows y Exchange Server

En las siguientes tablas se indican los parámetros de directivas de buzones de correo de dispositivos móviles compatibles con las diferentes versiones de Windows Phone, Windows 8, Windows RT y Exchange Server.

## Parámetros de directivas compatibles con Windows Phone 7

En la siguiente tabla se indica la configuración de la directiva de buzón de dispositivos móviles de Windows Phone 7.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
<td><p>AllowIRDA</p></td>
</tr>
<tr class="even">
<td><p>MinPasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>PasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
<tr class="even">
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
<td><p>AllowDesktopSync</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
<td><p>AllowRemoteDesktop</p></td>
</tr>
<tr class="even">
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
<td><p>AllowStorageCard</p></td>
</tr>
<tr class="odd">
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
<td><p>AllowInternetSharing</p></td>
</tr>
<tr class="even">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
</tbody>
</table>


## Parámetros de directivas compatibles con Windows Phone 8

En la siguiente tabla se indica la configuración de la directiva de buzón de dispositivos móviles de Windows Phone 8.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
<td><p>AlphanumericDevicePasswordRequired</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="even">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="odd">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="odd">
<td><p>N/D</p></td>
<td><p>IRMEnabled</p></td>
<td><p>IRMEnabled</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>


## Parámetros de directivas compatibles con Windows 8 y Windows RT

En la siguiente tabla se indica la configuración de la directiva de buzón de dispositivos móviles de Windows 8 y Windows RT.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007</th>
<th>Exchange 2010</th>
<th>Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
<td><p>DevicePasswordEnabled</p></td>
</tr>
<tr class="even">
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
<td><p>AllowSimpleDevicePassword</p></td>
</tr>
<tr class="odd">
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
<td><p>MinDevicePasswordLength</p></td>
</tr>
<tr class="even">
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
<td><p>MinDevicePasswordComplexCharacters</p></td>
</tr>
<tr class="odd">
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
<td><p>RequireDeviceEncryption</p></td>
</tr>
<tr class="even">
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
<td><p>MaxInactivityTimeDeviceLock</p></td>
</tr>
<tr class="odd">
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
<td><p>DevicePasswordHistory</p></td>
</tr>
<tr class="even">
<td><p>DeviceWipeThreshold</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
<td><p>MaxDevicePasswordFailedAttempts</p></td>
</tr>
<tr class="odd">
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
<td><p>AllowNonProvisionableDevices</p></td>
</tr>
<tr class="even">
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
<td><p>DevicePasswordExpiration</p></td>
</tr>
</tbody>
</table>

