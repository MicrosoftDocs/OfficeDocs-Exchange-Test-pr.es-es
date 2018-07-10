---
title: 'Administrar dispositivos en Outlook para iOS y Android para Exchange Server: Exchange 2013 Help'
TOCTitle: Administrar dispositivos en Outlook para iOS y Android para Exchange Server
ms:assetid: 16ce7d24-be74-4466-b126-828a67f69b6e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt465748(v=EXCHG.150)
ms:contentKeyID: 70312145
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar dispositivos en Outlook para iOS y Android para Exchange Server

 

_**Se aplica a:** Exchange Server 2010, Exchange Server 2013_

_**Última modificación del tema:** 2018-04-01_

**Resumen:**  En este artículo, se describe cómo Exchange Active Sync le ayuda a administrar dispositivos móviles con Outlook para iOS y Android en su organización local de Exchange.

Microsoft recomienda Exchange ActiveSync para administrar los dispositivos móviles que se usan para tener acceso a buzones de Exchange en su entorno local. Exchange ActiveSync es un protocolo de sincronización de Microsoft Exchange que permite a los teléfonos móviles tener acceso a la información de una organización en un servidor que está ejecutando Microsoft Exchange.

Este artículo se centra en los escenarios y características determinadas de Exchange ActiveSync para los dispositivos móviles que ejecutan Outlook para Android e iOS. La información completa sobre el protocolo de sincronización de Microsoft Exchange está disponible en [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md). Además, existe información en [el blog de Office](https://go.microsoft.com/fwlink/p/?linkid=62392) que detalla la aplicación de contraseñas y otras ventajas de usar Exchange ActiveSync con dispositivos que ejecutan Outlook para iOS y Android.

## Bloqueo de PIN y cifrado de dispositivos

Si la directiva de Exchange ActiveSync de su organización necesita una contraseña en los dispositivos móviles para que los usuarios sincronicen el correo electrónico, Outlook aplicará esta directiva en el nivel de dispositivo. Esto funciona de manera diferente entre dispositivos iOS y dispositivos Android, en función de los controles disponibles que Apple y Google han proporcionado.

En dispositivos iOS, Outlook comprueba para garantizar que se haya establecido correctamente un código de acceso o un PIN. En el caso de que no se haya establecido un código de acceso, Outlook pide a los usuarios que creen un código de acceso en la configuración de iOS. El usuario no podrá tener acceso a Outlook para iOS hasta que se configure el código de acceso.

Outlook para iOS solo se ejecuta en iOS 8.0 o versiones posteriores. Estos dispositivos se envían con cifrado integrado, que Outlook usa una vez que el código de acceso está habilitado para cifrar todos los datos que Outlook almacena localmente en el dispositivo iOS. Por lo tanto, los dispositivos iOS con un PIN, se cifrarán sea o no sea necesario para la directiva de ActiveSync.

En dispositivos Android, Outlook aplicará las reglas de bloqueo de pantalla. Además, Google proporciona controles que permiten que Outlook para Android cumpla con las directivas de Exchange con respecto a la complejidad y la longitud de contraseña, y con el número de intentos de desbloqueo de pantalla permitidos antes de eliminar los datos del teléfono. Outlook para Android también fomentará el cifrado de almacenamiento si no está habilitado, guiando a los usuarios a través de este proceso con un tutorial paso a paso.

Los dispositivos iOS y Android que no admitan esta configuración de seguridad de contraseña no podrán conectarse a un buzón de Exchange.

## Eliminación remota con Exchange ActiveSync

Exchange ActiveSync permite que los administradores eliminen datos de los dispositivos móviles de manera remota, por ejemplo, si están en peligro. Con Outlook para iOS y Android, se realiza una eliminación remota en la propia aplicación de Outlook, y no una eliminación completa de datos de los dispositivos móviles.

Después de que el administrador pida el comando de eliminación remota, la eliminación se produce segundos después de la siguiente conexión de la aplicación de Outlook a Exchange. La aplicación de Outlook se restablecerá y todos los datos de archivos, contactos, calendarios y correo electrónico de Outlook se quitarán del dispositivo, así como del servicio de Outlook. La eliminación no afectará a la información ni a ninguna aplicación personal del usuario fuera de Outlook.

Como Outlook para iOS y Android aparece como una asociación de dispositivos móviles única en los dispositivos móviles de un usuario de Exchange, un comando de eliminación remota quitará los datos y eliminará las relaciones de sincronización de todos los dispositivos que ejecutan Outlook (iPhone, iPad, Android) asociados con ese usuario.


> [!NOTE]
> Debido a la arquitectura de nube de Outlook para iOS y Android, el resultado de una eliminación remota de datos del dispositivo móvil no se notifica de nuevo a Exchange. Incluso cuando la eliminación se realice correctamente, el estado se mostrará como <STRONG>Pendiente</STRONG>. Este es un problema conocido y se está desarrollando una solución.



## Identificadores de dispositivo y control de acceso

Debido a la arquitectura basada en la nube de Outlook para iOS y Android, las conexiones de Outlook aparecen como un identificador de dispositivo móvil único (ID) para cada usuario de Exchange. Esto significa que los controles de acceso a los dispositivos móviles para cada usuario se aplican a todos los dispositivos asociados con este id. de dispositivo. Esta implementación crea dos condiciones que son diferentes de la manera de funcionamiento tradicional de los controles de acceso a los dispositivos de Exchange ActiveSync.

  - **Bloqueo:**  una regla de bloqueo bloquea Outlook en todos los dispositivos y sistemas operativos compatibles. No puede bloquear sistemas operativos ni dispositivos individuales.

  - **Cuarentena:**  el proceso de cuarentena funciona por usuario en lugar de por dispositivo. Una vez que un usuario tenga un dispositivo liberado de la cuarentena, puede instalar y configurar Outlook en todos los dispositivos adicionales que quiera. Como el usuario se ha liberado de la cuarentena, cualquier dispositivo nuevo asociado con ese usuario no estará en cuarentena.

Cuando existen directivas de buzón de correo para dispositivos móviles, se aplican a todos los dispositivos asociados. Por lo tanto, si aplica un bloqueo de PIN en un buzón determinado, todos los dispositivos que se conecten a ese buzón necesitarán un PIN.


> [!NOTE]
> Como los identificadores de dispositivo no se rigen por ningún identificador de <EM>dispositivo físico</EM>, pueden cambiarse sin previo aviso. Cuando esto suceda, puede provocar consecuencias no deseadas cuando los identificadores de dispositivo se usan para administrar dispositivos de usuario, ya que Exchange puede bloquear o poner en cuarentena de manera inesperada los dispositivos "permitidos" existentes. Por lo tanto, recomendamos que los administradores solo establezcan directivas de dispositivos móviles que permitan o bloqueen dispositivos en función del tipo o el modelo del dispositivo.



## Preguntas más frecuentes de la administración de dispositivos con Exchange ActiveSync

A continuación se muestran las preguntas más frecuentes sobre contraseñas, números PIN y directivas de cifrado para dispositivos que ejecutan Outlook para iOS y Android.

## La aplicación Correo nativa en iOS aplica directivas de Exchange ActiveSync para los requisitos de complejidad y longitud de contraseñas. ¿Por qué esto no sucede en Outlook?

Outlook se aprovecha de los controles de desarrolladores de aplicaciones de terceros que están disponibles en Microsoft. Seguiremos mejorando esta capacidad a medida que Apple realice más controles disponibles para los desarrolladores.

## ¿Por qué Outlook para iOS y Android aplica números PIN en el nivel de dispositivo en lugar de en el nivel de aplicación?

Después de evaluar las capacidades disponibles en iOS y Android, Microsoft cree que un PIN en el nivel de dispositivo proporciona la mejor experiencia para los clientes, en términos de comodidad y seguridad. Un PIN en el nivel de aplicación significa que los usuarios tienen que escribir dos números PIN diferentes para tener acceso al correo electrónico, lo que puede no ser conveniente. Además, un PIN en el nivel de dispositivo significa que podemos aprovecharnos de las características como el cifrado de dispositivos nativos, TouchID en iOS y Smart Lock en Android. La eliminación remota todavía se implementa en el nivel de aplicación, lo que significa que las aplicaciones personales de los usuarios y los datos no se verán afectados cuando Outlook se elimine.

## ¿Hace Outlook para el cifrado de dispositivos Android soporte?

Sí, Outlook para Android admite cifrado del dispositivo a través de directivas de buzón de Exchange dispositivo móvil. Sin embargo, antes de 7.0 Android, la disponibilidad y la implementación de este proceso varía según el sistema operativo Android versión y dispositivo fabricante, que permiten al usuario durante el proceso de cifrado se anulan. Con los cambios que introdujo Google Android 7.0, Outlook para Android ahora es capaz de exigir el cifrado en los dispositivos con Android 7.0 o posterior. Los usuarios con dispositivos que ejecutan estos sistemas operativos no podrá cancelar el proceso de cifrado.

Incluso si el dispositivo Android está cifrado y un atacante está en posesión del dispositivo, como un dispositivo PIN está habilitado, la base de datos de Outlook permanece inaccesible. Esto es cierto incluso con USB depuración habilitada y Android SDK instalado. Si un atacante intenta raíz en el dispositivo para que omita el PIN para tener acceso a esta información, el proceso de enraizamiento elimina el almacenamiento de información de todos los dispositivos y quita todos los datos de Outlook. Si el dispositivo está sin cifrar y arraigado por el usuario antes de ser robado, es posible que un atacante obtener acceso a la base de datos de Outlook al habilitar la depuración en el dispositivo USB y conectar el dispositivo a un equipo con el SDK de Android instalado.

