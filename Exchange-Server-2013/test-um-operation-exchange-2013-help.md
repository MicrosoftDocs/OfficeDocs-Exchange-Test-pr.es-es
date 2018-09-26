---
title: 'Comprobar el funcionamiento de la Mensajería unificada: Exchange 2013 Help'
TOCTitle: Comprobar el funcionamiento de la Mensajería unificada
ms:assetid: 06c9ab4e-8272-47b1-a217-e366f7e9dbaa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa995957(v=EXCHG.150)
ms:contentKeyID: 56271494
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Comprobar el funcionamiento de la Mensajería unificada

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-06-25_

En este tema, se explica cómo usar el Shell para comprobar el funcionamiento de su sistema de correo de voz. Al realizar el siguiente procedimiento, el servidor de mensajes de correo que ejecuta el Servicio de mensajería unificada de Microsoft Exchange inicia una llamada de Protocolo de inicio de sesión (SIP) de diagnóstico y, luego, devuelve una variable del estado de los Servicios de mensajería unificada.

Esta prueba de diagnóstico solo se puede ejecutar en un servidor de buzones de correo local, y se no puede comprobar el funcionamiento del servidor de buzones de correo mediante el EAC.

Para obtener información sobre otras tareas relacionadas con los servidores de acceso de cliente y de buzones de correo, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas “Servidor de buzones (servicio de Mensajería unificada)” y “Servidor de acceso de cliente (servicio enrutador de llamadas de Mensajería unificada)” del tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Para realizar los siguientes procedimientos, debe iniciar sesión en el servidor de buzones con una cuenta que sea miembro del grupo de administradores locales.

  - Compruebe que el servidor de buzones está instalado. No importa si está instalado en el mismo PC que el servidor de acceso de cliente o en otro distinto.

  - Compruebe que el servidor de acceso de cliente está instalado. No importa si está instalado en el mismo PC que el servidor de buzones o en otro distinto.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para comprobar el funcionamiento de los Servicios de mensajería unificada

En este ejemplo, se realizan las pruebas de conectividad y funcionalidad en el servidor de buzones de correo local y, luego, se muestra la información de conectividad de voz sobre IP (VoIP).

```powershell
Test-UMConnectivity
```

En este ejemplo, se comprueba la capacidad de un servidor de acceso de cliente local para escuchar las solicitudes SIP no cifradas entrantes en el puerto TCP 5060.

```powershell
Test-UMConnectivity -ListenPort 5060
```

En este ejemplo, se comprueba la capacidad de un servidor de acceso de cliente local para escuchar las solicitudes SIP cifradas entrantes en el puerto TCP 5061.

```powershell
Test-UMConnectivity -ListenPort 5061
```


> [!NOTE]
> Usar el modo 1 cuando no se especifica el parámetro <CODE>-UMIPGateway</CODE>.




> [!NOTE]
> Puede establecer el parámetro <CODE>-Timeout</CODE> con un valor menor que 5 segundos. Sin embargo, es recomendable que siempre configure este parámetro con un valor de 5 segundos o más.


