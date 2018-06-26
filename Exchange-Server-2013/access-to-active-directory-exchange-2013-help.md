---
title: 'Acceso a Active Directory: Exchange 2013 Help'
TOCTitle: Acceso a Active Directory
ms:assetid: 61080b45-8bce-4c23-b744-ed264d5f0b7d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998561(v=EXCHG.150)
ms:contentKeyID: 49895664
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Acceso a Active Directory

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Microsoft Exchange Server 2013 almacena toda la información de configuración y destinatario en la base de datos del servicio de directorio de Active Directory. Cuando un equipo en el que se ejecuta Exchange 2013 necesita información sobre los destinatarios y la configuración de la organización de Exchange, este debe consultar a Active Directory para tener acceso a la información. Los servidores de Active Directory tienen que estar disponibles para que Exchange 2013 funcione correctamente.

En este tema, se explica cómo Exchange 2013 almacena y recupera información en Active Directory de modo que pueda planear el acceso a Active Directory. Además, se analizan problemas que debe tener en cuenta si intenta recuperar objetos de Exchange 2013 Active Directory eliminados.

## Información de Exchange almacenada en Active Directory

La base de datos de Active Directory almacena información en tres tipos de particiones lógicas, que se describen en las siguientes secciones:

  - Partición de esquema

  - Partición de configuración

  - Partición de dominio

## Partición de esquema

La partición de esquema almacena dos tipos de información:

  - Las **clases de esquema** definen todos los tipos de objetos que se pueden crear y almacenar en Active Directory.

  - Los **atributos de esquema** definen todas las propiedades que se pueden usar para describir los objetos que se almacenan en Active Directory.

Cuando se instala el primer rol del servidor de Exchange 2013 en el bosque o se ejecuta el proceso de preparación de Active Directory, el proceso de preparación de Active Directory agrega varias clases y atributos al esquema de Active Directory. Las clases que se agregan al esquema se usan para crear objetos específicos de Exchange, como agentes y conectores. Los atributos que se agregan al esquema se usan para configurar los objetos específicos de Exchange y los usuarios y grupos habilitados para correo. Estos atributos incluyen propiedades, tales como la configuración de MicrosoftOffice Outlook Web Access y la configuración de mensajería unificada de MicrosoftExchange. Cada controlador de dominio y servidor de catálogo global del bosque contiene una réplica completa de la partición del esquema.

