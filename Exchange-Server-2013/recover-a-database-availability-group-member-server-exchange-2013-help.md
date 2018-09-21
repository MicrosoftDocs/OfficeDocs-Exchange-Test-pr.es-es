---
title: 'Recuperar servidor miembro grupo disponibilidad base datos: Exchange 2013 Help'
TOCTitle: Recuperar un servidor miembro de un grupo de disponibilidad de base de datos
ms:assetid: eccd8f61-9706-4bb7-a62a-ec7c166f8019
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638206(v=EXCHG.150)
ms:contentKeyID: 48268837
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recuperar un servidor miembro de un grupo de disponibilidad de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Si se pierde un servidor de buzones miembro de un grupo de disponibilidad de base datos (DAG), o bien falla, y no puede recuperarse sino que debe reemplazarse, puede llevar a cabo una operación de recuperación de servidor. El programa de instalación de Microsoft Exchange Server 2013 incluye el modificador */m:RecoverServer* que permite realizar una operación de recuperación de servidor. Al ejecutar el programa de instalación con el modificador */m:RecoverServer*, el programa de instalación lee la información de configuración del servidor de Active Directory para buscar un servidor con el mismo nombre que el servidor desde el que se está ejecutando la instalación. Una vez recopilada la información de configuración del servidor de Active Directory, los archivos y servicios originales de Exchange se instalan en el servidor, y los roles y la configuración que se almacenaba en Active Directory se aplica al servidor.

¿Está buscando otras tareas de administración relacionadas con los DAG? Consulte [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 30 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Si se instala Exchange en una ubicación que no sea la predeterminada, debe utilizar el conmutador de instalación */TargetDir* para especificar la ubicación de los archivos de programa de Exchange. Si no utiliza el conmutador */TargetDir*, los archivos de programa de Exchange se instalarán en la ubicación predeterminada (%programfiles%\\Microsoft\\Exchange Server\\V15).
    
    Para determinar la ubicación de la instalación, siga estos pasos:
    
    1.  Abra ADSIEDIT.MSC o LDP.EXE.
    
    2.  Desplácese a la siguiente ubicación: **CN=ExServerName,CN=Servidores,CN=Primer grupo administrativo,CN=Grupos administrativos,CN=ExOrg Name,CN=Microsoft Exchange,CN=Servicios,CN=Configuración,DC=NombreDeDominio,CN=Com**
    
    3.  Haga clic con el botón secundario en el objeto de servidor de Exchange y, a continuación, haga clic en **Propiedades**.
    
    4.  Localice el atributo **msExchInstallPath**. Este atributo almacena la ruta de instalación actual.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar la instalación de /m:RecoverServer para recuperar un servidor

1.  Recupere cualquier configuración de tiempo de retardo de reproducción o de truncamiento para las copias de bases de datos de buzones del servidor que se estén recuperando mediante el cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\)):
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  Quite cualquier copia de base de datos de buzones que haya en el servidor y que se esté recuperando mediante el cmdlet [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335119\(v=exchg.150\)):
    
    ```powershell
Remove-MailboxDatabaseCopy DB1\MBX1
```

3.  Quite la configuración del servidor que presente errores del DAG mediante el cmdlet [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/es-es/library/dd297956\(v=exchg.150\)):
    
    ```powershell
Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```
    

    > [!NOTE]
    > Si el miembro del DAG que va a quitar está sin conexión y no se puede poner en línea, debe agregar el parámetro <EM>ConfigurationOnly</EM> al comando anterior. Si usa el modificador <EM>ConfigurationOnly</EM>, también debe expulsar de forma manual el nodo del clúster.



4.  Restablezca la cuenta de equipo del servidor en Active Directory. Para conocer los pasos detallados, consulte [Restablecimiento de cuentas de equipo](http://go.microsoft.com/fwlink/p/?linkid=167188).

5.  Abra una ventana de símbolo del sistema. Use el medio de instalación original para ejecutar el comando siguiente:
    
    ```powershell
Setup /m:RecoverServer
```

6.  Cuando el proceso de recuperación del programa de instalación se haya completado, agregue el servidor recuperado al DAG mediante el cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/es-es/library/dd298049\(v=exchg.150\)):
    
    ```powershell
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```

7.  Una vez que se ha vuelto a agregar el servidor al DAG, puede volver a configurar las copias de base de datos de buzones mediante el cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298105\(v=exchg.150\)). Si alguna de las copias de base de datos que se van a agregar tenían previamente tiempos de retardo de reproducción o truncamiento superiores a 0, puede usar los parámetros *ReplayLagTime* y *TruncationLagTime* del cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298105\(v=exchg.150\)) para volver a configurar esos parámetros:
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX1
        Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00
        Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -TruncationLagTime 3.00:00:00

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el miembro del DAG se recuperó correctamente, realice lo siguiente:

  - En el Shell, ejecute el siguiente comando para comprobar el estado del miembro del DAG recuperado.
    
    ```
```powershell
Test-ReplicationHealth <ServerName>
```
    ```
    ```
```powershell
Get-MailboxDatabaseCopyStatus -Server <ServerName>
```
    ```
    
    Todas las pruebas de estado de replicación deben tener un resultado satisfactorio y el estado de las bases de datos y sus índices de contenido debe ser adecuado.

