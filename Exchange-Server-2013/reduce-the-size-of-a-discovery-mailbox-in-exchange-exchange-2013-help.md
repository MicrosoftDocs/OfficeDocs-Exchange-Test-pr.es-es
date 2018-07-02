---
title: 'Reducir el tamaño de un buzón de correo de detección en Exchange: Exchange 2013 Help'
TOCTitle: Reducir el tamaño de un buzón de correo de detección en Exchange
ms:assetid: fa762d14-f942-4728-8813-887d11441a68
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn750895(v=EXCHG.150)
ms:contentKeyID: 62371351
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Reducir el tamaño de un buzón de correo de detección en Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

¿Tiene un buzón de correo de detección que ha superado el límite de 50 GB? Para solucionar este problema, puede crear nuevos buzones de correo de detección y copiar en ellos los resultados de la búsqueda del buzón de mayor tamaño.

## ¿Por qué puede interesarme hacer eso?

En Exchange Server 2013 y Exchange Online, el tamaño máximo de los buzones de correo de detección que se usan para almacenar los resultados de la búsqueda de la exhibición de documentos electrónicos local es de 50 GB. Antes de imponerse el límite de tamaño actual, se podía aumentar la cuota de almacenamiento a más de 50 GB, lo que dio lugar a la existencia de buzones de correo de detección que excedían sobradamente los 50 GB. Los buzones de correo de detección mayores de 50 GB presentan tres problemas:

  - No son compatibles.

  - No se pueden migrar a Office 365.

  - En el caso de los buzones de correo de detección de Exchange Server 2010, no pueden actualizarse a Exchange Server 2013.

## El proceso de un vistazo

Aquí puede ver rápidamente todas las acciones que debe realizar para reducir el tamaño de un buzón de correo de detección que ha superado el límite de 50 GB:

1.  Paso 1: Crear buzones de correo de detección buzones de correo de detección adicionales para distribuir los resultados de la búsqueda.

2.  Paso 2: Copiar los resultados de la búsqueda en un buzón de correo de detección los resultados de la búsqueda del buzón de correo de detección existente en uno o varios de los nuevos buzones de correo de detección.

3.  Paso 3: Eliminar búsquedas de la exhibición de documentos electrónicos las búsquedas de la exhibición de documentos electrónicos del buzón de correo de detección original para reducir su tamaño.

La estrategia que se presenta aquí agrupa los resultados de la búsqueda del buzón de correo de detección original en búsquedas independientes de la exhibición de documentos electrónicos basadas en intervalos de fechas. Este procedimiento permite copiar rápidamente muchos resultados de la búsqueda en un nuevo buzón de correo de detección. El gráfico siguiente ilustra este enfoque.

![Reducir el tamaño de un buzón de correo de detección](images/Dn750895.4400df18-c7ed-4c62-b304-f9060ffbdba5(EXCHG.150).gif "Reducir el tamaño de un buzón de correo de detección")

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: el tiempo varía en función de la cantidad y el tamaño de los resultados de la búsqueda que deben copiarse en otros buzones de correo de detección.

  - Para determinar el tamaño de los buzones de correo de detección de la organización, ejecute el comando siguiente.
    
        Get-Mailbox -RecipientTypeDetails DiscoveryMailbox | Get-MailboxStatistics | FL DisplayName,TotalItemSize

  - Determine si necesita mantener algunos o todos los resultados de la búsqueda del buzón de correo de detección que ha superado el límite de 50 GB. Siga los pasos de este tema para copiar los resultados de la búsqueda en otro buzón de correo de detección con el objetivo de conservarlos. Si no desea conservar los resultados de una búsqueda específica de la exhibición de documentos electrónicos, puede eliminar la búsqueda conforme al procedimiento descrito en el paso 3. Cuando se elimina una búsqueda, se eliminan los resultados de la búsqueda del buzón de correo de detección.

  - Si no necesita ninguno de los resultados de la búsqueda del buzón de correo de detección que ha excedido el límite de 50 GB, puede eliminar este buzón. Si se trata del buzón de correo de detección predeterminado que se creó para aprovisionar a la organización de Exchange, puede crearlo de nuevo. Para más información, vea [Eliminar y volver a crear el buzón de correo de detección predeterminado en Exchange](delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md).

  - En casos jurídicos actuales, tal vez desee exportar los resultados de las búsquedas seleccionadas de la exhibición de documentos electrónicos a archivos .pst. De este modo se conservan intactos los resultados de una búsqueda específica. Además de los archivos .pst que contienen los resultados de la búsqueda, también se exporta un registro de resultados de la búsqueda (en formato de archivo .csv) que contiene una entrada por cada mensaje que se devuelve en estos resultados. Las entradas de este archivo identifican los buzones de origen donde se encuentran los mensajes. Para más información, vea [Exportar los resultados de la búsqueda de exhibición de documentos electrónicos a un archivo PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).
    
    Después de exportar los resultados de la búsqueda a archivos .pst, necesitará usar Outlook para importarlos a un nuevo buzón de correo de detección.

