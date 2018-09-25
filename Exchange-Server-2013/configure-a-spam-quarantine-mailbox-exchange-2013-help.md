---
title: 'Configurar un buzón de cuarentena de correo no deseado: Exchange 2013 Help'
TOCTitle: Configurar un buzón de cuarentena de correo no deseado
ms:assetid: 907d2f90-2a62-4d59-a4cf-945fef2e963f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123746(v=EXCHG.150)
ms:contentKeyID: 49895777
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar un buzón de cuarentena de correo no deseado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-19_

Los mensajes que el agente de filtro de contenidos determina como correo no deseado se pueden dirigir a un buzón en cuarentena de correo no deseado. Si el umbral de cuarentena del nivel de confianza de correo no deseado (SCL) está habilitado, todos los mensajes en cuarentena se ajustan como informes de no entrega (NDR) y se envían a la dirección SMTP especificada como buzón de cuarentena de correo no deseado. Podrá revisar los mensajes en cuarentena y entregarlos a los destinatarios deseados mediante la característica Volver a enviar de Microsoft Outlook.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea:  45 minutos.

  - De manera predeterminada, las características contra correo no deseado no están habilitadas en el Servicio de transporte en un servidor de buzones. Por lo general, solo se habilitan las características contra correo no deseado si la organización de Exchange no realiza un filtrado previo contra correo no deseado antes de aceptar mensajes entrantes. Para obtener más información, consulte [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - La persona a cargo del buzón de cuarentena de correo electrónico no deseado puede ver mensajes que pueden ser privados y confidenciales y, a continuación, enviar correo en nombre de cualquier persona dentro de la organización de.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Comprobar que el filtrado de contenido está habilitado

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones contra el correo no deseado" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

1.  Ejecute el comando siguiente para comprobar que el agente de filtro de contenido está instalado y habilitado en el servidor de Exchange:
    
    ```powershell
    Get-TransportAgent "Content Filter Agent"
    ```

2.  Ejecute el comando siguiente para verificar que el filtrado de contenido está habilitado:
    
    ```powershell
    Get-ContentFilterConfig | Format-List Enabled
    ```

Para obtener más información, consulte [Administrar el filtrado de contenido](manage-content-filtering-exchange-2013-help.md).

## Paso 2: Crear un buzón dedicado para la cuarentena de correo no deseado

Para crear un buzón dedicado de cuarentena de correo no deseado, siga estos pasos:

  - **Crear una base de datos de Exchange dedicada**   Es recomendable crear una base de datos dedicada para el buzón de cuarentena de correo no deseado. El buzón de cuarentena de correo no deseado debe tener una base de datos muy grande, dado que si se alcanza el límite de la cuota de almacenamiento, se perderán los mensajes. Para obtener más información, consulte [Administrar bases de datos de buzones en Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

  - **Crear un buzón dedicado y una cuenta de usuario**   Se recomienda que cree un buzón dedicado y una cuenta de usuario de Active Directory para el buzón de cuarentena de correo no deseado. Para obtener más información, consulte [Crear buzones de usuario](create-user-mailboxes-exchange-2013-help.md).
    
    Es posible aplicar distintas directivas de destinatarios, como la administración de los registros de mensajería, la cuotas de buzones y los derechos de delegación, en función de las necesidades y directivas de cumplimiento de la organización. Para obtener más información, consulte [Administración de registros de mensajes](https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/messaging-records-management).
    

    > [!NOTE]  
    > Si un mensaje de cuarentena se rechaza debido a una cuota de almacenamiento, el mensaje se perderá. Exchange no genera NDR para los mensajes de cuarentena porque éstos se empaquetan como NDR.



  - **Configurar Outlook**   Debe configurar los permisos de acceso delegado de Outlook para que cumplan las necesidades de la organización. Además, se recomienda configurar el perfil de Outlook para mostrar el `Sender[#0x0069001E]` original, `Recipient[#0x0E04001E]`, y los campos `Bcc[#0x0E02001E]` en la vista **Mensaje**. Para obtener más información, consulte [Recuperar mensajes en cuarentena del buzón de cuarentena de correo no deseado](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

## Paso 3: Especificar el buzón de cuarentena de correo no deseado

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones contra el correo no deseado" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

Ejecute el siguiente comando:

```powershell
Set-ContentFilterConfig -QuarantineMailbox <SmtpAddress>
```

En este ejemplo, todos los mensajes que superen el umbral de cuarentena de correo no deseado se envían a spamQ@contoso.com.

```powershell
Set-ContentFilterConfig -QuarantineMailbox spamQ@contoso.com
```

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que ha especificado correctamente el buzón de cuarentena de correo no deseado, siga estos pasos:

1.  Ejecute el siguiente comando:
    
    ```powershell
    Get-ContentFilterConfig | Format-List QuarantineMailbox
    ```

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Paso 4: Configurar el umbral de cuarentena de SCL

El umbral de cuarentena del nivel de confianza de correo no deseado (SCL) es el valor al que un determinado mensaje que se ha identificado como correo no deseado potencial se entrega al buzón de cuarentena de correo no deseado. El umbral de cuarentena de SCL se puede establecer en un valor entre 0 y 9, donde 0 es baja probabilidad de que sea correo no deseado y 9 es alta probabilidad de que lo sea.

Para obtener más información acerca de cómo ajustar los umbrales de correo no deseado de modo que se adapten a las necesidades de cada organización y cómo ajustar los umbrales de correo no deseado por destinatario, consulte [Administrar el filtrado de contenido](manage-content-filtering-exchange-2013-help.md) .

## Paso 5: Administrar el buzón de cuarentena de correo no deseado

Al administrar el buzón de cuarentena de correo no deseado, siga las indicaciones siguientes:

  - Libere los elementos enviados al buzón de cuarentena de correo no deseado mediante la característica Enviar de nuevo de Outlook para volver a enviar el mensaje original.
    
    Para obtener más información, consulte [Recuperar mensajes en cuarentena del buzón de cuarentena de correo no deseado](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md).

  - Supervise el buzón de cuarentena de correo no deseado para que el tamaño del mismo permanezca en un intervalo aceptable. El volumen de los mensajes de correo electrónico puede variar debido a un conjunto de destinatarios más grande, la tendencia natural de los mensajes más grandes, o el umbral de la acción de cuarentena del nivel de confianza de correo no deseado.

  - Supervise el buzón de cuarentena de correo no deseado para identificar falsos positivos. Si el buzón de cuarentena de correo no deseado contiene muchos falsos positivos, ajuste el umbral de cuarentena de SCL. Para obtener más información acerca de cómo determinar por qué los falsos positivos se entregan al buzón de cuarentena de correo no deseado, consulte[Marcas de correo no deseado](anti-spam-stamps-exchange-2013-help.md) .

  - Utilice el mismo perfil de Outlook para recuperar mensajes en cuarentena del buzón de cuarentena del correo no deseado. No se permite aplicar permisos a otro perfil de Outlook para recuperar mensajes. No se puede usar un perfil de Outlook diferente para recuperar o liberar mensajes del buzón de cuarentena del correo no deseado.


> [!IMPORTANT]  
> Los NDR identificados como correo no deseado se eliminan, incluso si la clasificación del nivel de confianza de correo no deseado indica que deben ser puestos en cuarentena. Los NDR no se entregan al buzón de cuarentena de correo no deseado. Para realizar un seguimiento de esos mensajes, use el registro de agente o el registro de seguimiento de mensajes. Para obtener más información, consulte <A href="anti-spam-agent-logging-exchange-2013-help.md">Registro de agente contra correo no deseado</A>.

## Paso 6: Ajustar el umbral de cuarentena de SCL

Tras configurar el umbral de cuarentena del nivel de confianza de correo no deseado, supervise periódicamente la configuración y ajústela dependiendo de las necesidades de la organización. Por ejemplo, si se filtran demasiados falsos positivos al buzón de cuarentena de correo no deseado, eleve el umbral de cuarentena del nivel de confianza de correo no deseado a un número mayor. Para obtener más información acerca de cómo ajustar umbral de cuarentena del nivel de confianza de correo no deseado, consulte[Umbral de nivel de confianza de correo no deseado](spam-confidence-level-threshold-exchange-2013-help.md) .