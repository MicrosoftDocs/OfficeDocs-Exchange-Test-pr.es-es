---
title: 'Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync
ms:assetid: 5fafaff3-eb37-4fdb-95f0-e56c45ea5884
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998357(v=EXCHG.150)
ms:contentKeyID: 48268190
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Obtenga más información acerca del protocolo de cliente de Exchange ActiveSync para Exchange Server 2013. Conocerá las características de Exchange ActiveSync, incluidas las características de seguridad, los elementos que puede administrar, cómo hacer que sea seguro y cómo evitar problemas de sincronización con Windows Phone 7.


> [!TIP]
> Este tema es para administradores. ¿Desea configurar su dispositivo Windows Phone, iOS o Android para poder acceder al buzón de Office 365 o Exchange Server? Consulte los temas siguientes. 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615415">Configurar el correo en Windows Phone</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615414">Configurar el correo electrónico en un iPhone, iPad o iPod Touch</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/?linkid=615417">Configurar el correo electrónico en una tableta o un teléfono Android</A></P></LI></UL>



Exchange ActiveSync es un protocolo de cliente que permite sincronizar un dispositivo móvil con un buzón de correo de Exchange. Exchange ActiveSync se habilita de manera predeterminada cuando se instala Microsoft Exchange 2013.

**Contenido**

Introducción a Exchange ActiveSync

Características de Exchange ActiveSync

Administrar Exchange ActiveSync

Sincronización de Windows Phone 7

## Introducción a Exchange ActiveSync

Exchange ActiveSync es un protocolo de sincronización de Microsoft Exchange que se optimiza para trabajar con redes de latencia elevada y ancho de banda bajo. El protocolo, basado en HTTP y XML, permite que los teléfonos móviles obtengan acceso a la información de una organización en un servidor que ejecuta Microsoft Exchange. Exchange ActiveSync permite que los usuarios de teléfonos móviles obtengan acceso al correo electrónico, el calendario, los contactos, las tareas y que puedan obtener acceso a esta información cuando trabajan sin conexión.


> [!NOTE]
> Exchange ActiveSync no admite buzones compartidos ni acceso delegado.




> [!IMPORTANT]
> Los teléfonos móviles de Windows Phone 7 solamente admiten un subconjunto de parámetros de directivas de buzones de Exchange ActiveSync. Para obtener una lista completa, consulte Sincronización de Windows Phone 7.



## Características de Exchange ActiveSync

Exchange ActiveSync proporciona lo siguiente:

  - Compatibilidad con mensajes HTML

  - Compatibilidad con marcadores de seguimiento

  - Agrupación de conversaciones de mensajes de correo electrónico

  - Capacidad para sincronizar o no sincronizar una conversación completa

  - Sincronización de los mensajes del servicio de mensajes cortos (SMS) con el buzón de un usuario de Exchange

  - Compatibilidad con la visualización del estado de respuesta de mensajes

  - Compatibilidad con la recuperación rápida de mensajes

  - Información de asistentes a reuniones

  - Búsqueda de Exchange mejorada

  - Restablecimiento de NIP

  - Seguridad de dispositivos mejorada mediante directivas de contraseña

  - Detección automática para la provisión a través del aire

  - Compatibilidad con la configuración de respuestas automáticas cuando los usuarios están ausentes, de vacaciones o fuera de la oficina

  - Compatibilidad con la sincronización de tareas

  - Envío directo

  - Compatibilidad con la información de disponibilidad de los contactos

## Administrar Exchange ActiveSync

Exchange ActiveSync está habilitado de forma predeterminada. Todos los usuarios que tienen un buzón de Exchange pueden sincronizar el dispositivo móvil con el servidor de Microsoft Exchange.

Puede realizar las siguientes tareas de Exchange ActiveSync:

  - Habilitar e inhabilitar Exchange ActiveSync para los usuarios

  - Establecer directivas como la longitud mínima de las contraseñas, el bloqueo de dispositivos y el número máximo de intentos erróneos de contraseña

  - Iniciar una limpieza remota para borrar todos los datos de un teléfono móvil perdido o robado

  - Ejecutar una serie de informes para su visualización o exportación en diversos formatos

  - Controlar los tipos de dispositivos móviles que se pueden sincronizar con su organización mediante reglas de acceso de dispositivo

## Seguridad en Exchange ActiveSync

Puede configurar Exchange ActiveSync para utilizar el cifrado de Capa de sockets seguros (SSL) a fin de establecer la comunicación entre el servidor Exchange y el dispositivo móvil.

## Administrar el acceso de los dispositivos móviles en Exchange ActiveSync

