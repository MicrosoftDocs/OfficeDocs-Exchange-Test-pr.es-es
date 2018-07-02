---
title: 'Mensajería unificada: Exchange 2013 Help'
TOCTitle: Mensajería unificada
ms:assetid: 004b5d1a-cae8-4034-ab65-db41bd2f7b97
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150478(v=EXCHG.150)
ms:contentKeyID: 48267744
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mensajería unificada

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La mensajería unificada (MU) permite a los usuarios usar el correo de voz y otras características, incluyendo Outlook Voice Access y Reglas de respuesta a llamada habilitadas. La mensajería unificada combina la mensajería de voz y la mensajería del correo electrónico en un buzón de correo al que se puede tener acceso desde muchos dispositivos diferentes. Los usuarios pueden escuchar los mensajes desde su Bandeja de entrada del correo electrónico o desde cualquier teléfono si utilizan Outlook Voice Access. Puede controlar el modo en que los usuarios realizan llamadas salientes desde la mensajería unificada, y la experiencia que tienen las personas cuando llaman a su organización.

Actualmente, los administradores de TI con frecuencia administran las redes de correo de voz o telefonía y los sistemas de correo electrónico o las redes de datos de sus organizaciones como sistemas separados. El correo de voz y el correo electrónico se encuentran en bandejas de entrada separadas que se hospedan en servidores independientes a los que se accede desde el escritorio para el correo electrónico y desde el teléfono para el correo de voz.

La mensajería unificada posibilita que los administradores de Exchange combinen mensajería de voz y mensajes de correo electrónico en un buzón de correo para que sus usuarios puedan escuchar sus mensajes de correo de voz en su bandeja de entrada o usando Outlook Voice Access desde cualquier teléfono. Utiliza el almacén de Exchange para los mensajes de correo electrónico y de voz.

**Contenido**

Características nuevas

Características de mensajería unificada

Planear e implementar la mensajería unificada

Gestión de la mensajería unificada con el EAC y el Shell

Documentación de mensajería unificada

## Características nuevas

La mensajería unificada (MU) se introdujo por primera vez en Microsoft Exchange Server 2007 y también estuvo disponible en Exchange 2010. La característica Mensajería unificada que se establece en Exchange 2013 es similar a las versiones anteriores de Exchange. Sin embargo, se han agregado nuevas características y ha habido cambios en la arquitectura. La mensajería unificada se considera ahora un componente o subfunción de las características relacionadas con la voz que se ofrecen en Exchange 2013. El término *Mensajería unificada* aún se utiliza ampliamente en cmdlets del Shell de administración de Exchange y los servicios relacionados con la mensajería unificada, y los componentes de la mensajería unificada (incluidos los planes de marcado, los operadores automáticos, las directivas de buzones de correo de mensajería unificada y las puertas de enlace IP de mensajería unificada), junto con la capacidad de administrar aquellos componentes de mensajería unificada, se ubican dentro del nodo de mensajería unificada del panel de navegación del Centro de administración de Exchange (EAC).

Los siguientes temas son puertas de enlace a información acerca de las nuevas funciones o las funciones mejoradas que se encuentran en la mensajería unificada de Exchange 2013:

  - [Cambios en la arquitectura de voz](voice-architecture-changes-exchange-2013-help.md)

  - [Compatibilidad con IPv6 en mensajería unificada](ipv6-support-in-unified-messaging-exchange-2013-help.md)

  - [Mejoras de vista previa del correo de voz](voice-mail-preview-enhancements-exchange-2013-help.md)

  - [Actualizaciones de cmdlet de mensajería unificada](unified-messaging-cmdlet-updates-exchange-2013-help.md)

Volver al principio

## Características de mensajería unificada

Las características del correo de voz que se encuentran en la mensajería unificada ofrecen ventajas a los usuarios finales y a los administradores de TI.

## Características para usuarios finales

