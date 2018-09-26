---
title: 'Buscar en registros seguimiento de mensajes: Exchange 2013 Help'
TOCTitle: Buscar en registros seguimiento de mensajes
ms:assetid: e1678327-bcd5-42d4-a363-67f33067fe9a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124926(v=EXCHG.150)
ms:contentKeyID: 51406564
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Buscar en registros seguimiento de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-25_

En Microsoft Exchange Server 2013, el registro de seguimiento de mensajes es un registro detallado de toda la actividad de mensajes cuando los mensajes se transfieren desde el servicio de transporte y hacia él, en los servidores de buzones de correo, buzones de correo en los servidores de buzones de correo y en los servidores de transporte perimetral.

Puede usar el cmdlet **Get-MessageTrackingLog** en el Shell de administración de Exchange para buscar entradas en el registro de seguimiento de mensajes mediante criterios de búsqueda específicos.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 30 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Seguimiento de mensajes" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Para realizar una búsqueda en los registros de seguimiento de mensajes el servicio de búsqueda del registro de transporte de Microsoft Exchange debe estar en ejecución. Si deshabilita o detiene este servicio, no se puede realizar ninguna búsqueda en los registros de seguimiento de mensajes ni ejecutar informes de entrega. Sin embargo, la detención de este servicio no afecta a otras características de Exchange.

  - Los nombres de campo que se muestran en los resultados del cmdlet **Get-MessageTrackingLog** son similares a los nombres de campo reales usados en los registros de seguimiento de mensajes. Las diferencias más destacables son:
    
      - Los guiones se eliminan de los nombres de campo. Por ejemplo, **internal-message-id** se muestra como `InternalMessageId`.
    
      - El campo **date-time** se muestra como `Timestamp`.
    
      - El campo **recipient-address** aparece como `Recipients`.
    
      - El campo **sender-address** aparece como `Sender`.

  - El campo **date-time** del registro de seguimiento de mensajes almacena la información con el formato de hora universal coordinada (UTC). Sin embargo, los criterios de búsqueda de fecha y hora se deben especificar en los parámetros *Start* o *End* en el formato de fecha y hora regional del equipo que se use para realizar la búsqueda.

  - No puede copiar archivos del registro de seguimiento de mensajes de otro servidor de Exchange y luego buscarlos mediante el cmdlet **Get-MessageTrackingLog**. Además, si guarda manualmente un archivo de registro de seguimiento de mensajes existente, el cambio en la marca de fecha y hora del archivo rompe la lógica de la consulta que Exchange usa para buscar los registros de seguimiento de mensajes.

  - El cmdlet Exchange 2013**Get-MessageTrackingLog** puede buscar los registros de seguimiento de mensajes en los servidores de Exchange 2007 y Exchange 2010 en el mismo sitio de Active Directory.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para buscar los registros de seguimiento de mensajes

Para buscar eventos concretos en las entradas del registro de seguimiento de mensajes, use la siguiente sintaxis.

```powershell
Get-MessageTrackingLog [-Server <ServerIdentity.] [-ResultSize <Integer> | Unlimited] [-Start <DateTime>] [-End <DateTime>] [-EventId <EventId>] [-InternalMessageId <InternalMessageId>] [-MessageId <MessageId>] [-MessageSubject <Subject>] [-Recipients <RecipientAddress1,RecipientAddress2...>] [-Reference <Reference>] [-Sender <SenderAddress>]
```

Para ver las 1 000 entradas más recientes del registro de seguimiento de mensajes en el servidor, ejecute el siguiente comando:

```powershell
Get-MessageTrackingLog
```

En este ejemplo se buscan registros de seguimiento de mensajes en el servidor local de todas las entradas del 3/28/2013 8:00 a. m. al 3/28/2013 5:00 p. m. de todos los eventos **FAIL** con el remitente del mensaje pat@contoso.com.

```powershell
Get-MessageTrackingLog -ResultSize Unlimited -Start "3/28/2013 8:00AM" -End "3/28/2013 5:00PM" -EventId "Fail" -Sender "pat@contoso.com"
```

## Uso del Shell para controlar la salida de una búsqueda del registro de seguimiento de mensajes

Use la siguiente sintaxis.

```powershell
Get-MessageTrackingLog <SearchFilters> | <Format-Table | Format-List> [<FieldNames>] [<OutputFileOptions>]
```

En este ejemplo se buscan los registros de seguimiento de mensajes con los siguientes criterios:

  - Devolver resultados de los primeros 1 000 eventos **Send**.

  - Mostrar los resultados en el formato de lista.

  - Mostrar solo los nombres de campo que empiezan por `Send` o `Recipient`.

  - Escribir la salida en un nuevo archivo denominado `D:\Send Search.txt`

<!-- end list -->

```powershell
Get-MessageTrackingLog -EventId Send | Format-List Send*,Recipient* > "D:\Send Search.txt"
```

## Uso del Shell para buscar registros de seguimiento de mensajes de las entradas de mensajes en varios servidores

Normalmente, el valor en el campo de encabezado **MessageID:**  permanece constante a medida que el mensaje recorre la organización de Exchange. Esta propiedad se denomina **InternetMessageId** en las utilidades de vista de la cola y **MessageId** en las utilidades de vista del registro de seguimiento de mensajes. Una vez determinado el valor `MessageID:` de un mensaje específico, puede buscar información sobre dicho mensaje en los registros de seguimiento de mensajes en todos los servidores de buzones de correo de la organización de Exchange.

Para buscar todas las entradas del registro de seguimiento de mensajes de un mensaje concreto en todos los servidores de buzones de correo, use la siguiente sintaxis.

```powershell
Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId <MessageID> | Select-Object <CommaSeparatedFieldNames> | Sort-Object -Property <FieldName>
```

En este ejemplo se buscan los registros de seguimiento de mensajes en todos los servidores de buzones de correo de Exchange 2013 con los siguientes criterios:

  - Buscar todas las entradas relacionadas con un mensaje que tenga un valor de **MessageID:**  de `<ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com>`. Tenga en cuenta que puede omitir los caracteres de paréntesis angulares (`<``>`). Si no lo hace, deberá incluir todo el valor de **MessageID:**  entre comillas.

  - Para cada entrada, muestre los campos **date-time**, **server-hostname**, **client-hostname**, **source**, **event-id** y **recipient-address**.

  - Ordenar los resultados por el campo **date-time**.

<!-- end list -->

```powershell
Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com | Select-Object Timestamp,ServerHostname,ClientHostname,Source,EventId,Recipients | Sort-Object -Property Timestamp
```

## Uso de EAC para buscar los registros de seguimiento de mensajes

Puede usar la característica Informes de entrega para administradores en el Centro de administración de Exchange (EAC) para buscar en los registros de seguimiento de mensajes información acerca de los mensajes enviados o recibidos por un buzón de correo específico de la organización. Para obtener más información, vea [Seguimiento de mensajes con informes de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).

