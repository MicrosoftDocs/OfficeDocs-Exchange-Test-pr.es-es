---
title: 'Configurar la seguridad del PIN de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurar la seguridad del PIN de Outlook Voice Access
ms:assetid: ef6d9151-d333-4f52-9338-273f7a291e54
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125162(v=EXCHG.150)
ms:contentKeyID: 50556905
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar la seguridad del PIN de Outlook Voice Access

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-16_

Cuando los usuarios de mensajería unificada (UM) se conectan al sistema de correo de voz por teléfono, usan Outlook Voice Access para navegar por el sistema de menús. El sistema solicita a los usuarios que especifiquen su PIN para que puedan tener acceso al sistema de correo de voz. Como administrador, puede configurar los valores y requisitos del PIN y ejecutar tareas de administración del PIN. Después de que un usuario se haya habilitado para el correo de voz y se haya generado un PIN, el PIN del usuario se almacena cifrado en su buzón.


> [!NOTE]
> Los usuarios de Outlook Voice Access deben usar entradas de marcación por tonos (también denominado tono de marcado de frecuencia múltiple (DTMF)) para especificar su PIN y tener así acceso al buzón habilitado para mensajería unificada. El reconocimiento de voz no está disponible para la entrada de PIN.



**Contenido**

Información general del PIN

Requisitos de PIN

Administración de PIN de Outlook Voice Access

## Información general del PIN

El PIN es una cadena numérica que se utiliza en algunos sistemas para que el usuario se pueda autenticar y obtener acceso a ellos. Los PIN se suelen utilizar sobre todo en los cajeros automáticos. También se utilizan en lugar de contraseñas alfanuméricas para sistemas de correo de voz. El nivel de seguridad de un PIN depende de su longitud, de lo bien que esté protegido y de lo difícil que resulte averiguarlo.

En la mensajería unificada, los usuarios de Outlook Voice Access escriben el PIN en un teléfono analógico, digital o móvil para que puedan tener acceso a correo electrónico, correo de voz, contactos o información de calendario en su buzón de Exchange Server.

En la mensajería unificada, las directivas de PIN se definen y se configuran en una directiva de buzones de mensajería unificada. Puede crear varias directivas de buzones de mensajería unificada dependiendo de sus necesidades. Cuando se habilita a un usuario para correo de voz, se le vincula a una directiva de buzones de mensajería unificada existente. Las directivas de PIN de mensajería unificada que se configuran en la directiva de buzón de mensajería unificada deben basarse en los requisitos de seguridad de la organización.

## Requisitos de PIN

A continuación se describen varias configuraciones de PIN que se pueden establecer en una directiva de buzones de mensajería unificada.

## Longitud mínima del NIP

El valor **Longitud mínima del PIN** especifica el número mínimo de dígitos que puede tener el PIN de un buzón. El intervalo va de 4 a 24, y el valor predeterminado es 6. Si escribe 0, los usuarios no tienen que especificar ningún PIN.


> [!IMPORTANT]
> Sin embargo, no se recomienda establecer este valor en cero. Si se configura en cero, disminuye considerablemente el nivel de seguridad de la red.



Si cambia el valor de longitud mínima del PIN a un valor superior, se solicita a los usuarios de Outlook Voice Access existentes que creen un nuevo PIN que contenga el nuevo número mínimo de dígitos para que puedan continuar.


> [!NOTE]
> Si aumenta este número, creará un entorno de mensajería unificada más seguro. Como contrapartida, si el valor es demasiado alto, los usuarios pueden olvidar el PIN.



## Aplicar vigencia del PIN

El valor **Aplicar vigencia de PIN** controla el intervalo de tiempo, en días, desde la última fecha en la que los usuarios de Outlook Voice Access cambiaron el PIN hasta la fecha en la que deben volver a cambiarlo. El intervalo es de 0 a 999, siendo el valor predeterminado 60 días. Si se especifica 0, el PIN no caducará.


> [!NOTE]
> La mensajería unificada no avisa a los usuarios cuando su PIN está a punto de caducar.



## Número de errores de inicio de sesión antes de restablecer el PIN

El valor **Número de errores de inicio de sesión antes de restablecer el PIN** especifica el número de intentos de inicio de sesión incorrectos seguidos antes de que el PIN del buzón se restablezca automáticamente. Para deshabilitar esta característica, establezca este valor en ilimitado. De lo contrario, se debe establecer en un número inferior al valor de **Número de errores de inicio de sesión antes de bloquearlo**. El intervalo es de 1 a 998, siendo el valor predeterminado 5.


