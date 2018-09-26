---
title: 'Distribución automática de buzones: Exchange 2013 Help'
TOCTitle: Distribución automática de buzones
ms:assetid: f4db4636-948c-466b-839c-300c1a3a9544
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff477621(v=EXCHG.150)
ms:contentKeyID: 59637143
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Distribución automática de buzones

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Última modificación del tema:** 2013-08-13_

Cuando se crea o se mueve un buzón, o se habilita un usuario existente para correo, el buzón se debe almacenar en una base de datos de buzones. En Microsoft Exchange Server 2013 puede dejar que Exchange elija la base de datos mediante la distribución automática de buzones.

Con la distribución automática de buzones, Exchange busca las bases de datos de buzones en la organización, excluye las que no son adecuadas de acuerdo con los criterios tratados más adelante en este tema, y luego elige una aleatoriamente en la que se ubicará el buzón. Mediante este proceso, los buzones se distribuyen aleatoriamente entre todas las bases de datos de buzones adecuadas de la organización.

La distribución automática se usa cuando no se especifica el parámetro *Database* en los cmdlets **New-Mailbox** y **Enable-Mailbox** o el parámetro *TargetDatabase* en el cmdlet **New-MoveRequest**.


> [!NOTE]
> La distribución automática se realiza únicamente cuando se crea un buzón en un servidor de Exchange&nbsp;2013, cuando se mueve a un servidor de&nbsp;Exchange&nbsp;2013 o cuando se habilita un usuario para correo. Los cmdlets <STRONG>New-Mailbox</STRONG>, <STRONG>New-MoveRequest</STRONG> y <STRONG>Enable-Mailbox</STRONG> deben ejecutarse desde un servidor con Exchange&nbsp;2013. Exchange no redistribuye buzones para distribuir la carga entre bases de datos automáticamente basándose en la carga del servidor.



El siguiente proceso se usa para encontrar una base de datos de buzones adecuada en la que se deberá ubicar un buzón nuevo o movido:

1.  Exchange recupera una lista de todas las bases de datos de buzones en la organización de Exchange 2013.

2.  Cualquier base de datos de buzones marcada para ser excluida del proceso de distribución se quita de la lista de bases de datos disponibles. Puede controlar qué bases de datos se excluyen. Para obtener más información, consulte Excluir bases de datos de la distribución automática más adelante en este tema.

3.  Cualquier base de datos de buzones fuera de los ámbitos de administración de base de datos aplicados al administrador que realiza la operación se quita de la lista de bases de datos disponibles. Para obtener más información, consulte Ámbitos de bases de datos más adelante en este tema.

4.  Cualquier base de datos de buzones fuera del sitio local de Active Directory en el que se está realizando la operación se quita de la lista de bases de datos disponibles.

5.  En la lista situada debajo de bases de datos de buzones, Exchange elige una base de datos de forma aleatoria. Si la base de datos está en línea y en buen estado, Exchange la usará. Si está sin conexión o en mal estado, se elige al azar otra base de datos. Si no se encuentran bases de datos en línea o en buen estado, la operación se interrumpirá con un error.

