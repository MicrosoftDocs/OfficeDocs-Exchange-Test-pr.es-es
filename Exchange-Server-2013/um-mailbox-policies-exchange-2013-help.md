---
title: 'directivas de buzón de mensajería unificada: Exchange 2013 Help'
TOCTitle: directivas de buzón de mensajería unificada
ms:assetid: dfae629e-ee89-4494-a3ed-9655b67eb87e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124909(v=EXCHG.150)
ms:contentKeyID: 50556899
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# directivas de buzón de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-15_

Las directivas de buzones de mensajería unificada (UM) son necesarias cuando habilita a los usuarios para mensajería unificada. Se crean directivas de buzones de mensajería unificada para aplicar un conjunto común de directivas o configuraciones de seguridad a una serie de buzones de usuarios de correo de voz. Las directivas de buzones de mensajería unificada permiten especificar configuraciones de mensajería unificada como las siguientes:

  - Directivas de PIN

  - Restricciones de marcado

  - Otras propiedades generales de directivas de buzón de mensajería unificada

Por ejemplo, puede crear una directiva de buzón de mensajería unificada para incrementar el nivel de seguridad del PIN, reduciendo el número máximo de errores de inicio de sesión de un grupo específico de usuarios con mensajería unificada, por ejemplo de ejecutivos.

## directivas de buzón de mensajería unificada

Se debe haber creado al menos una directiva de buzones de mensajería unificada para poder habilitar a los usuarios para mensajería unificada. Puede crear directivas de buzones de mensajería unificada para aplicar un conjunto común de valores a grupos de usuarios.

Para crear directivas de buzones de mensajería unificada, use el Shell de administración de Exchange o el Centro de administración de Exchange (EAC). De manera predeterminada, se crea una única directiva de buzón de mensajería unificada cada vez que crea un plan de marcado de mensajería unificada. La nueva directiva de buzones de mensajería unificada se asocia automáticamente al plan de marcado de mensajería unificada, y parte del nombre del plan se incluye en el nombre para mostrar de la directiva de buzones de mensajería unificada. La directiva de buzones de mensajería unificada predeterminada se puede editar.

Se pueden vincular varios usuarios habilitados para Mensajería unificada a una única directiva de buzón de Mensajería unificada. No obstante, el buzón de los usuarios habilitados para mensajería unificada debe estar vinculado a una única directiva de buzones de mensajería unificada. Esto permite controlar las opciones de seguridad del PIN, como el número mínimo de dígitos del PIN o el número máximo de intentos de inicio de sesión de los usuarios habilitados para mensajería unificada que están asociados a la directiva de buzones de mensajería unificada. También puede controlar la configuración de texto del mensaje o las restricciones de marcado para los mismos buzones habilitados para mensajería unificada.

