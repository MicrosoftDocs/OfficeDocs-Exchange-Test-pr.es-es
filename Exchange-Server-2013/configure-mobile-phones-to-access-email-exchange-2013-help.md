---
title: 'Configurar teléfonos móviles para tener acceso al correo electrónico: Exchange 2013 Help'
TOCTitle: Configurar teléfonos móviles para tener acceso al correo electrónico
ms:assetid: 8d6e2cea-265a-43d9-a074-076f35658436
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123704(v=EXCHG.150)
ms:contentKeyID: 52061849
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar teléfonos móviles para tener acceso al correo electrónico

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-12_

Puede configurar un teléfono móvil, como Windows Phone para usar Microsoft Exchange ActiveSync. Debe realizar este procedimiento en cada teléfono móvil de la organización.

## Requisitos previos

  - Ha revisado la documentación del fabricante del teléfono móvil que desea configurar.

  - Su organización tiene habilitado Exchange ActiveSync.


> [!NOTE]
> Para obtener información específica sobre cómo configurar correo electrónico basado en Microsoft Exchange en un teléfono o en una tableta, consulte <A href="https://support.office.com/es-es/article/set-up-a-mobile-device-using-office-365-for-business-7dabb6cb-0046-40b6-81fe-767e0b1f014f">Configurar un dispositivo móvil con Office&nbsp;365 para empresas</A>.



## Configurar un teléfono móvil para usar Exchange ActiveSync

La mayoría de teléfonos y dispositivos móviles pueden detectar automáticamente la configuración del cliente de correo móvil para usar Exchange ActiveSync. Para configurar una cuenta de correo electrónico en la mayoría de teléfonos móviles, necesitará dos datos.

  - La dirección de correo electrónico del usuario

  - La contraseña del usuario

Si el teléfono móvil no puede establecer contacto con el servidor Exchange mediante la detección automática, deberá configurar el teléfono móvil manualmente. Para realizar la configuración manual, necesitará la dirección de correo electrónico y la contraseña del usuario, así como el nombre del servidor Exchange ActiveSync. En la mayoría de organizaciones, el nombre del servidor Exchange ActiveSync es el mismo que el nombre del servidor Outlook Web App sin /owa, por ejemplo, mail.contoso.com.

## Sincronización de Windows Phone

Si está configurando un teléfono móvil Windows Phone para que se sincronice con un buzón de Exchange usando Exchange ActiveSync, sólo es compatible un subconjunto de directivas de buzón de dispositivo móvil. Esta configuración de directivas se describe en [Directivas de buzones de correo para dispositivos móviles compatibles con teléfonos y dispositivos de Windows](supported-mobile-device-mailbox-policies-for-windows-phones-and-devices-exchange-2013-help.md).

Si configura los ajustes de directivas de buzones de dispositivos móviles que no están admitidas en la versión de Windows Phone que utiliza, también deberá establecer el ajuste de la directiva **AllowNonProvisionableDevices** en verdadero o crear una directiva de buzones de dispositivos móviles separada para teléfonos móviles Windows Phone.

