---
title: Solución de problemas del conjunto de mantenimiento SiteMailbox
TOCTitle: Solución de problemas del conjunto de mantenimiento SiteMailbox
ms:assetid: ac00985c-c9a5-44bf-b152-4b99d8ae24ed
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.scom.sitemailbox(v=EXCHG.150)
ms:contentKeyID: 53181918
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solución de problemas del conjunto de mantenimiento SiteMailbox

 

_**Se aplica a:**Exchange Server 2013, Project Server 2013_

_**Última modificación del tema:**2013-02-11_

El conjunto de mantenimiento SiteMailbox supervisa el mantenimiento general y la accesibilidad de los buzones de correo del sitio de su organización.

Si recibe una alerta que especifique que el estado de SiteMailbox no es correcto, esto indica que el contenido del buzón de correo de un usuario no está sincronizado.

## Explicación

El sistema de supervisión de SiteMailbox recibe resultados de sincronización pasiva del servicio de sincronización en segundo plano. Este sistema no utiliza ninguna sonda. Los resultados de sincronización pasiva se escriben en el sistema de supervisión de SiteMailbox después de cada intento de sincronización. Las sincronizaciones también se activan cuando se producen los eventos siguientes:

  - Los usuarios acceden a sus buzones de correo del sitio mediante Outlook o Outlook Web App

  - Se ejecuta el comando **Update-SiteMailbox**

  - Se abre la ventana Opciones de Outlook Web App y se hace clic en el botón **Iniciar sincronización** de la página **Estado de sincronización** para el buzón de correo del sitio seleccionado

