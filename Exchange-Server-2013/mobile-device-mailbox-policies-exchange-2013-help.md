---
title: 'Directivas de buzón de dispositivo móvil: Exchange 2013 Help'
TOCTitle: Directivas de buzón de dispositivo móvil
ms:assetid: 9317b3bc-44a1-4e54-bc51-4f0b194b6a55
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123783(v=EXCHG.150)
ms:contentKeyID: 49895786
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Directivas de buzón de dispositivo móvil

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-06-16_

En MicrosoftExchange Server 2013, puede crear directivas de buzones de dispositivos móviles para aplicar un conjunto común de directivas o configuraciones de seguridad a un grupo de usuarios. Una vez que implemente Exchange ActiveSync en su organización de Exchange 2013, puede crear nuevas directivas de buzones de dispositivos móviles o modificar las directivas existentes. Al instalar Exchange 2013, se crea una directiva predeterminada de buzones de dispositivos móviles. A todos los usuarios se les asigna automáticamente esta directiva predeterminada de buzones de dispositivos móviles.


> [!IMPORTANT]
> Los teléfonos móviles de Windows Phone 7 solamente admiten un subconjunto de ajustes de directiva de buzón de Exchange ActiveSync. Para obtener una lista completa, vea Sincronización de Windows Phone 7.




> [!WARNING]
> El lector de huellas digitales iOS7 no se admite como contraseña de dispositivo. Si habilita el lector de huellas digitales para proteger su dispositivo iOS7, tendrá que crear y escribir una contraseña si las directivas de buzón de dispositivo móvil requieren una contraseña.



## Resumen de las directivas de buzones de dispositivos móviles

Puede usar las directivas de buzones de dispositivos móviles para administrar diferentes parámetros de configuración. Por ejemplo, los siguientes:

  - Solicitar una contraseña

  - Especificar la longitud mínima de la contraseña

  - Solicitar un número o un carácter especial en la contraseña

  - Designar el tiempo que puede permanecer inactivo un dispositivo antes de solicitar al usuario que vuelva a escribir la contraseña

  - Borrar un dispositivo tras un número específico de intentos de contraseña erróneos

Para obtener más información acerca de todos los parámetros que puede configurar, vea la configuración de directivas de dispositivos móviles.

## Administrar las directivas de buzones de correo de Exchange ActiveSync

Las directivas de buzones de dispositivos móviles se pueden cercar en el Centro de administración de Exchange (EAC) o en el Shell de administración de Exchange. Si crea una directiva en el EAC, solamente puede configurar un subconjunto de configuraciones disponibles. Puede configurar el resto de configuraciones mediante el Shell.

## Sincronización de Windows Phone 7

Si tiene teléfonos móviles de Windows Phone 7 en su organización, estos teléfonos experimentarán problemas de sincronización si algunas propiedades de la directiva de buzón de Exchange ActiveSync están configuradas. Para permitir que los teléfonos móviles de Windows Phone 7 se sincronicen con un buzón de Exchange, configure la propiedad **AllowNonProvisionableDevices** en True o solamente configure las siguientes propiedades de directiva del buzón Exchange ActiveSync:

  - AllowSimplePassword

  - BlockInternetSharing

  - BlockRemoteDesktop

  - DisableDesktopSync

  - DisableIrDA

  - DisableRemovableStorage

  - DeviceWipeThreshold

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - PasswordExpiration

  - PasswordHistory

  - PasswordRequired

## Configuración de directivas de buzón de dispositivo móvil

La siguiente tabla resume la configuración que puede especificar mediante las directivas de buzones de dispositivos móviles.

