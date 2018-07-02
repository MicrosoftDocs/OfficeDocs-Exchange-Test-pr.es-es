---
title: 'Configurar las sugerencias de correo electrónico personalizadas para los destinatarios: Exchange 2013 Help'
TOCTitle: Configurar las sugerencias de correo electrónico personalizadas para los destinatarios
ms:assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638199(v=EXCHG.150)
ms:contentKeyID: 52061890
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar las sugerencias de correo electrónico personalizadas para los destinatarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-06-01_

Las *sugerencias de correo electrónico* son mensajes informativos que se muestran a los usuarios en la barra de información de Outlook Web App y Microsoft Outlook 2010 o posterior cuando un usuario hace cualquiera de las operaciones siguientes mientras crea un mensaje de correo electrónico:

  - Agregar un destinatario

  - Agregar datos adjuntos

  - Responder o Responder a todos

  - Abrir un mensaje, que ya se ha dirigido a los destinatarios, de la carpeta Borradores

Además de las sugerencias de correo electrónico integradas que están disponibles, puede crear sugerencias de correo electrónico personalizadas para todos los tipos de destinatarios. Para más información sobre las sugerencias de correo electrónico integradas, vea [MailTips](mailtips-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Información sobre correo" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Puede configurar la sugerencia de correo electrónico principal en el Centro de administración de Exchange (EAC) o en el Shell. Sin embargo, solo puede configurar traducciones de sugerencias de correo electrónico adicionales en el Shell.

  - Cuando se agrega una sugerencia de correo electrónico a un destinatario, ocurren dos cosas:
    
      - Se agregan etiquetas HTML al texto automáticamente. Por ejemplo, si escribe el texto: `This mailbox is not monitored`, la sugerencia de correo electrónico se convierte automáticamente en: `<html><body>This mailbox is not monitored</body></html>`. No se admiten las etiquetas HTML adicionales en la información sobre correo.
    
      - El texto se agrega automáticamente a la propiedad *MailTipTranslations* del destinatario como valor predeterminado. Si modifica el texto de la sugerencia de correo electrónico, el valor predeterminado se actualiza automáticamente en la propiedad *MailTipTranslations*.

  - La longitud de la información de una sugerencia de correo electrónico no puede superar los 175 caracteres mostrados.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Configurar sugerencias de correo electrónico para los destinatarios

## Uso del EAC para configurar las sugerencias de correo electrónico para los destinatarios

1.  En la EAC, vaya a **Destinatarios** .

2.  Seleccione cualquiera de las siguientes pestañas de destinatarios según el tipo de destinatario:
    
      - **Buzones**
    
      - **Grupos**
    
      - **Recursos**
    
      - **Contactos**
    
      - **Compartido**

3.  En la pestaña destinatarios, seleccione el destinatario que quiere modificar y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  En la página de propiedades del destinatario que aparece, haga clic en **Sugerencias de correo electrónico**.

5.  Escriba el texto para la sugerencia de correo electrónico. Cuando haya terminado, haga clic en **Guardar**.

## Uso del Shell para configurar las sugerencias de correo electrónico para los destinatarios

Para configurar una sugerencia de correo electrónico para un destinatario, use la siguiente sintaxis.

    Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"

*\<RecipientType\>* puede ser cualquier tipo de destinatario. Por ejemplo, `Mailbox`, `MailUser`, `MailContact`, `DistributionGroup` o `DynamicDistributionGroup`.

Por ejemplo, suponga que tiene un buzón de correo denominado "Help Desk" para que los usuarios envíen solicitudes de soporte y que el tiempo de respuesta prometido es de dos horas. Para configurar una sugerencia de correo electrónico personalizada que lo explique, ejecute el comando siguiente:

    Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."

## Uso del Shell para configurar sugerencias de correo electrónico adicionales en diferentes idiomas

Para configurar traducciones de sugerencias de correo electrónico adicionales sin afectar al texto de la sugerencia de correo electrónico existente u otras traducciones de sugerencias de correo electrónico existentes, use la siguiente sintaxis:

    Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}

*\<culture\>* es un código de referencia cultural ISO 639 válido de dos letras correspondiente al idioma.

Por ejemplo, supongamos que el buzón de correo denominado Notificaciones actualmente tiene la sugerencia de correo electrónico: "This mailbox is not monitored". Para agregar la traducción al español, ejecute el siguiente comando:

    Set-Mailbox -MailTipTranslations @{Add="ES:Esta caja no se supervisa."}

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se configuró correctamente una sugerencia de correo electrónico para un destinatario, siga estos pasos:

1.  En Outlook Web App o Outlook 2010 o posterior, escriba un mensaje de correo electrónico dirigido al destinatario, pero no lo envíe.

2.  Compruebe que la sugerencia de correo electrónico aparezca en la barra de información.

3.  Si ha configurado traducciones de información sobre correo adicional, para comprobar los resultados, redacte el mensaje en Outlook Web App donde la configuración de idioma coincida con el idioma de esta traducción.

