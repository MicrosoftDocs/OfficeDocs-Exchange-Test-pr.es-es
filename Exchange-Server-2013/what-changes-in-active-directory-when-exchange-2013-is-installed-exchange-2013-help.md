---
title: '¿Qué cambia en Active Directory cuando Exchange 2013 está instalado?: Exchange 2013 Help'
TOCTitle: ¿Qué cambia en Active Directory cuando Exchange 2013 está instalado?
ms:assetid: 07386078-6103-49a2-8698-2d41db9cec95
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn750898(v=EXCHG.150)
ms:contentKeyID: 62371355
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ¿Qué cambia en Active Directory cuando Exchange 2013 está instalado?

 

_**Se aplica a:**Exchange Server, Exchange Server 2013_

_**Última modificación del tema:**2014-05-26_

Cuando instala Exchange 2013, se realizan cambios en el bosque y los dominios de Active Directory. Exchange lo hace para que se pueda almacenar información sobre los servidores de Exchange, los buzones y otros objetos relacionados con Exchange en la organización. Estos cambios se realizan cuando se ejecuta el Asistente para la instalación de Exchange 2013 o cuando se ejecutan los comandos *PrepareSchema*, *PrepareAD* y *PrepareDomains* (vea cómo usar estos comandos en [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md)) durante la instalación de la línea de comandos de Exchange 2013. Si tiene curiosidad sobre los cambios que Exchange hace en Active Directory, este tema es para usted. Explica lo que Exchange hace en cada paso de la preparación de Active Directory.

Hay tres pasos que deben realizarse para preparar Active Directory para Exchange:

  - Extender el esquema de Active Directory

  - Preparar los contenedores, objetos y otros elementos de Active Directory

  - Preparar dominios de Active Directory

