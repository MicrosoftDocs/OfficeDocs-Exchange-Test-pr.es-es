---
title: 'Habilitar funcionalidad contra spam servidor Buzón correo: Exchange 2013 Help'
TOCTitle: Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo
ms:assetid: 59d22c5e-64bc-4879-8ad1-364862b6ba11
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201691(v=EXCHG.150)
ms:contentKeyID: 49116240
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-01-23_

Microsoft Exchange Server 2013 incluye los siguientes agentes contra correo no deseado en el servicio de transporte de los servidores de buzones, aunque no están instalados de manera predeterminada:

  - Agente de filtro de contenido

  - Agente de Id. de remitente

  - Agente de filtro de remitentes

  - Agente de filtro de destinatarios

  - Agente de análisis de protocolo para la reputación del remitente

No obstante, puede instalar estos agentes contra correo no deseado en un servidor de buzones mediante un script en el Shell de administración de Exchange. En general, los agentes contra correo no deseado se instalan en un servidor de buzones solo si la organización acepta todo el correo entrante sin ningún tipo de filtrado previo contra correo no deseado.

¿Qué ocurre si se instalan los agentes contra correo no deseado disponibles en el servicio de transporte de un servidor de buzones, pero también hay otros agentes contra correo no deseado de Exchange que actúan en los mensajes antes de que lleguen al servidor de buzones? Por ejemplo, ¿qué ocurriría si hay un servidor de transporte perimetral de Microsoft Exchange 2007 o Exchange 2010 en la red perimetral que entrega el correo entrante directamente al servicio de transporte del servidor de buzones? Los agentes contra correo no deseado del servidor de buzones reconocen los valores de encabezado X contra correo no deseado que otros agentes de Exchange agregan a los mensajes, y los mensajes que contienen estos encabezados X pasan sin que se vuelvan a analizar. No obstante, las búsquedas de destinatarios que realiza el agente de filtrado de destinatarios se volverán a realizar en el servidor de buzones.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de transporte" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - El agente de filtrado de conexiones y el agente de filtrado de datos adjuntos no están disponibles en los servidores de buzones. Solo están disponibles en los servidores de transporte perimetral. Sin embargo, el agente de malware se instala y se habilita de forma predeterminada en un servidor de buzones. Para obtener más información, consulte [Protección antimalware](anti-malware-protection-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: usar el Shell para ejecutar el script Install-AntispamAgents.ps1

Ejecute el siguiente comando:

    & $env:ExchangeInstallPath\Scripts\Install-AntiSpamAgents.ps1

## ¿Cómo sabe si este paso se ha completado correctamente?

Se sabe que este paso se realizó correctamente si el script se ejecuta sin errores y se le pide que reinicie el servicio de transporte de Microsoft Exchange.

## Paso 2: usar el Shell para reiniciar el servicio de transporte de Microsoft Exchange

Ejecute el siguiente comando:

```powershell
Restart-Service MSExchangeTransport
```

## ¿Cómo sabe si este paso se ha completado correctamente?

Se sabe que este paso se realizó correctamente si el servicio de transporte de Microsoft Exchange se reinicia sin errores.

## Paso 3: usar el Shell para especificar los servidores SMTP internos en la organización

Debe especificar las direcciones IP de los servidores SMTP internos que el agente de id. de remitente debe omitir. De hecho, debe especificar la dirección IP de al menos un servidor SMTP interno. Si el servidor de transporte de buzones en el que ejecuta los agentes contra correo no deseado es el único servidor SMTP de la organización, indique la dirección IP de ese equipo.

Para agregar las direcciones IP de los servidores SMTP internos sin que afecte a los valores existentes, ejecute el siguiente comando:

```powershell
Set-TransportConfig -InternalSMTPServers @{Add="<ip address1>","<ip address2>"...}
```

En este ejemplo siguiente se agregan las direcciones del servidor SMTP interno 10.0.1.10 y 10.0.1.11 a la configuración de transporte de su organización.

```powershell
Set-TransportConfig -InternalSMTPServers @{Add="10.0.1.10","10.0.1.11"}
```

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que especificó la dirección IP de al menos un servidor SMTP interno correctamente, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
    ```powershell
Get-TransportConfig | Format-List InternalSMTPServers
```

2.  Compruebe que aparece la dirección IP de al menos un servidor SMTP interno válido.

