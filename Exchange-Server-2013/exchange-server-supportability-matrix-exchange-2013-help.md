---
title: 'Exchange Server Supportability Matrix: Exchange 2013 Help'
TOCTitle: Exchange Server Supportability Matrix
ms:assetid: dbac2d40-da8b-469f-a265-1d1f948fe446
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff728623(v=EXCHG.150)
ms:contentKeyID: 54652452
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server Supportability Matrix

 

_**Se aplica a:**Exchange Server 2007, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2018-03-20_

La Matriz de compatibilidad de Exchange Server proporciona un origen centralizado para que los administradores de Microsoft Exchange encuentren fácilmente información sobre el nivel de compatibilidad disponible para cualquier configuración o sobre cualquier componente necesario en las versiones compatibles de Microsoft Exchange.

## Modelo de versiones

La siguiente tabla identifica el modelo de versiones de cada versión compatible de Exchange. El modelo de versión se identifica con el carácter X.

En las versiones de Exchange anteriores a Exchange 2013, cada paquete acumulativo de actualizaciones es acumulativo con respecto al producto completo. Por lo tanto, si se aplica un paquete acumulativo de actualizaciones a Exchange Server 2010, se aplicarán todas las revisiones que contenga ese paquete acumulativo de actualizaciones. es decir, todas las revisiones que contenían todos los paquetes anteriores. Cuando se crea una actualización o una revisión de versiones anteriores de Exchange, uno o varios de los archivos binarios que se incluyen son acumulativos. en lo que respecta al contenido de los archivos, pero no en cuanto al producto Exchange completo. Para más información, vea [Servicio de actualización de Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=298627).