Una vez que se realizan los tres pasos, el bosque de Active Directory está listo para Exchange 2013. Encontrará más información sobre cómo instalar Exchange 2013 si lee [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

## Extender el esquema de Active Directory

La extensión del esquema de Active Directory agrega y actualiza clases, atributos y otros elementos. Estos cambios se necesitan para que Exchange pueda crear contenedores y objetos para almacenar información sobre la organización de Exchange. Como Exchange hace muchos cambios en el esquema de Active Directory, hay un tema dedicado a este paso. Para ver todos los cambios que se realizan en el esquema, vea [Cambios en el esquema de Active Directory de Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

Este paso se realiza automáticamente cuando se ejecuta el Asistente para la instalación de Exchange 2013 en el primer servidor de Exchange 2013 en el bosque de Active Directory. También se realiza cuando se ejecuta la instalación de la línea de comandos de Exchange 2013 con el comando *PrepareSchema* (u opcionalmente con el comando *PrepareAD*) en el primer servidor de Exchange 2013 en el bosque. Si desea encontrar más información sobre cómo extender el esquema, consulte [Extend the Active Directory schema](prepare-active-directory-and-domains-exchange-2013-help.md) en [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md).

Cuando Exchange termina de extender el esquema, establece la versión del esquema que se almacena en el atributo **ms-Exch-Schema-Version-Pt**. Si quiere asegurarse de que el esquema de Active Directory se ha extendido correctamente, puede comprobar el valor almacenado en este atributo. Si el valor en el atributo coincide con la versión del esquema que aparece en la versión de Exchange 2013 instalada, la extensión del esquema se realizó correctamente. Para ver una lista de las versiones de Exchange y cómo comprobar el valor de este atributo, consulte la sección [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) en [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md).

## Preparar los contenedores, objetos y otros elementos de Active Directory

Con el esquema extendido, el siguiente paso es agregar todos los contenedores, objetos, atributos y otros elementos que Exchange usa para almacenar información en Active Directory. Casi todos los cambios realizados en este paso se aplican a todo el bosque de Active Directory. Un conjunto más pequeño de cambios se realizan en el dominio local de Active Directory donde el comando *PrepareAD* se ejecutó durante la instalación.

Estos son los cambios que se realizan en el bosque de Active Directory:

  - Si aún no existe, el contenedor de Microsoft Exchange se crea en CN=Servicios,CN=Configuración,DC=\<*root domain*\>.

  - Si aún no existen, los siguientes contenedores y objetos se crean en CN=\<*organization name*\>,CN=Microsoft Exchange,CN=Servicios,CN=Configuración,DC=\<*root domain*\>.
    
      - CN=Contenedor listas de direcciones
    
      - CN=Directivas de buzón de la libreta de direcciones
    
      - CN=Dirección
    
      - CN=Grupos administrativos
    
      - CN=Aplicaciones de aprobación
    
      - CN=Configuración de autenticación
    
      - CN=Configuración de disponibilidad
    
      - CN=Acceso de cliente
    
      - CN=Conexiones
    
      - CN=Contenedor de carpetas ELC
    
      - CN=Directivas de buzón ELC
    
      - CN=Asistencia de Exchange
    
      - CN=Federación
    
      - CN=Confianzas de federación
    
      - CN=Configuración global
    
      - CN=Configuración híbrida
    
      - CN=Directivas de buzón móvil
    
      - CN=Configuración de buzón móvil
    
      - CN=Configuración de supervisión
    
      - CN=Directivas de buzón de OWA
    
      - CN=Contenedor de directivas de aprovisionamiento
    
      - CN=Configuración de notificaciones de inserción
    
      - CN=RBAC
    
      - CN=Directivas de destinatarios
    
      - CN=Contenedor de directivas de cuentas remotas
    
      - CN=Contenedor de directivas de retención
    
      - CN=Contenedor de etiqueta de directiva de retención
    
      - CN=Extremos de servicio
    
      - CN=Directivas del sistema
    
      - CN=Directivas de aprovisionamiento de buzón de equipo
    
      - CN=Configuración de transporte
    
      - CN=Contenedor de operador automático de mensajería unificada
    
      - CN=Contenedor de plan de marcado de mensajería unificada
    
      - CN=Contenedor de puerta de enlace IP de mensajería unificada
    
      - CN=Directivas de buzón de mensajería unificada
    
      - CN=Configuración de administración de carga de trabajo

  - Si aún no existen, los siguientes contenedores y objetos se crean en CN=Configuración de transporte, CN=\<*Organization Name*\>,CN=Microsoft Exchange,CN=Servicios,CN=Configuración,DC=\<*root domain*\>.
    
      - CN=Dominios aceptados
    
      - CN=Configuración de punto de control
    
      - CN=Personalización de DNS
    
      - CN=Reglas de interceptor
    
      - CN=Filtro de malware
    
      - CN=Clasificaciones de mensajes
    
      - CN=Higiene de mensajes
    
      - CN=Reglas
    
      - CN=MicrosoftExchange329e71ec88ae4615bbc36ab6ce41109e

  - Los permisos se establecen en toda la partición de configuración en Active Directory.

  - Se importa el archivo Rights.ldf. Este archivo agrega permisos que se necesitan para instalar Exchange y configurar Active Directory.

  - La unidad organizativa de los grupos de seguridad de MicrosoftExchange se crea en el dominio raíz del bosque y los permisos se asignan a esta.

  - Si aún no existen, se crean los siguientes grupos de roles de administración dentro de la unidad organizativa de los grupos de seguridad de Microsoft Exchange:
    
      - Administración de cumplimiento
    
      - Configuración delegada
    
      - Administración de la detección
    
      - Servicio de asistencia
    
      - Administración de higiene
    
      - Administración de la organización
    
      - Administración de carpetas públicas
    
      - Administración de destinatarios
    
      - Administración de registros
    
      - Administración de servidor
    
      - Administración de mensajería unificada
    
      - Administración de la organización de solo visualización

  - Los nuevos grupos de roles de administración (que aparecen como grupos de seguridad universales o USG en Active Directory) que se crearon en la unidad organizativa de los grupos de seguridad de MicrosoftExchange se agregan al atributo **otherWellKnownObjects** almacenado en el contenedor CN=Microsoft Exchange,CN=Servicios,CN=Configuración,DC=\<*root domain*\>.

  - Se crea el contacto creador de voz de mensajería unificada en el contenedor Objetos de sistema de Microsoft Exchange del dominio raíz.

  - El dominio en el que se ejecutó el comando *PrepareAD* está preparado para Exchange 2013. Para obtener información sobre cómo preparar el dominio de Active Directory para Exchange, consulte Preparar dominios de Active Directory.

  - Se establece la propiedad **msExchProductId** en el objeto de organización de Exchange. Si quiere asegurarse de que el esquema de Active Directory se ha extendido correctamente, puede comprobar el valor almacenado en esta propiedad. Si el valor en la propiedad coincide con la versión del esquema que aparece en la versión de Exchange 2013 instalada, la extensión del esquema se realizó correctamente. Para ver una lista de las versiones de Exchange y cómo comprobar el valor de esta propiedad, consulte la sección [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) en [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md).

## Preparar dominios de Active Directory

El paso final de la preparación de Active Directory para Exchange es preparar todos los dominios de Active Directory donde se instalarán los servidores de Exchange o donde se ubicarán los usuarios con buzones habilitados. Este paso se realiza automáticamente en el dominio donde se ejecuta el comando *PrepareAD*.

Estos son los cambios que se realizan en los dominios de Active Directory:

  - Si aún no existe, el contenedor Objetos de sistema de Microsoft Exchange se crea en la partición del dominio raíz en Active Directory.

  - Se establecen permisos en el contenedor Objetos de sistema de Microsoft Exchange para los grupos de seguridad de los usuarios autenticados, la administración de la organización y los servidores de Exchange.

  - Se crea el grupo global de servidores de dominio de instalación de Exchange en el dominio actual y se coloca en el contenedor Objetos del sistema de Microsoft Exchange.

  - El grupo Servidores de dominio de instalación de Exchange se agrega al grupo de seguridad universal de servidores Exchange en el dominio raíz.

  - Se asignan permisos en el nivel de dominio para el grupo de seguridad universal de servidores de Exchange y para el grupo de seguridad universal de administración de la organización.

  - Se establece la propiedad **objectVersion** en el contenedor Objetos de sistema de Microsoft Exchange en DC=\<*root domain*\>. Si quiere asegurarse de que el esquema de Active Directory se ha extendido correctamente, puede comprobar el valor almacenado en esta propiedad. Si el valor en la propiedad coincide con la versión del esquema que aparece en la versión de Exchange 2013 instalada, la extensión del esquema se realizó correctamente. Para ver una lista de las versiones de Exchange y cómo comprobar el valor de esta propiedad, consulte la sección [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) en [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md).

