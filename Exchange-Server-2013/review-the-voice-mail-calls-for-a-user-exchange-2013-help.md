---
title: 'Revisar las llamadas de correo de voz para un usuario: Exchange 2013 Help'
TOCTitle: Revisar las llamadas de correo de voz para un usuario
ms:assetid: 95768fe3-3ae2-43bd-9cbf-18c3b85c4592
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659070(v=EXCHG.150)
ms:contentKeyID: 50556817
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Revisar las llamadas de correo de voz para un usuario

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Los registros de llamadas del usuario se usan para ver la siguiente información acerca de determinados usuarios de mensajería unificada:

  - Detalles acerca de las llamadas de mensajería unificada de un usuario en los últimos 90 días.

  - Calidad de audio de cada llamada. Puede que no estén disponibles las métricas de calidad de audio para todas las llamadas, ya que dependen de varios factores, como el tipo y la duración de la llamada.

Para tareas adicionales relacionadas con informes de mensajería unificada, consulte [Procedimientos de informes de mensajería unificada](um-reports-procedures-exchange-2013-help.md).

## ¿Cómo obtengo los registros de llamadas de un usuario habilitado para mensajería unificada?

1.  En el Centro de Administración de Exchange, seleccione **Mensajería unificada **\> **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") \> **Registros de llamadas de usuario**.

2.  Haga clic en **Seleccionar un usuario** y, a continuación, seleccione el usuario para el que desea los datos.

3.  Para obtener más detalles acerca de la calidad de audio de una fila del informe, seleccione la fila y haga clic en **Detalles de la calidad de audio**. Para obtener más información acerca cómo interpretar la calidad de audio, vea [Investigación de la calidad de audio de llamadas de voz para un usuario](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md).

4.  Para copiar el informe en el Portapapeles, haga clic en **Copiar todas las filas en el Portapapeles.**

## ¿Cómo interpreto el registro de llamadas de usuario de mensajería unificada?

El registro de llamadas de usuario incluye la siguiente información por cada llamada:

  - **FECHA Y HORA** La fecha y la hora de la llamada, en la zona horaria que el usuario seleccionado ha establecido en Microsoft Outlook Web App.

  - **DURACIÓN** El tiempo que ha durado la llamada, en minutos (MM) y segundos (SS), con el siguiente formato: MM:SS.

  - **TIPO DE LLAMADA   **El tipo de llamada:
    
      - **Contestador automático**   La llamada no ha sido atendida y se ha reenviado a los servidores de buzones de correo; el autor de la llamada ha dejado un mensaje de voz.
    
      - **Llamadas perdidas de contestador automático**   La llamada no ha sido atendida y se ha reenviado a los servidores de buzones de correo; el autor de la llamada no ha dejado un mensaje de voz.
    
      - **Acceso de suscriptor**   Realizó una llamada al número de acceso de suscriptor. El autor de la llamada inició sesión y se autenticó con la mensajería unificada con su extensión y contraseña para acceder a mensajes de correo electrónico, calendarios y mensajes de voz por teléfono.
    
      - **Operador automático**   Un operador automático de mensajería unificada ha atendido la llamada. Estas llamadas son las típicas llamadas en las que el autor de la llamada marca el número de teléfono principal de la organización.
    
      - **Fax**   Se recibió una llamada en la que se ha detectado un tono de fax. Si ha configurado asociados de fax, esta llamada se envió al asociado.
    
      - **Reproducir en teléfono**   Llamada que realiza la mensajería unificada cuando el usuario hace clic en el botón Reproducir en teléfono en Microsoft Outlook Web App o Outlook.
    
      - **Encontrarme**   Llamada saliente que realiza la mensajería unificada como resultado de la existencia de una regla Buscarme en una regla de contestador automático.
    
      - **Número piloto no autenticado**   Se colocó una llamada al número de Outlook Voice Access. El autor de la llamada no inició sesión y no se autenticó.
    
      - **Grabación de saludo**   Se colocó una llamada que realiza la mensajería unificada para registrar los saludos personales de un usuario.
    
      - **Ninguno**   Se colocó una llamada pero su tipo no se ha definido.

  - **NÚMERO QUE LLAMA** Número de teléfono o dirección de SIP del autor de la llamada.

  - **NÚMERO LLAMADO** Número de teléfono o dirección de SIP (para los usuarios de los planes de marcado de SIP, como los usuarios de Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server) del destinatario de la llamada.

  - **PUERTA DE ENLACE IP DE MENSAJERÍA UNIFICADA** Puerta de enlace IP de mensajería unificada que aceptó la llamada.

  - **CALIDAD DE AUDIO** Calidad de audio general de la llamada. Para obtener más detalles acerca de la calidad de audio, seleccione la fila y haga clic en **Detalles de calidad de audio**.