## Paso 1: Crear buzones de correo de detección

El primer paso es crear buzones de correo de detección adicionales para poder copiar los resultados de la búsqueda del buzón de correo de detección que ha excedido el límite de tamaño. Partiendo del límite de tamaño de 50 GB para buzones de correo de detección, determine cuántos de estos buzones necesitará y créelos. A continuación, deberá asignar a los usuarios o grupos los permisos necesarios para abrir estos nuevos buzones de correo de detección.

1.  Ejecute el comando siguiente para crear un nuevo buzón de correo de detección.
    
        New-Mailbox -Name <discovery mailbox name> -Discovery

2.  Ejecute el comando siguiente para asignar a un usuario o grupo los permisos para abrir el buzón de correo de detección y ver los resultados de la búsqueda.
    
        Add-MailboxPermission <discovery mailbox name> -User <name of user or group> -AccessRights FullAccess -InheritanceType all

## Paso 2: Copiar los resultados de la búsqueda en un buzón de correo de detección

El paso siguiente permite usar el cmdlet **New-MailboxSearch** para copiar los resultados de la búsqueda del buzón de correo de detección existente en otro nuevo que se ha creado en el paso anterior. Este procedimiento usa los parámetros *StartDate* y *EndDate* para establecer el ámbito de los resultados de la búsqueda en lotes que no superen los 50 GB. Pueden ser necesarias algunas pruebas (mediante la estimación de los resultados de la búsqueda) para asignar el tamaño correcto a estos resultados.

1.  Ejecute el comando siguiente para crear una nueva búsqueda de la exhibición de documentos electrónicos.
    
        New-MailboxSearch -Name "Search results from 2010" -SourceMailboxes "Discovery Search Mailbox" -StartDate "01/01/2010" -EndDate "12/31/2010" -TargetMailbox "Discovery Mailbox Backup 01" -EstimateOnly -StatusMailRecipients admin@contoso.com
    
    Este ejemplo usa los parámetros siguientes:
    
      - *Name*   Este parámetro especifica el nombre de la nueva búsqueda de la exhibición de documentos electrónicos. Dado que el ámbito de la búsqueda se ha determinado en función de las fechas de envío y recepción, resulta útil incluir el intervalo de fechas en el nombre de la búsqueda.
    
      - *SourceMailboxes*   Este parámetro especifica el buzón de correo de detección predeterminado. También puede especificar el nombre de otro buzón de correo de detección que haya excedido el límite de tamaño.
    
      - *StartDate* y *EndDate*   Estos parámetros especifican el intervalo de fechas de los resultados de la búsqueda en el buzón de correo de detección predeterminado para incluirlo en los resultados de la búsqueda.
        

        > [!NOTE]
        > Para las fechas, use el formato de fecha corta (mm/dd/yyyy), incluso en el caso de que la configuración de Opciones regionales del equipo local indique un formato distinto (como dd/mm/yyyy). Por ejemplo, use <STRONG>03/01/2014</STRONG> para especificar el 1 de marzo de 2014.

    
      - *TargetMailbox*   Este parámetro especifica que se deben copiar los resultados de la búsqueda en el buzón de correo de detección denominado "Discovery Mailbox Backup 01".
    
      - *EstimateOnly*   Este modificador especifica que solo se proporciona una estimación del número de elementos que se devolverán cuando se inicia la búsqueda. Si no se incluye este modificador, los mensajes se copiarán en el buzón de destino cuando se inicie la búsqueda. Este modificador permite ajustar los intervalos de fechas si lo considera necesario para aumentar o disminuir el número de resultados de la búsqueda.
    
      - *StatusMailRecipients*   Este parámetro especifica que debe enviarse el mensaje de estado al destinatario especificado.

