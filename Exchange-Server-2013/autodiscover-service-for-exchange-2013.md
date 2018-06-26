---
title: 'Servicio Detección automática: Exchange 2013 Help'
TOCTitle: Servicio Detección automática
ms:assetid: b03c0f21-cbc2-4be8-ad03-73a7dac16ffc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124251(v=EXCHG.150)
ms:contentKeyID: 50556858
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servicio Detección automática

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Obtenga más información sobre el servicio Detección automática de Exchange para Microsoft Exchange 2013. Aprenderá qué hace y cómo funciona el servicio Detección automática de Exchange y cuáles son las opciones de implementación.

MicrosoftExchange 2013 incluye un servicio denominado Detección automática. En este tema se proporciona información general sobre el servicio y se explica cómo funciona, cómo configura los clientes de Outlook y qué opciones hay para implementar el servicio Detección automática en un entorno de mensajería.

El servicio Detección automática hace lo siguiente:

  - Configura automáticamente la configuración de perfil de usuario para los clientes que ejecuten MicrosoftOffice Outlook 2007, Outlook 2010 o Outlook 2013, así como los teléfonos móviles admitidos. Se admiten los teléfonos que ejecuten Windows Mobile 6.1 o una versión posterior. Si un teléfono no es Windows Mobile, consulte la documentación correspondiente para comprobar si es compatible.

  - Proporciona acceso a las características de Exchange para los clientes de Outlook 2007, Outlook 2010 o Outlook 2013 que estén conectados al entorno de mensajería de Exchange.

  - Utiliza la dirección de correo electrónico y la contraseña de un usuario para proporcionar la configuración de perfiles a clientes de Outlook 2007, Outlook 2010 o Outlook 2013 y a teléfonos móviles compatibles. Si el cliente de Outlook está unido a un dominio, se utiliza la cuenta de dominio del usuario.

**Contenido**

Introducción al servicio Detección automática

Cómo funciona el servicio Detección automática

Opciones de implementación del servicio Detección automática

Configuración de la Detección automática para movimientos entre bosques

## Introducción al servicio Detección automática

El servicio Detección automática facilita la configuración de Outlook 2007, Outlook 2010 o Outlook 2013 y de otros teléfonos móviles. Este servicio no se puede usar con versiones de Outlook anteriores a Office Outlook 2007. En las versiones anteriores de Microsoft Exchange (Exchange 2003 SP2 o anteriores) y Outlook (Outlook 2003 o anteriores), había que configurar manualmente todos los perfiles de usuario para tener acceso a Exchange. Si se producían cambios en el entorno de mensajería, era necesario realizar un trabajo adicional para administrar dichos perfiles. De lo contrario, los clientes de Outlook dejaban de funcionar correctamente.

Con el servicio Detección automática, Outlook encuentra un nuevo punto de conexión formado por el GUID del buzón del usuario + @ + la parte del dominio de la dirección SMTP principal del usuario. El servicio Detección automática devuelve la siguiente información al cliente:

  - El nombre para mostrar del usuario

  - Configuraciones de conexión independientes para conectividad interna y externa

  - La ubicación del servidor de buzones del usuario

  - La dirección URL de diversas características de Outlook que rigen cierta funcionalidad, como la información de disponibilidad, la mensajería unificada y la libreta de direcciones sin conexión

  - Configuración del servidor de Outlook Anywhere

Cuando cambia la información de un usuario de Exchange, Outlook reconfigura automáticamente el perfil del usuario mediante el servicio Detección automática. Por ejemplo, si se mueve el buzón de correo de un usuario o el cliente no consigue conectarse al buzón del usuario o a las características disponibles de Exchange, Outlook se pone en contacto con el servicio Detección automática y actualiza automáticamente el perfil del usuario de forma que contenga la información necesaria para conectarse con el buzón de correo y las características de Exchange.

Volver al principio

## Cómo funciona el servicio Detección automática

Al instalar un servidor de acceso de clientes en Exchange 2013, se crea un directorio virtual predeterminado llamado Detección automática en el sitio web predeterminado en Internet Information Services (IIS). Este directorio virtual controla las solicitudes del servicio Detección automática por parte de los clientes de Outlook 2007, Outlook 2010 y Outlook 2013 y de teléfonos móviles compatibles, en las circunstancias siguientes:

  - Cuando se configura o actualiza una cuenta de usuario

  - Cuando un cliente de Outlook comprueba periódicamente si hay cambios en las URL de los servicios Web Exchange

  - Cuando se producen cambios de conexión a la red subyacente en el entorno de mensajería de Exchange

Asimismo, se crea un nuevo objeto de Active Directory denominado punto de conexión de servicio (SCP) en el servidor en el que se instala el servidor de acceso de clientes.

