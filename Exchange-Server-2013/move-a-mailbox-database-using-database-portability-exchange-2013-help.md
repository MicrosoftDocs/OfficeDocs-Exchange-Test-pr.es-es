---
title: 'Mover una base de datos de buzones mediante la portabilidad de bases de datos: Exchange 2013 Help'
TOCTitle: Mover una base de datos de buzones mediante la portabilidad de bases de datos
ms:assetid: a765ead1-43bc-4786-ae93-1835cacfc8fc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876926(v=EXCHG.150)
ms:contentKeyID: 51406530
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mover una base de datos de buzones mediante la portabilidad de bases de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-06-16_

También puede usar la portabilidad de base de datos para mover una base de datos de buzones de correo de Microsoft Exchange Server 2013 entre servidores de buzones de Exchange 2013 de la misma organización. Esto puede ayudar a reducir los tiempos de recuperación generales para diversos escenarios de error. Para obtener más información, consulte [Portabilidad de bases de datos](database-portability-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos, más el tiempo que se tarda en restaurar todos los datos, mover los archivos de la base de datos y esperar a que se complete la replicación de Active Directory.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Recuperación de buzones" del tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - No puede usar el EAC para mover buzones de correo de usuario a una base de datos recuperada o de tono de marcado mediante la portabilidad de base de datos.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para mover buzones de usuarios a una base de datos recuperada o de tono de marcado mediante la portabilidad de base de datos

1.  Compruebe que la base de datos esté en estado de cierre correcto. Si la base de datos no está en estado de cierre correcto, realice una recuperación parcial.
    

    > [!NOTE]
    > Cuando se realiza una recuperación parcial, todos los archivos de registro no confirmados se confirman en la base de datos. Si no dispone de todos los archivos de registro requeridos, no podrá completar el proceso de recuperación parcial. Continúe con el paso&nbsp;2.

    
    Para confirmar todos los archivos de registro no confirmados en la base de datos, desde el símbolo del sistema ejecute el siguiente comando.
    
        ESEUTIL /R <Enn>
    

    > [!NOTE]
    > &lt;E<EM>nn</EM>&gt; especifica el prefijo de archivo de registro para la base de datos en la que desea reproducir los archivos de registro. El prefijo de archivo de registro especificado por &lt;E<EM>nn</EM>&gt; es un parámetro necesario de Eseutil /r.



2.  Crear una base de datos en un servidor con la siguiente sintaxis:
    
        New-MailboxDatabase -Name <DatabaseName> -Server <ServerName> -EdbFilePath <DatabaseFileNameandPath> -LogFolderPath <LogFilesPath>

3.  Establezca el atributo *This database can be over written by restore* mediante el uso de la siguiente sintaxis:
    
        Set-MailboxDatabase <DatabaseName> -AllowFileRestore $true

4.  Mueva los archivos originales de base de datos (archivo .edb, archivos de registro y el catálogo de Exchange Search) a la carpeta de base de datos especificada al crear la nueva base de datos indicada anteriormente.

5.  Monte la base de datos mediante la siguiente sintaxis:
    
        Mount-Database <DatabaseName>

6.  Después de montar la base de datos, modifique la configuración de la cuenta del usuario mediante el cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) para que la cuenta apunte al buzón que se encuentra en el nuevo servidor de buzones. Para mover todos los usuarios de la base de datos antigua y trasladarlos a la nueva, use la siguiente sintaxis.
    
        Get-Mailbox -Database <SourceDatabase> |where {$_.ObjectClass -NotMatch '(SystemAttendantMailbox|ExOleDbSystemMailbox)'}| Set-Mailbox -Database <TargetDatabase>

7.  Desencadene la entrega de los mensajes que puedan quedar en las colas con la siguiente sintaxis.
    
        Get-Queue <QueueName> | Retry-Queue -Resubmit $true

Una vez que se completó la replicación de Active Directory, todos los usuarios pueden obtener acceso a sus buzones en el nuevo servidor de Exchange. La mayoría de los clientes son redireccionados mediante la detección automática. Los usuarios de Outlook Web App de Microsoft Office también se redireccionan automáticamente.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha movido correctamente un buzón de correo, siga estos pasos:

  - Abra el buzón de correo usando Outlook Web App.

  - Abra el buzón de correo usando Microsoft Outlook.