Cuando se implementa la mensajería unificada, los usuarios pueden acceder al correo de voz, al correo electrónico y a la información del calendario que se almacena en su buzón de correo desde un cliente de correo electrónico, por ejemplo, Outlook o MicrosoftOutlook Web App, desde un teléfono móvil con MicrosoftExchange ActiveSync configurado, como un teléfono Windows o desde un teléfono. Además, los usuarios pueden utilizar las siguientes características:

  - **Acceso a información de Exchange   **Los usuarios habilitados para mensajería unificada pueden tener acceso a un conjunto completo de características de correo de voz de teléfonos móviles que tienen acceso a Internet, MicrosoftOffice Outlook 2007 o versiones posteriores y Outlook Web App. Estas características incluyen muchas opciones de configuración de correo de voz y la posibilidad de reproducir un mensaje de voz, ya sea desde el panel de lectura mediante un reproductor Windows Media Player integrado o desde la lista de mensajes usando los altavoces del equipo.

  - **Reproducir en teléfono**   La característica Reproducir en teléfono permite a los usuarios habilitados para mensajería unificada reproducir mensajes de voz en un teléfono. Si un usuario habilitado para MU está sentado en el cubículo de su oficina, está usando un equipo público o un equipo que no tiene características multimedia, o está escuchando un mensaje de voz confidencial, es posible que no desee que nadie escuche el mensaje de voz a través de los altavoces del equipo. En ese caso, pueden reproducirlo desde cualquier teléfono, ya sea el de casa, el de la oficina o un teléfono móvil.

  - **Formulario de correo de voz**   El formulario de correo de voz se parece al formulario predeterminado de correo electrónico. Ofrece a los usuarios una interfaz para realizar acciones tales como reproducir, detener o pausar mensajes de voz, reproducir mensajes de voz en un teléfono y agregar o editar notas.
    
    El formulario de correo de voz incluye Windows Media Player integrado y un campo de notas de audio. El reproductor Windows Media Player integrado y el campo de notas se muestran en el panel de lectura cuando los usuarios obtienen la vista previa de un mensaje de voz o en una ventana separada cuando abren el mensaje de voz. Si los usuarios no tienen habilitada la mensajería unificada o no se ha instalado un cliente de correo electrónico compatible en el equipo cliente, sólo pueden ver mensajes de voz en forma de datos adjuntos y el formulario de correo de voz no está disponible.

  - **Configuración de usuario**   Un usuario que tiene habilitada la mensajería unificada puede configurar varias opciones de correo de voz para mensajería unificada mediante Outlook Web App. Por ejemplo, el usuario puede configurar números de acceso telefónico y el número de correo de voz Reproducir en teléfono, además de restablecer el PIN de acceso al correo de voz.

  - **Contestador automático   **El contestador automático engloba responder llamadas entrantes en nombre de los usuarios, reproducir saludos personales de los usuarios, grabar mensajes y enviarlos a su bandeja de entrada como un mensaje de correo electrónico.

  - **Reglas de respuesta a llamada**   Reglas de respuesta a llamada permite a los usuarios con correo de voz habilitado determinar cómo se debería gestionar la respuesta a llamadas de sus llamadas entrantes. El modo en que se aplican las reglas de contestador automático es similar a cómo se aplican las reglas de bandeja de entrada con los mensajes entrantes. De forma predeterminada, no se configura ninguna regla de contestador automático. Si una llamada entrante recibe la respuesta de un servidor de buzones de correo, la persona que llama tiene la opción de dejar un mensaje de voz al destinatario de su llamada. Mediante las reglas de contestador automático, una persona que llama puede:
    
      - Dejar un mensaje de voz para el usuario habilitado para mensajería automática.
    
      - Transferir a un contacto alternativo del usuario habilitado para mensajería unificada.
    
      - Transferir al correo de voz del contacto alternativo.
    
      - Transferir a otros números de teléfono que ha configurado el usuario habilitado para mensajería unificada.
    
      - Usar la característica "Buscarme" o busque al usuario habilitado para mensajería unificada con una transferencia desde un operador.

  - **Vista previa de correo de voz**   El servidor de buzones de correo utiliza el reconocimiento de voz automático (ASR) en mensajes de correo de voz creados recientemente. Los mensajes de voz que reciben los usuarios contienen una grabación y un texto creados a partir de la grabación de voz. Los usuarios ven el texto del mensaje de voz en un mensaje de correo electrónico en Outlook Web App u otro cliente de correo electrónico compatible.

  - **Indicador de mensaje en espera**   El indicador de mensaje en espera existe en la mayoría de los sistemas de correo de voz antiguos y puede hacer referencia a cualquier mecanismo que indique la existencia de un mensaje nuevo. En Exchange 2007, esta función la aportaba una aplicación de otro proveedor que indicaba la recepción de un nuevo mensaje de voz encendiendo una luz en el teléfono fijo. Esta característica se incorporó a Exchange 2010 y ya no se necesita software de terceros. El indicador de mensaje en espera se habilita o deshabilita en el buzón del usuario o en una directiva de buzón de mensajería unificada.

  - **Llamada perdida y notificaciones de correo de voz a través de SMS**   Si los usuarios son parte de una implementación híbrida o de Office 365, y configuran las opciones de buzón de voz con su número de teléfono móvil y el reenvío de llamadas, pueden recibir notificaciones de llamadas perdidas y mensajes de voz nuevos en sus teléfonos móviles en un mensaje de texto a través de SMS (servicio de mensajes cortos). No obstante, para recibir esta clase de notificaciones, los usuarios deben configurar previamente los mensajes de texto y habilitar las notificaciones en su cuenta.

  - **Correo de voz protegido**   El correo de voz protegido es una funcionalidad de la mensajería unificada que permite a los usuarios enviar correo privado. Esta clase de correo está protegido por Active Directory Rights Management Services (AD RMS); los usuarios no pueden reenviar, copiar ni extraer el archivo del correo electrónico. Correo de voz protegido incrementa la confidencialidad de la mensajería unificada y permite a los usuarios limitar el público de sus mensajes de voz. Esta funcionalidad es similar a la forma en que se gestionan los mensajes de correo electrónico en Exchange 2007 pero ahora también se aplica a los mensajes de correo de voz.

  - **Outlook Voice Access   **Hay dos interfaces de mensajería unificada disponibles para los usuarios habilitados para MU: la interfaz de usuario de teléfono (TUI) y la interfaz de usuario de voz (VUI). Estas dos interfaces juntas se denominan Outlook Voice Access. Los usuarios de Outlook Voice Access pueden usar Outlook Voice Access cuando acceden al sistema de correo de voz desde un teléfono externo o interno. Los usuarios habilitados para mensajería unificada que llaman al sistema de mensajería unificada pueden obtener acceso a su buzón mediante Outlook Voice Access. Desde un teléfono, los usuarios habilitados para mensajería unificada pueden hacer lo siguiente:
    
      - Obtener acceso al correo de voz
    
      - Escuchar, reenviar o responder a mensajes de correo electrónico
    
      - Escuchar información del calendario
    
      - Acceder o marcar los contactos almacenados en el directorio de la organización o un sólo contacto o grupo de contacto ubicado en sus contactos personales.
    
      - Aceptar o cancelar convocatorias de reunión
    
      - Establecer un mensaje de voz para comunicar ausencias
    
      - Establecer preferencias de seguridad de usuario y opciones personales

  - **Envío a grupos con Outlook Voice Access**   En Exchange 2007, los usuarios podían usar la interfaz de usuario de teléfono (TUI) o la interfaz de usuario de voz (VUI) de Outlook Voice Access para enviar mensajes de correo electrónico y de voz al iniciar sesión en su buzón de correo. Sin embargo,los usuarios sólo podían enviar un mensaje de correo electrónico a un único usuario de sus contactos personales, a varios destinatarios del directorio agregando cada destinatario individualmente o agregando el nombre de una lista de distribución del directorio global de su organización. En Exchange 2013, cuando un usuario inicia sesión en su buzón mediante Outlook Voice Access, también puede enviar mensajes de correo electrónico y de voz a los usuarios de un grupo almacenado en sus contactos personales.

