---
title: 'Ejecución de informe de acceso al buzón de correo del que no se es propietario'
TOCTitle: Ejecución de un informe de acceso al buzón de correo del que no se es propietario
ms:assetid: dbbef170-e726-4735-abf1-2857db9bb52d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150575(v=EXCHG.150)
ms:contentKeyID: 48268774
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ejecución de un informe de acceso al buzón de correo del que no se es propietario

 

_**Se aplica a:** Exchange Online_

_**Última modificación del tema:** 2016-12-09_

El informe de acceso al buzón de correo del que no se es propietario en el centro de administración de Exchange (EAC) enumera los buzones de correo a los que ha tenido acceso otro usuario que no es su propietario. Cuando un usuario tiene acceso a un buzón de correo del que no es propietario, Microsoft Exchange registra información acerca de esta acción en un registro de auditoría de buzones de correo que se almacena como un mensaje de correo electrónico en una carpeta oculta del buzón de correo que se está auditando. Las entradas de este registro se muestran como resultados de la búsqueda e incluyen una lista de buzones de correo a los que ha obtenido acceso el usuario que no es el propietario, quién obtuvo acceso al buzón y cuándo, las acciones realizadas por el usuario que no es propietario y si la acción se ha llevado a cabo correctamente. De manera predeterminada, las entradas del registro de auditoría de buzones de correo se retienen durante 90 días.

Al habilitar el registro de auditoría de buzones de correo para un buzón de correo, Microsoft Exchange registra las acciones específicas de los usuarios que no son propietarios, incluidos los administradores y los usuarios, denominados *usuarios delegados*, a los que se les ha asignado permisos para un buzón. También puede limitar la búsqueda a los usuarios de dentro o de fuera de la organización.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría de buzones" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Habilitación del registro de auditoría de buzones de correo

Tiene que habilitar el registro de auditoría de buzones de correo para el que desee ejecutar un informe de acceso al buzón de correo del que no se es propietario. Si el registro de auditoría de buzones de correo no está habilitado, no se obtendrán resultados al ejecutar el informe.

Para habilitar el registro de auditoría de buzones de correo para un solo buzón de correo, ejecute el siguiente comando de Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Por ejemplo, para habilitar la auditoría de buzones de correo de un usuario que se llama Florence Flipo, ejecute el siguiente comando.

    Set-Mailbox "Florence Flipo" -AuditEnabled $true

