---
title: 'Configurar el directorio de recogida y el directorio de reproducción: Exchange 2013 Help'
TOCTitle: Configurar el directorio de recogida y el directorio de reproducción
ms:assetid: c9ca7358-9a08-4f57-89d0-910e4438df8a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124549(v=EXCHG.150)
ms:contentKeyID: 49895911
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el directorio de recogida y el directorio de reproducción

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

El servicio de transporte en los servidores de buzón de correo y en los servidores de transporte perimetral utilizan los directorios de recogida y reproducción para insertar archivos de mensajes directamente en la canalización de transporte. Los archivos de mensajes de correo electrónico con el formato correcto que copia al directorio de recogida o de reproducción se envían para su entrega. Los administradores usan el directorio de recogida para probar el flujo de correo y las aplicaciones lo usan para crear y enviar sus propios mensajes. El directorio de reproducción recibe mensajes de servidores de puertas de enlace externas que no son SMTP y reenvía los mensajes que usted exportó desde las colas de servidores de Microsoft Exchange.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada «Servicio de transporte» en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Los directorios de recogida y reproducción utilizan el valor del parámetro *PickupDirectoryMaxMessagesPerMinute* en el cmdlet **Set-TransportService**.

  - Al cambiar la ubicación del directorio de recogida o reproducción no se copia ningún archivo de mensaje existente de la antigua ubicación a la nueva. La nueva ubicación del directorio de recogida o reproducción se activa casi inmediatamente después del cambio de configuración, aunque los archivos de mensajes existentes quedan en la antigua ubicación.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para configurar el directorio de recogida

Para configurar el directorio de recogida, utilice la siguiente sintaxis.

    Set-TransportService <ServerIdentity> -PickupDirectoryPath <LocalFilePath> -PickupDirectoryMaxHeaderSize <Size> -PickupDirectoryMaxRecipientsPerMessage <Integer> -PickupDirectoryMaxMessagesPerMinute <Integer>

Este ejemplo realiza los siguientes cambios en el directorio de recogida en el servidor del buzón de correo, llamado Exchange01:

  - La ubicación del directorio de recogida se establece en el directorio D:\\Pickup.

  - El tamaño máximo permitido para encabezados de mensajes en un archivo de mensaje se aumenta a 96 KB.

  - El número máximo de destinatarios permitido en un archivo de mensaje se aumenta a 250.

  - La tasa máxima de procesamiento de mensajes de los directorios de recogida y de reproducción se incrementó a 200 mensajes por minuto.

<!-- end list -->

    Set-TransportService Exchange01 -PickupDirectoryPath "D:\Pickup Directory" -PickupDirectoryMaxHeaderSize 96KB -PickupDirectoryMaxRecipientsPerMessage 250 -PickupDirectoryMaxMessagesPerMinute 200


> [!NOTE]
> <UL>
> <LI>
> <P>Al establecer el valor del parámetro <EM>PickupDirectoryPath</EM> en <CODE>$null</CODE>, se deshabilita el directorio de recogida.</P>
> <LI>
> <P>El directorio especificado por el parámetro <EM>PickupDirectoryPath</EM> y el parámetro <EM>ReplayDirectoryPath</EM> no puede ser igual.</P></LI></UL>



## Uso del Shell para configurar el directorio de reproducción

Para configurar el directorio de reproducción, utilice la siguiente sintaxis.

    Set-TransportService <ServerIdentity> -ReplayDirectoryPath "C:\Replay Directory" <LocalFilePath> -PickupDirectoryMaxMessagesPerMinute <Integer>

Este ejemplo realiza los siguientes cambios en el directorio de reproducción en el servidor del buzón de correo, llamado Exchange01:

  - La ubicación del directorio de reproducción se establece en el directorio D:\\Replay.

  - La tasa máxima de procesamiento de mensajes de los directorios de recogida y de reproducción se incrementó a 200 mensajes por minuto.

<!-- end list -->

    Set-TransportService Exchange01 -ReplayDirectoryPath "D:\Replay Directory" -PickupDirectoryMaxMessagesPerMinute 200


> [!NOTE]
> <UL>
> <LI>
> <P>Al establecer el valor del parámetro <EM>ReplayDirectoryPath</EM> en <CODE>$null</CODE>, se deshabilita el directorio de reproducción.</P>
> <LI>
> <P>El directorio especificado por el parámetro <EM>PickupDirectoryPath</EM> y el parámetro <EM>ReplayDirectoryPath</EM> no puede ser igual.</P></LI></UL>



## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha configurado correctamente los directorios de recogida o reproducción, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-TransportService <ServerIdentity> | Format-List Pickup*,Replay*

2.  Verifique que los valores mostrados son los valores que ha configurado.

