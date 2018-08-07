---
title: 'Recuperar mensajes en cuarentena del buzón de cuarentena de correo no deseado'
TOCTitle: Recuperar mensajes en cuarentena del buzón de cuarentena de correo no deseado
ms:assetid: 7a86bfde-f868-4689-bdec-5f01e52b510d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998920(v=EXCHG.150)
ms:contentKeyID: 49895731
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recuperar mensajes en cuarentena del buzón de cuarentena de correo no deseado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Puede utilizar Microsoft Outlook para recuperar un mensaje en cuarentena del buzón en cuarentena de correo no deseado.

Cuarentena de correo no deseado es una característica del agente de filtrado de contenido que reduce el riesgo de perder mensajes legítimos. Cuando un mensaje coincide con el umbral de cuarentena de correo no deseado, se lo ubica en un informe de no entrega (NDR) y se lo envía al buzón de cuarentena de correo no deseado. Para obtener más información acerca de la característica de cuarentena de correo no deseado, consulte [Cuarentena de correo electrónico no deseado](spam-quarantine-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Acceso a buzones" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Este procedimiento requiere que haya configurado el buzón de cuarentena de correo no deseado. Para obtener más información, consulte [Configurar un buzón de cuarentena de correo no deseado](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

  - Para tener acceso al buzón de cuarentena, debe configurar un perfil de Outlook para ese buzón y, a continuación, abrir el buzón mediante Outlook. Para obtener más información acerca de cómo configurar y utilizar varios perfiles de Outlook, vea [Descripción general de correo electrónico perfiles Outlook](https://go.microsoft.com/fwlink/p/?linkid=178975).

  - Para localizar el mensaje que desea recuperar con más facilidad, puede crear un formulario de Outlook personalizado y modificar la vista predeterminada para mostrar la dirección del remitente original en la lista de mensajes. Para obtener instrucciones detalladas, consulte [Configurar Outlook para mostrar el remitente original en el buzón de cuarentena](configure-outlook-to-show-the-original-sender-in-the-quarantine-mailbox-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Utilice Outlook 2010 o Outlook 2013 para publicar un mensaje del buzón en cuarentena de correo no deseado

1.  Abra el buzón en cuarentena a través de Outlook 2010 o Outlook 2013 en un equipo cliente.

2.  En la vista **Correo**, busque el mensaje que desea recuperar en la **Bandeja de entrada** y, a continuación, haga doble clic en el mensaje para abrirlo.

3.  En la sección **Mover** de la Cinta, haga clic en **Acciones** \> **Enviar de nuevo este mensaje**.

4.  Cuando se abra el mensaje, haga clic en **Enviar** para volver a enviar el mensaje al destinatario deseado.

## Usar Outlook 2007 para enviar un mensaje desde el buzón de cuarentena de correo no deseado

1.  Abra el buzón en cuarentena mediante Outlook 2007 en un equipo cliente.

2.  En la vista **Carpetas de correo**, busque el mensaje que desea recuperar en la **Bandeja de entrada** y, a continuación, haga doble clic en el mensaje para abrirlo.

3.  En la ficha **Informe**, en el grupo **Responder**, haga clic en **Enviar de nuevo**.

4.  Cuando se abra el mensaje, haga clic en **Enviar** para volver a enviar el mensaje al destinatario deseado.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha enviado el mensaje correctamente desde el buzón en cuarentena de correo no deseado, contacte con el destinatario y compruebe que lo haya recibido.