Para habilitar la auditoría de buzones de correo para todos los buzones de la organización, ejecute los siguientes comandos.
```
    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
```
```
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Ejecute el siguiente comando para comprobar que configuró correctamente el registro de auditoría de buzones de correo.

    Get-Mailbox | FL Name,AuditEnabled

El valor `True` para la propiedad *AuditEnabled* comprueba que el registro de auditoría está habilitado.

¿Qué necesita saber antes de comenzar?

## Ejecución de un informe de acceso al buzón de correo del que no se es propietario

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Auditoría**.

2.  Haga clic en **Ejecutar un informe de acceso al buzón de correo del que no se es propietario**.
    
    De manera predeterminada, Microsoft Exchange ejecutará el informe para el acceso de no propietarios a cualquier buzón de correo de la organización durante las dos últimas semanas. Los buzones de correo enumerados en los resultados de la búsqueda se han habilitado para el registro de la auditoría de buzones de correo.

3.  Para ver el acceso de usuarios no propietarios de un buzón específico, selecciónelo en la lista de buzones. Vea los resultados de la búsqueda en el panel de detalles.


> [!TIP]
> ¿Desear limitar los resultados de la búsqueda? Seleccione la fecha de inicio, la fecha de finalización o ambas, y seleccione los buzones de correo concretos en los que se buscará. Haga clic en <STRONG>Buscar</STRONG> para volver a ejecutar el informe.



## Búsqueda de tipos específicos de acceso de no propietarios

También puede especificar el tipo de acceso de no propietarios, denominado tipo de inicio de sesión, que se buscará. Estas son las opciones que tiene:

  - **Todos los no propietarios**   Se busca el acceso por parte de administradores y usuarios delegados de la organización. También incluye usuario de acceso externo a la organización.

  - **Usuarios externos**   Se busca acceso por usuarios externos a la organización.

  - **Administradores y usuarios delegados**   Se busca el acceso por parte de administradores y usuarios delegados de la organización.

  - **Administradores**   Se busca el acceso por parte de los administradores de la organización.

¿Qué necesita saber antes de comenzar?

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ejecutó correctamente un informe de acceso al buzón de correo del que no se es propietario, vea el panel de resultados. Los buzones de correo para los que ejecuta el informe se muestran en este panel. Si no hay resultados para un buzón de correo específico, es posible que no se hayan producido accesos por parte de no propietarios o que estos accesos no hayan ocurrido dentro del intervalo de fechas especificado. Como se describió anteriormente, asegúrese de comprobar que se haya habilitado el registro de auditoría para los buzones de correo en los que desea buscar el acceso por parte de no propietarios.

¿Qué necesita saber antes de comenzar?

## ¿Qué se almacena en el registro de auditoría de buzones de correo?

Al ejecutar un informe de acceso al buzón de correo del que no se es propietario, las entradas del registro de auditoría de buzones de correo se muestran en los resultados de la búsqueda en el EAC. Cada entrada del informe contiene esta información:

  - Quién tuvo acceso al buzón y cuándo

  - Las acciones realizadas por el usuario no propietario

  - El mensaje correspondiente y su ubicación de carpeta

  - Si la acción se realizó correctamente

En la tabla siguiente se enumeran las acciones realizadas por los usuarios no propietarios que se pueden registrar mediante el registro de auditoría del buzón de correo. En la tabla, **Sí** indica que la acción se puede registrar para ese tipo de inicio de sesión, y **No** indica que no se puede registrar la acción. Un asterisco (**\***) indica que la acción se registra de forma predeterminada cuando el registro de auditoría del buzón de correo está habilitado para el buzón. Si quiere realizar un seguimiento de las acciones que no se registran de forma predeterminada, use PowerShell para habilitar el registro de dichas acciones.


> [!NOTE]
> Un administrador al que se haya asignado el permiso Acceso total en el buzón de un usuario se considera un usuario delegado.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Acción</th>
<th>Descripción</th>
<th>Administrador</th>
<th>Usuario delegado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Copiar</strong></p></td>
<td><p>Un mensaje se copió en otra carpeta.</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><strong>Create</strong></p></td>
<td><p>Se crea un elemento en la carpeta Calendario, Contactos, Notas o Tareas en el buzón. Por ejemplo, se crea una nueva convocatoria de reunión. Tenga en cuenta que la creación de carpetas o mensajes no se audita.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderBind</strong></p></td>
<td><p>Se tuvo acceso a una carpeta de buzón de correo.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p><strong>Eliminar de forma permanente</strong></p></td>
<td><p>Un mensaje se purgó de la carpeta Elementos recuperables.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
</tr>
<tr class="odd">
<td><p><strong>MessageBind</strong></p></td>
<td><p>Un mensaje se consultó en el panel de vista previa o se abrió.</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><strong>Mover</strong></p></td>
<td><p>Un mensaje se movió a otra carpeta.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mover a Elementos eliminados</strong></p></td>
<td><p>Un mensaje se movió a la carpeta Elementos eliminados.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p><strong>Enviar como</strong></p></td>
<td><p>Un mensaje se envió mediante el permiso SendAs. Esto significa que otro usuario envió el mensaje como si procediera del propietario del buzón.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Enviar en nombre de</strong></p></td>
<td><p>Un mensaje se envió mediante el permiso SendOnBehalf. Esto significa que otro usuario envió el mensaje en nombre del propietario del buzón. El mensaje indicará al destinatario en nombre de quién se envió el mensaje y quién lo envió realmente.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p><strong>Eliminar temporalmente</strong></p></td>
<td><p>Un mensaje se eliminó de la carpeta Elementos eliminados.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Actualizar</strong></p></td>
<td><p>Se cambió un mensaje.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> *&nbsp; Se audita de forma predeterminada si la auditoría está habilitada para un buzón.



¿Qué necesita saber antes de comenzar?

