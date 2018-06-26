---
title: 'Recuperar mensajes eliminados en el buzón de un usuario: Exchange 2013 Help'
TOCTitle: Recuperar mensajes eliminados en el buzón de un usuario
ms:assetid: 9e0e34ce-efc5-454e-8d15-57b4da867f12
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff660637(v=EXCHG.150)
ms:contentKeyID: 50556824
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recuperar mensajes eliminados en el buzón de un usuario

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

(Este tema está pensado para administradores de Exchange).

Los administradores pueden buscar y recuperar mensajes de correo electrónico eliminados en el buzón de un usuario. Esto incluye los elementos que una persona elimina permanentemente (purga) (mediante la característica Recuperar elementos eliminados en Outlook o Outlook Web App), o elementos eliminados por un proceso automatizado, por ejemplo, la directiva de retención asignada a los buzones de usuario. En estas situaciones, un usuario no puede recuperar los elementos purgados. Pero los administradores pueden recuperar mensajes purgados si no ha expirado el período de retención de elementos eliminados para el elemento.


> [!NOTE]
> Además de usar este procedimiento para buscar y recuperar elementos eliminados (que se mueven a la carpeta Elementos recuperables\Purgas si está habilitada la recuperación de único elemento o espera de litigio ) puede usar este procedimiento para buscar elementos que residan en las carpetas del buzón y eliminar los elementos del buzón de origen (también conocido como <EM>buscar y destruir</EM>).



