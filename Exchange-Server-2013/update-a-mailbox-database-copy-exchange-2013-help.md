---
title: 'Actualización de una copia de la base de datos de buzones: Exchange 2013 Help'
TOCTitle: Actualización de una copia de la base de datos de buzones
ms:assetid: bead3cc5-7d50-446f-95b7-e432bcb7968e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351100(v=EXCHG.150)
ms:contentKeyID: 48268631
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Actualización de una copia de la base de datos de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-02_

La actualización, también denominada *propagación*, es el proceso por el que se agrega una copia de una base de datos de buzones a otro servidor de buzones en un grupo de disponibilidad de base de datos (DAG). La copia recién agregada se convierte en la base de datos de línea base para la copia pasiva en la que se reproducen los archivos de registro copiados de la copia activa. La inicialización es necesaria en las siguientes condiciones:

  - Cuando se crea una copia pasiva de una base de datos. La inicialización de la copia de una base de datos de buzón nueva se puede posponer, pero tarde o temprano, se deberán inicializar todas las copias de bases de datos pasivas para que funcionen como una copia de base de datos redundante.

  - Tras un error en el que se pierde la información como resultado de que la copia pasiva de la base de datos no se puede recuperar ni divergir.

  - Cuando el sistema ha detectado un archivo de registro dañado que no se puede volver a reproducir en la copia pasiva de la base de datos.

  - Tras una desfragmentación sin conexión de cualquiera de las copias de la base de datos.

  - Después de que una secuencia de generación de registros para la base de datos se haya restablecido en 1.

Para realizar la inicialización lleve a cabo uno de los métodos siguientes:

  - **Propagación automática**   Una propagación automática crea una copia pasiva de la base de datos activa en el servidor de buzones de destino. La inicialización automática solo se produce durante la creación de una base de datos.

  - **Inicialización mediante el cmdlet Update-MailboxDatabaseCopy**   Puede usar el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)) en el Shell para inicializar una copia de la base de datos en cualquier momento.

  - **Inicialización mediante el asistente para la actualización de copias de bases de datos de buzones**   El asistente para la actualización de copias de bases de datos de buzones en la EAC permite propagar una copia de base de datos en cualquier momento.

  - **Copia manual de la base de datos sin conexión**   Puede desmontar la copia activa de la base de datos y copiar el archivo de la base de datos en la misma ubicación en otro servidor de buzones del mismo grupo de disponibilidad de base de datos (DAG). Si utiliza este método, se producirá una interrupción en el servicio ya que el proceso requiere que se desmonte la base de datos.

Actualizar una copia de base de datos puede tardar bastante tiempo, especialmente si la base de datos que se copia es grande o si hay mucha latencia de red o bajo ancho de banda. Después de iniciar el proceso de inicialización, no cierre la EAC ni el Shell hasta que el proceso se haya completado. De lo contrario, la operación de inicialización se dará por terminada.

Las copias de bases de datos se pueden inicializar usando la copia activa o una copia pasiva actualizada como origen para la inicialización. Cuando la inicialización se realiza a partir de una copia pasiva, debe tener en cuenta que la operación de inicialización puede terminar debido a un error de comunicación de red en las circunstancias siguientes:

  - Si el estado de la copia de origen de inicialización cambia a Failed o FailedAndSuspended.

  - Si la base de datos se conmuta por error a otra copia.

Se pueden inicializar varias copias de bases de datos al mismo tiempo. Sin embargo, si realiza la inicialización de varias copias al mismo tiempo, deberá inicializar únicamente el archivo de base de datos y omitir el catálogo del índice de contenido. Para ello, use el parámetro *DatabaseOnly* con el cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335201\(v=exchg.150\)).


> [!NOTE]
> Si al inicializar varios destinos desde un mismo origen, no usa el parámetro <EM>DatabaseOnly</EM>, la tarea finalizará con el error FE1C6491 SeedInProgressException.



¿Busca otras tareas de administración relacionadas con copias de bases de datos de buzones? Consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: dos minutos, más el tiempo necesario para inicializar la copia de base de datos, que depende de varios factores, como el tamaño de la base de datos, la velocidad, el ancho de banda disponible, la latencia de la red y las velocidades de almacenamiento.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Se debe suspender la copia de la base de datos del buzón. Para conocer los pasos detallados, consulte [Suspensión o reanudación de una copia de base de datos de buzones](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md).

  - El servicio de registro remoto debe estar ejecutándose en el servidor hospedando la copia de la base de datos pasiva que está actualizando.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para actualizar una copia de base de datos de buzones

