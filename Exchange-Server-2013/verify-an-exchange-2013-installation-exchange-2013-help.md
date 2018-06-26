---
title: 'Comprobar una instalación de Exchange 2013: Exchange 2013 Help'
TOCTitle: Comprobar una instalación de Exchange 2013
ms:assetid: fdd20a2a-c8c1-4d17-b813-3c05d88a4411
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125254(v=EXCHG.150)
ms:contentKeyID: 49116646
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Comprobar una instalación de Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Después de instalar Microsoft Exchange Server 2013, se recomienda comprobar la instalación mediante la ejecución del cmdlet **Get-ExchangeServer** y el análisis del archivo de registro de configuración. Si el proceso de instalación falla o se produce algún error durante la instalación, puede usar el archivo de registro de la instalación para averiguar el origen del problema.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

## Ejecutar Get-ExchangeServer

Para comprobar que Exchange 2013 se ha instalado correctamente, ejecute el cmdlet **Get-ExchangeServer** en el Shell de administración de Exchange. Se muestra una lista de todas las funciones del servidor de Exchange 2013 que se han instalado en el servidor especificado una vez se ejecuta este cmdlet.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Get-ExchangeServer](https://technet.microsoft.com/es-es/library/bb123873\(v=exchg.150\)).

## Analizar el archivo de registro de configuración

También puede saber más acerca de la instalación y la configuración de Exchange 2013 si analiza el archivo de registro de configuración creado durante el proceso de instalación.

Durante la instalación, la configuración de Exchange registra eventos en el registro **Aplicación** del **Visor de eventos** en los equipos que ejecutan Windows Server 2008 R2 con Service Pack 1 (SP1) y Windows Server 2012. Analice el registro **Aplicación** y asegúrese de que no hay mensajes de advertencia o error relacionados con la instalación de Exchange. Estos archivos de registro contienen un historial de cada acción que realiza el sistema durante la instalación de Exchange 2013 y de cualquier error que se haya producido. De manera predeterminada, el método de registro está configurado en `Verbose`. La información está disponible para cada rol de servidor instalado.

Puede encontrar el archivo de registro de instalación en *\<system drive\>*\\ExchangeSetupLogs\\ExchangeSetup.log. La variable *\<system drive\>* representa el directorio raíz de la unidad donde está instalado el sistema operativo.

El archivo de registro de instalación efectúa el seguimiento del progreso de cada tarea que se lleva a cabo durante la instalación y configuración de Exchange 2013. El archivo contiene información sobre el estado de las comprobaciones de requisitos previos y preparación del sistema que se realizan antes del inicio de la instalación, sobre el progreso de la instalación de aplicaciones y sobre los cambios de configuración que se efectúan en el sistema. Compruebe este archivo de registro para ver si las las funciones de servidor se han instalado de la manera esperada.

Se recomienda que inicie el análisis del archivo de registro de instalación mediante la búsqueda de errores. Si encuentra una entrada que indique que se ha producido un error, lea el texto relacionado para determinar la causa del mismo.

