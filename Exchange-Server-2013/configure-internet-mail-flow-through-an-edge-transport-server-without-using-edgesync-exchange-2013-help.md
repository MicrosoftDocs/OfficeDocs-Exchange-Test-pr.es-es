---
title: 'Configurar el flujo de correo de Internet a través de un servidor de transporte perimetral sin usar EdgeSync: Exchange 2013 Help'
TOCTitle: Configurar el flujo de correo de Internet a través de un servidor de transporte perimetral sin usar EdgeSync
ms:assetid: 6bb98d10-6f12-4b08-a58e-36375f605d65
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232082(v=EXCHG.150)
ms:contentKeyID: 61183328
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el flujo de correo de Internet a través de un servidor de transporte perimetral sin usar EdgeSync

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-01-23_

Se recomienda usar el proceso de suscripción perimetral para establecer flujo de correo entre la organización de Exchange y un servidor Transporte perimetral. Sin embargo, determinadas situaciones pueden impedir la suscripción del servidor Transporte perimetral a la organización de Exchange con el proceso de suscripción perimetral. Para establecer manualmente flujo de correo entre la organización de Exchange y el servidor Transporte perimetral, deberá crear y configurar los conectores de envío y recepción en el servidor Transporte perimetral y en los servidores de buzones de correo que haya en la organización de Exchange.

## Antes de empezar

  - Tiempo estimado para finalizar esta tarea: 30 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Conectores de envío", la entrada "Conectores de envío: transporte perimetral" y la entrada "Conectores de recepción: transporte perimetral" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Este procedimiento usa la autenticación básica por medio de Seguridad del nivel de transporte (TLS) para ofrecer cifrado y autenticación. Si se usa la autenticación básica por medio de TLS, el servidor receptor debe tener instalado un certificado de servidor de Nivel de sockets seguros (SSL) X.509. El valor del nombre de dominio completo (FQDN) configurado en el conector de recepción debe coincidir con el FQDN en el certificado del servidor de SSL. De forma predeterminada, el valor del FQDN en el conector de recepción es el FQDN del servidor que contiene el conector de recepción.

  - También puede usar el método de autenticación protegido externamente. No obstante, si lo usa, la comunicación entre el servidor de transporte perimetral y el servidor de transporte de buzones no se autentica ni se cifra mediante Exchange. Se recomienda usar el método de autenticación con seguridad externa solo cuando también se use un método de cifrado adicional. El método de cifrado puede ser una asociación de protocolo de seguridad de Internet (IPsec) o una red privada virtual (VPN).

  - El servidor de transporte perimetral tiene normalmente *hosts múltiples*. Esto significa que el servidor Transporte perimetral tiene adaptadores de red que se conectan a varios segmentos de red. Cada adaptador de red tiene una única configuración IP. El adaptador de red conectado al segmento de red externo o público debe configurarse para que use un servidor de sistema de nombres de dominio (DNS) público para la resolución de nombres. Esto permite al servidor resolver los nombres de dominio SMTP a los registros de los recursos de MX y enrutar el correo a Internet. El adaptador de red conectado al segmento de red interno o privado debe estar configurado para usar un servidor DNS en la red perimetral o debe tener un archivo de hosts disponible.

  - Es necesario crear una cuenta de usuario en Active Directory y agregarla al grupo de seguridad universal en el equipo de Exchange Server. El conector de envío usa esta cuenta en el servidor Transporte perimetral para autenticar el servidor de buzones de correo de destino en la organización de Exchange.
    

    > [!IMPORTANT]
    > A esta cuenta se conceden los permisos asociados con los equipos que ejecutan Exchange Server. Asegúrese de proteger las credenciales de la cuenta para evitar el uso indebido de la misma. Puede configurar la cuenta para permitir el inicio de sesión únicamente en equipos específicos.



## Procedimientos del servidor de transporte perimetral

En el servidor de transporte perimetral se necesitan los siguientes conectores:

  - Un conector de envío configurado para enviar mensajes a Internet

  - Un conector de envío configurado para enviar mensajes a los servidores de buzones de correo en la organización de Exchange

  - Un conector de recepción configurado para recibir mensajes solamente desde los servidores de buzones de correo en la organización de Exchange

  - Un conector de recepción configurado para aceptar mensajes solamente desde Internet

