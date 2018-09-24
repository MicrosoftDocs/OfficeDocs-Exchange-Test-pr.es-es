---
title: 'Migrar desde carpetas administradas: Exchange 2013 Help'
TOCTitle: Migrar desde carpetas administradas
ms:assetid: 6796a79d-501e-4216-9370-77965bc5835d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298032(v=EXCHG.150)
ms:contentKeyID: 52062032
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Migrar desde carpetas administradas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

En Microsoft Exchange Server 2013, la administración de registros de mensajes (MRM) se realiza mediante etiquetas de retención y directivas de retención. Una directiva de retención es un grupo de etiquetas de retención que se puede aplicar a un buzón. Para obtener más información, vea [Etiquetas de retención y directivas de retención](https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/retention-tags-and-policies). Las carpetas administradas, la tecnología MRM que se introdujo en Exchange Server 2007, no son compatibles.

Un buzón al que se le aplica una directiva de buzones de correo de carpetas administradas se puede migrar para que use una directiva de retención. Para ello, debe crear etiquetas de retención que sean equivalentes a las carpetas administradas vinculadas a la directiva de buzones de correo de carpetas administradas del usuario.


> [!IMPORTANT]
> Antes de migrar de carpetas administradas a directivas de retención en el entorno de producción, se recomienda que pruebe el proceso en un entorno de prueba.




> [!TIP]
> Puede colocar buzones de correo en suspensión de retención para detener el procesamiento de las directivas de retención o las directivas de buzón de la carpeta administrada. Colocar buzones de correo en suspensión de retención puede resultar útil en una migración para evitar eliminar mensajes o tener que archivarlos hasta que la nueva configuración de la directiva se haya probado en los buzones de correo de prueba o en un grupo reducido de buzones en producción. Para obtener información, vea <A href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">Poner un buzón en retención</A>.



