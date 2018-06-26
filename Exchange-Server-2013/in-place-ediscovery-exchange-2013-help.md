---
title: 'Exhibición de documentos electrónicos en contexto: Exchange 2013 Help'
TOCTitle: Exhibición de documentos electrónicos en contexto
ms:assetid: 6377cb7a-3416-4e15-8571-c45d2160fc6f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298021(v=EXCHG.150)
ms:contentKeyID: 48268212
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exhibición de documentos electrónicos en contexto

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-01-17_


> [!NOTE]
> Hemos pospuesto la fecha límite del 1 de julio de 2017 para crear nuevas búsquedas de eDiscovery local en Exchange Online (en los planes independientes de Office 365 y Exchange Online). Pero más tarde este año o a principios del año que viene no podrá crear nuevas búsquedas en Exchange Online. Para crear búsquedas de eDiscovery, comience usando <A href="https://go.microsoft.com/fwlink/?linkid=847843">Búsqueda de contenido</A> en el Centro de seguridad y cumplimiento de Office 365. Después de retirar las nuevas búsquedas de eDiscovery local, podrá seguir modificando las búsquedas de eDiscovery local existentes y se admitirá la creación de búsquedas de eDiscovery local en las implementaciones híbridas de Exchange Server 2013 y de Exchange.



Si su organización se ajusta a los requisitos legales de detección (relacionados con la directiva de la organización, el cumplimiento o procesos judiciales), la exhibición de documentos electrónicos local en Microsoft Exchange Server 2013 y Exchange Online puede ayudarlo a realizar búsquedas de detección de contenido pertinente dentro de buzones de correo. Exchange 2013 y Exchange Online también ofrecen capacidad de búsqueda federada e integración con Microsoft SharePoint 2013 y Microsoft SharePoint Online. Usando el Centro de exhibición de documentos electrónicos en SharePoint, puede buscar y retener todo el contenido relacionado con un caso, como los sitios web de SharePoint 2013 y SharePoint Online, documentos, recursos compartidos de archivos indexados por SharePoint (SharePoint 2013 solamente), el contenido de los buzones en Exchange y contenido archivado de Lync 2013. También puede usar la exhibición de documentos electrónicos local en un entorno híbrido de Exchange para buscar en buzones locales y de nube en la misma búsqueda.

**Contenido**

Cómo funciona la exhibición de documentos electrónicos local

Exchange Search

Grupo de roles de administración de detección y roles de administración

Ámbitos de administración personalizados para la exhibición de documentos electrónicos local

Integración con SharePoint Server 2013 y SharePoint Online

Exhibición de documentos electrónicos en una implementación híbrida de Exchange

Buzones de detección

Uso de la exhibición de documentos electrónicos local

Estimaciones, vistas previas y copias de resultados de búsquedas

Exportar los resultados de la búsqueda a un archivo PST

Diferentes resultados de búsqueda

Registro de búsquedas de exhibición de documentos electrónicos local

Exhibición de documentos electrónicos local y retención local

Conservar buzones la para exhibición de documentos electrónicos local

Límites de exhibición de documentos electrónicos local y directivas de limitación

Documentación de exhibición de documentos electrónicos local


> [!IMPORTANT]
> La exhibición de documentos electrónicos local es una característica eficaz que permite a un usuario con permisos correctos obtener acceso a todos los registros de mensajería almacenados en la organización de Exchange&nbsp;2013 o Exchange Online. Es importante controlar y supervisar las actividades de detección, como la incorporación de miembros al grupo de roles de administración de detección, la asignación del rol de administración de búsqueda de buzones y la asignación de permisos de acceso a los buzones para buzones de detección.



## Cómo funciona la exhibición de documentos electrónicos local

La exhibición de documentos electrónicos local usa los índices de contenido creados por Exchange Search. El control de acceso basado en roles (RBAC) proporciona el grupo de roles de [Administración de la detección](discovery-management-exchange-2013-help.md) para delegar tareas de detección a personal no técnico, sin la necesidad de proporcionar privilegios elevados que permitan a un usuario realizar cambios operativos en la configuración de Exchange. El Centro de administración de Exchange (EAC) ofrece una interfaz de búsqueda fácil de usar para personal no técnico, como personal legal y de cumplimiento, responsables de registros y profesionales de recursos humanos (RR. HH.).

Para realizar una búsqueda de exhibición de documentos electrónicos local, los usuarios autorizados seleccionan los buzones y, después, especifican criterios clave como palabras clave, fechas de inicio y finalización, direcciones de remitentes y destinatarios, y tipos de mensaje. Una vez completada la búsqueda, los usuarios autorizados pueden seleccionar una de las siguientes acciones:

  - **Cálculo de resultados de búsqueda**   Esta opción devuelve una estimación del tamaño y la cantidad totales de elementos que devolverá la búsqueda en función del criterio especificado.

  - **Vista previa de los resultados de búsqueda**   Esta opción proporciona una vista previa de los resultados. Se muestran los mensajes devueltos de cada buzón en el que se realizó la búsqueda.

  - **Copiar resultados de búsqueda** Esta opción permite copiar los mensajes a un buzón de detección.

  - **Exportar resultados de búsqueda** Una vez copiados los resultados de la búsqueda a un buzón de detección, puede exportarlos a un archivo PST.

![Calcular, mostrar vista previa, copiar y exportar resultados de búsqueda](images/Dd298021.6356971a-34ed-4586-8229-030448d4fe2d(EXCHG.150).gif "Calcular, mostrar vista previa, copiar y exportar resultados de búsqueda")

## Exchange Search

La exhibición de documentos electrónicos local usa los índices de contenido creados por Exchange Search. Exchange Search se ha rediseñado para utilizar Microsoft Search Foundation, una eficaz plataforma de búsqueda con un rendimiento muy mejorado en la indización y la consulta, así como en la funcionalidad de búsqueda. Dado que otros productos de Office también usan Microsoft Search Foundation, incluido SharePoint 2013, esta característica ofrece una gran interoperabilidad y una sintaxis de consulta similar a estos productos.

Con un solo motor de indización de contenido, no es necesario usar recursos adicionales para rastrear e indizar bases de datos para la exhibición de documentos electrónicos local cuando los departamentos de TI reciben solicitudes de exhibición de documentos electrónicos.

