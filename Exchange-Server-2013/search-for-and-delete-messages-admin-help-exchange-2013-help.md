---
title: 'Buscar y eliminar mensajes: Ayuda para administradores: Exchange 2013 Help'
TOCTitle: 'Buscar y eliminar mensajes: Ayuda para administradores'
ms:assetid: 8c36bb03-e716-4fdd-9958-4aa7a2a1db42
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff459253(v=EXCHG.150)
ms:contentKeyID: 52061895
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Buscar y eliminar mensajes: Ayuda para administradores

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-12-20_

Los administradores pueden usar el cmdlet **Search-Mailbox** para buscar en buzones de usuario y, después, eliminar mensajes de un buzón.

Para buscar y eliminar los mensajes en un solo paso, ejecute el cmdlet **Search-Mailbox** con el modificador *DeleteContent*. Sin embargo, cuando hace esto, no puede previsualizar los resultados de la búsqueda ni generar un registro de mensajes que será devuelto por la búsqueda y puede eliminar mensajes accidentalmente que pretendía conservar. Para previsualizar un registro de mensajes encontrados en la búsqueda antes de que se eliminen, ejecute el cmdlet **Search-Mailbox** con el modificador *LogOnly*.

Como una protección adicional, primero puede copiar los mensajes en otro buzón con los parámetros *TargetMailbox* y *TargetFolder*. Al hacer esto, guarda una copia de los mensajes eliminados en caso de que necesite obtener acceso a ellos nuevamente.

