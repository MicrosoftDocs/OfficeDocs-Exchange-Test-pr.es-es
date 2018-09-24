---
title: 'Deshabilitar TLS entre sitios de Active Directory: Exchange 2013 Help'
TOCTitle: Deshabilitar TLS entre sitios de Active Directory
ms:assetid: 1e1a0acf-24e7-4f94-9b33-603a4e0a812c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876856(v=EXCHG.150)
ms:contentKeyID: 52062016
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar TLS entre sitios de Active Directory

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-19_

Microsoft Exchange Server 2013 permite deshabilitar TLS para la comunicación SMTP entre los servidores de buzones de ciertas topologías en las se usan dispositivos WAN Optimization Controller (WOC) que comprimen el tráfico SMTP.

En este tema se dan instrucciones paso a paso sobre cómo configurar el servicio de transporte en los servidores de buzones afectados para deshabilitar TLS y garantizar que la topología de enrutamiento de Active Directory esté configurada para enrutar los mensajes correctamente. Para más información sobre este escenario, vea [Caso: Configurar Exchange para que sea compatible con los controladores de optimización de la WAN](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea:  60 minutos.

  - Aunque los pasos de configuración de este escenario se pueden completar con menos derechos, para completar todas las tareas del escenario de principio a fin, la cuenta debe ser miembro del grupo de funciones de administración de la organización.

  - Asegúrese de deshabilitar TLS solamente en conexiones que pasan a través de dispositivos WOC.

  - Este proceso requiere que se haya implementado Exchange 2013 en varios sitios de Active Directory y que al menos un sitio esté conectado a los otros a través de un vínculo WAN.

  - Este proceso requiere que los dispositivos WOC estén implementados para comprimir el tráfico SMPT a través del vínculo WAN.

  - Este proceso requiere que exista una ruta de flujo de mensajes lógicos para que Exchange analice el vínculo WAN que tiene los dispositivos WOC implementados.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Paso 1: Usar el Shell para configurar el servicio de transporte en el servidor de buzones para usar la autenticación degradada de Exchange Server

Para configurar el servicio de transporte en un servidor de buzones para usar la autenticación degradada de Exchange server, ejecute el comando siguiente:

```powershell
Set-TransportService <ServerIdentity> -UseDowngradedExchangeServerAuth $true
```

Este ejemplo hace que esta configuración cambie en el servidor denominado Mailbox01.

```powershell
Set-TransportService Mailbox01 -UseDowngradedExchangeServerAuth $true
```

## Paso 2: Crear un conector de recepción dedicado en el servidor de buzones para el sitio de Active Directory de destino

## Usar la EMC para crear el conector de recepción

1.  En el Centro de administración de Exchange (EAC), haga clic en **Flujo de correo** \> **Conectores de recepción** y en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la primera página del asistente **Nuevo conector de recepción**, escriba los siguientes valores:
    
      - **Nombre:**  escriba un valor descriptivo.
    
      - **Tipo:**  interno
    
    Cuando haya terminado, haga clic en **Siguiente**.

3.  En la segunda página del asistente **Nuevo conector de recepción**, en la sección **Configuración remota**, escriba las direcciones IP o intervalos de direcciones IP del sitio de Active Directory de destino. Cuando termine, haga clic en **Finalizar**.

## Uso del Shell para crear el conector de recepción

Para crear un conector de recepción en el servidor de buzones, ejecute el comando siguiente:

```powershell
    New-ReceiveConnector -Name <Name> -Server <ServerIdentity> -RemoteIPRanges <IPAddressRange> -Internal
```

En este ejemplo se crea el conector de recepción llamado WAN en el servidor Mailbox01 con la configuración siguiente:

  - El parámetro *RemoteIPRanges* está definido en 10.0.2.0/24. Este intervalo de direcciones IP deberá corresponderse con el sitio de Active Directory remoto desde el que este conector de recepción recibirá conexiones no cifradas. Si hay más de una subred IP en el sitio remoto, puede introducirlas separadas por coma.

  - El tipo de uso está establecido como interno.

<!-- end list -->

```powershell
New-ReceiveConnector -Name WAN -Server Hub01 -RemoteIPRanges 10.0.2.0/24 -Internal
```

## Paso 3: Usar el Shell para deshabilitar TLS en el conector de recepción dedicado

Para deshabilitar TLS en el conector de recepción, ejecute el siguiente comando:

```powershell
Set-ReceiveConnector <ReceiveConnectorIdentity> -SuppressXAnonymousTLS $true
```

En este ejemplo se deshabilita TLS en el conector de recepción llamado WAN del servidor de buzones Mailbox01.

```powershell
Set-ReceiveConnector Mailbox01\WAN -SuppressXAnonymousTLS $true
```

## Paso 4: Usar el Shell para designar los sitios de Active Directory como sitios de concentradores

Para designar un sitio de Active Directory como sitio de concentradores, ejecute el siguiente comando:

```powershell
Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true
```

Debe hacer este proceso una vez en cada sitio de Active Directory que tenga servidores de buzones que participen en el tráfico no cifrado.

En este ejemplo se configura el sitio de Active Directory denominado Central Office Site 1 como sitio de concentradores.

```powershell
Set-AdSite "Central Office Site 1" -HubSiteEnabled $true
```

## Paso 5: Usar el Shell para configurar como mínimo la ruta de enrutamiento de coste a través de la conexión WAN

En función de cómo estén configurados los costes de vínculos de sitios IP en Active Directory, es posible que este paso no sea necesario. Debe comprobar que el vínculo de red con los dispositivos WOC implementados está en la ruta de enrutamiento de menor coste. Para ver los costes de vínculos de sitio de Active Directory y los costes de vínculo de sitio específicos de Exchange, ejecute el comando siguiente:

```powershell
Get-AdSiteLink
```

Si el vínculo de red con los dispositivos WOC implementados no está en la ruta de enrutamiento de menor coste, deberá asignar un coste específico de Exchange al vínculo de sitio IP concreto para garantizar que los mensajes se enrutan correctamente. Para más información sobre este tema concreto, vea la sección "Configurar costes de vínculos de sitio de Active Directory específicos de Exchange" en [Caso: Configurar Exchange para que sea compatible con los controladores de optimización de la WAN](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

En este ejemplo se configura un coste específico de Exchange de 15 en el vínculo de sitio IP llamado Branch Office 2-Branch Office 1.

```powershell
Set-AdSiteLink "Branch Office 2-Branch Office 1" -ExchangeCost 15
```

