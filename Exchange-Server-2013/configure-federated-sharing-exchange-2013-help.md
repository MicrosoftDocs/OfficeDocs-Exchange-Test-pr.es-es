---
title: 'Configuración del uso compartido federado: Exchange 2013 Help'
TOCTitle: Configuración del uso compartido federado
ms:assetid: b25ae450-def3-4797-a5fc-6e9bcee71a5d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657483(v=EXCHG.150)
ms:contentKeyID: 49895848
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración del uso compartido federado

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Con el uso compartido federado en Exchange Server 2013, los usuarios pueden compartir información con los destinatarios en las organizaciones federadas externas. Esto incluye el uso compartido de la información de disponibilidad (también conocida como disponibilidad del calendario) para finalidad de programación o, según la naturaleza de la relación comercial, el uso compartido de información del calendario más detallada. Para obtener más información acerca del uso compartido federado, consulte [Uso compartido](sharing-exchange-2013-help.md).


> [!IMPORTANT]
> Esta característica de Exchange Server 2013 no es totalmente compatible con Office 365 operado por 21Vianet en China y pueden aplicarse ciertas limitaciones en las características. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/?linkid=313640">Acerca de Office 365 operado por 21Vianet</A>.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 1 hora.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Crear y configurar una confianza de federación

Una confianza de federación establece una relación de confianza ente una organización de Exchange 2013 y el sistema de autenticación de Azure Active Directory y es un requisito del uso compartido federado.

Para obtener instrucciones detalladas, consulte [Configurar una confianza de federación](configure-a-federation-trust-exchange-2013-help.md).

## Paso 2: Crear una relación de organización

Una relación de organización permite a los usuarios de su organización de Exchange compartir información de disponibilidad de calendario como parte del uso compartido federado con otras organizaciones federadas de Exchange. El uso compartido federado se puede configurar entre dos organizaciones federadas Exchange 2013 o entre una organización federada Exchange 2013 y organizaciones federadas Exchange 2010.

Para obtener instrucciones detalladas, consulte [Crear una relación de organización](create-an-organization-relationship-exchange-2013-help.md).

## Paso 3: Crear una directiva de uso compartido

Compartir directivas permite compartir información de calendario establecida por los usuarios de persona a persona con diferentes tipos de usuarios externos. Permiten compartir información de contacto y de calendario con organizaciones federadas externas, organizaciones no federadas externas e individuos con acceso a Internet. Si no necesita configurar el uso compartido entre personas o contactos (solamente el uso compartido a nivel de la organización), no necesita configurar una directiva de uso compartido.

Para obtener instrucciones detalladas, consulte [Crear una directiva de uso compartido](create-a-sharing-policy-exchange-2013-help.md).

## Paso 4: Configurar un registro DNS público de detección automática

Debe agregar un registro de recurso de nombre canónico de alias (CNAME) a su DNS público. El nuevo registro CNAME debe apuntar a un servidor de acceso de cliente Exchange 2013 orientado a Internet que esté ejecutando el servicio de detección automática.

Para obtener instrucciones detalladas sobre cómo agregar registros CNAME, consulte el servicio de host de los registros de DNS públicos. Generalmente es un servicio basado en Internet que también puede hospedar su sitio web de dominio.