## ¿Qué necesito saber antes de comenzar?

  - Tiempo estimado para finalizar:  10 minutos. El tiempo real puede variar en función del tamaño del buzón y la consulta de búsqueda.

  - No puede usar el Centro de administración de Exchange (EAC) para realizar estos procedimientos. Debe usar el Shell.

  - Tiene que tener asignados los siguientes roles de administración para buscar y eliminar los mensajes en los buzones de correo de los usuarios:
    
      - **Búsqueda en el buzón**   Este rol le permite buscar mensajes en varios buzones de correo de una organización. Los administradores no tienen asignado este rol de forma predeterminada. Para asignarse a sí mismo este rol para poder buscar en buzones, agréguese como miembro del grupo de rol de administración de la detección. Vea [Asignar permisos de exhibición de documentos electrónicos en Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).
    
      - **Importación o exportación de buzones:** este rol le permite eliminar los mensajes del buzón de correo de un usuario. De forma predeterminada, este rol no está asignado a ningún grupo de roles. Para eliminar mensajes de los buzones de los usuarios, puede agregar el rol de importación o exportación de buzones al grupo de roles de administración de la organización. Para obtener más información, consulte la sección \&quot;Agregar una función a un grupo de funciones\&quot; en [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - Si el buzón desde el cual desea eliminar los mensajes tiene la recuperación de un solo elemento habilitada, primero debe deshabilitar la función. Para obtener más información, consulte [Habilitar o deshabilitar la recuperación de elementos individuales de un buzón de correo](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md).

  - Si el buzón del que desea eliminar los mensajes está en espera, le recomendamos que se ponga en contacto con su departamento jurídico o de administración de registros antes de eliminar la espera y eliminar el contenido del buzón. Después de obtener la aprobación, siga los pasos mencionados en el tema [Limpiar la carpeta Elementos recuperables](clean-up-the-recoverable-items-folder-exchange-2013-help.md).

  - Puede buscar en un máximo de 10 000 buzones con el cmdlet **Search-Mailbox**. Si es Exchange Online de una organización y tiene más de 10 000 buzones, puede usar la característica Búsqueda de cumplimiento (o el cmdlet **New-ComplianceSearch** correspondiente) para buscar en un número ilimitado de buzones. Después, puede usar el cmdlet **New-ComplianceSearchAction** para eliminar los mensajes encontrados por una búsqueda de cumplimiento. Para obtener más información, vea [Buscar y eliminar mensajes de correo electrónico de la organización de Office 365](https://go.microsoft.com/fwlink/p/?linkid=786856).

  - Si incluye una consulta de búsqueda (utilizando el parámetro *SearchQuery*), el cmdlet **Search-Mailbox** devolverá un máximo de 10 000 elementos en los resultados de búsqueda. Por tanto, si incluye una consulta de búsqueda, es posible que deba ejecutar el comando **Search-Mailbox** varias veces para eliminar más de 10 000 elementos.

  - También se buscará el buzón del usuario archivo al ejecutar el cmdlet **Search-Mailbox** . Del mismo modo, se eliminarán elementos del buzón del archivo principal cuando se utiliza el cmdlet **Search-Mailbox** con el modificador *DeleteContent* . Para evitar esto, puede incluir el modificador *DoNotIncludeArchive* . Además, se recomienda que no utilice el modificador *DeleteContent* para eliminar los mensajes en los buzones de Exchange Online que tienen habilitado porque pueden producirse pérdidas de datos inesperadas el archivado ampliación automática.

## Buscar mensajes y registrar los resultados de la búsqueda

En este ejemplo, se buscan mensajes que contengan la frase "Su extracto bancario" en el campo Asunto en el buzón de correo de April Stewart y se registra el resultado en la carpeta SearchAndDeleteLog en el buzón de correo del administrador. Los mensajes no se copian ni eliminar en el buzón de correo de destino.

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

Este ejemplo busca en todos los buzones de la organización los mensajes que tienen cualquier tipo de archivo adjunto que contiene la palabra \&quot;Troyano\&quot; en el nombre de archivo y envía un mensaje de registro al buzón del administrador.

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery attachment:trojan* -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Search-Mailbox](https://technet.microsoft.com/es-es/library/dd298173\(v=exchg.150\)).

Volver al principio

## Buscar y eliminar mensajes

En este ejemplo, se buscan mensajes que contengan la frase "Su extracto bancario" en el asunto en el buzón de correo de Yolanda Sánchez y se eliminan los mensajes del buzón de correo de origen. Como se explicó anteriormente, tiene que tener asignado el rol de administración Importar o exportar buzones para eliminar los mensajes del buzón de un usuario.


> [!IMPORTANT]
> Cuando usa el cmdlet <STRONG>Search-Mailbox</STRONG> con el modificador <EM>DeleteContent</EM>, los mensajes se eliminan permanentemente del buzón origen. Antes de eliminar permanentemente los mensajes, le recomendamos que use el modificador <EM>LogOnly</EM> para generar un registro de los mensajes encontrados en la búsqueda antes de que se eliminen o que copie los mensajes en otro buzón antes de eliminarlo desde el buzón origen.



    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -DeleteContent

En este ejemplo, se buscan mensajes que contengan la frase "Su extracto bancario" en el campo Asunto en el buzón de correo de April Stewart, se copian los resultados de la búsqueda en la carpeta AprilStewart-DeletedMessages en el buzón BackupMailbox y se eliminan los mensajes del buzón de April.

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox "BackupMailbox" -TargetFolder "AprilStewart-DeletedMessages" -LogLevel Full -DeleteContent

Este ejemplo busca en todos los buzones de la organización los mensajes con el asunto \&quot;Descargar este archivo\&quot; y, a continuación, los elimina de forma definitiva.

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery 'Subject:"Download this file"' -DeleteContent

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Search-Mailbox](https://technet.microsoft.com/es-es/library/dd298173\(v=exchg.150\)).

Volver al principio

## Usar el parámetro -LogLevel Full

En algunos de los ejemplos anteriores, el parámetro *LogLevel* (con el valor `Full`) se usa para registrar información detallada sobre los resultados encontrados por el cmdlet **Search-Mailbox**. Al incluir este parámetro, se crea un mensaje de correo electrónico y se envía al buzón especificado por el parámetro *TargetMailbox*. El archivo de registro (que es un archivo con formato CSV llamado Search Results.csv) se adjunta a este mensaje de correo electrónico y se guarda en la carpeta especificada por el parámetro *TargetFolder*. El archivo de registro contiene una fila por cada mensaje incluido en los resultados de la búsqueda al ejecutar el cmdlet **Search-Mailbox**.

