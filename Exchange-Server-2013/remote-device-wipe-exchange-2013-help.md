---
title: 'Borrado remoto del dispositivo: Exchange 2013 Help'
TOCTitle: Borrado remoto del dispositivo
ms:assetid: cd615210-cd8a-48de-b3e3-8f9ec39ca380
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124591(v=EXCHG.150)
ms:contentKeyID: 49895921
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Borrado remoto del dispositivo

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-09-19_

Los dispositivos móviles, tabletas y otros dispositivos pueden almacenar datos corporativos importantes y proporcionar acceso a varios recursos corporativos. Si un dispositivo móvil se pierde o es robado, los datos pueden estar en peligro. Con las directivas de buzón de dispositivo móvil de Microsoft Exchange, puede agregar una contraseña a los dispositivos móviles. De este modo, los usuarios deberán introducir una contraseña para tener acceso a sus dispositivos móviles. Le recomendamos que, además de requerir una contraseña para el dispositivo, configure los dispositivos móviles para que solicite automáticamente una contraseña después de un período de inactividad. La combinación de una contraseña para el dispositivo y del bloqueo por inactividad proporciona seguridad mejorada a sus datos corporativos.

Además de estas características, Exchange Server 2013 proporciona la eliminación remota de datos del dispositivo móvil. Puede emitir un comando de eliminación remota de datos del dispositivo móvil desde el Shell de administración Exchange del Centro de administración de Exchange (EAC). Los usuarios pueden emitir sus propios comandos de eliminación remota de datos del dispositivo móvil desde la interfaz de usuario de MicrosoftOutlook Web App.

La característica de eliminación remota de datos del dispositivo móvil también incluye una función de confirmación que escribe una marca de hora en los datos de estado de sincronización del buzón de correo del usuario. Esta marca de hora se muestra en Outlook Web App y en el cuadro de diálogo de las propiedades del teléfono móvil del usuario en el EAC.


> [!IMPORTANT]
> Mediante la eliminación remota de datos del dispositivo móvil se puede restablecer un teléfono móvil a la condición predeterminada de fábrica. Si bien el protocolo de eliminación remota de datos del dispositivo móvil tal como se implementa en Exchange&nbsp;2013 solo requiere la eliminación de datos corporativos personales, todos los fabricantes actuales de dispositivos móviles interpretan el comando como un comando que elimina todos los datos del teléfono. Los sistemas operativos de muchos dispositivos móviles también eliminan todos los datos de cualquier tarjeta de almacenamiento que esté insertada en el dispositivo. Si realiza una eliminación remota de datos en un teléfono móvil de su propiedad y desea conservar los datos de la tarjeta de almacenamiento, se recomienda quitar la tarjeta antes de iniciar la eliminación remota.




> [!WARNING]
> Tras realizar una eliminación remota de datos del dispositivo móvil, resulta muy difícil recuperar los datos. No obstante, ningún proceso de eliminación de datos deja un dispositivo móvil tan limpio de datos residuales como cuando es nuevo. Los datos de un dispositivo móvil se pueden recuperar con determinadas herramientas sofisticadas.



## Eliminación de dispositivos remota y eliminación de dispositivos local

La eliminación de dispositivos local ocurre cuando un dispositivo móvil se elimina sin que la solicitud venga del servidor. Si la organización ha implementado las directivas de buzón de dispositivo móvil que especifican un número máximo de intentos de contraseña incorrectos y ese máximo se ha superado, el dispositivo móvil realiza una eliminación local de datos. El resultado de una eliminación local de datos del dispositivo móvil es el mismo que el de una eliminación remota. El dispositivo vuelve a su condición predeterminada de fábrica. Cuando un dispositivo móvil realiza una eliminación de dispositivos local, no se envía ninguna confirmación al servidor de Exchange.