De forma predeterminada, se crea un único conector de recepción durante la instalación de la función del servidor Transporte perimetral. Este conector se puede usar tanto para mensajes de Internet entrantes como para mensajes entrantes procedentes de servidores de buzones de correo. Normalmente, el proceso de suscripción perimetral configura automáticamente los permisos correctos y la autenticación en el conector de recepción predeterminado. Si no se usa el proceso de suscripción perimetral, es recomendable modificar el conector de recepción predeterminado en el servidor Transporte perimetral para que acepte únicamente mensajes procedentes de Internet. A continuación, debe crear un conector de recepción en el servidor Transporte perimetral que esté configurado para aceptar solamente mensajes procedentes de servidores internos de buzones.

En las siguientes secciones, conocerá todos los pasos de configuración requeridos para preparar su servidor de transporte perimetral con el fin de comunicarse con su organización de Exchange.


> [!NOTE]
> Solo puede usar el Shell para realizar estos procedimientos en los servidores de transporte perimetral.



## Paso 1: Cree un conector de envío configurado para enviar mensajes a Internet

Este conector de envío necesita la configuración siguiente:

  - **Nombre**   Para Internet (o cualquier nombre descriptivo)

  - **Tipo de uso**   Internet

  - **Espacios de direcciones**   "\*" (todos los dominios)

  - **Configuración de red**   Use registros MX de DNS para enrutar el correo automáticamente. Según la configuración de red, también puede enrutar el correo a través de un host inteligente. El host inteligente enruta el correo a Internet.

Para crear un conector de envío que esté configurado para enviar mensajes a Internet, ejecute el siguiente comando.

    New-SendConnector -Name "To Internet" -AddressSpaces * -Usage Internet -DNSRoutingEnabled $true

