---
title: 'Configurar características de correo de voz de cliente: Exchange 2013 Help'
TOCTitle: Configurar características de correo de voz de cliente
ms:assetid: 5e661cfd-d34e-4caa-91a5-967bbecb75eb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673529(v=EXCHG.150)
ms:contentKeyID: 50556794
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar características de correo de voz de cliente

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-20_

En este tema, se describen las características de cliente que proporcionan acceso a los mensajes de correo electrónico y de voz de su buzón de correo para los usuarios habilitados para la mensajería unificada (MU) de Exchange. Estas características le permiten ofrecer a los usuarios acceso simplificado a su correo de voz y electrónico y una mejor experiencia general de usuario.

**Contenido**

Voice mail client support

Outlook Voice Access

Forwarding calls

Voice Mail Preview

Receiving faxes

## Soporte para el cliente de correo de voz

**Clientes de Exchange ActiveSync**   El protocolo Microsoft Exchange ActiveSync se usa para conectar clientes móviles, como los que se encuentran en dispositivos móviles para Internet, a un buzón de Exchange. Los usuarios pueden usar dispositivos móviles para obtener acceso a su buzón de correo, ver sus mensajes de correo electrónico, ver y modificar la información de contacto y de calendario y escuchar sus mensajes de correo de voz. También pueden sincronizar sus elementos de calendario y correo de voz y electrónico, y su información de contacto con otros dispositivos.

**Integración con Outlook**   Microsoft Outlook permite a los usuarios obtener acceso a su buzón de Exchange, ver mensajes de correo electrónico en su Bandeja de entrada, ver y modificar la información de contacto y de calendario y escuchar sus mensajes de correo de voz mediante el Reproductor de Windows Media de Microsoft, que está integrado en los mensajes de correo electrónico. Al usar un cliente de correo electrónico compatible, los usuarios obtienen características adicionales, como la funcionalidad de Reproducir en teléfono.

**Integración con Outlook Web App**   Microsoft Outlook Web App proporciona a los usuarios un conjunto de interfaces de MU y herramientas comparables con un cliente de correo electrónico con todas las características, como Outlook. Con Outlook Web App, los usuarios pueden acceder a su buzón de Exchange utilizando un explorador web compatible. Al igual que Outlook, Outlook Web App proporciona el Reproductor de Windows Media integrado en los mensajes de correo electrónico para permitir a los usuarios escuchar los mensajes de voz, además de dejarles obtener acceso a otras características, como Reproducir en teléfono.

## Outlook Voice Access

En la mensajería unificada de Exchange, un usuario habilitado para la mensajería unificada puede llamar a un número de teléfono interno o externo configurado en un plan de marcado de MU para obtener acceso a su buzón de correo y usar el sistema de menús de Outlook Voice Access. Gracias a este menú, dichos usuarios pueden leer su correo electrónico, escuchar los mensajes de voz, interactuar con su calendario de Outlook, tener acceso a sus contactos personales y realizar tareas tales como configurar su PIN de Outlook Voice Access o grabar saludos de correo de voz. Para obtener información más detallada, consulte [Configuración de Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md).

## Reenvío de llamadas

Un usuario habilitado para la mensajería unificada puede crear y configurar reglas de respuesta a llamada con Outlook o Outlook Web App. Las reglas de respuesta a llamada permiten a los usuarios controlar cómo deben manejarse sus llamadas entrantes. Las reglas se aplican a las llamadas entrantes de manera similar al modo en que las reglas se aplican a los mensajes de correo de la bandeja de entrada, y se almacenan junto con otra configuración de voz en el buzón de correo del usuario. Es posible configurar hasta nueve reglas de respuesta a llamada para cada buzón de correo habilitado para la mensajería unificada. Estas reglas son independientes de las reglas de la Bandeja de entrada y no ocupan ninguna parte de la cuota de almacenamiento de las reglas de la Bandeja de entrada del usuario. Para obtener información más detallada, consulte [Permitir usuarios de mail reenviar llamadas de voz](allow-voice-mail-users-to-forward-calls-exchange-2013-help.md).

## Vista previa del correo de voz

La vista previa del correo de voz es una característica disponible para los usuarios que reciben mensajes de voz del sistema de correo de voz de la mensajería unificada. La vista previa del correo de voz mejora la experiencia de correo de voz, ya que proporciona una versión de texto de las grabaciones sonoras. Para obtener información detallada, consulte [Permitir a los usuarios ver una transcripción de correo de voz](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md).

## Recepción de faxes

La mensajería unificada reenvía las llamadas de fax entrantes de los usuarios habilitados para la mensajería unificada a una solución de asociado de fax dedicada que, luego, relaciona la llamada de fax con el remitente del fax y lo recibe en nombre del usuario. Antes de que sus usuarios habilitados para la mensajería unificada puedan recibir mensajes de fax en su buzón de correo, debe hacer lo siguiente:

  - Habilitar los faxes entrantes en el plan de marcado de MU vinculado a los usuarios. Para hacerlo, configure el parámetro *FaxEnabled* en `$true`.

  - Habilitar los faxes entrantes en el plan de marcado de MU vinculado a los usuarios. Para hacerlo, configure el parámetro *Allowfax* en `$true`.

  - Habilitar los faxes entrantes para los usuarios. Para hacerlo, configure el parámetro *FaxEnabled* en `$true`.

  - Configurar el URI de servidor de fax asociado para permitir los faxes entrantes.

  - Configurar la autenticación entre el servidor de buzones y el servidor de fax asociado.