Volver al principio

## Características administrativas

Actualmente, la mayoría de los usuarios y departamentos de TI administran sus mensajes de correo de voz de forma independiente al correo electrónico. El correo de voz y el correo electrónico existen como bandejas de entrada separadas hospedadas en servidores independientes a los que se tiene acceso desde el escritorio para el correo electrónico y desde el teléfono para el correo de voz. La mensajería unificada ofrece un almacén integrado para todos los mensajes y acceso al contenido desde el equipo y el teléfono.

Los administradores de Exchange pueden administrar la mensajería unificada desde la misma interfaz que usan para administrar el resto de las características de Exchange, desde el Centro de administración de Exchange (EAC) y el Shell de administración de Exchange. Pueden:

  - Administrar el correo de voz y el correo electrónico desde una única plataforma

  - Administrar la mensajería unificada empleando comandos en scripts

  - Crear infraestructuras de mensajería unificada de alta disponibilidad y confiabilidad

La mensajería unificada de Exchange 2013 ofrece a los administradores:

  - **Un sistema completo de correo de voz**   La mensajería unificada ofrece una solución de correo de voz completa mediante el uso de una única infraestructura de almacenaje, transporte y directorio. El almacén lo proporciona un servidor de buzonees de correo y el reenvío de las llamadas entrantes desde una puerta de enlace VoIP o IP PBX gestionada por un servidor de acceso de clientes. Todos los mensajes de correo electrónico y de voz se pueden administrar desde un único punto de administración, mediante una única interfaz de administración y un conjunto de herramientas.

  - **Un modelo de seguridad de Exchange   **El servicio de mensajería unificada de MicrosoftExchange en un servidor de buzones de correo y el servicio Enrutador de llamada de mensajería unificada de MicrosoftExchange en un servidor de acceso de clientes se ejecutan como una sola cuenta del servidor de Exchange.

  - **Consolidación de sistemas de correo de voz**   Actualmente, la mayoría de los sistemas de mensajería de voz requieren que todos los componentes de mensajería de voz se instalen en todas las oficinas físicas de una organización. Con este tipo de solución, los sistemas de mensajería de voz de las sucursales están situados fuera de la oficina central y se deben administrar in situ. Eso supone normalmente un aumento de los costes y la complejidad de la administración. La mensajería unificada permite administrar el sistema de correo de voz desde una ubicación central. Para crear un sistema de administración centralizado para la mensajería unificada, puede colocar algunos de sus servidores de Exchange en un centro de datos o en otra ubicación, y el resto de sus servidores de Exchange de forma local y, a continuación, implementar las puertas de enlace VoIP, las IP PBX o los controladores de borde de sesión (SBC) en cada una de las sucursales para sustituir el sistema de mensajería de voz de cada sucursal. Al implementar así un sistema de voz centralizado se consigue reducir los costos administrativos y de hardware.

  - **Roles administrativos de mensajería unificada integrada**   El conjunto de roles administrativos para administrar las características de mensajería unificada y correo de voz incluye lo siguiente:
    
      - Buzones de mensajería unificada
    
      - Mensajes de mensajería unificada
    
      - Mensajería unificada

  - **Compatibilidad de fax entrantes**Exchange 2013 proporciona compatibilidad de fax entrantes para los usuarios que tienen un buzón con mensajería unificada habilitada. Pueden recibir mensajes de fax a través de llamadas a su número de extensión.
    
    Los clientes que necesiten una solución de fax deberán implementar una solución de fax de una empresa asociada. Hay varios socios de fax que proporcionan soluciones de fax. Las soluciones de fax de asociados se han concebido para estar bien integradas en Exchange y permitir a los usuarios habilitados para mensajería unificada recibir mensajes de fax entrantes. Puede encontrar una solución asociada de fax en [Microsoft Pinpoint para fax de asociados](https://go.microsoft.com/fwlink/?linkid=190238).

  - **Compatibilidad con varios idiomas    **   Todos los paquetes de idioma incluyen el motor de conversión de texto a voz (TTS) y los mensajes de asistencia por voz grabados previamente para un determinado idioma, así como compatibilidad con el reconocimiento de voz automático (ASR). Sin embargo, solamente algunos paquetes de idioma admiten la vista previa de correo de voz. El paquete de idioma de inglés de EE. UU. (en-US) se suministra con el soporte de instalación y se pueden descargar otros paquetes de idioma de mensajería unificada en [Centro de descargas de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542).

  - **Operador automático**   Un operador automático es un conjunto de mensajes de voz que proporciona a los usuarios externos e internos acceso al sistema de correo de voz. Los usuarios pueden usar el teclado del teléfono o las entradas de voz para desplazarse por el menú del operador automático, llamar a un usuario o buscar primero a un usuario de la organización y luego llamarlo. El operador automático proporciona al administrador la capacidad de:
    
      - Crear un menú personalizado para usuarios externos.
    
      - Definir saludos informativos, saludos de horario de apertura y saludos de horario fuera de oficina.
    
      - Definir calendarios de vacaciones.
    
      - Describir cómo buscar en el directorio de la organización.
    
      - Describir cómo conectar con la extensión de un usuario para que quienes llamen desde el exterior puedan llamar a cualquier usuario especificando su extensión.
    
      - Describir la forma de buscar en el directorio de la organización para que quienes llamen desde el exterior puedan buscar a un usuario específico en el directorio de la organización y llamarle.
    
      - Permitir que los usuarios externos llamen al operador.

Volver al principio

## Planear e implementar la mensajería unificada

La mensajería unificada requiere que integre la implementación de Exchange Server con el sistema telefónico que haya en la organización. Una implementación correcta requiere un análisis cuidadoso de la infraestructura telefónica existente y la realización de los pasos de planificación adecuados para implementar y administrar el correo de voz en la mensajería unificada.

Al planear la implementación de la mensajería unificada, debe tener en cuenta el diseño y otros problemas que puedan afectar a la capacidad para lograr los objetivos de la organización al implementar la mensajería unificada. Por lo general, cuanto más simple sea la topología de mensajería unificada, mas fácil será implementar y mantener la mensajería unificada. Instale tan pocos servidores de buzones de correo y de acceso de clientes y cree pocos componentes de mensajería unificada como planes de marcado de mensajería unificada, operadores automáticos y directivas de buzones de mensajería que necesite para permitir los objetivos empresariales y de la organización. Las grandes empresas con complejos entornos de red y de telefonía, múltiples unidades de negocio u otras características complejas requieren una planificación mayor que las organizaciones más pequeñas con necesidades de mensajería unificada relativamente sencillas.

Para poder implementar correctamente la mensajería unificada, debe tener en cuenta y evaluar muchas áreas. Es preciso que conozca los distintos aspectos de la mensajería unificada, así como cada componente y característica, para poder planear adecuadamente su infraestructura e implementación. La asignación de tiempo paras planificar y trabajar en estos temas ayudará a prevenir problemas cuando implemente la mensajería unificada en su organización. A continuación, tiene algunas de las áreas que debería considerar y evaluar al planificar la mensajería unificada de su organización:

  - Las necesidades de su organización.

  - Los requisitos de seguridad de su organización.

  - Su telefonía existente, la red de conmutación de circuitos y su sistema de correo de voz actual.

  - Su diseño de red IP de conmutación de paquetes actual. Esto incluye su red de área local (LAN) y sus puntos de conectividad WAN y dispositivos.

  - Su entorno de Active Directory actual.

  - El número de usuarios a los que tendrá que dar soporte técnico.

  - El número de servidores de buzones de correo y de acceso de clientes que necesitará.

  - Si integrará la mensajería unificada con Microsoft Lync Server para habilitar Enterprise Voice.

  - La ubicación de las puertas de enlace de VoIP, el equipo de telefonía y los servidores de buzones de correo y de acceso de clientes.

  - El tipo de implementación de la mensajería unificada: local o híbrido.

  - Los requisitos de almacenamiento de los usuarios de correo de voz.

Volver al principio

## Gestión de la mensajería unificada con el EAC y el Shell

**Gestión del EAC**

Exchange 2013 proporciona una única consola de administración unificada para su organización que incluye todos los componentes y las características de la mensajería unificada. El Centro de administración de Exchange (EAC) proporciona una interfaz racionalizada y optimizada para la administración de implementaciones locales, en línea o híbridas. El EAC en Exchange 2013 sustituye la Consola de administración de Exchange (EMC) y el Panel de control de Exchange (ECP) en Exchange 2010. Algunas de las características del EAC incluyen:

  - **Vista de lista**   La vista de lista de EAC se ha diseñado para eliminar las limitaciones que existían en el EAC. ECP tenía la limitación de mostrar un máximo de 500 objetos y si deseaba ver los objetos que no estaban en la lista del panel de detalles, tenía que usar la búsqueda y el filtrado para encontrar esos objetos específicos. En Exchange 2013, el límite de visualización desde el interior de la vista de lista de EAC es de aproximadamente 20 000 objetos. Además, se ha agregado la paginación para que pueda ver los resultados en páginas. También puede configurar el tamaño de la página y exportar a un archivo CSV.

  - **Agregar o quitar columnas a la vista de lista de destinatarios**   Puede elegir qué columnas ver y puede guardar las vistas de lista personalizadas.

  - **Proteger el directorio virtual ECP**   Puede dividir el acceso desde Internet e Intranets en el directorio virtual ECP de IIS para permitir o no permitir las características de administración. Con esta característica, puede conceder o denegar acceso a los usuarios que intentan acceder al EAC desde Internet, fuera del entorno de su organización y, a la vez, conceder acceso a las opciones de Outlook Web App de un usuario final.

  - **Administración de carpeta pública**   En Exchange 2010 y Exchange 2007, las carpetas públicas se administraban desde la consola de administración de carpetas públicas. Las carpetas públicas están ahora en el EAC y no necesitará usar una herramienta independiente para su administración.

  - **Notificaciones**   En Exchange 2013, el EAC tiene ahora un visor de Notificaciones para que pueda ver el estado de los procesos de ejecución prolongada y, si lo elije, recibirá la notificación mediante un mensaje de correo electrónico cuando finalice el proceso.

  - **Editor de usuarios de control de acceso basado en funciones (RBAC)**   En Exchange 2010 podía usar el editor de usuarios RBAC para agregar usuarios a los grupos de roles de administración. En Exchange 2013, la funcionalidad Editor de usuarios RBAC ahora está en EAC, y no necesita una herramienta independiente para administrar RBAC.

  - **Herramientas de mensajería unificada**   En Exchange 2010 podía usar las herramientas "Estadísticas de llamadas" y "Registros de llamadas de usuario" para ayudar a proporcionar estadísticas e información de mensajería unificada acerca de llamadas específicas para un usuario habilitado para mensajería unificada. En Exchange 2013, las herramientas "Estadísticas de llamadas" y "Registros de llamadas de usuario" ahora están en el EAC, y no necesita una herramienta independiente para administrarlas.

**Shell de administración**

El Shell de administración de Exchange desarrollado con la tecnología Windows PowerShell, proporciona una eficaz interfaz de línea de comandos que permite automatizar las tareas administrativas. Con el Shell, se pueden administrar todos los aspectos de Exchange. Puede habilitar cuentas de correo electrónico nuevas, crear conectores de envío y recepción, configurar propiedades de base de datos, administrar todos los aspectos de la mensajería unificada, y más. El Shell puede realizar todas las tareas que puede realizar el EAC además de tareas que no se pueden realizar en el EAC. De hecho, cuando hace algo en el EAC, es el Shell el que está haciendo el trabajo en segundo plano.

Volver al principio

## Documentación de mensajería unificada

La tabla siguiente contiene vínculos a temas que le ayudarán a aprender acerca de y a administrar la mensajería unificada de Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tema</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="new-voice-mail-features-exchange-2013-help.md">Nuevas características de correo de voz</a></p></td>
<td><p>Conozca las nuevas características de Microsoft Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Diseño de mensajería unificada</a></p></td>
<td><p>Más información acerca de los conceptos y los datos que necesita para planificar la implementación de la mensajería unificada.</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Implementación del correo de voz y mensajería unificada</a></p></td>
<td><p>Más información acerca de los requisitos y los pasos involucrados en la implementación del correo de voz y la mensajería unificada.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-languages-prompts-and-greetings-exchange-2013-help.md">Idiomas, mensajes y saludos de mensajería unificada</a></p></td>
<td><p>Infórmese sobre los paquetes de idiomas y la configuración de idioma de la mensajería unificada.</p></td>
</tr>
<tr class="odd">
<td><p><a href="telephone-system-integration-with-um-exchange-2013-help.md">Integración del sistema telefónico con mensajería unificada</a></p></td>
<td><p>Infórmese sobre cómo integrar la red de telefonía con la mensajería unificada.</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md">Conecte su sistema de correo de voz a la red de teléfono</a></p></td>
<td><p>Más información acerca de cómo usar y configurar componentes de mensajería unificada para conectar su red de telefonía a la mensajería unificada de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatically-answer-and-route-incoming-calls-exchange-2013-help.md">Contestar y enrutar automáticamente las llamadas entrantes</a></p></td>
<td><p>Más información acerca de cómo crear los operadores automáticos de mensajería unificada y administrar la configuración de los menús de navegación, los saludos y el horario comercial y el horario no comercial.</p></td>
</tr>
<tr class="even">
<td><p><a href="set-up-voice-mail-for-users-exchange-2013-help.md">Configurar el correo de voz para los usuarios</a></p></td>
<td><p>Infórmese sobre cómo crear y administrar directivas de buzones de mensajería unificada y cómo habilitar a usuarios para este servicio.</p></td>
</tr>
<tr class="odd">
<td><p><a href="set-up-client-voice-mail-features-exchange-2013-help.md">Configurar características de correo de voz de cliente</a></p></td>
<td><p>Infórmese sobre cómo configurar las características de cliente para permitir que los usuarios accedan y administren sus mensajes de correo de voz.</p></td>
</tr>
<tr class="even">
<td><p><a href="set-outlook-voice-access-pin-security-exchange-2013-help.md">Configurar la seguridad del PIN de Outlook Voice Access</a></p></td>
<td><p>Infórmese sobre cómo establecer los requisitos de PIN para usuarios de Outlook Voice Access.</p></td>
</tr>
<tr class="odd">
<td><p><a href="protect-voice-mail-exchange-2013-help.md">Protección del correo de voz</a></p></td>
<td><p>Infórmese sobre cómo usar la mensajería unificada para proteger mensajes de voz.</p></td>
</tr>
<tr class="even">
<td><p><a href="run-reports-for-voice-mail-calls-exchange-2013-help.md">Ejecutar informes para llamadas de correo de voz</a></p></td>
<td><p>Conozca los informes de llamadas de mensajería unificada.</p></td>
</tr>
</tbody>
</table>

