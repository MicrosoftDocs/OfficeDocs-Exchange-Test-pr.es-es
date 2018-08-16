---
title: 'Ver estadística carpeta pública y elemento carpeta pública: Exchange 2013 Help'
TOCTitle: Ver estadísticas de carpetas públicas y elementos de carpetas públicas
ms:assetid: 4e412710-9a74-4649-ab01-502e969a7eda
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997949(v=EXCHG.150)
ms:contentKeyID: 49895620
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ver estadísticas de carpetas públicas y elementos de carpetas públicas

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-14_

En este tema, se explica cómo recuperar estadísticas de una carpeta pública, como el nombre para mostrar, la hora de creación, la hora de la última modificación del usuario, la hora del último acceso del usuario y el tamaño del elemento. Esta información se puede usar para decidir si se debe borrar o mantener una carpeta pública.


> [!NOTE]
> En el Centro de administración de Exchange (EAC), puede ver información sobre cuota y uso de las carpetas públicas navegando a <STRONG>Carpetas públicas</STRONG> &gt; <STRONG>Editar</STRONG><IMG title="Icono Editar" alt="Icono Editar" src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif"> &gt; <STRONG>Uso de buzón de correo</STRONG>. Sin embargo, esta información es incompleta y le aconsejamos que utilice el Shell para ver estadísticas de las carpetas públicas.



Para otras tareas de administración relacionadas con la administración de carpetas públicas, consulte [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las carpetas públicas, consulte [Procedimientos de carpetas públicas en Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/jj966272\(v=exchg.150\)).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Carpetas públicas" en el tema [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - No se puede utilizar el EAC para recuperar las estadísticas de la carpeta pública.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para recuperar estadísticas de las carpetas públicas

En este ejemplo, se obtienen las estadísticas de la carpeta pública llamada Marketing con un comando canalizado para dar formato a la lista.

    Get-PublicFolderStatistics -Identity \Marketing | Format-List


> [!NOTE]
> El valor del parámetro <EM>Identity</EM> debe incluir la ruta de acceso a la carpeta pública. Por ejemplo, si la carpeta pública llamada Marketing existía bajo una carpeta primaria llamada Business, deberá proporcionar los siguientes valores: <CODE>\Business\Marketing</CODE>



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-PublicFolderStatistics](https://technet.microsoft.com/es-es/library/aa998663\(v=exchg.150\)).

## Uso del Shell para ver estadísticas de elementos de carpeta pública

Puede ver la siguiente información de los elementos de una carpeta pública:

  - Tipo de elemento

  - Asunto

  - Hora de la última modificación del usuario

  - Hora del último acceso del usuario

  - Hora de creación

  - Datos adjuntos

  - Tamaño del mensaje

Utilice esta información para tomar decisiones acerca de las acciones que va a realizar con las carpetas públicas, como cuáles de ellas desea eliminar. Por ejemplo, puede que desee eliminar una carpeta pública si no se ha tenido acceso a sus elementos en más de dos años, o también puede convertir una carpeta pública que se usa como repositorio de documentos en otra aplicación de acceso de clientes.

En este ejemplo, se devuelven las estadísticas predeterminadas para todos los elementos en la carpeta pública Pamphlets en la ruta \\Marketing\\2013. La información predeterminada incluye la identidad del elemento, la fecha de creación y el asunto.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"

En este ejemplo, se devuelve información adicional sobre los elementos en la carpeta pública Pamphlets, como el asunto, la última fecha de modificación, la fecha de creación, los archivos adjuntos, el tamaño del mensaje y el tipo de elemento. También incluye un comando canalizado para dar formato a la lista.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-PublicFolderItemStatistics](https://technet.microsoft.com/es-es/library/ee332344\(v=exchg.150\)).

## Uso del Shell para exportar la salida del cmdlet Get-PublicFolderItemStatistics a un archivo .csv

En este ejemplo, se exporta la salida del cmdlet al archivo PFItemStats.csv, que incluye la siguiente información para todos los elementos de la carpeta pública \\Marketing\\Reports:

  - Asunto del mensaje (`Subject`)

  - Fecha y hora de la última modificación del elemento (`LastModificationTime`)

  - Si el elemento tiene datos adjuntos (`HasAttachments`)

  - Tipo de elemento (`ItemType)`)

  - Tamaño del elemento (`MessageSize`)

<!-- end list -->

    Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-PublicFolderItemStatistics](https://technet.microsoft.com/es-es/library/ee332344\(v=exchg.150\)).

