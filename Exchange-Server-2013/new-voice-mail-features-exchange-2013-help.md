---
title: 'Nuevas características de correo de voz: Exchange 2013 Help'
TOCTitle: Nuevas características de correo de voz
ms:assetid: 89faaa97-3485-4704-a56c-d13632f01e2a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ649002(v=EXCHG.150)
ms:contentKeyID: 49895759
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Nuevas características de correo de voz

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La mensajería unificada (MU) de Microsoft Exchange Server 2013 incluye el mismo conjunto de características que en Exchange 2010 y Exchange 2007, con algunas mejoras y cambios en la arquitectura. Sin embargo, la mensajería unificada ya no es un rol de servidor por separado. Ahora es un componente de las características relacionadas con voz que se ofrecen en Exchange 2013.

## Cambios en la arquitectura de voz

La arquitectura de voz de Exchange 2013 es diferente de la de Exchange 2010 y Exchange 2007. En versiones anteriores de la mensajería unificada de Exchange, todos los componentes de la mensajería unificada se incluían en un servidor que tenía instalado el rol de servidor Mensajería unificada. En Exchange 2013, los componentes de la mensajería unificada están divididos entre un servidor de acceso de cliente que ejecuta el servicio Enrutador de llamadas de mensajería unificada de Microsoft Exchange y un servidor de buzones de correo que ejecuta el servicio de mensajería unificada de Microsoft Exchange. La mayoría de funcionalidades, incluidos los servicios y procesos de trabajo de la mensajería unificada, están ubicados en cada servidor de buzones. El servidor de acceso de cliente, que ejecuta el servicio Enrutador de llamadas de mensajería unificada de Microsoft Exchange, dirige las llamadas entrantes al servidor de buzones de correo. Para obtener información más detallada, consulte [Cambios en la arquitectura de voz](voice-architecture-changes-exchange-2013-help.md).

## Compatibilidad con IPv6

El Protocolo de Internet versión 6 (IPv6) es la versión del Protocolo de Internet (IP) más reciente. IPv6 está diseñado para corregir muchas de las deficiencias de IPv4, que era la versión anterior de IP. Del mismo modo que sucedía con Exchange 2010, los servidores de acceso de cliente y de buzones de correo de Exchange 2013 admiten completamente redes IPv6. Para obtener información más detallada, consulte [Compatibilidad con IPv6 en mensajería unificada](ipv6-support-in-unified-messaging-exchange-2013-help.md).

## Compatibilidad con la API UCMA 4.0

Desde la versión de Exchange 2010 Service Pack 1 (SP1) , el rol de mensajería unificada ha dependido de la API administrada de comunicaciones unificadas v2.0 (UCMA) para la señalización y los medios. Por lo tanto, UCMA 2.0 era un prerrequisito para la configuración de MU de Exchange 2010. Los administradores pueden descargar por separado e implementar manualmente UCMA 2.0 en los servidores de MU que ejecutan Exchange 2010 SP1 o una versión posterior.

Sin embargo, UCMA 2.0 tiene varias limitaciones. Muchos de estos defectos aparecen corregidos por UCMA 4.0, un requisito de Exchange 2013. Ahora que el servidor de MU ya no es un rol de servidor por separado, son los servidores de acceso de cliente y de buzones de correo los que requieren UCMA 4.0.

UCMA 4.0 admite nuevas características en la mensajería unificada, como el uso de la misma versión del motor de conversión de texto a voz (TTS) y el reconocimiento de voz automático (ASR). La plataforma utilizada para Exchange 2013, .NET 4.0, incluye un único archivo instalador y permite la compatibilidad con versiones anteriores de los servidores de MU de Exchange 2010 y de Exchange 2007.

En Exchange 2010 SP2 y SP1, es necesario instalar UCMA 2.0 antes de instalar el service pack en un servidor de mensajería unificada.

El uso de UCMA 4.0 ofrece múltiples ventajas:

  - Incorpora revisiones y parches.

  - Es compatible con IPv6.

  - La implementación de UCMA 4.0 ha sido automatizada y simplificada.

  - La instalación de UCMA 4.0 incluye todos los requisitos previos para la implementación de Exchange 2013.

  - UCMA 4.0 proporciona traducciones de motor de voz más precisas y soporte de plataforma de voz más escalable en varios productos.


> [!NOTE]
> UCMA 4.0 se instala al instalar Exchange&nbsp;2013. Para obtener más información acerca de UCMA 4.0 y los requisitos de configuración, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</A>. Para actualizar a la versión más reciente de UCMA, primero debe desinstalar las versiones anteriores de UCMA que se hayan instalado mediante Agregar o quitar programas.



## Mejoras en la vista previa del correo de voz

Algunas de las mejoras en los servicios relacionados con voz se incluyen en la MU de Exchange Server 2013 a través del Motor de voz 11.0 y UCMA 4.0. Ha habido mejoras en la generación de gramática, los servicios de voz principales y el soporte para varios idiomas. La MU de Exchange Server 2013 también incluye varias mejoras de los servicios de transcripción que se entregan a los usuarios finales, así como también ha aumentado la confianza y precisión de la Vista previa de correo de voz. Para obtener información más detallada, consulte [Mejoras de vista previa del correo de voz](voice-mail-preview-enhancements-exchange-2013-help.md).