Para obtener información más detallada acerca de la sintaxis y los parámetros, vea [New-SendConnector](https://technet.microsoft.com/es-es/library/aa998936\(v=exchg.150\)).

## Paso 2: Cree un conector de envío configurado para enviar mensajes a la organización de Exchange

Use el cmdlet **New-SendConnector** para crear un conector de envío.


> [!NOTE]
> Antes de crear el conector de envío, primero, debe ejecutar el comando <STRONG>Get-Credential</STRONG> para guardar el nombre de usuario y la contraseña que usará en una variable temporal. Necesita hacer esto porque el cmdlet <STRONG>New-SendConnector</STRONG> no aceptará las credenciales de usuario en texto sin formato.



Este conector de envío necesita la configuración siguiente:

  - **Nombre**   Para org interna (o cualquier nombre descriptivo)

  - **Tipo de uso**   Interno

  - **Espacios de direcciones**   Todos los dominios aceptados para la organización de Exchange. Por ejemplo, \*.contoso.com.

  - Enrutamiento de DNS deshabilitado (enrutamiento de host inteligente habilitado)

  - **Hosts inteligentes**   FQDN de uno o varios servidores de buzones de correo como hosts inteligentes. Por ejemplo, mbxserver01.contoso.com y mbxserver02.contoso.com.

  - **Métodos de autenticación de host inteligente** Autenticación básica sobre TLS

  - **Credenciales de autenticación de host inteligente**   Credenciales para la cuenta de usuario en el dominio interno. Primero hay que guardar el nombre de usuario y la contraseña en una variable temporal, ya que el cmdlet **New-SendConnector** no aceptará credenciales de usuario en texto sin formato.

Para crear un conector de envío que esté configurado para enviar mensajes a la organización de Exchange, ejecute los siguientes comandos.

    $MailboxCredentials = Get-Credential
    New-SendConnector -Name "To Internal Org" -Usage Internal -AddressSpaces *.contoso.com -DNSRoutingEnabled $false -SmartHosts mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $MailboxCredentials

Para información detallada sobre la sintaxis y los parámetros, véase [New-SendConnector](https://technet.microsoft.com/es-es/library/aa998936\(v=exchg.150\)).

## Paso 3: Modifique el conector de recepción predeterminado para que solamente acepte mensajes de Internet

Debe realizar los siguientes cambios de configuración en el conector de recepción predeterminado:

  - Modifique el nombre para indicar que el conector se usará únicamente para recibir correo electrónico procedente de Internet. El nombre del conector de recepción predeterminado es "Conector de recepción interno predeterminado \<Nombre de servidor Transporte perimetral\>".

  - Cambie los enlaces de red para aceptar mensajes únicamente desde el adaptador de red al que se puede obtener acceso desde Internet. Por ejemplo, 10.1.1.1 y el valor de puerto SMTP TCP estándar de 25.

Si quiere modificar el conector de recepción predeterminado para que solo acepte mensajes procedentes de Internet, ejecute el siguiente comando.

    Set-ReceiveConnector "Default internal Receive connector Edge01" -Name "From Internet" -Bindings 10.1.1.1:25

Para obtener información más detallada acerca de la sintaxis y los parámetros, vea [Set-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125140\(v=exchg.150\)).

## Paso 4: Cree un conector de recepción que esté configurado únicamente para aceptar mensajes de la organización de Exchange

Este conector de recepción necesita la configuración siguiente:

  - **Nombre**   De org interna (o cualquier nombre descriptivo)

  - **Tipo de uso**   Interno

  - **Enlaces de red locales**   Adaptador de red expuesto a red interno. Por ejemplo, 10.1.1.2 y el valor de puerto SMTP TCP estándar de 25.

  - **Configuración de red remota**   Dirección IP de uno o varios servidores de buzones de correo en la organización de Exchange Por ejemplo, 192.168.5.10 y 192.168.5.20.

  - **Métodos de autenticación**   TLS, autenticación básica, autenticación básica sobre TLS y autenticación de Exchange Server.

Para crear un conector de recepción que esté configurado para aceptar mensajes procedentes de la organización de Exchange, ejecute el siguiente comando.

    New-ReceiveConnector -Name "From Internal Org" -Usage Internal -AuthMechanism TLS,BasicAuth,BasicAuthRequireTLS,ExchangeServer -Bindings 10.1.1.2:25 -RemoteIPRanges 192.168.5.10,192.168.5.20

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [New-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125139\(v=exchg.150\)).

## ¿Cómo saber si estos pasos han funcionado?

Para comprobar que haya configurado correctamente los conectores de envío y los conectores de recepción necesarios, ejecute los siguientes comandos en el servidor Transporte perimetral y compruebe los valores que se muestran como valores configurados.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,SourceTransportServers,DSNRoutingEnabled,SmartHosts,SmartHostAuthMechanism
    Get-ReceiveConnector | Format-List Name,Usage,AuthMechanism,Bindings,RemoteIPRanges

## Procedimientos de servidor de buzones de correo

Los servidores de buzones de correo en la organización requieren un conector de envío configurado para enviar mensajes al servidor Transporte perimetral para retransmitir a Internet.

De forma predeterminada, se crean dos conectores de recepción durante la instalación del rol del servidor de buzones de correo. El conector llamado "*nombreDeServidor* del cliente" está configurado para aceptar mensajes de todos los clientes de mensajería de POP3 e IMAP. El conector llamado "*nombreDeServidor* predeterminado" está configurado para aceptar mensajes de un servidor de transporte perimetral. No hace falta modificar estos conectores.

## Paso 5: Crear un conector de envío que esté configurado para enviar mensajes salientes al servidor de transporte perimetral

Este conector de envío necesita la configuración siguiente:

  - **Nombre**   Para servidor perimetral (o cualquier nombre descriptivo)

  - **Tipo de uso**   Interno

  - **Espacios de direcciones**   "\*" (todos los dominios)

  - Enrutamiento de DNS deshabilitado (enrutamiento de host inteligente habilitado)

  - **Hosts inteligentes**   Dirección IP o FQDN del servidor Transporte perimetral. Por ejemplo, edge01.contoso.net.

  - **Servidores de buzones de correo de origen**   FQDN de uno o varios servidores de buzones de correo. Por ejemplo, mbxserver01.contoso.com y mbxserver02.contoso.com.

  - **Método de autenticación de host inteligente** Autenticación básica sobre TLS.

  - **Credenciales de autenticación de host inteligente**   Credenciales para la cuenta de usuario en el servidor Transporte perimetral. Primero hay que guardar el nombre de usuario y la contraseña en una variable temporal, ya que el cmdlet **New-SendConnector** no aceptará credenciales de usuario en texto sin formato.

Para crear un conector de envío que esté configurado para enviar mensajes salientes al servidor Transporte perimetral, ejecute los siguientes comandos.

    $EdgeCredentials = Get-Credential
    New-SendConnector -Name "To Edge" -Usage Internal -AddressSpaces * -DNSRoutingEnabled $false -SmartHosts edge01.contoso.com -SourceTransportServers mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $EdgeCredentials

Para información detallada sobre la sintaxis y los parámetros, véase [New-SendConnector](https://technet.microsoft.com/es-es/library/aa998936\(v=exchg.150\)).

## ¿Cómo saber si el paso ha funcionado?

Para comprobar que haya creado correctamente un conector de envío configurado para enviar mensajes salientes al servidor Transporte perimetral, ejecute el siguiente comando en un servidor de buzones de correo y compruebe los valores que se muestran como valores configurados.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,DSNRoutingEnabled,SmartHosts,SourceTransportServers,SmartHostAuthMechanism

