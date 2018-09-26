---
title: 'Crear un conector externo para entregar los mensajes a una puerta de enlace no SMTP fax: Exchange 2013 Help'
TOCTitle: Crear un conector externo para entregar los mensajes a una puerta de enlace no SMTP fax
ms:assetid: 589db487-3c4c-409a-92e3-c78dd8f639b6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ710163(v=EXCHG.150)
ms:contentKeyID: 49895644
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear un conector externo para entregar los mensajes a una puerta de enlace no SMTP fax

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-17_

Pueden ocurrir situaciones en las que desee enviar y recibir mensajes desde un servidor de puerta de enlace de fax que no use SMTP como mecanismo principal de transporte. Siga los pasos descritos en este procedimiento para crear un conector externo que entregue y reciba mensajes del sistema externo.


> [!TIP]
> En la mayoría de los casos en que debe entregar mensajes salientes a un sistema que no es SMTP, recomendamos los conectores de agente de entrega porque permiten la administración de colas de mensajes. Además, los mensajes no tienen que escribirse en el sistema de archivos, entre otros beneficios. En el tema <A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">Agentes de entrega y conectores de agentes de entrega</A> se ofrece más información.



¿Le interesa ver escenarios donde se utiliza este procedimiento? Consulte los siguientes temas:

  - [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 30 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Conectores externos" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: usar el Shell para crear un conector externo que envíe mensajes a un servidor de puerta de enlace que no use SMTP

1.  Ejecute el siguiente comando para crear el conector externo:
    
    ```powershell
    New-ForeignConnector -Name "Contoso Foreign Connector" -AddressSpaces "X400:c=US;a=Fabrikam;P=Contoso;5" -SourceTransportServers Hub01,Hub02
    ```
    
    En este ejemplo, Hub01 y Hub02 son servidores de origen de una organización que se designan para entregar mensajes al sistema externo. Cuando se usa más de un servidor de origen, se consigue la tolerancia a errores.

Después de crear el conector externo, configure los directorios de recogida, de entrega y de reproducción, en función de las necesidades de la organización.

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que el conector externo se creó correctamente, ejecute el siguiente comando:

```powershell
Get-ForeignConnector | Format-List Name
```

Compruebe que aparece el nombre del conector externo que ha creado.

## Paso 2: usar el Shell para configurar el directorio de entrega para un servidor de buzones que ejecute el servicio de transporte

El directorio de entrega de un servidor de buzones que ejecute el servicio de transporte sirve para entregar mensajes salientes del conector externo.

Puede crear un directorio para usarlo como directorio de entrega en su sistema local de archivos. También puede utilizar un directorio en un recurso compartido de archivos de red.

1.  Ejecute el siguiente comando para especificar el directorio de entrega del conector externo (cambie el valor del parámetro *DropDirectory* a una ruta de acceso adecuada para su entorno):
    
    ```powershell
    Set-ForeignConnector "Contoso Foreign Connector" -DropDirectory "C:\Drop Directory"
    ```

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que el directorio de entrega se estableció correctamente, ejecute el siguiente script de cmdlet y compruebe el valor del parámetro *DropDirectory*:

```powershell
Get-ForeignConnector "Contoso Foreign Connector" | Format-List
```

Después de crear el conector externo y especificar el directorio de entrega, envíe un mensaje a través del servidor de buzones en el que creó el conector externo y compruebe que se entrega un archivo al directorio de entrega.

## Paso 3: usar el Shell para configurar el directorio de recogida para el servicio de transporte de un servidor de buzones

El directorio de recogida del servicio de transporte de un servidor de buzones sirve para recopilar los mensajes generados por sistemas que no usan SMTP. Utilice este procedimiento cuando desee recopilar mensajes nuevos generados por un sistema que no use SMTP, como un servidor de puerta de enlace de fax, mediante la transferencia de archivos.

Para obtener instrucciones detalladas sobre cómo configurar un directorio de recogida, vea [Configurar el directorio de recogida y el directorio de reproducción](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que el directorio de recogida se estableció correctamente, ejecute el siguiente comando y compruebe el valor del parámetro *PickupDirectoryPath*:

```powershell
Get-TransportService | Format-List PickupDirectoryPath
```

## Paso 4: usar el Shell para configurar el directorio de reproducción para el servicio de transporte de un servidor de buzones

El directorio de reproducción del servicio de transporte de un servidor de buzones sirve para recopilar los mensajes generados por sistemas que no usan SMTP. Utilice este procedimiento para configurar el directorio de reproducción cuando desee volver a enviar los mensajes de correo electrónico, generalmente desde un servidor de puerta de enlace externo que no use SMTP, que se generaron en el entorno de Exchange y se exportaron del transporte de Exchange.

Para obtener instrucciones detalladas sobre cómo configurar un directorio de recogida, vea [Configurar el directorio de recogida y el directorio de reproducción](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que el directorio de reproducción se estableció correctamente, ejecute el siguiente comando y compruebe el valor del parámetro *ReplayDirectoryPath*:

```powershell
Get-TransportService | Format-List ReplayDirectoryPath
```

## Más información

[Conectores externos](foreign-connectors-exchange-2013-help.md)

[Agentes de entrega y conectores de agentes de entrega](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

