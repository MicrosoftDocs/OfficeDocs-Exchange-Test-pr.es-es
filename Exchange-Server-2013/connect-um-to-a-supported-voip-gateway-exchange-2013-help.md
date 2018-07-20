---
title: 'Conectar la mensajería unificada a una puerta de enlace VoIP compatible: Exchange 2013 Help'
TOCTitle: Conectar la mensajería unificada a una puerta de enlace VoIP compatible
ms:assetid: b8dfc8bd-2ee5-418d-b0a4-4fa2ec7e2a2e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124360(v=EXCHG.150)
ms:contentKeyID: 50556873
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conectar la mensajería unificada a una puerta de enlace VoIP compatible

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-19_

Cuando configure la mensajería unificada (UM), deberá configurar puertas de enlace de voz sobre IP (VoIP), IP PBX, PBX habilitadas para SIP o controladores de borde de sesión (SBC) en la red a fin de poder comunicarse con los servidores de acceso de clientes que ejecuten el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange, así como con los servidores de buzones que ejecuten el servicio de mensajería unificada de Microsoft Exchange en la organización de Exchange. También deberá configurar los servidores de buzones y de acceso de clientes para comunicarse con las puertas de enlace VoIP, IP PBX, PBX habilitadas para SIP o SBC.


> [!NOTE]
> Después de conectar los servidores de buzones y de acceso de clientes a las puertas de enlace VoIP, IP&nbsp;PBX, PBX habilitadas para SIP o SBC en la red de datos, deberá crear los componentes necesarios de mensajería unificada, así como habilitar a los usuarios para la mensajería unificada a fin de que puedan usar el sistema de correo de voz.



## Pasos

A continuación se detallan los pasos básicos para conectar puertas de enlace VoIP, IP PBX, PBX habilitadas para SIP o SBC a los servidores de buzones o de acceso de clientes:

Paso 1: instalar los servidores de buzones y de acceso de clientes en la organización.

Paso 2: Cree y configure una extensión telefónica, un URI de SIP o un plan de marcado de mensajería unificada E.164.

Paso 3: Cree y configure una puerta de enlace IP de mensajería unificada. Debe crear y configurar una puerta de enlace IP de mensajería unificada por cada puerta de enlace VoIP, IP PBX, PBX habilitada para SIP o SBC que vaya a aceptar llamadas entrantes o enviar llamadas salientes.

Paso 4: crear un nuevo grupo de extensiones de mensajería unificada si es necesario. Si crea una puerta de enlace IP de mensajería unificada y no especifica ningún plan de marcado de mensajería unificada, se crea un grupo de extensiones de mensajería unificada de forma automática.

Para obtener información acerca de cada paso, consulte las siguientes secciones.

## Paso 1: instalar los servidores de buzones y de acceso de clientes

Al implementar servidores Exchange en una organización, puede instalar los servidores de buzones y de acceso de clientes en el mismo equipo o instalar cada uno de estos servidores en equipos diferentes. Para instalar el servidor de acceso de clientes, ejecute Setup.exe desde el medio de instalación. Independientemente de si instala el servidor de acceso de clientes en el mismo equipo o en un equipo diferente al del servidor de buzones, deberá usar el mismo comando. Para obtener información más detallada, consulte [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). Si desea agregar características y funcionalidad al servidor Exchange existente, use **Programas y características** o Setup.exe.

## Paso 2: Cree y configure un plan de marcado de mensajería unificada

Después de instalar los servidores necesarios, deberá crear un plan de marcado de mensajería unificada. Un plan de marcado de mensajería unificada contiene los valores de configuración que le permiten conectarse a su red de telefonía mediante la vinculación de una o varias puertas de enlace IP de mensajería unificada. Una puerta de enlace IP y un grupo de extensiones de mensajería unificada también se vinculan a un plan de marcado de mensajería unificada y son necesarios. Para obtener información más detallada, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

El plan de marcado de mensajería unificada establece un vínculo desde el número de extensión telefónica de un usuario hasta un buzón con la mensajería unificada habilitada. Al crear un plan de marcado de mensajería unificada, puede configurar el número de dígitos de los números de extensión, el tipo de identificador uniforme de recursos (URI) y los ajustes de seguridad VoIP correspondientes al plan de marcado.

Existen tres tipos de planes de marcado: extensión telefónica, URI de Protocolo de inicio de sesión (SIP) y E.164. Al crear y configurar un plan de marcado de mensajería unificada, debe determinar el tipo de información que se envía desde su IP PBX, PBX habilitada para SIP o PBX y, de igual modo, si las llamadas se envían a un servidor de buzones o de acceso de clientes en formato de extensión telefónica o E.164. Si va a implementar Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server, debe crear y configurar un plan de marcado URI de SIP.

## Paso 3: Crear y configurar una puerta de enlace IP de MU

Después de crear un plan de marcado de mensajería unificada, deberá crear una puerta de enlace IP de mensajería unificada que represente las puertas de enlace VoIP, IP PBX o SBC en la red. Cuando cree una puerta de enlace IP de mensajería unificada, puede configurarla para que use una dirección IP o un nombre de dominio completo (FQDN). Si se usa un FQDN, es preciso asegurarse de que se haya configurado correctamente un registro de host DNS para la puerta de enlace IP, de modo que el nombre del host se resuelva correctamente en una dirección IP.

