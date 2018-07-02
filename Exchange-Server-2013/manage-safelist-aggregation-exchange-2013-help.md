---
title: 'Administrar agregación de lista segura: Exchange 2013 Help'
TOCTitle: Administrar agregación de lista segura
ms:assetid: 5ac17168-f411-4cb7-ae98-ebefb865b210
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998280(v=EXCHG.150)
ms:contentKeyID: 49895651
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar agregación de lista segura

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

La *agregación de listas seguras* hace referencia a las funciones que actúan contra correo electrónico no deseado que comparten Microsoft Outlook y Microsoft Exchange Server 2013. Estas funciones recopilan datos de las listas de destinatarios seguros, de remitentes seguros, de remitentes bloqueados y los datos de contacto que configuran los usuarios de Outlook, y los ponen a disposición de los agentes que actúan contra correo electrónico no deseado de Exchange. La agregación de listas seguras puede ayudar a reducir los casos de falsos positivos generados por el filtrado contra correo no deseado que realizan los servidores Exchange en los que se ejecutan los agentes contra correo no deseado.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md) y la sección "Características contra correo no deseado" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - De manera predeterminada, las características contra correo no deseado no están habilitadas en el Servicio de transporte en un servidor de buzones. Por lo general, solo se habilitan las características contra correo no deseado si la organización de Exchange no realiza un filtrado previo contra correo no deseado antes de aceptar mensajes entrantes. Para obtener más información, consulte [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Tenga en cuenta el tráfico de la red y de replicación que se puede generar cuando ejecute el cmdlet **Update-SafeList**. Si ejecuta el comando en varios buzones en los que se hace un uso muy profuso de las listas seguras, es posible que se genere una cantidad significativa de tráfico. Si ejecuta el comando en varios buzones, se recomienda que ejecute el comando durante el horario no comercial y de poca actividad.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para configurar los límites de recopilación de listas seguras de buzones

Puede configurar el número máximo de remitentes seguros y de remitentes bloqueados que un usuario puede configurar. De forma predeterminada, los usuarios pueden configurar hasta 5000 remitentes seguros y 500 remitentes bloqueados.

Para configurar el número máximo de remitentes seguros y de remitentes bloqueados, ejecute el siguiente comando:

    Set-Mailbox <MailboxIdentity> -MaxSafeSenders <Integer> -MaxBlockedSenders <Integer>

En este ejemplo, se configura el buzón de juancarlos@contoso.com para que tenga un máximo de 2000 remitentes seguros y 200 remitentes bloqueados.

    Set-Mailbox john@contoso.com -MaxSafeSenders 2000 -MaxBlockedSenders 200

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que los límites de recopilación de listas seguras de buzones se configuraron correctamente, siga estos pasos:

1.  Ejecute el siguiente comando:
    
        Get-Mailbox <Identity> | Format-List Name,Max*Senders

2.  Compruebe que los valores mostrados coincidan con los valores que ha configurado.

## Usar el Shell para ejecutar el comando Update-Safelist

En Exchange 2013, la agregación de listas seguras se realiza de forma automática, por lo que no es necesario programar ni ejecutar manualmente el cmdlet **Update-Safelist**. No obstante, puede que desee ejecutar este cmdlet de manera ocasional para probar la agregación de listas seguras.

En este ejemplo, se escribe la lista de remitentes seguros para el buzón de john@contoso.com en Active Directory.

    Update-Safelist john@contoso.com -Type SafeSenders

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Update-SafeList](https://technet.microsoft.com/es-es/library/bb125034\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la agregación de listas seguras se configuró correctamente, siga estos pasos:

## Paso 1: usar el Shell para comprobar que el agente de filtrado de contenido está habilitado en el servidor Exchange

1.  Ejecute el siguiente comando:
    
        Get-ContentFilterConfig | Format-List Enabled

2.  Si el resultado muestra que el parámetro *Enabled* es `True`, el filtrado de contenido está habilitado. Si no lo está, ejecute el siguiente comando para habilitar el filtrado de contenido y el agente de filtrado de contenido en el servidor Exchange:
    
        Set-ContentFilterConfig -Enabled $true

## Paso 2: usar el editor ADSI para comprobar la replicación de los datos de agregación de listas seguras en los servidores de transporte perimetral (opcional)

Este paso solo es necesario si ejecuta el agente de filtrado de contenido en un servidor de transporte perimetral de su red perimetral.

Puede ver los objetos de usuario en la instancia de Active Lightweight Directory Services (AD LDS) del servidor de transporte perimetral para comprobar que la recopilación de datos de listas seguras está actualizada para los objetos de usuario y que el servicio Microsoft Exchange EdgeSync replicó los datos en la instancia de AD LDS.

Hay tres atributos de recopilación de lista segura para cada objeto de usuario:

  - **msExchSafeRecipientsHash**   Este atributo almacena el hash de la recopilación de la lista de destinatarios seguros del usuario.

  - **msExchSafeSendersHash**    Este atributo almacena el hash de la recopilación de la lista de remitentes seguros del usuario.

  - **msExchBlockedSendersHash**   Este atributo almacena para el usuario el hash de la recopilación de la lista de remitentes bloqueados.

Si hay una cadena hexadecimal, como `0xac 0xbd 0x03 0xca`, en el atributo, el objeto de usuario ha sido actualizado. Si el atributo tiene un valor de `<Not Set>`, el atributo no se actualizó.

Puede buscar y visualizar los atributos con el complemento Editor AD LDS (Active Directory Service Interfaces, ADSI).

## Paso 3: enviar un mensaje de prueba para comprobar que la agregación de listas seguras funciona

Para probar si la agregación de listas seguras funciona, envíese un mensaje a sí mismo desde un remitente seguro que, de lo contrario, el filtrado de contenido bloquearía. Si la agregación de listas seguras funciona, el mensaje debería llegar a su bandeja de entrada.

1.  Busque una cuenta de correo electrónico externa existente que pueda usar, o bien cree una cuenta de correo en un proveedor de correo electrónico gratuito basado en web como Microsoft Hotmail.

2.  Agregue esa cuenta a la lista de remitentes seguros en Microsoft Outlook.

3.  Use el cmdlet **Update-SafeList** para copiar la recopilación de listas seguras de ese buzón a Active Directory.

4.  Opcional: si ejecuta el agente de filtrado de contenido en un servidor de transporte perimetral en la red perimetral, ejecute el cmdlet **Start-EdgeSynchronization** para forzar la replicación de EdgeSync.

5.  Agregue una palabra específica como frase bloqueada a la configuración de filtrado de contenido. Para conocer los pasos detallados, consulte [Administrar el filtrado de contenido](manage-content-filtering-exchange-2013-help.md).

6.  Desde la cuenta de correo electrónico externa que creó en el paso 1, envíe un mensaje al buzón de Exchange que incluya la frase bloqueada que configuró en el paso 5.
    
    Si el mensaje se entrega correctamente a su buzón, significa que la agregación de listas seguras funciona correctamente.

