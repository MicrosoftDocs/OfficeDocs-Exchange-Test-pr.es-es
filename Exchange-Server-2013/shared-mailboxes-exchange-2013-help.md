---
title: 'Buzones compartidos: Exchange 2013 Help'
TOCTitle: Buzones compartidos
ms:assetid: 1d71c01b-e261-408e-a633-1d1c9d00032a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150498(v=EXCHG.150)
ms:contentKeyID: 48267867
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Buzones compartidos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-06-04_

Obtenga más información sobre el buzón compartido de Exchange en Microsoft Exchange Server 2013, los motivos para usarlo y cómo convertir un buzón de correo delegado en un buzón compartido de Exchange.

Un buzón compartido es un buzón que pueden abrir varios usuarios para leer y enviar mensajes de correo electrónico. Los buzones compartidos también se pueden usar para brindar un calendario común, que permite que varios usuarios puedan agendar y visualizar días de vacaciones o turnos de trabajo.

No se admiten los buzones compartidos en los dispositivos móviles.

**¿Por qué configurar un buzón compartido?**

  - Proporciona una dirección de correo electrónico genérica (por ejemplo, info@contoso.com o sales@contoso.com), que los clientes pueden usar para hacer consultas sobre su empresa.

  - Permite al personal de los departamentos que proporcionan servicios centralizados a los empleados, (por ejemplo, el departamento de soporte técnico, el de recursos humanos o el de servicios de impresión), responder a las preguntas de los empleados.

  - Permite que varios usuarios supervisen y respondan a los mensajes de correo enviados a una dirección (por ejemplo, una dirección usada especialmente por el departamento de soporte técnico).

## ¿Qué son los buzones compartidos?

Un buzón de correo compartido es un tipo de buzón de correo de usuario que no tiene su propio nombre de usuario y contraseña. Como resultado, los usuarios no pueden iniciar sesión en el buzón directamente. Para obtener acceso a un buzón de correo compartido, los usuarios primero deben obtener permisos para Enviar como o Acceso completo al buzón de correo. Luego, inician sesión en sus propios buzones de correo y, posteriormente, obtienen acceso al buzón de correo compartido agregándolo a su propio perfil de Outlook. En Exchange 2003 y en versiones anteriores, los buzones de correo compartidos eran sólo un buzón de correo regular a los cuales un administrador podía garantizar acceso delegado. A partir de Exchange 2007, los buzones compartidos se convirtieron en su propio tipo de destinatario:

  - **RecipientType:**  UserMailbox

  - **RecipientTypeDetails:**  SharedMailbox

En versiones anteriores de Exchange, la creación de un buzón de correo compartido era un proceso de varios pasos donde tenía que usar el Shell de administración de Exchange para completar algunas de las tareas. En Exchange 2013, puede usar el Centro de administración de Exchange (EAC) para crear un buzón compartido en un paso. Para obtener información más detallada, consulte [Creación de un buzón compartido](create-a-shared-mailbox-exchange-2013-help.md). De hecho, el EAC tiene un área de características dedicada completamente a los buzones de correo compartidos. Simplemente, navegue a **Destinatarios** \> **Buzones de correo compartidos** para ver todas las tareas de administración para los buzones de correo compartidos.

Puede usar los siguientes permisos con un buzón compartido.

  - **Acceso completo** El permiso Acceso completo permite al usuario iniciar sesión en el buzón compartido y actuar como el propietario de ese buzón. Después de tener acceso al buzón compartido, el usuario puede crear elementos de calendario; leer, ver, eliminar y modificar mensajes de correo electrónico; crear tareas y contactos del calendario. Sin embargo, un usuario con un permiso Acceso completo no puede enviar mensajes de correo electrónico desde el buzón compartido a menos que tenga un permiso para Enviar como o En nombre de.

  - **Enviar como**   El permiso para Enviar como le permite al usuario suplantar el buzón compartido al momento de enviar un mensaje de correo. Por ejemplo, si Kweku inicia sesión en el buzón compartido del Departamento de Marketing y envía un mensaje de correo electrónico, aparecerá como si el Departamento de Marketing enviara el mensaje de correo electrónico.

  - **Enviar en nombre de**   El permiso Enviar en nombre de le permite al usuario enviar mensajes en nombre del buzón compartido. Por ejemplo, si John inicia sesión en el buzón compartido del Edificio de recepción 32 y envía un mensaje de correo electrónico, los destinatarios verán el mensaje como enviado por “John en nombre del Edificio de recepción 32”. No puede usar el EAC para conceder permisos de Envío en nombre de; debe usar el cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) con el parámetro *GrantSendonBehalf*.

## Conversión de buzones de correo compartidos

En versiones anteriores de Exchange, era posible usar un buzón de correo regular como buzón de correo delegado. Si tiene buzones delegados, puede usar el Shell para convertirlos en buzones compartidos. Para obtener información más detallada, consulte [Convertir un buzón](https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-user-mailboxes/convert-a-mailbox).

