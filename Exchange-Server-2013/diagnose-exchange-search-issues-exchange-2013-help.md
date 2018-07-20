---
title: 'Diagnosticar problemas del servicio de búsqueda de Exchange: Exchange 2013 Help'
TOCTitle: Diagnosticar problemas del servicio de búsqueda de Exchange
ms:assetid: 8cfa26f4-ccf0-42dd-8570-67018188b4e8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123701(v=EXCHG.150)
ms:contentKeyID: 52062043
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Diagnosticar problemas del servicio de búsqueda de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

El servicio de búsqueda de Exchange indexa los buzones de correo y los datos adjuntos compatibles en los buzones de correo de Exchange. Debido al aumento en los volúmenes de correo electrónico, los tamaños de los buzones y las cuotas de almacenamiento cada vez más grandes, el aprovisionamiento de buzones de archivo para los usuarios y la exhibición de documentos electrónicos local para realizar búsquedas de detección, el servicio de búsqueda de Exchange es un componente fundamental de los servidores de buzones de correo en su organización de Microsoft Exchange Server 2013. Los problemas con el servicio de búsqueda de Exchange pueden afectar a la productividad del usuario y tener impacto en la funcionalidad de Exhibición de documentos electrónicos local.

Para más información sobre el servicio de búsqueda de Exchange, vea [Búsqueda de Exchange](exchange-search-exchange-2013-help.md).

¿Está buscando tareas de administración relacionadas con la administración del servicio de búsqueda de Exchange? Vea [Procedimientos de búsqueda de Exchange](exchange-search-procedures-exchange-2013-help.md).

## Uso del cmdlet Test-ExchangeSearch

En el paso 5 del procedimiento incluido en este tema se describe la ejecución del cmdlet **Test-ExchangeSearch** para diagnosticar problemas en el servicio de búsqueda de Exchange. Puede usar el cmdlet **Test-ExchangeSearch** para probar la funcionalidad del servicio de búsqueda de Exchange con un servidor de buzones de correo, una base de datos de buzones de correo o un buzón de correo específico. El cmdlet entrega un mensaje de prueba al buzón de correo especificado (o al buzón de correo del sistema de una base de datos si no hay especificado un buzón de correo) y luego ejecuta una búsqueda a fin de determinar si el mensaje está indexado e incluso el tiempo que tarda en indexarse. En circunstancias normales, el servicio de búsqueda de Exchange indexa un mensaje dentro de los 10 segundos posteriores a la creación del mensaje o a la entrega al buzón de correo. El mensaje de prueba se elimina automáticamente después de la prueba.

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [Test-ExchangeSearch](https://technet.microsoft.com/es-es/library/bb124733\(v=exchg.150\)).

## Recuperación de elementos no aptos para la búsqueda

Puede usar el cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/es-es/library/dd351154\(v=exchg.150\)) para recuperar una lista de elementos del buzón de correo no aptos para la búsqueda que el servicio de búsqueda de Exchange no pudo indexar correctamente. Puede ejecutar el cmdlet en un servidor de buzones de correo, una base de datos de buzones de correo o un buzón específico. El cmdlet devuelve detalles sobre cada elemento que no se pudo buscar. Hay varias razones por las que no se puede buscar un elemento del buzón de correo. Por ejemplo, un mensaje de correo electrónico puede contener un tipo de archivo adjunto que no se puede indizar para la búsqueda o no hay ningún filtro de búsqueda instalado o habilitado. Si hay un filtro de búsqueda para ese tipo de archivo, puede instalarlo en los servidores de exExchangeNoVersionExchange.


> [!IMPORTANT]
> Los filtros de búsqueda proporcionados por Microsoft son probados y admitidos por Microsoft. Se recomienda probar los filtros de búsqueda de terceros en un entorno de prueba antes de instalarlos en los servidores de exExchangeNoVersionExchange en un entorno de producción.



Para obtener más información acerca de los elementos no aptos para la búsqueda, vea:

  - [Formatos de archivo indizados por la búsqueda de Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

## Diagnosticar problemas del servicio de búsqueda de Exchange

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada sobre el servicio de búsqueda de Exchange en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

1.  **Comprobar estado del servicio**   ¿Se inició el servicio de búsqueda de Exchange (MSExchangeFastSearch) en el servidor de buzones de correo? En caso afirmativo, vaya al paso 2. En caso contrario, use el complemento Servicios de MMC para comprobar que el servicio MSExchangeFastSearch se esté ejecutando de la siguiente manera:
    
    1.  Haga clic en **Inicio**, elija **Herramientas administrativas** y, a continuación, haga clic en **Servicios**.
    
    2.  En **Servicios**, compruebe que el **Estado** del servicio de **búsqueda de Microsoft Exchange** aparezca como **Iniciado**.

2.  **Comprobar la configuración de la base de datos de buzones de correo**   ¿El parámetro *IndexEnabled* está configurado como verdadero para la base de datos de buzones de correo del usuario? En caso afirmativo, vaya al paso 3. En caso contrario, ejecute el siguiente comando en el Shell para comprobar que la marca *IndexEnabled* esté configurada como verdadera.
    
        Get-MailboxDatabase | Format-Table Name,IndexEnabled
    
    Para obtener información detallada acerca de la sintaxis y los parámetros, vea [Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\)).

