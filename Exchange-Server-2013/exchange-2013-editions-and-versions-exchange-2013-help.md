---
title: 'Exchange 2013: ediciones y versiones: Exchange 2013 Help'
TOCTitle: 'Exchange 2013: ediciones y versiones'
ms:assetid: b563b543-fb3f-4465-9a54-cbfd680aee1f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232170(v=EXCHG.150)
ms:contentKeyID: 50556870
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013: ediciones y versiones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Microsoft Exchange Server 2013 está disponible en dos ediciones de servidor: Standard Edition y Enterprise Edition. Enterprise Edition puede escalarse a 50 bases de datos montadas por servidor en las versiones RTM y CU1, y a 100 bases de datos montadas por servidor en CU2 y versiones posteriores; la Standard Edition está limitada a 5 bases de datos montadas por servidor. Una base de datos montada es una base de datos que está en uso. Una base de datos montada puede ser una base de datos de buzón de correo activa que esté montada para su uso por clientes, o una base de datos de buzón de correo pasiva que esté montada en recuperación para la reproducción y replicación de registros. Aunque se pueden crear más bases de datos que los límites descritos, solo se puede montar el número máximo especificado. La base de datos de recuperación no se tiene en cuenta para este límite.

Estas son ediciones de licencia que vienen definidas por una clave de producto. Al escribir una clave de producto con licencia válida, se implanta la edición correspondiente en el servidor. Las claves de producto sólo se pueden usar para actualizaciones e intercambios de la misma clave de edición, y no para pasar a versiones anteriores. Se puede usar una clave de producto válida para pasar de la versión de evaluación (edición de prueba) de Exchange 2013 a Standard Edition o Enterprise Edition. y para pasar de Standard Edition a Enterprise Edition.

También puede volver a licenciar el servidor con la misma clave de producto de edición. Por ejemplo, si tenía dos servidores con Standard Edition y dos claves pero usó accidentalmente la misma clave en ambos servidores, puede cambiar la clave de uno de ellos y usar la segunda clave que se le proporcionó. Estas acciones pueden realizarse sin necesidad de reinstalar o reconfigurar nada. Una vez escrita la clave de producto y reiniciado el servicio Almacén de información de Microsoft Exchange, quedará reflejada la edición correspondiente a la clave de producto utilizada.

Cuando expire la edición de prueba, no existirá pérdida alguna de funcionalidad, de forma que es posible mantener entornos que no sean de producción, por ejemplo, de laboratorio, demostración y aprendizaje, una vez transcurridos los 120 días sin necesidad de volver a instalar la edición de prueba de Exchange 2013.

Como ya se ha dicho, no puede usar claves de producto para pasar de Enterprise Edition a Standard Edition, ni para volver a la edición de prueba. Este tipo de cambios a versiones anteriores solo se puede realizar mediante la desinstalación de Exchange 2013, la instalación de Exchange 2013 y la especificación de la clave de producto correcta.

## Versiones de Exchange 2013

Para obtener una lista de las versiones de Exchange 2013, así como información sobre cómo descargar y actualizar a la versión más reciente de Exchange 2013, consulte los siguientes temas:

  - [Actualizaciones de Exchange Server: números de compilación y fechas de lanzamiento](https://technet.microsoft.com/es-es/library/hh135098\(v=exchg.150\))

  - [Actualizar Exchange 2013 a la actualización acumulativa o Service Pack más reciente](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)

Para ver el número de compilación de la versión de Exchange 2013 que está usando, ejecute el comando siguiente en el Shell de administración de Exchange.

```powershell
Get-ExchangeServer | fl name,edition,admindisplayversion
```

## Tipos de licencia de Exchange 2013

Las licencias de Exchange 2013 siguen un modelo de licencia de acceso de cliente (CAL) por servidor similar a las licencias de Exchange 2010. Estos son los tipos de licencias:

  - **Licencias de servidor**   Debe asignarse una licencia para cada instancia del software de servidor que se ejecute. La licencia de servidor se vende en dos ediciones de servidor: Standard Edition y Enterprise Edition.

  - **Licencias de acceso de cliente (CAL)**   Exchange 2013 también se presenta en dos ediciones de licencias de acceso de cliente (CAL), que se denominan Standard CAL y Enterprise CAL. Es posible mezclar las ediciones de servidor con los tipos de CAL. Por ejemplo, puede usar Enterprise CAL con Exchange 2013 Standard Edition. Del mismo modo, puede usar Standard CAL con Exchange 2013 Enterprise Edition.

Para más información sobre los tipos de licencia de Exchange, vea [Licencia de Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=392675).