Para obtener más información acerca del cmdlet Update-SiteMailbox, consulte: [Update-SiteMailbox](https://technet.microsoft.com/es-es/library/jj218690\(v=exchg.150\))

Para obtener más información acerca de monitores y sondas, consulte [Rendimiento y mantenimiento del servidor](https://technet.microsoft.com/es-es/library/jj150551\(v=exchg.150\)).

## Problemas comunes

Por lo general, el servicio de supervisión de la sincronización activa una alerta cuando se producen problemas de sincronización que se propagan a todo el sitio. No se envía una alerta cuando falla la sincronización de un solo buzón de correo del sitio. Para determinar la causa de una alerta de umbral excedido para un solo buzón de correo del sitio, se recomienda analizar los archivos de registro de sincronización de buzones de correo del sitio.

## Acción del usuario

Es posible que el servicio se haya recuperado después de emitir la alerta. Por lo tanto, cuando reciba una alerta que especifica que el conjunto de mantenimiento es incorrecto, primero compruebe que el problema aún exista. Si el problema existe, lleve a cabo las acciones de recuperación apropiadas que se describen en las siguientes secciones.

## Comprobar que el problema aún persiste

1.  Identifique el nombre del conjunto de mantenimiento y el nombre del servidor en la alerta.

2.  Los detalles del mensaje proporcionan información sobre la causa exacta de la alerta. En la mayoría de los casos, los detalles del mensaje proporcionan la suficiente información de solución de problemas para identificar la raíz del problema. Si los detalles del mensaje no son claros, haga lo siguiente:
    
    1.  Abra Shell de administración de Exchange y, luego, ejecute el siguiente comando para recuperar los detalles del conjunto de mantenimiento que emitió la alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por ejemplo, para recuperar los detalles del conjunto de mantenimiento SiteMailbox sobre server1.contoso.com, ejecute el siguiente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "SiteMailbox"}
    
    2.  Revise el resultado del comando para determinar qué monitor informó sobre el error. El valor **AlertValue** para el monitor que emitió la alerta será `Unhealthy`.

## Pasos para la solución de problemas

Cuando recibe una alerta de un conjunto de mantenimiento, el mensaje de correo electrónico contiene la siguiente información:

  - Nombre del servidor que envió la alerta

  - Fecha y hora cuando ocurrió la alerta

  - Mecanismo de autenticación utilizado e información de credenciales

  - Seguimiento de excepción completo del último error, incluidos datos de diagnóstico e información específica de encabezado HTTP  
    
    **Nota**   Puede utilizar la información en el seguimiento de excepción completo para ayudar a resolver el problema. La excepción generada por la sonda contiene un motivo de error que describe por qué la sonda falló.

**Errores de sincronización en segundo plano**

Cuando falla el proceso de sincronización en segundo plano, es posible que reciba una alerta semejante a la siguiente:

La sincronización en segundo plano del buzón de correo del sitio está fallando al menos un 25 %: 41 fallas en 87 intentos. Ejemplo de resultado de sincronización:

\[Mensaje: El servidor remoto devolvió un error: (401) No autorizado.\]\[Tipo: System.Net.WebException\]

Esta alerta se activa cuando ocurre un porcentaje regularmente alto de fallas de sincronización durante las cuatro horas anteriores. Para evitar falsos negativos, una alerta se envía solamente cuando se cumplen las siguientes condiciones en un período de 15 minutos durante las cuatro horas anteriores:

  - Al menos 20 fallas ocurren en un intervalo de 15 minutos.

  - El porcentaje de fallas excede el 25 % en comparación con el total de intentos en un intervalo de 15 minutos.

Todos los buzones de correo del sitio de Exchange están vinculados a un sitio de SharePoint. Para cada uno de los buzones de correo del sitio en un servidor Exchange determinado que hospeda el rol de Buzón de correo, el servidor sincroniza la información relacionada con el buzón de correo del sitio de SharePoint.

Durante este proceso, ocurren dos tipos de sincronización: sincronización de pertenencia y sincronización de documentos. Los metadatos para estos procesos de sincronización se originan en distintos servicios web. Además, un servidor Exchange puede contener buzones de correo del sitio que estén vinculados a varios servidores o granjas de SharePoint. Por lo tanto, la alerta puede originarse en varios servidores Buzón de correo según las siguientes condiciones:

1.  La manera en que se distribuyen los buzones de correo del sitio utilizados activamente en la organización

2.  Los servidores SharePoint a los que están vinculados los buzones de correo del sitio utilizados activamente

3.  Si el servidor de buzones de correo tiene suficiente volumen de sincronización para cumplir con los umbrales de alerta

Para solucionar este problema, el ejemplo de resultado de sincronización de la alerta puede ayudar a determinar la causa de la falla. Los detalles acerca del resultado correcto o el error de cada intento de sincronización se registra en la carpeta *\<exExchangeSvrNoVersion installation directory\>*Logging\\TeamMailbox. Revise los archivos Microsoft.Exchange.ServiceHost\_TeamMailboxSyncLog\* más recientes para identificar errores buscando el término **failed**. También puede usar los cmdlets **Test-OAuthConnectivity**, **Test-SiteMailbox** y **Get-SiteMailboxDiagnostics** para continuar con la solución de problemas.

**El servicio MSExchangeServiceHost no se está ejecutando**

Si el servicio MSExchangeServiceHost no se está ejecutando, recibirá una alerta similar a la siguiente:

El servicio 'MSExchangeServiceHost' no se está ejecutando después de los intentos de recuperación. Es posible que el servicio esté deshabilitado o en un bucle de bloqueo.

Para solucionar este problema, compruebe que el servicio MSExchangeServiceHost se esté ejecutando en el servidor que envió la alerta. Si el servicio se está ejecutando, revise los registros de eventos de Windows para buscar indicaciones del motivo por el que quizás el servicio no se estaba ejecutando antes, por ejemplo, control manual del servicio o bloqueos repetidos en el servicio.

**El servicio MSExchangeServiceHost se ha bloqueado**

Si el servicio MSExchangeServiceHost se bloquea, recibirá una alerta similar a la siguiente:

El proceso MSExchangeServiceHost se bloqueó al menos tres veces en los últimos 60 minutos.  
Mensaje de Watson:

\<*Mensaje*\>

Para solucionar este problema, revise el registro de eventos de aplicaciones de Windows en el servidor que envió la alerta para los eventos **4999** relacionados con el servicio MSExchangeServiceHost. El texto de los detalles puede proporcionar información sobre la causa del problema.

## Para obtener más información

[Novedades en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150540\(v=exchg.150\))

[Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\))

