---
title: 'Carpetas públicas: Exchange 2013 Help'
TOCTitle: Carpetas públicas
ms:assetid: 94c4fb69-9234-4b34-8c1c-da2a0a11da65
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150538(v=EXCHG.150)
ms:contentKeyID: 48268450
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Carpetas públicas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2017-03-27_

Las carpetas públicas están diseñadas para un acceso compartido y ofrecen una manera fácil y efectiva de obtener, organizar y compartir información con otras personas de su grupo de trabajo u organización. Las carpetas públicas organizan el contenido en una jerarquía profunda que es fácil de examinar. Los usuarios verán la jerarquía completa en Outlook, lo que les permitirá examinar fácilmente el contenido que les interesa.


> [!NOTE]
> Las carpetas públicas están disponibles en los siguientes clientes de Outlook: Outlook Web App para Exchange 2013, Outlook 2007, Outlook 2010, Outlook 2013 y Outlook para Mac.



Las carpetas públicas también se pueden utilizar como método de archivado para los grupos de distribución. Cuando habilita una carpeta pública para correo y la agrega como miembro del grupo de distribución, el correo electrónico enviado al grupo se agrega automáticamente a la carpeta pública para referencia futura.


> [!NOTE]
> Debe usar Outlook 2007 o superior para acceder a carpetas públicas en servidores Exchange 2013.



