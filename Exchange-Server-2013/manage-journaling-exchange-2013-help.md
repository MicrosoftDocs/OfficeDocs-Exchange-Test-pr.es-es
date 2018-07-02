---
title: 'Administrar registro en diario: Exchange 2013 Help'
TOCTitle: Administrar registro en diario
ms:assetid: d517f27e-f80a-4a06-988c-cbbf981c701d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ651670(v=EXCHG.150)
ms:contentKeyID: 49895937
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar registro en diario

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

El registro en diario puede ayudar a la organización a responder a los requisitos de cumplimiento legal, normativo y organizativo mediante el registro de las comunicaciones de correo electrónico entrantes y salientes. En este tema, se muestra cómo realizar tareas básicas relacionadas con la administración del registro en diario en Exchange 2013 y Exchange Online.

El registro en diario estándar está configurado en una base de datos de buzones de correo. Permite al agente de registro en diario registrar todos los mensajes enviados o recibidos a través de los buzones ubicados en una base de datos de buzones de correo. También puede usar el registro en diario premium, que le permite al agente de registro en diario realizar registros más individualizados mediante el uso de reglas de diario. En lugar de registrar en diario todos los buzones de una base de datos, es posible configurar reglas de diario que concuerden con las necesidades de la organización, registrando en diario destinatarios o miembros de grupos de distribución individuales. Para usar registro en diario premium debe tener una licencia de acceso de cliente (CAL) de servidor empresarial de Exchange.

Para obtener más información acerca del registro en diario, consulte [Registro en diario](journaling-exchange-2013-help.md).

**Contenido**

Creación de una regla de diario

Ver o modificar una regla de diario

Habilitar o deshabilitar una regla de diario

Quitar una regla de diario

Habilitar o deshabilitar el registro en diario por base de datos de buzones de correo

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro en diario" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Se ha creado un buzón de correo de registro en diario o hay un buzón existente disponible para usarse como buzón de correo de registro en diario. No puede designar un buzón de Exchange Online como buzón de registro en diario. Se pueden entregar informes de registro en diario a un sistema de archivado local o a un servicio de archivado de terceros. Si va a ejecutar una implementación híbrida con buzones divididos entre los servidores locales y Exchange Online, puede designar un buzón local como el buzón de registro en diario para los buzones locales y de Exchange Online.
    

    > [!IMPORTANT]
    > Si ha configurado una regla de registro en diario en Exchange Online para enviar los informes de diario a un buzón de correo de registro en diario que no exista o que sea un destino no válido, el informe de diario permanecerá en la cola de transporte en los servidores del centro de datos de Microsoft. Si esto ocurre, el personal del centro de datos de Microsoft intentará ponerse en contacto con su organización y le solicitará que corrija el problema para que puedan entregarse correctamente los informes de diario a un buzón de correo de diario. Si tras dos días de ponerse en contacto no ha resuelto el problema, Microsoft deshabilitará la regla de registro en diario problemática.



  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>. Si tiene problemas con el buzón <STRONG>JournalingReportDNRTo</STRONG>, vea <A href="https://go.microsoft.com/fwlink/p/?linkid=331674">Las reglas de transporte y buzón de correo en Exchange Online no funcionan como se esperaba</A>.



## Creación de una regla de diario

## Usar el EAC para crear una regla de diario

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Reglas de diario** y, luego, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En **Regla de diario**, proporcione un nombre para la regla de diario y, luego, complete los siguientes campos:
    
      - **Si el mensaje se envía o se recibe**   Especifique el destinatario que la regla tendrá como objetivo. Puede seleccionar un destinatario específico o aplicar la regla a todos los mensajes.
    
      - **Incluir en el diario los siguientes mensajes**   Especifique el ámbito de la regla de diario. Puede registrar en diario solo los mensajes internos, solo los mensajes externos o todos los mensajes independientemente del origen o del destino.
    
      - **Enviar informes de diario a**   Escriba la dirección del buzón de correo de registro en diario que recibirá todos los informes del diario.
        

        > [!NOTE]
        > También puede escribir el nombre para mostrar o el alias de un usuario de correo o un contacto de correo como buzón de correo del diario. En este caso, los informes de diario se enviarán a la dirección de correo electrónico externa del usuario de correo o contacto de correo. Pero como se ha explicado anteriormente, la dirección de correo electrónico externa de un usuario de correo o contacto de correo no puede ser la dirección de un buzón de Exchange Online.



3.  Haga clic en **Guardar** para crear la regla de diario.