Para obtener más información acerca de las modificaciones del esquema en Exchange 2013, consulte [Cambios en el esquema de Active Directory de Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

## Partición de configuración

La partición de configuración almacena información acerca de la configuración de todo el bosque. Esta información de configuración incluye la configuración de sitios Active Directory, configuración global de Exchange, configuración de transporte y directivas de buzón de correo. Cada tipo de información de configuración se almacena en un contenedor de la partición de configuración. La información de configuración de Exchange se almacena en una subcarpeta, bajo el contenedor de servicios de la partición de la configuración. La información que se almacena en este contenedor incluye lo siguiente:

  - Listas de direcciones

  - Directivas de buzones de libretas de direcciones

  - Grupos administrativos

  - Configuración de acceso de cliente

  - Conexiones

  - Configuración de buzones móviles

  - Configuración global

  - Configuración de supervisión

  - Directivas del sistema

  - Contenedor de directivas de retención

  - Configuración de transporte

Cada controlador de dominio y servidor de catálogo global del bosque contiene una réplica completa de la partición de configuración.

## Partición de dominio

La partición de dominio almacena información en contenedores predeterminados y en unidades organizativas que crea el administrador de Active Directory. Estos contenedores contienen los objetos específicos del dominio. Estos datos incluyen objetos del sistema de Exchange e información acerca de equipos, usuarios y grupos de ese dominio. Cuando Exchange 2013 está instalado, Exchange actualiza los objetos de esta partición para admitir la funcionalidad de Exchange. Esta funcionalidad afecta a cómo se almacena la información del destinatario y cómo se obtiene acceso a ella.

Cada controlador de dominio contiene una réplica completa de la partición del dominio para el que está autorizado. Cada servidor de catálogo global del bosque contiene un subconjunto de la información en cada partición de dominio del bosque.

## Cómo obtiene acceso Exchange 2013 a la información en Active Directory

Exchange 2013 usa una API de Active Directory para obtener acceso a la información que se almacena en Active Directory. El servicio de topología de Microsoft ExchangeActive Directory se ejecuta en todos los roles del servidor de Exchange 2013. Este servicio lee la información de todas las particiones de Active Directory. La información recuperada se guarda en caché y los servidores de Exchange 2013 la usan para detectar la ubicación del sitio de Active Directory de todos los servicios de Exchange de la organización.

Para obtener más información acerca de la topología y la detección del permiso, consulte [Planeamiento de uso de Active Directory para el enrutamiento de correo](planning-to-use-active-directory-sites-for-routing-mail-exchange-2013-help.md).

Exchange 2013 es una aplicación preparada para sitios de Active Directory que prefiere comunicarse con los servidores de directorio situados en el mismo sitio que el servidor de Exchange para optimizar el tráfico de la red. Cada rol del servidor organizativo de Exchange 2013 tiene que comunicarse con Active Directory para recuperar información acerca de los destinatarios y de los otros roles del servidor de Exchange 2013. En las siguientes secciones se describen los datos que obtiene cada función del servidor.

De forma predeterminada, siempre que se inicia un servidor de Exchange 2013, este se enlaza con un controlador de dominio y un servidor de catálogo global seleccionados aleatoriamente en su propio sitio. Para ver los servidores del directorio seleccionado, use el cmdlet **Get-ExchangeServer** en el Shell de administración de Exchange. También puede usar el cmdlet **Set-ExchangeServer** para configurar una lista estática de controladores de dominio a los que se debe enlazar un servidor de Exchange 2013 o una lista de controladores de dominio que se deben excluir.


> [!IMPORTANT]
> Un controlador de dominio de Windows Server 2008 se puede configurar como servidor de directorio de solo lectura. Esta configuración resulta útil si desea implementar un controlador de dominio o un servidor de catálogo global en un sitio remoto para fines de autenticación y autorización, pero no desea que los administradores de ese sitio puedan escribir cambios en Active Directory. No obstante, no podrá implementar un servidor de Exchange&nbsp;2013 en sitios que contengan servidores de directorio de solo lectura.



## Rol de servidor Buzón de correo

La función del servidor Buzón almacena información de configuración acerca de los usuarios y almacenes del buzón en Active Directory. Además, en Exchange 2013, el servidor de buzones incluye todos los componentes de servidor habituales incluidos en Exchange 2010: los protocolos de acceso de clientes, el servicio de transporte, las bases de datos de buzones y la mensajería unificada. El servidor de buzones administra la actividad de los buzones activos de ese servidor.

## Rol de servidor Acceso de clientes

En Exchange 2013, el servidor de acceso de clientes proporciona servicios de proxy, de autenticación y de redirección limitada. El servidor de acceso de clientes como tal no realiza ninguna representación de datos. El servidor Acceso de clientes es un servidor fino y sin estado. Nunca se encuentra nada en cola o almacenado en el servidor Acceso de clientes. El servidor de acceso de clientes ofrece todos los protocolos de acceso de clientes habituales: HTTP, POP e IMAP y SMTP.

## Recuperación de objetos eliminados de Exchange

La Papelera de reciclaje de Active Directory ayuda a minimizar el tiempo de inactividad del servicio de directorio mediante la mejora de la capacidad para conservar y recuperar los objetos de Active Directory eliminados por error sin necesidad de restaurar datos de Active Directory desde copias de seguridad, reiniciar los Servicios de dominio de Active Directory (AD DS) ni reiniciar los controladores de dominio.

Lo más importante que es necesario comprender acerca de la recuperación de objetos eliminados de Exchange relacionados con Active Directory es que los objetos de Exchange no existen de forma aislada. Por ejemplo, cuando se habilita un usuario para correo, se calculan varias directivas y vínculos distintos para el usuario sobre la base de la configuración de Exchange actual. Dos problemas que pueden surgir cuando se restaura una configuración de Exchange o un objeto de destinatario eliminados son los siguientes:

  - **Colisiones**   Algunos atributos de Exchange deben ser únicos en un bosque. Por ejemplo, las direcciones proxy (correo electrónico) no deben ser las mismas para dos usuarios distintos. Active Directory no exige el cumplimiento de la unicidad de las direcciones proxy, ya que las herramientas administrativas de Exchange comprueban la unicidad. Las directivas de direcciones de correo electrónico de Exchange también resuelven de forma automática los conflictos posibles en la asignación de direcciones proxy en función de reglas deterministas. Por lo tanto, es posible restaurar un objeto de usuario de Exchange y, como resultado, generar una colisión con las direcciones proxy o con otros atributos que deben ser únicos.

  - **Errores de configuración**   Exchange cuenta con reglas automáticas que asignan diversas directivas o configuraciones. Si elimina un destinatario y, a continuación, cambia las reglas o las directivas, la restauración de un objeto de usuario de Exchange puede dar como resultado que se asigne un usuario a la directiva incorrecta (o incluso a una directiva que ya no existe).

Las instrucciones a continuación le ayudarán a minimizar los problemas que pueden surgir durante la recuperación de objetos eliminados relacionados con Exchange:

  - Si eliminó un objeto de configuración de Exchange mediante las herramientas de administración de Exchange, no restaure el objeto. En su lugar, vuelva a crear el objeto mediante las herramientas de administración de Exchange (el Centro de administración de Exchange o el Shell de administración de Exchange).

  - Si eliminó un objeto de configuración de Exchange sin usar las herramientas de administración de Exchange, recupere el objeto tan pronto como sea posible. Cuantos más cambios administrativos y de configuración se realicen en el sistema desde la eliminación, mayor probabilidad habrá para que la restauración de los objetos dé como resultado errores de configuración.

  - Si recuperó destinatarios de Exchange eliminados (contactos, usuarios o grupos de distribución), supervise con atención las colisiones y los errores relacionados con los objetos recuperados. Si se modificaron directivas de Exchange u otras configuraciones relacionadas con los destinatarios desde la eliminación, vuelva a aplicar las directivas actuales a los destinatarios recuperados para asegurarse de que cuenten con la configuración correcta.

## Más información

[Guía paso a paso de la papelera de reciclaje de Active Directory](https://go.microsoft.com/fwlink/p/?linkid=178720)

[Introducción a mejoras del Centro de administración de Active Directory (nivel 100)](https://go.microsoft.com/fwlink/p/?linkid=267641)

[Administración de AD DS avanzada con el Centro de administración de Active Directory (nivel 200)](https://go.microsoft.com/fwlink/p/?linkid=267642)

