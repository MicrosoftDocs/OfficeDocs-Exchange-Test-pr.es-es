---
title: 'Grupo métricas y sugerencias de correo electrónico: Exchange 2013 Help'
TOCTitle: Grupo métricas y sugerencias de correo electrónico
ms:assetid: 74a55072-4ba9-45bb-a18f-41afbf3de30b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ674302(v=EXCHG.150)
ms:contentKeyID: 49895717
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Grupo métricas y sugerencias de correo electrónico

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-16_

Métricas de grupo es la recopilación de los siguientes datos sobre grupos de distribución y grupos de distribución dinámica en la organización:

  - Número de miembros

  - Número de miembros que no pertenecen a su organización

Los datos de métricas de grupo se usan para admitir información sobre correo en Microsoft Exchange Server 2013. Las sugerencias de correo electrónico son mensajes informativos que se muestran a los remitentes cuando redactan mensajes. Para obtener más información acerca de las sugerencias de correo electrónico, incluida una lista completa de sugerencias disponibles en Exchange 2013, consulte [MailTips](mailtips-exchange-2013-help.md).

Las siguientes sugerencias de correo electrónico utilizan datos de métricas de grupo:

  - **Gran audiencia**   Esta sugerencia de correo electrónico se visualiza cuando un remitente agrega un grupo de distribución cuya cantidad de miembros se considera una gran audiencia, según la configuración de la organización. De forma predeterminada, cualquier mensaje dirigido a más de 25 destinatarios se considera una gran audiencia.

  - **Destinatarios externos**   Esta sugerencia de correo electrónico se visualiza cuando un remitente agrega un grupo de distribución que tiene miembros que no pertenecen a la organización.

Las sugerencias de correo electrónico se evalúan cada vez que un remitente añade un destinatario a un mensajes. Para proporcionar estos datos, Exchange calcula los datos de métricas de grupo como proceso de fondo en segundo plano que puede planificarse para que su ejecución se realice fuera del horario laboral habitual de la organización. Al evaluar a los destinatarios para proporcionar sugerencias de correo electrónico, Exchange lee los datos de métricas de grupo.

## Generación de métricas de grupo

En Exchange 2013, los datos de métricas de grupo se almacenan en los atributos **msExchGroupMemberCount** y **msExchGroupExternalMemberCount** del objeto de grupo de Active Directory. Los siguientes archivos de la carpeta %ExchangeInstallPath%GroupMetrics también están asociados a las métricas de grupo:

  - **Cookie\_*\<nnnnnnnn\>*.dsc**   Este archivo de texto incluye información sobre el servidor de buzones de correo que está configurado para generar datos de métricas de grupo, así como la última hora en que se generaron correctamente las métricas de grupo. Esto permite que las métricas de grupo generen datos para los grupos modificados desde la última generación.

  - **ChangedGroups.txt**   Este archivo contiene la lista de grupos que se actualizaron la última vez que se generaron los datos de métricas de grupo.

La generación de métricas de grupo se lleva a cabo a través de un buzón de correo de arbitraje, que también se denomina "buzón de correo de organización". Cuando el parámetro *GMGen* de un buzón de arbitraje está establecido en `$true`, éste es el responsable de la generación de datos de métricas de grupo.

La primera vez que se ejecutan el asistente del buzón de correo Métricas de grupo, el servidor de buzones de correo genera datos completos de métricas de grupo para todos los grupos de distribución y grupos de distribución dinámica, así como también actualizaciones incrementales para cualquier grupo modificado después de la última generación completa. De forma predeterminada, los datos de métricas de grupo se generan diariamente en momentos aleatorios cuando la carga del servidor de Exchange es baja. En caso de que la carga esté constantemente a niveles altos, es posible que la generación de métricas de grupo no se realice.

Para configurar la generación de métricas de grupo, consulte [Configurar métricas de grupo](configure-group-metrics-exchange-2013-help.md).