### Configuración de directivas de buzón de dispositivo móvil

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Permitir Bluetooth</p></td>
<td><p>Esta configuración especifica si el dispositivo móvil admite conexiones Bluetooth. Las opciones disponibles son Deshabilitado, Solo manos libres y Permitir. El valor predeterminado es Admitir. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="even">
<td><p>Permitir explorador</p></td>
<td><p>Esta configuración especifica si se permite Pocket Internet Explorer en el dispositivo móvil. Esta configuración no afecta a exploradores de terceros que estén instalados en el dispositivo móvil. El valor predeterminado es <code>$true</code>. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir cámara</p></td>
<td><p>Esta configuración especifica si se puede usar la cámara del dispositivo móvil. El valor predeterminado es <code>$true</code>. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="even">
<td><p>Permitir correo electrónico del consumidor</p></td>
<td><p>Esta configuración especifica si el usuario del dispositivo móvil puede configurar una cuenta de correo personal (POP3 o IMAP4) en el dispositivo móvil. El valor predeterminado es <code>$true</code>. Esta configuración no controla el acceso a las cuentas de correo que usan programas de correo de terceros para dispositivos móviles. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir Desktop Sync</p></td>
<td><p>Esta configuración especifica si el dispositivo móvil se puede sincronizar con un equipo por cable, Bluetooth o conexión IrDA. El valor predeterminado es <code>$true</code>. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="even">
<td><p>Permitir la administración de dispositivos externos</p></td>
<td><p>Esta configuración permite especificar si un programa de administración de dispositivo externo tiene permiso para administrar el dispositivo.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir correo electrónico HTML</p></td>
<td><p>Esta configuración especifica si el correo electrónico sincronizado con el dispositivo móvil puede tener formato HTML. Si la configuración está establecida en <code>$false</code>, todo el correo electrónico se convertirá en texto sin formato.</p></td>
</tr>
<tr class="even">
<td><p>Permitir el uso compartido de Internet</p></td>
<td><p>Esta configuración especifica si el dispositivo móvil se puede usar como módem de un equipo de escritorio o portátil. El valor predeterminado es <code>$true</code>. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="odd">
<td><p>AllowIrDA</p></td>
<td><p>Esta configuración especifica si se permiten las conexiones infrarrojas a y desde el dispositivo móvil. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="even">
<td><p>Permitir la actualización de OTA para móviles</p></td>
<td><p>Esta configuración especifica si la configuración de la directiva de buzones de dispositivos móviles se puede enviar al dispositivo a través de una conexión de datos celular. El valor predeterminado es <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir dispositivos no aprovisionables</p></td>
<td><p>Esta configuración especifica si se permite que los dispositivos móviles que no admitan la aplicación de todas las configuraciones de directivas se conecten a Exchange 2013 mediante Exchange ActiveSync. Permitir dispositivos móviles no aprovisionables puede tener implicaciones de seguridad. Por ejemplo, es posible que algunos de los dispositivos no aprovisionables no puedan implementar los requisitos de contraseña de una organización.</p></td>
</tr>
<tr class="even">
<td><p>Permitir POPIMAPEmail</p></td>
<td><p>Esta configuración especifica si el usuario puede configurar una cuenta de correo POP3 o IMAP4 en el dispositivo móvil. El valor predeterminado es <code>$true</code>. Esta configuración no controla el acceso de los programas de correo de terceros.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir escritorio remoto</p></td>
<td><p>Esta configuración especifica si el dispositivo móvil puede iniciar una conexión de escritorio remoto. El valor predeterminado es <code>$true</code>. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="even">
<td><p>Permitir contraseña sencilla</p></td>
<td><p>Esta configuración habilita o deshabilita la habilidad de usar una contraseña sencilla como 1111 o 1234. El valor predeterminado es <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir la negociación del algoritmo de cifrado S/MIME</p></td>
<td><p>Esta configuración especifica si la aplicación de mensajería del dispositivo móvil puede negociar el algoritmo de cifrado en caso de que el certificado de un destinatario no admita el algoritmo de cifrado especificado.</p></td>
</tr>
<tr class="even">
<td><p>Permitir certificados de software S/MIME</p></td>
<td><p>Esta configuración especifica si se permiten los certificados de software S/MIME en dispositivos móviles.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir tarjeta de almacenamiento</p></td>
<td><p>Esta configuración especifica si el dispositivo móvil puede tener acceso a la información que está almacenada en una tarjeta de almacenamiento. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="even">
<td><p>Permitir mensajería de texto</p></td>
<td><p>Esta configuración especifica si la mensajería de texto se permite desde el dispositivo móvil. El valor predeterminado es <code>$true</code>. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir aplicaciones sin firmar</p></td>
<td><p>Esta configuración especifica si las aplicaciones sin firmar se pueden instalar en el dispositivo móvil. El valor predeterminado es <code>$true</code>. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="even">
<td><p>Permitir la instalación de paquetes sin firmar</p></td>
<td><p>Esta configuración especifica si los paquetes de instalación sin firmar se pueden ejecutar en el dispositivo móvil. El valor predeterminado es <code>$true</code>. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="odd">
<td><p>Permitir Wi-Fi</p></td>
<td><p>Esta configuración especifica si el acceso inalámbrico a Internet se permite en el dispositivo móvil. El valor predeterminado es <code>$true</code>. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="even">
<td><p>Se requiere contraseña alfanumérica</p></td>
<td><p>Esta configuración requiere que una contraseña contenga caracteres numéricos y no numéricos. El valor predeterminado es <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Lista de aplicaciones aprobada</p></td>
<td><p>Esta configuración almacena una lista de aplicaciones aprobadas que se pueden ejecutar en el dispositivo móvil. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
<tr class="even">
<td><p>Datos adjuntos habilitados</p></td>
<td><p>Esta configuración permite que los datos adjuntos se descarguen al dispositivo móvil. El valor predeterminado es <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Cifrado de dispositivos habilitado</p></td>
<td><p>Esta configuración permite el cifrado en el dispositivo móvil. No todos los dispositivos móviles pueden imponer el cifrado. Para obtener más información, vea la documentación del sistema operativo móvil y del dispositivo.</p></td>
</tr>
<tr class="even">
<td><p>Intervalo de actualización de la directiva de dispositivos</p></td>
<td><p>Esta configuración especifica la frecuencia con la que se envía la directiva de buzones de dispositivos móviles del servidor al dispositivo móvil.</p></td>
</tr>
<tr class="odd">
<td><p>IRM habilitado</p></td>
<td><p>Esta configuración especifica si Information Rights Management (IRMB) está habilitado en el dispositivo móvil.</p></td>
</tr>
<tr class="even">
<td><p>Tamaño máximo del archivo adjunto</p></td>
<td><p>Esta configuración controla el tamaño máximo de los datos adjuntos que se puede descargar al dispositivo móvil. El valor predeterminado es Ilimitado.</p></td>
</tr>
<tr class="odd">
<td><p>Filtro máximo de antigüedad del calendario</p></td>
<td><p>Esta configuración especifica el intervalo máximo de días de calendario que se puede sincronizar a este dispositivo móvil. Se aceptan los siguientes valores:</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>Filtro de antigüedad máxima del correo electrónico</p></td>
<td><p>Esta configuración especifica el número máximo de días en que los elementos de correo electrónico se sincronizarán con el dispositivo móvil. Se aceptan los siguientes valores:</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Tamaño máximo de truncamiento del cuerpo del correo electrónico</p></td>
<td><p>Esta configuración especifica el tamaño máximo con el que los mensajes de correo electrónico se truncarán cuando se sincronicen con el dispositivo móvil. El valor se especifica en kilobytes (KB).</p></td>
</tr>
<tr class="even">
<td><p>Tamaño máximo de truncamiento del cuerpo en HTML del correo electrónico</p></td>
<td><p>Esta configuración especifica el tamaño máximo con el que los mensajes de correo electrónico HTML se truncarán cuando se sincronicen con el dispositivo móvil. El valor se especifica en kilobytes (KB).</p></td>
</tr>
<tr class="odd">
<td><p>Tiempo máximo de bloqueo de inactividad</p></td>
<td><p>Esta configuración especifica el tiempo que puede estar inactivo el dispositivo móvil antes de que se necesite una contraseña para volver a activarlo. Puede escribir cualquier intervalo entre 30 segundos y 1 hora. El valor predeterminado es de 15 minutos.</p></td>
</tr>
<tr class="even">
<td><p>Número máximo de intentos fallidos de contraseña</p></td>
<td><p>Esta configuración especifica el número de intentos que puede realizar un usuario para escribir la contraseña correcta para el dispositivo móvil. Puede escribir cualquier número comprendido entre 4 y 16. El valor predeterminado es 8.</p></td>
</tr>
<tr class="odd">
<td><p>Número mínimo de caracteres complejos de contraseña</p></td>
<td><p>Esta configuración especifica el número de juegos de caracteres requeridos en la contraseña del dispositivo móvil. Los juegos de caracteres son:</p>
<ul>
<li><p>Letras minúsculas.</p></li>
<li><p>Letras mayúsculas.</p></li>
<li><p>Números (0 - 9).</p></li>
<li><p>Caracteres especiales (por ejemplo, los signos de exclamación).</p></li>
</ul>
<p>Puede escribir cualquier número comprendido entre 1 y 4. El valor predeterminado es 1.</p>
<p>En dispositivos Windows Phone 8, esta configuración especifica el número de juegos de caracteres requeridos en la contraseña. Por ejemplo, el valor 3 requiere al menos un carácter de tres de los juegos de caracteres.</p>
<p>En dispositivos Windows Phone 10, esta configuración especifica los siguientes requisitos de complejidad de contraseña:</p>
<ol>
<li><p>Solo dígitos.</p></li>
<li><p>Dígitos y letras minúsculas.</p></li>
<li><p>Dígitos, letras minúsculas y letras mayúsculas.</p></li>
<li><p>Dígitos, letras minúsculas, letras mayúsculas y caracteres especiales.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>Longitud mínima de la contraseña</p></td>
<td><p>Esta configuración especifica el número mínimo de caracteres de la contraseña del dispositivo móvil. Puede escribir cualquier número comprendido entre 1 y 16. El valor predeterminado es 4.</p></td>
</tr>
<tr class="odd">
<td><p>Contraseña habilitada</p></td>
<td><p>Esta configuración habilita la contraseña del dispositivo móvil.</p></td>
</tr>
<tr class="even">
<td><p>Expiración de contraseña</p></td>
<td><p>Esta configuración permite que el administrador pueda configurar un intervalo del tiempo tras el que es necesario cambiar la contraseña del dispositivo móvil.</p></td>
</tr>
<tr class="odd">
<td><p>Historial de contraseñas</p></td>
<td><p>Esta configuración especifica el número de contraseñas antiguas que pueden almacenarse en el buzón del usuario. Un usuario no puede volver a usar una contraseña almacenada.</p></td>
</tr>
<tr class="even">
<td><p>Recuperación de contraseña habilitada</p></td>
<td><p>Al habilitar esta configuración, el dispositivo móvil genera una contraseña de recuperación que se envía al servidor. Si el usuario olvida la contraseña del dispositivo móvil, se puede usar la contraseña de recuperación para desbloquearlo y permitir al usuario crear una nueva contraseña para dicho dispositivo.</p></td>
</tr>
<tr class="odd">
<td><p>Requerimiento de cifrado del dispositivo</p></td>
<td><p>Esta configuración especifica si se requiere un cifrado del dispositivo. Si se establece en <code>$true</code>, el dispositivo móvil debe ser capaz de admitir e implementar el cifrado para que se sincronice con el servidor.</p></td>
</tr>
<tr class="even">
<td><p>Requiere mensajes S/MINE cifrados</p></td>
<td><p>Esta configuración especifica si los mensajes S/MIME deben cifrarse. El valor predeterminado es <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Requerimiento del algoritmo S/MIME de cifrado</p></td>
<td><p>Esta configuración especifica qué algoritmo requerido se debe usar al cifrar un mensaje S/MIME.</p></td>
</tr>
<tr class="even">
<td><p>Requiere sincronización manual durante la movilidad</p></td>
<td><p>Esta configuración especifica si el dispositivo móvil se debe sincronizar manualmente durante la movilidad. Permitir la sincronización automática al movilizarse llevará a costos de datos más que esperados para el plan de datos del dispositivo móvil.</p></td>
</tr>
<tr class="odd">
<td><p>Requerimiento del algoritmo S/MIME firmado</p></td>
<td><p>Esta configuración especifica qué algoritmo requerido se debe usar al firmar un mensaje.</p></td>
</tr>
<tr class="even">
<td><p>Requerimiento de mensajes S/MIME firmados</p></td>
<td><p>Esta configuración especifica si el dispositivo debe enviar mensajes S/MIME firmados.</p></td>
</tr>
<tr class="odd">
<td><p>Requiere cifrado de tarjeta de almacenamiento</p></td>
<td><p>Esta configuración especifica si la tarjeta de almacenamiento debe cifrarse. No todos los sistemas operativos de dispositivos móviles admiten el cifrado de la tarjeta de almacenamiento. Para obtener más información, vea la documentación del dispositivo y la del sistema operativo del mismo.</p></td>
</tr>
<tr class="even">
<td><p>Lista de aplicaciones InROM sin aprobar</p></td>
<td><p>Esta configuración especifica una lista de aplicaciones que no se pueden ejecutar en ROM. La licencia de acceso de cliente de Exchange Enterprise es necesaria para cambiar los valores de esta opción.</p></td>
</tr>
</tbody>
</table>

