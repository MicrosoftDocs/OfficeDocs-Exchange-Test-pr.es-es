---
title: 'Exportar mensajes de las colas: Exchange 2013 Help'
TOCTitle: Exportar mensajes de las colas
ms:assetid: 688b342c-f380-4fe0-afce-7e38cf490627
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998625(v=EXCHG.150)
ms:contentKeyID: 51406524
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportar mensajes de las colas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-05-05_

Cuando se exporta un mensaje desde una cola a un archivo, el mensaje no se elimina de la cola. Se copiará el mensaje como archivo de texto sin formato en la ubicación especificada. El archivo que se origina se puede visualizar en una aplicación, como un editor de texto o una aplicación de cliente de correo electrónico, o el archivo de mensaje se puede reenviar por medio del directorio de reproducción en cualquier otro servidor de buzones o de transporte perimetral, tanto dentro como fuera de la organización de Exchange.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Colas" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Los mensajes deben estar en estado de suspensión para que el proceso de exportación se realice correctamente. Puede exportar los mensajes desde las colas de entrega, la cola inaccesible o la cola de mensajes dudosos. Los mensajes de la cola de mensajes dudosos ya se encuentran en estado suspendido. No puede suspender ni exportar mensajes que se encuentren en la cola de envío.

  - No puede utilizar el Visor de cola en Exchange Toolbox para exportar mensajes. Sin embargo, se puede usar el Visor de cola para ubicar, identificar y suspender los mensajes antes de exportarlos mediante el Shell.

  - Compruebe la siguiente información acerca de la ubicación del directorio de destino para los archivos de mensajes:
    
      - El directorio de destino debe existir antes de exportar mensajes. El directorio no se creará para usted. Si no se especifica una ruta de acceso absoluta, se usa el directorio de trabajo actual del Shell de administración de Exchange.
    
      - La ruta puede ser local en el servidor Exchange o puede ser una ruta de acceso de convención de nomenclatura universal (UNC) a un recurso compartido en un servidor remoto.
    
      - La cuenta debe tener permiso de **escritura** en el directorio de destino.
    
      - Al especificar un nombre de archivo para los mensajes exportados, asegúrese de incluir la extensión del nombre de archivo .eml para que las aplicaciones de correo electrónico de cliente puedan abrir los archivos con facilidad o para que el directorio de reproducción los procese correctamente.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para exportar un mensaje específico de una cola en particular

Para exportar un mensaje específico de una cola específica, ejecute el comando siguiente:

    Export-Message -Identity <MessageIdentity> | AssembleMessage -Path <FilePath>\<FileName>.eml

En este ejemplo, se exporta una copia de un mensaje que tiene 1234 como valor de **InternalMessageID** y está ubicado en la cola de entrega de contoso.com, en el servidor Mailbox01 al archivo denominado export.eml en la ruta C:\\Contoso Export.

    Export-Message -Identity Exchange01\Contoso.com\1234 | AssembleMessage -Path "D:\Contoso Export\export.eml"

## Usar el Shell para exportar todos los mensajes de una cola en particular

Para exportar todos los mensajes de una cola específica y usar el valor **InternetMessageID** de cada mensaje como nombre de archivo, utilice la sintaxis siguiente:

    Get-Message -Queue <QueueIdentity> | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

Observe que el valor **InternetMessageID** contiene paréntesis angulares (\> y \<), que deben quitarse porque no están admitidos en los nombres de archivo.

En este ejemplo se exporta una copia de todos los mensajes desde la cola de entrega contoso.com en el servidor denominado Mailbox01 al directorio local denominado D:\\Contoso Export.

    Get-Message -Queue Mailbox01\Contoso.com | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

## Usar el Shell para exportar mensajes específicos de todas las colas de un servidor

Para exportar mensajes determinados de todas las cola en un servidor y usar el valor **InternetMessageID** de cada mensaje como nombre de archivo, utilice la sintaxis siguiente:

    Get-Message -Filter {<MessageFilter>} [-Server <ServerIdentity>] | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

Observe que el valor **InternetMessageID** contiene paréntesis angulares (\> y \<), que deben quitarse porque no están admitidos en los nombres de archivo.

En este ejemplo se exporta una copia de todos los mensajes de remitentes en el dominio contoso.com desde todas las colas en el servidor denominado Mailbox01 al directorio local denominado D:\\Contoso Export.

    Get-Message -Filter {FromAddress -like "*@contoso.com"} -Server Mailbox01 | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}


> [!NOTE]
> Si omite el parámetro <EM>Server</EM>, el comando se ejecuta en el servidor local.


