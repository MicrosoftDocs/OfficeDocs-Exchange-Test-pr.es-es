---
title: 'Descripción del control de acceso basado en funciones: Exchange 2013 Help'
TOCTitle: Descripción del control de acceso basado en funciones
ms:assetid: fd268867-2ae5-441b-8103-7a7583eb2bbe
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298183(v=EXCHG.150)
ms:contentKeyID: 49896037
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Descripción del control de acceso basado en funciones

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2018-01-31_

*Role Based Access Control* (RBAC) es el modelo de permisos de Microsoft Exchange Server 2013. Con RBAC no necesitará modificar ni administrar las listas de control de acceso, como sucedía en Exchange Server 2007. Las listas de control de acceso dificultaban el uso de Exchange 2007, pues había que modificarlas sin causar resultados no deseados, había que mantener dichas modificaciones en las actualizaciones posteriores y había que solucionar los problemas que pudieran surgir al no utilizarlas de la forma habitual.

RBAC permite controlar lo que los administradores y los usuarios finales pueden hacer, ya sea de un modo general o pormenorizado, así como alinear más exactamente los roles que se asignan a usuarios y administradores con los verdaderos roles que éstos desempeñan dentro de la organización. En Exchange 2007, el modelo de permisos de servidor se aplicaba solamente a los administradores encargados de la infraestructura de Exchange 2007. Sin embargo, en Exchange 2013 RBAC controla tanto las tareas administrativas que se pueden llevar a cabo como las posibilidades que tienen los usuarios de administrar su propio buzón y grupos de distribución.

Mediante RBAC se pueden asignar permisos a los usuarios de una organización de dos formas distintas, en función de si el usuario es administrador o usuario experto, o bien usuario final: grupos de roles de administración y directivas de asignación de roles de administración. Cada método asocia a los usuarios con los permisos que necesitan para realizar su trabajo. También se puede usar un tercer método más avanzado: la asignación directa de roles de usuario. En las siguientes secciones de este tema se describe RBAC con ejemplos sobre el modo de usarlo.


> [!NOTE]
> Este tema se centra en las funciones avanzadas de RBAC. Si desea administrar los permisos básicos de Exchange&nbsp;2013, como usar el Panel de control de Exchange (EAC) para agregar y quitar miembros de grupos de roles, crear y modificar grupos de roles o crear y modificar directivas de asignación de roles, consulte <A href="permissions-exchange-2013-help.md">Permisos</A>.



**Contenido**

Management role groups

Management role assignment policies

Direct user role assignment

Summary and examples

For more information

## Grupos de roles de administración

Los *grupos de roles de administración* asocian los roles de administración a un grupo de administradores o usuarios especialistas. Los administradores gestionan una amplia organización de Exchange o de configuración de destinatarios. Los usuarios especialistas administran las características específicas de Exchange, como la conformidad. Estos últimos pueden tener una capacidad de administración limitada, como los miembros del departamento de soporte técnico, pero en cualquier caso no disfrutarán de derechos administrativos globales. Los grupos de funciones normalmente están relacionados con funciones de administración pública que permiten que los administradores y los usuarios especialistas administren la configuración de su organización y destinatarios. Por ejemplo, con los grupos de funciones se controla si los administradores pueden administrar a los destinatarios o utilizar características de detección de buzones.

La forma más común de asignar permisos a administradores o usuarios especialistas consiste en agregar usuarios a los grupos de roles o quitarlos. Para obtener más información, consulte [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md).