## Compatibilidad mejorada con identificador de llamada

En versiones anteriores de la mensajería unificada de Exchange, un servidor de MU que recibía una llamada usaba el identificador de llamada para buscar la posible identidad de la persona que llamaba. Esta búsqueda se extendía a Active Directory y los contactos personales del usuario de mensajería unificada se almacenaban en su buzón de correo.

Anteriormente, a veces los usuarios sufrían fallos en el sistema de correo de voz para identificar a los contactos de Exchange o personales desde su identificador de autor de llamada. Hasta ahora, únicamente se usaba la carpeta de contactos predeterminados del buzón de Exchange de un usuario para realizar esta búsqueda. Ahora, hay mayor probabilidad de que los usuarios de Exchange Server 2013 tengan contactos agregados de redes sociales externas o contactos agregados a carpetas exclusivas que generan para organizar sus contactos. En Exchange 2013, la MU amplía el ámbito de búsqueda para incluir las demás carpetas de contactos de Exchange y personales del usuario que se crearon manualmente. Exchange 2013 también admite la adición de contactos desde redes sociales externas, ofrece inteligencia para vincular múltiples contactos que hacen referencia a la misma persona y usa dichos datos para presentar vistas centradas en las personas (en lugar de centrarse en los contactos). Esto significa que los contactos añadidos desde redes sociales externas se pueden colocar en la carpeta de contactos almacenada en el buzón del usuario en Microsoft Outlook Web App y Outlook. Dichos contactos también se pueden añadir a cualquier carpeta de contactos adicional que cree el usuario.

La búsqueda de identificadores de llamada se integra en la agregación de contactos, con el fin de que se busque en los contactos externos. La propiedad **PersonID**, en los casos en que está presente y establecida con un valor no nulo, se usará para mejorar la experiencia del usuario para la resolución del identificador de llamada mediante la supresión de coincidencias duplicadas en los contactos asociadas a la misma persona. Dado que la propiedad PersonID es la misma en ambos resultados, la mensajería unificada trata esto como una coincidencia de un solo contacto.

## Mejoras en la plataforma de voz y el reconocimiento de voz

La mensajería unificada de Exchange Server 2013 presenta ciertas mejoras en la plataforma de voz y el reconocimiento de voz, entre las que se incluyen:

  - Mejoras y precisión mejorada para la vista previa del correo de voz.

  - Compatibilidad con la [plataforma de voz de Microsoft, en tiempo de ejecución (versión 11.0)](https://go.microsoft.com/fwlink/p/?linkid=253196).

  - Generación de gramática de voz mediante el buzón del sistema para una organización.

La mensajería unificada de Exchange utiliza una gramática estática y dinámica para reconocer comandos, nombres de contactos en la lista global de direcciones (LGD) y nombres de contactos personales en el buzón del usuario. Actualmente, en Exchange Server 2013 todos los servidores de buzones que ejecutan el servicio de mensajería unificada de Microsoft Exchange generan gramáticas para todos los idiomas de MU instalados y las almacenan en directorios. Los servidores de buzones almacenan todas las gramáticas posibles, que se generan según el número de planes de marcado, operadores automáticos e idiomas de mensajería unificada instalados.

La MU utiliza los archivos de gramáticas para permitir que los autores de llamadas utilicen la voz para ubicar a los usuarios de la organización. Los archivos se actualizan cada 24 horas mediante el Asistente de buzones de correo. El comando GGG.exe de Exchange 2007 y Exchange 2010 permiten la actualización manual de los archivos de gramáticas sin tener que esperar a la actualización programada. En Exchange Server 2013, para solucionar los problemas de escalabilidad de generación de gramática de ASR para mensajería unificada, la generación de gramáticas de la LGD de voz ya no se genera en el servidor con el rol de servidor de mensajería unificada instalado. En su lugar, se realiza periódicamente a través del asistente de buzones, en el servidor de buzones que ejecuta el servicio de mensajería unificada de Microsoft Exchange que hospeda el buzón de arbitraje de la organización. En su ligar, el archivo de gramática de voz de la LGD se almacena en el buzón de arbitraje de una organización y se descarga posteriormente en todos los servidores de buzones de correo de la organización de Exchange. De forma predeterminada, el asistente de buzones se ejecuta cada 24 horas. Puede ajustar la frecuencia con el cmdlet **Set-MailboxServer**.

## Actualizaciones de cmdlet

Muchos de los cmdlets de la MU en Exchange 2013 provienen de Exchange 2010. Sin embargo, ha habido cambios en algunos cmdlets y se han añadido otros nuevos para aportar una nueva funcionalidad. Para obtener información más detallada, consulte [Actualizaciones de cmdlet de mensajería unificada](unified-messaging-cmdlet-updates-exchange-2013-help.md).