## Usar Shell para crear una regla de diario

Este ejemplo crea la regla de diario Destinatarios de diario de detección para registrar todos los mensajes que envía y recibe el destinatario usuario1@contoso.com.

    New-JournalRule -Name "Discovery Journal Recipients" -Recipient user1@contoso.com -JournalEmailAddress "Journal Mailbox" -Scope Global -Enabled $True

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la regla de diario se creó correctamente, siga uno de estos pasos:

  - Desde el EAC, compruebe que la nueva regla de diario que creó se incluye en la pestaña **Reglas de diario**.

  - Desde el Shell, compruebe que exista la nueva regla de diario. Para ello, ejecute el siguiente comando (el ejemplo a continuación comprueba la regla creada en el ejemplo de Shell anterior):
    
        Get-JournalRule "Discovery Journal Recipients"

Volver al principio

## Ver o modificar una regla de diario

## Usar el EAC para ver o modificar una regla de diario

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Reglas de diario**.

2.  En la vista de lista, verá todas las reglas de diario de su organización.

3.  Haga doble clic en la regla que desee ver o modificar.

4.  En **Regla de diario**, modifique la configuración que desee. Para obtener más información acerca de la configuración de este cuadro de diálogo, consulte el procedimiento Usar el EAC para crear una regla de diario mencionado anteriormente en este tema.

## Usar el Shell para ver o modificar una regla de diario

En este ejemplo, se muestra una lista a modo de resumen de todas las reglas de diario de la organización de Exchange:

    Get-JournalRule

En este ejemplo se recupera la regla de diario Brokerage Journal Rule y se canaliza el resultado al comando **Format-List** para mostrar las propiedades de la regla en formato de lista:

    Get-JournalRule "Brokerage Journal Rule" | Format-List