Puede controlar los dispositivos móviles que se pueden sincronizar. Para ello, supervise los nuevos dispositivos móviles a medida que se conectan a la organización o establezca reglas que determinen los tipos de dispositivos móviles que se pueden conectar. Independientemente del método que elija para especificar los dispositivos móviles que se pueden sincronizar, puede aceptar o denegar el acceso a cualquier dispositivo móvil para un usuario específico en un momento dado

## Características de seguridad del dispositivo en Exchange ActiveSync

Además de la capacidad para configurar las opciones de seguridad de las comunicaciones entre el servidor de Exchange y los dispositivos móviles, Exchange ActiveSync ofrece las siguientes características para mejorar la seguridad de los dispositivos móviles:

  - **Eliminación remota**   En caso de pérdida o robo de un dispositivo móvil, o si un dispositivo se encuentra en alguna situación peligrosa, puede ejecutar un comando de eliminación remota desde el equipo con Exchange Server o desde cualquier explorador web usando Outlook Web App. Este comando borra todos los datos del dispositivo móvil.

  - **Directivas de contraseña de dispositivos **  Exchange ActiveSync permite configurar varias opciones de contraseñas para el dispositivo.
    

    > [!WARNING]
    > No se puede usar la tecnología de lector de huellas digitales de iOS7 como dispositivo de contraseña. Si elige usar el lector de huellas digitales de iOS7, necesitará crear y especificar una contraseña de dispositivo si la directiva de buzón de correo del dispositivo móvil de su organización requiere una contraseña de dispositivo.

    
    Entre las opciones de contraseña de dispositivo se incluyen las siguientes:
    
      - **Longitud mínima de contraseña (caracteres)**   Esta opción especifica la longitud de la contraseña del dispositivo móvil. La longitud predeterminada es de 4 caracteres, pero puede tener un máximo de 18.
    
      - **Cantidad mínima de conjuntos de caracteres**   Este cuadro de texto se usa para especificar la complejidad de la contraseña alfanumérica y exigir a los usuarios el uso de una cantidad de conjuntos de caracteres distintos de entre los siguientes: minúsculas, mayúsculas, símbolos y números.
    
      - **Requerir contraseña alfanumérica**   Esta opción determina la potencia de la contraseña. Puede hacer que se use un carácter o símbolo en la contraseña, además de los números.
    
      - **Tiempo de inactividad (segundos)**   Esta opción determina el tiempo que el dispositivo móvil debe estar inactivo antes de que se le solicite al usuario una contraseña que lo desbloquee.
    
      - **Exigir historial de contraseñas**   Seleccione esta casilla de verificación para exigir el teléfono móvil para evitar que el usuario vuelva a usar sus contraseñas anteriores. El número definido determina la cantidad de contraseñas anteriores que el usuario no podrá volver a usar.
    
      - **Permitir la recuperación de contraseña**   Active esta casilla para permitir la recuperación de la contraseña del dispositivo móvil.  Los administradores pueden usar el cmdlet **Get-ActiveSyncDeviceStatistics** para buscar la contraseña de recuperación del usuario.
    
      - **Borrar dispositivo después de error (intentos)**  Esta opción le permite especificar si desea limpiar la memoria del teléfono después de varios intentos erróneos de contraseña.

  - **Directivas de cifrado de dispositivos**   Hay varias directivas de cifrado de dispositivos móviles que puede aplicar a un grupo de usuarios. Estas directivas son las siguientes:
    
      - **Requerir cifrado en el dispositivo**   Active esta casilla para requerir el cifrado en el dispositivo móvil. Esto aumenta la seguridad mediante el cifrado de toda la información del dispositivo móvil.
    
      - **Pedir cifrado en tarjetas de almacenamiento**   Active esta casilla para requerir el cifrado en la tarjeta de almacenamiento extraíble del dispositivo móvil. Esto aumenta la seguridad mediante el cifrado de toda la información en las tarjetas de almacenamiento del dispositivo móvil.

## Sincronización de Windows Phone 7

Si tiene dispositivos móviles de Windows Phone 7 en su organización, estos dispositivos experimentarán problemas de sincronización si se configuran ciertas propiedades de la directiva de buzón de dispositivo móvil. Para permitir que los teléfonos móviles de Windows Phone 7 se sincronicen con un buzón de correo de Exchange, establezca la propiedad **AllowNonProvisionableDevices** en True o configure solo las siguientes propiedades de directiva de buzón de dispositivo móvil:

  - PasswordRequired

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - DeviceWipeThreshold

  - AllowSimplePassword

  - PasswordExpiration

  - PasswordHistory

  - DisableRemovableStorage

  - DisableIrDA

  - DisableDesktopSync

  - BlockRemoteDesktop

  - BlockInternetSharing