Para información sobre otras tareas administrativas relacionadas con MRM, vea [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

## Comparación de etiquetas de retención con carpetas gestionadas

A diferencia de las carpetas administradas, que necesitan que los usuarios muevan los elementos a una carpeta administrada según la configuración de retención, las etiquetas de retención se pueden aplicar a una carpeta o a un elemento individual del buzón. Este proceso tiene un impacto mínimo en el flujo de trabajo del usuario y los métodos de organización del correo electrónico. Cuando se aplican etiquetas de retención a una carpeta, todos los elementos de esa carpeta heredan la configuración de retención. Los usuarios pueden especificar otra configuración de retención aplicando distintas etiquetas de retención a los elementos individuales de esa carpeta.

Las carpetas administradas son compatibles con distintas configuraciones de contenido administrado para una carpeta, cada una con una clase de mensaje distinto (como elementos de correo o elementos de calendario). Las etiquetas de retención no requieren un objeto de configuración de contenido administrado independiente porque la configuración de retención se especifica en las propiedades de la etiqueta. No se admite la creación de etiquetas de retención para clases de mensajes específicas, con la excepción de una etiqueta de directivas predeterminada (DPT) para mensajes de correo de voz. Las etiquetas de retención tampoco le permiten usar un registro en diario en el Asistente para carpeta administrada.


> [!NOTE]
> Las reglas de diario, que se usan para enviar copias de mensajes con un informe de diario a un buzón de registro, se aplican obligatoriamente en la ruta de transporte por parte del agente de registro en diario y son independientes de MRM. Para obtener más información, vea <A href="journaling-exchange-2013-help.md">Registro en diario</A>.



En la siguiente tabla, se compara la funcionalidad de MRM disponible con el uso de etiquetas de retención o carpetas administradas.

### Comparación de las etiquetas de retención con las carpetas administradas

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Funcionalidad</th>
<th>Etiquetas de retención</th>
<th>Carpetas administradas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Especificar la configuración de retención de las carpetas predeterminadas (como Bandeja de entrada)</p></td>
<td><p>Usar etiquetas de directivas de retención (RPT)</p></td>
<td><p>Usar carpetas administradas predeterminadas</p></td>
</tr>
<tr class="even">
<td><p>Especificar la configuración de retención de buzón completo</p></td>
<td><p>Usar una etiqueta de directiva predeterminada (DPT)</p></td>
<td><p>Uso de carpetas predeterminadas administradas</p></td>
</tr>
<tr class="odd">
<td><p>Usar la configuración de retención para carpetas personalizadas</p></td>
<td><p>Usar etiquetas personales</p></td>
<td><p>Usar carpetas administradas personalizadas</p></td>
</tr>
<tr class="even">
<td><p>Solicitar configuración de contenido administrado</p></td>
<td><p>No (la configuración de retención está incluida en una etiqueta de retención)</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Usar la configuración de retención para distintas clases de mensajes (como mensajes de correo electrónico, correo de voz o elementos de calendario)</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Admitir la acción Mover a archivo, la cual mueve elementos al buzón de archivo del usuario</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Admitir la acción Mover a carpeta administrada</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Permitir registro en diario mediante el Asistente de carpeta administrada</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Directiva aplicada al usuario</p></td>
<td><p>Directiva de retención</p></td>
<td><p>Directiva de buzones de correo de carpetas administradas</p></td>
</tr>
<tr class="even">
<td><p>Número máximo de directivas que se pueden aplicar a un usuario de buzón</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>Procesado por el Asistente de carpeta administrada</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Compatibilidad con clientes</p></td>
<td><p>Microsoft Outlook 2010 y OfficeOutlook Web App</p></td>
<td><p>Outlook 2010, Office Outlook 2007 y Outlook Web App</p></td>
</tr>
</tbody>
</table>


## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  20 minutos.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - No puede usar el Centro de administración de Exchange (EMC) para crear etiquetas de retención basadas en directivas de retención.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Migración de usuarios de buzones desde carpetas administradas

A continuación, se indican los pasos generales para la migración de usuarios desde esta directiva de buzones de correo de carpetas administradas hacia una directiva de retención. Cada paso se detalla más adelante en este tema:

1.  Reúna información acerca de las directivas de buzones de carpetas administradas aplicadas a todos los buzones de correo de Exchange 2010 y Exchange 2007, las carpetas administradas en cada directiva y las configuraciones de contenido administrado para cada carpeta administrada. Para obtener esta información, puede usar el EMC o el Shell en un servidor Exchange 2010 o Exchange 2007.

2.  Crear etiquetas de retención para la migración.

3.  Crear una directiva de retención y vincular a dicha directiva las etiquetas de retención recientemente creadas.

4.  Quite la directiva de buzones de correo de carpetas administradas y, a continuación, aplique la directiva de retención para usar buzones de correo.
    

    > [!IMPORTANT]
    > Después de aplicar la directiva de retención a un usuario y de ejecutar el Asistente de carpeta administrada, las carpetas administradas en el buzón del usuario dejarán de ser administradas.



Para los siguientes procedimientos, se aplica a los buzones Contoso una directiva de buzones de correo de carpetas administradas que contiene las siguientes carpetas administradas.

### Carpetas administradas de Contoso

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Carpeta administrada</th>
<th>Configuraciones de contenido administrado</th>
<th>Habilitado para retención</th>
<th>Antigüedad de retención</th>
<th>Acción de retención</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Corp-DeletedItems</p></td>
<td><p>CS-Corp-DeletedItems</p></td>
<td><p>Sí</p></td>
<td><p>30 días</p></td>
<td><p>Eliminar y permitir la recuperación</p></td>
</tr>
<tr class="even">
<td><p>Corp-SentItems</p></td>
<td><p>CS-Corp-SentItems</p></td>
<td><p>Sí</p></td>
<td><p>1825 días</p></td>
<td><p>Mover a Elementos eliminados</p></td>
</tr>
<tr class="odd">
<td><p>Corp-JunkMail</p></td>
<td><p>CS-Corp-JunkMail</p></td>
<td><p>Sí</p></td>
<td><p>30 días</p></td>
<td><p>Eliminar permanentemente</p></td>
</tr>
<tr class="even">
<td><p>Corp-EntireMailbox</p></td>
<td><p>CS-Corp-EntireMailbox</p></td>
<td><p>Sí</p></td>
<td><p>365 días</p></td>
<td><p>Mover a Elementos eliminados</p></td>
</tr>
<tr class="odd">
<td><p>30 días</p></td>
<td><p>CS-30Days</p></td>
<td><p>Sí</p></td>
<td><p>30 días</p></td>
<td><p>Mover a Elementos eliminados</p></td>
</tr>
<tr class="even">
<td><p>5 años</p></td>
<td><p>CS-5Years</p></td>
<td><p>Sí</p></td>
<td><p>1.825 días</p></td>
<td><p>Mover a Elementos eliminados</p></td>
</tr>
<tr class="odd">
<td><p>No caduca nunca</p></td>
<td><p>CS-NeverExpire</p></td>
<td><p>No</p></td>
<td><p>365 días</p></td>
<td><p>No disponible</p></td>
</tr>
</tbody>
</table>


## ¿Cómo realiza esto?

## Paso 1: Crear etiquetas de retención para la migración

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Administración de registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Hay dos métodos que puede usar para este paso:

  - **Crear etiquetas de retención basadas en las carpetas administradas y sus correspondientes ajustes de contenido administrado**   Con este método, puede usar el cmdlet **New-RetentionPolicyTag** con el parámetro *ManagedFolderToUpgrade*. Si especifica este parámetro, la etiqueta de retención correspondiente se aplicará automáticamente a la carpeta administrada.
    

    > [!IMPORTANT]
    > Si la carpeta administrada que se desea portar tiene distintas configuraciones de contenido administrado para distintas clases de mensaje, solamente se creará una etiqueta de retención y se usará la antigüedad de retención más alta de todas las configuraciones de contenido administrado como antigüedad de retención para la etiqueta portada, independientemente de la clase de mensaje en la configuración de contenido administrado.<BR>Por ejemplo, eche un vistazo a la siguiente configuración de contenido administrado de la carpeta administrada Corp-DeletedItems.



  - **Crear etiquetas de retención especificando manualmente los ajustes de retención**   Con este método, puede usar el cmdlet **New-RetentionPolicyTag** sin el parámetro *ManagedFolderToUpgrade*. Si no especifica este parámetro, cualquier etiqueta de directiva de retención que agregue a la directiva se aplicará a las carpetas predeterminadas y la etiqueta de directiva predeterminada se aplicará al buzón de correo completo. No obstante, las etiquetas personales que agregue a la directiva no se aplicarán automáticamente a las carpetas administradas.


> [!NOTE]
> En el caso de entornos mixtos con servidores Exchange&nbsp;2013 y Exchange 2010, puede usar el asistente <STRONG>Carpeta de puerto administrado</STRONG> en la Consola de administración de Exchange (EMC) en un servidor Exchange 2010 para portar fácilmente la carpeta administrada y la correspondiente configuración del contenido administrado a las etiquetas de retención.



**Crear etiquetas de retención según las carpetas administradas**

En este ejemplo, se crean etiquetas de retención según la configuración de contenido administrado correspondiente que se muestra en la directiva de buzones de correo de carpetas administradas de Contoso.

```powershell
New-RetentionPolicyTag Corp-DeletedItems -ManagedFolderToUpgrade Corp-DeletedItems
New-RetentionPolicyTag Corp-SentItems -ManagedFolderToUpgrade Corp-SentItems
New-RetentionPolicyTag Corp-JunkMail -ManagedFolderToUpgrade Corp-JunkMail
New-RetentionPolicyTag Corp-EntireMailbox -ManagedFolderToUpgrade Corp-EntireMailbox
New-RetentionPolicyTag 30Days -ManagedFolderToUpgrade 30Days
New-RetentionPolicyTag 5Years -ManagedFolderToUpgrade 5Years
New-RetentionPolicyTag NeverExpire -ManagedFolderToUpgrade NeverExpire
```

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [New-RetentionPolicyTag](https://technet.microsoft.com/es-es/library/dd335226\(v=exchg.150\)).

**Crear etiquetas de retención de forma manual**


> [!NOTE]
> También puede usar el EAC para crear etiquetas de retención manualmente (sin basarse en ajustes de las carpetas administradas). Para obtener información, vea <A href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">Crear directivas de retención</A>.



En este ejemplo, se crean etiquetas de retención según las carpetas administradas y la configuración de contenido administrado correspondiente que se muestra en la directiva de buzones de correo de carpetas administradas de Contoso. La configuración de retención se especifica manualmente sin usar el parámetro *ManagedFolderToUpgrade*.

```powershell
New-RetentionPolicyTag Corp-DeletedItems -Type DeletedItems -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction DeleteAndAllowRecovery
New-RetentionPolicyTag Corp-SentItems -Type SentItems -RetentionEnabled $true -AgeLimitforRetention 1825 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag Corp-JunkMail -Type JunkMail -RetentionEnabled $true -AgeLimitforRetention 30 -RetentionAction PermanentlyDelete
New-RetentionPolicyTag Corp-EntireMailbox -Type All -RetentionEnabled $true -AgeLimitForRetention 365 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag 30Days -Type Personal -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag 5Years -Type Personal -RetentionEnabled $true -AgeLimitForRetention 1825 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag NeverExpire -Type Personal -RetentionEnabled $false
```

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [New-RetentionPolicyTag](https://technet.microsoft.com/es-es/library/dd335226\(v=exchg.150\)).

## Paso 2: Crear una directiva de retención

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Administración de los registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> También puede usar el EAC para crear una directiva de retención y agregar etiquetas de retención a la directiva. Para obtener información, vea <A href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">Crear directivas de retención</A>.



En este ejemplo, se crea la directiva de retención RP-Corp y se vinculan a dicha directiva las etiquetas de retención recientemente creadas.

```powershell
New-RetentionPolicy RP-Corp -RetentionPolicyTagLinks Corp-DeletedItems,Corp-SentItems,Corp-JunkMail,Corp-EntireMailbox,30Days,NeverExpire
```

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [New-RetentionPolicy](https://technet.microsoft.com/es-es/library/dd297970\(v=exchg.150\)).

## Paso 3: Quitar la directiva de buzones de correo de carpetas administradas de los buzones de correo de usuarios

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Entrada "Aplicación de directivas de retención" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

En este ejemplo se quita la directiva de buzones de correo de carpetas administradas y cualquier carpeta administrada del buzón de correo de Ken Kwok. Las carpetas administradas que tienen mensajes no se eliminan.

```powershell
Set-Mailbox -Identity Kwok -RemoveManagedFolderAndPolicy RP-Corp
```

## Paso 4: Aplicar la directiva de retención a los buzones de usuario

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Entrada "Aplicación de directivas de retención" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> También puede usar el EAC para aplicar directivas de retención a los usuarios. Para obtener información, vea <A href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/messaging-records-management/apply-retention-policy">Aplicar una directiva de retención a los buzones</A>.



En este ejemplo, se aplica la directiva de retención RP-Corp recientemente creada al buzón del usuario Arturo López.

```powershell
Set-Mailbox -Identity Kwok -RetentionPolicy RP-Corp
```

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si esta tarea se ha completado correctamente?

Para verificar que ha realizado la migración de las carpetas administradas a las directivas de retención, siga los siguientes pasos:

  - Genere un informe de todos los buzones de correo de los usuarios y la directiva de retención que tienen aplicada.
    
    Este comando recupera la directiva de retención aplicada a todos los buzones de correo de una organización, así como su estado de suspensión de retención.
    
    ```powershell
    Get-Mailbox -ResultSize unlimited -Filter {Name -NotLike "DiscoverySearch*�?} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto
    ```

  - Una vez que el Asistente para carpeta administrada haya procesado un buzón de correo con una directiva de retención, use el cmdlet [Get-RetentionPolicyTag](https://technet.microsoft.com/es-es/library/dd298009\(v=exchg.150\)) para recuperar las etiquetas de retención suministradas en el buzón del usuario.
    
    Este comando recupera las etiquetas de retención aplicadas efectivamente al buzón de correo de April Stewart.
    
    ```powershell
    Get-RetentionPolicyTag -Mailbox astewart
    ```