> [!NOTE]
> Para aumentar la seguridad de los usuarios con mensajería unificada habilitada, especifique un número inferior a 5.



## Número de errores de inicio de sesión antes de bloquearlo

El valor **Número de errores de inicio de sesión antes de bloquearlo** especifica el número de errores de entrada de PIN en llamadas sucesivas que los usuarios de Outlook Voice Access pueden realizar antes de bloquear su buzón. De forma predeterminada, después de 5 intentos, el PIN se restablece automáticamente. El intervalo es de 1 a 999, siendo el valor predeterminado 15.


> [!NOTE]
> Para aumentar la seguridad, disminuya el número de intentos con error permitidos. Recuerde que si disminuye este valor a un número muy inferior al valor predeterminado, puede ocasionar el bloqueo innecesario del buzón de los usuarios. Si se produce algún error en la autenticación del PIN de algún usuario con la mensajería unificada habilitada o si el usuario no logra iniciar sesión en el sistema, la mensajería unificada generará advertencias, que se pueden ver con el Visor de sucesos.



## Permitir patrones comunes de PIN

El valor **Permitir patrones comunes de PIN** se utiliza para habilitar o deshabilitar el uso de patrones numéricos comunes al crear un PIN. De manera predeterminada, esta configuración está deshabilitada y no permite a los usuarios de Outlook Voice Access especificar los siguientes patrones numéricos:

  - **Números secuenciales**   Valores de PIN formados totalmente por números consecutivos. Ejemplos de números secuenciales para un PIN son 1234 y 65432.

  - **Números repetidos**   Valores de PIN formados por números repetidos. Ejemplos de números repetidos son 11111 y 22222.

  - **Sufijo de extensión de buzón**   Valores de PIN formados por el sufijo de la extensión de buzón de un usuario. Si la extensión de buzón es 36697, el PIN no puede ser 6697.

## Número de reciclajes de PIN

El valor **Número de reciclajes de PIN** configura el número de PIN diferentes que debe utilizar el usuario para poder volver a utilizar los PIN previamente utilizados. El intervalo es de 1 a 20, siendo el valor predeterminado 5.

## Administración de PIN de Outlook Voice Access

Al planificar la configuración de PIN de Outlook Voice Access, debe elegir los niveles adecuados de seguridad para la organización. Preste mucha atención a los requisitos de PIN de Outlook Voice Access y a cómo los valores de seguridad del PIN satisfacen o superan la directiva de seguridad de la organización.


> [!IMPORTANT]
> La práctica de seguridad recomendada consiste en implementar requisitos seguros de PIN para los usuarios de Outlook Voice Access. Esto se puede lograr mediante la creación de directivas de PIN de directivas de buzones de mensajería unificada que requieran PIN de seis o más dígitos, lo que permite aumentar el nivel de seguridad de la red.



Después de establecer los requisitos de PIN de Outlook Voice Access, debe crear y configurar una directiva de buzones de mensajería unificada para aplicar los requisitos de PIN organizativos. Para obtener más detalles acerca de cómo crear una directiva de buzones de mensajería unificada, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md). Para obtener más detalles acerca de cómo administrar las directivas de buzones de mensajería unificada, consulte [Administrar una directiva de buzones de correo de mensajería unificada](manage-a-um-mailbox-policy-exchange-2013-help.md).


> [!NOTE]
> Después de crear la directiva de buzones de mensajería unificada, debe vincular al usuario o usuarios habilitados para mensajería unificada con la directiva de buzones apropiada. Para ello, utilice el cmdlet <STRONG>Enable-UMMailbox</STRONG> en el Shell de administración de Exchange o en el Centro de administración de Exchange (EAC). Para obtener más información acerca del cmdlet del Shell de administración de Exchange, consulte <A href="https://technet.microsoft.com/es-es/library/aa998033(v=exchg.150)">Enable-UMMailbox</A>.



Hay situaciones en las que los usuarios de Outlook Voice Access olvidan su PIN o se les bloquea el acceso al correo de voz de su buzón. En cualquier caso, puede ser necesario que se restablezca el PIN del usuario habilitado para mensajería unificada. Para obtener información más detallada, consulte [Restablecer el PIN del correo de voz.](reset-a-voice-mail-pin-exchange-2013-help.md).

Puede recuperar la información del PIN de un usuario que está habilitado para mensajería unificada. La información devuelta se calcula mediante los datos cifrados del PIN almacenados en el correo del usuario. Esto permite ver información del PIN del usuario y también indica si se ha bloqueado su buzón. Para obtener información detallada, consulte [Recuperar información de PIN del correo de voz](retrieve-voice-mail-pin-information-exchange-2013-help.md).