El proceso de selección de una base de datos de buzones lo realiza un agente de extensión del cmdlet Mailbox Resources Management Agent. El `Mailbox Resources Management Agent` es uno de los diversos agentes de extensión de cmdlet que amplían la funcionalidad de los cmdlets en ejecución. Para obtener más información acerca de los agentes de extensión del cmdlet, consulte [Agentes de extensión de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

Si no desea que los buzones se distribuyan automáticamente, puede deshabilitar el `Mailbox Resources Management Agent`. Cuando se deshabilita el agente, el cambio se aplica a toda la organización de Exchange. Para obtener más información acerca de cómo deshabilitar los agentes de extensión de cmdlet, vea [Administrar los agentes de extensión de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Excluir bases de datos de la distribución automática

De forma predeterminada, todas las bases de datos de buzones en línea y en buen estado en servidores de Exchange 2013 en el sitio local de Active Directory pueden ser elegidas por la distribución automática como almacén para un buzón nuevo o movido. Sin embargo, quizás desee excluir algunas bases de datos del proceso de distribución por diversos motivos. Por ejemplo, podría designar una base de datos de buzones como base de datos de registro en diario en la que únicamente pueda haber los buzones especificados manualmente. O puede que desee eliminar temporalmente una base de datos de la rotación para realizar un mantenimiento programado. Exchange 2013 le da la opción de excluir de forma permanente o temporal las bases de datos del proceso de exclusión usando el parámetro *IsExcludedFromProvisioning*, que se puede definir usando el cmdlet **Set-MailboxDatabase**.


> [!NOTE]
> Dos otros parámetros, <EM>IsSuspendedFromProvisioning</EM> y <EM>IsExcludedFromInitialProvisioning</EM>, también están disponibles en el cmdlet <STRONG>Set-MailboxDatabase</STRONG>. Estos parámetros se eliminarán en una versión futura de Exchange y su uso no es compatible.



El parámetro *IsExcludedFromProvisioning* tiene dos valores válidos, `$True` y `$False`. Al definir esta propiedad como `$True`, la base de datos de buzones se excluye del proceso de distribución automática. Al definirla como `$False`, la base de datos de buzones se incluyen en el proceso de distribución automática. El valor predeterminado es `$False`.

Para excluir una base de datos de buzones de la distribución automática, use el siguiente comando:

```powershell
Set-MailboxDatabase <database name> -IsExcludedFromProvisioning $True
```

Cuando se excluye una base de datos de buzones de la distribución automática, la única forma de crear un buzón o moverlo a ella es usar el parámetro *Database* en los cmdlets **New-Mailbox** y **Enable-Mailbox**, o el parámetro *TargetDatabase* en el cmdlet **New-MoveRequest**.

## Ámbitos de bases de datos

Los ámbitos de administración de bases de datos son un nivel adicional de control sobre el proceso de distribución automática de buzones que están disponibles en Exchange 2013. Si una base de datos de buzones está en línea y en buen estado, se encuentra en el sitio local de Active Directory y no ha sido excluida del proceso de distribución automática, Exchange 2013 comprueba si está incluida en el ámbito de bases de datos aplicado al administrador que ejecuta el cmdlet. Si lo está, estará incluida en la lista de bases de datos disponibles para dicho administrador.

Los ámbitos de bases de datos forman parte del modelo de permisos de control de acceso basado en roles (RBAC). Para obtener más información acerca de los ámbitos de bases de datos y el RBAC, vea los temas siguientes:

  - [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

Los ámbitos de bases de datos pueden resultar útiles si se tienen muchas bases de datos de buzones en el sitio local de Active Directory que están disponibles para la distribución automática pero se desea limitar las que pueden ser utilizadas por determinados conjuntos de administradores. Por ejemplo, sus servidores de Exchange 2013 podrían estar al servicio de diversas agencias, pero usted desea que cada agencia pueda crear o mover buzones únicamente a las bases de datos de buzones que tenga asignadas.

De forma predeterminada, todos los administradores de una organización de Exchange 2013 pueden ver todas las bases de datos de buzones en la organización. Para limitar las bases de datos que pueden ver y, por lo tanto, limitar las bases de datos en las que potencialmente pueden crear buzones o a las que pueden mover buzones, debe realizar las acciones siguientes:

1.  Crear un ámbito personalizado de administración de bases de datos mediante el cmdlet **New-ManagementScope** que incluya únicamente las bases de datos que desee que el administrador utilice.

2.  Asociar el nuevo ámbito de bases de datos con una asignación de rol de administración de una de las dos maneras siguientes:
    
      - Agregar el nuevo ámbito de bases de datos a una asignación existente de rol de administración mediante el parámetro *CustomConfigWriteScope* en el cmdlet **Set-ManagementRoleAssignment**. El ámbito de bases de datos se aplica ahora al grupo de roles de administración, al grupo de seguridad universal (USG) o al usuario que tiene asignada la asignación de rol.
    
      - Crear una asignación de rol de administración con el cmdlet **New-ManagementRoleAssignment** y usar el parámetro *CustomConfigWriteScope* para especificar el nuevo ámbito de bases de datos. Puede crear una asignación de roles entre un rol de administración y un grupo de roles, un USG o un usuario.

3.  Si ha creado una asignación de rol a un grupo de roles o un USG, agregue usuarios al grupo de roles o al USG para que la asignación de rol y el ámbito de bases de datos se apliquen a los usuarios.

4.  Si procede, quite el usuario (o los usuarios miembros de los grupos de roles o USG creados en los pasos anteriores) al que haya asignado la nueva asignación de rol de los demás grupos de roles o USG que puedan tener asignado un ámbito de bases de datos que contenga bases de datos a las que no deban tener acceso.

5.  Compruebe que los administradores tengan acceso únicamente a las bases de datos a las que deban tener acceso.

Una vez completados estos pasos, los administradores que tengan asignaciones de rol con los ámbitos de bases de datos que ha creado podrán crear o mover buzones únicamente a las bases de datos que haya especificado.

Para obtener más información acerca de cómo usar los ámbitos de bases de datos para limitar qué bases de datos de buzones están disponibles para los administradores, consulte [Controlar la distribución automática de buzones mediante los ámbitos de base de datos](control-automatic-mailbox-distribution-using-database-scopes-exchange-2013-help.md).

