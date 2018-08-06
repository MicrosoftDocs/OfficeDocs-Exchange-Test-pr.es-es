---
title: 'Agregar o quitar direcciones correo electrónico de buzón: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Agregar o quitar direcciones de correo electrónico de un buzón
ms:assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123794(v=EXCHG.150)
ms:contentKeyID: 50556812
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agregar o quitar direcciones de correo electrónico de un buzón

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Puede configurar más de una dirección de correo electrónico para el mismo buzón de correo. Las direcciones adicionales se denominan *direcciones proxy*. Una dirección proxy permite a un usuario recibir el correo que se envía a otra dirección de correo electrónico. Todos los mensajes de correo electrónico que se envíen a la dirección proxy del usuario se entregan a la dirección de correo electrónico principal, también conocida como la *dirección SMTP principal* o la *dirección de respuesta predeterminada*.


> [!IMPORTANT]
> Si usa Office 365 para empresas, debe agregar o quitar direcciones de correo electrónico para los buzones de usuario en el <A href="https://go.microsoft.com/fwlink/p/?linkid=8347775">Centro de administración de Office 365: Agregar alias de correo electrónico adicionales a un usuario en Office 365</A>



Para tareas de administración adicionales relacionadas con la administración de destinatarios, consulte la tabla "Documentación de destinatarios" en [Destinatarios](recipients-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Los procedimientos de este tema le muestran cómo agregar o eliminar direcciones de correo electrónico para un buzón de correo de usuario. Puede usar procedimientos similares para agregar o eliminar direcciones de correo electrónico para otros tipos de destinatarios.

## ¿Qué desea hacer?

## Agregar una dirección de correo electrónico a un buzón de usuario

## Usar el EAC para agregar una dirección de correo electrónico

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón de correo donde desee agregar una dirección de correo electrónico y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones de correo, haga clic en **Dirección de correo electrónico**.
    

    > [!NOTE]
    > En la página <STRONG>Dirección de correo electrónico</STRONG>, la dirección SMTP principal se muestra en texto en negrita en la lista de direcciones, con el valor en mayúscula <STRONG>SMTP</STRONG> en la columna <STRONG>Tipo</STRONG>.



4.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, a continuación, haga clic en **SMTP** para agregar una dirección de correo electrónico SMTP a este buzón de correo.
    

    > [!NOTE]
    > SMTP es el tipo de dirección de correo electrónico predeterminado. También puede añadir direcciones de mensajería unificada de Exchange (EUM) o direcciones personalizadas a un buzón de correo. Para obtener más información, consulte "Cambiar las propiedades del buzón de correo del usuario" en el tema <A href="manage-user-mailboxes-exchange-2013-help.md">Administrar los buzones de usuario</A>.



5.  Escriba la nueva dirección SMTP en el cuadro **Dirección de correo electrónico** y, a continuación, haga clic en **Aceptar**.
    
    La nueva dirección se muestra en la lista de direcciones de correo electrónico del buzón de correo seleccionado.

6.  Haga clic en **Guardar** para guardar el cambio.

## Usar el Shell para agregar una dirección de correo electrónico

Las direcciones de correo electrónico asociadas a un buzón de correo se encuentran en la propiedad *EmailAddresses* del buzón de correo. Como puede contener más de una dirección de correo electrónico, la propiedad *EmailAddresses* se conoce como una propiedad *multivalor*. Los siguientes ejemplos muestran diferentes maneras de modificar una propiedad multivalor.

Este ejemplo muestra cómo agregar una dirección SMTP al buzón de correo de Dan Jump.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}

Este ejemplo muestra cómo agregar varias direcciones SMTP a un buzón de correo.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}

Para obtener más información acerca de cómo usar este método de agregar o quitar valores de propiedades multivalor, consulte [Modificación de propiedades multivalor](modifying-multivalued-properties-exchange-2013-help.md).

Este ejemplo muestra otra forma de agregar direcciones de correo electrónico a un buzón de correo especificando todas las direcciones asociadas al buzón de correo. En este ejemplo, danj@tailspintoys.com es la dirección de correo electrónico nueva que desea agregar. Las otras dos direcciones de correo electrónico son direcciones existentes. La dirección con el calificador que distingue mayúsculas de minúsculas `SMTP` es la dirección SMTP principal. Debe incluir todas las direcciones de correo electrónico del buzón de correo cuando use esta sintaxis del comando. Si no lo hace, las direcciones especificadas en el comando sobrescribirán las direcciones existentes.

    Set-Mailbox "Dan Jump" -EmailAddresses SMTP:dan.jump@contoso.com,dan.jump@northamerica.contoso.com,danj@tailspintoys.com

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si agregó una dirección de correo electrónico correctamente en un buzón de correo, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Buzones de correo**, haga clic en el buzón de correo y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

  - En la página de propiedades de buzones de correo, haga clic en **Dirección de correo electrónico**.

  - En la lista de direcciones de correo electrónico del buzón de correo, verifique que se incluya la dirección de correo electrónico nueva.