Los grupos de roles constan de los siguientes componentes, que definen lo que los administradores y usuarios especialistas pueden llevar a cabo:

  - **Grupo de roles de administración**   El *grupo de roles de administración* es un grupo de seguridad universal especial que contiene buzones, usuarios, grupos de seguridad universal y otros grupos de roles que son miembros del grupo en cuestión. Aquí es donde se agregan y quitan miembros, y también adonde se asignan los roles de administración. La combinación de todos los roles de un grupo de roles define todo lo que los usuarios agregaron a un grupo de roles de la organización Exchange.

  - **Rol de administración**   Un *rol de administración* es un contenedor para una agrupación de entradas de roles de administración. Los roles se usan para definir las tareas específicas que pueden realizar los miembros de un grupo de roles asignados a un rol. Una *entrada de rol de administración* es un cmdlet, un script o un permiso especial que permite realizar todas y cada una de las tareas que tiene un rol. Para obtener más información, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

  - **Asignación de roles de administración**   Una *asignación de roles de administración* vincula un rol con un grupo de roles. La asignación de un rol a un grupo de roles permite que los miembros de dicho grupo usen los cmdlets y los parámetros definidos en el rol. Las asignaciones de roles pueden usar ámbitos de administración para controlar dónde se puede usar la asignación. Para obtener más información, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

  - **Ámbito de roles de administración**   Un *ámbito de roles de administración* es el ámbito de influencia o de impacto sobre una asignación de roles. Cuando un rol se asigna con un ámbito a un grupo de roles, el ámbito de administración define qué objetos puede administrar esa asignación. A continuación, los miembros del grupo de roles reciben la asignación y su ámbito, los cuales restringen lo que estos miembros pueden administrar. Un ámbito puede estar formado por una lista de servidores o bases de datos, unidades organizativas o filtros en servidores, bases de datos u objetos de destinatario. Para obtener más información, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

Al agregar un usuario a un grupo de roles, aquél obtiene todos los roles que dicho grupo tiene asignados. Si hay ámbitos aplicados a cualquier asignación de roles entre el grupo de roles y los roles, dichos ámbitos establecerán la configuración de servidor o los destinatarios que el usuario podrá administrar.

