---
title: 'Copiar los resultados de la búsqueda de exhibición de documentos electrónicos en un buzón de correo de detección: Exchange 2013 Help'
TOCTitle: Copiar los resultados de la búsqueda de exhibición de documentos electrónicos en un buzón de correo de detección
ms:assetid: bff2ce89-9e6f-494a-bd6a-2f2011507845
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn624163(v=EXCHG.150)
ms:contentKeyID: 61183332
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Copiar los resultados de la búsqueda de exhibición de documentos electrónicos en un buzón de correo de detección

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-24_

Después de crear una búsqueda de exhibición de documentos electrónicos local, puede usar el EAC para copiar los resultados en un buzón de correo de detección. También puede usar el Shell para iniciar una búsqueda de exhibición de documentos electrónicos que se creó con el cmdlet **New-MailboxSearch**, que copiará los resultados en el buzón de correo de detección que se especificó cuando creó la búsqueda.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos o más según la cantidad de elementos del buzón de correo que se proporcionen en los resultados de la búsqueda.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el sección "Exhibición de documentos electrónicos local" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para poder copiar los resultados de la búsqueda, debe crearse una búsqueda de exhibición de documentos electrónicos, mediante el EAC o el Shell. Para obtener información detallada, vea [Crear una búsqueda de exhibición de documentos electrónicos local](create-an-in-place-ediscovery-search-exchange-2013-help.md).

  - La instalación de Exchange 2013 crea un buzón de correo de detección denominado **Buzón de búsqueda de detección** para copiar los resultados de la búsqueda. El buzón de búsqueda de detección se crea también de forma predeterminada en Exchange Online. Puede crear buzones de detección adicionales. Para obtener información detallada, vea [Crear un buzón de correo de detección](create-a-discovery-mailbox-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué quiere hacer?

## Usar el EAC para copiar los resultados de la búsqueda

1.  En el EAC, vaya a **Administración de cumplimiento** \> **eDiscovery y retención local**.

2.  En la vista de lista, seleccione una búsqueda de exhibición de documentos electrónicos.

3.  Haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar") y luego haga clic en **Copiar resultados de búsqueda** en la lista desplegable.

4.  En **Copiar resultados de búsqueda**, seleccione entre las siguientes opciones:
    
      - **Incluir elementos que no se pueden buscar**   Active esta casilla para incluir elementos de buzones que no se pudieron buscar (por ejemplo, mensajes con archivos adjuntos de tipos de archivo que la búsqueda de Exchange no pudo indexar). Para más información, vea [Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).
    
      - **Habilitar la desduplicación**   Active esta casilla para excluir los mensajes duplicados. Solo una instancia del mensaje se copiará en el buzón de correo de detección.
    
      - **Habilitar registro completo**   Active esta casilla para incluir un registro completo en los resultados de la búsqueda.
    
      - **Enviarme un correo cuando se haya completado la copia**   Active esta casilla para recibir una notificación por correo electrónico cuando la búsqueda se haya completado.
    
      - **Copia los resultados en este buzón de correo de detección**   Haga clic en **Examinar** para seleccionar el buzón de detección en donde desea que se copien los resultados de la búsqueda.
        
        ![Copiar resultados de búsqueda](images/Dn624163.875e25ed-8308-408c-92c4-8c76fc9d9bfc(EXCHG.150).gif "Copiar resultados de búsqueda")  

5.  Haga clic en **Copiar** para iniciar el proceso de copia de los resultados de la búsqueda en el buzón de correo de detección especificado.

6.  Haga clic en **Actualizar**![Icono Actualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Icono Actualizar") para actualizar la información sobre el estado de copia que se muestra en el panel de detalles.

7.  Una vez que la copia esté completa, haga clic en **Abrir** para abrir el buzón de correo de detección para ver los resultados de la búsqueda.

## Usar el Shell para copiar los resultados de la búsqueda

Después de usar el cmdlet **New-MailboxSearch** para crear una búsqueda de exhibición de documentos electrónicos local, debe iniciar la búsqueda para copiar mensajes al buzón de correo de detección especificado en el parámetro *TargetMailbox*. Para obtener más información sobre cómo crear búsquedas de exhibición de documentos electrónicos mediante el Shell, vea:

  - [Use the Shell to create an In-Place eDiscovery search](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [New-MailboxSearch](https://technet.microsoft.com/es-es/library/dd298064\(v=exchg.150\))

Por ejemplo, para iniciar una búsqueda de exhibición de documentos electrónicos llamada *Fabrikam Investigation* debería ejecutar el siguiente comando para copiar los resultados de la búsqueda en el buzón de correo de detección especificado.

    Start-MailboxSearch "Fabrikam Investigation"

Si usó el modificador *EstimateOnly* para obtener un cálculo de los resultados de la búsqueda, debe quitar el modificador antes de poder copiar los resultados de la búsqueda. También debe especificar un buzón de correo de detección en el que copiará los resultados de la búsqueda. Por ejemplo, supongamos que creó una búsqueda solo de cálculo mediante el siguiente comando:

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeUnsearchableItems

Para copiar los resultados de esta búsqueda en un buzón de correo de detección, debería ejecutar los siguientes comandos:

    Set-MailboxSearch "FY13 Q2 Financial Results" -EstimateOnly $false -TargetMailbox "Discovery Search Mailbox"

    Start-MailboxSearch "FY13 Q2 Financial Results"

## Más información sobre cómo copiar los resultados de la búsqueda

  - Después de copiar los resultados de la búsqueda en el buzón de correo de detección, puede exportar esos resultados de la búsqueda en un archivo PST. Para más información, vea [Exportar los resultados de la búsqueda de exhibición de documentos electrónicos a un archivo PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).

  - Para obtener más información acerca de los elementos que no se pueden buscar, vea [Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - Si va a copiar todo el contenido del buzón dentro de un intervalo de fechas específico (no especificando ninguna palabra clave en los criterios de búsqueda), todos los elementos que no se pueden buscar dentro de ese intervalo de fechas se incluirán automáticamente en los resultados de la búsqueda. Por lo tanto, no active la casilla **Incluir elementos que no se pueden buscar** cuando copie resultados de la búsqueda. De lo contrario, se copiará una copia duplicada de todos los elementos que no se pueden buscar en el buzón de correo de detección.

  - Además de copiar los resultados de la búsqueda en un buzón de correo de detección, también puede estimar los resultados de la búsqueda de una búsqueda seleccionada u obtener una vista previa de ellos.
    
      - **Cálculo de resultados de búsqueda**   Esta opción devuelve un cálculo del tamaño y la cantidad totales de elementos que devolverá la búsqueda en función del criterio especificado. Los cálculos se muestran en el panel de detalles en el EAC.
    
      - **Vista previa de los resultados de búsqueda**   Esta opción permite obtener una vista previa de los resultados que proporciona la búsqueda en vez de tener que copiarlos en un buzón de correo de detección para verlos. Esto le permite determinar, rápidamente, si los resultados de la búsqueda son relevantes. Después de obtener una vista previa de los resultados, puede revisar su consulta de búsqueda para restringir los resultados y volver a ejecutar la búsqueda. Los elementos en la vista previa de la página son versiones de solo lectura de los resultados de búsqueda actuales, por lo tanto, no puede realizar movimientos, ediciones, eliminaciones ni reenviar datos en la vista previa de la página.
    
    Para más información, vea [Estimate or preview search results](create-an-in-place-ediscovery-search-exchange-2013-help.md).