Si desea modificar las propiedades de una regla específica, tiene que usar el cmdlet [Set-JournalRule](https://technet.microsoft.com/es-es/library/bb125010\(v=exchg.150\)). En este ejemplo se cambia el nombre de la regla de diario `JR-Sales` por `TraderVault`. También se cambian las reglas siguientes:

  - Destinatario

  - JournalEmailAddress

  - Ámbito

<!-- end list -->

    Set-JournalRule JR-Sales -Name TraderVault -Recipient traders@woodgrovebank.com -JournalEmailAddress tradervault@woodgrovebank.com -Scope Internal

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la regla de diario se modificó correctamente, siga uno de estos pasos:

  - Desde el EAC, vaya a **Administración de cumplimiento** \> **Reglas de diario**. Haga doble clic en la regla que ha modificado y compruebe que se hayan guardado los cambios.

  - Desde el Shell, compruebe que modificó la regla de diario correctamente. Para ello, ejecute el siguiente comando. Este comando detallará las propiedades que modificó junto con el nombre de la regla (el ejemplo a continuación comprueba la regla modificada en el ejemplo de Shell anterior):
    
        Get-TransportRule "TraderVault" | Format-List Name,Recipient,JournalEmailAddress,Scope

Volver al principio

## Habilitar o deshabilitar una regla de diario


> [!IMPORTANT]
> Cuando deshabilita una regla de diario, el agente de registro en diario dejará de registrar los mensajes objeto de esa regla. Cuando una regla de diario se deshabilita, los mensajes que la regla normalmente registraría en diario no se registran. Asegúrese de no poner en riesgo los requisitos normativos o de cumplimiento de su organización al deshabilitar una regla de diario.



## Usar el EAC para habilitar o deshabilitar una regla de diario

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Reglas de diario**.

2.  En la vista de lista, en la columna **Activado** junto al nombre de la regla, seleccione la casilla para habilitar la regla o anule la selección para deshabilitarla.

## Uso del Shell para habilitar o deshabilitar una regla de diario

En este ejemplo se habilita la regla Contoso.

    Enable-JournalRule "Contoso Journal Rule"

En este ejemplo se deshabilita la regla Contoso.

    Disable-JournalRule "Contoso Journal Rule"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la regla de diario se habilitó o deshabilitó correctamente, siga uno de estos pasos:

  - Desde el EAC, vea la lista de reglas de diario y compruebe el estado de la casilla en la columna **Activado**.

  - Desde el Shell, ejecute el siguiente comando para obtener una lista de todas las reglas de diario de la organización, incluido el estado:
    
        Get-JournalRule | Format-Table Name,Enabled

Volver al principio

## Quitar una regla de diario

## Usar el EAC para quitar una regla de diario

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Reglas de diario**.

2.  En la vista de lista, seleccione la regla que desea quitar y, luego, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

## Usar el Shell para quitar una regla de diario

En este ejemplo, se quita la regla de diario de corretaje.

    Remove-JournalRule "Brokerage Journal Rule"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la regla de diario se quitó correctamente, siga uno de estos pasos:

  - Desde el EAC, compruebe que la regla que quitó ya no se incluye en la pestaña **Reglas de diario**.

  - Desde el Shell, ejecute el siguiente comando para comprobar que la regla que quitó ya no se incluye en la lista:
    
        Get-JournalRule

Volver al principio

## Habilitar o deshabilitar el registro en diario por base de datos de buzones de correo


> [!WARNING]
> Deshabilitar el registro en diario de mensajes en una base de datos de buzones de correo puede hacer que su organización infrinja alguna directiva aplicable de retención de mensajería. Cuando deshabilita el registro en diario de mensajes en una base de datos de buzones de correo, no se envían confirmaciones de diario para los mensajes que los buzones de esa base de datos de buzones de correo envían o reciben.



## Usar el EAC para habilitar o deshabilitar el registro en diario por base de datos de buzones de correo

1.  En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  En la vista de lista, haga doble clic en la base de datos de buzones de correo para la que desea habilitar el registro en diario.

3.  Haga clic en **Mantenimiento** y, luego, en **Examinar** junto al cuadro **Destinatario del diario** para seleccionar el buzón de correo de registro. Especificar a un destinatario del diario habilita el registro en diario para la base de datos.
    
    Para deshabilitar el registro en diario, haga clic en **Quitar X** para quitar el destinatario del diario.

## Usar el Shell para habilitar o deshabilitar el registro en diario por base de datos de buzones de correo

En este ejemplo, se habilita el registro en diario para la base de datos de buzones de correo Base de datos de ventas y configura el buzón de diario de dicha base de datos como el destinatario del diario.

    Set-MailboxDatabase "Sales Database" -JournalRecipient "Sales Database Journal Mailbox"

En este ejemplo, se deshabilita el registro en diario por base de datos de buzones de correo en la base de datos de buzones de correo Base de datos de ventas.

    Set-MailboxDatabase "Sales Database" -JournalRecipient $Null

En este ejemplo, se deshabilita el registro en diario por base de datos de buzones de correo en todas las bases de datos de buzones de correo de la organización de Exchange. El cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\)) se utiliza para obtener todas las bases de datos de buzones de correo de la organización Exchange, y los resultados del cmdlet se redireccionan al cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)).

    Get-MailboxDatabase | Set-MailboxDatabase -JournalRecipient $Null

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el registro en diario por base de datos de buzones de correo se habilitó o deshabilitó correctamente, siga uno de estos pasos:

1.  En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  Haga doble clic en la base de datos que desea comprobar y, luego, seleccione la pestaña **Mantenimiento**.

3.  Si en el cuadro **Destinatario del diario** se muestra el correcto destinatario del diario, habilitó correctamente el registro en diario para la base de datos de buzones de correo. Si no se muestra ningún destinatario de diario, el registro en diario está deshabilitado para la base de datos.

<!-- end list -->

  - Desde el Shell, ejecute el siguiente comando para obtener una lista de todas las bases de datos de buzones de correo de la organización, incluidos los destinatarios del diario asociados con ellas. El registro en diario está habilitado para las bases de datos que muestran un destinatario del diario. De lo contrario, está deshabilitado.
    
        Get-MailboxDatabase | Format-Table Name,JournalRecipient

Volver al principio

## Más información

[Registro en diario](journaling-exchange-2013-help.md)

[Deshabilitar o habilitar el registro en diario de correo de voz y notificaciones de llamadas perdidas](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md)

[New-JournalRule](https://technet.microsoft.com/es-es/library/bb125242\(v=exchg.150\))

[Get-JournalRule](https://technet.microsoft.com/es-es/library/aa998866\(v=exchg.150\))

[Set-JournalRule](https://technet.microsoft.com/es-es/library/bb125010\(v=exchg.150\))

[Enable-JournalRule](https://technet.microsoft.com/es-es/library/bb123902\(v=exchg.150\))

[Disable-JournalRule](https://technet.microsoft.com/es-es/library/aa995925\(v=exchg.150\))

[Remove-JournalRule](https://technet.microsoft.com/es-es/library/bb123489\(v=exchg.150\))

[Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\))

