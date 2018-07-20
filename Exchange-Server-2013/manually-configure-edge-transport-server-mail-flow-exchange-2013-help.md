---
title: 'Configurar manualmente el flujo de correo del servidor de transporte perimetral: Exchange 2013 Help'
TOCTitle: Configurar manualmente el flujo de correo del servidor de transporte perimetral
ms:assetid: cb4cc165-6c09-44ab-a95f-167ae8ed2485
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn606261(v=EXCHG.150)
ms:contentKeyID: 61183333
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar manualmente el flujo de correo del servidor de transporte perimetral

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-21_

En este tema se describen los procedimientos para realizar cambios de configuración manuales en la forma en que un servidor de transporte perimetral administra el flujo de correo. Estos procedimientos están dirigidos a determinados escenarios. Cuando suscriba servidores de transporte perimetral, es preferible usar la configuración predeterminada, a menos que su organización tenga unas necesidades concretas que requieran realizar cambios de configuración manuales.

**Contenido**

Configuración manual de conectores de envío

Conectores de envío internos de la organización

Crear conectores de envío adicionales después de la suscripción perimetral

Motivos para suprimir la creación automática de conectores de envío

Partición del flujo de correo

Enrutar correo saliente a un host inteligente

Configurar conectores de envío para dominios de retransmisión externos

## Configuración manual de conectores de envío

Puede modificar manualmente la configuración de un conector de envío. Por ejemplo, si necesita enrutar correo electrónico saliente a través de un host inteligente, puede suprimir la creación automática de un conector de envío y configurar manualmente un conector de envío para Internet.

## Conectores de envío internos de la organización

El conector de envío interno de la organización es un conector de envío implícito y oculto, calculado automáticamente por Exchange. Este conector de envío habilita el servicio de transporte en servidores de buzones de correo dentro de la misma organización para que retransmitan mensajes entre ellos sin usar conectores de envío explícitos. Dado que en Active Directory hay un objeto de configuración que tiene una asociación de sitio de Active Directory para una suscripción perimetral, el conector de envío interno de la organización se usará también para retransmitir mensajes a ese servidor de transporte perimetral.

Únicamente los servidores de buzones de correo que se encuentren en el sitio suscrito de Active Directory pueden transferir correo electrónico directamente al servidor de transporte perimetral, o desde él. Si tiene un bosque de varios sitios de Active Directory y Exchange está implementado en varios sitios, los servidores de buzones de correo de los sitios no suscritos enrutarán el correo electrónico saliente al sitio suscrito. Un servidor de buzones de correo en el sitio suscrito enrutará el correo electrónico saliente al servidor de transporte perimetral.

## Crear conectores de envío adicionales después de la suscripción perimetral

Después de suscribir un servidor de transporte perimetral a un sitio de Active Directory, se deshabilitan los cmdlets de creación y modificación de los conectores de envío en el servidor de transporte perimetral. Si quiere crear un conector de envío en el que el servidor de origen sea el servidor de transporte perimetral, puede crear el conector de envío dentro de la organización de Exchange. Puede especificar una o varias suscripciones perimetrales como servidor de origen para un conector de envío. No puede especificar servidores de buzones de correo y suscripciones perimetrales como servidores de origen para el mismo conector de envío. El conector de envío se replicará en la sesión de AD LDS del servidor de transporte perimetral que está configurado como servidor de origen la próxima vez que EdgeSync sincronice los datos de configuración. Si enumera más de una suscripción perimetral como servidor de origen, las conexiones a ese conector de envío tendrán equilibrio de carga entre los servidores de transporte perimetral con suscripción. Los servidores de transporte perimetral tienen que suscribirse al mismo sitio de Active Directory para que se produzca el equilibrio de carga. Si se configuran suscripciones perimetrales en distintos sitios de Active Directory como servidores de origen en el mismo conector de envío, los servidores de transporte perimetral solo enrutarán al servidor de origen más cercano.