3.  **Comprobar el estado de rastreo de la base de datos de buzones de correo**   ¿Se ha rastreado la base de datos de Exchange? En caso afirmativo, vaya al paso 4. De lo contrario, use el Monitor de confiabilidad y rendimiento para comprobar el contador de **Rastreador de datos: buzones restantes** del objeto de rendimiento **Índices de búsqueda de MSExchange**. Realice los siguientes pasos:
    
    1.  abra el **Monitor de rendimiento** (perfmon.exe).
    
    2.  En el árbol de consola, en **Herramientas de supervisión**, haga clic en **Monitor de rendimiento**.
    
    3.  En el panel Monitor de rendimiento, haga clic en **Agregar** (signo más de color verde).
    
    4.  En **Agregar contadores**, en la lista **Seleccionar contadores del equipo**, seleccione el servidor en el que se ubica la base de datos de buzones de correo que desea supervisar.
    
    5.  En el cuadro sin etiqueta que está debajo de la lista **Seleccionar contadores del equipo**, seleccione el objeto de rendimiento **Índices de búsqueda de MSExchange**.
    
    6.  En el cuadro **Instancias del objeto seleccionado**, seleccione la instancia de la base de datos de buzones de correo del usuario.
    
    7.  Haga clic en **Agregar** y, a continuación, en **Aceptar**.
        
        En el panel Monitor de rendimiento, el objeto de rendimiento **Índices de búsqueda de MSExchange** aparece en la columna **Objeto** y los distintos contadores se enumeran en la columna **Contador**.
    
    8.  Vea el contador **Rastreador de datos: buzones restantes**. Cualquier valor igual o superior a 1 indica que los buzones de correo de la base de datos aún se están rastreando. Cuando finaliza el rastreo, el valor es **0**.
    
    Para obtener información acerca de cómo usar el Monitor de rendimiento, vea [Guía paso a paso para la supervisión del rendimiento y la confiabilidad en Windows Server 2008](https://go.microsoft.com/fwlink/p/?linkid=178005)

4.  **Comprobar el estado de indización de la copia de base de datos** ¿El estado del índice de contenido es correcto? Use el cmdlet **Get-MailboxDatabaseCopyStatus** para comprobar el estado de indización del contenido de una copia de base de datos.
    
        Get-MailboxDatabaseCopyStatus -Server $env:ComputerName | Format-Table Name,Status,ContentIndex* -Auto
    
    Para obtener información detallada acerca de la sintaxis y los parámetros, vea [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/es-es/library/dd298044\(v=exchg.150\)).

5.  **Ejecutar el cmdlet Test-ExchangeSearch**   Si ya se ha rastreado la base de datos de buzones de correo, puede ejecutar el cmdlet **Test-ExchangeSearch** para la base de datos de buzones de correo o para un buzón específico.
    
        Test-ExchangeSearch -Identity AlanBrewer@contoso.com
    
    Para obtener información detallada acerca de la sintaxis y los parámetros, vea [Test-ExchangeSearch](https://technet.microsoft.com/es-es/library/bb124733\(v=exchg.150\)).

6.  **Comprobar el registro de eventos de la aplicación**   Mediante el visor de eventos o el Shell, compruebe el registro de eventos de la aplicación en busca de mensajes de error relacionados con la búsqueda. Busque los siguientes orígenes de eventos.
    
      - **MSExchangeFastSearch**
    
      - **MSExchangeIS**
    
    Para obtener más información, haga clic en el vínculo incluido en la entrada del registro de eventos.

7.  **Reiniciar el servicio de búsqueda de Microsoft Exchange**   Use el complemento MMC de servicios o la Shell para detener y luego reiniciar el servicio de búsqueda de MicrosoftExchange (MSExchangeFastSearch):
    
    1.  Haga clic en **Inicio**, apunte **Herramientas administrativas** y luego haga clic en **Servicios**.
    
    2.  En **Servicios**, haga clic con el botón derecho en **Búsqueda de Microsoft Exchange** y luego haga clic en **Detener**. Una vez detenido el servicio, haga clic con el botón secundario en el servicio y, a continuación, elija **Iniciar**.

8.  **Reinicializar el catálogo de búsqueda**   En algunos casos, por ejemplo, cuando el catálogo de búsqueda está dañado, es posible que deba reinicializarlo. Cuando un catálogo de búsqueda debe reinicializarse, el servicio de búsqueda de Exchange le notifica las entradas de registro en el registro de eventos de la aplicación. Para obtener más información acerca de la reinicialización del catálogo de búsqueda, vea [Reinicializar el catálogo de búsqueda](reseed-the-search-catalog-exchange-2013-help.md).

