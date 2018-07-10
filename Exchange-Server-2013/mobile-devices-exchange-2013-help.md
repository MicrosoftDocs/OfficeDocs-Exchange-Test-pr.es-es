---
title: 'Dispositivos móviles: Exchange 2013 Help'
TOCTitle: Dispositivos móviles
ms:assetid: 93a949e7-b3ef-43ea-ae0c-6698826fc8d2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232129(v=EXCHG.150)
ms:contentKeyID: 49895787
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dispositivos móviles

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-09-24_

Los dispositivos móviles habilitados para Microsoft Exchange ActiveSync permiten a los usuarios obtener acceso a la mayoría de sus datos de buzón de correo de Microsoft Exchange en cualquier momento y lugar. Existen muchos teléfonos y dispositivos móviles diferentes habilitados para Exchange ActiveSync. Entre ellos se incluyen los teléfonos Windows, teléfonos móviles Nokia, teléfonos y tablets Android, y los iPhone, iPod e iPad de Apple.

Pese a que estos dispositivos telefónicos y no telefónicos admiten Exchange ActiveSync, en la mayor parte de la documentación de Exchange ActiveSync se utiliza el término *dispositivo móvil*. A menos que las características que analicemos requieran una señal de teléfono móvil, como notificación de mensaje SMS, el término teléfono móvil se aplicará tanto a teléfonos móviles como a otros dispositivos móviles (como las tablets).

## Exchange ActiveSync

Exchange ActiveSync es un protocolo de comunicaciones que permite acceso móvil, a través del aire, a mensajes de correo electrónico, datos de programación, contactos y tareas. Exchange ActiveSync está disponible en teléfonos móviles de terceros de Windows habilitados para Exchange ActiveSync.

Exchange ActiveSync ofrece tecnología Direct Push. Direct Push usa una conexión HTTPS cifrada que se establece y mantiene entre el teléfono móvil y el servidor para insertar mensajes de correo electrónico nuevos y otros datos de Exchange en el teléfono.

Para usar Direct Push con MicrosoftExchange Server 2013, los usuarios deben tener un dispositivo móvil diseñado para ser compatible con Direct Push.

## Características de Exchange ActiveSync

Exchange ActiveSync proporciona acceso a muchas características diferentes que le permiten aplicar directivas de protección en los dispositivos móviles. Mediante Exchange 2013, puede configurar diversas directivas de buzones de correo del dispositivo móvil y controlar los dispositivos que pueden sincronizarse con el servidor de Exchange. Exchange ActiveSync le permite enviar un comando de eliminación remota del dispositivo que elimina todos los datos de un teléfono móvil en caso de pérdida o robo. Los usuarios también pueden iniciar una eliminación remota de datos del dispositivo móvil desde Outlook Web App.

Exchange ActiveSync permite a los usuarios generar una contraseña de recuperación. Esta contraseña de recuperación se guarda en el dispositivo móvil y se usa cuando el usuario olvida su contraseña. El usuario genera la contraseña de recuperación al mismo tiempo que genera el NIP o la contraseña del dispositivo. Esta contraseña de recuperación se puede usar para desbloquear el teléfono móvil. Inmediatamente después de usar esta contraseña de recuperación, se le solicitará al usuario que cree un NIP nuevo.

## POP3 e IMAP4

Si su teléfono móvil no admite Exchange ActiveSync, o bien no necesita el conjunto de características completas que proporciona Exchange ActiveSync, puede usar POP3 o IMAP4 para acceder a su correo electrónico desde el dispositivo móvil. Para obtener más información acerca del acceso al buzón de correo mediante POP3 e IMAP4, consulte [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

