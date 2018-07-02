---
title: 'Características de teléfonos móviles y tabletas: Exchange 2013 Help'
TOCTitle: Características de teléfonos móviles y tabletas
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50556855
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Características de teléfonos móviles y tabletas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Los usuarios pueden acceder a su correo electrónico, calendario, contactos e informaciones de tareas en teléfonos móviles, tabletas y otros dispositivos portátiles a través de Microsoft Exchange ActiveSync. También pueden usarlo para configurar su firma y las respuestas automáticas. Una amplia variedad de teléfonos móviles y dispositivos funcionan con Exchange ActiveSync.


> [!NOTE]
> Si bien denominamos teléfonos móviles a los dispositivos que tienen acceso a Exchange Server 2013, existen numerosos dispositivos que pueden tener acceso a Exchange&nbsp;2013, pero que no poseen la funcionalidad de los teléfonos móviles. En esta documentación, el término "teléfono móvil" también hace referencia a esos dispositivos.



## Dispositivos compatibles con Exchange ActiveSync

Los usuarios pueden beneficiarse de las útiles características que ofrece Exchange ActiveSync seleccionando teléfonos móviles compatibles con Exchange ActiveSync. Estos teléfonos móviles están disponibles de muchos fabricantes y en muchos operadores. Para obtener más información, vea la documentación específica del teléfono móvil.

Algunos de los teléfonos móviles compatibles con Microsoft Exchange son:

  - **Apple** Apple iPhone, iPod Touch e iPad todos admiten Exchange ActiveSync.

  - **Windows Phone**   Windows Phone 8, Windows Phone 7 y las versiones anteriores son compatibles con Exchange ActiveSync.

  - **Android** Muchos teléfonos móviles y tabletas con el sistema operativo Android admiten Exchange ActiveSync. Sin embargo, estos dispositivos móviles puede que no sean compatibles con todas las directivas de buzones de correo del dispositivo móvil. Para obtener más información, vea [Directivas de buzón de dispositivo móvil](mobile-device-mailbox-policies-exchange-2013-help.md).

## Características del software Windows Phone

Los teléfonos móviles que tienen una versión del software Windows Phone como sistema operativo ofrecen una mayor funcionalidad al sincronizar con Exchange 2013. La siguiente tabla indica las directivas de buzones de correo de dispositivos disponibles con Windows Phone 8 y Windows Phone 7.

### Características de Windows Phone 7 y 8

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Sistema operativo</th>
<th>Características</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Phone 8</p></td>
<td><p>Windows Phone 8 es compatible con las siguientes directivas de buzón de correo de dispositivo móvil:</p>
<ul>
<li><p>Permitir una contraseña sencilla de dispositivo</p></li>
<li><p>Se requiere contraseña alfanumérica</p></li>
<li><p>Contraseña del dispositivo habilitada</p></li>
<li><p>Expiración de la contraseña del dispositivo</p></li>
<li><p>IRM habilitado</p></li>
<li><p>Número máximo de intentos de contraseña del dispositivo erróneos</p></li>
<li><p>Bloqueo del tiempo de inactividad del dispositivo máximo</p></li>
<li><p>Mínimo de caracteres complejos de contraseña de dispositivo</p></li>
<li><p>Longitud mínima de la contraseña del dispositivo</p></li>
<li><p>Requerimiento de cifrado del dispositivo</p></li>
<li><p>Eliminación remota de datos</p></li>
</ul>

> [!WARNING]
> Si la organización usa otras configuraciones de directivas de buzón de correo de dispositivos móviles, deberá establecer la directiva <STRONG>Permitir dispositivos no aprovisionables</STRONG> a verdadero. Esto puede tener implicaciones de seguridad para su organización, ya que se permitirá la sincronización de otros teléfonos móviles y dispositivos que no cumplen con los requisitos de la configuración de la directiva de dispositivos móviles. Para obtener más información, vea <A href="mobile-device-mailbox-policies-exchange-2013-help.md">Directivas de buzón de dispositivo móvil</A>.


</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Los teléfonos móviles de Windows Phone 7 solamente admiten un subconjunto de parámetros de directivas de buzones de Exchange ActiveSync:</p>
<ul>
<li><p>Se necesita contraseña</p></li>
<li><p>Longitud mínima de la contraseña</p></li>
<li><p>Bloqueo del tiempo de inactividad máximo</p></li>
<li><p>Número máximo de intentos de contraseña del dispositivo erróneos</p></li>
<li><p>Permitir contraseña sencilla</p></li>
<li><p>Expiración de contraseña</p></li>
<li><p>Historial de contraseñas</p></li>
<li><p>Deshabilitar almacenamiento extraíble</p></li>
<li><p>Deshabilitar IrDA</p></li>
<li><p>Deshabilitar la sincronización del escritorio</p></li>
<li><p>Bloquear el escritorio remoto</p></li>
<li><p>Bloquear uso compartido de Internet</p></li>
</ul></td>
</tr>
</tbody>
</table>