Las carpetas públicas no están diseñadas para hacer lo siguiente:

  - **Archivado de datos** Los usuarios que tienen límites de buzón usan a veces carpetas públicas en lugar de buzones para archivar datos. Esto no se recomienda, ya que afecta al almacenamiento en las carpetas públicas y debilita el objetivo de los límites de buzón. En cambio, se recomienda utilizar [Archivado local en Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) como solución de archivado.

  - **Uso compartido de documentos y colaboración** Las carpetas públicas no proporcionan control de versiones ni otras características de administración de documentos, como la funcionalidad de protección y desprotección controladas y la notificación automática de cambios de contenido. En lugar de ello, se recomienda utilizar [SharePoint](https://go.microsoft.com/fwlink/?linkid=282474) como solución para compartir documentos.

Para obtener más información acerca de carpetas públicas y otros métodos de colaboración en Exchange 2013, consulte [Colaboración](collaboration-exchange-2013-help.md).

Para navegar por algunas de las preguntas más frecuentes sobre carpetas públicas en Exchange 2013, consulte [P+F: Carpetas públicas](faq-public-folders-exchange-2013-help.md).

Para obtener más información sobre los límites y las cuotas de las carpetas públicas, consulte [Límites de las carpetas públicas](limits-for-public-folders-exchange-2013-help.md).

Para obtener una lista de las tareas de administración de carpetas públicas, consulte [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

¿Está buscando la versión de Exchange Online de este tema? Vea [Carpetas públicas de Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/jj200758\(v=exchg.150\)).

**Contenido**

Arquitectura de carpetas públicas

Migrar carpetas públicas

Movimientos de carpetas públicas

Cuotas de carpetas públicas

Recuperación ante desastres

## Arquitectura de carpetas públicas

En Exchange 2013, las carpetas públicas se han rediseñado usando infraestructura de buzones de correo para beneficiarse de las tecnologías existentes de alta disponibilidad y almacenamiento de la base de datos de buzones de correo. La arquitectura de carpetas públicas usa buzones de correo especialmente diseñados para almacenar la jerarquía y el contenido de las carpetas públicas. Esto también significa que ya no hay una base de datos de carpetas públicas. La alta disponibilidad para los buzones de correo de carpeta pública se debe al grupo de disponibilidad de base de datos (DAG). Para obtener más información acerca de los DAG, consulte [Grupos de disponibilidad de base de datos (DAG)](database-availability-groups-dags-exchange-2013-help.md).

Los principales componentes de arquitectura de las carpetas públicas son los buzones de carpeta pública, que pueden residir en una o más bases de datos.

## Buzones de carpetas públicas

Existen dos tipos de buzones de carpetas públicas: el *buzón de jerarquía principal* y los *buzones de jerarquía secundarios*. Ambos tipos de buzones de correo pueden incluir contenido:

  - **Buzón de jerarquía principal**   El buzón de jerarquía principal es la única copia grabable de la jerarquía de carpetas públicas. La jerarquía de carpetas públicas se copiará a todos los demás buzones de carpetas públicas, pero serán copias de solo lectura.

  - **Buzones de jerarquía secundarios**   Los buzones de jerarquía secundarios incluyen contenido de carpetas públicas y una copia de solo lectura de la jerarquía de carpetas públicas.


> [!NOTE]
> Las directivas de retención no son compatibles para los buzones de carpetas públicas.



Los buzones de carpetas públicas se pueden administrar de dos maneras:

  - En el Centro de administración de Exchange (EAC), vaya a **Carpetas públicas** \> **Buzones de carpetas públicas**.

  - En el Shell de administración de Exchange, utilice el conjunto de cmdlets **\*-Mailbox**. Los siguientes parámetros se han añadido al cmdlet [New-Mailbox](https://technet.microsoft.com/es-es/library/aa997663\(v=exchg.150\)) para tener compatibilidad con los buzones de carpetas públicas:
    
      - *PublicFolder*   Este parámetro se utiliza con el cmdlet **New-Mailbox** para crear un buzón de carpeta pública. Al crear un buzón de carpeta pública, se crea un nuevo buzón de tipo `PublicFolder`. Para obtener más información, consulte [Crear un buzón de carpetas públicas](create-a-public-folder-mailbox-exchange-2013-help.md).
    
      - *HoldForMigration*   Este parámetro se utiliza sólo si migra carpetas públicas de una versión anterior a Exchange 2013. Para más información, consulte Migrar carpetas públicas más adelante en este tema.
    
      - *IsHierarchyReady*   Este parámetro indica si el buzón de la carpeta pública está listo para servir a la jerarquía de carpetas públicas a los usuarios. Se establece en `$True` solo después de que se haya sincronizado la jerarquía completa con el buzón de carpetas públicas. Si el parámetro se establece en $False, los usuarios no lo usarán para tener acceso a la jerarquía. No obstante, si establece la propiedad *DefaultPublicFolderMailbox* de un buzón de usuario en un buzón de carpetas públicas específico, el usuario podrá tener acceso al buzón de carpetas públicas especificado aunque el parámetro *IsHierarchyReady* no esté establecido en `$False`.
    
      - *IsExcludedFromServingHierarchy*   Este parámetro impide que los usuarios tengan acceso a la jerarquía de carpetas públicas en el buzón de carpetas públicas especificado. A fin de mantener el equilibrio de carga, los usuarios se distribuyen por igual en los buzones de carpetas públicas de manera predeterminada. Cuando este parámetro se establece en un buzón de carpetas públicas, ese buzón no se incluye en el equilibrio de carga automático y los usuarios no podrán tener acceso a él para recuperar la jerarquía de carpetas públicas. No obstante, si establece la propiedad *DefaultPublicFolderMailbox* de un buzón de usuario en un buzón de carpetas públicas específico, el usuario podrá tener acceso al buzón de carpetas públicas especificado aunque el parámetro *IsExcludedFromServingHierarchy* no esté establecido para ese buzón de carpetas públicas.

Un buzón de jerarquía secundaria servirá solamente información de jerarquía de carpetas públicas a los usuarios si se ha especificado explícitamente en los buzones de los usuarios mediante la propiedad *DefaultPublicFolderMailbox*, o si se cumplen las condiciones siguientes:

  - La propiedad *IsHierarchyReady* del buzón de carpetas públicas está establecida en `$True`.

  - La propiedad *IsExcludedFromServingHierarchy* del buzón de carpeta pública está establecida en `$False`.

## Jerarquía de carpetas públicas

La jerarquía de carpetas públicas contiene información organizativa y las propiedades de las carpetas, incluida la estructura de árbol. Cada buzón de carpetas públicas contiene una copia de la jerarquía de carpetas públicas. Solo hay una copia grabable de la jerarquía, que se encuentra en el buzón de carpetas de públicas principal. Para una carpeta específica, la información de jerarquía se utiliza para identificar lo siguiente:

  - Permisos de la carpeta

  - La posición de la carpeta en el árbol de carpetas públicas, incluidas las carpetas principales y secundarias


> [!NOTE]
> La jerarquía no almacena información sobre direcciones de correo electrónico para carpetas públicas habilitadas para correo. Las direcciones de correo se almacenan en el objeto de directorio de Active Directory.



## Sincronización de la jerarquía

El proceso de sincronización de la jerarquía de carpetas públicas utiliza la sincronización de cambios incremental (ICS), que proporciona un mecanismo para supervisar y sincronizar cambios con un contenido o jerarquía de almacén de Exchange. Los cambios incluyen crear, modificar y eliminar carpetas y mensajes. Cuando los usuarios están conectados a los buzones de contenido y los están utilizando, la sincronización se realiza cada 15 minutos. Si no hay usuarios conectados al buzón de contenido, la sincronización se desencadenará con menos frecuencia (cada 24 horas). Si una operación de escritura, como crear una carpeta, se realiza en una jerarquía principal, la sincronización se desencadenará inmediatamente (de forma sincrónica) al buzón de contenido.


> [!IMPORTANT]
> Dado que solo hay una copia grabable de la jerarquía, la creación de carpetas se conecta mediante proxy al buzón de jerarquía en función del buzón de contenido al que están conectados los usuarios.



En una organización grande, cuando crea un nuevo buzón de carpetas públicas, la jerarquía debe sincronizarse a dicha carpeta pública antes de que los usuarios puedan conectarse a la misma. De lo contrario, los usuarios pueden ver una estructura de carpeta pública incompleta cuando se conecten con Outlook. Para dar tiempo para que se produzca esta sincronización sin que los usuarios traten de conectarse al nuevo buzón de carpeta pública, establezca el parámetro *IsExcludedFromServingHierarchy* en el cmdlet **New-Mailbox** al crear el buzón de carpeta pública. Este parámetro impide que los usuarios se conecten al buzón de carpeta pública que se acaba de crear. Cuando se complete la sincronización, ejecute el cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) con el parámetro *IsExcludedFromServingHierarchy* establecido en `false`, lo que indica que el buzón de carpeta pública ya puede aceptar conexiones. También puede usar el cmdlet [Get-PublicFolderMailboxDiagnostics](https://technet.microsoft.com/es-es/library/jj218720\(v=exchg.150\)) para ver el estado de sincronización por las propiedades *SyncInfo* y *AssistantInfo*.

Para obtener más información, consulte [Crear una carpeta pública](create-a-public-folder-exchange-2013-help.md).

## Contenido de carpetas públicas

El contenido de las carpetas públicas puede incluir mensajes de correo electrónico, mensajes, documentos y formularios electrónicos. El contenido se almacena en el buzón de carpetas públicas, pero no se replica en varios buzones de carpetas públicas. Todos los usuarios obtienen acceso al mismo buzón de carpetas públicas para ver el mismo conjunto de contenidos. Si bien se encuentra disponible una búsqueda de texto completo del contenido de las carpetas públicas, no se puede buscar contenido de carpetas públicas entre carpetas públicas y Exchange Search no lo indiza.


> [!NOTE]
> Outlook Web App es compatible, pero con limitaciones. Puede agregar y eliminar carpetas públicas favoritas y realizar operaciones de nivel de elemento, como crear, editar, eliminar y responder mensajes. Sin embargo, no puede crear o borrar carpetas públicas de Outlook Web App. Además, solo las carpetas públicas de Correo, Exponer, Calendario y Contacto se pueden agregar a la lista de favoritos en Outlook Web App.



## Migrar carpetas públicas

Puede migrar las carpetas públicas desde una versión anterior de Exchange Server a Exchange 2013, así como desde versiones anteriores de Exchange Server a Exchange Online. Asimismo, puede migrar las carpetas públicas de Exchange 2013 a Exchange Online

Si ya tiene carpetas públicas de Exchange 2010 SP3 o Exchange 2007 SP3 RU10 en su organización antes de instalar Exchange 2013, debe migrar dichas carpetas públicas a Exchange 2013. Para ello, debe usar los cmdlets **PublicFolderMigrationRequst**. Para obtener más información, consulte [Usar migración por lotes para migrar carpetas públicas a Exchange 2013 desde versiones anteriores](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md). Si su organización está cambiando a Exchange Online, podrá migrar las carpetas públicas a la nube y actualizarlas al mismo tiempo. Para obtener información detallada, consulte [Usar la migración por lotes para migrar carpetas públicas heredadas a Office 365 y Exchange Online](use-batch-migration-to-migrate-legacy-public-folders-to-office-365-and-exchange-online-exchange-online-help.md) y [Usar la migración por lotes para migrar carpetas públicas de Exchange 2013 a Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md).

Debido a los cambios en el sistema de almacenamiento de carpetas públicas, los buzones heredados de Exchange no pueden tener acceso a la jerarquía de carpetas públicas en servidores Exchange 2013 o en Exchange Online. Sin embargo, los buzones de usuarios en servidores Exchange 2013 o Exchange Online pueden conectarse a las carpetas públicas heredadas. Las carpetas públicas de Exchange 2013 y las carpetas públicas heredadas no pueden coexistir simultáneamente en una organización de Exchange. Esto implica que no puede haber coexistencia entre versiones. La migración de carpetas públicas a Exchange Server 2013 o Exchange Online actualmente es un proceso de traslado que se realiza en un único paso.

Por este motivo se recomienda que, antes de migrar las carpetas públicas, migre primero los buzones heredados a Exchange 2013 o Exchange Online. Para obtener más información sobre cómo migrar buzones, consulte [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md), [Realizar una migración total de correo electrónico a Office 365](https://go.microsoft.com/fwlink/p/?linkid=536689) y [Realizar una migración preconfigurada de correo electrónico a Office 365](https://go.microsoft.com/fwlink/p/?linkid=536687).

## Movimientos de carpetas públicas

Puede mover carpetas públicas a un buzón de carpeta pública distinto y puede mover los buzones de carpetas públicas a diferentes bases de datos de buzones de correo. Para mover carpetas públicas a diferentes buzones de carpetas públicas, puede usar el conjunto de cmdlets **PublicFolderMoveRequest**. Las subcarpetas de la carpeta pública que está moviendo no se mueven por defecto. Si quiere mover una rama de carpetas públicas, puede usar el script `Move-PublicFolderBranch.ps1` instalado por defecto en Exchange 2013. Para obtener más información, consulte [Mover una carpeta pública a otro buzón de carpetas públicas](move-a-public-folder-to-a-different-public-folder-mailbox-exchange-2013-help.md).

Además de mover carpetas públicas, puede mover buzones de carpetas públicas a diferentes bases de datos de buzones de correo usando el conjunto de cmdlets **MoveRequest**. Es el mismo conjunto de cmdlets que se utiliza para mover buzones normales. Para obtener más información, consulte [Mover un buzón de carpetas públicas a una base de datos de buzones diferente](move-a-public-folder-mailbox-to-a-different-mailbox-database-exchange-2013-help.md).

Los cmdlets **PublicFolderMoveRequest** y **MoveRequest** usan el servicio de replicación de buzones para mover carpetas públicas de forma asíncrona. Esto significa que el cmdlet no se encarga realmente de esta tarea y que, durante la mayor gran parte del movimiento, la carpeta pública y los buzones de carpetas públicas seguirán estando disponibles para los usuarios. Dado que el servicio de replicación de buzones se encarga de las peticiones para mover, importar y exportar buzones, así como de las peticiones para mover carpetas públicas, es importante tener en cuenta la administración de limitación de peticiones y carga de trabajo.

## Cuotas de carpetas públicas

Al crearse, los buzones de carpetas públicas heredan automáticamente los límites de tamaño que tiene por defecto la base de datos de buzones de correo. En consecuencia, para evaluar con precisión el estado de cuota de almacenamiento actual al usar el cmdlet [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)), debe revisar la propiedad *UseDatabaseQuotaDefaults* además de las propiedades *ProhibitSendQuota*, *ProhibitSendReceiveQuota* y *IssueWarningQuota*. Si la propiedad *UseDatabaseQuotaDefaults* se establece en `true`, se ignoran los ajustes por buzón y se utilizan los límites de la base de datos de buzones de correo. Si la propiedad se establece en `true` y las propiedades *ProhibitSendQuota*, *ProhibitSendReceiveQuota* y *IssueWarningQuota* se establecen en `unlimited`, el tamaño del buzón no es verdaderamente ilimitado. En lugar de ello, debe usar el cmdlet **Get-MailboxDatabase** y revisar los límites de almacenamiento de la base de datos de buzones de correo para determinar cuáles son los límites de los buzones. Si la propiedad *UseDatabaseQuotaDefaults* se establece en `false`, se utilizan los ajustes por buzón. En Exchange 2013, los límites de cuota predeterminados de la base de datos de buzones de correo son los siguientes:

  - *Cuota de advertencia de problema*: 1,9 GB

  - *Cuota de prohibición de envío*: 2 GB

  - *Cuota de prohibición de recepción*: 2,3 GB

Para conocer las cuotas de la base de datos de buzones de correo, ejecute el cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\)).

Para establecer cuotas en un buzón de carpetas públicas, use el cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)).

