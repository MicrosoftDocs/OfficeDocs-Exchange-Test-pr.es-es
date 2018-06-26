---
title: 'Creación de un buzón compartido: Exchange 2013 Help'
TOCTitle: Creación de un buzón compartido
ms:assetid: d34bc827-1e83-4a7f-a219-8ba9c19fe24b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150570(v=EXCHG.150)
ms:contentKeyID: 48268729
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creación de un buzón compartido

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**Última modificación del tema:**2016-12-09_

**Tiempo estimado para finalizar: 5 minutos**

Con los buzones compartidos, un grupo de personas de la organización puede supervisar y enviar correo electrónico fácilmente desde una cuenta común, como info@contoso.com o soporte@contoso.com. Cuando una persona del grupo responde a un mensaje enviado al buzón compartido, el correo electrónico aparece como enviado por el buzón compartido, no por el usuario individual.


> [!IMPORTANT]
> Si usa Office 365 para empresas, debe crear el buzón compartido en el Centro de administración de Office 365. 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=834766">Crear buzones compartidos en Office 365</A></P></LI></UL>



Si su organización usa un entorno híbrido de Exchange, debe usar el Centro de administración de Exchange (EAC) local para crear y administrar buzones compartidos. Para obtener más información sobre los buzones compartidos, consulte [Buzones compartidos](shared-mailboxes-exchange-2013-help.md).

## Usar el EAC para crear un buzón compartido

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "buzones de usuario" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

1.  Vaya a **Destinatarios**\>**Compartido**\>**Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  Rellene los campos obligatorios:
    
      - **Nombre para mostrar**
    
      - **Dirección de correo electrónico**

3.  Para conceder los permisos Acceso total o Enviar como, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, luego, seleccione los usuarios a los que quiera conceder los permisos. Puede utilizar la clave **CTRL** para seleccionar varios usuarios. ¿No tiene claro qué permiso debe usar? Vea ¿Qué permisos debe usar?, más adelante en este mismo tema.
    

    > [!NOTE]
    > El permiso Acceso total permite a los usuarios abrir el buzón y crear y modificar los elementos que hay en él. El permiso Enviar como permite a los usuarios que no son el propietario del buzón enviar correo electrónico desde este buzón compartido. Para que el buzón compartido funcione correctamente, se necesitan ambos permisos.



4.  Haga clic en **Guardar** para guardar los cambios y crear el buzón compartido.

## Usar el EAC para editar la delegación de buzones compartidos

1.  Vaya a **Destinatarios**\>**Compartido**\>**Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  Haga clic en **Delegación de buzones**.

3.  Para conceder o quitar los permisos Acceso total y Enviar como, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") o **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") y, luego, seleccione los usuarios a los que quiera conceder los permisos.
    

    > [!NOTE]
    > El permiso Acceso total permite a los usuarios abrir el buzón y crear y modificar los elementos que hay en él. El permiso Enviar como permite a los usuarios que no son el propietario del buzón enviar correo electrónico desde este buzón compartido. Para que el buzón compartido funcione correctamente, se necesitan ambos permisos.



4.  Haga clic en **Guardar** para guardar los cambios.

## Usar un buzón compartido

Para obtener información sobre cómo pueden acceder y usar los usuarios los buzones compartidos, consulte los temas siguientes:

  - [Abrir y usar un buzón compartido en Outlook 2016 y Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=834764)

  - [Abrir y usar un buzón compartido en Outlook en la web para empresas](https://go.microsoft.com/fwlink/p/?linkid=834766)

## Usar el Shell para crear un buzón compartido

Este ejemplo crea el buzón compartido del Departamento de ventas y otorga permisos Acceso completo y Enviar en nombre de para el grupo de seguridad MarketingSG. Se otorgarán los permisos de buzón a los usuarios que sean miembros del grupo de seguridad.


> [!NOTE]
> En este ejemplo, se presupone que ya ha creado el grupo de seguridad MarketingSG y que ese grupo de seguridad está habilitado para correo. Vea <A href="manage-mail-enabled-security-groups-exchange-2013-help.md">Administrar grupos de seguridad habilitados para correo</A>.



    New-Mailbox -Shared -Name "Sales Department" -DisplayName "Sales Department" -Alias Sales | Set-Mailbox -GrantSendOnBehalfTo MarketingSG | Add-MailboxPermission -User MarketingSG -AccessRights FullAccess -InheritanceType All

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [New-Mailbox](https://technet.microsoft.com/es-es/library/aa997663\(v=exchg.150\)).

## ¿Qué permisos debe usar?

Puede usar los siguientes permisos con un buzón compartido.

  - **Acceso completo** El permiso Acceso completo permite al usuario iniciar sesión en el buzón compartido y actuar como el propietario de ese buzón. Después de tener acceso al buzón compartido, el usuario puede crear elementos de calendario; leer, ver, eliminar y modificar mensajes de correo electrónico; crear tareas y contactos del calendario. Sin embargo, un usuario con un permiso Acceso completo no puede enviar mensajes de correo electrónico desde el buzón compartido a menos que tenga un permiso para Enviar como o En nombre de.

  - **Enviar como**   El permiso para Enviar como le permite al usuario suplantar el buzón compartido al momento de enviar un mensaje de correo. Por ejemplo, si Kweku inicia sesión en el buzón compartido del Departamento de Marketing y envía un mensaje de correo electrónico, aparecerá como si el Departamento de Marketing enviara el mensaje de correo electrónico.

  - **Enviar en nombre de**   El permiso Enviar en nombre de le permite al usuario enviar mensajes en nombre del buzón compartido. Por ejemplo, si John inicia sesión en el buzón compartido del Edificio de recepción 32 y envía un mensaje de correo electrónico, los destinatarios verán el mensaje como enviado por “John en nombre del Edificio de recepción 32”. No puede usar el EAC para conceder permisos de Envío en nombre de; debe usar el cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) con el parámetro *GrantSendonBehalf*.

## Más información

Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


