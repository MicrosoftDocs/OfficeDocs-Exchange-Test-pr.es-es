---
title: 'Destinatarios: Exchange 2013 Help'
TOCTitle: Destinatarios
ms:assetid: 40300ed4-85a5-463d-bb3a-cf787bd44e9d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201680(v=EXCHG.150)
ms:contentKeyID: 49895593
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Destinatarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Las personas y los recursos que envían y reciben mensajes son el núcleo de cualquier sistema de mensajería y colaboración. En una organización de Exchange, estas personas y estos recursos se conocen como *destinatarios*. Un destinatario es cualquier objeto habilitado para correo en Active Directory al que Microsoft Exchange puede entregar o enrutar mensajes.

## Tipos de destinatarios de Exchange

Exchange incluye varios tipos de destinatarios explícitos. Cada tipo de destinatario está identificado en el centro de administración de (EAC) y tiene un valor único en la propiedad *RecipientTypeDetails* en el Shell de administración de Exchange. El uso de tipos explícitos de destinatarios tiene las ventajas siguientes:

  - A golpe de vista, se puede diferenciar entre varios tipos de destinatarios.

  - Puede buscar y clasificar por cada tipo de destinatario.

  - Puede realizar operaciones de administración en conjunto con más facilidad para los tipos de destinatario seleccionados.

  - Puede ver propiedades de destinatarios con más facilidad porque el EAC usa tipos de destinatarios para presentar diferentes páginas de propiedades. Por ejemplo, la capacidad de los recursos se muestra para un buzón de correo de sala pero no está presente para un buzón de correo de usuario.

En la lista siguiente se describen las propiedades de destinatarios disponibles. Todos estos tipos de destinatarios se tratan con más detalle más adelante en este tema.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de destinatario</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Grupo de distribución dinámico</p></td>
<td><p>Grupo de distribución que usa los filtros y condiciones del destinatario para derivar su pertenencia al mismo tiempo que se envían mensajes.</p></td>
</tr>
<tr class="even">
<td><p>Buzón de equipo</p></td>
<td><p>Un buzón de recursos que se asigna a un recurso sin una ubicación específica, como un proyector de un equipo portátil, un micrófono o un automóvil de la empresa. Los buzones de equipamiento se pueden incluir como recursos en las convocatorias de reuniones, ya que son un método sencillo y eficaz de usar recursos para sus usuarios.</p></td>
</tr>
<tr class="odd">
<td><p>Buzón vinculado</p></td>
<td><p>Un buzón de correo que es asignado a un usuario individual en un bosque de confianza independiente.</p></td>
</tr>
<tr class="even">
<td><p>Contacto de correo</p></td>
<td><p>Un contacto de Active Directory habilitado para correo que contiene información acerca de las personas u organizaciones que existen fuera de la organización de Exchange. Cada contacto de correo tiene una dirección de correo electrónico externa. Todos los mensajes enviados al contacto de correo se enrutan en esta dirección de correo electrónico externa.</p></td>
</tr>
<tr class="odd">
<td><p>Contacto de bosque de correo</p></td>
<td><p>Contacto de correo que representa un objeto destinatario de otro bosque. Los contactos de bosque de correo se suelen crear por la sincronización de Microsoft Identity Integration Server (MIIS).</p>

> [!IMPORTANT]
> Los contactos de bosque de correo son objetos de destinatario de solo lectura que solo se actualizan a través de MIIS o de una sincronización personalizada similar. No puede usar el EAC ni el Shell para quitar o modificar un contacto de correo del bosque.