La exhibición de documentos electrónicos local utiliza el lenguaje de consulta de palabras clave (KQL), una sintaxis de consulta similar a la sintaxis de consulta avanzada (AQS) que la Búsqueda instantánea usa en Microsoft Outlook y en Outlook Web App. Los usuarios muy familiarizados con KQL pueden construir fácilmente consultas de búsqueda eficaces para buscar índices de contenido.

Para obtener más información acerca de los formatos de archivo indizados por la búsqueda de Exchange, vea [Formatos de archivo indizados por la búsqueda de Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md).

## Grupo de roles de administración de detección y roles de administración

Para que los usuarios autorizados realicen búsquedas de exhibición de documentos electrónicos locales, debe agregarlos al grupo de roles de [Administración de la detección](discovery-management-exchange-2013-help.md). Este grupo de roles consta de dos roles de administración: [Rol Búsqueda entre buzones](mailbox-search-role-exchange-2013-help.md), que permite a los usuarios realizar búsquedas de exhibición de documentos electrónicos locales, y [Rol Retención legal](legal-hold-role-exchange-2013-help.md), que permite a los usuarios poner un buzón en retención local o en retención por juicio.

De forma predeterminada, los permisos para realizar tareas relacionadas con la exhibición de documentos electrónicos local no se asignan a ningún usuario ni a ningún administrador de Exchange. Los administradores de Exchange que son miembros del grupo de roles de administración de la organización pueden agregar usuarios al grupo de roles de administración de detección y crear así grupos de roles personalizados para limitar el ámbito de los administradores de detección respecto a un subconjunto de usuarios. Para obtener más información sobre cómo agregar usuarios al grupo de roles de administración de detección, vea [Asignar permisos de exhibición de documentos electrónicos en Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).


> [!IMPORTANT]
> Si un usuario no se agregó al grupo de roles de administración de detección o no está asignado al rol de búsqueda de buzones de correo, la interfaz de usuario de <STRONG>Suspensión y exhibición de documentos electrónicos local</STRONG> no se mostrará al usuario en el EAC, y los cmdlets de exhibición de documentos electrónicos local no estarán disponibles en el Shell de administración de Exchange.



