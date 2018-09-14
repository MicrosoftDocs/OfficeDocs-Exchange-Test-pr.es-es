---
title: 'Aplicaciones para Outlook: Exchange 2013 Help'
TOCTitle: Aplicaciones para Outlook
ms:assetid: 28b6f2a1-a235-4023-b561-6fd304962775
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ943753(v=EXCHG.150)
ms:contentKeyID: 52062019
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aplicaciones para Outlook

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2017-03-13_

**Resumen:**  una visión general de complementos para Outlook, que funcione con Outlook en los equipos Windows y MacIntosh, en dispositivos móviles y en Outlook Web App y Outlook en el web.

Complementos para Outlook son aplicaciones que amplían las posibilidades de los clientes de Outlook agregando información o herramientas que pueden utilizar los usuarios sin tener que salir de Outlook. Complementos son construidos por programadores de otros fabricantes y pueden instalarse desde un archivo o una dirección URL o desde el almacén de la oficina. De forma predeterminada, todos los usuarios pueden instalar complementos los administradores de Exchange pueden utilizar funciones para controlar la capacidad del usuario para instalar complementos.


> [!TIP]
> Para obtener información sobre los complementos de Outlook desde la perspectiva del usuario final, consulte el tema de la Ayuda <A href="https://go.microsoft.com/fwlink/p/?linkid=282387">los complementos instalados</A> en Office.com. Este tema proporciona una visión general de los complementos y también muestra algunos de los complementos de Outlook que se instalan de forma predeterminada.



## Complementos de almacén de Office y complementos personalizados

Los clientes de Outlook es compatible con una gran variedad de complementos que están disponibles a través del almacén de Office. Outlook también admite complementos personalizados que puede crear y distribuir a los usuarios de su organización.


> [!NOTE]
> El acceso a la Tienda Office no se admite para buzones y organizaciones de ciertas regiones. Si no puede ver la opción <STRONG>Agregar desde la Tienda Office</STRONG> en el <STRONG>Centro de administración de Exchange</STRONG>, que encontrará en <STRONG>Organización</STRONG> &gt; <STRONG>Complementos</STRONG> &gt; <IMG title="Agregar icono" alt="Agregar icono" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">, es posible que no pueda instalar un complemento de Outlook desde una URL o una ubicación de archivo. Para obtener más información, póngase en contacto con su proveedor de servicios.




> [!NOTE]
> Algunos complementos para Outlook se instalan de forma predeterminada. Sólo activan complementos predeterminado para Outlook en el contenido del idioma inglés. Por ejemplo, alemán direcciones postales en el cuerpo del mensaje no activan el complemento de Bing Maps.



## Instalación y complemento de access

De forma predeterminada, todos los usuarios pueden instalar y quitar complementos los administradores de Exchange tienen un número de controles disponibles para la administración de complementos y el acceso de los usuarios a ellos. Los administradores pueden impedir que los usuarios instalar complementos no se descargan desde el almacén de Office (en lugar de ello son "lado cargado" de un archivo o dirección URL). Los administradores también pueden deshabilitar a los usuarios de instalar complementos de almacén de Office y de instalar complementos en nombre de otros usuarios. También es posible asignar a usuarios a una función que les permite instalar complementos para su organización o para un subconjunto de usuarios de la organización.

Para impedir que los usuarios de instalar un complemento que no está en el almacén de Office, quitar la función de **Mis aplicaciones personalizadas** de ellos. Para impedir que los usuarios instalar complementos de almacén de Office, quitar la función de **Mis aplicaciones de mercado** de los mismos. Para obtener más detalles, consulte [Especifique los administradores y los usuarios que pueden instalar y administrar complementos para Outlook](https://docs.microsoft.com/es-es/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/specify-who-can-install-and-manage-add-ins).

Para instalar complementos para algunos o todos los usuarios de su organización, consulte [Instalación o eliminación de aplicaciones para Outlook en la organización](https://docs.microsoft.com/es-es/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/install-or-remove-outlook-add-ins).

Si es necesario, puede limitar la disponibilidad de un complemento a usuarios específicos de su organización. Para obtener más información, consulte [Administrar el acceso del usuario a aplicaciones para Outlook](manage-user-access-to-add-ins-for-outlook-exchange-online-help.md).

## Tareas administrativas comunes con complementos para Outlook

Hay un par de escenarios comunes que los administradores de Exchange administren en sus organizaciones.

**Si desea impedir que los usuarios finales instalar complementos para Outlook en todos los clientes de Outlook, realice los siguientes cambios a las funciones en el centro de administración de Exchange**:

  - Para impedir que los usuarios instalar complementos de almacén de Office, quitar la función de **Mi catálogo de soluciones** de ellos.

  - Para impedir que los usuarios cargar complementos desde orígenes que no sean el almacén Office, quitar la función de **Mis aplicaciones personalizadas** de ellos.

  - Para impedir que los usuarios instalen todos los complementos, quite dos de las funciones anteriores de ellos.

Consulte [Especifique los administradores y los usuarios que pueden instalar y administrar complementos para Outlook](https://docs.microsoft.com/es-es/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/specify-who-can-install-and-manage-add-ins) para obtener más información.

**Si los usuarios finales tienen actualmente acceso a complementos y desea quitar ese acceso, use el cmdlet `Get-App` para ver qué complementos cada usuario ha instalado.**

A continuación, utilice el cmdlet `Remove-App` para quitar los complementos de uno o más usuarios.

Para obtener más información, consulte [Get-App](https://technet.microsoft.com/es-es/library/jj218673\(v=exchg.150\)) y [Remove-App](https://technet.microsoft.com/es-es/library/jj218709\(v=exchg.150\)) para Exchange de 2013. Para Exchange Online o 2016 de Exchange, vaya [aquí](https://go.microsoft.com/fwlink/p/?linkid=844721).

## Permitir que los administradores y usuarios instalar complementos

Puede especificar que los administradores de la organización tienen permiso para instalar y administrar complementos para Outlook. También puede especificar qué usuarios de la organización tienen permiso para instalar y administrar complementos para su propio uso. Para obtener más información, consulte [Especifique los administradores y los usuarios que pueden instalar y administrar complementos para Outlook](https://docs.microsoft.com/es-es/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/specify-who-can-install-and-manage-add-ins).