1.  En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  Seleccione la base de datos de buzones cuya copia pasiva desea actualizar.

3.  En el panel de detalles, en **Copias de bases de datos**, haga clic en **Suspender** en la copia de base de datos pasiva que desea propagar. Proporcione cualquier comentario opcional y haga clic en **Guardar**.

4.  En el panel de detalles, en **Copias de bases de datos**, haga clic en **Actualizar** en la copia de base de datos pasiva que desea propagar.

5.  De forma predeterminada, la copia activa de la base de datos se usa como base de datos de origen para la inicialización. Si prefiere utilizar una copia pasiva de la base de datos para la propagación, haga clic en **Examinar…** para seleccionar el servidor que contiene la copia de la base de datos pasiva que desea utilizar para el origen.

6.  Haga clic en **Guardar** para actualizar la copia de la base de datos pasiva.

## Usar el Shell para actualizar una copia de base de datos de buzones

En este ejemplo se muestra cómo inicializar una copia de la base de datos DB1 en MBX1.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1
```

En este ejemplo se muestra cómo inicializar una copia de la base de datos DB1 en MBX1 usando MBX2 como servidor de buzones de origen para la inicialización.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2
```

En este ejemplo se muestra cómo inicializar una copia de la base de datos DB1 en MBX1 sin inicializar el catálogo del índice de contenido.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -DatabaseOnly
```

En este ejemplo se muestra cómo inicializar el catálogo del índice de contenido para la copia de la base de datos DB1 en MBX1 sin inicializar el archivo de la base de datos.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly
```

## Copiar manualmente una base de datos sin conexión

1.  Si la base de datos tiene el registro circular habilitado, se lo debe deshabilitar antes de proceder. El registro circular de una base de datos de buzones de correo puede deshabilitarse mediante el cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)), como se muestra en este ejemplo.
    
    ```powershell
    Set-MailboxDatabase DB1 -CircularLoggingEnabled $false
    ```

2.  Desmonte la base de datos. Puede usar el cmdlet [Dismount-Database](https://technet.microsoft.com/es-es/library/bb124936\(v=exchg.150\)), tal como se muestra en este ejemplo.
    
    ```powershell
    Dismount-Database DB1 -Confirm $false
    ```

3.  Copie manualmente los archivos de base de datos (el archivo de base de datos y todos los archivos de registro) en otra ubicación como, por ejemplo, un disco duro externo o un espacio de red compartido.

4.  Monte la base de datos. Puede usar el cmdlet [Mount-Database](https://technet.microsoft.com/es-es/library/aa998871\(v=exchg.150\)), tal como se muestra en este ejemplo.
    
    ```powershell
    Mount-Database DB1
    ```

5.  En el servidor que hospedará la copia, copie los archivos de base de datos desde el disco externo o el espacio de red compartido a la misma ruta que la copia de base de datos activa. Por ejemplo, si la ruta de la base de datos de copia activa es D:\\DB1\\DB1.edb y la ruta del archivo de registro es D:\\DB1, los archivos de base de datos se copiarán a D:\\DB1 en el servidor que hospedará la copia.

6.  Agregue la copia de base de datos de buzones de correo utilizando el cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298105\(v=exchg.150\)) con el parámetro *SeedingPostponed*, tal y como indica el ejemplo.
    
    ```powershell
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -SeedingPostponed
    ```

7.  Si la base de datos tiene el registro circular habilitado, habilítelo de nuevo utilizando el cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)), tal y como indica el ejemplo.
    
    ```powershell
    Set-MailboxDatabase DB1 -CircularLoggingEnabled $true
    ```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la copia de la base de datos de buzones se inicializó correctamente, realice lo siguiente:

  - En el EAC, vaya a **Servidores** \> **Bases de datos**. Seleccione la base de datos que se propagó. En el panel Detalles se muestra el estado de la copia de base de datos y su índice de contenido, junto con la longitud de cola de la copia actual.

  - En el Shell, ejecute el siguiente comando para comprobar que la copia de la base de datos de buzones se inicializó correctamente y está en buen estado.
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    ```
    
    Los valores de estado y de estado del índice de contenido deben ser correctos.