La auditoría de los cambios de roles de RBAC, que se habilita de forma predeterminada, garantiza que se conserven los registros adecuados para realizar un seguimiento del grupo de roles de administración de detección. Puede usar el informe de grupo de roles de administrador para buscar los cambios realizados en los grupos de roles de administrador. Para obtener más información, vea [Buscar los informes de cambios del grupo de roles o auditorías de administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Volver al principio

## Ámbitos de administración personalizados para la exhibición de documentos electrónicos local

Puede usar un ámbito de administración personalizado para permitir que determinadas personas o grupos usen la exhibición de documentos electrónicos local para buscar un subconjunto de los buzones de la organización de Exchange 2013 o Exchange Online. Por ejemplo, quizás quiera permitir que un administrador de detección realice búsquedas solo en los buzones de los usuarios de un departamento o una ubicación en particular. Para ello, se crea un ámbito de administración personalizado que usa un filtro de destinatarios personalizado para controlar los buzones en los que se pueden realizar búsquedas. Los ámbitos de filtro de destinatario usan filtros para dirigirse a destinatarios específicos en función del tipo de destinatario o de otras propiedades del destinatario.

Para la exhibición de documentos electrónicos local, la única propiedad de un buzón de usuario que puede usar para crear un filtro de destinatarios para un ámbito personalizado es la pertenencia al grupo de distribución. Si usa otras propiedades, como *CustomAttributeN*, *Department* o *PostalCode*, la búsqueda no se realiza correctamente si la ejecuta un miembro del grupo de roles que ha asignado el ámbito personalizado. Para más información, vea [Crear un ámbito de administración personalizado para las búsquedas de exhibición de documentos electrónicos local](create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md).

## Integración con SharePoint Server 2013 y SharePoint Online

Exchange 2013 y Exchange Online ofrecen integración con SharePoint 2013 y SharePoint Online, lo que permite que un administrador de detecciones utilice el Centro de exhibición de documentos electrónicos en SharePoint para realizar las siguientes tareas:

  - **Buscar y conservar contenido desde una sola ubicación** Un administrador de detección autorizado puede buscar y conservar el contenido en SharePoint y en Exchange, incluido el contenido de Lync como las conversaciones de mensajería instantánea y los documentos de reuniones compartidos archivados en buzones de Exchange.

  - **Administración de casos** El centro de exhibición de documentos electrónicos usa un enfoque de administración de casos para la exhibición de documentos electrónicos, lo que permite crear casos y buscar y conservar el contenido en distintos repositorios de contenido para cada caso.

  - **Exportar resultados de la búsqueda** Los administradores de detección pueden usar el centro de exhibición de documentos electrónicos para exportar los resultados de la búsqueda. El contenido de los buzones incluido en los resultados de la búsqueda se exporta a un archivo PST.

SharePoint también utiliza Microsoft Search Foundation para indexar el contenido y realizar consultas. Independientemente de si un administrador de detección usa el EAC o el centro de exhibición de documentos electrónicos para buscar contenido de Exchange, se devuelve el mismo contenido de buzón.

En implementaciones locales, antes de usar el Centro de exhibición de documentos electrónicos en SharePoint para buscar en buzones de Exchange, primero debe establecer una confianza entre ambas aplicaciones. En Exchange 2013 y en SharePoint 2013, esto se hace mediante la autenticación OAuth. Para obtener más información, vea [Configurar Exchange para el Centro de exhibición de documentos electrónicos de SharePoint](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md). Exchange autoriza las búsquedas de exhibición de documentos electrónicos realizadas en SharePoint a través de RBAC. Para que un usuario de SharePoint pueda realizar una búsqueda de exhibición de documentos electrónicos en buzones de Exchange, debe tener asignado el permiso de administración de detección delegado en Exchange. Para poder obtener una vista previa del contenido de buzones devuelto en una búsqueda de exhibición de documentos electrónicos realizada a través del Centro de exhibición de documentos electrónicos de SharePoint, el administrador de detección debe tener un buzón en la misma organización de Exchange.

Para obtener instrucciones paso a paso para configurar un centro de exhibición de documentos electrónicos en una organización de Office 365, consulte [Configurar un centro de exhibición de documentos electrónicos en SharePoint Online](https://go.microsoft.com/fwlink/p/?linkid=331600).

## Exhibición de documentos electrónicos en una implementación híbrida de Exchange

Para realizar con éxito búsquedas de exhibición de documentos electrónicos entre locales en una organización híbrida de Exchange 2013, tendrá que configurar la autenticación OAuth (Open Authorization) entre sus organizaciones de Exchange locales y de Exchange Online para que pueda usar la exhibición de documentos electrónicos local para buscar buzones locales y en nube. La autenticación OAuth es un protocolo de autenticación de servidor a servidor que permite a las aplicaciones autenticarse mutuamente.

La autenticación OAuth admite los siguientes escenarios de exhibición de documentos electrónicos en una implementación híbrida de Exchange:

  - Buzones locales de búsqueda que usan el Archivado de Exchange Online para buzones de archivo en nube.

  - Búsqueda de buzones locales y en nube en la misma búsqueda de exhibición de documentos electrónicos.

  - Búsqueda de buzones locales mediante el centro de exhibición de documentos electrónicos en SharePoint Online.

Para obtener más información acerca de los escenarios de exhibición de documentos electrónicos que requieren autenticación OAuth para configurarse en una implementación híbrida de Exchange, vea [Uso de la autenticación de OAuth para admitir la exhibición de documentos electrónicos en una implementación híbrida de Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md). Para obtener instrucciones paso a paso para configurar la autenticación OAuth para admitir la exhibición de documentos electrónicos, vea [Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## Buzones de detección

Después de crear una búsqueda de exhibición de documentos electrónicos local, puede copiar los resultados de la búsqueda en un buzón de destino. El EAC permite seleccionar un buzón de detección como buzón de destino. Un buzón de detección es un tipo especial de buzón que ofrece la siguiente funcionalidad:

  - **Selección de buzón de correo de destino más simple y segura**   Cuando usa el EAC para copiar los resultados de la búsqueda de exhibición de documentos electrónicos local, solo los buzones de correo de detección estarán disponibles como un repositorio en donde almacenar los resultados de la búsqueda. No necesita revisar una posible lista extensa de buzones disponibles en la organización. Esto también elimina la posibilidad de que un administrador de detección seleccione accidentalmente otro buzón de correo del usuario o un buzón de correo no seguro en donde almacenar mensajes potencialmente confidenciales.

  - **Cuota de almacenamiento en buzones elevada**   El buzón de correo de destino debe poder almacenar la gran cantidad de mensajes que puede generar una búsqueda de exhibición de documentos electrónicos en contexto. De forma predeterminada, los buzones de detección tienen una cuota de almacenamiento de buzones de 50 gigabytes (GB). No se puede incrementar la cuota de almacenamiento.

  - **Más seguro de forma predeterminada**   Como todos los tipos de buzones de correo, un buzón de detección tiene una cuenta de usuario de Active Directory asociada. Sin embargo, esta cuenta está deshabilitada de forma predeterminada. Solamente los usuarios explícitamente autorizados para tener acceso al buzón de correo de detección tienen acceso al mismo. A los miembros del grupo de roles de administración de detección se les asignan permisos de acceso total al buzón de detección predeterminado. Los buzones de detección adicionales que crea no tienen permiso de acceso al buzón de correo asignado a ningún usuario.

  - **Entrega de correo electrónico deshabilitada**   Si bien se puede ver en las listas de direcciones de Exchange, los usuarios no podrán enviar correo electrónico a un buzón de detección. La entrega de correo electrónico a los buzones de detección está prohibida por restricciones de entrega. Esto conserva la integridad de los resultados de la búsqueda que se copiaron a un buzón de detección.

El programa de instalación de Exchange 2013 crea un buzón de detección con el nombre para mostrar **Buzón de búsqueda de detección**. Puede usar el Shell para crear buzones de correo de detección adicionales. De forma predeterminada, los buzones de correo de detección que cree no tendrán permisos de acceso al buzón de correo asignado. Puede asignar permisos de acceso total para que un administrador de descubrimiento tenga acceso a los mensajes copiados a un buzón de detección. Para obtener información más detallada, vea [Crear un buzón de correo de detección](create-a-discovery-mailbox-exchange-2013-help.md).

La exhibición de documentos electrónicos local también usa un buzón del sistema con el nombre para mostrar **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}** para retener los metadatos de la exhibición de documentos electrónicos local. Los buzones del sistema no se pueden ver en el EAC ni en las listas de direcciones de Exchange. En las organizaciones locales, antes de quitar una base de datos de buzones de correo donde esté ubicado el buzón del sistema de exhibición de documentos electrónicos local, mueva el buzón a otra base de datos de buzones de correo. Si el buzón se elimina o está dañado, los administradores de detección no podrán realizar búsquedas de exhibición de documentos electrónicos hasta que vuelva a crear el buzón. Para obtener información detallada, vea [Re-create the Discovery system mailbox](re-create-the-discovery-system-mailbox-exchange-2013-help.md).

Volver al principio

## Uso de la exhibición de documentos electrónicos local

Los usuarios que se agregaron al grupo de roles de administración de detección pueden realizar búsquedas de exhibición de documentos electrónicos local. Puede realizar una búsqueda mediante la interfaz basada en web del EAC. Esto facilita el uso de la exhibición de documentos electrónicos local para los usuarios no técnicos, como los responsables de registros, el personal de cumplimiento o los profesionales legales y de RR. HH. También puede usar el Shell para realizar una búsqueda. Para obtener más información, vea [Crear una búsqueda de exhibición de documentos electrónicos local](create-an-in-place-ediscovery-search-exchange-2013-help.md)


> [!NOTE]
> En organizaciones locales, puede utilizar la exhibición de documentos electrónicos local para buscar en buzones ubicados en servidores de buzones de correo de Exchange&nbsp;2013. Para buscar en buzones ubicados en servidores de buzones de correo de Exchange 2010, utilice la búsqueda en varios buzones en un servidor de Exchange 2010.<BR>En una implementación híbrida, que es un entorno en el que algunos buzones están en los servidores de buzones de correo locales y otros buzones en una organización basada en la nube, se pueden efectuar búsquedas de exhibición de documentos electrónicos local en buzones basados en la nube mediante el EAC de la organización local. Si piensa copiar mensajes en un buzón de detección, primero debe seleccionar un buzón de detección local. Los mensajes de los buzones basados en nube que se devuelven en los resultados de las búsquedas se copian en el buzón de detección local especificado. Para obtener más información acerca de las implementaciones híbridas, vea <A href="https://technet.microsoft.com/es-es/library/jj200581(v=exchg.150)">Implementaciones híbridas de Exchange Server</A>.



El asistente para la **suspensión y exhibición de documentos electrónicos local** del EAC permite crear una búsqueda de exhibición de documentos electrónicos local y usar la retención local para retener los resultados de la búsqueda. Al crear una búsqueda de exhibición de documentos electrónicos local, se crea un objeto de búsqueda en el buzón del sistema de exhibición de documentos electrónicos local. El objeto se puede manipular para iniciar, detener, modificar o quitar la búsqueda. Después de crear la búsqueda, puede optar por obtener una estimación de los resultados de la búsqueda, que incluye las estadísticas de palabras clave que le ayudarán a determinar la efectividad de la consulta. También puede obtener una vista previa dinámica de los elementos devueltos en la búsqueda, lo que permite ver el contenido de los mensajes, el número de mensajes devueltos de cada buzón de origen y el número total de mensajes. Utilice esta información para ajustar aún más la consulta si es necesario.

Cuando esté satisfecho con los resultados de la búsqueda, cópielos a un buzón de detección. También puede usar el EAC o Outlook para exportar un buzón de detección o parte de su contenido a un archivo PST.

Al crear una búsqueda de exhibición de documentos electrónicos local, debe especificar los siguientes parámetros:

  - **Nombre** El nombre de la búsqueda se utiliza para identificar la búsqueda. Al copiar los resultados de la búsqueda en un buzón de detección, se crea una carpeta en el buzón de detección con el nombre de la búsqueda y la marca de tiempo para identificar los resultados de la búsqueda de manera exclusiva en un buzón de detección.

  - **Buzones de correo** Puede elegir entre buscar en todos los buzones de la organización de Exchange 2013 o Exchange Online, o especificar aquellos en los que desee buscar. Los buzones principal y de archivo de un usuario se incluyen en la búsqueda. Asimismo, si desea usar la misma búsqueda para retener elementos, debe especificar los buzones. Puede especificar un grupo de distribución para incluir usuarios de buzones de correo que sean miembros de ese grupo. La pertenencia al grupo se calcula una vez creada la búsqueda. Los cambios posteriores en la pertenencia al grupo no se reflejan de manera automática en la búsqueda.
    
    En Exchange Online también puede especificar grupos de Office 365 como origen de contenido para que se efectúen búsquedas en el buzón de los grupos (o para que quede en suspensión). Al agregar un grupo de Office 365 a una búsqueda de exhibición de documentos electrónicos local, solo se busca en el buzón del grupo (no se busca en los buzones de los miembros del grupo).

  - **Consulta de búsqueda** Puede incluir todo el contenido de los buzones especificados o usar una consulta de búsqueda para devolver elementos que sean más relevantes para el caso o la investigación. Puede especificar los siguientes parámetros en una consulta de búsqueda:
    
      - **Palabras clave**   Puede especificar palabras clave y frases para buscar contenido de mensaje. También puede usar los operadores lógicos **AND**, **OR** o **NOT**. De manera adicional, Exchange 2013 también admite el operador **NEAR**, que permite buscar una palabra o frase que esté cerca de otras.
        
        Para buscar una coincidencia exacta de una frase de varias palabras, debe colocar la frase entre comillas. Por ejemplo, al buscar la frase "plan y competencia" verá mensajes que contienen una coincidencia exacta de la frase, mientras que si especifica **plan AND competencia** verá mensajes que contienen las palabras **plan** y **competencia** en cualquier parte del mensaje.
        
        Exchange 2013 también admite la sintaxis del lenguaje de consulta de palabras clave (KQL) para las búsquedas de exhibición de documentos electrónicos local.
        

        > [!NOTE]
        > La exhibición de documentos electrónicos local no admite expresiones regulares.

        
        Los operadores lógicos deben estar en mayúsculas como, por ejemplo **AND** y **OR**, para que se traten como operadores en lugar de palabras clave. Se recomienda usar paréntesis explícitos en las consultas donde se mezclen varios operadores lógicos para evitar errores o malas interpretaciones. Por ejemplo, si desea buscar mensajes que contengan WordA o WordB AND WordC o WordD, debe usar **(WordA OR WordB) AND (WordC OR WordD)**.
    
      - **Fechas de inicio y de finalización** De forma predeterminada, la exhibición de documentos electrónicos local no limita las búsquedas por intervalos de fechas. Para buscar mensajes enviados durante un intervalo de fechas específico, puede limitar la búsqueda especificando la fecha de inicio y de finalización. Si no especifica una fecha de finalización, la búsqueda mostrará los últimos resultados cada vez que la reinicie.
    
      - **Remitentes y destinatarios** Para limitar la búsqueda, puede especificar los remitentes y los destinatarios de los mensajes. Puede usar direcciones de correo electrónico, nombres para mostrar o el nombre de un dominio para buscar los elementos que ha enviado alguien o que se han enviado a alguien en el dominio. Por ejemplo, para buscar el correo electrónico enviado por alguien o que se le ha enviado a alguien en Contoso, Ltd, especifique **@contoso.com** en el campo **De** o **Para/CC** del EAC. También puede especificar **@contoso.com** en los parámetros *Senders* o *Recipients* en el Shell.
    
      - **Tipos de mensajes** De forma predeterminada, se realizan búsquedas en todos los tipos de mensaje. Para limitar la búsqueda, seleccione tipos de mensaje específicos como correo electrónico, contactos, documentos, diario, reuniones, notas o contenido de Lync.

La siguiente captura de pantalla muestra un ejemplo de una consulta de búsqueda en el EAC.

![Configurar la consulta de búsqueda de exhibición de documentos electrónicos](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "Configurar la consulta de búsqueda de exhibición de documentos electrónicos")

Al utilizar la exhibición de documentos electrónicos local, tenga en cuenta lo siguiente:

  - **Datos adjuntos** La exhibición de documentos electrónicos local busca datos adjuntos que sean compatibles con Exchange Search. Para obtener información detallada, vea [Formatos de archivo indizados por la búsqueda de Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md). En implementaciones locales, puede agregar compatibilidad con tipos de archivos adicionales al instalar filtros de búsqueda (también conocidos como iFilter) para el tipo de archivo que hay en los servidores de buzones de correo.

  - **Elementos que no permiten búsquedas**  Los elementos en los que no se puede buscar son los elementos de los buzones que Exchange Search no puede indizar. Entre los motivos por los que no se pueden indizar se incluye la falta de un filtro de búsqueda instalado para un dato adjunto, un error de filtro o mensajes cifrados. Para que una búsqueda de exhibición de documentos electrónicos se realice correctamente, puede que se le solicite a la organización que incluya dichos elementos para que se revisen. Al copiar los resultados de la búsqueda a un buzón de detección o al exportarlos a un archivo PST, puede incluir elementos no aptos para la búsqueda. Para obtener más información, vea [Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - **Elementos cifrados** Como Exchange Search no puede indizar los mensajes cifrados con S/MIME, la exhibición de documentos electrónicos local no realiza búsquedas en estos mensajes. Si selecciona la opción para incluir los elementos que no permiten búsquedas en los resultados de la búsqueda, estos mensajes cifrados con S/MIME se copian en el buzón de detección.

  - **Elementos protegidos por IRM** Exchange Search indiza los mensajes protegidos con Information Rights Management (IRM) y, por lo tanto, se incluyen en los resultados de la búsqueda si coinciden con los parámetros de consulta. Los mensajes deben protegerse mediante un clúster de Active Directory Rights Management Services (AD RMS) en el mismo bosque de Active Directory que el servidor de buzones de correo. Para obtener más información, vea [Information Rights Management](information-rights-management-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Cuando Exchange Search no indiza un mensaje protegido por IRM, ya sea por un error de descifrado o porque IRM está deshabilitado, el mensaje protegido no se agrega a la lista de elementos en los que se ha producido un error. Si selecciona la opción para incluir los elementos que no permiten búsquedas en los resultados de la búsqueda, es posible que los resultados no incluyan los mensajes protegidos por IRM que no se pudieron descifrar.<BR>Para incluir los mensajes protegidos por IRM en la búsqueda, puede crear otra búsqueda que incluya los mensajes con datos adjuntos .rpmsg. Utilice la cadena de consulta <CODE>attachment:rpmsg</CODE> para buscar mensajes protegidos por IRM en los buzones especificados, independientemente de si están indizados correctamente o no. Esto puede generar cierta duplicación de los resultados de búsqueda en escenarios en los que una búsqueda muestra mensajes que coinciden con los criterios de búsqueda, incluidos los mensajes protegidos por IRM que se han indizado correctamente. La búsqueda no muestra los mensajes protegidos por IRM que no se pudieron indizar.<BR>La realización de una segunda búsqueda de todos los mensajes protegidos por IRM también incluye los mensajes protegidos por IRM que se pudieron indizar correctamente y que mostró la primera búsqueda. Además, es posible que los mensajes protegidos por IRM que muestra la segunda búsqueda no coincidan con los criterios de búsqueda tales como las palabras clave usadas para la primera búsqueda.



  - **Desduplicación** Al copiar los resultados de la búsqueda en un buzón de detección, puede habilitar la *desduplicación* de los resultados de la búsqueda para copiar solo una instancia de un único mensaje en el buzón de detección. Las desduplicación tiene las siguientes ventajas:
    
      - Requisitos de almacenamiento y tamaño de buzón de detección menores debido a la disminución de la cantidad de mensajes copiados.
    
      - Reducción de la carga de trabajo para los administradores de detección, los asesores legales o cualquier otro individuo que esté involucrado en la revisión de los resultados de la búsqueda.
    
      - Reducción del coste de la exhibición de documentos electrónicos, en función del número de elementos duplicados de los resultados de la búsqueda.

Volver al principio

## Estimaciones, vistas previas y copias de resultados de búsquedas

Después de completar una búsqueda de exhibición de documentos electrónicos local, puede ver estimaciones de los resultados de la búsqueda en el panel de detalles del EAC. La estimación incluye el número de elementos devueltos y su tamaño total. También puede ver las estadísticas de palabras clave, que muestran detalles sobre el número de elementos devueltos para cada palabra clave que se usó en la consulta de búsqueda. Esta información resulta útil para determinar la efectividad de la consulta. Si la consulta es demasiado amplia, se devolverá un conjunto de datos mucho mayor, lo que requiere revisar más recursos y podría aumentar los costes de exhibición de documentos electrónicos. Si la consulta es demasiado limitada, podría reducir considerablemente el número de registros devueltos o no devolver ninguno. Utilice las estimaciones y las estadísticas de palabras clave para ajustar la consulta a sus necesidades.


> [!NOTE]
> En Exchange&nbsp;2013, las estadísticas de palabras clave también incluyen estadísticas para las propiedades que no son de palabras clave, como las fechas, los tipos de mensaje y los destinatarios o remitentes especificados en una consulta de búsqueda.



También puede obtener una vista previa de los resultados de la búsqueda para asegurarse de que los mensajes devueltos incluyen el contenido que está buscando y para ajustar aún más la consulta si es necesario. La vista previa de búsquedas de exhibición de documentos electrónicos muestra el número de mensajes devueltos de cada buzón en el que se buscó y el número total de mensajes devueltos por la búsqueda. La vista previa se genera rápidamente, sin tener que copiar los mensajes a un buzón de detección.

Una vez que esté satisfecho con la cantidad y la calidad de los resultados de la búsqueda, cópielos a un buzón de detección. Al copiar los mensajes, tiene las siguientes opciones:

  - **Incluir elementos que no se pueden buscar** Para obtener más información acerca de los tipos de elementos que se considera que no se pueden buscar, vea la consideraciones de las búsquedas de exhibición de documentos electrónicos en la sección anterior.

  - **Habilitar la desduplicación** La desduplicación reduce el conjunto de datos mediante la inclusión de una sola instancia de un único registro si se encuentran varias instancias en uno o más buzones.

  - **Habilitar el registro completo** De forma predeterminada, el registro básico solo se habilita al copiar elementos. Seleccione el registro completo para incluir información sobre todos los registros devueltos por la búsqueda.

  - **Enviarme un correo cuando se haya completado la copia** Una búsqueda de exhibición de documentos electrónicos local puede devolver un gran número de registros. La copia de los mensajes devueltos a un buzón de detección puede llevar mucho tiempo. Use esta opción para recibir una notificación por correo electrónico cuando el proceso de copia se haya completado. Para obtener un acceso más sencillo con Outlook Web App, la notificación incluye un vínculo a la ubicación del buzón de detección en el que se copian los mensajes.

Para obtener más información, vea [Copiar los resultados de la búsqueda de exhibición de documentos electrónicos en un buzón de correo de detección](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

Volver al principio

## Exportar los resultados de la búsqueda a un archivo PST

Una vez copiados los resultados de la búsqueda a un buzón de detección, puede exportarlos a un archivo PST.

![Exportar resultados de búsqueda de exhibición de documentos electrónicos a un archivo PST](images/Dd298021.4ddca8af-1af5-4cb2-852c-e3a292099a58(EXCHG.150).gif "Exportar resultados de búsqueda de exhibición de documentos electrónicos a un archivo PST")

Después de exportar los resultados de la búsqueda a un archivo PST, usted u otros usuarios pueden abrirlos en Outlook para revisar o imprimir los mensajes devueltos en los resultados de búsqueda. Para obtener más información, vea [Exportar los resultados de la búsqueda de exhibición de documentos electrónicos a un archivo PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).

## Diferentes resultados de búsqueda

Dado que la exhibición de documentos electrónicos local realiza búsquedas en los datos en directo, es posible que dos búsquedas de los mismos orígenes de contenido y con la misma consulta de búsqueda devuelvan resultados diferentes. Los resultados de la búsqueda estimados también pueden ser diferentes de los resultados de la búsqueda reales que se copian a un buzón de detección. Esto puede suceder incluso al volver a ejecutar la misma búsqueda dentro de un período de tiempo breve. Hay varios factores que pueden afectar a la coherencia de los resultados de búsqueda:

  - El hecho de que el correo entrante se indiza continuamente, porque Exchange Search rastrea e indiza continuamente las bases de datos de buzones de correo y la canalización de transporte de su organización.

  - La eliminación de correo electrónico por parte de usuarios o procesos automatizados.

  - La importación masiva de grandes cantidades de correo electrónico, que tardan tiempo en indizarse.

Si encuentra resultados distintos con la misma búsqueda, puede mantener los buzones en espera para conservar el contenido, ejecutar búsquedas fuera de las horas pico o dejar tiempo para la indización después de importar grandes cantidades de correo electrónico.

## Registro de búsquedas de exhibición de documentos electrónicos local

Existen dos tipos de registro disponibles para las búsquedas de exhibición de documentos electrónicos local:

  - **Registro básico** El registro básico está habilitado de forma predeterminada para todas las búsquedas de exhibición de documentos electrónicos local. Incluye información acerca de la búsqueda y quién la realizó. La información que captura el registro básico se muestra en el mensaje de correo electrónico que se envía al buzón de correo en el que se almacenan los resultados de la búsqueda. El mensaje se encuentra en la carpeta que se crea para almacenar los resultados de la búsqueda.

  - **Registro completo**   El registro completo incluye información acerca de todos los mensajes que muestra la búsqueda. Esta información se proporciona en un archivo con formato de valores separados por comas (.csv) que se adjunta al mensaje de correo electrónico que contiene la información del registro básico. El nombre de la búsqueda se usa para el nombre del archivo .csv. Esta información puede ser necesaria para el cumplimiento de normas o la conservación de un registro. Para habilitar el registro completo, seleccione la opción **Habilitar el registro completo** al copiar los resultados de búsqueda a un buzón de correo de detección en el EAC. Si usa el Shell, especifique la opción de registro completo mediante el parámetro *LogLevel*.


> [!NOTE]
> Cuando use el Shell para crear o modificar una búsqueda de exhibición de documentos electrónicos local, también puede deshabilitar el registro.



Además del registro de búsqueda incluido al copiar los resultados de la búsqueda en un buzón de detección, Exchange también registra los cmdlets que usa el EAC o el Shell para crear, modificar o quitar búsquedas de exhibición de documentos electrónicos local. Esta información se registra en las entradas del registro de auditoría de administración. Para obtener información detallada, vea [Registro de auditoría de administrador](administrator-audit-logging-exchange-2013-help.md).

Volver al principio

## Exhibición de documentos electrónicos local y retención local

Como parte de las solicitudes de exhibición de documentos electrónicos, es posible que tenga que conservar el contenido de los buzones de correo hasta que finalice un proceso judicial o una investigación. También de se deben conservar los mensajes eliminados o modificados por el usuario o por otros procesos. En Exchange 2013, esto se realiza mediante la retención local. Para obtener información más detallada, vea [Conservación local y retención por juicio](in-place-hold-and-litigation-hold-exchange-2013-help.md).

En Exchange 2013, puede usar el **Asistente de retención y exhibición de documentos electrónicos** para buscar elementos y conservarlos durante el tiempo que sea necesario para la exhibición de documentos electrónicos o para cumplir otros requisitos empresariales. Al usar la misma búsqueda para la exhibición de documentos electrónicos local y la retención local, tenga en cuenta lo siguiente:

  - No puede usar la opción para buscar en todos los buzones. Debe seleccionar los buzones de correo o grupos de distribución.

  - No puede eliminar una búsqueda de exhibición de documentos electrónicos local si la búsqueda también se usa para la retención local. Primero debe deshabilitar la opción de retención local en una búsqueda y, a continuación, eliminar la búsqueda.

## Conservar buzones la para exhibición de documentos electrónicos local

Cuando un empleado deja una empresa, es habitual inhabilitar o eliminar su buzón. Después de deshabilitar un buzón de correo, este se desconecta de la cuenta de usuario, aunque permanece en el buzón durante un período determinado, por lo general, 30 días. El asistente para carpetas administradas no procesa los buzones desconectados y durante este período no se aplica ninguna directiva de retención. No se puede buscar el contenido de un buzón desconectado. Al llegar al período de retención de buzones eliminados configurado para la base de datos de buzones de correo, el buzón se purga de la base de datos de buzones de correo.


> [!IMPORTANT]
> En Exchange Online, la exhibición de documentos electrónicos local puede buscar contenido en buzones inactivos. Los buzones inactivos son buzones de correo que se han puesto en retención local o en retención por juicio. Los buzones inactivos se conservan mientras se hayan puesto en retención. Cuando un buzón inactivo se quita de la retención local o cuando se deshabilita la retención por juicio, queda eliminado permanentemente. Para obtener más información, vea <A href="https://technet.microsoft.com/es-es/library/dn144876(v=exchg.150)">Administrar buzones inactivos en Exchange&nbsp;Online</A>.



En implementaciones locales, si su organización necesita que se apliquen valores de retención a los mensajes de los empleados que ya no trabajan en la organización, o bien si necesita conservar el buzón de un antiguo empleado para una búsqueda de exhibición de documentos electrónicos en curso o futura, no deshabilite ni elimine el buzón. Puede ejecutar los pasos siguientes para asegurarse de que no se pueda acceder al buzón y ni enviarle mensajes.

1.  Deshabilite la cuenta de usuario de Active Directory mediante **Usuarios y equipos de Active Directory** u otra herramienta o script de aprovisionamiento de cuenta de Active Directory. Esto impide que se inicie sesión en el buzón mediante la cuenta de usuario asociada.
    

    > [!IMPORTANT]
    > Los usuarios con permisos de acceso total a buzones podrán tener acceso al buzón. Para evitar que otros usuarios tengan acceso, debe quitarles el permiso de acceso total al buzón. Para obtener información acerca de cómo quitarle permisos de acceso total a un buzón de correo, vea <A href="manage-permissions-for-recipients-exchange-online-help.md">Administrar permisos para los destinatarios</A>.



2.  Establezca el límite de tamaño de los mensajes que el usuario del buzón puede enviar o recibir en un valor muy bajo; por ejemplo, 1 KB. Esto impide la entrega de correo electrónico en el buzón o el envío desde el mismo. Para obtener información detallada, vea [Configurar límites de tamaño de mensaje para un buzón de correo](configure-message-size-limits-for-a-mailbox-exchange-2013-help.md).

3.  Configure las restricciones de entrega del buzón de correo, de modo que nadie pueda enviar mensajes desde el mismo. Para obtener información detallada, vea [Configurar restricciones de entrega de mensajes para un buzón de correo](configure-message-delivery-restrictions-for-a-mailbox-exchange-2013-help.md).


> [!IMPORTANT]
> Ejecute estos pasos junto con cualquier otro proceso de administración de cuentas que su organización exija, sin deshabilitar ni eliminar el buzón o la cuenta de usuario asociada.



Cuando prevea implementar una retención de buzón para una administración de retención de mensajes (MRM), debe tener en cuenta el flujo de mensajes del empleado. Una retención a largo plazo de los buzones de antiguos empleados precisará un almacenamiento adicional en los servidores de buzones de correo, lo que también producirá un incremento de la base de datos de Active Directory, ya que la cuenta del usuario asociado también deberá retenerse por un mismo período de tiempo. Asimismo, será preciso efectuar cambios en los procesos de administración y de aprovisionamiento de cuentas de su organización.

Volver al principio

## Límites de exhibición de documentos electrónicos local y directivas de limitación

En Exchange 2013 y Exchange Online, los recursos que puede consumir la exhibición de documentos electrónicos local se controlan con directivas de limitación de peticiones.

La directiva de limitación predeterminada contiene los siguientes parámetros de limitación.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Descripción</th>
<th>Valor predeterminado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DiscoveryMaxConcurrency</p></td>
<td><p>El número máximo de búsquedas de exhibición de documentos electrónicos local que se pueden ejecutar al mismo tiempo en su organización</p></td>
<td><p>2</p>

> [!NOTE]
> Si se efectúa una búsqueda de exhibición de documentos electrónicos mientras aún se ejecutan dos búsquedas anteriores, la tercera búsqueda no se colocará en cola ni se ejecutará. Debe esperar a que una de las búsquedas anteriores acabe para iniciar correctamente una nueva búsqueda.


</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxMailboxes</p></td>
<td><p>El número máximo de buzones en los que se puede buscar en una sola búsqueda de exhibición de documentos electrónicos local.</p></td>
<td><p>Exchange Online: 10,0001</p>
<p>Exchange 2013: 5,000</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxStatsSearchMailboxes</p></td>
<td><p>El número máximo de buzones que se pueden buscar en una búsqueda única de exhibición de documentos electrónicos local que aún permite ver las estadísticas de palabras clave.</p></td>
<td><p>100</p>

> [!NOTE]
> Tras ejecutar un cálculo de búsqueda de exhibición de documentos electrónicos, puede ver las estadísticas de palabras clave. Estas estadísticas muestran detalles sobre el número de elementos proporcionados para cada palabra clave que se usa en la consulta de búsqueda. Si se incluyen más de 100 buzones de origen en la búsqueda, se devolverá un error si intenta ver las estadísticas de palabras clave.


</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxKeywords</p></td>
<td><p>El número máximo de palabras clave que se pueden especificar en una sola búsqueda de exhibición de documentos electrónicos local.</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxSearchResultsPageSize</p></td>
<td><p>El número máximo de elementos que se muestran en una sola página al obtener una vista previa de resultados de búsqueda de exhibición de documentos electrónicos local.</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>DiscoverySearchTimeoutPeriod</p></td>
<td><p>El número de minutos que se ejecutará una búsqueda de exhibición de documentos electrónicos local antes de que se agote el tiempo de espera.</p></td>
<td><p>10 minutos</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp; Si inicia una búsqueda de exhibición de documentos electrónicos desde el Centro de exhibición de documentos electrónicos de SharePoint Online en una organización de Office 365, puede buscar en 1500&nbsp;buzones en cada búsqueda, como máximo.



En Exchange Server 2013, puede cambiar los valores predeterminados de estos parámetros de modo que se ajusten a sus necesidades, o crear directivas de limitación de peticiones adicionales y asignarlas a usuarios con el permiso delegado Administración de la detección. En Exchange Online, los valores predeterminados de estos parámetros de limitación de peticiones no se pueden cambiar.

## Documentación de exhibición de documentos electrónicos local

La tabla siguiente contiene vínculos a temas que le ayudarán a obtener información acerca de la exhibición de documentos electrónicos local y a administrarla.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tema</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Asignar permisos de exhibición de documentos electrónicos en Exchange</a></p></td>
<td><p>Obtenga información acerca de cómo dar a un usuario acceso para usar la exhibición de documentos electrónicos local en el EAC para buscar en los buzones de Exchange. Agregar un usuario al grupo de roles de administración de la detección también permite que la persona use el Centro de exhibición de documentos electrónicos en SharePoint 2013 y SharePoint Online para buscar en los buzones de Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-discovery-mailbox-exchange-2013-help.md">Crear un buzón de correo de detección</a></p></td>
<td><p>Aprenda a usar el Shell para crear un buzón de detección y asignar permisos de acceso.</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">Crear una búsqueda de exhibición de documentos electrónicos local</a></p></td>
<td><p>Aprenda cómo crear una búsqueda de exhibición de documentos electrónicos local, cómo calcular los resultados de la búsqueda de exhibición de documentos electrónicos, y cómo obtener una vista previa.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=506799">Propiedades de mensajes y operadores de búsqueda para la exhibición de documentos electrónicos local</a></p></td>
<td><p>Obtenga más información sobre qué propiedades de mensajes de correo electrónico se pueden buscar mediante la exhibición de documentos electrónicos local. El tema proporciona ejemplos de sintaxis para cada propiedad, información sobre operadores de búsqueda como <strong>AND</strong> y <strong>OR</strong>, e información sobre otras técnicas de consultas de búsqueda como el uso de comillas dobles (&quot; &quot;) y caracteres comodín de prefijo.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/es-es/library/dn798915(v=exchg.150)">Buscar límites para exhibición de documentos electrónicos local en Exchange Online</a></p></td>
<td><p>Conozca los límites de Exhibición de documentos electrónicos local en Exchange Online que ayudan a conservar el mantenimiento y la calidad de los servicios de Exhibición de documentos electrónicos local para organizaciones de Office 365.</p></td>
</tr>
<tr class="even">
<td><p><a href="start-or-stop-an-in-place-ediscovery-search-exchange-2013-help.md">Iniciar o detener una búsqueda de exhibición de documentos electrónicos local</a></p></td>
<td><p>Obtenga información acerca de cómo iniciar, detener y reiniciar búsquedas de exhibición de documentos electrónicos.</p></td>
</tr>
<tr class="odd">
<td><p><a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">Modificar una búsqueda de exhibición de documentos electrónicos local</a></p></td>
<td><p>Obtenga información acerca de cómo modificar una búsqueda existente de exhibición de documentos electrónicos.</p></td>
</tr>
<tr class="even">
<td><p><a href="copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md">Copiar los resultados de la búsqueda de exhibición de documentos electrónicos en un buzón de correo de detección</a></p></td>
<td><p>Obtenga información acerca de cómo copiar los resultados de una búsqueda de exhibición de documentos electrónicos en un buzón de detección.</p></td>
</tr>
<tr class="odd">
<td><p><a href="export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md">Exportar los resultados de la búsqueda de exhibición de documentos electrónicos a un archivo PST</a></p></td>
<td><p>Obtenga información acerca de cómo exportar los resultados de una búsqueda de exhibición de documentos electrónicos a un archivo PST.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md">Crear un ámbito de administración personalizado para las búsquedas de exhibición de documentos electrónicos local</a></p></td>
<td><p>Aprenda a usar ámbitos de administración personalizados para limitar los buzones en los que puede buscar un administrador de detección.</p></td>
</tr>
<tr class="odd">
<td><p><a href="remove-an-in-place-ediscovery-search-exchange-2013-help.md">Quitar una búsqueda de exhibición de documentos electrónicos local</a></p></td>
<td><p>Obtenga información acerca de cómo eliminar una búsqueda de exhibición de documentos electrónicos.</p></td>
</tr>
<tr class="even">
<td><p><a href="search-for-and-delete-messages-admin-help-exchange-2013-help.md">Buscar y eliminar mensajes: Ayuda para administradores</a></p></td>
<td><p>Aprenda a usar el cmdlet <strong>Search-Mailbox</strong> para buscar y eliminar mensajes de correo electrónico.</p></td>
</tr>
<tr class="odd">
<td><p><a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Reducir el tamaño de un buzón de correo de detección en Exchange</a></p></td>
<td><p>Use este proceso para reducir el tamaño de un buzón de correo de detección que supere los 50 GB.</p></td>
</tr>
<tr class="even">
<td><p><a href="delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md">Eliminar y volver a crear el buzón de correo de detección predeterminado en Exchange</a></p></td>
<td><p>Aprenda a eliminar el buzón de detección predeterminado, a volver a crearlo y, a continuación, a volver a asignarle permisos. Use este procedimiento si este buzón de correo ha superado el límite de 50 GB y no necesita los resultados de la búsqueda.</p></td>
</tr>
<tr class="odd">
<td><p><a href="re-create-the-discovery-system-mailbox-exchange-2013-help.md">Re-create the Discovery system mailbox</a></p></td>
<td><p>Obtenga información acerca de cómo volver a crear el buzón del sistema de detección. Esta tarea solo es aplicable a organizaciones de Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md">Uso de la autenticación de OAuth para admitir la exhibición de documentos electrónicos en una implementación híbrida de Exchange</a></p></td>
<td><p>Obtenga información acerca de los escenarios de exhibición de documentos electrónicos en una implementación híbrida de Exchange que requiere que se configure la autenticación OAuth.</p></td>
</tr>
<tr class="odd">
<td><p><a href="configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md">Configurar Exchange para el Centro de exhibición de documentos electrónicos de SharePoint</a></p></td>
<td><p>Obtenga información acerca de cómo configurar Exchange 2013 para que pueda usar el Centro de exhibición de documentos electrónicos de SharePoint 2013 para buscar en los buzones de Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange</a></p></td>
<td><p>Obtenga información sobre los elementos que la búsqueda de Exchange no puede indizar y que se devuelven en los resultados de la búsqueda de exhibición de documentos electrónicos como elementos que no se pueden buscar.</p></td>
</tr>
</tbody>
</table>


Para obtener más información sobre la exhibición de documentos electrónicos en Office 365, Exchange 2013, SharePoint 2013 y Lync 2013, consulte [Preguntas más frecuentes sobre la exhibición de documentos electrónicos](https://go.microsoft.com/fwlink/p/?linkid=386633).

Volver al principio

