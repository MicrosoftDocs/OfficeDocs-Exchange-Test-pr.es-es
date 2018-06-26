---
title: 'Administrar el filtrado de remitentes: Exchange 2013 Help'
TOCTitle: Administrar el filtrado de remitentes
ms:assetid: a7f4b3e1-2970-45ad-911e-a9f46d880d3d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124087(v=EXCHG.150)
ms:contentKeyID: 49895821
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar el filtrado de remitentes

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

El Agente de filtrado de remitentes proporciona el filtrado del remitente. El agente de filtro de remitentes se basa en **MAIL FROM:** El encabezado SMTP determina qué acción, si la hay, se debería realizar en un mensaje de correo electrónico de entrada.

Si se habilita en un servidor Exchange la función de filtrado de remitentes, ésta filtra todos los mensajes que llegan a través de los conectores de recepción a dicho equipo.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones contra el correo no deseado" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - De manera predeterminada, las características contra correo no deseado no están habilitadas en el Servicio de transporte en un servidor de buzones. Por lo general, solo se habilitan las características contra correo no deseado si la organización de Exchange no realiza un filtrado previo contra correo no deseado antes de aceptar mensajes entrantes. Para obtener más información, consulte [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para habilitar o deshabilitar el filtrado de remitentes

Para deshabilitar el filtro de remitentes, ejecute el comando siguiente:

    Set-SenderFilterConfig -Enabled $false

Para habilitar el filtrado de remitentes, ejecute el siguiente comando:

    Set-SenderFilterConfig -Enabled $true


> [!NOTE]
> Cuando deshabilita el filtrado de remitentes, el agente de filtro de destinatarios subyacente todavía sigue habilitado. Para deshabilitar el agente de filtro de remitentes, ejecute el siguiente comando: <CODE>Disable-TransportAgent "Sender Filter Agent"</CODE>.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que habilitó o deshabilitó correctamente el filtrado de destinatarios, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderFilterConfig | Format-List Enabled

2.  Verifique que el valor mostrado es el valor que ha configurado.

## Use el Shell para configurar los remitentes y dominios bloqueados

Para reemplazar los valores existentes, ejecute el siguiente comando:

    Set-SenderFilterConfig -BlockedSenders <sender1,sender2...> -BlockedDomains <domain1,domain2...> -BlockedDomainsAndSubdomains <domain1,domain2...>

En este ejemplo se configura al agente de filtro de destinatarios para bloquear mensajes de kim@contoso.com y john@contoso.com, mensajes del dominio fabrikam.com y mensajes de northwindtraders.com y todos sus subdominios.

    Set-SenderFilterConfig -BlockedSenders kim@contoso.com,john@contoso.com -BlockedDomains fabrikam.com -BlockedDomainsAndSubdomains northwindtraders.com

Para agregar o quitar entradas sin modificar valores existentes, ejecute el siguiente comando:

    Set-SenderFilterConfig -BlockedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BlockedDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...} -BlockedDomainsAndSubdomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

En este ejemplo se configura al agente de filtro de remitentes con la siguiente información:

  - Agregue chris@contoso.com y michelle@contoso.com a la lista de remitentes existentes bloqueados.

  - Quite tailspintoys.com de la lista de los dominios existentes de remitentes bloqueados.

  - Agregue blueyonderairlines.com a la lista de dominios y subdominios de remitentes existentes bloqueados.

<!-- end list -->

    Set-SenderFilterConfig -BlockedSenders @{Add="chris@contoso.com","michelle@contoso.com"} -BlockedDomains @{Remove="tailspintoys.com"} -BlockedDomainsAndSubdomains @{Add="blueyonderairlines.com"}

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que configuró correctamente los remitentes bloqueados, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderFilterConfig | Format-List BlockedSenders,BlockedDomains,BlockedDomainsAndSubdomains

2.  Verifique que los valores mostrados son los valores que ha configurado.

## Use el Shell para habilitar o deshabilitar los mensajes bloqueados con remitentes en blanco

Para habilitar o deshabilitar los mensajes bloqueados con remitentes en blanco, ejecute el siguiente comando:

    Set-SenderFilterConfig -BlankSenderBlockingenabled <$true | $false>

En este ejemplo se configura el agente de filtro de remitentes para bloquear mensajes que no especifiquen ningún remitente en MAIL FROM: Comando SMTP:

    Set-SenderFilterConfig -BlankSenderBlockingEnabled $true

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que habilitó o deshabilitó correctamente los mensajes bloqueados con remitentes en blanco, realice lo siguiente:

1.  Ejecute el siguiente comando:
    
        Get-SenderFilterConfig | Format-List BlankSenderBlockingEnabled

2.  Verifique que el valor mostrado es el valor que ha configurado.

