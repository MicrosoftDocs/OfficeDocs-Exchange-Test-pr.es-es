---
title: Introducción al módulo de administración de Exchange Server 2013
TOCTitle: Introducción al módulo de administración de Exchange Server 2013
ms:assetid: 72d1609f-ab32-44d8-aa40-b1de587442d2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn195908(v=EXCHG.150)
ms:contentKeyID: 53181934
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Introducción al módulo de administración de Exchange Server 2013

 

_**Última modificación del tema:** 2013-04-08_

El módulo de administración de Exchange Server 2013 agrega un contenedor a la sección **Supervisión** de la consola SCOM. Cuando expande el contenedor de Exchange Server 2013, puede ver que solo hay tres vistas debajo del contenedor.

![Contenedores del módulo de administración de Exchange 2013](images/Dn195908.253b4ec5-2103-4b0c-a22e-5ebd24d08600(EXCHG.150).png "Contenedores del módulo de administración de Exchange 2013")

## Alertas activas: ¿hay algún problema con Exchange?

La vista **Alertas activas** muestra todas las alertas generadas y activas en la organización de Exchange. Puede hacer clic en cualquier alerta para ver más información en el panel de detalles. Esta vista básicamente le proporciona una respuesta afirmativa o negativa a la pregunta "¿hay algún problema con mi implementación de Exchange?" Cada alerta corresponde a uno o más problemas para un conjunto de mantenimiento particular. Además, según el problema particular, se puede generar más de una alerta.

## Estado de la organización: ¿cuál es el impacto?

Si ve una alerta en la vista Alertas activas, lo primero que debe hacer es consultar la vista **Estado de la organización**. Esta es la primera fuente de información para el estado general de la organización. Le informa específicamente qué se ve afectado en la organización, como grupos de disponibilidad de base de datos y sitios de Active Directory.

![Mantenimiento de la organización](images/Dn195908.603c920b-7b88-4956-87d9-09d93fa6cba3(EXCHG.150).png "Mantenimiento de la organización")

## Estado del servidor: ¿los problemas de qué servidor debo solucionar?

La vista **Estado del servidor** proporciona detalles sobre servidores individuales en la organización. Aquí puede ver el estado individual de todos los servidores. Con esta vista, puede reducir cualquier problema a un servidor particular.

![Estado del servidor](images/Dn195913.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "Estado del servidor")

## Supervisión de categorías

Mientras recorre las tres vistas del panel de Exchange Server 2013, puede haber observado que, además de la columna **Estado**, tiene cuatro indicadores adicionales de estado.

![Intercambiar indicadores de mantenimiento](images/Dn195908.dd10ed0b-abe5-41aa-8d43-b4fb10133984(EXCHG.150).png "Intercambiar indicadores de mantenimiento")

Cada uno de estos indicadores de estado le proporciona información general de aspectos específicos de la implementación de Exchange.

  - **Puntos táctiles de los clientes** Muestra lo que están experimentando los usuarios. Si este indicador es correcto, significa que el problema posiblemente no esté afectando sus usuarios. Por ejemplo, supongamos que un miembro DAG está teniendo problemas, pero la base de datos realizó correctamente una conmutación por error. En este caso, verá indicadores incorrectos para ese DAG particular, pero el indicador de puntos táctiles de los clientes aparecerá como correcto porque los usuarios no están experimentando ninguna interrupción de servicio.

  - **Componentes del servicio** Esto muestra el estado del servicio particular asociado con el componente. Por ejemplo, el indicador de componente de servicio para OWA indica si el servicio OWA general está correcto.

  - **Recursos de servidor** Muestra el estado de recursos físicos que afectan la funcionalidad de un servidor.

  - **Dependencias clave** Muestra el estado de los recursos externos de los cuales Exchange depende. Por ejemplo, conectividad de red, DNS o Active Directory.

Las vistas del módulo de administración de Exchange Server 2013 proporcionan una visualización simple, pero eficaz, que permite determinar fácil y rápidamente que la organización está correcta. Sin embargo, las vistas también están estructuradas de manera que lo puedan guiar rápidamente hacia la raíz del problema en caso de alerta. Consulte [Usar el módulo de administración de Exchange Server 2013 para solucionar problemas](using-the-exchange-server-2013-management-pack-for-troubleshooting.md) para obtener más información sobre el uso del módulo de administración de Exchange Server 2013 para resolver problemas.

