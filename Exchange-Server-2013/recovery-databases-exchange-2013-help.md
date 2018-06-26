---
title: 'Bases de datos de recuperación: Exchange 2013 Help'
TOCTitle: Bases de datos de recuperación
ms:assetid: f3c6fd0b-2e25-442e-a0fc-46f663130c3e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876954(v=EXCHG.150)
ms:contentKeyID: 48268860
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Bases de datos de recuperación

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-11-02_

Una base de datos de recuperación (RDB) es un tipo de base de datos de buzones especial que permite montar una base de datos de buzones restaurada y extraer los datos de la base de datos restaurada como parte del proceso de recuperación. Puede usar el cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)) para extraer los datos de una RDB. Tras la extracción, los datos pueden exportarse a una carpeta o combinarse en un buzón que ya exista. Las bases de datos de recuperación permiten recuperar datos de una copia de seguridad o de una copia de base de datos sin perjudicar el acceso del usuario a los datos actuales.

Microsoft Exchange Server 2013 admite la posibilidad de restaurar datos directamente a una base de datos de recuperación. Al montar los datos recuperados como una base de datos de recuperación, el administrador podrá recuperar los buzones o elementos individuales de un buzón. La restauración a una base de datos de recuperación se puede realizar de dos formas:

  - Si ya existe una base de datos de recuperación, la aplicación puede desmontarla, restaurar los datos en una base de datos de recuperación y registrar los archivos para, a continuación, volver a montar la base de datos.

  - La base de datos y los archivos de registro se pueden restaurar a cualquier ubicación de disco. Exchange analiza los datos restaurados y reproduce los registros de transacción para actualizar la bases de datos; después, puede configurarse una base de datos de recuperación para que apunte a los archivos de base de datos que ya se han recuperado.

## Diferencia entre una base de datos de buzones y una base de datos de recuperación

Las bases de datos de recuperación (RDB) se diferencian de las bases de datos de buzones estándar en varios aspectos:

  - Una RDB se crea mediante el Shell de administración de Exchange.

  - No se puede enviar correo de o a una RDB. Cualquier acceso de protocolo de cliente a una RDB (incluido SMTP, POP3 y IMAP4) se bloquea. Este diseño evita que una RDB pueda insertar o eliminar correo en un sistema de mensajería.

  - El acceso de cliente MAPI mediante Microsoft Office Outlook o Outlook Web App se bloquea. El acceso MAPI se admite para una base de datos de recuperación, pero solo en el caso de aplicaciones y herramientas de recuperación. Debe especificarse tanto el GUID del buzón como el de la base de datos cuando se una MAPI para iniciar sesión en un buzón de una RDB.

  - Los buzones de una RDB no se pueden conectar a cuentas de usuario. Para permitir que un usuario tenga acceso a los datos de un buzón de una RDB, el buzón debe combinarse con un buzón existente, o exportarse a una carpeta.

  - No se aplican las directivas de administración de buzones y del sistema. El diseño evita que los elementos de una RDB puedan ser eliminados por el sistema durante el proceso de recuperación.

  - No se lleva a cabo un mantenimiento en línea para bases de datos de recuperación.

  - No se puede habilitar el registro circular para bases de datos de recuperación.

  - Solo se puede montar una RDB en un servidor de buzones. El uso de una RDB no computa para el límite de base de datos por servidor de buzones.

  - No se pueden crear copias de base de datos de una RDB.

  - Se puede usar una RDB como destino para operaciones de restauración, pero no para operaciones de copia de seguridad.

  - Una base de datos de recuperación que se monta como una RDB no está ligada de ningún modo al buzón original.

## Uso de una base de datos de recuperación

Antes de poder usar una RDB, se deben cumplir algunos requisitos. Solo se puede usar una RDB para bases de datos de buzones de Exchange 2013. No se admiten las bases de datos de buzones de versiones previas de Exchange. Además, el buzón de destino que se usa para combinaciones y extracciones de datos debe estar en el mismo bosque de Active Directory que la base de datos montada en la RDB.

Se puede usar una RDB para recuperar datos en distintas situaciones, como las siguientes:

  - **Recuperación de tonos de marcado del mismo servidor**   Puede llevar a cabo una recuperación de una RDB una vez que la base de datos original se ha restaurado de una copia de seguridad, como parte de una operación de recuperación de tonos de marcado.

  - **Recuperación de tonos de marcado del servidor alternativo**   Puede usar un servidor alternativo para hospedar una base de datos de tonos de marcado y, a continuación, recuperar los datos de una RDB una vez que la base de datos original se ha restaurado de una copia de seguridad.

  - **Recuperación de buzón**   Puede recuperar un buzón individual de una copia de seguridad una vez transcurrido el periodo de tiempo de retención del buzón eliminado. A continuación, se extraen los datos del buzón restaurado y se copian a una carpeta de destino o se combinan con otro buzón.

  - **Recuperación de elementos concretos**   Puede restaurar datos de una copia de seguridad que se haya eliminado o purgado de un buzón.


> [!NOTE]
> Las listas de control de acceso a carpetas (ACL) no se conservarán al recuperar el contenido en un buzón activo. Como el proceso de recuperación suele conllevar la recuperación de datos y la combinación de contenido con la base de datos original, no será necesario recuperar o copiar listas de control de acceso.



Las RDB están diseñadas para la recuperación de bases de datos de buzones bajo las siguientes condiciones y situaciones:

  - La información lógica acerca de la base de datos original y de los buzones de esa base de datos permanece intacta y sin cambios en Active Directory.

  - Debe recuperar un solo buzón o una sola base de datos. Entre las situaciones de recuperación se incluyen:
    
      - Recuperación o reparación de una base de datos mientras se usa una base de datos de tonos de marcado, con el objetivo de combinar ambas bases de datos.
    
      - Recuperación de una base de datos en un servidor distinto al original de esa base de datos. Si lo necesita, puede combinar los datos recuperados en el servidor original.
    
      - Recuperación de elementos eliminados que los usuarios han eliminado previamente de su buzón, una vez que ha transcurrido el periodo de retención.

Las RDB, generalmente, no están diseñadas para escenarios en los que hay que restaurar servidores enteros, cuando hay que restaurar varias bases de datos o cuando se produce una situación de emergencia que exige el cambio o la restauración de la topología de Active Directory.

Para obtener los pasos detallados que se deben seguir para crear una RDB, consulte [Creación de una base de datos de recuperación](create-a-recovery-database-exchange-2013-help.md). Para obtener los pasos detallados acerca de cómo usar una RDB, consulte [Restauración de datos mediante una base de datos de recuperación](restore-data-using-a-recovery-database-exchange-2013-help.md).