</td>
</tr>
<tr class="even">
<td><p>Usuario de correo</p></td>
<td><p>Un usuario de Active Directory habilitado para correo que representa a un usuario externo a la organización de Exchange. Cada usuario de correo tiene una dirección de correo electrónico externa. Todos los mensajes enviados al usuario de correo se enrutan en esta dirección de correo electrónico externa.</p>
<p>Un usuario de correo es similar a un contacto de correo, con la excepción de que un usuario de correo tiene credenciales de inicio de sesión de Active Directory y puede tener acceso a los recursos.</p></td>
</tr>
<tr class="odd">
<td><p>Grupo no universal habilitado para correo</p></td>
<td><p>Un objeto de grupo global o local de Active Directory habilitado para correo. En Exchange Server 2007, se han interrumpido los grupos no universales habilitados para correo y solo pueden existir si se han migrado de Exchange 2003 o de versiones anteriores de Exchange. No puede usar Exchange Server 2013 para crear grupos de distribución no universales.</p></td>
</tr>
<tr class="even">
<td><p>Carpeta pública habilitada para correo</p></td>
<td><p>Una carpeta pública de Exchange que se configuró para recibir mensajes.</p></td>
</tr>
<tr class="odd">
<td><p>Grupos de distribución</p></td>
<td><p>Un grupo de distribución es un grupo de distribución de Active Directory habilitado para correo que se puede usar solo para distribuir mensajes a un grupo de destinatarios.</p></td>
</tr>
<tr class="even">
<td><p>Grupo de seguridad habilitado para correo</p></td>
<td><p>Un grupo de seguridad con correo habilitado es un objeto de grupo de seguridad universal de Active Directory habilitado para correo que se puede usar para asignar permisos de acceso a los recursos de Active Directory y, también, para distribuir mensajes.</p></td>
</tr>
<tr class="odd">
<td><p>Destinatario de Microsoft Exchange</p></td>
<td><p>Un objeto de destinatario especial que proporciona un remitente de mensaje unificado y conocido que diferencia los mensajes generados por el sistema de otros mensajes. Reemplaza el remitente Administrador de sistema usado para mensajes generados por el sistema de versiones anteriores de Exchange.</p></td>
</tr>
<tr class="even">
<td><p>Buzón de sala</p></td>
<td><p>Un buzón de recursos que se asigna a la ubicación de una reunión, como una sala de conferencia, un auditorio o un aula. Los buzones de sala se pueden incluir como recursos en las solicitudes de reuniones, ya que son un método sencillo y eficaz de organizar reuniones para sus usuarios.</p></td>
</tr>
<tr class="odd">
<td><p>Buzón compartido</p></td>
<td><p>Un buzón de correo no asociado principalmente a un único usuario y que suele estar configurado para permitir el acceso a varios usuarios.</p></td>
</tr>
<tr class="even">
<td><p>Buzones de correo del sitio</p></td>
<td><p>Un buzón de correo está formado por un buzón de correo de Exchange para almacenar mensajes de correo electrónico y un sitio de SharePoint para almacenar documentos. Los usuarios pueden acceder a mensajes de correo electrónico y documentos usando la misma interfaz de cliente. Para obtener más información, vea <a href="site-mailboxes-exchange-2013-help.md">Buzones de correo del sitio</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Buzón de usuario</p></td>
<td><p>Un buzón de correo asignado a un usuario individual en su organización de Exchange. Normalmente contiene mensajes, elementos de calendario, contactos, tareas, documentos y otros datos de empresa importantes.</p></td>
</tr>
<tr class="even">
<td><p>Buzón de correo de Office 365</p></td>
<td><p>En las implementaciones híbridas, un buzón de correo de Office 365 está formado por un usuario de correo que existe en Active Directory local y un buzón de correo en la nube asociado que existe en Exchange Online.</p></td>
</tr>
<tr class="odd">
<td><p>Usuario vinculado</p></td>
<td><p>Un usuario vinculado es un usuario cuyo buzón de correo reside en un bosque diferente al bosque donde reside el usuario.</p></td>
</tr>
</tbody>
</table>


## Buzones

Los buzones son el tipo de destinatario más frecuente que usan las personas que trabajan con datos en una organización de Exchange. Cada buzón de correo está asociado a una cuenta de usuario de Active Directory. El usuario puede usar el buzón para enviar y recibir mensajes, así como para almacenar mensajes, citas, tareas, notas y documentos. Los buzones representan las principales herramientas de mensajería y colaboración para los usuarios de su organización de Exchange.

