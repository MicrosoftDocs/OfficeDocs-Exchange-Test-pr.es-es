---
title: 'Creación de una base de datos de recuperación: Exchange 2013 Help'
TOCTitle: Creación de una base de datos de recuperación
ms:assetid: 34d87491-b7b7-44a9-8d69-e1a9c1fe5852
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee332321(v=EXCHG.150)
ms:contentKeyID: 48267982
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creación de una base de datos de recuperación

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-01-21_

Puede usar el Shell para crear una base de datos de recuperación, un tipo especial de base de datos de buzones de correo que se usa para instalar y extraer datos de la base de datos restaurada como parte de la operación de recuperación. Después de crear una base de datos de recuperación, es posible trasladar a ella una base de datos de buzones de correo recuperada o restaurada y luego utilizar el cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)) para extraer los datos de la base recuperada. Una vez hecha la extracción, los datos pueden exportarse a una carpeta o combinarse en los de un buzón existente. Con las bases de datos de recuperación, también puede recuperar datos de una copia de seguridad o copia de una base de datos sin interrumpir el acceso del usuario a los datos actuales.

¿Está buscando otras tareas de administración relacionadas con las bases de datos de recuperación? Consulte [Bases de datos de recuperación](recovery-databases-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Recuperación de buzones" del tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para crear una base de datos de recuperación

En este ejemplo, se crea la base de datos de recuperación RDB1 en el servidor de buzones MBX2.

    New-MailboxDatabase -Recovery -Name RDB1 -Server MBX2

En este ejemplo, se crea la base de datos de recuperación RDB2 en el servidor de buzones MBX1 mediante una ruta de acceso personalizada para el archivo de base de datos y la carpeta de registro.

    New-MailboxDatabase -Recovery -Name RDB2 -Server MBX1 -EdbFilePath "C:\Recovery\RDB2\RDB2.EDB" -LogFolderPath "C:\Recovery\RDB2"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MailboxDatabase](https://technet.microsoft.com/es-es/library/aa997976\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la base de datos de recuperación se haya creado correctamente, siga estos pasos:

  - En el Shell, ejecute el siguiente comando para mostrar la información de configuración de una base de datos de recuperación.
    
        Get-MailboxDatabase <RecoveryDatabaseName> | Format-List

## Otras tareas

Después de crear una base de datos de recuperación, es posible que también desee restaurar datos mediante una base de datos de recuperación. Para obtener instrucciones detalladas, consulte [Restauración de datos mediante una base de datos de recuperación](restore-data-using-a-recovery-database-exchange-2013-help.md).

