---
title: 'Registros de IIS e informes de Log Parser Studio: Exchange 2013 Help'
TOCTitle: Registros de IIS e informes de Log Parser Studio
ms:assetid: 01fa67d4-dc02-4c5f-93af-6da7b97d282f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn904092(v=EXCHG.150)
ms:contentKeyID: 63910972
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Registros de IIS e informes de Log Parser Studio

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

## Análisis de los informes de Log Parser Studio

Log Parser Studio es una utilidad que permite buscar y crear informes a partir de varios tipos de archivos de registro, incluidos los de Internet Information Services (IIS). Se basa en Log Parser 2.2 y tiene una interfaz de usuario completa que facilita la creación y administración de consultas SQL relacionadas.

[Descargue Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524244) y, después, lea la entrada de blog de [introducción a Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524243).

Recuerde que, en Exchange 2013, todo el tráfico tiene que ir a través de IIS. Esto significa que analizar los registros de IIS es la mejor manera de obtener una visión completa del número de conexiones que llegan a un servidor, información específica del protocolo acerca de las conexiones y los usuarios que más afectan al rendimiento. Se han desarrollado más de veinte nuevos informes para Log Parser Studio con el fin de solucionar problemas de rendimiento de Exchange 2013.

## Informes de Log Parser Studio para problemas de rendimiento de Exchange 2013

Para obtener una descripción detallada de la carga global de su entorno de Exchange 2013, use los siguientes informes y compare las cifras con cada servidor.

[Aquí puede descargar](https://go.microsoft.com/fwlink/p/?linkid=524245) un archivo .zip que contiene los informes de Log Parser Studio mencionados además de otros informes para la resolución de problemas.

  - **IIS: Solicitudes por hora**. Utilice registros de IIS del sitio web predeterminado (directorio W3SVC1) o del sitio web back-end (directorio W3SVC2), pero no de ambos al mismo tiempo.

  - **ACTIVESYNC\_WP: Clientes por porcentaje**. Calcula todas las solicitudes de ActiveSync desglosadas por agente de usuario y por el porcentaje de cada cliente sobre el número total de solicitudes.

  - **ACTIVESYNC\_WP: solicitudes por hora (CSV)**. Enumera las solicitudes de ActiveSync por hora y envía los resultados a un archivo CSV.

  - **ACTIVESYNC\_WP: solicitudes por usuario (CSV)**. Enumera las solicitudes de ActiveSync por usuario y envía los resultados a un archivo CSV.

  - **ACTIVESYNC\_WP: solicitudes por usuario (primeros 10.000)**. Enumera las solicitudes de ActiveSync por usuario para los primeros 10.000 usuarios.

  - **ACTIVESYNC\_WP: principales clientes (CSV)**. Enumera los clientes de ActiveSync de mayor a menor número de solicitudes y envía el resultado a un archivo CSV.

  - **EWS\_WP: clientes por porcentaje**. Calcula todas las solicitudes de EWS desglosadas por agente de usuario y por el porcentaje de cada cliente sobre el número total de solicitudes.

  - **EWS\_WP: solicitudes por hora (CSV)**. Indica el número total de solicitudes de EWS por hora.

  - **EWS\_WP: solicitudes por usuario (CSV)**. Enumera las solicitudes de EWS por usuario y envía los resultados a un archivo CSV.

  - **EWS\_WP: solicitudes por usuario (primeros 10.000)**. Enumera las solicitudes de EWS por usuario para los primeros 10.000 usuarios.

  - **EWS\_WP: principales clientes (CSV)**. Enumera los principales clientes de EWS, de mayor a menor número de solicitudes.

  - **OLA\_WP: errores por usuario, por hora, por día**. Usuarios de Outlook en cualquier lugar por número de solicitudes.

  - **OLA\_WP: solicitudes por hora**. Enumera las solicitudes de Outlook en cualquier lugar por hora.

  - **OLA\_WP: Solicitudes por hora, por usuario**. Enumera las solicitudes de Outlook en cualquier lugar por hora, por usuario.

  - **OLA\_WP: solicitudes por usuario (CSV)**. Enumera las solicitudes de Outlook en cualquier lugar por usuario.

  - **OLA\_WP: solicitudes por usuario (primeros 10.000)**. Enumera las solicitudes de Outlook en cualquier lugar por usuario para los primeros 10.000 usuarios.

  - **OLA\_WP: principales clientes**. Enumera los principales clientes de Outlook en cualquier lugar, de mayor a menor número de solicitudes.

  - **OWA\_WP: clientes por porcentaje**. Calcula todas las solicitudes de OWA desglosadas por agente de usuario y por el porcentaje de cada cliente sobre el número total de solicitudes.

  - **OWA\_WP: solicitudes por hora (CSV)**. Enumera las solicitudes de OWA por hora y envía los resultados a un archivo CSV.

  - **OWA\_WP: solicitudes por usuario (CSV)**. Enumera las solicitudes de OWA por usuario y envía los resultados a un archivo CSV.

  - **OWA\_WP: solicitudes por usuario (primeros 10.000)**. Enumera las solicitudes de OWA por usuario para los primeros 10.000 usuarios.

  - **OWA\_WP: principales clientes (CSV)**. Enumera los clientes de OWA de mayor a menor número de solicitudes y envía el resultado a un archivo CSV.

