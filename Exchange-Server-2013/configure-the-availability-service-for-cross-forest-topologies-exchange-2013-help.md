---
title: 'Configurar el servicio de disponibilidad para topologías entre bosques: Exchange 2013 Help'
TOCTitle: Configurar el servicio de disponibilidad para topologías entre bosques
ms:assetid: f1e7d407-f0d3-47a7-8cc3-03c5980445d5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125182(v=EXCHG.150)
ms:contentKeyID: 52062077
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el servicio de disponibilidad para topologías entre bosques

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-10-22_

El servicio de disponibilidad mejora la información de los datos de disponibilidad de los trabajadores y proporciona información de disponibilidad segura, coherente y actualizada a los clientes que ejecutan MicrosoftOutlook. El servicio está instalado de forma predeterminada con Exchange Server 2013. En las topologías entre bosques en las que todos los clientes de conexión ejecutan Outlook, el servicio de disponibilidad es el único método de recuperar la información de disponibilidad. Puede usar el Shell para configurar el servicio de disponibilidad para topologías entre bosques.


> [!NOTE]
> Puede usar el EAC para configurar el servicio de disponibilidad para topologías entre bosques.



## Usar el servicio de disponibilidad en bosques de confianza y que no son de confianza

Puede utilizar el servicio de disponibilidad en las topologías entre bosques en bosques que sean o no de confianza. El tipo de información de disponibilidad que se ofrece depende de si se usa un bosque de confianza o no.

**Bosques de confianza**   En los bosques de confianza, puede configurar el servicio de disponibilidad para recuperar información de disponibilidad usuario por usuario. Cuando el servicio de disponibilidad se configura para recuperar información de disponibilidad usuario por usuario, el servicio podrá hacer solicitudes entre bosques en nombre de un usuario determinado. Esto permite que un usuario en un bosque remoto pueda recuperar información de disponibilidad de alguien que no está en el mismo bosque.

**Bosques que no son de confianza**   En los bosques que no son de confianza, solo puede configurar el servicio de disponibilidad para recuperar información de disponibilidad de la organización en general. Cuando el servicio de disponibilidad hace solicitudes de disponibilidad entre bosques de la organización en su conjunto, se devuelve información de cada usuario de la organización. En el caso de bosques que no son de confianza, es imposible controlar el grado de información de disponibilidad que se devuelve de cada usuario.

## Configuración de Windows para topologías entre bosques

De manera predeterminada, una lista global de direcciones (GAL) contiene destinatarios de correo de un único bosque. Si tiene un entorno entre bosques, le recomendamos que utilice Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) para asegurarse de que la GAL de cualquier bosque determinado contenga los destinatarios de correo de los demás bosques. ILM 2007 FP1 crea usuarios de correo que representan destinatarios de otros bosques, lo que permite, por tanto, que los usuarios los vean en la GAL y envíen correo. Por ejemplo, los usuarios del Bosque A aparecen como un usuario de correo en el Bosque B y viceversa. De este modo, los usuarios del bosque de destino pueden seleccionar el objeto de usuario de correo que representa un destinatario de otro bosque para enviarle correo.

Para habilitar la sincronización de GAL, se crean agentes de administración que importan usuarios con correo habilitado, contactos y grupos de servicios de Active Directory designados dentro de un metadirectorio centralizado. En el metadirectorio, los objetos con correo habilitado se representan como usuarios de correo. Los grupos se representan como contactos sin ninguna pertenencia asociada. Los agentes de administración exportan estos usuarios de correo a una unidad organizativa en el bosque de destino especificado.

## ¿Qué debe saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas de "Permisos del servicio de disponibilidad" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para configurar datos de disponibilidad por usuario en una topología entre bosques de confianza

En este ejemplo se configura el servicio de disponibilidad para recuperar información de disponibilidad por usuario en un servidor de buzón del bosque de destino.

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedrights "ms-Exch-
    EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

En este ejemplo se define el método de acceso de disponibilidad que el servicio de disponibilidad usa en el servidor de buzón local del bosque de origen. El servidor de buzón se configura para acceder a la información de disponibilidad del bosque ContosoForest.com por usuario. En este ejemplo se usa la cuenta de servicio para recuperar datos de disponibilidad.

    Add-AvailabilityAddressSpace -Forestname ContosoForest.com -AccessMethod PerUserFB -UseServiceAccount:$true


> [!NOTE]
> Para configurar la disponibilidad entre bosques bidireccionales, repita estos pasos en el bosque de destino.



Si elige configurar la disponibilidad entre bosques de confianza y utilizar una cuenta de servicio (en lugar de especificar credenciales para toda la organización o por usuario), debe extender permisos como se muestra en el ejemplo de la sección "Usar el Shell para configurar disponibilidad entre bosques de confianza con una cuenta de servicio". Al llevar a cabo ese procedimiento en el bosque de destino se otorga a los servidores de buzón del bosque de origen permiso para serializar el contexto de usuario original.

## Usar el Shell para configurar disponibilidad entre bosques de confianza con una cuenta de servicio

En este ejemplo se configura la disponibilidad entre bosques de confianza con una cuenta de servicio.

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedright "ms-Exch-EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [Get-MailboxServer](https://technet.microsoft.com/es-es/library/bb123539\(v=exchg.150\))

  - [Add-ADPermission](https://technet.microsoft.com/es-es/library/bb124403\(v=exchg.150\))

  - [Add-AvailabilityAddressSpace](https://technet.microsoft.com/es-es/library/bb124122\(v=exchg.150\))

  - [Set-AvailabilityConfig](https://technet.microsoft.com/es-es/library/bb124103\(v=exchg.150\))

## Usar el Shell para configurar datos de disponibilidad de la organización en general en una topología entre bosques que no son de confianza

En este ejemplo se crea una cuenta para toda la organización sobre el objeto de configuración de disponibilidad para configurar el nivel de acceso a datos de disponibilidad en el bosque de destino.

    Set-AvailabilityConfig -OrgWideAccount "Contoso.com\User"

En este ejemplo se agrega el objeto de configuración del espacio de direcciones de disponibilidad para el bosque de origen.

    $a = Get-Credential (Enter the credentials for organization-wide user in Contoso.com domain)
    Add-AvailabilityAddressspace -Forestname Contoso.com -Accessmethod OrgWideFB -Credential:$a