## Recuperación ante desastres

Las carpetas públicas de Exchange 2013 se construyen en una infraestructura de buzón de correo y usan los mismos mecanismos de disponibilidad y redundancia. Cada buzón de carpeta pública puede tener varias copias redundantes con conmutación automática por error, exactamente igual que los buzones. Para obtener más información, consulte [Alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-exchange-2013-help.md).

Además del escenario general de recuperación ante desastres, también puede restaurar carpetas públicas en las siguientes situaciones:

  - **Restaurar carpetas públicas eliminadas temporalmente**   La carpeta pública se eliminó pero todavía se encuentra en el período de retención.

  - **Restaurar buzones de carpetas públicas eliminadas temporalmente**   El buzón de carpeta pública se eliminó y todavía se encuentra en el período de retención de buzones.

  - **Restaurar buzones de carpetas públicas de una base de datos recuperada**   Puede recuperar un buzón de carpetas públicas determinado de una copia de seguridad cuando ha transcurrido el período de retención de buzones. A continuación, se extraen los datos del buzón restaurado y se copian a una carpeta de destino o se combinan con otro buzón.

En todas estas situaciones, la carpeta pública o el buzón de carpeta pública es recuperable usando los cmdlets **MailboxRestoreRequest**.

Para obtener más información, consulte [Restaurar carpetas públicas y buzones de carpetas públicas de movimientos fallidos](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

