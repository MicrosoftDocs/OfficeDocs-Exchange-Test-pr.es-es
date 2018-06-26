---
title: 'P+F: Carpetas públicas: Exchange 2013 Help'
TOCTitle: 'P+F: Carpetas públicas'
ms:assetid: 1cdcdcb7-f11b-45ca-ad23-7c38f640208c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ552408(v=EXCHG.150)
ms:contentKeyID: 49116073
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# P+F: Carpetas públicas

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2017-03-27_

En este tema, se proporciona una lista de las preguntas más frecuentes referentes a las carpetas públicas en Exchange Server 2013. Para obtener más información acerca de las carpetas públicas, consulte [Carpetas públicas](public-folders-exchange-2013-help.md).

¿Tiene preguntas acerca de las carpetas públicas que no encuentran respuesta aquí? Envíenos un correo electrónico a [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com).

## Preguntas frecuentes acerca de la migración de las carpetas públicas

Esta sección contiene las preguntas más frecuentes acerca de la migración de carpetas públicas. Para obtener más información, vea [Usar migración por lotes para migrar carpetas públicas a Exchange 2013 desde versiones anteriores](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md), [Usar la migración por lotes para migrar carpetas públicas heredadas a Office 365 y Exchange Online](use-batch-migration-to-migrate-legacy-public-folders-to-office-365-and-exchange-online-exchange-online-help.md)o [Usar la migración por lotes para migrar carpetas públicas de Exchange 2013 a Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md).

## ¿Cuáles son los escenarios admitidos de migración de carpetas públicas?

La lista siguiente describe las opciones disponibles para migrar carpetas públicas a Exchange 2013 o Exchange Online.

  - Las carpetas públicas de Exchange 2007 (RU15 SP3 o posterior) pueden migrarse a Exchange 2013 o Exchange Online.

  - Las carpetas públicas de Exchange 2010 (RU8 SP3 o posterior) pueden migrarse a Exchange 2013 o Exchange Online.

  - Las carpetas públicas de Exchange 2013 (CU15 o posterior) se pueden migrar a Exchange Online.

Actualmente, sólo las migraciones a Exchange 2013 en el mismo bosque de Active Directory son compatibles. Las migraciones entre bosques se admitirá en el futuro.

## Tras la migración, ¿qué pasa con la jerarquía en los servidores de origen de Exchange 2010?

Durante la fase de finalización de la migración, se coloca un bloqueo en el servidor de origen para que el usuario no pueda acceder al mismo. Este bloqueo se mantiene para evitar que los usuarios obtengan acceso a las carpetas públicas de origen una vez completada la migración. Si bien es posible liberar este bloqueo, no es recomendable, ya que los cambios no se pueden sincronizar con Exchange 2013.

## ¿Qué sucede con las reglas existentes de las carpetas públicas cuando las carpetas públicas se migran?

Las reglas de las carpetas públicas se migran junto con los datos, y se mantienen como reglas de las carpetas públicas. No se convierten en reglas de buzón de correo.

## ¿Qué pasa si los cambios en la jerarquía se realizan en el origen después de que se genere el archivo .csv inicial? ¿Cómo se reflejaría en el destino?

El archivo .csv se usa para determinar la asignación entre la jerarquía de origen y el buzón de correo de destino. Contiene sólo las carpetas de nivel superior. Las carpetas secundarias se migran automáticamente en las carpetas de nivel superior. Por lo tanto, si se añade una carpeta secundaria, se migra durante el proceso. Si se crea una nueva carpeta de nivel superior, se creará en el buzón de correo que contenga la copia que se puede escribir de la jerarquía.

## Durante la migración a las carpetas públicas de Exchange 2013, si hay una ventana larga de tiempo entre la suspensión y la finalización, ¿cómo puedo forzar una sincronización delta para que los usuarios puedan acceder a las carpetas públicas durante la sincronización final?

