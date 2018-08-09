---
title: 'Configurar grupo disponibilidad de base de datos AutoReseed Exchange 2013 Help'
TOCTitle: Configurar un grupo de disponibilidad de la base de datos AutoReseed
ms:assetid: 4a8bd779-b52a-40ed-8040-4d76eabeb41e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ619303(v=EXCHG.150)
ms:contentKeyID: 49116195
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar un grupo de disponibilidad de la base de datos AutoReseed

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-04-15_

La Reinicialización automática es una función para restaurar rápidamente la redundancia después de un error de disco. Si un disco presenta un error, las copias de la base de datos almacenadas en ese disco se reinicializan automáticamente en un disco de repuesto preconfigurado en un servidor de buzones. Siga los pasos descritos en este tema para configurar la Reinicialización automática para un grupo de disponibilidad de base de datos (DAG).


> [!WARNING]
> La característica Reinicialización automática no realiza las tareas de configuración de requisitos previos por usted. La instalación correcta de los discos, la adición de discos de repuestos al sistema, el reemplazo de discos con errores y el formateo de discos nuevos debe realizarlo un administrador de manera manual.



Para consultar otras tareas de administración relacionadas con los grupos de disponibilidad de base de datos (DAG), vea [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de disponibilidad de base de datos" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Debe crearse una partición o un disco lógico único por disco físico.

  - Se debe usar la estructura de carpetas de registro y bases de datos específica que se describe en los siguiente pasos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Cómo realiza esto?

## Paso 1: configurar las rutas de acceso raíz para bases de datos y volúmenes

En el primer paso se configuran los directorios raíz para las bases de datos (*AutoDagDatabasesRootFolderPath*) y los volúmenes (*AutoDagVolumesRootFolderPath*) que utiliza el DAG. Los valores predeterminados son C:\\ExchangeDatabases y C:\\ExchangeVolumes, respectivamente. Omita este paso si desea usar las rutas de acceso predeterminadas.

En este ejemplo, se muestra cómo configurar la ruta de acceso raíz para las bases de datos.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabasesRootFolderPath "C:\ExchDbs"

En este ejemplo, se muestra cómo configurar la ruta de acceso raíz para los volúmenes de almacenamiento.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagVolumesRootFolderPath "C:\ExchVols"

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que las rutas de acceso raíz para las bases de datos y los volúmenes se hayan configurado correctamente, ejecute el siguiente comando.

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

El resultado de *AutoDagDatabasesRootFolderPath* y *AutoDagVolumesRootFolderPath* debe reflejar las rutas de acceso configuradas.

## Paso 2: configurar el número de bases de datos por volumen

A continuación, configure el número de bases de datos por volumen (*AutoDagDatabaseCopiesPerVolume*) para el DAG.

En este ejemplo, se muestra cómo configurar la Reinicialización automática para un DAG configurado con cuatro bases de datos por volumen.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabaseCopiesPerVolume 4

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que el número de bases de datos por volumen se haya configurado correctamente, ejecute el siguiente comando.

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

El resultado de *AutoDagDatabaseCopiesPerVolume* debe reflejar el valor configurado.

## Paso 3: crear los directorios raíz para las bases de datos y los volúmenes

A continuación, cree los directorios que correspondan a los directorios raíz configurados en el paso 1. En este ejemplo, se muestra cómo crear los directorios predeterminados mediante el símbolo del sistema.

    md C:\ExchangeDatabases
    md C:\ExchangeVolumes

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que los directorios raíz para las bases de datos y los volúmenes se hayan configurado correctamente, ejecute el siguiente comando.

    Dir C:\

Los directorios creados deben aparecer en la lista de salida.

## Paso 4: montar las carpetas de volumen

Utilice la aplicación Windows Disk Management (diskmgmt.msc) para montar los volúmenes que se usen para las bases de datos (incluidos los volúmenes de reserva) en una carpeta montada en C:\\ExchangeVolumes\\. Por ejemplo, si hay dos volúmenes con bases de datos y un volumen de reserva, monte los volúmenes en las siguientes carpetas montadas:

  - C:\\ExchangeVolumes\\Volumen1

  - C:\\ExchangeVolumes\\Volumen2

  - C:\\ExchangeVolumes\\Volumen3

Los nombres de las carpetas montadas pueden ser cualquier nombre de carpeta, siempre y cuando las carpetas se monten dentro de la ruta del volumen raíz.

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que las carpetas de volumen se hayan montado correctamente, ejecute el siguiente comando.

    Dir C:\

Los volúmenes montados deben aparecer en la lista de resultados.

## Paso 5: crear las carpetas de la base de datos

A continuación, cree los directorios de base de datos en la ruta de acceso raíz C:\\ExchangeDatabases. En este ejemplo, se ilustra cómo crear directorios para una configuración de almacenamiento con cuatro bases de datos en cada volumen.
```
    md c:\ExchangeDatabases\db001
```
```
    md c:\ExchangeDatabases\db002
```
```
    md c:\ExchangeDatabases\db003
```
```
    md c:\ExchangeDatabases\db004
```

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que las carpetas de base de datos se hayan montado correctamente, ejecute el siguiente comando.

    Dir C:\ExchangeDatabases

Los directorios creados deben aparecer en la lista de salida.

## Paso 6: crear los puntos de montaje para las bases de datos

Cree puntos de montaje para las bases de datos y vincúlelos al volumen correcto. Por ejemplo, la carpeta montada para db001 debe estar en C:\\ExchangeDatabases\\db001. Para ello puede utilizar diskmgmt.msc o mountvol.exe. En este ejemplo, se muestra cómo montar db001 en C:\\ExchangeDatabases\\db001 mediante mountvol.exe.

    Mountvol.exe c:\ExchangeDatabases\db001 \\?\Volume (GUID)

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que los puntos de montaje para la base de datos se hayan creado correctamente, ejecute el siguiente comando.

    Mountvol.exe C:\ExchangeDatabases\db001 /L

El volumen montado debe aparecer en la lista de puntos de montaje.

## Paso 7: crear la estructura de directorios de base de datos

Después, cree dos directorios debajo de las carpetas creadas en el paso 5, uno para las bases de datos y otro para las secuencias de registro de las bases de datos que se almacenarán en el mismo volumen. Debe usar el siguiente formato para su estructura de directorios:

C:\\\<*nombreCarpetaBaseDeDatos*\>\\*nombreBaseDeDatos*\\\<*nombreBaseDeDatos*\>.db

C:\\\<*nombreCarpetaBaseDeDatos*\>\\*nombreBaseDeDatos*\\\<*nombreBaseDeDatos*\>.log

En este ejemplo, se muestra cómo crear directorios para cuatro bases de datos que se almacenarán en el Volumen 1:
```
    md c:\ExchangeDatabases\db001\db001.db
```
```
    md c:\ExchangeDatabases\db001\db001.log
```
```
    md c:\ExchangeDatabases\db002\db002.db
```
```
    md c:\ExchangeDatabases\db002\db002.log
```
```
    md c:\ExchangeDatabases\db003\db003.db
```
```
    md c:\ExchangeDatabases\db003\db003.log
```
```
    md c:\ExchangeDatabases\db004\db004.db
```
```
    md c:\ExchangeDatabases\db004\db004.log
```

Repita los comandos anteriores para las bases de datos de cada volumen.

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que la estructura de directorios de las bases de datos se haya creado correctamente, ejecute el siguiente comando.

    Dir C:\ExchangeDatabases /s

Los directorios creados deben aparecer en la lista de salida.

## Paso 8: crear las bases de datos

Cree bases de datos con rutas de bases de datos y de registros configuradas con las carpetas adecuadas. En este ejemplo, se muestra cómo crear una base de datos almacenada en el directorio recién creado y la estructura de puntos de montaje.

    New-MailboxDatabase -Name db001 -Server MBX1 -LogFolderPath C:\ExchangeDatabases\db001\db001.log -EdbFilePath C:\ExchangeDatabases\db001\db001.db\db001.edb

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que las bases de datos se hayan creado correctamente en la carpeta adecuada, ejecute el siguiente comando.

    Get-MailboxDatabase db001 | Format List *path*

Las propiedades de la base de datos que se devuelven deben indicar que el archivo de base de datos y los archivos de registro se almacenan en las carpetas anteriores.

## ¿Cómo sabe si esta tarea se ha completado correctamente?

Para comprobar que haya configurado la Reinicialización automática para un DAG, siga estos pasos:

1.  Ejecute el siguiente comando para comprobar que el DAG está configurado correctamente.
    
        Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

2.  Ejecute el siguiente comando para comprobar que la estructura de directorios esté configurada correctamente (las rutas de acceso predeterminadas se muestran a continuación; si es necesario, sustitúyalas por las que esté usando).
    ```
        Dir c:\ExchangeDatabases /s
    ```
    ```
        Dir c:\ExchangeVolumes /s
    ```

