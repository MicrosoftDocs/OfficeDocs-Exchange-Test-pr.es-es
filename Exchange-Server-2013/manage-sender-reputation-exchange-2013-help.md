---
title: 'Administrar la reputación del remitente: Exchange 2013 Help'
TOCTitle: Administrar la reputación del remitente
ms:assetid: f2716bd9-e3ac-46d9-9264-4e3dabfa0f38
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125186(v=EXCHG.150)
ms:contentKeyID: 49896009
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar la reputación del remitente

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

La reputación del remitente es proporcionada por el agente de análisis del protocolo. La reputación del remitente bloquea los mensajes según diversas características del remitente. La reputación del remitente depende de datos que se conserven de él para decidir la acción que efectuar con el mensaje entrante, si se debe realizar alguna.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones contra el correo no deseado" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - De manera predeterminada, las características contra correo no deseado no están habilitadas en el Servicio de transporte en un servidor de buzones. Por lo general, solo se habilitan las características contra correo no deseado si la organización de Exchange no realiza un filtrado previo contra correo no deseado antes de aceptar mensajes entrantes. Para obtener más información, consulte [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - El agente de análisis de protocolo es el agente subyacente que se encarga de la función de reputación del remitente. Al deshabilitar la reputación del remitente, el agente de análisis del protocolo aún está habilitado.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para habilitar o deshabilitar la reputación del remitente

En este ejemplo, se deshabilita la reputación del remitente.

    Set-SenderReputationConfig -Enabled $false

En este ejemplo, se habilita la reputación del remitente.

    Set-SenderReputationConfig -Enabled $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la reputación del remitente se habilitó o deshabilitó correctamente, realice lo siguiente:

1.  Ejecute el siguiente comando para comprobar que el agente de análisis del protocolo esté instalado y habilitado:
    
        Get-TransportAgent

2.  Ejecute el siguiente comando para comprobar los valores de reputación del remitente configurados:
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

## Usar el Shell para habilitar o deshabilitar la reputación del remitente para mensajes internos o externos

De manera predeterminada, la reputación del remitente está habilitada para mensajes externos y deshabilitada para mensajes internos. Un mensaje se considera externo si proviene de una conexión no autenticada que es externa para la organización de Exchange. Un mensaje se considera interno si proviene de una conexión autenticada y si el dominio del remitente está configurado como un dominio autorizado en la organización de Exchange.

Para deshabilitar la reputación del remitente en los mensajes externos, ejecute el siguiente comando:

    Set-SenderReputationConfig -ExternalMailEnabled $false

Para habilitar la reputación del remitente en los mensajes externos, ejecute el siguiente comando:

    Set-SenderReputationConfig -ExternalMailEnabled $true

Para deshabilitar la reputación del remitente en los mensajes internos, ejecute el siguiente comando:

    Set-SenderReputationConfig -InternalMailEnabled $false

Para habilitar la reputación del remitente en los mensajes internos, ejecute el siguiente comando:

    Set-SenderReputationConfig -InternalMailEnabled $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la reputación del remitente se habilitó o deshabilitó correctamente para mensajes internos y externos, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

2.  Verifique que los valores mostrados coincidan con los valores que ha configurado.

## Usar el Shell para configurar las propiedades de reputación del remitente

Para configurar las propiedades de reputación del remitente, ejecute el siguiente comando:

    Set-SenderReputationConfig -SrlBlockThreshold <Value> -SenderBlockingPeriod <Hours>

En este ejemplo, se establece en 6 el umbral de bloqueo del nivel de reputación del remitente (SRL) y se configura la reputación del remitente para agregar remitentes ofensivos a la lista de direcciones IP bloqueadas durante 36 horas:

    Set-SenderReputationConfig -SrlBlockThreshold 6 -SenderBlockingPeriod 36

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que las propiedades de reputación del remitente se configuraron correctamente, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderReputationConfig

2.  Verifique que los valores mostrados coincidan con los valores que ha configurado.

## Usar el Shell para configurar el acceso saliente para la detección de servidores proxy abiertos

Posiblemente deba seguir pasos adicionales para permitir que la reputación del remitente atraviese firewalls entre Internet y el servidor de Exchange que ejecuta el agente de análisis del protocolo. En la tabla siguiente, se enumeran los puertos salientes necesarios para la reputación del remitente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocolos</th>
<th>Puertos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SOCKS4, SOCKS5</p></td>
<td><p>1081, 1080</p></td>
</tr>
<tr class="even">
<td><p>Wingate, Telnet, Cisco</p></td>
<td><p>23</p></td>
</tr>
<tr class="odd">
<td><p>HTTP CONNECT, HTTP POST</p></td>
<td><p>6588, 3128, 80</p></td>
</tr>
</tbody>
</table>


Para configurar el acceso saliente para la detección de servidores proxy abiertos, ejecute el siguiente comando:

    Set-SenderReputationConfig -ProxyServerName <String> -ProxyServerPort <Port> -ProxyServerType <String>

En este ejemplo, se configura la reputación del remitente para usar el servidor proxy abierto denominado SERVER01 que utiliza el protocolo HTTP CONNECT en el puerto 80.

    Set-SenderReputationConfig - ProxyServerName SERVER01 -ProxyServerPort 80 -ProxyServerType HttpConnect

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el acceso saliente se configuró correctamente para la detección de servidores proxy abiertos, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderReputationConfig | Format-List ProxyServer*

2.  Verifique que los valores mostrados son los valores que ha configurado.