Puede forzar una sincronización delta para que se produzca antes de la finalización (antes de bloquear el origen) ejecutando el siguiente comando de Shell:

    Resume-PublicFolderMigrationRequest \PublicFolderMigration

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Resume-PublicFolderMigrationRequest](https://technet.microsoft.com/es-es/library/jj218689\(v=exchg.150\)).

## Para la migración de una jerarquía distribuida geográficamente, ¿cómo puedo asegurarme que las carpetas se crean en la ubicación más cercana a los usuarios de destino?

Como parte del proceso de migración, se genera un archivo .csv (con el script `publicfoldertomailboxmapgenerator.ps1`). Este archivo contiene la asignación de la carpeta al buzón para la nueva jerarquía. Puede usar este archivo .csv para crear buzones de correo de carpetas públicas en la ubicación geográfica adecuada y modificar el archivo para tener las carpetas necesarias en el buzón de correo necesario para que estén cerca de los usuarios de destino.

El archivo .csv de entrada se puede generar ejecutando el script `AggregatePFData.ps1`, ubicado en el directorio \<*Exchange Installation Directory*\>\\V15\\Scripts. Ejecute el script como se indica a continuación:

    .\AggregatePFData.ps1 | Select-Object -property @{Name="FolderName"; Expression = {$_.Identity}}, @{Name="FolderSize"; Expression = {$_.TotalItemSize.Value.ToBytes()}} | Export-CSV -Path <Path followed by the name of the CSV>

## ¿Los permisos de carpetas públicas existentes migran?

Sí, los permisos migran automáticamente en la carpeta con los datos. No es necesario realizar este paso por separado.

## ¿Las carpetas públicas van a desaparecer?

No. Las carpetas públicas son excelentes para la integración de Outlook, para casos de compartición simple y para permitir que un gran público pueda acceder a los mismos datos.

## ¿Qué clientes son compatibles con las carpetas públicas?

Los usuarios de Outlook 2007, Outlook 2010, Outlook 2013 y Outlook 2011 para Mac pueden obtener acceso a las carpetas públicas. Sin embargo, los usuarios cuyos buzones están en servidores de Exchange 2013, no podrán conectarse a carpetas públicas de Exchange 2007 o Exchange 2010 desde clientes que usen servicios Web Exchange (EWS), como Outlook para Mac. Le recomendamos migrar las carpetas públicas heredadas a Exchange 2013 para mantener el acceso para esos usuarios.

## ¿Existen limitaciones en los clientes?

Outlook Web App se admite, pero con limitaciones. Puede agregar y quitar carpetas públicas favoritas (si son carpetas públicas de correo, mensajes, calendario y contactos) y realizar operaciones en el nivel de elemento, como crear, editar, eliminar y responder mensajes. Pero no puede hacer lo siguiente en Outlook Web App:

  - Crear o eliminar carpetas públicas.

  - Arrastrar y soltar contenido.

  - Acceder a carpetas públicas ubicadas en servidores que ejecutan versiones anteriores de Exchange.


> [!NOTE]
> Solo se pueden crear reglas de carpeta pública que contengan el elemento <STRONG>responder usando una plantilla determinada</STRONG> en las carpetas públicas habilitadas para correo. Es posible que las reglas preexistentes que contengan <STRONG>responder usando una plantilla determinada</STRONG> continúen funcionando en las carpetas públicas no habilitadas para correo, pero en dichas carpetas no es posible crear nuevas reglas con este elemento de plantilla ni modificar reglas existentes con este elemento.



En un escenario híbrido, Outlook en la web y Outlook 2011 para Mac no se admiten en las carpetas públicas entre locales. Los usuarios deben estar en la misma ubicación que las carpetas públicas para acceder a ellas con Outlook 2011 para Mac o Outlook en la web. Los usuarios de Outlook de 2016 para Mac pueden acceder a las carpetas públicas en un escenario híbrido, si se permiten los procedimientos en [Procedimientos de implementación híbrida](https://technet.microsoft.com/es-es/library/jj200788\(v=exchg.150\).aspx) y se ha instalado la actualización de abril de 2016 de Outlook 2016 para Mac en todos los clientes.

## ¿Cómo puedo guardar una jerarquía muy amplia en un buzón de correo de carpetas públicas?

Para obtener más información acerca de los límites de almacenamiento de carpetas públicas, consulte [Límites de las carpetas públicas](limits-for-public-folders-exchange-2013-help.md).

## ¿Cómo puedo ver el buzón carpetas públicas de la jerarquía?

Ejecute el siguiente comando:

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997571\(v=exchg.150\)).

## ¿Cómo puedo crear buzones de correo de contenido para carpetas públicas con los cmdlets del Shell de administración de Exchange?

Ejecute el siguiente comando para crear el primer buzón de correo electrónico de carpetas públicas de jerarquía maestro y los buzones de correo de jerarquías secundarios.

    New-Mailbox -PublicFolder -Name <name of public folder>

Para obtener más información, consulte [Crear una carpeta pública](create-a-public-folder-exchange-2013-help.md).

## En versiones anteriores de Exchange, cada base de datos de buzones de correo tenía una opción para especificar si base de datos de carpetas públicas. ¿Cómo funcionará en Exchange 2013?

No hay configuración en el nivel de la base de datos en Exchange 2013. Exchange 2013 tiene la capacidad en el nivel del buzón de correo de especificar el buzón de carpetas públicas, pero, de manera predeterminada, Exchange calcula automáticamente el buzón de correo de jerarquía por usuario.

## ¿Cómo se utilizan herramientas métricas de carpetas públicas en Exchange 2013?

En Exchange 2013, puede usar los cmdlets [Get-PublicFolderStatistics](https://technet.microsoft.com/es-es/library/aa998663\(v=exchg.150\)) y [Get-PublicFolderItemStatistics](https://technet.microsoft.com/es-es/library/ee332344\(v=exchg.150\)) para obtener los datos de métricas de las carpetas públicas. Es la misma solución que teníamos en Exchange 2010, así que aquí no hay cambios. Las carpetas públicas no requieren complementos adicionales de presentación de informes.

## ¿Las carpetas públicas pueden distinguir entre el acceso interno a las carpetas públicas y el acceso de terceros?

En Exchange 2013, los permisos de las carpetas públicas se administran mediante el Control de acceso basado en roles (RBAC). Las listas de control de acceso (ACL) no se usan en Exchange 2013. Puede usar los cmdlets [Get-PublicFolderStatistics](https://technet.microsoft.com/es-es/library/aa998663\(v=exchg.150\)) y [Get-PublicFolderItemStatistics](https://technet.microsoft.com/es-es/library/ee332344\(v=exchg.150\)) para mantener un registro de las cuentas que están realizando tareas administrativas y, luego, auditar el acceso según corresponda. Para obtener más información acerca de RBAC, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

## ¿El registro de auditoría de buzones funciona en las carpetas públicas?

No, en estos momentos no funciona.

## ¿Cuáles son los límites de las carpetas públicas? ¿Cuáles son las recomendaciones?

Para obtener más información acerca de los límites de carpetas públicas, consulte [Límites de las carpetas públicas](limits-for-public-folders-exchange-2013-help.md).

## ¿Cuáles son las recomendaciones para la división de buzones de carpetas públicas? ¿Deben permanecer en la misma base de datos?

En versiones anteriores de Exchange, se podían dividir las carpetas públicas entre las bases de datos de carpetas públicas. Puede decidir si quiere dividir el contenido de un buzón de carpetas públicas en un buzón de la misma base de datos de buzones o una base de datos diferente. Normalmente, se recomienda la división en una base de datos individual, ya que lo que quiere es equilibrar el almacenamiento y la entrada/salida.

## ¿Es posible configurar directivas de retención en las carpetas públicas?

Al igual que en versiones anteriores de Exchange, es posible configurar límites de retención en elementos. Para obtener información detallada, consulte [Límites de las carpetas públicas](limits-for-public-folders-exchange-2013-help.md).

## ¿Es posible especificar qué usuarios pueden usar un buzón de correo de carpetas públicas específico?

En Exchange 2007 y en Exchange 2010, era posible especificar qué usuarios tenían acceso a carpetas públicas específicas. En Exchange 2013, puede establecer el buzón de correo de las carpetas públicas por usuario. Para hacerlo, ejecute el cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) con el parámetro *DefaultPublicFolderMailbox*.

    Set-Mailbox -Identity kweku@contoso.com -DefaultPublicFolderMailbox "PF_Administration"

## Si la jerarquía principal falla, ¿cuál es el impacto en el usuario?

Si el buzón de correo de carpetas públicas de la jerarquía principal falla, el usuario puede ver las carpetas públicas, pero no escribir en ellas. Para ayudar a prevenir los fallos en la jerarquía, le recomendamos que las carpetas públicas se incluyan en un grupo de disponibilidad de bases de datos (DAG). Para obtener más información acerca de los DAG, consulte [Grupos de disponibilidad de base de datos (DAG)](database-availability-groups-dags-exchange-2013-help.md).

## ¿Es posible cambiar qué buzón de carpetas públicas es el buzón de correo de jerarquía principal?

No. Si intenta cambiar el buzón de correo de la jerarquía maestro, recibirá un error.

## ¿Las carpetas públicas tienen funcionalidades de búsqueda de texto completo?

Sí, la función de búsqueda de texto completo está disponible para las carpetas públicas de Exchange 2013. Sin embargo, no podrá realizar búsquedas entre múltiples carpetas públicas.

