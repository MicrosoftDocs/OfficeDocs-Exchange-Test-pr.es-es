---
title: 'Realizar una recuperación del tono de marcado: Exchange 2013 Help'
TOCTitle: Realizar una recuperación del tono de marcado
ms:assetid: 158817fa-4b17-4fa9-8341-a86609e6a388
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd979810(v=EXCHG.150)
ms:contentKeyID: 51406478
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Realizar una recuperación del tono de marcado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-06-27_

Con el uso de la portabilidad del tono de marcado, los usuarios pueden tener un buzón temporal para enviar y recibir mensajes de correo mientras su buzón original se recupera o restaura. El buzón temporal puede estar en el mismo servidor de buzones de Exchange 2013 o en cualquier otro servidor de buzones de Exchange 2013 de su organización. El proceso para usar la portabilidad del tono de marcado se denomina recuperación del tono de marcado, que implica la creación de una base de datos vacía en el servidor de buzones para sustituir la base de datos en la que se produjeron errores. Para obtener más información, consulte [Portabilidad del tono de marcado](dial-tone-portability-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos más el tiempo necesario para restaurar los datos.

  - Para crear una base de datos de tonos de marcado, debe tener un número menor de bases de datos que el número máximo de bases de datos implementadas. Exchange 2013 Standard Edition admite un máximo de 5 bases de datos por servidor. Exchange 2013 Enterprise Edition admite un máximo de 50 bases de datos por servidor en RTM y CU1, y 100 bases de datos por servidor en CU2 y posteriores.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Recuperación de buzones" del tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para realizar una recuperación del tono de marcado en un servidor único


> [!NOTE]
> No puede usar el EAC para realizar una recuperación del tono de marcado en un servidor único.



1.  Asegúrese de que se conserven todos los archivos existentes en la base de datos en la que se realiza la recuperación en caso de ser necesarios para otras operaciones de recuperación posteriores.

2.  Use el cmdlet [New-MailboxDatabase](https://technet.microsoft.com/es-es/library/aa997976\(v=exchg.150\)) para crear una base de datos de tono de marcado, como se muestra en este ejemplo.
    
        New-MailboxDatabase -Name DTDB1 -EdbFilePath D:\DialTone\DTDB1.EDB

3.  Use el cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) para volver a asignar los buzones de usuario alojados en la base de datos en la que se realiza la recuperación, como se muestra en este ejemplo.
    
        Get-Mailbox -Database DB1 | Set-Mailbox -Database DTDB1

4.  Use el cmdlet [Mount-Database](https://technet.microsoft.com/es-es/library/aa998871\(v=exchg.150\)) para montar la base de datos para que los equipos cliente puedan tener acceso a la base de datos y enviar y recibir mensajes, como se muestra en este ejemplo.
    
        Mount-Database -Identity DTDB1

5.  Cree una base de datos de recuperación (RDB) y restaure o copie la base de datos y los archivos de registro que contienen los datos que desea recuperar en la RDB. Para obtener instrucciones detalladas, consulte [Creación de una base de datos de recuperación](create-a-recovery-database-exchange-2013-help.md).

6.  Después de copiar los datos en la RDB, pero antes de montar la base de datos recuperada, copie todos los archivos de registro de la base de datos en la que se produjo el error en la carpeta de registro de la base de datos de recuperación para que se puedan reproducir en la base de datos recuperada.

7.  Monte la RDB y, a continuación, use el cmdlet [Dismount-Database](https://technet.microsoft.com/es-es/library/bb124936\(v=exchg.150\)) para desmontarla, como se muestra en este ejemplo.
    
        Mount-Database -Identity RDB1
        Dismount-Database -Identity RDB1

8.  Después de desmontar la RDB, mueva la base de datos actual y los archivos de registro de la carpeta de la RDB a una ubicación segura. Esto se hace como preparación para intercambiar la base de datos recuperada con la base de datos de tono de marcado.

9.  Desmonte la base de datos de tono de marcado, como se muestra en este ejemplo. Tenga en cuenta que los usuarios finales experimentarán una interrupción del servicio cuando desmonte esta base de datos.
    
        Dismount-Database -Identity DTDB1

10. Mueva la base de datos y los archivos de registro a la carpeta de la base de datos de tono de marcado de la carpeta de la RDB.

11. Mueva la base de datos y los archivos de registro de la ubicación segura que contienen la base de datos recuperada a la carpeta de la base de datos de tono de marcado y, a continuación, móntela como se muestra en este ejemplo.
    
        Mount-Database -Identity DTDB1
    
    Esto finaliza la interrupción del servicio para los usuarios finales. Podrán obtener acceso a su base de datos de producción original y enviar y recibir mensajes.

12. Monte la RDB, como se muestra en este ejemplo.
    
        Mount-Database -Identity RDB1

13. Use los cmdlet [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) y [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)) para exportar los datos de la RDB e importarlos en la base de datos recuperada, como se muestra en este ejemplo. Esto importará todos los mensajes enviados y recibidos con la base de datos de tono de marcado a la base de datos de producción.
    
        $mailboxes = Get-Mailbox -Database DTDB1
    
        $mailboxes | %{ New-MailboxRestoreRequest -SourceStoreMailbox $_.ExchangeGuid -SourceDatabase RDB1 -TargetMailbox $_ }

14. Después de finalizar la operación de restauración, puede desmotar y quitar la RDB, como se muestra en este ejemplo.
    
        Dismount-Database -Identity RDB1
        Remove-MailboxDatabase -Identity RDB1

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [New-MailboxDatabase](https://technet.microsoft.com/es-es/library/aa997976\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\))

  - [Mount-Database](https://technet.microsoft.com/es-es/library/aa998871\(v=exchg.150\))

  - [Dismount-Database](https://technet.microsoft.com/es-es/library/bb124936\(v=exchg.150\))

  - [Remove-MailboxDatabase](https://technet.microsoft.com/es-es/library/aa997931\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha desplazado correctamente un buzón de correo, siga estos pasos:

  - Abra el buzón con Microsoft Office Outlook Web App.

  - Abra el buzón de correo con Microsoft Outlook.