Con Exchange 2013, cambiamos nuestra forma de entregar las revisiones y los Service Pack. En lugar de seguir el modelo de paquetes acumulativos de actualizaciones y versiones de revisión basadas en prioridades que se usaba en las versiones anteriores de Exchange, Exchange 2013 y versiones posteriores se adhieren ahora a un modelo de entregas programadas. En este modelo, las actualizaciones acumulativas se publican cada tres meses. Las actualizaciones acumulativas (CU) para Exchange 2013 y versiones posteriores se lanzan como actualizaciones completas de esa versión de Exchange, similares a una actualización de un producto o una versión de Service Pack. Para obtener más información, vea [Actualizaciones para Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Servicios del modelo de versión</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Actualizaciones acumulativas</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Paquetes acumulativos de actualizaciones</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Las revisiones de seguridad se entregan por separado</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## Ciclo de vida de soporte técnico

Para obtener más información sobre el ciclo de vida de soporte técnico de una versión específica de Exchange o de los sistemas operativos de cliente o servidor MicrosoftWindows, consulte la página [Ciclo de vida de soporte técnico de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=55839). Para obtener más información acerca del ciclo de vida de soporte técnico de Microsoft, vea [Preguntas más frecuentes sobre la directiva Ciclo de vida de soporte técnico de Microsoft](https://go.microsoft.com/fwlink/?linkid=158902).

## Final de ciclo de vida de Exchange Server 2007

El 11 de abril de 2017 finalizó el soporte técnico de Exchange 2007, de acuerdo con la [Directiva de ciclos de vida de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=833210). Se recuerda que, tras esa fecha, no se publicarán nuevas actualizaciones de seguridad ni de otro tipo, así como tampoco habrá opciones de soporte técnico de pago o gratuito, ni se actualizará el contenido técnico en línea. Además, dada la rápida adopción de Office 365 y el incremento en el uso de la nube, las opciones de soporte personalizado para productos de Office no estarán disponibles. Esto incluye Exchange Server, así como los conjuntos de aplicaciones Office, SharePoint Server, Office Communications Server, Lync Server, Skype Empresarial Server, Project Server y Visio. Después de alcanzarse la fecha de finalización de soporte técnico para Exchange 2007, animamos a los clientes a que completen sus planes de migración y actualización. Recomendamos que los clientes aprovechen los beneficios de implementación ofrecidos por Microsoft y Microsoft Certified Partners, tales como [Microsoft FastTrack](https://go.microsoft.com/fwlink/p/?linkid=238431) para migraciones a la nube y los [Servicios de implementación y planeación de Software Assurance](https://go.microsoft.com/fwlink/p/?linkid=833211) para actualizaciones locales.

## Plataformas de sistema operativo admitidas

En la tabla siguiente se identifican las plataformas de sistema operativo en las que se puede ejecutar cada versión de Exchange. Las plataformas compatibles se identifican con un símbolo X.


> [!IMPORTANT]
> No se admiten las versiones del cliente de Windows y de Windows Server que no figuren en la siguiente tabla para su uso con cualquier versión de Exchange.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Plataforma de sistema operativo</th>
<th>Exchange 2016 CU3 y versiones posteriores</th>
<th>Exchange 2016 CU2 y versiones anteriores</th>
<th>Exchange 2013 SP1 y posterior</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Vista SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows 7 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="odd">
<td><p>Windows 8</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows 8.1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Windows 10</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


1Solo para las herramientas de administración de Exchange

## Entornos de Active Directory admitidos

En la tabla siguiente se identifican los entornos de Active Directory con los que se puede comunicar cada versión de Exchange. Los entornos compatibles se identifican con una X. Un servidor de Active Directory hace referencia tanto a servidores de catálogo global modificables como a controladores de dominio modificables. No se admiten servidores de catálogo global ni controladores de dominio que sean de solo lectura.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Entorno de sistema operativo</th>
<th>Exchange 2016 CU3 y versiones posteriores</th>
<th>Exchange 2016 CU2 y versiones anteriores</th>
<th>Exchange 2013 SP1 y posterior</th>
<th>Paquete acumulativo de actualizaciones 5 para Exchange 2010 SP3 o posterior</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de Active Directory con Windows Server 2003 SP2</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Active Directory con Windows Server 2008 SP2</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Active Directory con Windows Server 2008 R2 SP1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Active Directory de Windows Server 2012</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Active Directory de Windows Server 2012 R2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Servidores Active Directory de Windows Server 2016</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nivel funcional del bosque</th>
<th>Exchange 2016 CU3 y versiones posteriores</th>
<th>Exchange 2016 CU2 y versiones anteriores</th>
<th>Exchange 2013 SP1 y posterior</th>
<th>Paquete acumulativo de actualizaciones 5 para Exchange 2010 SP3 o posterior</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nivel funcional del bosque de Windows Server 2003</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Nivel funcional del bosque de Windows Server 2008</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Nivel funcional del bosque de Windows Server 2008 R2 SP1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Nivel funcional del bosque de Windows Server 2012</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Nivel funcional del bosque de Windows Server 2012 R2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Nivel funcional del bosque de Windows Server 2016</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Exploradores web compatibles con la versión Premium de Outlook Web App u Outlook en la web

En la tabla siguiente se identifican los exploradores web compatibles con la versión Premium de Outlook Web App u Outlook en el web. Los exploradores compatibles se identifican con una X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Explorador</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 y posterior</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Versión actual de Microsoft Edge</p></td>
<td><p>N/D </p></td>
<td><p>N/D </p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Versión actual o inmediatamente anterior de Internet Explorer</p></td>
<td><p>N/D </p></td>
<td><p>N/D </p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox</p></td>
<td><p>Versión actual o inmediatamente anterior de Firefox</p></td>
<td><p>N/D </p></td>
<td><p>N/D </p></td>
</tr>
<tr class="odd">
<td><p>Firefox 3.0.1 o posterior</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox 12 o posterior</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari</p></td>
<td><p>Versión actual de Safari</p></td>
<td><p>N/D </p></td>
<td><p>N/D </p></td>
</tr>
<tr class="even">
<td><p>Safari 3.1 o posterior</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari 5.0 o posterior</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Versión actual de Chrome</p></td>
<td><p>N/D </p></td>
<td><p>N/D </p></td>
</tr>
<tr class="odd">
<td><p>Chrome 3.0.195 o posterior</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome 18 o posterior</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Exploradores web compatibles con la versión básica de Outlook Web App u Outlook en la web

En la tabla siguiente se identifican los exploradores web compatibles con la versión ligera (básica) de Outlook Web App u Outlook en el web. Los exploradores compatibles se identifican con una X.


> [!NOTE]
> Outlook Web App Basic (Outlook Web App Light) se admite en los exploradores móviles. Sin embargo, si se producen problemas de procesamiento o autenticación en un explorador móvil, determine si el problema puede reproducirse al usar Outlook Web App Light en el cliente completo de un explorador admitido. Por ejemplo, pruebe el uso de Outlook Web App Light en Safari, Chrome o Internet Explorer. Si el problema no puede reproducirse en el cliente completo, le recomendamos que se ponga en contacto con el proveedor de dispositivos móviles para obtener ayuda. En estos casos, colaboramos con el proveedor según corresponda.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Explorador</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Versión actual de Microsoft Edge</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Versión actual o inmediatamente anterior de Internet Explorer</p></td>
<td><p>N/D </p></td>
<td><p>N/D </p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X<span></span></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Safari</p></td>
<td><p>Versión actual de Safari</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Firefox</p></td>
<td><p>Versión actual o inmediatamente anterior de Firefox</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Versión actual de Chrome</p></td>
<td><p>N/D </p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Opera</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Exploradores web compatibles para usar S/MIME con Outlook Web App u Outlook en la web

En la tabla siguiente se identifican los exploradores web compatibles para usar S/MIME con Outlook Web App u Outlook en el web. Los exploradores compatibles se identifican con una X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Explorador</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 y posterior</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Versión actual de Microsoft Edge</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Versión actual o inmediatamente anterior de Internet Explorer</p></td>
<td><p>N/D </p></td>
<td><p>N/D </p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Clientes

En la tabla siguiente se identifican los clientes de buzón de correo compatibles con cada versión de Exchange. Los clientes compatibles se identifican con una X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Cliente</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 y posterior</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>X4</p></td>
<td><p>X2</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2016</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook Mac para Office 365</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 7.5</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 8</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 8.1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Mobile 10</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Entourage 2008 (EWS)</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
</tr>
</tbody>
</table>


1Requiere Outlook 2007 Service Pack 3 y la última actualización pública.

2Requiere Outlook 2010 Service Pack 1 y la última actualización pública.

3Solo EWS. No hay compatibilidad con DAV para Exchange 2010.

4Compatible con las actualizaciones públicas y el Service Pack de Office más recientes.

## Herramientas

En la siguiente tabla se identifica la versión de Microsoft Exchange que puede utilizarse con la herramienta de replicación entre organizaciones de Microsoft Exchange (Exscfg.exe; Exssrv.exe). Esta herramienta se utiliza para replicar la información de las carpetas públicas (incluida la información de disponibilidad) entre organizaciones Exchange. Para obtener más información, vea [Replicación entre organizaciones de Microsoft Exchange Server](https://go.microsoft.com/fwlink/?linkid=22455). Las versiones compatibles se identifican mediante una X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Herramienta</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 y posterior</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Herramienta de replicación entre organizaciones</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Microsoft .NET Framework

En la tabla siguiente se identifica la versión de Microsoft.NET Framework que se puede utilizar con cada versión de Exchange. Las versiones compatibles se identifican mediante una X.


> [!IMPORTANT]
> <STRONG>Las versiones de .NET Framework que no figuren en la siguiente tabla no son compatibles con ninguna versión de Exchange.</STRONG> Esto incluye las versiones menores y de nivel de revisión de .NET Framework.




> [!NOTE]
> Al actualizar Exchange desde una CU incompatible hasta la CU actual y sin ninguna CU intermedia disponible, se debe actualizar a la última versión de .NET que sea compatible con Exchange, en primer lugar, y luego actualizar inmediatamente a la CU actual. Este método no reemplaza la necesidad de mantener los servidores de Exchange actualizados y con la CU compatible más reciente.<BR>Microsoft no garantiza que con este método no se produzca un error de actualización, por lo que es posible que tenga que ponerse en contacto con el servicio de soporte técnico de Microsoft.




<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>.NET Framework</th>
<th>Exchange 2016 CU8</th>
<th>Exchange 2016 CU5 - CU7</th>
<th>Exchange 2013 CU19</th>
<th>Exchange 2013 CU16 - CU18</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>.NET Framework 3.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 3.5 SP1</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1,2</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.5</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X1,2 </p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.6.2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.7.1</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


1 Si está usando Windows Server 2012, el .NET Framework 3.5 debe estar instalado antes de usar Exchange 2010 SP3.

2Exchange 2010 solo usa las bibliotecas .NET .NET Framework 3.5 y .NET .NET Framework 3.5 SP1. No usa las bibliotecas .NET .NET Framework 4.5 si están instaladas en el equipo. Se admite la instalación de una versión principal o secundaria de .NET .NET Framework 4.5 (por ejemplo, .NET .NET Framework 4.5.1, .NET .NET Framework 4.5.2, etc.) siempre y cuando .NET .NET Framework 3.5 o .NET .NET Framework 3.5 SP1 también estén instaladas en el equipo.

## Windows Management Framework

En la siguiente tabla se identifica la versión de Windows Management Framework, que contiene la interfaz de línea de comandos de Windows PowerShell, que se puede usar con todas las versiones de Exchange. Las versiones compatibles se identifican mediante una X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows PowerShell</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows PowerShell 2.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Management Framework</p></td>
<td><p>Versión de Windows Management Framework integrado en la versión de Windows Server en la que está instalando Exchange.</p></td>
<td><p>Versión de Windows Management Framework integrado en la versión de Windows Server en la que está instalando Exchange.</p></td>
<td><p>Versión de Windows Management Framework integrado en la versión de Windows Server en la que está instalando Exchange.1</p></td>
</tr>
</tbody>
</table>


1Windows Management Framework 3.0 y Windows Management Framework 4.0 se pueden usar para realizar tareas de administración relacionadas con el sistema operativo en un equipo que ejecute Exchange 2010 SP3 RU5 o posterior. Sin embargo, los cmdlets de Exchange 2010 y los scripts de Exchange 2010 requieren Windows PowerShell 2.0. No se admite el uso de cmdlets y scripts de Exchange 2010 con Windows Management Framework 3.0 o Windows Management Framework 4.0.

## Microsoft Management Console

En la tabla siguiente se identifica la versión de Microsoft Management Console (MMC) que se puede utilizar con cada versión de Exchange. Las versiones compatibles se identifican mediante una X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>MMC</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 o versiones posteriores</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MMC 3.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Windows Installer

En la tabla siguiente se identifica la versión de Windows que se usa con cada versión de Exchange. Las versiones compatibles se identifican mediante una X.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows Installer</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 y posterior</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Installer 4.5</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Installer 5.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

