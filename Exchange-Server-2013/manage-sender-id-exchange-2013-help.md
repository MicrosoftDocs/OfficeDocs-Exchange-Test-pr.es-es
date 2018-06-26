---
title: 'Administración del Id. del remitente: Exchange 2013 Help'
TOCTitle: Administración del Id. del remitente
ms:assetid: 2e7b646a-8a66-4be7-a7c1-0bd43bb79a5b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997136(v=EXCHG.150)
ms:contentKeyID: 49895543
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administración del Id. del remitente

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

El agente del Id. de remitente proporciona la funcionalidad del Id. del remitente. Para validar el origen de los mensajes de correo electrónico, el Id. del remitente compara la dirección IP del remitente con el supuesto propietario del dominio de envío. El filtrado del Id. del remitente se realiza en los mensajes entrantes procedentes de Internet pero no autenticados. Estos mensajes se tratan como si fuesen mensajes externos.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones contra el correo no deseado" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - De manera predeterminada, las características contra correo no deseado no están habilitadas en el Servicio de transporte en un servidor de buzones. Por lo general, solo se habilitan las características contra correo no deseado si la organización de Exchange no realiza un filtrado previo contra correo no deseado antes de aceptar mensajes entrantes. Para obtener más información, consulte [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar Shell para habilitar o deshabilitar el Id. del remitente

Para deshabilitar el Id. del remitente, ejecute el siguiente comando:

    Set-SenderIDConfig -Enabled $false

Para habilitar el Id. del remitente, ejecute el siguiente comando:

    Set-SenderIDConfig -Enabled $true


> [!NOTE]
> Al deshabilitar el Id. del remitente, el agente del Id. de remitente subyacente todavía está habilitado. Para deshabilitar el agente del Id. de remitente, ejecute el comando: <CODE>Disable-TransportAgent "Sender ID Agent"</CODE>.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya habilitado o deshabilitado el filtrado del Id. de remitente, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderIDConfig | Format-List Enabled

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Uso del Shell para configurar las acciones del Id. del remitente para mensajes falsificados

Para configurar la acción del Id. del remitente para mensajes falsificados, ejecute el siguiente comando:

    Set-SenderIDConfig -SpoofedDomainAction <StampStatus | Reject | Delete>

Este ejemplo configura el agente del Id. de remitente para rechazar mensajes en los que la dirección IP del servidor de envío no consta como servidor de envío SMTP con autoridad en el registro de la estructura de directivas de remitente (SPF) de DNS para el dominio de envío.

    Set-SenderIDConfig -SpoofedDomainAction Reject

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha configurado correctamente las acciones del Id. de remitente de los mensajes falsificados, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderIDConfig | Format-List SpoofedDomainAction

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Uso del Shell para configurar las acciones de Id. del remitente para errores transitorios

Para configurar la acción del Id. del remitente para errores transitorios, ejecute el siguiente comando:

    Set-SenderIDConfig -TempErrorAction <StampStatus | Reject | Delete>

Este ejemplo configura el agente del Id. del remitente para marcar los mensajes cuyo estado de identificador del remitente no se puede establecer debido a un error temporal. Otros agentes de correo no deseado procesarán el mensaje y el agente de filtro de contenido usará la marca al determinar el valor de SCL para el mensaje.

    Set-SenderIDConfig -TempErrorAction StampStatus

Tenga en cuenta que `StampStatus` es el valor predeterminado del parámetro *TempErrorAction*.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha configurado correctamente las acciones del Id. de remitente de los errores transitorios, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderIDConfig | Format-List TempErrorAction

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Uso del Shell para configurar las excepciones de dominios de destinatarios y remitentes

Para reemplazar los valores existentes, ejecute el siguiente comando:

    Set-SenderIDConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenderDomains <domain1,domain2...>

Este ejemplo configura el agente del Id. del remitente para omitir la comprobación del Id. del remitente de los mensajes enviados a kim@contoso.com y a john@contoso.com, y omitir la comprobación del Id. del remitente de los mensajes enviados desde el dominio fabrikam.com.

    Set-SenderIDConfig -BypassedRecipients kim@contoso.com,john@contoso.com -BypassedSenderDomains fabrikam.com

Para agregar o quitar entradas sin modificar valores existentes, ejecute el siguiente comando:

    Set-SenderIDConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Este ejemplo configura al agente del Id. del remitente con la siguiente información:

  - Agregar chris@contoso.com y michelle@contoso.com a la lista de destinatarios existentes que omiten la comprobación del Id. del remitente.

  - Eliminar tailspintoys.com de la lista de dominios existentes que omiten la comprobación del Id. del remitente.

<!-- end list -->

    Set-SenderIDConfig -BypassedRecipients @{Add="chris@contoso.com","michelle@contoso.com"} -BypassedSenderDomains @{Remove="tailspintoys.com"}

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha configurado correctamente las excepciones de remitente o dominio, haga lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderIDConfig | Format-List BypassedRecipients,BypassedSenderDomains

2.  Verifique que los valores mostrados son los valores que ha configurado.

