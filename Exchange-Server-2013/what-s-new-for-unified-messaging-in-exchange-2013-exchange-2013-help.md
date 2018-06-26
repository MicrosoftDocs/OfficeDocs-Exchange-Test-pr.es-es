---
title: 'Novedades de mensajería unificada en Exchange 2013: Exchange 2013 Help'
TOCTitle: Novedades de mensajería unificada en Exchange 2013
ms:assetid: a444ef2d-d893-408e-adf9-c9d8a8b07593
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150545(v=EXCHG.150)
ms:contentKeyID: 48268506
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Novedades de mensajería unificada en Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

En Microsoft Exchange Server 2013, estamos mejorando versiones anteriores de Exchange introduciendo nuevas funciones y cambios arquitectónicos. La mensajería unificada (UM) de Exchange 2013 incluye el mismo conjunto de funciones que Exchange 2010 y Exchange 2007, pero la mensajería unificada no es una función de servidor independiente. Ahora es un componente de las funciones relacionadas con la voz que se ofrecen en Exchange 2013.

## Cambios en la arquitectura de voz

La arquitectura de Exchange 2013 es diferente de la de Exchange 2010 y Exchange 2007. En versiones anteriores de la mensajería unificada de Exchange, todos los componentes de la mensajería unificada se incluían en un servidor que tenía instalado el rol de servidor Mensajería unificada. En Exchange 2013, todos los componentes de mensajería unificada se dividen entre un servidor de acceso de clientes que ejecuta el servicio de Enrutador de llamada de mensajería unificada de Microsoft Exchange y un servidor de buzón de correo que ejecuta el servicio de mensajería unificada de Microsoft Exchange. Todas las funciones, incluidos los servicios y procesos de trabajo para mensajería unificada, se ubican en cada servidor de buzón de correo, con la excepción del servidor de acceso de clientes que ejecuta el servicio Enrutador de llamada de mensajería unificada de Microsoft Exchange, que pone en proxy todas las llamadas entrantes en el servidor de buzón de correo. Para obtener información más detallada, consulte [Cambios en la arquitectura de voz](voice-architecture-changes-exchange-2013-help.md).

## Compatibilidad con IPv6

El Protocolo de Internet versión 6 (IPv6) es la versión del Protocolo de Internet más reciente. IPv6 está diseñado para corregir muchas de las deficiencias de IPv4, que era la versión anterior de IP. Del mismo modo que con Exchange 2010, los servidores Buzón de correo y Acceso de clientes de Exchange 2013 son totalmente compatibles con las redes IPv6. Para obtener información más detallada, consulte [Compatibilidad con IPv6 en mensajería unificada](ipv6-support-in-unified-messaging-exchange-2013-help.md).

## Compatibilidad con la API UCMA 4.0

A partir de Exchange 2010 Service Pack 1, el rol del servidor Mensajería unificada dependía de API administrado de comunicaciones unificadas v2.0 (UCMA) para la señalización y los medios. Por lo tanto, UCMA 2.0 es un requisito para la configuración de la mensajería unificada de Exchange 2010. Los administradores descargan UCMA 2.0 forma separa y lo implementan de forma manual en servidores de mensajería unificada que ejecutan Exchange 2010 SP1 o posterior. Para Exchange 2013, se requiere UCMA 4.0. Sin embargo, dado que el servidor de mensajería unificada no es un rol de servidor separado en Exchange 2013, ahora los servidores de acceso de clientes y buzón de correo requieren UCMA 4.0.

UCMA 4.0 admite nuevas características en la mensajería unificada, como el uso de la misma versión del motor de conversión de texto a voz (TTS) y el reconocimiento de voz automático (ASR). La plataforma utilizada para Exchange 2013, .NET 4.0, incluye un único archivo instalador y habilitará la compatibilidad con versiones anteriores de servidores de mensajería unificada de Exchange 2010 y Exchange 2007.

En Exchange 2010 SP2 y SP1, es necesario instalar UCMA 2.0 antes de instalar el service pack en un servidor de mensajería unificada. No obstante, UCMA 2.0 presentaba las siguientes limitaciones. UCMA 4.0 corrige muchas de las deficiencias. En Exchange Server 2013, la mensajería unificada seguirá utilizando UCMA. Sin embargo, el paso a la versión más reciente de UCMA proporciona estos beneficios:

  - La versión más reciente de UCMA incorpora revisiones y parches.

  - UCMA requiere .NET 4.0, que es la plataforma que utilizará Exchange Server 2013. (UCMA 2.0 no es compatible con .NET 4.0.)

  - UCMA 4.0 es compatible con IPv6.

  - Implementación simplificada y automatizada de UCMA 4.0. Exchange 2013 El programa de instalación realiza una comprobación individual para UCMA 4.0.

  - La instalación de UCMA 4.0 incluye todos los requisitos previos para Exchange 2013.


> [!NOTE]
> UCMA 4.0 se instala al instalar Exchange&nbsp;2013. Para obtener más información sobre UCMA 4.0 y los requisitos de configuración, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</A>. Para actualizar a la versión más reciente de UCMA, primero debe desinstalar las versiones anteriores de UCMA que se hayan instalado mediante Agregar o quitar programas.