El objeto SCP contiene la lista autorizada de direcciones URL del servicio Autodiscover del bosque. Puede utilizar el cmdlet **Set-ClientAccessServer** para actualizar el objeto SCP. Para obtener más información, consulte [Set-ClientAccessServer](https://technet.microsoft.com/es-es/library/bb125157\(v=exchg.150\)).


> [!IMPORTANT]
> Antes de ejecutar el cmdlet <STRONG>Set-ClientAccessServer</STRONG>, asegúrese de que la cuenta Usuarios autenticados del servidor de acceso de cliente tiene permisos de lectura para el objeto SCP. Si los usuarios no tienen los permisos correctos, no pueden buscar elementos ni leerlos.



Para obtener más información acerca de los objetos SCP, vea [Publicar puntos de conexión de servicio](https://go.microsoft.com/fwlink/p/?linkid=72744).

Para el acceso externo, o mediante DNS, el cliente busca el servicio Detección automática en Internet utilizando la dirección de dominio SMTP principal desde la dirección de correo electrónico del usuario.


> [!NOTE]
> Es necesario proporcionar un registro de recurso de servicio de host (SRV) en DNS para que los clientes de Outlook&nbsp;detecten el servicio Detección automática mediante&nbsp;DNS. Para obtener más información, consulte la documentación de Windows sobre la configuración de DNS, y el <A href="https://go.microsoft.com/fwlink/p/?linkid=85214">documento: Servicio de detección automática de Exchange 2007</A>.



En función de si se ha configurado el servicio Detección automática en un sitio separado o no, la URL del servicio Detección automática será https://\<*smtp-address-domain*\>/autodiscover o https://autodiscover.\<*smtp-address-domain*\>/autodiscover/autodiscover.xml, donde ://\<*smtp-address-domain*\> es la dirección del dominio SMTP principal. Por ejemplo, si la dirección de correo electrónico del usuario es tony@contoso.com, la dirección principal del dominio SMTP es contoso.com. Cuando el cliente se conecte a Active Directory, buscará el objeto SCP creado durante la instalación. En implementaciones que incluyen varios servidores de acceso de cliente, se crea un objeto SCP para cada uno de estos servidores. El objeto SCP contiene el atributo *ServiceBindingInfo* con el nombre de dominio completo (FQDN) del servidor de acceso de cliente con el formato https://CAS01/autodiscover/autodiscover.xml, donde CAS01 es el nombre de dominio completo del servidor de acceso de cliente. Al utilizar las credenciales del usuario, el cliente de Outlook 2007, Outlook 2010 o Outlook 2013 se autentica en Active Directory y busca los objetos SCP de la detección automática. Cuando el cliente obtiene y enumera las instancias del servicio Detección automática, se conecta al primer servidor de acceso de cliente de la lista enumerada y obtiene la información de perfil en forma de datos XML que necesita para conectarse al buzón de correo del usuario y a las características disponibles de Exchange.

Volver al principio

## Opciones de implementación del servicio Detección automática

El servicio Detección automática debe implementarse y configurarse correctamente para que los clientes de Outlook 2007, Outlook 2010 y Outlook 2013 se conecten automáticamente a las características de Exchange, como la libreta de direcciones sin conexión, el servicio de disponibilidad y la mensajería unificada (UM). La implementación del servicio Detección automática es sólo uno de los pasos para asegurar el acceso a los servicios de Exchange, como el servicio de disponibilidad, por parte de los clientes de Outlook 2007, Outlook 2010 o Outlook 2013.

## Configuración de la Detección automática para movimientos entre bosques

El servicio Detección automática puede proporcionar información sobre perfiles de usuario a clientes de Outlook que se conectan para tener acceso a buzones de correo que se han movido de un bosque de Exchange a otro. Para que esto ocurra, debe configurar un usuario habilitado para buzones en el bosque original donde reside el buzón del usuario y en el bosque de destino mediante el cmdlet **New-MailUser**. En el bosque original, utilice el parámetro *ExternalEmailAddress* en el cmdlet para especificar la nueva dirección de correo electrónico del buzón en el bosque de destino. Para obtener más información, consulte [New-MailUser](https://technet.microsoft.com/es-es/library/aa996335\(v=exchg.150\)).

Cuando configure un usuario habilitado para correo, el servicio Detección automática del bosque original redirigirá el usuario que se está autenticando a la nueva dirección de correo electrónico del bosque de destino. A continuación, el cliente de Outlook que se está conectando será redirigido al servidor de acceso de cliente del bosque de destino al que se ha movido el buzón de correo.

Volver al principio