Una vez instalada la puerta de enlace VoIP, IP PBX o SBC, debe crear una puerta de enlace IP de mensajería unificada que represente el dispositivo de hardware físico. Una vez creada una puerta de enlace IP de mensajería unificada, el servidor de acceso de clientes que usa dicha puerta de enlace envía una solicitud SIP OPTIONS a la puerta de enlace VoIP, IP PBX o SBC para asegurarse de que responde. En caso de que la puerta de enlace VoIP, IP PBX o SBC no responda, el servidor de acceso de clientes registra un evento con el identificador 1088, en el que se informa de que la solicitud no se cursó. Para solucionar este problema, procure que la puerta de enlace VoIP, IP PBX o SBC esté disponible y en línea y, asimismo, que la configuración de mensajería unificada sea correcta.

Los servidores de buzones y de acceso de clientes solo se comunican con las puertas de enlace VoIP, IP PBX o SBC que figuren como homólogos SIP de confianza. En algunos casos, si dos puertas de enlace VoIP, PBX IP, o SBCsIP están configuradas para usar la misma dirección IP, se registrará un evento con el Id. 1175. Este evento puede producirse si se han configurado zonas DNS con nombres de dominio completos (FQDN) para las puertas de enlace VoIP en la red. La mensajería unificada protege de las solicitudes no autorizadas recuperando la dirección URL interna del directorio virtual de servicios web de mensajería unificada que se encuentra en el servidor de buzones y, luego, usando dicha dirección URL para crear una lista de FQDN para los homólogos SIP de confianza. Cuando dos FQDN se resuelven con la misma dirección IP, este evento se registra.

Debe reiniciar el servicio de mensajería unificada de MicrosoftExchange si se ha configurado una puerta de enlace IP de mensajería unificada para que use un FQDN y el registro DNS de la puerta de enlace IP de mensajería unificada ha cambiado después de iniciarse el servicio. Si no reinicia el servicio, el servidor de buzones no encontrará la puerta de enlace IP de mensajería unificada. Esto se debe a que los servidores de buzones mantienen una memoria caché para todas las puertas de enlace IP de mensajería unificada que haya en memoria y la resolución de DNS solo se realiza cuando se reinicia el servicio o cuando cambia la configuración de una puerta de enlace VoIP, IP PBX o SBC.

La mensajería unificada de Exchange admite varios proveedores de puertas de enlace VoIP y otros proveedores de IP PBX, PBX habilitadas para SIP y SBC. Las puertas de enlace VoIP admitidas están diseñadas para conectarse a distintos sistemas PBX de terceros.

Para obtener más información sobre las puertas de enlace VoIP, consulte los siguientes temas:

  - [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md)

  - [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Conectar una puerta de enlace VoIP, IP PBX o un controlador de borde de sesión a mensajería unificada](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)

Para obtener información más detallada, consulte [Conecte su sistema de correo de voz a la red de teléfono](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md).

## Paso 4: crear un nuevo grupo de extensiones de mensajería unificada (si es necesario)

Grupo de extensiones es un término empleado para describir un grupo de números de extensión de centrales de conmutación (PBX) o IP PBX que se comparten entre los usuarios. Los grupos de extensiones se usan para distribuir las llamadas de forma eficaz dentro o fuera de una unidad de negocio determinada. Al crear y definir un grupo de extensiones, se reduce la posibilidad de que la persona que efectúe una llamada entrante reciba una señal de línea ocupada cuando se recibe la llamada.

Los grupos de extensiones de mensajería unificada reflejan los grupos de extensiones que se usan en PBX e IP PBX. Al configurar sus PBX o IP PBX, debe crear y configurar uno o más grupos de extensiones de mensajería unificada. Los grupos de extensiones de mensajería unificada actúan como vínculo entre la puerta de enlace IP y el plan de marcado de mensajería unificada.

En función de cómo cree la puerta de enlace IP de mensajería unificada, puede que necesite crear uno o más grupos de extensiones de mensajería unificada. Si no vincula una puerta de enlace IP de mensajería unificada con un plan de marcado al crear la puerta de enlace IP de mensajería unificada, se crea un solo grupo de extensiones de mensajería unificada de manera predeterminada. Si vincula una puerta de enlace IP de mensajería unificada a un plan de marcado de mensajería unificada al crear la puerta de enlace IP, todas las llamadas entrantes se enviarán a través de la puerta de enlace IP de mensajería unificada y los servidores de buzones y de acceso de clientes las aceptarán. Si no vincula una puerta de enlace IP de mensajería unificada a un plan de marcado de mensajería unificada al crear la puerta de enlace IP, deberá crear un grupo de extensiones de mensajería unificada con el identificador piloto correcto para que las llamadas entrantes se reenvíen desde una puerta de enlace IP de mensajería unificada a un plan de marcado.

Si tiene varios números de operadores automáticos y de Outlook Voice Access y ha vinculado una puerta de enlace IP de mensajería unificada a un plan de marcado, deberá eliminar el grupo de extensiones de mensajería unificada que se creó de forma predeterminada y crear varios grupos de extensiones de mensajería unificada. Para obtener más detalles sobre cómo crear un grupo de extensiones de mensajería unificada, consulte [Crear un grupo de extensiones de mensajería unificada](create-a-um-hunt-group-exchange-2013-help.md).