O bien

  - Ejecute el siguiente comando en el Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Compruebe que la nueva dirección de correo electrónico esté incluida en los resultados.

## Quitar una dirección de correo electrónico de un buzón de usuario

## Usar el EAC para eliminar una dirección de correo electrónico

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón de correo donde desee quitar una dirección de correo electrónico y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones de correo, haga clic en **Dirección de correo electrónico**.

4.  En la lista de direcciones de correo electrónico, seleccione la lista de direcciones que desee quitar y, a continuación, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

5.  Haga clic en **Guardar** para guardar el cambio.

## Usar el Shell para quitar una dirección de correo electrónico

Este ejemplo muestra cómo quitar una dirección de correo electrónico del buzón de correo de Janet Schorr.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}

Este ejemplo muestra cómo quitar varias direcciones de un buzón de correo.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}

Para obtener más información acerca de cómo usar este método de agregar o quitar valores de propiedades multivalor, consulte [Modificación de propiedades multivalor](modifying-multivalued-properties-exchange-2013-help.md).

También puede quitar una dirección de correo electrónico omitiéndola del comando para establecer direcciones de correo electrónico de un buzón de correo. Por ejemplo, supongamos que el buzón de correo de Janet Schorr tiene tres direcciones de correo electrónico: janets@contoso.com (la dirección SMTP principal), janets@corp.contoso.com y janets@tailspintoys.com. Para quitar la dirección janets@corp.contoso.com, ejecutaría el siguiente comando.

    Set-Mailbox "Janet Schorr" -EmailAddresses SMTP:janets@contoso.com,janets@tailspintoys.com

Como janets@corp.contoso.com se omitió en el comando anterior, se quitó del buzón de correo.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si quitó una dirección de correo electrónico correctamente de un buzón de correo, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Buzones de correo**, haga clic en el buzón de correo y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

  - En la página de propiedades de buzones de correo, haga clic en **Dirección de correo electrónico**.

  - En la lista de direcciones de correo electrónico del buzón de correo, verifique que no se incluya la dirección de correo electrónico.

O bien

  - Ejecute el siguiente comando en el Shell.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - Verifique que la dirección de correo electrónico no esté incluida en los resultados.

## Usar el Shell para agregar direcciones de correo electrónico a varios buzones

Puede agregar una dirección de correo electrónico nueva a varios buzones a la vez usando el Shell y un archivo de valores separados por comas (CSV).

Este ejemplo importa datos de C:\\Users\\Administrator\\Desktop\\AddEmailAddress.csv, que tiene el siguiente formato.

    Mailbox,NewEmailAddress
    Dan Jump,danj@northamerica.contoso.com
    David Pelton,davidp@northamerica.contoso.com
    Kim Akers,kima@northamerica.contoso.com
    Janet Schorr,janets@northamerica.contoso.com
    Jeffrey Zeng,jeffreyz@northamerica.contoso.com
    Spencer Low,spencerl@northamerica.contoso.com
    Toni Poe,tonip@northamerica.contoso.com
    ...

Ejecute el siguiente comando para usar los datos en el archivo CSV para agregar una dirección de correo electrónico a cada buzón de correo especificado en el archivo CSV.

    Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}


> [!NOTE]
> Los nombres de columna de la primera fila de este archivo CSV (<CODE>Mailbox,NewEmailAddress</CODE>) son arbitrarios. Independientemente de cuales sean los nombres de columna que use, asegúrese de que usa los mismos nombres de columna en el comando de Shell.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si agregó una dirección de correo electrónico correctamente en varios buzones de correo, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Buzones de correo**, haga clic en el buzón de correo al cual agregó una dirección y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

  - En la página de propiedades de buzones de correo, haga clic en **Dirección de correo electrónico**.

  - En la lista de direcciones de correo electrónico del buzón de correo, verifique que se incluya la dirección de correo electrónico nueva.

O bien

  - Ejecute el comando en el Shell, usando el mismo archivo CSV que usó para agregar la dirección de correo electrónico nueva.
    
        Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Get-Mailbox $_.Mailbox | fl Name,EmailAddresses}

  - Compruebe que la nueva dirección de correo electrónico esté incluida en los resultados para cada buzón.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..