En caso de que desee cambiar los roles que se han asignado a los grupos de roles, deberá cambiar las asignaciones que vinculan los grupos con los roles. De todas formas, no será necesario modificar estas asignaciones a menos que las creadas en Exchange 2013 no se ajusten a sus necesidades. Para obtener más información, vea [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Para obtener más información acerca de los grupos de roles, consulte [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md).

## Directivas de asignación de roles de administración

Las directivas de asignación de roles de administración asocian los roles de administración de usuarios finales a los usuarios. Estas directivas constan de roles que controlan lo que un usuario puede hacer con su buzón o sus grupos de distribución. Estos roles no permiten la administración de características que no estén directamente asociadas con el usuario. Cuando se crea una directiva de asignación de roles, se define todo lo que un usuario puede hacer con el buzón. Por ejemplo, una directiva de asignación de funciones puede permitir que un usuario establezca el nombre para mostrar, configure el correo de voz y las reglas de la bandeja de entrada. Otra directiva de asignación de funciones puede permitir que un usuario cambie la dirección, utilice la mensajería de texto y configure los grupos de distribución. De forma predeterminada, cada usuario que tenga un buzón de correo de Exchange 2013, incluidos los administradores, tiene una directiva de asignación de roles. Puede decidir la directiva de asignación de roles que se aplica de forma predeterminada, elegir el contenido de la directiva de asignación de roles predeterminada, anular la directiva predeterminada en algunos buzones de correo o no asignar ninguna directiva de asignación de roles predeterminada.

El modo más habitual de administrar los permisos para que los usuarios administren las opciones de su propio buzón y grupos de distribución es asignando un usuario a una directiva de asignación. Para obtener más información, consulte [Descripción de las directivas de asignación de roles de administración](understanding-management-role-assignment-policies-exchange-2013-help.md).

Las directivas de asignación de roles constan de los siguientes componentes, que definen lo que los usuarios pueden hacer con sus buzones. Observe que algunos de estos componentes se aplican también a grupos de roles. Cuando se usan con las directivas de asignaciones de roles, tales componentes son limitados para que los usuarios administren únicamente su propio buzón:

  - **Directiva de asignación de roles de administración**   La *directiva de asignación de roles de administración* es un objeto especial de Exchange 2013. Los usuarios se asocian a la directiva de asignación de roles al crear sus buzones o si se cambia la directiva de asignación de roles en un buzón. También es a ella a la que se asignan los roles de administración de los usuarios finales. La combinación de todos los roles en una directiva de asignación de roles define todo lo que puede administrar un usuario en su buzón o grupo de distribución.

  - **Rol de administración**   Un *rol de administración* es un contenedor para una agrupación de entradas de roles de administración. Los roles se usan para definir tareas específicas que un usuario puede realizar con su buzón o sus grupos de distribución. Una *entrada de rol de administración* es un cmdlet, un script o un permiso especial que permite realizar todas y cada una de las tareas específicas que tiene un rol de administración. Sólo se pueden usar roles de usuario final con directivas de asignación de roles. Para obtener más información, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

  - **Asignación de roles de administración**   Una *asignación de roles de administración* es el vínculo entre un rol y una directiva de asignación de roles. La asignación de un rol a una directiva de asignación de roles garantiza la posibilidad de usar cmdlets y parámetros definidos en dicho rol. Cuando se crea una asignación de roles entre una directiva de asignación de roles y un rol, no se puede especificar ningún ámbito. El ámbito aplicado por la asignación es `Self` o `MyGAL`. El ámbito de todas las asignaciones de roles se reduce al buzón o a los grupos de distribución del usuario. Para obtener más información, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

En caso de que desee cambiar los roles que se han asignado a las directivas de asignación de roles, deberá cambiar las asignaciones de roles que vinculan las directivas de asignación a roles. De todas formas, no será necesario modificar estas asignaciones a menos que las creadas en Exchange 2013 no se ajusten a sus necesidades. Para obtener más información, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Para obtener más información, consulte [Descripción de las directivas de asignación de roles de administración](understanding-management-role-assignment-policies-exchange-2013-help.md).

## Asignación directa de roles de usuario

La *asignación directa de roles* es un método avanzado mediante el cual se asignan roles de administración directamente a un usuario o grupo de seguridad universal sin usar un grupo de roles ni una directiva de asignación de roles. Las asignaciones directas de roles pueden resultar útiles cuando se debe proporcionar un conjunto de permisos pormenorizado a un usuario en concreto y no a otros. sin embargo, el uso de las asignaciones de funciones directas puede aumentar significativamente la complejidad de su modelo de permisos. Si un usuario cambia de puesto de trabajo o deja la empresa, tendrá que eliminar manualmente las asignaciones y agregarlas al nuevo empleado. Por lo tanto, se recomienda usar los grupos de roles para asignar permisos a los administradores y usuarios especialistas, y las directivas de asignación de roles para asignar permisos a los usuarios.

Para obtener más información sobre la asignación directa de usuarios, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

## Resumen y ejemplos

La siguiente ilustración muestra los componentes de RBAC y el modo en que se combinan entre sí:

  - Grupos de roles:
    
      - Uno o más administradores pueden ser miembros de un grupo de roles. También pueden ser miembros de más de un grupo de roles.
    
      - El grupo de roles se asigna a una o más asignaciones de roles. Y éstas vinculan el grupo de roles con uno o varios roles administrativos que definen las tareas que se pueden llevar a cabo.
    
      - Las asignaciones de roles pueden contener ámbitos de administración que definen dónde pueden realizar acciones los usuarios del grupo de roles. Los ámbitos determinan qué aspectos de la configuración pueden modificar los usuarios del grupo de roles.

  - Directivas de asignación de roles:
    
      - Uno o varios usuarios se pueden asociar a una directiva de asignación de roles.
    
      - La directiva de asignación de roles se asocia a una o varias asignaciones de roles. Y éstas vinculan la directiva de asignación de roles a uno o varios roles de usuario final. Los roles de usuario final definen lo que el usuario puede configurar en su buzón.
    
      - Las asignaciones de roles entre las directivas de asignación de roles y los roles cuentan con ámbitos integrados que acotan el ámbito de las asignaciones al buzón o los grupos de distribución del usuario.

  - Asignación directa de roles (avanzada):
    
      - Se puede crear una asignación de roles directamente entre un usuario o grupo de seguridad universal y uno o varios roles. El rol define las tareas que el usuario o grupo de seguridad universal puede realizar.
    
      - Las asignaciones de roles pueden contener ámbitos de administración que definen dónde puede realizar acciones el usuario o el grupo de seguridad universal. Los ámbitos determinan qué aspectos de la configuración puede modificar el usuario o el grupo de seguridad universal.

**Información general sobre RBAC**

![Relaciones de componentes de RBAC](images/Dd298183.1dee60cc-1d58-4d36-b34e-639f091e7a56(EXCHG.150).jpg "Relaciones de componentes de RBAC")

Como se muestra en la figura anterior, la mayoría de los componentes de RBAC están relacionados entre sí. El modo en que cada componente se agrupa es lo que define los permisos que se aplican a cada administrador o usuario. Los siguientes ejemplos ofrecen más contexto sobre el modo en que los grupos de roles y las directivas de asignación de roles se usan en una organización.

## Julia, la administradora

Julia es administradora de Contoso, una mediana empresa. Como tal, se encarga de administrar los destinatarios de la compañía en su oficina de Vancouver. Cuando el modelo de permisos de Contoso se creó, se designó a Julia como miembro del grupo de roles personalizado Recipient Management - Vancouver. El grupo de roles personalizado Recipient Management - Vancouver es el que más se parece a las tareas que ella desempeña en su trabajo, como crear y eliminar destinatarios (p. ej. buzones y contactos), administrar la pertenencia a los grupos de distribución y las propiedades de los buzones, etc.

Aparte del grupo de roles personalizado Recipient Management - Vancouver, Julia también precisa de una directiva de asignación de roles para administrar las opciones de configuración de su propio buzón. Los administradores de la compañía han decidido que todos los usuarios, excepto los más altos cargos, reciban los mismos permisos al administrar sus propios buzones. Así, pueden configurar el correo de voz, establecer directivas de retención y cambiar la información de dirección. La directiva de asignación de roles predeterminada que se suministró con Exchange 2013 refleja ahora estos requisitos.


> [!NOTE]
> Habrá observado que como Julia es miembro del grupo de roles personalizado Recipient Management - Vancouver, tendrá permisos para administrar su propio buzón. Eso es cierto, pero el grupo de roles no le proporciona todos los permisos necesarios para administrar todas las características del buzón. Los permisos necesarios para administrar el correo de voz y la configuración de la directiva de retención quedan fuera del ámbito de su grupo de roles. Sólo podrá adquirirlos a través de la directiva de asignación de roles predeterminada que se le haya asignado.



Para hacer esto posible, considere el grupo de roles que proporciona los permisos administrativos de Julia sobre los destinatarios de Vancouver:

1.  Se creó un grupo de roles personalizado llamado Recipient Management - Vancouver. Cuando se creó, sucedió lo siguiente:
    
    1.  El grupo de roles se asignó a los mismos roles de administración que se asignaron al grupo de roles integrado Recipient Management. De esta forma, se otorgó a los usuarios agregados al grupo de roles personalizado Recipient Management - Vancouver los mismos permisos que los de los usuarios agregados al grupo de roles Recipient Management. Sin embargo, los siguientes pasos limitan dónde pueden hacer uso de tales permisos.
    
    2.  Se creó el ámbito de administración personalizado Destinatarios de Vancouver, que engloba únicamente a los destinatarios sitos en Vancouver. Y se hizo creando un ámbito que filtraba por ciudad del usuario o cualquier otra información única.
    
    3.  El grupo de roles se creó con el ámbito de administración personalizado de Destinatarios de Vancouver. Esto quiere decir que, si bien los administradores agregados al grupo de roles personalizado Recipient Management - Vancouver disponían de plenos permisos de administración de destinatarios, solamente podían usar esos permisos con los destinatarios de Vancouver.
    
    Para obtener más información acerca de la creación de grupos de roles personalizados, consulte [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

2.  Julia se agrega como miembro del grupo de roles personalizado Recipient Management - Vancouver.
    
    Para obtener más información acerca de agregar miembros de un grupo de roles, consulte [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

A fin de que Julia pueda configurar su propio buzón, será necesario definir una directiva de asignación de roles con los permisos pertinentes. La directiva de asignación de roles predeterminada sirve para dar a los usuarios los permisos que necesitan para configurar su propio buzón. Todos los roles de usuario final se quitan de la directiva de asignación de roles predeterminada, a excepción de los siguientes: `MyBaseOptions`, `MyContactInformation`, `MyVoicemail` y `MyRetentionPolicies`. `MyBaseOptions` se incluye porque este rol de administración proporciona la funcionalidad de usuario básica en Outlook Web App, como las reglas de la Bandeja de entrada, la configuración del calendario y otras tareas.

No es preciso hacer nada más, dado que Julia ya tiene asignada la directiva de asignación de roles predeterminada. Esto significa que los cambios efectuados en esa directiva de asignación de roles se aplicarán inmediatamente a su buzón, así como al resto de buzones asignados a dicha directiva.

Para obtener más información acerca de cómo personalizar la directiva de asignación de roles predeterminada, consulte [Administrar directivas de asignación de funciones](manage-role-assignment-policies-exchange-2013-help.md).

## Fabricio, el especialista

Fabricio trabaja para Contoso, la misma empresa que Julia. Se encarga de llevar a cabo detecciones legales, establecer directivas de retención y configurar las reglas de transporte y el registro en el diario de toda la organización. Al igual que ocurrió con Julia, cuando se creó el modelo de permisos de Contoso, Fabricio se agregó al grupo de roles que coincidía con su labor profesional. El grupo de roles Records Management provee a Fabricio de permisos para configurar las directivas de retención, el registro en diario y las reglas de transporte. El grupo de roles de Discovery Management le permite realizar búsquedas en el buzón.

Al igual que Julia, Fabricio también necesita permisos para administrar su propio buzón. Posee los mismo permisos que Julia: puede configurar su correo de voz y las directivas de retención y cambiar la información de dirección.

Para que Fabricio obtenga los permisos necesarios para poder desempeñar su trabajo, se le agrega a los grupos de roles Records Management y Discovery Management. No es necesario modificar los grupos de roles porque ya le suministran los permisos que necesita, mientras que los ámbitos de administración aplicados a tales grupos abarcan a toda la organización.

Para obtener más información sobre cómo añadir un usuario a un grupo de roles, consulte [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

El buzón de Fabricio tiene asignada la misma directiva de asignación de roles predeterminada que se aplicó al buzón de Julia. Gracias a ello, dispone de todos los permisos necesarios para administrar aquellas características de su buzón que puede administrar.

## Isabel, la vicepresidenta

Isabel es la vicepresidenta de marketing de Contoso. En tanto que miembro del cuerpo ejecutivo de Contoso, Isabel disfruta de más permisos que el usuario medio. entre ellos están los que le permiten administrar su buzón, salvo una excepción: en conformidad con la ley, Isabel no puede administrar sus propias directivas de retención. Puede configurar su buzón de voz; cambiar los datos de contacto y la información de perfil; crear y administrar sus propios grupos de distribución, y agregarse a grupos de distribución que son propiedad de otros, así como quitarse de ellos.

Por lo tanto, a Isabel se le conceden distintos permisos para su propio buzón. La mayoría de los usuarios de Contoso se asignan a la directiva de asignación de funciones predeterminada. Sin embargo, los altos ejecutivos se asignan a la directiva de asignación de roles del cuerpo ejecutivo. Para crear la directiva de asignación de roles personalizada, se realiza lo siguiente:

1.  Se crea una directiva de asignación de roles personalizada llamada Cuerpo ejecutivo. La directiva de asignación de roles tiene asignados los roles `MyBaseOptions`, `MyContactInformation`, `MyVoicemail`, `MyProfileInformation`, `MyDistributionGroupMembership` y ` MyDistributionGroups`. `MyBaseOptions` se incluye porque es el rol que proporciona la funcionalidad de usuario básica en la Outlook Web App, como las reglas de la Bandeja de entrada, la configuración del calendario y otras tareas.

2.  A continuación, a Isabel se le asigna manualmente la directiva de asignación de roles Cuerpo ejecutivo.

Ahora el buzón de Isabel tiene los permisos que reporta la directiva de asignación de roles Cuerpo ejecutivo. Cualquier cambio efectuado en esa directiva de asignación de roles se aplicará automáticamente a su buzón, así como al resto de buzones asignados a dicha directiva.

## Más información

[Administrar directivas de asignación de funciones](manage-role-assignment-policies-exchange-2013-help.md)

[Cambiar la directiva de asignación en un buzón](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