## Componentes del buzón de correo

Cada buzón de correo está compuesto por un usuario de Active Directory y los datos de buzón se almacenan en la base de datos de buzones de correo de Exchange (tal como se muestra en la figura siguiente). Todos los datos de configuración para el buzón de correo se almacenan en los atributos de Exchange del objeto de usuario Active Directory. La base de datos de buzones de correo contiene los datos que se encuentran en el buzón de correo asociado a la cuenta de usuario.


> [!IMPORTANT]
> Cuando se crea un buzón de correo para un usuario nuevo o existente, los atributos de Exchange necesarios para un buzón de correo se agregan al objeto de usuario en Active Directory. Los datos de buzón de correo asociados no se crean hasta que el buzón de correo recibe un mensaje o el usuario inicia una sesión en él.



**Componentes del buzón de correo**

![Partes que componen un buzón](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "Partes que componen un buzón")


> [!WARNING]
> Si quita un buzón de correo, los datos del buzón almacenados en la base de datos de buzones de correo de Exchange&nbsp;se marcarán para ser eliminados y la cuenta de usuario asociada se borrará también de Active Directory. Para conservar la cuenta de usuario y borrar solo los datos de buzón de correo, deshabilite el buzón.



## Tipos de buzones de correo

Exchange es compatible con los tipos de buzones de correo siguientes:

  - **Buzones de usuario   **Los buzones de usuario que se asignan a usuarios individuales en la organización de Exchange. Los buzones de usuario ofrecen a los usuarios una rica plataforma para la colaboración. Los usuarios pueden enviar y recibir mensajes, administrar sus contactos, programar reuniones y actualizar una lista de tareas. Pueden hacer también que se entreguen mensajes de correo de voz en sus buzones. Los buzones de usuario son el tipo de buzón de correo más usado y el que normalmente se asigna a los usuarios de su organización.

  - **Buzones vinculados**   Los buzones vinculados son buzones de correo a los que los usuarios obtienen acceso en un bosque de confianza independiente. Es posible que los buzones vinculados sean necesarios para organizaciones que eligen implementar Exchange en un bosque de recursos. El caso del bosque de recursos permite a una organización centralizar Exchange en un único bosque, a la vez que permite tener acceso a la organización de Exchange con cuentas de usuario en uno o más bosques de confianza.
    
    Como se mencionó anteriormente, todos los buzones de correo deben tener una cuenta de usuario asociada. No obstante, la cuenta de usuario que tendrá acceso al buzón vinculado no existe en el bosque en el que se ha implementado Exchange. Por ello, hay una cuenta de usuario deshabilitada en el mismo bosque de Exchange que está asociada a cada buzón vinculado. La figura siguiente ilustra la relación entre la cuenta de usuario vinculada usada para tener acceso al buzón vinculado y la cuenta de usuario deshabilitada en el bosque de recursos de Exchange asociada al buzón vinculado.
    
    **Buzón vinculado**
    
    ![Organización de Exchange compleja con bosque de recursos](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organización de Exchange compleja con bosque de recursos")  

  - **Buzón de correo de Office 365   **Cuando crea un buzón de correo de Office 365 en Exchange Online en una implementación híbrida, el usuario de correo se crea en Active Directory local. La sincronización de directorios, si se ha configurado, sincroniza automáticamente este nuevo objeto de usuario con Office 365, donde se convierte en un buzón de correo en la nube en Exchange Online. Puede crear buzones de correo de Office 365 como buzones de correo de usuario regulares, buzones de recursos para salas de reuniones y equipos y buzones de correo compartidos.

  - **Buzones compartidos**   Los buzones compartidos no están asociados principalmente a usuarios individuales y, generalmente, se configuran para permitir el acceso de varios usuarios.
    
    A pesar de que se pueden asignar permisos de acceso adicionales de inicio de sesión de usuarios para cualquier tipo de buzón de correo, los buzones compartidos son específicos para esta funcionalidad. El usuario de Active Directory asociado a un buzón de correo compartido debe ser una cuenta deshabilitada. Después de crear un buzón de correo compartido, deberá asignar permisos a todos los usuarios que necesiten acceso al buzón de correo compartido.

  - **Buzones de recursos**   Los buzones de recursos son buzones especiales diseñados para usarse en la programación de recursos. Al igual que todos los tipos de buzones de correo, un buzón de recursos tiene asociada una cuenta de usuario de Active Directory, pero debe ser una cuenta deshabilitada. A continuación se enumeran los tipos de buzones de recursos:
    
      - **Buzones de sala**   Estos buzones de correo se asignan a ubicaciones de reuniones, como salas de reuniones, auditorios y aulas de aprendizaje.
    
      - **Buzones de equipo**   Estos buzones de correo se asignan a recursos sin una ubicación específica como, por ejemplo, equipos portátiles, proyectores, micrófonos o incluso automóviles de empresa.
    
    Puede incluir ambos tipos de buzones de recursos como recursos en las solicitudes de reuniones, ya que constituyen un medio sencillo y eficaz para que los usuarios usen los recursos. Puede configurar buzones de recursos para que procesen automáticamente solicitudes entrantes de reunión basándose en las directivas de reserva de recursos definidas por los propietarios del recurso. Por ejemplo, puede configurar una sala de conferencias para que acepte automáticamente solicitudes entrantes de reunión salvo de reuniones repetitivas, que pueden estar sujetas a la aprobación del propietario del recurso.

## Buzones del sistema

Exchange crea los buzones del sistema en el dominio raíz del bosque de Active Directory durante la instalación. Los usuarios y los administradores no pueden iniciar sesión en estos buzones. Los buzones de sistema se crean para las características de Exchange como la mensajería unificada (MU), la migración, la aprobación de mensajes y la Exhibición de documentos electrónicos en contexto. Esta tabla muestra información acerca de los buzones del sistema tal como se muestran en Active Directory.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Buzón de correo</th>
<th>Nombre</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization</p></td>
<td><p>SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
</tr>
<tr class="even">
<td><p>Aprobación de mensajes</p></td>
<td><p>SystemMailbox {1f05a927-<em>xxxx</em>- <em>xxxx</em> - <em>xxxx</em> -<em>xxxxxxxxxxxx</em>}</p>
<p>donde <em>x</em> es un número exclusivo asignado de forma aleatoria para cada bosque de Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Almacenamiento de datos de mensajería unificada</p></td>
<td><p>SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
</tr>
<tr class="even">
<td><p>Detección</p></td>
<td><p>DiscoverySearchMailbox {D919BA05-46A6-415f-80AD-7E09334BB852}</p></td>
</tr>
<tr class="odd">
<td><p>Correo electrónico federado</p></td>
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
</tr>
<tr class="even">
<td><p>Migración</p></td>
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
</tr>
</tbody>
</table>


Si desea retirar el último servidor de buzones de correo de Exchange de su organización, en primer lugar, debe deshabilitar los buzones del sistema con el cmdlet [Disable-Mailbox](https://technet.microsoft.com/es-es/library/aa997210\(v=exchg.150\)). Después de decomisar un servidor de buzones de correo que contenga estos buzones de sistemas, debe mover los buzones de correo del sistema a otro servidor de buzones de correo para asegurarse de no perder funcionalidad.

## Planificación de buzones

Los buzones se crean en bases de datos de buzones de correo en servidores de Exchange que tienen instalado el rol de servidor Buzón de correo. Para contribuir a ofrecer una plataforma confiable y eficaz para los usuarios de buzones de correo, es esencial planear en detalle la implementación de los servidores y bases de datos de buzones de correo. Para obtener más información acerca de la planificación de los servidores de buzones de correo y las bases de datos, vea [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Grupos de distribución

Los grupos de distribución son objetos de grupo de Active Directory con correo habilitado que se usan sobre todo para distribuir mensajes a varios destinatarios. Cualquier tipo de destinatario puede ser miembro de un grupo de distribución.


> [!IMPORTANT]
> Tenga en cuenta las diferencias de terminología entre Active Directory y Exchange. En Active Directory, un grupo de distribución es cualquier grupo que no tiene ningún contexto de seguridad con independencia de que esté habilitado para correo. En Exchange, todos los grupos habilitados para correo se denominan grupos de distribución, tengan o no un contexto de seguridad.



Exchange admite los tipos de grupos de distribución siguientes:

  - **Grupos de distribución**   Se trata de objetos de grupos de distribución universal de Active Directory habilitados para correo. Solamente se pueden usar para distribuir mensajes a un grupo de destinatarios.

  - **Grupos de seguridad habilitados para correo**   Se trata de grupos de seguridad universal de Active Directory habilitados para correo. Se pueden usar para asignar permisos de acceso a recursos en Active Directory y también para distribuir mensajes.

  - **Grupos no universales habilitados para correo**   Se trata de objetos de grupos globales o locales de Active Directory habilitados para correo. Solamente puede crear o habilitar para correo grupos de distribución universal. Es posible que tenga grupos habilitados para correo que migraron de versiones anteriores de Exchange que no son grupos universales. Estos grupos aún pueden administrarse mediante el EAC o el Shell.
    

    > [!NOTE]
    > Para convertir un grupo de dominio local o global en un grupo universal, puede usar el cmdlet <A href="https://technet.microsoft.com/es-es/library/bb123770(v=exchg.150)">Set-Group</A> del Shell.



## Grupos de distribución dinámicos

Los grupos de distribución dinámica son grupos de distribución cuya pertenencia se basa en filtros de destinatarios específicos en vez de basarse en un grupo de destinatarios definido.

A diferencia de los grupos de distribución normales, la lista de miembros para grupos de distribución dinámicos se calcula cada vez que se les envía un mensaje en base a los filtros y condiciones definidos. Cuando se envía un mensaje de correo electrónico a un grupo de distribución dinámica, éste se entrega a todos los destinatarios de la organización que coincidan con el criterio definido para el grupo de distribución dinámicos.


> [!IMPORTANT]
> Un grupo de distribución dinámico incluye cualquier destinatario de Active Directory que tiene atributos que coinciden con el filtro del grupo cuando se envía el mensaje. Si las propiedades de un destinatario se modifican para que coincidan con el filtro de grupo, ese destinatario podría pasar, inadvertidamente, a ser un miembro del grupo y empezar a recibir mensajes enviados al grupo de distribución dinámico. Unos procesos de aprovisionamiento de cuentas coherentes y bien definidos reducirán las probabilidades de que esto ocurra.



Para ayudarle a crear filtros de destinatario para grupos de distribución dinámico, puede usar filtros prefabricados. Un *filtro predefinido* es un filtro de uso común que puede usar para satisfacer diversos criterios de filtrado de destinatarios. Puede usar estos filtros para especificar los tipos de destinatario que desea incluir en el grupo de distribución dinámica. Además, también puede especificar una lista de condiciones que los destinatarios deben cumplir. Puede crear condiciones prefabricadas a partir de las propiedades siguientes:

  - Atributos personalizados 1–15

  - Estado o provincia

  - Empresa

  - Departamento

  - Contenedor de destinatarios

También puede especificar condiciones basadas en propiedades de destinatario distintas a las detalladas anteriormente. Para ello, debe usar el Shell a fin de crear una consulta personalizada para el grupo de distribución dinámico. Tenga en cuenta que los ajustes de filtro y condición para los grupos de distribución dinámicos que tienen filtros de destinatario personalizados solo se pueden administrar usando el Shell. Encontrará un ejemplo de cómo crear un grupo de distribución dinámico mediante una consulta personalizada en [Administrar grupos de distribución dinámica](manage-dynamic-distribution-groups-exchange-2013-help.md).

## Contactos de correo

Los contactos de correo suelen contener información acerca de personas u organizaciones externas a la organización de Exchange. Los contactos de correo pueden aparecer en la libreta de direcciones (también denominada la lista global de direcciones o GAL) y en otras listas de direcciones, y se pueden agregar como miembros a grupos de distribución. Cada contacto tiene una dirección externa de correo electrónico y todos los mensajes de correo electrónico enviados a ese contacto se reenviarán automáticamente a dicha dirección. Los contactos son perfectos para representar a personas externas a la organización de Exchange (en la lista de direcciones compartida) que no precisan acceso a ningún recurso interno. Los siguientes son tipos de contactos de correo:

  - **Contactos de correo**   Estos son contactos de Active Directory habilitados para correo que contienen información acerca de personas u organizaciones que existen fuera de su organización de Exchange.

  - **Contactos de bosque de correo**   Representan objetos de destinatario procedentes de otro bosque. Estos contactos suelen ser creados mediante la sincronización de directorios. Los contactos de bosque de correo son objetos de destinatario de solo lectura que solo se actualizan o se quitan a través de una sincronización. No puede usar interfaces de administración de Exchange para modificar o quitar un contacto de bosque de correo.

## Usuarios de correo

Los usuarios de correo son similares a los contactos de correo. Ambos tienen direcciones de correo electrónico externas y contienen información acerca de personas no pertenecientes a la organización de Exchange. Ambos se pueden mostrar en la GAL y en otras listas de direcciones. Sin embargo, a diferencia de un contacto de correo, los usuarios de correo tienen credenciales de inicio de sesión de Active Directory y tienen acceso a los recursos para los que se les ha asignado permisos.

Si una persona externa a su organización necesita acceso a recursos en su red, cree un usuario de correo en lugar de un contacto de correo. Por ejemplo, puede que desee crear usuarios de correo para consultores a corto plazo que requieran acceso a la infraestructura del servidor aunque usen sus propias direcciones de correo electrónico externas.

También se pueden crear usuarios de correo en la organización para usuarios que no desean tener un buzón de correo de Exchange. Por ejemplo, después de una adquisición, la compañía adquirida podría conservar su infraestructura de mensajería separada, pero aun así necesitará acceso a los recursos de su red. Para estos usuarios, cree usuarios de correo en lugar de usuarios de buzón.


> [!NOTE]
> En el EAC, use la página <STRONG>Destinatarios</STRONG> &gt; <STRONG>Contactos</STRONG> para crear y administrar usuarios de correo. No hay un ninguna página separada para usuarios de correo.



## Carpetas públicas habilitadas para correo

Las carpetas públicas tienen la finalidad de servir como un almacén de información compartido por muchos usuarios. El hecho de habilitar una carpeta pública para correo genera un nivel adicional de funcionalidad para los usuarios. Además de poder registrar mensajes en la carpeta, los usuarios pueden enviar mensajes de correo electrónico a la carpeta pública y, en algunos casos, recibir mensajes de correo electrónico de la misma. Cada carpeta habilitada para correo incluye un objeto en Active Directory que almacena su dirección de correo electrónico, el nombre de la libreta de direcciones y otros atributos relativos al correo.

Puede administrar las carpetas públicas usando el EAC o el Shell. Para obtener más información acerca de la administración de carpetas públicas, vea [Carpetas públicas](public-folders-exchange-2013-help.md).

## Destinatario de Microsoft Exchange

El destinatario de Microsoft Exchange es un objeto de destinatario especial que proporciona un remitente de mensajes unificado y conocido que diferencia mensajes generados por el sistema de otros mensajes. Reemplaza el remitente Administrador de sistema usado para mensajes generados por el sistema de versiones anteriores de Exchange.

El destinatario de Microsoft Exchange no es un objeto de destinatario típico, como un buzón de correo, un usuario de correo o un contacto de correo, y no se administra mediante las herramientas de destinatario típicas. Sin embargo, puede usar el cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)) del Shell para configurar el destinatario de Microsoft Exchange.


> [!NOTE]
> Cuando se envían mensajes generados por el sistema a un remitente externo, el destinatario de Microsoft Exchange no se usa como remitente del mensaje. En su lugar, se usa la dirección de correo electrónico especificada por el parámetro&nbsp;<EM>ExternalPostmasterAddress</EM> en el cmdlet&nbsp;<A href="https://technet.microsoft.com/es-es/library/bb124151(v=exchg.150)">Set-TransportConfig</A>.



## Documentación de los destinatarios

La tabla siguiente contiene vínculos a temas que le ayudarán a aprender acerca de y a administrar los destinatarios de Exchange.


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
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Crear buzones de usuario</a></p></td>
<td><p>Obtenga más información sobre cómo crear buzones de usuario con el Centro de administración de Exchange o el Shell de administración de Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">Administrar los buzones de usuario</a></p></td>
<td><p>Más información acerca de cómo crear buzones de correo de usuarios, cambiar propiedades del buzón de correo y editar de forma masiva las propiedades seleccionadas de varios buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-mailboxes-exchange-2013-help.md">Administrar buzones vinculados</a></p></td>
<td><p>Más información acerca de los requisitos para los buzones de correo vinculados, cómo crear y vincularlos a una cuenta maestro, y cambiar las propiedades del buzón de correo vinculadas.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-and-manage-distribution-groups-exchange-2013-help.md">Crear y administrar grupos de distribución</a></p></td>
<td><p>Más información acerca de cómo crear y administrar grupos de distribución y crear una directiva de nomenclatura de grupo para su organización.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-mail-enabled-security-groups">Administrar grupos de seguridad habilitados para correo</a></p></td>
<td><p>Más información acerca de cómo crear y administrar grupos de seguridad habilitados para correo.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-dynamic-distribution-groups-exchange-2013-help.md">Administrar grupos de distribución dinámica</a></p></td>
<td><p>Más información acerca de cómo crear grupos de distribución dinámicos y administrar las propiedades del grupo de distribución dinámico, como el uso de los atributos personalizados y otras propiedades para determinar la pertenencia al grupo.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-mail-contacts">Administrar contactos de correo</a></p></td>
<td><p>Más información acerca de cómo crear y administrar contactos de correo.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-mail-users">Administrar usuarios de correo</a></p></td>
<td><p>Más información acerca de cómo crear y administrar usuarios de correo.</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-and-manage-room-mailboxes-exchange-2013-help.md">Creación y administración de buzones de sala</a></p></td>
<td><p>Más información acerca de cómo crear buzones de correo y administrar propiedades del buzón de correo de sala, como habilitar reuniones periódicas y configurar opciones de reservas y programación.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-equipment-mailboxes-exchange-2013-help.md">Administrar buzones de correo de equipamiento</a></p></td>
<td><p>Más información acerca de cómo crear buzones de correo de equipos, configurar opciones de reservas y programación y administrar otras propiedades de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p><a href="disconnected-mailboxes-exchange-2013-help.md">Buzones desconectados</a></p></td>
<td><p>Obtenga más información acerca de los dos tipos de buzones desconectados y cómo trabajar con ellos.</p></td>
</tr>
<tr class="even">
<td><p><a href="custom-attributes-exchange-2013-help.md">Atributos personalizados</a></p></td>
<td><p>Obtenga información acerca de cómo agregar información sobre un destinatario usando los atributos personalizados.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/bb124268(v=exchg.150)">Filtros en los comandos de Shell del destinatario</a></p></td>
<td><p>Obtenga información sobre cómo usar filtros predefinidos o personalizados con comandos para filtrar un conjunto de destinatarios.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-permissions-for-recipients-exchange-online-help.md">Administrar permisos para los destinatarios</a></p></td>
<td><p>Obtenga información sobre cómo usar el EAC o el Shell para asignar permisos a usuarios y grupos.</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatic-mailbox-distribution-exchange-2013-help.md">Distribución automática de buzones</a></p></td>
<td><p>Obtenga información sobre cómo funciona la distribución automática de buzones y cómo controlar qué bases de datos de buzones de correo se seleccionan para buzones nuevos y buzones movidos.</p></td>
</tr>
</tbody>
</table>

