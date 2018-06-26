---
title: 'Crear una búsqueda de exhibición de documentos electrónicos local: Exchange 2013 Help'
TOCTitle: Crear una búsqueda de exhibición de documentos electrónicos local
ms:assetid: feedc0c9-4a44-4bb2-8520-cc29d66d4fc3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd353189(v=EXCHG.150)
ms:contentKeyID: 48268923
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una búsqueda de exhibición de documentos electrónicos local

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-01-17_


> [!NOTE]
> Hemos pospuesto la fecha límite del 1 de julio de 2017 para crear nuevas búsquedas de eDiscovery local en Exchange Online (en los planes independientes de Office 365 y Exchange Online). Pero más tarde este año o a principios del año que viene no podrá crear nuevas búsquedas en Exchange Online. Para crear búsquedas de eDiscovery, comience usando <A href="https://go.microsoft.com/fwlink/?linkid=847843">Búsqueda de contenido</A> en el Centro de seguridad y cumplimiento de Office 365. Después de retirar las nuevas búsquedas de eDiscovery local, podrá seguir modificando las búsquedas de eDiscovery local existentes y se admitirá la creación de búsquedas de eDiscovery local en las implementaciones híbridas de Exchange Server 2013 y de Exchange.



Use [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md) para buscar en todo el contenido del buzón, incluso los elementos eliminados y las versiones originales de elementos modificados para usuarios colocados en [Conservación local y retención por juicio](in-place-hold-and-litigation-hold-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Exhibición de documentos electrónicos en contexto" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para crear búsquedas de exhibición de documentos electrónicos es necesario tener una dirección SMTP en la organización en la que se vayan a crear dichas búsquedas. Por lo tanto, en Exchange Online deberá poseer un buzón de Exchange Online (Plan 2) con licencia para poder crear este tipo de búsquedas. En una organización híbrida de Exchange, el buzón de Exchange local debe tener su correspondiente cuenta de usuario de correo en la organización de Office 365 para, así, poder efectuar búsquedas en los buzones de Exchange Online. En caso de que inicie sesión con una cuenta que existe únicamente en Office 365 (como una cuenta de administrador de inquilinos), dicha cuenta deberá tener asignada una licencia de Exchange Online (Plan 2).

  - La instalación de Exchange 2013 crea un buzón de detección denominado **Buzón de búsqueda de detección** para copiar los resultados de la búsqueda. El buzón de búsqueda de detección se crea también de forma predeterminada en Exchange Online. Puede crear buzones de detección adicionales. Para obtener información más detallada, consulte [Crear un buzón de correo de detección](create-a-discovery-mailbox-exchange-2013-help.md).

  - Cuando se crea una búsqueda de exhibición de documentos electrónicos en contexto, los mensajes incluidos en los resultados de la búsqueda no se copian automáticamente en un buzón de detección. Después de crear la búsqueda, puede usar el Centro de administración de Exchange (EAC) para realizar una estimación u obtener una vista previa de los resultados de la búsqueda, así como copiarlos en un buzón de detección. Para más información detallada, consulte:
    
      - Estimate or preview search results (más adelante en este tema)
    
      - [Copiar los resultados de la búsqueda de exhibición de documentos electrónicos en un buzón de correo de detección](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Centro de administración de Exchange para crear una búsqueda de exhibición de documentos electrónicos en contexto

Tal y como se ha explicado anteriormente, para crear búsquedas de exhibición de documentos electrónicos hay que iniciar sesión en una cuenta de usuario que tenga una dirección SMTP en la organización.

1.  Vaya a **Administración del cumplimiento** \> **eDiscovery y retención local**.

2.  Haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En **Suspensión y exhibición de documentos electrónicos local**, en la página **Nombre y descripción** escriba un nombre para la búsqueda, agregue una descripción opcional y, luego, haga clic en **Siguiente**.

4.  En la página **Buzones**, seleccione los buzones para buscar. Puede buscar en todos los buzones o seleccionar buzones específicos para la búsqueda. En Exchange Online, también puede seleccionar grupos de Office 365 como origen de contenido para realizar una búsqueda.
    

    > [!IMPORTANT]
    > La opción <STRONG>Buscar en todos los buzones</STRONG> no sirve para retener todos los buzones. Para crear una retención en contexto, debe seleccionar <STRONG>Especificar los buzones para buscar</STRONG>. Para obtener más información, consulte <A href="create-or-remove-an-in-place-hold-exchange-2013-help.md">Crear o quitar una conservación local</A>.



5.  En la página **Consulta de búsqueda**, complete los campos siguientes:
    
      - **Incluir todo el contenido del buzón del usuario**   Seleccione esta opción para colocar todo el contenido de los buzones seleccionados en retención. Si selecciona esta opción, no puede especificar más criterios de búsqueda.
    
      - **Filtros basados en criterios**   Seleccione esta opción para especificar los criterios de búsqueda, incluso palabras clave, fechas de inicio y finalización, direcciones de remitente y destinatario, y tipos de mensaje.
        
        ![Configurar la consulta de búsqueda de exhibición de documentos electrónicos](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "Configurar la consulta de búsqueda de exhibición de documentos electrónicos")  
    

    > [!NOTE]
    > Los campos <STRONG>De:</STRONG> y <STRONG>Para/CC/CCO:</STRONG> están conectados por un operador <STRONG>OR</STRONG> en la consulta de búsqueda que se crea al ejecutar la búsqueda. Esto significa que en los resultados de la búsqueda se incluyen todos los mensajes enviados o recibidos por cualquiera de los usuarios especificados (y que coinciden con los demás criterios de búsqueda).<BR>Las fechas están conectadas por un operador <STRONG>AND</STRONG>.



6.  En la página **Configuración de retención local**, puede activar la casilla **Pausar el contenido que coincida con la consulta de búsqueda en los buzones seleccionados** y, luego, seleccionar una de las siguientes opciones para poner elementos en retención local:
    
      - **Retener de manera indefinida**   Seleccione esta opción para colocar los elementos devueltos en retención indefinidamente. Los elementos en espera se conservarán hasta que quite el buzón de correo de la búsqueda o la búsqueda.
    
      - **Especificar el número de días para guardar los elementos relacionados con la fecha de recepción** Use esta opción para retener elementos durante un período específico. Por ejemplo, puede usar esta opción si su organización necesita que todos los mensajes se conserven durante un mínimo de siete años. Puede usar una retención en contexto *basada en tiempo* junto con una directiva de retención para asegurarse de que los elementos se eliminen en siete años.
        

        > [!IMPORTANT]
        > Al colocar buzones o elementos en "Retención en contexto" por propósitos legales, normalmente se recomienda retener elementos de forma indefinida y eliminar la retención una vez completado el caso o la investigación.



7.  Haga clic en **Finalizar** para guardar la búsqueda y devolver una estimación del tamaño y cantidad totales de elementos que la búsqueda arrojará en función del criterio especificado. Las estimaciones se muestran en el panel de detalles. Haga clic en **Actualizar**![Icono Actualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icono Actualizar") para actualizar la información que se muestra en el panel de detalles.

Volver al principio

## Usar el Shell para crear una búsqueda de exhibición de documentos electrónicos en contexto

En este ejemplo se crea la búsqueda de exhibición de documentos electrónicos local denominada Discovery-CaseId012 que busca elementos que contienen las palabras clave Contoso y ProjectA, y que también cumplen con los siguientes criterios:

  - Fecha de inicio: 1/1/2009

  - Fecha de finalización: 12/31/2011

  - Buzón de origen: DG-Finance

  - Buzón de destino: Buzón de búsqueda de detección

  - Tipos de mensaje: Email

  - Incluye elementos no aptos para la búsqueda en las estadísticas de búsqueda

  - Nivel de registro: Completa


> [!IMPORTANT]
> Si no especifica parámetros de búsqueda adicionales al ejecutar una búsqueda de exhibición de documentos electrónicos en contexto, se mostrarán en los resultados todos los elementos de los buzones de origen especificados. Si no especifica los buzones donde buscar, la búsqueda se realizará en todos los buzones de la organización de Exchange o Exchange Online.



    New-MailboxSearch "Discovery-CaseId012" -StartDate "01/01/2009" -EndDate "12/31/2011" -SourceMailboxes "DG-Finance" -TargetMailbox "Discovery Search Mailbox" -SearchQuery '"Contoso" AND "Project A"' -MessageTypes Email -IncludeUnsearchableItems -LogLevel Full


> [!NOTE]
> Al usar los parámetros <EM>StartDate</EM> y <EM>EndDate</EM>, debe usar el formato de fecha mm/dd/aaaa, aun cuando el equipo local esté configurado para usar otro formato, como dd/mm/aaaa. Por ejemplo, para encontrar mensajes enviados entre el 1&nbsp;de abril de 2013 y el 1&nbsp;de julio de 2013, usaríamos <STRONG>04/01/2013</STRONG> y <STRONG>07/01/2013</STRONG> como fechas de inicio y fin.



En este ejemplo se crea una búsqueda de exhibición de documentos electrónicos local denominada HRCase090116 que busca mensajes de correo electrónico enviados por Alex Darrow a Sara Davis en 2015.

    New-MailboxSearch "HRCase090116" -StartDate "01/01/2015" -EndDate "12/31/2015" -SourceMailboxes  alexd,sarad -SearchQuery 'From:alexd@contoso.com AND To:sarad@contoso.com' -MessageTypes Email -TargetMailbox "Discovery Search Mailbox" -IncludeUnsearchableItems -LogLevel Full

Tras usar el Shell para crear una búsqueda de exhibición de documentos electrónicos en contexto, deberá iniciar la búsqueda con el cmdlet **Start-MailboxSearch** para copiar los mensajes en el buzón de detección especificado en el parámetro *TargetMailbox*. Para más información, consulte [Copiar los resultados de la búsqueda de exhibición de documentos electrónicos en un buzón de correo de detección](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MailboxSearch](https://technet.microsoft.com/es-es/library/dd298064\(v=exchg.150\)).

Volver al principio

## Usar el EAC para obtener una estimación o vista previa de los resultados

Después de crear una búsqueda de exhibición de documentos electrónicos en contexto, puede usar el EAC para obtener una estimación o una vista previa de los resultados de la búsqueda. Si creó una búsqueda mediante el cmdlet **New-MailboxSearch**, puede hacer uso del Shell para iniciarla con el fin de obtener una estimación de los resultados. No puede usar el Shell para obtener una vista previa de los mensajes de los resultados de búsqueda.

1.  Desplácese a **Administración del cumplimiento** \> **Suspensión y exhibición de documentos electrónicos local**.

2.  En la vista de lista, seleccione la búsqueda de exhibición de documentos electrónicos local y, luego, realice una de las siguientes acciones:
    
      - Haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar") \> **Cálculo de resultados de búsqueda** para devolver un cálculo del tamaño y la cantidad totales de elementos que devolverá la búsqueda en función del criterio especificado. Si la selecciona, la búsqueda se reiniciará y se realizará una estimación.
        
        Las estimaciones de la búsqueda se muestran en el panel de detalles. Haga clic en **Actualizar**![Icono Actualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icono Actualizar") para actualizar la información que se muestra en el panel de detalles.
    
      - Haga clic en **Vista previa de los resultados de búsqueda** en el panel de detalles para obtener una vista previa de los resultados después de que se completa el cálculo de la búsqueda. Al seleccionar esta opción se abre la ventana **Vista previa de búsqueda de exhibición de documentos electrónicos**. Se mostrarán todos los mensajes devueltos de los buzones en los que se efectuó la búsqueda.
        

        > [!NOTE]
        > Los buzones en los que se realizó la búsqueda aparecen recogidos en el panel derecho de la ventana <STRONG>Vista previa de búsqueda de exhibición de documentos electrónicos</STRONG>. También se muestra el número de elementos devuelto y el tamaño total de estos correspondientes a cada buzón. Todos los elementos que la búsqueda ha arrojado aparecen en el panel derecho y se pueden ordenar por más reciente o más antiguo. Los elementos de cada buzón no se pueden ver en el panel derecho si hace clic en un buzón del panel izquierdo. Para ver los elementos devueltos de un buzón específico, puede copiar los resultados de la búsqueda y ver los elementos en el buzón de correo de detección.

    
    ![Estimar u obtener vista previa de resultados de búsqueda](images/Dd353189.57e0fc2d-71bf-42aa-aa4b-4a77148f2b43(EXCHG.150).gif "Estimar u obtener vista previa de resultados de búsqueda")  

Volver al principio

## Usar el Shell para realizar una estimación de los resultados de búsqueda

El conmutador *EstimateOnly* sirve únicamente para obtener una estimación de los resultados, no para copiarlos en un buzón de detección. Se debe iniciar una búsqueda de solo estimación con el cmdlet **Start-MailboxSearch**. A continuación, puede recuperar los resultados de búsqueda estimados mediante el cmdlet **Get-MailboxSearch**.

Así, por ejemplo, para crear una búsqueda de exhibición de documentos electrónicos y, luego, ver una estimación de los resultados, ejecutaríamos los siguientes comandos:

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeKeywordStatistics

    Start-MailboxSearch "FY13 Q2 Financial Results"

    Get-MailboxSearch "FY13 Q2 Financial Results"

Para ver información concreta sobre los resultados de búsqueda estimados del ejemplo anterior, ejecutaríamos el siguiente comando:

    Get-MailboxSearch "FY13 Q2 Financial Results" | FL Name,Status,LastRunBy,LastStartTime,LastEndTime,Sources,SearchQuery,ResultSizeEstimate,ResultNumberEstimate,Errors,KeywordHits

Volver al principio

## Más información sobre las búsquedas de exhibición de documentos electrónicos

  - Después de crear una búsqueda de exhibición de documentos electrónicos, los resultados se pueden copiar en el buzón de detección y exportarlos a un archivo PST. Para más información, consulte:
    
      - [Copiar los resultados de la búsqueda de exhibición de documentos electrónicos en un buzón de correo de detección](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)
    
      - [Exportar los resultados de la búsqueda de exhibición de documentos electrónicos a un archivo PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)

  - Después de ejecutar un cálculo de búsqueda de exhibición de documentos electrónicos (que incluye palabras clave en los criterios de búsqueda), puede ver las estadísticas de palabras clave si hace clic en **Ver estadísticas de la palabra clave** en el panel de detalles de la búsqueda seleccionada. Estas estadísticas muestran detalles sobre el número de elementos proporcionados para cada palabra clave que se usa en la consulta de búsqueda. Sin embargo, si se incluyen más de 100 buzones de origen en la búsqueda, obtendrá un error si intenta ver las estadísticas de palabras clave. Para ver las estadísticas de palabras clave, no se pueden incluir más de 100 buzones de origen en la búsqueda.

  - Si usa **Get-MailboxSearch** en Exchange Online para recuperar información sobre una búsqueda de exhibición de documentos electrónicos, debe especificar el nombre de una búsqueda para devolver una lista completa de las propiedades de búsqueda; por ejemplo, `Get-MailboxSearch "Contoso Legal Case"`. Si ejecuta el cmdlet **Get-MailboxSearch** sin usar parámetros, no se devuelven las siguientes propiedades:
    
      - SourceMailboxes
    
      - Fuentes
    
      - SearchQuery
    
      - ResultsLink
    
      - PreviewResultsLink
    
      - Errores
    
    El motivo es que requiere muchos recursos para devolver estas propiedades para todas las búsquedas de exhibición de documentos electrónicos en su organización.

Volver al principio