2.  Tras crear la búsqueda, iníciela desde el Shell o desde el Centro de administración de Exchange (EAC).
    
      - **Desde el Shell:**  ejecute el comando siguiente para iniciar la búsqueda que se ha creado en el paso anterior. Como se incluyó el modificador *EstimateOnly* al crear la búsqueda, los resultados de esta no se copiarán en el buzón de correo de detección de destino.
        
            Start-MailboxSearch "Search results from 2010"
    
      - **Desde el EAC:**  vaya a **Administración de cumplimiento** \> **eDiscovery y retención local**. Seleccione la búsqueda que se ha creado en el paso anterior y haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar") y en **Cálculo de resultados de búsqueda**.

3.  Si lo considera necesario, ajuste el intervalo de fechas para aumentar o disminuir la cantidad de resultados de la búsqueda que se devuelven. Si cambia el intervalo, ejecute la búsqueda de nuevo para obtener una nueva estimación de los resultados. Considere la posibilidad de cambiar el nombre de la búsqueda para que refleje el nuevo intervalo de fechas.

4.  Cuando finalice las pruebas de la búsqueda, copie los resultados de la búsqueda en el buzón de correo de detección de destino desde el Shell o el EAC.
    
      - **Desde el Shell:**  ejecute los comandos siguientes para copiar los resultados de la búsqueda. Antes de hacerlo, debe quitar el modificador *EstimateOnly*.
        
            Set-MailboxSearch "Search results from 2010" -EstimateOnly $false
        
            Start-MailboxSearch "Search results from 2010"
    
      - **Desde el EAC:**  vaya a **Administración de cumplimiento** \> **eDiscovery y retención local**. Seleccione la búsqueda y haga clic en **Buscar**![icono de Buscar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icono de Buscar") y en **Copiar resultados de búsqueda**.
    
    Para más información, vea [Copiar los resultados de la búsqueda de exhibición de documentos electrónicos en un buzón de correo de detección](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

5.  Repita los pasos del 1 al 4 para crear nuevas búsquedas para otros intervalos de fechas. Incluya el intervalo de fechas en el nombre de la nueva búsqueda para indicar el intervalo de los resultados. Para asegurarse de que ninguno de los buzones de correo de detección excede el límite de 50 GB, use varios buzones diferentes como buzón de destino.

## Paso 3: Eliminar búsquedas de la exhibición de documentos electrónicos

Una vez haya copiado los resultados de la búsqueda del buzón de correo de detección original en otro buzón, podrá eliminar las búsquedas originales de la exhibición de documentos electrónicos. Si elimina una búsqueda de este tipo eliminará los resultados de la búsqueda del buzón de correo de detección donde se encuentran almacenados.

Antes de eliminar una búsqueda, puede ejecutar el comando siguiente para identificar el tamaño de los resultados de la búsqueda que se han copiado en un buzón de correo de detección en todas las búsquedas de la organización.

    Get-MailboxSearch | FL Name,TargetMailbox,ResultSizeCopied

Las búsquedas de la exhibición de documentos electrónicos pueden eliminarse desde el Shell o desde el EAC.

  - **Desde el Shell:**  ejecute el comando siguiente.
    
        Remove-MailboxSearch -Identity <name of search>

  - **Desde el EAC:**  vaya a **Administración de cumplimiento** \> **eDiscovery y retención local**. Seleccione la búsqueda que desea eliminar y haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

## ¿Cómo puedo saber si el proceso se ha completado correctamente?

Tras eliminar las búsquedas de la exhibición de documentos electrónicos para quitar los resultados del buzón de correo de detección donde se encontraban almacenados, ejecute el comando siguiente para mostrar el tamaño de un buzón seleccionado.

    Get-Mailbox <name of discovery mailbox> | Get-MailboxStatistics | FL TotalItemSize

