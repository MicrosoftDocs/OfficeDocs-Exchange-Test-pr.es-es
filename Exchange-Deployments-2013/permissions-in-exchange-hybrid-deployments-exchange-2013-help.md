---
title: 'Permisos en implementaciones híbridas de Exchange: Exchange 2013 Help'
TOCTitle: Permisos en implementaciones híbridas de Exchange
ms:assetid: 58b46b2c-a6b2-424a-8fc2-0f1fe1ad8e18
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ906433(v=EXCHG.150)
ms:contentKeyID: 51406224
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permisos en implementaciones híbridas de Exchange

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2018-05-02_

La organización de Exchange Online de Office 365 está basada en Exchange Server y, como sucede con las organizaciones locales, también usa el control de acceso basado en roles (RBAC) para controlar los permisos. Los permisos se otorgan a los administradores usando grupos de roles de administración, mientras que los permisos a los usuarios finales se otorgan mediante directivas de asignación de roles de administración.

Encontrará más información acerca de los permisos en Exchange Online y en implementaciones de Exchange locales en: [Permisos](https://technet.microsoft.com/es-es/library/dd351175\(v=exchg.150\))

## Permisos de administrador

De forma predeterminada, el usuario que se usó para crear el inquilino de Office 365 se convierte en miembro del grupo de roles de Administración de organización de la organización Exchange Online. Este usuario puede administrar toda la organización de Exchange Online, incluida la configuración en el nivel de la organización y la administración de los destinatarios de Exchange Online.

También puede agregar administradores adicionales en la organización de Exchange Online, según las necesidades de administración que deban llevarse a cabo. Por ejemplo, puede agregar administradores de organización y administradores de destinatarios adicionales, habilitar usuarios especialistas para realizar tareas de cumplimiento, como detección y configuración de permisos personalizados y mucho más. Toda la administración de permisos de Exchange Online para los administradores Office 365 se debe realizar en la organización de Exchange Online usando el EAC de Exchange o PowerShell remoto.


> [!IMPORTANT]
> No habrá transferencia de permisos entre la organización local y la organización de Office 365. Los permisos definidos en la organización local se deben recrear en la organización de Office&nbsp;365.



Para obtener más información, consulte [Administrar grupos de roles](https://technet.microsoft.com/es-es/library/jj657480\(v=exchg.150\)) y [Administrar miembros de grupos de roles](https://technet.microsoft.com/es-es/library/jj657492\(v=exchg.150\)).

## Delegar permisos de buzón

En las implementaciones de Exchange local, los usuarios pueden tener una variedad de permisos a los buzones de otros usuarios. Esto se denomina permisos de delegado del buzón y su útil cuando necesita un Ayudante administrativo para administrar parte de buzón de otro usuario; Por ejemplo, administración de calendario de un ejecutivo. Implementaciones de híbrido de Exchange admiten el uso de algunos, pero no todos, los permisos de buzón entre buzones ubicados en una organización de Exchange local y buzones ubicados en Office 365. Las secciones siguientes detallan los permisos que son y no son compatibles; configuración adicional necesaria para admitir permisos de buzón híbrido; y cómo se sincronizan los permisos de buzón entre la organización local y Office 365.

## Permisos de buzón que se admite en entornos híbridos

Los permisos siguientes **son** compatibles:

  - **Acceso total** Un buzón en un servidor de Exchange local puede tener concedido el permiso de **Acceso completo** a un buzón de Office 365 y viceversa. Por ejemplo, un buzón de Office 365 puede concederse el permiso de **Acceso completo** a un buzón compartido local. Los usuarios necesitan abrir el buzón mediante el cliente de escritorio de Outlook; no se admiten permisos de buzón entre locales en Outlook en el web.
    

    > [!NOTE]
    > Es posible que se pidan nuevamente las credenciales a los usuarios la primera vez que estos accedan a un buzón ubicado en la otra organización y lo agreguen a su perfil de Outlook.



  - **Enviar en nombre de** Un buzón en un servidor de Exchange local puede tener concedido el permiso **Enviar en nombre de** un buzón de Office 365 y viceversa. Por ejemplo, un buzón de Office 365 puede concederse el permiso **Enviar en nombre de** a un buzón compartido local. Los usuarios necesitan abrir el buzón mediante el cliente de escritorio de Outlook; no se admiten permisos de buzón entre locales en Outlook en el web.
    
    Son necesarios algunos cambios en el servidor de directorio activo Azure Connect para enviar en nombre de permisos para la sincronización entre los servidores de Exchange locales y Exchange Online. Para obtener más información, vea Habilitar compatibilidad con permisos de buzón híbrido en Azure Active Directory conectar más adelante en este tema.

  - **Folder permissions** Grants access to the contents of a particular folder.

  - **Elementos privados** Cuando se agrega que un delegado la opción puede configurarse para permitir que a un usuario con permisos de carpeta para ver los elementos de calendario privados.


> [!NOTE]
> A partir de febrero de 2018 la característica soportan el acceso total, enviar en nombre de y carpeta derechos entre bosques se está distribuyendo y deben ser completado por abril de 2018.



Las siguientes capacidades o permisos **no** compatibles:

  - **Send-As** Permite a un usuario enviar correo como si parece provenir de buzón de otro usuario.

  - **Auto-mapping** Permite a Outlook, cuando se inicia, para abrir automáticamente los buzones que se ha concedido **Acceso completo** a un usuario.

Es necesario mover al mismo tiempo que el buzón concede todos los buzones que reciban estos permisos de otro buzón. Si un buzón recibe permisos de varios buzones, ese buzón y todos los buzones a la concesión de permisos, deben moverse al mismo tiempo.

## Configuración de los servidores de Exchange locales para admitir permisos de buzón híbrido

Para habilitar el acceso total y enviar en nombre de permisos en una implementación híbrida, configuración adicional cambios puede ser necesarios dependiendo de la versión de Exchange que se ha instalado. La siguiente tabla muestra qué versiones de Exchange admiten permisos de buzón delegada en una implementación híbrida con Office 365 y qué configuración adicional es necesaria. Para conocer los pasos acerca de cómo configurar Exchange 2013 y 2010 los buzones y servidores para admitir las ACL, consulte [Configurar Exchange para admitir permisos de buzón delegada en una implementación híbrida](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versión de Exchange</th>
<th>Requisitos previos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2016</p></td>
<td><p>No requerida ninguna configuración adicional.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p>Los servidores de Exchange de 2013 necesitan lo siguiente:</p>
<ul>
<li><p>La actualización acumulativa más reciente (CU), o el inmediatamente anterior CU, instalado. Servidores de Exchange de 2013 con CUs antiguos no son compatibles y no funcionen con los permisos de buzón delegada en una implementación híbrida.</p></li>
<li><p>La organización de Exchange está configurada para permitir el control de acceso (ACL) que se estampa en objetos de correo electrónico enumera y sincronizado con Office 365.</p></li>
<li><p>Local remotos buzones asociados a buzones de correo que se trasladó a Office 365 antes de CU10 de 2013 de Exchange deben configurarse manualmente para admitir las ACL. Buzones de correo remotos, creada en servidores que ejecutan Exchange 2013 CU10 o posterior y tras el intercambio de organización está configurada para permitir las ACL, se configuran automáticamente.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Servidores de Exchange 2010 SP3 necesitan lo siguiente:</p>
<ul>
<li><p>El último paquete acumulativo (RU), o el inmediatamente anterior RU, instalado. Servidores de Exchange 2010 SP3 con RU anterior no son compatibles y no funcionen con los permisos de buzón delegada en una implementación híbrida.</p></li>
<li><p>Local remotos buzones asociados a Office 365 buzones deben configurarse para admitir las ACL. Esto debe hacerse para cada buzón remoto local que está asociado con un buzón de Office 365.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 o anterior</p></td>
<td><p>No compatible.</p></td>
</tr>
</tbody>
</table>


## Habilitar la compatibilidad para los permisos de buzón híbrido en Azure Active Directory Connect

Además de configurar los servidores de Exchange local, también debe asegurarse de Azure Active Directory Connect (conectar DAA) server está configurado para sincronizar permisos de buzón híbrido. Aquí está lo que necesita hacer para asegurarse de que su servidor DAA conectar está preparado para admitir estos permisos:

  - **Conectar actualización DAA** DAA conectar debe actualizarse como mínimo a la versión 1.1.553.0. Puede descargar la versión más reciente de DAA Connect de [Microsoft Azure Active Directory Connect](http://go.microsoft.com/fwlink/p/?linkid=510956).

  - **Habilitar Exchange híbrido de DAA conectar** Para sincronizar los atributos que habilite los permisos de buzón híbrido (específicamente el permiso Enviar en nombre), debe asegurarse de que está habilitada la opción de configuración de **implementación híbrida de Exchange** en DAA Connect. Para obtener información acerca de cómo ejecutar el Asistente de instalación DAA conectarse otra vez para actualizar su configuración, consulte [sync de Azure Connect AD: ejecutando el Asistente para la instalación de una segunda vez](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnectsync-installation-wizard)

## Cómo se sincronizan los permisos de buzón entre los locales y organizaciones de Office 365

## Permisos de usuario final

Al igual que con los permisos de administrador, se pueden otorgar permisos a los usuarios finales de Exchange Online. De forma predeterminada, se otorgan permisos a los usuarios finales mediante la directiva de asignación de roles predeterminada. Esta directiva se aplica a todos los buzones de la organización de Exchange Online. Si los permisos otorgados de forma predeterminada son suficientes, no necesita cambiar nada.

Si desea personalizar los permisos de usuario final, puede modificar la directiva de asignación de roles predeterminada o puede crear otras directivas de asignación. Si crea varias directivas de asignación, puede asignar diferentes directivas a los diferentes grupos de buzones, lo que le permite controlar los permisos otorgados a cada grupo según sus requisitos. La administración de todos los permisos para los usuarios finales de Exchange Online se debe realizar en la organización de Exchange Online a través del EAC o de PowerShell remoto.

Como los permisos de administrador, los permisos de usuarios finales no se transfieren entre la organización local y la organización de Exchange Online. Los permisos definidos en la organización local se deben volver a crear en la organización de Exchange Online.

Para obtener más información, consulte [Administrar directivas de asignación de funciones](https://technet.microsoft.com/es-es/library/jj657511\(v=exchg.150\)) y [Cambiar la directiva de asignación en un buzón](https://technet.microsoft.com/es-es/library/dd638076\(v=exchg.150\)).

En la tabla siguiente se muestra una lista de los permisos otorgados por las directivas de asignación de roles predeterminadas de la organización de Exchange Online.

### Permisos de directiva de asignación de roles predeterminada

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de administración</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyTeamMailboxes</p></td>
<td><p>El rol de administración <code>MyTeamMailboxes</code> permite que los usuarios individuales creen buzones de sitio y los conecten a los sitios de Microsoft SharePoint.</p></td>
</tr>
<tr class="even">
<td><p>Mis aplicaciones del mercado</p></td>
<td><p>El rol de administración de <code>My Marketplace Apps</code> permite a los usuarios individuales ver y modificar sus aplicaciones del mercado de Microsoft Office.</p></td>
</tr>
<tr class="odd">
<td><p>MyBaseOptions</p></td>
<td><p>La función de administración <code>MyBaseOptions</code> permite que los usuarios individuales vean y modifiquen la configuración básica de sus propios buzones y las configuraciones asociadas.</p></td>
</tr>
<tr class="even">
<td><p>MyContactInformation</p></td>
<td><p>La función de administración <code>MyContactInformation</code> permite a los usuarios individuales modificar su información de contacto, por ejemplo, la dirección y los números telefónicos.</p></td>
</tr>
<tr class="odd">
<td><p>MyDistributionGroupMembership</p></td>
<td><p>La función de administración <code>MyDistributionGroupMembership</code> permite que los usuarios individuales vean y modifiquen su pertenencia a grupos de distribución de una organización, siempre que dichos grupos de distribución permitan la manipulación de la pertenencia a grupos.</p></td>
</tr>
<tr class="even">
<td><p>MyDistributionGroups</p></td>
<td><p>La función de administración <code>MyDistributionGroups</code> permite a los usuarios individuales crear, modificar y ver grupos de distribución, y modificar, ver, quitar y agregar miembros a grupos de distribución de los que son propietarios.</p></td>
</tr>
<tr class="odd">
<td><p>MyMailSubscription</p></td>
<td><p>El rol <code>MyMailSubscription</code> permite a los usuarios individuales ver y modificar su configuración de suscripción de correo electrónico, como la configuración predeterminada del protocolo y el formato del mensaje.</p></td>
</tr>
<tr class="even">
<td><p>MyProfileInformation</p></td>
<td><p>La función de administración de <code>MyProfileInformation</code> permite modificar el nombre de los usuarios individuales.</p></td>
</tr>
<tr class="odd">
<td><p>MyRetentionPolicies</p></td>
<td><p>La función de administración <code>MyRetentionPolicies</code> permite que los usuarios individuales puedan tener acceso a sus etiquetas de retención, además de ver y modificar la configuración y la predeterminación de dichas etiquetas.</p></td>
</tr>
<tr class="even">
<td><p>MyTextMessaging</p></td>
<td><p>La función de administración de <code>MyTextMessaging</code> permite que los usuarios individuales creen, vean y modifiquen las configuraciones de sus mensajes de texto.</p></td>
</tr>
<tr class="odd">
<td><p>MyVoiceMail</p></td>
<td><p>La función de administración de <code>MyVoiceMail</code> permite que los usuarios individuales vean y modifiquen las configuraciones de su correo de voz.</p></td>
</tr>
<tr class="even">
<td><p>Mis aplicaciones ReadWriteMailbox</p></td>
<td><p>El rol de administración <code>My ReadWriteMailbox Apps</code> permite a los usuarios instalar aplicaciones con permisos ReadWriteMailbox.</p></td>
</tr>
<tr class="odd">
<td><p>Mis aplicaciones personalizadas</p></td>
<td><p>El rol de administración <code>My Custom Apps</code> permite a los usuarios ver y modificar sus aplicaciones personalizadas.</p></td>
</tr>
</tbody>
</table>