Tendrá que crear conectores de envío manualmente si:

  - Suprimió la creación automática de conectores de envío de Internet o entrantes.

  - Aceptó dominios de la organización que están configurados como dominios de retransmisión externa.

## Motivos para suprimir la creación automática de conectores de envío

Según la topología de su organización de Exchange, puede decidir suprimir la creación automática de conectores de envío. En estos ejemplos describimos escenarios en los que es necesario suprimir la creación automática de conectores de envío.

## Partición del flujo de correo

Si decide realizar una partición del procesamiento de correo entrante y saliente entre dos servidores de transporte perimetral, uno de ellos se encargará de procesar el flujo de correo saliente y el otro se encargará de procesar el flujo de correo entrante. Para hacerlo, configure las suscripciones perimetrales de este modo:

  - Para el servidor de transporte perimetral saliente, ejecute este comando en el servidor de buzones de correo.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $false -CreateInternetSendConnector $true

  - Para el servidor de transporte perimetral entrante, ejecute este comando en el servidor de buzones de correo.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $true -CreateInternetSendConnector $false

## Enrutar correo saliente a un host inteligente

Si la organización de Exchange enruta todo el correo saliente a través de un host inteligente, el conector de envío creado automáticamente no tendrá la configuración adecuada.

Ejecute este comando en el servidor de buzones de correo para suprimir la creación automática del conector de envío a Internet.

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInternetSendConnector $false

Una vez completado el proceso de suscripción perimetral, cree manualmente un conector de envío a Internet. Cree el conector de envío dentro de la organización de Exchange y seleccione la suscripción perimetral como el servidor de origen para el conector. Seleccione el tipo de uso `Custom` y configure uno o varios hosts inteligentes. El nuevo conector de envío se replicará en la sesión de AD LDS del servidor de transporte perimetral la próxima vez que EdgeSync sincronice los datos de configuración. Puede forzar la sincronización de EdgeSync inmediata. Para ello, ejecute el cmdlet **Start-EdgeSynchronization** en un servidor de buzones de correo.

Ejemplo: usar el Shell para configurar un conector de envío para que un servidor de transporte perimetral suscrito enrute mensajes para todos los espacios de direcciones de Internet a través de un host inteligente. Ejecute esta tarea en un servidor de buzones de correo dentro de la organización de Exchange, en lugar de en un servidor de transporte perimetral.

    New-SendConnector -Name "EdgeSync - Site-A to Internet" -Usage Custom -AddressSpaces SMTP:*;100 -DNSRoutingEnabled $false -SmartHosts 192.168.10.1 -SmartHostAuthMechanism None -SourceTransportServers EdgeSubscriptionName


> [!IMPORTANT]
> Este mecanismo no especifica ningún mecanismo de autenticación de host inteligente. Asegúrese de configurar el mecanismo de autenticación correcto y facilitar todas las credenciales necesarias al crear un conector de host inteligente en su propia organización de Exchange.



## Configurar conectores de envío para dominios de retransmisión externos

Si ha aceptado dominios en su organización de Exchange que estén configurados como dominios de retransmisión externos, tiene que crear manualmente un conector de envío para estos espacios de dirección. Los mensajes que se envían a estos dominios de retransmisión externos se retransmiten mediante el servidor de transporte perimetral. El proceso de suscripción perimetral no crea ni configura automáticamente conectores de envío para dominios de retransmisión externos. Por eso, necesita configurar conectores de envío para estos dominios y especificar una o varias suscripciones perimetrales como el servidor de origen para estos conectores de envío.

El registro de recurso DNS MX para un dominio de retransmisión externo se resuelve en su servidor de transporte perimetral. Puede configurar un conector de envío que retransmita el correo electrónico a un dominio de retransmisión externo para usar un host inteligente para el enrutamiento. Si configura el conector de envío para un dominio de retransmisión externo para usar un enrutamiento DNS, se producirá un bucle de enrutamiento. Para más información sobre los dominios de retransmisión externos, vea [Dominios aceptados](accepted-domains-exchange-2013-help.md).

Volver al principio