## ¿Qué necesita hacer antes de comenzar?

  - Tiempo estimado para finalizar: 15-30 minutos.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - La recuperación de un único elemento debe estar habilitada para un buzón de correo antes de que el elemento que desee recuperar se elimine. En Exchange Online, la recuperación de un elemento único está habilitada de forma predeterminada, cuando se crea un nuevo buzón. En Exchange 2013, la recuperación de un elemento único se deshabilita cuando se crea un buzón. Para obtener más información, consulte [Habilitar o deshabilitar la recuperación de elementos individuales de un buzón de correo](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md).

  - Para buscar y recuperar los elementos, debe tener la siguiente información:
    
      - **Buzón de correo de origen**   Este es el buzón en el que se va a buscar.
    
      - **Buzón de correo de destino**   Este es el buzón de detección en el que se recuperarán los mensajes. El programa de instalación de Exchange crea un buzón de correo de detección predeterminado. En Exchange Online, también se crea un buzón de correo de detección de forma predeterminada. Si es necesario, puede crear buzones de correo de detección adicionales. Para obtener información más detallada, consulte [Crear un buzón de correo de detección](create-a-discovery-mailbox-exchange-2013-help.md).
        

        > [!NOTE]
        > Cuando use el cmdlet <STRONG>Search-Mailbox</STRONG>, puede especificar un buzón de correo de destino que no sea el buzón de correo de detección. No obstante, no puede especificar el mismo buzón de correo que el buzón de origen y de destino.

    
      - **Criterio de búsqueda**   El criterio incluye el remitente o destinatario o palabras claves (palabras o frases) del mensaje.

  - Este tema se centra en el uso de PowerShell para recuperar elementos eliminados en el buzón de un usuario. También puede usar la herramienta de eDiscovery local basada en GUI para buscar los elementos eliminados y exportarlos a un archivo PST. El usuario usará este archivo PST para restaurar los mensajes eliminados en su buzón. Para obtener instrucciones detalladas, vea [Recuperar elementos eliminados en el buzón de un usuario: ayuda para el administrador](https://go.microsoft.com/fwlink/p/?linkid=722928).

## Paso 1 (opcional): conectarse a Exchange Online mediante PowerShell remoto

Solo necesita realizar este paso si tiene una organización de Exchange Online o Office 365. Si tiene una organización de Exchange 2013, vaya al paso siguiente y ejecute el comando en el Shell de administración de Exchange.

1.  En el equipo local, abra Windows PowerShell y ejecute el siguiente comando.
    
        $UserCredential = Get-Credential
    
    En el cuadro de diálogo **Solicitud de credenciales de Windows PowerShell**, escriba el nombre de usuario y la contraseña de una cuenta de administrador global de Office 365 y, después, haga clic en **Aceptar**.

2.  Ejecute el comando siguiente.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  Ejecute el comando siguiente.
    
        Import-PSSession $Session

4.  Para comprobar que se ha conectado a su organización de Exchange Online, ejecute el comando siguiente para obtener una lista de todos los buzones de correo de su organización.
    
        Get-Mailbox

Para obtener más información o si tiene problemas para conectarse a su organización de Exchange Online, consulte [Conectarse a Exchange Online mediante PowerShell remoto](https://go.microsoft.com/fwlink/p/?linkid=517283).

## Paso 2: busque y recupere los elementos faltantes

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Exhibición de documentos electrónicos en contexto" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> Puede usar exhibición de documentos electrónicos en contexto en el Centro de administración de Exchange (EAC) para buscar los elementos que faltan. Sin embargo, al usar el EAC, no puede restringir la búsqueda en la carpeta Elementos recuperables. Se devolverán los mensajes que coincidan con los parámetros de búsqueda aunque no se hayan eliminado. Una vez recuperados en el buzón de correo de detección especificado, puede que tenga que revisar los resultados de la búsqueda y eliminar los mensajes innecesarios antes de recuperar los mensajes restantes en el buzón de correo del usuario o exportarlos en un archivo .pst.<BR>Para obtener información acerca de cómo usar el EAC para realizar una búsqueda de exhibición de documentos electrónicos en contexto, consulte <A href="create-an-in-place-ediscovery-search-exchange-2013-help.md">Crear una búsqueda de exhibición de documentos electrónicos local</A>.



El primer paso en el proceso de recuperación es buscar los mensajes en el buzón de correo de origen. Use uno de los siguientes métodos para buscar en el buzón de correo de un usuario y copiar los mensajes en el buzón de detección.

Este ejemplo busca los mensajes en el buzón de correo de April Stewart que cumple con los siguientes criterios:

  - Remitente: Ken Kwok

  - Palabra clave: Caracas

<!-- end list -->

    Search-Mailbox "April Stewart" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "Discovery Search Mailbox" -TargetFolder "April Stewart Recovery" -LogLevel Full


> [!NOTE]
> Cuando use el cmdlet <STRONG>Search-Mailbox</STRONG>, puede realizar un ámbito de búsqueda si usa el parámetro <EM>SearchQuery</EM> para especificar una consulta con formato mediante el lenguaje de consultas de las palabras clave (KQL). También puede usar el conmutador <EM>SearchDumpsterOnly</EM> para buscar elementos solo en la carpeta Elementos recuperables.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Search-Mailbox](https://technet.microsoft.com/es-es/library/dd298173\(v=exchg.150\)).

**¿Cómo saber si el proceso se ha completado correctamente?**

Para verificar que haya buscado correctamente los mensajes que desee recuperar, inicie sesión en el buzón de correo de detección seleccionado como buzón de correo de destino y revise los resultados de la búsqueda.

## Paso 3: restaure elementos recuperados

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Exhibición de documentos electrónicos en contexto" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> No puede usar el EAC para restaurar los elementos recuperados.



Después de recuperar los mensajes en un buzón de correo de detección, puede restaurarlos al buzón de correo del usuario mediante el cmdlet **Search-Mailbox**. Además, en Exchange 2013, puede usar los cmdlets **New-MailboxExportRequest** y **New-MailboxImportRequest** para exportar los mensajes a un archivo .pst o importarlos desde ese formato.

## Use el Shell para restaurar los mensajes

En este ejemplo, los mensajes se restauran al buzón de correo de April Stewart y se eliminan del buzón de búsqueda de detección.

    Search-Mailbox "Discovery Search Mailbox" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "April Stewart" -TargetFolder "Recovered Messages" -LogLevel Full -DeleteContent

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Search-Mailbox](https://technet.microsoft.com/es-es/library/dd298173\(v=exchg.150\)).

**¿Cómo saber si el proceso se ha completado correctamente?**

Para verificar que haya recuperado mensajes correctamente en el buzón de correo del usuario, tenga los mensajes de revisión en la carpeta de destino especificada en el comando anterior.

## (Exchange 2013) Use el Shell para exportar e importar los mensajes de un archivo .pst

En Exchange 2013, puede exportar contenido de un buzón de correo en un archivo .pst e importar el contenido de un archivo .pst a un buzón de correo. Para obtener más información acerca de de la importación y exportación del buzón de correo, consulte [Solicitudes de importación y exportación de buzones](mailbox-import-and-export-requests-exchange-2013-help.md). No se puede realizar esta tarea en Exchange Online.

En este ejemplo, se usa la siguiente configuración para exportar mensajes de la carpeta Recuperación de April Stewart en el buzón de búsqueda de recuperación a un archivo .pst:

  - **Buzón de correo**   Buzón de búsqueda de detección

  - **Carpeta de origen**   Recuperación de April Stewart

  - **ContentFilter**   Planes de viaje de April

  - **Ruta del archivo PST**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxExportRequest -Mailbox "Discovery Search Mailbox" -SourceRootFolder "April Stewart Recovery" -ContentFilter {Subject -eq "April travel plans"} -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MailboxExportRequest](https://technet.microsoft.com/es-es/library/ff607299\(v=exchg.150\)).

Este ejemplo usa la siguiente configuración para importar mensajes desde un archivo .pst a la carpeta Recuperado por el departamento de soporte técnico del buzón de correo de April Stewart:

  - **Buzón de correo**   April Stewart

  - **Carpeta de destino**   Recuperado por el departamento de soporte técnico

  - **Ruta del archivo PST**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxImportRequest -Mailbox "April Stewart" -TargetRootFolder "Recovered By Helpdesk" -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst 

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-MailboxImportRequest](https://technet.microsoft.com/es-es/library/ff607310\(v=exchg.150\)).

**¿Cómo saber si el proceso se ha completado correctamente?**

Para verificar que haya exportado correctamente los mensajes a un archivo .pst, use Outlook para abrir el archivo .pst e inspeccione sus contenidos. Para verificar que haya importado mensajes correctamente del archivo .pst, haga que el usuario inspeccione los contenidos de la carpeta de destino especificada en el comando anterior.

## Más información

  - La capacidad de recuperar elementos eliminados es habilitada por la *recuperación de elemento único*, que permite a un administrador recuperar un mensaje que un usuario o una directiva de retención ha purgado siempre y cuando no haya expirado el período de retención de elementos eliminados para ese elemento. Para más información sobre la recuperación de un elemento único, consulte [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

  - Un buzón de Exchange Online está configurado de forma predeterminada para retener elementos eliminados durante 14 días. El valor de esta configuración se puede ampliar a un máximo de 30 días. En Exchange 2013, se configura una base de datos de buzón para que retenga los elementos eliminados por 14 días de manera predeterminada. Puede configurar la configuración de retención de elementos eliminados para un buzón o una base de datos de buzón. Para obtener más información, visite:
    
      - [Cambiar el tiempo que se conservan los elementos eliminados permanentemente para un buzón de correo de Exchange Online](https://technet.microsoft.com/es-es/library/dn163584\(v=exchg.150\))
    
      - [Configurar la retención de elementos eliminados y las cuotas de elementos recuperables](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)

  - Como ya se ha explicado anteriormente, también puede usar la herramienta de eDiscovery local para buscar los elementos eliminados y exportarlos a un archivo PST. El usuario usará este archivo PST para restaurar los mensajes eliminados en su buzón. Para obtener instrucciones detalladas, vea [Recuperar elementos eliminados en el buzón de un usuario: ayuda para el administrador](https://go.microsoft.com/fwlink/p/?linkid=722928).

  - Los usuarios pueden recuperar un elemento eliminado si todavía no se ha purgado y si no ha expirado el período de retención de elementos eliminados para ese elemento. Si los usuarios necesitan recuperar elementos eliminados de la carpeta Elementos recuperables, remítalos a los siguientes temas:
    
      - [Recuperar elementos eliminados en Outlook 2010](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Recuperar elementos eliminados en Outlook para Windows](https://go.microsoft.com/fwlink/p/?linkid=624829)
    
      - [Recuperar elementos eliminados o correo electrónico en Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

  - Este tema le muestra cómo usar el cmdlet **Search-Mailbox** para buscar y recuperar elementos que faltan. Si usa este cmdlet, solo puede buscar en un buzón por vez. Si desea buscar en varios buzones al mismo tiempo, puede usar [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md) en el Centro de administración de Exchange (EAC) o el cmdlet [New-MailboxSearch](https://technet.microsoft.com/es-es/library/dd298064\(v=exchg.150\)) en Windows PowerShell.

  - Además de usar este procedimiento para buscar y recuperar elementos eliminados, también puede usar un procedimiento similar para buscar elementos en buzones de usuario y, a continuación, eliminar los elementos del buzón de origen. Para obtener más información, consulte [Buscar y eliminar mensajes: Ayuda para administradores](search-for-and-delete-messages-admin-help-exchange-2013-help.md).

