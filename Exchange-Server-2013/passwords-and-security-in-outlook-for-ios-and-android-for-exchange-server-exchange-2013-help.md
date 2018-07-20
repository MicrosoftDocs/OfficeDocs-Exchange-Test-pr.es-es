---
title: 'Passwords and Security in Outlook for iOS and Android for Exchange Server: Exchange 2013 Help'
TOCTitle: Passwords and Security in Outlook for iOS and Android for Exchange Server
ms:assetid: e5565beb-7ef3-47c4-8daf-6d8f1d22dceb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt465750(v=EXCHG.150)
ms:contentKeyID: 70312149
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passwords and Security in Outlook for iOS and Android for Exchange Server

 

_**Se aplica a:** Exchange Server 2010, Exchange Server 2013_

_**Última modificación del tema:** 2018-04-01_

**Resumen:**  En este artículo se describe cómo funcionan las contraseñas y la seguridad en Outlook para iOS y Android con Exchange Server.

La primera vez que la aplicación Outlook para iOS y Android se ejecuta en un entorno de Exchange local, Outlook genera una clave AES-128 aleatoria. Esta clave se conoce como la *clave de dispositivo* y solo se almacena en el dispositivo del usuario.

## Crear una cuenta y proteger contraseñas

Cuando un usuario inicia sesión en Exchange, el nombre de usuario, la contraseña y una clave de dispositivo AES-128 única se envían desde el dispositivo del usuario al servicio Outlook a través de una conexión TLS, donde la clave de dispositivo se conserva en la memoria de cálculo en tiempo de ejecución. Después de comprobar la contraseña con el servidor de Exchange, el servicio Outlook usa la clave de dispositivo para cifrar la contraseña, y la contraseña cifrada se almacena posteriormente en el servicio. Mientras tanto, la clave de dispositivo se elimina de la memoria y nunca se almacena en el servicio Outlook (la clave solo se almacena en el dispositivo del usuario).

Después, cuando un usuario intenta conectarse a Exchange para recuperar los datos del buzón, la clave de dispositivo se pasa de nuevo del dispositivo al servicio Outlook a través de una conexión protegida por TLS, donde se usa para descifrar la contraseña en la memoria de cálculo en tiempo de ejecución. Una vez descifrada, la contraseña nunca se almacena en el servicio ni se escribe en un disco de almacenamiento local, y la clave de dispositivo se elimina de nuevo de la memoria.

Después de que el servicio Outlook haya descifrado la contraseña en tiempo de ejecución, el servicio puede conectarse al servidor de Exchange para sincronizar el correo, el calendario y otros datos del buzón. Siempre que el usuario abra y use Outlook periódicamente, el servicio Outlook conservará una copia de la contraseña descifrada del usuario en memoria para mantener la conexión activa con el servidor de Exchange.

## Inactividad de cuenta y vacío de contraseñas de la memoria

Después de tres días de inactividad, el servicio Outlook vaciará una contraseña descifrada de la memoria. Una vez se haya vaciado la contraseña descifrada, el servicio Outlook no podrá acceder al buzón del usuario. La contraseña cifrada sigue almacenándose en el servicio Outlook, pero descifrarla de nuevo no es posible sin la clave de dispositivo, que solo está disponible en el dispositivo del usuario.

Existen tres maneras en las que una cuenta de usuario puede volverse inactiva:

  - El usuario desinstala Outlook para iOS y Android.

  - La actualización de la aplicación en segundo plano está deshabilitada en las opciones de configuración y, después, se fuerza el cierre de Outlook.

  - Ninguna conexión de Internet está disponible en el dispositivo, evitando que Outlook se sincronice con Exchange.


> [!NOTE]
> Outlook no se volverá inactivo simplemente porque el usuario no abra la aplicación durante un período de tiempo, como el fin de semana o en vacaciones. Siempre que la actualización de la aplicación en segundo plano esté habilitada (que es la configuración predeterminada de Outlook para iOS y Android), las funciones como las notificaciones de inserción y la sincronización en segundo plano del correo electrónico contarán como actividad.



**Vaciar la contraseña cifrada y la caché de mensajes del disco duro**

El servicio Outlook vacía o elimina cuentas inactivas en una programación semanal. Después de que la cuenta de un usuario se vuelva inactiva, el servicio Outlook vaciará la contraseña cifrada y todo el contenido del buzón almacenado en caché del usuario del servicio.

**Combinación de seguridad de servicios y dispositivos**

Cada clave de dispositivo única de un usuario nunca se almacena en el servicio Outlook, y la contraseña de Exchange de un usuario nunca se almacena en el dispositivo. Esta arquitectura significa que para que una parte malintencionada obtenga acceso a la contraseña de un usuario, necesitará el acceso no autorizado del servicio Outlook y el acceso físico al dispositivo del usuario.

