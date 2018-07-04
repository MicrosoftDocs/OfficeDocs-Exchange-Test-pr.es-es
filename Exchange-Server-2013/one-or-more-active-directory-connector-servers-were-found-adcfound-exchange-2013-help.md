---
title: 'Se han encontrado uno o varios servidores Conector de Active Directory_ADCFound: Exchange 2013 Help'
TOCTitle: Se han encontrado uno o varios servidores Conector de Active Directory_ADCFound
ms:assetid: a874f51f-09a2-4a76-9695-d61fb1ee6c1c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.adcfound(v=EXCHG.150)
ms:contentKeyID: 48268529
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Se han encontrado uno o varios servidores Conector de Active Directory\_ADCFound

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-15_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2007 y Exchange Server 2010 Setup no puede continuar porque se han encontrado uno o varios Conectores de Active Directory (ADC) en el entorno actual de Microsoft Exchange.

ADC replica los objetos de la versión 5.5 de Exchange Server al servicio de directorio de Active Directory® en un entorno de modo mixto de Microsoft Exchange y no se admite en Exchange 2007 o Exchange 2010.

La instalación de Exchange 2007 o Exchange 2010 requiere que se eliminen todos los componentes ADC.

Para resolver este problema, elimine todos los componentes ADC, y vuelva a ejecutar la instalación de Exchange 2007 o Exchange 2010.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Para eliminar los componentes del Conector de Active Directory</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Para deshabilitar el servicio ADC en el servidor donde se ejecuta el servicio ADC, haga clic con el botón secundario en <strong>Mi PC</strong> en el escritorio y, a continuación, haga clic en <strong>Administrar</strong>.</p></li>
<li><p>Expanda el nodo <strong>Servicios y aplicaciones</strong> y, a continuación, haga clic en el nodo <strong>Servicios</strong>.</p></li>
<li><p>En el panel derecho, haga clic con el botón secundario en <strong>Conector de Microsoft Active Directory</strong> y haga clic en <strong>Propiedades</strong>.</p></li>
<li><p>Cambie el <strong>Tipo de inicio</strong> a <strong>Deshabilitado</strong>. La próxima vez que se inicie el equipo, no se iniciará el servicio ADC.</p></li>
<li><p>Haga clic en <strong>Aplicar</strong> y, después, en <strong>Aceptar</strong>.</p></li>
<li><p>Para desinstalar el servicio ADC, use el Asistente de instalación de Active Directory del servidor de Microsoft Exchange 2000 o el CD de Microsoft Exchange Server 2003. Abra la carpeta \ADC\I386 y haga doble clic en el programa Setup.exe. Siga las instrucciones para <strong>Eliminar todos</strong> los componentes de servicio ADC.</p>

> [!IMPORTANT]
> Debe completar el paso 6 y <STRONG>Eliminar todos</STRONG> los componentes ADC para resolver este problema. No es suficiente con deshabilitar el servicio ADC.


</li>
</ol></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de ADC, consulte los artículos siguientes de Microsoft Knowledge Base:

  - 325300, "presentación técnica de soporte: Introducción para el conector de Active Directory" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325300](https://go.microsoft.com/fwlink/?linkid=3052&kbid=325300)).

  - 325221, "presentación técnica de soporte: Microsoft Advanced Active Directory Connector" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325221](https://go.microsoft.com/fwlink/?linkid=3052&kbid=325221)).

  - 312632 "Cómo instalar y configurar el conector de Active Directory en Exchange 2000 Server" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=312632](https://go.microsoft.com/fwlink/?linkid=3052&kbid=312632)).

