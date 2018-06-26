---
title: 'Portabilidad de bases de datos: Exchange 2013 Help'
TOCTitle: Portabilidad de bases de datos
ms:assetid: 387b727a-ce51-4910-b5c4-613c693fa5bd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876873(v=EXCHG.150)
ms:contentKeyID: 51406500
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Portabilidad de bases de datos

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2017-01-30_

La portabilidad de bases de datos es una característica que permite que una base de datos de buzones de correo de Microsoft Exchange Server 2013 se pueda mover o montar en cualquier otro servidor de buzones de correo en la misma organización que ejecuta Exchange 2013 y que tiene bases de datos con la misma versión de esquema de la base de datos. Las bases de datos de buzones de correo de versiones anteriores de Exchange no pueden moverse a un servidor de buzón que ejecuta Exchange 2013. Al usar esta función, la fiabilidad se mejora mediante la eliminación de varios pasos manuales propensos a errores en el proceso de recuperación. Además, la portabilidad de bases de datos reduce los tiempos de recuperación completa en distintos escenarios de error.

Cuando se usa la portabilidad de bases de datos para recuperar una base de datos de buzones de correo, la versión del sistema operativo y la versión de Exchange Server en los servidores Exchange de origen y de destino deben ser las mismas. Por ejemplo, si una base de datos de buzones de correo de Exchange 2013 se ha montado anteriormente en un servidor que ejecuta Windows Server 2012, la portabilidad de bases de datos solo funcionará al migrar la base de datos a un servidor que también ejecute Windows Server 2012 y Exchange 2013.

Para obtener información acerca de cómo llevar a cabo una recuperación de bases de datos a través de la característica de portabilidad de bases de datos, consulte [Mover una base de datos de buzones mediante la portabilidad de bases de datos](move-a-mailbox-database-using-database-portability-exchange-2013-help.md).