Al aplicar directivas de PIN y cifrado en dispositivos de su organización, la parte malintencionada también tendrá que superar el cifrado del dispositivo solo para obtener acceso a la clave de dispositivo. Esto tendría que tener lugar antes de que el usuario observe que el dispositivo se ha puesto en peligro y pida una eliminación remota de este.

## Preguntas más frecuentes de la seguridad de contraseñas

A continuación se muestran las preguntas más frecuentes con respecto a la configuración y el diseño de seguridad de Outlook para iOS y Android.

## ¿Se almacenan las credenciales de usuario en el servicio Outlook si bloqueo el acceso de Outlook a mi servidor de Exchange?

Si ha decidido bloquear el acceso de Outlook para iOS y Android a sus servidores de Exchange locales, Exchange rechazará la conexión inicial. El servicio Outlook no almacenará las credenciales de usuario y las credenciales que se encuentran en el intento de conexión erróneo se vacían inmediatamente de la memoria.

## ¿Cómo se cifra la contraseña de usuario y la clave de dispositivo en el tránsito al servicio Outlook?

Toda la comunicación entre la aplicación Outlook y el servicio Outlook se realiza mediante una conexión TLS cifrada. Outlook para iOS y Android es capaz de conectarse solo con el servicio Outlook.

## ¿Cómo quito las credenciales de usuario y la información del buzón del servicio de Outlook?

Existen tres maneras de quitar información del servicio Outlook:

  - Opción 1: Iniciar un borrado remoto para cada usuario que haya usado la aplicación para conectarse a Exchange.

  - Opción 2: Que todos los usuarios eliminen Outlook para iOS y Android. Todos los datos se quitarán del servicio Outlook aproximadamente de 3 a 7 días.

  - Opción 3: Que los usuarios quiten su cuenta de la aplicación Outlook y, después, eliminen la aplicación de sus dispositivos. En la aplicación, los usuarios deben ir a **Configuración**, pulsar **Configuración de cuenta**, **Seleccionar una cuenta** y, después, pulsar **Eliminar cuenta**.

## La aplicación se cierra o se desinstala, pero todavía la veo conectándose a mi servidor de Exchange. ¿Por qué ocurre esto?

El servicio Outlook descifra contraseñas de usuarios en la memoria de cálculo en tiempo de ejecución y, después, usa las contraseñas descifradas para conectarse a Exchange. Como el servicio Outlook está conectándose a Exchange en nombre del dispositivo para capturar y almacenar datos del buzón en caché, puede continuar así durante un breve período de tiempo hasta que el servicio detecte que Outlook ya no está solicitando datos.

Si un usuario desinstala la aplicación de su dispositivo sin usar primero la opción **Eliminar cuenta**, el servicio Outlook permanecerá conectado en su servidor de Exchange hasta que la cuenta se vuelva inactiva, como se ha descrito anteriormente en "Inactividad de cuenta y vacío de contraseñas de la memoria". Para detener esta actividad, simplemente siga la opción 1 o la opción 3 de las preguntas más frecuentes anteriores, o bloquee la aplicación como se describe en [Bloquear Outlook para iOS y Android](https://technet.microsoft.com/es-es/library/mt759239\(v=exchg.150\)).

## ¿Es una contraseña de usuario menos segura en Outlook para iOS y Android que cuando se usan otros clientes de Exchange ActiveSync?

No. Los clientes de EAS normalmente guardan las credenciales de usuario localmente en el dispositivo del usuario. Esto significa que un dispositivo robado o en peligro puede provocar que una parte malintencionada tenga acceso a la contraseña del usuario. Con el diseño de seguridad de Outlook para iOS y Android, una parte malintencionada necesitaría un acceso no autorizado al servicio en la nube de Outlook **y** tener acceso físico a un dispositivo del usuario.

## ¿Qué sucede si un usuario intenta usar Outlook para iOS y Android después de que sus datos se hayan eliminado del servicio Outlook?

Si una cuenta de usuario se vuelve inactiva (por ejemplo, deshabilitando la actualización de la aplicación en segundo plano en el dispositivo o desconectando el dispositivo de Internet durante un período de tiempo), la aplicación Outlook volverá a conectarse al servicio Outlook la próxima vez que la aplicación se inicie, y el proceso de almacenamiento en caché del correo electrónico y el cifrado de contraseña se reiniciará. Todo esto es transparente para el usuario.

## ¿Cómo se protegen los datos del buzón almacenados en caché temporalmente mientras se almacenan en el servicio Outlook?

Puede leer acerca de cómo nuestros datos están protegidos actualmente en el [Centro de confianza de Azure](https://azure.microsoft.com/support/trust-center/). Como se mencionó anteriormente, cambiamos de domicilio de Azure y Office 365. La seguridad de estos servicios está cubierta en [El centro de confianza de Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).

