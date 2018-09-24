---
title: 'Restaurar datos mediante una base de datos de recuperación: Exchange 2013 Help'
TOCTitle: Restauración de datos mediante una base de datos de recuperación
ms:assetid: d64c18e7-16af-4bd8-a5c5-01206984d4d1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee332351(v=EXCHG.150)
ms:contentKeyID: 48268739
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Restauración de datos mediante una base de datos de recuperación

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-10-01_

Una base de datos de recuperación (RDB) es un tipo de base de datos de buzones especial que permite montar una base de datos de buzones restaurada y extraer los datos ella como parte del proceso de recuperación. Las bases de datos de recuperación permiten recuperar datos de una copia de seguridad o copia de una base de datos sin perjudicar el acceso del usuario a los datos actuales.

Después de crear una RDB, puede restaurar una base de datos de buzones en la RDB mediante una aplicación de copia de seguridad o copiando una base de datos y sus archivos de registro en la estructura de carpetas de la RDB. A continuación, puede usar el cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)) para extraer los datos de la base de datos recuperada. Una vez hecha la extracción, los datos pueden exportarse a una carpeta o combinarse en los de un buzón existente.

Para otras tareas de administración relacionadas con las bases de datos de recuperación, consulte [Bases de datos de recuperación](recovery-databases-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: Un minuto, además del tiempo que lleve poner la base de datos en un estado de cierre correcto para extraer los datos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Recuperación de buzones" del tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Algunas aplicaciones de copia de seguridad tienen la capacidad de restaurar los datos de Exchange directamente a una base de datos de recuperación. Copia de seguridad de Windows Server puede restaurar solo copias de seguridad en el nivel de archivo a una base de datos de recuperación. No se puede usar para restaurar copias de seguridad en el nivel de aplicación a una base de datos de recuperación.

  - Los archivos de base de datos y de registro que contienen los datos recuperados deben restaurarse o copiarse en la estructura de carpetas de la RDB.

  - La base de datos debe estar en un estado de cierre correcto. Si tenemos en cuenta que una RDB es una ubicación alternativa para todas las bases de datos, todas las bases de datos recuperadas estarán en un estado de cierre con errores. Debe usar **Eseutil /R** para poner las bases de datos restauradas en un estado de cierre correcto.

## Usar el Shell para recuperar datos con una base de datos de recuperación

1.  Copie una base de datos recuperada y sus archivos de registro o restaure una base de datos y archivos de registro, a la ubicación que usará para la base de datos de recuperación.

2.  Use Eseutil para poner la base de datos en un estado de cierre correcto. En el ejemplo siguiente, EXX es el prefijo de generación de registros para la base de datos (por ejemplo, E00, E01, E02, etc.).
    
    ```powershell
    Eseutil /R EXX /l <RDBLogFilePath> /d <RDBEdbFolder>
    ```
    
    En el ejemplo siguiente se ilustra el prefijo de generación de registro E01 y la ruta de archivo de base de datos de recuperación y de registro E:\\Databases\\RDB1:
    
    ```powershell
    Eseutil /R E01 /l E:\Databases\RDB1 /d E:\Databases\RDB1
    ```

3.  Crear una base de datos de recuperación Asigne a la base de datos de recuperación un nombre único, pero use el nombre y la ruta de acceso del archivo de base de datos para el parámetro EdbFilePath y la ubicación de los archivos de recuperación recuperados para el parámetro LogFolderPath.
    ```powershell
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath <RDBPathandFileName> -LogFolderPath <LogFilePath>
    ```
    
    En el siguiente ejemplo se muestra cómo crear una base de datos de recuperación que se usará para recuperar DB1.edb y sus archivos de registro, ubicados en E:\\Databases\\RDB1.
    ```powershell
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath "E:\Databases\RDB1\DB1.EDB" -LogFolderPath "E:\Databases\RDB1"
    ```

4.  Reinicie el servicio Almacén de información de Microsoft Exchange:
    
    ```powershell
    Restart-Service MSExchangeIS
    ```

5.  Monte la base de datos de recuperación:
    
    ```powershell
    Mount-database <RDBName>
    ```

6.  Compruebe que la base de datos montada contiene los buzones que quiere restaurar:
    
    ```powershell
    Get-MailboxStatistics -Database <RDBName> | ft -auto
    ```

7.  Use el cmdlet New-MailboxRestoreRequest para restaurar un buzón o los elementos de la base de datos de recuperación a un buzón de producción.
    
    En el siguiente ejemplo se restaura el buzón de origen con el valor de MailboxGUID 1d20855f-fd54-4681-98e6-e249f7326ddd en la base de datos de buzones DB1 en el buzón de destino con el alias Morris.
    ```powershell
        New-MailboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox 1d20855f-fd54-4681-98e6-e249f7326ddd -TargetMailbox Morris
    ```    
    En el siguiente ejemplo se restaura el contenido del buzón de origen con el nombre para mostrar Morris Cornejo de la base de datos de buzones DB1 en el buzón de archivo de Morris@contoso.com.
    
        New-MaiboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox "Morris Cornejo" -TargetMailbox Morris@contoso.com -TargetIsArchive

8.  Compruebe periódicamente el estado de la solicitud de restauración de buzones mediante [Get-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829907\(v=exchg.150\)).
    
    Cuando la restauración tenga el estado Completado, quite la solicitud de restauración con [Remove-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829910\(v=exchg.150\)). Por ejemplo:
    
    ```powershell
    Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest
    ```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que los datos del buzón de correo se recuperaron correctamente, abra el buzón de correo de destino con Outlook o Outlook Web App y compruebe que los datos recuperados están allí.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