## Mejoras en la vista previa del correo de voz

Se ofrecen algunas mejoras de servicios relacionados con la voz en la mensajería unificada de Exchange Server 2013 a través del motor de voz 11.0 y UCMA 4.0. Se incluyen mejoras lingüísticas y de generación de gramática. Además, la mensajería unificada de Exchange Server 2013 incluye varias mejoras en la interfaz del usuario y mejoras para aumentar la confianza y la precisión de la Vista previa de correo de voz. Para obtener información más detallada, consulte [Mejoras de vista previa del correo de voz](voice-mail-preview-enhancements-exchange-2013-help.md).

## Compatibilidad mejorada con identificador de llamada

En versiones anteriores de mensajería unificada de Exchange, un servidor de mensajería unificada que tomaba una llamada usaba el identificador de llamada para intentar buscar la identidad de la persona que llama. Esta búsqueda se extendía a Active Directory y los contactos personales del usuario de mensajería unificada almacenados en sus buzones.

A los usuarios de Exchange les suelen aburrir la incapacidad para identificar los contactos personales o de Exchange desde su Id. de llamada. Hasta ahora, solo se usaba la carpeta de contactos por defecto de mensajería unificada de Exchange para la búsqueda. Pero los usuarios de Exchange Server 2013 probablemente hayan agregado contactos desde redes sociales externas o contactos en carpetas únicas que los usuarios han creado de forma manual. Exchange 2013 admite agregar contactos desde redes sociales externas, proporciona inteligencia para enlazar múltiples contactos que se refieren a la misma persona, y utiliza esos datos para presentar vistas centradas en personas (en lugar de contactos). Los contactos que se agregan desde redes externas se ubican en carpetas de contactos junto con otras carpetas de contactos adicionales que hayan creado los usuarios. Las características de mensajería unificada de Exchange 2013 amplían el alcance de la búsqueda para incluir las demás carpetas de contactos personales y de Exchange que tenga el usuario y que haya creado manualmente.

La búsqueda de identificadores de llamada se integra en la agregación de contactos, con el fin de que se busque en los contactos externos. La propiedad PersonID, en los casos en que está presente y con un valor no nulo, mejora la experiencia del usuario para la resolución del identificador de llamada mediante la supresión de coincidencias duplicadas en los contactos asociadas a la misma persona. Dado que la propiedad PersonID es la misma en ambos resultados, la mensajería unificada trata esto como una coincidencia de un solo contacto.

## Mejoras en la plataforma de voz y el reconocimiento de voz

La mensajería unificada de Exchange Server 2013 presenta ciertas mejoras en la plataforma de voz y el reconocimiento de voz que incluye:

  - Mejoras y precisión mejorada para la vista previa del correo de voz.

  - Compatibilidad con [Microsoft Speech Platform – Runtime (Versión 11.0)](https://go.microsoft.com/fwlink/p/?linkid=253196).

  - Generación de gramática de voz mediante el buzón del sistema para una organización.

La mensajería unificada de Exchange utiliza gramáticas de voz dinámicas y estáticas para reconocer comandos, nombres de contactos en la lista global de direcciones y nombres de contactos personales en el buzón del usuario. Actualmente, en Exchange Server 2013 todos los servidores de buzones que ejecutan el servicio de mensajería unificada de Microsoft Exchange generan gramáticas para los idiomas de mensajería unificada instalados y las almacenan en directorios. Los servidores de buzones almacenan todas las gramáticas posibles, que se generan según el número de planes de marcado, operadores automáticos e idiomas de mensajería unificada instalados.

Los archivos de gramática se usan como entradas para el proceso de reconocimiento de voz y se generan en forma periódica. El comando GGG.exe en Exchange 2007 y Exchange 2010 permitía actualizar manualmente los archivos de gramática sin esperar la actualización programada. En Exchange Server 2013, para solucionar los problemas de escalabilidad de generación de gramática de ASR para mensajería unificada, la generación de gramática LGD de voz ya no tiene lugar en el servidor con el rol de servidor de mensajería unificada instalado. En su lugar, se realiza periódicamente a través del asistente de buzones, en el servidor de buzones que ejecuta el servicio de mensajería unificada de Microsoft Exchange que hospeda el buzón de arbitraje de la organización. El archivo de gramática de voz de LGD se almacena en el buzón de arbitraje de una organización y posteriormente se descarga en todos los servidores Buzón de correo de la organización de Exchange. De forma predeterminada, el asistente de buzones se ejecuta cada 24 horas. Puede configurar la frecuencia usando el cmdlet **Set-MailboxServer**.

## Actualizaciones de cmdlet

Para Exchange 2013, se trajeron varios cmdlets de mensajería unificada de Exchange 2010 pero se realizaron cambios en algunos de ellos y se agregaron nuevos cmdlets para funciones nuevas. Para obtener información más detallada, consulte [Actualizaciones de cmdlet de mensajería unificada](unified-messaging-cmdlet-updates-exchange-2013-help.md).

